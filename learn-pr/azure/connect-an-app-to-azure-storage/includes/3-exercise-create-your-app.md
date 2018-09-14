Azure Storage를 사용 하 여 사진 및 사용자를 대신 하 여 저장 된 데이터의 다른 비트를 관리 하는 사진 공유 응용 프로그램에 노력을 기억 하십시오.

::: zone pivot="csharp"

를 간소화 하기 위해 시나리오 Storage Api에 집중할 수 있도록 새.NET Core 콘솔 응용 프로그램을 만듭니다. 네트워크 연결을 항상 포함 되기만 가정 합니다. 그러나 네트워크 오류는 사용자 환경에 영향을 않거나 응용 프로그램 자체의 오류가 발생 하도록 앱을 항상 강화 해야 합니다.

## <a name="create-a-net-core-application"></a>.NET Core 응용 프로그램 만들기

.NET core는 macOS, Windows, 및 Linux에서 실행 되는.NET의 플랫폼 간 버전입니다. 로컬로 도구를 설치 하거나 실행 하려면 창의 오른쪽에 Cloud Shell을 사용할 수 있습니다는 아래 다음 단계를 수행 합니다.

1. Cloud Shell에 로그인 하거나 명령줄 세션을 열고 "PhotoSharingApp" 라는 이름의 새.NET Core 콘솔 응용 프로그램을 만듭니다. 추가할 수 있습니다 합니다 `-o` 또는 `--output` 플래그를 특정 폴더에 앱을 만듭니다.

    ```bash
    dotnet new console --name PhotoSharingApp
    ```

1. 빌드하고 제대로 실행 되도록 앱을 실행 합니다. "Hello, World!" 표시 됩니다. 표시 합니다.

    ```bash
    cd PhotoSharingApp
    
    dotnet run
    ```
::: zone-end

::: zone pivot="javascript"

저장소 Api에 집중할 수 있도록이 시나리오를 간소화, 콘솔에서 실행할 수 있는 새 Node.js 응용 프로그램을 만들겠습니다. 네트워크 연결을 항상 포함 되기만 가정 합니다. 그러나 네트워크 오류는 사용자 환경에 영향을 않거나 응용 프로그램 자체의 오류가 발생 하도록 앱을 항상 강화 해야 합니다.

## <a name="create-a-nodejs-application"></a>Node.js 응용 프로그램 만들기

Node.js는 JavaScript 앱을 실행 하기 위한 인기 있는 프레임 워크입니다. Web apps에 대해 가장 많이 사용 됩니다 있지만 사용도 명령줄에서 논리를 실행할 수 있습니다. 로컬로 설치 된 도구를 사용 하는 경우 명령줄에서 다음 단계를 실행할 수 있습니다. 또는 사용할 수는 Cloud Shell 창의 오른쪽에 실행 하는 아래 단계입니다.

1. Cloud Shell에 로그인 하거나 명령줄 세션을 열고 "PhotoSharingApp" 라는 새 폴더를 만듭니다.

    ```bash
    mkdir PhotoSharingApp
    ```

1. 새 폴더로 변경 하 고 만듭니다는 **package.json** 으로 패키지 관리자 (NPM (Node) 새 앱을 설명 하는 파일입니다.
    - "PhotoSharingApp" 이름을 지정 합니다.
    - 다른 모든 메시지에 대 한 기본값을 사용할 수 있습니다.

    ```bash
    cd PhotoSharingApp
    npm init
    ```

1. 새 소스 파일을 만듭니다 **index.js**, 코드는 어디에 합니다.

    ```bash
    touch index.js
    ```

1. 엽니다는 **index.js** 편집기를 사용 하 여 파일입니다. Cloud Shell을 사용 하는 경우 입력할 수 있습니다 `code .` 는 편집기를 엽니다.

1. 다음 프로그램을 배치 합니다 **index.js** 파일입니다.

    ```javascript
    #!/usr/bin/env node
    
    function main() {
        console.log('Hello, World!');
    }
    
    main();
    ```
1. 파일을 저장 합니다&mdash;Cloud Shell 편집기의 오른쪽 위 모서리에서 "..." 메뉴를 사용할 수 있습니다.

1. 올바르게 실행 되도록 앱을 실행 합니다. "Hello, World!" 표시 됩니다. 표시 합니다.

    ```bash
    node index.js
    ```

::: zone-end