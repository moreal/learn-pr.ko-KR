Azure에서 만든 Redis 캐시가 있으니, 이 캐시를 사용할 응용 프로그램을 만들어 보겠습니다. Azure Portal에서 연결 문자열 정보가 있는지 확인합니다.

> [!NOTE]
> 통합 Cloud Shell은 오른쪽에서 사용할 수 있습니다. 여기서 우리가 작성하려는 예제 코드를 만들고 실행하는 명령 프롬프트를 사용하거나, .NET Core 개발 환경을 설정한 경우 로컬로 다음 단계를 수행합니다.

## <a name="create-a-console-application"></a>콘솔 응용 프로그램 만들기

Redis 구현에 집중할 수 있도록 간단한 콘솔 응용 프로그램을 사용하겠습니다.

1. Cloud Shell에서 새 .NET Core 콘솔 응용 프로그램을 만들고 이름을 "SportsStatsTracker"로 지정합니다.

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. 그러면 프로젝트의 폴더가 생성됩니다. 현재 디렉터리를 변경합니다.

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a>연결 문자열 추가

Azure Portal에서 얻은 연결 문자열을 코드에 추가하겠습니다. 이와 같은 자격 증명을 절대로 소스 코드에 저장하지 마세요. 이 샘플이 복잡해지지 않도록, 구성 파일을 사용하겠습니다. Azure의 서버 쪽 응용 프로그램에 접근하는 보다 효과적인 방법은 인증서와 함께 Azure Key Vault를 사용하는 것입니다.

1. 프로젝트에 추가할 새 **appsettings.json** 파일을 만듭니다.

    ```bash
    touch appsettings.json
    ```

1. 프로젝트 폴더에 `code .`를 입력하여 코드 편집기를 엽니다. 로컬로 작업하는 경우 **Visual Studio Code**를 사용하는 것이 좋습니다. 여기에 나오는 단계는 대부분 사용법과 일치합니다.

1. 편집기에서 **appsettings.json** 파일을 선택하고 다음 텍스트를 추가합니다. 연결 문자열을 설정의 **값**에 붙여넣습니다.

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. 변경 내용을 저장합니다.

    > [!IMPORTANT]
    > 편집기에서 파일에 코드를 붙여넣거나 코드를 변경할 때마다 "..." 메뉴 또는 바로 가기 키(Windows 및 Linux는 <kbd>Ctrl+S</kbd>, macOS는 <kbd>Cmd+S</kbd>)를 사용하여 저장하세요.

1. 편집기에서 **SportsStatsTracker.csproj** 파일을 클릭하여 엽니다.

1. `<Project>` 루트 요소에 다음 `<ItemGroup>` 구성 블록을 추가하여 프로젝트에 새 파일을 포함하고 출력 폴더에 복사합니다. 이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.

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

1. 파일을 저장합니다. (반드시 이 작업을 수행해야 합니다. 그렇지 않으면 아래의 패키지를 추가할 때 변경 내용이 손실됩니다!)

## <a name="add-support-to-read-a-json-configuration-file"></a>JSON 구성 파일을 읽도록 지원 추가

.NET Core 응용 프로그램을 사용하려면 JSON 구성 파일을 읽을 NuGet 패키지가 필요합니다.

1. 창의 명령 프롬프트 섹션에서 **Microsoft.Extensions.Configuration.Json** NuGet 패키지 참조를 추가합니다.

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a>구성 파일을 읽는 코드 추가

구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.

1. 편집기에서 **Program.cs**를 선택합니다.

1. 파일 맨 위에 `using System` 줄이 표시됩니다. 해당 줄 아래에 다음 코드 줄을 추가합니다.

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. **Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다. 이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.

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

1. **Program.cs**의 **Main** 메서드 끝부분에서, 연결 문자열을 검색한 후 **connectionString**이라는 새 변수에 저장하는 새 **config** 변수를 사용합니다.
    - **config** 변수는 **appSettings.json** 파일에서 검색하는 문자열을 전달할 수 있는 인덱서를 갖고 있습니다.

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a>Redis 캐시 .NET 클라이언트에 대한 지원 추가

