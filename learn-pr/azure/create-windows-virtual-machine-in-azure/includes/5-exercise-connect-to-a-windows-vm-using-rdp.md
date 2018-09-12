<span data-ttu-id="9b005-101">Windows VM을 배포하여 실행하고 있지만 작업을 수행하도록 구성되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-101">We have our Windows VM deployed and running, but it's not configured to do any work.</span></span>

<span data-ttu-id="9b005-102">해당 시나리오는 비디오 처리 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-102">Recall our scenario is a video processing system.</span></span> <span data-ttu-id="9b005-103">해당 플랫폼은 FTP를 통해 파일을 받습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-103">Our platform receives files through FTP.</span></span> <span data-ttu-id="9b005-104">교통 카메라는 서버의 폴더에 매핑되는 알려진 URL에 비디오 클립을 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-104">The traffic cameras upload video clips to a known URL which is mapped to a folder on the server.</span></span> <span data-ttu-id="9b005-105">각 Windows VM에서 사용자 지정 소프트웨어는 서비스로 실행되며, 폴더를 감시하고, 각 업로드된 클립을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-105">The custom software on each Windows VM runs as a service and watches the folder and processes each uploaded clip.</span></span> <span data-ttu-id="9b005-106">그런 다음, 정규화된 비디오를 다른 Azure 서비스에서 실행되는 알고리즘에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-106">It then passes the normalized video to our algorithms running on other Azure services.</span></span>

<span data-ttu-id="9b005-107">이 시나리오를 지원하도록 구성해야 하는 몇 가지 단계가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-107">There are a few things we would need to configure to support this scenario:</span></span>

- <span data-ttu-id="9b005-108">FTP를 설치하고 통신에 필요한 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-108">Install FTP and open the ports it needs to communicate.</span></span>
- <span data-ttu-id="9b005-109">도시의 카메라 시스템에 고유한 전용 비디오 코덱을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-109">Install the proprietary video codec unique to the city's camera system.</span></span>
- <span data-ttu-id="9b005-110">업로드된 비디오를 처리하는 코드 변환 서비스를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-110">Install our transcoding service that processes uploaded videos.</span></span>

<span data-ttu-id="9b005-111">이 중 대부분은 실제로 여기에서 다루지 않으며 소프트웨어를 설치하지 않는 일반적인 관리 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-111">Many of these are typical administrative tasks we won't actually cover here, and we don't have software to install.</span></span> <span data-ttu-id="9b005-112">대신, 단계를 안내하고, 원격 데스크톱을 사용하여 사용자 지정 또는 타사 소프트웨어를 설치_할 수_ 있는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-112">Instead, we will walk through the steps and show you how you _could_ install custom or 3rd party software using Remote Desktop.</span></span> <span data-ttu-id="9b005-113">연결 정보를 가져와서 시작해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-113">Let's start by getting the connection information.</span></span>

## <a name="connect-to-the-vm-with-remote-desktop-protocol"></a><span data-ttu-id="9b005-114">RDP(원격 데스크톱 프로토콜)를 사용하여 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="9b005-114">Connect to the VM with Remote Desktop Protocol</span></span>

<span data-ttu-id="9b005-115">RDP 클라이언트로 Azure VM에 연결하려면 다음 항목이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-115">To connect to an Azure VM with an RDP client, you will need:</span></span>

- <span data-ttu-id="9b005-116">VM의 공용 IP 주소(또는 VM이 사용자 네트워크에 연결하도록 구성된 경우에는 개인 IP 주소).</span><span class="sxs-lookup"><span data-stu-id="9b005-116">The public IP address of the VM (or private if the VM is configured to connect to your network).</span></span>
- <span data-ttu-id="9b005-117">포트 번호.</span><span class="sxs-lookup"><span data-stu-id="9b005-117">The port number.</span></span>

<span data-ttu-id="9b005-118">이 정보를 RDP 클라이언트에 입력하거나 미리 구성된 **RDP** 파일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-118">You can enter this information into the RDP client, or download a pre-configured **RDP** file.</span></span>

### <a name="download-the-rdp-file"></a><span data-ttu-id="9b005-119">RDP 파일 다운로드</span><span class="sxs-lookup"><span data-stu-id="9b005-119">Download the RDP file</span></span>

