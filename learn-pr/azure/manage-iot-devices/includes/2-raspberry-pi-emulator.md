<span data-ttu-id="a89b0-101">Raspberry Pi 보드는 최근에 이론 테스트용으로 또는 멋진 작업을 수행하는 용도로 관심을 끌고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-101">Raspberry Pi boards have garnered much interest of late for testing theories or event making cool things.</span></span> <span data-ttu-id="a89b0-102">이 보드의 비용은 상당히 저렴하지만, 구매 전에 Raspberry Pi 기능을 테스트하고 싶은 분들도 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-102">While the cost on this boards are quite low, some may be interested in testing out the Raspberry Pi functionality before investing in one.</span></span>

<span data-ttu-id="a89b0-103">Microsoft는 사용자가 코드를 통해 에뮬레이트된 하드웨어를 제어할 수 있는 온라인 Raspberry Pi 시뮬레이터를 개발했습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-103">Microsoft has built an online Raspberry Pi simulator allowing users to control the emulated hardware via code.</span></span> <span data-ttu-id="a89b0-104">에뮬레이터는 회로를 서로 유선으로 연결할 수 있는 실험용 회로판을 통해 온도, 습도, 압력 센서와 연결된 Raspberry Pi의 그래픽과 빨간색 LED를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-104">The emulator portrays a graphic of a Raspberry Pi connected to a temperature, humidity, pressure sensor, and a red LED via breadboard allowing circuits to be wired together.</span></span> <span data-ttu-id="a89b0-105">표시된 측면 패널을 통해 사용자는 LED를 제어하고 시뮬레이트된 센서에서 더미 데이터를 수집하는 Node.js JavaScript 코드를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-105">The displayed side panel allows users to enter Node.js JavaScript code to control the LED and collect dummy data from the simulated sensor.</span></span>

<span data-ttu-id="a89b0-106">시뮬레이터를 처음으로 실행하면 시뮬레이터는 명령줄을 통해 표시되는 온도 캡처 프로그램 샘플이 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-106">At first run, the simulator operates a sample temperature capture program which is displayed via the command line.</span></span> <span data-ttu-id="a89b0-107">시뮬레이터는 사람이 코드를 테스트한 후 실제 장치에 전송할 수 있도록 설계되었기 때문에 동일한 샘플 응용 프로그램을 실제 Pi에서 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-107">The same sample application can also be run on a real Pi as the simulator is designed to allow people to test code before transferring it to a real device.</span></span>

## <a name="web-simulator"></a><span data-ttu-id="a89b0-108">웹 시뮬레이터</span><span class="sxs-lookup"><span data-stu-id="a89b0-108">Web simulator</span></span>

<span data-ttu-id="a89b0-109">웹 시뮬레이터에는 세 가지 영역이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-109">There are three areas in the web simulator:</span></span>

1.  <span data-ttu-id="a89b0-110">어셈블리 영역 - 기본 회로에서는 Pi가 BME280 센서 및 LED에 연결됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-110">Assembly area - The default circuit is that a Pi connects with a BME280 sensor and an LED.</span></span> <span data-ttu-id="a89b0-111">미리 보기 버전에서는 이 영역이 잠겨 있으므로 지금은 사용자 지정을 수행할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-111">The area is locked in preview version so currently you cannot do customization.</span></span>

2.  <span data-ttu-id="a89b0-112">코딩 영역 - Raspberry Pi를 사용하여 코딩할 수 있는 온라인 코드 편집기입니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-112">Coding area - An online code editor for you to code with Raspberry Pi.</span></span> <span data-ttu-id="a89b0-113">기본 샘플 응용 프로그램을 사용하여 BME280 센서에서 센서 데이터를 손쉽게 수집한 후 Azure IoT Hub로 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-113">The default sample application helps to collect sensor data from BME280 sensor and sends to your Azure IoT Hub.</span></span> <span data-ttu-id="a89b0-114">응용 프로그램은 실제 Pi 장치와 완벽하게 호환됩니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-114">The application is fully compatible with real Pi devices.</span></span>

3.  <span data-ttu-id="a89b0-115">통합 콘솔 창 - 코드의 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-115">Integrated console window - It shows the output of your code.</span></span> <span data-ttu-id="a89b0-116">이 창의 맨 위에는 세 개의 단추가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-116">At the top of this window, there are three buttons.</span></span>

    -   <span data-ttu-id="a89b0-117">**실행** - 코딩 영역에서 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-117">**Run** - Run the application in the coding area.</span></span>

    -   <span data-ttu-id="a89b0-118">**다시 설정** - 기본 샘플 응용 프로그램으로 코딩 영역을 다시 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-118">**Reset** - Reset the coding area to the default sample application.</span></span>

    -   <span data-ttu-id="a89b0-119">**접기/확장** - 오른쪽에 있는 단추를 사용하여 콘솔 창 접기/확장을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a89b0-119">**Fold/Expand** - On the right side there is a button for you to fold/expand the console window.</span></span>

[<span data-ttu-id="a89b0-120">Pi 온라인 시뮬레이터의 개요 이미지</span><span class="sxs-lookup"><span data-stu-id="a89b0-120">Overview image of Pi online simulator</span></span>](./../media-draft/image1.png)

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>

-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->

