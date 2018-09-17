<span data-ttu-id="3b2c2-101">신규 스타트업 기업을 위해 재무 관리 응용 프로그램을 개발한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-101">Suppose you are developing a financial management application for new business startups.</span></span> <span data-ttu-id="3b2c2-102">모든 고객 데이터를 보호해야 하므로 이 응용 프로그램을 호스트할 서버의 모든 OS 및 데이터 디스크에서 ADE(Azure Disk Encryption)를 구현하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-102">You want to ensure that all your customers' data is secured, so you have decided to implement Azure Disk Encryption (ADE) across all OS and data disks on the servers that will host this application.</span></span> <span data-ttu-id="3b2c2-103">규정 준수 요구 사항의 일부분으로 자체 암호화 키 관리를 담당해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-103">As part of your compliance requirements, you also need to be responsible for your own encryption key management.</span></span>

<span data-ttu-id="3b2c2-104">이 단원에서는 기존 Windows VM의 디스크를 암호화하고 자체 Azure Key Vault를 사용하여 암호화 키를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-104">In this unit, you'll encrypt disks on existing Windows VMs, and manage the encryption keys using your own Azure Key Vault.</span></span>

> [!IMPORTANT] 
> <span data-ttu-id="3b2c2-105">이 연습에서는 Azure PowerShell이 컴퓨터에 설치되어 있다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-105">This exercise assumes that Azure PowerShell is installed on your computer.</span></span> <span data-ttu-id="3b2c2-106">Azure PowerShell을 설치하는 방법에 대한 정보를 보려면 [PowerShellGet으로 Windows에 Azure PowerShell 설치](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0)로 이동하세요.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-106">Go to [Install Azure PowerShell on Windows with PowerShellGet](https://docs.microsoft.com/powershell/azure/install-azurerm-ps?view=azurermps-6.7.0) for information on how to install Azure PowerShell.</span></span>

## <a name="prepare-the-environment"></a><span data-ttu-id="3b2c2-107">환경 준비</span><span class="sxs-lookup"><span data-stu-id="3b2c2-107">Prepare the environment</span></span>

<span data-ttu-id="3b2c2-108">먼저 새 리소스 그룹에 Windows VM을 배포한 다음, 해당 VM에 데이터 디스크를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-108">We'll start by deploying a Windows VM to a new resource group, and then add a data disk to the VM.</span></span>

### <a name="deploy-windows-vm-using-the-azure-portal"></a><span data-ttu-id="3b2c2-109">Azure Portal을 사용하여 Windows VM 배포</span><span class="sxs-lookup"><span data-stu-id="3b2c2-109">Deploy Windows VM using the Azure portal</span></span>

<span data-ttu-id="3b2c2-110">여기서는 Azure Portal을 사용하여 Windows VM을 만들고 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-110">Here you'll use the Azure portal to create and deploy a Windows VM.</span></span> <span data-ttu-id="3b2c2-111">먼저 기본 VM 정보부터 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-111">Start by defining the basic VM information:</span></span>

1. <span data-ttu-id="3b2c2-112">브라우저에서 [Azure Portal](http://portal.azure.com)로 이동하여 기본 자격 증명으로 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-112">In a browser, navigate to the [Azure portal](http://portal.azure.com) and sign in with your normal credentials.</span></span>

1. <span data-ttu-id="3b2c2-113">사이드바에서 **가상 머신**, **가상 머신 만들기**를 차례로 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-113">In the sidebar, click **Virtual machines**, and then click **Create virtual machine**.</span></span>

1. <span data-ttu-id="3b2c2-114">계산 블레이드의 **권장** 섹션에서 **Windows Server**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-114">On the Compute blade, in the **Recommended** section, click **Windows Server**.</span></span>

1. <span data-ttu-id="3b2c2-115">**Windows Server** 블레이드에서 **Windows Server 2016 Datacenter**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-115">In the **Windows Server** blade, click **Windows Server 2016 Datacenter**.</span></span>

1. <span data-ttu-id="3b2c2-116">**Windows Server 2016 Datacenter** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-116">In the **Windows Server 2016 Datacenter** blade, click **Create**.</span></span>

1. <span data-ttu-id="3b2c2-117">**기본 사항** 블레이드의 **이름** 상자에 **moneyappsvr01**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-117">In the **Basics** blade, in the **Name** box, type **moneyappsvr01.**</span></span>

1. <span data-ttu-id="3b2c2-118">**사용자 이름** 및 **암호** 상자에 이 서버의 관리자 계정 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-118">In the **Username** and **Password boxes**, type a name and password for an administrator account on this server.</span></span>

1. <span data-ttu-id="3b2c2-119">**구독** 상자에서 Azure 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-119">In the **Subscription** box, select your Azure subscription.</span></span>

1. <span data-ttu-id="3b2c2-120">**리소스 그룹**에서 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-120">Under **Resource Group**, select **Create new**.</span></span> <span data-ttu-id="3b2c2-121">상자에서 **moneyapprg**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-121">In the box, type **moneyapprg**.</span></span>

1. <span data-ttu-id="3b2c2-122">**위치** 드롭다운 목록에서 인근 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-122">In the **Location** drop-down list, select a region near you.</span></span>

1. <span data-ttu-id="3b2c2-123">**확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-123">Click **OK**.</span></span>

### <a name="choose-a-size-for-the-vm-and-start-the-deployment"></a><span data-ttu-id="3b2c2-124">VM의 크기를 선택하고 배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-124">Choose a size for the VM, and start the deployment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3b2c2-125">기본 계층 VM은 ADE를 지원하지 않음을 명심합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-125">Remember that basic tier VMs do not support ADE.</span></span>

1. <span data-ttu-id="3b2c2-126">**크기 선택** 블레이드에서 **표준** SKU(예: **B1s**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-126">On the **Choose a size** blade, select a **Standard** SKU, such as **B1s**.</span></span> <span data-ttu-id="3b2c2-127">그런 다음, **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-127">Then click **Select**.</span></span>

1. <span data-ttu-id="3b2c2-128">**설정** 블레이드의 **공용 인바운드 포트 선택** 목록에서 **RDP**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-128">On the **Settings** blade, in the **Select public inbound ports** list, click **RDP**.</span></span> <span data-ttu-id="3b2c2-129">그런 다음, 아래로 스크롤하여 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-129">Then scroll down and click **OK**.</span></span>

1. <span data-ttu-id="3b2c2-130">**만들기** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-130">On the **Create** blade, click **Create**.</span></span>

1. <span data-ttu-id="3b2c2-131">VM이 배포될 때까지 기다렸다가 연습을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-131">Wait until the VM has deployed before continuing with the exercise.</span></span>

### <a name="add-a-data-disk-to-the-vm"></a><span data-ttu-id="3b2c2-132">VM에 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="3b2c2-132">Add a data disk to the VM</span></span>

1. <span data-ttu-id="3b2c2-133">왼쪽 메뉴에서 **모든 리소스**를 클릭한 다음, **moneyappsvr01**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-133">In the left menu, click **All resources**, and then click **moneyappsvr01**.</span></span>

1. <span data-ttu-id="3b2c2-134">**가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-134">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="3b2c2-135">**디스크** 블레이드에서 OS 디스크 암호화 상태가 현재 **사용 안 함**인지 확인한 후에 **데이터 디스크 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-135">On the **Disks** blade, note that the OS disk encryption status is currently **Not enabled**, and then click **Add data disk**.</span></span>

1. <span data-ttu-id="3b2c2-136">**이름** 목록을 클릭하고 **디스크 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-136">Click in the **Name** list, and then click **Create disk**.</span></span>

1. <span data-ttu-id="3b2c2-137">**관리 디스크 만들기** 블레이드의 **이름** 상자에 **moneyappsvr01_data**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-137">In the **Create managed disk** blade, in the **Name** box, type **moneyappsvr01_data**.</span></span>

1. <span data-ttu-id="3b2c2-138">**리소스 그룹**에서 **기존 항목 사용**을 선택한 다음 목록에서 **moneyapprg**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-138">Under **Resource Group**, select **Use existing**, and in the list, select **moneyapprg**.</span></span>

1. <span data-ttu-id="3b2c2-139">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-139">Click **Create**.</span></span>

1. <span data-ttu-id="3b2c2-140">디스크가 만들어질 때까지 기다렸다가 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-140">Wait until the disk has been created before continuing.</span></span>

1. <span data-ttu-id="3b2c2-141">**디스크** 블레이드에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-141">On the **Disks** blade, click **Save**.</span></span> <span data-ttu-id="3b2c2-142">데이터 디스크 암호화 상태가 현재 **사용 안 함**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-142">Note that the data disk encryption status is currently **Not enabled**.</span></span>

## <a name="configure-disk-encryption-prerequisites"></a><span data-ttu-id="3b2c2-143">디스크 암호화 필수 구성 요소 구성</span><span class="sxs-lookup"><span data-stu-id="3b2c2-143">Configure disk encryption prerequisites</span></span>

<span data-ttu-id="3b2c2-144">이번에는 Azure Disk Encryption 필수 구성 요소 구성 스크립트를 사용하여 모든 디스크 암호화 필수 구성 요소를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-144">You'll now use the Azure Disk Encryption prerequisites configuration script to configure all the disk encryption prerequisites.</span></span> <span data-ttu-id="3b2c2-145">이 스크립트는 VM과 동일한 지역에 Key Vault를 만들고 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-145">This script will create and prepare a key vault in the same region as your VM.</span></span>

### <a name="prepare-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="3b2c2-146">Azure Disk Encryption 필수 구성 요소 설치 스크립트 준비</span><span class="sxs-lookup"><span data-stu-id="3b2c2-146">Prepare the Azure Disk Encryption prerequisite setup script</span></span>

1. <span data-ttu-id="3b2c2-147">[Azure Disk Encryption 필수 구성 요소 설치 스크립트](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) GitHub 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-147">Go to the [Azure Disk Encryption prerequisite setup script](https://github.com/Azure/azure-powershell/blob/master/src/ResourceManager/Compute/Commands.Compute/Extension/AzureDiskEncryption/Scripts/AzureDiskEncryptionPreRequisiteSetup.ps1) GitHub page.</span></span>

1. <span data-ttu-id="3b2c2-148">GibHub 페이지에서 **원시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-148">On the GibHub page, click **Raw**.</span></span>

1. <span data-ttu-id="3b2c2-149">Ctrl+A를 사용하여 페이지에서 모든 텍스트를 선택한 다음, Ctrl+C를 사용하여 페이지의 모든 텍스트를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-149">Use Ctrl-A to select all the text on the page, and then use Ctrl-C to copy all the text on the page to the clipboard.</span></span>

1. <span data-ttu-id="3b2c2-150">컴퓨터에서 **시작**을 클릭한 다음, **Windows PowerShell ISE**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-150">On your computer, click **Start**, and then browse to **Windows PowerShell ISE**.</span></span>

1. <span data-ttu-id="3b2c2-151">마우스 오른쪽 단추로 **Windows PowerShell ISE**를 클릭하고 **관리자 권한으로 실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-151">Right-click **Windows PowerShell ISE**, and click **Run as administrator**.</span></span>

1. <span data-ttu-id="3b2c2-152">관리자: Windows PowerShell ISE 창에서 **보기**를 클릭한 다음, **스크립트 창 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-152">In the Administrator: Windows PowerShell ISE window, click **View**, and then click **Show Script Pane**.</span></span>

1. <span data-ttu-id="3b2c2-153">스크립트 창에 복사한 텍스트를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-153">Paste the copied text into the script pane.</span></span>

1. <span data-ttu-id="3b2c2-154">스크립트 창에서 다음 코드 블록을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-154">In the script pane, locate the following block of code:</span></span>

    ```powershell
    [Parameter(Mandatory = $false,
            HelpMessage="Name of the AAD application that will be used to write secrets to KeyVault. A new application with this name will be created if one doesn't exist. If this app already exists, pass aadClientSecret parameter to the script")]
    [ValidateNotNullOrEmpty()]
    [string]$aadAppName,
    ```
1. <span data-ttu-id="3b2c2-155">코드 블록에서 `$false`를 `$true`로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-155">In the code block, change `$false` to `$true`.</span></span>

1. <span data-ttu-id="3b2c2-156">**파일**, **다른 이름으로 저장**을 차례로 클릭한 다음 스크립트를 저장하는 데 사용할 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-156">Click **File**, then click **Save As**, and navigate to the folder you'd like to use to save the script.</span></span>

1. <span data-ttu-id="3b2c2-157">**파일 이름** 상자에 **ADEPrereqScript.ps1**을 입력하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-157">In the **File name** box, type **ADEPrereqScript.ps1**, and click **Save**.</span></span>

### <a name="run-the-azure-disk-encryption-prerequisite-setup-script"></a><span data-ttu-id="3b2c2-158">Azure Disk Encryption 필수 구성 요소 설치 스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="3b2c2-158">Run the Azure Disk Encryption prerequisite setup script</span></span>

1. <span data-ttu-id="3b2c2-159">PowerShell ISE 콘솔 창에서 다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-159">In the  PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```console
   cd <path to your folder containing ADEPrereqScript.ps1>
   ```

1. <span data-ttu-id="3b2c2-160">PowerShell ISE 콘솔 창에서 다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-160">In the PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```powershell
   Set-ExecutionPolicy Unrestricted
   ```

   <span data-ttu-id="3b2c2-161">**실행 정책 변경** 대화 상자가 표시되면 **모두 예** 또는 **예**(_모두 예_ 옵션이 표시되지 않는 경우)를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-161">If you get an **Execution Policy Change** dialog box, click either **Yes to all** or **Yes** (if you do not get a _Yes to all_ option).</span></span>

1. <span data-ttu-id="3b2c2-162">PowerShell ISE 콘솔 창에서 다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-162">In the  PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

   ```powershell
   Login-AzureRmAccount
   ```

1. <span data-ttu-id="3b2c2-163">Azure 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-163">Enter your Azure credentials.</span></span>

1. <span data-ttu-id="3b2c2-164">**SubscriptionId** 문자열을 선택하여 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-164">Select your **SubscriptionId** string, and copy it to the clipboard.</span></span>

1. <span data-ttu-id="3b2c2-165">PowerShell ISE에서 **파일**를 클릭한 다음, **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-165">In the PowerShell ISE, click **File**, and then click **Run**.</span></span>

1. <span data-ttu-id="3b2c2-166">콘솔 창의 **resourceGroupName:** 프롬프트에 **moneyapprg**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-166">In the console pane, at the **resourceGroupName:** prompt, type  **moneyapprg**.</span></span> <span data-ttu-id="3b2c2-167">그런 다음, **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-167">Then press **Enter**.</span></span>

1. <span data-ttu-id="3b2c2-168">콘솔 창의 **keyVaultName:** 프롬프트에 **moneyappkv**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-168">In the console pane, at the **keyVaultName:** prompt, type **moneyappkv**.</span></span> <span data-ttu-id="3b2c2-169">그런 다음, **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-169">Then press **Enter**.</span></span>

1. <span data-ttu-id="3b2c2-170">콘솔 창의 **location:** 프롬프트에 VM을 만들 때 사용한 위치를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-170">In the console pane, at the **location:** prompt, type the location you used when creating your VM.</span></span>

1. <span data-ttu-id="3b2c2-171">콘솔 창의 **subscriptionId:** 프롬프트에 구독 ID를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-171">In the console pane, at the **subscriptionId:** prompt, paste your subscription ID.</span></span>

1. <span data-ttu-id="3b2c2-172">이렇게 하면 **moneyappkv** Key Vault가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-172">The **moneyappkv** key vault will now be created.</span></span> <span data-ttu-id="3b2c2-173">이 작업이 완료되면 요약 텍스트(녹색)를 선택하여 메모장에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-173">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="3b2c2-174">**Enter** 키를 눌러 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-174">Press **Enter** to continue.</span></span>

1. <span data-ttu-id="3b2c2-175">콘솔 창의 **aadAppName:** 프롬프트에 **moneyapp**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-175">In the console pane, at the **aadAppName:**  prompt, type **moneyapp**.</span></span> <span data-ttu-id="3b2c2-176">그런 다음, **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-176">Then press **Enter**.</span></span>

1. <span data-ttu-id="3b2c2-177">이렇게 하면 **moneyapp** Azure AD 응용 프로그램이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-177">The **moneyapp** Azure AD application will now be created.</span></span> <span data-ttu-id="3b2c2-178">이 작업이 완료되면 요약 텍스트(녹색)를 선택하여 메모장에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-178">When this has completed, select the summary text (in green), and copy it to Notepad.</span></span>

1. <span data-ttu-id="3b2c2-179">**Enter** 키를 눌러 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-179">Press **Enter** to continue.</span></span>

### <a name="encrypt-your-vm-disks-with-powershell"></a><span data-ttu-id="3b2c2-180">PowerShell을 사용하여 VM 디스크 암호화</span><span class="sxs-lookup"><span data-stu-id="3b2c2-180">Encrypt your VM disks with PowerShell</span></span>

<span data-ttu-id="3b2c2-181">OS 및 데이터 디스크의 암호화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-181">Verify the encryption status of the OS and data disks:</span></span>

1. <span data-ttu-id="3b2c2-182">PowerShell ISE 콘솔 창에서 다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-182">In the PowerShell ISE console pane, type the following command, and press **Enter**:</span></span>

    ```powershell
    $vmName = 'moneyappsvr01'
    ```

    > [!NOTE]
    > <span data-ttu-id="3b2c2-183">VM 이름은 작은따옴표로 묶어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-183">The VM name must be enclosed in single quotes.</span></span>

1. <span data-ttu-id="3b2c2-184">PowerShell ISE 스크립트 창에 다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-184">In the PowerShell ISE script pane, enter the following command, and press **Enter**:</span></span>

    ```powershell
    Set-AzureRmVMDiskEncryptionExtension -ResourceGroupName $resourceGroupName -VMName $vmName -AadClientID $aadClientID -AadClientSecret $aadClientSecret -DiskEncryptionKeyVaultUrl $diskEncryptionKeyVaultUrl -DiskEncryptionKeyVaultId $keyVaultResourceId -VolumeType All
    ```

1. <span data-ttu-id="3b2c2-185">**VM에서 AzureDiskEncryption 사용** 대화 상자에서 **예**를 클릭하고 암호화를 완료하려면 10-15분이 걸린다는 메시지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-185">In the **Enable AzureDiskEncryption on the VM** dialog box, click **Yes**, and note the message that encryption may take 10-15 minutes to complete.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="3b2c2-186">명령이 완료될 때까지 기다렸다가 이 연습을 계속 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-186">Wait until the command has completed before continuing with this exercise.</span></span>

### <a name="verify-the-encryption-status-of-your-vm-disks"></a><span data-ttu-id="3b2c2-187">VM 디스크의 암호화 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-187">Verify the encryption status of your VM disks</span></span>

<span data-ttu-id="3b2c2-188">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-188">Switch to the Azure portal.</span></span> <span data-ttu-id="3b2c2-189">**moneyappsvr01**의 **디스크** 블레이드에서 OS 및 데이터 디스크의 디스크 암호화 상태가 이제 **사용**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="3b2c2-189">On the **Disks** blade for **moneyappsvr01**, note that the disk encryption status for the OS and Data disks is now **Enabled**.</span></span>
