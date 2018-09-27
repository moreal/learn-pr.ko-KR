::: zone pivot="csharp"
Azure Storage 클라이언트 라이브러리를 .NET Core 콘솔 응용 프로그램에 통합해 보겠습니다.

.NET용 Azure Storage 클라이언트 라이브러리는 NuGet을 사용하여 배포됩니다. **WindowsAzure.Storage** 패키지를 .NET 또는 .NET Core 응용 프로그램에 추가하겠습니다.

## <a name="add-the-azure-storage-nuget-package"></a>Azure Storage NuGet 패키지 추가

1. 터미널에 아직 없는 경우 `cd`를 PhotoSharingApp 디렉터리로 이동합니다.

1. **WindowsAzure.Storage** 패키지를 응용 프로그램에 추가합니다.

    ```bash
    dotnet add package WindowsAzure.Storage
    ```

1. 이렇게 하면 클라이언트 라이브러리 및 필요한 모든 종속성이 다운로드되는 동안 일부 콘솔 활동이 발생합니다. 완료되면 앱을 다시 빌드하고 실행하여 모든 준비가 완료되었는지 확인합니다.

    ```bash
    dotnet run
    ```

1. 이전과 마찬가지로, "Hello World!"가 출력되어야 합니다.

::: zone-end

::: zone pivot="javascript"

**Node.js 및 JavaScript용 Microsoft Azure Storage 클라이언트 라이브러리**를 응용 프로그램에 통합해 보겠습니다.

Node.js용 클라이언트 라이브러리는 NPM(노드 패키지 관리자)를 통해 제공됩니다. **azure-storage** 패키지를 **packages.json** 파일에 추가할 것입니다.

> [!NOTE]
> **Node.js 및 JavaScript용 Microsoft Azure Storage 클라이언트 라이브러리**는 서버 응용 프로그램을 위한 것입니다. 클라이언트 쪽 JavaScript를 수행하는 경우 동일한 기능을 제공하지만 브라우저에서 실행되도록 조정된 **JavaScript용 Azure Storage 클라이언트 라이브러리**를 사용합니다.

## <a name="add-the-azure-storage-package"></a>Azure Storage 패키지 추가

1. Cloud Shell에 아직 없는 경우 `cd`를 PhotoSharingApp 디렉터리로 이동합니다.

1. **azure-storage** 패키지를 응용 프로그램에 추가합니다. **packages.json**을 유지하도록 `--save` 옵션을 제공해야 합니다.

    ```bash
    npm install azure-storage --save
    ```

1. 이렇게 하면 클라이언트 라이브러리 및 필요한 모든 종속성이 다운로드되는 동안 일부 콘솔 활동이 발생합니다. 완료되면 앱을 다시 빌드하고 실행하여 모든 준비가 완료되었는지 확인합니다.

    ```bash
    node index.js
    ```

1. 이전과 마찬가지로, "Hello, World!"가 출력되어야 합니다.

::: zone-end

필요한 라이브러리를 얻었으니, Azure 저장소를 사용하기 위해 코드에서 수행해야 하는 몇 가지 일반적인 작업을 살펴보겠습니다.
