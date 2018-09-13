다음은 Azure Blob Storage를 사용하는 앱의 일반적인 워크플로입니다.

1. **구성 검색**: 시작 시 저장소 계정 구성을 로드합니다. 이는 일반적으로 저장소 계정 연결 문자열입니다.

1. **클라이언트 초기화**: 연결 문자열을 사용하여 Azure Storage 클라이언트 라이브러리를 초기화합니다. 이렇게 하면 앱이 Blob Storage API로 작업하는 데 사용할 개체가 생성됩니다.

1. **사용**: 클라이언트 라이브러리를 사용하여 컨테이너 및 Blob에서 작동하는 API 호출을 만듭니다.

## <a name="configure-your-connection-string"></a>연결 문자열 구성

코드를 작성하기 전에 사용할 저장소 계정에 대한 연결 문자열이 필요합니다.

저장소 계정 연결 문자열에는 계정 키가 포함됩니다. 계정 키는 비밀로 간주하며 안전하게 저장되어야 합니다. 여기서 연결 문자열을 App Service 응용 프로그램 설정에 저장합니다. App Service 응용 프로그램 설정은 응용 프로그램 비밀을 저장할 안전한 장소이지만, 이 디자인은 로컬 개발을 지원하지 않고 단독으로는 강력한 종단 간 솔루션이 아닙니다.

> [!WARNING]
> **저장소 계정 키를 코드 또는 보호되지 않은 구성 파일에 저장하지 마세요.** 저장소 계정 키는 저장소 계정에 대한 전체 액세스를 가능하게 합니다. 키가 유출되면 복구할 수 없는 피해와 상당한 요금이 발생할 수 있습니다. 저장소 지침 및 유출된 키에서 복구하는 방법에 대한 조언은 이 모듈의 끝에 있는 추가 참고 자료 섹션을 참조하세요.

## <a name="initialize-the-blob-storage-object-model"></a>Blob Storage 개체 모델 초기화

.NET Core용 Azure Storage SDK에서 Blob Storage를 사용하는 표준 패턴은 다음 단계로 구성됩니다.

1. 연결 문자열로 `CloudStorageAccount.Parse`(또는 `TryParse`)를 호출하여 `CloudStorageAccount`를 가져옵니다.

1. `CloudStorageAccount`에서 `CreateCloudBlobClient`를 호출하여 `CloudBlobClient`를 가져옵니다.

1. `CloudBlobClient`에서 `GetContainerReference`를 호출하여 `CloudBlobContainer`를 가져옵니다.

1. 컨테이너에서 메서드를 사용하여 Blob 목록을 가져오거나 개별 Blob에 대한 참조를 가져와 데이터를 업로드 및 다운로드합니다.

코드에서 1&ndash;3단계는 다음과 같습니다.

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

이 초기화 코드는 네트워크를 통해 호출하지 않습니다. 이는 잘못된 정보로 인해 발생하는 일부 예외가 나중에도 throw되지 않음을 의미합니다. 예를 들어 `CloudStorageAccount.Parse` 호출은 연결 문자열의 형식이 잘못 지정될 경우 즉시 예외를 throw하지만, 연결 문자열이 가리키는 저장소 계정이 존재하지 않는 경우에는 예외가 throw되지 않습니다.

## <a name="create-containers-at-startup"></a>시작 시 컨테이너 만들기

`CloudBlobContainer`에서 `CreateIfNotExistsAsync`를 호출하는 것은 응용 프로그램이 시작되거나 응용 프로그램을 처음 사용하려고 할 때 컨테이너를 만드는 가장 좋은 방법입니다.

컨테이너가 이미 있는 경우 `CreateIfNotExistsAsync`는 예외를 throw하지 않지만 Azure Storage에 대한 네트워크 호출을 수행합니다. 컨테이너를 사용할 때마다가 아니라 초기화 중에 한 번 호출합니다.

## <a name="exercise"></a>연습

### <a name="clone-and-explore-the-unfinished-app"></a>완료되지 않은 앱 복제 및 살펴보기

먼저 GitHub의 시작 앱을 복제해 보겠습니다. Cloud Shell 터미널에서 다음 명령을 실행하여 소스 코드의 복사본을 가져오고 편집기에서 엽니다.

**최종 리포지토리 URL에 대한 TODO 업데이트**

```console
git clone https://github.com/nickwalkmsft/FileUploader.git
cd FileUploader
code .
```

`Controllers/FilesController.cs`파일을 엽니다. 여기에서 수행할 작업이 없지만 앱이 수행하는 작업을 빠르게 확인하려고 합니다.

이 컨트롤러는 다음과 같은 세 가지 작업으로 API를 구현합니다.

- **인덱스**(GET /api/Files)는 업로드된 각 파일에 하나씩 URL 목록을 반환합니다. 앱 프런트 엔드는 이 메서드를 호출하여 업로드된 파일에 대한 하이퍼링크 목록을 빌드합니다.
- **업로드**(POST /api/Files)는 업로드된 파일을 수신하고 저장합니다.
- **다운로드**(GET /api/Files/{filename})는 해당 이름으로 개별 파일을 다운로드합니다.

각 메서드는 `storage`라는 `IStorage` 인스턴스를 사용하여 작업을 수행합니다. 입력하려는 `Models/BlobStorage.cs`에 `IStorage`의 불완전한 구현이 있습니다.

### <a name="add-the-nuget-package"></a>NuGet 패키지 추가

먼저 Azure Storage SDK에 참조를 추가합니다. 터미널에서 다음을 실행합니다.

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

이렇게 하면 최신 버전의 Blob Storage 클라이언트 라이브러리를 사용하게 됩니다.

### <a name="configure"></a>구성

앱을 실행하는 데 필요한 구성 값은 저장소 계정 연결 문자열이고 컨테이너의 이름은 앱이 파일을 저장하는 데 사용됩니다. 이 단원에서는 Azure App Service에서 앱을 실행하기만 하므로 App Service 모범 사례를 따르고 App Service 응용 프로그램 설정에 값을 저장합니다. App Service 인스턴스를 만들 때 작업을 수행하므로 지금은 작업을 수행할 필요가 없습니다.

구성을 ‘사용’할 때 시작 앱에는 이미 필요한 구성 연결이 포함되어 있습니다. `BlobStorage`의 `IOptions<AzureStorageConfig>` 생성자 매개 변수에는 두 개의 속성인 저장소 계정 연결 문자열 및 앱이 Blob을 저장하는 컨테이너의 이름이 있습니다. `Startup.cs`의 `ConfigureServices` 메서드에 앱이 시작될 때 구성에서 값을 로드하는 코드가 있습니다.

### <a name="initialize"></a>초기화

`Models/BlobStorage.cs`를 엽니다. 다음 `using` 문을 파일 위쪽에 추가하여 연습 중에 추가할 코드를 준비합니다.

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

`Initialize` 메서드를 찾습니다. 앱은 `BlobStorage`가 처음 사용될 때 이 메서드를 호출합니다. 필요한 경우 `Startup.cs`에서 `ConfigureServices`를 확인하여 이 작업을 수행하는 방법을 확인할 수 있습니다.

`Initialize`에서 컨테이너를 만들려고 합니다(아직 없는 경우). 현재 `Initialize` 구현을 다음 코드로 바꾸고 작업을 저장합니다.

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```