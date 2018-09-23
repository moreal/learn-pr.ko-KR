<span data-ttu-id="c7372-101">PowerShell을 사용하면 명령을 작성하고 즉시 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-101">PowerShell lets you write commands and execute them immediately.</span></span> <span data-ttu-id="c7372-102">이를 **대화형 모드**라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-102">This is known as **interactive mode**.</span></span>

<span data-ttu-id="c7372-103">CRM(고객 관계 관리) 예제의 전반적인 목표는 VM을 포함하는 세 개의 테스트 환경을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-103">Recall that the overall goal in the Customer Relationship Management (CRM) example is to create three test environments containing VMs.</span></span> <span data-ttu-id="c7372-104">리소스 그룹을 사용하여 VM이 유닛 테스트용, 통합 테스트용, 수용 테스트용 개별 환경으로 구성되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-104">You will use resource groups to ensure the VMs are organized into separate environments: one for unit testing, one for integration testing, and one for acceptance testing.</span></span> <span data-ttu-id="c7372-105">리소스 그룹을 한 번만 만들기만 하면 되기 때문에 PowerShell의 대화형 모드를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-105">You only need to create the resource groups once, which means using the interactive mode of PowerShell is a good choice.</span></span>

<span data-ttu-id="c7372-106">PowerShell 명령을 입력하면 요청한 작업을 수행하는 _cmdlet_에 일치시킵니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-106">When you type a command into PowerShell, it matches it to a _cmdlet_ which then performs the requested action.</span></span> <span data-ttu-id="c7372-107">사용할 수 있는 일부 공통 명령을 찾아본 다음, PowerShell에 Azure 지원을 설치하는 방법을 확인하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-107">We're going to look at some of the common commands you can use, and then look at installing the Azure support for PowerShell.</span></span>

## <a name="what-are-powershell-cmdlets"></a><span data-ttu-id="c7372-108">PowerShell cmdlet이란?</span><span class="sxs-lookup"><span data-stu-id="c7372-108">What are PowerShell cmdlets?</span></span>
<span data-ttu-id="c7372-109">PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-109">A PowerShell command is called a **cmdlet** (pronounced "command-let").</span></span> <span data-ttu-id="c7372-110">cmdlet은 단일 기능을 조작하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-110">A cmdlet is a command that manipulates a single feature.</span></span> <span data-ttu-id="c7372-111">**cmdlet**이란 용어는 “작은 명령”을 의미하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-111">The term **cmdlet** is intended to imply "small command".</span></span> <span data-ttu-id="c7372-112">규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-112">By convention, cmdlet authors are encouraged to keep cmdlets simple and single-purpose.</span></span>

<span data-ttu-id="c7372-113">기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-113">The base PowerShell product ships with cmdlets that work with features such as sessions and background jobs.</span></span> <span data-ttu-id="c7372-114">PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-114">You add modules to your PowerShell installation to get cmdlets that manipulate other features.</span></span> <span data-ttu-id="c7372-115">예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-115">For example, there are third-party modules to work with ftp, administer your operating system, access the file system, and so on.</span></span>

<span data-ttu-id="c7372-116">cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-116">Cmdlets follow a verb-noun naming convention; for example, **Get-Process**, **Format-Table**, and **Start-Service**.</span></span> <span data-ttu-id="c7372-117">동사 선택 규칙도 있습니다. “get”은 데이터를 검색하고, “set”은 데이터를 삽입하거나 업데이트하고, “format”은 데이터 서식을 지정하고, “out”은 출력을 대상으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-117">There is also a convention for verb choice: "get" to retrieve data, "set" to insert or update data, "format" to format data, "out" to direct output to a destination, and so on.</span></span>

<span data-ttu-id="c7372-118">cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-118">Cmdlet authors are encouraged to include a help file for each cmdlet.</span></span> <span data-ttu-id="c7372-119">**Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-119">The **Get-Help** cmdlet displays the help file for any cmdlet.</span></span> <span data-ttu-id="c7372-120">예를 들어 다음 명령문을 사용하여 `Get-ChildItem` cmdlet에 대한 도움말을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-120">For example, we could get help on the `Get-ChildItem` cmdlet with the following statement:</span></span>

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a><span data-ttu-id="c7372-121">PowerShell 모듈이란?</span><span class="sxs-lookup"><span data-stu-id="c7372-121">What is a PowerShell module?</span></span>

