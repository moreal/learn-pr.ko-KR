<span data-ttu-id="046e8-101">Azure Storage는 각 계정에 저장된 컨테이너 및 데이터를 사용하는 REST API를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-101">Azure Storage provides a REST API to work with the containers and data stored in each account.</span></span> <span data-ttu-id="046e8-102">저장 가능한 각 데이터 형식을 사용할 수 있는 독립적인 API가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-102">There are independent APIs available to work with each type of data you can store.</span></span> <span data-ttu-id="046e8-103">다음과 같은 네 가지 데이터 형식이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-103">Recall that we have four specific data types:</span></span>

- <span data-ttu-id="046e8-104">**Blob**은 이진 및 텍스트 파일처럼 구조화되지 않은 데이터를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-104">**Blobs** for unstructured data such as binary and text files.</span></span>
- <span data-ttu-id="046e8-105">**큐**는 영구 메시징을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-105">**Queues** for persistent messaging.</span></span>
- <span data-ttu-id="046e8-106">**테이블**은 구조화된 키/값 저장소를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-106">**Tables** for structured storage of key/values.</span></span>
- <span data-ttu-id="046e8-107">**파일**은 전통적인 SMB 파일 공유를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-107">**Files** for traditional SMB file shares.</span></span>

## <a name="using-the-rest-api"></a><span data-ttu-id="046e8-108">REST API 사용</span><span class="sxs-lookup"><span data-stu-id="046e8-108">Using the REST API</span></span>

<span data-ttu-id="046e8-109">Storage REST API는 HTTP/HTTPS 요청을 보내고 HTTP/HTTPS 응답을 받을 수 있는 모든 응용 프로그램을 통해 어디에서나 인터넷으로 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-109">The Storage REST APIs are accessible from anywhere on the Internet, by any application that can send an HTTP/HTTPS request and receive an HTTP/HTTPS response.</span></span>

<span data-ttu-id="046e8-110">예를 들어 컨테이너의 모든 Blob을 나열하려면 다음과 같은 것을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-110">For example, if you wanted to list all the blobs in a container, you would send something like:</span></span>

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

<span data-ttu-id="046e8-111">그러면 계정 관련 데이터가 포함된 XML 블록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-111">This would return an XML block with data specific to the account:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>  
<EnumerationResults AccountName="https://[url-for-service-account]/">  
  <Containers>  
    <Container>  
      <Name>container1</Name>  
      <Url>https://[url-for-service-account]/container1</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 18:09:03 GMT</Last-Modified>  
        <Etag>0x8CAE7D0C4AF4487</Etag>  
      </Properties>  
      <Metadata>  
        <Color>orange</Color>  
        <ContainerNumber>01</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container2</Name>  
      <Url>https://[url-for-service-account]/container2</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8C24928</Etag>  
      </Properties>  
      <Metadata>  
        <Color>pink</Color>  
        <ContainerNumber>02</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
    <Container>  
      <Name>container3</Name>  
      <Url>https://[url-for-service-account]/container3</Url>  
      <Properties>  
        <Last-Modified>Sun, 24 Sep 2018 17:26:40 GMT</Last-Modified>  
        <Etag>0x8CAE7CAD8EAC0BB</Etag>  
      </Properties>  
      <Metadata>  
        <Color>brown</Color>  
        <ContainerNumber>03</ContainerNumber>  
        <SomeMetadataName>SomeMetadataValue</SomeMetadataName>  
      </Metadata>  
    </Container>  
  </Containers>  
  <NextMarker>container4</NextMarker>  
</EnumerationResults>  
```

<span data-ttu-id="046e8-112">그러나 이 방법은 수많은 수동 구문 분석이 필요하고 각 API를 사용하는 HTTP 패킷을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-112">However, this approach requires a lot of manual parsing and the creation of HTTP packets to work with each API.</span></span> <span data-ttu-id="046e8-113">이러한 이유로 Azure는 공용 언어 및 프레임워크에 서비스를 간편하게 사용할 수 있도록 미리 빌드된 _클라이언트 라이브러리_를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-113">For this reason, Azure provides pre-built _client libraries_ that make working with the service easier for common languages and frameworks.</span></span>

## <a name="using-a-client-library"></a><span data-ttu-id="046e8-114">클라이언트 라이브러리 사용</span><span class="sxs-lookup"><span data-stu-id="046e8-114">Using a client library</span></span>

<span data-ttu-id="046e8-115">클라이언트 라이브러리를 사용하면 응용 프로그램 개발자가 해야 하는 작업을 대폭 줄일 수 있습니다. API에 대한 테스트가 실행되고 종종 REST API가 주고 받는 데이터 모델과 관련하여 더 좋은 래퍼를 제공하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-115">Client libraries can save a significant amount of work for application developers because the API is tested and it often provides nicer wrappers around the data models sent and received by the REST API.</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="046e8-116">Microsoft는 .NET, Java, Python, Node.js, Go를 비롯한 다양한 언어와 프레임워크를 지원하는 Azure 클라이언트 라이브러리를 제공합니다. :::column-end:::</span><span class="sxs-lookup"><span data-stu-id="046e8-116">Microsoft has Azure client libraries that support a number of languages and frameworks including: - .NET - Java - Python - Node.js - Go :::column-end::::</span></span> :::column:::
        <br> <span data-ttu-id="046e8-117">![Azure에 사용할 수 있는 지원되는 프레임워크의 샘플 로고](../media/4-common-tools.png)</span><span class="sxs-lookup"><span data-stu-id="046e8-117">![Sample logos of supported frameworks you can use with Azure](../media/4-common-tools.png)</span></span> 
    :::column-end:::
:::row-end:::

<span data-ttu-id="046e8-118">예를 들어 동일한 목록을 C#에서 검색하려면 다음 코드 조각을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-118">For example, to retrieve the same list of blobs in C#, we could use the following code snippet:</span></span>

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

<span data-ttu-id="046e8-119">또는 JavaScript에서는 다음을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-119">Or in JavaScript:</span></span>

```javascript
const containerName = "...";
const blobService = storage.createBlobService();

blobService.listBlobsSegmented(containerName, null, function (error, results) {
    if (results) {
        for (var i = 0, blob; blob = results.entries[i]; i++) {
            // Work with blob item .. could be page blob, block blob, etc.
        }
    }
});
```

> [!NOTE]
> <span data-ttu-id="046e8-120">클라이언트 라이브러리는 REST API를 통한 씬 _래퍼_일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-120">The client libraries are just thin _wrappers_ over the REST API.</span></span> <span data-ttu-id="046e8-121">라이브러리는 웹 서비스를 직접 사용한 경우 작업을 그대로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-121">They are doing exactly what you would do if you used the web services directly.</span></span> <span data-ttu-id="046e8-122">이러한 라이브러리는 오픈 소스로서 라이브러리를 매우 투명하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-122">These libraries are also open source, making them very transparent.</span></span> <span data-ttu-id="046e8-123">GitHub에서 라이브러리를 찾아보세요.</span><span class="sxs-lookup"><span data-stu-id="046e8-123">Look for them on GitHub.</span></span>

<span data-ttu-id="046e8-124">해당 응용 프로그램에 클라이언트 라이브러리 지원을 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="046e8-124">Let's add client library support to our application.</span></span>