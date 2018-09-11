<span data-ttu-id="226e8-101">.NET Core용 Azure Storage SDK에서 개별 Blob을 사용하여 작업하려면 ‘Blob 참조’, 즉 `ICloudBlob` 개체의 인스턴스가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-101">Working with an individual blob in the Azure Storage SDK for .NET Core requires a *blob reference* &mdash; an instance of an `ICloudBlob` object.</span></span>

<span data-ttu-id="226e8-102">Blob의 이름을 사용하거나 컨테이너의 Blob 목록에서 선택하여 `ICloudBlob`을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-102">You can get an `ICloudBlob` by requesting it with the blob's name or selecting it from a list of blobs in the container.</span></span> <span data-ttu-id="226e8-103">두 방법 모두 `CloudBlobContainer`가 필요하며, 이에 대해서는 마지막 단원에서 가져오는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-103">Both require a `CloudBlobContainer`, which we saw how to get in the last unit.</span></span>

## <a name="getting-blobs-by-name"></a><span data-ttu-id="226e8-104">이름으로 Blob 가져오기</span><span class="sxs-lookup"><span data-stu-id="226e8-104">Getting blobs by name</span></span>

<span data-ttu-id="226e8-105">`CloudBlobContainer`에서 `GetXXXReference` 메서드 중 하나를 호출하여 이름을 기준으로 `ICloudBlob`을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-105">Call one of the `GetXXXReference` methods on a `CloudBlobContainer` to get an `ICloudBlob` by name.</span></span> <span data-ttu-id="226e8-106">검색 중인 Blob 유형을 알고 있는 경우 특정 메서드(`GetBlockBlobReference`, `GetAppendBlobReference` 또는 `GetPageBlobReference`) 중 하나를 사용하여 해당 Blob 유형에 맞게 조정된 메서드 및 속성을 포함하는 개체를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-106">If you know the type of the blob you are retrieving, use one of the specific methods (`GetBlockBlobReference`, `GetAppendBlobReference`, or `GetPageBlobReference`) to get an object that includes methods and properties tailored for that blob type.</span></span>

<span data-ttu-id="226e8-107">이러한 메서드는 네트워크 호출을 수행하지 않고 대상 Blob이 실제로 존재하는지 여부를 확인하지도 않습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-107">None of these methods make network calls, nor do they confirm whether or not the targeted blob actually exists.</span></span> <span data-ttu-id="226e8-108">또한 Blob 참조 개체를 로컬로만 만듭니다. 이러한 개체는 네트워크를 통해 ‘작동’하고 저장소의 Blob과 상호 작용하는 메서드를 호출하는 데 사용될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-108">They only create a blob reference object locally, which can then be used to call methods that *do* operate over the network and interact with blobs in storage.</span></span> <span data-ttu-id="226e8-109">별도의 `GetBlobReferenceFromServerAsync` 메서드가 Blob Storage API를 호출하고 Blob이 아직 없는 경우 예외를 throw합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-109">A separate method, `GetBlobReferenceFromServerAsync`, does call the Blob storage API and will throw an exception if the blob doesn't already exist.</span></span>

## <a name="listing-blobs-in-a-container"></a><span data-ttu-id="226e8-110">컨테이너 Blob 나열</span><span class="sxs-lookup"><span data-stu-id="226e8-110">Listing blobs in a container</span></span>

<span data-ttu-id="226e8-111">`CloudBlobContainer`의 `ListBlobsSegmentedAsync` 메서드를 사용하여 컨테이너의 Blob 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-111">You can get a list of the blobs in a container using `CloudBlobContainer`'s `ListBlobsSegmentedAsync` method.</span></span> <span data-ttu-id="226e8-112">*Segmented*는 별개의 결과 페이지가 반환됨을 나타냅니다. `ListBlobsSegmentedAsync`에 대한 단일 호출은 단일 페이지에 모든 결과를 반환할 것을 보장하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-112">*Segmented* refers to the separate pages of results returned &mdash; a single call to `ListBlobsSegmentedAsync` is never guaranteed to return all the results in a single page.</span></span> <span data-ttu-id="226e8-113">여러 페이지에 걸쳐 작업할 수 있으려면, 반환되는 `ContinuationToken`을 사용하여 반복적으로 호출해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-113">We may need to call it repeatedly using the `ContinuationToken` it returns to work our way through the pages.</span></span> <span data-ttu-id="226e8-114">이렇게 하면 Blob을 나열하는 코드가 업로드 또는 다운로드하기 위한 코드보다 좀 더 복잡해지지만 컨테이너의 모든 Blob을 가져오는 데 사용할 수 있는 표준 패턴이 확보됩니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-114">This makes the code for listing blobs a little more complex than the code for uploading or downloading, but there's a standard pattern you can use to get every blob in a container:</span></span>

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

