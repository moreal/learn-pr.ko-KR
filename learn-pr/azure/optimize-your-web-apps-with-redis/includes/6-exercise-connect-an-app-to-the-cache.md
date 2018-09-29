<span data-ttu-id="6d333-101">Azure에서 만든 Redis 캐시가 있으니, 이 캐시를 사용할 응용 프로그램을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-101">Now that we have a Redis cache created in Azure, let's create an application to use it.</span></span> <span data-ttu-id="6d333-102">Azure Portal에서 연결 문자열 정보가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-102">Make sure you have your connection string information from the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="6d333-103">통합 Cloud Shell은 오른쪽에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-103">The integrated Cloud Shell is available on the right.</span></span> <span data-ttu-id="6d333-104">여기서 우리가 작성하려는 예제 코드를 만들고 실행하는 명령 프롬프트를 사용하거나, .NET Core 개발 환경을 설정한 경우 로컬로 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-104">You can use that command prompt to create and run the example code we are building here, or perform these steps locally if you have a .NET Core development environment setup.</span></span>

## <a name="create-a-console-application"></a><span data-ttu-id="6d333-105">콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="6d333-105">Create a Console Application</span></span>

<span data-ttu-id="6d333-106">Redis 구현에 집중할 수 있도록 간단한 콘솔 응용 프로그램을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-106">We'll use a simple Console Application so we can focus on the Redis implementation.</span></span>

1. <span data-ttu-id="6d333-107">Cloud Shell에서 새 .NET Core 콘솔 응용 프로그램을 만들고 이름을 "SportsStatsTracker"로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-107">In the Cloud Shell, create a new .NET Core Console Application, name it "SportsStatsTracker"</span></span>

    ```bash
    dotnet new console --name SportsStatsTracker
    ```
    
1. <span data-ttu-id="6d333-108">그러면 프로젝트의 폴더가 생성됩니다. 현재 디렉터리를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-108">This will create a folder for the project, go ahead and change the current directory.</span></span>

    ```bash
    cd SportsStatsTracker
    ```
    
## <a name="add-the-connection-string"></a><span data-ttu-id="6d333-109">연결 문자열 추가</span><span class="sxs-lookup"><span data-stu-id="6d333-109">Add the connection string</span></span>

<span data-ttu-id="6d333-110">Azure Portal에서 얻은 연결 문자열을 코드에 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-110">Let's add the connection string we got from the Azure portal into the code.</span></span> <span data-ttu-id="6d333-111">이와 같은 자격 증명을 절대로 소스 코드에 저장하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="6d333-111">Never store credentials like this in your source code.</span></span> <span data-ttu-id="6d333-112">이 샘플이 복잡해지지 않도록, 구성 파일을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-112">To keep this sample simple, we're going to use a configuration file.</span></span> <span data-ttu-id="6d333-113">Azure의 서버 쪽 응용 프로그램에 접근하는 보다 효과적인 방법은 인증서와 함께 Azure Key Vault를 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-113">A better approach for a server-side application in Azure would be to use Azure Key Vault with certificates.</span></span>

1. <span data-ttu-id="6d333-114">프로젝트에 추가할 새 **appsettings.json** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-114">Create a new **appsettings.json** file to add to the project.</span></span>

    ```bash
    touch appsettings.json
    ```

1. <span data-ttu-id="6d333-115">프로젝트 폴더에 `code .`를 입력하여 코드 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-115">Open the code editor by typing `code .` in the project folder.</span></span> <span data-ttu-id="6d333-116">로컬로 작업하는 경우 **Visual Studio Code**를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-116">If you are working locally, we recommend using **Visual Studio Code**.</span></span> <span data-ttu-id="6d333-117">여기에 나오는 단계는 대부분 사용법과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-117">The steps here will mostly align with it's usage.</span></span>

