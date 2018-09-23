<span data-ttu-id="db8bd-101">일단은 연습에서 사용할 빈 Azure Cosmos DB 데이터베이스와 컬렉션을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-101">The first thing we need to do is create an empty Azure Cosmos DB database and collection to work with.</span></span> <span data-ttu-id="db8bd-102">이 두 항목은 이 학습 경로의 마지막 모듈에서 만들었던 **"Products"** 데이터베이스 및 **"Clothing"** 컬렉션과 일치하도록 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-102">We want them to match the ones you created in the last module in this Learning Path: a database named **"Products"** and a collection named **"Clothing"**.</span></span> <span data-ttu-id="db8bd-103">다음 지침에 따라 화면 오른쪽의 Azure Cloud Shell을 사용하여 데이터베이스를 다시 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-103">Use the following instructions and the Azure Cloud Shell on the right side of the screen to recreate the database.</span></span>

## <a name="create-an-azure-cosmos-db-account--database-with-the-azure-cli"></a><span data-ttu-id="db8bd-104">Azure CLI를 사용하여 Azure Cosmos DB 계정 + 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="db8bd-104">Create an Azure Cosmos DB account + database with the Azure CLI</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="select-a-subscription"></a><span data-ttu-id="db8bd-105">구독 선택하기</span><span class="sxs-lookup"><span data-stu-id="db8bd-105">Select a subscription</span></span>

<span data-ttu-id="db8bd-106">한동안 Azure를 사용했다면 사용 가능한 여러 구독을 했을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-106">If you've been using Azure for a while, you might have multiple subscriptions available to you.</span></span> <span data-ttu-id="db8bd-107">Visual Studio 및 또다른 회사 리소스를 구독했을 개발자의 경우가 종종 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-107">This is often the case for developers who might have a subscription for Visual Studio, and another for corporate resources.</span></span>

<span data-ttu-id="db8bd-108">Azure 샌드박스가 Cloud Shell에서 컨시어스 구독을 이미 선택했으며, 이 단계를 사용하여 구독 설정을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-108">The Azure Sandbox has already selected the Concierge Subscription for you in the Cloud Shell, and you can validate the subscription setting using these steps.</span></span> <span data-ttu-id="db8bd-109">또는 사용자 고유 구독으로 작업하는 경우, 다음의 단계를 사용하면 Azure CLI를 사용하여 구독을 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-109">Or, when you are working with your own subscription, you can use the following steps to switch subscriptions with the Azure CLI.</span></span>

1. <span data-ttu-id="db8bd-110">사용 가능한 구독을 나열하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-110">Start by listing the available subscriptions.</span></span>

    ```azurecli
    az account list --output table
    ```

   <span data-ttu-id="db8bd-111">컨시어지 구독을 사용하는 경우, 그것이 유일한 목록이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-111">If you're working with a Concierge Subscription, it should be the only one listed.</span></span>

1. <span data-ttu-id="db8bd-112">사용하려는 기본 구독이 없으면 `account set` 명령으로 기본 구독을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-112">Next, if the default subscription isn't the one you want to use, you can change it with the `account set` command:</span></span>

    ```azurecli
    az account set --subscription "<subscription name>"
    ```
    
1. <span data-ttu-id="db8bd-113">샌드박스에서 만든 리소스 그룹을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-113">Get the Resource Group that has been created for you by the sandbox.</span></span> <span data-ttu-id="db8bd-114">자체 구독을 사용 중인 경우, 이 단계를 건너뛰고 아래의 `RESOURCE_GROUP` 환경 변수에서 사용하려는 고유 이름을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-114">If you are using your own subscription, skip this step and just supply a unique name you want to use in the `RESOURCE_GROUP` environment variable below.</span></span> <span data-ttu-id="db8bd-115">리소스 그룹 이름을 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-115">Take note of the Resource Group name.</span></span> <span data-ttu-id="db8bd-116">이것은 데이터베이스를 만들 장소입니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-116">This is where we will create our database.</span></span>

    ```azurecli
    az group list --out table
    ```
### <a name="setup-environment-variables"></a><span data-ttu-id="db8bd-117">환경 변수 설정하기</span><span class="sxs-lookup"><span data-stu-id="db8bd-117">Setup environment variables</span></span>

1. <span data-ttu-id="db8bd-118">매번 공통 값을 입력하지 않아도 되도록 환경 변수를 몇 개 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-118">Set a few environment variables so you don't have to type the common values each time.</span></span> <span data-ttu-id="db8bd-119">Azure Cosmos DB 계정의 이름을 설정하는 것부터 시작합니다(예: `export NAME="mycosmosdbaccount"`).</span><span class="sxs-lookup"><span data-stu-id="db8bd-119">Start by setting a name for the Azure Cosmos DB account, for example `export NAME="mycosmosdbaccount"`.</span></span> <span data-ttu-id="db8bd-120">필드는 소문자, 숫자 및 '-' 문자만 포함할 수 있으며, 3자에서 31자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-120">The field can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

    ```azurecli
    export NAME="<Azure Cosmos DB account name>"
    ```

