<span data-ttu-id="e1be3-101">다음은 Azure Blob Storage를 사용하는 앱의 일반적인 워크플로입니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="e1be3-102">**구성 검색**: 시작 시 계정 키와 함께 연결 문자열과 같은 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-102">**Retrieve configuration**: At startup, load the configuration, such as the connection string with the account key.</span></span> <span data-ttu-id="e1be3-103">이 구성은 API 호출을 인증하는 데 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-103">This is needed to authenticate API calls.</span></span>
1. <span data-ttu-id="e1be3-104">**클라이언트 초기화**: 연결 문자열을 사용하여 Azure Storage 클라이언트 라이브러리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="e1be3-105">이렇게 하면 앱이 Blob Storage API로 작업하는 데 사용할 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="e1be3-106">**사용**: 클라이언트 라이브러리를 사용하여 컨테이너 및 Blob에서 작동하는 API 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="e1be3-107">연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="e1be3-107">Configure your connection string</span></span>

<span data-ttu-id="e1be3-108">코드를 작성하기 전에 사용할 저장소 계정에 대한 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span> 

<span data-ttu-id="e1be3-109">연결 문자열에는 계정 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-109">The connection string includes your account key.</span></span> <span data-ttu-id="e1be3-110">계정 키는 비밀로 간주하며 안전하게 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="e1be3-111">연결 문자열을 App Service 응용 프로그램 설정에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-111">We will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="e1be3-112">응용 프로그램 설정은 응용 프로그램 비밀을 저장할 안전한 장소이지만, 로컬 개발을 지원하지 않고 단독으로는 강력한 종단 간 솔루션이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-112">An application setting is a secure place for application secrets, but it does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="e1be3-113">**저장소 계정 키를 코드 또는 보호되지 않은 구성 파일에 저장하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="e1be3-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="e1be3-114">저장소 계정 키는 저장소 계정에 대한 전체 액세스를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="e1be3-115">키가 유출되면 복구할 수 없는 피해와 상당한 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="e1be3-116">저장소 지침 및 유출된 키에서 복구하는 방법에 대한 조언은 이 모듈의 끝에 있는 추가 리소스 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e1be3-116">See the Additional Resources section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="e1be3-117">Blob Storage 개체 모델 초기화</span><span class="sxs-lookup"><span data-stu-id="e1be3-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="e1be3-118">.NET Core용 Azure Storage SDK에서 Blob Storage를 사용하는 표준 패턴은 다음 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="e1be3-119">연결 문자열로 `CloudStorageAccount.Parse`(또는 `TryParse`)를 호출하여 `CloudStorageAccount`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="e1be3-120">`CloudStorageAccount`에서 `CreateCloudBlobClient`를 호출하여 `CloudBlobClient`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="e1be3-121">`CloudBlobClient`에서 `GetContainerReference`를 호출하여 `CloudBlobContainer`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="e1be3-122">컨테이너에서 메서드를 사용하여 Blob 목록을 가져오거나 개별 Blob에 대한 참조를 가져와 데이터를 업로드 및 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="e1be3-123">코드에서 1&ndash;3단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="e1be3-124">이 초기화 코드는 네트워크를 통해 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="e1be3-125">이는 잘못된 정보에서 발생하는 예외가 후반까지 throw되지 않음을 의미합니다. 예를 들어 컨테이너가 실제로 계정에 존재하는지 여부에 관계없이 `GetContainerReference` 호출이 성공합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-125">This means exceptions that occur from incorrect information won't be thrown until later; for example, the call to `GetContainerReference` will succeed whether or not the container actually exists in the account.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="e1be3-126">시작 시 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="e1be3-126">Create containers at startup</span></span>

<span data-ttu-id="e1be3-127">일반적인 사례는 선행되는 컨테이너를 알고 있는 경우에도 응용 프로그램이 코드에서 필요한 컨테이너를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-127">Common practice is for applications to create needed containers in code, even when we know what those containers will be up-front.</span></span> <span data-ttu-id="e1be3-128">`CloudBlobContainer`에서 `CreateIfNotExistsAsync`를 호출하는 것은 이 작업을 수행하는 가장 적합한 방법이고, 컨테이너를 사용하기 전에 필요할 것을 알고 있는 각 컨테이너를 만들려면 이 방법을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to do this, and we should use it to create each container we know we'll need before we use them.</span></span>

