Azure Storage 클라이언트 라이브러리는 Azure Storage 계정으로 조작하는 데 사용되는 개체 모델을 제공합니다. 이러한 개체 모델을 통해 Azure Storage 계정에 빠르게 연결하고 Azure Storage 서비스 API를 사용합니다. 

여기서는 코드에 계정 개체 모델을 사용하여 Azure Storage 계정에 연결합니다.

## <a name="azure-storage-client-library-object-model"></a>Azure Storage 클라이언트 라이브러리 개체 모델

Azure Storage 클라이언트 라이브러리 개체 모델을 사용하는 방법을 이해하는 것이 Azure Storage 계정에 연결하는 경우의 간편한 구현에 매우 중요합니다.

.NET Core 클라이언트 라이브러리에 있는 저장소 계정 개체 모델의 기반은 **CloudStorageAccount**입니다. 개체 모델을 초기화하는 가장 간단한 방법은 `CloudStorageAccount.Parse` 또는 `CloudStorageAccount.TryParse`를 사용하여 연결 문자열을 구문 분석하는 것입니다.

클라이언트 라이브러리는 라이브러리가 필요한 작업이 호출될 때까지 연결을 시도하지 않습니다. `Parse()` 및 `TryParse()`는 연결 문자열 형식이 올바르게 지정되도록 보장할 뿐입니다. 계정이 존재하는지 또는 키가 올바른지는 확인하지 않습니다. `Parse()` 또는 `TryParse()` 메서드 호출에서 반환된 결과 `CloudStorageAccount` 인스턴스는 Blob, File, Table 또는 Queue Storage 유형에 대한 클라이언트를 만드는 메서드를 표시합니다. Blob, File, Queue 및 Table Storage 서비스에 대한 서비스 클라이언트 개체 인스턴스를 만드는 데 사용됩니다. 아래 코드 조각은 Blob Storage에 사용할 클라이언트를 만드는 예제를 보여 줍니다.

```c#
using Microsoft.WindowsAzure.Storage;

var storageAccount = CloudStorageAccount.Parse("your-storage-key-connection-string");
var blobClient = storageAccount.CreateCloudBlobClient()
```

응용 프로그램 내에서 요청 시 또는 미리 공유되도록 만들 수 있는 `CloudStorageAccount` 및 클라이언트 개체는 경량입니다. 표준 접근 방식은 응용 프로그램의 진입점 가까이에 `CloudStorageAccount.TryParse()`를 사용하여 인스턴스를 만들고 클라이언트 인스턴스를 만들기 위해 응용 프로그램 내에서 사용할 수 있도록 하는 것입니다.

## <a name="summary"></a>요약

Azure Storage 클라이언트 라이브러리 개체 모델은 간편하게 Azure Storage 계정에 연결하는 방법을 제공합니다. 사용자가 연결 문자열을 제공하기만 하면 개체 모델이 해당 형식을 확인하고 계정이 존재하는지 확인합니다. `CloudStorageAccount` 인스턴스가 있으면 Blob, File, Table 또는 Queue Storage 유형에 대한 클라이언트를 만들 수 있습니다.