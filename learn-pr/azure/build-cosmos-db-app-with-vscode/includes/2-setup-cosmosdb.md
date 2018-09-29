<span data-ttu-id="00dee-101">Visual Studio Code용 Azure Cosmos DB 확장은 명령 창을 사용하여 리소스를 만들 수 있게 함으로써 계정, 데이터베이스 및 컬렉션 만들기를 간소화합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-101">The Azure Cosmos DB extension for Visual Studio Code simplifies account, database, and collection creation by enabling you to create resources using the command window.</span></span>

<span data-ttu-id="00dee-102">이 단원에서는 Visual Studio용 Azure Cosmos DB 확장을 설치한 다음, 이 확장을 사용하여 계정, 데이터베이스 및 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-102">In this unit you will install the Azure Cosmos DB extension for Visual Studio, and then use it to create an account, database, and collection.</span></span>

## <a name="install-the-azure-cosmos-db-extension-for-visual-studio"></a><span data-ttu-id="00dee-103">Visual Studio용 Azure Cosmos DB 확장 설치</span><span class="sxs-lookup"><span data-stu-id="00dee-103">Install the Azure Cosmos DB extension for Visual Studio</span></span>

1. <span data-ttu-id="00dee-104">[Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb)로 이동하여 Visual Studio Code용 **Azure Cosmos DB** 확장을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-104">Go to the [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-cosmosdb) and install the **Azure Cosmos DB** extension for Visual Studio Code.</span></span>

1. <span data-ttu-id="00dee-105">확장 탭이 Visual Studio Code에 로드되면 **설치**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-105">When the extension tab loads in Visual Studio Code, click **Install**.</span></span>

1. <span data-ttu-id="00dee-106">설치가 완료되면 **다시 로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-106">After installation is complete, click **Reload**.</span></span>

    <span data-ttu-id="00dee-107">Visual Studio Code에서</span><span class="sxs-lookup"><span data-stu-id="00dee-107">Visual Studio Code displays the</span></span> ![Azure 아이콘 표시](../media/2-setup/visual-studio-code-explorer-icon.png) <span data-ttu-id="00dee-109">확장을 설치하고 다시 로드한 후 화면 왼쪽에 Azure 아이콘이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-109">Azure icon on the left side of the screen after the extension is installed and reloaded.</span></span>

## <a name="create-an-azure-cosmos-db-account-in-visual-studio-code"></a><span data-ttu-id="00dee-110">Visual Studio Code에서 Azure Cosmos DB 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="00dee-110">Create an Azure Cosmos DB account in Visual Studio Code</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

1. <span data-ttu-id="00dee-111">Visual Studio Code에서 **보기** > **명령 팔레트**를 클릭하고 **Azure: Sign In**을 입력하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-111">In Visual Studio Code, sign in to Azure by clicking **View** > **Command Palette** and typing **Azure: Sign In**.</span></span> <span data-ttu-id="00dee-112">Azure: Sign In을 사용하려면 [Azure 계정](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-112">You must have the [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) extension installed to use Azure: Sign In.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="00dee-113">샌드박스를 만드는 데 사용된 동일한 계정을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-113">Login to Azure using the same account used to create the sandbox.</span></span> <span data-ttu-id="00dee-114">샌드박스는 컨시어지 구독에 대한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-114">The sandbox provides access to a Concierge Subscription.</span></span>

    <span data-ttu-id="00dee-115">지시에 따라 웹 브라우저에 제공된 코드를 복사하고 붙여넣어 Visual Studio Code 세션을 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-115">Follow the prompts to copy and paste the code provided in the web browser, which authenticates your Visual Studio Code session.</span></span>

