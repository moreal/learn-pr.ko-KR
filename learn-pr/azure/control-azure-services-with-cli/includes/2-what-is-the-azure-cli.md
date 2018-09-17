<span data-ttu-id="14545-101">Azure CLI는 Azure에 연결하고 Azure 리소스에서 관리 명령을 실행하는 명령줄 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="14545-101">The Azure CLI is a command-line program to connect to Azure and execute administrative commands on Azure resources.</span></span> <span data-ttu-id="14545-102">이 기능은 Linux, macOS 및 Windows에서 실행되며 관리자와 개발자가 이를 사용하여 웹 브라우저 대신 터미널 또는 명령줄 프롬프트(또는 스크립트)를 통해 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14545-102">It runs on Linux, macOS, and Windows and allows administrators and developers to execute their commands through a terminal or command-line prompt (or script!) instead of a web browser.</span></span> <span data-ttu-id="14545-103">예를 들어 VM(가상 머신)을 다시 시작하려면 다음과 같은 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-103">For example, to restart a virtual machine (VM), you would use a command like the following:</span></span>

 ```azurecli
 az vm restart -g MyResourceGroup -n MyVm
 ```

<span data-ttu-id="14545-104">Azure CLI는 Azure 리소스를 관리하기 위한 플랫폼 간 명령줄 도구를 제공하며 Linux, Mac 또는 Windows 컴퓨터에 로컬로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14545-104">The Azure CLI provides cross-platform command-line tools for managing Azure resources, and can be installed locally on Linux, Mac, or Windows computers.</span></span> <span data-ttu-id="14545-105">Azure CLI는 Azure Cloud Shell을 통해 브라우저에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14545-105">The Azure CLI can also be used from a browser through the Azure Cloud Shell.</span></span> <span data-ttu-id="14545-106">두 경우에 모두 대화형으로 사용하거나 스크립팅할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="14545-106">In both cases, it can be used interactively or scripted.</span></span> <span data-ttu-id="14545-107">대화형 사용의 경우 먼저 Windows에서 cmd.exe와 같은 셸을 먼저 시작하거나 Linux 또는 macOS에서 Bash를 시작한 후 셸 프롬프트에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-107">For interactive use, you first launch a shell such as cmd.exe on Windows or Bash on Linux or macOS and then issue the command at the shell prompt.</span></span> <span data-ttu-id="14545-108">반복 작업을 자동화하려면 선택한 셸의 스크립트 구문을 사용하여 셸 스크립트로 CLI 명령을 어셈블한 후 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-108">To automate repetitive tasks, you assemble the CLI commands into a shell script using the script syntax of your chosen shell and then execute the script.</span></span>

## <a name="how-to-install-azure-cli"></a><span data-ttu-id="14545-109">Azure CLI를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="14545-109">How to install Azure CLI</span></span>

<span data-ttu-id="14545-110">Linux 및 macOS에서는 둘 다 패키지 관리자를 사용하여 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-110">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="14545-111">권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="14545-111">The recommended package manager differs by OS and distribution:</span></span>

- <span data-ttu-id="14545-112">Linux: **apt-get**(Ubuntu), **yum**(Red Hat) 및 **zypper**(OpenSUSE)</span><span class="sxs-lookup"><span data-stu-id="14545-112">Linux: **apt-get** on Ubuntu, **yum** on Red Hat, and **zypper** on OpenSUSE</span></span>
- <span data-ttu-id="14545-113">Mac: **Homebrew**</span><span class="sxs-lookup"><span data-stu-id="14545-113">Mac: **Homebrew**</span></span>

<span data-ttu-id="14545-114">Azure CLI는 Microsoft 리포지토리에서 사용할 수 있으므로 먼저 패키지 관리자에 해당 리포지토리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-114">The Azure CLI is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

<span data-ttu-id="14545-115">Windows에서는 MSI 파일을 다운로드하고 실행하여 Azure CLI를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-115">On Windows, you install the Azure CLI by downloading and running an MSI file.</span></span>

## <a name="using-the-azure-cli-in-scripts"></a><span data-ttu-id="14545-116">스크립트에서 Azure CLI 사용</span><span class="sxs-lookup"><span data-stu-id="14545-116">Using the Azure CLI in scripts</span></span>

<span data-ttu-id="14545-117">스크립트에서 Azure CLI 명령을 사용하려면 스크립트 실행에 사용되는 “셸” 또는 환경에 관련된 문제를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-117">If you want to use the Azure CLI commands in scripts, you need to be aware of any issues around the "shell" or environment used for running the script.</span></span> <span data-ttu-id="14545-118">예를 들어 bash 셸에서는 변수를 설정할 때 다음 구문이 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="14545-118">For example, in a bash shell, the following syntax is used when setting variables:</span></span>

```azurecli
variable="value"
variable=integer
```

<span data-ttu-id="14545-119">Azure CLI 스크립트를 실행하는 데 PowerShell 환경을 사용하는 경우 변수에 이 구문을 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-119">If you use a PowerShell environment for running Azure CLI scripts, you'll need to use this syntax for variables:</span></span>

```powershell
$variable="value"
$variable=integer
```

<span data-ttu-id="14545-120">로컬 컴퓨터에서 Azure 리소스를 관리하는 데 사용하려면 먼저 Azure CLI를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="14545-120">The Azure CLI must be installed before it can be used to manage Azure resources from a local computer.</span></span> <span data-ttu-id="14545-121">설치 단계는 Windows, Linux 및 macOS에 따라 다르지만, 설치된 후에 명령은 전체 플랫폼에서 공통적입니다.</span><span class="sxs-lookup"><span data-stu-id="14545-121">The installation steps vary for Windows, Linux, and macOS, but once installed, the commands are common across platforms.</span></span>
