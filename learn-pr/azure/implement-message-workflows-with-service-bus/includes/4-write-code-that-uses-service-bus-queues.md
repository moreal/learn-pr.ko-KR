<span data-ttu-id="3e4b8-101">분산 응용 프로그램은 대상 구성 요소로 전송 대기 중인 메시지를 임시로 저장하는 위치로 Service Bus 큐 등의 큐를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-101">Distributed applications use queues, such as Service Bus queues, as temporary storage locations for messages that are awaiting delivery to a destination component.</span></span> <span data-ttu-id="3e4b8-102">큐를 통해 메시지를 보내고 받으려면 원본 및 대상 구성 요소에서 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-102">To send and receive messages through a queue, you must write code in the source and destination components.</span></span>

<span data-ttu-id="3e4b8-103">Contoso Slices 응용 프로그램의 예를 고려해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-103">Consider the Contoso Slices application.</span></span> <span data-ttu-id="3e4b8-104">고객이 웹 사이트 또는 모바일 앱을 통해 주문을 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-104">The customer places the order through a website or mobile app.</span></span> <span data-ttu-id="3e4b8-105">웹 사이트 및 모바일 앱은 고객 장치에서 실행되므로 한 번에 들어올 수 있는 주문 수에는 실제로 제한이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-105">Because websites and mobile apps run on customer devices, there is really no limit to how many orders could come in at once.</span></span> <span data-ttu-id="3e4b8-106">모바일 앱과 웹 사이트에서 큐에 주문을 보관하도록 하면 백 엔드 구성 요소(웹앱)가 해당 큐에서 적절한 속도로 주문을 처리하도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-106">By having the mobile app and website deposit the orders in a queue, we can allow the back-end component (a web app) to process orders from that queue at its own pace.</span></span>

<span data-ttu-id="3e4b8-107">실제로 Contoso Slices 응용 프로그램은 몇 단계를 통해 새 주문을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-107">The Contoso Slices application actually has several steps to handle a new order.</span></span> <span data-ttu-id="3e4b8-108">하지만 모든 주문을 처리하려면 먼저 결제가 승인되어야 하므로, 여기서는 큐를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-108">But all of them are dependent on first authorizing payment, so we decide to use a queue.</span></span> <span data-ttu-id="3e4b8-109">수신 구성 요소에서는 먼저 결제를 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-109">Our receiving component's first job will be processing the payment.</span></span>

<span data-ttu-id="3e4b8-110">Contoso는 모바일 앱과 웹 사이트에서 메시지를 큐에 추가하는 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-110">In the mobile app and website, Contoso needs to write code that adds a message to the queue.</span></span> <span data-ttu-id="3e4b8-111">메시지를 큐에서 선택하는 코드를 백 엔드 웹앱에서 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-111">In the back-end web app, they'll write code that picks up messages from the queue.</span></span>

<span data-ttu-id="3e4b8-112">여기서는 해당 코드를 작성하는 방법을 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-112">Here, you will learn how to write that code.</span></span>

## <a name="the-microsoftazureservicebus-nuget-package"></a><span data-ttu-id="3e4b8-113">Microsoft.Azure.ServiceBus NuGet 패키지</span><span class="sxs-lookup"><span data-stu-id="3e4b8-113">The Microsoft.Azure.ServiceBus NuGet package</span></span>

<span data-ttu-id="3e4b8-114">Service Bus를 통해 메시지를 보내고 받는 코드를 쉽게 작성할 수 있도록 Microsoft에서는 .NET 클래스 라이브러리를 제공합니다. 이 라이브러리는 모든 .NET Framework 언어에서 Service Bus 큐, 항목 또는 릴레이와 상호 작용하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-114">To make it easy to write code that sends and receives messages through Service Bus, Microsoft provides a library of .NET classes, which you can use in any .NET Framework language to interact with a Service Bus queue, topic, or relay.</span></span> <span data-ttu-id="3e4b8-115">**Microsoft.Azure.ServiceBus** NuGet 패키지를 추가하여 응용 프로그램에 이 라이브러리를 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-115">You can include this library in your application by adding the **Microsoft.Azure.ServiceBus** NuGet package.</span></span>

<span data-ttu-id="3e4b8-116">큐의 경우 이 라이브러리에서 가장 중요한 클래스는 `QueueClient` 클래스입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-116">The most important class in this library for queues is the `QueueClient` class.</span></span> <span data-ttu-id="3e4b8-117">먼저 전송 구성 요소와 수신 구성 요소 둘 다에서 이 클래스를 인스턴스화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-117">You must start by instantiating this class both in sending and receiving components.</span></span>

## <a name="connection-strings-and-keys"></a><span data-ttu-id="3e4b8-118">연결 문자열 및 키</span><span class="sxs-lookup"><span data-stu-id="3e4b8-118">Connection strings and keys</span></span>

<span data-ttu-id="3e4b8-119">Service Bus 네임스페이스에서 큐에 연결하려면 원본 구성 요소와 대상 구성 요소 둘 다에 두 가지 정보가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-119">Source components and destination components both need two pieces of information to connect to a queue in a Service Bus namespace:</span></span>

