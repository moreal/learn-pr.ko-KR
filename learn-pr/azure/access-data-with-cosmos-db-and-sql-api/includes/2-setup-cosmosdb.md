일단은 연습에서 사용할 빈 Azure Cosmos DB 데이터베이스와 컬렉션을 만들어야 합니다. 이 두 항목은 이 학습 경로의 마지막 모듈에서 만들었던 **"Products"** 데이터베이스 및 **"Clothing"** 컬렉션과 일치하도록 만듭니다. 다음 지침에 따라 화면 오른쪽의 Azure Cloud Shell을 사용하여 데이터베이스를 다시 만듭니다.

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a>Azure CLI를 사용하여 Azure Cosmos DB 계정 + 데이터베이스 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a>구독 선택하기

한동안 Azure를 사용했다면 사용 가능한 여러 구독을 했을 수 있습니다. 이는 종종 Visual Studio용 구독 및 회사 리소스용 다른 구독을 보유한 개발자의 사례입니다.

Azure 샌드박스가 Cloud Shell에서 컨시어지 구독을 이미 선택했으므로, 이러한 단계를 사용하여 구독 설정을 확인할 수 있습니다. 또는 사용자 고유 구독으로 작업하는 경우 다음의 단계를 사용하여 Azure CLI를 통해 구독을 전환할 수 있습니다.

1. 사용 가능한 구독을 나열하여 시작합니다.

    ```azurecli
    az account list --output table
    ```

   컨시어지 구독을 사용하는 경우, 그것이 유일한 목록이어야 합니다.

1. 사용하려는 기본 구독이 없으면 `account set` 명령으로 기본 구독을 변경할 수 있습니다.

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. 샌드박스에서 만든 리소스 그룹을 가져옵니다. 자체 구독을 사용 중인 경우, 이 단계를 건너뛰고 아래의 `RESOURCE_GROUP` 환경 변수에서 사용하려는 고유 이름을 입력하면 됩니다. 리소스 그룹 이름을 적어 둡니다. 이것은 데이터베이스를 만들 장소입니다.

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a>환경 변수 설정하기

1. 매번 공통 값을 입력하지 않아도 되도록 환경 변수를 몇 개 설정합니다. Azure Cosmos DB 계정의 이름을 설정하는 것부터 시작합니다(예: `export NAME="mycosmosdbaccount"`). 필드는 소문자, 숫자 및 '-' 문자만 포함할 수 있으며, 3자에서 31자 사이여야 합니다.

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. 리소스 그룹을 설정하여 기존 샌드박스 리소스 그룹을 사용합니다.

    ```azurecli
    export RESOURCE_GROUP="<rgn>[sandbox resource group name]</rgn>"
    ```

1. 사용자와 가장 가까운 지역을 선택하고 `export LOCATION="EastUS"`와 같은 환경 변수를 설정합니다.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. 데이터베이스 이름에 대한 변수를 설정합니다. 변수 이름을 “Products”로 지정하여 마지막 모듈에서 만든 데이터베이스와 일치시킵니다.

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a>구독에서 리소스 그룹 만들기

자체 구독에서 Cosmos DB를 만들 때 모든 관련 리소스를 포함할 새 리소스 그룹을 만들려고 합니다.

> [!IMPORTANT]
> Microsoft Learn에서 제공하는 Azure 샌드박스를 사용하는 경우에는 이 단계를 실행할 필요가 없습니다. 대신, 위의 `RESOURCE_GROUP` 변수가 **<rgn>[샌드박스 리소스 그룹 이름</rgn>** 으로 설정되어 있는지 확인합니다.

자체 구독에서 다음의 명령을 사용하여 리소스 그룹을 만듭니다. 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a>Azure Cosmos DB 계정 만들기

1. `cosmosdb create` 명령을 사용하여 Azure Cosmos DB 계정을 만듭니다. 명령은 다음의 매개 변수를 사용하며, 권장 사항에 따라 환경 변수를 설정하는 경우 수정 없이 실행할 수 있습니다.
    - `--name`: 리소스의 고유 이름입니다.
    - `--kind`: 데이터베이스 종류, _GlobalDocumentDB_를 사용합니다.
    - `--resource-group`: 리소스 그룹입니다. **<rgn>[샌드박스 리소스 그룹]</rgn>** 을 사용합니다. `RESOURCE_GROUP` 변수에 할당되어야 합니다.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    명령을 완료하려면 몇 분 정도 걸리며, cloud shell이 배포된 후 새 계정에 대한 설정을 표시합니다.

1. 계정에서 `Products` 데이터베이스를 만듭니다.

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. 마지막으로 `Clothing` 컬렉션을 만듭니다.

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

Azure Cosmos DB 계정, 데이터베이스 및 컬렉션이 준비되었으면 데이터를 추가해 보겠습니다.