1. <span data-ttu-id="6d333-118">편집기에서 **appsettings.json** 파일을 선택하고 다음 텍스트를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-118">Select the **appsettings.json** file in the editor and add the following text.</span></span> <span data-ttu-id="6d333-119">연결 문자열을 설정의 **값**에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-119">Paste your connection string into the **value** of the setting.</span></span>

    ```json
    {
      "CacheConnection": "[value-goes-here]"
    }
    ```

1. <span data-ttu-id="6d333-120">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-120">Save the changes.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6d333-121">편집기에서 파일에 코드를 붙여넣거나 코드를 변경할 때마다 "..." 메뉴 또는 바로 가기 키(Windows 및 Linux는 <kbd>Ctrl+S</kbd>, macOS는 <kbd>Cmd+S</kbd>)를 사용하여 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="6d333-121">Whenever you paste or change code into a file in the editor, make sure to save afterwards using the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="6d333-122">편집기에서 **SportsStatsTracker.csproj** 파일을 클릭하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-122">Click on the **SportsStatsTracker.csproj** file in the editor to open it.</span></span>

1. <span data-ttu-id="6d333-123">`<Project>` 루트 요소에 다음 `<ItemGroup>` 구성 블록을 추가하여 프로젝트에 새 파일을 포함하고 출력 폴더에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-123">Add the following `<ItemGroup>` configuration block into the root `<Project>` element to include the new file in the project and copy it to the output folder.</span></span> <span data-ttu-id="6d333-124">이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-124">This ensures that the app configuration file is placed in the output directory when the app is compiled/built.</span></span>

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

1. <span data-ttu-id="6d333-125">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-125">Save the file.</span></span> <span data-ttu-id="6d333-126">(반드시 이 작업을 수행해야 합니다. 그렇지 않으면 아래의 패키지를 추가할 때 변경 내용이 손실됩니다!)</span><span class="sxs-lookup"><span data-stu-id="6d333-126">(Make sure you do this or you will lose the change when you add the package below!)</span></span>

## <a name="add-support-to-read-a-json-configuration-file"></a><span data-ttu-id="6d333-127">JSON 구성 파일을 읽도록 지원 추가</span><span class="sxs-lookup"><span data-stu-id="6d333-127">Add support to read a JSON configuration file</span></span>

<span data-ttu-id="6d333-128">.NET Core 응용 프로그램을 사용하려면 JSON 구성 파일을 읽을 NuGet 패키지가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-128">A .NET Core application requires additional NuGet packages to read a JSON configuration file.</span></span>

1. <span data-ttu-id="6d333-129">창의 명령 프롬프트 섹션에서 **Microsoft.Extensions.Configuration.Json** NuGet 패키지 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-129">In the command prompt section of the window, add a reference to the  **Microsoft.Extensions.Configuration.Json** NuGet package.</span></span>

    ```bash
    dotnet add package Microsoft.Extensions.Configuration.Json
    ```

## <a name="add-code-to-read-the-configuration-file"></a><span data-ttu-id="6d333-130">구성 파일을 읽는 코드 추가</span><span class="sxs-lookup"><span data-stu-id="6d333-130">Add code to read the configuration file</span></span>

<span data-ttu-id="6d333-131">구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-131">Now that we have added the required libraries to enable reading configuration, we need to enable that functionality within our console application.</span></span>

1. <span data-ttu-id="6d333-132">편집기에서 **Program.cs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-132">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="6d333-133">파일 맨 위에 `using System` 줄이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-133">At the top of the file, a `using System` line is present.</span></span> <span data-ttu-id="6d333-134">해당 줄 아래에 다음 코드 줄을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-134">Underneath that line, add the following lines of code:</span></span>

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. <span data-ttu-id="6d333-135">**Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-135">Replace the contents of the **Main** method with the following code.</span></span> <span data-ttu-id="6d333-136">이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-136">This code initializes the configuration system to read from the **appsettings.json** file.</span></span>

    ```csharp
    var config = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json")
        .Build();
    ```

