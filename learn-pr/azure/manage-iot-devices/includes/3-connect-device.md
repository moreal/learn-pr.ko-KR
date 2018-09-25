<span data-ttu-id="6b9e7-101">날씨는 트래픽 패턴부터 소매 매장의 HVAC(난방, 환기, 공기 조절) 시스템이 작동하는 방식까지 모든 것에 영향을 미칠 수 있기 때문에 날씨 데이터를 캡처하는 것은 중요한 작업입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-101">Capturing of weather data is an important task as weather can effect everything from traffic patterns to how heating, ventilation, and air conditioning (HVAC) systems in retail stores are operated.</span></span> <span data-ttu-id="6b9e7-102">이 연습에서는 앞의 단원에서 알아본 온라인 Raspberry Pi 시뮬레이터와 상호 작용하여 Azure IoT Hub를 통해 시물레이션된 날씨 데이터를 캡처할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-102">In this exercise, you will be interacting with the online Raspberry Pi simulator you learned about in the previous unit to capture simulated weather data and via the Azure IoT Hub.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="6b9e7-103">시뮬레이션된 환경에서 이 연습을 수행하는 동안, 시뮬레이션된 장치에서 실행되는 응용 프로그램을 나중에 실제 장치로 전송할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-103">While this exercise is being conducted in a simulated environment, the application running on the simulated device can be transferred to a real device in the future.</span></span>

## <a name="create-an-iot-hub"></a><span data-ttu-id="6b9e7-104">IoT Hub 만들기</span><span class="sxs-lookup"><span data-stu-id="6b9e7-104">Create an IoT hub</span></span>
<span data-ttu-id="6b9e7-105">Azure IoT Hub는 장치 및 백 엔드 개발자가 강력한 장치 관리 솔루션을 빌드할 수 있도록 하는 기능 및 확장성 모델을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-105">Azure IoT Hub provides the features and an extensibility model that enable device and back-end developers to build robust device management solutions.</span></span> <span data-ttu-id="6b9e7-106">장치의 범위는 제한된 센서 및 단일 목적 마이크로컨트롤러에서 다수의 장치에 대한 통신을 라우팅하는 강력한 게이트웨이까지를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-106">Devices range from constrained sensors and single purpose microcontrollers, to powerful gateways that route communications for groups of devices.</span></span> <span data-ttu-id="6b9e7-107">또한 IoT 운영자의 사용 사례 및 요구 사항은 여러 산업에 따라 크게 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-107">In addition, the use cases and requirements for IoT operators vary significantly across industries.</span></span> <span data-ttu-id="6b9e7-108">이 변형에도 불구하고 IoT Hub 장치 관리는 기능, 패턴 및 코드 라이브러리를 다양한 장치 및 최종 사용자에게 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-108">Despite this variation, device management with IoT Hub provides the capabilities, patterns, and code libraries to cater to a diverse set of devices and end users.</span></span>

<span data-ttu-id="6b9e7-109">Raspberry Pi 시뮬레이터에서 데이터를 수집하기 시작하기 위해 먼저 IoT Hub를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-109">In order to start collecting the data from the Raspberry Pi simulator, you need to first create an IoT hub.</span></span>

1. <span data-ttu-id="6b9e7-110">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-110">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

2. <span data-ttu-id="6b9e7-111">Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-111">Choose **Create a resource** in the upper left-hand corner of the Azure portal.</span></span>

3. <span data-ttu-id="6b9e7-112">**사물 인터넷**을 선택한 다음, **IoT Hub**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-112">Select **Internet of Things**, and then select **IoT Hub**.</span></span>

