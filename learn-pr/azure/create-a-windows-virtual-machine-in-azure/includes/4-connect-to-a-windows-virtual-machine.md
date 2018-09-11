<span data-ttu-id="6d99c-101">데이터 분석 회사의 네트워크 관리자는 Azure의 가상 머신에 연결하여 가상 머신이 제대로 구성되어 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-101">As a network administrator at a data analysis company, you're responsible for connecting to virtual machines in Azure and checking that they're properly configured.</span></span> <span data-ttu-id="6d99c-102">이러한 작업은 원격 데스크톱 프로토콜 클라이언트로 VM의 Windows 데스크톱 UI에 연결하여 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-102">You do that using a Remote Desktop Protocol client to connect to the VM's Windows desktop UI.</span></span>

## <a name="what-is-the-remote-desktop-protocol"></a><span data-ttu-id="6d99c-103">원격 데스크톱 프로토콜이란 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6d99c-103">What is the Remote Desktop Protocol?</span></span>

<span data-ttu-id="6d99c-104">RDP(원격 데스크톱 프로토콜)는 Windows 기반 컴퓨터의 UI에 대한 원격 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-104">Remote Desktop Protocol (RDP) provides remote connectivity to the UI of Windows-based computers.</span></span> <span data-ttu-id="6d99c-105">RDP를 사용하면 물리적 또는 가상 Windows 컴퓨터에 원격으로 로그인하여 마치 콘솔에서 작업하는 것처럼 해당 컴퓨터를 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-105">RDP enables you to sign in to a remote physical or virtual Windows computer and control that computer as if you were seated at the console.</span></span>

> [!Note]
> <span data-ttu-id="6d99c-106">Windows Server 2016 및 Windows 10의 Windows Hyper-V는 RDP를 사용하여 하이퍼바이저에서 실행 중인 가상 머신에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-106">Windows Hyper-V in Windows Server 2016 and Windows 10 uses RDP to connect to virtual machines running on the hypervisor.</span></span>

<span data-ttu-id="6d99c-107">RDP 연결을 사용하면 일부 전원 및 하드웨어 관련 기능을 제외하고는 물리적 컴퓨터의 콘솔에서 수행할 수 있는 작업을 대부분 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-107">An RDP connection enables you to carry out the vast majority of operations that you can do from the console of a physical computer, with the exception of some power and hardware-related functions.</span></span>

<span data-ttu-id="6d99c-108">RDP 연결에는 RDP 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-108">An RDP connection requires an RDP client.</span></span> <span data-ttu-id="6d99c-109">Microsoft는 다음 운영 체제에 대해 RDP 클라이언트를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-109">Microsoft provides RDP clients for the following operating systems:</span></span>

* <span data-ttu-id="6d99c-110">Windows</span><span class="sxs-lookup"><span data-stu-id="6d99c-110">Windows</span></span>
* <span data-ttu-id="6d99c-111">iOS</span><span class="sxs-lookup"><span data-stu-id="6d99c-111">iOS</span></span>
* <span data-ttu-id="6d99c-112">MacOS</span><span class="sxs-lookup"><span data-stu-id="6d99c-112">MacOS</span></span>
* <span data-ttu-id="6d99c-113">Android</span><span class="sxs-lookup"><span data-stu-id="6d99c-113">Android</span></span>

<span data-ttu-id="6d99c-114">Ubuntu 배포에서 Windows PC에 연결할 수 있도록 해주는 Remmina 같은 오픈 소스 Linux 클라이언트도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-114">There are also open-source Linux clients, such as Remmina that enable you to connect to a Windows PC from an Ubuntu distribution.</span></span>

<span data-ttu-id="6d99c-115">Windows 10에는 RDP 클라이언트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-115">Windows 10 includes an RDP client.</span></span>

![Windows RDP 클라이언트](../media-drafts/4-rdp-client.PNG)

## <a name="what-functionality-does-an-rdp-connection-support"></a><span data-ttu-id="6d99c-117">RDP 연결에서 지원하는 기능은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6d99c-117">What functionality does an RDP connection support?</span></span>

<span data-ttu-id="6d99c-118">RDP 연결을 사용하면 UI를 조작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-118">With an RDP connection, you can interact with the UI.</span></span> <span data-ttu-id="6d99c-119">그러나 원격 컴퓨터의 다른 서비스에 연결할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-119">However, you can also connect to other services on the remote computer.</span></span> <span data-ttu-id="6d99c-120">이러한 서비스에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-120">These services include:</span></span>