- <span data-ttu-id="3e4b8-120">Service Bus 네임스페이스 위치(**엔드포인트**라고도 함).</span><span class="sxs-lookup"><span data-stu-id="3e4b8-120">The location of the Service Bus namespace, also known as an **endpoint**.</span></span> <span data-ttu-id="3e4b8-121">이 위치는 **servicebus.windows.net** 도메인 내에서 정규화된 도메인 이름으로 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-121">The location is specified as a fully qualified domain name within the **servicebus.windows.net** domain.</span></span> <span data-ttu-id="3e4b8-122">예를 들면 **pizzaService.servicebus.windows.net**과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-122">For example: **pizzaService.servicebus.windows.net**.</span></span>
- <span data-ttu-id="3e4b8-123">액세스 키.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-123">An access key.</span></span> <span data-ttu-id="3e4b8-124">Service Bus는 액세스 키를 요구하는 방식으로 큐/항목/릴레이 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-124">Service Bus restricts access to queues, topics, and relays by requiring an access key.</span></span>

<span data-ttu-id="3e4b8-125">이 두 정보는 모두 연결 문자열 형식으로 `QueueClient` 개체에 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-125">Both of these pieces of information are provided to the `QueueClient` object in the form of a connection string.</span></span> <span data-ttu-id="3e4b8-126">네임스페이스에 대한 올바른 연결 문자열은 Azure Portal에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-126">You can obtain the correct connection string for your namespace from the Azure portal.</span></span>

## <a name="calling-methods-asynchronously"></a><span data-ttu-id="3e4b8-127">비동기식 메서드 호출</span><span class="sxs-lookup"><span data-stu-id="3e4b8-127">Calling methods asynchronously</span></span>

<span data-ttu-id="3e4b8-128">Azure의 큐는 전송 및 수신 구성 요소에서 매우 멀리 떨어져 있을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-128">The queue in Azure may be located thousands of miles away from sending and receiving components.</span></span> <span data-ttu-id="3e4b8-129">그리고 실제 위치가 가깝더라도 연결 속도가 느리고 대역폭 경합이 발생하는 경우에는 구성 요소가 큐에 대해 메서드를 호출하는 과정이 지연될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-129">Even if it is physically close, slow connections and bandwidth contention may cause delays when a component calls a method on the queue.</span></span> <span data-ttu-id="3e4b8-130">이러한 이유로 인해 Service Bus 클라이언트 라이브러리는 큐와 상호 작용할 수 있도록 `async` 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-130">For this reason, the Service Bus client library makes `async` methods available for interacting with the queues.</span></span> <span data-ttu-id="3e4b8-131">여기서는 호출이 완료되기를 기다리는 동안 스레드가 차단되지 않도록 이러한 메서드를 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-131">We'll use these methods to avoid blocking a thread while waiting for calls to complete.</span></span>

<span data-ttu-id="3e4b8-132">예를 들어 큐에 메시지를 보낼 때는 `await` 키워드가 포함된 `QueueClient.SendAsync()` 메서드를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-132">When sending a message to a queue, for example, use the `QueueClient.SendAsync()` method with the `await` keyword.</span></span>

## <a name="write-code-that-sends-to-queues"></a><span data-ttu-id="3e4b8-133">큐로 정보를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="3e4b8-133">Write code that sends to queues</span></span>

<span data-ttu-id="3e4b8-134">모든 전송 또는 수신 구성 요소에서 Service Bus 큐를 호출하는 코드 파일에 다음의 `using` 문을 추가해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-134">In any sending or receiving component, you should add the following `using` statements to any code file that calls a Service Bus queue:</span></span>

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

<span data-ttu-id="3e4b8-135">그런 다음, 새 `QueueClient` 개체를 만들어 연결 문자열과 큐 이름을 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-135">Next, create a new `QueueClient` object and pass it the connection string and the name of the queue:</span></span>

```C#
queueClient = new QueueClient(TextAppConnectionString, "PrivateMessageQueue");
```

<span data-ttu-id="3e4b8-136">`QueueClient.SendAsync()` 메서드를 호출하고 UTF-8 인코딩 문자열 형식으로 메시지를 전달하여 큐에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-136">You can send a message to the queue by calling the `QueueClient.SendAsync()` method and passing the message in the form of a UTF-8 encoded string:</span></span>

```C#
string message = "Sure would like a large pepperoni!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await queueClient.SendAsync(encodedMessage);
```

## <a name="receive-messages-from-queue"></a><span data-ttu-id="3e4b8-137">큐에서 메시지 받기</span><span class="sxs-lookup"><span data-stu-id="3e4b8-137">Receive messages from queue</span></span>

<span data-ttu-id="3e4b8-138">메시지를 받으려면 먼저 메시지 처리기(큐에 사용 가능한 메시지가 있을 때 호출되는 코드의 메서드)를 등록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-138">To receive messages, you must first register a message handler - this is the method in your code that will be invoked when a message is available on the queue.</span></span>

```C#
queueClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

<span data-ttu-id="3e4b8-139">처리 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-139">Do your processing work.</span></span> <span data-ttu-id="3e4b8-140">그런 다음, 메시지 처리기 내에서 `QueueClient.CompleteAsync()` 메서드를 호출하여 큐에서 메시지를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="3e4b8-140">Then, within the message handler, call the `QueueClient.CompleteAsync()` method to remove the message from the queue:</span></span>

```C#
await queueClient.CompleteAsync(message.SystemProperties.LockToken);
```