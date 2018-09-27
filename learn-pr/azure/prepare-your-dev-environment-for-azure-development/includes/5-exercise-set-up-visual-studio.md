<span data-ttu-id="ad803-101">여기에서는 Windows 또는 macOS 개발 머신에 Visual Studio를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-101">Here, you'll install Visual Studio on either your Windows or your macOS development machine.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="ad803-102">연습 단계</span><span class="sxs-lookup"><span data-stu-id="ad803-102">Exercise steps</span></span>

<span data-ttu-id="ad803-103">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="ad803-103">::: zone pivot="windows"</span></span>

### <a name="windows"></a><span data-ttu-id="ad803-104">Windows</span><span class="sxs-lookup"><span data-stu-id="ad803-104">Windows</span></span>

1. <span data-ttu-id="ad803-105">https://visualstudio.microsoft.com/downloads/에서 Visual Studio 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-105">Download the Visual Studio installer from https://visualstudio.microsoft.com/downloads/.</span></span>

1. <span data-ttu-id="ad803-106">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-106">Run the installer.</span></span>

1. <span data-ttu-id="ad803-107">**워크로드** 탭에서 **Azure 개발** 워크로드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-107">On the **Workloads** tab, select the **Azure development** workload.</span></span>

    <span data-ttu-id="ad803-108">다음 스크린샷은 Visual Studio 내에서 Azure 개발을 허용하도록 Visual Studio 설치 관리자 워크로드가 선택되어 있는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-108">The following screenshot shows the Visual Studio Installer workload selected to allow Azure development within Visual Studio.</span></span>

    ![Azure 개발 워크로드가 강조되어 있는 Visual Studio 설치 관리자의 스크린샷입니다.](../media/5-select-azure-workload.png)

1. <span data-ttu-id="ad803-110">(선택 사항) ASP.NET 및 웹 개발 워크로드를 설치하여 Azure용 웹 응용 프로그램을 만들 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-110">(Optional) Install the ASP.NET and web development workload to be ready to create web applications for Azure.</span></span>

1. <span data-ttu-id="ad803-111">**설치**를 클릭하고 Visual Studio가 설치될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-111">Click **Install**, and wait for Visual Studio to install.</span></span> <span data-ttu-id="ad803-112">Visual Studio가 이미 설치된 시스템의 경우 이 단추는 **수정**을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-112">For systems with Visual Studio already installed, this button may say **Modify**.</span></span>

1. <span data-ttu-id="ad803-113">설치가 완료되면 Visual Studio를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-113">When the installation is complete, open Visual Studio.</span></span>

1. <span data-ttu-id="ad803-114">Visual Studio의 보기 메뉴로 이동하여 **클라우드 탐색기** 옵션이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-114">Go to the View menu in Visual Studio and make sure you have the **Cloud Explorer** option.</span></span>

    <span data-ttu-id="ad803-115">다음 스크린샷은 Azure 개발 워크로드가 설치되어 있으면 표시되는 클라우드 탐색기 메뉴 옵션을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-115">The following screenshot shows the Cloud Explorer menu option that will be present if you have the Azure development workload installed.</span></span>

    ![클라우드 탐색기 메뉴 옵션이 강조 표시된 Visual Studio 보기 메뉴의 스크린샷입니다.](../media/5-verify-cloud-explorer.png)

<span data-ttu-id="ad803-117">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="ad803-117">::: zone-end</span></span>

<span data-ttu-id="ad803-118">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="ad803-118">::: zone pivot="macos"</span></span>

### <a name="macos"></a><span data-ttu-id="ad803-119">macOS</span><span class="sxs-lookup"><span data-stu-id="ad803-119">macOS</span></span>

1. <span data-ttu-id="ad803-120">https://visualstudio.microsoft.com/으로 이동하여 Mac용 Visual Studio 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-120">Go to https://visualstudio.microsoft.com/ and download the Visual Studio for Mac installer.</span></span>

1. <span data-ttu-id="ad803-121">VisualStudioInstaller.dmg 파일을 클릭하여 설치 관리자를 탑재한 후, 로고를 두 번 클릭하여 설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-121">Click the VisualStudioInstaller.dmg file to mount the installer, then run it by double-clicking the logo.</span></span>

1. <span data-ttu-id="ad803-122">개인정보처리방침 및 라이선스 조건이 표시되면 동의합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-122">Acknowledge the Privacy and License terms when presented.</span></span>

1. <span data-ttu-id="ad803-123">설치 관리자에서 설치할 구성 요소를 물어봅니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-123">The installer will ask which components you wish to install.</span></span> <span data-ttu-id="ad803-124">Azure 구성 요소는 이미 Mac용 Visual Studio의 일부이지만 Azure용 웹 환경을 개발하려면 **.NET Core** 플랫폼을 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-124">Azure components are already part of Visual Studio for Mac, but it is recommended to install the **.NET Core** platform to develop web experiences for Azure.</span></span>

    <span data-ttu-id="ad803-125">다음 스크린샷은 Mac용 Visual Studio에 Azure 개발 기능을 추가하는 데 필요한 .NET Core 플랫폼을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-125">The following screenshot shows the .NET Core platform required to add Azure development capabilities to Visual Studio for Mac.</span></span>

    ![선택한 .NET Core 플랫폼 옵션이 강조되어 있는 Mac용 Visual Studio 설치 관리자의 스크린샷입니다.](../media/5-vsmac-install-net-core.png)

1. <span data-ttu-id="ad803-127">선택 사항에 만족하면 **설치 및 업데이트**를 클릭하고 설치 관리자가 완료될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-127">Click **Install and Update** once you are happy with the selections, and wait for the installer to complete.</span></span>

1. <span data-ttu-id="ad803-128">필요한 권한을 승격하도록 메시지가 표시되면 관리자 자격 증명을 사용하여 권한을 승격합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-128">If you are prompted to elevate the permissions needed, use your administrator credentials to do so.</span></span>

1. <span data-ttu-id="ad803-129">설치 관리자가 완료되면 Mac용 Visual Studio를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ad803-129">Once the installer is complete, start Visual Studio for Mac.</span></span>

<span data-ttu-id="ad803-130">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="ad803-130">::: zone-end</span></span>