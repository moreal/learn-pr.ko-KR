<span data-ttu-id="9ffc9-101">스포츠 통계 개발 팀에서는 캐싱이 최근에 요청된 데이터에 필요한 성능을 크게 향상할 수 있다고 판단했습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-101">Your sports statistics development team has decided that caching could dramatically improve performance for recently requested data.</span></span> <span data-ttu-id="9ffc9-102">그래서 다음 단계로 Azure Redis Cache 인스턴스를 만들고 구성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-102">Your next step is to create and configure an Azure Redis Cache instance.</span></span>

## <a name="create-and-configure-the-azure-redis-cache-instance"></a><span data-ttu-id="9ffc9-103">Azure Redis Cache 인스턴스 만들기 및 구성</span><span class="sxs-lookup"><span data-stu-id="9ffc9-103">Create and configure the Azure Redis Cache instance</span></span>

<span data-ttu-id="9ffc9-104">Azure Portal, Azure CLI 또는 Azure PowerShell을 사용하여 Redis Cache를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-104">You can create a Redis cache using the Azure portal, the Azure CLI, or Azure PowerShell.</span></span> <span data-ttu-id="9ffc9-105">용도에 맞게 캐시를 제대로 구성하기 위해 결정해야 하는 몇 가지 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-105">There are several parameters you will need to decide in order to configure the cache properly for your purposes.</span></span>

### <a name="name"></a><span data-ttu-id="9ffc9-106">이름</span><span class="sxs-lookup"><span data-stu-id="9ffc9-106">Name</span></span>

<span data-ttu-id="9ffc9-107">Redis Cache에는 전세계에 고유한 이름이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-107">The Redis cache will need a globally unique name.</span></span> <span data-ttu-id="9ffc9-108">이름이 서비스와 연결하고 통신하기 위해 공용 URL을 생성하는 데 사용되므로 Azure 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-108">The name has to be unique within Azure because it is used to generate a public-facing URL to connect and communicate with the service.</span></span>

<span data-ttu-id="9ffc9-109">이름은 1-63자이며 숫자, 영문자 및 '-' 문자로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-109">The name must be between 1 and 63 characters, composed of numbers, letters, and the '-' character.</span></span> <span data-ttu-id="9ffc9-110">캐시 이름은 '-' 문자로 시작하거나 끝날 수 없으며, 연속되는 '-' 문자는 유효하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-110">The cache name can't start or end with the '-' character, and consecutive '-' characters aren't valid.</span></span>

### <a name="resource-group"></a><span data-ttu-id="9ffc9-111">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="9ffc9-111">Resource Group</span></span>

<span data-ttu-id="9ffc9-112">Azure Redis Cache는 관리되는 리소스이며 _리소스 그룹_ 소유자 역할이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-112">The Azure Redis Cache is a managed resource and needs a _resource group_ owner.</span></span> <span data-ttu-id="9ffc9-113">새 리소스 그룹을 만들거나 속한 구독에서 기존 리소스 그룹을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-113">You can either create a new resource group, or use an existing one in a subscription you are part of.</span></span>

### <a name="location"></a><span data-ttu-id="9ffc9-114">위치</span><span class="sxs-lookup"><span data-stu-id="9ffc9-114">Location</span></span>

<span data-ttu-id="9ffc9-115">Azure 지역을 선택하여 Redis Cache를 물리적으로 배치할 위치를 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-115">You will need to decide where the Redis cache will be physically located by selecting an Azure region.</span></span> <span data-ttu-id="9ffc9-116">캐시 인스턴스와 응용 프로그램을 항상 동일한 지역에 배치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-116">You should always place your cache instance and your application in the same region.</span></span> <span data-ttu-id="9ffc9-117">다른 지역의 캐시에 연결하면 대기 시간이 크게 증가하고 안정성이 떨어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-117">Connecting to a cache in a different region can significantly increase latency and reduce reliability.</span></span> <span data-ttu-id="9ffc9-118">Azure 외부의 캐시에 연결하는 경우 데이터를 소비하는 응용 프로그램이 실행되는 곳과 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-118">If you are connecting to the cache outside of Azure, then select a location close to where the application consuming the data is running.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9ffc9-119">가능하면 Redis Cache를 _소비자_의 데이터에 가깝게 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-119">Put the Redis cache as close to the data _consumer_ as you can.</span></span>

