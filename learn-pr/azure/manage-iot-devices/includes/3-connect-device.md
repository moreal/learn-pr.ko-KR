<span data-ttu-id="c58fe-101">날씨는 트래픽 패턴부터 소매 매장의 HVAC 시스템이 작동하는 방식까지 모든 것에 영향을 미칠 수 있기 때문에 날씨 데이터를 캡처하는 것은 중요한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-101">Capturing of weather data is an important task as weather can effect everything from traffic patterns to how HVAC systems in retail stores are operated.</span></span> <span data-ttu-id="c58fe-102">이 연습에서는 온라인 Raspberry Pi 시뮬레이터를 활용하여 날씨 데이터를 캡처하고 Azure IoT Hub를 통해 앞서 언급한 데이터를 캡처할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-102">In this exercise, you will be harnessing the online Raspberry Pi simulator to capture simulated weather data and capture said data via the Azure IoT Hub.</span></span>

<span data-ttu-id="c58fe-103">시뮬레이션된 환경에서 이 연습을 수행하는 동안, 시뮬레이션된 장치에서 실행되는 응용 프로그램을 나중에 실제 장치로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-103">While this exercise is being conducted in a simulated environment, the application running on the simulated device can be transferred to a real device in future.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="c58fe-104">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="c58fe-104">Create an IoT hub</span></span>

