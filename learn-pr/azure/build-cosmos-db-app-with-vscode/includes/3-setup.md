<span data-ttu-id="2e076-101">Visual Studio Code를 사용하면 통합 터미널 및 몇 가지 간단한 명령을 사용하여 콘솔 응용 프로그램을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-101">Visual Studio Code enables you to create a console application by using the integrated terminal and a few short commands.</span></span>

<span data-ttu-id="2e076-102">이 단원에서는 통합 터미널을 사용하여 간단한 콘솔 앱을 만들고, 확장 프로그램에서 Azure Cosmos DB 연결 문자열을 검색하고, 응용 프로그램에서 Azure Cosmos DB로 연결을 구성해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-102">In this unit, you will create a simple console app using the integrated terminal, retrieve your Azure Cosmos DB connection string from the extension, and then configure the connection from your application to Azure Cosmos DB.</span></span>

## <a name="create-a-console-app"></a><span data-ttu-id="2e076-103">콘솔 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="2e076-103">Create a console app</span></span>

1. <span data-ttu-id="2e076-104">Visual Studio Code에서 **파일** > **폴더 열기**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-104">In Visual Studio Code, select **File** > **Open Folder**.</span></span>

1. <span data-ttu-id="2e076-105">선택한 위치에서 `learning-module`이라는 새 폴더를 만든 다음, **폴더 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-105">Create a new folder named `learning-module` in the location of your choice, and then click **Select Folder**.</span></span>

1. <span data-ttu-id="2e076-106">[파일] 메뉴를 클릭하고, **자동 저장**이 선택되어 있지 않으면 선택하여 파일 자동 저장을 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-106">Ensure that file auto-save is enabled by clicking on the File menu and checking **Auto Save** if it is blank.</span></span> <span data-ttu-id="2e076-107">여러 코드 블록에 복사되며, 이렇게 되면 항상 파일의 최신 편집본으로 작업하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-107">You will be copying in several blocks of code, and this will ensure you are always operating against the latest edits of your files.</span></span>

1. <span data-ttu-id="2e076-108">주 메뉴에서 **보기** > **터미널**을 선택하여 Visual Studio Code에서 통합 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-108">Open the integrated terminal from Visual Studio Code by selecting **View** > **Terminal** from the main menu.</span></span>

1. <span data-ttu-id="2e076-109">터미널 창에 다음 명령을 복사하고 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-109">In the terminal window, copy and paste the following command.</span></span>

    ```bash
    dotnet new console
    ```

    <span data-ttu-id="2e076-110">이 명령은 이미 작성된 간단한 “Hello World” 프로그램과 **learning-module.csproj**이라는 C# 프로젝트 파일을 함께 사용하여 폴더에 **Program.cs** 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-110">This command creates a **Program.cs** file in your folder with a simple "Hello World" program already written, along with a C# project file named **learning-module.csproj**.</span></span>

1. <span data-ttu-id="2e076-111">터미널 창에 다음 명령을 복사하고 붙여넣기 하여 “Hello World” 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-111">In the terminal window, copy and paste the following command to run the "Hello World" program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="2e076-112">터미널 창에 “Hello world!”가 출력으로</span><span class="sxs-lookup"><span data-stu-id="2e076-112">The terminal window displays "Hello world!"</span></span> <span data-ttu-id="2e076-113">표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-113">as output.</span></span>

## <a name="connect-the-app-to-azure-cosmos-db"></a><span data-ttu-id="2e076-114">Azure Cosmos DB에 앱 연결</span><span class="sxs-lookup"><span data-stu-id="2e076-114">Connect the app to Azure Cosmos DB</span></span>

1. <span data-ttu-id="2e076-115">터미널 프롬프트에 다음 명령 블록을 복사하고 붙여넣기 하여 필요한 NuGet 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-115">At the terminal prompt, copy and paste the following command block to install the required NuGet packages.</span></span>

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

1. <span data-ttu-id="2e076-116">탐색기 창의 맨 위에서 **Program.cs**를 클릭하여 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-116">At the top of the Explorer pane, click **Program.cs** to open the file.</span></span>

1. <span data-ttu-id="2e076-117">명령문을 사용하여 `using System;` 뒤에 다음 항목을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-117">Add the following using statements after `using System;`.</span></span>

    ```csharp
    using System.Configuration;
    using System.Linq;
    using System.Threading.Tasks;
    using System.Net;
    using Microsoft.Azure.Documents;
    using Microsoft.Azure.Documents.Client;
    using Newtonsoft.Json;
    ```

    <span data-ttu-id="2e076-118">필요한 누락 자산 추가에 대한 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-118">If you get a message about adding required missing assets, click **Yes**.</span></span>

