<span data-ttu-id="6e588-101">중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-101">You've discovered that spikes in traffic can overwhelm our middle-tier.</span></span> <span data-ttu-id="6e588-102">이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-102">To deal with this, you've decided to add a queue between the front-end and the middle tier in your article-upload application.</span></span>

<span data-ttu-id="6e588-103">큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-103">The first step in creating a queue is to create the Azure Storage Account that will store our data.</span></span>

## <a name="create-a-storage-account-with-the-azure-cli"></a><span data-ttu-id="6e588-104">Azure CLI를 사용하여 저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="6e588-104">Create a Storage Account with the Azure CLI</span></span>

<span data-ttu-id="6e588-105">시작하기 위해 저장소 계정을 보유할 Azure 리소스 그룹을 만들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-105">To start with, let's create an Azure Resource Group to hold our storage account.</span></span>

1. <span data-ttu-id="6e588-106">오른쪽의 Cloud Shell에서 Bash 선택 옵션이 제공되면 Bash를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-106">In the Cloud shell on the right, select Bash if you are given a choice.</span></span>

1. <span data-ttu-id="6e588-107">`az group create` Azure CLI 명령을 사용하여 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-107">Use the `az group create` Azure CLI command to create a new resource group.</span></span> <span data-ttu-id="6e588-108">이름을 **ExerciseResources**로 지정하고 가까운 위치에 둡니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-108">Give it the name **ExerciseResources** and place it into a location near you.</span></span> 
    - <span data-ttu-id="6e588-109">아래 예제에서는 위치로 “eastus”를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-109">The example below uses "eastus" as the location.</span></span>

    ```azurecli
    az group create -n ExerciseResources --location eastus
    ```
        
1. <span data-ttu-id="6e588-110">다음으로 `az storage account create` 명령을 사용하여 실제 저장소 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-110">Next, use the `az storage account create` command to create the actual Storage Account.</span></span> <span data-ttu-id="6e588-111">다음과 같은 몇 가지 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-111">You'll need to supply several parameters:</span></span>

| <span data-ttu-id="6e588-112">매개 변수</span><span class="sxs-lookup"><span data-stu-id="6e588-112">Parameter</span></span> | <span data-ttu-id="6e588-113">값</span><span class="sxs-lookup"><span data-stu-id="6e588-113">Value</span></span> |
|-----------|-------|
| `--name`  | <span data-ttu-id="6e588-114">이름을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-114">Sets the name.</span></span> <span data-ttu-id="6e588-115">저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-115">Remember that storage accounts use the name to generate a public URL - so it has to be unique.</span></span> <span data-ttu-id="6e588-116">또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-116">In addition, the account name must be between 3 and 24 characters, and be composed of numbers and lowercase letters only.</span></span> <span data-ttu-id="6e588-117">접두사 **articles**와 무작위 숫자 접미사로 사용하는 것이 좋지만 어떤 접미사도 사용 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-117">We recommend you use the prefix **articles** with a random number suffix but you can use whatever you like.</span></span> |
| `-g`        | <span data-ttu-id="6e588-118">리소스 그룹을 제공하고 값으로 **ExerciseResources**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-118">Supplies the Resource Group, use **ExerciseResources** as the value.</span></span> |
| `--kind`    | <span data-ttu-id="6e588-119">저장소 계정 유형을 설정합니다. 범용 V2 계정을 생성하려면 **StorageV2**를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-119">Sets the Storage Account type - use **StorageV2** to create a general-purpose V2 account.</span></span> |
| `-l`        | <span data-ttu-id="6e588-120">리소스 그룹 소유자는 별도로 위치를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-120">Sets the location independent of the Resource Group owner.</span></span> <span data-ttu-id="6e588-121">선택적이지만 리소스 그룹과는 다른 지역에 큐를 배치하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-121">It's optional, but you can use it to place the queue in a different region than the Resource Group.</span></span> |
| `--sku`     | <span data-ttu-id="6e588-122">계정 유형을 설정합니다. 기본 유형은 **Standard_RAGRS**이지만, 이 데모에서는 불필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-122">Sets the account type, it defaults to **Standard_RAGRS**, which is overkill for this demonstration.</span></span> <span data-ttu-id="6e588-123">여기서는 데이터 센터 내에서 로컬로만 중복되는 것을 의미하는 **Standard_LRS**를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-123">Let's use **Standard_LRS** which means it's only locally redundant within the data center.</span></span> |

<span data-ttu-id="6e588-124">다음은 위의 매개 변수를 사용하는 예제 명령줄입니다.</span><span class="sxs-lookup"><span data-stu-id="6e588-124">Here's an example command line that uses the above parameters.</span></span> <span data-ttu-id="6e588-125">이 명령을 복사하여 붙여넣으려면 `--name` 매개 변수를 고유한 다른 값으로 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="6e588-125">Make sure to change the `--name` parameter to be something unique if you decide to copy/paste this command.</span></span>

```azurecli
az storage account create --name <name> -g ExerciseResources --kind StorageV2 -l eastus --sku Standard_LRS
```