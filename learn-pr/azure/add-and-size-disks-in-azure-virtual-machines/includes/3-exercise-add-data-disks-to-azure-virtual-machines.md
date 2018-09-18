<span data-ttu-id="35cc8-101">이 연습에서는 회사가 SMTP(Simple Mail Transfer Protocol) 메일 서버를 실행한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-101">In this exercise, let's assume your company runs a Simple Mail Transfer Protocol (SMTP) email server.</span></span> <span data-ttu-id="35cc8-102">이 서버를 Azure로 마이그레이션하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-102">You want to migrate this server into Azure.</span></span> <span data-ttu-id="35cc8-103">SMTP 서버가 고유한 도메인에 대한 들어오는 메시지를 전용 VHD의 “Drop”이라는 폴더에 저장하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-103">You want the SMTP server to store incoming messages for your own domain in a folder called "Drop" on a dedicated VHD.</span></span>

<span data-ttu-id="35cc8-104">연습의 목표는 Windows VM(가상 머신)을 만들고 “Incoming”이라는 새 VHD(가상 하드 디스크)를 연결하여 “Drop” 디렉터리를 저장하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-104">The goal of the exercise is to create a Windows virtual machine (VM) and attach a new virtual hard disk (VHD) called "Incoming" to store the "Drop" directory.</span></span>

## <a name="sign-in-to-azure"></a><span data-ttu-id="35cc8-105">Azure에 로그인</span><span class="sxs-lookup"><span data-stu-id="35cc8-105">Sign in to Azure</span></span>
<!---TODO: Need update for sanbox?--->

