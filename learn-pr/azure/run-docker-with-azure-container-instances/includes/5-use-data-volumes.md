기본적으로 Azure Container Instances는 상태 비저장 방식입니다. 컨테이너의 작동이 중단되거나 중지되면 모든 상태가 손실됩니다. 컨테이너 수명이 지난 후에도 상태를 유지하려면 외부 저장소의 볼륨을 탑재해야 합니다.

여기에서는 데이터 저장 및 검색을 위해 Azure Container Instance에 Azure 파일 공유를 탑재합니다.

## <a name="create-an-azure-file-share"></a>Azure 파일 공유 만들기

다음 스크립트를 실행하여 저장소 계정을 만듭니다. 저장소 계정 이름은 글로벌로 고유해야 하므로 이 스크립트는 기준 문자열에 임의 값을 추가합니다.

```azurecli
ACI_PERS_STORAGE_ACCOUNT_NAME=mystorageaccount$RANDOM

az storage account create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --sku Standard_LRS \
    --location eastus
```

다음 명령을 실행하여 저장소 계정 연결 문자열을 *AZURE_STORAGE_CONNECTION_STRING*이라는 환경 변수에 배치합니다. 이 환경 변수는 Azure CLI에서 인식되며 저장소 관련 작업에 사용될 수 있습니다.

```azurecli
export AZURE_STORAGE_CONNECTION_STRING=$(az storage account show-connection-string --resource-group <rgn>[sandbox resource group name]</rgn> --name $ACI_PERS_STORAGE_ACCOUNT_NAME --output tsv)
```

`az storage share create` 명령을 실행하여 저장소 계정에 파일 공유를 만듭니다. 다음 예제에서는 *aci-share-demo*라는 공유를 만듭니다.

```azurecli
az storage share create --name aci-share-demo
```

## <a name="get-storage-credentials"></a>저장소 자격 증명 가져오기

Azure Container Instances의 볼륨으로 Azure 파일 공유를 탑재하려면 저장소 계정 이름, 공유 이름, 저장소 계정 액세스 키라는 세 가지 값이 필요합니다.

위의 스크립트를 사용한 경우 끝에 임의 값이 포함된 저장소 계정 이름이 생성되었습니다. 임의 값 부분을 포함한 최종 문자열을 쿼리하려면 다음 명령을 사용합니다.

```azurecli
STORAGE_ACCOUNT=$(az storage account list --resource-group <rgn>[sandbox resource group name]</rgn> --query "[?contains(name,'$ACI_PERS_STORAGE_ACCOUNT_NAME')].[name]" --output tsv)
echo $STORAGE_ACCOUNT
```

공유 이름은 이미 확인되었으므로(aci-share-demo) 저장소 계정 키만 확인하면 됩니다. 다음 명령을 사용하면 키를 확인할 수 있습니다.

```azurecli
STORAGE_KEY=$(az storage account keys list --resource-group <rgn>[sandbox resource group name]</rgn> --account-name $STORAGE_ACCOUNT --query "[0].value" --output tsv)
echo $STORAGE_KEY
```

## <a name="deploy-container-and-mount-volume"></a>컨테이너 배포 및 볼륨 탑재

Azure 파일 공유를 컨테이너의 볼륨으로 탑재하려면 컨테이너를 만들 때 공유 및 볼륨 탑재 지점을 지정합니다.

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --image microsoft/aci-hellofiles \
    --location eastus \
    --ports 80 \
    --ip-address Public \
    --azure-file-volume-account-name $ACI_PERS_STORAGE_ACCOUNT_NAME \
    --azure-file-volume-account-key $STORAGE_KEY \
    --azure-file-volume-share-name aci-share-demo \
    --azure-file-volume-mount-path /aci/logs/
```

컨테이너가 만들어지면 공용 IP 주소를 가져옵니다.

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-files \
    --query ipAddress.ip \
    --output tsv
```

브라우저를 열고 컨테이너 IP 주소로 이동합니다. 간단한 양식이 표시됩니다. 텍스트를 입력하고 **제출**을 클릭합니다. 이 작업을 수행하면 Azure Files 공유에 입력된 텍스트를 포함하는 파일이 생성됩니다.

![Azure Container Instances 파일 공유 데모](../media/5-files-ui.png)

유효성을 검사하려면 Azure Portal에서 파일 공유로 이동한 후 파일을 다운로드할 수 있습니다.

1. 파일 이름 확인

    ```azurecli
    az storage file list -s aci-share-demo -o table
    ```

1. 파일을 다운로드하고 아래에서 `<filename>`을 바꿉니다.

    ```azurecli
    az storage file download -s aci-share-demo -n <filename>
    ```
    
![콘텐츠 데모 응용 프로그램이 있는 샘플 텍스트 파일](../media/5-sample-text.png)

Azure Files 공유에 저장된 파일과 데이터가 임의의 값인 경우 상태 저장 데이터를 제공하기 위해 새 컨테이너 인스턴스에 이 공유를 다시 탑재할 수 있습니다.