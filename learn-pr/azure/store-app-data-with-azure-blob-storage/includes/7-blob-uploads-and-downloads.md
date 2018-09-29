<span data-ttu-id="e5f6b-101">Blob에 대한 참조가 있으면 데이터를 업로드하고 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-101">Once we have a reference to a blob, we can upload and download data.</span></span> <span data-ttu-id="e5f6b-102">`ICloudBlob` 개체에는 바이트 배열, 스트림 및 파일을 소스 및 대상으로 지원하는 `Upload` 및 `Download` 메서드가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-102">`ICloudBlob` objects have `Upload` and `Download` methods that support byte arrays, streams, and files as sources and targets.</span></span> <span data-ttu-id="e5f6b-103">특정 유형에는 편의를 위한 추가 메서드가 있습니다. 예를 들어, `CloudBlockBlob`은 `UploadTextAsync` 및 `DownloadTextAsync`를 사용하여 문자열을 업로드하고 다운로드하는 것을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-103">Specific types have additional methods for convenience &mdash; for example, `CloudBlockBlob` supports uploading and downloading strings with `UploadTextAsync` and `DownloadTextAsync`.</span></span>

## <a name="creating-new-blobs"></a><span data-ttu-id="e5f6b-104">새 Blob 만들기</span><span class="sxs-lookup"><span data-stu-id="e5f6b-104">Creating new blobs</span></span>

<span data-ttu-id="e5f6b-105">새 Blob을 만들려면 저장소에 존재하지 않는 Blob에 대한 참조에서 `Upload` 메서드 중 하나를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-105">To create a new blob, you call one of the `Upload` methods on a reference to a blob that doesn't exist in storage.</span></span> <span data-ttu-id="e5f6b-106">이 호출은 두 가지 작업, 즉 저장소에서 Blob 만들기 및 데이터 업로드를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-106">This does two things: creates the blob in storage and uploads the data.</span></span>

## <a name="moving-data-to-and-from-blobs"></a><span data-ttu-id="e5f6b-107">Blob 간 데이터 이동</span><span class="sxs-lookup"><span data-stu-id="e5f6b-107">Moving data to and from blobs</span></span>

<span data-ttu-id="e5f6b-108">Blob 간에 데이터를 이동하는 것은 시간이 걸리는 네트워크 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-108">Moving data to and from a blob is a network operation that takes time.</span></span> <span data-ttu-id="e5f6b-109">.NET Core용 Azure Storage SDK에서는 네트워크 활동을 필요로 하는 모든 메서드가 `Task`를 반환하므로, 컨트롤러 메서드에서 `await`를 적절히 사용하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-109">In the Azure Storage SDK for .NET Core, all methods that require network activity return `Task`s, so make sure you use `await` in your controller methods appropriately.</span></span>

<span data-ttu-id="e5f6b-110">용량이 큰 데이터 개체에 대해 작업할 때 일반적인 권장 사항은 바이트 배열 또는 문자열과 같은 메모리 내 구조 대신 스트림을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-110">A common recommendation when working with large data objects is to use streams instead of in-memory structures like byte arrays or strings.</span></span> <span data-ttu-id="e5f6b-111">이렇게 하면 대상으로 전송하기 전에 전체 콘텐츠를 메모리 내에 버퍼링하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-111">This avoids buffering the full content in memory before sending it to the target.</span></span> <span data-ttu-id="e5f6b-112">ASP.NET Core는 요청 및 응답에서 스트림을 읽고 쓰는 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-112">ASP.NET Core supports reading and writing streams from requests and responses.</span></span>

## <a name="concurrent-access"></a><span data-ttu-id="e5f6b-113">동시 액세스</span><span class="sxs-lookup"><span data-stu-id="e5f6b-113">Concurrent access</span></span>

<span data-ttu-id="e5f6b-114">앱에서 Blob을 사용 중일 때 다른 프로세스가 Blob을 추가, 변경 또는 삭제하고 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-114">Other processes may be adding, changing, or deleting blobs as your app is using them.</span></span> <span data-ttu-id="e5f6b-115">다운로드하려고 시도할 때 Blob이 삭제되거나 예기치 않은 시기에 Blob 콘텐츠가 변경되는 등 동시성으로 인해 발생하는 문제에 대해 생각하고, 항상 방어적으로 코딩하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-115">Always code defensively and think about problems caused by concurrency, such as blobs that are deleted right as you try to download from them, or blobs whose contents change when you don't expect them to.</span></span> <span data-ttu-id="e5f6b-116">AccessConditions 및 Blob 임대를 사용하여 동시 Blob 액세스를 관리하는 방법에 대한 자세한 내용은 이 모듈 끝에 있는 추가 참고 자료 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-116">See the Further Reading section at the end of this module for information about using AccessConditions and blob leases to manage concurrent blob access.</span></span>

