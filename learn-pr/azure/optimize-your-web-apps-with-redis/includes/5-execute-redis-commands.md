<span data-ttu-id="44377-101">앞서 언급했듯이, Redis는 여러 서버 간에 복제할 수 있는 메모리 내 NoSQL 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-101">As mentioned earlier, Redis is an in-memory NoSQL database which can be replicated across multiple servers.</span></span> <span data-ttu-id="44377-102">종종 캐시로 사용되지만, 정식 데이터베이스 또는 심지어 메시지 broker로 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-102">It is often used as a cache, but can be used as a formal database or even message-broker.</span></span> 

<span data-ttu-id="44377-103">다양한 데이터 형식 및 구조를 저장할 수 있으며 캐시된 데이터 또는 캐시 자체에 대한 쿼리 정보를 검색하는 다양한 명령을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-103">It can store a variety of data types and structures and supports a variety of commands you can issue to retrieve cached data or query information about the cache itself.</span></span> <span data-ttu-id="44377-104">작업하는 데이터는 항상 키/값 쌍으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-104">The data you work with is always stored as key/value pairs.</span></span>

## <a name="executing-commands-on-the-redis-cache"></a><span data-ttu-id="44377-105">Redis 캐시에서 명령 실행</span><span class="sxs-lookup"><span data-stu-id="44377-105">Executing commands on the Redis cache</span></span>

