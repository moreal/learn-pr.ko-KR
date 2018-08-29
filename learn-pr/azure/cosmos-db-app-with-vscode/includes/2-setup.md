<span data-ttu-id="1f5e3-101">이 모듈에서는 통합 터미널을 사용하여 간단한 콘솔 앱을 만들고, NuGet 패키지를 설치하고, Azure Cosmos DB 확장을 사용하여 이전 모듈에서 만든 데이터베이스와 컬렉션을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-101">In this module you will create a simple console app using the integrated terminal, install NuGet packages, and use the Azure Cosmos DB extension to see databases and collections created in the previous module.</span></span> <span data-ttu-id="1f5e3-102">확장에서 Azure Cosmos DB 연결 문자열을 검색하고 Azure Cosmos DB에 대한 개발을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-102">You'll retrieve your Azure Cosmos DB connection string from the extension, and then start developing against Azure Cosmos DB.</span></span> 

## <a name="create-a-console-app"></a><span data-ttu-id="1f5e3-103">콘솔 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1f5e3-103">Create a console app</span></span>

1. <span data-ttu-id="1f5e3-104">Visual Studio Code를 열고 **파일** > **폴더 열기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-104">Open Visual Studio Code, and then select **File** > **Open Folder**.</span></span>

2. <span data-ttu-id="1f5e3-105">새 C# 프로젝트가 있을, 이름이 **learning-module**인 새 폴더를 만들고 **폴더 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-105">Create a new folder named **learning-module** where you want your new C# project to be, and then click **Select Folder**.</span></span>

2. <span data-ttu-id="1f5e3-106">주 메뉴에서 **보기** > **통합 터미널**을 선택하여 Visual Studio Code의 통합 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-106">Open the integrated terminal from Visual Studio Code by selecting **View** > **Integrated Terminal** from the main menu.</span></span>

3. <span data-ttu-id="1f5e3-107">터미널 창에 **dotnet new console**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-107">In the terminal window, type **dotnet new console**.</span></span>

    <span data-ttu-id="1f5e3-108">이 명령은 이미 작성된 간단한 “Hello World” 프로그램과 이름이 **learning-module.csproj**인 C# 프로젝트 파일을 함께 사용하여 폴더에 **Program.cs** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-108">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

4. <span data-ttu-id="1f5e3-109">터미널 창에 다음 명령을 입력하여 “Hello World” 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-109">In the terminal window, type the following command to run the "Hello World" program.</span></span> 

    ```
    dotnet run
    ```

    <span data-ttu-id="1f5e3-110">터미널 창에 “Hello world!”가 출력으로</span><span class="sxs-lookup"><span data-stu-id="1f5e3-110">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="1f5e3-111">표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-111">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="1f5e3-112">Azure Cosmos DB에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="1f5e3-112">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="1f5e3-113">**보기** > **명령 팔레트**를 클릭하고 **Azure: Sign In**을 입력하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-113">Sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span>

    <span data-ttu-id="1f5e3-114">지시에 따라 웹 브라우저에 제공된, Visual Studio Code 세션을 인증하는 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-114">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

2. <span data-ttu-id="1f5e3-115">왼쪽 메뉴에서 **탐색기** 아이콘(![탐색기 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png))을 클릭하고 **Azure Cosmos DB**를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-115">Click the ![Explorer icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Explorer** icon on the left menu, and then expand **Azure Cosmos DB**.</span></span>

3. <span data-ttu-id="1f5e3-116">Azure 구독 > Azure Cosmos DB 계정을 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-116">Expand your Azure subscription > Azure Cosmos DB account.</span></span> <span data-ttu-id="1f5e3-117">이전 모듈에서 **Products** 데이터베이스와 **Clothing** 컬렉션을 만든 경우 확장하면 해당 항목이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-117">If you created the **Products** database and **Clothing** collection in the previous modules, the extension displays them.</span></span>

   ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/azure-cosmos-db-vs-code-extension.png) 

