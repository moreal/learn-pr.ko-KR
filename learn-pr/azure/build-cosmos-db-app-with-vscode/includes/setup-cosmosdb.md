> [!NOTE]
> 계속 진행 **확장을 작성 하는 Azure Cosmos DB 데이터베이스를 만들** 또는 **Azure Cosmos DB 데이터베이스의 데이터를 삽입 및 쿼리** 는 Azure Cosmos DB 계정이 이미 하 고이 건너뛸 수 있습니다 단위 및 이동 하려면 Visual Studio Code를 설정 합니다.

가장 먼저 해야 할 경우 Azure Cosmos DB 계정 만들기

# <a name="create-an-azure-cosmos-db-account"></a>Azure Cosmos DB 계정 만들기

1. 먼저 올바른 구독을 선택합니다. 무료 교육용 구독과 연결된 구독 ID를 선택해야 합니다.

    ```azurecli
    az account list --output table
    ```

1. 구독 목록에 “샌드박스”가 표시되는지 확인한 다음 해당 항목을 사용할 현재 구독으로 설정합니다. <!-- TODO: get official name here -->

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. 자동으로 작성된 리소스 그룹을 가져옵니다. 자체 구독을 사용 중인 경우 이 단계를 건너뛰고 아래의 `RESOURCE_GROUP` 환경 변수에서 사용하려는 고유한 이름만 입력하면 됩니다. 리소스 그룹 이름을 적어 둡니다. 이 그룹에 데이터베이스를 만들 것입니다. <!-- Do we get a token for this? -->

    ```azurecli
    az group list --out table
    ```

1. 이 작업을 좀 더 쉽게 수행하려면 매번 공통 값을 입력하지 않아도 되도록 환경 변수 몇 개를 설정합니다. 

    > [!IMPORTANT]
    > 이러한 값은 세션에 적합한 값으로 변경해야 합니다. 예를 들어 `<resource group>` 값은 위에 나와 있는 리소스 그룹 이름으로 바꿉니다.

    ```azurecli
    export RESOURCE_GROUP="<resource group>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```
      
1. 자체 구독에서 이 작업을 수행하며 _새_ 리소스 그룹을 사용하는 경우(권장)에는 다음 명령을 사용하여 리소스 그룹을 만듭니다. **중요:** Microsoft Learn에서 제공되는 무료 교육 리소스를 사용하는 경우에는 이 단계를 실행할 필요가 없습니다. 대신 위의 `RESOURCE_GROUP` 변수가 할당된 리소스 그룹으로 설정되어 있는지 확인합니다.

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
    
1. 다음으로는 Cosmos DB 계정을 만듭니다. 작업을 완료하는 데 몇 분 정도 걸립니다.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

이 Cosmos DB 계정을 만들었으므로 Visual Studio Code에서 작업을 시작할 수 있습니다.
