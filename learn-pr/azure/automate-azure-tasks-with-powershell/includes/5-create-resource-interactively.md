<span data-ttu-id="92ab2-101">Azure PowerShell을 사용하면 명령을 작성하고 즉시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-101">Azure PowerShell lets you write commands and execute them immediately.</span></span> <span data-ttu-id="92ab2-102">이를 **대화형 모드**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-102">This is known as **interactive mode**.</span></span>

<span data-ttu-id="92ab2-103">CRM(고객 관계 관리) 예제의 전반적인 목표는 VM을 포함하는 세 개의 테스트 환경을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-103">Recall that the overall goal in the Customer Relationship Management (CRM) example is to create three test environments containing VMs.</span></span> <span data-ttu-id="92ab2-104">리소스 그룹을 사용하여 VM이 유닛 테스트용, 통합 테스트용, 수용 테스트용 개별 환경으로 구성되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-104">You will use resource groups to ensure the VMs are organized into separate environments: one for unit testing, one for integration testing, and one for acceptance testing.</span></span> <span data-ttu-id="92ab2-105">리소스 그룹을 한 번만 만들면 되기 때문에 PowerShell의 대화형 모드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-105">You only need to create the resource groups once, which means using the interactive mode of PowerShell is a good choice.</span></span>

<span data-ttu-id="92ab2-106">이 섹션에서는 PowerShell을 대화형으로 사용하여 Azure 구독에 로그온하고 리소스 그룹을 만드는 방법의 몇 가지 예를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-106">This section shows some examples of using PowerShell interactively to log on to your Azure subscription and create resource groups.</span></span>

## <a name="what-are-powershell-cmdlets"></a><span data-ttu-id="92ab2-107">PowerShell cmdlet이란?</span><span class="sxs-lookup"><span data-stu-id="92ab2-107">What are PowerShell cmdlets?</span></span>
<span data-ttu-id="92ab2-108">PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-108">A PowerShell command is called a **cmdlet** (pronounced "command-let").</span></span> <span data-ttu-id="92ab2-109">cmdlet은 단일 기능을 조작하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-109">A cmdlet is a command that manipulates a single feature.</span></span> <span data-ttu-id="92ab2-110">**cmdlet**이란 용어는 “작은 명령”을 의미하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-110">The term **cmdlet** is intended to imply "small command".</span></span> <span data-ttu-id="92ab2-111">규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-111">By convention, cmdlet authors are encouraged to keep cmdlets simple and single-purpose.</span></span>

<span data-ttu-id="92ab2-112">기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-112">The base PowerShell product ships with cmdlets that work with features such as sessions and background jobs.</span></span> <span data-ttu-id="92ab2-113">PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-113">You add modules to your PowerShell installation to get cmdlets that manipulate other features.</span></span> <span data-ttu-id="92ab2-114">예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-114">For example, there are third-party modules to work with ftp, administer your operating system, access the file system, and so on.</span></span>

<span data-ttu-id="92ab2-115">cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-115">Cmdlets follow a verb-noun naming convention; for example, **Get-Process**, **Format-Table**, and **Start-Service**.</span></span> <span data-ttu-id="92ab2-116">동사 선택 규칙도 있습니다. “get”은 데이터를 검색하고, “set”은 데이터를 삽입하거나 업데이트하고, “format”은 데이터 서식을 지정하고, “out”은 출력을 대상으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-116">There is also a convention for verb choice: "get" to retrieve data, "set" to insert or update data, "format" to format data, "out" to direct output to a destination, and so on.</span></span>

<span data-ttu-id="92ab2-117">cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-117">Cmdlet authors are encouraged to include a help file for each cmdlet.</span></span> <span data-ttu-id="92ab2-118">**Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-118">The **Get-Help** cmdlet displays the help file for any cmdlet:</span></span>

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a><span data-ttu-id="92ab2-119">AzureRM이란?</span><span class="sxs-lookup"><span data-stu-id="92ab2-119">What is AzureRM?</span></span>
<span data-ttu-id="92ab2-120">**AzureRM**은 Azure 기능을 사용하는 cmdlet이 포함된 Azure PowerShell 모듈의 정식 이름입니다(이름에 포함된 **RM**은 **리소스 관리자**를 나타냄).</span><span class="sxs-lookup"><span data-stu-id="92ab2-120">**AzureRM** is the formal name for the Azure PowerShell module containing cmdlets to work with Azure features (the **RM** in the name stands for **Resource Manager**).</span></span> <span data-ttu-id="92ab2-121">여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-121">It contains hundreds of cmdlets that let you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="92ab2-122">리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-122">You can work with resource groups, storage, virtual machines, Azure Active Directory, containers, machine learning, and so on.</span></span>

