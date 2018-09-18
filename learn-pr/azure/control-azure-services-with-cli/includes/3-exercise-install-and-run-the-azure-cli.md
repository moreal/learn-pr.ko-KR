<span data-ttu-id="450dd-101">로컬 머신에 Azure CLI를 설치한 다음, 명령을 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-101">Let's install the Azure CLI on your local machine, and then run a command to verify your installation.</span></span> <span data-ttu-id="450dd-102">Azure CLI 설치에 사용하는 방법은 컴퓨터의 운영 체제에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-102">The method you use for installing the Azure CLI depends on the operating system of your computer.</span></span> <span data-ttu-id="450dd-103">운영 체제에 맞는 단계를 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="450dd-103">Choose the steps for your operating system.</span></span>

> [!NOTE]
> <span data-ttu-id="450dd-104">이 연습에서는 Azure CLI 도구를 로컬로 설치하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-104">This exercise guides you through installing the Azure CLI tool locally.</span></span> <span data-ttu-id="450dd-105">모듈의 나머지 부분에서는 Microsoft Learn의 무료 구독 지원을 활용할 수 있도록 Azure Cloud Shell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-105">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="450dd-106">이 연습을 선택적 작업으로 고려하고 원하는 경우 지침을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-106">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

<span data-ttu-id="450dd-107">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="450dd-107">::: zone pivot="linux"</span></span>

## <a name="linux"></a><span data-ttu-id="450dd-108">Linux</span><span class="sxs-lookup"><span data-stu-id="450dd-108">Linux</span></span>

<span data-ttu-id="450dd-109">여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 **Ubuntu Linux**에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-109">Here you will install the Azure CLI on **Ubuntu Linux** using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span>

> [!TIP]
> <span data-ttu-id="450dd-110">아래에 나열된 명령은 Ubuntu 버전 18.04용입니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-110">The commands listed below are for Ubuntu version 18.04.</span></span> <span data-ttu-id="450dd-111">Linux의 기타 버전 및 분산에는 다양한 지침이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-111">Other versions and distributions of Linux have different instructions.</span></span> <span data-ttu-id="450dd-112">다른 Linux 버전을 사용하는 경우 [공식 설명서](https://docs.microsoft.com/cli/azure/install-azure-cli)를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="450dd-112">Check the [official documentation](https://docs.microsoft.com/cli/azure/install-azure-cli) if you are using a different Linux version.</span></span>

1. <span data-ttu-id="450dd-113">Microsoft 리포지토리가 등록되도록 소스 목록을 수정하면 패키지 관리자가 Azure CLI 패키지를 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-113">Modify your sources list so that the Microsoft repository is registered, and the package manager can locate the Azure CLI package.</span></span>

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. <span data-ttu-id="450dd-114">Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-114">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="450dd-115">이렇게 하면 설치한 Azure CLI 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-115">This will allow the package manager to verify that the Azure CLI package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="450dd-116">Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-116">Install the Azure CLI.</span></span>

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

<span data-ttu-id="450dd-117">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="450dd-117">::: zone-end</span></span>

<span data-ttu-id="450dd-118">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="450dd-118">::: zone pivot="macos"</span></span>

## <a name="macos"></a><span data-ttu-id="450dd-119">macOS</span><span class="sxs-lookup"><span data-stu-id="450dd-119">macOS</span></span>

<span data-ttu-id="450dd-120">여기서는 Homebrew 패키지 관리자를 사용하여 macOS에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-120">Here you will install the Azure CLI on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="450dd-121">**brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-121">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="450dd-122">자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="450dd-122">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="450dd-123">최신 Azure CLI 패키지를 가져올 수 있도록 brew 리포지토리를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-123">Update your brew repository to make sure you get the latest Azure CLI package.</span></span>

    ```bash
    brew update
    ```

1. <span data-ttu-id="450dd-124">Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-124">Install the Azure CLI.</span></span>

    ```bash
    brew install azure-cli
    ```

<span data-ttu-id="450dd-125">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="450dd-125">::: zone-end</span></span>

<span data-ttu-id="450dd-126">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="450dd-126">::: zone pivot="windows"</span></span>

## <a name="windows"></a><span data-ttu-id="450dd-127">Windows</span><span class="sxs-lookup"><span data-stu-id="450dd-127">Windows</span></span>

<span data-ttu-id="450dd-128">여기서는 MSI 설치 프로그램을 사용하여 Windows에 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-128">Here you will install the Azure CLI on Windows using the MSI installer.</span></span>

1. <span data-ttu-id="450dd-129">[https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)로 이동하여 브라우저 보안 대화 상자에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-129">Go to [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows), and in the browser security dialog box, click **Run**.</span></span>
1. <span data-ttu-id="450dd-130">설치 프로그램에서 라이선스 이용 약관에 동의한 후에 **설치**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-130">In the installer, accept the license terms, and then click **Install**.</span></span>
1. <span data-ttu-id="450dd-131">**사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-131">In the **User Account Control** dialog, select **Yes**.</span></span>

<span data-ttu-id="450dd-132">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="450dd-132">::: zone-end</span></span>

## <a name="running-the-azure-cli"></a><span data-ttu-id="450dd-133">Azure CLI 실행</span><span class="sxs-lookup"><span data-stu-id="450dd-133">Running the Azure CLI</span></span>

<span data-ttu-id="450dd-134">bash 셸(Linux 및 macOS) 또는 명령 프롬프트나 PowerShell(Windows)을 열어 Azure CLI를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-134">You run the Azure CLI by opening a bash shell (Linux and macOS), or from the command prompt or PowerShell (Windows).</span></span>

1. <span data-ttu-id="450dd-135">Azure CLI를 시작하고 버전 검사를 실행하여 설치를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-135">Start the Azure CLI and verify your installation by running the version check.</span></span>

    ```azurecli
    az --version
    ```

<span data-ttu-id="450dd-136">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="450dd-136">::: zone pivot="windows"</span></span>

> [!TIP]
> <span data-ttu-id="450dd-137">PowerShell에서 Azure CLI를 실행하면 Windows 명령 프롬프트에서 Azure CLI를 실행할 때에 비해 몇 가지 장점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-137">Running the Azure CLI from PowerShell has some advantages over running the Azure CLI from the Windows command prompt.</span></span> <span data-ttu-id="450dd-138">PowerShell은 명령 프롬프트에서 사용할 수 있는 탭 완성 기능 외에 일부 탭 완성 기능을 추가로 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-138">PowerShell provides additional tab completion features over those available from the command prompt.</span></span>

<span data-ttu-id="450dd-139">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="450dd-139">::: zone-end</span></span>

<span data-ttu-id="450dd-140">Azure CLI를 사용하여 Azure 리소스를 관리하도록 로컬 머신을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-140">You set up your local machines to administer Azure resources with the Azure CLI.</span></span> <span data-ttu-id="450dd-141">이제 로컬에서 Azure CLI를 사용하여 명령을 입력하거나 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-141">You can now use the Azure CLI locally to enter commands or execute scripts.</span></span> <span data-ttu-id="450dd-142">Azure CLI가 Azure 데이터 센터로 명령을 전달하면 Azure 구독 내에서 명령이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="450dd-142">The Azure CLI will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>