1. <span data-ttu-id="2e076-119">learning-module 폴더에 App.config라는 새 파일을 만들고 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-119">Create a new file named App.config in the learning-module folder, and add the following code.</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
        <configuration>
          <appSettings>
            <add key="accountEndpoint" value="<replace with your Endpoint URL>" />
            <add key="accountKey" value="<replace with your Primary Key>" />
          </appSettings>
    </configuration>
    ```

1. <span data-ttu-id="2e076-120">왼쪽의 ![Azure 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png)을 클릭하고, 컨시어지 구독을 확장하고, 새 Azure Cosmos DB 계정을 마우스 오른쪽 단추로 클릭한 다음, **연결 문자열 복사**를 클릭하여 연결 문자열을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-120">Copy your connection string by clicking the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) Azure icon on the left, expanding your Concierge Subscription, right-clicking your new Azure Cosmos DB account, and then clicking **Copy Connection String**.</span></span>

1. <span data-ttu-id="2e076-121">연결 문자열을 App.config 파일의 끝에 붙여넣고 연결 문자열의 **AccountEndpoint** 부분을 App.config의 **accountEndpoint** 값에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-121">Paste the connection string into the end of the App.config file, and then copy the **AccountEndpoint** portion from the connection string into the **accountEndpoint** value in App.config.</span></span>

    <span data-ttu-id="2e076-122">accountEndpoint는 다음 코드와 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-122">The accountEndpoint should look like the following code:</span></span>

    ```xml
    <add key="accountEndpoint" value="https://<account-name>.documents.azure.com:443/" />
    ```

1. <span data-ttu-id="2e076-123">이제 연결 문자열의 **AccountKey** 값을 **accountKey** 값에 복사한 다음, 복사한 원본 연결 문자열을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-123">Now copy the **AccountKey** value from the connection string into the **accountKey** value, and then delete the original connection string you copied in.</span></span>

1. <span data-ttu-id="2e076-124">터미널 프롬프트에 다음 명령을 복사하고 붙여넣기 하여 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-124">At the terminal prompt, copy and paste the following command to run the program.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="2e076-125">프로그램이 터미널에 Hello World!를</span><span class="sxs-lookup"><span data-stu-id="2e076-125">The program displays Hello World!</span></span> <span data-ttu-id="2e076-126">표시합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-126">in the terminal.</span></span>

## <a name="create-the-documentclient"></a><span data-ttu-id="2e076-127">DocumentClient 만들기</span><span class="sxs-lookup"><span data-stu-id="2e076-127">Create the DocumentClient</span></span>

<span data-ttu-id="2e076-128">이제 Azure Cosmos DB 서비스의 클라이언트 쪽 표현인 DocumentClient의 인스턴스를 만들 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-128">Now it's time to create an instance of the DocumentClient, which is the client-side representation of the Azure Cosmos DB service.</span></span> <span data-ttu-id="2e076-129">이 클라이언트는 서비스에 대한 요청을 구성하고 실행하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-129">This client is used to configure and execute requests against the service.</span></span>

1. <span data-ttu-id="2e076-130">Program.cs에서 Program 클래스의 시작 부분에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-130">In Program.cs, add the following to the beginning of the Program class.</span></span>

    ```csharp
    private DocumentClient client;
    ```

1. <span data-ttu-id="2e076-131">새 비동기 작업을 추가하여 새 클라이언트를 만들고, `Main` 메서드 뒤에 다음 메서드를 추가하여 사용자 데이터베이스가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-131">Add a new asynchronous task to create a new client, and check whether the Users database exists by adding the following method after the `Main` method.</span></span>

    ```csharp
    private async Task BasicOperations()
    {
        this.client = new DocumentClient(new Uri(ConfigurationManager.AppSettings["accountEndpoint"]), ConfigurationManager.AppSettings["accountKey"]);

        await this.client.CreateDatabaseIfNotExistsAsync(new Database { Id = "Users" });

        await this.client.CreateDocumentCollectionIfNotExistsAsync(UriFactory.CreateDatabaseUri("Users"), new DocumentCollection { Id = "WebCustomers" });

        Console.WriteLine("Database and collection validation complete");
    }
    ```

1. <span data-ttu-id="2e076-132">통합 터미널에서 다시 다음 명령을 복사하고 붙여넣어 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-132">In the integrated terminal, again, copy and paste the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="2e076-133">다음 코드를 복사하여 **Main** 메서드에 붙여넣어 현재 `Console.WriteLine("Hello World!");` 줄을 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-133">Copy and paste the following code into the **Main** method, overwriting the current `Console.WriteLine("Hello World!");` line.</span></span>

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

1. <span data-ttu-id="2e076-134">통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-134">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="2e076-135">콘솔에 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-135">The console displays the following output.</span></span>

    ```output
    Database and collection validation complete
    End of demo, press any key to exit.
    ```

<span data-ttu-id="2e076-136">이 단원에서는 Azure Cosmos DB 응용 프로그램의 기초를 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-136">In this unit, you set up the groundwork for your Azure Cosmos DB application.</span></span> <span data-ttu-id="2e076-137">Visual Studio Code에서 개발 환경을 설정하고, 간단한 HelloWorld 프로젝트를 만들고, 프로젝트를 Azure Cosmos DB 엔드포인트에 연결하고, 데이터베이스와 컬렉션이 있는지 확인했습니다.</span><span class="sxs-lookup"><span data-stu-id="2e076-137">You set up your development environment in Visual Studio Code, created a simple HelloWorld project, connected the project to the Azure Cosmos DB endpoint, and ensured your database and collection exist.</span></span>
