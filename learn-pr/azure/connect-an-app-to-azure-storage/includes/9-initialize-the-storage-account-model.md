Azure Storage 클라이언트 라이브러리는 Azure Storage 계정과 상호 작용하는 데 사용되는 개체 모델을 제공합니다. 이 개체 모델을 통해 Azure Storage 계정에 빠르게 연결하고 Azure Storage 서비스 API를 사용합니다. 

## <a name="azure-storage-client-library-object-model"></a>Azure Storage 클라이언트 라이브러리 개체 모델

::: zone pivot="csharp"

.NET Core 클라이언트 라이브러리의 저장소 계정 개체 모델의 기초 클래스인 `CloudStorageAccount`합니다. 개체 모델을 초기화하는 가장 간단한 방법은 `CloudStorageAccount.Parse` 또는 `CloudStorageAccount.TryParse`를 사용하여 연결 문자열을 구문 분석하는 것입니다.

> [!NOTE]
> 클라이언트 라이브러리는 라이브러리가 필요한 작업이 호출될 때까지 연결을 시도하지 않습니다. `Parse()` 및 `TryParse()`는 연결 문자열 형식이 올바르게 지정되도록 보장할 뿐, 계정이 존재하는지 또는 키가 올바른지는 확인하지 않습니다. 

결과 `CloudStorageAccount` 에서 반환 된 인스턴스를 `Parse()` 또는 `TryParse()` 메서드 호출 클라이언트를 Azure Blob, 파일, 큐 및 Table storage 서비스에 액세스 하는 개체를 만드는 메서드를 노출 합니다. 

아래 코드 조각은 Blob Storage에 사용할 클라이언트를 만드는 예제를 보여 줍니다.

```csharp
using Microsoft.WindowsAzure.Storage;

CloudStorageAccount storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");

CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient()
```

`CloudStorageAccount` 및 클라이언트 개체는 경량이며, 응용 프로그램 내에서 미리 공유되도록 만들거나 요청 시 만들 수 있습니다. 표준 접근 방식은 응용 프로그램의 진입점에 가까운 `CloudStorageAccount.TryParse()`를 사용하여 인스턴스를 만들고 클라이언트 인스턴스를 만들기 위해 응용 프로그램 내에서 사용할 수 있게 합니다.

특정 저장소 형식으로 클라이언트 개체를 만든 후에 실제 작업을 수행할 메서드를 사용할 수 있습니다. 네트워크 호출을 수행 하는 메서드는 의도적으로 비동기-.NET에서 사용 합니다 `async` 및 `await` 효율적으로 이러한 메서드를 사용 하는 키워드입니다.

예를 들어 사용할 수 있습니다 합니다 `CloudBlobClient` 만들려면를 _blob 컨테이너_ blob storage로 파일을 업로드 합니다.

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

::: zone pivot="javascript"

저장소 계정 개체 모델의 기초를 **Node.js 및 JavaScript 용 Microsoft Azure Storage 클라이언트 라이브러리** 는 `azurestorage` 개체입니다. 추가 하 여 만들어집니다를 **azure storage** 모듈을 통해 앱을 `require` 문입니다.

```javascript
const storage = require('azure-storage');
```

이 개체는 일련의 제공 _팩터리_ 각 패싯 별로 Azure storage를 사용 하려면 특정 개체를 만드는 방법. 호출 `createXXX` 각 개체를 만드는 방법.

| 유형 | 방법 | 반환 |
|--------|---------|-------------|
| **Blob** | `createBlobService` | `BlobService` |
| **테이블** | `createTableService` | `TableService` |
| **큐** | `createQueueService` | `QueueService` |
| **파일** | `createFileService` | `FileService` |

> [!NOTE]
> 클라이언트 라이브러리는 라이브러리가 필요한 작업이 호출될 때까지 연결을 시도하지 않습니다. 이러한 사항의 `create` 저장소 형식에 대 한 액세스를 나타내는 경량 개체를 반환 하는 메서드&mdash;연결 또는 사용 되는 액세스 키를 확인 하지 않습니다.

특정 저장소 형식으로 서비스 개체를 만든 후에 실제 작업을 수행할 메서드를 사용할 수 있습니다. 네트워크 호출을 수행 하는 메서드는 의도적으로 비동기적입니다. 라이브러리는 현재 지원 _콜백을_ 비동기 결과를 반환 합니다. 예를 들어, blob 컨테이너를 만드는 코드가입니다.

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

이 방법은 제대로 작동 하지만 많아지기 때문 얻을 수 있는 콜백을 추가 되 고 코드를 많이 발생할 지는 경향이 있습니다. JavaScript에서 더 나은 방법은 사용 하는 것 _약속_ 이러한 메서드를 사용 하 여 작동 합니다. 약속에 스타일 콜백 메서드를 변환 하는 몇 가지 유용한 라이브러리는&mdash;원하는 것을 선택할 수 있습니다.

여기에서 사용 하 여는 `util.promisify` 노드를 사용 하 여 기능을 `BlobService` 컨테이너를 만들고 blob 저장소에 파일을 업로드 합니다. 에서는 또한 합니다 `async` 및 `await` 조금 더 자연스럽 게 된 프라미스를 사용 하는 키워드입니다.

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

앱에서이 사용해 보겠습니다.