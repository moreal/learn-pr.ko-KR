<span data-ttu-id="ee22c-101">일반적으로 사용되는 값을 저장하고 반환하는 Azure Redis Cache 인스턴스를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-101">Let's create an Azure Redis Cache instance to store and return commonly used values.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a><span data-ttu-id="ee22c-102">Azure에서 Redis Cache 만들기</span><span class="sxs-lookup"><span data-stu-id="ee22c-102">Create a Redis cache in Azure</span></span>

1. <span data-ttu-id="ee22c-103">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-103">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="ee22c-104">**리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-104">Click **Create a resource**, click **Databases**, and click **Redis Cache**.</span></span>

    <span data-ttu-id="ee22c-105">다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-105">The following screenshot shows the Redis Cache location within the various database resource options on the Azure portal.</span></span>

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조되어 있는 Azure Portal 데이터베이스 옵션을 보여 주는 스크린샷입니다.](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a><span data-ttu-id="ee22c-107">캐시 구성</span><span class="sxs-lookup"><span data-stu-id="ee22c-107">Configure your cache</span></span>

<span data-ttu-id="ee22c-108">캐시에서 다음 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-108">Apply the following settings on the cache.</span></span>

1. <span data-ttu-id="ee22c-109">**DNS 이름:** **ContosoSportsApp[nnn]** 과 같은 전역적으로 고유한 이름을 만듭니다. 여기서 `[nnn]`은 임의의 숫자로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-109">**DNS Name:** Create a globally unique name such as **ContosoSportsApp[nnn]**, where `[nnn]` is replaced with random numbers.</span></span>

1. <span data-ttu-id="ee22c-110">**구독**: 컨시어지 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-110">**Subscription:** Select the Concierge subscription.</span></span>

1. <span data-ttu-id="ee22c-111">**리소스 그룹**: 리소스 그룹의 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-111">**Resource group:** Select <rgn>[Sandbox resource group name]</rgn> for the Resource Group.</span></span>

1. <span data-ttu-id="ee22c-112">**위치:** 일반적으로 고객과 가까운 위치를 선택합니다. 이 예에서는 동부 해안입니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-112">**Location:** Normally, you would select a location near your customers - in this case, the East Coast.</span></span> <span data-ttu-id="ee22c-113">그러나 Azure 샌드박스는 특정 지역만 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-113">However, the Azure Sandbox only allows specific regions to be selected for resources.</span></span> <span data-ttu-id="ee22c-114">다음 위치 중 하나를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="ee22c-114">Please select one of the following locations.</span></span>
    
    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]
        
5. <span data-ttu-id="ee22c-115">**가격 책정 계층:** **기본 C0**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-115">**Pricing tier:** Select **Basic C0**.</span></span> <span data-ttu-id="ee22c-116">사용할 수 있는 가장 낮은 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-116">This is the lowest tier you can use.</span></span> <span data-ttu-id="ee22c-117">프로덕션 앱은 더 많은 데이터를 저장하기를 원하고 더 높은 계층이 필요한 클러스터링 같은 일부 프리미엄 기능을 활용하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-117">Production apps would likely want to store more data and utilize some of the Premium features such as clustering which would require a higher tier selection.</span></span>

1. <span data-ttu-id="ee22c-118">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-118">Click **Create**.</span></span> <span data-ttu-id="ee22c-119">Azure에서 자동으로 Redis Cache 인스턴스를 생성 및 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-119">Azure will create and deploy the Redis Cache instance for you.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="ee22c-120">일반적으로 Redis Cache 리소스가 생성되고 Azure Portal에서 매우 신속하게 볼 수 있지만 캐시 자체는 몇 분간 볼 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-120">Usually, the Redis cache resource will be created and viewable in the Azure portal very quickly, but the cache itself will not be available for a few minutes.</span></span> <span data-ttu-id="ee22c-121">다음 단계에서는 캐시의 상태를 확인하는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-121">The next steps show how to check the status of your cache.</span></span>