다음으로, .NET용 **StackExchange.Redis** 클라이언트를 사용하도록 콘솔 응용 프로그램을 구성하겠습니다.

1. Cloud Shell 편집기의 맨 아래에서 명령 프롬프트를 사용하여 프로젝트에 **StackExchange.Redis** NuGet 패키지를 추가합니다.

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. 편집기에서 **Program.cs**를 선택하고 **StackExchange.Redis** 네임스페이스에 대한 `using`을 추가합니다.

    ```csharp
    using StackExchange.Redis;
    ```
    
설치가 완료되면 Redis 캐시 클라이언트를 프로젝트에 사용할 수 있습니다.

## <a name="connect-to-the-cache"></a>캐시에 연결

캐시에 연결하는 코드를 추가하겠습니다.

1. 편집기에서 **Program.cs**를 선택합니다.

1. 연결 문자열로 전달하여 `ConnectionMultiplexer.Connect`를 통해 `ConnectionMultiplexer`를 만듭니다. 반환된 값의 이름을 **캐시**로 지정합니다.

1. 생성된 연결은 _일회용_이므로 `using` 블록에 래핑합니다. 코드는 다음과 유사해야 합니다.

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> Azure Redis Cache 연결은 `ConnectionMultiplexer` 클래스로 관리됩니다. 이 클래스는 클라이언트 응용 프로그램 전체에서 공유하고 다시 사용해야 합니다. 각 작업에 대해 새 연결을 만들지 _않겠습니다_. 그 대신, 클래스에서 필드로 저장하고 각 작업에 다시 사용할 것입니다. 여기서는 **Main** 메서드에만 사용할 예정이지만, 프로덕션 응용 프로그램에서는 클래스 필드 또는 싱글톤에 저장해야 합니다.

## <a name="add-a-value-to-the-cache"></a>캐시에 값 추가

연결이 설정되었으니, 캐시에 값을 추가하겠습니다.

1. 연결을 만든 후 `using` 블록 내부에서 `GetDatabase` 메서드를 사용하여 `IDatabase` 인스턴스를 검색합니다.

1. `IDatabase` 개체에서 `StringSet`을 호출하여 "test:key" 키를 "some value" 값으로 설정합니다.
    - `StringSet`에서 반환된 값은 키의 추가 여부를 나타내는 `bool`입니다.

1. `StringSet`의 반환 값을 콘솔에 표시합니다.

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a>캐시에서 값 가져오기

1. 다음으로, `StringGet`을 사용하여 값을 검색합니다. 이 작업에는 값을 검색하고 반환하는 키가 필요합니다.

1. 반환된 값을 출력합니다.

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 코드는 다음과 비슷합니다.

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
    
1. 응용 프로그램을 실행하여 결과를 봅니다. 편집기 아래의 터미널 창에 `dotnet run`을 입력합니다. 프로젝트 폴더에 있어야 합니다. 그렇지 않으면 편집기에서 빌드 및 실행하는 코드를 찾지 못합니다.
    
    ```bash
    dotnet run
    ```
    
> [!TIP] 
> 프로그램이 예상대로 작동하지 않지만 컴파일되기는 하는 경우 편집기에서 변경 내용을 저장하지 않은 것일 수 있습니다. 터미널과 편집기 창 사이에서 전환할 때 항상 변경 내용을 저장해야 합니다. 

## <a name="use-the-async-versions-of-the-methods"></a>메서드의 비동기 버전 사용

캐시에서 값을 가져오고 설정할 수 있었지만, 기존의 동기 버전을 사용 중입니다. 서버 쪽 응용 프로그램에서는 스레드를 효율적으로 사용하는 방법이 아닙니다. 그 대신 메서드의 _비동기_ 버전을 사용하겠습니다. 비동기 버전은 모두 **Async**로 끝나기 때문에 쉽게 찾을 수 있습니다.

C# `async` 및 `await` 키워드를 사용하면 이러한 메서드를 좀 더 쉽게 작업할 수 있습니다. 하지만 **Main** 메서드에 이러한 키워드를 적용하려면 C# 7.1 _이상_을 사용해야 합니다.

### <a name="switch-to-c-71"></a>C# 7.1로 전환

