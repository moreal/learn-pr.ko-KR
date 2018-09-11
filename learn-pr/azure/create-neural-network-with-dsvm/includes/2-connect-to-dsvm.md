### <a name="exercise-2-connect-to-the-data-science-vm"></a><span data-ttu-id="09f99-101">연습 2: Data Science VM에 연결</span><span class="sxs-lookup"><span data-stu-id="09f99-101">Exercise 2: Connect to the Data Science VM</span></span>

<span data-ttu-id="09f99-102">이 연습에서는 이전 연습에서 만든 VM의 Ubuntu 데스크톱에 원격으로 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-102">In this exercise, you will connect remotely to the Ubuntu desktop in the VM that you created in the previous exercise.</span></span> <span data-ttu-id="09f99-103">이를 수행하려면 Linux용 경량 데스크톱 환경인 [Xfce](https://xfce.org/)를 지원하는 클라이언트가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-103">To do so, you need a client that supports [Xfce](https://xfce.org/), which is a lightweight desktop environment for Linux.</span></span> <span data-ttu-id="09f99-104">배경 정보 및 DSVM에 연결할 수 있는 다양한 방법에 대한 개요를 보려면 [Linux용 Data Science Virtual Machine에 액세스하는 방법](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#how-to-access-the-data-science-virtual-machine-for-linux)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="09f99-104">For background, and for an overview of the various ways you can connect to a DSVM, see [How to access the Data Science Virtual Machine for Linux ](https://docs.microsoft.com/en-us/azure/machine-learning/data-science-virtual-machine/dsvm-ubuntu-intro#how-to-access-the-data-science-virtual-machine-for-linux).</span></span>

1. <span data-ttu-id="09f99-105">아직 Xfce 클라이언트가 설치되지 않은 경우 이 연습을 계속하기 전에 [X2Go 클라이언트](https://wiki.x2go.org/doku.php/download:start)를 다운로드한 후 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="09f99-105">If you don't already have an Xfce client installed, download the [X2Go client](https://wiki.x2go.org/doku.php/download:start) and install it before continuing with this exercise.</span></span> <span data-ttu-id="09f99-106">X2Go는 Windows 및 OS X를 비롯한 다양한 운영 체제에서 작동하는 무료 오픈 소스 Xfce 솔루션입니다. 이 연습의 지침에서는 사용자가 X2Go를 사용하고 있다고 가정하지만 Xfce를 지원하는 다른 클라이언트를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-106">X2Go is a free and open-source Xfce solution that works on a variety of operating systems, including Windows and OS X. The instructions in this exercise assume you are using X2Go, but you may use any client that supports Xfce.</span></span>

1. <span data-ttu-id="09f99-107">Azure Portal에서 “data-science-rg” 리소스 그룹으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-107">Return to the "data-science-rg" resource group in the Azure portal.</span></span> <span data-ttu-id="09f99-108">“data-science-vm” 리소스를 클릭하여 포털에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-108">Click the "data-science-vm" resource to open it in the portal.</span></span>

    ![Data Science VM 열기](../images/open-data-science-vm.png)

    <span data-ttu-id="09f99-110">_Data Science VM 열기_</span><span class="sxs-lookup"><span data-stu-id="09f99-110">_Opening the Data Science VM_</span></span>

1. <span data-ttu-id="09f99-111">VM에 대해 표시된 IP 주소 위로 마우스를 가져간 후 나타나는 **복사** 단추를 클릭하여 IP 주소를 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-111">Hover over the IP address shown for the VM and click the **Copy** button that appears to copy the IP address to the clipboard.</span></span>

    ![VM의 IP 주소 복사](../images/copy-ip-address.png)

    <span data-ttu-id="09f99-113">_VM의 IP 주소 복사_</span><span class="sxs-lookup"><span data-stu-id="09f99-113">_Copying the VM's IP address_</span></span>

1. <span data-ttu-id="09f99-114">X2Go 클라이언트를 시작하고 클립보드의 IP 주소와 이전 연습에서 지정한 사용자 이름을 사용하여 Data Science VM에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-114">Start the X2Go client and connect to the Data Science VM using the IP address on the clipboard and the user name you specified in the previous exercise.</span></span> <span data-ttu-id="09f99-115">포트 **22**(SSH 연결에 사용되는 표준 포트)를 통해 연결하고 세션 유형으로 **XFCE**를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-115">Connect via port **22** (the standard port used for SSH connections), and specify **XFCE** as the session type.</span></span> <span data-ttu-id="09f99-116">**확인** 단추를 클릭하여 기본 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-116">Click the **OK** button to confirm your preferences.</span></span>

    ![X2Go를 사용하여 연결](../images/new-session-1.png)

    <span data-ttu-id="09f99-118">_X2Go를 사용하여 연결_</span><span class="sxs-lookup"><span data-stu-id="09f99-118">_Connecting with X2Go_</span></span>

1. <span data-ttu-id="09f99-119">오른쪽의 “새 세션” 패널에서 원격 데스크톱에 사용할 해상도를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-119">In the "New session" panel on the right, select the resolution that you wish to use for the remote desktop.</span></span> <span data-ttu-id="09f99-120">그런 다음, 패널 위쪽의 **새 세션**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-120">Then click **New session** at the top of the panel.</span></span>

    ![새 세션 시작](../images/new-session-2.png)

    <span data-ttu-id="09f99-122">_새 세션 시작_</span><span class="sxs-lookup"><span data-stu-id="09f99-122">_Starting a new session_</span></span>

1. <span data-ttu-id="09f99-123">[연습 1](#Exercise1)에서 지정한 암호를 입력한 다음, **확인** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-123">Enter the password you specified in [Exercise 1](#Exercise1), and then click the **OK** button.</span></span> <span data-ttu-id="09f99-124">호스트 키를 신뢰할 것인지 묻는 메시지가 표시되면 **예**로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-124">If asked if you trust the host key, answer **Yes**.</span></span> <span data-ttu-id="09f99-125">또한 SSH 디먼을 시작할 수 없음을 알려 주는 오류 메시지도 무시합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-125">Also ignore any error messages stating that the SSH daemon could not be started.</span></span>

    ![VM에 로그인](../images/new-session-3.png)

    <span data-ttu-id="09f99-127">_VM에 로그인_</span><span class="sxs-lookup"><span data-stu-id="09f99-127">_Logging into the VM_</span></span>

1. <span data-ttu-id="09f99-128">원격 데스크톱이 표시될 때까지 기다리고 아래와 유사한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-128">Wait for the remote desktop to appear and confirm that it resembles the one below.</span></span>

    > <span data-ttu-id="09f99-129">데스크톱의 텍스트와 아이콘이 너무 크면 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-129">If the text and icons on the desktop are too large, terminate the session.</span></span> <span data-ttu-id="09f99-130">“새 세션” 패널의 오른쪽 아래에 있는 아이콘을 클릭하고 메뉴에서 **세션 기본 설정...** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-130">Click the icon in the lower-right corner of the "New Session" panel and select **Session preferences...** from the menu.</span></span> <span data-ttu-id="09f99-131">“새 세션” 대화 상자의 “입/출력” 탭으로 이동한 후 디스플레이 DPI를 조정하고 새 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-131">Go to the "Input/Output" tab in the "New session" dialog and adjust the display DPI, and then start a new session.</span></span> <span data-ttu-id="09f99-132">96 DPI로 시작하고 필요에 따라 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-132">Start with 96 DPI and adjust as needed.</span></span>

    ![연결됨](../images/ubuntu-desktop.png)

    <span data-ttu-id="09f99-134">_연결됨_</span><span class="sxs-lookup"><span data-stu-id="09f99-134">_Connected!_</span></span>

<span data-ttu-id="09f99-135">이제 연결되었으므로 잠시 데스크톱의 바로 가기를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-135">Now that you are connected, take a moment to explore the shortcuts on the desktop.</span></span> <span data-ttu-id="09f99-136">[Jupyter](http://jupyter.org/), [R Studio](https://www.rstudio.com/) 및 [Microsoft Azure Storage 탐색기](https://azure.microsoft.com/en-us/features/storage-explorer/)를 포함하여 VM에 미리 설치된 다양한 데이터 과학 도구에 대한 바로 가기가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="09f99-136">These are shortcuts to the numerous data-science tools preinstalled in the VM, which include [Jupyter](http://jupyter.org/), [R Studio](https://www.rstudio.com/), and the [Microsoft Azure Storage Explorer](https://azure.microsoft.com/en-us/features/storage-explorer/), among others.</span></span>