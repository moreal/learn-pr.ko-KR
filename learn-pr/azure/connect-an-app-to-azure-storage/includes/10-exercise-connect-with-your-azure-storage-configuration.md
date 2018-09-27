::: zone pivot="csharp"
구성에서 연결 문자열을 검색하고 해당 연결 문자열을 사용하여 Azure 저장소 계정에 연결하는 코드를 추가해 보겠습니다.

## <a name="retrieve-the-connection-string"></a>연결 문자열 검색

1. 코드 편집기에서 **Program.cs**를 엽니다.

1. `Microsoft.WindowsAzure.Storage` 네임스페이스를 참조하려면 파일 맨 위에 `using` 명령문을 추가합니다.

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. `Main` 메서드의 맨 끝에 다음 줄을 추가하여 구성 파일에서 Azure 저장소 계정 연결 문자열을 검색합니다. 전달된 _키_가 **appsettings.json** 파일에 사용된 이름과 일치해야 합니다.

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>BLOB 클라이언트 만들기

1. 정적 `CloudStorageAccount.TryParse` 메서드를 사용하여 `CloudStorageAccount` 개체를 만듭니다. 이 메서드는 연결 문자열과 `out` 매개 변수를 사용하여 생성된 개체를 반환합니다. 이 메서드는 문자열을 성공적으로 구문 분석했는지 여부를 나타내는 `bool` 값을 반환합니다.
    - 실패하면 콘솔에 메시지를 출력하고 메서드에서 돌아갑니다.

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString,
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. 반환된 `CloudStorageAccount` 개체를 사용하여 BLOB 클라이언트를 만듭니다.

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 다음으로, BLOB 클라이언트를 사용하여 "photoblobs" 컨테이너의 참조를 검색합니다. 계정 이름과 비슷하게, Blob 컨테이너 이름은 소문자여야 하고 문자와 숫자로 구성되어야 합니다.

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. `CreateIfNotExistsAsync` 메서드를 사용하여 컨테이너를 만듭니다. 그러면 컨테이너 생성 여부를 나타내는 `bool`이 반환됩니다. 이 값을 `created` 변수에 저장합니다.
    - 이 메서드는 실제 네트워크 호출을 수행하는 **비동기** 메서드입니다.
    - `await` 키워드를 사용하여 `bool` 결과를 가져와야 합니다.

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. `await` 키워드를 사용할 것이므로 `Main` 메서드가 `async` 되도록 서명을 변경하고 `Task`를 반환합니다.

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

    맨 위에 새로 `using` 명령문을 추가해야 합니다.

    ```csharp
    using System.Threading.Tasks;
    ```

1. 마지막으로, Blob 컨테이너 생성 여부를 출력합니다.

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. 파일을 저장합니다.

작업을 확인하고 싶은 경우 최종 파일은 이렇게 생겼습니다.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using Microsoft.WindowsAzure.Storage;
using System.Threading.Tasks;

namespace PhotoSharingApp
{
    class Program
    {
        static async Task Main(string[] args)
        {
            var builder = new ConfigurationBuilder()
                .SetBasePath(Directory.GetCurrentDirectory())
                .AddJsonFile("appsettings.json");

            var configuration = builder.Build();
            var connectionString = configuration["StorageAccountConnectionString"];

            if (!CloudStorageAccount.TryParse(connectionString, out CloudStorageAccount storageAccount))
            {
                Console.WriteLine("Unable to parse connection string");
                return;
            }

            var blobClient = storageAccount.CreateCloudBlobClient();
            var blobContainer = blobClient.GetContainerReference("photoblobs");
            bool created = await blobContainer.CreateIfNotExistsAsync();

            Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
        }
    }
}
```

## <a name="use-c-71-to-build-our-app"></a>C# 7.1을 사용하여 앱 빌드

`Main` 메서드의 `async` 및 `await`에 대한 지원이 C# 7.1에 추가되었습니다. 이 버전은 여러분이 사용 중인 컴파일러의 기본 버전이 아닐 수 있습니다. 이 컴파일러 버전을 사용하도록 구성 파일에서 설정해 보겠습니다.

1. `PhotoSharingApp.csproj` 파일을 열고 `TargetFramework`를 지정하는 `PropertyGroup`에 `<LangVersion>7.1</LangVersion>`을 추가합니다. 완료되면 파일이 다음과 비슷한 모양입니다.

    ```xml
    <Project Sdk="Microsoft.NET.Sdk">
      <PropertyGroup>
        <OutputType>Exe</OutputType>
        <LangVersion>7.1</LangVersion>
        <TargetFramework>netcoreapp2.0</TargetFramework>
      </PropertyGroup>
      ...
    </Project>
    ```

1. 파일을 저장합니다.

## <a name="run-the-app"></a>앱 실행

1. 응용 프로그램을 빌드 및 실행합니다. **참고:** 올바른 작업 디렉터리에 있는지 확인합니다.

    ```bash
    dotnet run
    ```

::: zone-end

::: zone-pivot="javascript"
저장된 연결 문자열을 사용하여 Azure 저장소 계정에 연결하려면 코드를 추가하겠습니다. Azure 클라이언트 라이브러리는 자동으로 **AZURE_STORAGE_CONNECTION_STRING** 환경 변수를 사용하여 연결 문자열을 가져옵니다.

## <a name="create-a-blob-client"></a>BLOB 클라이언트 만들기

1. 코드 편집기에서 **index.js** 파일을 엽니다.

1. **azure-storage** 모듈을 포함하여 시작합니다. **storage**라는 변수에 모듈을 저장합니다.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();

    const storage = require('azure-storage');
    ```