C#의 `async` 및 `await` 키워드는 C# 7.1까지는 **Main** 메서드에서 유효한 키워드가 아니었습니다. **.csproj** 파일의 플래그를 통해 해당 컴파일러로 쉽게 전환할 수 있습니다.

1. 편집기에서 **SportsStatsTracker.csproj** 파일을 엽니다.

1. 빌드 파일에서 첫 번째 `PropertyGroup`에 `<LangVersion>7.1</LangVersion>`을 추가합니다. 완성된 최종 상태는 다음과 비슷합니다.
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a>비동기 키워드 적용

다음으로, **Main** 메서드에 `async` 키워드를 적용합니다. 세 가지를 수행해야 합니다.

1. **Main** 메서드 서명에 `async` 키워드를 추가합니다.
1. 반환 형식을 `void`에서 `Task`로 변경합니다.
1. `System.Threading.Tasks`를 포함하도록 `using` 문을 추가합니다.

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

### <a name="get-and-set-values-asynchronously"></a>비동기적으로 값을 가져오고 설정

동기 메서드를 그대로 둘 수도 있지만, 캐시에 또 다른 값을 추가하는 `StringSetAsync` 및 `StringGetAsync` 메서드 호출을 추가해 보겠습니다. "카운터" 값을 "100"으로 설정합니다.  

1. `StringSetAsync` 및 `StringGetAsync` 메서드를 사용하여 "카운터"라는 키를 설정하고 검색합니다. 값을 "100"으로 설정합니다.

1. 각 메서드에서 결과를 가져오도록 `await` 키워드를 적용합니다.

1. 동기 버전과 마찬가지로 콘솔 창에 결과를 출력합니다.

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. 응용 프로그램을 다시 실행합니다. 응용 프로그램은 여전히 작동하며 이제 두 개의 값을 갖고 있습니다.

#### <a name="increment-the-value"></a>값 증가

1. `StringIncrementAsync` 메서드를 사용하여 **카운터** 값을 증가시킵니다. 카운터에 추가할 숫자 **50**을 전달합니다.
    - 이 메서드는 _and_ 키와 `long` 또는 `double` 키를 사용합니다.
    - 전달된 매개 변수에 따라 `long` 또는 `double`을 반환합니다.

1. 메서드 결과를 콘솔로 출력합니다.

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a>기타 작업

마지막으로, `ExecuteAsync` 지원을 사용하여 몇 가지 추가 메서드를 실행해 보겠습니다.

1. 서버 연결을 테스트하는 "PING"을 실행합니다. "PONG"으로 응답해야 합니다.
1. 데이터베이스 값을 지우는 "FLUSHDB"를 실행합니다. "OK"로 응답해야 합니다.

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

최종 코드는 다음과 유사해야 합니다.

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

                setValue = await db.StringSetAsync("test", "100");
                Console.WriteLine($"SET: {setValue}");

                getValue = await db.StringGetAsync("test");
                Console.WriteLine($"GET: {getValue}");

                var result = await db.ExecuteAsync("ping");
                Console.WriteLine($"PING = {result.Type} : {result}");
                
                result = await db.ExecuteAsync("flushdb");
                Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
            }
        }
    }
}
```

## <a name="challenge"></a>과제

여러분에게 드리는 과제로, 개체 형식을 캐시로 직렬화해보세요. 기본 단계는 다음과 같습니다.

1. 몇 가지 공용 속성을 사용하여 새 `class`를 만듭니다. 자신만의 클래스를 만들어도 되고(인기 있는 클래스는 "사람" 또는 "자동차"), 이전 모듈에 제공된 "GameStats" 예제를 사용해도 됩니다.

1. `dotnet add package`를 사용하여 **Newtonsoft.Json** NuGet 패키지에 대한 지원을 추가합니다.

1. `Newtonsoft.Json` 네임스페이스에 대한 `using`을 추가합니다.

1. 개체 중 하나를 만듭니다.

1. `JsonConvert.SerializeObject`를 사용하여 개체를 직렬화하고 `StringSetAsync`를 사용하여 캐시로 푸시합니다.

1. `StringGetAsync`를 사용하여 캐시에서 다시 가져온 후 `JsonConvert.DeserializeObject<T>`를 사용하여 deserialize합니다.

