<span data-ttu-id="21761-101">다음은 Azure Blob Storage를 사용하는 앱의 일반적인 워크플로입니다.</span><span class="sxs-lookup"><span data-stu-id="21761-101">The following is the typical workflow for apps that use Azure Blob storage:</span></span>

1. <span data-ttu-id="21761-102">**구성 검색**: 시작 시 저장소 계정 구성을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-102">**Retrieve configuration**: At startup, load the storage account configuration.</span></span> <span data-ttu-id="21761-103">이는 일반적으로 저장소 계정 연결 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="21761-103">This is typically a storage account connection string.</span></span>
1. <span data-ttu-id="21761-104">**클라이언트 초기화**: 연결 문자열을 사용하여 Azure Storage 클라이언트 라이브러리를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-104">**Initialize client**: Use the connection string to initialize the Azure Storage client library.</span></span> <span data-ttu-id="21761-105">이렇게 하면 앱이 Blob Storage API로 작업하는 데 사용할 개체가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="21761-105">This creates the objects the app will use to work with the Blob storage API.</span></span>
1. <span data-ttu-id="21761-106">**사용**: 클라이언트 라이브러리를 사용하여 컨테이너 및 Blob에서 작동하는 API 호출을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="21761-106">**Use**: Make API calls with the client library to operate on containers and blobs.</span></span>

## <a name="configure-your-connection-string"></a><span data-ttu-id="21761-107">연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="21761-107">Configure your connection string</span></span>

<span data-ttu-id="21761-108">코드를 작성하기 전에 사용할 저장소 계정에 대한 연결 문자열이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-108">Before writing any code, you'll need the connection string for the storage account you will use.</span></span>

<span data-ttu-id="21761-109">저장소 계정 연결 문자열에는 계정 키가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="21761-109">Storage account connection strings include the account key.</span></span> <span data-ttu-id="21761-110">계정 키는 비밀로 간주하며 안전하게 저장되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-110">The account key is considered a secret and should be stored securely.</span></span> <span data-ttu-id="21761-111">여기서 연결 문자열을 App Service 응용 프로그램 설정에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-111">Here, we will store the connection string in an App Service application setting.</span></span> <span data-ttu-id="21761-112">App Service 응용 프로그램 설정은 응용 프로그램 비밀을 저장할 안전한 장소이지만, 이 디자인은 로컬 개발을 지원하지 않고 단독으로는 강력한 종단 간 솔루션이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="21761-112">App Service application settings are a secure place for application secrets, but this design does not support local development and is not a robust, end-to-end solution on its own.</span></span>

> [!WARNING]
> <span data-ttu-id="21761-113">**저장소 계정 키를 코드 또는 보호되지 않은 구성 파일에 저장하지 마세요.**</span><span class="sxs-lookup"><span data-stu-id="21761-113">**Do not place storage account keys in code or in unprotected configuration files.**</span></span> <span data-ttu-id="21761-114">저장소 계정 키는 저장소 계정에 대한 전체 액세스를 가능하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-114">Storage account keys enable full access to your storage account.</span></span> <span data-ttu-id="21761-115">키가 유출되면 복구할 수 없는 피해와 상당한 요금이 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-115">Leaking a key can result in unrecoverable damage and large bills.</span></span> <span data-ttu-id="21761-116">저장소 지침 및 유출된 키에서 복구하는 방법에 대한 조언은 이 모듈의 끝에 있는 추가 참고 자료 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="21761-116">See the Further Reading section at the end of this module for storage guidance and advice about how to recover from a leaked key.</span></span>

## <a name="initialize-the-blob-storage-object-model"></a><span data-ttu-id="21761-117">Blob Storage 개체 모델 초기화</span><span class="sxs-lookup"><span data-stu-id="21761-117">Initialize the Blob storage object model</span></span>

<span data-ttu-id="21761-118">.NET Core용 Azure Storage SDK에서 Blob Storage를 사용하는 표준 패턴은 다음 단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="21761-118">In the Azure Storage SDK for .NET Core, the standard pattern for using Blob storage consists of the following steps:</span></span>

1. <span data-ttu-id="21761-119">연결 문자열로 `CloudStorageAccount.Parse`(또는 `TryParse`)를 호출하여 `CloudStorageAccount`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21761-119">Call `CloudStorageAccount.Parse` (or `TryParse`) with your connection string to get a `CloudStorageAccount`.</span></span>
1. <span data-ttu-id="21761-120">`CloudStorageAccount`에서 `CreateCloudBlobClient`를 호출하여 `CloudBlobClient`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21761-120">Call `CreateCloudBlobClient` on the `CloudStorageAccount` to get a `CloudBlobClient`.</span></span>
1. <span data-ttu-id="21761-121">`CloudBlobClient`에서 `GetContainerReference`를 호출하여 `CloudBlobContainer`를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="21761-121">Call `GetContainerReference` on the `CloudBlobClient` to get a `CloudBlobContainer`.</span></span>
1. <span data-ttu-id="21761-122">컨테이너에서 메서드를 사용하여 Blob 목록을 가져오거나 개별 Blob에 대한 참조를 가져와 데이터를 업로드 및 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-122">Use methods on the container to get a list of blobs and/or get references to individual blobs to upload and download data.</span></span>

