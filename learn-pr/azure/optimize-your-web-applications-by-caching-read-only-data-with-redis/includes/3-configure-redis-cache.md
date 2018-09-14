<span data-ttu-id="2b3b1-101">스포츠 통계 개발 팀에서는 캐싱이 최근에 요청된 데이터에 필요한 성능을 크게 향상할 수 있다고 판단했습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="2b3b1-102">그래서 다음 단계로 Azure Redis Cache 인스턴스를 만들고 구성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-102">Your next step is to create and configure an Azure Redis Cache instance.</span></span>

### <a name="create-and-configure-the-azure-redis-cache-instance"></a><span data-ttu-id="2b3b1-103">Azure Redis Cache 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="2b3b1-103">Create and configure the Azure Redis Cache instance</span></span>

1. <span data-ttu-id="2b3b1-104">Azure Portal의 데이터베이스 리소스에서 Azure Redis Cache 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-104">You can add an Azure Redis Cache instance from the database resources in the Azure portal.</span></span>

1. <span data-ttu-id="2b3b1-105">전역적으로 고유한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-105">Provide a globally unique name.</span></span> <span data-ttu-id="2b3b1-106">이름은 1-63자의 문자열로, 숫자, 영문자 및 ‘-’ 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-106">The name must be a string between 1 and 63 characters and include only numbers, letters, and the '-' character.</span></span> <span data-ttu-id="2b3b1-107">캐시 이름은 ‘-’ 문자로 시작하거나 끝날 수 없으며, 연속되는 ‘-’ 문자는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-107">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

1. <span data-ttu-id="2b3b1-108">이 새로운 Azure Redis Cache 인스턴스가 만들어지는 구독을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-108">Provide the subscription under which this new Azure Redis Cache instance is created.</span></span>

1. <span data-ttu-id="2b3b1-109">캐시를 만들 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-109">Name the resource group in which to create your cache.</span></span> <span data-ttu-id="2b3b1-110">앱의 모든 리소스를 한 그룹에 배치하여 다 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-110">By putting all the resources for an app in a group, you can manage them together.</span></span>

1. <span data-ttu-id="2b3b1-111">데이터 소비자에게 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-111">Choose a location that is close to the consumer of the data.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2b3b1-112">캐시가 데이터 저장소보다 데이터 소비자에게 가까운 것보다 훨씬 더 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-112">It's far more important that the cache is close to the data consumer than the data store.</span></span>

1. <span data-ttu-id="2b3b1-113">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-113">Select the pricing tier.</span></span> <span data-ttu-id="2b3b1-114">데이터 지속성을 활용하려면 프리미엄 계층을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-114">Remember, to take advantage of data persistence, you'll need to choose a premium tier.</span></span>

    - <span data-ttu-id="2b3b1-115">프리미엄 계층을 사용하면 다음 두 가지 방법 중 하나로 데이터를 유지하여 재해 복구를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-115">The premium tier allows you to persist data in one of two ways to provide disaster recovery:</span></span>

        - <span data-ttu-id="2b3b1-116">RDB 지속성은 주기적 스냅숏을 만들고 실패가 발생하면 해당 스냅숏을 사용하여 캐시를 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-116">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

            ![새 Redis Cache 인스턴스에 대한 RDB 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-1.png)

        - <span data-ttu-id="2b3b1-118">AOF 지속성은 초당 한 번 이상 저장되는 로그에 모든 쓰기 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-118">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="2b3b1-119">이렇게 하면 RDB보다 큰 파일이 만들어지지만 데이터 손실은 더 적습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-119">This creates bigger files than RDB but has less data loss.</span></span>

            ![새 Redis Cache 인스턴스에 대한 AOF 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-2.png)

    - <span data-ttu-id="2b3b1-121">가상 네트워크로 캐시를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-121">Secure your cache with a virtual network.</span></span>
      <span data-ttu-id="2b3b1-122">프리미엄 계층 Redis Cache가 있는 경우 클라우드의 가상 네트워크에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-122">If you have a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="2b3b1-123">캐시는 동일한 가상 네트워크의 다른 가상 머신 및 응용 프로그램에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-123">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span>

    - <span data-ttu-id="2b3b1-124">클러스터링을 통해 캐시를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-124">Distribute your cache with clustering.</span></span>
      <span data-ttu-id="2b3b1-125">프리미엄 계층 Redis Cache를 사용하면 여러 노드에 데이터 집합을 자동으로 분할하도록 클러스터링을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-125">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="2b3b1-126">클러스터링을 구현하려면 최대 10까지 분할 수를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-126">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="2b3b1-127">비용은 원래 노드에 분할 수를 곱한 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-127">The cost is the cost of the original node multiplied by the number of shards.</span></span>

    - <span data-ttu-id="2b3b1-128">Azure Managed Cache Service에서 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-128">Migrate from Azure Managed Cache Service.</span></span>
      <span data-ttu-id="2b3b1-129">사용하는 Managed Cache Service 기능에 따라 응용 프로그램 변경을 최소화하여 Azure Managed Cache Service 사용 응용 프로그램을 Azure Redis Cache로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-129">Depending on the Managed Cache Service features you use, migrating applications that use Azure Managed Cache Service to Azure Redis Cache can be accomplished with minimal changes to your application.</span></span> <span data-ttu-id="2b3b1-130">API가 정확하게 동일하지는 않더라도 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-130">While the APIs aren't exactly the same, they're similar.</span></span> <span data-ttu-id="2b3b1-131">Managed Cache Service를 사용하여 캐시에 액세스하는 기존 코드의 대부분은 최소한의 변경만으로 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-131">Much of your existing code that accesses the cache with Managed Cache Service can be reused with minimal changes.</span></span>

