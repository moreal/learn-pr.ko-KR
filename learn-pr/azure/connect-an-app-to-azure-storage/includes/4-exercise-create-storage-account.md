<span data-ttu-id="57c85-101">이제 앱이 있으므로 작업할 Azure 저장소 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-101">Now that we have an app, we need an Azure storage account to work with.</span></span>

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a><span data-ttu-id="57c85-102">Azure CLI를 사용하여 Azure 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="57c85-102">Use the Azure CLI to create an Azure storage account</span></span>

<span data-ttu-id="57c85-103">`az storage account create` 명령을 사용하여 새 저장소 계정을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-103">We will use the `az storage account create` command to create a new storage account.</span></span> <span data-ttu-id="57c85-104">저장소 계정 구성을 제어하기 위한 여러 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-104">There are several parameters to control the configuration of the storage account.</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="57c85-105">옵션</span><span class="sxs-lookup"><span data-stu-id="57c85-105">Option</span></span> | <span data-ttu-id="57c85-106">설명</span><span class="sxs-lookup"><span data-stu-id="57c85-106">Description</span></span> |
> |--------|-------------|
> | `--name` | <span data-ttu-id="57c85-107">**저장소 계정 이름**입니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-107">A **Storage account name**.</span></span> <span data-ttu-id="57c85-108">이름은 계정의 데이터에 액세스하는 데 사용되는 공용 URL을 생성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-108">The name will be used to generate the public URL used to access the data in the account.</span></span> <span data-ttu-id="57c85-109">이름은 Azure의 모든 기존 저장소 계정 이름 중에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-109">It must be unique across all existing storage account names in Azure.</span></span> <span data-ttu-id="57c85-110">이름은 3~24자 사이여야 하며, 소문자와 숫자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-110">It must be 3 to 24 characters long and can contain only lowercase letters and numbers.</span></span> |
> | `--resource-group` | <span data-ttu-id="57c85-111">**<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용하여 저장소 계정을 무료 샌드박스에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-111">Use **<rgn>[sandbox resource group name]</rgn>** to place the storage account into the free sandbox.</span></span> |
> | `--location` | <span data-ttu-id="57c85-112">사용자에게 가까운 위치를 선택합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="57c85-112">Select a location near you (see below).</span></span> |
> | `--kind` | <span data-ttu-id="57c85-113">저장소 계정 _유형_을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-113">This determines the storage account _type_.</span></span> <span data-ttu-id="57c85-114">옵션에는 `BlobStorage`, `Storage` 및 `StorageV2`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-114">Options include `BlobStorage`, `Storage`, and `StorageV2`.</span></span> |
> | `--sku` | <span data-ttu-id="57c85-115">저장소 계정 성능 및 복제 모델을 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-115">This decides the storage account performance and replication model.</span></span> <span data-ttu-id="57c85-116">옵션에는 `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS` 및 `Standard_ZRS`가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-116">Options include `Premium_LRS`, `Standard_GRS`, `Standard_LRS`, `Standard_RAGRS`, and `Standard_ZRS`.</span></span> |
> | `--access-tier` | <span data-ttu-id="57c85-117">**액세스 계층**은 Blob Storage에만 사용되며, 사용 가능한 옵션으로 [`Cool` \| `Hot`]이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-117">The **Access tier** is only used for Blob storage, available options are [`Cool` \| `Hot`].</span></span> <span data-ttu-id="57c85-118">**핫 액세스 계층**은 자주 액세스하는 데이터에 적합하며, **쿨 액세스 계층**은 자주 액세스하지 않는 데이터에 더 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-118">The **Hot Access Tier** is ideal for frequently accessed data, and the **Cool Access Tier** is better for infrequently accessed data.</span></span> <span data-ttu-id="57c85-119">여기서는 _기본_ 값만 설정합니다. Blob을 만들 때 데이터에 대한 다른 값을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-119">Note that this only sets the _default_ value&mdash;when you create a Blob, you can set a different value for the data.</span></span> |
    
<span data-ttu-id="57c85-120">위의 표를 사용하여 오른쪽의 Cloud Shell에서 계정을 만드는 명령줄을 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-120">Use the above table to craft a command line in the Cloud Shell on the right to create the account.</span></span>
- <span data-ttu-id="57c85-121">고유한 이름을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-121">Use a unique name.</span></span> <span data-ttu-id="57c85-122">이니셜과 임의의 숫자로 된 “photostore”과 같은 이름을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-122">We recommend something like "photostore" with your initials and a random number.</span></span> <span data-ttu-id="57c85-123">고유하지 않으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-123">You will get an error if it's not unique.</span></span>
- <span data-ttu-id="57c85-124">일반적으로 앱 리소스를 보관할 새 리소스 그룹을 만들지만 이 경우에는 샌드박스 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-124">Normally you would create a new resource group to hold your app resources, but in this case, use the sandbox resource group "**<rgn>[sandbox resource group name]</rgn>**".</span></span>
- <span data-ttu-id="57c85-125">**sku**에 대해 “Standard_LRS”를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-125">Use "Standard_LRS" for the **sku**.</span></span> <span data-ttu-id="57c85-126">이 예에서는 로컬 복제가 있는 표준 저장소를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-126">This will use standard storage with local replication, which is fine for this example.</span></span>
- <span data-ttu-id="57c85-127">**액세스 계층**에 대해 “쿨”을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-127">Use "Cool" for the **Access Tier**.</span></span>

### <a name="selecting-a-location"></a><span data-ttu-id="57c85-128">위치 선택</span><span class="sxs-lookup"><span data-stu-id="57c85-128">Selecting a location</span></span>
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a><span data-ttu-id="57c85-129">명령 예제</span><span class="sxs-lookup"><span data-stu-id="57c85-129">Example command</span></span>

```azurecli
az storage account create \
        --name <name> \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \
        --access-tier Cool
```

> [!TIP]
> <span data-ttu-id="57c85-130">저장소 계정에 대한 옵션을 알아보려면 **Azure Storage 계정 만들기** 모듈로 이동하여 자세히 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="57c85-130">If you are interested in exploring the options for the storage account, make sure to go through the **Create an Azure storage account** module where we go through them in depth.</span></span>

<span data-ttu-id="57c85-131">계정을 배포하는 데는 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-131">It will take a few minutes to deploy the account.</span></span> <span data-ttu-id="57c85-132">Azure에서 이 작업을 수행하는 동안 이 계정에서 사용할 API를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="57c85-132">While Azure is working on that, let's explore the APIs we'll use with this account.</span></span>
