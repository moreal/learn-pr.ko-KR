우리는 지금 Azure Storage를 사용하여 사용자 대신 저장하는 사진과 기타 데이터를 관리하는 사진 공유 응용 프로그램을 만들고 있다는 사실을 잊지 마세요.

[!include[](../../../includes/azure-sandbox-activate.md)]

::: zone pivot="csharp"

Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 새 .NET Core 콘솔 응용 프로그램을 만들겠습니다. 또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다. 그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.

## <a name="create-a-net-core-application"></a>.NET Core 응용 프로그램 만들기

.NET Core는 macOS, Windows 및 Linux에서 실행되는 .NET의 플랫폼 간 버전입니다. 도구를 로컬로 설치하거나 창의 오른쪽에 있는 Cloud Shell을 사용하여 아래 단계를 실행할 수 있습니다.

1. Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 .NET Core 콘솔 응용 프로그램을 만듭니다. `-o` 또는 `--output` 플래그를 추가하여 특정 폴더에 앱을 만들 수 있습니다.

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. 앱을 실행하여 올바르게 빌드 및 실행되는지 확인합니다. 콘솔에 "Hello, World!"가 표시될 것입니다.

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

Storage API에 집중할 수 있도록 시나리오를 간소화하기 위해 콘솔에서 실행할 수 있는 새 Node.js 응용 프로그램을 만들겠습니다. 또한 응용 프로그램이 항상 네트워크에 연결된다고 가정하겠습니다. 그러나 네트워크 장애 시 사용자 환경에 영향을 미치거나 응용 프로그램 자체가 중단되는 일이 없도록 항상 앱을 보완해야 합니다.

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기

Node.js는 JavaScript 앱을 실행하기 위한 인기 있는 프레임워크입니다. 주로 웹앱에 사용되지만, 명령줄에서 논리를 실행하는 데 사용할 수도 있습니다. 도구를 로컬로 설치한 경우 명령줄에서 다음 단계를 실행할 수 있습니다. 또는 창 오른쪽에 있는 Cloud Shell을 사용하여 아래 단계를 실행할 수 있습니다.

1. Cloud Shell에 로그인하거나 명령줄 세션을 열고 "PhotoSharingApp"이라는 이름의 새 폴더를 만듭니다.

    ```bash
    mkdir PhotoSharingApp
    ```

1. 새 폴더로 변경하고 `npm`을 사용하여 새 Node.js 앱을 초기화합니다. 이렇게 하면 앱을 설명하는 메타데이터가 포함된 **package.json** 파일이 생성됩니다.

    ```bash
    cd PhotoSharingApp
    npm init -y
    ```

1. 코드가 이동할 새 소스 파일 **index.js**를 만듭니다.

    ```bash
    touch index.js
    ```

1. 편집기를 사용하여 **index.js** 파일을 엽니다. Cloud Shell을 사용하는 경우 `code .`를 입력하여 편집기를 엽니다.

1. 다음 프로그램을 **index.js** 파일에 붙여넣습니다. **Ctrl+V** 바로 가기 키를 사용하거나 마우스 오른쪽 단추를 클릭하여 붙여넣을 수 있습니다.

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. &mdash; 파일을 저장하면 Cloud Shell 편집기의 오른쪽 상단 모서리에 있는 "..." 메뉴를 사용할 수 있습니다.

1. 앱을 실행하여 올바르게 실행되는지 확인합니다. 콘솔에 "Hello, World!"가 표시될 것입니다.

    ```bash
    node index.js
    ```

::: zone-end