4. <span data-ttu-id="1f5e3-119">이제 고객을 위한 새 데이터베이스와 컬렉션을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-119">Now let's create a new database and collection for your customers.</span></span>

    <span data-ttu-id="1f5e3-120">탐색기 창에서 계정을 마우스 오른쪽 단추로 클릭하고 **데이터베이스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-120">In the Explorer window, right-click your account, and then click **Create Database**.</span></span> 
    
    <span data-ttu-id="1f5e3-121">화면 맨 위에 있는 텍스트 상자에서 데이터베이스 이름에 **Users** > **Enter 키** > 컬렉션 이름에 **WebCustomers** > **Enter 키** > 파티션 키에 **userId** > **Enter 키** > 초기 처리 용량에 **1000** > **Enter 키**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-121">In the text box at the top of the screen, type **Users** for the database name > **Enter** > **WebCustomers** for the collection name > **Enter** > **userId** for the partition key > **Enter** > **1000** for the initial throughput capacity > **Enter**.</span></span>

    <span data-ttu-id="1f5e3-122">![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span><span class="sxs-lookup"><span data-stu-id="1f5e3-122">![Azure Cosmos DB Visual Studio Code extension](../media/2-setup/vs-code-azure-cosmos-db-extension.gif) <!--Retake on fresh machine without the other subscriptions showing--></span></span>

    <span data-ttu-id="1f5e3-123">새 Users 데이터베이스와 WebCustomers 컬렉션이 탐색기 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-123">The new Users database and WebCustomers collection are displayed in the Explorer window.</span></span>

5. <span data-ttu-id="1f5e3-124">통합 터미널의 새 프롬프트에서 다음 명령을 각각 실행하여 필요한 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-124">In the integrated terminal, run each of the following commands at a new prompt to install the required NuGet packages.</span></span>

    ```
    dotnet add package System.Net.Http
    dotnet add package Microsoft.Azure.DocumentDB.Core
    dotnet add package Newtonsoft.Json
    dotnet add package System.Threading.Tasks
    dotnet add package System.Linq
    dotnet add package Bogus
    dotnet restore
    ```

6. <span data-ttu-id="1f5e3-125">탐색기 창의 맨 위에서 **Program.cs**를 클릭하여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-125">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

7. <span data-ttu-id="1f5e3-126">명령문을 사용하여 `using System;` 뒤에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-126">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

8. <span data-ttu-id="1f5e3-127">다음 두 개의 상수와 ‘클라이언트’ 변수를 프로그램 클래스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-127">Add the following two constants and your *client* variable to the Program class:</span></span>

    ```csharp
    public class Program
    {
        // ADD THIS PART TO YOUR CODE
        private const string EndpointUrl = "<your endpoint URL>";
        private const string PrimaryKey = "<your primary key>";
        private DocumentClient client;
    ```

    <!--TODO: Use more secure method-->

9. <span data-ttu-id="1f5e3-128">learning-module 계정을 마우스 오른쪽 단추로 클릭하고 **연결 문자열 복사**를 클릭하여 Azure Cosmos DB 확장에서 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-128">Copy your connection string from the Azure Cosmos DB extension by right-clicking the learning-module account, and clicking **Copy Connection String**.</span></span>

    ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/vs-code-copy-connection-string.gif) 

10. <span data-ttu-id="1f5e3-130">연결 문자열을 텍스트 파일에 붙여넣고 텍스트 파일의 **AccountEndpoint** 부분을 Program.cs의 **EndpointUrl**로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-130">Paste the connection string into a text file, and then copy the **AccountEndpoint** portion from the text file into the **EndpointUrl** in Program.cs.</span></span>

    <span data-ttu-id="1f5e3-131">AccountEndpoint는 다음 코드와 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-131">The AccountEndpoint should look like the following code:</span></span>

    ```csharp
    private const string EndpointUrl = "https://<account name>.documents.azure.com:443/;
    ```

12. <span data-ttu-id="1f5e3-132">이제 텍스트 값의 **AccountKey** 값을 Program.cs의 **PrimaryKey** 값으로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-132">Now copy the **AccountKey** value from the text value into the **PrimaryKey** value in Program.cs.</span></span>

12. <span data-ttu-id="1f5e3-133">통합 터미널에서 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-133">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

13. <span data-ttu-id="1f5e3-134">새 비동기 작업을 추가하여 새 클라이언트를 만들고, Main 메서드 뒤에 다음 메서드를 추가하여 Users 데이터베이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-134">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the main method.</span></span>
    
    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(EndpointUrl), PrimaryKey);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });
    }
    ```

14. <span data-ttu-id="1f5e3-135">통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-135">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

15. <span data-ttu-id="1f5e3-136">다음 코드를 복사하여 **Main** 메서드에 붙여넣어 현재 `Console.WriteLine("Hello World!");` 줄을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-136">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

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

16. <span data-ttu-id="1f5e3-137">통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-137">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="1f5e3-138">콘솔에 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-138">The console displays the following output.</span></span>
    
    ```
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

## <a name="summary"></a><span data-ttu-id="1f5e3-139">요약</span><span class="sxs-lookup"><span data-stu-id="1f5e3-139">Summary</span></span>

<span data-ttu-id="1f5e3-140">이 모듈에서는 Azure Cosmos DB 응용 프로그램의 기초를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-140">In this module, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="1f5e3-141">Visual Studio Code에서 개발 환경을 설정하고, 간단한 HelloWorld 프로젝트를 만들고, 프로젝트를 Azure Cosmos DB 엔드포인트에 연결하고, 데이터베이스와 컬렉션이 있는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="1f5e3-141">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>