## <a name="how-to-create-a-resource-group"></a><span data-ttu-id="92ab2-123">리소스 그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="92ab2-123">How to create a resource group</span></span>
<span data-ttu-id="92ab2-124">이제 Azure PowerShell의 로컬 설치를 사용하여 리소스 그룹을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-124">Next, we'll create a resource group using a local installation of Azure PowerShell.</span></span> 

<span data-ttu-id="92ab2-125">이 프로세스는 다음 4단계로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-125">There are four steps:</span></span> 
1. <span data-ttu-id="92ab2-126">Azure cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-126">Import the Azure cmdlets.</span></span>
1. <span data-ttu-id="92ab2-127">Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-127">Connect to your Azure subscription.</span></span>
1. <span data-ttu-id="92ab2-128">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-128">Create the resource group.</span></span>
1. <span data-ttu-id="92ab2-129">생성이 성공했는지 확인합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="92ab2-129">Verify that creation was successful (see below).</span></span>

![Azure PowerShell을 사용하여 Azure에서 리소스를 만드는 단계](../media/5-create-resource-overview.png)

<span data-ttu-id="92ab2-131">각 단계는 다른 cmdlet에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-131">Each step corresponds to a different cmdlet.</span></span>

### <a name="import"></a><span data-ttu-id="92ab2-132">가져오기</span><span class="sxs-lookup"><span data-stu-id="92ab2-132">Import</span></span>
<span data-ttu-id="92ab2-133">시작 시 PowerShell은 기본적으로 핵심 cmdlet만 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-133">At startup, PowerShell loads only the core cmdlets by default.</span></span> <span data-ttu-id="92ab2-134">따라서 Azure에서 작업해야 하는 cmdlet은 로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-134">This means the cmdlets you need to work with Azure won't be loaded.</span></span> <span data-ttu-id="92ab2-135">필요한 cmdlet을 로드하는 가장 신뢰할 수 있는 방법은 PowerShell 세션을 시작할 때 수동으로 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-135">The most reliable way to load the cmdlets you need is to import them manually at the start of your PowerShell session.</span></span>

<span data-ttu-id="92ab2-136">**Import-Module** cmdlet을 사용하여 모듈을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-136">You use the **Import-Module** cmdlet to load modules.</span></span> <span data-ttu-id="92ab2-137">이 cmdlet에는 다양한 상황을 처리하는 많은 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-137">This cmdlet has many parameters to handle a variety of situations.</span></span> <span data-ttu-id="92ab2-138">예를 들어 여러 모듈, 특정 모듈 버전, 모듈의 일부 등을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-138">For example, it can load multiple modules, a specific module version, part of a module, and so on.</span></span> <span data-ttu-id="92ab2-139">하나의 모듈 전체를 로드하기 위한 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-139">To load the entirety of one module, the syntax is simply:</span></span>

```powershell
Import-Module <module-name>
```

> [!TIP]
> <span data-ttu-id="92ab2-140">Azure PowerShell을 자주 사용하는 경우 모듈 로드 프로세스를 자동화하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-140">If you find that you work with Azure PowerShell frequently, there are two ways you can automate the module-loading process.</span></span> <span data-ttu-id="92ab2-141">PowerShell 프로필에 항목을 추가하여 시작 시 Azure 모듈을 가져오거나, cmdlet을 사용할 때 자동으로 포함된 모듈을 로드하는 최신 버전의 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-141">You can add an entry to your PowerShell profile to import the Azure module at startup or use the latest versions of PowerShell, which loads the containing module automatically when you use a cmdlet.</span></span>

