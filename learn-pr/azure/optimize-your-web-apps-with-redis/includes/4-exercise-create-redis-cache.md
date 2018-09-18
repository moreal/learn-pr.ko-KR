<span data-ttu-id="f0542-101">일반적으로 사용되는 값을 저장하고 반환하는 Azure Redis Cache 인스턴스를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-101">Let's create an Azure Redis Cache instance to store and return commonly used values.</span></span>

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a><span data-ttu-id="f0542-102">Azure에서 Redis 캐시 만들기</span><span class="sxs-lookup"><span data-stu-id="f0542-102">Create a Redis cache in Azure</span></span>

1. <span data-ttu-id="f0542-103">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-103">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="f0542-104">**리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-104">Click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="f0542-105">다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조 표시된 Azure Portal 데이터베이스 옵션을 보여주는 스크린샷.](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a><span data-ttu-id="f0542-107">캐시의 위치 식별</span><span class="sxs-lookup"><span data-stu-id="f0542-107">Identify the location for the cache</span></span>

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a><span data-ttu-id="f0542-108">캐시 구성</span><span class="sxs-lookup"><span data-stu-id="f0542-108">Configure your cache</span></span>

<span data-ttu-id="f0542-109">캐시에서 다음 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-109">Apply the following settings on the cache.</span></span>

1. <span data-ttu-id="f0542-110">**DNS 이름:** **ContosoSportsApp1028**처럼 전역적으로 고유한 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-110">**DNS Name:** Create a globally unique name such as **ContosoSportsApp1028**.</span></span>

1. <span data-ttu-id="f0542-111">**구독**: Azure 샌드박스 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-111">**Subscription:** Select the Azure Sandbox subscription.</span></span>

1. <span data-ttu-id="f0542-112">**리소스 그룹**: 리소스 그룹의 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-112">**Resource group:** Select <rgn>[Sandbox resource group name]</rgn> for the Resource Group.</span></span>

1. <span data-ttu-id="f0542-113">**위치:** 일반적으로 고객과 가까운 위치를 선택합니다. 이 예에서는 동부 해안입니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-113">**Location:** Normally, you would select a location near your customers - in this case, the East Coast.</span></span> <span data-ttu-id="f0542-114">그러나 위에서 언급했듯이 Azure 샌드박스는 특정 지역만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-114">However, the Azure Sandbox only allows specific regions to be selected for resources as noted above.</span></span> <span data-ttu-id="f0542-115">다음 위치 중 하나를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="f0542-115">Please select one of those locations.</span></span>

1. <span data-ttu-id="f0542-116">**가격 책정 계층:** **기본 C0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-116">**Pricing tier:** Select **Basic C0**.</span></span> <span data-ttu-id="f0542-117">사용할 수 있는 가장 낮은 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-117">This is the lowest tier you can use.</span></span> <span data-ttu-id="f0542-118">프로덕션 앱은 더 많은 데이터를 저장하기를 원하고 더 높은 계층이 필요한 클러스터링 같은 일부 프리미엄 기능을 활용하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-118">Production apps would likely want to store more data and utilize some of the Premium features such as clustering which would require a higher tier selection.</span></span>

1. <span data-ttu-id="f0542-119">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-119">Click **Create**.</span></span>

    <span data-ttu-id="f0542-120">다음 스크린샷은 새 Redis Cache 리소스를 만드는 데 사용되는 대표적인 구성을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-120">The following screenshot shows a representative configuration used to create a new Redis Cache resource.</span></span> <span data-ttu-id="f0542-121">Azure 샌드박스 때문에 여러분의 구성과 약간 다를 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-121">Note that yours will be slightly different due to the Azure Sandbox.</span></span>

    ![구성 DNS 이름, 구독, 새 리소스 그룹, 위치, 가격 책정 계층 예제로 채워진 새 Redis Cache 리소스를 만들 때 Azure Portal 블레이드의 모습을 보여주는 스크린샷.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> <span data-ttu-id="f0542-123">계속하기 전에 캐시가 배포될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-123">You will have to wait until the cache is deployed before continuing.</span></span> <span data-ttu-id="f0542-124">이 프로세스는 시간이 약간 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-124">This process might take some time.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="f0542-125">액세스 키 및 호스트 이름 검색</span><span class="sxs-lookup"><span data-stu-id="f0542-125">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="f0542-126">Azure Portal에서 새 캐시 인스턴스를 찾아서 **설정** > **액세스 키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-126">Navigate to your new cache instance in the Azure portal and select **Settings** > **Access keys**.</span></span> 

1. <span data-ttu-id="f0542-127">**기본 연결 문자열(StackExchange.Redis)** 을 안전한 장소에 복사합니다. 그 다음 연습에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-127">Copy the **Primary connection string (StackExchange.Redis)** to a safe place, you will need it for the next exercise.</span></span>

    <span data-ttu-id="f0542-128">이 키는 우리가 사용하려는 **StackExchange.Redis** 패키지의 응용 프로그램 설정 내에서 사용할 전체 연결 문자열의 기본 키와 호스트 이름을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-128">This key includes your primary key and host name in a complete connection string for use within your application settings for the **StackExchange.Redis** package we are going to use.</span></span>

<span data-ttu-id="f0542-129">다음으로, 캐시를 조사하는 데 사용할 수 있는 명령을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f0542-129">Next, let's learn about some of the commands we can use to interrogate the cache.</span></span>