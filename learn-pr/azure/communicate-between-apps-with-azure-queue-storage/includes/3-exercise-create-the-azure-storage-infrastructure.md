<span data-ttu-id="fe81a-101">중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-101">You've discovered that spikes in traffic can overwhelm our middle-tier.</span></span> <span data-ttu-id="fe81a-102">이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-102">To deal with this, you've decided to add a queue between the front-end and the middle tier in your article-upload application.</span></span>

<span data-ttu-id="fe81a-103">큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-103">The first step in creating a queue is to create the Azure Storage Account that will store our data.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a><span data-ttu-id="fe81a-104">Azure CLI를 사용하여 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="fe81a-104">Create a Storage Account with the Azure CLI</span></span>

> [!TIP] 
> <span data-ttu-id="fe81a-105">일반적으로 모든 연결된 리소스를 포함할 _리소스 그룹_을 만들어 새 프로젝트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-105">Normally, you'd start a new project by creating a _resource group_ to hold all the associated resources.</span></span> <span data-ttu-id="fe81a-106">이 경우 <rgn>[샌드박스 리소스 그룹 이름]</rgn>이라는 리소스 그룹을 제공하는 Azure 샌드박스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-106">In this case, we'll be using the Azure Sandbox which provides a resource group named <rgn>[Sandbox resource group name]</rgn>.</span></span>

1. <span data-ttu-id="fe81a-107">오른쪽의 Cloud Shell에서 Bash 선택 옵션이 제공되면 Bash를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-107">In the Cloud shell on the right, select Bash if you are given a choice.</span></span>

1. <span data-ttu-id="fe81a-108">`az storage account create` 명령을 사용하여 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-108">Use the `az storage account create` command to create the storage account.</span></span> <span data-ttu-id="fe81a-109">다음과 같은 몇 가지 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-109">You'll need to supply several parameters:</span></span>

| <span data-ttu-id="fe81a-110">매개 변수</span><span class="sxs-lookup"><span data-stu-id="fe81a-110">Parameter</span></span> | <span data-ttu-id="fe81a-111">값</span><span class="sxs-lookup"><span data-stu-id="fe81a-111">Value</span></span> |
|-----------|-------|
| `--name`  | <span data-ttu-id="fe81a-112">이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-112">Sets the name.</span></span> <span data-ttu-id="fe81a-113">저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-113">Remember that storage accounts use the name to generate a public URL - so it has to be unique.</span></span> <span data-ttu-id="fe81a-114">또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-114">In addition, the account name must be between 3 and 24 characters, and be composed of numbers and lowercase letters only.</span></span> <span data-ttu-id="fe81a-115">접두사 **articles**와 무작위 숫자 접미사로 사용하는 것이 좋지만 어떤 접미사도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-115">We recommend you use the prefix **articles** with a random number suffix but you can use whatever you like.</span></span> |
| `-g`        | <span data-ttu-id="fe81a-116">**리소스 그룹**을 제공하고 값으로 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-116">Supplies the **Resource Group**, use <rgn>[Sandbox resource group name]</rgn> as the value.</span></span> |
| `--kind`    | <span data-ttu-id="fe81a-117">**저장소 계정 유형**을 설정합니다. _StorageV2_를 사용하여 범용 V2 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-117">Sets the **Storage Account type** - use _StorageV2_ to create a general-purpose V2 account.</span></span> |
| `-l`        | <span data-ttu-id="fe81a-118">리소스 그룹 소유자와 관계없이 **위치**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-118">Sets the **Location** independent of the Resource Group owner.</span></span> <span data-ttu-id="fe81a-119">선택적이지만 리소스 그룹과는 다른 지역에 큐를 배치하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-119">It's optional, but you can use it to place the queue in a different region than the Resource Group.</span></span> |
| `--sku`     | <span data-ttu-id="fe81a-120">**복제 및 저장소 유형**을 설정합니다. 기본값인 _Standard_RAGRS_로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-120">Sets the **Replication and Storage type**, it defaults to _Standard_RAGRS_.</span></span> <span data-ttu-id="fe81a-121">여기서는 데이터 센터 내에서 로컬로만 중복되는 것을 의미하는 _Standard_LRS_를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-121">Let's use _Standard_LRS_ which means it's only locally redundant within the data center.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="fe81a-122">다음은 위의 매개 변수를 사용하는 예제 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-122">Here's an example command line that uses the above parameters.</span></span> <span data-ttu-id="fe81a-123">이 명령을 복사하여 붙여넣으려면 `--name` 및 `--location` 매개 변수를 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fe81a-123">Make sure to change the `--name` and `--location` parameters if you decide to copy/paste this command.</span></span>

```azurecli
az storage account create --name [unique-name] -g <rgn>[Sandbox resource group name]</rgn> --kind StorageV2 -l [location-name] --sku Standard_LRS
```