<span data-ttu-id="6d333-137">**Program.cs** 파일은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-137">Your **Program.cs** file should now look like the following:</span></span>

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

## <a name="get-the-connection-string-from-configuration"></a><span data-ttu-id="6d333-138">구성에서 연결 문자열 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d333-138">Get the connection string from configuration</span></span>

1. <span data-ttu-id="6d333-139">**Program.cs**의 **Main** 메서드 끝부분에서, 연결 문자열을 검색한 후 **connectionString**이라는 새 변수에 저장하는 새 **config** 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-139">In **Program.cs**, at the end of the **Main** method, use the new **config** variable to retrieve the connection string and store it in a new variable named **connectionString**.</span></span>
    - <span data-ttu-id="6d333-140">**config** 변수는 **appSettings.json** 파일에서 검색하는 문자열을 전달할 수 있는 인덱서를 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-140">The **config** variable has an indexer where you can pass in a string to retrieve from your **appSettings.json** file.</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    ```
    
## <a name="add-support-for-the-redis-cache-net-client"></a><span data-ttu-id="6d333-141">Redis 캐시 .NET 클라이언트에 대한 지원 추가</span><span class="sxs-lookup"><span data-stu-id="6d333-141">Add support for the Redis cache .NET client</span></span>

<span data-ttu-id="6d333-142">다음으로, .NET용 **StackExchange.Redis** 클라이언트를 사용하도록 콘솔 응용 프로그램을 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-142">Next, let's configure the console application to use the **StackExchange.Redis** client for .NET.</span></span>

1. <span data-ttu-id="6d333-143">Cloud Shell 편집기의 맨 아래에서 명령 프롬프트를 사용하여 프로젝트에 **StackExchange.Redis** NuGet 패키지를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-143">Add the **StackExchange.Redis** NuGet package to the project using the command prompt at the bottom of the Cloud Shell editor.</span></span>

    ```bash
    dotnet add package StackExchange.Redis
    ```

1. <span data-ttu-id="6d333-144">편집기에서 **Program.cs**를 선택하고 **StackExchange.Redis** 네임스페이스에 대한 `using`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-144">Select **Program.cs** in the editor and add a `using` for the namespace **StackExchange.Redis**</span></span>

    ```csharp
    using StackExchange.Redis;
    ```
    
<span data-ttu-id="6d333-145">설치가 완료되면 Redis 캐시 클라이언트를 프로젝트에 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-145">Once the installation is completed, the Redis cache client is available to use with your project.</span></span>

## <a name="connect-to-the-cache"></a><span data-ttu-id="6d333-146">캐시에 연결</span><span class="sxs-lookup"><span data-stu-id="6d333-146">Connect to the cache</span></span>

<span data-ttu-id="6d333-147">캐시에 연결하는 코드를 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-147">Let's add the code to connect to the cache.</span></span>

1. <span data-ttu-id="6d333-148">편집기에서 **Program.cs**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-148">Select **Program.cs** in the editor.</span></span>

1. <span data-ttu-id="6d333-149">연결 문자열로 전달하여 `ConnectionMultiplexer.Connect`를 통해 `ConnectionMultiplexer`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-149">Create a `ConnectionMultiplexer` using `ConnectionMultiplexer.Connect` by passing it your connection string.</span></span> <span data-ttu-id="6d333-150">반환된 값의 이름을 **캐시**로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-150">Name the returned value **cache**.</span></span>

1. <span data-ttu-id="6d333-151">생성된 연결은 _일회용_이므로 `using` 블록에 래핑합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-151">Since the created connection is _disposable_, wrap it in a `using` block.</span></span> <span data-ttu-id="6d333-152">코드는 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-152">Your code should look something like:</span></span>

    ```csharp
    string connectionString = config["CacheConnection"];
    
    using (var cache = ConnectionMultiplexer.Connect(connectionString))
    {
        
    }
    ```

