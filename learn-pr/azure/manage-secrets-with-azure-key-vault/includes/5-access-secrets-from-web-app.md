<span data-ttu-id="87a87-101">이제 Azure 리소스에 관리 ID를 사용하도록 설정하여 앱이 인증에 사용할 ID를 만드는 방법을 알고 있으므로 자격 증명 모음의 비밀에 액세스하는 데 해당 ID를 사용하는 앱을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-101">Now that you know how enabling managed identities for Azure resources creates an identity for our app to use for authentication, we'll create an app that uses that identity to access secrets in the vault.</span></span>

## <a name="reading-secrets-in-an-aspnet-core-app"></a><span data-ttu-id="87a87-102">ASP.NET Core 앱에서 비밀 읽기</span><span class="sxs-lookup"><span data-stu-id="87a87-102">Reading secrets in an ASP.NET Core app</span></span>

<span data-ttu-id="87a87-103">Azure Key Vault API는 키 및 자격 증명 모음의 모든 관리와 사용을 처리하는 REST API입니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-103">The Azure Key Vault API is a REST API that handles all management and usage of keys and vaults.</span></span> <span data-ttu-id="87a87-104">자격 증명 모음의 각 비밀에는 고유한 URL이 있으며 비밀 값은 HTTP GET 요청으로 검색됩니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-104">Each secret in a vault has a unique URL, and secret values are retrieved with HTTP GET requests.</span></span>

