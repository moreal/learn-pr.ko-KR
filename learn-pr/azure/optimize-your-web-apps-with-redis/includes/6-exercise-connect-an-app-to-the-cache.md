Azure에서 만든 Redis cache를 만들었으므로를 사용 하도록 응용 프로그램을 만들어 보겠습니다. Azure portal에서 연결 문자열 정보가 있는지 확인 합니다.

> [!NOTE]
> 통합 된 Cloud Shell은 오른쪽에 사용할 수 있습니다. 만들고 여기에서 우리가 제작 하려는 예제 코드를 실행 하는 명령 프롬프트를 사용 하거나 로컬로 개발 환경을 설정 해야 하는 경우 이러한 단계를 수행 수 있습니다. Cloud Shell을 사용 하려는 경우 선택 영역에 대 한 메시지가 표시 되는 경우 Bash 셸을 선택 하십시오.

## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

Redis 구현에 집중할 수 있도록 간단한 콘솔 응용 프로그램을 사용 하겠습니다.

1. Cloud Shell에 새.NET Core 콘솔 응용 프로그램을 만들기, 이름을 "SportsStatsTracker"

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. 이 프로젝트의 폴더, 계속 해 서를 만들고 현재 디렉터리를 변경 합니다.

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a>연결 문자열 추가

코드에 Azure portal에서 가져온 연결 문자열을 추가 해 보겠습니다. 소스 코드에서 다음과 같은 자격 증명을 저장 하지 마십시오. 간단히 유지 하기 위해이 샘플 구성 파일을 사용 하는 것이 하겠습니다. Azure에서 서버 쪽 응용 프로그램을 위한 더 나은 방법 인증서를 사용 하 여 Azure Key Vault를 사용 하는 것입니다.

1. 새 **appsettings.json** 파일을 프로젝트에 추가 합니다.

    ```bash
    touch appsettings.json
    ```

1. 입력 하 여 코드 편집기를 열고 `code .` 프로젝트 폴더에 있습니다. 로컬로 작업 하는 경우 사용 하는 것이 좋습니다 **Visual Studio Code**합니다. 여기에 나오는 단계의 사용 대부분 정렬 됩니다.

1. 선택 된 **appsettings.json** 편집기에서 파일을 다음 텍스트를 추가 합니다. 에 연결 문자열을 붙여 합니다 **값** 설정 합니다.

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. 파일 저장-온라인 편집기에서 일반적인 파일 작업에는 상단 오른쪽 모서리의 메뉴가입니다.

1. 프로젝트에 새 파일을 포함 하 고 출력 폴더에 복사 하려면 다음 구성 블록을 추가 합니다. 이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
       ...
        <ItemGroup>
            <None Update="appsettings.json">
              <CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
            </None>
        </ItemGroup>
    </Project>
    ```

1. 파일을 저장합니다. (이 작업을 수행 하거나 아래의 패키지를 추가 하면 변경 내용이 손실 됩니다 있는지 확인!)

## <a name="add-support-to-read-a-json-configuration-file"></a>JSON 구성 파일을 읽도록 지원 추가

.NET Core 응용 프로그램을 추가 NuGet 패키지는 JSON 구성 파일을 읽이 필요 합니다.

1. 명령 프롬프트 창의 섹션에서 참조를 추가 합니다 **Microsoft.Extensions.Configuration.Json** NuGet 패키지.

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a>구성 파일을 읽는 코드를 추가 합니다.

구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.

1. 선택 **Program.cs** 편집기에서.

1. 파일 맨 위에 **using System;** 줄이 표시됩니다. 해당 줄 아래에 다음 코드 줄을 추가합니다.

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. 내용을 대체 합니다 **Main** 메서드를 다음 코드로 합니다. 이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.

    ```csharp
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