### <a name="pricing-tier"></a><span data-ttu-id="9ffc9-120">가격 책정 계층</span><span class="sxs-lookup"><span data-stu-id="9ffc9-120">Pricing tier</span></span>

<span data-ttu-id="9ffc9-121">마지막 단원에서 언급했듯이 세 가지 가격 책정 계층을 Azure Redis Cache에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-121">As mentioned in the last unit, there are three pricing tiers available for an Azure Redis Cache.</span></span>

- <span data-ttu-id="9ffc9-122">**기본**: 기본 캐시는 개발/테스트에 이상적입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-122">**Basic**: Basic cache ideal for development/testing.</span></span> <span data-ttu-id="9ffc9-123">단일 서버, 53GB의 메모리 및 20,000개의 연결로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-123">Is limited to a single server, 53 GB of memory, and 20,000 connections.</span></span> <span data-ttu-id="9ffc9-124">이 서비스 계층에 대한 SLA가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-124">There is no SLA for this service tier.</span></span>
- <span data-ttu-id="9ffc9-125">**표준**: 복제를 지원하고 99.99% SLA를 포함하는 프로덕션 캐시입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-125">**Standard**: Production cache which supports replication and includes an 99.99% SLA.</span></span> <span data-ttu-id="9ffc9-126">두 서버(마스터/슬레이브)를 지원하고, 기본 계층과 동일한 메모리/연결 제한이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-126">It supports two servers (master/slave), and has the same memory/connection limits as the Basic tier.</span></span>
- <span data-ttu-id="9ffc9-127">**프리미엄**: 표준 계층에서 빌드하고 지속성, 클러스터링 및 스케일 아웃 캐시 지원이 포함된 Enterprise 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-127">**Premium**: Enterprise tier which builds on the Standard tier and includes persistence, clustering, and scale-out cache support.</span></span> <span data-ttu-id="9ffc9-128">최대 530GB의 메모리 및 40,000개의 동시 연결을 포함한 최고 성능 계층입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-128">This is the highest performing tier with up to 530 GB of memory and 40,000 simultaneous connections.</span></span>