<span data-ttu-id="e1be3-129">`CreateIfNotExistsAsync`는 Azure Storage에 대한 네트워크 호출을 ‘수행’합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-129">`CreateIfNotExistsAsync` *does* make a network call to Azure Storage.</span></span> <span data-ttu-id="e1be3-130">모범 사례는 컨테이너에 액세스할 때마다가 아니라 시작 시 한 번 호출하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-130">Best practice is to call it once at startup and not every time we access a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="e1be3-131">연습</span><span class="sxs-lookup"><span data-stu-id="e1be3-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="e1be3-132">완료되지 않은 앱 복제 및 살펴보기</span><span class="sxs-lookup"><span data-stu-id="e1be3-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="e1be3-133">먼저 GitHub의 시작 앱을 복제해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="e1be3-134">Cloud Shell 터미널에서 다음 명령을 실행하여 원본 코드의 복사본을 가져오고 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

```console
git clone TODO
cd TODO
code .
```

<span data-ttu-id="e1be3-135">`Controllers/FilesController.cs`파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-135">Open the file `Controllers/FilesController.cs`.</span></span>

<span data-ttu-id="e1be3-136">이 컨트롤러는 다음과 같은 세 가지 작업으로 API를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-136">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="e1be3-137">**인덱스**(GET /api/Files)는 업로드된 각 파일에 하나씩 URL 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-137">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="e1be3-138">앱 프런트 엔드는 이 메서드를 호출하여 업로드된 파일에 대한 하이퍼링크 목록을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-138">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="e1be3-139">**업로드**(POST /api/Files)는 업로드된 파일을 수신하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-139">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="e1be3-140">**다운로드**(GET /api/Files/{file-name})는 해당 이름으로 개별 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-140">**Download** (GET /api/Files/{file-name}) downloads an individual file by its name.</span></span>

<span data-ttu-id="e1be3-141">각 메서드는 `storage`라는 `IStorage` 인스턴스를 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-141">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="e1be3-142">`Models/BlobStorage.cs`에 `IStorage`의 불완전한 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-142">There is an incomplete implementation of `IStorage` in  `Models/BlobStorage.cs`.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="e1be3-143">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="e1be3-143">Add the NuGet package</span></span>

<span data-ttu-id="e1be3-144">먼저 Azure Storage SDK에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-144">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="e1be3-145">터미널에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-145">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="e1be3-146">이렇게 하면 최신 버전의 Blob Storage 클라이언트 라이브러리를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-146">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="e1be3-147">구성</span><span class="sxs-lookup"><span data-stu-id="e1be3-147">Configure</span></span>

<span data-ttu-id="e1be3-148">시작 앱에는 이미 필요한 구성 연결이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-148">Our starter app already includes the configuration plumbing we need.</span></span> <span data-ttu-id="e1be3-149">`BlobStorage`의 `IOptions<AzureStorageConfig>` 생성자 매개 변수에는 두 개의 속성인 저장소 계정 연결 문자열 및 앱이 Blob을 저장하는 컨테이너의 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-149">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="e1be3-150">`Startup.cs`의 `ConfigureServices` 메서드에 앱이 시작될 때 구성에서 값을 로드하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-150">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

<span data-ttu-id="e1be3-151">이 연습에서는 Azure App Service에서 앱을 실행하므로 나중에 App Service 응용 프로그램 설정에 구성 값을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-151">In this exercise, we will run the app in Azure App Service, so we will add the configuration values to the App Service application settings later.</span></span> <span data-ttu-id="e1be3-152">이제는 구성과 관련된 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-152">For now, we don't need to do any work related to configuration.</span></span>

### <a name="initialize"></a><span data-ttu-id="e1be3-153">초기화</span><span class="sxs-lookup"><span data-stu-id="e1be3-153">Initialize</span></span>

<span data-ttu-id="e1be3-154">`BlobStorage.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-154">Open `BlobStorage.cs`.</span></span>

<span data-ttu-id="e1be3-155">`Initialize` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-155">Location the `Initialize` method.</span></span> <span data-ttu-id="e1be3-156">앱은 처음 사용할 때 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-156">Our app will call this method when it's first used.</span></span> <span data-ttu-id="e1be3-157">필요한 경우 `Startup.cs`에서 `ConfigureServices`를 확인하여 이 작업을 수행하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-157">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span> 

<span data-ttu-id="e1be3-158">`Initialize`에서 컨테이너를 만들려고 합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="e1be3-158">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="e1be3-159">다음 코드로 `Initialize`를 채우고 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e1be3-159">Fill in `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```