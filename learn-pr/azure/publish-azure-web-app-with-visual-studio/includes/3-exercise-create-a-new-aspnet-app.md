<span data-ttu-id="feb80-101">이제 로컬 머신에서 앱이 실행되고 있으므로 Azure에 게시해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-101">Now that you've got your app up and running on your local machine, it's time to get it published to Azure.</span></span> 

<span data-ttu-id="feb80-102">이 단원에서는 로컬 컴퓨터에서 새 ASP.NET 웹 응용 프로그램을 만들고, 빌드하고, 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-102">In this unit, you will create, build, and run a new ASP.NET web application on your local machine.</span></span>

## <a name="create-a-new-project"></a><span data-ttu-id="feb80-103">새 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="feb80-103">Create a new project</span></span>

### <a name="visual-studio-for-windows"></a><span data-ttu-id="feb80-104">Windows용 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="feb80-104">Visual Studio for Windows</span></span>

<span data-ttu-id="feb80-105">첫 번째 단계는 Visual Studio를 시작하고 로컬 ASP.NET Core 웹 응용 프로그램을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-105">The first step is to start Visual Studio and create a local ASP.NET Core web application.</span></span>

1. <span data-ttu-id="feb80-106">Visual Studio 시작 페이지에서 **파일**을 선택하고 **새로 만들기**를 클릭한 후 **프로젝트..** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-106">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="feb80-107">**새 프로젝트** 대화 상자의 왼쪽 창에서 **웹**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-107">In the **New Project** dialog box, on the left-hand pane, select **Web**.</span></span>

1. <span data-ttu-id="feb80-108">가운데 창에서 **ASP.NET Core 웹 응용 프로그램**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-108">In the center pane, click **ASP.NET Core Web Application**.</span></span>

1. <span data-ttu-id="feb80-109">대화 상자의 아래쪽의 **이름** 필드에 **Alpine Ski House**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-109">At the bottom of the dialog box, in the **Name** field, enter **Alpine Ski House**.</span></span>

1. <span data-ttu-id="feb80-110">새 솔루션의 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-110">Select a **Location** for your new solution.</span></span>

1. <span data-ttu-id="feb80-111">**확인** 단추를 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-111">Click the **OK** button to create your project.</span></span>

1. <span data-ttu-id="feb80-112">**새 ASP.NET Core 웹 응용 프로그램** 대화 상자에 선택할 시작 템플릿이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-112">In the **New ASP.NET Core Web Application** dialog box, you will see a selection of starting templates.</span></span> <span data-ttu-id="feb80-113">이 연습에서는 **웹 응용 프로그램**을 선택한 후 **확인**을 클릭하여 프로젝트를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-113">For this exercise, select **Web Application**, and then click **OK** to create your project.</span></span>

    ![새 프로젝트 대화 상자](../media-draft/3-aspnet-templates.png)

    > [!NOTE]
    > <span data-ttu-id="feb80-115">웹 개발 요구 사항에 따라, 이 대화 상자에서 다른 시작 템플릿을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-115">You can also select different starting templates in this dialog box depending on your web development requirements.</span></span> <span data-ttu-id="feb80-116">대화 상자의 맨 위에서 ASP.NET Core의 버전을 선택할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-116">At the top of the dialog box, you are also able to select the version of ASP.NET Core.</span></span> <span data-ttu-id="feb80-117">ASP.NET Core 2.0 이상을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-117">You should select ASP.NET Core 2.0 or later.</span></span>

1. <span data-ttu-id="feb80-118">이제 새로운 ASP.NET Core 웹 응용 프로그램 솔루션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-118">You should now have your new ASP.NET Core web application solution.</span></span>

    ![새 프로젝트 대화 상자](../media-draft/3-new-solution.png)

### <a name="visual-studio-mac"></a><span data-ttu-id="feb80-120">Visual Studio Mac</span><span class="sxs-lookup"><span data-stu-id="feb80-120">Visual Studio Mac</span></span>

1. <span data-ttu-id="feb80-121">Visual Studio 시작 페이지에서 **파일**을 선택하고 **새로 만들기**를 클릭한 후 **프로젝트..** 를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-121">On the Visual Studio start page, select **File**, then click **New**, and then click **Project..**.</span></span>

1. <span data-ttu-id="feb80-122">**.NET Core**에서 **ASP.NET Core 웹앱**을 선택하고 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-122">Under .**NET Core**, select an **ASP.NET Core Web App**, and then click **Next**.</span></span>

