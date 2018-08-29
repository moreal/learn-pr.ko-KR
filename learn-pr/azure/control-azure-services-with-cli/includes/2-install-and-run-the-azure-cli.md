## <a name="motivation"></a><span data-ttu-id="2dcaf-101">사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="2dcaf-101">Motivation</span></span>
<span data-ttu-id="2dcaf-102">회사에서 Azure 리소스를 관리하기 위한 명령줄 솔루션으로 Azure CLI를 선택했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-102">Suppose your company has chosen the Azure CLI as your command-line solution for managing Azure resources.</span></span> <span data-ttu-id="2dcaf-103">관리자 및 개발자는 브라우저를 사용하는 것보다 명령 및 스크립트를 로컬로 실행하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-103">Your administrators and developers prefer to run their commands and scripts locally rather than through a browser.</span></span> <span data-ttu-id="2dcaf-104">팀은 Linux, macOS 및 Windows를 실행하는 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-104">The team uses machines that run Linux, macOS, and Windows.</span></span> <span data-ttu-id="2dcaf-105">Azure CLI가 모든 장치에서 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-105">You need to get the Azure CLI working on all their devices.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="2dcaf-106">Azure CLI란?</span><span class="sxs-lookup"><span data-stu-id="2dcaf-106">What is the Azure CLI?</span></span>
<span data-ttu-id="2dcaf-107">Azure CLI는 Azure에 연결하고 Azure 리소스에서 관리 명령을 실행하는 명령줄 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-107">The Azure CLI is a command-line program to connect to Azure and execute administrative commands on Azure resources.</span></span> <span data-ttu-id="2dcaf-108">예를 들어 VM(가상 머신)을 다시 시작하려면 다음과 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-108">For example, to restart a Virtual Machine (VM), you would use a command like the following:</span></span>

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

<span data-ttu-id="2dcaf-109">Azure CLI는 Azure 리소스를 관리하기 위한 플랫폼 간 명령줄 도구를 제공하며 Linux, Mac 또는 Windows 컴퓨터에 로컬로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-109">The Azure CLI provides cross-platform command-line tools for managing Azure resources, and can be installed locally on Linux, Mac, or Windows computers.</span></span> <span data-ttu-id="2dcaf-110">Azure CLI는 Azure Cloud Shell을 통해 브라우저에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-110">The Azure CLI can also be used from a browser through the Azure Cloud Shell.</span></span> <span data-ttu-id="2dcaf-111">두 경우에 모두 대화형으로 사용하거나 스크립팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-111">In both cases, it can be used interactively or scripted.</span></span> <span data-ttu-id="2dcaf-112">대화형 사용의 경우 먼저 Windows에서 cmd.exe와 같은 셸을 먼저 시작하거나 Linux 또는 macOS에서 Bash를 시작한 후 셸 프롬프트에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-112">For interactive use, you first launch a shell such as cmd.exe on Windows or Bash on Linux or macOS and then issue the command at the shell prompt.</span></span> <span data-ttu-id="2dcaf-113">반복 작업을 자동화하려면 선택한 셸의 스크립트 구문을 사용하여 셸 스크립트로 CLI 명령을 어셈블한 후 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-113">To automate repetitive tasks, you assemble the CLI commands into a shell script using the script syntax of your chosen shell and then execute the script.</span></span>

## <a name="how-to-install-azure-cli"></a><span data-ttu-id="2dcaf-114">Azure CLI를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="2dcaf-114">How to install Azure CLI</span></span>
<span data-ttu-id="2dcaf-115">Linux 및 macOS에서는 둘 다 패키지 관리자를 사용하여 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-115">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="2dcaf-116">권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-116">The recommended package manager differs by OS and distribution:</span></span>
- <span data-ttu-id="2dcaf-117">Linux: **apt-get**(Ubuntu), **yum**(Red Hat) 및 **zypper**(OpenSUSE)</span><span class="sxs-lookup"><span data-stu-id="2dcaf-117">Linux: **apt-get** on Ubuntu, **yum** on Red Hat, and **zypper** on OpenSUSE</span></span>
- <span data-ttu-id="2dcaf-118">Mac: **Homebrew**</span><span class="sxs-lookup"><span data-stu-id="2dcaf-118">Mac: **Homebrew**</span></span>

<span data-ttu-id="2dcaf-119">Azure CLI는 Microsoft 리포지토리에서 사용할 수 있으므로 먼저 패키지 관리자에 해당 리포지토리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-119">The Azure CLI is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

<span data-ttu-id="2dcaf-120">Windows에서는 MSI 파일을 다운로드하고 실행하여 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-120">On Windows, you install the Azure CLI by downloading and running an MSI file.</span></span>

## <a name="using-the-azure-cli-in-scripts"></a><span data-ttu-id="2dcaf-121">스크립트에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="2dcaf-121">Using the Azure CLI in scripts</span></span>
<span data-ttu-id="2dcaf-122">스크립트에서 Azure CLI 명령을 사용하려면 스크립트 실행에 사용되는 “셸” 또는 환경에 관련된 문제를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-122">If you want to use the Azure CLI commands in scripts, you need to be aware of any issues around the "shell" or environment used for running the script.</span></span> <span data-ttu-id="2dcaf-123">예를 들어 bash 셸에서는 변수를 설정할 때 다음 구문이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-123">For example, in a bash shell, the following syntax is used when setting variables:</span></span>

 ```bash
 variable="string"
 variable=integer
 ```

<span data-ttu-id="2dcaf-124">Azure CLI 스크립트를 실행하는 데 PowerShell 환경을 사용하는 경우 변수에 이 구문을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-124">If you use a PowerShell environment for running Azure CLI scripts, you'll need to use this syntax for variables:</span></span>

 ```powershell
 $variable="string"
 $variable=integer
 ```

## <a name="summary"></a><span data-ttu-id="2dcaf-125">요약</span><span class="sxs-lookup"><span data-stu-id="2dcaf-125">Summary</span></span>
<span data-ttu-id="2dcaf-126">로컬 컴퓨터에서 Azure 리소스를 관리하는 데 사용하려면 먼저 Azure CLI를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-126">The Azure CLI must be installed before it can be used to manage Azure resources from a local computer.</span></span> <span data-ttu-id="2dcaf-127">설치 단계는 Windows, Linux 및 macOS에 따라 다르지만, 설치된 후에 명령은 전체 플랫폼에서 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="2dcaf-127">The installation steps vary for Windows, Linux, and macOS, but once installed, the commands are common across platforms.</span></span> 
