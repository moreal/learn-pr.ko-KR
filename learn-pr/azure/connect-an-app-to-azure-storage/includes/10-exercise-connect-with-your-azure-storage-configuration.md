::: 영역 피벗 = "csharp" 구성에서 연결 문자열을 검색 하 고 사용 하 여 Azure 저장소 계정에 연결할 코드를 추가 해 보겠습니다.

## <a name="retrieve-the-connection-string"></a>연결 문자열 검색

1. 선택 **Program.cs** 코드 편집기에서 엽니다.

1. 추가 된 `using` 참조 파일의 맨 위에 있는 문을 `Microsoft.WindowsAzure.Storage` 네임 스페이스:

    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. 끝을 `Main` 메서드를 구성 파일에서 Azure storage 계정 연결 문자열을 검색 하려면 다음 줄을 추가 합니다. 전달 된 _키_ 에 사용 되는 이름과 일치 해야 하 **appsettings.json** 파일입니다.

    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>Blob 클라이언트 만들기

1. 정적을 사용 하 여 `CloudStorageAccount.TryParse` 메서드를를 `CloudStorageAccount` 개체-연결 문자열 사용 및 `out` 매개 변수를 만든된 개체를 반환 합니다. 반환 된 `bool` 문자열 구문 분석 하는지 여부를 나타내는 값입니다.
    - 실패 한 경우 콘솔에 메시지를 출력 하 고 메서드의 반환 합니다.

    ```csharp
    if (!CloudStorageAccount.TryParse(connectionString, 
            out CloudStorageAccount storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    ```

1. 사용 하 여 반환 된 `CloudStorageAccount` blob 클라이언트를 만드는 개체입니다.

    ```csharp
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```

1. 다음으로, blob 클라이언트를 사용 하 여 "photoblobs" 라는 컨테이너에 대 한 참조를 검색 합니다. 훨씬 같은 계정 이름, 소문자 및 문자와 숫자로 구성 된 Blob 컨테이너 이름 이어야 합니다.

    ```csharp
    var blobContainer = blobClient.GetContainerReference("photoblobs");
    ```

1. 사용 된 `CreateIfNotExistsAsync` 컨테이너를 만드는 방법. 반환 합니다.는 `bool` 컨테이너 만들어졌는지 여부를 나타내는입니다. 라는 변수에 저장 `created`합니다.
    - 이 **비동기** 메서드-의미 실제 네트워크 호출을 수행 합니다.
    - 사용 해야 합니다는 `await` 가져오려는 키워드는 `bool` 결과입니다.

    ```csharp
    bool created = await blobContainer.CreateIfNotExistsAsync();
    ```

1. 사용 하기 때문를 `await` 키워드를 계속 해 서의 서명 변경 합니다 `Main` 메서드를 `async` 반환 하 고는 `Task`.

    ```csharp
    static async Task Main(string[] args)
    {
        ...
    }
    ```

1. 에서는 Blob 컨테이너를 만들지 여부를 마지막으로 출력 합니다.

    ```csharp
    Console.WriteLine(created ? "Created the Blob container" : "Blob container already exists.");
    ```

1. 파일을 저장합니다.

작업을 확인 하려는 경우에 최종 파일이 다음과 같아야 합니다.