1. 다음으로, 저장한 바로 뒤에 **저장소** 개체를 사용하여 `BlobService` 개체를 만들고 **blobService**라는 글로벌에 저장합니다. 이러한 개체는 저장소 계정에 대한 액세스를 나타내는 경량 개체입니다.

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. 만들려는 컨테이너를 나타내려면 상수를 추가합니다. 컨테이너 이름을 "photoblobs"로 지정하겠습니다.

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a>컨테이너 만들기

`BlobService` 개체를 사용하여 Azure 저장소에서 BLOB API를 작업할 수 있습니다. 앞서 언급했듯이, 네트워크 호출을 만드는 모든 API는 비동기적으로 앱 응답성을 유지합니다. `createContainerIfNotExists` 메서드도 이러한 메서드 중 하나입니다. _promises_를 사용하여 응답을 포함하는 콜백을 처리하겠습니다.

1. `util.promisify`를 통해 `createContainerIfNotExists`의 콜백 버전을 사용하여 promise-returning 메서드로 전환합니다.
    - 콜백 메서드는 개체에 있으므로 해당 컨텍스트에 연결하려면 끝부분에 `bind` 호출을 추가해야 합니다.
    - 아래와 같이 `createContainerAsync` 파일의 맨 위에 있는 상수에 반환 값을 할당합니다.
    - 파일의 맨 위에 있는 `util` 모듈에 대해 `require`도 필요합니다.

    ```javascript
    const util = require('util');
    const storage = require('azure-storage');
    const blobService = storage.createBlobService();

    const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

    const containerName = 'photoblobs';
    ```

2. "Hello, World!" 출력을 `main()`에서 제거합니다.

3. 새 `createContainerAsync` promise를 호출합니다.
    - **containerName** 상수에 전달합니다.
    - 호출에 `await` 키워드를 적용합니다.
    - 호출을 `try` / `catch` 구문에 래핑하고 모든 오류를 출력합니다.

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. `createContainerAsync` promise는 컨테이너 결과인 기본 `createContainerIfNotExists`에서 첫 번째 값을 반환합니다. 이 값에는 컨테이너 생성 여부에 대한 정보가 포함됩니다. 결과를 변수에 캡처하고 `result.created` 속성에 따라 컨테이너 생성 여부를 출력합니다.

    ```javascript
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
    ```

1. 마지막으로, `async` 키워드로 `main` 함수를 데코레이트합니다.

1. 파일을 저장합니다.

작업을 확인하려는 경우 최종 파일은 이렇게 표시되어야 합니다.

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function main() {
    try {
        var result = await createContainerAsync(containerName);
        if (result.created) {
            console.log(`Blob container ${containerName} created`);
        }
        else {
            console.log(`Blob container ${containerName} already exists.`);
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

main();
```

## <a name="run-the-app"></a>앱 실행

1. 응용 프로그램을 빌드 및 실행합니다. **참고:** PhotoSharingApp 디렉터리에 있어야 합니다.

    ```bash
    node index.js
    ```

::: zone-end

BLOB 컨테이너가 생성되었다고 응용 프로그램이 보고할 것입니다. 응용 프로그램을 두 번째로 실행하면 컨테이너가 이미 있다고 보고할 것입니다.

컨테이너를 확인하려면:

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 저장소 계정으로 이동합니다. **모든 리소스** 섹션을 사용하여 저장소 계정을 찾거나, 포털 창의 맨 위에 있는 _검색 상자_에서 이름으로 검색할 수 있습니다.

1. **Blob 서비스** 섹션에서 저장소 계정의 **Blob** 항목을 선택합니다.

1. Blob 패널에 **photoblobs** 컨테이너가 표시되어야 합니다. 항목의 오른쪽에 있는 "..." 메뉴를 통해 컨테이너를 삭제하여 앱에서 컨테이너를 다시 만들 수 있습니다.

> [!NOTE]
> 포털에서 컨테이너가 매우 빠르게 사라지지만, 실제로 삭제되는 데 몇 분이 걸립니다. 컨테이너가 삭제되는 동안 컨테이너를 다시 만들려고 시도하면 Azure에서 오류 응답을 받게 됩니다.

## <a name="delete-the-app"></a>앱 삭제
응용 프로그램 소스 코드를 Cloud Shell 환경에 유지하지 않기로 결정하는 경우 다음 명령을 사용하여 폴더와 모든 콘텐츠를 제거할 수 있습니다.

```bash
rm -r PhotoSharingApp/
```