> [!NOTE] 
> <span data-ttu-id="6d333-153">Azure Redis Cache 연결은 `ConnectionMultiplexer` 클래스로 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-153">The connection to Azure Redis Cache is managed by the `ConnectionMultiplexer` class.</span></span> <span data-ttu-id="6d333-154">이 클래스는 클라이언트 응용 프로그램 전체에서 공유하고 다시 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-154">This class should be shared and reused throughout your client application.</span></span> <span data-ttu-id="6d333-155">각 작업에 대해 새 연결을 만들지 _않겠습니다_.</span><span class="sxs-lookup"><span data-stu-id="6d333-155">We do _not_ want to create a new connection for each operation.</span></span> <span data-ttu-id="6d333-156">그 대신, 클래스에서 필드로 저장하고 각 작업에 다시 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-156">Instead, we want to store it off as a field in our class and reuse it for each operation.</span></span> <span data-ttu-id="6d333-157">여기서는 **Main** 메서드에만 사용할 예정이지만, 프로덕션 응용 프로그램에서는 클래스 필드 또는 싱글톤에 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-157">Here we are only going to use it in the **Main** method, but in a production application, it should be stored in a class field, or a singleton.</span></span>

## <a name="add-a-value-to-the-cache"></a><span data-ttu-id="6d333-158">캐시에 값 추가</span><span class="sxs-lookup"><span data-stu-id="6d333-158">Add a value to the cache</span></span>

<span data-ttu-id="6d333-159">연결이 설정되었으니, 캐시에 값을 추가하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-159">Now that we have the connection, let's add a value to the cache.</span></span>

1. <span data-ttu-id="6d333-160">연결을 만든 후 `using` 블록 내부에서 `GetDatabase` 메서드를 사용하여 `IDatabase` 인스턴스를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-160">Inside the `using` block after the connection has been created, use the `GetDatabase` method to retrieve an `IDatabase` instance.</span></span>

1. <span data-ttu-id="6d333-161">`IDatabase` 개체에서 `StringSet`을 호출하여 "test:key" 키를 "some value" 값으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-161">Call `StringSet` on the `IDatabase` object to set the key "test:key" to the value "some value".</span></span>
    - <span data-ttu-id="6d333-162">`StringSet`에서 반환된 값은 키의 추가 여부를 나타내는 `bool`입니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-162">the return value from `StringSet` is a `bool` indicating whether the key was added.</span></span>

1. <span data-ttu-id="6d333-163">`StringSet`의 반환 값을 콘솔에 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-163">Display the return value from `StringSet` onto the console.</span></span>

    ```csharp
    bool setValue = db.StringSet("test:key", "some value");
    Console.WriteLine($"SET: {setValue}");
    ```
    
## <a name="get-a-value-from-the-cache"></a><span data-ttu-id="6d333-164">캐시에서 값 가져오기</span><span class="sxs-lookup"><span data-stu-id="6d333-164">Get a value from the cache</span></span>

1. <span data-ttu-id="6d333-165">다음으로, `StringGet`을 사용하여 값을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-165">Next, retrieve the value using `StringGet`.</span></span> <span data-ttu-id="6d333-166">이 작업에는 값을 검색하고 반환하는 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-166">This takes the key to retrieve and returns the value.</span></span>