<span data-ttu-id="9ffc9-129">각 계층에서 사용 가능한 캐시 메모리 양을 제어할 수 있습니다. 기본/표준에 대해 C0-C6 및 프리미엄에 대해 P0-P4의 캐시 수준을 선택하여 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-129">You can control the amount of cache memory available on each tier - this is selected by choosing a cache level from C0-C6 for Basic/Standard and P0-P4 for Premium.</span></span> <span data-ttu-id="9ffc9-130">전체 세부 내용은 [가격 책정 페이지](https://azure.microsoft.com/pricing/details/cache/)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-130">Check the [pricing page](https://azure.microsoft.com/pricing/details/cache/) for full details.</span></span>

> [!TIP]
> <span data-ttu-id="9ffc9-131">프로덕션 시스템에는 항상 표준 또는 프리미엄 계층을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-131">Microsoft recommends you always use Standard or Premium Tier for production systems.</span></span> <span data-ttu-id="9ffc9-132">기본 계층은 데이터 복제 및 SLA가 없는 단일 노드 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-132">The Basic Tier is a single node system with no data replication and no SLA.</span></span> <span data-ttu-id="9ffc9-133">또한 C1 이상의 캐시를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-133">Also, use at least a C1 cache.</span></span> <span data-ttu-id="9ffc9-134">C0 캐시는 공유 CPU 코어를 사용하고 메모리가 매우 적기 때문에 간단한 개발/테스트 시나리오에만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-134">C0 caches are really meant for simple dev/test scenarios since they have a shared CPU core and very little memory.</span></span>

<span data-ttu-id="9ffc9-135">프리미엄 계층을 사용하면 두 가지 방법으로 데이터를 유지하여 재해 복구를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-135">The Premium tier allows you to persist data in two ways to provide disaster recovery:</span></span>

1. <span data-ttu-id="9ffc9-136">RDB 지속성은 주기적 스냅숏을 만들고 실패가 발생하면 해당 스냅숏을 사용하여 캐시를 다시 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-136">RDB persistence takes a periodic snapshot and can rebuild the cache using the snapshot in case of failure.</span></span>

    ![새 Redis Cache 인스턴스에 대한 RDB 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-1.png)

2. <span data-ttu-id="9ffc9-138">AOF 지속성은 초당 한 번 이상 저장되는 로그에 모든 쓰기 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-138">AOF persistence saves every write operation to a log that is saved at least once per second.</span></span> <span data-ttu-id="9ffc9-139">이렇게 하면 RDB보다 큰 파일이 만들어지지만 데이터 손실은 더 적습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-139">This creates bigger files than RDB but has less data loss.</span></span>

    ![새 Redis Cache 인스턴스에 대한 AOF 지속성 옵션을 보여주는 Azure Portal의 스크린샷](../media/3-redis-persistence-2.png)

<span data-ttu-id="9ffc9-141">**프리미엄** 계층에만 사용할 수 있는 몇 가지 다른 설정이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-141">There are several other settings which are only available to the **Premium** tier.</span></span>

### <a name="virtual-network-support"></a><span data-ttu-id="9ffc9-142">Virtual Network 지원</span><span class="sxs-lookup"><span data-stu-id="9ffc9-142">Virtual Network support</span></span>

<span data-ttu-id="9ffc9-143">프리미엄 계층 Redis Cache를 만들 경우 클라우드의 가상 네트워크에 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-143">If you create a premium tier Redis cache, you can deploy it to a virtual network in the cloud.</span></span> <span data-ttu-id="9ffc9-144">캐시는 동일한 가상 네트워크의 다른 가상 머신 및 응용 프로그램에만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-144">Your cache will be available to only other virtual machines and applications in the same virtual network.</span></span> <span data-ttu-id="9ffc9-145">서비스와 캐시가 Azure에서 호스트되거나 Azure Virtual Network VPN을 통해 연결된 경우 이 기능은 더 높은 수준의 보안을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-145">This provides a higher level of security when your service and cache are both hosted in Azure, or are connected through an Azure virtual network VPN.</span></span>

### <a name="clustering-support"></a><span data-ttu-id="9ffc9-146">클러스터링 지원</span><span class="sxs-lookup"><span data-stu-id="9ffc9-146">Clustering support</span></span>

<span data-ttu-id="9ffc9-147">프리미엄 계층 Redis Cache를 사용하면 여러 노드에 데이터 집합을 자동으로 분할하도록 클러스터링을 구현할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-147">With a premium tier Redis cache, you can implement clustering to automatically split your dataset among multiple nodes.</span></span> <span data-ttu-id="9ffc9-148">클러스터링을 구현하려면 분할된 데이터베이스 수를 최대 10개까지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-148">To implement clustering, you specify the number of shards to a maximum of 10.</span></span> <span data-ttu-id="9ffc9-149">발생하는 비용은 원래 노드에 분할된 데이터베이스 수를 곱한 비용입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-149">The cost incurred is the cost of the original node, multiplied by the number of shards.</span></span>

## <a name="accessing-the-redis-instance"></a><span data-ttu-id="9ffc9-150">Redis 인스턴스에 액세스</span><span class="sxs-lookup"><span data-stu-id="9ffc9-150">Accessing the Redis instance</span></span>

<span data-ttu-id="9ffc9-151">Redis는 [알려진 명령](https://redis.io/commands) 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-151">Redis supports a set of [known commands](https://redis.io/commands).</span></span> <span data-ttu-id="9ffc9-152">명령은 일반적으로 `COMMAND parameter1 parameter2 parameter3`으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-152">A command is typically issued as `COMMAND parameter1 parameter2 parameter3`.</span></span>

<span data-ttu-id="9ffc9-153">다음은 사용할 수 있는 몇 가지 일반적인 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-153">Here are some common commands you can use:</span></span>

| <span data-ttu-id="9ffc9-154">명령</span><span class="sxs-lookup"><span data-stu-id="9ffc9-154">Command</span></span> | <span data-ttu-id="9ffc9-155">설명</span><span class="sxs-lookup"><span data-stu-id="9ffc9-155">Description</span></span> |
|---------|-------------|
| `ping` | <span data-ttu-id="9ffc9-156">서버를 ping 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-156">Ping the server.</span></span> <span data-ttu-id="9ffc9-157">"PONG"을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-157">Returns "PONG".</span></span> |
| `set [key] [value]` | <span data-ttu-id="9ffc9-158">캐시의 키/값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-158">Sets a key/value in the cache.</span></span> <span data-ttu-id="9ffc9-159">성공 시 "OK"를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-159">Returns "OK" on success.</span></span> |
| `get [key]` | <span data-ttu-id="9ffc9-160">캐시에서 값을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-160">Gets a value from the cache.</span></span> |
| `exists [key]` | <span data-ttu-id="9ffc9-161">캐시에 **키**가 있으면 '1'을 반환하고, 없으면 '0'을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-161">Returns '1' if the **key** exists in the cache, '0' if it doesn't.</span></span> |
| `type [key]` | <span data-ttu-id="9ffc9-162">특정 **키** 값과 연결된 형식을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-162">Returns the type associated to the value for the given **key**.</span></span> |
| `incr [key]` | <span data-ttu-id="9ffc9-163">**키**와 연결된 특정 값을 '1'씩 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-163">Increment the given value associated with **key** by '1'.</span></span> <span data-ttu-id="9ffc9-164">이 값은 정수이거나 double 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-164">The value must be an integer or double value.</span></span> <span data-ttu-id="9ffc9-165">새 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-165">This returns the new value.</span></span> |
| `incrby [key] [amount]` | <span data-ttu-id="9ffc9-166">**키**와 연결된 특정 값을 지정된 양만큼 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-166">Increment the given value associated with **key** by the specified amount.</span></span> <span data-ttu-id="9ffc9-167">이 값은 정수이거나 double 값이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-167">The value must be an integer or double value.</span></span> <span data-ttu-id="9ffc9-168">새 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-168">This returns the new value.</span></span> |
| `del [key]` | <span data-ttu-id="9ffc9-169">**키**와 연결된 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-169">Deletes the value associated with the **key**.</span></span> |
| `flushdb` | <span data-ttu-id="9ffc9-170">데이터베이스의 _모든_ 키와 값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-170">Delete _all_ keys and values in the database.</span></span> |

<span data-ttu-id="9ffc9-171">Redis는 다음 명령을 사용하여 직접 실험에 사용할 수 있는 명령줄 도구(**redis-cli**)를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-171">Redis has a command-line tool (**redis-cli**) you can use to experiment directly with these commands.</span></span> <span data-ttu-id="9ffc9-172">다음은 몇 가지 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-172">Here are some examples.</span></span>

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

<span data-ttu-id="9ffc9-173">다음은 `INCR` 명령을 사용하는 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-173">Here's an example of working with the `INCR` commands.</span></span> <span data-ttu-id="9ffc9-174">캐시를 사용하는 _여러 응용 프로그램에서_ 원자성 증분을 제공하므로 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-174">These are convenient because they provide atomic increments _across multiple applications_ that are using the cache.</span></span>

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

### <a name="adding-an-expiration-time-to-values"></a><span data-ttu-id="9ffc9-175">값에 만료 시간 추가</span><span class="sxs-lookup"><span data-stu-id="9ffc9-175">Adding an expiration time to values</span></span>

<span data-ttu-id="9ffc9-176">캐싱을 사용하면 일반적으로 사용되는 값을 저장소에 저장할 수 있으므로 캐싱이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-176">Caching is important because it allows us to store commonly used values in memory.</span></span> <span data-ttu-id="9ffc9-177">그러나 오래된 값을 만료하는 방법도 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-177">However, we also need a way to expire values when they are stale.</span></span> <span data-ttu-id="9ffc9-178">Redis에서는 _TTL(Time to live)_ 을 키에 적용하여 오래된 값을 만료합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-178">In Redis this is done by applying a _time to live_ (TTL) to a key.</span></span>

<span data-ttu-id="9ffc9-179">TTL이 경과되면 마치 DEL 명령을 실행한 것처럼 키가 자동으로 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-179">When the TTL elapses, the key is automatically deleted, exactly as if the DEL command were issued.</span></span> <span data-ttu-id="9ffc9-180">다음은 TTL 만료에 대한 참고 사항입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-180">Here are some notes on TTL expirations.</span></span>

- <span data-ttu-id="9ffc9-181">만료 시간은 초 또는 밀리초 단위로 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-181">Expirations can be set using seconds or milliseconds precision.</span></span>
- <span data-ttu-id="9ffc9-182">만료 시간 해상도는 항상 1밀리초입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-182">The expire time resolution is always 1 millisecond.</span></span>
- <span data-ttu-id="9ffc9-183">Redis 서버가 중지된 상태로 남아 있으면(즉, Redis가 키의 만료 날짜를 저장하면) 만료에 대한 정보가 복제되어 디스크에 보관되고, 시간이 가상으로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-183">Information about expires are replicated and persisted on disk, the time virtually passes when your Redis server remains stopped (this means that Redis saves the date at which a key will expire).</span></span>

<span data-ttu-id="9ffc9-184">다음은 만료의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-184">Here is an example of an expiration:</span></span>

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

## <a name="accessing-a-redis-cache-from-a-client"></a><span data-ttu-id="9ffc9-185">클라이언트에서 Redis Cache에 액세스</span><span class="sxs-lookup"><span data-stu-id="9ffc9-185">Accessing a Redis cache from a client</span></span>

<span data-ttu-id="9ffc9-186">Azure Redis Cache 인스턴스에 연결하려면 일부 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-186">To connect to an Azure Redis Cache instance, you'll need several pieces of information.</span></span> <span data-ttu-id="9ffc9-187">클라이언트에는 캐시의 호스트 이름, 포트 및 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-187">Clients need the host name, port, and an access key for the cache.</span></span> <span data-ttu-id="9ffc9-188">이 정보는 Azure Portal의 **설정 > 액세스 키** 페이지에서 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-188">You can retrieve this information in the Azure portal through the **Settings > Access Keys** page.</span></span> 

- <span data-ttu-id="9ffc9-189">호스트 이름은 캐시 이름을 사용하여 만든 캐시의 공용 인터넷 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-189">The host name is the public Internet address of your cache, which was created using the name of the cache.</span></span> <span data-ttu-id="9ffc9-190">예: `sportsresults.redis.cache.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-190">For example `sportsresults.redis.cache.windows.net`.</span></span>

- <span data-ttu-id="9ffc9-191">액세스 키는 캐시의 암호 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-191">The access key acts as a password for your cache.</span></span> <span data-ttu-id="9ffc9-192">두 개의 키가 생성되는데, 하나는 기본 키이고 다른 하나는 보조 키입니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-192">There are two keys created: primary and secondary.</span></span> <span data-ttu-id="9ffc9-193">둘 중 어느 것이든 사용할 수 있으며, 기본 키를 변경해야 하는 경우에는 둘 다 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-193">You can use either key, two are provided in case you need to change the primary key.</span></span> <span data-ttu-id="9ffc9-194">모든 클라이언트를 보조 키로 전환하고, 기본 키를 다시 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-194">You can switch all of your clients to the secondary key, and regenerate the primary key.</span></span> <span data-ttu-id="9ffc9-195">이렇게 하면 원래 기본 키를 사용하는 응용 프로그램이 차단됩니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-195">This would block any applications using the original primary key.</span></span> <span data-ttu-id="9ffc9-196">개인 암호처럼 키를 주기적으로 다시 생성하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-196">Microsoft recommends periodically regenerating the keys - much like you would your personal passwords.</span></span>

> [!WARNING]
> <span data-ttu-id="9ffc9-197">액세스 키는 기밀 정보라고 생각하고 암호처럼 취급해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9ffc9-197">Your access keys should be considered confidential information, treat them like you would a password.</span></span> <span data-ttu-id="9ffc9-198">액세스 키를 갖고 있는 사람은 누구든지 캐시에서 모든 작업을 수행할 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="9ffc9-198">Anyone who has an access key can perform any operation on your cache!</span></span>
