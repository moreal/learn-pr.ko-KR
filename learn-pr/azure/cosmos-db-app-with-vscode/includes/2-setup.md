이 모듈에서는 통합 터미널을 사용하여 간단한 콘솔 앱을 만들고, NuGet 패키지를 설치하고, Azure Cosmos DB 확장을 사용하여 이전 모듈에서 만든 데이터베이스와 컬렉션을 봅니다. 확장에서 Azure Cosmos DB 연결 문자열을 검색한 후 Azure Cosmos DB에 대한 연결 구성을 시작하여 사용자 데이터베이스를 만듭니다.

## <a name="create-a-console-app"></a>콘솔 앱 만들기

1. Visual Studio Code를 열고 **파일** > **폴더 열기**를 선택합니다.

2. 새 C# 프로젝트가 있을, 이름이 **learning-module**인 새 폴더를 만들고 **폴더 선택**을 클릭합니다.

2. 주 메뉴에서 **보기** > **통합 터미널**을 선택하여 Visual Studio Code의 통합 터미널을 엽니다.

3. 터미널 창에 **dotnet new console**을 입력합니다.

    이 명령은 이미 작성된 간단한 “Hello World” 프로그램과 이름이 **learning-module.csproj**인 C# 프로젝트 파일을 함께 사용하여 폴더에 **Program.cs** 파일을 만듭니다.

4. 터미널 창에 다음 명령을 입력하여 “Hello World” 프로그램을 실행합니다. 

    ```
    dotnet run
    ```

    터미널 창에 “Hello world!”가 출력으로 표시됩니다.

## <a name="connect-the-app-to-azure-cosmos-db"></a>Azure Cosmos DB에 앱 연결

1. **보기** > **명령 팔레트**를 클릭하고 **Azure: Sign In**을 입력하여 Azure에 로그인합니다.

    지시에 따라 웹 브라우저에 제공된, Visual Studio Code 세션을 인증하는 코드를 복사하여 붙여넣습니다.

2. 왼쪽 메뉴에서 **탐색기** 아이콘(![탐색기 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png))을 클릭하고 **Azure Cosmos DB**를 확장합니다.

3. Azure 구독 > Azure Cosmos DB 계정을 확장합니다. 이전 모듈에서 **Products** 데이터베이스와 **Clothing** 컬렉션을 만든 경우 확장하면 해당 항목이 표시됩니다.

   ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. 이제 고객을 위한 새 데이터베이스와 컬렉션을 만들어 보겠습니다.

    탐색기 창에서 계정을 마우스 오른쪽 단추로 클릭하고 **데이터베이스 만들기**를 클릭합니다. 
    
    화면 맨 위에 있는 텍스트 상자에서 데이터베이스 이름에 **Users** > **Enter 키** > 컬렉션 이름에 **WebCustomers** > **Enter 키** > 파티션 키에 **userId** > **Enter 키** > 초기 처리 용량에 **1000** > **Enter 키**를 입력합니다.

    ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing-->

    새 Users 데이터베이스와 WebCustomers 컬렉션이 탐색기 창에 표시됩니다.

5. 통합 터미널의 새 프롬프트에서 다음 명령을 각각 실행하여 필요한 NuGet 패키지를 설치합니다.

    ```
    dotnet add package System.Net.Http
    dotnet add package System.Configuration
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. 탐색기 창의 맨 위에서 **Program.cs**를 클릭하여 파일을 엽니다.

7. 명령문을 사용하여 `using System;` 뒤에 다음을 추가합니다.

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. learning-module 폴더에 App.config라는 새 파일을 만들고 다음 코드를 추가합니다.
  
    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

9. learning-module 계정을 마우스 오른쪽 단추로 클릭하고 **연결 문자열 복사**를 클릭하여 Azure Cosmos DB 확장에서 연결 문자열을 복사합니다.

    ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/vs-code-copy-connection-string.gif) 

10. 연결 문자열을 텍스트 파일에 붙여넣고 텍스트 파일의 **AccountEndpoint** 부분을 App.config의 **accountEndpoint**로 복사합니다.

    accountEndpoint는 다음 코드와 비슷합니다.

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

12. 이제 텍스트 값의 **AccountKey** 값을 App.config의 **accountKey** 값으로 복사합니다.

12. 통합 터미널에서 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

13. 새 비동기 작업을 추가하여 새 클라이언트를 만들고, Main 메서드 뒤에 다음 메서드를 추가하여 Users 데이터베이스가 있는지 확인합니다.
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["endpointUrl"]), ConfigurationManager.AppSettings["primaryKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. 통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

15. 다음 코드를 복사하여 **Main** 메서드에 붙여넣어 현재 `Console.WriteLine("Hello World!");` 줄을 덮어씁니다.

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

16. 통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.

    ```csharp
    dotnet run
    ```

    콘솔에 다음 출력이 표시됩니다.
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a>요약

이 모듈에서는 Azure Cosmos DB 응용 프로그램의 기초를 설정했습니다. Visual Studio Code에서 개발 환경을 설정하고, 간단한 HelloWorld 프로젝트를 만들고, 프로젝트를 Azure Cosmos DB 엔드포인트에 연결하고, 데이터베이스와 컬렉션이 있는지 확인했습니다.