1. <span data-ttu-id="6d333-167">반환된 값을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-167">Output the returned value.</span></span>

    ```csharp
    string getValue = db.StringGet("test:key");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="6d333-168">코드는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-168">Your code should look like this:</span></span>

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
    
1. <span data-ttu-id="6d333-169">응용 프로그램을 실행하여 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-169">Run the application to see the result.</span></span> <span data-ttu-id="6d333-170">편집기 아래의 터미널 창에 `dotnet run`을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-170">Type `dotnet run` into the terminal window below the editor.</span></span> <span data-ttu-id="6d333-171">프로젝트 폴더에 있어야 합니다. 그렇지 않으면 편집기에서 빌드 및 실행하는 코드를 찾지 못합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-171">Make sure you are in the project folder or it won't find your code to build and run.</span></span>
    
    ```bash
    dotnet run
    ```
    
> [!TIP] 
> <span data-ttu-id="6d333-172">프로그램이 예상대로 작동하지 않지만 컴파일되기는 하는 경우 편집기에서 변경 내용을 저장하지 않은 것일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-172">If the program doesn't do what you expect, but compiles, it may be because you have not saved changes in the editor.</span></span> <span data-ttu-id="6d333-173">터미널과 편집기 창 사이에서 전환할 때 항상 변경 내용을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-173">Always remember to save changes as you switch between the terminal and the editor windows</span></span> 

## <a name="use-the-async-versions-of-the-methods"></a><span data-ttu-id="6d333-174">메서드의 비동기 버전 사용</span><span class="sxs-lookup"><span data-stu-id="6d333-174">Use the async versions of the methods</span></span>

<span data-ttu-id="6d333-175">캐시에서 값을 가져오고 설정할 수 있었지만, 기존의 동기 버전을 사용 중입니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-175">We have been able to get and set values from the cache, but we are using the older synchronous versions.</span></span> <span data-ttu-id="6d333-176">서버 쪽 응용 프로그램에서는 스레드를 효율적으로 사용하는 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-176">In server-side applications, these are not an efficient use of our threads.</span></span> <span data-ttu-id="6d333-177">그 대신 메서드의 _비동기_ 버전을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-177">Instead, we want to use the _asynchronous_ versions of the methods.</span></span> <span data-ttu-id="6d333-178">비동기 버전은 모두 **Async**로 끝나기 때문에 쉽게 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-178">You can easily spot them - they all end in **Async**.</span></span>

<span data-ttu-id="6d333-179">C# `async` 및 `await` 키워드를 사용하면 이러한 메서드를 좀 더 쉽게 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-179">To make these methods easy to work with, we can use the C# `async` and `await` keywords.</span></span> <span data-ttu-id="6d333-180">하지만 **Main** 메서드에 이러한 키워드를 적용하려면 C# 7.1 _이상_을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-180">However, we will need to be using _at least_ C# 7.1 to be able to apply these keywords to our **Main** method.</span></span>

### <a name="switch-to-c-71"></a><span data-ttu-id="6d333-181">C# 7.1로 전환</span><span class="sxs-lookup"><span data-stu-id="6d333-181">Switch to C# 7.1</span></span>

<span data-ttu-id="6d333-182">C#의 `async` 및 `await` 키워드는 C# 7.1까지는 **Main** 메서드에서 유효한 키워드가 아니었습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-182">C#'s `async` and `await` keywords were not valid keywords in **Main** methods until C# 7.1.</span></span> <span data-ttu-id="6d333-183">**.csproj** 파일의 플래그를 통해 해당 컴파일러로 쉽게 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-183">We can easily switch to that compiler through a flag in the **.csproj** file.</span></span>

1. <span data-ttu-id="6d333-184">편집기에서 **SportsStatsTracker.csproj** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-184">Open the **SportsStatsTracker.csproj** file in the editor.</span></span>

1. <span data-ttu-id="6d333-185">빌드 파일에서 첫 번째 `PropertyGroup`에 `<LangVersion>7.1</LangVersion>`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-185">Add `<LangVersion>7.1</LangVersion>` into the first `PropertyGroup` in the build file.</span></span> <span data-ttu-id="6d333-186">완성된 최종 상태는 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-186">It should look like the following when you are finished.</span></span>
    
    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
    
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <TargetFramework>netcoreapp2.0</TargetFramework>
        <LangVersion>7.1</LangVersion> 
      </PropertyGroup>
    ...
    ```
    
### <a name="apply-the-async-keyword"></a><span data-ttu-id="6d333-187">비동기 키워드 적용</span><span class="sxs-lookup"><span data-stu-id="6d333-187">Apply the async keyword</span></span>