1. <span data-ttu-id="35cc8-106">[Azure Portal](https://portal.azure.com/?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-106">Sign in to the [Azure portal](https://portal.azure.com/?azure-portal=true).</span></span>

## <a name="create-a-windows-vm-in-the-azure-portal"></a><span data-ttu-id="35cc8-107">Azure Portal에서 Windows VM 만들기</span><span class="sxs-lookup"><span data-stu-id="35cc8-107">Create a Windows VM in the Azure portal</span></span>

<span data-ttu-id="35cc8-108">VM을 만들어 데이터 드라이브가 포함된 SMTP 서버를 호스트하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-108">To create a VM to host the SMTP server with its data drives, follow these steps:</span></span>

1. <span data-ttu-id="35cc8-109">Azure Portal의 왼쪽 위에 있는 **리소스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-109">Choose **Create a resource** in the upper left corner of the Azure portal.</span></span>

1. <span data-ttu-id="35cc8-110">Azure Marketplace 리소스 목록 위에 있는 검색 상자에서 **Windows Server 2016 Datacenter**를 검색하고 선택한 다음, **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-110">In the search box above the list of Azure Marketplace resources, search for and select **Windows Server 2016 Datacenter**, and then choose **Create**.</span></span>

1. <span data-ttu-id="35cc8-111">오른쪽에 열리는 **기본 사항** 창에서 다음 속성 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-111">In the **Basics** pane that opens to the right, enter the following property values.</span></span> 


|<span data-ttu-id="35cc8-112">속성</span><span class="sxs-lookup"><span data-stu-id="35cc8-112">Property</span></span>  |<span data-ttu-id="35cc8-113">값</span><span class="sxs-lookup"><span data-stu-id="35cc8-113">Value</span></span>  |<span data-ttu-id="35cc8-114">참고</span><span class="sxs-lookup"><span data-stu-id="35cc8-114">Notes</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="35cc8-115">이름</span><span class="sxs-lookup"><span data-stu-id="35cc8-115">Name</span></span>     |   <span data-ttu-id="35cc8-116">**MailSenderVM**</span><span class="sxs-lookup"><span data-stu-id="35cc8-116">**MailSenderVM**</span></span>      |         |
|<span data-ttu-id="35cc8-117">VM 디스크 유형</span><span class="sxs-lookup"><span data-stu-id="35cc8-117">VM disk type</span></span>     |  <span data-ttu-id="35cc8-118">**표준 HDD**</span><span class="sxs-lookup"><span data-stu-id="35cc8-118">**Standard HDD**</span></span>       |   <span data-ttu-id="35cc8-119">드롭다운에서 이 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-119">Select this value from the dropdown.</span></span>      |
|<span data-ttu-id="35cc8-120">사용자 이름</span><span class="sxs-lookup"><span data-stu-id="35cc8-120">User name</span></span>     |  <span data-ttu-id="35cc8-121">**mailmaster**</span><span class="sxs-lookup"><span data-stu-id="35cc8-121">**mailmaster**</span></span>       |         |
|<span data-ttu-id="35cc8-122">암호</span><span class="sxs-lookup"><span data-stu-id="35cc8-122">Password</span></span>     |  <span data-ttu-id="35cc8-123">암호는 12자 이상이어야 하며 [정의된 복잡성 요구 사항](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm)을 충족해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-123">The password must be at least 12 characters long and meet the [defined complexity requirements](https://docs.microsoft.com/azure/virtual-machines/windows/faq#what-are-the-password-requirements-when-creating-a-vm).</span></span>       | <span data-ttu-id="35cc8-124">모듈 전체에서 사용하므로 이 사용자 이름과 암호를 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="35cc8-124">Make sure to remember this user name and password because we'll use them throughout the module.</span></span>         |
|<span data-ttu-id="35cc8-125">구독</span><span class="sxs-lookup"><span data-stu-id="35cc8-125">Subscription</span></span>     |  <span data-ttu-id="35cc8-126">구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-126">Choose your subscription.</span></span>       |  <span data-ttu-id="35cc8-127">드롭다운에서 이 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-127">Select this value from the dropdown.</span></span>       |
|<span data-ttu-id="35cc8-128">리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="35cc8-128">Resource group</span></span>     |  <span data-ttu-id="35cc8-129">**새로 만들기**를 선택한 다음, **MailInfrastructure**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-129">Select **Create new**, and then type **MailInfrastructure**.</span></span>       |  <span data-ttu-id="35cc8-130">이 모듈에서 사용된 모든 리소스를 하나의 리소스 그룹으로 수집합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-130">We'll gather all resource used in this module into one resource group.</span></span>       |
|<span data-ttu-id="35cc8-131">위치</span><span class="sxs-lookup"><span data-stu-id="35cc8-131">Location</span></span>     |   <span data-ttu-id="35cc8-132">사용자에게 가까운 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-132">A location near you.</span></span>      | <span data-ttu-id="35cc8-133">드롭다운에서 이 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-133">Select this value from the dropdown.</span></span>        |

4. <span data-ttu-id="35cc8-134">**기본 사항** 페이지의 맨 아래에서 **확인**을 선택하여 **크기** 구성 창을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-134">Select **OK** at the bottom of the **Basics** page to continue to the **Size** configuration pane.</span></span>

1. <span data-ttu-id="35cc8-135">**크기** 구성 창에서 **B1ms**를 검색하여 선택한 후 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-135">In the **Size** configuration pane, search for and select **B1ms**, and then click **Select**.</span></span>

1. <span data-ttu-id="35cc8-136">**설정** 창의 **관리 디스크 사용** 아래에서 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-136">In the **Settings** pane, under **Use managed disks**, click **No**.</span></span> <span data-ttu-id="35cc8-137">이 모듈의 뒷부분에서 관리 디스크에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-137">We'll discuss managed disks later in this module.</span></span>

1. <span data-ttu-id="35cc8-138">**공용 인바운드 포트 선택** 드롭다운 목록에서 **RDP(3389)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-138">In the **Select public inbound ports** dropdown list, select **RDP (3389)**.</span></span> <span data-ttu-id="35cc8-139">이 포트를 사용하여 VM이 만들어진 후 이 VM에 원격으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-139">We'll use this port to remote into our VM after it's created.</span></span>

1. <span data-ttu-id="35cc8-140">다른 모든 설정을 기본값으로 유지하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-140">Leave all the other settings at their default, and then click **OK**.</span></span>

1. <span data-ttu-id="35cc8-141">**만들기** 창에서 구성을 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-141">In the **Create** pane, review the configuration.</span></span>

1. <span data-ttu-id="35cc8-142">구성을 검토한 후 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-142">When you have reviewed the configuration,  select **Create**.</span></span> <span data-ttu-id="35cc8-143">Azure가 새 VM을 만들고 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-143">Azure creates and starts the new VM.</span></span>

> [!TIP]
> <span data-ttu-id="35cc8-144">VM을 만들고 Azure에 배포하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-144">Creating your VM and deploying it in Azure can take a few minutes.</span></span> <span data-ttu-id="35cc8-145">**알림** 허브에서 진행 상황을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-145">You can watch the progress in the **Notifications** hub.</span></span> <span data-ttu-id="35cc8-146">완료되면 Azure에 알림 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-146">Azure will display a notification dialog when it finishes.</span></span>

## <a name="add-an-empty-data-disk-to-our-vm"></a><span data-ttu-id="35cc8-147">VM에 빈 데이터 디스크 추가</span><span class="sxs-lookup"><span data-stu-id="35cc8-147">Add an empty data disk to our VM</span></span>

<span data-ttu-id="35cc8-148">디스크 저장소의 이름을 SMTP 서버 “Incoming”의 “Drop” 디렉터리로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-148">We're going to name the disk stores the "Drop" directory for your SMTP server "Incoming".</span></span> <span data-ttu-id="35cc8-149">다음 단계를 사용하여 새 빈 디스크를 서버에 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-149">Let's add a new empty disk to the server using the following steps:</span></span>

1. <span data-ttu-id="35cc8-150">왼쪽 탐색의 **즐겨찾기**에서 **가상 머신**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-150">In the navigation on the left, under **FAVORITES**, select **Virtual machines**.</span></span>

1. <span data-ttu-id="35cc8-151">VM 목록에서 **MailSenderVM**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-151">In the list of VMs, select **MailSenderVM**.</span></span>

1. <span data-ttu-id="35cc8-152">왼쪽 **MailSenderVM** 구성 메뉴의 **설정** 아래에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-152">Under **SETTINGS** of the **MailSenderVM** configuration menu on the left, select **Disks**.</span></span>

1. <span data-ttu-id="35cc8-153">**데이터 디스크**에서 **데이터 디스크 추가**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-153">Under **Data disks**, select **Add data disk**.</span></span>

1. <span data-ttu-id="35cc8-154">**관리되지 않는 디스크 연결** 창에서 다음 속성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-154">In the **Attach unmanaged disks** pane, set the following properties.</span></span>


|<span data-ttu-id="35cc8-155">속성</span><span class="sxs-lookup"><span data-stu-id="35cc8-155">Property</span></span>  |<span data-ttu-id="35cc8-156">값</span><span class="sxs-lookup"><span data-stu-id="35cc8-156">Value</span></span>  |<span data-ttu-id="35cc8-157">참고</span><span class="sxs-lookup"><span data-stu-id="35cc8-157">Notes</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="35cc8-158">이름</span><span class="sxs-lookup"><span data-stu-id="35cc8-158">Name</span></span>     |   <span data-ttu-id="35cc8-159">**MailSenderVMIncoming**</span><span class="sxs-lookup"><span data-stu-id="35cc8-159">**MailSenderVMIncoming**</span></span>      |         |
|<span data-ttu-id="35cc8-160">원본 형식</span><span class="sxs-lookup"><span data-stu-id="35cc8-160">Source type</span></span>     |  <span data-ttu-id="35cc8-161">**새로 만들기(빈 디스크)**</span><span class="sxs-lookup"><span data-stu-id="35cc8-161">**New (empty disk)**</span></span>       |   <span data-ttu-id="35cc8-162">드롭다운에서 이 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-162">Select this value from the dropdown.</span></span>       |
|<span data-ttu-id="35cc8-163">계정 유형</span><span class="sxs-lookup"><span data-stu-id="35cc8-163">Account type</span></span>     |  <span data-ttu-id="35cc8-164">**표준 HDD**</span><span class="sxs-lookup"><span data-stu-id="35cc8-164">**Standard HDD**</span></span>       |  <span data-ttu-id="35cc8-165">드롭다운에서 이 값을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-165">Select this value from the dropdown.</span></span>        |


6. <span data-ttu-id="35cc8-166">**저장소 컨테이너** 필드의 왼쪽에서 **찾아보기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-166">To the left of the **Storage container** field, select **Browse**.</span></span>

1. <span data-ttu-id="35cc8-167">저장소 계정 목록에서 이름이 **mailinfrastructure**로 시작하는 저장소 계정을 검색하고 이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-167">In the list of storage accounts, search for the storage account whose name begins with **mailinfrastructure** and select it.</span></span>

1. <span data-ttu-id="35cc8-168">컨테이너 목록에서 **vhds**를 클릭한 후 **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-168">In the list of containers, click **vhds** and then choose **Select**.</span></span>

1. <span data-ttu-id="35cc8-169">**관리되지 않는 디스크 연결** 화면으로 돌아가 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-169">Back on the **Attach unmanaged disk** screen, select **OK**.</span></span>

1. <span data-ttu-id="35cc8-170">**MailSenderVM - 디스크** 화면으로 돌아가 **저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-170">Back on the **MailSenderVM - Disks** screen, select **Save**.</span></span>

<span data-ttu-id="35cc8-171">이제 **MainSenderVMIncoming**이라는 디스크를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-171">We've now defined a disk called **MainSenderVMIncoming**.</span></span> <span data-ttu-id="35cc8-172">디스크를 사용하려면 먼저 VM에 로그인할 때 디스크를 분할하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-172">To use the disk, we'll first need to partition and format it when we log into the VM.</span></span> 

## <a name="partition-and-format-a-data-disk"></a><span data-ttu-id="35cc8-173">데이터 디스크 분할 및 포맷</span><span class="sxs-lookup"><span data-stu-id="35cc8-173">Partition and format a data disk</span></span>

<span data-ttu-id="35cc8-174">물리적 디스크와 마찬가지로, 사용하기 전에 VHD에서 파티션을 시작하고 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-174">As with physical disks, initiate and format a partition on a VHD before it can be used.</span></span>

### <a name="log-into-our-windows-vm-using-rdp"></a><span data-ttu-id="35cc8-175">RDP를 사용하여 Windows VM에 로그인</span><span class="sxs-lookup"><span data-stu-id="35cc8-175">Log into our Windows VM using RDP</span></span>

1. <span data-ttu-id="35cc8-176">**MailSenderVM** 가상 머신 기본 화면에서 **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-176">In the **MailSenderVM** virtual machine main screen, select **Overview**.</span></span>

1. <span data-ttu-id="35cc8-177">개요 화면의 왼쪽 위에서 **연결**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-177">Select **Connect** from the top left of the overview screen.</span></span>

1. <span data-ttu-id="35cc8-178">오른쪽에 열리는 **가상 머신에 연결** 대화 상자에서 **RDP 파일로 다운로드**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-178">In the **Connect to virtual machine** dialog that opens on the right, select **Download to RDP File**.</span></span>

   ![“RDP 파일 다운로드” 단추가 강조 표시된 “가상 머신에 연결” 대화 상자의 스크린샷입니다.](../media-draft/download-rdp.png)

4. <span data-ttu-id="35cc8-180">**MailSenderVM.rdp** 파일이 로컬 `Downloads` 폴더에 다운로드됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-180">A file called **MailSenderVM.rdp** is downloaded to your local `Downloads` folder.</span></span> <span data-ttu-id="35cc8-181">이 파일은 MailSenderVM 가상 머신의 원격 데스크톱 구성 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-181">This file is the remote desktop configuration file for the MailSenderVM virtual machine.</span></span> <span data-ttu-id="35cc8-182">파일을 열어 연결 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-182">Open the file to start the connection process.</span></span>

1. <span data-ttu-id="35cc8-183">**원격 데스크톱 연결** 대화 상자에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-183">In the **Remote Desktop Connection** dialog, click **Connect**.</span></span>

1. <span data-ttu-id="35cc8-184">**Windows 보안** 대화 상자에서 **다른 계정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-184">In the **Windows Security** dialog, click **Use another account**.</span></span>

1. <span data-ttu-id="35cc8-185">**사용자 이름** 텍스트 상자에 **mailmaster**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-185">In the **Username** textbox, type **mailmaster**.</span></span>

1. <span data-ttu-id="35cc8-186">**암호** 텍스트 상자에 이 연습에서 이 사용자 이름에 대해 입력한 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-186">In the **Password** textbox, type the password you entered for this user name in this exercise.</span></span> 

1. <span data-ttu-id="35cc8-187">**원격 데스크톱 연결** 대화 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-187">In the **Remote Desktop Connection** dialog, click **Yes**.</span></span>

<span data-ttu-id="35cc8-188">이제 가상 머신에 대한 원격 데스크톱 세션이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-188">A remote desktop session to the virtual machine is now started.</span></span> <span data-ttu-id="35cc8-189">처음으로 로그인하는 데 시간이 잠시 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-189">It might take a few moments to sign in for the first time.</span></span> <span data-ttu-id="35cc8-190">로그인이 완료되면 **서버 관리자** 도구가 화면에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-190">When sign-in is finished, the **Server Manager** tool will be displayed on the screen.</span></span>

### <a name="partition-and-format-our-data-disk-using-server-manager"></a><span data-ttu-id="35cc8-191">서버 관리자를 사용하여 데이터 디스크 분할 및 포맷</span><span class="sxs-lookup"><span data-stu-id="35cc8-191">Partition and format our data disk using Server Manager</span></span>

1. <span data-ttu-id="35cc8-192">**서버 관리자**가 표시되면 왼쪽에 있는 탐색에서 **파일 및 저장소 서비스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-192">When **Server Manager** is displayed, select **File and Storage Services** in the navigation on the left.</span></span>

1. <span data-ttu-id="35cc8-193">**볼륨**에서 **디스크**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-193">Under **Volumes**, select **Disks**.</span></span>

1. <span data-ttu-id="35cc8-194">디스크 목록에서 디스크 **0**은 운영 체제 디스크이고 디스크 **1**은 임시 디스크입니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-194">In the list of disks, disk **0** is the operating system disk and disk **1** is the temporary disk.</span></span> <span data-ttu-id="35cc8-195">방금 추가한 새 VHD인 디스크 **2**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-195">Select disk **2**, which is the new VHD you just added.</span></span>

1. <span data-ttu-id="35cc8-196">**볼륨** 창의 위쪽에서 **작업**, **새 볼륨...** 을 차례로 선택합니다. 메뉴는 다음과 같이 화면의 오른쪽 위에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-196">At the top of the **VOLUMES** pane, select **TASKS** followed by **New Volume...**. The menu is in the top right of the screen as follows.</span></span>

   ![세 가지 메뉴 항목을 표시하도록 확장된 “작업” 메뉴의 스크린샷입니다.](../media-draft/tasks-menu.png)


1. <span data-ttu-id="35cc8-199">**새 볼륨** 마법사에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-199">In the **New Volume** wizard, click **Next**.</span></span>

1. <span data-ttu-id="35cc8-200">**서버 및 디스크 선택** 페이지에서 **MailSenderVM** 및 **디스크 2**를 선택한 후 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-200">In the **Select server and disk** page, select **MailSenderVM** and **Disk 2**, and then click **Next**.</span></span>

1. <span data-ttu-id="35cc8-201">**오프라인 또는 시작되지 않은 디스크** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-201">In the **Offline or Uninitiated Disk** dialog, click **OK**.</span></span>

1. <span data-ttu-id="35cc8-202">**볼륨 크기 지정** 페이지에서 **다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-202">In the **Specify the size of the volume** page, click **Next**.</span></span>

1. <span data-ttu-id="35cc8-203">**드라이브 문자 할당** 페이지에서 **F:**, **다음**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-203">In the **Assign a drive letter** page, select **F:** followed by **Next**.</span></span>

1. <span data-ttu-id="35cc8-204">**파일 시스템 설정 선택** 페이지에서 **볼륨 레이블** 텍스트 상자에 **Incoming**을 입력한 후 **다음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-204">In the **Select file system settings** page, in the **Volume label** textbox, type **Incoming** and then select **Next**.</span></span>

1. <span data-ttu-id="35cc8-205">**선택 확인** 페이지에서 **만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-205">In the **Confirm selections** page, select **Create**.</span></span> <span data-ttu-id="35cc8-206">Windows가 디스크를 시작하고 새 파티션을 포맷합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-206">Windows initiates the disk and formats the new partition.</span></span>

1. <span data-ttu-id="35cc8-207">**완료** 페이지에서 **닫기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-207">In the **Completion** page, select **Close**.</span></span>

<span data-ttu-id="35cc8-208">파일 탐색기에서 새 디스크 볼륨을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-208">Let's have a look at our new disk volume in File Explorer.</span></span> 
1. <span data-ttu-id="35cc8-209">**파일 탐색기**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-209">Open **File Explorer**.</span></span>

1. <span data-ttu-id="35cc8-210">왼쪽 탐색에서 **이 PC**를 클릭한 후 **Incoming (F:)** 을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-210">In the navigation in the left, click **This PC** and then double-click **Incoming (F:)**.</span></span>

1. <span data-ttu-id="35cc8-211">**홈**, **새 폴더**를 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-211">Select **Home**, and then **New Folder**.</span></span>

1. <span data-ttu-id="35cc8-212">**Drop**을 입력한 후 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-212">Type **Drop** and then press Enter.</span></span>

<span data-ttu-id="35cc8-213">이제 **Incoming**이라는 VHD에 새 볼륨을 만들었고 해당 볼륨에서 **Drop**이라는 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-213">We now have a new volume created on our VHD called **Incoming**, and we've created a folder called **Drop** on that volume.</span></span>  

1. <span data-ttu-id="35cc8-214">Windows 탐색기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-214">Close Windows Explorer.</span></span>

1. <span data-ttu-id="35cc8-215">**작업 표시줄**에서 **시작** 단추를 클릭하고, **전원** 단추를 클릭한 후, **연결 끊기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-215">On the **Task Bar**, click the **Start** button, click the **Power** button, and then click **Disconnect**.</span></span>

<span data-ttu-id="35cc8-216">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-216">Congratulations!</span></span> <span data-ttu-id="35cc8-217">성공적으로 Windows VM을 만들고, 새 VHD를 연결하고, 해당 VHD에 볼륨을 만들고, 해당 볼륨에 폴더를 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-217">You've successfully created a Windows VM, attached a new VHD, created a volume on that VHD and added a folder to that volume.</span></span> <span data-ttu-id="35cc8-218">새 VHD에 사용한 디스크 유형은 **표준 HDD**였습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-218">If you recall, the disk type we used for the new VHD was a **Standard HDD**.</span></span> <span data-ttu-id="35cc8-219">다음 단원에서는 표준 및 프리미엄 저장소 간의 차이점에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35cc8-219">In the next unit, we'll learn the differences between standard and premium storage.</span></span> 