**Program.cs** 파일은 이제 다음과 같이 표시됩니다.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace SportsStatsTracker
{
    class Program
    {
        static void Main(string[] args)
        {
            var config = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json")
                .Build();
        }
    }
}
```

## <a name="get-the-connection-string-from-configuration"></a>구성에서 연결 문자열 가져오기

1. **Program.cs**, 끝에 **Main** 메서드를 사용 하 여 새 **구성** 연결 문자열을 검색 하 고 새 변수에 저장 하는 변수  **connectionString**합니다.
    - 합니다 **config** 변수가 인덱서에서 검색할 문자열에 전달 될 수 있는 프로그램 **appSettings.json** 파일입니다.

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a>Redis 캐시.NET 클라이언트에 대 한 지원 추가

다음으로 사용 하 여 콘솔 응용 프로그램을 구성 하겠습니다 합니다 **StackExchange.Redis** .NET 용 클라이언트입니다.

1. 추가 된 **StackExchange.Redis** Cloud Shell 편집기의 맨 아래에서 명령 프롬프트를 사용 하 여 프로젝트에 NuGet 패키지.

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. 선택 **Program.cs** 편집기에서 추가 된 `using` 네임 스페이스에 대 한 **StackExchange.Redis**

    ```csharp
    using StackExchange.Redis;
    ```
    
설치가 완료 되 면 Redis 캐시 클라이언트는 프로젝트를 사용 하 여 사용할 수 있습니다.

## <a name="connect-to-the-cache"></a>캐시에 연결

캐시에 연결 하기 위한 코드를 추가 해 보겠습니다.

1. 선택 **Program.cs** 편집기에서.

1. 만들기는 `ConnectionMultiplexer` 를 사용 하 여 `ConnectionMultiplexer.Connect` 연결 문자열을 전달 하 여 합니다. 반환 된 값의 이름을 **캐시**합니다.

1. 만든된 연결 이므로 _일회용_를 래핑합니다를 `using` 블록입니다. 코드는 다음과 유사해야 합니다.

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> Azure Redis Cache에 연결 하 여 관리 되는 `ConnectionMultiplexer` 클래스입니다. 이 클래스는 클라이언트 응용 프로그램 전체에서 공유하고 다시 사용해야 합니다. 우리가 _되지_ 각 작업에 대 한 새 연결을 만들려면. 대신 하고자 클래스에서 필드로 해제 저장 하 고 각 작업에 다시 사용 합니다. 여기만 하겠습니다에서 사용 하는 **Main** 메서드 하지만 프로덕션 응용 프로그램에서 단일 클래스 필드에 저장 되어야 합니다.

## <a name="add-a-value-to-the-cache"></a>캐시에 값을 추가 합니다.

이제 연결 했으므로 캐시에 값을 추가 해 보겠습니다.

1. 내부를 `using` 연결이 만들어진 후 블록에서 사용 하 여는 `GetDatabase` 검색 하는 메서드는 `IDatabase` 인스턴스.

1. 호출 `StringSet` 에 `IDatabase` "일부 값" 키 "테스트: 키" 값으로 설정할 개체입니다.
    - 반환 값 `StringSet` 는 `bool` 는 키가 추가 되어 있는지 여부를 나타내는입니다.

1. 반환 값을 표시 `StringSet` 콘솔에 있습니다.

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a>캐시에서 값 가져오기

1. 다음으로 사용 하 여 값을 검색할 `StringGet`합니다. 이 키를 검색 하 고 값을 반환 합니다.

1. 반환된 된 값을 출력 합니다.

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 코드는 다음과 같습니다.

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;
    using StackExchange.Redis;
    
    namespace SportsStatsTracker
    {
        class Program
        {
            static void Main(string[] args)
            {
                var config = new ConfigurationBuilder()
                    .SetBasePath(Directory.GetCurrentDirectory())
                    .AddJsonFile("appsettings.json")
                    .Build();
    
                string connectionString = config["CacheConnection"];
    
                using (var cache = ConnectionMultiplexer.Connect(connectionString))
                {
                    var db = cache.GetDatabase();
    
                    bool setValue = db.StringSet("test:key", "some value");
                    Console.WriteLine($"SET: {setValue}");
    
                    string getValue = db.StringGet("test:key");
                    Console.WriteLine($"GET: {getValue}");
                }
            }
        }
    }
    ```
    
1. 결과를 보려면 응용 프로그램을 실행 합니다. 형식 `dotnet run` 편집기 아래의 터미널 창에 있습니다. 프로젝트 폴더에 빌드 및 실행 하는 코드를 찾지 못합니다 되었는지 확인 합니다.
    
    ```bash
    dotnet run
    ```
    
## <a name="use-the-async-versions-of-the-methods"></a>메서드의 비동기 버전을 사용 하 여