```csharp
using System;
using Microsoft.Extensions.Configuration;
using System.IO;
using System.Threading.Tasks;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;

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

## <a name="use-c-71-to-build-our-app"></a>C# 7.1을 사용 하 여 앱 빌드

에 대 한 지원 `async` 하 고 `await` 에서 `Main` 메서드는 C# 7.1에 추가 되었습니다. 사용 중인 컴파일러의 기본 버전 되지 않을 수 있습니다. 에서는 해당 버전의 컴파일러를 사용 하 여 구성 파일에서 설정 하 여 있는지 확인해 보겠습니다.

1. 열기는 `PhotoSharingApp.csproj` 추가한 `<LangVersion>7.1</LangVersion>` 에 `PropertyGroup` 지정 하는 `TargetFramework`합니다. 완료 되 면 다음과 같이 표시 됩니다.

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

1. 응용 프로그램을 빌드 및 실행합니다. **참고:** 올바른 작업 디렉터리에 있는지 확인 합니다.

    ```bash
    dotnet run
    ```

::: zone-end

::: 영역 피벗 = "javascript"는 저장 된 연결 문자열을 사용 하 여 Azure storage 계정에 연결 하는 코드를 추가 해 보겠습니다. Azure 클라이언트 라이브러리는 자동으로 사용 합니다 **AZURE_STORAGE_CONNECTION_STRING** 환경 변수를 연결 문자열을 가져옵니다.

## <a name="create-a-blob-client"></a>Blob 클라이언트 만들기

1. 오픈 **index.js** 코드 편집기에서.

1. 포함 하 여 시작 합니다 **azure storage** 모듈입니다. 모듈 이라는 변수에 저장할 **저장소**합니다.

    ```javascript
    #!/usr/bin/env node
    require('dotenv').load();
    
    const storage = require('azure-storage');
    ```

1. 다음으로, 바로 그 사용 합니다 **저장소** 만들 개체를 `BlobService` 개체 및 명명 된 전역에 저장 **blobService**합니다. 기억 하는 저장소 계정에 대 한 액세스를 나타내는 경량 개체입니다.

    ```javascript
    const blobService = storage.createBlobService();
    ```

1. 생성 하려는 컨테이너를 나타낼 때는 상수를 추가 합니다. 이름을 컨테이너 "photoblobs"입니다.

    ```javascript
    const containerName = 'photoblobs';
    ```

## <a name="create-a-container"></a>컨테이너 만들기

사용할 수 있습니다는 `BlobService` Azure storage에 blob Api 사용 하는 개체입니다. 앞서 언급 했 듯이 네트워크 호출을 수행 하는 모든 Api는 비동기적으로 앱 응답성을 유지 하기. `createContainerIfNotExists` 메서드는 이러한 메서드 중 하나입니다. 사용 하 여 _약속_ 응답을 포함 하는 콜백을 처리 하도록 합니다.

1. 사용 하 여 `util.promisify` 콜백 버전 되려면 `createContainerIfNotExists` 프라미스를 반환 메서드로 설정 합니다.
    - 콜백 메서드는 개체 이므로 추가 해야는 `bind` 호출 끝에 해당 컨텍스트에 연결 합니다.
    - 라는 파일의 맨 위에 있는 상수에 반환 값을 할당 `createContainerAsync`다음과 같이 합니다.

```javascript
const storage = require('azure-storage');
const blobService = storage.createBlobService();

const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';
```

1. "Hello, World!"를 제거 합니다. 출력 `main()`합니다.

1. 새 호출 `createContainerAsync` 약속 합니다.
    - 전달 된 **containerName** 상수입니다.
    - 적용 된 `await` 키워드를 호출 합니다.
    - 에 대 한 호출을 래핑하는 `try`  /  `catch` 생성 하 고 오류를 출력 합니다.

    ```javascript
    try {
        await createContainerAsync(containerName);
    }
    catch (err) {
        console.log(err.message);
    }
    ```
    
1. 합니다 `createContainerAsync` 내부에서 첫 번째 값을 반환 하는 약속 `createContainerIfNotExists`, 컨테이너가 결과 합니다. 컨테이너 생성 된 여부에 대 한 정보 포함 됩니다. 변수에 결과 캡처 및 출력에 따라 컨테이너가 생성 되는 여부는 `result.created` 속성입니다.

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

1. 마지막으로 데코 레이트 합니다 `main` 함수는 `async` 키워드입니다.
        
1. 파일을 저장합니다.

작업을 확인 하려는 경우 최종 파일 같이 표시 됩니다.

```javascript
#!/usr/bin/env node

require('dotenv').load();

const util = require('util');

const storage = require('azure-storage');
const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);

const containerName = 'photoblobs';

async function run() {
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

run();
```

## <a name="run-the-app"></a>앱 실행

1. 응용 프로그램을 빌드 및 실행합니다. **참고:** 올바른 작업 디렉터리에 있는지 확인 합니다.

    ```bash
    node index.js
    ```

::: zone-end

Blob 컨테이너가 생성 되는 보고 해야 합니다. 두 번째로 실행을 하는 경우 해당 알려 주어 야 이미 존재 합니다.

컨테이너를 확인 합니다.

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.

1. 저장소 계정으로 이동합니다. 사용할 수는 **모든 리소스** 섹션에서 이름으로 저장소 계정 또는 검색을 찾을 수 합니다 _검색 상자_ 포털 창의 맨 위에 있는 합니다. 

1. 선택 된 **Blob** 에서 저장소 계정의 항목은 **Blob 서비스** 섹션.

1. 표시 되어야 하 **photoblobs** [Blob] 패널에는 컨테이너입니다. 앱을 사용 하 여 다시 시도 하십시오. 항목의 오른쪽에 있는 "..." 메뉴를 통해 컨테이너를 삭제할 수 있습니다.

> [!NOTE]
> 컨테이너에서에서 사라집니다 포털 매우 신속 하 게 되지만 실제로 삭제 하는 데 몇 분이 걸립니다. 다시 하려고 하면 삭제 되는 동안 Azure에서 오류 응답을 받게 됩니다.

## <a name="delete-the-app"></a>앱 삭제
Cloud Shell 환경에서 응용 프로그램 소스 코드를 유지 하지 않으려는 경우 폴더 및 모든 내용을 제거 하려면 다음 명령을 사용할 수 있습니다.

```bash
rm -r PhotoSharingApp/
```
