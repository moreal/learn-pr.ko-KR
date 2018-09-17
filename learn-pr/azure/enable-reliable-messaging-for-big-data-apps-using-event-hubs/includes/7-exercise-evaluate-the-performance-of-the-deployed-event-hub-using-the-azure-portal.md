<span data-ttu-id="62d9a-101">이 단원에서는 Azure Portal을 사용하여 이벤트 허브가 예상대로 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-101">In this unit, you'll use the Azure portal to verify your event hub is working and performing according to the desired expectations.</span></span> <span data-ttu-id="62d9a-102">또한 일시적으로 사용할 수 없을 때 이벤트 허브 메시징이 어떻게 작동하는지 테스트하고 Event Hubs 메트릭을 사용하여 이벤트 허브의 성능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-102">You'll also test how event hub messaging works when it's temporarily unavailable and use Event Hubs metrics to check the performance of your event hub.</span></span>

## <a name="view-event-hub-activity"></a><span data-ttu-id="62d9a-103">이벤트 허브 활동 보기</span><span class="sxs-lookup"><span data-stu-id="62d9a-103">View event hub activity</span></span>

1. <span data-ttu-id="62d9a-104">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-104">Sign in to the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>

1. <span data-ttu-id="62d9a-105">검색 창을 사용하여 이벤트 허브를 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-105">Find your event hub, using the Search bar, and open it.</span></span>

1. <span data-ttu-id="62d9a-106">개요 페이지에서 메시지 개수를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-106">On the Overview page, view the message counts.</span></span>

    ![이벤트 허브 메시지 보기](../media-draft/6-view-messages.png)

1. <span data-ttu-id="62d9a-108">SimpleSend 및 EventProcessorSample 응용 프로그램은 100개의 메시지를 보내거나 받도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-108">The SimpleSend and EventProcessorSample applications are configured to send/receive 100 messages.</span></span> <span data-ttu-id="62d9a-109">이벤트 허브가 SimpleSend 응용 프로그램에서 100개의 메시지를 처리했고 100개의 메시지를 EventProcessorSample 응용 프로그램으로 전송했음을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-109">You'll see that the event hub has processed 100 messages from the SimpleSend application and has transmitted 100 messages to the EventProcessorSample application.</span></span>

## <a name="test-event-hub-resilience"></a><span data-ttu-id="62d9a-110">이벤트 허브 복원력 테스트</span><span class="sxs-lookup"><span data-stu-id="62d9a-110">Test event hub resilience</span></span>

<span data-ttu-id="62d9a-111">다음 단계를 사용하여 일시적으로 사용할 수 없는 동안 응용 프로그램이 이벤트 허브에 메시지를 보내면 어떻게 되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-111">Use the following steps to see what happens when an application sends messages to an event hub while it's temporarily unavailable.</span></span>

1. <span data-ttu-id="62d9a-112">SimpleSend 응용 프로그램을 사용하여 이벤트 허브로 메시지를 다시 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-112">Resend messages to the event hub using the SimpleSend application.</span></span> <span data-ttu-id="62d9a-113">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-113">Use the following command:</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="62d9a-114">**보내기 완료...** 가 표시되면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-114">When you see **Send Complete...**, press ENTER.</span></span>

1. <span data-ttu-id="62d9a-115">Azure Portal에서 **Event Hubs 인스턴스** > **설정** > **속성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-115">In the Azure portal, click **Event Hubs Instance** > **SETTINGS** > **Properties**.</span></span>

1. <span data-ttu-id="62d9a-116">이벤트 허브 상태에서 **사용 안 함**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-116">Under Event Hub state, click **Disabled**.</span></span>

    ![이벤트 허브 사용 안 함](../media-draft/7-disable-event-hub.png)

<span data-ttu-id="62d9a-118">5분 이상 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-118">Wait for a minimum of five minutes.</span></span>

1. <span data-ttu-id="62d9a-119">이벤트 허브 상태에서 **활성**을 클릭하여 이벤트 허브를 다시 사용하고 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-119">Click **Active** under Event Hub state to re-enable your event hub and save your changes.</span></span>

1. <span data-ttu-id="62d9a-120">EventProcessorSample 응용 프로그램을 다시 실행하여 메시지를 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-120">Rerun the EventProcessorSample application to receive messages.</span></span> <span data-ttu-id="62d9a-121">다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-121">Use the following command.</span></span>

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. <span data-ttu-id="62d9a-122">메시지가 콘솔에 표시되는 작업이 중지하면 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-122">When messages stop being displayed to the console, press ENTER.</span></span>

1. <span data-ttu-id="62d9a-123">Azure Portal에서 이벤트 허브 **‘네임스페이스’** 를 찾아 엽니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-123">In the Azure portal, find your event hub **_namespace_** and open it.</span></span> 

1. <span data-ttu-id="62d9a-124">**Event Hubs 네임스페이스** > **모니터링** > **메트릭(미리 보기)** 을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-124">Click **Event Hubs Namespace** > **MONITORING** > **Metrics (preview)**.</span></span>

    ![이벤트 허브 메트릭 사용](../media-draft/7-event-hub-metrics.png)

1. <span data-ttu-id="62d9a-126">**메트릭** 목록에서 **들어오는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-126">From the **Metric** list, select **Incoming Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="62d9a-127">**메트릭** 목록에서 **보내는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-127">From the **Metric** list, select **Outgoing Messages** and click **Add Metric**.</span></span>

1. <span data-ttu-id="62d9a-128">차트의 맨 위에서 **최근 24시간(자동)** 을 클릭하여 기간을 **지난 30분**으로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-128">At the top of the chart, click **Last 24 hours (Automatic)** to change the time period to **Last 30 minutes**.</span></span>

1. <span data-ttu-id="62d9a-129">**적용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-129">Click **Apply**.</span></span>

<span data-ttu-id="62d9a-130">일정 기간에 이벤트 허브를 오프라인으로 전환하기 전에 메시지가 전송되었지만 100개의 모든 메시지가 성공적으로 전송되었음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-130">You'll see that though the messages were sent before the event hub was taken offline for a period, all 100 messages were successfully transmitted.</span></span>

## <a name="summary"></a><span data-ttu-id="62d9a-131">요약</span><span class="sxs-lookup"><span data-stu-id="62d9a-131">Summary</span></span>

<span data-ttu-id="62d9a-132">이 단원에서는 Event Hubs 메트릭을 사용하여 이벤트 허브가 보내고 받는 메시지를 성공적으로 처리하고 있는지 테스트했습니다.</span><span class="sxs-lookup"><span data-stu-id="62d9a-132">In this unit, you used the Event Hubs metrics to test that your event hub is successfully processing the sending and receiving messages.</span></span>
