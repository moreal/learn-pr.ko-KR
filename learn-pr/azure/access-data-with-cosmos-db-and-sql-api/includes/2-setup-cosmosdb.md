> [!NOTE]
> <span data-ttu-id="0ab1e-101">**확장 가능하도록 작성되는 Azure Cosmos DB 데이터베이스 만들기**부터 연습을 계속 진행하는 경우 해당 과정에서 만든 Cosmos DB 데이터베이스 + 컬렉션을 삭제하지 않았다면 이 단원을 건너뛰고 데이터 탐색기를 사용하여 데이터를 추가하는 단원으로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-101">If you are continuing on from **Create an Azure Cosmos DB database built to scale** and you did not delete the Cosmos DB database + collection that you created, then you can skip this unit and move on to adding data with the Data Explorer.</span></span>

<span data-ttu-id="0ab1e-102">일단은 연습에서 사용할 빈 Cosmos DB 데이터베이스와 컬렉션을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-102">The first thing we need to do is create an empty Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="0ab1e-103">이 두 항목은 이 학습 경로의 마지막 모듈에서 만들었던 **"Products"** 데이터베이스 및 **"Clothing"** 컬렉션과 일치하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-103">We want it to match the one you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="0ab1e-104">다음 지침에 따라 화면 오른쪽의 Azure Cloud Shell을 사용하여 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-104">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

# <a name="create-a-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="0ab1e-105">Azure CLI를 사용하여 Cosmos DB 계정 + 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="0ab1e-105">Create a Cosmos DB account + database with the Azure CLI</span></span>

1. <span data-ttu-id="0ab1e-106">먼저 올바른 구독을 선택합니다. 무료 교육용 구독과 연결된 구독 ID를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-106">Start by selecting the correct subscription - you want to select the subscription ID associated with your free education access subscription.</span></span>

    ```azurecli
    az account list --output table
    ```

1. <span data-ttu-id="0ab1e-107">구독 목록에 “샌드박스”가 표시되는지 확인한 다음 해당 항목을 사용할 현재 구독으로 설정합니다. <!-- TODO: get official name here --></span><span class="sxs-lookup"><span data-stu-id="0ab1e-107">Make sure you see "sandbox" in the subscription list and set it as the current one to use: <!-- TODO: get official name here --></span></span>

    ```azurecli
    az account set --subscription "sandbox"
    ```
    
1. <span data-ttu-id="0ab1e-108">자동으로 작성된 리소스 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-108">Get the Resource Group that has been created for you.</span></span> <span data-ttu-id="0ab1e-109">자체 구독을 사용 중인 경우 이 단계를 건너뛰고 아래의 `RESOURCE_GROUP` 환경 변수에서 사용하려는 고유한 이름만 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-109">If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below.</span></span> <span data-ttu-id="0ab1e-110">리소스 그룹 이름을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-110">Take note of the Resource Group name.</span></span> <span data-ttu-id="0ab1e-111">이 그룹에 데이터베이스를 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-111">This is where we will create our database.</span></span> <!-- Do we get a token for this? -->

    ```azurecli
    az group list --out table
    ```

1. <span data-ttu-id="0ab1e-112">이 작업을 좀 더 쉽게 수행하려면 매번 공통 값을 입력하지 않아도 되도록 환경 변수 몇 개를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-112">To make this a bit easier, set a few environment variables so you don't have to type the common values each time.</span></span> 

    > [!IMPORTANT]
    > <span data-ttu-id="0ab1e-113">이러한 값은 세션에 적합한 값으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-113">Make sure to change these values to ones appropriate for your session.</span></span> <span data-ttu-id="0ab1e-114">예를 들어 `<resource group>` 값은 위에 나와 있는 리소스 그룹 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-114">For example, replace the `<resource group>` value with the Resource Group name you identified above.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<resource group>"
    export NAME="<cosmos db name>"
    export LOCATION="<location>"
    ```
    
1. <span data-ttu-id="0ab1e-115">다음으로는 데이터베이스 이름에 대한 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-115">Next, set a variable for the database name.</span></span> <span data-ttu-id="0ab1e-116">마지막 모듈에서 만든 데이터베이스와 일치하도록 변수 이름을 “Users”로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-116">Name it "Users" so it matches the database we created in the last module.</span></span>

    ```azurecli
    export DB_NAME="Products"
    ```
    
1. <span data-ttu-id="0ab1e-117">자체 구독에서 이 작업을 수행하며 _새_ 리소스 그룹을 사용하는 경우(권장)에는 다음 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-117">If you are doing this on your own subscription, and you are using a _new_ Resource Group (recommended), then use the following command to create the Resource Group.</span></span> <span data-ttu-id="0ab1e-118">**중요:** Microsoft Learn에서 제공되는 무료 교육 리소스를 사용하는 경우에는 이 단계를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-118">**Important:** If you are using the free education resources provided by Microsoft Learn, then you do not need to execute this step.</span></span> <span data-ttu-id="0ab1e-119">대신 위의 `RESOURCE_GROUP` 변수가 할당된 리소스 그룹으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-119">Instead, make sure the `RESOURCE_GROUP` variable above is set to your assigned resource group.</span></span>

    ```azurecli
    az group create --name $RESOURCE_GROUP --location $LOCATION
    ```
    
1. <span data-ttu-id="0ab1e-120">다음으로는 Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-120">Next, create the Cosmos DB account.</span></span> <span data-ttu-id="0ab1e-121">작업을 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-121">This will take a few minutes to complete.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```
    
1. <span data-ttu-id="0ab1e-122">계정에서 `Products` 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-122">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```
    
1. <span data-ttu-id="0ab1e-123">마지막으로 `Clothing` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-123">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="0ab1e-124">이제 Cosmos DB 계정, 데이터베이스 및 컬렉션이 준비되었으므로 데이터를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="0ab1e-124">Now that we have our Cosmos DB account, database, and collection, let's go add some data!</span></span>