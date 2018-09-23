<span data-ttu-id="9b131-101">영업용 분산 응용 프로그램에서 Azure Service Bus 항목을 사용하여 영업 실적 관련 메시지를 배포하기로 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-101">You have chosen to use an Azure Service Bus topic to distribute messages about sales performance in your sales force distributed application.</span></span> <span data-ttu-id="9b131-102">영업 사원이 모바일 장치에서 사용하는 앱이 각 지역과 기간의 판매 수치가 요약된 메시지를 전송하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-102">The app used by sales personnel on their mobile devices will send messages that summarize sales figures for each area and time period.</span></span> <span data-ttu-id="9b131-103">이러한 메시지는 아메리카/유럽을 비롯하여 회사가 사업을 운영하는 지역에 있는 웹 서비스로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-103">Those messages will be distributed to web services located in the company's operational regions, including the Americas and Europe.</span></span>

<span data-ttu-id="9b131-104">항목과 구독을 포함해 Azure 구독에서 필요한 인프라는 이미 구현한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-104">You have already implemented the necessary infrastructure in your Azure subscription, including the topic and subscriptions.</span></span> <span data-ttu-id="9b131-105">이제 메시지를 해당 항목으로 보내고 구독에서 메시지를 검색하는 코드를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-105">Now, you want to write the code that sends messages to the topic and retrieves messages from a subscription.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="9b131-106">Service Bus 네임스페이스에 대한 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="9b131-106">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="9b131-107">먼저 송신 및 수신 구성 요소에서 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-107">Start by configuring connection strings both in the sending and receiving components:</span></span>

1. <span data-ttu-id="9b131-108">편집기에서 **performancemessagesender/Program.cs**를 열고 코드의 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-108">In the editor, open **performancemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="9b131-109">따옴표 사이에 연결 문자열을 붙여넣고 "..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-109">Paste the connection string between the quotation marks and save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

1. <span data-ttu-id="9b131-110">**performancemessagereceiver/Program.cs**에서 이전 단계를 반복하여 동일한 연결 문자열 값을 붙여넣고 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-110">Repeat the previous step in **performancemessagereceiver/Program.cs**, pasting in the same connection string value and save the file.</span></span>

## <a name="write-code-that-sends-a-message-to-the-topic"></a><span data-ttu-id="9b131-111">토픽에 메시지를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="9b131-111">Write code that sends a message to the topic</span></span>

<span data-ttu-id="9b131-112">영업 실적 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-112">To complete the component that sends messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="9b131-113">편집기에서 **performancemessagesender/Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-113">Open **performancemessagesender/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="9b131-114">`SendPerformanceMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-114">Locate the `SendPerformanceMessageAsync()` method.</span></span>

1. <span data-ttu-id="9b131-115">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-115">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Topic Client here
    ```

1. <span data-ttu-id="9b131-116">항목 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-116">To create a topic client, replace that line of code with the following code:</span></span>

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. <span data-ttu-id="9b131-117">`try...catch` 블록 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-117">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="9b131-118">큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-118">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="9b131-119">콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-119">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="9b131-120">큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-120">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await topicClient.SendAsync(message);
    ```

1. <span data-ttu-id="9b131-121">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-121">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the topic here
    ```

1. <span data-ttu-id="9b131-122">Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-122">To close the connection to Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await topicClient.CloseAsync();
    ```

1. <span data-ttu-id="9b131-123">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-123">Save the file.</span></span>

## <a name="send-a-message-to-the-topic"></a><span data-ttu-id="9b131-124">항목에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="9b131-124">Send a message to the topic</span></span>

<span data-ttu-id="9b131-125">영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-125">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p performancemessagesender
```

<span data-ttu-id="9b131-126">프로그램을 실행하면 메시지를 보내는 중인지 나타내는 출력 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-126">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="9b131-127">앱을 실행할 때마다 항목에 메시지가 하나씩 더 추가되며 각 구독자는 복사본을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-127">Each time you run the app, one additional message will be added to the topic, and each subscriber will receive a copy.</span></span>

<span data-ttu-id="9b131-128">완료되면 다음 명령을 실행하여 아메리카 구독에 얼마나 많은 메시지가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-128">Once it's finished, run the following command to see how many messages are in the Americas subscription:</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="9b131-129">`Americas`를 `EuropeAndAfrica`로 바꾸면 두 구독에 모두 동일한 수의 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-129">If you substitute `EuropeAndAfrica` for `Americas`, you should see that both subscriptions have the same number of messages.</span></span>

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a><span data-ttu-id="9b131-130">항목 구독에서 메시지를 받는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="9b131-130">Write code that receives a message from a topic subscription</span></span>

<span data-ttu-id="9b131-131">영업 실적 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-131">To complete the component that retrieves messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="9b131-132">편집기에서 **performancemessagereceiver/Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-132">Open **performancemessagereceiver/Program.cs** in the editor.</span></span>

1. <span data-ttu-id="9b131-133">`MainAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-133">Locate the `MainAsync()` method.</span></span>

1. <span data-ttu-id="9b131-134">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-134">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a subscription client here
    ```

1. <span data-ttu-id="9b131-135">구독 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-135">To create a subscription client, replace that line with the following code:</span></span>

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. <span data-ttu-id="9b131-136">`RegisterMessageHandler()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-136">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="9b131-137">메시지 처리 옵션을 구성하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-137">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="9b131-138">메시지 처리기를 등록하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-138">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="9b131-139">`ProcessMessagesAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-139">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="9b131-140">이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-140">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="9b131-141">들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-141">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="9b131-142">구독에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-142">To remove the received message from the subscription, on the next line, add the following code:</span></span>

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="9b131-143">`MainAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-143">Return to the `MainAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the subscription here
    ```

1. <span data-ttu-id="9b131-144">Service Bus 연결을 닫으려면 해당 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-144">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. <span data-ttu-id="9b131-145">Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-145">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-a-topic-subscription"></a><span data-ttu-id="9b131-146">항목 구독에서 메시지 검색</span><span class="sxs-lookup"><span data-stu-id="9b131-146">Retrieve a message from a topic subscription</span></span>

<span data-ttu-id="9b131-147">영업 실적 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-147">To run the component that retrieves a message about sales performance, follow these steps:</span></span>

```bash
dotnet run -p performancemessagereceiver
```

<span data-ttu-id="9b131-148">프로그램이 메시지를 수신하는 중인 알림의 인쇄를 중지하는 경우</span><span class="sxs-lookup"><span data-stu-id="9b131-148">When the program stops printing notifications that it is receiving messages.</span></span> <span data-ttu-id="9b131-149">`Enter`를 눌러 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-149">press `Enter` to stop the app.</span></span> <span data-ttu-id="9b131-150">그런 다음, 전과 동일한 명령을 실행하여 `Americas` 구독에 남은 메시지가 없음을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-150">Then, run the same command as before to confirm that there are zero remaining messages in the `Americas` subscription.</span></span>

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

<span data-ttu-id="9b131-151">`Americas`를 `EuropeAndAfrica`로 바꾸는 경우 메시지 수는 변경되지 않았음을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-151">If you substitute `EuropeAndAfrica` for `Americas`, you'll see that the message count has not changed.</span></span> <span data-ttu-id="9b131-152">응용 프로그램은 `Americas` 구독에서만 메시지를 수신했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b131-152">The application only received messages from the `Americas` subscription.</span></span>