가져오기 및 캐시에서 값을 설정 하려면 연결할 수 있지만 이전 동기 버전을 사용 하는 것입니다. 서버 쪽 응용 프로그램에서 이러한 없는 스레드를 효율적으로 사용 합니다. 사용 하고자 하는 대신 합니다 _비동기_ 메서드의 버전입니다. 쉽게 확인할 수 있습니다-모두 끝날 **비동기**합니다.

이러한 메서드를 더 쉽게 작업을 사용할 수 있습니다. C# `async` 고 `await` 키워드입니다. 하지만 사용 해야 _적어도_ C# 7.1에 이러한 키워드를 적용할 수 있게 되기를 우리의 **Main** 메서드.

### <a name="switch-to-c-71"></a>C# 7.1로 전환

C#의 `async` 하 고 `await` 키워드의 유효한 키워드 없습니다 **Main** C# 7.1까지 메서드. 해당 컴파일러 플래그를 통해 쉽게 전환할 수 있습니다 합니다 **.csproj** 파일입니다.

1. 엽니다는 **SportsStatsTracker.csproj** 파일을 편집기에서.

1. 추가 `<LangVersion>7.1</LangVersion>` 첫 번째 `PropertyGroup` 빌드 파일에서입니다. 완료 했으면 다음과 같이 표시 됩니다.
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>Async 키워드를 적용 합니다.

다음에 적용 합니다 `async` 키워드를 합니다 **Main** 메서드. 세 가지를 수행 해야 합니다.

1. 추가 합니다 `async` 키워드에는 **Main** 메서드 시그니처입니다.
1. 반환 형식을 변경 `void` 에 `Task`입니다.
1. 추가 된 `using` 포함 하도록 문을 `System.Threading.Tasks`합니다.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using StackExchange.Redis;
using System.Threading.Tasks;

namespace SportsStatsTracker
{
    class Program
    {
        static async Task Main(string[] args)
        {
        ...
```

### <a name="get-and-set-values-asynchronously"></a>가져오기 및 값을 비동기적으로 설정

1. 사용 된 `StringSetAsync` 및 `StringGetAsync` 설정 하 고 키를 검색 하는 메서드 이름이 "counter"입니다. "100" 값을 설정 합니다.

1. 적용 된 `await` 키워드를 각 메서드에서 결과 가져옵니다.

1. 동기 버전과 마찬가지로 콘솔 창-결과 출력 합니다.

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 응용 프로그램을 다시 실행이 계속 작동 하 고 이제 다음 두 값 해야 합니다.

#### <a name="increment-the-value"></a>증분 값

1. 사용 된 `StringIncrementAsync` 증가 하는 방법에 **카운터** 값입니다. 번호를 전달 **50** 카운터를 추가 합니다.
    - 메서드는 키 _하 고_ 중 하나는 `long` 또는 `double`합니다.
    - 전달 된 매개 변수에 따라 반환 된 `long` 또는 `double`합니다.

1. 콘솔로 메서드의 결과 출력 합니다.

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a>기타 작업

마지막으로, 몇 가지 추가 메서드를 사용 하 여 실행 해 보겠습니다 시도 `ExecuteAsync` 지원 합니다.

1. 서버 연결을 테스트 하려면 "PING"를 실행 합니다. "퐁"를 사용 하 여 응답 해야 합니다.
1. "FLUSHDB"를 실행 합니다. 데이터베이스 값의 선택을 취소 합니다. "OK"로 응답 해야 합니다.

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

## <a name="challenge"></a>챌린지

으로 캐시에 개체 형식을 직렬화 하는 작업을 시도 합니다. 기본 단계는 다음과 같습니다.

1. 새 `class` 몇 가지 공용 속성을 사용 하 여 합니다. 자신만의 하나를 만들 수 있습니다 ("Person" 또는 "Car"은 인기 있는) 하거나 이전 단위에 제공 된 "GameStats" 예제를 사용 합니다.
1. 에 대 한 지원을 추가 합니다 **Newtonsoft.Json** NuGet 패키지를 사용 하 여 `dotnet add package`입니다.
1. 추가 된 `using` 에 대 한는 `Newtonsoft.Json` 네임 스페이스입니다.
1. 개체 중 하나를 만듭니다.
1. 사용 하 여 serialize `JsonConvert.SerializeObject` 사용 하 여 `StringSetAsync` 캐시로 푸시를 합니다.
1. 캐시에서 다시 가져와야 `StringGetAsync` 한 다음 사용 하 여 deserialize `JsonConvert.DeserializeObject<T>`합니다.

