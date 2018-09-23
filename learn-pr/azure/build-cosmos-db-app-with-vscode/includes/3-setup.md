Visual Studio Code를 사용하면 통합 터미널 및 몇 가지 간단한 명령을 사용하여 콘솔 응용 프로그램을 만들 수 있습니다.

이 단원에서는 통합 터미널을 사용하여 간단한 콘솔 앱을 만들고, 확장 프로그램에서 Azure Cosmos DB 연결 문자열을 검색하고, 응용 프로그램에서 Azure Cosmos DB로 연결을 구성해 봅니다.

## <a name="create-a-console-app"></a>콘솔 앱 만들기

1. Visual Studio Code에서 **파일** > **폴더 열기**를 차례로 선택합니다.

1. 선택한 위치에서 `learning-module`이라는 새 폴더를 만든 다음, **폴더 선택**을 클릭합니다.

1. [파일] 메뉴를 클릭하고, **자동 저장**이 선택되어 있지 않으면 선택하여 파일 자동 저장을 사용하도록 설정합니다. 여러 코드 블록에 복사되며, 이렇게 되면 항상 파일의 최신 편집본으로 작업하게 됩니다.

1. 주 메뉴에서 **보기** > **터미널**을 선택하여 Visual Studio Code에서 통합 터미널을 엽니다.

1. 터미널 창에 다음 명령을 복사하고 붙여넣습니다.

    ```bash
    dotnet new console
    ```

    이 명령은 이미 작성된 간단한 “Hello World” 프로그램과 **learning-module.csproj**이라는 C# 프로젝트 파일을 함께 사용하여 폴더에 **Program.cs** 파일을 만듭니다.

1. 터미널 창에 다음 명령을 복사하고 붙여넣기 하여 “Hello World” 프로그램을 실행합니다.

    ```bash
    dotnet run
    ```

    터미널 창에 “Hello world!”가 출력으로 표시됩니다.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Azure Cosmos DB에 앱 연결

1. 터미널 프롬프트에 다음 명령 블록을 복사하고 붙여넣기 하여 필요한 NuGet 패키지를 설치합니다.

    ```bash
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package System.Configuration.ConfigurationManager
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet restore
    ```

1. 탐색기 창의 맨 위에서 **Program.cs**를 클릭하여 파일을 엽니다.

1. 명령문을 사용하여 `using System;` 뒤에 다음 항목을 추가합니다.

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

    필요한 누락 자산 추가에 대한 메시지가 표시되면 **예**를 클릭합니다.

1. learning-module 폴더에 App.config라는 새 파일을 만들고 다음 코드를 추가합니다.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. 왼쪽의 ![Azure 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png)을 클릭하고, 컨시어지 구독을 확장하고, 새 Azure Cosmos DB 계정을 마우스 오른쪽 단추로 클릭한 다음, **연결 문자열 복사**를 클릭하여 연결 문자열을 복사합니다.

1. 연결 문자열을 App.config 파일의 끝에 붙여넣고 연결 문자열의 **AccountEndpoint** 부분을 App.config의 **accountEndpoint** 값에 복사합니다.

    accountEndpoint는 다음 코드와 비슷해야 합니다.

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. 이제 연결 문자열의 **AccountKey** 값을 **accountKey** 값에 복사한 다음, 복사한 원본 연결 문자열을 삭제합니다.

1. 터미널 프롬프트에 다음 명령을 복사하고 붙여넣기 하여 프로그램을 실행합니다.

    ```csharp
    dotnet run
    ```

    프로그램이 터미널에 Hello World!를 표시합니다.

## <a name="create-the-documentclient"></a>DocumentClient 만들기

이제 Azure Cosmos DB 서비스의 클라이언트 쪽 표현인 DocumentClient의 인스턴스를 만들 차례입니다. 이 클라이언트는 서비스에 대한 요청을 구성하고 실행하는 데 사용됩니다.

1. Program.cs에서 Program 클래스의 시작 부분에 다음을 추가합니다.

    ```csharp
    private DocumentClient client;
    ```

1. 새 비동기 작업을 추가하여 새 클라이언트를 만들고, `Main` 메서드 뒤에 다음 메서드를 추가하여 사용자 데이터베이스가 있는지 확인합니다.

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. 통합 터미널에서 다시 다음 명령을 복사하고 붙여넣어 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

1. 다음 코드를 복사하여 **Main** 메서드에 붙여넣어 현재 `Console.WriteLine("Hello World!");` 줄을 덮어씁니다.

    ```csharp
    try
    {
        Program p = new Program();
        p.BasicOperations().Wait();
    }
    catch (DocumentClientException de)
    {
        Exception baseException = de.GetBaseException();
        Console.WriteLine("{0} error occurred: {1}, Message: {2}", de.StatusCode, de.Message, baseException.Message);
    }
    catch (Exception e)
    {
        Exception baseException = e.GetBaseException();
        Console.WriteLine("Error: {0}, Message: {1}", e.Message, baseException.Message);
    }
    finally
    {
        Console.WriteLine("End of demo, press any key to exit.");
        Console.ReadKey();
    }
    ```

1. 통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

    콘솔에 다음 출력이 표시됩니다.

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

이 단원에서는 Azure Cosmos DB 응용 프로그램의 기초를 설정했습니다. Visual Studio Code에서 개발 환경을 설정하고, 간단한 HelloWorld 프로젝트를 만들고, 프로젝트를 Azure Cosmos DB 엔드포인트에 연결하고, 데이터베이스와 컬렉션이 있는지 확인했습니다.
