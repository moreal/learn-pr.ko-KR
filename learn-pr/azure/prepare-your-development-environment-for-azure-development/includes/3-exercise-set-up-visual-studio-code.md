<span data-ttu-id="1dff3-101">이 연습에서는 Visual Studio Code 및 Azure App Service 확장을 설치하여 Microsoft Azure용으로 개발하고 웹앱을 배포할 준비를 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-101">In this exercise, you will install Visual Studio Code and the Azure App Service extension, which will get you ready to develop for Microsoft Azure and to deploy a web app.</span></span>

## <a name="exercise-steps"></a><span data-ttu-id="1dff3-102">연습 단계</span><span class="sxs-lookup"><span data-stu-id="1dff3-102">Exercise steps</span></span>

<span data-ttu-id="1dff3-103">먼저, 사용 중인 운영 체제를 식별하고 아래 해당 섹션의 단계에 따라 Visual Studio Code를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-103">First, identify which operating system you are using, and follow the steps in the appropriate section below to install Visual Studio Code.</span></span>

### <a name="windows"></a><span data-ttu-id="1dff3-104">Windows</span><span class="sxs-lookup"><span data-stu-id="1dff3-104">Windows</span></span>

1. <span data-ttu-id="1dff3-105">Windows용 Visual Studio Code 설치 관리자를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-105">Download the Visual Studio Code installer for Windows.</span></span>

1. <span data-ttu-id="1dff3-106">설치 관리자를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-106">Run the installer.</span></span> <span data-ttu-id="1dff3-107">시간이 오래 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-107">This won't take long.</span></span>

1. <span data-ttu-id="1dff3-108">설치 폴더(64비트 머신의 경우 기본 경로는 C:\Program Files\Microsoft VS Code)로 이동하여 VS Code를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-108">Open VS Code by navigating to the installation folder (the default path is C:\Program Files\Microsoft VS Code for a 64-bit machine).</span></span>

### <a name="macos"></a><span data-ttu-id="1dff3-109">macOS</span><span class="sxs-lookup"><span data-stu-id="1dff3-109">macOS</span></span>

1. <span data-ttu-id="1dff3-110">macOS용 Visual Studio Code를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-110">Download Visual Studio Code for macOS.</span></span>

1. <span data-ttu-id="1dff3-111">다운로드한 압축 파일을 두 번 클릭하여 콘텐츠를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-111">Double-click on the downloaded archive to expand the contents.</span></span>

1. <span data-ttu-id="1dff3-112">Visual Studio Code.app을 응용 프로그램 폴더로 끌어 실행 패드에서 사용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-112">Drag Visual Studio Code.app to the Applications folder, making it available in the Launchpad.</span></span>

1. <span data-ttu-id="1dff3-113">아이콘을 마우스 오른쪽 단추로 클릭하고 [옵션] > [Keep in Dock]\(도크에 유지)를 선택하여 VS Code를 도크에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-113">Add VS Code to your Dock by right-clicking on the icon, and choosing Options > Keep in Dock.</span></span>

### <a name="linux--debian-and-ubuntu"></a><span data-ttu-id="1dff3-114">Linux - Debian 및 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="1dff3-114">Linux – Debian and Ubuntu</span></span>