## <a name="exercise"></a><span data-ttu-id="e5f6b-117">연습</span><span class="sxs-lookup"><span data-stu-id="e5f6b-117">Exercise</span></span>

<span data-ttu-id="e5f6b-118">업로드 및 다운로드 코드를 추가하여 앱을 완료한 후 테스트를 위해 Azure App Service에 배포하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-118">Let's finish our app by adding upload and download code, then deploy it to Azure App Service for testing.</span></span>

### <a name="upload"></a><span data-ttu-id="e5f6b-119">업로드</span><span class="sxs-lookup"><span data-stu-id="e5f6b-119">Upload</span></span>

<span data-ttu-id="e5f6b-120">Blob을 업로드하기 위해, `GetBlockBlobReference`를 사용하여 컨테이너에서 `CloudBlockBlob`을 가져오는 `BlobStorage.Save` 메서드를 구현하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-120">To upload a blob, we'll implement the `BlobStorage.Save` method using `GetBlockBlobReference` to get a `CloudBlockBlob` from the container.</span></span> <span data-ttu-id="e5f6b-121">`FilesController.Upload`는 파일 스트림을 `Save`에 전달하므로, 최대 효율성을 위해 `UploadFromStreamAsync`를 사용하여 업로드를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-121">`FilesController.Upload` passes the file stream to `Save`, so we can use `UploadFromStreamAsync` to perform the upload for maximum efficiency.</span></span>

<span data-ttu-id="e5f6b-122">편집기에서 `BlobStorage.cs`의 `Save`를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-122">In the editor, replace `Save` in `BlobStorage.cs` with the following code:</span></span>

```csharp
public Task Save(Stream fileStream, string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    CloudBlockBlob blockBlob = container.GetBlockBlobReference(name);
    return blockBlob.UploadFromStreamAsync(fileStream);
}
```

> [!NOTE]
> <span data-ttu-id="e5f6b-123">여기에 표시된 스트림 기반 업로드 코드는 Azure Blob Storage에 전송하기 전에 바이트 배열로 파일을 읽는 것보다 효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-123">The stream-based upload code shown here is more efficient than reading the file into a byte array before sending it to Azure Blob storage.</span></span> <span data-ttu-id="e5f6b-124">그러나 클라이언트에서 파일을 가져오는 데 사용하는 ASP.NET Core `IFormFile` 기술은 진정한 종단 간 스트리밍 구현이 아니며 작은 파일의 업로드를 처리하는 데에만 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-124">However, the ASP.NET Core `IFormFile` technique we use to get the file from the client is not a true end-to-end streaming implementation and is only appropriate for handling uploads of small files.</span></span> <span data-ttu-id="e5f6b-125">완전히 스트리밍되는 파일 업로드에 대한 정보는 이 모듈의 끝부분에 있는 추가 참고 자료 섹션을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-125">See the Further Reading section at the end of this module for information about fully streamed file uploads.</span></span>

### <a name="download"></a><span data-ttu-id="e5f6b-126">다운로드</span><span class="sxs-lookup"><span data-stu-id="e5f6b-126">Download</span></span>

<span data-ttu-id="e5f6b-127">`BlobStorage.Load`는 `Stream`을 반환합니다. 다시 말해서, 코드가 Blob Storage에서 실제로 바이트를 이동하지 않아도 된다는 의미입니다. 그러므로 Blob 스트림에 대한 참조를 반환하기만 하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-127">`BlobStorage.Load` returns a `Stream`, meaning that our code doesn't need to physically move the bytes from Blob storage at all &mdash; we just need to return a reference to the blob stream.</span></span> <span data-ttu-id="e5f6b-128">그러려면 `OpenReadAsync`를 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-128">We can do that with `OpenReadAsync`.</span></span> <span data-ttu-id="e5f6b-129">ASP.NET Core는 클라이언트 응답을 빌드할 때 스트림을 읽고 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-129">ASP.NET Core will handle reading and closing the stream when it builds the client response.</span></span>

