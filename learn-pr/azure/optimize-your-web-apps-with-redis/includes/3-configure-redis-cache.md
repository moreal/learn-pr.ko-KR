<span data-ttu-id="56964-101">스포츠 통계 개발 팀에서는 캐싱이 최근에 요청된 데이터에 필요한 성능을 크게 향상할 수 있다고 판단했습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="56964-102">그래서 다음 단계로 Azure Redis Cache 인스턴스를 만들고 구성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-102">Your next step is to create and configure an Azure Redis Cache instance.</span></span>

## <a name="create-and-configure-the-azure-redis-cache-instance"></a><span data-ttu-id="56964-103">Azure Redis Cache 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="56964-103">Create and configure the Azure Redis Cache instance</span></span>

1. <span data-ttu-id="56964-104">브라우저에서 [Azure Portal](https://portal.azure.com/?azure-portal=true)을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="56964-104">Open the [Azure Portal](https://portal.azure.com/?azure-portal=true) in your browser.</span></span>

1. <span data-ttu-id="56964-105">**리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-105">Click on **Create a resource**.</span></span>

1. <span data-ttu-id="56964-106">**Redis Cache**를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-106">Search for **Redis Cache**.</span></span>

1. <span data-ttu-id="56964-107">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-107">Click **Create**.</span></span>

1. <span data-ttu-id="56964-108">Azure Portal의 데이터베이스 리소스에서 Azure Redis Cache 인스턴스를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-108">You can add an Azure Redis Cache instance from the database resources in the Azure portal.</span></span>

1. <span data-ttu-id="56964-109">전역적으로 고유한 이름을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-109">Provide a globally unique name.</span></span> <span data-ttu-id="56964-110">이름은 1-63자의 문자열로, 숫자, 영문자 및 ‘-’ 문자만 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-110">The name must be a string between 1 and 63 characters and include only numbers, letters, and the '-' character.</span></span> <span data-ttu-id="56964-111">캐시 이름은 ‘-’ 문자로 시작하거나 끝날 수 없으며, 연속되는 ‘-’ 문자는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-111">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

1. <span data-ttu-id="56964-112">이 새로운 Azure Redis Cache 인스턴스가 만들어지는 구독을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-112">Provide the subscription under which this new Azure Redis Cache instance is created.</span></span>

1. <span data-ttu-id="56964-113">캐시를 만들 리소스 그룹의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-113">Name the resource group in which to create your cache.</span></span> <span data-ttu-id="56964-114">앱의 모든 리소스를 한 그룹에 배치하여 다 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-114">By putting all the resources for an app in a group, you can manage them together.</span></span>

1. <span data-ttu-id="56964-115">캐시 인스턴스와 응용 프로그램을 항상 동일한 지역/위치에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-115">Always place your cache instance and your application in the same region / location.</span></span> <span data-ttu-id="56964-116">다른 지역의 캐시에 연결하면 대기 시간이 대폭 증가하고 안정성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-116">Connecting to a cache in a different region can significantly increase latency and reduce reliability.</span></span> <span data-ttu-id="56964-117">Azure 외부의 캐시에 연결하는 경우 데이터를 소비하는 응용 프로그램이 실행되는 곳과 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-117">If you are connecting to the cache outside of Azure, then select a location close to where the application consuming the data is running.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="56964-118">캐시가 데이터 저장소보다 데이터 소비자와 가까이에 있는 것이 훨씬 더 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-118">It's far more important that the cache is close to the data consumer than the data store.</span></span>

1. <span data-ttu-id="56964-119">가격 책정 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-119">Select the pricing tier.</span></span> 
    - <span data-ttu-id="56964-120">프로덕션 시스템에는 항상 표준 또는 프리미엄 계층을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-120">We recommend you always use Standard or Premium Tier for production systems.</span></span> <span data-ttu-id="56964-121">기본 계층은 데이터 복제 및 SLA가 없는 단일 노드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-121">The Basic Tier is a single node system with no data replication and no SLA.</span></span> <span data-ttu-id="56964-122">또한 C1 이상의 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-122">Also, use at least a C1 cache.</span></span> <span data-ttu-id="56964-123">C0 캐시는 공유 CPU 코어를 사용하고 메모리가 매우 적기 때문에 간단한 개발/테스트 시나리오에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-123">C0 caches are really meant for simple dev/test scenarios since they have a shared CPU core and very little memory.</span></span>

    - <span data-ttu-id="56964-124">프리미엄 계층을 사용하면 두 가지 방법으로 데이터를 유지하여 재해 복구를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-124">The Premium tier allows you to persist data in two ways to provide disaster recovery:</span></span>

        - <span data-ttu-id="56964-125">RDB 지속성은 주기적 스냅숏을 만들고 실패가 발생하면 해당 스냅숏을 사용하여 캐시를 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-125">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

            ![새 Redis Cache 인스턴스에 대한 RDB 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-1.png)

        - <span data-ttu-id="56964-127">AOF 지속성은 초당 한 번 이상 저장되는 로그에 모든 쓰기 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-127">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="56964-128">이렇게 하면 RDB보다 큰 파일이 만들어지지만 데이터 손실은 더 적습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-128">This creates bigger files than RDB but has less data loss.</span></span>

            ![새 Redis Cache 인스턴스에 대한 AOF 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-2.png)

    - <span data-ttu-id="56964-130">가상 네트워크로 캐시를 보호합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-130">Secure your cache with a virtual network.</span></span>
      <span data-ttu-id="56964-131">프리미엄 계층 Redis Cache가 있는 경우 클라우드의 가상 네트워크에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-131">If you have a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="56964-132">캐시는 동일한 가상 네트워크의 다른 가상 머신 및 응용 프로그램에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-132">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span>

    - <span data-ttu-id="56964-133">클러스터링을 통해 캐시를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-133">Distribute your cache with clustering.</span></span>
      <span data-ttu-id="56964-134">프리미엄 계층 Redis Cache를 사용하면 여러 노드에 데이터 집합을 자동으로 분할하도록 클러스터링을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-134">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="56964-135">클러스터링을 구현하려면 분할된 데이터베이스 수를 최대 10개까지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-135">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="56964-136">발생하는 비용은 원래 노드에 분할 수를 곱한 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-136">The cost incurred is the cost of the original node, multiplied by the number of shards.</span></span>

    - <span data-ttu-id="56964-137">Azure Managed Cache Service에서 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-137">Migrate from Azure Managed Cache Service.</span></span>
      <span data-ttu-id="56964-138">사용하는 Managed Cache Service 기능에 따라 응용 프로그램 변경을 최소화하여 Azure Managed Cache Service 사용 응용 프로그램을 Azure Redis Cache로 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-138">Depending on the Managed Cache Service features you use, migrating applications that use Azure Managed Cache Service to Azure Redis Cache can be accomplished with minimal changes to your application.</span></span> <span data-ttu-id="56964-139">API가 정확하게 동일하지는 않더라도 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-139">While the APIs aren't exactly the same, they're similar.</span></span> <span data-ttu-id="56964-140">Managed Cache Service를 사용하여 캐시에 액세스하는 기존 코드는 대부분 최소한의 변경만으로 재사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-140">Much of your existing code that accesses the cache with Managed Cache Service can be reused with minimal changes.</span></span>

## <a name="accessing-the-redis-instance"></a><span data-ttu-id="56964-141">Redis 인스턴스에 액세스</span><span class="sxs-lookup"><span data-stu-id="56964-141">Accessing the Redis instance</span></span>

<span data-ttu-id="56964-142">Redis는 [알려진 명령](https://redis.io/commands) 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-142">Redis supports a set of [known commands](https://redis.io/commands).</span></span> <span data-ttu-id="56964-143">명령은 일반적으로 `COMMAND parameter1 parameter2 parameter3`으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="56964-143">A command is typically issued as `COMMAND parameter1 parameter2 parameter3`.</span></span>

<span data-ttu-id="56964-144">다음은 사용할 수 있는 몇 가지 일반적인 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-144">Here are some common commands you can use:</span></span>

| <span data-ttu-id="56964-145">명령</span><span class="sxs-lookup"><span data-stu-id="56964-145">Command</span></span> | <span data-ttu-id="56964-146">설명</span><span class="sxs-lookup"><span data-stu-id="56964-146">Description</span></span> |
|---------|-------------|
| `ping` | <span data-ttu-id="56964-147">서버를 ping 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-147">Ping the server.</span></span> <span data-ttu-id="56964-148">"PONG"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-148">Returns "PONG".</span></span> |
| `set [key] [value]` | <span data-ttu-id="56964-149">캐시의 키/값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-149">Sets a key/value in the cache.</span></span> <span data-ttu-id="56964-150">성공 시 "OK"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-150">Returns "OK" on success.</span></span> |
| `get [key]` | <span data-ttu-id="56964-151">캐시에서 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="56964-151">Gets a value from the cache.</span></span> |
| `exists [key]` | <span data-ttu-id="56964-152">캐시에 **키**가 있으면 '1'을 반환하고, 없으면 '0'을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-152">Returns '1' if the **key** exists in the cache, '0' if it doesn't.</span></span> |
| `type [key]` | <span data-ttu-id="56964-153">특정 **키** 값과 연결된 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-153">Returns the type associated to the value for the given **key**.</span></span> |
| `incr [key]` | <span data-ttu-id="56964-154">**키**와 연결된 특정 값을 '1'씩 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="56964-154">Increment the given value associated with **key** by \`1'.</span></span> <span data-ttu-id="56964-155">이 값은 정수이거나 double 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-155">The value must be an integer or double value.</span></span> <span data-ttu-id="56964-156">새 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-156">This returns the new value.</span></span> |
| `incrby [key] [amount]` | <span data-ttu-id="56964-157">**키**와 연결된 특정 값을 지정된 양만큼 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="56964-157">Increment the given value associated with **key** by the specified amount.</span></span> <span data-ttu-id="56964-158">이 값은 정수이거나 double 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-158">The value must be an integer or double value.</span></span> <span data-ttu-id="56964-159">새 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-159">This returns the new value.</span></span> |
| `del [key]` | <span data-ttu-id="56964-160">**키**와 연결된 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-160">Deletes the value associated with the **key**.</span></span> |
| `flushdb` | <span data-ttu-id="56964-161">데이터베이스의 _모든_ 키와 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-161">Delete _all_ keys and values in the database.</span></span> |

<span data-ttu-id="56964-162">Redis는 다음 명령을 사용하여 직접 실험에 사용할 수 있는 명령줄 도구(**redis-cli**)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-162">Redis has a command-line tool (**redis-cli**) you can use to experiment directly with these commands.</span></span> <span data-ttu-id="56964-163">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-163">Here are some examples.</span></span>

```output
> set somekey somevalue
OK
> get somekey
"somevalue"
> exists somekey
(string) 1
> del somekey
(string) 1
> exists somekey
(string) 0
```

<span data-ttu-id="56964-164">다음은 `INCR` 명령을 사용하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-164">Here's an example of working with the `INCR` commands.</span></span> <span data-ttu-id="56964-165">캐시를 사용하는 _여러 응용 프로그램에서_ 원자성 증분을 제공하므로 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-165">These are convenient because they provide atomic increments _across multiple applications_ that are using the cache.</span></span>

```output
> set counter 100
OK
> incr counter
(integer) 101
> incrby counter 50
(integer) 151
> type counter
(integer)
```

### <a name="adding-an-expiration-time-to-values"></a><span data-ttu-id="56964-166">값에 만료 시간 추가</span><span class="sxs-lookup"><span data-stu-id="56964-166">Adding an expiration time to values</span></span>

<span data-ttu-id="56964-167">캐싱을 사용하면 일반적으로 사용되는 값을 저장소에 저장할 수 있으므로 캐싱이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-167">Caching is important because it allows us to store commonly used values in memory.</span></span> <span data-ttu-id="56964-168">그러나 오래된 값을 만료하는 방법도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-168">However, we also need a way to expire values when they are stale.</span></span> <span data-ttu-id="56964-169">Redis에서는 _TTL(Time to live)_ 을 키에 적용하여 오래된 값을 만료합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-169">In Redis this is done by applying a _time to live_ (TTL) to a key.</span></span>

<span data-ttu-id="56964-170">TTL이 경과되면 마치 DEL 명령을 실행한 것처럼 키가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="56964-170">When the TTL elapses, the key is automatically deleted, exactly as if the DEL command were issued.</span></span> <span data-ttu-id="56964-171">다음은 TTL 만료에 대한 참고 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-171">Here are some notes on TTL expirations.</span></span>

- <span data-ttu-id="56964-172">만료 시간은 초 또는 밀리초 단위로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-172">Expirations can be set using seconds or milliseconds precision.</span></span>
- <span data-ttu-id="56964-173">만료 시간 해상도는 항상 1밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-173">The expire time resolution is always 1 millisecond.</span></span>
- <span data-ttu-id="56964-174">Redis 서버가 중지된 상태로 남아 있으면(즉, Redis가 키의 만료 날짜를 저장하면) 만료에 대한 정보가 복제되어 디스크에 보관되고, 시간이 가상으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="56964-174">Information about expires are replicated and persisted on disk, the time virtually passes when your Redis server remains stopped (this means that Redis saves the date at which a key will expire).</span></span>

<span data-ttu-id="56964-175">다음은 만료의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-175">Here is an example of an expiration:</span></span>

```output
> set counter 100
OK
> expire counter 5
(integer) 1
> get counter
100
... wait ...
> get counter
(nil)
```

## <a name="accessing-a-redis-cache-from-a-client"></a><span data-ttu-id="56964-176">클라이언트에서 Redis 캐시에 액세스</span><span class="sxs-lookup"><span data-stu-id="56964-176">Accessing a Redis cache from a client</span></span>

<span data-ttu-id="56964-177">Azure Redis Cache 인스턴스에 연결할 때 클라이언트에 캐시의 호스트 이름, 포트 및 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-177">When connecting to an Azure Redis Cache instance, clients need the host name, port, and an access key for the cache.</span></span> <span data-ttu-id="56964-178">이 정보는 Azure Portal의 **설정 > 액세스 키** 페이지에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-178">You can retrieve this information in the Azure portal through the **Settings > Access Keys** page.</span></span> 

- <span data-ttu-id="56964-179">호스트 이름은 캐시 이름을 사용하여 만든 캐시의 공용 인터넷 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-179">The host name is the public Internet address of your cache, which was created using the name of the cache.</span></span> <span data-ttu-id="56964-180">예: `sportsresults.redis.cache.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="56964-180">For example `sportsresults.redis.cache.windows.net`.</span></span>

- <span data-ttu-id="56964-181">액세스 키는 캐시의 암호 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-181">The access key acts as a password for your cache.</span></span> <span data-ttu-id="56964-182">두 개의 키가 생성되는데, 하나는 기본 키이고 다른 하나는 보조 키입니다.</span><span class="sxs-lookup"><span data-stu-id="56964-182">There are two keys created: primary and secondary.</span></span> <span data-ttu-id="56964-183">둘 중 어느 것이든 사용할 수 있으며, 기본 키를 변경해야 하는 경우에는 둘 다 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="56964-183">You can use either key, two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="56964-184">모든 클라이언트를 보조 키로 전환하고, 기본 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-184">You can switch all of your clients to the secondary key, and regenerate the primary key.</span></span> <span data-ttu-id="56964-185">이렇게 하면 원래 기본 키를 사용하는 응용 프로그램이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="56964-185">This would block any applications using the original primary key.</span></span> <span data-ttu-id="56964-186">개인 암호처럼 키를 주기적으로 다시 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="56964-186">Microsoft recommends periodically regenerating the keys - much like you would your personal passwords.</span></span>

> [!WARNING]
> <span data-ttu-id="56964-187">액세스 키는 기밀 정보라고 생각하고 암호처럼 취급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="56964-187">Your access keys should be considered confidential information, treat them like you would a password.</span></span> <span data-ttu-id="56964-188">액세스 키를 갖고 있는 사람은 누구든지 캐시에서 모든 작업을 수행할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="56964-188">Anyone who has an access key can perform any operation on your cache!</span></span>
