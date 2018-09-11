이 연습에서는 구성에서 Azure Storage 계정 연결 문자열을 로드한 후 Azure Storage 계정에 연결하는 데 사용합니다.

## <a name="retrieve-the-connection-string"></a>연결 문자열 검색

1. 이전 단원의 콘솔 응용 프로그램이 Visual Studio에 로드되었는지 확인합니다.
1. **Program.cs** 파일에서 파일 맨 위에 *using* 문을 추가하여 **Microsoft.WindowsAzure.Storage** 라이브러리를 참조합니다.
    ```csharp
    using Microsoft.WindowsAzure.Storage;
    ```
1. **Main** 메서드의 맨 아래에 다음 줄을 추가하여 구성 파일에서 Azure Storage 계정 연결 문자열을 검색합니다.
    ```csharp
    var connectionString = configuration["StorageAccountConnectionString"];
    ```

## <a name="create-a-blob-client"></a>Blob 클라이언트 만들기

1. **Main** 메서드의 맨 아래에 다음 코드를 삽입하여 연결 문자열을 구문 분석하고 Blob 클라이언트를 만듭니다.
    ```csharp
    CloudStorageAccount storageAccount;
    if (!CloudStorageAccount.TryParse(connectionString,out storageAccount))
    {
        Console.WriteLine("Unable to parse connection string");
        return;
    }
    var blobClient = storageAccount.CreateCloudBlobClient();
    ```
1. 다음 코드를 삽입하여 Blob 클라이언트를 만들고, 컨테이너에 대한 참조를 검색합니다. 경우에 따라 **Main** 메서드 아래에 컨테이너가 없으면 만듭니다.
    ```csharp
    var containerName = "MyBlobContainer";
    var success = blobClient
        .GetContainerReference(containerName)
        .CreateIfNotExistsAsync()
        .Result;
    ```

  **비동기** 메서드 **CreateIfNotExistsAsync()** 및 해당 **Result** 속성을 사용한다는 점에 유의하세요. 전형적인 응용 프로그램에서는 일반적으로 **await** 키워드를 사용합니다. 그러나 이 응용 프로그램은 콘솔 응용 프로그램이고, 비동기식이 아니므로 **Result** 속성을 호출하여 **CreateIfNotExistsAsync()** 메서드에 의해 만들어진 비동기 작업의 결과를 가져와야 합니다.

## <a name="print-a-status-message"></a>상태 메시지 인쇄

1. **Main** 메서드의 아래쪽에 다음 코드를 추가하여 성공 또는 실패 메시지를 인쇄합니다.
    ```csharp
    if (!success)
    {
        Console.WriteLine("Error: Could not connect to Azure Storage container");
        return;
    }
    Console.WriteLine("Successfully connected to Azure Storage container");
    ```
1. 마지막으로 응용 프로그램을 실행하여 성공적으로 연결되었는지 확인하고, 저장소 컨테이너가 이전에 없었던 경우 Azure Portal에서 저장소 컨테이너가 만들어졌는지 확인합니다.
1. **선택 사항**: 컨테이너를 사용하지 않으려는 경우, 사용하지 않는 리소스에 대해 비용이 청구되지 않도록 해당 컨테이너가 있는 리소스 그룹을 삭제합니다.


