<span data-ttu-id="f5983-101">Linux 관리 도구 모음을 만드는 회사에서 일한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-101">Suppose you work at a company that makes a suite of Linux admin tools.</span></span> <span data-ttu-id="f5983-102">담당 업무는 잠재 고객이 소프트웨어를 구입하기 전에 사용해 보도록 지원하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-102">Your job is to help potential customers try your software before they buy it.</span></span> <span data-ttu-id="f5983-103">소프트웨어는 루트 수준에서 OS를 변경하므로 각 평가판 고객을 위한 Linux VM을 만들기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-103">Because the software makes root-level changes to the OS, you have decided to create a Linux VM for each trial customer.</span></span> <span data-ttu-id="f5983-104">필요에 따라 VM을 만들고 평가판 구독이 끝나면 해당 VM을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-104">You create the VMs as needed and delete them at the end of the trial subscription.</span></span> <span data-ttu-id="f5983-105">이런 식으로 각 고객은 초기 버전의 OS로 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-105">This way, each customer starts with a clean version of the OS.</span></span> 

<span data-ttu-id="f5983-106">이러한 VM을 회사에서 내부 테스트용으로 사용하는 VM과구분하려면 VM을 포함할 전용 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-106">To keep these VMs separate from the VMs your company uses for internal testing, you will create a dedicated resource group to house them.</span></span> <span data-ttu-id="f5983-107">리소스 그룹은 하나만 필요하므로 대화형 모드의 Azure PowerShell을 이 작업에 사용하는 것이 합리적입니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-107">You only need one resource group so using Azure PowerShell in interactive mode is a reasonable choice for this task.</span></span>

## <a name="steps-to-create-a-resource-group"></a><span data-ttu-id="f5983-108">리소스 그룹을 만드는 단계</span><span class="sxs-lookup"><span data-stu-id="f5983-108">Steps to create a resource group</span></span>

1. <span data-ttu-id="f5983-109">PowerShell을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-109">Launch PowerShell.</span></span>

1. <span data-ttu-id="f5983-110">Azure cmdlet에 액세스할 수 있도록 모듈을 현재 세션으로 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-110">Import the module into the current session so you have access to the Azure cmdlets.</span></span>

   ```powershell
   Import-Module AzureRM
   ```

1. <span data-ttu-id="f5983-111">아래 표시된 명령을 사용하여 Azure에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-111">Connect to Azure using the command shown below.</span></span> <span data-ttu-id="f5983-112">명령을 입력한 후 Azure 자격 증명을 제공하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-112">After entering the command, authenticate by providing your Azure credentials.</span></span>

   ```powershell
   Connect-AzureRmAccount
   ```

1. <span data-ttu-id="f5983-113">리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-113">Create a resource group.</span></span>

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. <span data-ttu-id="f5983-114">리소스 그룹이 성공적으로 만들어졌는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-114">Verify the resource group was created successfully.</span></span>

    ```powershell
    Get-AzureRmResource | Format-Table
    ```
<span data-ttu-id="f5983-115">리소스 그룹이 성공적으로 만들어졌는지 확인하는 또 다른 방법은 Azure Portal을 사용하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-115">Another way to check whether the resource group was created successfully is to use the Azure Portal.</span></span> <span data-ttu-id="f5983-116">이렇게 하려면 포털에 로그인하고 **리소스 그룹** 섹션(아래 참조)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-116">To do this, login to the Portal and navigate to the **Resource Groups** section (see below).</span></span> <span data-ttu-id="f5983-117">새 리소스 그룹이 목록에 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-117">The new resource group should be displayed in the list.</span></span>

<span data-ttu-id="f5983-118">다음 스크린샷은 Azure Portal에서 리소스 그룹 범주의 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-118">The following screenshot shows the location of the Resource groups category in the Azure Portal.</span></span>

![리소스 그룹 범주가 강조 표시된 Azure Portal 즐겨찾기 블레이드의 스크린샷](../media/6-listing-resource-groups.png)

## <a name="summary"></a><span data-ttu-id="f5983-120">요약</span><span class="sxs-lookup"><span data-stu-id="f5983-120">Summary</span></span>
<span data-ttu-id="f5983-121">이 연습에서는 대화형 PowerShell 세션의 일반적인 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-121">This exercise shows a common pattern for an interactive PowerShell session.</span></span> <span data-ttu-id="f5983-122">표준 cmdlet을 사용하여 AzureRM 모듈을 가져온 후에 Azure PowerShell cmdlet을 사용하여 특정 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-122">You used a standard cmdlet to import the AzureRM module and then the Azure PowerShell cmdlets to perform a specific task.</span></span> <span data-ttu-id="f5983-123">이제 구독에 리소스 그룹이 있으며 VM을 만들 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="f5983-123">You now have a resource group in your subscription and are ready to create VMs.</span></span>