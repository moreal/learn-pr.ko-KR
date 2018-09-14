> [!NOTE]
> **확장 가능하도록 작성되는 Azure Cosmos DB 데이터베이스 만들기**부터 연습을 계속 진행하는 경우 해당 과정에서 만든 Cosmos DB 데이터베이스 + 컬렉션을 삭제하지 않았다면 이 단원을 건너뛰고 데이터 탐색기를 사용하여 데이터를 추가하는 단원으로 이동할 수 있습니다.

일단은 연습에서 사용할 빈 Cosmos DB 데이터베이스와 컬렉션을 만들어야 합니다. 이 두 항목은 이 학습 경로의 마지막 모듈에서 만들었던 **"Products"** 데이터베이스 및 **"Clothing"** 컬렉션과 일치하도록 만듭니다. 다음 지침에 따라 화면 오른쪽의 Azure Cloud Shell을 사용하여 데이터베이스를 다시 만듭니다.

# <a name="create-a-cosmos-db-account--database-with-the-azure-cli"></a>Azure CLI를 사용하여 Cosmos DB 계정 + 데이터베이스 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<!--
TODO: This is original text prior to updates to use the sandbox. These can be worked back in as instructions for people using their own subscriptions. There is one more block like this below. Note that the assignment of RESOURCE_GROUP below would need to be different as well.

1. Start by selecting the correct subscription - you want to select the subscription ID associated with your free education access subscription.

    ```azurecli
    az account list --output table
    ```

1. Make sure you see "sandbox" in the subscription list and set it as the current one to use:

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. Get the Resource Group that has been created for you. If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below. Take note of the Resource Group name. This is where we will create our database.

    ```azurecli
    az group list --out table
    ```
-->

1. 공통의 가치를 매번 입력 하지 않아도 되므로 몇 가지 환경 변수를 설정 합니다.

    > [!IMPORTANT]
    > 이러한 값은 세션에 적합한 값으로 변경해야 합니다. 예를 들어 대체 된 `<comsos db name>` 에 Cosmos DB에서 원하는 이름의 값입니다.

    ```azurecli
    export RESOURCE_GROUP="<rgn>[Sandbox resource group name]</rgn>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```

2. 다음으로는 데이터베이스 이름에 대한 변수를 설정합니다. 마지막 모듈에서 만든 데이터베이스와 일치하도록 변수 이름을 “Users”로 지정합니다.

    ```azurecli
    export DB_NAME="Products"
    ```

<!-- 

TODO: Pre-sandbox text to be worked back in.

1. If you are doing this on your own subscription, and you are using a _new_ Resource Group (recommended), then use the following command to create the Resource Group. **Important:** If you are using the free education resources provided by Microsoft Learn, then you do not need to execute this step. Instead, make sure the `RESOURCE_GROUP` variable above is set to your assigned resource group.

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
-->

3. 다음으로는 Cosmos DB 계정을 만듭니다. 작업을 완료하는 데 몇 분 정도 걸립니다.

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

4. 계정에서 `Products` 데이터베이스를 만듭니다.

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

5. 마지막으로 `Clothing` 컬렉션을 만듭니다.

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

이제 Cosmos DB 계정, 데이터베이스 및 컬렉션이 준비되었으므로 데이터를 추가해 보겠습니다.