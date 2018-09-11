<span data-ttu-id="8d837-101">이 단원에서는 로컬 컴퓨터에 **Azure PowerShell**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-101">In this unit, you will install **Azure PowerShell** on your local machine.</span></span> <span data-ttu-id="8d837-102">운영 체제에 적합한 섹션을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="8d837-102">Choose the appropriate section for your operating system.</span></span>

## <a name="linux-and-mac"></a><span data-ttu-id="8d837-103">Linux 및 Mac</span><span class="sxs-lookup"><span data-stu-id="8d837-103">Linux and Mac</span></span>
<span data-ttu-id="8d837-104">Linux 및 macOS에서의 첫 번째 단계는 **PowerShell Core**를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-104">On Linux and macOS, the first step is to install **PowerShell Core**.</span></span>

### <a name="linux"></a><span data-ttu-id="8d837-105">Linux</span><span class="sxs-lookup"><span data-stu-id="8d837-105">Linux</span></span>
<span data-ttu-id="8d837-106">마지막 단원에서 언급한 것처럼 Linux용 PowerShell을 설치하면 패키지 관리자를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-106">As mentioned in the last unit, installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="8d837-107">여기에 나온 예에서는 **Ubuntu 18.04**를 사용하지만, [설명서에 다른 버전 및 배포에 대한 자세한 지침](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-107">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="8d837-108">여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 Ubuntu Linux에 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-108">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="8d837-109">Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-109">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="8d837-110">이렇게 하면 설치한 PowerShell Core 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-110">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="8d837-111">패키지 관리자가 PowerShell Core 패키지를 찾을 수 있도록 **Microsoft Ubuntu 리포지토리**를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-111">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="8d837-112">패키지 목록을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-112">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="8d837-113">PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-113">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="8d837-114">PowerShell을 시작하여 성공적으로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-114">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```

### <a name="macos"></a><span data-ttu-id="8d837-115">macOS</span><span class="sxs-lookup"><span data-stu-id="8d837-115">macOS</span></span>
<span data-ttu-id="8d837-116">이번에는 Homebrew 패키지 관리자를 사용하여 macOS에 **PowerShell Core**를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-116">Next, install **PowerShell Core** on macOS using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d837-117">**brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-117">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="8d837-118">자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="8d837-118">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="8d837-119">PowerShell Core 패키지를 포함하여 추가 패키지를 얻으려면 Homebrew-Cask를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="8d837-119">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```

1. <span data-ttu-id="8d837-120">PowerShell Core 설치:</span><span class="sxs-lookup"><span data-stu-id="8d837-120">Install PowerShell Core:</span></span>

    ```bash
    brew cask installs powershell
    ```

1. <span data-ttu-id="8d837-121">PowerShell Core를 시작하여 성공적으로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-121">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

## <a name="install-azure-powershell"></a><span data-ttu-id="8d837-122">Azure Powershell 설치</span><span class="sxs-lookup"><span data-stu-id="8d837-122">Install Azure PowerShell</span></span>
<span data-ttu-id="8d837-123">기본 **PowerShell** 제품을 설치한 후에는 **Azure PowerShell**을 설치하여 Azure 관련 명령을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-123">After installing the base **PowerShell** product, install **Azure PowerShell** to add the Azure-specific commands.</span></span>

### <a name="windows"></a><span data-ttu-id="8d837-124">Windows</span><span class="sxs-lookup"><span data-stu-id="8d837-124">Windows</span></span>
<span data-ttu-id="8d837-125">`Install-Module` PowerShell 명령을 사용하여 Windows에 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-125">Install Azure PowerShell on Windows using the `Install-Module` PowerShell command.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8d837-126">Azure PowerShell을 설치하려면 PowerShell 버전 5.0 이상이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-126">You must have PowerShell version 5.0 or higher to install Azure PowerShell.</span></span> <span data-ttu-id="8d837-127">PowerShell 버전을 확인하려면 다음 명령을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="8d837-127">To check your version of PowerShell, use the following command:</span></span> 
>
> `$PSVersionTable.PSVersion` 
>
><span data-ttu-id="8d837-128">버전 번호가 5.0 미만인 경우 [기존 Windows PowerShell 업그레이드](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)에 대한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="8d837-128">If the version number is lower than 5.0, follow the instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

1. <span data-ttu-id="8d837-129">**시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-129">Open the **Start** menu and type **Windows PowerShell**.</span></span>

1. <span data-ttu-id="8d837-130">**Windows PowerShell** 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-130">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>

1. <span data-ttu-id="8d837-131">**사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-131">In the **User Account Control** dialog, select **Yes**.</span></span>

1. <span data-ttu-id="8d837-132">다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-132">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```

1. <span data-ttu-id="8d837-133">PSGallery의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-133">If you are asked whether you trust modules from PSGallery, answer **Yes** or **Yes to All**.</span></span>

> [!TIP]
> <span data-ttu-id="8d837-134">Azure PowerShell 모듈 버전이 이미 설치되어 있음을 나타내는 오류 메시지가 표시되면 다음 명령을 실행하여 _최신_ 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-134">If you get an error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>
> 
> `Update-Module -Name AzureRM`
> 
> <span data-ttu-id="8d837-135">`Install-Module` 명령과 마찬가지로, 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-135">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span>

### <a name="linux-or-macos"></a><span data-ttu-id="8d837-136">Linux 또는 macOS</span><span class="sxs-lookup"><span data-stu-id="8d837-136">Linux or macOS</span></span>
<span data-ttu-id="8d837-137">동일한 기본 프로세스를 사용하여 Linux 또는 macOS에 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-137">We use the same basic process to install the Azure PowerShell on either Linux or macOS.</span></span> <span data-ttu-id="8d837-138">이 절차는 두 운영 체제에서 모두 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-138">The procedure is the same for both operating systems.</span></span> <span data-ttu-id="8d837-139">차이점은 승격된 PowerShell Core 세션을 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-139">The difference is in getting an elevated PowerShell Core session.</span></span>

1. <span data-ttu-id="8d837-140">터미널에서 승격된 권한으로 PowerShell Core를 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-140">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="8d837-141">Azure PowerShell을 설치하려면 PowerShell Core 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-141">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="8d837-142">**PSGallery**의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-142">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

## <a name="summary"></a><span data-ttu-id="8d837-143">요약</span><span class="sxs-lookup"><span data-stu-id="8d837-143">Summary</span></span>
<span data-ttu-id="8d837-144">Azure PowerShell을 사용하여 Azure 리소스를 관리할 로컬 머신을 설정했습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-144">You have setup your local machine(s) to administer Azure resources with Azure PowerShell.</span></span> <span data-ttu-id="8d837-145">이제 Azure PowerShell을 로컬에서 사용하여 명령을 입력하거나 스크립트를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-145">You can now use Azure PowerShell locally to enter commands or execute scripts.</span></span> <span data-ttu-id="8d837-146">Azure PowerShell이 Azure 데이터 센터로 명령을 전달하면 Azure 구독 내에서 명령이 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d837-146">Azure PowerShell will forward your commands to the Azure datacenters where they will run inside your Azure subscription.</span></span>