<span data-ttu-id="21761-123">코드에서 1&ndash;3단계는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-123">In code, steps 1&ndash;3 look like this:</span></span>

```csharp
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString); // or TryParse()
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
CloudBlobContainer container = blobClient.GetContainerReference(containerName);
```

<span data-ttu-id="21761-124">이 초기화 코드는 네트워크를 통해 호출하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-124">None of this initialization code makes calls over the network.</span></span> <span data-ttu-id="21761-125">이는 잘못된 정보로 인해 발생하는 일부 예외가 나중에도 throw되지 않음을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-125">This means that some exceptions that occur because of incorrect information won't be thrown until later.</span></span> <span data-ttu-id="21761-126">예를 들어 `CloudStorageAccount.Parse` 호출은 연결 문자열의 형식이 잘못 지정될 경우 즉시 예외를 throw하지만, 연결 문자열이 가리키는 저장소 계정이 존재하지 않는 경우에는 예외가 throw되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-126">For example, the call to `CloudStorageAccount.Parse` will throw an exception immediately if the connection string is formatted incorrectly, but no exception will be thrown if the storage account that a connection string points to doesn't exist.</span></span>

## <a name="create-containers-at-startup"></a><span data-ttu-id="21761-127">시작 시 컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="21761-127">Create containers at startup</span></span>

<span data-ttu-id="21761-128">`CloudBlobContainer`에서 `CreateIfNotExistsAsync`를 호출하는 것은 응용 프로그램이 시작되거나 응용 프로그램을 처음 사용하려고 할 때 컨테이너를 만드는 가장 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="21761-128">Calling `CreateIfNotExistsAsync` on a `CloudBlobContainer` is the best way to create a container when your application starts or when it first tries to use it.</span></span>

<span data-ttu-id="21761-129">컨테이너가 이미 있는 경우 `CreateIfNotExistsAsync`는 예외를 throw하지 않지만 Azure Storage에 대한 네트워크 호출을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-129">`CreateIfNotExistsAsync` won't throw an exception if the container already exists, but it does make a network call to Azure Storage.</span></span> <span data-ttu-id="21761-130">컨테이너를 사용할 때마다가 아니라 초기화 중에 한 번 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-130">Call it once during initialization, not every time you try to use a container.</span></span>

## <a name="exercise"></a><span data-ttu-id="21761-131">연습</span><span class="sxs-lookup"><span data-stu-id="21761-131">Exercise</span></span>

### <a name="clone-and-explore-the-unfinished-app"></a><span data-ttu-id="21761-132">완료되지 않은 앱 복제 및 살펴보기</span><span class="sxs-lookup"><span data-stu-id="21761-132">Clone and explore the unfinished app</span></span>

<span data-ttu-id="21761-133">먼저 GitHub의 시작 앱을 복제해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-133">First, let's clone the starter app from GitHub.</span></span> <span data-ttu-id="21761-134">Cloud Shell 터미널에서 다음 명령을 실행하여 소스 코드의 복사본을 가져오고 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="21761-134">In the Cloud Shell terminal, run the following command to get a copy of the source code and open it in the editor:</span></span>

<span data-ttu-id="21761-135">**최종 리포지토리 URL에 대한 TODO 업데이트**</span><span class="sxs-lookup"><span data-stu-id="21761-135">**TODO update to final repo URL**</span></span>

```console
git clone https://github.com/nickwalkmsft/FileUploader.git
cd FileUploader
code .
```

<span data-ttu-id="21761-136">`Controllers/FilesController.cs`파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="21761-136">Open the file `Controllers/FilesController.cs`.</span></span> <span data-ttu-id="21761-137">여기에서 수행할 작업이 없지만 앱이 수행하는 작업을 빠르게 확인하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-137">There's no work to do here, but we're going to have a quick look at what the app does.</span></span>

<span data-ttu-id="21761-138">이 컨트롤러는 다음과 같은 세 가지 작업으로 API를 구현합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-138">This controller implements an API with three actions:</span></span>

* <span data-ttu-id="21761-139">**인덱스**(GET /api/Files)는 업로드된 각 파일에 하나씩 URL 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-139">**Index** (GET /api/Files) returns a list of URLs, one for each file that's been uploaded.</span></span> <span data-ttu-id="21761-140">앱 프런트 엔드는 이 메서드를 호출하여 업로드된 파일에 대한 하이퍼링크 목록을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-140">The app front end calls this method to build a list of hyperlinks to the uploaded files.</span></span>
* <span data-ttu-id="21761-141">**업로드**(POST /api/Files)는 업로드된 파일을 수신하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-141">**Upload** (POST /api/Files) receives an uploaded file and saves it.</span></span>
* <span data-ttu-id="21761-142">**다운로드**(GET /api/Files/{filename})는 해당 이름으로 개별 파일을 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-142">**Download** (GET /api/Files/{filename}) downloads an individual file by its name.</span></span>

