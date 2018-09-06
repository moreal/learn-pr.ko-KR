<span data-ttu-id="204bd-101">이전 시나리오에서는 학생이 Windows Server 컴퓨터에 역할과 기능을 추가하는 방법을 배우고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-101">From our previous scenario, you're now a student and you want to learn about adding roles and features to a Windows Server computer.</span></span> <span data-ttu-id="204bd-102">그러나 네트워크 관리자는 학생이 네트워크의 물리적 컴퓨터에서 이 작업을 수행하는 것을 원하지 않으며, 학교의 컴퓨터가 Windows Hyper-V를 실행하도록 잘못 지정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-102">However, your network administrator doesn't want you to do this on a physical computer on the network, and the school's computers are too poorly specified to run Windows Hyper-V.</span></span> <span data-ttu-id="204bd-103">Azure는 완벽한 솔루션을 제공하므로 클라우드에서 이러한 Windows VM을 호스트하고 Windows RDP(원격 데스크톱 프로토콜)을 사용하여 해당 VM에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-103">Azure provides the perfect solution - we can host these Windows VMs in the cloud and you can access it using Windows Remote Desktop Protocol (RDP).</span></span> <span data-ttu-id="204bd-104">원격 데스크톱 클라이언트를 사용하여 이전 단원에서 만든 Windows VM에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-104">Let's use the Remote Desktop client to connect to the Windows VM that you created in the previous unit.</span></span> <span data-ttu-id="204bd-105">Azure Portal에서 **.RDP** 파일을 다운로드하고 실행하면 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-105">You can connect by downloading and running an **.RDP** file from the Azure portal.</span></span> 

<span data-ttu-id="204bd-106">이 RDP 파일에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-106">This RDP file will have:</span></span>

* <span data-ttu-id="204bd-107">VM의 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="204bd-107">The public IP address of the VM.</span></span>
* <span data-ttu-id="204bd-108">포트 번호</span><span class="sxs-lookup"><span data-stu-id="204bd-108">The port number.</span></span>

## <a name="configure-network-and-public-ip-address-settings"></a><span data-ttu-id="204bd-109">네트워크 및 공용 IP 주소 설정 구성</span><span class="sxs-lookup"><span data-stu-id="204bd-109">Configure network and public IP address settings</span></span>

1. <span data-ttu-id="204bd-110">Azure Portal에서 이전에 만든 가상 머신의 블레이드가 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-110">In the Azure portal, ensure the blade for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="204bd-111">블레이드를 열어야 하는 경우 **모든 리소스** 아래에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-111">You can find the blade under **All Resources** if you need to open it.</span></span>

1. <span data-ttu-id="204bd-112">**네트워킹** 섹션으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-112">Go to the **Networking** section.</span></span> <span data-ttu-id="204bd-113">이 섹션의 맨 위에는 기본값을 사용했기 때문에 VM과 함께 생성된 가상 서브넷 및 동적 IP 주소에 대한 링크가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-113">The top of this section has links to the virtual subnet and dynamic IP address that were created along with our VM since we used the defaults.</span></span> <span data-ttu-id="204bd-114">이러한 리소스를 변경하려는 경우(예: 고정 IP 주소로 변경) 해당 링크를 따릅니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-114">We would follow these links if we wanted to change those resources (for example, changing to a static IP address).</span></span>

1. <span data-ttu-id="204bd-115">**인바운드 포트 규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-115">Click **Add inbound port rule**.</span></span>

1. <span data-ttu-id="204bd-116">**인바운드 보안 규칙 추가** 대화 상자의 맨 위에서 **기본**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-116">At the top of the **Add inbound security rule** dialog box, click **basic**.</span></span>

1. <span data-ttu-id="204bd-117">**서비스** 아래에서 **RDP**를 선택하고 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-117">Under **Service**, select **RDP**, and then click **Add**.</span></span>

## <a name="connect-to-the-vm-by-using-rdp"></a><span data-ttu-id="204bd-118">RDP를 사용하여 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="204bd-118">Connect to the VM by using RDP</span></span>

<span data-ttu-id="204bd-119">RDP 파일을 다운로드하고 VM에 연결하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-119">To download the RDP file and connect to the VM, carry out the following steps.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="204bd-120">RDP 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="204bd-120">Download the RDP file</span></span>

1. <span data-ttu-id="204bd-121">가상 머신 블레이드의 **개요** 섹션에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-121">In the **Overview** section of the virtual machine's blade, click **Connect**.</span></span>

1. <span data-ttu-id="204bd-122">**가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인하고 **RDP 파일 다운로드**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-122">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File**.</span></span>

1. <span data-ttu-id="204bd-123">브라우저에서 **열기** 또는 **실행**을 클릭하여 RDP 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-123">In your browser, click **Open** or **Run** to open the RDP file.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="204bd-124">Windows VM에 연결</span><span class="sxs-lookup"><span data-stu-id="204bd-124">Connect to the Windows VM</span></span>

1. <span data-ttu-id="204bd-125">**원격 데스크톱 연결** 대화 상자에서 보안 경고 및 원격 컴퓨터 IP 주소를 확인하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-125">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="204bd-126">**Windows 보안** 대화 상자에서, 6단계 및 7단계에서 사용한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-126">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="204bd-127">두 번째 **원격 데스크톱 연결** 대화 상자에서 인증서 오류를 확인하고 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-127">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

   > [!Note]
   > <span data-ttu-id="204bd-128">잠시 후에 가상 머신 데스크톱이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-128">The virtual machine desktop takes a while to appear.</span></span> <span data-ttu-id="204bd-129">이 결과는 B1 이미지가 미달 지정되었기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-129">This effect is because the B1 image is under-specified.</span></span> <span data-ttu-id="204bd-130">메모리 할당 부족에 대한 메시지가 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-130">You may receive a message about low memory allocation.</span></span>