<span data-ttu-id="6d333-188">다음으로, **Main** 메서드에 `async` 키워드를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-188">Next, apply the `async` keyword to the **Main** method.</span></span> <span data-ttu-id="6d333-189">세 가지를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-189">We will have to do three things.</span></span>

1. <span data-ttu-id="6d333-190">**Main** 메서드 서명에 `async` 키워드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-190">Add the `async` keyword onto the **Main** method signature.</span></span>
1. <span data-ttu-id="6d333-191">반환 형식을 `void`에서 `Task`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-191">Change the return type from `void` to `Task`.</span></span>
1. <span data-ttu-id="6d333-192">`System.Threading.Tasks`를 포함하도록 `using` 문을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-192">Add a `using` statement to include `System.Threading.Tasks`.</span></span>

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

### <a name="get-and-set-values-asynchronously"></a><span data-ttu-id="6d333-193">비동기적으로 값을 가져오고 설정</span><span class="sxs-lookup"><span data-stu-id="6d333-193">Get and set values asynchronously</span></span>

<span data-ttu-id="6d333-194">동기 메서드를 그대로 둘 수도 있지만, 캐시에 또 다른 값을 추가하는 `StringSetAsync` 및 `StringGetAsync` 메서드 호출을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-194">We can leave the synchronous methods in place, let's add a call to the `StringSetAsync` and `StringGetAsync` methods to add another value to the cache.</span></span> <span data-ttu-id="6d333-195">"카운터" 값을 "100"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-195">Set "counter" to the value "100".</span></span>  

1. <span data-ttu-id="6d333-196">`StringSetAsync` 및 `StringGetAsync` 메서드를 사용하여 "카운터"라는 키를 설정하고 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-196">Use the `StringSetAsync` and `StringGetAsync` methods to set and retrieve a key named "counter".</span></span> <span data-ttu-id="6d333-197">값을 "100"으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-197">Set the value to "100".</span></span>

1. <span data-ttu-id="6d333-198">각 메서드에서 결과를 가져오도록 `await` 키워드를 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-198">Apply the `await` keyword to get the results from each method.</span></span>

1. <span data-ttu-id="6d333-199">동기 버전과 마찬가지로 콘솔 창에 결과를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-199">Output the results to the console window - just as you did with the synchronous versions.</span></span>

    ```csharp
    // Simple get and put of integral data types into the cache
    setValue = await db.StringSetAsync("test", "100");
    Console.WriteLine($"SET: {setValue}");
    
    getValue = await db.StringGetAsync("test");
    Console.WriteLine($"GET: {getValue}");
    ```
    
1. <span data-ttu-id="6d333-200">응용 프로그램을 다시 실행합니다. 응용 프로그램은 여전히 작동하며 이제 두 개의 값을 갖고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-200">Run the application again - it should still work and now have two values.</span></span>

#### <a name="increment-the-value"></a><span data-ttu-id="6d333-201">값 증가</span><span class="sxs-lookup"><span data-stu-id="6d333-201">Increment the value</span></span>

1. <span data-ttu-id="6d333-202">`StringIncrementAsync` 메서드를 사용하여 **카운터** 값을 증가시킵니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-202">Use the `StringIncrementAsync` method to increment your **counter** value.</span></span> <span data-ttu-id="6d333-203">카운터에 추가할 숫자 **50**을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-203">Pass the number **50** to add to the counter.</span></span>
    - <span data-ttu-id="6d333-204">이 메서드는 _and_ 키와 `long` 또는 `double` 키를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-204">Notice that the method takes the key _and_ either a `long` or `double`.</span></span>
    - <span data-ttu-id="6d333-205">전달된 매개 변수에 따라 `long` 또는 `double`을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-205">Depending on the parameters passed, it either returns a `long` or `double`.</span></span>

