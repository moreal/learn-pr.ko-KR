::: zone pivot="csharp" .NET Core 응용 프로그램에 지원을 추가하여 구성 파일에서 연결 문자열을 검색해 보겠습니다. 먼저 필요한 배관을 추가하여 JSON 파일의 구성을 관리합니다.

## <a name="create-a-json-configuration-file"></a>JSON 구성 파일 만들기

1. 프로젝트의 올바른 작업 디렉터리에 있는지 확인합니다.

1. 명령줄에서 `touch` 도구를 사용하여 이름이 **appsettings.json**인 파일을 만듭니다.

    ```bash
    touch appsettings.json
    ```

1. 대화형 편집기로 프로젝트를 열고, 로컬에서 작업하는 경우 원하는 편집기를 사용합니다. **Visual Studio Code**를 사용하는 것이 좋습니다. 확장 가능한 크로스 플랫폼 IDE이기 때문입니다. 다음 명령은 Cloud Shell 편집기용이지만 VS Code와 매우 유사합니다.
    
    ```bash
    code .
    ```

1. 편집기에서 **appsettings.json** 파일을 선택하고 다음 텍스트를 추가합니다. 온라인 편집기에서 파일을 저장합니다. 오른쪽 상단 모서리를 보면 일반 파일 작업과 관련된 메뉴가 있습니다.

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```

1. 다음으로 프로젝트 파일(**PhotoSharingApp.csproj**)을 선택하여 편집기에서 엽니다.

1. 프로젝트에 새 파일을 포함하고 출력 폴더에 복사할 다음 구성 블록을 추가합니다. 이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.

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

1. 파일 맨 위에 **using System;** 줄이 표시됩니다. 해당 줄 아래에 다음 코드 줄을 추가합니다.

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. **Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다. 이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

**Program.cs** 파일은 이제 다음과 같이 표시됩니다.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;

namespace PhotoSharingApp
{
    class Program
    {
        static void Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();            
        }
    }
}
```

::: zone-end

::: zone-pivot="javascript"

Node.js 응용 프로그램에 지원을 추가하여 구성 파일에서 연결 문자열을 검색해 보겠습니다. 먼저 필요한 배관을 추가하여 JavaScript 파일의 구성을 관리합니다.

## <a name="create-a-env-configuration-file"></a>.env 구성 파일 만들기

1. 프로젝트의 올바른 작업 디렉터리에 있는지 확인합니다.

1. 명령줄에서 `touch` 도구를 사용하여 이름이 **.env**인 파일을 만듭니다.

    ```bash
    touch .env
    ```

1. 대화형 편집기로 프로젝트를 열고, 로컬에서 작업하는 경우 원하는 편집기를 사용합니다. **Visual Studio Code**를 사용하는 것이 좋습니다. 확장 가능한 크로스 플랫폼 IDE이기 때문입니다. 다음 명령은 Cloud Shell 편집기용이지만 VS Code와 매우 유사합니다.
    
    ```bash
    code .
    ```

1. 편집기에서 **.env** 파일을 선택하고 다음 텍스트를 추가합니다. 온라인 편집기에서 파일을 저장합니다. 오른쪽 상단 모서리를 보면 일반 파일 작업과 관련된 메뉴가 있습니다.

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > **AZURE_STORAGE_CONNECTION_STRING** 값은 Storage API가 액세스 키를 조회하는 데 사용되는 하드 코딩된 환경 변수입니다. 원하는 경우 자신이 원하는 이름을 사용할 수 있지만 `BlobService` 개체를 만들 때 이름을 제공해야 합니다.

1. 파일을 저장합니다.

## <a name="add-support-to-read-an-environment-configuration-file"></a>환경 구성 파일을 읽도록 지원 추가

Node.js 앱은 **dotenv** 패키지를 추가하여 **.env** 파일을 읽도록 지원할 수 있습니다.

1. 창의 명령 프롬프트 섹션에서 *dotenv** 패키지에 대한 종속성을 추가합니다.

    ```bash
    node install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a>구성 파일을 읽는 코드 추가

구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.

1. 편집기에서 *index.js**를 선택합니다.

1. 파일 맨 위에 **#!/usr/bin/env node** 줄이 표시됩니다. 이 줄 아래에 **dotenv** 패키지를 로드하도록 `require` 문을 추가합니다. 이렇게 하면 **.env** 파일에 정의된 환경 변수를 프로그램에서 사용할 수 있습니다.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
::: zone-end

## <a name="add-the-connection-string-to-the-configuration-file"></a>구성 파일에 연결 문자열 추가

이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

1. 저장소 계정으로 이동합니다. **모든 리소스** 섹션을 사용하여 저장소 계정을 찾거나, 포털 창의 맨 위에 있는 _검색 상자_에서 이름으로 검색할 수 있습니다. 

1. 포털에서 저장소 계정의 **액세스 키** 블레이드를 선택합니다.

1. **key1** 연결 문자열을 복사합니다.

1. 포털에서 복사한 액세스 키의 콘텐츠를 연결 문자열 구성 변수의 값으로 붙여넣습니다.

이제 구성이 다음과 비슷하게 표시됩니다.

::: zone pivot="csharp"
    ```json
    {
        "StorageAccountConnectionString": "DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net"
    }
    ```
::: zone-end

::: zone-pivot="javascript"
    ```
    AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net
    ```
::: zone-end

이제 모든 정보가 정리되었으므로 저장소 계정을 사용하기 위한 코드를 추가할 수 있습니다.