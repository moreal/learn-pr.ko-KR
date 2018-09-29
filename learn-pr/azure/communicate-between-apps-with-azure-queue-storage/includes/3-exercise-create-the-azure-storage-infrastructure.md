<span data-ttu-id="aa6ae-101">중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-101">You've discovered that spikes in traffic can overwhelm our middle-tier.</span></span> <span data-ttu-id="aa6ae-102">이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-102">To deal with this, you've decided to add a queue between the front-end and the middle tier in your article-upload application.</span></span>

<span data-ttu-id="aa6ae-103">큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-103">The first step in creating a queue is to create the Azure Storage Account that will store our data.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a><span data-ttu-id="aa6ae-104">Azure CLI를 사용하여 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="aa6ae-104">Create a Storage Account with the Azure CLI</span></span>

> [!TIP] 
> <span data-ttu-id="aa6ae-105">일반적으로 모든 연결된 리소스를 포함할 _리소스 그룹_을 만들어 새 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-105">Normally, you'd start a new project by creating a _resource group_ to hold all the associated resources.</span></span> <span data-ttu-id="aa6ae-106">이 경우에 <rgn>[샌드박스 리소스 그룹 이름]</rgn>이라는 리소스 그룹을 제공하는 Azure 샌드박스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-106">In this case, we'll be using the Azure sandbox which provides a resource group named <rgn>[sandbox resource group name]</rgn>.</span></span>

<span data-ttu-id="aa6ae-107">`az storage account create` 명령을 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-107">Use the `az storage account create` command to create the storage account.</span></span> <span data-ttu-id="aa6ae-108">오른쪽의 Cloud Shell 창에 명령을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-108">You can type the command into the Cloud Shell window on the right.</span></span>

<span data-ttu-id="aa6ae-109">명령에는 몇 가지 매개 변수가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-109">The command needs several parameters:</span></span>

| <span data-ttu-id="aa6ae-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="aa6ae-110">Parameter</span></span> | <span data-ttu-id="aa6ae-111">값</span><span class="sxs-lookup"><span data-stu-id="aa6ae-111">Value</span></span> |
|-----------|-------|
| `--name`  | <span data-ttu-id="aa6ae-112">이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-112">Sets the name.</span></span> <span data-ttu-id="aa6ae-113">저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-113">Remember that storage accounts use the name to generate a public URL - so it has to be unique.</span></span> <span data-ttu-id="aa6ae-114">또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-114">In addition, the account name must be between 3 and 24 characters, and be composed of numbers and lowercase letters only.</span></span> <span data-ttu-id="aa6ae-115">무작위 숫자 접미사가 포함된 접두사 **articles**를 사용하는 것이 좋지만 어떤 접두사도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-115">We recommend you use the prefix **articles** with a random number suffix but you can use whatever you like.</span></span> |
| `-g`        | <span data-ttu-id="aa6ae-116">**리소스 그룹**을 제공하고, 값으로 _<rgn>[샌드박스 리소스 그룹 이름]</rgn>_ 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-116">Supplies the **Resource Group**, use _<rgn>[sandbox resource group name]</rgn>_ as the value.</span></span> |
| `--kind`    | <span data-ttu-id="aa6ae-117">**저장소 계정 형식**을 설정합니다. _StorageV2_를 사용하여 범용 V2 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-117">Sets the **Storage Account type** - use _StorageV2_ to create a general-purpose V2 account.</span></span> |
| `--sku`     | <span data-ttu-id="aa6ae-118">**복제 및 저장소 형식**을 설정합니다. _Standard_RAGRS_를 기본값으로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-118">Sets the **Replication and Storage type**, it defaults to _Standard_RAGRS_.</span></span> <span data-ttu-id="aa6ae-119">_Standard_LRS_를 사용하겠습니다. 즉, 데이터 센터 내에서 로컬로만 중복됩니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-119">Let's use _Standard_LRS_ which means it's only locally redundant within the data center.</span></span> |
| `-l`        | <span data-ttu-id="aa6ae-120">리소스 그룹 소유자와 관계없이 **위치**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-120">Sets the **Location** independent of the resource group owner.</span></span> <span data-ttu-id="aa6ae-121">위치는 선택적이지만 이를 사용하여 리소스 그룹과 다른 지역에 큐를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-121">It's optional, but you can use it to place the queue in a different region than the resource group.</span></span> <span data-ttu-id="aa6ae-122">샌드박스에서 사용 가능한 아래 지역 목록에서 선택하여 사용자와 가까운 위치에 큐를 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-122">Place it close to you, choosing from the below list of available regions in the sandbox.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="aa6ae-123">위의 매개 변수를 사용하는 예제 명령줄은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-123">Here's an example command line that uses the above parameters.</span></span> <span data-ttu-id="aa6ae-124">`--name` 매개 변수를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="aa6ae-124">Make sure to change the `--name` parameter.</span></span>

```azurecli
az storage account create --name [unique-name] -g <rgn>[sandbox resource group name]</rgn> --kind StorageV2 --sku Standard_LRS
```

<!-- Paste tip-->
[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]