1. <span data-ttu-id="1dff3-115">그래픽 소프트웨어 센터(사용 가능한 경우) 또는 명령줄(다운로드한 .deb 파일 이름으로 `<file>`을 바꿈)을 통해 [.deb 패키지(64비트)](https://go.microsoft.com/fwlink/?LinkID=760868)를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-115">Download and install the [.deb package (64-bit)](https://go.microsoft.com/fwlink/?LinkID=760868), either through the graphical software center, if it's available, or through the command line (replacing `<file>` with the .deb filename you downloaded):</span></span>

    ```bash
    sudo dpkg -i <file>.deb
    sudo apt-get install -f # Install dependencies
    ```

### <a name="linux--rhel-fedora-and-centos"></a><span data-ttu-id="1dff3-116">Linux - RHEL, Fedora 및 CentOS</span><span class="sxs-lookup"><span data-stu-id="1dff3-116">Linux – RHEL, Fedora, and CentOS</span></span>

1. <span data-ttu-id="1dff3-117">다음 스크립트를 사용하여 키 및 리포지토리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-117">Use the following script to install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/yum.repos.d/vscode.repo'
    ```

1. <span data-ttu-id="1dff3-118">패키지 캐시를 업데이트하고 dnf(Fedora 22 이상)를 사용하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-118">Update the package cache, and install the package by using dnf (Fedora 22 and above):</span></span>

    ```bash
    dnf check-update
    sudo dnf install code
    ```

### <a name="linux--opensuse-and-sle"></a><span data-ttu-id="1dff3-119">Linux - openSUSE 및 SLE</span><span class="sxs-lookup"><span data-stu-id="1dff3-119">Linux – openSUSE and SLE</span></span>

1. <span data-ttu-id="1dff3-120">yum 리포지토리는 openSUSE 및 SLE 기반 시스템에 대해서도 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-120">The yum repository also works for openSUSE and SLE based systems.</span></span> <span data-ttu-id="1dff3-121">다음 스크립트는 키 및 리포지토리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-121">The following script will install the key and repository:</span></span>

    ```bash
    sudo rpm --import https://packages.microsoft.com/keys/microsoft.asc
    sudo sh -c 'echo -e "[code]\nname=Visual Studio Code\nbaseurl=https://packages.microsoft.com/yumrepos/vscode\nenabled=1\ntype=rpm-md\ngpgcheck=1\ngpgkey=https://packages.microsoft.com/keys/microsoft.asc" > /etc/zypp/repos.d/vscode.repo'
    ```

1. <span data-ttu-id="1dff3-122">패키지 캐시를 업데이트하고 다음을 사용하여 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-122">Update the package cache and install the package by using:</span></span>

    ```bash
    sudo zypper refresh
    sudo zypper install code
    ```

> [!NOTE]
> <span data-ttu-id="1dff3-123">다양한 Linux 배포에서 VS Code를 설치하거나 업데이트하는 방법에 대한 자세한 내용은 [Running VS Code on Linux](https://code.visualstudio.com/docs/setup/linux)(Linux에서 VS Code 실행) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="1dff3-123">For further details about installing or updating VS Code on various Linux distributions, please see the [Running VS Code on Linux documentation](https://code.visualstudio.com/docs/setup/linux).</span></span>

## <a name="install-azure-app-service-extension"></a><span data-ttu-id="1dff3-124">Azure App Service 확장 설치</span><span class="sxs-lookup"><span data-stu-id="1dff3-124">Install Azure App Service extension</span></span>

<span data-ttu-id="1dff3-125">VS Code를 설치했으면 VS Code를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-125">Once you have installed VS Code, open it.</span></span>

1. <span data-ttu-id="1dff3-126">확장 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-126">Go to the Extensions tab.</span></span>

1. <span data-ttu-id="1dff3-127">Azure App Service를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-127">Search for Azure App Service.</span></span>

1. <span data-ttu-id="1dff3-128">[설치]를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-128">Click Install.</span></span>

    <span data-ttu-id="1dff3-129">다음 스크린샷은 Visual Studio Code 확장 검색 결과에서 Azure App Service 확장이 선택되어 있는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-129">The following screenshot shows the Azure App Service extension selected from the Visual Studio Code extension search results.</span></span>

    ![검색 결과에 Azure App Service 확장이 강조되어 있는 확장 탭을 보여 주는 VS Code 스크린샷입니다.](../media/3-install-azure-extension.png)

<span data-ttu-id="1dff3-131">확장이 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-131">This will install the extension.</span></span> <span data-ttu-id="1dff3-132">Azure 구독에 연결하고 웹, 모바일 또는 API 앱용으로 개발하여 Azure App Service에 배포할 준비도 완료됩니다.</span><span class="sxs-lookup"><span data-stu-id="1dff3-132">You will be ready to connect to your Azure subscription, and develop for and deploy your web, mobile, or API app to an Azure App Service.</span></span>
