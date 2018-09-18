<span data-ttu-id="55844-101">이 연습에서는 Microsoft Azure에 가상 네트워크를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55844-101">In this exercise, you will create a virtual network in Microsoft Azure.</span></span> <span data-ttu-id="55844-102">그런 다음, 두 개의 가상 머신을 만들고 가상 네트워크를 사용하여 가상 머신을 서로 연결하고 인터넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-102">You will then create two virtual machines and use the virtual network to connect the virtual machines to each other and to the internet.</span></span>

<span data-ttu-id="55844-103">이 단원을 시작하기 전에 평가판 구독 자격 증명을 사용하여 [Azure Cloud Shell](https://shell.azure.com)에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-103">Before you begin this unit, you will need to log into [Azure Cloud Shell](https://shell.azure.com) with your trial subscription credentials.</span></span> <span data-ttu-id="55844-104">Azure Cloud Shell을 사용하여 리소스 그룹, 가상 네트워크 및 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55844-104">We will use Azure Cloud Shell to create the resource groups, virtual networks, and virtual machines.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="55844-105">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="55844-105">Create a resource group</span></span>

1. <span data-ttu-id="55844-106">**Azure Cloud Shell 시작** 창에서 **PowerShell(Linux)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-106">In the **Welcome to Azure Cloud Shell** window, click **PowerShell (Linux)**.</span></span>

1. <span data-ttu-id="55844-107">**탑재된 저장소가 없음** 창에서 **저장소 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-107">In the **you have no storage mounted** window, click **Create Storage**.</span></span>

1. <span data-ttu-id="55844-108">Azure PowerShell 명령줄 프롬프트에서 다음 코드를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-108">In the Azure PowerShell command-line prompt, type the following code and press Enter.</span></span>

    ```PowerShell
    az group create --name myResourceGroup --location eastus
    ```

## <a name="create-a-virtual-network"></a><span data-ttu-id="55844-109">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="55844-109">Create a virtual network</span></span>

1. <span data-ttu-id="55844-110">가상 네트워크를 만들려면 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-110">To create a virtual network, enter the following command and press Enter.</span></span>

    ```PowerShell
    az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
    ```

## <a name="create-two-virtual-machines"></a><span data-ttu-id="55844-111">두 개의 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="55844-111">Create two virtual machines</span></span>

1. <span data-ttu-id="55844-112">첫 번째 가상 머신을 만들려면 다음 명령을 실행하여 포트 3389(원격 데스크톱)를 통해 액세스할 수 있는 공용 IP 주소가 있는 Windows VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55844-112">To create the first virtual machine, execute the following command to create a Windows VM with a public IP address that is accessible over port 3389 (Remote Desktop):</span></span>

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="55844-113">메시지가 표시되면 암호의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-113">Supply values for your password at the prompts.</span></span>

1. <span data-ttu-id="55844-114">다음 명령을 실행하여 공용 IP 주소 없이 Windows VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="55844-114">Execute the following command to create a Windows VM without a public IP address:</span></span>

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="55844-115">작업이 완료되면 두 번째 명령의 출력에 publicIpAddress의 값이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="55844-115">When completed, the output from the second command will return a value for publicIpAddress.</span></span>

## <a name="connect-to-dataprocessingstage1-using-remote-desktop"></a><span data-ttu-id="55844-116">원격 데스크톱을 사용하여 dataProcessingStage1에 연결</span><span class="sxs-lookup"><span data-stu-id="55844-116">Connect to dataProcessingStage1 using Remote Desktop</span></span>

1. <span data-ttu-id="55844-117">클라이언트 컴퓨터에서 Windows 로고 키를 누르고 RDP를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-117">On your client computer, press the Windows key and type RDP.</span></span>

1. <span data-ttu-id="55844-118">**원격 데스크톱 연결** 앱을 선택했는지 확인한 다음, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-118">Ensure that **Remote Desktop Connection** app is selected, and then press Enter.</span></span>

1. <span data-ttu-id="55844-119">**원격 데스크톱 연결** 대화 상자의 **컴퓨터** 필드에 dataProcessingStage1PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-119">In the **Remote Desktop Connection** dialog box, in the **Computer** field, enter the value of dataProcessingStage1PublicIPAddress, and then click **Connect**.</span></span>

1. <span data-ttu-id="55844-120">**이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-120">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="55844-121">**Windows 보안** 대화 상자에서 dataProcessingStage1을 만들 때 사용한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-121">In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage1.</span></span>

1. <span data-ttu-id="55844-122">**원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-122">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span>

1. <span data-ttu-id="55844-123">Azure에서 원격 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-123">Sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="55844-124">**네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-124">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="55844-125">서버 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="55844-125">Close Server Manager.</span></span>

1. <span data-ttu-id="55844-126">원격 세션에서 Windows 로고 키를 마우스 오른쪽 단추로 클릭하고 **명령 프롬프트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-126">In the remote session, right-click the Windows key and click **Command Prompt**.</span></span>

1. <span data-ttu-id="55844-127">명령 프롬프트 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-127">In the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="55844-128">원격 컴퓨터에서 응답이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-128">There should be no response from the remote computer.</span></span> <span data-ttu-id="55844-129">기본적으로 Windows 방화벽이 ICMP 응답을 차단하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="55844-129">This is because by default, Windows Firewall prevents ICMP responses.</span></span>

## <a name="connect-to-dataprocessingstage2-using-remote-desktop"></a><span data-ttu-id="55844-130">원격 데스크톱을 사용하여 dataProcessingStage2에 연결</span><span class="sxs-lookup"><span data-stu-id="55844-130">Connect to dataProcessingStage2 using Remote Desktop</span></span>

1. <span data-ttu-id="55844-131">클라이언트 컴퓨터에서 Windows 로고 키를 누르고 **RDP**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-131">On your client computer, press the Windows key and type **RDP**.</span></span> <span data-ttu-id="55844-132">**원격 데스크톱 연결** 앱을 선택하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-132">Select the **Remote Desktop Connection** app and press Enter.</span></span>

1. <span data-ttu-id="55844-133">**컴퓨터** 필드에 dataProcessingStage2PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-133">In the **Computer** field, enter the value of dataProcessingStage2PublicIPAddress, and then click **Connect**.</span></span>

1. <span data-ttu-id="55844-134">**이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-134">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="55844-135">**Windows 보안** 대화 상자에서 dataProcessingStage2를 만들 때 사용한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-135">In the **Windows Security** dialog box, enter the user name and password you used when you created dataProcessingStage2.</span></span>

1. <span data-ttu-id="55844-136">**원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-136">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span> <span data-ttu-id="55844-137">이제 Azure에서 원격 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-137">You now sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="55844-138">**네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-138">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="55844-139">서버 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="55844-139">Close Server Manager.</span></span>

1. <span data-ttu-id="55844-140">dataProcessingStage2에서 Windows 로고 키를 누르고, **방화벽**을 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-140">On dataProcessingStage2, press the Windows key, type **Firewall**, and press Enter.</span></span> <span data-ttu-id="55844-141">**고급 보안이 포함된 Windows 방화벽** 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="55844-141">The **Windows Firewall with Advanced Security** console appears.</span></span>

1. <span data-ttu-id="55844-142">왼쪽 창에서 **인바운드 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-142">In the left-hand pane, click **Inbound Rules**.</span></span>

1. <span data-ttu-id="55844-143">오른쪽 창에서 아래로 스크롤하여 **파일 및 프린터 공유(에코 요청 - ICMPv4-In)** 를 마우스 오른쪽 단추로 클릭한 다음, **규칙 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-143">In the right-hand pane, scroll down and right-click **File and Printer Sharing (Echo Request - ICMPv4-In)**, and then click **Enable Rule**.</span></span>

1. <span data-ttu-id="55844-144">dataProcessingStage1 콘솔로 다시 전환한 후, 명령 프롬프트 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="55844-144">Switch back to the dataProcessingStage1 console and in the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="55844-145">dataProcessingStage2는 두 개의 VM 간에 연결을 보여주는 네 개의 회신으로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-145">dataProcessingStage2 responds with four replies, demonstrating connectivity between the two VMs.</span></span>

## <a name="summary"></a><span data-ttu-id="55844-146">요약</span><span class="sxs-lookup"><span data-stu-id="55844-146">Summary</span></span>

<span data-ttu-id="55844-147">성공적으로 가상 네트워크를 만들고, 이 가상 네트워크에 연결된 두 개의 VM을 만들고, VM 중 하나에 연결하고, 동일한 가상 네트워크 내의 다른 VM에 대한 네트워크 연결을 표시했습니다.</span><span class="sxs-lookup"><span data-stu-id="55844-147">You have successfully created a virtual network, created two VMs that are attached to that virtual network, connected to one of the VMs and shown network connectivity to the other VM within the same virtual network.</span></span> <span data-ttu-id="55844-148">Azure Virtual Network를 사용하여 Azure 네트워크 내에서 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="55844-148">You can use Azure Virtual Network to connect resources within the Azure network.</span></span> <span data-ttu-id="55844-149">단, 이러한 리소스는 동일한 리소스 그룹 및 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="55844-149">However, those resources need to be within the same resource group and subscription.</span></span> <span data-ttu-id="55844-150">다음으로, 다양한 리소스 그룹, 구독 및 지리적 지역의 가상 네트워크에 연결할 수 있는 VPN 게이트웨이를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="55844-150">Next, we will look at VPN gateways, which enable you to connect virtual network in different resource groups, subscriptions, and even geographical regions.</span></span>
