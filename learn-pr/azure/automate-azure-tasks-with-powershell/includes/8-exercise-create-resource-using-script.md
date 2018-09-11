<span data-ttu-id="a2bce-101">이 연습에서는 Linux 관리 도구를 만드는 회사의 예제를 계속 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-101">In this exercise, you will continue with the example of a company that makes Linux admin tools.</span></span> <span data-ttu-id="a2bce-102">Linux VM을 사용하여 잠재 고객이 소프트웨어를 테스트하도록 할 계획입니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-102">Recall that you plan to use Linux VMs to let potential customers test your software.</span></span> <span data-ttu-id="a2bce-103">리소스 그룹이 준비되었고 이제 VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-103">You have a resource group ready and now it is time to create the VMs.</span></span>

<span data-ttu-id="a2bce-104">회사는 대규모 Linux 무역 박람회에서 부스에 대한 비용을 지급했습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-104">Your company has paid for a booth at a big Linux trade show.</span></span> <span data-ttu-id="a2bce-105">별도의 Linux VM에 연결된 세 개의 터미널을 포함하는 데모 영역을 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-105">You plan a demo area containing three terminals each connected to a separate Linux VM.</span></span> <span data-ttu-id="a2bce-106">매일 끝날 때 VM을 삭제하고 다시 만들어 매일 아침 새로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-106">At the end of each day, you want to delete the VMs and recreate them, so they start fresh every morning.</span></span> <span data-ttu-id="a2bce-107">피곤할 때 작업 후에 수동으로 VM을 만들면 오류가 발생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-107">Creating the VMs manually after work when you are tired would be error prone.</span></span> <span data-ttu-id="a2bce-108">VM 만들기 프로세스를 자동화하기 위해 PowerShell 스크립트를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-108">You want to write a PowerShell script to automate the VM creation process.</span></span>

## <a name="write-a-script-that-creates-virtual-machines"></a><span data-ttu-id="a2bce-109">가상 머신을 만드는 스크립트 작성</span><span class="sxs-lookup"><span data-stu-id="a2bce-109">Write a script that creates Virtual Machines</span></span>

<span data-ttu-id="a2bce-110">다음 단계를 수행하여 스크립트를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-110">Follow these steps to write the script:</span></span>

1. <span data-ttu-id="a2bce-111">**ConferenceDailyReset.ps1**이라는 새 텍스트 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-111">Create a new text file named **ConferenceDailyReset.ps1**.</span></span>

2. <span data-ttu-id="a2bce-112">매개 변수를 변수로 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-112">Capture the parameter in a variable:</span></span>

    ```powershell
    param([string]$resourceGroup)
    ```

3. <span data-ttu-id="a2bce-113">자격 증명을 사용하여 Azure로 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-113">Authenticate with Azure using your credentials:</span></span>

    ```powershell
    Connect-AzureRmAccount
    ```

4. <span data-ttu-id="a2bce-114">VM의 관리자 계정에 대한 사용자 이름 및 암호를 묻는 메시지를 표시하고 결과를 변수로 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-114">Prompt for a username and password for the VM's admin account and capture the result in a variable:</span></span>

    ```powershell
    $adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."
    ```

5. <span data-ttu-id="a2bce-115">세 번 실행되는 루프를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-115">Create a loop that executes three times:</span></span>

    ```powershell
    For ($i = 1; $i -le 3; $i++) 
    {

    }
    ```

6. <span data-ttu-id="a2bce-116">루프 본문에서 각 VM의 이름을 만들고 변수에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-116">In the loop body, create a name for each VM and store it in a variable:</span></span>

    ```powershell
    $vmName = "ConferenceDemo" + $i
    ```

7. <span data-ttu-id="a2bce-117">다음으로 `$vmName` 변수를 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-117">Next, create a VM using the `$vmName` variable:</span></span>

   ```powershell
   New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" 
   ```

8. <span data-ttu-id="a2bce-118">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-118">Save the file.</span></span>

<span data-ttu-id="a2bce-119">완료된 스크립트는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-119">The completed script should look like this:</span></span>

```powershell
param([string]$resourceGroup)

$adminCredential = Get-Credential -Message "Enter a username and password for the VM administrator."

Connect-AzureRmAccount

For ($i = 1; $i -le 3; $i++)
{
    $vmName = "ConferenceDemo" + $i

    New-AzureRmVm -ResourceGroupName $resourceGroup -Name $vmName -Credential $adminCredential -Location "East US" -Image UbuntuLTS
}
```

## <a name="execute-the-script"></a><span data-ttu-id="a2bce-120">스크립트 실행</span><span class="sxs-lookup"><span data-stu-id="a2bce-120">Execute the script</span></span>

<span data-ttu-id="a2bce-121">PowerShell을 시작하고 스크립트 파일을 저장한 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-121">Launch PowerShell and change to the directory where you saved the script file.</span></span> <span data-ttu-id="a2bce-122">스크립트를 실행하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-122">To run the script, execute the following command:</span></span>

```powershell
.\ConferenceDailyReset.ps1 TrialsResourceGroup
```

<span data-ttu-id="a2bce-123">스크립트를 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-123">The script may take a few minutes to complete.</span></span> <span data-ttu-id="a2bce-124">완료되면 성공적으로 실행되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-124">When it is finished, verify that it ran successfully:</span></span>

1. <span data-ttu-id="a2bce-125">브라우저에서 Azure Portal에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-125">In a browser, sign into the Azure portal.</span></span>
2. <span data-ttu-id="a2bce-126">왼쪽 탐색에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-126">In the navigation on the left, click **Resource Groups**.</span></span>
3. <span data-ttu-id="a2bce-127">리소스 그룹 목록에서 **TrialsResourceGroup**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-127">In the list of resource groups, click **TrialsResourceGroup**.</span></span> <span data-ttu-id="a2bce-128">리소스 목록에 새로 만든 VM 및 연결된 리소스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-128">In the list of resources, you should see the newly created VMs and their associated resources.</span></span>

## <a name="summary"></a><span data-ttu-id="a2bce-129">요약</span><span class="sxs-lookup"><span data-stu-id="a2bce-129">Summary</span></span>
<span data-ttu-id="a2bce-130">스크립트 매개 변수로 표시된 리소스 그룹에서 세 개의 VM 만들기를 자동화하는 스크립트를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-130">You wrote a script that automated the creation of three VMs in the resource group indicated by a script parameter.</span></span> <span data-ttu-id="a2bce-131">스크립트는 짧고 간단하지만 포털을 통해 수동으로 완료하는 데 시간이 오래 걸리는 프로세스를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="a2bce-131">The script is short and simple but automates a process that would take a long time to complete manually with the portal.</span></span>