<span data-ttu-id="87a87-105">.NET Core의 공식 Key Vault 클라이언트 라이브러리는 Microsoft.Azure.KeyVault NuGet 패키지의 `KeyVaultClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-105">The official Key Vault client library for .NET Core is the `KeyVaultClient` class in the Microsoft.Azure.KeyVault NuGet package.</span></span> <span data-ttu-id="87a87-106">이를 직접 사용할 필요가 없습니다. ASP.NET Core의 `AddAzureKeyVault` 메서드를 사용하여 자격 증명 모음의 모든 비밀을 시작 시 구성 API로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-106">You don't need to use it directly, though &mdash; with ASP.NET Core's `AddAzureKeyVault` method, you can load all the secrets from a vault into the Configuration API at startup.</span></span> <span data-ttu-id="87a87-107">이 방법을 사용하면 구성의 나머지 부분에 사용하는 것과 동일한 `IConfiguration` 인터페이스를 사용하여 이름별로 모든 비밀에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-107">This technique enables you to access all of your secrets by name using the same `IConfiguration` interface you use for the rest of your configuration.</span></span> <span data-ttu-id="87a87-108">`AddAzureKeyVault`를 사용하는 앱에는 자격 증명 모음에 대한 **Get** 및 **List** 권한이 둘 다 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-108">Apps that use `AddAzureKeyVault` require both **Get** and **List** permissions to the vault.</span></span>

> [!TIP]
> <span data-ttu-id="87a87-109">앱을 빌드하는 데 사용하는 프레임워크나 언어와 관계없이, 특별한 이유가 없는 한 비밀 값을 로컬로 캐시하거나 비밀을 시작 시 메모리에 로드하도록 설계해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-109">Regardless of the framework or language you use to build your app, you should design it to cache secret values locally or load them into memory at startup unless you have a specific reason not to.</span></span> <span data-ttu-id="87a87-110">필요할 때마다 자격 증명 모음에서 직접 비밀을 읽으면 불필요하게 속도가 느려지고 비용이 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-110">Reading them directly from the vault every time you need them is unnecessarily slow and expensive.</span></span>

<span data-ttu-id="87a87-111">`AddAzureKeyVault`에는 자격 증명 모음 이름만 입력으로 필요하며 이 이름은 로컬 앱 구성에서 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-111">`AddAzureKeyVault` only requires the vault name as an input, which we'll get from our local app configuration.</span></span> <span data-ttu-id="87a87-112">또한 관리 ID 인증을 자동으로 처리합니다. Azure 리소스에 대한 관리 ID를 사용하도록 설정된 Azure App Service에 배포된 앱에서 사용될 경우 관리 ID 토큰 서비스를 검색하고 이를 사용하여 인증합니다.&mdash;</span><span class="sxs-lookup"><span data-stu-id="87a87-112">It also automatically handles managed identity authentication &mdash; when used in an app deployed to Azure App Service with managed identities for Azure resources enabled, it will detect the managed identities token service and use it to authenticate.</span></span> <span data-ttu-id="87a87-113">대부분의 시나리오에 적합하고 모든 모범 사례를 구현하며, 이 단원의 연습에서 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-113">It's a good fit for most scenarios and implements all best practices, and we'll use it in this unit's exercise.</span></span>

## <a name="handling-secrets-in-an-app"></a><span data-ttu-id="87a87-114">앱에서 비밀 처리</span><span class="sxs-lookup"><span data-stu-id="87a87-114">Handling secrets in an app</span></span>

<span data-ttu-id="87a87-115">비밀이 앱에 로드되면 앱이 비밀을 안전하게 처리하도록 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-115">Once a secret is loaded into your app, it's up to your app to handle it securely.</span></span> <span data-ttu-id="87a87-116">이 모듈에서 빌드하는 앱에서는 클라이언트 응답에 대한 비밀 값을 기록하고 웹 브라우저에 비밀 값을 표시하여 성공적으로 로드되었음을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-116">In the app we build in this module, we write our secret value out to the client response and view it in a web browser to demonstrate that it has been loaded successfully.</span></span> <span data-ttu-id="87a87-117">**클라이언트에 비밀 값을 반환하는 것은 일반적으로 수행하는 작업이 ‘아닙니다’.**</span><span class="sxs-lookup"><span data-stu-id="87a87-117">**Returning a secret value to the client is *not* something you'd normally do!**</span></span> <span data-ttu-id="87a87-118">일반적으로 데이터베이스 또는 원격 API의 클라이언트 라이브러리 초기화와 같은 작업을 수행하는 데 비밀을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-118">Usually, you'll use secrets to do things like initialize client libraries for databases or remote APIs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="87a87-119">앱이 로그, 저장소 및 응답을 비롯한 모든 종류의 출력에 비밀을 쓰지 않도록 항상 코드를 주의 깊게 검토하세요.</span><span class="sxs-lookup"><span data-stu-id="87a87-119">Always carefully review your code to ensure that your app never writes secrets to any kind of output, including logs, storage, and responses.</span></span>

## <a name="exercise"></a><span data-ttu-id="87a87-120">연습</span><span class="sxs-lookup"><span data-stu-id="87a87-120">Exercise</span></span>

<span data-ttu-id="87a87-121">새 ASP.NET Core 웹 API를 만들고 `AddAzureKeyVault`를 사용하여 자격 증명 모음에서 비밀을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-121">We'll create a new ASP.NET Core web API and use `AddAzureKeyVault` to load the secret from our vault.</span></span>

### <a name="create-the-app"></a><span data-ttu-id="87a87-122">앱 만들기</span><span class="sxs-lookup"><span data-stu-id="87a87-122">Create the app</span></span>

<span data-ttu-id="87a87-123">Azure Cloud Shell 터미널에서 다음을 실행하여 새 ASP.NET Core 웹 API 응용 프로그램을 만들고 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-123">In the Azure Cloud Shell terminal, run the following to create a new ASP.NET Core web API application and open it in the editor.</span></span>

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

<span data-ttu-id="87a87-124">편집기가 로드된 후 셸에서 다음 명령을 실행하여 `AddAzureKeyVault`를 포함하는 NuGet 패키지를 추가하고 모든 앱의 종속성을 복원합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-124">After the editor loads, run the following commands in the shell to add the NuGet package containing `AddAzureKeyVault` and restore all of the app's dependencies.</span></span>

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a><span data-ttu-id="87a87-125">비밀을 로드하고 사용하는 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-125">Add code to load and use secrets</span></span>

<span data-ttu-id="87a87-126">Key Vault를 효과적으로 사용하려면 시작 시 자격 증명 모음에서 비밀을 로드하도록 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-126">To demonstrate good usage of Key Vault, we will modify our app to load secrets from the vault at startup.</span></span> <span data-ttu-id="87a87-127">또한 자격 증명 모음에서 **SecretPassword** 비밀을 가져오는 엔드포인트가 있는 새 컨트롤러를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-127">We'll also add a new controller with an endpoint that gets our **SecretPassword** secret from the vault.</span></span>

<span data-ttu-id="87a87-128">먼저 앱 시작: `Program.cs`를 열고, 콘텐츠를 삭제하고, 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-128">First, the app startup: Open `Program.cs`, delete the contents and replace them with the following code:</span></span>

```csharp
using Microsoft.AspNetCore;
using Microsoft.AspNetCore.Hosting;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp
{
    public class Program
    {
        public static void Main(string[] args)
        {
            CreateWebHostBuilder(args).Build().Run();
        }

        public static IWebHostBuilder CreateWebHostBuilder(string[] args) =>
            WebHost.CreateDefaultBuilder(args)
                .ConfigureAppConfiguration((context, config) =>
                {
                    // Build the current set of configuration to load values from
                    // JSON files and environment variables, including VaultName.
                    var builtConfig = config.Build();

                    // Use VaultName from the configuration to create the full vault URL.
                    var vaultUrl = $"https://{builtConfig["VaultName"]}.vault.azure.net/";

                    // Load all secrets from the vault into configuration. This will automatically
                    // authenticate to the vault using a managed identity. If a managed identity
                    // is not available, it will check if Visual Studio and/or the Azure CLI are
                    // installed locally and see if they are configured with credentials that can
                    // access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!IMPORTANT]
> <span data-ttu-id="87a87-129">편집이 완료되면 파일을 저장해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-129">Make sure to save files when you're done editing them.</span></span> <span data-ttu-id="87a87-130">"..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-130">You can do this either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

<span data-ttu-id="87a87-131">시작 코드의 유일한 변경 내용은 `ConfigureAppConfiguration`를 추가하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-131">The only change from the starter code is the addition of `ConfigureAppConfiguration`.</span></span> <span data-ttu-id="87a87-132">이를 통해 구성에서 자격 증명 모음 이름을 로드하고 `AddAzureKeyVault`를 함께 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-132">This is where we load the vault name from configuration and call `AddAzureKeyVault` with it.</span></span>

<span data-ttu-id="87a87-133">그런 다음, 컨트롤러: `SecretTestController.cs`라는 `Controllers` 폴더에 새 파일을 만들고 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-133">Next, the controller: Create a new file in the `Controllers` folder called `SecretTestController.cs` and paste the following code into it.</span></span>

> [!TIP]
> <span data-ttu-id="87a87-134">새 파일을 만들려면 셸에서 `touch` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-134">To create a new file, use the `touch` command in the shell.</span></span> <span data-ttu-id="87a87-135">이 예제의 경우 `touch Controllers/SecretTestController.cs`입니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-135">In this case, use `touch Controllers/SecretTestController.cs`.</span></span> <span data-ttu-id="87a87-136">이 파일을 표시하려면 편집기의 [파일] 창에서 [새로 고침] 단추를 클릭해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-136">You'll need to click the refresh button in the Files pane of the editor to see it there.</span></span>

```csharp
using System;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Extensions.Configuration;

namespace KeyVaultDemoApp.Controllers
{
    [Route("api/[controller]")]
    public class SecretTestController : ControllerBase
    {
        private readonly IConfiguration _configuration;

        public SecretTestController(IConfiguration configuration)
        {
            _configuration = configuration;
        }

        [HttpGet]
        public IActionResult Get()
        {
            // Get the secret value from configuration. This can be done anywhere
            // we have access to IConfiguration. This does not call the Key Vault
            // API, because the secrets were loaded at startup.
            var secretName = "SecretPassword";
            var secretValue = _configuration[secretName];

            if (secretValue == null)
            {
                return StatusCode(
                    StatusCodes.Status500InternalServerError,
                    $"Error: No secret named {secretName} was found...");
            }
            else {
                return Content($"Secret value: {secretValue}" +
                    Environment.NewLine + Environment.NewLine +
                    "This is for testing only! Never output a secret " +
                    "to a response or anywhere else in a real app!");
            }
        }
    }
}
```

<span data-ttu-id="87a87-137">셸에서 `dotnet build`를 실행하여 모든 항목이 컴파일되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-137">Run `dotnet build` in the shell to make sure everything compiles.</span></span> <span data-ttu-id="87a87-138">앱이 실행할 준비가 되었습니다. 이제 Azure에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="87a87-138">The app is ready to run &mdash; now let's get it into Azure!</span></span>