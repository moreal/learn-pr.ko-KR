<span data-ttu-id="b4281-101">이제 앱이 있으므로 사용할 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-101">Now that we have an app, we need an Azure storage account to work with.</span></span> <span data-ttu-id="b4281-102">Azure Portal을 사용하여 **Azure 저장소 계정 만들기** 모듈에서 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-102">We created one using the Azure portal in the **Create an Azure storage account** module.</span></span> <span data-ttu-id="b4281-103">이번에는 Azure CLI를 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-103">Let's use the Azure CLI this time.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a><span data-ttu-id="b4281-104">Azure CLI를 사용하여 Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="b4281-104">Use the Azure CLI to create an Azure storage account</span></span>

<span data-ttu-id="b4281-105">`az storage account create` 명령을 사용하여 새 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-105">We will use the `az storage account create` command to create a new storage account.</span></span> <span data-ttu-id="b4281-106">원하는 방식으로 구성하는 데 필요한 몇 가지 매개 변수를 제공하거나 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-106">It takes several parameters which we either need to supply (or should) to configure it the way we want.</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="b4281-107">옵션</span><span class="sxs-lookup"><span data-stu-id="b4281-107">Option</span></span> | <span data-ttu-id="b4281-108">설명</span><span class="sxs-lookup"><span data-stu-id="b4281-108">Description</span></span> |
> |--------|-------------|
> | `--name` | <span data-ttu-id="b4281-109">**저장소 계정 이름**입니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-109">A **Storage account name**.</span></span> <span data-ttu-id="b4281-110">이름은 계정의 데이터에 액세스하는 데 사용되는 공용 URL을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-110">The name will be used to generate the public URL used to access the data in the account.</span></span> <span data-ttu-id="b4281-111">이름은 Azure의 모든 기존 저장소 계정 이름 중에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-111">It must be unique across all existing storage account names in Azure.</span></span> <span data-ttu-id="b4281-112">3-24자여야 하며, 소문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-112">It must be 3 to 24 characters long and can contain only lowercase letters and numbers.</span></span> |
> | `--resource-group` | <span data-ttu-id="b4281-113"><rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용하여 저장소 계정을 무료 샌드박스에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-113">Use <rgn>[Sandbox resource group name]</rgn> to place the storage account into the free sandbox.</span></span> |
> | `--location` | <span data-ttu-id="b4281-114">사용자에게 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-114">Select a location near you.</span></span> |
> | `--kind` | <span data-ttu-id="b4281-115">저장소 계정 _유형_을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-115">This determines the storage account _type_.</span></span> <span data-ttu-id="b4281-116">옵션으로 BlobStorage, Storage 및 StorageV2가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-116">Options include BlobStorage, Storage, and StorageV2.</span></span> |
> | `--sku` | <span data-ttu-id="b4281-117">저장소 계정 성능 및 복제 모델을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-117">This decides the storage account performance and replication model.</span></span> <span data-ttu-id="b4281-118">옵션으로 Premium_LRS, Standard_GRS, Standard_LRS, Standard_RAGRS 및 Standard_ZRS가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-118">Options include Premium_LRS, Standard_GRS, Standard_LRS, Standard_RAGRS, and Standard_ZRS.</span></span> |
> | `--access-tier` | <span data-ttu-id="b4281-119">**액세스 계층**은 Blob 저장소에만 사용되며, 사용 가능한 옵션으로 쿨 및 핫이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-119">The **Access tier** is only used for Blob storage, available options are Cool and Hot.</span></span> <span data-ttu-id="b4281-120">**핫 액세스 계층**은 자주 액세스하는 데이터에 적합하며, **쿨 액세스 계층**은 자주 액세스하지 않는 데이터에 더 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-120">The **Hot Access Tier** is ideal for frequently accessed data, and the **Cool Access Tier** is better for infrequently accessed data.</span></span> <span data-ttu-id="b4281-121">여기서는 _기본_ 값만 설정합니다. Blob을 만들 때 데이터에 대한 다른 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-121">Note that this only sets the _default_ value - when you create a Blob, you can set a different value for the data.</span></span> |
    
<span data-ttu-id="b4281-122">위의 표를 사용하여 오른쪽의 Cloud Shell에서 계정을 만드는 명령줄을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-122">Use the above table to craft a command line in the Cloud Shell on the right to create the account.</span></span>
- <span data-ttu-id="b4281-123">고유한 이름을 사용합니다. 이니셜과 임의의 숫자로 된 "photostore"와 같은 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-123">Use a unique name, we recommend something like "photostore" with your initials and a random number.</span></span> <span data-ttu-id="b4281-124">고유하지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-124">You will get an error if it's not unique.</span></span>
- <span data-ttu-id="b4281-125">샌드박스 리소스 그룹을 사용하는 경우 일반적으로 응용 프로그램 리소스를 보관할 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-125">Normally you would create a new resource group to hold your app resources, in this case use the Sandbox resource group.</span></span>
- <span data-ttu-id="b4281-126">**sku**에 대해 "Standard_LRS"를 사용합니다. 이 예에서는 로컬 복제가 있는 표준 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-126">Use "Standard_LRS" for the **sku**, this will use standard storage with local replication which is fine for this example.</span></span>
- <span data-ttu-id="b4281-127">**액세스 계층**에 대해 "콜드"를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-127">Use "Cold" for the **Access Tier**.</span></span>

### <a name="selecting-a-location"></a><span data-ttu-id="b4281-128">위치 선택</span><span class="sxs-lookup"><span data-stu-id="b4281-128">Selecting a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a><span data-ttu-id="b4281-129">명령 예제</span><span class="sxs-lookup"><span data-stu-id="b4281-129">Example command</span></span>

```bash
az storage account create \
        --name <name> \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \ 
        --access-tier Cold
```

> [!TIP]
> <span data-ttu-id="b4281-130">저장소 계정에 대한 옵션을 알아보려면 **Azure 저장소 계정 만들기**로 이동하여 자세히 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="b4281-130">If you are interested in exploring the options for the storage account, make sure to go through the **Create an Azure storage account** where we go through them in depth.</span></span>

<span data-ttu-id="b4281-131">계정을 배포하는 데는 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-131">It will take a few minutes to deploy the account.</span></span> <span data-ttu-id="b4281-132">Azure에서 이 작업을 수행하는 동안 이 계정에서 사용할 API를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b4281-132">While Azure is working on that, let's explore the APIs we'll use with this account.</span></span>