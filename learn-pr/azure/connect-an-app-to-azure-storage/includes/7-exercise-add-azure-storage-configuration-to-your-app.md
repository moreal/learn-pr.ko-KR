이 단원에서는 액세스 키를 검색하여 앱 구성에 추가합니다. 또한 .NET Core 콘솔 응용 프로그램을 만들었으므로 구성 파일에서 해당 응용 프로그램으로 읽어오기 위한 지원을 추가해야 합니다.

## <a name="create-a-json-configuration-file"></a>JSON 구성 파일 만들기

1. 이전 단원에서 만든 Visual Studio 프로젝트에서 프로젝트를 마우스 오른쪽 단추로 클릭하고, **추가**를 선택한 다음, **새 항목**을 선택하거나 Ctrl+Shift+A를 누르고 있습니다.

1. 모달 대화 상자가 표시됩니다. **JavaScript JSON 구성 파일**을 선택하고 **appsettings.json**을 *이름* 텍스트 상자에 입력한 다음, **추가**를 클릭합니다.

  ![앱 설정](..\media-draft\7-appsettings.png)

1. 파일이 콘텐츠가 다음과 비슷한 프로젝트에 추가됩니다.

    ```json
    {
      "exclude": [
        "**/bin",
        "**/bower_components",
        "**/jspm_packages",
        "**/node_modules",
        "**/obj",
        "**/platforms"
      ]
    }
    ```
1. **제외** 항목 및 연관된 콘텐츠를 제거하고 빈 문자열 값을 사용하여 단일 항목 **StorageAccountConnectionString**으로 바꿉니다. 다음과 유사하게 나타납니다.

    ```json
    {
      "StorageAccountConnectionString": ""
    }
    ```
1. **appsettings.json** 파일을 선택하고, 마우스 오른쪽 단추를 클릭한 다음, **속성**을 선택합니다(또는 Alt+Enter나 F4 키를 누름).

1. **출력 디렉터리로 복사**를 **변경된 내용만 복사**로 변경합니다.

  ![빌드 작업](..\media-draft\7-build-action.png)

  > 이렇게 하면 앱이 컴파일/빌드되는 경우 앱 구성 파일이 출력 디렉터리에 배치됩니다.

## <a name="add-support-to-read-a-json-configuration-file"></a>JSON 구성 파일을 읽도록 지원 추가

.NET Core 콘솔 응용 프로그램이 쉽게 JSON 구성 파일에서 읽을 수 있도록 하려면 특정 라이브러리를 추가해야 합니다.

1. 프로젝트를 마우스 오른쪽 단추로 클릭하고 **NuGet 패키지 관리 …** 를 선택합니다.

![NuGet 패키지 관리](..\media-draft\5-manage-nuget-packages.png)

1. 현재 설치된 NuGet 패키지를 보여주는 페이지가 표시됩니다. **찾아보기** 옵션을 클릭하고 검색 필드에 **Microsoft.Extensions.Configuration.Json**을 입력합니다. **Microsoft.Extensions.Configuration.Json** 패키지가 검색 결과에 표시됩니다.

1. **Microsoft.Extensions.Configuration.Json** 패키지를 선택하고 오른쪽 창에서 **설치**를 선택합니다.

1. **변경 내용 미리 보기** 대화 상자가 표시됩니다. **확인**을 클릭합니다.

1. 라이선스 승인 대화 상자가 표시됩니다. **동의함**을 클릭합니다.


## <a name="read-from-the-configuration-file"></a>구성 파일에서 읽기

구성을 읽을 수 있도록 하는 데 필요한 라이브러리를 추가했으므로 콘솔 응용 프로그램 내에서 해당 기능을 사용하도록 설정해야 합니다.

1. 프로젝트에서 **Program.cs** 파일을 찾아 Visual Studio에서 엽니다.

1. 파일 맨 위에 **using System;** 줄이 표시됩니다. 해당 줄 아래에 다음 코드 줄을 추가합니다.

    ```csharp
    using Microsoft.Extensions.Configuration;
    using System.IO;
    ```

1. **Main** 메서드의 콘텐츠를 다음 코드로 바꿉니다.

    ```csharp
    var builder = new ConfigurationBuilder()
        .SetBasePath(Directory.GetCurrentDirectory())
        .AddJsonFile("appsettings.json");

    var configuration = builder.Build();
    ```

1. **Program.cs** 파일은 이제 다음과 같이 표시됩니다.

    ```csharp
    using System;
    using Microsoft.Extensions.Configuration;
    using System.IO;

    namespace DemoConsoleApp
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

> 이 코드는 **appsettings.json** 파일에서 읽을 구성 시스템을 초기화합니다.

## <a name="add-your-connection-string-to-the-configuration-file"></a>구성 파일에 연결 문자열 추가

이제 저장소 계정 연결 문자열을 가져와서 앱의 구성에 배치해야 합니다.

1. 저장소 계정이 포함된 구독의 Azure Portal로 이동합니다.

1. 저장소 계정으로 이동합니다.

1. 포털에서 저장소 계정의 계정 키 블레이드로 이동합니다.

1. **key1** 연결 문자열을 복사합니다.

1. 포털에서 복사한 액세스 키의 콘텐츠에 **StorageAccountConnectionString**의 값으로 붙여넣습니다. 이제 구성은 다음과 비슷하게 표시됩니다.

    ```json
    {
      "StorageAccountConnectionString": "your-access-key-connection-string-goes-here"
    }
    ```
