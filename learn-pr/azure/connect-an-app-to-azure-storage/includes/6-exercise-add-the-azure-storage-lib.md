::: 영역 피벗 = "csharp".NET Core 콘솔 응용 프로그램에 Azure Storage 클라이언트 라이브러리를 통합 해 보겠습니다.

.NET 용 Azure storage 클라이언트 라이브러리는 NuGet을 사용 하 여 배포 됩니다. 추가 하려는 합니다 **WindowsAzure.Storage** .NET 또는.NET Core 응용 프로그램을 패키지 합니다.

## <a name="add-the-azure-storage-nuget-package"></a>Azure Storage NuGet 패키지 추가

1. Cloud Shell에서 `cd` PhotoSharingApp 디렉터리 아니라면 이미 있습니다.

1. 추가 된 **WindowsAzure.Storage** 응용 프로그램에 패키지 합니다.

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. 이 클라이언트 라이브러리 및 필요한 모든 종속성을 다운로드 하는 동안 콘솔 활동이 발생 해야 합니다. 완료 되 면 계속 해 서 및 빌드 및 앱 모두 이동할 준비 되었는지 확인을 다시 실행 합니다.

    ```bash
    dotnet run
    ```

1. 이전 처럼 "Hello World!" 출력 되어야 합니다.

::: zone-end

::: zone pivot="javascript"

통합 하겠습니다 합니다 **Node.js 및 JavaScript 용 Microsoft Azure Storage 클라이언트 라이브러리** 응용 프로그램에 있습니다.

Node.js 용 클라이언트 라이브러리를 노드 패키지 관리자 (NPM)를 통해 제공 됩니다. 추가 하려는 합니다 **azure storage** 패키지를 프로그램 **packages.json** 파일입니다.

> [!NOTE]
> 합니다 **Node.js 및 JavaScript 용 Microsoft Azure Storage 클라이언트 라이브러리** 서버 응용 프로그램을 위한 것입니다. 사용 하려는 클라이언트 쪽 JavaScript를 수행 하는 경우는 **JavaScript 용 Azure Storage 클라이언트 라이브러리**에 동일한 기능을 제공 하지만 브라우저에서 실행에 맞게 조정 됩니다.

## <a name="add-the-azure-storage-package"></a>Azure Storage 패키지를 추가 합니다.

1. Cloud Shell에서 `cd` PhotoSharingApp 디렉터리 아니라면 이미 있습니다.

1. 추가 된 **azure storage** 응용 프로그램에 패키지 합니다. 제공 해야 합니다 `--save` 옵션을 유지 하므로 **packages.json**합니다.

    ```bash
    npm install azure-storage --save
    ```

1. 이 클라이언트 라이브러리 및 필요한 모든 종속성을 다운로드 하는 동안 콘솔 활동이 발생 해야 합니다. 완료 되 면 계속 해 서 및 빌드 및 앱 모두 이동할 준비 되었는지 확인을 다시 실행 합니다.

    ```bash
    node index.js
    ```

1. "Hello, World!"를 출력 하도록 이전 처럼

::: zone-end

위치에 필요한 라이브러리를 만들었으므로 이제 해당 Azure storage를 사용 하려면 코드에서 수행 되는 일반적인에서 살펴보겠습니다.