1. <span data-ttu-id="00dee-116">왼쪽 메뉴에서 ![Azure 아이콘](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure** 아이콘을 클릭한 다음, **컨시어지 구독**을 마우스 오른쪽 단추로 클릭하고 **계정 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-116">Click the ![Azure icon](../media/2-setup/visual-studio-code-explorer-icon.png) **Azure** icon on the left menu, and then right-click **Concierge Subscription**, and click **Create Account**.</span></span>

    <span data-ttu-id="00dee-117">나열된 컨시어지 구독이 표시되지 않은 경우 샌드박스를 만드는 데 사용된 동일한 계정을 사용하여 Visual Studio Code의 Azure에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-117">If you do not see the Concierge Subscription listed, ensure you logged into Azure in Visual Studio Code using the same account used to create the sandbox.</span></span> <span data-ttu-id="00dee-118">또한 Azure 계정 확장에서 Azure 구독을 필터링한 경우 `> Azure: Select Subscriptions` 명령에 컨시어지 구독이 선택되어 있는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="00dee-118">Additionally, if you have filtered your Azure subscriptions in the Azure Account extension, verify the Concierge Subscription is checked in the `> Azure: Select Subscriptions` command.</span></span>

1. <span data-ttu-id="00dee-119">__+__ 단추를 클릭하여 Cosmos DB 계정 만들기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-119">Click the __+__ button to start creating a Cosmos DB account.</span></span> <span data-ttu-id="00dee-120">둘 이상의 구독이 있는 경우 구독을 선택하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-120">You will be asked to select the subscription if you have more than one.</span></span>

1. <span data-ttu-id="00dee-121">화면 맨 위에 있는 텍스트 상자에 Azure Cosmos DB 계정의 고유한 이름을 입력한 다음 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-121">In the text box at the top of the screen, enter a unique name for your Azure Cosmos DB account, and then press enter.</span></span> <span data-ttu-id="00dee-122">계정 이름은 소문자, 숫자 및 '-' 문자만 포함할 수 있으며, 3자에서 31자 사이여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-122">The account name can contain only lowercase letters, numbers and the '-' character, and must be between 3 and 31 characters.</span></span>

1. <span data-ttu-id="00dee-123">다음으로, **SQL(DocumentDB)** > **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 선택한 다음, 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-123">Next, select **SQL (DocumentDB)** > **<rgn>[sandbox resource group name]</rgn>**, and then select a location.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note-friendly.md)]

    <span data-ttu-id="00dee-124">Visual Studio Code의 출력 탭에 계정 만들기 진행률이 표시되며, 완료하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-124">The output tab in Visual Studio Code displays the progress of the account creation, it takes a few minutes to complete.</span></span>

1. <span data-ttu-id="00dee-125">계정을 만든 후 **Azure: Cosmos DB** 창에서 Azure 구독을 확장하면 확장 프로그램에 새 Azure Cosmos DB 계정이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-125">After the account is created, expand your Azure subscription in the **Azure: Cosmos DB** pane and the extension displays the new Azure Cosmos DB account.</span></span> <span data-ttu-id="00dee-126">다음 이미지에서 새 계정 이름은 **학습 모듈**입니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-126">In the following image, the new account is named **learning-modules**.</span></span>

    ![Azure Cosmos DB Visual Studio Code 확장](../media/2-setup/azure-cosmos-db-vs-code-extension.png)

## <a name="create-an-azure-cosmos-db-database-and-collection-in-visual-studio-code"></a><span data-ttu-id="00dee-128">Visual Studio Code에서 Azure Cosmos DB 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="00dee-128">Create an Azure Cosmos DB database and collection in Visual Studio Code</span></span>

<span data-ttu-id="00dee-129">이제 고객을 위한 새 데이터베이스와 컬렉션을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-129">Now let's create a new database and collection for your customers.</span></span>

1. <span data-ttu-id="00dee-130">Azure: Cosmos DB 창에서 새 계정을 마우스 오른쪽 단추로 클릭한 다음, **데이터베이스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-130">In the Azure: Cosmos DB pane, right-click your new account, and then click **Create Database**.</span></span>
1. <span data-ttu-id="00dee-131">화면 맨 위의 입력 팔레트에서 데이터베이스 이름에 `Users`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-131">In the input palette at the top of the screen, type `Users` for the database name and press Enter.</span></span>
1. <span data-ttu-id="00dee-132">컬렉션 이름에 `WebCustomers`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-132">Enter `WebCustomers` for the collection name and press Enter.</span></span>
1. <span data-ttu-id="00dee-133">파티션 키에 `userId`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-133">Enter `userId` for the partition key and press Enter.</span></span>
1. <span data-ttu-id="00dee-134">마지막으로, 초기 처리량 용량에 대해 `1000`을 확인하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-134">Finally, confirm `1000` for the initial throughput capacity and press Enter.</span></span>
1. <span data-ttu-id="00dee-135">**Azure: Cosmos DB** 창에서 계정을 확장하면 새 **사용자** 데이터베이스 및 **WebCustomers** 컬렉션이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-135">Expand the account in the **Azure: Cosmos DB** pane, and the new **Users** database and **WebCustomers** collection are displayed.</span></span>

    ![Visual Studio Code의 Azure Cosmos DB 확장 프로그램에 위의 지침을 보여 주는 애니메이션이 실행됩니다.](../media/2-setup/vs-code-azure-cosmos-db-extension.gif)

<span data-ttu-id="00dee-137">Azure Cosmos DB 계정이 있으므로 Visual Studio Code에서 작업을 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="00dee-137">Now that you have your Azure Cosmos DB account, lets get to work in Visual Studio Code!</span></span>
