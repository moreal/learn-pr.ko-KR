앞서 언급했듯이, Redis는 여러 서버 간에 복제할 수 있는 메모리 내 NoSQL 데이터베이스입니다. 종종 캐시로 사용되지만, 정식 데이터베이스 또는 심지어 메시지 broker로 사용할 수도 있습니다. 

다양한 데이터 형식 및 구조를 저장할 수 있으며 캐시된 데이터 또는 캐시 자체에 대한 쿼리 정보를 검색하는 다양한 명령을 지원합니다. 작업하는 데이터는 항상 키/값 쌍으로 저장됩니다.

## <a name="executing-commands-on-the-redis-cache"></a>Redis 캐시에서 명령 실행

일반적으로 클라이언트 응용 프로그램은 _클라이언트 라이브러리_를 사용하여 요청을 작성하고 Redis 캐시에서 명령을 실행합니다. [Redis 클라이언트 페이지](https://redis.io/clients)에서 직접 클라이언트 라이브러리 목록을 가져올 수 있습니다. .NET 언어를 위한 인기 있는 고성능 Redis 클라이언트는 **StackExchange.Redis**입니다. 패키지는 NuGet을 통해 사용할 수 있으며 명령줄 또는 IDE를 사용하여 .NET 코드에 추가할 수 있습니다.

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a>StackExchange.Redis를 사용하여 Redis 캐시에 연결

Redis 서버에 연결할 때 호스트 주소, 포트 번호 및 액세스 키를 사용합니다. Azure는 일부 Redis 클라이언트에 이 데이터를 단일 문자열로 번들하는 _연결 문자열_도 제공합니다.

### <a name="what-is-a-connection-string"></a>연결 문자열이란 무엇일까요?

연결 문자열은 Azure에서 Redis 캐시에 연결하고 인증하는 데 필요한 모든 정보 조각을 포함하고 있는 한 줄의 텍스트입니다. 다음과 비슷합니다(**cache-name** 및 **password-here** 필드는 실제 값으로 채워짐).

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> 연결 문자열은 응용 프로그램 내에서 보호되어야 합니다. 응용 프로그램이 Azure에 호스트되는 경우 Azure Key Vault를 사용하여 값을 저장하는 방안을 고려해야 합니다.

이 문자열을 **StackExchange.Redis**로 전달하여 서버에 연결할 수 있습니다. 

끝부분에 두 개의 추가 매개 변수가 있습니다. 

- **ssl** - 통신이 암호화되도록 보장합니다.
- **abortConnection** - 특정 시점에서 서버를 사용할 수 없더라도 연결 생성을 허용합니다.

그 외에도 문자열에 추가하여 클라이언트 라이브러리를 구성할 수 있는 여러 [선택적 매개 변수](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options)가 있습니다.

### <a name="creating-a-connection"></a>연결 만들기

**StackExchange.Redis**의 기본 연결 개체는 `StackExchange.Redis.ConnectionMultiplexer` 클래스입니다. 이 개체는 Redis 서버(또는 서버 그룹)에 연결하는 프로세스를 추상화합니다. 연결을 효율적으로 관리하도록 최적화되었으며 캐시에 액세스해야 하는 동안 유지하는 것이 목적입니다.

정적 `ConnectionMultiplexer.Connect` 또는 `ConnectionMultiplexer.ConnectAsync` 메서드를 사용하여 `ConnectionMultiplexer` 인스턴스를 만들고, 연결 문자열 또는 `ConfigurationOptions` 개체를 전달합니다. 

다음은 간단한 예제입니다.

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

`ConnectionMultiplexer`가 있으면 다음과 같은 3가지 기본 작업을 수행하는 것이 좋습니다.

1. Redis 데이터베이스에 액세스. 여기서는 이 부분을 집중적으로 살펴보겠습니다.
2. Redis의 게시자/첨자 기능 사용. 이 모듈의 범위를 벗어납니다.
3. 유지 관리 또는 모니터링을 위해 개별 서버에 액세스.

### <a name="accessing-a-redis-database"></a>Redis 데이터베이스에 액세스

Redis 데이터베이스는 `IDatabase` 형식으로 표현됩니다. `GetDatabase()` 메서드를 사용하여 검색할 수 있습니다.

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> `GetDatabase`에서 반환된 개체는 경량의 개체이며 저장할 필요가 없습니다. `ConnectionMultiplexer`만 활성 상태로 유지하면 됩니다.

`IDatabase` 개체가 있으면 캐시와 상호 작용하는 메서드를 실행할 수 있습니다. 모든 메서드는 `async` 및 `await` 키워드와 호환되도록 `Task` 개체를 반환하는 동기 및 비동기 버전을 갖고 있습니다.

다음은 캐시에 키/값을 저장하는 예제입니다.

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

`StringSet` 메서드는 값이 설정되었는지(`true`) 아니면 설정되지 않았는지(`false`) 나타내는 `bool`을 반환합니다. 그 후 `StringGet` 메서드를 사용하여 값을 검색할 수 있습니다.

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a>이진 값 가져오기 및 설정

Redis 키와 값은 _안전한 이진_입니다. 이처럼 동일한 메서드를 사용하여 이진 데이터를 저장할 수 있습니다. 데이터를 자연스럽게 작업할 수 있도록 `byte[]` 형식과 함께 작동하는 암시적 변환 연산자가 있습니다.

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
> **StackExchange.Redis**는 `RedisKey` 형식을 사용하여 키를 나타냅니다. 이 클래스는 `string` 및 `byte[]`로 또는 그 반대로 암묵적 변환을 제공하며, 컴파일 없이 텍스트 및 이진 키를 모두 사용할 수 있습니다. 값은 `RedisValue` 형식으로 표현됩니다. `RedisKey`와 마찬가지로, `string` 또는 `byte[]`를 전달할 수 있도록 암시적 변환이 제공됩니다.

#### <a name="other-common-operations"></a>기타 일반 작업

`IDatabase` 인터페이스는 Redis 캐시와 함께 작동하는 여러 다른 메서드를 포함하고 있습니다. 해시, 목록, 집합 및 정렬된 집합과 함께 작동하는 메서드가 있습니다.

다음은 단일 키와 함께 작동하는 보다 일반적인 메서드이며, 전체 목록을 보려면 [소스 코드](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs)를 참조하세요.

| 메서드 | 설명 |
|--------|-------------|
| `CreateBatch` | 서버에 단일 단위로 전송되지만 반드시 단위로 처리되지는 않는 _작업 그룹_을 만듭니다. |
| `CreateTransaction` | 서버에 단일 단위로 전송되고 서버에서 단일 단위로 처리_되는_ 작업 그룹을 만듭니다. |
| `KeyDelete` | 키/값을 삭제합니다. |
| `KeyExists` | 지정된 키가 캐시에 있는지 여부를 반환합니다. |
| `KeyExpire` | 키에서 TTL(Time to Live) 만료를 설정합니다. |
| `KeyRename` | 키의 이름을 바꿉니다. |
| `KeyTimeToLive` | 키의 TTL을 반환합니다. |
| `KeyType` | 키에 저장된 값 형식의 문자열 표현을 반환합니다. 반환 가능한 형식은 문자열, 목록, 집합, zset 및 해시입니다. |
       
### <a name="executing-other-commands"></a>기타 명령 실행

`IDatabase` 개체는 텍스트 명령을 Redis 서버에 전달할 수 있는 `Execute` 및 `ExecuteAsync` 메서드를 갖고 있습니다. 예:

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

`Execute` 및 `ExecuteAsync` 메서드는 다음 두 속성을 포함하는 데이터 보유자인 `RedisResult` 개체를 반환합니다.

- "STRING", "INTEGER" 등 결과의 형식을 나타내는 `string`을 반환하는 `Type`.
- 결과가 `null`인 것을 감지하는 true/false 값인 `IsNull`.

`RedisResult`에서 `ToString()`을 사용하여 실제 반환 값을 가져올 수 있습니다.

`Execute`를 사용하여 지원되는 명령을 수행할 수 있습니다. 예를 들어 캐시("클라이언트 목록")에 연결된 모든 클라이언트를 가져올 수 있습니다.

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

이렇게 하면 연결된 모든 클라이언트가 출력됩니다.

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a>좀 더 복잡한 값 저장
Redis는 안전한 이진 문자열을 지향하지만, 텍스트 형식(일반적으로 XML 또는 JSON)으로 직렬화하여 개체 그래프를 캐시할 수 있습니다. 예를 들어, 우리가 사용하는 통계의 `GameStats` 개체는 다음과 비슷할 것입니다.

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

**Newtonsoft.Json** 라이브러리를 사용하여 이 개체의 인스턴스를 문자열로 변환할 수 있습니다.

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

역방향 프로세스를 사용하여 이 문자열을 검색하고 다시 개체로 되돌릴 수 있습니다.

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a>연결 정리
Redis 연결이 끝나면 `ConnectionMultiplexer`를 **삭제**할 수 있습니다. 그러면 모든 연결이 닫히고 서버와의 통신이 종료됩니다.

```csharp
redisConnection.Dispose();
redisConnection = null;
```

응용 프로그램을 만들고 Redis 캐시로 간단한 작업을 수행하겠습니다.