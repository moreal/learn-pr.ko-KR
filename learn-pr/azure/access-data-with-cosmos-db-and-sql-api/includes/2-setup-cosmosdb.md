<span data-ttu-id="44b56-101">가장 먼저 해야 할 경우 빈 Azure Cosmos DB 데이터베이스 및 컬렉션을 사용 하 여 작업 만들기</span><span class="sxs-lookup"><span data-stu-id="44b56-101">The first thing we need to do is create an empty Azure Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="44b56-102">이 학습 경로에 있는 마지막 모듈에서 만든 것과 일치 하도록 하려고: 라는 데이터베이스 **"제품"** 컬렉션과 라는 **"Clothing"** 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-102">We want them to match the ones you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="44b56-103">다음 지침에 따라 화면 오른쪽의 Azure Cloud Shell을 사용하여 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-103">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

# <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="44b56-104">Azure CLI는 Azure Cosmos DB 계정 및 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="44b56-104">Create an Azure Cosmos DB account + database with the Azure CLI</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

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

1. <span data-ttu-id="44b56-105">공통의 가치를 매번 입력 하지 않아도 되므로 몇 가지 환경 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-105">Set a few environment variables so you don't have to type the common values each time.</span></span> <span data-ttu-id="44b56-106">예를 들어 Azure Cosmos DB 계정에 대 한 이름을 설정 하 여 시작 `export NAME="mycosmosdbaccount"`합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-106">Start by setting a name for the Azure Cosmos DB account, for example `export NAME="mycosmosdbaccount"`.</span></span> <span data-ttu-id="44b56-107">필드는 소문자, 숫자를 포함할 수 있습니다 및 '-' 문자 및 3 ~ 31 자 사이 여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-107">The field can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

2. <span data-ttu-id="44b56-108">기존 샌드박스 리소스 그룹을 사용 하는 리소스 그룹을 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-108">Set the resource group to use the existing Sandbox resource group.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<rgn>[Sandbox resource group name]</rgn>"
    ```

2. <span data-ttu-id="44b56-109">사용자에 게 가장 가까운 지역을 선택 하 고 같은 환경 변수를 설정 `export LOCATION="EastUS"`합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-109">Select the region closest to you, and set the environment variable, such as `export LOCATION="EastUS"`.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

2. <span data-ttu-id="44b56-110">데이터베이스 이름에 대 한 변수를 설정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-110">Set a variable for the database name.</span></span> <span data-ttu-id="44b56-111">마지막 모듈에서 만든 데이터베이스와 일치 하도록 "제품" 이름을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-111">Name it "Products" so it matches the database we created in the last module.</span></span>

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

3. <span data-ttu-id="44b56-112">다음으로 Azure Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-112">Next, create the Azure Cosmos DB account.</span></span> <span data-ttu-id="44b56-113">작업을 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-113">This will take a few minutes to complete.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

4. <span data-ttu-id="44b56-114">계정에서 `Products` 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-114">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

5. <span data-ttu-id="44b56-115">마지막으로 `Clothing` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44b56-115">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="44b56-116">이제가 있는 경우에 Azure Cosmos DB 계정, 데이터베이스 및 컬렉션에 일부 데이터를 추가 이동 하겠습니다!</span><span class="sxs-lookup"><span data-stu-id="44b56-116">Now that you have your Azure Cosmos DB account, database, and collection, let's go add some data!</span></span>