1. <span data-ttu-id="db8bd-121">기존 샌드박스 리소스 그룹을 사용하도록 리소스 그룹을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-121">Set the resource group to use the existing Sandbox resource group.</span></span>

    ```azurecli
    export RESOURCE_GROUP="<rgn>[Sandbox resource group name]</rgn>"
    ```

1. <span data-ttu-id="db8bd-122">가장 가까운 지역을 선택하고 `export LOCATION="EastUS"`와 같은 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-122">Select the region closest to you, and set the environment variable, such as `export LOCATION="EastUS"`.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    export LOCATION="<location>"
    ```

1. <span data-ttu-id="db8bd-123">데이터베이스 이름에 대한 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-123">Set a variable for the database name.</span></span> <span data-ttu-id="db8bd-124">변수 이름을 “Products”로 지정하여 마지막 모듈에서 만든 데이터베이스와 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-124">Name it "Products" so it matches the database we created in the last module.</span></span>

    ```azurecli
    export DB_NAME="Products"
    ```

### <a name="create-a-resource-group-in-your-subscription"></a><span data-ttu-id="db8bd-125">구독에서 리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="db8bd-125">Create a resource group in your subscription</span></span>

<span data-ttu-id="db8bd-126">자체 구독에서 Cosmos DB를 만들 때 모든 관련 리소스를 포함할 새 리소스 그룹을 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-126">When you are creating a Cosmos DB on your own subscription you will want to create a new resource group to hold all the related resources.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="db8bd-127">Microsoft Learn에서 제공하는 Azure 샌드박스를 사용하는 경우에는 이 단계를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-127">If you are using the Azure Sandbox provided by Microsoft Learn, then you do not need to execute this step.</span></span> <span data-ttu-id="db8bd-128">대신, 위의 `RESOURCE_GROUP` 변수가 **<rgn>[샌드박스 리소스 그룹 이름</rgn>** 으로 설정되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-128">Instead, make sure the `RESOURCE_GROUP` variable above is set to **<rgn>[Sandbox Resource Group Name</rgn>**.</span></span>

<span data-ttu-id="db8bd-129">자체 구독에서 다음의 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-129">In your own subscription you would use the following command to create the Resource Group.</span></span> 

```azurecli
az group create --name <name> --location <location>
```

### <a name="create-the-azure-cosmos-db-account"></a><span data-ttu-id="db8bd-130">Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="db8bd-130">Create the Azure Cosmos DB account</span></span>

1. <span data-ttu-id="db8bd-131">`cosmosdb create` 명령을 사용하여 Azure Cosmos DB 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-131">Create the Azure Cosmos DB account with the `cosmosdb create` command.</span></span> <span data-ttu-id="db8bd-132">명령은 다음의 매개 변수를 사용하며, 권장 사항에 따라 환경 변수를 설정하는 경우 수정 없이 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-132">The command uses the following parameters and can be run with no modifications if you set the environment variables as recommended.</span></span>
    - <span data-ttu-id="db8bd-133">`--name`: 리소스의 고유 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-133">`--name`: Unique name for the resource.</span></span>
    - <span data-ttu-id="db8bd-134">`--kind`: 데이터베이스 종류, _GlobalDocumentDB_를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-134">`--kind`: Kind of database, use _GlobalDocumentDB_.</span></span>
    - <span data-ttu-id="db8bd-135">`--resource-group`: 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-135">`--resource-group`: The resource group.</span></span> <span data-ttu-id="db8bd-136">**<rgn>[샌드박스 리소스 그룹]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-136">Use **<rgn>[Sandbox Resource Group]</rgn>**.</span></span> <span data-ttu-id="db8bd-137">`RESOURCE_GROUP` 변수에 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-137">It should be assigned to the `RESOURCE_GROUP` variable.</span></span>

    ```azurecli
    az cosmosdb create --name $NAME --kind GlobalDocumentDB --resource-group $RESOURCE_GROUP
    ```

    <span data-ttu-id="db8bd-138">명령을 완료하려면 몇 분 정도 걸리며, cloud shell이 배포된 후 새 계정에 대한 설정을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-138">The command takes a few minutes to complete and the cloud shell displays the settings for the new account once it's deployed.</span></span>

1. <span data-ttu-id="db8bd-139">계정에서 `Products` 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-139">Create the `Products` database in the account.</span></span>

    ```azurecli
    az cosmosdb database create --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

1. <span data-ttu-id="db8bd-140">마지막으로 `Clothing` 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-140">Finally, create the `Clothing` collection.</span></span>

    ```azurecli
    az cosmosdb collection create --collection-name "Clothing" --partition-key-path "/productId" --throughput 1000 --name $NAME --db-name $DB_NAME --resource-group $RESOURCE_GROUP
    ```

<span data-ttu-id="db8bd-141">Azure Cosmos DB 계정, 데이터베이스 및 컬렉션이 준비되었으면 데이터를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="db8bd-141">Now that you have your Azure Cosmos DB account, database, and collection, let's go add some data!</span></span>