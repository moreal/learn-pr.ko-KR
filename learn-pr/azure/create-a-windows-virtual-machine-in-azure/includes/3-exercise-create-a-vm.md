<span data-ttu-id="ac8fa-101">이 연습에서는 Azure에서 Windows 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-101">In this exercise, you'll create a Windows virtual machine in Azure.</span></span>

## <a name="motivation"></a><span data-ttu-id="ac8fa-102">사용해야 하는 이유</span><span class="sxs-lookup"><span data-stu-id="ac8fa-102">Motivation</span></span>

<span data-ttu-id="ac8fa-103">이 연습을 위한 대체 시나리오를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-103">Let's consider an alternate scenario for this exercise.</span></span> <span data-ttu-id="ac8fa-104">여기서 조직은 Windows Virtual Machines를 사용하여 학생들이 학교 컴퓨터에 영향을 주지 않고 웹앱을 설치하고, 도메인을 구성하고, Windows 서비스 및 기능을 탐색하는 테스트 환경을 실행하는 학교입니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-104">Here, your organization is a school that uses Windows virtual machines to spin up test environments on which students install web apps, configure domains, and explore Windows services and features without affecting the school's computers.</span></span> <span data-ttu-id="ac8fa-105">교사는 RDP를 사용하여 이러한 VM에 연결하고 학생의 진행 상황을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-105">Teachers connect to these VMs by using RDP and check on student progress.</span></span>

## <a name="create-a-windows-vm"></a><span data-ttu-id="ac8fa-106">Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="ac8fa-106">Create a Windows VM</span></span>

<span data-ttu-id="ac8fa-107">Windows VM을 만들려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-107">To create a Windows VM, complete the following steps:</span></span>

1. <span data-ttu-id="ac8fa-108">[Azure Portal](https://portal.azure.com)을 통해 Azure에 로그온합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-108">Log onto Azure through the [Azure portal](https://portal.azure.com).</span></span>

1. <span data-ttu-id="ac8fa-109">Azure Portal의 왼쪽 위에 있는 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-109">Click **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="ac8fa-110">**검색 창**에서 **Windows Server 2016 Datacenter**를 입력하고 동일한 제목의 링크를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-110">In the **search bar**, enter  **Windows Server 2016 Datacenter**  and then click on the link with the same title.</span></span>

### <a name="configure-the-vm-settings"></a><span data-ttu-id="ac8fa-111">VM 설정 구성</span><span class="sxs-lookup"><span data-stu-id="ac8fa-111">Configure the VM settings</span></span>

1. <span data-ttu-id="ac8fa-112">**기본** 아래의 **이름** 필드에 VM의 이름(예: “StudentVM”)을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-112">Under **Basics**, in the **Name** field, enter a name for your VM, such as "StudentVM."</span></span>

1. <span data-ttu-id="ac8fa-113">**VM 디스크 유형** 필드에서 드롭다운 메뉴를 클릭하여 옵션을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-113">In the **VM Disk Type** field, click the drop-down menu to see the options.</span></span> <span data-ttu-id="ac8fa-114">**SSD**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-114">Ensure that **SSD** is selected.</span></span>

1. <span data-ttu-id="ac8fa-115">**사용자 이름** 필드에 VM에 로그인하는 데 사용할 적합한 사용자 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-115">In the **Username** field, enter a suitable user name to use to sign in to the VM.</span></span>

1. <span data-ttu-id="ac8fa-116">**암호** 필드에 최소 12자 이상인 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-116">In the **Password** field, enter a password that's at least 12 characters long.</span></span> <span data-ttu-id="ac8fa-117">또한 대문자와 소문자, 숫자 및 특수 문자가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-117">It must also have upper and lowercase characters, numbers, and special characters.</span></span>

1. <span data-ttu-id="ac8fa-118">**리소스 그룹** 아래에서 **새로 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-118">Under **Resource group**, click **Create new**.</span></span> <span data-ttu-id="ac8fa-119">리소스 그룹에 “myTestRG” 등의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-119">Give the resource group a name, such as "myTestRG."</span></span>

1. <span data-ttu-id="ac8fa-120">VM을 만들 적합한 위치를 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-120">Select a suitable location for the VM to be created, and then click **OK**.</span></span>

### <a name="select-the-vm-image-size-and-options"></a><span data-ttu-id="ac8fa-121">VM 이미지 크기 및 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="ac8fa-121">Select the VM image size and options</span></span>

1. <span data-ttu-id="ac8fa-122">**크기 선택** 페이지에서 **B1** 이미지를 클릭하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-122">In the **Choose a size** page, click the **B1s** image, and then click **Select**.</span></span>

   > [!Note] 
   > <span data-ttu-id="ac8fa-123">B1 이미지에는 1GB의 RAM만 있으므로 처음 로그인할 때 메모리 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-123">The B1 image has only 1 GB of RAM and will result in memory errors when you first sign in.</span></span> <span data-ttu-id="ac8fa-124">그러나 나중에 랩의 일부로 이미지 크기를 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-124">However, you can resize the image later as part of a later lab.</span></span>

1. <span data-ttu-id="ac8fa-125">**설정** 페이지의 **공용 인바운드 포트 선택** 아래에서 **공용 인바운드 포트 없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-125">In the **Settings** page, under **Select Public Inbound Ports**, select **No public inbound ports**.</span></span> <span data-ttu-id="ac8fa-126">RDP 액세스는 나중에 구성하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-126">We'll configure RDP access later.</span></span>

### <a name="finish-configuring-the-vm-and-create-the-image"></a><span data-ttu-id="ac8fa-127">VM 구성 완료 및 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="ac8fa-127">Finish configuring the VM and create the image</span></span>

1. <span data-ttu-id="ac8fa-128">맨 아래로 스크롤하여 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-128">Scroll to the bottom and click **OK**.</span></span>

1. <span data-ttu-id="ac8fa-129">**만들기** 아래에서 구성한 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-129">Under **Create**, check the settings that you configured.</span></span> <span data-ttu-id="ac8fa-130">맨 아래에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-130">At the bottom, click **Create**.</span></span> <span data-ttu-id="ac8fa-131">Azure 대시보드에 배포 중인 VM이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-131">The Azure dashboard will show the VM that's being deployed.</span></span> <span data-ttu-id="ac8fa-132">이 작업은 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-132">This may take several minutes.</span></span>

## <a name="summary"></a><span data-ttu-id="ac8fa-133">요약</span><span class="sxs-lookup"><span data-stu-id="ac8fa-133">Summary</span></span>

<span data-ttu-id="ac8fa-134">이제 학생 요구 사항에 적합하고 학교 네트워크에서 액세스할 수 있는 Windows Server 가상 머신을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-134">You've now created a Windows Server virtual machine that's suitable for student requirements and accessible from the school network.</span></span> <span data-ttu-id="ac8fa-135">다음 단원에서는 RDP를 사용하여 해당 VM에 연결하고 관리하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac8fa-135">In the next unit, you will look at how you connect to and manage that VM by using RDP.</span></span>
