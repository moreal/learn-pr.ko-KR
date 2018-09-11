컨테이너 이미지는 Azure Container Instances, Azure Kubernetes 레지스트리, Windows 또는 Mac용 Docker 등 여러 컨테이너 관리 플랫폼의 Azure Container Registry에서 끌어올 수 있습니다. Azure Container Registry에서 컨테이너 이미지를 실행하는 경우 인증 자격 증명이 필요할 수 있습니다. Container Registry에서의 인증에는 Azure 서비스 주체를 사용하는 것이 좋습니다. 또한 Azure Key Vault에서 Azure 서비스 주체 자격 증명을 보호하는 것이 좋습니다.

이 단원에서는 Azure Container Registry용 서비스 주체를 만들고 Azure Key Vault에 저장한 후 서비스 주체의 자격 증명을 사용하여 Azure Container Instances에 컨테이너를 배포합니다.

## <a name="configure-registry-authentication"></a>레지스트리 인증 구성

모든 프로덕션 시나리오에서는 서비스 주체를 사용하여 Azure Container Registry에 액세스해야 합니다. 서비스 주체를 통해 컨테이너 이미지에 대해 RBAC(역할 기반 액세스 제어)를 제공할 수 있습니다. 예를 들어, 레지스트리에 대해 끌어오기 전용 액세스 권한을 가지는 서비스 주체를 구성할 수 있습니다.

Azure Key Vault에 자격 증명 모음이 아직 없는 경우 Azure CLI에서 다음 명령을 사용하여 만듭니다.

먼저 컨테이너 레지스트리 이름으로 변수를 만듭니다. 이 변수는 이 단원 전체에서 사용됩니다.

```azurecli
ACR_NAME=<acrName>
```

`az keyvault create` 명령을 사용하여 Azure Key Vault를 만듭니다.

```azurecli
az keyvault create --resource-group myResourceGroup --name $ACR_NAME-keyvault
```

이제 서비스 주체를 만들고 해당 자격 증명을 주요 자격 증명 모음에 저장해야 합니다.

`az ad sp create-for-rbac` 명령을 사용하여 서비스 주체를 만듭니다. `--role` 인수는 *읽기 권한자* 역할을 사용하여 서비스 주체를 구성하고, 레지스트리에 대해 끌어오기 전용 액세스 권한을 부여합니다. 밀어넣기 및 끌어오기 액세스 권한을 부여하려면 `--role` 인수를 *contributor*로 변경합니다.

```azurecli
az ad sp create-for-rbac --scopes $(az acr show --name $ACR_NAME --query id --output tsv) --role reader
```

서비스 주체 만들기 출력은 다음과 유사합니다. `appId` 및 `password` 값을 기록해 둡니다. 이러한 값은 Azure Key Vault에 저장됩니다.

```bash
{
  "appId": "1fa05179-0000-0000-0000-e269a4e97c41",
  "displayName": "azure-cli-2018-08-19-22-35-26",
  "name": "http://azure-cli-2018-08-19-22-35-26",
  "password": "72377509-0000-0000-0000-c8edbcb2d950",
  "tenant": "00000000-0000-0000-0000-000000000000"
}
```

그런 다음, `az keyvault secret set` 명령을 사용하여 서비스 주체의 *appId*를 자격 증명 모음에 저장합니다. `<appId>`를 서비스 주체의 `appId`로 바꿉니다.

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --value <appId>
```

이제 `az keyvault secret set` 명령을 사용하여 서비스 주체의 *암호*를 자격 증명 모음에 저장합니다. `<password>`를 서비스 주체의 `password`로 바꿉니다.

```azurecli
az keyvault secret set --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --value <password>
```

Azure Key Vault를 만들고 다음 두 비밀을 저장했습니다.

* `$ACR_NAME-pull-usr`: 서비스 주체 ID로, 컨테이너 레지스트리 **username**으로 사용됩니다.
* `$ACR_NAME-pull-pwd`: 서비스 주체 암호로, 컨테이너 레지스트리 **password**로 사용됩니다.

이제 사용자나 응용 프로그램 및 서비스가 레지스트리에서 이미지를 끌어올 때 이러한 비밀을 이름으로 참조할 수 있습니다.

### <a name="deploy-a-container-with-azure-cli"></a>Azure CLI를 사용하여 컨테이너 배포

서비스 주체 자격 증명은 Azure Key Vault에 저장되므로, 응용 프로그램 및 서비스는 해당 자격 증명을 사용하여 개인 레지스트리에 액세스할 수 있습니다.

다음 `az container create` 명령을 실행하여 컨테이너 인스턴스를 배포합니다. 이 명령은 Azure Key Vault에 저장된 서비스 주체의 자격 증명을 사용하여 컨테이너 레지스트리를 인증합니다.

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name acr-build \
    --image $ACR_NAME.azurecr.io/helloacrbuild:v1 \
    --registry-login-server $ACR_NAME.azurecr.io \
    --ip-address Public \
    --registry-username $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-usr --query value -o tsv) \
    --registry-password $(az keyvault secret show --vault-name $ACR_NAME-keyvault --name $ACR_NAME-pull-pwd --query value -o tsv)
```

Azure 컨테이너 인스턴스의 IP 주소를 가져옵니다.

```azurecli
az container show --resource-group myResourceGroup --name acr-build --query ipAddress.ip --output table
```

브라우저를 열고 컨테이너의 IP 주소로 이동합니다. 모든 항목이 올바르게 구성되면 다음 결과가 표시됩니다.

![Hello World 텍스트가 있는 샘플 웹 응용 프로그램](../media/hello.png)

## <a name="summary"></a>요약

이 단원에서는 Azure Container Registry 자격 증명이 Azure Key Vault에 저장되었습니다. 그런 다음, Azure CLI를 사용하여 Azure Container Instances에 컨테이너 이미지를 배포했습니다. 다음 단원에서는 Azure Container Registry 지역 복제를 사용하여 컨테이너 이미지를 여러 Azure 데이터 센터에 복사합니다.