1. <span data-ttu-id="c58fe-105">[Azure Portal](https://portal.azure.com/)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-105">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>

1. <span data-ttu-id="c58fe-106">**리소스 만들기** \> **사물 인터넷** \> **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-106">Select **Create a resource** \> **Internet of Things** \> **IoT Hub**.</span></span>

![IoT Hub를 탐색하는 Azure Portal 스크린 샷](../media-draft/fa40d1bc51bc4490f657e3c1a8371b5b.png)

1. <span data-ttu-id="c58fe-108">**IoT Hub** 창에서 IoT Hub에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-108">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

 - <span data-ttu-id="c58fe-109">**구독**: 이 IoT Hub를 만드는 데 사용할 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-109">**Subscription**: Choose the subscription that you want to use to create this IoT hub.</span></span>
 - <span data-ttu-id="c58fe-110">**리소스 그룹**: IoT Hub를 호스트할 리소스 그룹을 만들거나 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-110">**Resource group**: Create a resource group to host the IoT hub or use an existing one.</span></span> <span data-ttu-id="c58fe-111">자세한 내용은 [리소스 그룹을 사용하여 Azure 리소스 관리](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fe-111">For more information, see [Use resource groups to manage your Azure resources](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-portal).</span></span>
 - <span data-ttu-id="c58fe-112">**지역**: 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-112">**Region**: Select the closest location to you.</span></span>
 - <span data-ttu-id="c58fe-113">**이름**: IoT Hub의 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-113">**Name**: Create a name for your IoT hub.</span></span> <span data-ttu-id="c58fe-114">입력한 이름을 사용할 수 있으면 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-114">If the name you enter is available, a green check mark appears.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58fe-115">IoT Hub를 DNS 엔드포인트로 공개적으로 검색할 수 있게 되므로 이름을 지정할 때 중요한 정보를 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-115">The IoT hub will be publicly discoverable as a DNS endpoint, so make sure to avoid any sensitive information while naming it.</span></span>

   ![IoT Hub 기본 사항 창](./../media-draft/dbb7319388673b8ee0e0b407536156c0.png)

1.  <span data-ttu-id="c58fe-117">**다음: 크기 및 규모**를 선택하여 IoT Hub를 계속 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-117">Select **Next: Size and scale** to continue creating your IoT hub.</span></span>

1.  <span data-ttu-id="c58fe-118">**가격 책정 및 규모 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-118">Choose your **Pricing and scale tier**.</span></span> <span data-ttu-id="c58fe-119">이 문서의 경우 구독에서 아직 사용할 수 있다면 **F1 - 체험** 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-119">For this article, select the **F1 - Free** tier if it's still available on your subscription.</span></span> <span data-ttu-id="c58fe-120">자세한 내용은 [가격 책정 및 규모 계층](https://azure.microsoft.com/pricing/details/iot-hub/)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fe-120">For more information, see the [Pricing and scale tier](https://azure.microsoft.com/pricing/details/iot-hub/).</span></span>

   ![IoT Hub 크기 및 규모 창](../media-draft/b506eb3293fa4aa9d4785ad498fc476c.png)

1.  <span data-ttu-id="c58fe-122">**검토 + 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-122">Select **Review + create**.</span></span>

1.  <span data-ttu-id="c58fe-123">IoT Hub 정보를 검토한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-123">Review your IoT hub information, then click **Create**.</span></span> <span data-ttu-id="c58fe-124">IoT Hub를 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-124">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="c58fe-125">**알림** 창에서 진행 상황을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-125">You can monitor the progress in the **Notifications** pane.</span></span>

<span data-ttu-id="c58fe-126">IoT 허브를 만들었으니, 장치 및 응용 프로그램을 IoT 허브에 연결하는 데 사용할 중요 정보를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-126">Now that you have created an IoT hub, locate the important information that you use to connect devices and applications to your IoT hub.</span></span>

<span data-ttu-id="c58fe-127">IoT Hub 탐색 메뉴에서 **공유 액세스 정책**을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-127">In your IoT hub navigation menu, open **Shared access policies**.</span></span> <span data-ttu-id="c58fe-128">**iothubowner** 정책을 선택하고, IoT Hub의 **연결 문자열---기본 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-128">Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub.</span></span> <span data-ttu-id="c58fe-129">자세한 내용은 [IoT Hub에 대한 액세스 제어](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c58fe-129">For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).</span></span>

> [!NOTE]
> <span data-ttu-id="c58fe-130">이 설치 자습서에는 이 iothubowner 연결 문자열이 필요 없습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-130">You do not need this iothubowner connection string for this set-up tutorial.</span></span> <span data-ttu-id="c58fe-131">그러나 이 설치를 완료한 후 다른 IoT 시나리오의 일부 자습서에는 필요할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-131">However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.</span></span>

![IoT Hub 연결 문자열 가져오기](../media-draft/a4b41e6ea46ccbef653c411a9829610c.png)

## <a name="register-a-device-in-the-iot-hub-for-your-device"></a><span data-ttu-id="c58fe-133">장치의 IoT Hub에서 장치 등록</span><span class="sxs-lookup"><span data-stu-id="c58fe-133">Register a device in the IoT hub for your device</span></span>
------------------------------------------------

1.  <span data-ttu-id="c58fe-134">IoT Hub 탐색 메뉴에서 **IoT 장치**를 열고 **추가**를 클릭하여 IoT Hub에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-134">In your IoT hub navigation menu, open **IoT devices**, then click **Add** to register a device in your IoT hub.</span></span>

   ![IoT 허브의 IoT 장치에 장치 추가](../media-draft/ee5f177abcf06b86dd007fce3b8448ad.png)

1.  <span data-ttu-id="c58fe-136">새 장치의 **장치 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-136">Enter a **Device ID** for the new device.</span></span> <span data-ttu-id="c58fe-137">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-137">Device IDs are case sensitive.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c58fe-138">고객 지원 및 문제 해결을 위해 수집한 로그에 장치 ID를 표시할 수 있으므로 이름을 지정할 때 중요한 정보를 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-138">The device ID may be visible in the logs collected for customer support and troubleshooting, so make sure to avoid any sensitive information while naming it.</span></span>

1.  <span data-ttu-id="c58fe-139">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-139">Click **Save**.</span></span>

1.  <span data-ttu-id="c58fe-140">장치가 만들어진 후 **IoT 장치** 창의 목록에서 장치를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-140">After the device is created, open the device from the list in the **IoT devices** pane.</span></span>

1.  <span data-ttu-id="c58fe-141">나중에 사용할 수 있도록 **연결 문자열---기본 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-141">Copy the **Connection string---primary key** to use later.</span></span>

   ![장치 연결 문자열 가져오기](../media-draft/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="run-a-sample-application-on-pi-web-simulator"></a><span data-ttu-id="c58fe-143">Pi 웹 시뮬레이터에서 샘플 응용 프로그램 실행</span><span class="sxs-lookup"><span data-stu-id="c58fe-143">Run a sample application on Pi web simulator</span></span>

1. <span data-ttu-id="c58fe-144">코딩 영역에서 기본 샘플 응용 프로그램으로 작업 중인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-144">In coding area, make sure you are working on the default sample application.</span></span> <span data-ttu-id="c58fe-145">15행의 자리 표시자를 Azure IoT Hub 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-145">Replace the placeholder in Line 15 with the Azure IoT hub device connection string.</span></span>

    ![장치 연결 문자열 바꾸기](../media-draft/92ea2c31d42f5b939fb5512e7220e957.png)

2.  <span data-ttu-id="c58fe-147">**실행**을 클릭하거나 npm start를 입력하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-147">Click **Run** or type npm start to run the application.</span></span>

<span data-ttu-id="c58fe-148">IoT Hub로 전송되는 센서 데이터와 메시지를 보여주는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c58fe-148">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub</span></span>

   ![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](../media-draft/96b28d30e317b04347abb0d613738117.png)

<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
