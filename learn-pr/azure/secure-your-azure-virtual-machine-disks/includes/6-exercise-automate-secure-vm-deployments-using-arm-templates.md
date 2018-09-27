<span data-ttu-id="19bee-101">이 단원에서는 Azure Resource Manager 템플릿을 사용하여 앞서 만든 Windows VM의 암호를 해독합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-101">In this unit, you'll use an Azure Resource Manager template to decrypt our Windows VM we created earlier.</span></span> <span data-ttu-id="19bee-102">Windows VM에서 OS 드라이브를 암호화했습니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-102">We encrypted the OS drive on our Windows VM.</span></span> <span data-ttu-id="19bee-103">그러나 OS 드라이브에는 기밀 정보가 없으므로 암호화되지 않은 상태로 내버려둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-103">However, the OS drive won't have any confidential information on it, so we could leave it unencrypted.</span></span> <span data-ttu-id="19bee-104">템플릿을 사용하여 OS 드라이브의 암호를 해독해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-104">Let's use a template to decrypt the OS drive.</span></span>

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a><span data-ttu-id="19bee-105">Azure Resource Manager 템플릿을 사용하여 새 VM 구성 및 배포</span><span class="sxs-lookup"><span data-stu-id="19bee-105">Configure and deploy a new VM using an Azure Resource Manager template</span></span>

<span data-ttu-id="19bee-106">Microsoft가 Github에 게시한 템플릿을 사용하여 기본적으로 암호화가 작동되는 새 VM을 만들 예정입니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-106">We're going to use a template Microsoft has published on Github to create a new VM with encryption turned on by default.</span></span>

1. <span data-ttu-id="19bee-107">샌드박스를 활성화한 동일한 계정으로 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-107">Sign into the [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) with the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="19bee-108">왼쪽 사이드바에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-108">Click **Create a Resource** in the left sidebar.</span></span>

1. <span data-ttu-id="19bee-109">검색 상자에 **템플릿**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-109">Type **Template** in the search box.</span></span>

1. <span data-ttu-id="19bee-110">결과 목록에서 **템플릿 배포**를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-110">Select **Template Deployment** from the resulting list and click **Create**.</span></span>

    ![강조 표시된 만들기 단추를 사용하여 선택한 템플릿 배포 항목을 보여 주는 스크린샷](../media/6-create-template.png)

1. <span data-ttu-id="19bee-112">**템플릿을 선택** 검색 상자에서 "201-암호 해독" 입력을 시작하고 "201-decrypt-running-windows-vm-without-aad" 템플릿을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-112">In the **Select a template** search box, start typing "201-decrypt" and select the "201-decrypt-running-windows-vm-without-aad" template.</span></span>

    ![자동 완성을 사용하여 템플릿 검색 상자 선택을 보여 주는 스크린샷](../media/6-custom-deployment.png)

1. <span data-ttu-id="19bee-114">**템플릿 선택**을 클릭하여 템플릿 실행기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-114">Click **Select Template** to launch the template runner.</span></span>

1. <span data-ttu-id="19bee-115">설정 보기에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-115">In the settings view, enter the following information:</span></span>
    - <span data-ttu-id="19bee-116">**구독**에 대해 _컨시어지 구독_을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-116">Select _Concierge Subscription_ for the **Subscription**.</span></span>
    - <span data-ttu-id="19bee-117">샌드박스에서 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-117">Select your Resource Group, created in the sandbox.</span></span>
    - <span data-ttu-id="19bee-118">VM을 만든 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-118">Select the location you created the VM in.</span></span>
    - <span data-ttu-id="19bee-119">**VM 이름**에 "fmdata-vm01"을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-119">Enter "fmdata-vm01" for the **VM Name**.</span></span>
    - <span data-ttu-id="19bee-120">**볼륨 형식**을 _모두_로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-120">Leave the **Volume Type** as _All_.</span></span>

1. <span data-ttu-id="19bee-121">**사용 약관에 동의함** 확인란을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-121">Select the **I agree to the terms and conditions** check box.</span></span>
1. <span data-ttu-id="19bee-122">**구매**를 클릭하여 템플릿을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-122">Click **Purchase** to run the template.</span></span> <span data-ttu-id="19bee-123">이 템플릿에 대한 비용은 없습니다 - 이것은 표준 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-123">Note that there is no cost to this - it's a standard button.</span></span>

<span data-ttu-id="19bee-124">배포가 완료될 때까지 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-124">The deployment may take a few minutes to complete.</span></span>

## <a name="verify-the-encryption-status-of-the-vm"></a><span data-ttu-id="19bee-125">VM의 암호화 상태를 확인</span><span class="sxs-lookup"><span data-stu-id="19bee-125">Verify the encryption status of the VM</span></span>

1. <span data-ttu-id="19bee-126">Azure Portal의 사이트바에서 **가상 머신**을 클릭하고 VM **fmdata-vm01**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-126">In the sidebar of the Azure portal, click **Virtual machines** and select your VM **fmdata-vm01**.</span></span> <span data-ttu-id="19bee-127">또는 **모든 리소스**에서 이름으로 VM을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-127">Alternatively, you can search for your VM by name from **All Resources**.</span></span>

1. <span data-ttu-id="19bee-128">**가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-128">On the **Virtual machine** blade, under **SETTINGS**, click **Disks**.</span></span>

1. <span data-ttu-id="19bee-129">**디스크** 블레이드에서 OS 디스크 암호화 상태가 **사용 안 함**인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="19bee-129">On the **Disks** blade, notice the OS disk encryption status is now **Disabled**.</span></span>