### <a name="connect"></a><span data-ttu-id="92ab2-142">연결</span><span class="sxs-lookup"><span data-stu-id="92ab2-142">Connect</span></span>
<span data-ttu-id="92ab2-143">Azure PowerShell의 로컬 설치를 사용하므로 Azure 명령을 실행하기 전에 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-143">Since you are working with a local install of Azure PowerShell, you will need to authenticate before you can execute Azure commands.</span></span> <span data-ttu-id="92ab2-144">**Connect-AzureRmAccount** cmdlet은 Azure 자격 증명을 묻는 메시지를 표시하고 Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-144">The **Connect-AzureRmAccount** cmdlet prompts for your Azure credentials and then connects to your Azure subscription.</span></span> <span data-ttu-id="92ab2-145">여기에는 많은 선택적 매개 변수가 있지만, 대화형 프롬프트만 필요한 경우에는 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-145">It has many optional parameters, but if all you need is an interactive prompt, no parameters are needed:</span></span>

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a><span data-ttu-id="92ab2-146">생성</span><span class="sxs-lookup"><span data-stu-id="92ab2-146">Create</span></span>
<span data-ttu-id="92ab2-147">**New-AzureRmResourceGroup** cmdlet은 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-147">The **New-AzureRmResourceGroup** cmdlet creates a resource group.</span></span> <span data-ttu-id="92ab2-148">이름 및 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-148">You must specify a name and location.</span></span> <span data-ttu-id="92ab2-149">이름은 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-149">The name must be unique within your subscription.</span></span> <span data-ttu-id="92ab2-150">위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다(규정 준수에 중요할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="92ab2-150">The location determines where the metadata for your resource group will be stored (which may be important to you for compliance reasons).</span></span> <span data-ttu-id="92ab2-151">“미국 서부”, “북유럽” 또는 “인도 서부”와 같은 문자열을 사용하여 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-151">You use strings like "West US", "North Europe", or "West India" to specify the location.</span></span> <span data-ttu-id="92ab2-152">대부분의 Azure cmdlet과 마찬가지로 **New-AzureRmResourceGroup**에는 많은 선택적 매개 변수가 있지만 핵심 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-152">As with most of the Azure cmdlets, **New-AzureRmResourceGroup** has many optional parameters; however, the core syntax is:</span></span>

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a><span data-ttu-id="92ab2-153">Verify</span><span class="sxs-lookup"><span data-stu-id="92ab2-153">Verify</span></span>
<span data-ttu-id="92ab2-154">**Get-AzureRmResource**는 Azure 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-154">The **Get-AzureRmResource** lists your Azure resources.</span></span> <span data-ttu-id="92ab2-155">이 cmdlet은 리소스 그룹 생성에 성공했는지 여부를 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-155">This is useful here to verify whether creation of the resource group was successful.</span></span>

```powershell
Get-AzureRmResource
```

<span data-ttu-id="92ab2-156">보다 간결하게 표시하려면 파이프 ‘|’를 사용하여 **Get-AzureRmResource**의 출력을 **Format-Table** cmdlet으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-156">To get a more concise view, you can send the output from the **Get-AzureRmResource** to the **Format-Table** cmdlet using a pipe '|'.</span></span>

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a><span data-ttu-id="92ab2-157">요약</span><span class="sxs-lookup"><span data-stu-id="92ab2-157">Summary</span></span>
<span data-ttu-id="92ab2-158">PowerShell의 대화형 모드는 일회성 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-158">PowerShell's interactive mode is appropriate for one-off tasks.</span></span> <span data-ttu-id="92ab2-159">예제에서는 프로젝트 수명 동안 동일한 리소스 그룹을 사용하므로 대화형으로 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-159">In our example, we'll use the same resource group for the lifetime of the project, which means creating it interactively is reasonable.</span></span> <span data-ttu-id="92ab2-160">대체로, 이 작업에는 스크립트를 작성하고 해당 스크립트를 한 번만 실행하는 것보다 대화형 모드를 사용하는 것이 더 빠르고 편리합니다.</span><span class="sxs-lookup"><span data-stu-id="92ab2-160">Interactive mode is often quicker and easier for this task than writing a script and executing that script exactly once.</span></span>