1. <span data-ttu-id="204bd-131">**네트워크** 대화 상자에서 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-131">In the **Networks** dialog, click **No**.</span></span>

### <a name="resize-the-vm-in-the-azure-portal"></a><span data-ttu-id="204bd-132">Azure Portal에서 VM 크기 조정</span><span class="sxs-lookup"><span data-stu-id="204bd-132">Resize the VM in the Azure portal</span></span>

1. <span data-ttu-id="204bd-133">Azure Portal로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-133">Switch back to the Azure portal.</span></span> <span data-ttu-id="204bd-134">가상 머신 속성 페이지의 **설정**에서 **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-134">On the virtual machine properties page, under **Settings**, click **Size**.</span></span>

1. <span data-ttu-id="204bd-135">**D2s_v3**(vCPU 2개, 8GB RAM)을 클릭하고 **선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-135">Click **D2s_v3** (2 vCPUs, 8-GB RAM), and then click **Select**.</span></span> <span data-ttu-id="204bd-136">가상 머신 크기 조정 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-136">A resizing virtual machine message will display.</span></span> <span data-ttu-id="204bd-137">또한 RDP 창의 VM이 종료됩니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-137">The VM in the RDP window will also close down.</span></span>

1. <span data-ttu-id="204bd-138">Azure Portal로 다시 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-138">Switch back to the Azure portal.</span></span> <span data-ttu-id="204bd-139">왼쪽 창에서 **가상 머신**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-139">In the left pane, click **Virtual machines**.</span></span>

1. <span data-ttu-id="204bd-140">**가상 머신** 아래에 VM이 **실행 중**상태로 표시될 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-140">Under **Virtual machines**, wait until your VM shows a status of **Running**.</span></span> <span data-ttu-id="204bd-141">**새로 고침**을 클릭해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-141">You may need to click **Refresh**.</span></span>

1. <span data-ttu-id="204bd-142">가상 머신의 이름을 클릭하고 **설정**에서 **크기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-142">Click the virtual machine's name, then in **Settings**, click **Size**.</span></span> <span data-ttu-id="204bd-143">이제 VM 크기가 **D2s_v3**으로 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-143">Note the VM size is now set to **D2s_v3**.</span></span>

### <a name="reconnect-to-the-resized-vm"></a><span data-ttu-id="204bd-144">크기 조정된 VM에 다시 연결</span><span class="sxs-lookup"><span data-stu-id="204bd-144">Reconnect to the resized VM</span></span>

1. <span data-ttu-id="204bd-145">**가상 머신**을 클릭하고 VM을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-145">Click **Virtual machines**, then click your VM.</span></span> <span data-ttu-id="204bd-146">**공용 IP 주소** 값이 변경되었을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-146">Note the **Public IP Address** value has probably changed.</span></span> <span data-ttu-id="204bd-147">브라우저에서 **연결**을 클릭하고 **실행** 또는 **열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-147">Click **Connect**, and then click **Run** or **Open** in your browser.</span></span>

1. <span data-ttu-id="204bd-148">**원격 데스크톱 연결** 대화 상자에서 보안 경고 및 원격 컴퓨터 IP 주소를 확인하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-148">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="204bd-149">**Windows 보안** 대화 상자에서, 6단계 및 7단계에서 사용한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-149">In the **Windows Security** dialog box, enter your user name and password that you used in steps 6 and 7.</span></span>

1. <span data-ttu-id="204bd-150">두 번째 **원격 데스크톱 연결** 대화 상자에서 인증서 오류를 확인하고 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-150">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span> <span data-ttu-id="204bd-151">로그인 프로세스에 대한 가상 머신의 응답성이 얼마나 향상되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-151">Notice how much more responsive the virtual machine is to the sign-in process.</span></span>

1. <span data-ttu-id="204bd-152">작업 표시줄을 마우스 오른쪽 단추로 클릭하고 **작업 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-152">Right-click the taskbar and click **Task Manager**.</span></span>

1. <span data-ttu-id="204bd-153">**작업 관리자** 창에서 **자세한 내용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-153">In the **Task Manager** window, click **More details**.</span></span>

1. <span data-ttu-id="204bd-154">**성능** 탭을 클릭합니다. 사용 가능한 총 메모리는 8GB로, 그중에서 약 1.2GB가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-154">Click the **Performance** tab. Note the total available memory is 8 GB of which about 1.2 GB will be in use.</span></span> <span data-ttu-id="204bd-155">**작업 관리자**를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-155">Close **Task Manager**.</span></span>

## <a name="summary"></a><span data-ttu-id="204bd-156">요약</span><span class="sxs-lookup"><span data-stu-id="204bd-156">Summary</span></span>

<span data-ttu-id="204bd-157">RDP를 사용하여 Windows VM에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-157">You have connected to a Windows VM by using RDP.</span></span> <span data-ttu-id="204bd-158">데스크톱 UI 액세스를 사용하면 Windows 컴퓨터와 마찬가지로 이 VM을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="204bd-158">With Desktop UI access, you can administer this VM as you would any Windows computer.</span></span>