<span data-ttu-id="c7372-122">Cmdlet은 _모듈_에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-122">Cmdlets are shipped in _modules_.</span></span> <span data-ttu-id="c7372-123">PowerShell 모듈은 사용할 수 있는 각 cmdlet을 처리하는 코드를 포함하는 DLL입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-123">A PowerShell Module is a DLL that includes the code to proces each available cmdlet.</span></span> <span data-ttu-id="c7372-124">포함된 모듈을 로드하여 PowerShell에 cmdlet을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-124">You load cmdlets into PowerShell by loading the module they are contained in.</span></span> <span data-ttu-id="c7372-125">`Get-Module` 명령을 사용하여 로드된 모듈 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-125">You can get a list of loaded modules using the `Get-Module` command:</span></span>

```powershell
Get-Module
```

<span data-ttu-id="c7372-126">그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-126">This will output something like:</span></span>

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-azurerm"></a><span data-ttu-id="c7372-127">AzureRM이란?</span><span class="sxs-lookup"><span data-stu-id="c7372-127">What is AzureRM?</span></span>
<span data-ttu-id="c7372-128">**AzureRM**은 Azure 기능을 사용하는 cmdlet이 포함된 Azure PowerShell 모듈의 정식 이름입니다(이름에 포함된 **RM**은 **리소스 관리자**를 나타냄).</span><span class="sxs-lookup"><span data-stu-id="c7372-128">**AzureRM** is the formal name for the Azure PowerShell module containing cmdlets to work with Azure features (the **RM** in the name stands for **Resource Manager**).</span></span> <span data-ttu-id="c7372-129">여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-129">It contains hundreds of cmdlets that let you control nearly every aspect of every Azure resource.</span></span> <span data-ttu-id="c7372-130">리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-130">You can work with resource groups, storage, virtual machines, Azure Active Directory, containers, machine learning, and so on.</span></span> <span data-ttu-id="c7372-131">이 모듈은 [GitHub에서 사용할 수 있는](https://github.com/Azure/azure-powershell) 오픈 소스 구성 요소입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-131">This module is an open source component [available on GitHub](https://github.com/Azure/azure-powershell).</span></span>

> [!NOTE]
> <span data-ttu-id="c7372-132">Azure PowerShell 모듈은 선택적 설치입니다. cmdlet은 모듈을 가져올 때까지 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-132">The Azure PowerShell module is an optional install - the cmdlets aren't available until you import the module.</span></span>

### <a name="install-the-azurerm-module"></a><span data-ttu-id="c7372-133">AzureRM 모듈 설치</span><span class="sxs-lookup"><span data-stu-id="c7372-133">Install the AzureRM module</span></span>

<span data-ttu-id="c7372-134">AzureRM 모듈은 PowerShell 갤러리라는 글로벌 리포지토리에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-134">The AzureRM module is available from a global repository called the PowerShell Gallery.</span></span> <span data-ttu-id="c7372-135">`Install-Module` 명령을 통해 로컬 머신에 모듈을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-135">You can install the module onto your local machine through the `Install-Module` command.</span></span> <span data-ttu-id="c7372-136">PowerShell 갤러리에서 모듈을 설치하려면 관리자 권한의 PowerShell 쉘이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-136">You need an elevated PowerShell shell to install modules from the PowerShell Gallery.</span></span> 

<span data-ttu-id="c7372-137">::: zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="c7372-137">::: zone pivot="windows"</span></span>

<span data-ttu-id="c7372-138">Azure PowerShell 모듈을 설치하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-138">To install the latest Azure PowerShell module, run the following commands:</span></span>

1. <span data-ttu-id="c7372-139">**시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-139">Open the **Start** menu and type **Windows PowerShell**.</span></span>

1. <span data-ttu-id="c7372-140">**Windows PowerShell** 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-140">Right-click the **Windows PowerShell** icon and select **Run as administrator**.</span></span>

1. <span data-ttu-id="c7372-141">**사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-141">In the **User Account Control** dialog, select **Yes**.</span></span>

1. <span data-ttu-id="c7372-142">다음 명령을 입력한 다음, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-142">Type the following command, and then press Enter:</span></span>

    ```powershell
    Install-Module -Name AzureRM
    ```

<span data-ttu-id="c7372-143">그러면 기본적으로 모든 사용자에 대해 모듈을 설치합니다(범위 매개 변수에 의해 제어됨).</span><span class="sxs-lookup"><span data-stu-id="c7372-143">This installs the module for all users by default (controlled by the scope parameter).</span></span> 

<span data-ttu-id="c7372-144">명령은 NuGet을 사용하여 구성 요소를 검색합니다. 설치한 NuGet 버전에 따라 최신 버전의 NuGet을 다운로드하여 설치하라는 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-144">The command relies on NuGet to retrieve components, depending on the version of NuGet you have installed you might get a prompt to download and install the latest version of NuGet.</span></span>

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

<span data-ttu-id="c7372-145">기본적으로 PowerShell 갤러리는 PowerShellGet에 대해 신뢰할 수 있는 리포지토리로 구성되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-145">By default, the PowerShell gallery isn't configured as a trusted repository for PowerShellGet.</span></span> <span data-ttu-id="c7372-146">PSGallery를 처음 사용할 때는 다음과 같은 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-146">The first time you use the PSGallery you see the following prompt:</span></span>

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a><span data-ttu-id="c7372-147">스크립트 실행 실패</span><span class="sxs-lookup"><span data-stu-id="c7372-147">Script execution failed</span></span>
<span data-ttu-id="c7372-148">보안 구성에 따라 `Import-Module`은 다음과 같이 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-148">Depending on your security configuration, `Import-Module` might fail with something like the following.</span></span>

```output
import-module : File C:\Program Files (x86)\WindowsPowerShell\Modules\azurerm\6.8.1\AzureRM.psm1 cannot be loaded
because running scripts is disabled on this system. For more information, see about_Execution_Policies at
https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ import-module azurerm
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [Import-Module], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand
```

<span data-ttu-id="c7372-149">일반적으로 실행 정책이 "restricted"되었음을 나타냅니다. 즉, PowerShell 갤러리를 비롯한 외부 원본에서 다운로드하는 모듈을 실행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-149">This normally indicates that the execution policy is "restricted", meaning you can't execute modules you download from an external source - including the PowerShell gallery.</span></span> <span data-ttu-id="c7372-150">`Get-ExecutionPolicy` 명령을 실행하여 대/소문자인지 여부를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-150">You can check whether this is the case by executing the command `Get-ExecutionPolicy`.</span></span> <span data-ttu-id="c7372-151">"Restricted"를 반환하는 경우 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-151">If it returns "Restricted", then do the following:</span></span>

1. <span data-ttu-id="c7372-152">관리자 권한으로 PowerShell 명령 프롬프트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-152">Open an elevated PowerShell command prompt.</span></span>
1. <span data-ttu-id="c7372-153">`SetExecutionPolicy` cmdlet을 사용하여 정책을 "RemoteSigned"로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-153">Use the `SetExecutionPolicy` cmdlet to change the policy to "RemoteSigned":</span></span>

```powershell
Set-ExecutionPolicy RemoteSigned
```

<span data-ttu-id="c7372-154">그러면 사용 권한을 묻는 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-154">This will prompt you for permission:</span></span>

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

<span data-ttu-id="c7372-155">`Import-Module`을 사용하여 cmdlet을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-155">You should then be able to use `Import-Module` to load the cmdlets.</span></span>

<span data-ttu-id="c7372-156">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-156">:::zone-end</span></span>

<span data-ttu-id="c7372-157">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="c7372-157">::: zone pivot="linux,macos"</span></span>

<span data-ttu-id="c7372-158">동일한 명령을 사용하여 Linux 또는 macOS에 Azure PowerShell을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-158">We use the same commands to install the Azure PowerShell on either Linux or macOS.</span></span>

1. <span data-ttu-id="c7372-159">터미널에서 관리자 권한으로 PowerShell Core를 시작하려면 다음 명령을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-159">In a terminal, type the following command to launch PowerShell Core with elevated privileges.</span></span>

    ```bash
    sudo pwsh
    ```

1. <span data-ttu-id="c7372-160">Azure PowerShell을 설치하려면 PowerShell Core 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-160">Run the following command at the PowerShell Core prompt to install Azure PowerShell.</span></span>

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. <span data-ttu-id="c7372-161">**PSGallery**의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-161">If you are asked whether you trust modules from **PSGallery**, answer **Yes** or **Yes to All**.</span></span>

<span data-ttu-id="c7372-162">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-162">:::zone-end</span></span>

### <a name="update-a-module"></a><span data-ttu-id="c7372-163">모듈 업데이트</span><span class="sxs-lookup"><span data-stu-id="c7372-163">Update a module</span></span>

<span data-ttu-id="c7372-164">Azure PowerShell 모듈 버전이 이미 설치되어 있음을 나타내는 경고 또는 오류 메시지가 표시되면 다음 명령을 실행하여 _최신_ 버전으로 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-164">If you get a warning or error message indicating that a version of the Azure PowerShell module is already installed, you can update to the _latest_ version by issuing the command:</span></span>

<span data-ttu-id="c7372-165">:::zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="c7372-165">:::zone pivot="windows"</span></span>

```powershell
Update-Module -Name AzureRM
```

<span data-ttu-id="c7372-166">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-166">:::zone-end</span></span>

<span data-ttu-id="c7372-167">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="c7372-167">::: zone pivot="linux,macos"</span></span>

```powershell
Update-Module -Name AzureRM.NetCore
```

<span data-ttu-id="c7372-168">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-168">:::zone-end</span></span>

<span data-ttu-id="c7372-169">`Install-Module` 명령과 마찬가지로, 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-169">As with the `Install-Module` command, answer **Yes** or **Yes to All** when prompted to trust the module.</span></span> <span data-ttu-id="c7372-170">`Update-Module` 명령을 사용하여 이 문제가 발생하는 경우 모듈을 다시 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-170">You can also use the `Update-Module` command to re-install a module if you are having trouble with it.</span></span>

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a><span data-ttu-id="c7372-171">예제: Azure PowerShell을 사용하여 리소스 그룹을 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="c7372-171">Example: How to create a resource group with Azure PowerShell</span></span>
<span data-ttu-id="c7372-172">Azure 모듈을 로드하면 Azure로 작업을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-172">Once you have the Azure module loaded, you can begin working with Azure.</span></span> <span data-ttu-id="c7372-173">일반 작업을 수행하겠습니다. 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-173">Let's do a common task - create a Resource Group.</span></span> <span data-ttu-id="c7372-174">알아본 대로 리소스 그룹을 사용하여 관련된 리소스를 함께 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-174">As you know, we use resource groups to administer related resources together.</span></span> <span data-ttu-id="c7372-175">새 리소스 그룹을 만드는 것은 새 Azure 솔루션을 시작할 때 수행할 첫 번째 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-175">Creating a new resource group is one of the first tasks you'll do when starting a new Azure solution.</span></span>

<span data-ttu-id="c7372-176">네 단계를 수행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-176">There are four steps we need to perform:</span></span>

1. <span data-ttu-id="c7372-177">Azure cmdlet을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-177">Import the Azure cmdlets.</span></span>

1. <span data-ttu-id="c7372-178">Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-178">Connect to your Azure subscription.</span></span>

1. <span data-ttu-id="c7372-179">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-179">Create the resource group.</span></span>

1. <span data-ttu-id="c7372-180">생성이 성공했는지 확인합니다(아래 참조).</span><span class="sxs-lookup"><span data-stu-id="c7372-180">Verify that creation was successful (see below).</span></span>

<span data-ttu-id="c7372-181">다음 그림은 이러한 단계의 개요를 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-181">The following illustration shows an overview of these steps.</span></span>

![리소스 그룹을 만드는 단계를 보여주는 그림입니다.](../media/5-create-resource-overview.png)

<span data-ttu-id="c7372-183">각 단계는 다른 cmdlet에 해당합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-183">Each step corresponds to a different cmdlet.</span></span>

### <a name="import-the-azure-cmdlets"></a><span data-ttu-id="c7372-184">Azure cmdlet 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7372-184">Import the Azure cmdlets</span></span>
<span data-ttu-id="c7372-185">시작 시 PowerShell은 기본적으로 핵심 cmdlet만 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-185">At startup, PowerShell loads only the core cmdlets by default.</span></span> <span data-ttu-id="c7372-186">따라서 Azure에서 작업해야 하는 cmdlet은 로드되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-186">This means the cmdlets you need to work with Azure won't be loaded.</span></span> <span data-ttu-id="c7372-187">필요한 cmdlet을 로드하는 가장 신뢰할 수 있는 방법은 PowerShell 세션을 시작할 때 수동으로 가져오는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-187">The most reliable way to load the cmdlets you need is to import them manually at the start of your PowerShell session.</span></span>

<span data-ttu-id="c7372-188">**Import-Module** cmdlet을 사용하여 모듈을 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-188">You use the **Import-Module** cmdlet to load modules.</span></span> <span data-ttu-id="c7372-189">이 cmdlet에는 다양한 상황을 처리하는 많은 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-189">This cmdlet has many parameters to handle a variety of situations.</span></span> <span data-ttu-id="c7372-190">예를 들어 여러 모듈, 특정 모듈 버전, 모듈의 일부 등을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-190">For example, it can load multiple modules, a specific module version, part of a module, and so on.</span></span>

<span data-ttu-id="c7372-191">예를 들어, **관리자 권한의 PowerShell 세션에서** 다음 명령을 사용하여 AzureRM에 대한 모든 cmdlet을 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-191">For example, we can load all the cmdlets for AzureRM with the following command **in an elevated PowerShell session**:</span></span>

<span data-ttu-id="c7372-192">:::zone pivot="windows"</span><span class="sxs-lookup"><span data-stu-id="c7372-192">:::zone pivot="windows"</span></span>

```powershell
Import-Module AzureRM
```

<span data-ttu-id="c7372-193">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-193">:::zone-end</span></span>

<span data-ttu-id="c7372-194">::: zone pivot="linux,macos"</span><span class="sxs-lookup"><span data-stu-id="c7372-194">::: zone pivot="linux,macos"</span></span>

```powershell
Import-Module AzureRM.NetCore
```

<span data-ttu-id="c7372-195">:::zone-end</span><span class="sxs-lookup"><span data-stu-id="c7372-195">:::zone-end</span></span>

> [!TIP]
> <span data-ttu-id="c7372-196">Azure PowerShell을 자주 사용하는 경우 모듈 로드 프로세스를 자동화하는 두 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-196">If you find that you work with Azure PowerShell frequently, there are two ways you can automate the module-loading process.</span></span> <span data-ttu-id="c7372-197">PowerShell 프로필에 항목을 추가하여 시작 시 Azure 모듈을 가져오거나, cmdlet을 사용할 때 자동으로 포함된 모듈을 로드하는 최신 버전의 PowerShell을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-197">You can add an entry to your PowerShell profile to import the Azure module at startup or use the latest versions of PowerShell, which loads the containing module automatically when you use a cmdlet.</span></span>

### <a name="connect"></a><span data-ttu-id="c7372-198">연결</span><span class="sxs-lookup"><span data-stu-id="c7372-198">Connect</span></span>
<span data-ttu-id="c7372-199">Azure PowerShell의 로컬 설치를 사용하는 경우 Azure 명령을 실행하기 전에 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-199">When you are working with a local install of Azure PowerShell, you will need to authenticate before you can execute Azure commands.</span></span> <span data-ttu-id="c7372-200">**Connect-AzureRmAccount** cmdlet은 Azure 자격 증명을 묻는 메시지를 표시한 다음, Azure 구독에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-200">The **Connect-AzureRmAccount** cmdlet prompts for your Azure credentials and then connects to your Azure subscription.</span></span> <span data-ttu-id="c7372-201">여기에는 많은 선택적 매개 변수가 있지만, 대화형 프롬프트만 필요한 경우에는 매개 변수가 필요하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-201">It has many optional parameters, but if all you need is an interactive prompt, no parameters are needed:</span></span>

```powershell
Connect-AzureRmAccount
```

<span data-ttu-id="c7372-202">이 모듈이 핵심 집합의 일부가 아니므로 모든 새 PowerShell 세션에 대해 이러한 단계를 반복해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-202">You'll need to repeat these steps for every new PowerShell session you start since this module is not part of the core set.</span></span>


### <a name="working-with-subscriptions"></a><span data-ttu-id="c7372-203">구독 작업</span><span class="sxs-lookup"><span data-stu-id="c7372-203">Working with subscriptions</span></span>
<span data-ttu-id="c7372-204">Azure를 처음 접하는 경우 아마도 단일 구독만 보유할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-204">If you are new to Azure, you probably only have a single subscription.</span></span> <span data-ttu-id="c7372-205">하지만 한동안 Azure를 사용한 경우 Azure 구독을 여러 개 만들었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-205">But if you have been using Azure for a while, you may have created multiple Azure subscriptions.</span></span> <span data-ttu-id="c7372-206">특정 구독에 대해 명령을 실행하도록 Azure PowerShell을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-206">You can configure Azure PowerShell to execute commands against a particular subscription.</span></span>

<span data-ttu-id="c7372-207">한 번에 하나의 구독에서만 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-207">You can only be in one subscription at a time.</span></span> <span data-ttu-id="c7372-208">`Get-AzureRmContext` cmdlet을 사용하여 활성 구독을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-208">Use the `Get-AzureRmContext` cmdlet to determine which subscription is active.</span></span> <span data-ttu-id="c7372-209">이 올바른 구독이 아닌 경우 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-209">If it's not the correct one, you can change it.</span></span>

1. <span data-ttu-id="c7372-210">`Get-AzureRmSubscription` 명령을 사용하여 계정에 모든 구독 이름 목록을 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-210">Get a list of all subscription names in your account with the `Get-AzureRmSubscription` command.</span></span> 

2. <span data-ttu-id="c7372-211">선택한 구독 이름을 전달하여 구독을 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-211">Change the subscription by passing the name of the one to select.</span></span>

```powershell
Select-AzureRmSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a><span data-ttu-id="c7372-212">모든 리소스 그룹 목록 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7372-212">Get a list of all Resource Groups</span></span>

<span data-ttu-id="c7372-213">활성 구독에서 모든 리소스 그룹 목록을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-213">You can retrieve a list of all Resource Groups in the active subscription:</span></span>

```powershell
Get-AzureRmResourceGroup
```

<span data-ttu-id="c7372-214">보다 간결하게 표시하려면 파이프 '|'를 사용하여 `Get-AzureRmResourceGroup`의 출력을 `Format-Table` cmdlet으로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-214">To get a more concise view, you can send the output from the `Get-AzureRmResourceGroup` to the `Format-Table` cmdlet using a pipe '|'.</span></span>

```powershell
Get-AzureRmResourceGroup | Format-Table
```

<span data-ttu-id="c7372-215">그러면 다음과 같이 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-215">This will output something like:</span></span>

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a><span data-ttu-id="c7372-216">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c7372-216">Create a Resource Group</span></span>

<span data-ttu-id="c7372-217">알아본 대로 Azure에서 리소스를 만드는 경우 항상 관리 목적을 위해 리소스 그룹에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-217">As you know, when you are creating resources in Azure, you will always place them into a resource group for management purposes.</span></span> <span data-ttu-id="c7372-218">리소스 그룹은 새 응용 프로그램을 시작할 때 만들 첫 번째 작업 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-218">A resource group is often one of the first things you will create when starting a new application.</span></span>

<span data-ttu-id="c7372-219">`New-AzureRmResourceGroup` cmdlet을 사용하여 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-219">You can create resource groups with the `New-AzureRmResourceGroup` cmdlet.</span></span> <span data-ttu-id="c7372-220">이름 및 위치를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-220">You must specify a name and location.</span></span> <span data-ttu-id="c7372-221">이름은 구독 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-221">The name must be unique within your subscription.</span></span> <span data-ttu-id="c7372-222">위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다(규정 준수에 중요할 수 있음).</span><span class="sxs-lookup"><span data-stu-id="c7372-222">The location determines where the metadata for your resource group will be stored (which may be important to you for compliance reasons).</span></span> <span data-ttu-id="c7372-223">"미국 서부", "북유럽" 또는 "인도 서부"와 같은 문자열을 사용하여 위치를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-223">You use strings like "West US", "North Europe", or "West India" to specify the location.</span></span> <span data-ttu-id="c7372-224">대부분의 Azure cmdlet과 마찬가지로 `New-AzureRmResourceGroup`에는 많은 선택적 매개 변수가 있지만 핵심 구문은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-224">As with most of the Azure cmdlets, `New-AzureRmResourceGroup` has many optional parameters; however, the core syntax is:</span></span>

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> <span data-ttu-id="c7372-225">Azure 샌드박스에서 사용할 예정이며 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-225">Remember, we will be working in the Azure Sandbox which creates the Resource Group for you.</span></span> <span data-ttu-id="c7372-226">위의 명령은 고유한 구독에서 작업하는 경우에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-226">The above command would be used if you work in your own subscription.</span></span>

### <a name="verify-the-resources"></a><span data-ttu-id="c7372-227">리소스 확인</span><span class="sxs-lookup"><span data-stu-id="c7372-227">Verify the resources</span></span>
<span data-ttu-id="c7372-228">`Get-AzureRmResource`는 Azure 리소스를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-228">The `Get-AzureRmResource` lists your Azure resources.</span></span> <span data-ttu-id="c7372-229">이 cmdlet은 리소스 그룹 생성에 성공했는지 여부를 확인하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-229">This is useful here to verify whether creation of the resource group was successful.</span></span>

```powershell
Get-AzureRmResource
```

<span data-ttu-id="c7372-230">`Get-AzureRmResourceGroup` 명령과 같이 `Format-Table` cmdlet을 통해 좀 더 간략히 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-230">Like the `Get-AzureRmResourceGroup` command, you can get a more concise view through the `Format-Table` cmdlet.</span></span> <span data-ttu-id="c7372-231">여기에서는 약식 버전 `ft`을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-231">Here we will use a shorthand version `ft`:</span></span>

```powershell
Get-AzureRmResource | ft
```

<span data-ttu-id="c7372-232">특정 리소스 그룹으로 필터링하여 그룹과 연결된 리소스만 나열할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-232">You can also filter it to specific resource groups to only list resources associated with that group:</span></span>

```powershell
Get-AzureRmResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a><span data-ttu-id="c7372-233">Azure Virtual Machine 만들기</span><span class="sxs-lookup"><span data-stu-id="c7372-233">Creating an Azure Virtual Machine</span></span>

<span data-ttu-id="c7372-234">PowerShell을 사용하여 수행할 수 있는 일반적인 작업은 다른 VM을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-234">Another common task that could be done with PowerShell is to create VMs.</span></span>

<span data-ttu-id="c7372-235">Azure PowerShell은 가상 머신을 만드는 `New-AzureRmVm` cmdlet을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-235">Azure PowerShell provides the `New-AzureRmVm` cmdlet to create a virtual machine.</span></span> <span data-ttu-id="c7372-236">이 cmdlet에는 많은 VM 구성 설정을 처리할 수 있는 여러 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-236">The cmdlet has many parameters to let it handle the large number of VM configuration settings.</span></span> <span data-ttu-id="c7372-237">대부분의 매개 변수에 적절한 기본값이 있으므로 다음 5개 매개 변수만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-237">Most of the parameters have reasonable default values so we only need to specify five things:</span></span>

- <span data-ttu-id="c7372-238">**ResourceGroupName**: 새 VM이 배치될 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-238">**ResourceGroupName**: The resource group into which the new VM will be placed.</span></span>
- <span data-ttu-id="c7372-239">**Name**: Azure의 VM 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-239">**Name**: The name of the VM in Azure.</span></span>
- <span data-ttu-id="c7372-240">**Location**: VM이 프로비전될 지리적 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-240">**Location**: Geographic location where the VM will be provisioned.</span></span>
- <span data-ttu-id="c7372-241">**Credential**: VM 관리자 계정의 사용자 이름과 암호를 포함하는 개체입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-241">**Credential**: An object containing the username and password for the VM admin account.</span></span> <span data-ttu-id="c7372-242">`Get-Credential` cmdlet을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-242">We will use the `Get-Credential` cmdlet.</span></span> <span data-ttu-id="c7372-243">이 cmdlet은 사용자 이름 및 암호를 묻는 메시지를 표시하고 자격 증명 개체에 패키지합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-243">This cmdlet will prompt for a username and password and package it into a credential object.</span></span>
- <span data-ttu-id="c7372-244">**Image**: VM에 사용할 운영 체제 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-244">**Image**: The operating system image to use for the VM.</span></span> <span data-ttu-id="c7372-245">Linux 배포 또는 Windows Server인 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-245">This is often a Linux distribution, or Windows Server.</span></span>

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

<span data-ttu-id="c7372-246">위에 표시된 대로 이러한 매개 변수를 cmdlet에 직접 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-246">You can supply these parameters directly to the cmdlet as shown above.</span></span> <span data-ttu-id="c7372-247">또는 `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface` 및 `Set-AzureRmVMOSDisk`와 같은 가상 머신을 구성하는 데 다른 cmdlet를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-247">Alternatively, other cmdlets can be used to configure the virtual machine, such as `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface`, and `Set-AzureRmVMOSDisk`.</span></span>

<span data-ttu-id="c7372-248">`-Credential` 매개 변수와 함께 `Get-Credential` cmdlet을 이어 놓은 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-248">Here's an example that strings the `Get-Credential` cmdlet together with the `-Credential` parameter:</span></span>

```powershell
New-AzureRmVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

<span data-ttu-id="c7372-249">`AzureRmVM` 접미사는 PowerShell의 VM 기반 명령에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-249">The `AzureRmVM` suffix is specific to VM-based commands in PowerShell.</span></span> <span data-ttu-id="c7372-250">사용할 수 있는 다른 방법은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-250">There are several others you can use:</span></span>

| <span data-ttu-id="c7372-251">명령</span><span class="sxs-lookup"><span data-stu-id="c7372-251">Command</span></span> | <span data-ttu-id="c7372-252">설명</span><span class="sxs-lookup"><span data-stu-id="c7372-252">Description</span></span> |
|---------|-------------|
| `Remove-AzureRmVM` | <span data-ttu-id="c7372-253">Azure VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-253">Deletes an Azure VM.</span></span> |
| `Start-AzureRmVM` | <span data-ttu-id="c7372-254">중지된 VM을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-254">Start a stopped VM.</span></span> |
| `Stop-AzureRmVM` | <span data-ttu-id="c7372-255">실행 중인 VM을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-255">Stop a running VM.</span></span> |
| `Restart-AzureRmVM` | <span data-ttu-id="c7372-256">VM을 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-256">Restart a VM.</span></span> |
| `Update-AzureRmVM` | <span data-ttu-id="c7372-257">VM에 대한 구성을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-257">Updates the configuration for a VM.</span></span> |

#### <a name="example-getting-the-information-for-a-vm"></a><span data-ttu-id="c7372-258">예제: VM에 대한 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c7372-258">Example: getting the information for a VM</span></span>

<span data-ttu-id="c7372-259">`Get-AzureRmVM -Status` 명령을 사용하여 구독에서 VM을 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-259">You can list the VMs in your subscription with the `Get-AzureRmVM -Status` command.</span></span> <span data-ttu-id="c7372-260">`-Name` 속성을 사용하여 VM을 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-260">This can also specify a VM with the `-Name` property.</span></span> <span data-ttu-id="c7372-261">여기에서는 PowerShell 변수에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-261">Here we assign it to a PowerShell variable:</span></span>

```powershell
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName ExerciseResources
```

<span data-ttu-id="c7372-262">흥미로운 것은 상호 작용할 수 있는 _개체_라는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-262">The interesting thing is this is an _object_ you can interact with.</span></span> <span data-ttu-id="c7372-263">예를 들어, 해당 개체를 사용하고, 변경한 다음, `Update-AzureRmVM` 명령을 사용하여 Azure에 변경 내용을 다시 푸시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-263">For example, you can take that object, make changes and then push changes back to Azure with the `Update-AzureRmVM` command:</span></span>

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzureRmVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

<span data-ttu-id="c7372-264">PowerShell의 대화형 모드는 일회성 작업에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-264">PowerShell's interactive mode is appropriate for one-off tasks.</span></span> <span data-ttu-id="c7372-265">예제에서는 프로젝트 수명 동안 동일한 리소스 그룹을 사용할 가능성이 높으므로 대화형으로 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-265">In our example, we'll likely use the same resource group for the lifetime of the project, which means creating it interactively is reasonable.</span></span> <span data-ttu-id="c7372-266">이 작업에는 스크립트를 작성하고 해당 스크립트를 한 번만 실행하는 것보다 대화형 모드를 사용하는 것이 더 빠르고 편리한 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="c7372-266">Interactive mode is often quicker and easier for this task than writing a script and executing that script exactly once.</span></span>