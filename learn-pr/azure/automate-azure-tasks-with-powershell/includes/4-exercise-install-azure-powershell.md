<span data-ttu-id="2c15c-101">이 단원에서는 로컬 머신에 **PowerShell**을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-101">In this unit, you will install **PowerShell** on your local machine.</span></span>

> [!NOTE]
> <span data-ttu-id="2c15c-102">이 연습에서는 PowerShell 도구를 로컬로 설치하는 단계를 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-102">This exercise guides you through installing the PowerShell tools locally.</span></span> <span data-ttu-id="2c15c-103">모듈의 나머지 부분에서는 Microsoft Learn의 무료 구독 지원을 활용할 수 있도록 Azure Cloud Shell을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-103">The remainder of the module will use the Azure Cloud Shell so you can leverage the free subscription support in Microsoft Learn.</span></span> <span data-ttu-id="2c15c-104">이 연습을 선택적 작업으로 고려하고 원하는 경우 지침을 검토할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-104">You can consider this exercise as an optional activity and just review the instructions if you prefer.</span></span>

<span data-ttu-id="2c15c-105">::: zone pivot="linux"</span><span class="sxs-lookup"><span data-stu-id="2c15c-105">::: zone pivot="linux"</span></span>

## <a name="linux"></a><span data-ttu-id="2c15c-106">Linux</span><span class="sxs-lookup"><span data-stu-id="2c15c-106">Linux</span></span>

<span data-ttu-id="2c15c-107">Linux용 PowerShell을 설치하면 패키지 관리자를 사용하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-107">Installing PowerShell for Linux will involve using a package manager.</span></span> <span data-ttu-id="2c15c-108">여기 예제에서는 **Ubuntu 18.04**를 사용하지만, [설명서에 다른 버전 및 배포에 대한 자세한 지침](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)이 나와 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-108">We will use **Ubuntu 18.04** for our example here, but we have [detailed instructions for other versions and distributions in our documentation](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux).</span></span>

<span data-ttu-id="2c15c-109">여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 Ubuntu Linux에 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-109">You will install PowerShell Core on Ubuntu Linux using the Advanced Packaging Tool (**apt**) and the Bash command line.</span></span> 

1. <span data-ttu-id="2c15c-110">Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-110">Import the encryption key for the Microsoft Ubuntu repository.</span></span> <span data-ttu-id="2c15c-111">이렇게 하면 설치한 PowerShell Core 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-111">This will allow the package manager to verify that the PowerShell Core package you install comes from Microsoft.</span></span>

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. <span data-ttu-id="2c15c-112">패키지 관리자가 PowerShell Core 패키지를 찾을 수 있도록 **Microsoft Ubuntu 리포지토리**를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-112">Register the **Microsoft Ubuntu repository** so the package manager can locate the PowerShell Core package.</span></span>

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. <span data-ttu-id="2c15c-113">패키지 목록을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-113">Update the list of packages.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="2c15c-114">PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-114">Install PowerShell Core.</span></span>

    ```bash
    sudo apt-get install -y powershell
    ```

1. <span data-ttu-id="2c15c-115">PowerShell을 시작하여 성공적으로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-115">Start PowerShell to verify that it installed successfully.</span></span>

    ```bash
    pwsh
    ```
<span data-ttu-id="2c15c-116">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="2c15c-116">::: zone-end</span></span>

<span data-ttu-id="2c15c-117">::: zone pivot="macos"</span><span class="sxs-lookup"><span data-stu-id="2c15c-117">::: zone pivot="macos"</span></span>

## <a name="macos"></a><span data-ttu-id="2c15c-118">MacOS</span><span class="sxs-lookup"><span data-stu-id="2c15c-118">MacOS</span></span>