* <span data-ttu-id="6d99c-121">프린터 연결 - 원격 컴퓨터가 사용자의 로컬 인쇄 장치로 인쇄할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-121">Printer connections that enable the remote computer to print to your local print device.</span></span>
* <span data-ttu-id="6d99c-122">오디오 재생 - 오디오를 로컬 컴퓨터 또는 원격 장치에서 재생할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-122">Audio playback, where audio can play either on the local computer or on the remote device.</span></span>
* <span data-ttu-id="6d99c-123">오디오 녹음 - 로컬 컴퓨터에서 오디오를 녹음하고 해당 소리를 원격 장치로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-123">Audio recording, where you can record audio from the local computer and direct that sound to the remote device.</span></span>
* <span data-ttu-id="6d99c-124">포트 - 로컬 컴퓨터의 포트로 리디렉션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-124">Ports, which you can redirect to the ports on the local computer.</span></span>
* <span data-ttu-id="6d99c-125">드라이브 - 매핑된 네트워크 드라이브를 비롯한 드라이브가 원격 컴퓨터에 연결된 상태로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-125">Drives, including mapped network drives, where the drives will appear as connected to the remote computer.</span></span>
* <span data-ttu-id="6d99c-126">비디오 캡처 장치 - 통합 웹캠 등이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-126">Video capture devices, such as integrated web cams.</span></span>
* <span data-ttu-id="6d99c-127">기타 지원되는 플러그 앤 플레이 장치.</span><span class="sxs-lookup"><span data-stu-id="6d99c-127">Other supported plug and play devices.</span></span>

<span data-ttu-id="6d99c-128">해당 플랫폼에서 사용할 수 있는 물리적 자산에 대한 제한이 있으므로 이러한 기능 중 일부는 Azure에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-128">Not all of these features are supported in Azure, as there are restrictions on what physical assets are available on that platform.</span></span> <span data-ttu-id="6d99c-129">예를 들어 소프트웨어 프린터만 Azure에서 호스트된 VM의 RDP 연결에서 연결 클라이언트의 인쇄 장치로 리디렉션될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-129">For example, only software printers can be redirected across an RDP connection from an Azure-hosted VM to the connecting client's print devices.</span></span>

## <a name="configure-network-settings-for-rdp-access-to-virtual-machines"></a><span data-ttu-id="6d99c-130">가상 머신에 대한 RDP 액세스를 위한 네트워크 설정 구성</span><span class="sxs-lookup"><span data-stu-id="6d99c-130">Configure network settings for RDP access to virtual machines</span></span>

<span data-ttu-id="6d99c-131">Azure VM에 대한 연결을 설정하는 방법은 다음 세 가지입니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-131">Connections to Azure VMs can be made in three ways:</span></span>

1. <span data-ttu-id="6d99c-132">VM의 공용 IP 주소로 직접 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-132">Directly to the public IP address of the VM.</span></span>
2. <span data-ttu-id="6d99c-133">VPN(가상 사설망) 연결을 통해 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-133">Through a virtual private network (VPN) connection.</span></span>
3. <span data-ttu-id="6d99c-134">ExpressRoute 연결을 통해 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-134">Through an ExpressRoute connection.</span></span>

<span data-ttu-id="6d99c-135">공용 IP 주소는 영구적으로 할당될 수도 있고 동적일 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-135">A public IP address can be either permanently allocated or dynamic.</span></span> <span data-ttu-id="6d99c-136">포트 3389(RDP)에서 VM의 공용 주소에 액세스할 수 있는지도 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-136">You also need to ensure that you have access to the VM's public address on port 3389 (RDP).</span></span> <span data-ttu-id="6d99c-137">이 프로비전에서는 조직의 방화벽 보안을 관리하는 팀과 협의하여 포트 3389에서 해당 VM의 공용 IP 주소에 대한 규칙을 설정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-137">This provision may require negotiation with the team that's managing your organization's firewall security, setting up a rule to your VM's public IP address on port 3389.</span></span>

<span data-ttu-id="6d99c-138">동적 공용 IP 주소는 VM이 다시 시작될 때마다 다시 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-138">Dynamic public IP addresses are reallocated every time the VM restarts.</span></span> <span data-ttu-id="6d99c-139">정적 주소는 영구적이지만 비용이 더 많이 듭니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-139">Static addresses are persistent, but cost more.</span></span>

<span data-ttu-id="6d99c-140">VPN을 통해 연결하려면 로컬 네트워크에 Microsoft Azure에 대한 활성 VPN 연결이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-140">To connect through a VPN, your local network must have an active VPN connection to Microsoft Azure.</span></span>

<span data-ttu-id="6d99c-141">ExpressRoute 연결 방식은 VM에 대한 연결을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-141">The ExpressRoute link approach manages connectivity to the VM.</span></span> <span data-ttu-id="6d99c-142">이 방식은 또한 대기 시간은 가장 짧고 대역폭 연결은 가장 높습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-142">This approach also provides the lowest latency and highest bandwidth connection.</span></span>

