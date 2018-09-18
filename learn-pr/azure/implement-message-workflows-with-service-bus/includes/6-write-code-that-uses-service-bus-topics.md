<span data-ttu-id="c945a-101">분산 응용 프로그램에서는 받는 사람 구성 요소 하나로 보내야 하는 메시지도 있고,</span><span class="sxs-lookup"><span data-stu-id="c945a-101">In a distributed application, some messages need to be sent to a single recipient component.</span></span> <span data-ttu-id="c945a-102">여러 대상으로 보내야 하는 메시지도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-102">Other messages need to reach more than one destination.</span></span>

<span data-ttu-id="c945a-103">사용자가 피자 주문을 취소하는 경우 발생하는 상황을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-103">Let's discuss what happens when a user cancels a pizza order.</span></span> <span data-ttu-id="c945a-104">이 상황은 초기 주문을 할 때와는 약간 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-104">This is a little different than placing the initial order.</span></span> <span data-ttu-id="c945a-105">초기 주문의 경우 주문을 다른 단계(예: 해당 지역 상점에서 피자를 준비 및 요리하는 단계)로 보내기 전에 주문에서 결제 처리가 완료될 때까지 기다려야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-105">In that case, we wanted to wait until the order cleared payment processing before sending the order on to other steps (like having it prepared and cooked at the local storefront).</span></span> <span data-ttu-id="c945a-106">그러나 취소 작업의 경우에는 상점 *및* 결제 처리 업체에 동시에 알림을 보내야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-106">But for the cancel operation, we are going to notify both the storefront *and* the payment processor at the same time.</span></span> <span data-ttu-id="c945a-107">이 방식을 사용하는 경우 식자재 또는 배달 차량 운전자의 시간 낭비 가능성을 최소화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-107">This approach minimizes the chances that we waste ingredients or delivery driver time.</span></span>

<span data-ttu-id="c945a-108">여러 구성 요소가 같은 메시지를 받을 수 있도록 하기 위해 Azure Service Bus 항목을 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-108">To allow multiple components to receive the same message, we'll use an Azure Service Bus topic.</span></span>

## <a name="how-code-that-uses-topics-differs-from-queues"></a><span data-ttu-id="c945a-109">항목을 사용하는 코드와 큐의 차이점</span><span class="sxs-lookup"><span data-stu-id="c945a-109">How code that uses topics differs from queues</span></span>

<span data-ttu-id="c945a-110">항목으로 보내는 모든 메시지가 모든 구독 구성 요소에 배달되도록 하려는 경우에 항목을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-110">If you want every message sent to the topic to be delivered to all subscribing components, you'll use topics.</span></span> <span data-ttu-id="c945a-111">항목을 사용하는 코드를 작성하는 것은 큐를 대체하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-111">Writing code that uses topics is a way to replace queues.</span></span> <span data-ttu-id="c945a-112">이 경우에도 같은 **Microsoft.Azure.ServiceBus** NuGet 패키지를 사용하고, 연결 문자열을 구성하고, 비동기 프로그래밍 패턴을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-112">You use the same **Microsoft.Azure.ServiceBus** NuGet package, configure connection strings, and use asynchronous programming patterns.</span></span>

<span data-ttu-id="c945a-113">그러나 `QueueClient` 클래스 대신 `TopicClient` 클래스를 사용하여 메시지를 보내며 `SubscriptionClient` 클래스를 사용하여 메시지를 받습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-113">However, you use the `TopicClient` class instead of the `QueueClient` class to send messages and the `SubscriptionClient` class to receive messages.</span></span>

## <a name="setting-filters-on-subscriptions"></a><span data-ttu-id="c945a-114">구독에 대해 필터 설정</span><span class="sxs-lookup"><span data-stu-id="c945a-114">Setting filters on subscriptions</span></span>

<span data-ttu-id="c945a-115">항목으로 전송되는 메시지가 배달되는 구독을 제어하려는 경우 항목의 각 구독에 대해 필터를 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-115">If you want to control which messages sent to the topic are delivered to which subscriptions, you can place filters on each subscription in the topic.</span></span> <span data-ttu-id="c945a-116">예를 들어, 피자 응용 프로그램의 경우 상점에서는 UWP(Universal Windows Platform) 응용 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-116">In the pizza application, for instance, our storefronts are running Universal Windows Platform (UWP) applications.</span></span> <span data-ttu-id="c945a-117">각 매장은 “OrderCancellation” 항목을 구독하되 고유한 StoreID를 필터로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-117">Each store can subscribe to the "OrderCancellation" topic but filter for its own StoreId.</span></span> <span data-ttu-id="c945a-118">이 경우 멀리 떨어져 있는 매장 위치로 불필요한 메시지가 전송되지 않으므로 인터넷 대역폭도 절약됩니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-118">We save internet bandwidth because we are not sending unnecessary messages to distant store locations.</span></span> <span data-ttu-id="c945a-119">단, 결제 처리 구성 요소는 모든 취소 메시지를 구독합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-119">Meanwhile, the payment processing component subscribes to all our cancellation messages.</span></span>

<span data-ttu-id="c945a-120">필터는 다음의 세 가지 유형 중 하나일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-120">Filters can be one of three types:</span></span>

