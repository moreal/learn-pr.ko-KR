<span data-ttu-id="c3ed7-101">.NET Core용 Azure Storage SDK에서 개별 Blob을 사용하여 작업하려면 ‘Blob 참조’, 즉 `ICloudBlob` 개체의 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="c3ed7-102">Blob의 이름을 사용하거나 컨테이너의 Blob 목록에서 선택하여 `ICloudBlob`을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="c3ed7-103">두 방법 모두 `CloudBlobContainer`가 필요하며, 이에 대해서는 마지막 단원에서 가져오는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="c3ed7-104">이름으로 Blob 가져오기</span><span class="sxs-lookup"><span data-stu-id="c3ed7-104">Getting blobs by name</span></span>

<span data-ttu-id="c3ed7-105">`CloudBlobContainer`에서 `GetXXXReference` 메서드 중 하나를 호출하여 이름을 기준으로 `ICloudBlob`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="c3ed7-106">검색 중인 Blob의 유형을 알고 있는 경우에는 보다 구체적인 메서드(`GetBlockBlobReference`, `GetAppendBlobReference`, `GetPageBlobReference`) 중 하나를 사용하는 것이 더 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-106">If you know the type of the blob you are retrieving, prefer using one of the more specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`).</span></span>

<span data-ttu-id="c3ed7-107">이러한 메서드는 네트워크 호출을 수행하지 않고 Blob이 실제로 존재하는지 여부를 확인하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-107">None of these methods make a network call, nor do they confirm whether or not the blob actually exists.</span></span> <span data-ttu-id="c3ed7-108">별도의 `GetBlobReferenceFromServerAsync` 메서드가 Blob Storage API를 호출하고 Blob이 아직 없는 경우 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-108">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="c3ed7-109">컨테이너 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="c3ed7-109">Listing blobs in a container</span></span>

<span data-ttu-id="c3ed7-110">`CloudBlobContainer`의 `ListBlobsSegmentedAsync` 메서드를 사용하여 컨테이너의 Blob 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-110">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="c3ed7-111">*Segmented*는 별개의 결과 페이지가 반환됨을 나타냅니다. `ListBlobsSegmentedAsync`에 대한 단일 호출은 단일 페이지에 모든 결과를 반환할 것을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-111">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="c3ed7-112">여러 페이지에 걸쳐 작업할 수 있으려면, 반환되는 `ContinuationToken`을 사용하여 반복적으로 호출해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-112">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="c3ed7-113">이렇게 하면 Blob을 나열하는 코드가 업로드 또는 다운로드하기 위한 코드보다 좀 더 복잡해지지만 컨테이너의 모든 Blob을 가져오는 데 사용할 수 있는 표준 패턴이 확보됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-113">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

```csharp
BlobContinuationToken continuationToken = null;
BlobResultSegment resultSegment = null; 

do
{
    resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

    // Do work here on resultSegment.Results

    continuationToken = resultSegment.ContinuationToken;
} while (continuationToken != null);
```

<span data-ttu-id="c3ed7-114">`continuationToken`이 결과의 끝을 나타내는 `null`일 때까지 `ListBlobsSegmentedAsync`을 반복적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-114">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="c3ed7-115">목록 결과 처리</span><span class="sxs-lookup"><span data-stu-id="c3ed7-115">Processing list results</span></span>

<span data-ttu-id="c3ed7-116">`ListBlobsSegmentedAsync`에서 가져올 개체에는 `IEnumerable<IListBlobItem>` 유형의 `Results` 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-116">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="c3ed7-117">`IListBlobItem`에는 Blob의 컨테이너 및 URL에 대한 몇 가지 속성이 포함되어 있지만 업로드 또는 다운로드 메서드는 포함되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-117">`IListBlobItem`s contain a handful of properties about the blob's container and URL, but no upload or download methods.</span></span> <span data-ttu-id="c3ed7-118">이는 일부 결과 개체가 개별 Blob 대신 가상 디렉터리를 나타내는 `CloudBlobDirectory` 개체일 수 있기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-118">This is because some of the result objects may be `CloudBlobDirectory` objects that represent virtual directories rather than individual blobs.</span></span>

<span data-ttu-id="c3ed7-119">개별 Blob에만 관심이 있는 경우에는 `OfType<>` 메서드를 사용하여 결과를 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-119">If you are only interested in individual blobs, you can use the `OfType<>` method to filter the results.</span></span> <span data-ttu-id="c3ed7-120">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-120">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

<span data-ttu-id="c3ed7-121">`OfType<>`을 사용하려면 `System.Linq` 네임스페이스에 대한 참조(`using System.Linq;`)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-121">Using `OfType<>` will require a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="c3ed7-122">연습</span><span class="sxs-lookup"><span data-stu-id="c3ed7-122">Exercise</span></span>

<span data-ttu-id="c3ed7-123">앱의 기능 중 하나가 작동하려면 API에서 Blob 목록을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-123">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="c3ed7-124">위에 나온 패턴을 사용하여 컨테이너의 모든 Blob을 나열하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-124">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="c3ed7-125">목록을 처리할 때 각 Blob의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-125">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="c3ed7-126">편집기에서 `BlobStorage.cs`를 열고 `GetNames`에 다음 코드를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-126">Open `BlobStorage.cs` in the editor and fill in `GetNames` with the following code:</span></span>

```csharp
public async Task<IEnumerable<string>> GetNames()
{
    List<string> names = new List<string>();

    CloudStorageAccount storageAccount = CloudStorageAccount.Parse(storageConfig.ConnectionString);
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
    CloudBlobContainer container = blobClient.GetContainerReference(storageConfig.FileContainerName);

    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    do
    {
        resultSegment = await container.ListBlobsSegmentedAsync(continuationToken);

        // Get the name of each blob.
        names.AddRange(resultSegment.Results.OfType<ICloudBlob>().Select(b => b.Name));

        continuationToken = resultSegment.ContinuationToken;
    } while (continuationToken != null);

    return names;
}
```

<span data-ttu-id="c3ed7-127">이 메서드로 반환된 이름은 `FilesController`에 의해 처리되어 URL로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-127">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="c3ed7-128">이 이름이 클라이언트에 반환되면 페이지에서 하이퍼링크로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3ed7-128">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>