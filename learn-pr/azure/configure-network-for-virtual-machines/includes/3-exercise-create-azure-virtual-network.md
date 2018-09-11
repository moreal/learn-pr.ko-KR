<span data-ttu-id="6b36c-101">이 연습에서는 Microsoft Azure에서 Virtual Network를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-101">In this exercise, you will create a Virtual Network in Microsoft Azure.</span></span> <span data-ttu-id="6b36c-102">그런 다음, 두 개의 가상 머신을 만들고 가상 네트워크를 사용하여 가상 머신을 서로 또는 인터넷에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-102">You will then create two virtual machines and use the virtual network to connect the virtual machines to each other and to the Internet.</span></span>

<span data-ttu-id="6b36c-103">이 연습을 시작하기 전에 평가판 구독 자격 증명을 사용하여 [Azure Cloud Shell](https://shell.azure.com)에 로그인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-103">Before you begin this exercise, you will need to log into the [Azure Cloud Shell](https://shell.azure.com) with your trial subscription credentials.</span></span> <span data-ttu-id="6b36c-104">Azure Cloud Shell을 사용하여 리소스 그룹, 가상 네트워크 및 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-104">We will use Azure Cloud Shell to create the resource groups, virtual networks, and virtual machines.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="6b36c-105">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="6b36c-105">Create a resource group</span></span>

1. <span data-ttu-id="6b36c-106">**Azure Cloud Shell 시작** 창에서 **PowerShell(Linux)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-106">In the **Welcome to Azure Cloud Shell** window, click **PowerShell (Linux)**.</span></span>

1. <span data-ttu-id="6b36c-107">**탑재된 저장소가 없음** 화면에서 **저장소 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-107">In the **you have no storage mounted** window, click **Create Storage**.</span></span>

1. <span data-ttu-id="6b36c-108">PS Azure:\> 프롬프트에서 다음 코드를 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-108">In the PS Azure:\> prompt, type the following code and press Enter.</span></span>

```PowerShell
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-virtual-network"></a><span data-ttu-id="6b36c-109">Virtual Network 만들기</span><span class="sxs-lookup"><span data-stu-id="6b36c-109">Create a Virtual Network</span></span>

1. <span data-ttu-id="6b36c-110">가상 네트워크를 만들려면 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-110">To create a virtual network, enter the following command and press Enter.</span></span>

```PowerShell
az network vnet create --name myVirtualNetwork --resource-group myResourceGroup --subnet-name default
```

## <a name="create-two-virtual-machines"></a><span data-ttu-id="6b36c-111">두 개의 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="6b36c-111">Create two virtual machines</span></span>

1. <span data-ttu-id="6b36c-112">첫 번째 가상 머신을 만들려면 포트 3389(원격 데스크톱)를 통해 액세스할 수 있는 공용 IP 주소를 사용하여 Windows VM을 만드는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-112">To create the first virtual machine, execute the following command to create a Windows VM with a public IP address that is accessible over port 3389 (Remote Desktop):</span></span>

    ``` PowerShell
    az vm create --name dataProcessingStage1 --resource-group MyResourceGroup --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="6b36c-113">프롬프트에서 암호의 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-113">Supply values for your password at the prompts.</span></span>

1. <span data-ttu-id="6b36c-114">다음 명령을 실행하여 공용 IP 주소 없이 Windows VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-114">Execute the following command to create a Windows VM without a public IP address:</span></span>

    ```PowerShell
    az vm create -n dataProcessingStage2 -g MyResourceGroup --public-ip-address '' --admin-username "DataAdmin"--image Win2016Datacenter
    ```

1. <span data-ttu-id="6b36c-115">작업이 완료되면 두 번째 명령의 출력이 publicIpAddress의 값을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-115">When completed, the output from the second command will return a value for publicIpAddress.</span></span> 

## <a name="connect-to-dataprocessingstage1-using-remote-desktop"></a><span data-ttu-id="6b36c-116">원격 데스크톱을 사용하여 dataProcessingStage1에 연결</span><span class="sxs-lookup"><span data-stu-id="6b36c-116">Connect to dataProcessingStage1 using Remote Desktop</span></span>

1. <span data-ttu-id="6b36c-117">클라이언트 컴퓨터에서 Windows 로고 키를 누르고 RDP를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-117">On your client computer, press the Windows key and type RDP.</span></span>

1. <span data-ttu-id="6b36c-118">**원격 데스크톱 연결** 앱을 선택했는지 확인한 다음, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-118">Ensure that **Remote Desktop Connection** app is selected, then press Enter.</span></span>

1. <span data-ttu-id="6b36c-119">**원격 데스크톱 연결** 대화 상자의 **컴퓨터** 필드에 dataProcessingStage1PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-119">In the **Remote Desktop Connection** dialog box, in the **Computer** field, enter the value of dataProcessingStage1PublicIPAddress, then click **Connect**.</span></span>

1. <span data-ttu-id="6b36c-120">**이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-120">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="6b36c-121">**Windows 보안** 대화 상자에 dataProcessingStage1을 만들 때 사용한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-121">In the **Windows Security** dialog box, enter the User name and password you used when you created dataProcessingStage1</span></span>

1. <span data-ttu-id="6b36c-122">**원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-122">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span>

1. <span data-ttu-id="6b36c-123">Azure에서 원격 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-123">Sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="6b36c-124">**네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-124">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="6b36c-125">서버 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-125">Close Server Manager.</span></span>

1. <span data-ttu-id="6b36c-126">원격 세션에서 Windows 로고 키를 마우스 오른쪽 단추로 클릭하고, **명령 프롬프트**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-126">In the remote session, right-click the Windows Key and click **Command Prompt**.</span></span>

1. <span data-ttu-id="6b36c-127">명령 프롬프트 창에서 다음 명령을 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-127">In the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="6b36c-128">원격 컴퓨터에서 응답이 없어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-128">There should be no response from the remote computer.</span></span> <span data-ttu-id="6b36c-129">기본적으로 Windows 방화벽이 ICMP 응답을 차단하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-129">This is because by default, Windows Firewall prevents ICMP responses.</span></span>

## <a name="connect-to-dataprocessingstage2-using-remote-desktop"></a><span data-ttu-id="6b36c-130">원격 데스크톱을 사용하여 dataProcessingStage2에 연결</span><span class="sxs-lookup"><span data-stu-id="6b36c-130">Connect to dataProcessingStage2 using Remote Desktop</span></span>

1. <span data-ttu-id="6b36c-131">클라이언트 컴퓨터에서 Windows 로고 키를 누르고 **RDP**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-131">On your client computer, press the Windows key and type **RDP**.</span></span> <span data-ttu-id="6b36c-132">**원격 데스크톱 연결** 앱을 선택하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-132">Select the **Remote Desktop Connection** app and press Enter.</span></span>

1. <span data-ttu-id="6b36c-133">**컴퓨터** 필드에 dataProcessingStage2PublicIPAddress 값을 입력한 다음, **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-133">In the **Computer** field, enter the value of dataProcessingStage2PublicIPAddress, then click **Connect**.</span></span>

1. <span data-ttu-id="6b36c-134">**이 원격 연결을 신뢰하십니까?** 대화 상자에서 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-134">In the **Do you trust this remote connection?** dialog box, click **Connect**.</span></span>

1. <span data-ttu-id="6b36c-135">**Windows 보안** 대화 상자에 dataProcessingStage2를 만들 때 사용한 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-135">In the **Windows Security** dialog box, enter the User name and password you used when you created dataProcessingStage2</span></span>

1. <span data-ttu-id="6b36c-136">**원격 데스크톱 연결** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-136">In the **Remote Desktop Connection** dialog box, click **OK**.</span></span> <span data-ttu-id="6b36c-137">이제 Azure에서 원격 컴퓨터에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-137">You now sign in to the remote computer in Azure.</span></span>

1. <span data-ttu-id="6b36c-138">**네트워크** 메시지가 나타나는 경우 **아니요**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-138">When the **Networks** message appears, click **No**.</span></span>

1. <span data-ttu-id="6b36c-139">서버 관리자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-139">Close Server Manager.</span></span>

1. <span data-ttu-id="6b36c-140">dataProcessingStage2에서 Windows 로고 키를 누른 다음, **방화벽**을 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-140">On dataProcessingStage2, press the Windows Key, then type **Firewall**, and press Enter.</span></span> <span data-ttu-id="6b36c-141">**고급 보안이 포함된 Windows 방화벽** 콘솔이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-141">The **Windows Firewall with Advanced Security** console appears.</span></span>

1. <span data-ttu-id="6b36c-142">왼쪽 창에서 **인바운드 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-142">In the left-hand pane, click **Inbound Rules**.</span></span>

1. <span data-ttu-id="6b36c-143">오른쪽 창에서 아래로 스크롤하여 **파일 및 프린터 공유(에코 요청 - ICMPv4-In)** 를 마우스 오른쪽 단추로 클릭한 다음, **규칙 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-143">In the right-hand pane, scroll down and right-click **File and Printer Sharing (Echo Request - ICMPv4-In)**, then click **Enable Rule**.</span></span>

1. <span data-ttu-id="6b36c-144">dataProcessingStage1 콘솔로 다시 전환하고, 명령 프롬프트 창에 다음 명령을 입력하고, Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-144">Switch back to the dataProcessingStage1 console and in the command prompt window, type the following command and press Enter.</span></span>

    ```cmd
    ping dataProcessingStage2 -4
    ```

1. <span data-ttu-id="6b36c-145">dataProcessingStage2는 두 개의 VM 간에 연결을 보여주는 네 개의 회신을 사용하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-145">dataProcessingStage2 responds with four replies, demonstrating connectivity between the two VMs.</span></span>

## <a name="summary"></a><span data-ttu-id="6b36c-146">요약</span><span class="sxs-lookup"><span data-stu-id="6b36c-146">Summary</span></span>

<span data-ttu-id="6b36c-147">성공적으로 vNet을 만들고, 해당 VNet에 연결된 두 개의 VM을 만들고, VM 중 하나에 연결하고, 동일한 vNet 내의 다른 VM에 대한 네트워크 연결을 표시했습니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-147">You have successfully created a vNet, created two VMs that are attached to that VNet, connected to one of the VMs and shown network connectivity to the other VM within the same vNet.</span></span> <span data-ttu-id="6b36c-148">Azure vNet을 사용하여 Azure 네트워크 내에서 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-148">You can use Azure vNets to connect resources within the Azure network.</span></span> <span data-ttu-id="6b36c-149">그러나 이러한 리소스는 동일한 리소스 그룹 및 구독 내에 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-149">However, those resources need to be within the same resource group and subscription.</span></span> <span data-ttu-id="6b36c-150">다음으로, 다른 리소스 그룹, 구독 및 지리적 지역에 있는 vNet에 연결할 수 있도록 하는 VPN Gateway를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b36c-150">Next, we will look at VPN Gateways, which enable you to connect vNets in different resource groups, subscriptions, and even geographical regions.</span></span>
