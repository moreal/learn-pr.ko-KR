<span data-ttu-id="ca0c5-101">이 단원에서는 Linux 관리 도구를 만드는 회사의 예제를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-101">In this unit, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="ca0c5-102">Linux VM을 사용하여 잠재 고객이 소프트웨어를 테스트하도록 할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="ca0c5-103">리소스 그룹이 준비되었고 이제 VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="ca0c5-104">회사는 대규모 Linux 무역 박람회에서 부스에 대한 비용을 지급했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="ca0c5-105">별도의 Linux VM에 연결된 세 개의 터미널을 포함하는 데모 영역을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="ca0c5-106">매일 끝날 때 VM을 삭제하고 다시 만들어 매일 아침 새로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="ca0c5-107">피곤할 때 작업 후에 수동으로 VM을 만들면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="ca0c5-108">VM 만들기 프로세스를 자동화하기 위해 PowerShell 스크립트를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="ca0c5-109">Virtual Machines를 만드는 스크립트 작성</span><span class="sxs-lookup"><span data-stu-id="ca0c5-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="ca0c5-110">스크립트를 작성할 수 있는 권한을 얻으려면 Cloud Shell에서 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-110">Follow these steps in the Cloud Shell on the right to write the script:</span></span>

1. <span data-ttu-id="ca0c5-111">Cloud Shell에서 홈 폴더로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-111">Switch to your home folder in the Cloud Shell.</span></span>

    ```powershell
    cd $HOME\clouddrive
    ```

1. <span data-ttu-id="ca0c5-112">**ConferenceDailyReset.ps1**이라는 새 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-112">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

    ```powershell
    touch "./ConferenceDailyReset.ps1"
    ```

1. <span data-ttu-id="ca0c5-113">통합 편집기를 열고 **ConferenceDailyReset.ps1** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-113">Open the integrated editor and select the **ConferenceDailyReset.ps1** file.</span></span>

    ```powershell
    code "./ConferenceDailyReset.ps1"
    ```
    > [!TIP]
    > <span data-ttu-id="ca0c5-114">통합 Cloud Shell에서는 vim, nano 및 emacs도 지원하므로 선호하는 편집기를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-114">The integrated Cloud Shell also supports vim, nano, and emacs if you'd prefer to use one of those editors.</span></span>

1. <span data-ttu-id="ca0c5-115">입력 매개 변수를 변수로 캡처하여 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-115">Start by capturing the input parameter in a variable.</span></span> <span data-ttu-id="ca0c5-116">다음 줄을 스크립트에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-116">Add the following line to your script:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

    > [!NOTE]
    > <span data-ttu-id="ca0c5-117">일반적으로 `Connect-AzureRmAccount`를 사용하여 자격 증명을 통해 Azure에서 인증해야 하며 스크립트에서 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-117">Normally, you'd have to authenticate with Azure using your credentials using `Connect-AzureRmAccount` and this could be done in the script.</span></span> <span data-ttu-id="ca0c5-118">그러나 Cloud Shell 환경에서는 미리 인증이 되므로 이는 불필요한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-118">However, in the Cloud Shell environment you will already be authenticated so this is unnecessary.</span></span>

1. <span data-ttu-id="ca0c5-119">VM의 관리자 계정에 대한 사용자 이름과 암호를 묻는 메시지를 표시하고 결과를 변수로 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-119">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

1. <span data-ttu-id="ca0c5-120">세 번 실행되는 루프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-120">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

1. <span data-ttu-id="ca0c5-121">루프 본문에서 각 VM의 이름을 만들고, 변수에 저장하고, 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-121">In the loop body, create a name for each VM and store it in a variable and output it to the console:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    ```

1. <span data-ttu-id="ca0c5-122">다음으로, `$vmName` 변수를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-122">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
   ```

1. <span data-ttu-id="ca0c5-123">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-123">Save the file.</span></span> <span data-ttu-id="ca0c5-124">편집기의 오른쪽 위 모서리에서 "..." 메뉴를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-124">You can use the "..." menu at the top right corner of the editor.</span></span> <span data-ttu-id="ca0c5-125">저장을 위한 일반 액셀러레이터 키도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-125">There are also common accelerator keys for Save.</span></span>

<span data-ttu-id="ca0c5-126">완료된 스크립트는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-126">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i
    Write-Host "Creating VM: " $vmName
    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="ca0c5-127">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="ca0c5-127">Execute the script</span></span>

<span data-ttu-id="ca0c5-128">"..." 상황에 맞는 메뉴를 통해 편집기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-128">Close the editor through the "..." context menu.</span></span>

1. <span data-ttu-id="ca0c5-129">스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-129">Execute the script.</span></span>

    ```powershell
    .\ConferenceDailyReset.ps1 <rgn>[sandbox resource group name]</rgn>
    ```
    
<span data-ttu-id="ca0c5-130">스크립트를 완료하는 데는 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-130">The script will take several minutes to complete.</span></span> <span data-ttu-id="ca0c5-131">완료되면 리소스 그룹에 포함된 리소스를 확인하여 스크립트가 성공적으로 실행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-131">When it is finished, verify that it ran successfully by looking at the resources you now have in your resource group:</span></span>

```powershell
Get-AzureRmResource -ResourceType Microsoft.Compute/virtualMachines
```

<span data-ttu-id="ca0c5-132">각각 고유한 이름을 가진 세 개의 VM이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-132">You should see three VMs, each with a unique name.</span></span>

<span data-ttu-id="ca0c5-133">스크립트 매개 변수로 표시된 리소스 그룹에서 세 개의 VM 만들기를 자동화하는 스크립트를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-133">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="ca0c5-134">스크립트는 짧고 간단하지만 포털을 통해 수동으로 완료하는 데 시간이 오래 걸리는 프로세스를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="ca0c5-134">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>