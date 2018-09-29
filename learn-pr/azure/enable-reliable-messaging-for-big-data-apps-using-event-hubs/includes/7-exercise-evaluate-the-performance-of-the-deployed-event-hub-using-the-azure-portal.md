<span data-ttu-id="5ea19-101">이 단원에서는 Azure Portal을 사용하여 이벤트 허브가 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-101">In this unit, you'll use the Azure portal to verify your Event Hub is working and performing according to the desired expectations.</span></span> <span data-ttu-id="5ea19-102">또한 일시적으로 사용할 수 없을 때 이벤트 허브 메시징이 어떻게 작동하는지 테스트하고 Event Hubs 메트릭을 사용하여 이벤트 허브의 성능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-102">You'll also test how Event Hub messaging works when it's temporarily unavailable and use Event Hubs metrics to check the performance of your Event Hub.</span></span>

## <a name="view-event-hub-activity"></a><span data-ttu-id="5ea19-103">이벤트 허브 작업 보기</span><span class="sxs-lookup"><span data-stu-id="5ea19-103">View Event Hub activity</span></span>

1. <span data-ttu-id="5ea19-104">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-104">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="5ea19-105">검색 창을 사용하여 이벤트 허브를 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-105">Find your Event Hub, using the Search bar, and open it.</span></span>

1. <span data-ttu-id="5ea19-106">개요 페이지에서 메시지 개수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-106">On the Overview page, view the message counts.</span></span>

    ![메시지 개수가 포함된 이벤트 허브 네임스페이스를 표시하는 Azure Portal의 스크린샷](../media/6-view-messages.png)

1. <span data-ttu-id="5ea19-108">SimpleSend 및 EventProcessorSample 응용 프로그램은 100개의 메시지를 보내거나 받도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-108">The SimpleSend and EventProcessorSample applications are configured to send/receive 100 messages.</span></span> <span data-ttu-id="5ea19-109">이벤트 허브가 SimpleSend 응용 프로그램에서 100개의 메시지를 처리했고 100개의 메시지를 EventProcessorSample 응용 프로그램으로 전송했음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-109">You'll see that the Event Hub has processed 100 messages from the SimpleSend application and has transmitted 100 messages to the EventProcessorSample application.</span></span>

## <a name="test-event-hub-resilience"></a><span data-ttu-id="5ea19-110">이벤트 허브 복원력 테스트</span><span class="sxs-lookup"><span data-stu-id="5ea19-110">Test Event Hub resilience</span></span>

<span data-ttu-id="5ea19-111">다음 단계를 사용하여 일시적으로 사용할 수 없는 동안 응용 프로그램이 이벤트 허브에 메시지를 보내면 어떻게 되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-111">Use the following steps to see what happens when an application sends messages to an Event Hub while it's temporarily unavailable.</span></span>

1. <span data-ttu-id="5ea19-112">SimpleSend 응용 프로그램을 사용하여 이벤트 허브로 메시지를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-112">Resend messages to the Event Hub using the SimpleSend application.</span></span> <span data-ttu-id="5ea19-113">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-113">Use the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="5ea19-114">**보내기 완료...** 가 표시되면 <kbd>ENTER</kbd> 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-114">When you see **Send Complete...**, press <kbd>ENTER</kbd>.</span></span>

1. <span data-ttu-id="5ea19-115">**개요** 화면에서 이벤트 허브를 선택하면 이벤트 허브와 관련된 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-115">Select your Event Hub in the **Overview** screen - this will show details specific to the Event Hub.</span></span> <span data-ttu-id="5ea19-116">네임스페이스 페이지의 **Event Hubs** 항목에서 이 화면으로 이동할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-116">You can also get to this screen through the **Event Hubs** entry from the namespace page.</span></span>

1. <span data-ttu-id="5ea19-117">**설정** > **속성**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-117">Select **Settings** > **Properties**.</span></span>

1. <span data-ttu-id="5ea19-118">이벤트 허브 상태에서 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-118">Under Event Hub state, click **Disabled**.</span></span> <span data-ttu-id="5ea19-119">변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-119">Save the changes.</span></span>

    ![이벤트 허브 사용 안 함](../media/7-disable-event-hub.png)

    <span data-ttu-id="5ea19-121">**5분 정도 기다립니다.**</span><span class="sxs-lookup"><span data-stu-id="5ea19-121">**Wait for a minimum of five minutes.**</span></span>

1. <span data-ttu-id="5ea19-122">이벤트 허브 상태에서 **활성**을 클릭하여 이벤트 허브를 다시 사용하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-122">Click **Active** under Event Hub state to re-enable your Event Hub and save your changes.</span></span>

1. <span data-ttu-id="5ea19-123">EventProcessorSample 응용 프로그램을 다시 실행하여 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-123">Rerun the EventProcessorSample application to receive messages.</span></span> <span data-ttu-id="5ea19-124">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-124">Use the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="5ea19-125">메시지가 콘솔에 표시되는 작업이 중지하면 <kbd>ENTER</kbd> 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-125">When messages stop being displayed to the console, press <kbd>ENTER</kbd>.</span></span>

1. <span data-ttu-id="5ea19-126">Azure Portal에서 이벤트 허브 네임스페이스로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-126">Back in the Azure portal, go back to your Event Hub Namespace.</span></span> <span data-ttu-id="5ea19-127">여전히 이벤트 허브 페이지에 있는 경우 화면 맨 위에 있는 이동 경로 탐색을 사용하여 뒤로 돌아갈 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-127">If you are still on the Event Hub page, you can use the breadcrumb on the top of the screen to go backwards.</span></span> <span data-ttu-id="5ea19-128">또는 네임스페이스를 검색하여 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-128">Or you can search for the namespace and select it.</span></span>

1. <span data-ttu-id="5ea19-129">**모니터링** > **메트릭(미리 보기)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-129">Click **MONITORING** > **Metrics (preview)**.</span></span>

    ![들어오는 메시지와 나가는 메시지의 수가 포함된 이벤트 허브 메트릭을 보여주는 스크린샷.](../media/7-event-hub-metrics.png)

1. <span data-ttu-id="5ea19-131">**메트릭** 목록에서 **들어오는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-131">From the **Metric** list, select **Incoming Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="5ea19-132">**메트릭** 목록에서 **보내는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-132">From the **Metric** list, select **Outgoing Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="5ea19-133">차트 맨 위에서 **최근 24시간(자동)** 을 클릭하고 기간을 **지난 30분**으로 변경하여 데이터 그래프를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-133">At the top of the chart, click **Last 24 hours (Automatic)** to change the time period to **Last 30 minutes** to expand the data graph.</span></span>

<span data-ttu-id="5ea19-134">일정 기간에 이벤트 허브를 오프라인으로 전환하기 전에 메시지가 전송되었지만 100개의 모든 메시지가 성공적으로 전송되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-134">You'll see that though the messages were sent before the Event Hub was taken offline for a period, all 100 messages were successfully transmitted.</span></span>

## <a name="summary"></a><span data-ttu-id="5ea19-135">요약</span><span class="sxs-lookup"><span data-stu-id="5ea19-135">Summary</span></span>

<span data-ttu-id="5ea19-136">이 단원에서는 Event Hubs 메트릭을 사용하여 이벤트 허브가 보내고 받는 메시지를 성공적으로 처리하고 있는지 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="5ea19-136">In this unit, you used the Event Hubs metrics to test that your Event Hub is successfully processing the sending and receiving messages.</span></span>
