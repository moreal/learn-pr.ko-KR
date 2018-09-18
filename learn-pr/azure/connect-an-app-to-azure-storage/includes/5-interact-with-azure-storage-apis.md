Azure Storage는 각 계정에 저장된 컨테이너 및 데이터를 작업하는 REST(Representational State Transfer) 기반 웹 API를 제공합니다. 저장 가능한 각 데이터 형식을 다루는 데 사용되는 독립 API가 있습니다. 다음과 같은 네 가지 데이터 형식이 있습니다.

- **Blob**은 이진 및 텍스트 파일처럼 구조화되지 않은 데이터를 나타냅니다.
- **큐**는 영구 메시징을 나타냅니다.
- **테이블**은 구조화된 키/값 저장소를 나타냅니다.
- **파일**은 전통적인 SMB 파일 공유를 나타냅니다.

## <a name="using-the-rest-api"></a>REST API 사용

Storage REST API는 Azure에서 실행되는 서비스에서 가상 네트워크를 통해 또는 HTTP/HTTPS 요청을 보내고 HTTP/HTTPS 응답을 받을 수 있는 모든 응용 프로그램에서 인터넷을 통해 액세스할 수 있습니다.

예를 들어 컨테이너의 모든 BLOB을 나열하려면 다음과 같이 보내야 합니다.

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

그러면 계정 관련 데이터가 포함된 XML 블록이 반환됩니다.

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

그러나 이 방법은 수많은 수동 구문 분석이 필요하고 각 API를 사용하기 위한 HTTP 패킷을 만들어야 합니다. 이러한 이유로 Azure는 공용 언어 및 프레임워크에 서비스를 간편하게 사용할 수 있도록 미리 빌드된 _클라이언트 라이브러리_를 제공합니다.

## <a name="using-a-client-library"></a>클라이언트 라이브러리 사용

클라이언트 라이브러리를 사용하면 응용 프로그램 개발자가 해야 하는 작업을 대폭 줄일 수 있습니다. API에 대한 테스트가 실행되고 종종 REST API가 주고 받는 데이터 모델과 관련하여 더 좋은 래퍼를 제공하기 때문입니다.

:::row:::
    :::column:::
        Microsoft는 .NET, Java, Python, Node.js, Go를 비롯한 다양한 언어와 프레임워크를 지원하는 Azure 클라이언트 라이브러리를 제공합니다. :::column-end::: :::column:::
        <br> ![Azure에 사용할 수 있는 지원되는 프레임워크의 샘플 로고](../media/4-common-tools.png)
    :::column-end:::
:::row-end:::

예를 들어 동일한 목록을 C#에서 검색하려면 다음 코드 조각을 사용합니다.

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

또는 JavaScript에서는 다음을 사용합니다.

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
> 클라이언트 라이브러리는 REST API를 통한 씬 _래퍼_일 뿐입니다. 여러분이 웹 서비스를 직접 사용할 때 하는 작업을 그대로 실행합니다. 이러한 라이브러리는 오픈 소스이므로 매우 투명합니다. GitHub에서 라이브러리를 찾아보세요.

응용 프로그램에 클라이언트 라이브러리 지원을 추가 해 보겠습니다.