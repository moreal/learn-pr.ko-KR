Azure Storage 컨테이너 및 각 계정에 저장 된 데이터 작업에 따라 Representational State Transfer (REST) web API를 제공 합니다. 독립 Api 저장할 수 있는 데이터의 각 형식을 다루는 데 사용할 수 있습니다. 네 가지 특정 데이터 형식이 있다는 것을 회수 합니다.

- **Blob** 이진 및 텍스트 파일과 같은 구조화 되지 않은 데이터에 대 한 합니다.
- **큐** 영구 메시징에 대 한 합니다.
- **테이블** 구조화 된 키/값 저장소입니다.
- **파일** 기존 SMB 파일 공유 합니다.

## <a name="using-the-rest-api"></a>REST API 사용

Storage REST Api를 HTTP/HTTPS 요청을 보내고 HTTP/HTTPS 응답을 받을 수 있는 모든 응용 프로그램에서 가상 네트워크를 통해 인터넷을 통해 Azure에서 실행 하는 서비스에서 액세스할 수 있습니다.

예를 들어 컨테이너의 모든 blob을 나열 하려는 경우 보내는 것 같이:

```http
GET https://[url-for-service-account]/?comp=list&include=metadata
```

이 반환 데이터를 사용 하 여 XML 블록에는 특정 계정에 합니다.

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

그러나이 방법은 많은 수동 구문 분석 및 각 API를 사용 하려면 HTTP 패킷 생성 해야 합니다. 따라서 Azure에서 제공 하는 미리 빌드된 _클라이언트 라이브러리_ 는 쉽게 작업할 서비스를 공용 언어 및 프레임 워크에 대 한 합니다.

## <a name="using-a-client-library"></a>클라이언트 라이브러리를 사용 하 여

클라이언트 라이브러리는 API가 테스트 하 고 REST API를 통해 보내고 받은 데이터 모델에 대 한 편리한 래퍼를 제공 하기도 없으므로 상당한 양의 응용 프로그램 개발자를 위한 작업을 절약할 수 있습니다.

:::row:::
    :::column:::
        Microsoft는 다양 한 언어 및 프레임 워크를 지 원하는 Azure 클라이언트 라이브러리:-.NET-Java-Python-Node.js-Go :::column-end:::: :::column:::
        <br> ![Azure를 사용 하 여 사용할 수는 지원 되는 프레임 워크의 샘플 로고](../media/4-common-tools.png)
    :::column-end:::
:::row-end:::

예를 들어, 동일한 목록을 C#의 blob 검색 하려면 다음 코드 조각 사용 수 있습니다.:

```csharp
CloudBlobDirectory directory = ...;
foreach (IEnumerable<IListBlobItem> blob in directory.ListBlobs(
                useFlatBlobListing: true,
                blobListingDetails: BlobListingDetails.All))
{
    // Work with blob item .. could be page blob, block blob, etc.
}
```

또는 JavaScript에서:

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
> 클라이언트 라이브러리는 방금 씬 _래퍼_ REST API를 통해. 정확 하 게 수행 하는 웹 서비스를 직접 사용 하는 경우 수행 하 고 있습니다. 이러한 라이브러리는 오픈 소스, 투명 한 매우 쉽게도 합니다. GitHub에서 검색 합니다.

클라이언트 라이브러리 지원 응용 프로그램에 추가 해 보겠습니다.