<span data-ttu-id="c3745-101">Event Hubs를 사용할 경우 허브를 모니터링하여 예상대로 작동하는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-101">When using Event Hubs, it's crucial for you to monitor your hub to ensure that it's working and performing as expected.</span></span>

<span data-ttu-id="c3745-102">계속해서 은행 예제에서, Azure Event Hubs를 배포하고 발신자 및 수신자 응용 프로그램을 구성했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-102">Continuing with the banking example, suppose that you've deployed Azure Event Hubs and configured sender and receiver applications.</span></span> <span data-ttu-id="c3745-103">응용 프로그램이 결제 처리 솔루션을 테스트할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-103">Your applications are ready for testing the payment processing solution.</span></span> <span data-ttu-id="c3745-104">발신자 응용 프로그램은 고객의 신용 카드 데이터를 수집하고 수신자 응용 프로그램은 신용 카드가 유효한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-104">The sender application collects customer's credit card data and the receiver application verifies that the credit card is valid.</span></span> <span data-ttu-id="c3745-105">회사 비즈니스의 민감한 특성으로 인해 결제 처리는 일시적으로 사용할 수 없는 경우에도 강력하고 안정적이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-105">Due to the sensitive nature of your employer's business, it's essential that your payment processing is robust and reliable, even when it's temporarily unavailable.</span></span>

<span data-ttu-id="c3745-106">이벤트 허브가 예상대로 데이터를 처리하고 있는지 테스트하여 이벤트 허브를 평가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-106">You must evaluate your event hub by testing that your event hub is processing data as expected.</span></span> <span data-ttu-id="c3745-107">Event Hubs에서 사용 가능한 메트릭을 통해 제대로 작동하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-107">The metrics available in the Event Hubs allow you to ensure that it's working fine.</span></span>

## <a name="how-do-you-use-the-azure-portal-to-view-your-event-hub-activity"></a><span data-ttu-id="c3745-108">Azure Portal을 사용하여 이벤트 허브 작업을 보려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c3745-108">How do you use the Azure portal to view your event hub activity?</span></span>

<span data-ttu-id="c3745-109">Azure Portal > 이벤트 허브 개요 페이지에 메시지 개수가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-109">The Azure portal > Overview page for your event hub shows message counts.</span></span> <span data-ttu-id="c3745-110">이 메시지 개수는 이벤트 허브가 수신 및 전송한 데이터(이벤트)를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-110">These message counts represent the data (events) received and sent by the event hub.</span></span> <span data-ttu-id="c3745-111">이러한 이벤트를 보기 위한 시간 간격을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-111">You can choose the timescale for viewing these events.</span></span>

![이벤트 허브 메시지 보기](../media-draft/6-view-messages.png)

## <a name="how-can-you-test-event-hub-resilience"></a><span data-ttu-id="c3745-113">이벤트 허브 복원력을 테스트하려면 어떻게 해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="c3745-113">How can you test Event Hub resilience?</span></span>

<span data-ttu-id="c3745-114">Azure Event Hubs는 사용할 수 없는 경우에도 발신자 응용 프로그램에서 메시지를 계속 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-114">Azure Event Hubs keeps receiving messages from the sender application even when it's unavailable.</span></span> <span data-ttu-id="c3745-115">이 기간에 받은 메시지는 허브를 사용할 수 있게 되는 즉시 성공적으로 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-115">The messages received during this period are transmitted successfully as soon as the hub becomes available.</span></span>

<span data-ttu-id="c3745-116">이 기능을 테스트하려면 Azure Portal을 사용하여 이벤트 허브를 사용하지 않도록 설정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-116">To test this functionality, you can use the Azure portal to disable your event hub.</span></span>

<span data-ttu-id="c3745-117">이벤트 허브를 다시 사용하도록 설정하면 수신자 응용 프로그램을 다시 실행하고 네임스페이스에 대한 Event Hubs 메트릭을 사용하여 모든 발신자 메시지가 성공적으로 전송되고 수신되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-117">When you re-enable your event hub, you can rerun your receiver application and use Event Hubs metrics for your namespace to check whether all sender messages have been successfully transmitted and received.</span></span>

<span data-ttu-id="c3745-118">Event Hubs에서 사용 가능한 기타 유용한 메트릭은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-118">Other useful metrics available in the Event Hubs include:</span></span>

- <span data-ttu-id="c3745-119">제한된 요청: 처리량 단위 사용량이 초과되었기 때문에 제한된 요청 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-119">Throttled Requests: The number of requests that were throttled because the throughput unit usage was exceeded.</span></span>
- <span data-ttu-id="c3745-120">ActiveConnections: 네임스페이스 또는 이벤트 허브의 활성 연결 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-120">ActiveConnections: The number of active connections on a namespace or event hub.</span></span>
- <span data-ttu-id="c3745-121">들어오는/나가는 바이트: 지정된 기간에 Event Hubs 서비스에 보내거나 서비스에서 받은 바이트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-121">Incoming/Outgoing Bytes: The number of bytes sent to/received from the Event Hubs service over a specified period.</span></span>

## <a name="summary"></a><span data-ttu-id="c3745-122">요약</span><span class="sxs-lookup"><span data-stu-id="c3745-122">Summary</span></span>

<span data-ttu-id="c3745-123">Azure Portal은 Event Hubs에 대한 상태 검사로 사용할 수 있는 메시지 개수와 기타 메트릭을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c3745-123">The Azure portal provides message counts and other metrics that you can use as a health check for your Event Hubs.</span></span>
