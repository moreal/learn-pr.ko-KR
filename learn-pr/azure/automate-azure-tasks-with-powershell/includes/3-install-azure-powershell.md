<span data-ttu-id="79219-101">Azure PowerShell을 자동화 솔루션으로 선택했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-101">Suppose you have chosen Azure PowerShell as your automation solution.</span></span> <span data-ttu-id="79219-102">관리자는 Azure Cloud Shell 대신 로컬로 스크립트를 실행하는 것을 선호합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-102">Your administrators prefer to run their scripts locally rather than in the Azure Cloud Shell.</span></span> <span data-ttu-id="79219-103">팀은 Linux, macOS 및 Windows를 실행하는 컴퓨터를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-103">The team uses machines that run Linux, macOS, and Windows.</span></span> <span data-ttu-id="79219-104">Azure PowerShell이 모든 장치에서 작동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-104">You need to get Azure PowerShell working on all their devices.</span></span> 

## <a name="what-must-be-installed"></a><span data-ttu-id="79219-105">무엇을 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="79219-105">What must be installed?</span></span>
<span data-ttu-id="79219-106">다음 단원에서 실제 설치 지침을 살펴보고 Azure PowerShell을 구성하는 두 개의 구성 요소를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="79219-106">We'll go through the actual installation instructions in the next unit, but let's look at the two components which make up Azure PowerShell.</span></span>

- <span data-ttu-id="79219-107">**기본 PowerShell 제품** 이 제품에는 Windows용 PowerShell 및 macOS/Linux용 PowerShell Core의 두 가지 변형이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="79219-107">**The base PowerShell product** This comes in two variants: PowerShell on Windows, and PowerShell Core on macOS and Linux.</span></span>
- <span data-ttu-id="79219-108">**Azure PowerShell 모듈** PowerShell에 Azure 특정 명령을 추가하려면 이 추가 모듈을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-108">**The Azure PowerShell module** This extra module must be installed to add the Azure-specific commands to PowerShell.</span></span>

> [!TIP]
> <span data-ttu-id="79219-109">PowerShell은 Windows에 포함되지만 업데이트가 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79219-109">PowerShell is included with Windows (but might have an update available).</span></span> <span data-ttu-id="79219-110">Linux 및 macOS에 PowerShell Core를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-110">You will need to install PowerShell Core on Linux and macOS.</span></span>

<span data-ttu-id="79219-111">기본 제품이 설치되면 설치에 Azure PowerShell 모듈을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-111">Once the base product is installed, you then add the Azure PowerShell module to your installation.</span></span>

## <a name="how-to-install-powershell-core"></a><span data-ttu-id="79219-112">PowerShell Core를 설치하는 방법</span><span class="sxs-lookup"><span data-stu-id="79219-112">How to install PowerShell Core</span></span>
<span data-ttu-id="79219-113">Linux 및 macOS에서는 둘 다 패키지 관리자를 사용하여 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-113">On both Linux and macOS, you use a package manager to install PowerShell Core.</span></span> <span data-ttu-id="79219-114">권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="79219-114">The recommended package manager differs by OS and distribution.</span></span>

> [!NOTE]
> <span data-ttu-id="79219-115">PowerShell Core는 Microsoft 리포지토리에서 사용할 수 있으므로 먼저 패키지 관리자에 해당 리포지토리를 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-115">PowerShell Core is available in the Microsoft repository, so you'll first need to add that repository to your package manager.</span></span>

### <a name="linux"></a><span data-ttu-id="79219-116">Linux</span><span class="sxs-lookup"><span data-stu-id="79219-116">Linux</span></span>
<span data-ttu-id="79219-117">Linux에서 패키지 관리자는 선택한 Linux 배포에 따라 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="79219-117">On Linux, the package manager will change based on the Linux distribution you choose.</span></span>

| <span data-ttu-id="79219-118">배포</span><span class="sxs-lookup"><span data-stu-id="79219-118">Distribution(s)</span></span>  | <span data-ttu-id="79219-119">패키지 관리자</span><span class="sxs-lookup"><span data-stu-id="79219-119">Package manager</span></span> |
|------------------|-----------------|
| <span data-ttu-id="79219-120">Ubuntu, Debian</span><span class="sxs-lookup"><span data-stu-id="79219-120">Ubuntu, Debian</span></span>   | `apt-get`       |
| <span data-ttu-id="79219-121">Red Hat, CentOS</span><span class="sxs-lookup"><span data-stu-id="79219-121">Red Hat, CentOS</span></span>  | `yum`           |
| <span data-ttu-id="79219-122">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="79219-122">OpenSUSE</span></span>         | `zypper`        |
| <span data-ttu-id="79219-123">Fedora</span><span class="sxs-lookup"><span data-stu-id="79219-123">Fedora</span></span>           | `dnf`           |

### <a name="mac"></a><span data-ttu-id="79219-124">Mac</span><span class="sxs-lookup"><span data-stu-id="79219-124">Mac</span></span>
<span data-ttu-id="79219-125">macOS에서는 `Homebrew`를 사용하여 PowerShell Core를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-125">On macOS, you will use `Homebrew` to install PowerShell Core.</span></span>

## <a name="summary"></a><span data-ttu-id="79219-126">요약</span><span class="sxs-lookup"><span data-stu-id="79219-126">Summary</span></span>
<span data-ttu-id="79219-127">Windows에서는 PowerShell이 기본 제공되지만 Azure PowerShell 모듈을 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-127">On Windows, PowerShell is built-in, but you must install the Azure PowerShell module.</span></span> <span data-ttu-id="79219-128">Linux 및 macOS에서는 PowerShell Core 및 Azure PowerShell 모듈을 둘 다 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-128">On Linux and macOS, you must install both PowerShell Core and the Azure PowerShell module.</span></span> <span data-ttu-id="79219-129">다음 섹션에서는 몇 가지 일반적인 플랫폼에 대한 자세한 설치 단계를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="79219-129">In the next section, you will go through the detailed installation steps for some common platforms.</span></span>