<span data-ttu-id="e5f6b-130">`Load`를 다음 코드로 바꾸고 작업을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-130">Replace `Load` with this code and save your work:</span></span>

```csharp
public Task<Stream> Load(string name)
{
    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);
    return container.GetBlobReference(name).OpenReadAsync();
}
```

### <a name="deploy-and-run-in-azure"></a><span data-ttu-id="e5f6b-131">Azure에서 배포 및 실행</span><span class="sxs-lookup"><span data-stu-id="e5f6b-131">Deploy and run in Azure</span></span>

<span data-ttu-id="e5f6b-132">앱이 완료되었으므로, 앱을 배포하고 작동을 확인해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-132">Our app is finished &mdash; let's deploy it and see it work.</span></span> <span data-ttu-id="e5f6b-133">App Service 앱을 만들고 저장소 계정 연결 문자열 및 컨테이너 이름에 대한 응용 프로그램 설정을 사용하여 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-133">Create an App Service app and configure it with application settings for our storage account connection string and container name.</span></span> <span data-ttu-id="e5f6b-134">`az storage account show-connection-string`을 사용하여 저장소 계정의 연결 문자열을 가져오고 컨테이너 이름을 `files`로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-134">Get the storage account's connection string with `az storage account show-connection-string` and set the name of the container to be `files`.</span></span>

<span data-ttu-id="e5f6b-135">앱 이름은 전역적으로 고유해야 하므로 `<your-unique-app-name>`에 입력할 자신만의 이름을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-135">The app name needs to be globally unique, so you'll need to choose your own name to fill in `<your-unique-app-name>`.</span></span>

```azurecli
az appservice plan create --name blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
az webapp create --name <your-unique-app-name> --plan blob-exercise-plan --resource-group <rgn>[sandbox resource group name]</rgn>
CONNECTIONSTRING=$(az storage account show-connection-string --name <your-unique-storage-account-name> --output tsv)
az webapp config appsettings set --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn> --settings AzureStorageConfig:ConnectionString=$CONNECTIONSTRING AzureStorageConfig:FileContainerName=files
```

<span data-ttu-id="e5f6b-136">이제 앱을 배포해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-136">Now we'll deploy our app.</span></span> <span data-ttu-id="e5f6b-137">아래 명령은 사이트를 `pub` 폴더에 게시하고, `site.zip`으로 압축하고, 해당 Zip 파일을 App Service에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-137">The below commands will publish the site to the `pub` folder, zip it up into `site.zip`, and deploy the zip to App Service.</span></span>

> [!NOTE]
> <span data-ttu-id="e5f6b-138">다음 명령을 실행하기 전에 셸이 `mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start` 디렉터리에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-138">Make sure your shell is still in the `mslearn-store-data-in-azure/store-app-data-with-azure-blob-storage/src/start` directory before running the following commands.</span></span>

```azurecli
dotnet publish -o pub
cd pub
zip -r ../site.zip *
az webapp deployment source config-zip --src ../site.zip --name <your-unique-app-name> --resource-group <rgn>[sandbox resource group name]</rgn>
```

<span data-ttu-id="e5f6b-139">브라우저에서 `https://<your-unique-app-name>.azurewebsites.net`을 열어 실행 중인 앱을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-139">Open `https://<your-unique-app-name>.azurewebsites.net` in a browser to see the running app.</span></span> <span data-ttu-id="e5f6b-140">다음 이미지와 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-140">It should look like the image below.</span></span>

![FileUploader 웹앱 스크린샷](../media/7-fileuploader-empty.PNG)

<span data-ttu-id="e5f6b-142">일부 파일을 업로드하고 다운로드하여 앱을 테스트해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-142">Try uploading and downloading some files to test the app.</span></span> <span data-ttu-id="e5f6b-143">몇 개의 파일을 업로드한 후 셸에서 다음을 실행하여 컨테이너에 업로드된 Blob을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e5f6b-143">After you've uploaded a few files, run the following in the shell to see the blobs that have been uploaded to the container:</span></span>

```console
az storage blob list --account-name <your-unique-storage-account-name> --container-name files --query [].{Name:name} --output table
```