> [!Note]
> <span data-ttu-id="6d99c-143">Azure에 연결하는 데 사용하는 옵션과 관계없이 일반적으로 기본 포트 3389에서 RDP를 통해 가상 머신에 액세스할 수 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-143">Regardless of which option you use to connect to Azure, you need to ensure the virtual machine is accessible over RDP, typically on the default port 3389.</span></span> <span data-ttu-id="6d99c-144">자체 클라이언트 IP 주소에서만 VM에 액세스할 수 있도록 VM을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-144">You can configure the VM so it can be accessed only from your own client IP address.</span></span> <span data-ttu-id="6d99c-145">공용 IP 주소에서 포트 3389를 통해 VM에 연결하는 방법은 테스트 환경에서만 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-145">Connecting to a VM over port 3389 on a public IP address is only recommended for test environments.</span></span> <span data-ttu-id="6d99c-146">프로덕션 환경에서는 두 번째 또는 세 번째 옵션을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="6d99c-146">In production environments, use option 2 or 3.</span></span>

## <a name="how-do-you-connect-to-a-vm-in-azure-using-rdp"></a><span data-ttu-id="6d99c-147">Azure에서 RDP를 사용하여 VM에 연결하는 방법은 무엇인가요?</span><span class="sxs-lookup"><span data-stu-id="6d99c-147">How do you connect to a VM in Azure using RDP?</span></span>

<span data-ttu-id="6d99c-148">Azure에서 RDP를 사용하여 VM에 연결하는 작업은 간단한 프로세스입니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-148">Connecting to a VM in Azure using RDP is a simple process.</span></span> <span data-ttu-id="6d99c-149">Azure Portal에서 VM 속성으로 이동하여 맨 위에 있는 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-149">In the Azure portal, you go to the properties of your VM, and at the top, click **Connect**.</span></span> <span data-ttu-id="6d99c-150">이렇게 하면 사전 구성된 .RDP 파일을 다운로드하며 Windows는 해당 파일을 RDP 클라이언트에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-150">This action downloads a preconfigured .RDP file that Windows then opens in the RDP client.</span></span> <span data-ttu-id="6d99c-151">RDP 파일에서 VM의 공용 IP 주소를 통해 연결하도록 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-151">You can choose to connect over the public IP address of the VM in the RDP file.</span></span> <span data-ttu-id="6d99c-152">VPN 또는 ExpressRoute를 통해 연결하는 경우에는 내부 IP 주소를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-152">Alternatively, if you're connecting over VPN or ExpressRoute, you can select the internal IP address.</span></span> <span data-ttu-id="6d99c-153">연결할 포트 번호도 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-153">You can also select the port number for the connection.</span></span>

<span data-ttu-id="6d99c-154">VM의 정적 공용 IP 주소를 사용하는 경우 .RDP 파일을 데스크톱에 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-154">If you're using a static public IP address for the VM, you can save the .RDP file to your desktop.</span></span> <span data-ttu-id="6d99c-155">동적 IP 주소를 사용하는 경우에는 VM이 실행 중인 동안에만 .RDP 파일이 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-155">If you're using dynamic IP addressing, the .RDP file only remains valid while the VM is running.</span></span> <span data-ttu-id="6d99c-156">VM을 중지했다가 다시 시작하는 경우 다른 .RDP 파일을 다운로드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-156">If you stop and restart the VM, you must download another .RDP file.</span></span>

> [!Note]
> <span data-ttu-id="6d99c-157">VM의 공용 IP 주소를 Windows RDP 클라이언트에 입력하고 **연결**을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-157">You can also enter the public IP address of the VM into the Windows RDP client and click **Connect**.</span></span>

<span data-ttu-id="6d99c-158">연결하는 경우 일반적으로 두 개의 경고를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-158">When you connect, you will typically receive two warnings.</span></span> <span data-ttu-id="6d99c-159">다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-159">These are:</span></span>

* <span data-ttu-id="6d99c-160">게시자 경고 - 공개적으로 서명되지 않은 .RDP 파일 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-160">Publisher warning - caused by the .RDP file not being publicly signed.</span></span>
* <span data-ttu-id="6d99c-161">인증서 경고 - 신뢰할 수 없는 머신 인증서 때문에 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-161">Certificate warning - caused by the machine certificate not being trusted.</span></span>

<span data-ttu-id="6d99c-162">테스트 환경에서는 이러한 경고를 무시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-162">In test environments, these warnings can be ignored.</span></span> <span data-ttu-id="6d99c-163">프로덕션 환경에서는 RDPSIGN.EXE를 사용하여 .RDP 파일에 서명하고 클라이언트의 **신뢰할 수 있는 루트 인증 기관** 저장소에 머신 인증서를 배치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-163">In production environments, the .RDP file could be signed using RDPSIGN.EXE and the machine certificate placed in the client's **Trusted Root Certification Authorities** store.</span></span>

## <a name="summary"></a><span data-ttu-id="6d99c-164">요약</span><span class="sxs-lookup"><span data-stu-id="6d99c-164">Summary</span></span>

<span data-ttu-id="6d99c-165">이제 RDP를 사용하여 Windows VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-165">Now you can connect to a Windows VM by using RDP.</span></span> <span data-ttu-id="6d99c-166">다음 연습에서는 RDP를 사용하여 VM에 연결한 후에 해당 컴퓨터에 서버 역할을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="6d99c-166">In the following exercise, you will use RDP to connect to a VM, then install a server role on that computer.</span></span>
