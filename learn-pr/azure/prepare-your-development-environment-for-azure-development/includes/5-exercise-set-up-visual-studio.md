<span data-ttu-id="42847-101">이 연습에서는 Windows 또는 macOS 컴퓨터에 Visual Studio를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-101">In this exercise, you will install Visual Studio on either your Windows or your macOS computer.</span></span> <span data-ttu-id="42847-102">Windows에서는 Azure 개발 워크로드를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-102">On Windows, the Azure development workload will need to be installed.</span></span> <span data-ttu-id="42847-103">Mac용 Visual Studio에서는 기본 제공 연결된 서비스 워크플로를 통해 Azure App Service에 대한 앱을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42847-103">And on Visual Studio for Mac, the built-in Connected Services workflow will enable you to build apps for Azure App Service.</span></span> <span data-ttu-id="42847-104">그러면 응용 프로그램을 만들어 Azure에 게시할 준비가 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="42847-104">At the end, you will be ready to start creating applications and publishing them to Azure.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="42847-105">연습 단계</span><span class="sxs-lookup"><span data-stu-id="42847-105">Exercise steps</span></span>

<span data-ttu-id="42847-106">Windows와 macOS 간에는 Visual Studio를 설치하는 데 약간의 차이가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="42847-106">There are slight differences in installing Visual Studio between Windows and macOS.</span></span> <span data-ttu-id="42847-107">다음 섹션에서는 이러한 차이점을 간략하게 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-107">The following sections outline these differences.</span></span>

### <a name="windows"></a><span data-ttu-id="42847-108">Windows</span><span class="sxs-lookup"><span data-stu-id="42847-108">Windows</span></span>

1. <span data-ttu-id="42847-109">https://visualstudio.microsoft.com/downloads/에서 Visual Studio 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-109">Download the Visual Studio installer from https://visualstudio.microsoft.com/downloads/.</span></span>

1. <span data-ttu-id="42847-110">설치 관리자를 실행하면 워크로드 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="42847-110">Run the installer and it will open the Workloads window.</span></span>

1. <span data-ttu-id="42847-111">**Azure 개발** 워크로드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-111">Choose the **Azure development** workload.</span></span>

    <span data-ttu-id="42847-112">다음 스크린샷은 Visual Studio 내에서 Azure 개발을 허용하도록 Visual Studio 설치 관리자 워크로드가 선택되어 있는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42847-112">The following screenshot shows the Visual Studio Installer workload selected to allow Azure development within Visual Studio.</span></span>

    ![Azure 개발 워크로드가 강조되어 있는 Visual Studio 설치 관리자의 스크린샷입니다.](../media/5-select-azure-workload.png)

1. <span data-ttu-id="42847-114">(선택 사항) ASP.NET 및 웹 개발 워크로드를 설치하여 Azure용 웹 응용 프로그램을 만들 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-114">(Optional) Install the ASP.NET and web development workload to be ready to create web applications for Azure.</span></span>

1. <span data-ttu-id="42847-115">**설치**를 클릭하고 Visual Studio가 설치될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="42847-115">Click **Install**, and wait for Visual Studio to install.</span></span>

1. <span data-ttu-id="42847-116">설치가 완료되면 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="42847-116">When the installation is complete, open Visual Studio.</span></span>

1. <span data-ttu-id="42847-117">Visual Studio의 보기 메뉴로 이동하여 **클라우드 탐색기** 옵션이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-117">Go to the View menu in Visual Studio and make sure you have the **Cloud Explorer** option.</span></span>

    <span data-ttu-id="42847-118">다음 스크린샷은 Azure 개발 워크로드가 설치되어 있으면 표시되는 클라우드 탐색기 메뉴 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42847-118">The following screenshot shows the Cloud Explorer menu option that will be present if you have the Azure development workload installed.</span></span>

    ![클라우드 탐색기 메뉴 옵션이 강조되어 있는 Visual Studio 보기 메뉴의 스크린샷입니다.](../media/5-verify-cloud-explorer.png)

### <a name="macos"></a><span data-ttu-id="42847-120">macOS</span><span class="sxs-lookup"><span data-stu-id="42847-120">macOS</span></span>

1. <span data-ttu-id="42847-121">https://visualstudio.microsoft.com/으로 이동하여 Mac용 Visual Studio 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-121">Go to https://visualstudio.microsoft.com/ and download the Visual Studio for Mac installer.</span></span>

1. <span data-ttu-id="42847-122">VisualStudioInstaller.dmg 파일을 클릭하여 설치 관리자를 탑재한 후 로고를 두 번 클릭하여 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-122">Click the VisualStudioInstaller.dmg file to mount the installer and then run it by double-clicking the logo.</span></span>

1. <span data-ttu-id="42847-123">개인정보처리방침 및 사용 조건이 표시되면 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-123">Acknowledge the Privacy and License terms when presented.</span></span>

1. <span data-ttu-id="42847-124">설치 관리자에서 설치할 구성 요소를 물어봅니다.</span><span class="sxs-lookup"><span data-stu-id="42847-124">The installer will ask which components you wish to install.</span></span> <span data-ttu-id="42847-125">Azure 구성 요소는 이미 Mac용 Visual Studio의 일부이지만 Azure용 웹 환경을 개발하려면 **.NET Core** 플랫폼을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="42847-125">Azure components are already part of Visual Studio for Mac, but it is recommended to install the **.NET Core** platform to develop web experiences for Azure.</span></span>

    <span data-ttu-id="42847-126">다음 스크린샷은 Mac용 Visual Studio에 Azure 개발 기능을 추가하는 데 필요한 .NET Core 플랫폼을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="42847-126">The following screenshot shows the .NET Core platform required to add Azure development capabilities to Visual Studio for Mac.</span></span>

    ![선택한 .NET Core 플랫폼 옵션이 강조되어 있는 Mac용 Visual Studio 설치 관리자의 스크린샷입니다.](../media/5-vsmac-install-net-core.png)

1. <span data-ttu-id="42847-128">선택 사항에 만족하면 **설치 및 업데이트**를 클릭하고 설치 관리자가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="42847-128">Click **Install and Update** once you are happy with the selections, and wait for the installer to complete.</span></span>

1. <span data-ttu-id="42847-129">필요한 권한을 승격하도록 메시지가 표시되면 관리자 자격 증명을 사용하여 권한을 승격합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-129">If you are prompted to elevate the permissions needed, use your administrator credentials to do so.</span></span>

1. <span data-ttu-id="42847-130">설치 관리자가 완료되면 Mac용 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="42847-130">Once the installer is complete, start Visual Studio for Mac.</span></span>
