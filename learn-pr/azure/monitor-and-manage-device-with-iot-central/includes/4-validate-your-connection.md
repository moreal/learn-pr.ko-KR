<span data-ttu-id="c72ad-101">이제 Azure IoT Central 응용 프로그램을 사용하여 커피 머신을 Azure IoT Central에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-101">You’ve now worked with the Azure IoT Central application and connected the coffee machine to Azure IoT Central.</span></span> <span data-ttu-id="c72ad-102">따라서 원격 커피 머신을 모니터링하고 관리를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-102">You are well on your way to begin to monitor and manage your remote coffee machine.</span></span> <span data-ttu-id="c72ad-103">이 모듈에서는 앞에서 정의한 연결된 커피 메이커 템플릿을 사용하여 설정과 연결의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-103">In this unit, you take a moment to validate your setup and connection by using the Connected Coffee Maker template that you defined earlier.</span></span> <span data-ttu-id="c72ad-104">설정에서 최적의 온도를 업데이트하고, 머신 상태를 확인하는 명령을 실행하고, 대시보드에서 연결된 커피 머신을 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-104">You update the optimal temperature in settings, run commands to check for the state of your machine, and view your connected coffee machine in the dashboard.</span></span> 

## <a name="update-settings-to-sync-your-application-with-the-coffee-machine"></a><span data-ttu-id="c72ad-105">응용 프로그램이 커피 머신과 동기화되도록 설정 업데이트</span><span class="sxs-lookup"><span data-stu-id="c72ad-105">Update settings to sync your application with the coffee machine</span></span>

<span data-ttu-id="c72ad-106">**설정** 페이지에서 응용 프로그램의 구성 데이터를 커피 머신으로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-106">On the **Settings** page, you send configuration data to the coffee machine from your application.</span></span> 

<span data-ttu-id="c72ad-107">이 시나리오에서는 최적 온도를 변경하고 **업데이트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-107">In this scenario, change the optimal temperature and choose **Update**.</span></span> <span data-ttu-id="c72ad-108">변경된 설정은 커피 머신이 설정 변경에 응답했음을 승인할 때까지 UI에서 보류 중으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-108">When the setting is changed, the setting is marked as pending in the UI until the coffee machine acknowledges that it has responded to the setting change.</span></span> 

> [!NOTE]
> <span data-ttu-id="c72ad-109">설정이 정상적으로 업데이트되면 데이터 흐름을 나타내고 연결 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-109">Successful updates in the setting indicate data flow and validate your  connection.</span></span> <span data-ttu-id="c72ad-110">그러면 원격 분석 측정에서 최적 온도 업데이트에 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-110">The telemetry measurements will respond to the update in optimal temperature.</span></span> <span data-ttu-id="c72ad-111">**측정값** 페이지에서 변경 내용을 관찰할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-111">You can observe the change on the **Measurements** page.</span></span> 

## <a name="run-commands-on-the-coffee-machine"></a><span data-ttu-id="c72ad-112">커피 머신에서 명령 실행</span><span class="sxs-lookup"><span data-stu-id="c72ad-112">Run commands on the coffee machine</span></span> 
<span data-ttu-id="c72ad-113">다음 연습의 **명령** 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-113">Navigate to the **Commands** page for the following exercise.</span></span> <span data-ttu-id="c72ad-114">명령 설정의 유효성을 검사하기 위해 IoT Central에서 원격으로 커피 머신에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-114">To validate the commands setup, you remotely run commands on the coffee machine from IoT Central.</span></span> <span data-ttu-id="c72ad-115">명령이 성공하면 커피 머신에서 확인 메시지가 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-115">If the commands are successful, confirmation messages are sent from the coffee machine.</span></span>

1. <span data-ttu-id="c72ad-116">**실행**을 선택하여 원격으로 끓이기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-116">Start brewing remotely by choosing **Run**.</span></span> 
    
    <span data-ttu-id="c72ad-117">다음 세 가지 조건이 충족되면 커피 머신이 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-117">The coffee machine will start if these three conditions are satisfied:</span></span>
    - <span data-ttu-id="c72ad-118">컵이 검색됨</span><span class="sxs-lookup"><span data-stu-id="c72ad-118">Cup detected</span></span>
    - <span data-ttu-id="c72ad-119">유지 관리 중이 아님</span><span class="sxs-lookup"><span data-stu-id="c72ad-119">Not in maintenance</span></span>
    - <span data-ttu-id="c72ad-120">이미 커피를 끓이고 있는 상태가 아님</span><span class="sxs-lookup"><span data-stu-id="c72ad-120">Not brewing already</span></span>  

    > [!NOTE]
    > <span data-ttu-id="c72ad-121">커피 끓이기가 정상적으로 시작되면 **측정값** > **상태**에 표시된 대로 머신 상태가 노란색으로 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-121">When you've successfully started brewing, the state of the machine changes to yellow as indicated in **Measurements** > **State**.</span></span> 
    
    <span data-ttu-id="c72ad-122">node.js 시뮬레이션된 커피 머신의 콘솔 로그에서 확인 메시지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-122">Look for confirmation messages in the console log on the node.js simulated coffee machine.</span></span> 

    ![명령 실행](../media/4-commands-brewing.png)