<span data-ttu-id="44377-106">일반적으로 클라이언트 응용 프로그램은 _클라이언트 라이브러리_를 사용하여 요청을 작성하고 Redis 캐시에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-106">Typically, a client application will use a _client library_ to form requests and execute commands on a Redis cache.</span></span> <span data-ttu-id="44377-107">[Redis 클라이언트 페이지](https://redis.io/clients)에서 직접 클라이언트 라이브러리 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-107">You can get a list of client libraries directly from the [Redis clients page](https://redis.io/clients).</span></span> <span data-ttu-id="44377-108">.NET 언어를 위한 인기 있는 고성능 Redis 클라이언트는 **StackExchange.Redis**입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-108">A popular high-performance Redis client for the .NET language is **StackExchange.Redis**.</span></span> <span data-ttu-id="44377-109">패키지는 NuGet을 통해 사용할 수 있으며 명령줄 또는 IDE를 사용하여 .NET 코드에 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-109">The package is available through NuGet and can be added to your .NET code using the command line or IDE.</span></span>

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a><span data-ttu-id="44377-110">StackExchange.Redis를 사용하여 Redis 캐시에 연결</span><span class="sxs-lookup"><span data-stu-id="44377-110">Connecting to your Redis cache with StackExchange.Redis</span></span>

<span data-ttu-id="44377-111">Redis 서버에 연결할 때 호스트 주소, 포트 번호 및 액세스 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-111">Recall that we use the host address, port number, and an access key to connect to a Redis server.</span></span> <span data-ttu-id="44377-112">Azure는 일부 Redis 클라이언트에 이 데이터를 단일 문자열로 번들하는 _연결 문자열_도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-112">Azure also offers a _connection string_ for some Redis clients which bundles this data together into a single string.</span></span>

### <a name="what-is-a-connection-string"></a><span data-ttu-id="44377-113">연결 문자열이란 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="44377-113">What is a connection string?</span></span>

<span data-ttu-id="44377-114">연결 문자열은 Azure에서 Redis 캐시에 연결하고 인증하는 데 필요한 모든 정보 조각을 포함하고 있는 한 줄의 텍스트입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-114">A connection string is a single line of text that includes all the required pieces of information to connect and authenticate to a Redis cache in Azure.</span></span> <span data-ttu-id="44377-115">다음과 비슷합니다(**cache-name** 및 **password-here** 필드는 실제 값으로 채워짐).</span><span class="sxs-lookup"><span data-stu-id="44377-115">It will look something like the following (with the **cache-name** and **password-here** fields filled in with real values):</span></span>

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> <span data-ttu-id="44377-116">연결 문자열은 응용 프로그램 내에서 보호되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-116">The connection string should be protected in your application.</span></span> <span data-ttu-id="44377-117">응용 프로그램이 Azure에 호스트되는 경우 Azure Key Vault를 사용하여 값을 저장하는 방안을 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-117">If the application is hosted on Azure, consider using an Azure Key Vault to store the value.</span></span>

<span data-ttu-id="44377-118">이 문자열을 **StackExchange.Redis**로 전달하여 서버에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-118">You can pass this string to **StackExchange.Redis** to create a connection the server.</span></span> 

<span data-ttu-id="44377-119">끝부분에 두 개의 추가 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-119">Notice that there are two additional parameters at the end:</span></span> 

- <span data-ttu-id="44377-120">**ssl** - 통신이 암호화되도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-120">**ssl** - ensures that communication is encrypted.</span></span>
- <span data-ttu-id="44377-121">**abortConnection** - 특정 시점에서 서버를 사용할 수 없더라도 연결 생성을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-121">**abortConnection** - allows a connection to be created even if the server is unavailable at that moment.</span></span>

<span data-ttu-id="44377-122">그 외에도 문자열에 추가하여 클라이언트 라이브러리를 구성할 수 있는 여러 [선택적 매개 변수](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-122">There are several other [optional parameters](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options) you can append to the string to configure the client library.</span></span>

### <a name="creating-a-connection"></a><span data-ttu-id="44377-123">연결 만들기</span><span class="sxs-lookup"><span data-stu-id="44377-123">Creating a connection</span></span>

<span data-ttu-id="44377-124">**StackExchange.Redis**의 기본 연결 개체는 `StackExchange.Redis.ConnectionMultiplexer` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-124">The main connection object in **StackExchange.Redis** is the `StackExchange.Redis.ConnectionMultiplexer` class.</span></span> <span data-ttu-id="44377-125">이 개체는 Redis 서버(또는 서버 그룹)에 연결하는 프로세스를 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-125">This object abstracts the process of connecting to a Redis server (or group of servers).</span></span> <span data-ttu-id="44377-126">연결을 효율적으로 관리하도록 최적화되었으며 캐시에 액세스해야 하는 동안 유지하는 것이 목적입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-126">It's optimized to manage connections efficiently and intended to be kept around while you need access to the cache.</span></span>

<span data-ttu-id="44377-127">정적 `ConnectionMultiplexer.Connect` 또는 `ConnectionMultiplexer.ConnectAsync` 메서드를 사용하여 `ConnectionMultiplexer` 인스턴스를 만들고, 연결 문자열 또는 `ConfigurationOptions` 개체를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-127">You create a `ConnectionMultiplexer` instance using the static `ConnectionMultiplexer.Connect` or `ConnectionMultiplexer.ConnectAsync` method, passing in either a connection string or a `ConfigurationOptions` object.</span></span> 

<span data-ttu-id="44377-128">다음은 간단한 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-128">Here's a simple example:</span></span>

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

<span data-ttu-id="44377-129">`ConnectionMultiplexer`가 있으면 다음과 같은 3가지 기본 작업을 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-129">Once you have a `ConnectionMultiplexer`, there are 3 primary things you might want to do:</span></span>

1. <span data-ttu-id="44377-130">Redis 데이터베이스에 액세스.</span><span class="sxs-lookup"><span data-stu-id="44377-130">Access a Redis Database.</span></span> <span data-ttu-id="44377-131">여기서는 이 부분을 집중적으로 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-131">This is what we will focus on here.</span></span>
2. <span data-ttu-id="44377-132">Redis의 게시자/첨자 기능 사용.</span><span class="sxs-lookup"><span data-stu-id="44377-132">Make use of the publisher/subscript features of Redis.</span></span> <span data-ttu-id="44377-133">이 모듈의 범위를 벗어납니다.</span><span class="sxs-lookup"><span data-stu-id="44377-133">This is outside the scope of this module.</span></span>
3. <span data-ttu-id="44377-134">유지 관리 또는 모니터링을 위해 개별 서버에 액세스.</span><span class="sxs-lookup"><span data-stu-id="44377-134">Access an individual server for maintenance or monitoring purposes.</span></span>

### <a name="accessing-a-redis-database"></a><span data-ttu-id="44377-135">Redis 데이터베이스에 액세스</span><span class="sxs-lookup"><span data-stu-id="44377-135">Accessing a Redis database</span></span>

<span data-ttu-id="44377-136">Redis 데이터베이스는 `IDatabase` 형식으로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-136">The Redis database is represented by the `IDatabase` type.</span></span> <span data-ttu-id="44377-137">`GetDatabase()` 메서드를 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-137">You can retrieve one using the `GetDatabase()` method:</span></span>

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> <span data-ttu-id="44377-138">`GetDatabase`에서 반환된 개체는 경량의 개체이며 저장할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-138">The object returned from `GetDatabase` is a lightweight object, and does not need to be stored.</span></span> <span data-ttu-id="44377-139">`ConnectionMultiplexer`만 활성 상태로 유지하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-139">Only the `ConnectionMultiplexer` needs to be kept alive.</span></span>

<span data-ttu-id="44377-140">`IDatabase` 개체가 있으면 캐시와 상호 작용하는 메서드를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-140">Once you have a `IDatabase` object, you can execute methods to interact with the cache.</span></span> <span data-ttu-id="44377-141">모든 메서드는 `async` 및 `await` 키워드와 호환되도록 `Task` 개체를 반환하는 동기 및 비동기 버전을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-141">All methods have synchronous and asynchronous versions which return `Task` objects to make them compatible with the `async` and `await` keywords.</span></span>

<span data-ttu-id="44377-142">다음은 캐시에 키/값을 저장하는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-142">Here is an example of storing a key/value in the cache:</span></span>

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

<span data-ttu-id="44377-143">`StringSet` 메서드는 값이 설정되었는지(`true`) 아니면 설정되지 않았는지(`false`) 나타내는 `bool`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-143">The `StringSet` method returns a `bool` indicating whether the value was set (`true`) or not (`false`).</span></span> <span data-ttu-id="44377-144">그 후 `StringGet` 메서드를 사용하여 값을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-144">We can then retrieve the value with the `StringGet` method:</span></span>

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a><span data-ttu-id="44377-145">이진 값 가져오기 및 설정</span><span class="sxs-lookup"><span data-stu-id="44377-145">Getting and Setting binary values</span></span>

<span data-ttu-id="44377-146">Redis 키와 값은 _안전한 이진_입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-146">Recall that Redis keys and values are _binary safe_.</span></span> <span data-ttu-id="44377-147">이처럼 동일한 메서드를 사용하여 이진 데이터를 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-147">These same methods can be used to store binary data.</span></span> <span data-ttu-id="44377-148">데이터를 자연스럽게 작업할 수 있도록 `byte[]` 형식과 함께 작동하는 암시적 변환 연산자가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-148">There are implicit conversion operators to work with `byte[]` types so you can work with the data naturally:</span></span>

```csharp
byte[] key = ...;
byte[] value = ...;

db.StringSet(key, value);
```

```csharp
byte[] key = ...;
byte[] value = db.StringGet(key);
```

> [!TIP]
> <span data-ttu-id="44377-149">**StackExchange.Redis**는 `RedisKey` 형식을 사용하여 키를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="44377-149">**StackExchange.Redis** represents keys using the `RedisKey` type.</span></span> <span data-ttu-id="44377-150">이 클래스는 `string` 및 `byte[]`로 또는 그 반대로 암묵적 변환을 제공하며, 컴파일 없이 텍스트 및 이진 키를 모두 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-150">This class has implicit conversions to and from both `string` and `byte[]`, allowing both text and binary keys to be used without any complication.</span></span> <span data-ttu-id="44377-151">값은 `RedisValue` 형식으로 표현됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-151">Values are represented by the `RedisValue` type.</span></span> <span data-ttu-id="44377-152">`RedisKey`와 마찬가지로, `string` 또는 `byte[]`를 전달할 수 있도록 암시적 변환이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-152">As with `RedisKey`, there are implicit conversions in place to allow you to pass `string` or `byte[]`.</span></span>

#### <a name="other-common-operations"></a><span data-ttu-id="44377-153">기타 일반 작업</span><span class="sxs-lookup"><span data-stu-id="44377-153">Other common operations</span></span>

<span data-ttu-id="44377-154">`IDatabase` 인터페이스는 Redis 캐시와 함께 작동하는 여러 다른 메서드를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-154">The `IDatabase` interface includes several other methods to work with the Redis cache.</span></span> <span data-ttu-id="44377-155">해시, 목록, 집합 및 정렬된 집합과 함께 작동하는 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-155">There are methods to work with hashes, lists, sets, and ordered sets.</span></span>

<span data-ttu-id="44377-156">다음은 단일 키와 함께 작동하는 보다 일반적인 메서드이며, 전체 목록을 보려면 [소스 코드](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="44377-156">Here are some of the more common ones that work with single keys, you can [read the source code](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) for the interface to see the full list.</span></span>

| <span data-ttu-id="44377-157">메서드</span><span class="sxs-lookup"><span data-stu-id="44377-157">Method</span></span> | <span data-ttu-id="44377-158">설명</span><span class="sxs-lookup"><span data-stu-id="44377-158">Description</span></span> |
|--------|-------------|
| `CreateBatch` | <span data-ttu-id="44377-159">서버에 단일 단위로 전송되지만 반드시 단위로 처리되지는 않는 _작업 그룹_을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44377-159">Creates a _group of operations_ that will be sent to the server as a single unit, but not necessarily processed as a unit.</span></span> |
| `CreateTransaction` | <span data-ttu-id="44377-160">서버에 단일 단위로 전송되고 서버에서 단일 단위로 처리_되는_ 작업 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="44377-160">Creates a group of operations that will be sent to the server as a single unit _and_ processed on the server as a single unit.</span></span> |
| `KeyDelete` | <span data-ttu-id="44377-161">키/값을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-161">Delete the key/value.</span></span> |
| `KeyExists` | <span data-ttu-id="44377-162">지정된 키가 캐시에 있는지 여부를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-162">Returns whether the given key exists in cache.</span></span> |
| `KeyExpire` | <span data-ttu-id="44377-163">키에서 TTL(Time to Live) 만료를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-163">Sets a time-to-live (TTL) expiration on a key.</span></span> |
| `KeyRename` | <span data-ttu-id="44377-164">키의 이름을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="44377-164">Renames a key.</span></span> |
| `KeyTimeToLive` | <span data-ttu-id="44377-165">키의 TTL을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-165">Returns the TTL for a key.</span></span> |
| `KeyType` | <span data-ttu-id="44377-166">키에 저장된 값 형식의 문자열 표현을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-166">Returns the string representation of the type of the value stored at key.</span></span> <span data-ttu-id="44377-167">반환 가능한 형식은 문자열, 목록, 집합, zset 및 해시입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-167">The different types that can be returned are: string, list, set, zset and hash.</span></span> |
       
### <a name="executing-other-commands"></a><span data-ttu-id="44377-168">기타 명령 실행</span><span class="sxs-lookup"><span data-stu-id="44377-168">Executing other commands</span></span>

<span data-ttu-id="44377-169">`IDatabase` 개체는 텍스트 명령을 Redis 서버에 전달할 수 있는 `Execute` 및 `ExecuteAsync` 메서드를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-169">The `IDatabase` object has an `Execute` and `ExecuteAsync` method which can be used to pass textual commands to the Redis server.</span></span> <span data-ttu-id="44377-170">예:</span><span class="sxs-lookup"><span data-stu-id="44377-170">For example:</span></span>

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

<span data-ttu-id="44377-171">`Execute` 및 `ExecuteAsync` 메서드는 다음 두 속성을 포함하는 데이터 보유자인 `RedisResult` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="44377-171">The `Execute` and `ExecuteAsync` methods return a `RedisResult` object which is a data holder that includes two properties:</span></span>

- <span data-ttu-id="44377-172">"STRING", "INTEGER" 등 결과의 형식을 나타내는 `string`을 반환하는 `Type`.</span><span class="sxs-lookup"><span data-stu-id="44377-172">`Type` which returns a `string` indicating the type of the result - "STRING", "INTEGER", etc.</span></span>
- <span data-ttu-id="44377-173">결과가 `null`인 것을 감지하는 true/false 값인 `IsNull`.</span><span class="sxs-lookup"><span data-stu-id="44377-173">`IsNull` a true/false value to detect when the result is `null`.</span></span>

<span data-ttu-id="44377-174">`RedisResult`에서 `ToString()`을 사용하여 실제 반환 값을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-174">You can then use `ToString()` on the `RedisResult` to get the actual return value.</span></span>

<span data-ttu-id="44377-175">`Execute`를 사용하여 지원되는 명령을 수행할 수 있습니다. 예를 들어 캐시("클라이언트 목록")에 연결된 모든 클라이언트를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-175">You can use `Execute` to perform any supported commands - for example, we can get all the clients connected to the cache ("CLIENT LIST"):</span></span>

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

<span data-ttu-id="44377-176">이렇게 하면 연결된 모든 클라이언트가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-176">This would output all the connected clients:</span></span>

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a><span data-ttu-id="44377-177">좀 더 복잡한 값 저장</span><span class="sxs-lookup"><span data-stu-id="44377-177">Storing more complex values</span></span>
<span data-ttu-id="44377-178">Redis는 안전한 이진 문자열을 지향하지만, 텍스트 형식(일반적으로 XML 또는 JSON)으로 직렬화하여 개체 그래프를 캐시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-178">Redis is oriented around binary safe strings, but you can cache off object graphs by serializing them to a textual format - typically XML or JSON.</span></span> <span data-ttu-id="44377-179">예를 들어, 우리가 사용하는 통계의 `GameStats` 개체는 다음과 비슷할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="44377-179">For example, perhaps for our statistics, we have a `GameStats` object which looks like:</span></span>

```csharp
public class GameStat
{
    public string Id { get; set; }
    public string Sport { get; set; }
    public DateTimeOffset DatePlayed { get; set; }
    public string Game { get; set; }
    public IReadOnlyList<string> Teams { get; set; }
    public IReadOnlyList<(string team, int score)> Results { get; set; }

    public GameStat(string sport, DateTimeOffset datePlayed, string game, string[] teams, IEnumerable<(string team, int score)> results)
    {
        Id = Guid.NewGuid().ToString();
        Sport = sport;
        DatePlayed = datePlayed;
        Game = game;
        Teams = teams.ToList();
        Results = results.ToList();
    }

    public override string ToString()
    {
        return $"{Sport} {Game} played on {DatePlayed.Date.ToShortDateString()} - " +
               $"{String.Join(',', Teams)}\r\n\t" + 
               $"{String.Join('\t', Results.Select(r => $"{r.team } - {r.score}\r\n"))}";
    }
}
```

<span data-ttu-id="44377-180">**Newtonsoft.Json** 라이브러리를 사용하여 이 개체의 인스턴스를 문자열로 변환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-180">We could use the **Newtonsoft.Json** library to turn an instance of this object into a string:</span></span>

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

<span data-ttu-id="44377-181">역방향 프로세스를 사용하여 이 문자열을 검색하고 다시 개체로 되돌릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-181">We could retrieve it and turn it back into an object using the reverse process:</span></span>

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a><span data-ttu-id="44377-182">연결 정리</span><span class="sxs-lookup"><span data-stu-id="44377-182">Cleaning up the connection</span></span>
<span data-ttu-id="44377-183">Redis 연결이 끝나면 `ConnectionMultiplexer`를 **삭제**할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-183">Once you are done with the Redis connection, you can **Dispose** the `ConnectionMultiplexer`.</span></span> <span data-ttu-id="44377-184">그러면 모든 연결이 닫히고 서버와의 통신이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="44377-184">This will close all connections and shutdown the communication to the server.</span></span>

```csharp
redisConnection.Dispose();
redisConnection = null;
```

<span data-ttu-id="44377-185">응용 프로그램을 만들고 Redis 캐시로 간단한 작업을 수행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="44377-185">Let's create an application and do some simple work with our Redis cache.</span></span>