<span data-ttu-id="21761-143">각 메서드는 `storage`라는 `IStorage` 인스턴스를 사용하여 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-143">Each method uses an `IStorage` instance called `storage` to do its work.</span></span> <span data-ttu-id="21761-144">입력하려는 `Models/BlobStorage.cs`에 `IStorage`의 불완전한 구현이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-144">There is an incomplete implementation of `IStorage` in `Models/BlobStorage.cs` that we're going to fill in.</span></span>

### <a name="add-the-nuget-package"></a><span data-ttu-id="21761-145">NuGet 패키지 추가</span><span class="sxs-lookup"><span data-stu-id="21761-145">Add the NuGet package</span></span>

<span data-ttu-id="21761-146">먼저 Azure Storage SDK에 참조를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-146">First, add a reference to the Azure Storage SDK.</span></span> <span data-ttu-id="21761-147">터미널에서 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-147">In the terminal, run the following:</span></span>

```console
dotnet add package WindowsAzure.Storage
dotnet restore
```

<span data-ttu-id="21761-148">이렇게 하면 최신 버전의 Blob Storage 클라이언트 라이브러리를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="21761-148">This will make sure we're using the newest version of the Blob storage client library.</span></span>

### <a name="configure"></a><span data-ttu-id="21761-149">구성</span><span class="sxs-lookup"><span data-stu-id="21761-149">Configure</span></span>

<span data-ttu-id="21761-150">앱을 실행하는 데 필요한 구성 값은 저장소 계정 연결 문자열이고 컨테이너의 이름은 앱이 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="21761-150">The configuration values we need to run the app are the storage account connection string and the name of the container the app will use to store files.</span></span> <span data-ttu-id="21761-151">이 연습에서는 Azure App Service에서 앱을 실행하기만 하므로 App Service 모범 사례를 따르고 App Service 응용 프로그램 설정에 값을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-151">In this exercise, we're only going to run the app in Azure App Service, so we'll follow App Service best practice and store the values in App Service application settings.</span></span> <span data-ttu-id="21761-152">App Service 인스턴스를 만들 때 작업을 수행하므로 지금은 작업을 수행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-152">We'll do that when we create the App Service instance, so there's nothing we need to do at the moment.</span></span>

<span data-ttu-id="21761-153">구성을 ‘사용’할 때 시작 앱에는 이미 필요한 구성 연결이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-153">When it comes to *using* the configuration, our starter app already includes the plumbing we need.</span></span> <span data-ttu-id="21761-154">`BlobStorage`의 `IOptions<AzureStorageConfig>` 생성자 매개 변수에는 두 개의 속성인 저장소 계정 연결 문자열 및 앱이 Blob을 저장하는 컨테이너의 이름이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-154">The `IOptions<AzureStorageConfig>` constructor parameter in `BlobStorage` has two properties: the storage account connection string and the name of the container our app will store blobs in.</span></span> <span data-ttu-id="21761-155">`Startup.cs`의 `ConfigureServices` 메서드에 앱이 시작될 때 구성에서 값을 로드하는 코드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-155">There is code in the `ConfigureServices` method of `Startup.cs` that loads the values from configuration when the app starts.</span></span>

### <a name="initialize"></a><span data-ttu-id="21761-156">초기화</span><span class="sxs-lookup"><span data-stu-id="21761-156">Initialize</span></span>

<span data-ttu-id="21761-157">`Models/BlobStorage.cs`를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="21761-157">Open `Models/BlobStorage.cs`.</span></span> <span data-ttu-id="21761-158">다음 `using` 문을 파일 위쪽에 추가하여 연습 중에 추가할 코드를 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-158">Add the following `using` statements to the top of the file to prepare it for the code you're going to add during the exercise.</span></span>

```csharp
using System.Linq;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
```

<span data-ttu-id="21761-159">`Initialize` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-159">Locate the `Initialize` method.</span></span> <span data-ttu-id="21761-160">앱은 `BlobStorage`가 처음 사용될 때 이 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-160">Our app will call this method when `BlobStorage` is used for the first time.</span></span> <span data-ttu-id="21761-161">필요한 경우 `Startup.cs`에서 `ConfigureServices`를 확인하여 이 작업을 수행하는 방법을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="21761-161">If you're curious, you can look at `ConfigureServices` in `Startup.cs` to see how this is done.</span></span>

<span data-ttu-id="21761-162">`Initialize`에서 컨테이너를 만들려고 합니다(아직 없는 경우).</span><span class="sxs-lookup"><span data-stu-id="21761-162">`Initialize` is where we want to create our container if it doesn't already exist.</span></span> <span data-ttu-id="21761-163">현재 `Initialize` 구현을 다음 코드로 바꾸고 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="21761-163">Replace the current implementation of `Initialize` with the following code and save your work:</span></span>

```csharp
public Task Initialize()
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.CreateIfNotExistsAsync();
}
```