1. <span data-ttu-id="feb80-123">**프로젝트 이름**의 경우 **AlpineSkiHouse**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-123">For the **Project Name**, type **AlpineSkiHouse**.</span></span> <span data-ttu-id="feb80-124">이렇게 하면 솔루션 이름도 자동으로 입력되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-124">This should also auto-populate the solution name.</span></span>

1. <span data-ttu-id="feb80-125">프로젝트의 로컬 머신에서 **위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-125">Select a **location** on your local machine for the project.</span></span>

1. <span data-ttu-id="feb80-126">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-126">Click **Create**.</span></span>

## <a name="build-and-test-on-your-local-machine"></a><span data-ttu-id="feb80-127">로컬 머신에서 빌드 및 테스트</span><span class="sxs-lookup"><span data-stu-id="feb80-127">Build and test on your local machine</span></span>

<span data-ttu-id="feb80-128">이제 로컬 머신에서 새 프로젝트를 빌드하고 테스트하여 Azure에 배포하기 전에 로컬로 빌드하고 배포하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-128">Now, let's build and test your new project on your local machine to ensure it builds and deploys locally before deploying to Azure.</span></span>

1. <span data-ttu-id="feb80-129">**F5**를 눌러 앱을 디버그 모드로 실행하거나 **Ctrl-F5**를 눌러 디버거를 연결하지 않고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-129">Press **F5** to run the app in debug mode or **Ctrl-F5** to run without attaching the debugger.</span></span>

    ![새 프로젝트 대화 상자](../media-draft/3-webapp-launch.png)

<span data-ttu-id="feb80-131">Visual Studio는 IIS Express를 시작하고 앱을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-131">Visual Studio starts IIS Express and runs the app.</span></span> <span data-ttu-id="feb80-132">Visual Studio가 웹 프로젝트를 만들면 임의의 포트가 웹 서버에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-132">When Visual Studio creates a web project, a random port is used for the web server.</span></span> <span data-ttu-id="feb80-133">이전 이미지에서는 포트 번호가 44381입니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-133">In the preceding image, the port number is 44381.</span></span> <span data-ttu-id="feb80-134">앱을 실행하면 다른 포트 번호가 표시될 가능성이 큽니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-134">When you run the app, you'll likely see a different port number.</span></span>

> [!TIP]
> <span data-ttu-id="feb80-135">**Ctrl+F5**(비디버그 모드)를 사용하여 앱을 시작하면 코드를 변경하고, 파일을 저장하고, 브라우저를 새로 고치고, 코드 변경 내용을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-135">Launching the app with **Ctrl+F5** (non-debug mode) allows you to make code changes, save the file, refresh the browser, and see the code changes.</span></span> <span data-ttu-id="feb80-136">많은 개발자가 비디버그 모드를 사용하여 빠르게 앱을 시작하고 변경 내용을 표시하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-136">Many developers prefer to use non-debug mode to quickly launch the app and view changes.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="feb80-137">웹 페이지 맨 위 섹션에서는 개인정보처리방침 및 쿠키 사용 정책을 위한 공간을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-137">You might notice the section at the top of the web page that provides a place for your privacy and cookie use policy.</span></span> <span data-ttu-id="feb80-138">추적에 동의하려면 **동의**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-138">Select **Accept** to consent to tracking.</span></span> <span data-ttu-id="feb80-139">이 앱은 개인 정보를 추적하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-139">This app doesn't track personal information.</span></span> <span data-ttu-id="feb80-140">템플릿 생성 코드에는 GDPR(일반 데이터 보호 규정)을 충족하는 데 도움이 되는 자산이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-140">The template-generated code includes assets to help meet General Data Protection Regulation (GDPR).</span></span>

## <a name="summary"></a><span data-ttu-id="feb80-141">요약</span><span class="sxs-lookup"><span data-stu-id="feb80-141">Summary</span></span>

<span data-ttu-id="feb80-142">ASP.NET 사이트를 실행하는 첫 번째 단계는 사이트를 만들고 로컬로 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-142">The first step to getting your ASP.NET site up and running is to create it and run it locally.</span></span> <span data-ttu-id="feb80-143">이제 사이트가 만들어졌으므로 Azure에 배포할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="feb80-143">Now that your site is created, you are ready to deploy it to Azure.</span></span>