- <span data-ttu-id="c945a-121">**부울 필터.**</span><span class="sxs-lookup"><span data-stu-id="c945a-121">**Boolean Filters.**</span></span> <span data-ttu-id="c945a-122">`TrueFilter`를 사용하면 항목으로 보내는 모든 메시지가 현재 구독으로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-122">The `TrueFilter` ensures that all messages sent to the topic are delivered to the current subscription.</span></span> <span data-ttu-id="c945a-123">`FalseFilter`는 현재 구독에 배달된 메시지가 없음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-123">The `FalseFilter` ensures that none of the messages are delivered to the current subscription.</span></span> <span data-ttu-id="c945a-124">(이로 인해 구독이 효과적으로 차단되거나 해제됩니다.)</span><span class="sxs-lookup"><span data-stu-id="c945a-124">(This effectively blocks or switches off the subscription.)</span></span>
- <span data-ttu-id="c945a-125">**SQL 필터.**</span><span class="sxs-lookup"><span data-stu-id="c945a-125">**SQL Filters.**</span></span> <span data-ttu-id="c945a-126">SQL 필터는 SQL 쿼리의 `WHERE` 절과 같은 구문을 사용하여 조건을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-126">A SQL filter specifies a condition by using the same syntax as a `WHERE` clause in a SQL query.</span></span> <span data-ttu-id="c945a-127">이 구독을 기준으로 평가했을 때 `True`를 반환하는 메시지만 구독자에게 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-127">Only messages that return `True` when evaluated against this subscription will be delivered to the subscribers.</span></span>
- <span data-ttu-id="c945a-128">**상관관계 필터.**</span><span class="sxs-lookup"><span data-stu-id="c945a-128">**Correlation Filters.**</span></span> <span data-ttu-id="c945a-129">상관관계 필터는 각 메시지 속성과의 일치 여부를 비교하는 조건 집합을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-129">A correlation filter holds a set of conditions that are matched against the properties of each message.</span></span> <span data-ttu-id="c945a-130">필터의 속성과 메시지의 속성 값이 같으면 두 속성은 일치하는 것으로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-130">If the property in the filter and the property on the message have the same value, it is considered a match.</span></span>

<span data-ttu-id="c945a-131">StoreId 필터의 경우 SQL 필터를 사용할 수 *있습니다*.</span><span class="sxs-lookup"><span data-stu-id="c945a-131">For our StoreId filter, we *could* use a SQL filter.</span></span> <span data-ttu-id="c945a-132">이러한 필터는 가장 유연하지만 계산 비용이 가장 많이 들고 Service Bus 처리 속도가 느려질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-132">Those filters are the most flexible, but they're also the most computationally expensive and could slow down our Service Bus throughput.</span></span> <span data-ttu-id="c945a-133">그러므로 여기서는 상관관계 필터를 대신 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-133">In this case, we choose a correlation filter instead.</span></span> 

## <a name="topicclient-example"></a><span data-ttu-id="c945a-134">TopicClient 예제</span><span class="sxs-lookup"><span data-stu-id="c945a-134">TopicClient example</span></span>

<span data-ttu-id="c945a-135">모든 전송 또는 수신 구성 요소에서 Service Bus 항목을 호출하는 코드 파일에 다음의 `using` 문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-135">In any sending or receiving component, you should add the following `using` statements to any code file that calls a Service Bus topic:</span></span>

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

<span data-ttu-id="c945a-136">메시지를 보내려면 먼저 새 `TopicClient` 개체를 만들어 연결 문자열과 항목 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-136">To send a message, start by creating a new `TopicClient` object and pass it the connection string and the name of the topic:</span></span>

```C#
topicClient = new TopicClient(TextAppConnectionString, "GroupMessageTopic");
```

<span data-ttu-id="c945a-137">`TopicClient.SendAsync()` 메서드를 호출하고 메시지를 전달하면 항목에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-137">You can send a message to the topic by calling the `TopicClient.SendAsync()` method and passing the message.</span></span> <span data-ttu-id="c945a-138">큐와 마찬가지로 메시지는 UTF-8 인코딩 문자열 형식이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-138">As with queues, the message must be in the form of a UTF-8 encoded string:</span></span>

```C#
string message = "Cancel! I can't believe you use canned mushrooms!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await topicClient.SendAsync(encodedMessage);
```

<span data-ttu-id="c945a-139">메시지를 받으려면 `TopicClient` 개체가 아닌 `SubscriptionClient` 개체를 만들어 연결 문자열, 항목의 이름 **및** 구독 이름을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-139">To receive messages, you must create a `SubscriptionClient` object, not a `TopicClient` object, and pass it the connection string, the name of the topic, **and** the name of the subscription:</span></span>

```C#
subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, "GroupMessageTopic", "NorthAmerica");
```

<span data-ttu-id="c945a-140">그런 다음 메시지 처리기를 등록합니다. 메시지 처리기는 검색된 메시지를 처리하는 코드의 비동기 메서드입니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-140">Then register a message handler - this is the asynchronous method in your code that processes the retrieved message.</span></span>

```C#
subscriptionClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

<span data-ttu-id="c945a-141">메시지 처리기 내에서 `SubscriptionClient.CompleteAsync()` 메서드를 호출하여 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="c945a-141">Within the message handler, call the `SubscriptionClient.CompleteAsync()` method to remove the message from the queue:</span></span>

```C#
await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
```