<span data-ttu-id="226e8-115">`continuationToken`이 결과의 끝을 나타내는 `null`일 때까지 `ListBlobsSegmentedAsync`을 반복적으로 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-115">This will call `ListBlobsSegmentedAsync` repeatedly until `continuationToken` is `null`, which signals the end of the results.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="226e8-116">`ListBlobsSegmentedAsync` 결과가 단일 페이지로 도착할 것으로 가정하지 마세요.</span><span class="sxs-lookup"><span data-stu-id="226e8-116">Never assume that `ListBlobsSegmentedAsync` results will arrive in a single page.</span></span> <span data-ttu-id="226e8-117">항상 연속 토큰을 확인하고 해당 토큰이 있으면 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-117">Always check for a continuation token and use it if it's present.</span></span>

### <a name="processing-list-results"></a><span data-ttu-id="226e8-118">목록 결과 처리</span><span class="sxs-lookup"><span data-stu-id="226e8-118">Processing list results</span></span>

<span data-ttu-id="226e8-119">`ListBlobsSegmentedAsync`에서 가져올 개체에는 `IEnumerable<IListBlobItem>` 유형의 `Results` 속성이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-119">The object you'll get back from `ListBlobsSegmentedAsync` contains a `Results` property of type `IEnumerable<IListBlobItem>`.</span></span> <span data-ttu-id="226e8-120">`IListBlobItem` 인터페이스는 Blob 컨테이너 및 URL에 대한 몇 개의 속성을 포함할 뿐이며 자체적으로 그렇게 유용하지는 않습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-120">The `IListBlobItem` interface includes only a handful of properties about the blob's container and URL, and isn't very useful by itself.</span></span>

<span data-ttu-id="226e8-121">`Results`에서 유용한 Blob 개체를 가져오려면 `OfType<>` 메서드를 사용하여 결과를 필터링하고 좀 더 구체적인 Blob 개체 형식으로 캐스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-121">To get useful blob objects out of `Results`, you can use the `OfType<>` method to filter and cast the results to more specific blob object types.</span></span> <span data-ttu-id="226e8-122">다음은 몇 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-122">Here are a few examples:</span></span>

```csharp
// Get all blobs
var allBlobs = resultSegment.Results.OfType<ICloudBlob>();

// Get only block blobs
var blockBlobs = resultSegment.Results.OfType<CloudBlockBlob();
```

> [!NOTE]
> <span data-ttu-id="226e8-123">`OfType<>`을 사용하려면 `System.Linq` 네임스페이스에 대한 참조(`using System.Linq;`)가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-123">Using `OfType<>` requires a reference to the `System.Linq` namespace (`using System.Linq;`).</span></span>

## <a name="exercise"></a><span data-ttu-id="226e8-124">연습</span><span class="sxs-lookup"><span data-stu-id="226e8-124">Exercise</span></span>

<span data-ttu-id="226e8-125">앱의 기능 중 하나가 작동하려면 API에서 Blob 목록을 가져와야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-125">One of the features in our app requires getting a list of blobs from the API.</span></span> <span data-ttu-id="226e8-126">위에 나온 패턴을 사용하여 컨테이너의 모든 Blob을 나열하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-126">We'll use the pattern shown above to list all the blobs in our container.</span></span> <span data-ttu-id="226e8-127">목록을 처리할 때 각 Blob의 이름을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-127">As we process the list, we get the name of each blob.</span></span>

<span data-ttu-id="226e8-128">편집기에서 `BlobStorage.cs`를 열고 `GetNames`를 다음 코드로 바꾼 후 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-128">Open `BlobStorage.cs` in the editor, replace `GetNames` with the following code and save your changes.</span></span>

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

> [!TIP]
> <span data-ttu-id="226e8-129">이제 메서드 서명은 `async`를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-129">Note that the method signature now needs to specify `async`.</span></span>

<span data-ttu-id="226e8-130">이 메서드로 반환된 이름은 `FilesController`에 의해 처리되어 URL로 변환됩니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-130">The names returned by this method are processed by `FilesController` to turn them into URLs.</span></span> <span data-ttu-id="226e8-131">이 이름이 클라이언트에 반환되면 페이지에서 하이퍼링크로 렌더링됩니다.</span><span class="sxs-lookup"><span data-stu-id="226e8-131">When they are returned to the client, they are rendered as hyperlinks on the page.</span></span>