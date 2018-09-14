::: 영역 피벗 = "csharp" 구성 파일에서 연결 문자열을 검색 하는.NET core 응용 프로그램을 지원을 추가 해 보겠습니다. JSON 파일에서 구성을 관리 하는 데 필요한 작업을 추가 하 여 시작 하겠습니다.

## <a name="create-a-json-configuration-file"></a>JSON 구성 파일 만들기

1. 프로젝트에 대 한 올바른 작업 디렉터리에 있는지 확인 합니다.

1. 사용 된 `touch` 라는 파일을 만들고 명령줄에서 도구 **appsettings.json**합니다.

    ```bash
    touch appsettings.json
    ```

1. 대화형 편집기를 사용 하 여 프로젝트를 엽니다. 로컬로 작업 하는 경우 원하는 편집기를 사용 합니다. 것이 좋습니다 **Visual Studio Code**, 확장 가능한 플랫폼 간 IDE 인 합니다. 다음 명령을 Cloud Shell 편집기는 VS Code와 매우 비슷합니다.

    ```bash
    code .
    ```

1. 선택 된 **appsettings.json** 편집기에서 파일을 다음 텍스트를 추가 합니다. 파일을 저장합니다. 온라인 편집기에서 있는 일반적인 파일 작업에는 오른쪽 위 모서리의 메뉴가입니다.

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```

1. 다음으로 프로젝트 파일을 선택 (**PhotoSharingApp.csproj**) 하 여 편집기에서 엽니다.

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

::: zone pivot="javascript"

구성 파일에서 연결 문자열을 검색 하는 Node.js 응용 프로그램에 지원을 추가 해 보겠습니다. JavaScript 파일에서 구성을 관리 하는 데 필요한 작업을 추가 하 여 시작 하겠습니다.

## <a name="create-a-env-configuration-file"></a>.Env 구성 파일 만들기

1. 프로젝트에 대 한 올바른 작업 디렉터리에 있는지 확인 합니다.

1. 사용 된 `touch` 라는 파일을 만들고 명령줄에서 도구 **.env**합니다.

    ```bash
    touch .env
    ```

1. 열기 대화형 편집기를 사용 하 여 프로젝트를 로컬로 작업 하는 경우 사용 하 여-원하는 편집기 것이 좋습니다 **Visual Studio Code** 확장 가능한 플랫폼 간 IDE 인 합니다. 다음 명령을 Cloud Shell 편집기에 있고 VS Code와 매우 비슷합니다.
    
    ```bash
    code .
    ```

1. 선택 된 **.env** 편집기에서 파일을 다음 텍스트를 추가 합니다. 파일 저장-온라인 편집기에서 일반적인 파일 작업에는 상단 오른쪽 모서리의 메뉴가입니다.

    ```
    AZURE_STORAGE_CONNECTION_STRING=<value>
    ```

    > [!TIP]
    > 합니다 **AZURE_STORAGE_CONNECTION_STRING** 값은 액세스 키를 찾는 데 저장소 Api에 대 한 하드 코드 된 환경 변수입니다. 이름을 제공 해야 하지만 원하는 경우 고유한 이름을 사용할 수 있습니다 만든 경우에는 `BlobService` 개체입니다.

1. 파일을 저장합니다.

## <a name="add-support-to-read-an-environment-configuration-file"></a>환경 구성 파일을 읽을 지원 추가

Node.js 앱에서 읽을 수를 포함할 수 있습니다는 **.env** 추가 하 여 파일을 **dotenv** 패키지 있습니다.

1. 명령 프롬프트 창의 섹션에서 종속성을 추가 합니다 *dotenv**를 사용 하 여 패키지 `npm`합니다.

    ```bash
    npm install dotenv --save
    ```

## <a name="add-code-to-read-the-configuration-file"></a>구성 파일을 읽는 코드를 추가 합니다.

읽기 구성을 사용 하도록 설정 하 여 필요한 라이브러리 추가 했지만, 이제는 응용 프로그램 내에서 해당 기능을 사용 하도록 설정 해야 합니다.

1. 선택 *index.js** 편집기에서.

1. 파일의 맨 위에 있는 **#! usr/bin/env/노드** 줄이 표시 됩니다. 해당 줄 아래에 추가 `require` 로드 하는 문을 합니다 **dotenv** 패키지 있습니다. 이렇게 하면 환경 변수에서 정의 된 우리의 **.env** 파일을 프로그램에 사용할 수 있습니다.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    ```
::: zone-end

## <a name="add-the-connection-string-to-the-configuration-file"></a>구성 파일에 연결 문자열 추가

이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

1. 저장소 계정으로 이동합니다. 사용할 수는 **모든 리소스** 저장소 계정을 찾으려면 섹션 또는 이름별로 검색할 수 있습니다 합니다 _검색 상자_ 포털 창의 맨 위에 있는 합니다.

1. 선택 된 **액세스 키** 포털에서 저장소 계정 블레이드입니다.

1. 복사 합니다 **key1** 연결 문자열입니다.

1. 연결 문자열 구성 변수 값으로는 portal에서 복사한 선택 키의 내용을 붙여 넣습니다.

이제 구성은 다음과 비슷하게 표시됩니다.

::: zone pivot="csharp"
```json
{
    "StorageAccountConnectionString": "DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net"
}
```
::: zone-end

::: zone pivot="javascript"
```
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;AccountName=[account-name];AccountKey=[account-key];EndpointSuffix=core.windows.net
```
::: zone-end

만들었으므로 모든 연결에 저장소 계정을 사용 하는 코드를 추가 해 보겠습니다.