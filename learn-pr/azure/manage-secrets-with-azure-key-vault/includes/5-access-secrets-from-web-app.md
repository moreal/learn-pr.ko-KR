이제 MSI를 사용하도록 설정하여 앱이 인증에 사용할 ID를 만드는 방법을 알고 있으므로 자격 증명 모음의 비밀에 액세스하는 데 해당 ID를 사용하는 앱을 만듭니다.

## <a name="reading-secrets-in-an-aspnet-core-app"></a>ASP.NET Core 앱에서 비밀 읽기

Azure Key Vault API는 키 및 자격 증명 모음의 모든 관리와 사용을 처리하는 REST API입니다. 자격 증명 모음의 각 비밀에는 고유한 URL이 있으며 비밀 값은 HTTP GET 요청으로 검색됩니다.

.NET Core의 공식 Key Vault 클라이언트 라이브러리는 Microsoft.Azure.KeyVault NuGet 패키지의 `KeyVaultClient` 클래스입니다. 이를 직접 사용할 필요가 없습니다. ASP.NET Core의 `AddAzureKeyVault` 메서드를 사용하여 자격 증명 모음의 모든 비밀을 시작 시 구성 API로 로드할 수 있습니다. 이 방법을 사용하면 구성의 나머지 부분에 사용하는 것과 동일한 `IConfiguration` 인터페이스를 사용하여 이름별로 모든 비밀에 액세스할 수 있습니다. `AddAzureKeyVault`를 사용하는 앱에는 자격 증명 모음에 대한 **Get** 및 **List** 권한이 둘 다 필요합니다.

> [!TIP]
> 앱을 빌드하는 데 사용하는 프레임워크나 언어와 관계없이, 특별한 이유가 없는 한 비밀 값을 로컬로 캐시하거나 비밀을 앱 시작 시 메모리에 로드합니다. 필요할 때마다 자격 증명 모음에서 직접 비밀을 읽으면 불필요하게 속도가 느려지고 비용이 많이 듭니다.

`AddAzureKeyVault`에는 자격 증명 모음 이름만 입력으로 필요하며 이 이름은 로컬 앱 구성에서 가져옵니다. MSI 인증을 자동으로 처리하기도 합니다. MSI를 사용하도록 설정하고 Azure App Service에 배포된 앱에서 사용될 경우 이 메서드는 MSI 토큰 서비스를 검색하고 이를 사용하여 인증합니다. 대부분의 시나리오에 적합하고 모범 사례를 모두 구현하며 이 단원의 연습에서 사용합니다.

## <a name="handling-secrets-in-an-app"></a>앱에서 비밀 처리

비밀이 앱에 로드되면 앱이 비밀을 안전하게 처리하도록 해야 합니다. 이 모듈에서 빌드하는 앱에서는 클라이언트 응답에 대한 비밀 값을 기록하고 웹 브라우저에 비밀 값을 표시하여 성공적으로 로드되었음을 보여 줍니다. **클라이언트에 비밀 값을 반환하는 것은 일반적으로 수행하는 작업이 ‘아닙니다’.** 일반적으로 데이터베이스 또는 원격 API의 클라이언트 라이브러리 초기화와 같은 작업을 수행하는 데 비밀을 사용합니다.

> [!IMPORTANT]
> 앱이 로그, 저장소 및 응답을 비롯한 모든 종류의 출력에 비밀을 쓰지 않도록 항상 코드를 주의 깊게 검토하세요.

## <a name="exercise"></a>연습

새 ASP.NET Core 웹 API를 만들고 `AddAzureKeyVault`를 사용하여 자격 증명 모음에서 비밀을 로드합니다.

### <a name="create-the-app"></a>앱 만들기

Azure Cloud Shell 터미널에서 다음을 실행하여 새 ASP.NET Core 웹 API 응용 프로그램을 만들고 편집기에서 엽니다.

```console
dotnet new webapi -o KeyVaultDemoApp
cd KeyVaultDemoApp
code .
```

편집기가 로드된 후 셸에서 다음 명령을 실행하여 `AddAzureKeyVault`를 포함하는 NuGet 패키지를 추가하고 모든 앱의 종속성을 복원합니다.

```console
dotnet add package Microsoft.Extensions.Configuration.AzureKeyVault
dotnet restore
```

### <a name="add-code-to-load-and-use-secrets"></a>비밀을 로드하고 사용하는 코드를 추가합니다.

Key Vault를 효과적으로 사용하려면 시작 시 자격 증명 모음에서 비밀을 로드하도록 앱을 수정합니다. 또한 자격 증명 모음에서 **SecretPassword** 비밀을 가져오는 엔드포인트가 있는 새 컨트롤러를 추가합니다.

먼저 앱 시작: `Program.cs`를 열고, 콘텐츠를 삭제하고, 다음 코드로 바꿉니다.

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
                    // authenticate to the vault using MSI. If MSI is not available, it will
                    // check if Visual Studio and/or the Azure CLI are installed locally and
                    // see if they are configured with credentials that can access the vault.
                    config.AddAzureKeyVault(vaultUrl);
                })
                .UseStartup<Startup>();
    }
}
```

> [!TIP]
> 편집이 완료되면 `Ctrl+S`로 파일을 저장해야 합니다.

시작 코드의 유일한 변경 내용은 `ConfigureAppConfiguration`를 추가하는 것입니다. 이를 통해 구성에서 자격 증명 모음 이름을 로드하고 `AddAzureKeyVault`를 함께 호출합니다.

그런 다음, 컨트롤러: `SecretTestController.cs`라는 `Controllers` 폴더에 새 파일을 만들고 다음 코드를 붙여넣습니다.

> [!TIP]
> 새 파일을 만들려면 셸에서 `touch` 명령을 사용합니다. 이 예제의 경우 `touch Controllers/SecretTestController.cs`입니다. 이 파일을 표시하려면 편집기의 [파일] 창에서 [새로 고침] 단추를 클릭해야 합니다.

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

셸에서 `dotnet build`를 실행하여 모든 항목이 컴파일되는지 확인합니다. 앱이 실행할 준비가 되었습니다. 이제 Azure에 액세스할 수 있습니다.