1. <span data-ttu-id="6d333-206">메서드 결과를 콘솔로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-206">Output the results of the method to the console.</span></span>

    ```csharp
    long newValue = await db.StringIncrementAsync("counter", 50);
    Console.WriteLine($"INCR new value = {newValue}");
    ```
    
## <a name="other-operations"></a><span data-ttu-id="6d333-207">기타 작업</span><span class="sxs-lookup"><span data-stu-id="6d333-207">Other operations</span></span>

<span data-ttu-id="6d333-208">마지막으로, `ExecuteAsync` 지원을 사용하여 몇 가지 추가 메서드를 실행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-208">Finally, let's try executing a few additional methods with the `ExecuteAsync` support.</span></span>

1. <span data-ttu-id="6d333-209">서버 연결을 테스트하는 "PING"을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-209">Execute "PING" to test the server connection.</span></span> <span data-ttu-id="6d333-210">"PONG"으로 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-210">It should respond with "PONG".</span></span>
1. <span data-ttu-id="6d333-211">데이터베이스 값을 지우는 "FLUSHDB"를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-211">Execute "FLUSHDB" to clear the database values.</span></span> <span data-ttu-id="6d333-212">"OK"로 응답해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-212">It should respond with "OK".</span></span>

```csharp
var result = await db.ExecuteAsync("ping");
Console.WriteLine($"PING = {result.Type} : {result}");

result = await db.ExecuteAsync("flushdb");
Console.WriteLine($"FLUSHDB = {result.Type} : {result}");
```

<span data-ttu-id="6d333-213">최종 코드는 다음과 유사해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-213">The final code should look something like:</span></span>

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

## <a name="challenge"></a><span data-ttu-id="6d333-214">과제</span><span class="sxs-lookup"><span data-stu-id="6d333-214">Challenge</span></span>

<span data-ttu-id="6d333-215">여러분에게 드리는 과제로, 개체 형식을 캐시로 직렬화해보세요.</span><span class="sxs-lookup"><span data-stu-id="6d333-215">As a challenge, try serializing an object type to the cache.</span></span> <span data-ttu-id="6d333-216">기본 단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-216">Here are the basic steps.</span></span>

1. <span data-ttu-id="6d333-217">몇 가지 공용 속성을 사용하여 새 `class`를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-217">Create a new `class` with some public properties.</span></span> <span data-ttu-id="6d333-218">자신만의 클래스를 만들어도 되고(인기 있는 클래스는 "사람" 또는 "자동차"), 이전 모듈에 제공된 "GameStats" 예제를 사용해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-218">You can invent one of your own ("Person" or "Car" are popular), or use the "GameStats" example given in the previous unit.</span></span>

1. <span data-ttu-id="6d333-219">`dotnet add package`를 사용하여 **Newtonsoft.Json** NuGet 패키지에 대한 지원을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-219">Add support for the **Newtonsoft.Json** NuGet package using `dotnet add package`.</span></span>

1. <span data-ttu-id="6d333-220">`Newtonsoft.Json` 네임스페이스에 대한 `using`을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-220">Add a `using` for the `Newtonsoft.Json` namespace.</span></span>

1. <span data-ttu-id="6d333-221">개체 중 하나를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-221">Create one of your objects.</span></span>

1. <span data-ttu-id="6d333-222">`JsonConvert.SerializeObject`를 사용하여 개체를 직렬화하고 `StringSetAsync`를 사용하여 캐시로 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-222">Serialize it with `JsonConvert.SerializeObject` and use `StringSetAsync` to push it into the cache.</span></span>

1. <span data-ttu-id="6d333-223">`StringGetAsync`를 사용하여 캐시에서 다시 가져온 후 `JsonConvert.DeserializeObject<T>`를 사용하여 deserialize합니다.</span><span class="sxs-lookup"><span data-stu-id="6d333-223">Get it back from the cache with `StringGetAsync` and then deserialize it with `JsonConvert.DeserializeObject<T>`.</span></span>