![IoT Hub를 탐색하는 Azure Portal의 스크린샷](../media/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. <span data-ttu-id="6b9e7-114">**IoT Hub** 창에서 IoT Hub에 다음 정보를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-114">In the **IoT hub** pane, enter the following information for your IoT hub:</span></span>

   - <span data-ttu-id="6b9e7-115">**구독**: 이 예제에 대해 기본 구독을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-115">**Subscription**: Use the default subscription for this example.</span></span>
   - <span data-ttu-id="6b9e7-116">**리소스 그룹**: 기존 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-116">**Resource group**: Use the existing resource group.</span></span> <span data-ttu-id="6b9e7-117">모든 관련 리소스를 동일한 그룹에 배치하여 다 함께 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-117">By putting all related resources in the same group you can manage them all together.</span></span> <span data-ttu-id="6b9e7-118">예를 들어 리소스 그룹을 삭제하면 해당 그룹에 들어 있는 모든 리소스가 삭제됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-118">For example, deleting the resource group deletes all resources contained in that group.</span></span>
   - <span data-ttu-id="6b9e7-119">**이름**: IoT Hub에 대한 고유한 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-119">**Name**: Create a unique name for your IoT hub.</span></span> <span data-ttu-id="6b9e7-120">입력한 이름을 사용할 수 있으면 녹색 확인 표시가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-120">If the name you enter is available, a green check mark appears.</span></span>
   - <span data-ttu-id="6b9e7-121">**지역**: 다음 목록 중 사용자에게 가장 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-121">**Region**: Select the closest location to you from the following list.</span></span>

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    > [!IMPORTANT]
    > <span data-ttu-id="6b9e7-122">IoT Hub에서는 DNS 엔드포인트로 공개적으로 검색할 수 있으므로 이름을 지정할 때 중요한 정보를 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-122">The IoT hub will be publicly discoverable as a DNS endpoint, so make sure to avoid any sensitive information while naming it.</span></span>

    ![IoT Hub 기본 사항 창](./../media/dbb7319388673b8ee0e0b407536156c0.png)

1. <span data-ttu-id="6b9e7-124">**다음: 크기 및 규모**를 선택하여 IoT Hub를 계속 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-124">Select **Next: Size and scale** to continue creating your IoT hub.</span></span>
2. <span data-ttu-id="6b9e7-125">**가격 책정 및 규모 계층**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-125">Choose your **Pricing and scale tier**.</span></span> <span data-ttu-id="6b9e7-126">이 예제의 경우 **F1 - 무료** 계층을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-126">For this example, select the **F1 - Free** tier.</span></span>

    ![IoT Hub 크기 및 규모 창](../media/b506eb3293fa4aa9d4785ad498fc476c.png)

3. <span data-ttu-id="6b9e7-128">**검토 + 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-128">Select **Review + create**.</span></span>

4. <span data-ttu-id="6b9e7-129">IoT Hub 정보를 검토한 다음, **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-129">Review your IoT hub information, then click **Create**.</span></span> <span data-ttu-id="6b9e7-130">IoT Hub를 만드는 데 몇 분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-130">Your IoT hub might take a few minutes to create.</span></span> <span data-ttu-id="6b9e7-131">**알림** 창에서 진행 상황을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-131">You can monitor the progress in the **Notifications** pane.</span></span>

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up exercise. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a><span data-ttu-id="6b9e7-132">장치 등록</span><span class="sxs-lookup"><span data-stu-id="6b9e7-132">Register a device</span></span>
<span data-ttu-id="6b9e7-133">연결하기 전에 장치를 IoT Hub에 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-133">A device must be registered with your IoT hub before it can connect.</span></span>

1. <span data-ttu-id="6b9e7-134">IoT Hub 탐색 메뉴에서 **IoT 장치**를 연 다음, **추가**를 클릭하여 IoT Hub에 장치를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-134">In your IoT hub navigation menu, open **IoT devices**, then click **Add** to register a device in your IoT hub.</span></span>

   ![IoT 허브의 IoT 장치에 장치 추가](../media/ee5f177abcf06b86dd007fce3b8448ad.png)

2. <span data-ttu-id="6b9e7-136">새 장치의 **장치 ID**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-136">Enter a **Device ID** for the new device.</span></span> <span data-ttu-id="6b9e7-137">장치 ID는 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-137">Device IDs are case sensitive.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="6b9e7-138">고객 지원 및 문제 해결을 위해 수집한 로그에 장치 ID를 표시할 수 있으므로 이름을 지정할 때 중요한 정보를 사용하면 안 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-138">The device ID may be visible in the logs collected for customer support and troubleshooting, so make sure to avoid any sensitive information while naming it.</span></span>

3. <span data-ttu-id="6b9e7-139">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-139">Click **Save**.</span></span>
4. <span data-ttu-id="6b9e7-140">장치가 만들어진 후 **IoT 장치** 창의 목록에서 장치를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-140">After the device is created, open the device from the list in the **IoT devices** pane.</span></span>
5. <span data-ttu-id="6b9e7-141">나중에 사용할 수 있도록 **연결 문자열---기본 키**를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-141">Copy the **Connection string---primary key** to use later.</span></span>

   ![장치 연결 문자열 가져오기](../media/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a><span data-ttu-id="6b9e7-143">시뮬레이션된 원격 분석 보내기</span><span class="sxs-lookup"><span data-stu-id="6b9e7-143">Send simulated telemetry</span></span>

1. <span data-ttu-id="6b9e7-144">[Azure IoT Raspberry Pi 시뮬레이터](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true)를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-144">Open the [Raspberry Pi Azure IoT Simulator](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true).</span></span>
1. <span data-ttu-id="6b9e7-145">15행의 자리 표시자를 방금 복사한 Azure IoT Hub 장치 연결 문자열로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-145">Replace the placeholder in Line 15 with the Azure IoT hub device connection string you just copied.</span></span>
1. <span data-ttu-id="6b9e7-146">콘솔 창에서 `Run` 단추 또는 `npm start` 형식을 클릭하여 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-146">Click the `Run` button or type `npm start` in the console window to run the application.</span></span>

    ![장치 연결 문자열 바꾸기](../media/Line15.png)

1. <span data-ttu-id="6b9e7-148">IoT Hub로 전송되는 센서 데이터와 메시지를 보여주는 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-148">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

    ![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](../media/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a><span data-ttu-id="6b9e7-150">허브에서 원격 분석 읽기</span><span class="sxs-lookup"><span data-stu-id="6b9e7-150">Read the telemetry from your hub</span></span>
<span data-ttu-id="6b9e7-151">그러면 어떻게 되나요?</span><span class="sxs-lookup"><span data-stu-id="6b9e7-151">So what's happening?</span></span> <span data-ttu-id="6b9e7-152">IoT Hub는 시뮬레이션된 장치에서 전송된 장치-클라우드 메시지를 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-152">IoT hub is receiving the device-to-cloud messages sent from the simulated device.</span></span> <span data-ttu-id="6b9e7-153">확인하기 위해 Azure IoT Hub에서 들어오는 데이터를 처리하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-153">In order to see that, let's take a quick look at how Azure IoT Hub is processing the incoming data.</span></span> <span data-ttu-id="6b9e7-154">IoT Hub의 **모니터링**에서 **메트릭**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-154">In your IoT Hub, under **Monitoring**, select **Metrics**.</span></span> <span data-ttu-id="6b9e7-155">데이터가 그림에 배치되기를 기다리기 위해 잠시 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="6b9e7-155">Give it a few minutes as you wait for the data to come into the picture.</span></span>

![IoT Hub 메트릭](../media/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