1. <span data-ttu-id="9b005-120">[Azure Portal](https://portal.azure.com?azure-portal=true)에서 이전에 만든 가상 머신의 **개요** 패널이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-120">In the [Azure portal](https://portal.azure.com?azure-portal=true), ensure the **Overview** panel for the virtual machine that you created earlier is open.</span></span> <span data-ttu-id="9b005-121">VM을 열어야 하는 경우 **모든 리소스** 아래에서 해당 VM을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-121">You can find the VM under **All Resources** if you need to open it.</span></span> <span data-ttu-id="9b005-122">개요 패널에는 VM에 대해 많은 정보가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-122">The overview panel has a lot of information about the VM.</span></span>

    - <span data-ttu-id="9b005-123">VM이 실행 중인지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-123">You can see whether the VM is running.</span></span>
    - <span data-ttu-id="9b005-124">VM을 중지하거나 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-124">Stop or restart it.</span></span>
    - <span data-ttu-id="9b005-125">VM에 연결하기 위한 공용 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-125">Get the public IP address to connect to the VM.</span></span>
    - <span data-ttu-id="9b005-126">CPU, 디스크 및 네트워크의 작업을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-126">See the activity of the CPU, disk, and network.</span></span>

1. <span data-ttu-id="9b005-127">창 위쪽에서 **연결** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-127">Click the **Connect** button at the top of the pane.</span></span>

1. <span data-ttu-id="9b005-128">**가상 머신에 연결** 블레이드에서 **IP 주소** 및 **포트 번호** 설정을 확인하고 **RDP 파일 다운로드**를 클릭한 다음, 사용자 컴퓨터에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-128">In the **Connect to virtual machine** blade, note the **IP address** and **Port number** settings, then click **Download RDP File** and save it to your computer.</span></span>

1. <span data-ttu-id="9b005-129">연결하기 전에 몇 가지 설정을 조정해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-129">Before we connect, let's adjust a few settings.</span></span> <span data-ttu-id="9b005-130">Windows의 탐색기를 사용하여 파일을 찾아 마우스 오른쪽 단추로 클릭하고 **편집**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-130">On Windows, find the file using Explorer, right-click and select **Edit**.</span></span> <span data-ttu-id="9b005-131">MacOS에서 RDP 클라이언트를 사용하여 먼저 파일을 연 다음, 표시된 목록에서 항목을 마우스 오른쪽 단추로 클릭하고 **편집**을 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-131">On MacOS you will need to open the file first with the RDP client and then right-click on the item in the displayed list and select **Edit**.</span></span>

1. <span data-ttu-id="9b005-132">Azure VM의 연결 환경을 제어하려면 다양한 설정을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-132">You can adjust a variety of settings to control the experience in connecting to the Azure VM.</span></span> <span data-ttu-id="9b005-133">검사하려는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-133">The settings you will want to examine are:</span></span>

    - <span data-ttu-id="9b005-134">**표시**: 기본적으로 전체 화면입니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-134">**Display**: By default, it will be full screen.</span></span> <span data-ttu-id="9b005-135">이 화면을 낮은 해상도로 변경하거나 하나를 초과해서 있는 경우 모든 모니터를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-135">You can change this to a lower resolution, or use all your monitors if you have more than one.</span></span>
    - <span data-ttu-id="9b005-136">**로컬 리소스**: VM과 로컬 드라이브를 공유하여 PC에서 VM으로 파일을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-136">**Local Resources**: You can share local drives with the VM - allowing you to copy files from your PC to the VM.</span></span> <span data-ttu-id="9b005-137">**로컬 장치 및 리소스**에서 **자세히** 단추를 클릭하여 공유된 것을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-137">Click the **More** button under **Local devices and resources** to select what is shared.</span></span>
    - <span data-ttu-id="9b005-138">**환경**: 네트워크 품질에 따라 시각적 환경을 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-138">**Experience**: Adjust the visual experience based on your network quality.</span></span>

1. <span data-ttu-id="9b005-139">VM에 표시되도록 로컬 C: 드라이브를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-139">Share your Local C: drive so it will be visible to the VM.</span></span>

1. <span data-ttu-id="9b005-140">변경 내용을 저장하려면 **일반적인** 탭으로 다시 전환하고 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-140">Switch back to the **General** tab and click **Save** to save the changes.</span></span> <span data-ttu-id="9b005-141">언제든 다시 방문하여 나중에 이 파일을 편집해서 다른 설정을 시도해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-141">You can always come back and edit this file later to try other settings.</span></span>

### <a name="connect-to-the-windows-vm"></a><span data-ttu-id="9b005-142">Windows VM에 연결</span><span class="sxs-lookup"><span data-stu-id="9b005-142">Connect to the Windows VM</span></span>

1. <span data-ttu-id="9b005-143">**연결** 단추를 클릭하여 VM에 대한 연결을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-143">Click the **Connect** button to start the connection to the VM.</span></span>

1. <span data-ttu-id="9b005-144">**원격 데스크톱 연결** 대화 상자에서 보안 경고 및 원격 컴퓨터 IP 주소를 확인하고 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-144">In the **Remote Desktop Connection** dialog box, note the security warning and the remote computer IP address, then click **Connect**.</span></span>

1. <span data-ttu-id="9b005-145">**Windows 보안** 대화 상자에서, 6단계 및 7단계에서 사용한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-145">In the **Windows Security** dialog box, enter your username and password that you used in steps 6 and 7.</span></span>
    
    > [!NOTE]
    > <span data-ttu-id="9b005-146">Windows 클라이언트를 사용하여 VM에 연결하는 경우 사용자 머신의 알려진 ID로 초기화됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-146">If you are using a Windows client to connect to the VM, it will default to known identities on your machine.</span></span> <span data-ttu-id="9b005-147">**더 많은 선택** 옵션을 클릭하고 "다른 계정 사용"을 선택하여 다른 사용자 이름/암호 조합을 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-147">You can click the **More choices** option and select "Use a different account" to let you enter a different username/password combination.</span></span>
    
1. <span data-ttu-id="9b005-148">두 번째 **원격 데스크톱 연결** 대화 상자에서 인증서 오류를 확인하고 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-148">In the second **Remote Desktop Connection** dialog box, note the certificate errors, then click **Yes**.</span></span>

### <a name="install-worker-roles"></a><span data-ttu-id="9b005-149">작업자 역할 설치</span><span class="sxs-lookup"><span data-stu-id="9b005-149">Install worker roles</span></span>

<span data-ttu-id="9b005-150">처음으로 Windows 서버 VM에 연결할 경우 서버 관리자가 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-150">The first time you connect to a Windows server VM, it will launch Server Manager.</span></span> <span data-ttu-id="9b005-151">이렇게 하면 일반적인 웹 또는 데이터 작업에 대한 작업자 역할을 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-151">This allows you to assign a worker role for common web or data tasks.</span></span> <span data-ttu-id="9b005-152">시작 메뉴를 통해 서버 관리자를 시작할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-152">You can also launch the Server Manager through the Start Menu.</span></span>

<span data-ttu-id="9b005-153">이 위치에서 서버에 웹 서버 역할을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-153">This is where we would add the Web Server role to the server.</span></span> <span data-ttu-id="9b005-154">이렇게 하면 IIS를 설치하게 되고, 구성의 일부로 HTTP 요청을 해제하고 FTP 서버를 사용하도록 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-154">This will install IIS and as part of the configuration you would turn off HTTP requests and enable the FTP server.</span></span> <span data-ttu-id="9b005-155">그렇지 않으면 IIS를 무시하고 타사 FTP 서버를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-155">Or, we could ignore IIS and install a 3rd party FTP server.</span></span> <span data-ttu-id="9b005-156">그런 다음, VM에 추가한 빅 데이터 드라이브의 폴더에 대한 액세스를 허용하도록 FTP 서버를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-156">We'd then configure the FTP server to allow access to a folder on our big data drive we added to the VM.</span></span>

<span data-ttu-id="9b005-157">실제로 여기에서는 해당 FTP 서버를 구성하지 않으므로 서버 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-157">Since we aren't going to actually configure that here, just close Server Manager.</span></span>

## <a name="install-custom-software"></a><span data-ttu-id="9b005-158">사용자 지정 소프트웨어 설치</span><span class="sxs-lookup"><span data-stu-id="9b005-158">Install custom software</span></span>

<span data-ttu-id="9b005-159">소프트웨어를 설치하는 데 사용할 수 있는 방법이 두 가지 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-159">We have two approaches we can use to install software.</span></span> <span data-ttu-id="9b005-160">먼저, 이 VM을 인터넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-160">First, this VM is connected to the Internet.</span></span> <span data-ttu-id="9b005-161">필요한 소프트웨어에 다운로드할 수 있는 설치 관리자가 있는 경우 RDP 세션에서 웹 브라우저를 열고 소프트웨어를 다운로드하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-161">If the software you need has a downloadable installer, you can open a web browser in the RDP session, download the software, and install it.</span></span> <span data-ttu-id="9b005-162">다음으로, 소프트웨어가 사용자 지정 서비스처럼 사용자 지정인 경우 로컬 머신에서 소프트웨어를 VM에 복사하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-162">Second, if your software is custom - like our custom service, you can copy it from your local machine over to the VM to install it.</span></span> <span data-ttu-id="9b005-163">두 번째 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-163">Let's look at this latter approach.</span></span>

1. <span data-ttu-id="9b005-164">파일 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-164">Open File Explorer.</span></span> <span data-ttu-id="9b005-165">사이드바에서 **이 PC**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-165">Click on **This PC** in the sidebar.</span></span> <span data-ttu-id="9b005-166">여러 드라이브가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-166">You should see several drives:</span></span>

    - <span data-ttu-id="9b005-167">OS를 나타내는 Windows(C:) 드라이브.</span><span class="sxs-lookup"><span data-stu-id="9b005-167">Windows (C:) drive representing the OS.</span></span>
    - <span data-ttu-id="9b005-168">임시 저장소(D:) 드라이브.</span><span class="sxs-lookup"><span data-stu-id="9b005-168">Temporary Storage (D:) drive.</span></span>
    - <span data-ttu-id="9b005-169">로컬 C: 드라이브(아래 표시된 것과 다른 이름이 있습니다).</span><span class="sxs-lookup"><span data-stu-id="9b005-169">Your local C: drive (it will have a different name than shown below).</span></span>

    ![Azure로 공유된 로컬 드라이브](../media-drafts/6-drive-list.png)

<span data-ttu-id="9b005-171">로컬 드라이브에 대한 액세스를 통해 사용자 지정 소프트웨어에 대한 파일을 VM에 복사하고 소프트웨어를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-171">With access to your local drive, you can copy the files for the custom software onto the VM and install the software.</span></span> <span data-ttu-id="9b005-172">시뮬레이션된 시나리오이므로 실제로 해당 작업을 수행하지 않지만 작동 방법을 상상할 수는 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-172">We won't actually do that since it's just a simulated scenario, but you can imagine how it would work.</span></span>

<span data-ttu-id="9b005-173">드라이브 목록에서 주목해야 할 사항은 _누락된_ 드라이브입니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-173">The more interesting thing to observe in the list of drives is what is _missing_.</span></span> <span data-ttu-id="9b005-174">해당 **데이터** 드라이브가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-174">Notice that our **Data** drive is not present.</span></span> <span data-ttu-id="9b005-175">Azure에서 VHD를 추가했지만 초기화하지는 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-175">Azure added a VHD but didn't initialize it.</span></span>

## <a name="initialize-data-disks"></a><span data-ttu-id="9b005-176">데이터 디스크 초기화</span><span class="sxs-lookup"><span data-stu-id="9b005-176">Initialize data disks</span></span>

<span data-ttu-id="9b005-177">처음부터 새로 만드는 모든 추가 드라이브는 초기화하고 포맷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-177">Any additional drives you create from scratch will need to be initialized and formatted.</span></span> <span data-ttu-id="9b005-178">이 과정을 수행하는 프로세스는 실제 드라이브와 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-178">The process for doing this is identical to a physical drive.</span></span>

1. <span data-ttu-id="9b005-179">시작 메뉴에서 **디스크 관리** 도구를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-179">Launch the **Disk Management** tool from the Start Menu.</span></span>

1. <span data-ttu-id="9b005-180">초기화되지 않은 디스크가 감지됐음을 알리는 경고 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-180">It will display a warning that it has detected an uninitialized disk.</span></span>

    ![VM에서 데이터 디스크 초기화](../media-drafts/6-disk-management.png)

1. <span data-ttu-id="9b005-182">**확인**을 클릭하여 디스크를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-182">Click **OK** to initialize the disk.</span></span> <span data-ttu-id="9b005-183">그러면 드라이브를 포맷하고 드라이브 문자를 할당할 수 있는 볼륨 목록에 드라이브가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-183">It will then show up in the list of volumes where you can format it and assign a drive letter.</span></span>

1. <span data-ttu-id="9b005-184">파일 탐색기를 열면 이제 데이터 드라이브가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-184">Open File Explorer and you should now see your data drive.</span></span>

1. <span data-ttu-id="9b005-185">계속해서 RDP 클라이언트를 닫아 VM에서 로그아웃합니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-185">Go ahead and close the RDP client to sign out of the VM.</span></span> <span data-ttu-id="9b005-186">서버는 계속 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-186">The server will continue to run.</span></span>

<span data-ttu-id="9b005-187">RDP를 사용하면 Azure VM을 로컬 컴퓨터처럼 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-187">RDP allows you to work with the Azure VM just like a local computer.</span></span> <span data-ttu-id="9b005-188">데스크톱 UI 액세스를 사용하여 이 VM을 모든 Windows 컴퓨터처럼 관리하면서 소프트웨어를 설치하고, 역할을 구성하고, 기능 및 기타 일상적인 작업을 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-188">With Desktop UI access, you can administer this VM as you would any Windows computer: installing software, configuring roles, adjusting features and other common tasks.</span></span> <span data-ttu-id="9b005-189">단, 이것은 수동 프로세스입니다. 소프트웨어를 항상 설치해야 하는 경우에는 스크립팅을 사용하여 프로세스를 자동화하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b005-189">However, it's a manual process - if we always need to install some software, you might consider automating the process using scripting.</span></span>