### <a name="configure-your-client"></a><span data-ttu-id="2b3b1-132">클라이언트 구성</span><span class="sxs-lookup"><span data-stu-id="2b3b1-132">Configure your client</span></span>

<span data-ttu-id="2b3b1-133">클라이언트 응용 프로그램은 Redis Cache를 사용하도록 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-133">Client applications need to be configured to use the Redis cache.</span></span> <span data-ttu-id="2b3b1-134">.NET 언어를 위한 인기 있는 고성능 Redis 클라이언트는 **StackExchange.Redis**입니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-134">A popular high-performance Redis client for the .NET language is **StackExchange.Redis**.</span></span> <span data-ttu-id="2b3b1-135">Visual Studio에서 **NuGet 패키지 관리자**를 사용하는 Redis 클라이언트는 **Install-Package** 명령을 사용하여 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-135">You add the Redis client using the **NuGet Package Manager** in Visual Studio using the **Install-Package** command.</span></span>

<span data-ttu-id="2b3b1-136">그런 다음, 캐시에 연결하도록 클라이언트를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-136">You then need to configure your client to connect to your cache.</span></span> <span data-ttu-id="2b3b1-137">호스트 이름과 기본 또는 보조 키 설정이 포함된 **.config** 파일 확장을 사용하여 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-137">Create a text file with a **.config** file extension that contains the settings for the host name and primary, or secondary, key.</span></span> <span data-ttu-id="2b3b1-138">파일의 구조는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-138">The file should have the following structure:</span></span>

```XML
    <appSettings>
        <add key="CacheConnection" value="HOST-NAME.redis.cache.windows.net,abortConnect=false,ssl=true,password=PRIMARY-KEY"/>
    </appSettings>
```

<span data-ttu-id="2b3b1-139">**App.config** 파일을 편집하고 방금 만든 구성 파일을 참조하는 **appSettings** 파일 특성을 포함하도록 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-139">You will then edit your **App.config** file and update it to include an **appSettings** file attribute that references the config file that you just created.</span></span>

### <a name="what-are-access-keys"></a><span data-ttu-id="2b3b1-140">액세스 키란?</span><span class="sxs-lookup"><span data-stu-id="2b3b1-140">What are access keys?</span></span>

<span data-ttu-id="2b3b1-141">Azure Redis Cache 인스턴스에 연결할 때 캐시 클라이언트에 캐시의 호스트 이름, 포트 및 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-141">When connecting to an Azure Redis Cache instance, cache clients need the host name, ports, and a key for the cache.</span></span> <span data-ttu-id="2b3b1-142">이 정보는 Azure Portal에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-142">You can retrieve this information in the Azure portal.</span></span>

### <a name="connection-settings"></a><span data-ttu-id="2b3b1-143">연결 설정</span><span class="sxs-lookup"><span data-stu-id="2b3b1-143">Connection settings</span></span>

<span data-ttu-id="2b3b1-144">Azure Redis Cache에 연결하려면 호스트 이름과 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-144">To connect to your Azure Redis Cache, you'll need the host name and access key.</span></span> <span data-ttu-id="2b3b1-145">호스트 이름은 캐시의 인터넷 주소입니다(예: *sportsresults.redis.cache.windows.net*).</span><span class="sxs-lookup"><span data-stu-id="2b3b1-145">The host name is the internet address of your cache, for example *sportsresults.redis.cache.windows.net*.</span></span> <span data-ttu-id="2b3b1-146">액세스 키는 캐시의 암호 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-146">The access key acts as a password for your cache.</span></span> <span data-ttu-id="2b3b1-147">기본 및 보조 액세스 키가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-147">There are primary and secondary access keys.</span></span> <span data-ttu-id="2b3b1-148">둘 중 어느 것이든 사용할 수 있지만 기본 키를 변경해야 하는 경우에는 둘 다 입력됩니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-148">You can use either key, but two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="2b3b1-149">모든 클라이언트를 보조 키로 전환한 후 기본 키를 변경하면 서비스 손실을 예방할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2b3b1-149">You can switch all of your clients to the secondary key and then make the change to the primary key, which would prevent any loss of service.</span></span>
