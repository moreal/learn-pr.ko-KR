앞에서 설명한 대로 Redis 여러 서버 간에 복제할 수 있는 메모리 내 NoSQL 데이터베이스입니다. 캐시에 사용 되는 경우가 있지만 정식 데이터베이스 또는 심지어 메시지 브로커도 사용할 수 있습니다. 

다양 한 데이터 형식 및 구조를 저장할 수 있습니다 하 고 다양 한 캐시 자체에 대 한 캐시 된 데이터 또는 쿼리 정보를 검색 하는 동안 실행할 수 있습니다 하는 명령 지원 합니다. 사용 하 여 작업 하는 데이터는 항상 키/값 쌍으로 저장 됩니다.

## <a name="executing-commands-on-the-redis-cache"></a>Redis cache에서 명령을 실행

클라이언트 응용 프로그램을 사용 하는 일반적으로 _클라이언트 라이브러리_ 요청 하는 Redis cache에서 명령을 실행 합니다. 클라이언트 라이브러리에서 직접 목록을 가져올 수 있습니다 합니다 [Redis 클라이언트 페이지](https://redis.io/clients)합니다. .NET 언어를 위한 인기 있는 고성능 Redis 클라이언트는 **StackExchange.Redis**입니다. 패키지가는 NuGet을 통해 사용할 수 있으며 명령줄 또는 IDE를 사용 하 여.NET 코드에 추가할 수 있습니다.

### <a name="connecting-to-your-redis-cache-with-stackexchangeredis"></a>StackExchange.Redis 사용 하 여 Redis cache에 연결

Redis 서버에 연결할 호스트 주소, 포트 번호 및 액세스 키를 사용 하는 회수 합니다. 또한 azure 제공을 _연결 문자열_ 일부 Redis 클라이언트는 단일 문자열에이 데이터를 함께 번들에 대 한 합니다.

### <a name="what-is-a-connection-string"></a>연결 문자열 이란?

연결 문자열은 모든 필요한 가지 연결 하 여 azure에서 Redis cache에 대 한 인증 정보를 포함 하는 텍스트 한 줄. 다음과 같이 표시 됩니다 (사용 하 여 합니다 **캐시 이름** 하 고 **암호 여기** 실제 값으로 채워진 필드):

```
[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False
```

> [!TIP]
> 연결 문자열은 응용 프로그램에서 보호 되어야 합니다. 응용 프로그램이 Azure에서 호스트 되는 경우에 Azure Key Vault를 사용 하 여 값을 저장 하는 것이 좋습니다.

이 문자열을 전달할 수 있습니다 **StackExchange.Redis** 서버 연결을 만들려고 합니다. 

끝에 두 개의 추가 매개 변수가 있는지 확인 합니다. 

- **ssl** -통신이 암호화 됨을 보장 합니다.
- **abortConnection** -특정 시점에서 서버를 사용할 수 없는 경우에 만들 수에 대 한 연결을 허용 합니다.

몇 가지 다른 [선택적 매개 변수](https://github.com/StackExchange/StackExchange.Redis/blob/master/docs/Configuration.md#configuration-options) 클라이언트 라이브러리를 구성 하는 문자열에 추가할 수 있습니다.

### <a name="creating-a-connection"></a>연결 만들기

기본 연결 개체 **StackExchange.Redis** 되는 `StackExchange.Redis.ConnectionMultiplexer` 클래스입니다. 이 개체는 Redis 서버 (또는 서버 그룹)에 연결 하는 프로세스를 추상화 합니다. 액세스에 최적화 된 연결을 효율적으로 관리 하 고 캐시에 액세스 해야 하는 동안 유지 되어야 하는 데 있습니다.

만든를 `ConnectionMultiplexer` 정적을 사용 하 여 인스턴스 `ConnectionMultiplexer.Connect` 또는 `ConnectionMultiplexer.ConnectAsync` 하거나 연결 문자열을 전달 하는 메서드 또는 `ConfigurationOptions` 개체입니다. 

간단한 예는 다음과 같습니다.

```csharp
using StackExchange.Redis;
...
var connectionString = "[cache-name].redis.cache.windows.net:6380,password=[password-here],ssl=True,abortConnect=False";
var redisConnection = ConnectionMultiplexer.Connect(connectionString);
    // ^^^ store and re-use this!!!
```

만든 후는 `ConnectionMultiplexer`, 가지 3 기본 작업을 수행 하는 것이 좋습니다.

1. Redis 데이터베이스에 액세스 합니다. 여기에 맞게 중점적입니다.
2. 확인의 Redis 게시자/첨자 기능을 사용 합니다. 이이 모듈의 범위를 벗어납니다.
3. 유지 관리 또는 모니터링을 위해 개별 서버에 액세스 합니다.

### <a name="accessing-a-redis-database"></a>Redis 데이터베이스 액세스

Redis 데이터베이스는 표현 된 `IDatabase` 형식입니다. 사용 하 여 검색할 수 있습니다는 `GetDatabase()` 메서드:

```csharp
IDatabase db = redisConnection.GetDatabase();
```

> [!TIP]
> 반환 되는 개체 `GetDatabase` 경량 개체 이며 저장할 필요가 없습니다. 만 `ConnectionMultiplexer` 활성 상태로 유지 해야 합니다.

만든 후를 `IDatabase` 개체를 캐시와 상호 작용 하는 메서드를 실행할 수 있습니다. 모든 메서드를 반환 하는 동기 및 비동기 버전을 보유 `Task` 개체를 사용 하 여 호환 되는 `async` 및 `await` 키워드입니다.

캐시에 키/값을 저장 하는 예는 다음과 같습니다.

```csharp
bool wasSet = db.StringSet("favorite:flavor", "i-love-rocky-road");
```

합니다 `StringSet` 메서드가 반환 되는 `bool` 값이 설정 되었는지 여부를 나타내는 (`true`) 여부 (`false`). 다음 값을 검색할 수는 `StringGet` 메서드:

```csharp
string value = db.StringGet("favorite:flavor");
Console.WriteLine(value); // displays: ""i-love-rocky-road""
```

#### <a name="getting-and-setting-binary-values"></a>가져오기 및 이진 값 설정

Redis 키와 값이는 회수 _안전한 이진_합니다. 이진 데이터를 저장 하려면 동일한 메서드를 사용할 수 있습니다. 암시적 변환 연산자를 사용 하려면 가지 `byte[]` 자연스럽 게 데이터를 사용 하 여 작업할 수 있도록 형식:

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
> **StackExchange.Redis** 를 사용 하 여 키를 나타내는 `RedisKey` 형식입니다. 이 클래스는 둘 다의 암시적 변환 `string` 고 `byte[]`, 텍스트 및 이진을 모두 키 모든 complication 없이 사용할 수 있습니다. 값은 표시 되는 `RedisValue` 형식입니다. 와 마찬가지로 `RedisKey`에 전달할 수 있도록 할에서의 암시적 변환은 `string` 또는 `byte[]`합니다.

#### <a name="other-common-operations"></a>다른 일반적인 작업

`IDatabase` 인터페이스 Redis cache를 사용 하려면 몇 가지 다른 방법도 포함 되어 있습니다. 가지 해시, 목록, 집합 및 정렬 된 집합을 사용 하는 방법이 있습니다.

다음은 단일 키를 사용 하는 흔한 문제 중 일부를 할 수 있습니다 [소스 코드를 읽기](https://github.com/StackExchange/StackExchange.Redis/blob/master/src/StackExchange.Redis/Interfaces/IDatabase.cs) 전체 목록을 보려면 인터페이스에 대 한 합니다.

| 방법 | 설명 |
|--------|-------------|
| `CreateBatch` | 만듭니다는 _작업 그룹_ 하나의 단위로 서버로 전송 되지만 반드시 하나의 단위로 처리 됩니다 하는 합니다. |
| `CreateTransaction` | 하나의 단위로 서버로 전송 될 작업 그룹을 만듭니다 _고_ 단일 단위로 서버에서 처리 합니다. |
| `KeyDelete` | 키/값을 삭제 합니다. |
| `KeyExists` | 지정된 된 키 캐시에 있는지 여부를 반환 합니다. |
| `KeyExpire` | 키에 대 한 활성 시간 (TTL) 만료를 설정합니다. |
| `KeyRename` | 키를 이름을 바꿉니다. |
| `KeyTimeToLive` | 키에 대 한 TTL을 반환합니다. |
| `KeyType` | 키에 저장 된 값 형식의 문자열 표현을 반환 합니다. 반환 될 수 있는 다른 형식은: 문자열, 목록, zset 및 해시를 설정 합니다. |
       
### <a name="executing-other-commands"></a>다른 명령을 실행합니다.

합니다 `IDatabase` 개체에는 `Execute` 및 `ExecuteAsync` 텍스트 명령을 Redis 서버에 전달 하는 메서드. 예: 

```csharp
var result = db.Execute("ping");
Console.WriteLine(result.ToString()); // displays: "PONG"
```

`Execute` 하 고 `ExecuteAsync` 메서드는 반환을 `RedisResult` 두 속성을 포함 하는 데이터 보유자 인 개체:

- `Type` 반환 하는 한 `string` 결과-"STRING", "INTEGER" 등의 형식을 나타내는입니다.
- `IsNull` 결과 시기를 감지 하는 true/false 값 `null`합니다.

사용할 수 있습니다 `ToString()` 에 `RedisResult` 가져오려면 실제 값을 반환 합니다.

사용할 수 있습니다 `Execute` 수행 하려면 지원 되는 명령-예를 들어, 캐시 ("클라이언트 목록")에 연결 된 모든 클라이언트 가져올 수 있습니다.

```csharp
var result = await db.ExecuteAsync("client", "list");
Console.WriteLine($"Type = {result.Type}\r\nResult = {result}");
```

이 연결된 된 모든 클라이언트 출력 됩니다.

```output
Type = BulkString
Result = id=9469 addr=16.183.122.154:54961 fd=18 name=DESKTOP-AAAAAA age=0 idle=0 flags=N db=0 sub=1 psub=0 multi=-1 qbuf=0 qbuf-free=0 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=subscribe numops=5
id=9470 addr=16.183.122.155:54967 fd=13 name=DESKTOP-BBBBBB age=0 idle=0 flags=N db=0 sub=0 psub=0 multi=-1 qbuf=0 qbuf-free=32768 obl=0 oll=0 omem=0 ow=0 owmem=0 events=r cmd=client numops=17
```

### <a name="storing-more-complex-values"></a>더 복잡 한 값 저장
Redis는 이진 안전한 문자열을 지향 하지만 캐시할 수 있습니다 개체 그래프 해제-일반적으로 텍스트 형식으로 직렬화 하 여 XML 또는 JSON입니다. 예를 들어, 아마도 통계에 대 한 것을 `GameStats` 개체과 같은 형식입니다.

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

사용할 수는 **Newtonsoft.Json** 문자열로이 개체의 인스턴스를 설정 하려면 라이브러리:

```csharp
var stat = new GameStat("Soccer", new DateTime(1950, 7, 16), "FIFA World Cup", 
                new[] { "Uruguay", "Brazil" },
                new[] { ("Uruguay", 2), ("Brazil", 1) });

string serializedValue = Newtonsoft.Json.JsonConvert.SerializeObject(stat);
bool added = db.StringSet("event:1950-world-cup", serializedValue);
```

검색 하 고 역 프로세스를 사용 하 여 개체를 다시 설정할 수 있었습니다.

```csharp
var result = db.StringGet("event:1950-world-cup");
var stat = Newtonsoft.Json.JsonConvert.DeserializeObject<GameStat>(result.ToString());
Console.WriteLine(stat.Sport); // displays "Soccer"
```

## <a name="cleaning-up-the-connection"></a>연결을 정리
Redis 연결이 끝나면 있습니다 **Dispose** 는 `ConnectionMultiplexer`합니다. 모든 연결 및 서버 통신이 종료 닫힙니다.

```csharp
redisConnection.Dispose();
redisConnection = null;
```

응용 프로그램을 만들고이 Redis cache 사용 하 여 간단한 작업을 수행 하겠습니다.