## <a name="verify-your-data"></a><span data-ttu-id="ee22c-122">데이터 확인</span><span class="sxs-lookup"><span data-stu-id="ee22c-122">Verify your data</span></span>

<span data-ttu-id="ee22c-123">Redis Cache 인스턴스가 생성된 후 Azure Portal의 **콘솔** 기능을 사용하여 이에 대한 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-123">You can use the **Console** feature in the Azure portal to issue commands to your Redis cache instance after it has been created.</span></span>

1. <span data-ttu-id="ee22c-124">왼쪽 사이드바에서 **모든 리소스**를 선택하거나 배포가 완료되면 표시되는 **알림** 팝업을 통해 Redis Cache를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Redis Cache 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-124">Locate your Redis cache through the **Notification** popup when it finishes deployment, or by selecting **All Resources** in the left-hand sidebar and using the filter box on the left to select Redis Cache instances.</span></span> <span data-ttu-id="ee22c-125">또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-125">Alternatively, you can use the search box at the top and type the name of the cache.</span></span>

1. <span data-ttu-id="ee22c-126">Redis Cache 인스턴스를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-126">Select your Redis cache instance.</span></span>

1. <span data-ttu-id="ee22c-127">"상태" 필드 값을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-127">Check the value of the "Status" field.</span></span> <span data-ttu-id="ee22c-128">상태가 "실행 중"이어야 캐시가 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-128">The cache is not ready until the status is "Running".</span></span> <span data-ttu-id="ee22c-129">계속하기 전에 몇 분 정도 기다려야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-129">You might have to wait for a few minutes before proceeding.</span></span>

1. <span data-ttu-id="ee22c-130">캐시가 실행되면 Redis Cache의 **개요** 블레이드에서 `>_ Console` 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-130">Once the cache is running, Click the `>_ Console` button in the toolbar on the **Overview** blade for your Redis Cache.</span></span> <span data-ttu-id="ee22c-131">하위 수준 Redis 명령을 입력할 수 있는 Redis 콘솔이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-131">This will open a Redis console, which allows you to enter low-level Redis commands.</span></span> <span data-ttu-id="ee22c-132">다음을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="ee22c-132">Try some of the following:</span></span>

    ```console
    ping
    ```
    
    ```output
    PONG
    ```
    
    ```console
    set test one
    ```
    
    ```output
    OK
    ```
    
    ```console
    get test
    ```
    
    ```output
    "one"
    ```
    
<span data-ttu-id="ee22c-133">상단의 이동 경로 탐색 막대를 통해 **개요** 패널로 다시 전환하거나 스크롤 막대를 사용하여 보기를 다시 왼쪽으로 밉니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-133">Switch back to the **Overview** panel either through the breadcrumb bar on the top, or use the scrollbar to slide the view back to the left.</span></span>

## <a name="retrieve-the-access-keys-and-host-name"></a><span data-ttu-id="ee22c-134">선택키 및 호스트 이름 검색</span><span class="sxs-lookup"><span data-stu-id="ee22c-134">Retrieve the access keys and host name</span></span>

1. <span data-ttu-id="ee22c-135">**설정** > **선택키**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-135">Select **Settings** > **Access keys**.</span></span> 

1. <span data-ttu-id="ee22c-136">**기본 연결 문자열(StackExchange.Redis)** 을 안전한 장소에 복사합니다. 그 다음 연습에서 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-136">Copy the **Primary connection string (StackExchange.Redis)** to a safe place, you will need it for the next exercise.</span></span>

    <span data-ttu-id="ee22c-137">이 키는 우리가 사용하려는 **StackExchange.Redis** 패키지의 응용 프로그램 설정 내에서 사용할 전체 연결 문자열의 기본 키와 호스트 이름을 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-137">This key includes your primary key and host name in a complete connection string for use within your application settings for the **StackExchange.Redis** package we are going to use.</span></span>

<span data-ttu-id="ee22c-138">다음으로, 캐시를 조사하는 데 사용할 수 있는 명령을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ee22c-138">Next, let's learn about some of the commands we can use to interrogate the cache.</span></span>