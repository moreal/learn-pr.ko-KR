컨테이너 인스턴스에서 환경 변수를 사용하면 컨테이너가 실행하는 응용 프로그램 또는 스크립트의 동적 구성을 제공할 수 있습니다. 컨테이너를 만들 때 Azure CLI, PowerShell 또는 Azure Portal을 사용하여 변수를 설정할 수 있습니다. 보안 환경 변수는 중요한 정보가 컨테이너 출력에 표시되지 않도록 방지하는 데 사용됩니다.

여기에서 Azure Cosmos DB 인스턴스를 만들고 환경 변수를 사용하여 연결 정보를 Azure Container Instance에 전달합니다. 컨테이너의 응용 프로그램은 해당 변수를 사용하여 Cosmos DB에서 데이터를 읽고 씁니다. 환경 변수와 보안 환경 변수 모두를 만듭니다.

## <a name="deploy-azure-cosmos-db"></a>Azure Cosmos DB 배포

`az cosmosdb create` 명령을 사용하여 Azure Cosmos DB 인스턴스를 만듭니다. 또한 이 예제에서는 *COSMOS_DB_ENDPOINT*라는 변수에 Azure Cosmos DB 엔드포인트 주소를 배치하기도 합니다. `[cosmos-db-name]`에 고유한 이름을 지정해야 합니다.

이 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.

```azurecli
COSMOS_DB_ENDPOINT=$(az cosmosdb create --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query documentEndpoint --output tsv)
```

그런 다음, `az cosmosdb list-keys` 명령을 사용하여 Azure Cosmos DB 연결 키를 가져온 후 *COSMOS_DB_MASTERKEY*라는 변수에 저장합니다. `[cosmos-db-name]`을 다시 바꾸는 것을 잊지 마세요.

```azurecli
COSMOS_DB_MASTERKEY=$(az cosmosdb list-keys --resource-group <rgn>[sandbox resource group name]</rgn> --name [cosmos-db-name] --query primaryMasterKey --output tsv)
```

## <a name="deploy-a-container-instance"></a>컨테이너 인스턴스 배포

`az container create` 명령을 사용하여 Azure 컨테이너 인스턴스를 만듭니다. 두 개의 환경 변수인 `COSMOS_DB_ENDPOINT` 및 `COSMOS_DB_MASTERKEY`가 만들어집니다. 이러한 변수는 Azure Cosmos DB 인스턴스에 연결하는 데 필요한 값을 포함합니다.

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --environment-variables COSMOS_DB_ENDPOINT=$COSMOS_DB_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_DB_MASTERKEY
```

컨테이너가 만들어지면 `az container show` 명령을 사용하여 IP 주소를 가져옵니다.

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo \
    --query ipAddress.ip \
    --output tsv
```

브라우저를 열고 컨테이너의 IP 주소로 이동합니다. 

> [!IMPORTANT]
> 컨테이너가 완전히 시작되고 연결을 수신할 수 있을 때까지 1~2분 정도 걸리는 경우가 있습니다. 브라우저에서 IP 주소로 이동할 때 응답이 없는 경우 몇 분 정도 기다렸다가 페이지를 새로 고칩니다.

 앱을 사용할 수 있게 되면 다음 응용 프로그램이 표시됩니다. 투표를 진행하면 해당 투표 내용이 Azure Cosmos DB 인스턴스에 저장됩니다.

![두 가지 선택 사항인 고양이와 강아지가 표시되는 Azure 투표 응용 프로그램입니다.](../media/4-azure-vote.png)

## <a name="secured-environment-variables"></a>보안 환경 변수

이전 연습에서는 두 개의 환경 변수에 저장된 Azure Cosmos DB에 대한 연결 정보를 사용하여 컨테이너가 만들어졌습니다. 기본적으로 환경 변수는 Azure Portal 및 명령줄 도구에 일반 텍스트로 표시됩니다.

예를 들어 `az container show` 명령을 사용하여 이전 연습에서 만든 컨테이너에 대한 정보를 가져오는 경우 해당 환경 변수에 일반 텍스트로 액세스할 수 있습니다.

```azurecli
az container show --resource-group <rgn>[sandbox resource group name]</rgn> --name aci-demo --query containers[0].environmentVariables
```

예제 출력:

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": "https://aci-cosmos.documents.azure.com:443/"
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": "Xm5BwdLlCllBvrR26V00000000S2uOusuglhzwkE7dOPMBQ3oA30n3rKd8PKA13700000000095ynys863Ghgw=="
  }
]
```

보안 환경 변수로 인해 명확한 텍스트 출력이 표시되지 않습니다. 보안 환경 변수를 사용하려면 `--environment-variables` 인수를 `--secure-environment-variables` 인수로 바꿉니다.

다음 예제를 실행하여 보안 환경 변수를 활용하는 *aci-demo-secure*라는 컨테이너를 만드세요.

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --image microsoft/azure-vote-front:cosmosdb \
    --ip-address Public \
    --location eastus \
    --secure-environment-variables COSMOS_DB_ENDPOINT=$COSMOS_ENDPOINT \
    COSMOS_DB_MASTERKEY=$COSMOS_KEY
```

이제 `az container show` 명령을 사용하여 컨테이너가 반환될 때 환경 변수가 표시되지 않습니다.

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name aci-demo-secure \
    --query containers[0].environmentVariables
```

예제 출력:

```json
[
  {
    "name": "COSMOS_DB_ENDPOINT",
    "secureValue": null,
    "value": null
  },
  {
    "name": "COSMOS_DB_MASTERKEY",
    "secureValue": null,
    "value": null
  }
]
```