1. <span data-ttu-id="c72ad-124">**실행**을 선택하여 유지 관리 모드를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-124">Set maintenance mode by choosing **Run**.</span></span> <span data-ttu-id="c72ad-125">커피 머신이 아직 유지 관리 모드가 *아닌* 경우 유지 관리 모드로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-125">The coffee machine will set to maintenance if it's *not* already in maintenance.</span></span>
    
    <span data-ttu-id="c72ad-126">커피 머신의 콘솔 로그에서 확인 메시지를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-126">Look for confirmation messages in the console log on the coffee machine.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="c72ad-127">실제 상황에서 수리 기사가 커피 머신을 오프라인으로 전환하여 필요한 수리를 수행한 후 머신을 다시 온라인으로 전환하는 것처럼, 커피 머신도 클라이언트 코드를 다시 부팅할 때까지 유지 관리 모드로 계속 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-127">As in real life, when the technician takes the machine offline to perform necessary repairs before switching it back online, the coffee machine continues to stay in the maintenance mode until you reboot the client code.</span></span>

    ![명령 실행](../media/4-commands-maintenance.png)

> [!IMPORTANT]
> <span data-ttu-id="c72ad-129">응용 프로그램이 원치 않는 알림/이메일을 보내지 않도록 Node.js 응용 프로그램을 60분 이내로 실행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-129">It's recommended that you run the Node.js application no more than 60 minutes or so to prevent the application from sending you unwanted notifications/emails.</span></span> <span data-ttu-id="c72ad-130">또한 모듈에서 작업하지 않을 때에는 일일 메시지 할당량이 소진되지 않도록 응용 프로그램을 중지하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-130">Stopping the application when you're not working on the module also prevents you from exhausting the daily message quota.</span></span>

## <a name="view-the-coffee-machine-in-the-dashboard"></a><span data-ttu-id="c72ad-131">대시보드에서 커피 머신 확인</span><span class="sxs-lookup"><span data-stu-id="c72ad-131">View the coffee machine in the dashboard</span></span>

1. <span data-ttu-id="c72ad-132">**대시보드** 탭으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-132">Navigate to the **Dashboard** tab.</span></span>

1. <span data-ttu-id="c72ad-133">**템플릿 편집**을 선택하여 대시보드를 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-133">Select **Edit Template** to edit the dashboard.</span></span>

1. <span data-ttu-id="c72ad-134">사이드 메뉴에서 **꺾은선형 차트**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-134">Choose **Line Chart** from the side menu.</span></span>

1. <span data-ttu-id="c72ad-135">**차트 구성**의 **제목** 필드에 `Telemetry`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-135">In **Configure Chart**  enter `Telemetry` in the **Title** field.</span></span> <span data-ttu-id="c72ad-136">이 차트를 통해 원격 분석 데이터를 볼 수 했습니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-136">We'll view our telemetry data with this chart.</span></span> 

1. <span data-ttu-id="c72ad-137">**시간 범위**로 **지난 30분**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-137">Select **Past 30 minutes** for **Time Range**.</span></span> 

1. <span data-ttu-id="c72ad-138">**측정값** 영역에서 각 측정의 오른쪽에 있는 표시 아이콘을 선택하여 해당 측정을 차트에 표시할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-138">In the **Measures** area, select the visibility icon to the right of each measurement to make that measurement visible for our chart.</span></span> 

1. <span data-ttu-id="c72ad-139">**저장**을 선택하여 구성을 저장하고 꺾은선형 차트를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-139">Select **Save** to save our configuration and display the line chart.</span></span> 

    ![대시보드 확인](../media/4-dashboard-a.png)

1. <span data-ttu-id="c72ad-141">왼쪽 메뉴에서 **설정 및 속성**을 선택하여 **장치 세부 정보 구성** 패널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-141">Choose **Settings and Properties** in the left-hand menu to open the **Configure Device Details** panel.</span></span> 

1. <span data-ttu-id="c72ad-142">**제목** 필드에 `Device properties`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-142">Enter `Device properties` in the **Title** filed.</span></span>

1. <span data-ttu-id="c72ad-143">**추가/제거**에서 **커피 메이커 최대 온도**, **커피 메이커 최소 온도**, **장치 보증 만료**를 선택한 다음, **확인**을 선택하여 선택을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-143">In **Add/Remove**, choose **Coffee Makers Max Temperature**, **Coffee Makers Min Temperature**, **Device Warranty Expired** and then select **OK** to complete the selection.</span></span>

1. <span data-ttu-id="c72ad-144">대시보드에서 **저장**을 선택하여 새 *장치 속성* 패널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-144">Select **Save** to create a new *Device properties* panel in our dashboard.</span></span> 

1. <span data-ttu-id="c72ad-145">**설정 및 속성**을 다시 선택하고 제목으로 `Optimal Temperature`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-145">Choose **Settings and Properties** again,  and enter `Optimal Temperature` as the title.</span></span> <span data-ttu-id="c72ad-146">**추가/제거**에서 **최적 온도**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-146">In **Add/Remove**, choose **Optimal  Temperature**.</span></span>

1. <span data-ttu-id="c72ad-147">**저장**을 선택하여 작업을 저장하고 대시보드에 새 창을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-147">Select **Save** to save your work and display a new pane in our dashboard.</span></span> 

1. <span data-ttu-id="c72ad-148">**완료**를 선택하여 편집 모드를 종료하고 새 대시보드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="c72ad-148">Select **Done** to exit edit mode and display the new dashboard.</span></span> 