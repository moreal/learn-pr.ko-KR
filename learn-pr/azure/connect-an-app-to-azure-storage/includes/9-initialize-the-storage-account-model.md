Azure Storage 클라이언트 라이브러리는 Azure Storage 계정과 상호 작용하는 데 사용되는 개체 모델을 제공합니다. 이 개체 모델을 통해 Azure Storage 계정에 빠르게 연결하고 Azure Storage 서비스 API를 사용합니다. 

## <a name="azure-storage-client-library-object-model"></a>Azure Storage 클라이언트 라이브러리 개체 모델

::: zone pivot="csharp"

.NET Core 클라이언트 라이브러리에 있는 저장소 계정 개체 모델의 기반은 `CloudStorageAccount` 클래스입니다. 개체 모델을 초기화하는 가장 간단한 방법은 `CloudStorageAccount.Parse` 또는 `CloudStorageAccount.TryParse`를 사용하여 연결 문자열을 구문 분석하는 것입니다.

> [!NOTE]
> 클라이언트 라이브러리는 라이브러리가 필요한 작업이 호출될 때까지 연결을 시도하지 않습니다. `Parse()` 및 `TryParse()`는 연결 문자열 형식이 올바르게 지정되도록 보장할 뿐, 계정이 존재하는지 또는 키가 올바른지는 확인하지 않습니다. 

`Parse()` 또는 `TryParse()` 메서드 호출에서 반환된 결과 `CloudStorageAccount` 인스턴스는 Blob, File, Table 또는 Queue Storage 유형에 대한 클라이언트를 만드는 메서드를 표시합니다. 

아래 코드 조각은 Blob Storage에 사용할 클라이언트를 만드는 예제를 보여 줍니다.

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient()
```

`CloudStorageAccount` 및 클라이언트 개체는 경량이며, 응용 프로그램 내에서 미리 공유되도록 만들거나 요청 시 만들 수 있습니다. 표준 접근 방식은 응용 프로그램의 진입점 가까이에 `CloudStorageAccount.TryParse()`를 사용하여 인스턴스를 만들고 클라이언트 인스턴스를 만들기 위해 응용 프로그램 내에서 사용할 수 있도록 하는 것입니다.

특정 저장소 유형에 대한 클라이언트 개체가 있으면 메서드를 사용하여 실제 작업을 수행할 수 있습니다. 네트워크 호출을 생성하는 메서드는 의도적으로 비동기식입니다. .NET에서는 `async` 및 `await` 키워드를 사용하여 이러한 메서드를 효율적으로 처리합니다.

예를 들어 `CloudBlobClient`를 사용하여 _BLOB 컨테이너_를 만들고 BLOB 저장소에 파일을 업로드할 수 있습니다.

```csharp
// Create a local CloudBlobContainer object. No network call.
string containerName = "myblobcontainer";
CloudBlobContainer blobContainer = blobClient.GetContainerReference(containerName);

// This makes an actual service call to the Azure Storage service. 
// Unless this call fails, the container will have been created.
await blobContainer.CreateAsync();

// Create a local object to represent our blob. No network call.
string blobName = "myphoto";
CloudBlockBlob blob = blobContainer.GetBlockBlobReference(blobName);

// This transfers data in the file to the blob on the service.
string filename = "photo.png";
await blob.UploadFromFileAsync(fileName);
```

::: zone-end

::: zone-pivot="javascript"

**Node.js 및 JavaScript용 Microsoft Azure Storage 클라이언트 라이브러리**에 있는 저장소 계정 개체 모델의 기초는 `azurestorage` 개체입니다. 이것은 `require` 문을 통해 앱에 **azure-storage** 모듈을 추가하여 생성됩니다.

```javascript
const storage = require('azure-storage');
```

이 개체는 일련의 _factory_ 메서드를 제공합니다. 이 메서드는 Azure 저장소의 각 패싯과 작동할 특정 개체를 생성합니다. `createXXX` 메서드를 호출하여 각 개체를 생성합니다.

| 형식 | 방법 | 반환 |
|--------|---------|-------------|
| **Blob** | `createBlobService` | `BlobService` |
| **테이블** | `createTableService` | `TableService` |
| **큐** | `createQueueService` | `QueueService` |
| **파일** | `createFileService` | `FileService` |

> [!NOTE]
> 클라이언트 라이브러리는 라이브러리가 필요한 작업이 호출될 때까지 연결을 시도하지 않습니다. 이러한 각 `create` 메서드는 저장소 유형에 대한 액세스를 나타내는 경량 개체를 반환합니다. 사용 중인 연결 또는 액세스 키의 유효성을 검사하지 않습니다. 

특정 저장소 유형에 대한 서비스 개체가 있으면 메서드를 사용하여 실제 작업을 수행할 수 있습니다. 네트워크 호출을 생성하는 메서드는 의도적으로 비동기식입니다. 라이브러리는 현재 _callback_을 지원하여 비동기 결과를 반환합니다. 예를 들어, 다음은 Blob 컨테이너를 만드는 코드입니다.

```javascript
var azure = require('azure-storage');
var blobService = azure.createBlobService();

blobService.createContainerIfNotExists('myblobcontainer', function(err, result, response) {
  if (!err) {
    // if result.created = true, container was created.
    // if result.created = false, container already existed.
  }
});
```

이 방식은 정상적으로 작동하지만 콜백에 추가되는 코드가 많아져서 관리가 어려워질 수 있습니다. JavaScript의 더 나은 방법은 _promises_를 사용하여 이 메서드로 작업하는 것입니다. callback 스타일의 메서드를 promise로 변환하는 유용한 라이브러리가 몇 가지 있으며 원하는 라이브러리를 선택할 수 있습니다.

여기에서는 노드의 `util.promisify` 기능과 `BlobService`를 사용하여 컨테이너를 만들고 Blob 저장소에 파일을 업로드합니다. 또한 `async` 및 `await` 키워드를 사용하여 promise를 보다 자연스럽게 사용합니다.

```javascript
const util = require('util');
const storage = require('azure-storage');

const blobService = storage.createBlobService();
const createContainerAsync = util.promisify(blobService.createContainerIfNotExists).bind(blobService);
const uploadBlobAsync = util.promisify(blobService.createBlockBlobFromLocalFile).bind(blobService);

async function main() {
    try {
        // This makes an actual service call to the Azure Storage service. 
        // Unless this call fails, the container will have been created.
        await createContainerAsync(containerName);

        // This transfers data in the file to the blob on the service.
        var uploadResult = await uploadBlobAsync(containerName, "myphoto", "photo.png");
        if (uploadResult) {
            console.log("blob uploaded");
        }
    }
    catch (err) {
        console.log(err.message);
    }
}

main();
```
::: zone-end

이것을 앱에서 시도해 보겠습니다.