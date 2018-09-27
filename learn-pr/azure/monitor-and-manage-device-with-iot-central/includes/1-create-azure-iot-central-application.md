<span data-ttu-id="e1590-101">Azure IoT Central은 글로벌 IoT 자산의 연결, 모니터링 및 관리를 도와주는, 완전히 관리되는 IoT 솔루션입니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-101">Azure IoT Central is a fully managed IoT solution that makes it easy to connect, monitor, and manage your global IoT assets.</span></span>

<span data-ttu-id="e1590-102">여기에서는 원격 커피 머신을 Azure IoT Central에 연결하여 문제를 모니터링하고 관리하는 시나리오를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-102">Here, you'll follow the scenario in which a remote coffee machine is connected to Azure IoT Central for monitoring and management of issues.</span></span> <span data-ttu-id="e1590-103">물 온도와 습도 같은 원격 분석 데이터를 모니터링하고, 머신 상태를 관찰하고, 최적 온도를 설정하고, 보증 상태를 수신하고, 명령을 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-103">You can monitor telemetry such as water temperature and humidity, observe the state of your machine, set optimal temperature, receive warranty status, and send commands.</span></span> <span data-ttu-id="e1590-104">보증 기간이 만료된 커피 머신의 물 온도가 적정 범위를 벗어나면 추가 작업을 수행할 수 있도록 IoT Central의 이메일이 고객의 유지 관리 부서로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-104">If the warranty is expired when the water temperature is outside the expected range, an email from IoT Central is sent to the client’s maintenance department for further action.</span></span>

<span data-ttu-id="e1590-105">먼저 Azure IoT Central에서 IoT 장치와 교환할 수 있는 데이터 및 명령을 정의하는 장치를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-105">You'll begin by a creating a device in Azure IoT Central that defines the data and commands that can be exchanged with the IoT device.</span></span>

<span data-ttu-id="e1590-106">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-106">In this module, you will:</span></span>
  - <span data-ttu-id="e1590-107">Azure IoT Central 사용자 지정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e1590-107">Create an Azure IoT Central custom application</span></span>
  - <span data-ttu-id="e1590-108">장치 템플릿 만들기 및 정의</span><span class="sxs-lookup"><span data-stu-id="e1590-108">Create and define your device template</span></span>
  - <span data-ttu-id="e1590-109">Azure IoT Central에서 응용 프로그램에 커피 머신 시뮬레이터 연결</span><span class="sxs-lookup"><span data-stu-id="e1590-109">Connect a coffee machine simulator to your application in Azure IoT Central</span></span>
  - <span data-ttu-id="e1590-110">연결 및 데이터 흐름의 유효성 검사</span><span class="sxs-lookup"><span data-stu-id="e1590-110">Validate your connection and data flow</span></span>
  - <span data-ttu-id="e1590-111">유지 관리 알림을 전송하도록 규칙 구성</span><span class="sxs-lookup"><span data-stu-id="e1590-111">Configure rules for maintenance notifications</span></span>
 
## <a name="sign-in-to-azure-iot-central"></a><span data-ttu-id="e1590-112">Azure IoT Central 로그인</span><span class="sxs-lookup"><span data-stu-id="e1590-112">Sign in to Azure IoT Central</span></span>
<span data-ttu-id="e1590-113">이 모듈에서는 IoT Central에 로그인하여 새 사용자 지정 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-113">In this unit, you sign in to IoT Central to create a new custom application.</span></span> <span data-ttu-id="e1590-114">7일 평가판이면 이 모듈을 완료하기에 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-114">A 7-day trial is sufficient to complete this module.</span></span> 

1. <span data-ttu-id="e1590-115">Azure IoT Central [응용 프로그램 관리자](https://aka.ms/iotcentral?azure-portal=true) 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-115">Navigate to the Azure IoT Central [Application Manager](https://aka.ms/iotcentral?azure-portal=true) page.</span></span> 

1. <span data-ttu-id="e1590-116">로그인 페이지에서 Microsoft 계정에 액세스하는 데 사용하는 이메일 주소와 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-116">On the sign-in page, enter the email address and password that you use to access your Microsoft account.</span></span>

## <a name="create-a-new-custom-application"></a><span data-ttu-id="e1590-117">새 사용자 지정 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="e1590-117">Create a new custom application</span></span>

1. <span data-ttu-id="e1590-118">새 Azure IoT Central 응용 프로그램을 만들려면 **새 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-118">To create a new Azure IoT Central application, choose **New Application**.</span></span> 

1. <span data-ttu-id="e1590-119">**응용 프로그램 만들기** 페이지에서:</span><span class="sxs-lookup"><span data-stu-id="e1590-119">On the **Create Application** page:</span></span> 
    * <span data-ttu-id="e1590-120">결제 플랜으로 **무료**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-120">Choose **Free** for the payment plan</span></span>
    * <span data-ttu-id="e1590-121">응용 프로그램 템플릿으로 **사용자 지정 응용 프로그램**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-121">Select **Custom Application** as the application template</span></span>
    * <span data-ttu-id="e1590-122">**Coffee Maker 01-A** 같은 친숙한 응용 프로그램 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-122">Choose a friendly application name, like **Coffee Maker 01-A**</span></span>
    * <span data-ttu-id="e1590-123">(선택 사항) URL을 편집합니다. 이 작업은 선택한 이름이 이미 사용 중인 경우에 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-123">(Optionally) edit the URL - this will be required if the name you selected is already in use</span></span>
    * <span data-ttu-id="e1590-124">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e1590-124">Choose **Create**</span></span>