<span data-ttu-id="2c15c-119">macOS에서 첫 번째 단계는 **PowerShell Core**를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-119">On macOS, the first step is to install **PowerShell Core**.</span></span> <span data-ttu-id="2c15c-120">Homebrew 패키지 관리자를 사용하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-120">This is done using the Homebrew package manager.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2c15c-121">**brew** 명령을 사용할 수 없는 경우 Homebrew 패키지 관리자를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-121">If the **brew** command is unavailable, you may need to install the Homebrew package manager.</span></span> <span data-ttu-id="2c15c-122">자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="2c15c-122">For details see the [Homebrew website](https://brew.sh/).</span></span>

1. <span data-ttu-id="2c15c-123">PowerShell Core 패키지를 포함하여 추가 패키지를 얻으려면 Homebrew-Cask를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="2c15c-123">Install Homebrew-Cask to obtain more packages, including the PowerShell Core package:</span></span>

    ```bash
    brew tap caskroom/cask
    ```

1. <span data-ttu-id="2c15c-124">PowerShell Core 설치:</span><span class="sxs-lookup"><span data-stu-id="2c15c-124">Install PowerShell Core:</span></span>

    ```bash
    brew cask install powershell
    ```

1. <span data-ttu-id="2c15c-125">PowerShell Core를 시작하여 성공적으로 설치되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-125">Start PowerShell Core to verify that it installed successfully:</span></span>

    ```bash
    pwsh
    ```

<span data-ttu-id="2c15c-126">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="2c15c-126">::: zone-end</span></span>

<span data-ttu-id="2c15c-127">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="2c15c-127">::: zone pivot="windows"</span></span>

## <a name="windows"></a><span data-ttu-id="2c15c-128">Windows</span><span class="sxs-lookup"><span data-stu-id="2c15c-128">Windows</span></span>
<span data-ttu-id="2c15c-129">PowerShell은 Windows에 포함되지만 머신에 사용할 수 없는 업데이트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-129">PowerShell is included with Windows, however there may be an update available for your machine.</span></span> <span data-ttu-id="2c15c-130">사용하려는 Azure 지원에는 PowerShell 버전 5.0 이상이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-130">The Azure support we are going to use requires PowerShell version 5.0 or higher.</span></span> <span data-ttu-id="2c15c-131">다음 단계를 통해 설치된 버전을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-131">You can check the version you have installed through the following steps:</span></span>

1. <span data-ttu-id="2c15c-132">**시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-132">Open the **Start** menu and type **Windows PowerShell**.</span></span> <span data-ttu-id="2c15c-133">여러 바로 가기 링크를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-133">There may be multiple shortcut links available:</span></span>
    - <span data-ttu-id="2c15c-134">Windows PowerShell - 64비트 버전이며 일반적으로 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-134">Windows PowerShell - this is the 64-bit version and generally what you should choose.</span></span>
    - <span data-ttu-id="2c15c-135">Windows PowerShell(x86) - 64비트 Windows에 설치된 32비트 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-135">Windows PowerShell (x86) - this is a 32-bit version installed on 64-bit Windows.</span></span>
    - <span data-ttu-id="2c15c-136">Windows PowerShell ISE - ISE(통합 스크립팅 환경)는 PowerShell에서 스크립트를 작성하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-136">Windows PowerShell ISE - The Integrated Scripting Environment (ISE) is used for writing scripts in PowerShell.</span></span> 
    - <span data-ttu-id="2c15c-137">Windows PowerShell ISE(x86) - 32비트 버전의 ISE입니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-137">Windows PowerShell ISE (x86) - A 32-bit version of the ISE.</span></span>

1. <span data-ttu-id="2c15c-138">Windows PowerShell 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-138">Select the Windows PowerShell icon.</span></span>

1. <span data-ttu-id="2c15c-139">다음 명령을 입력하여 설치된 PowerShell 버전을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-139">Type the following command to determine the version of PowerShell installed.</span></span>

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
<span data-ttu-id="2c15c-140">버전 번호가 5.0 미만인 경우 [기존 Windows PowerShell을 업그레이드](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)하기 위한 이러한 지침을 따르세요.</span><span class="sxs-lookup"><span data-stu-id="2c15c-140">If the version number is lower than 5.0, follow these instructions for [upgrading existing Windows PowerShell](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell).</span></span>

<span data-ttu-id="2c15c-141">::: zone-end</span><span class="sxs-lookup"><span data-stu-id="2c15c-141">::: zone-end</span></span>

<span data-ttu-id="2c15c-142">PowerShell을 지원하도록 로컬 머신을 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-142">You have setup your local machine(s) to support PowerShell.</span></span> <span data-ttu-id="2c15c-143">다음으로, Azure 모듈을 포함하여 추가할 수 있는 추가 명령에 대해 다루겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2c15c-143">Next, we will talk about additional commands you can add including the Azure module.</span></span>