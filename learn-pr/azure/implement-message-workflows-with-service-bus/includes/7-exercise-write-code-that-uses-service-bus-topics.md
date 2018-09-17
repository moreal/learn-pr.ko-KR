<span data-ttu-id="63d39-101">영업용 분산 응용 프로그램에서 Azure Service Bus 항목을 사용하여 영업 실적 관련 메시지를 배포하기로 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-101">You have chosen to use an Azure Service Bus topic to distribute messages about sales performance in your sales force distributed application.</span></span> <span data-ttu-id="63d39-102">영업 사원이 모바일 장치에서 사용하는 앱이 각 지역과 기간의 판매 수치가 요약된 메시지를 전송하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-102">The app used by sales personnel on their mobile devices will send messages that summarize sales figures for each area and time period.</span></span> <span data-ttu-id="63d39-103">이러한 메시지는 아메리카/유럽을 비롯하여 회사가 사업을 운영하는 지역에 있는 웹 서비스로 배포됩니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-103">Those messages will be distributed to web services located in the company's operational regions, including the Americas and Europe.</span></span>

<span data-ttu-id="63d39-104">항목과 구독을 포함해 Azure 구독에서 필요한 인프라는 이미 구현한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-104">You have already implemented the necessary infrastructure in your Azure subscription, including the topic and subscriptions.</span></span> <span data-ttu-id="63d39-105">이제 메시지를 해당 항목으로 보내고 각 구독에서 메시지를 검색하는 코드를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-105">Now, you want to write the code that sends messages to the topic and retrieves messages from each subscription.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="63d39-106">Service Bus 네임스페이스에 대한 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="63d39-106">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="63d39-107">먼저 송신 및 수신 구성 요소에서 연결 문자열을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-107">Start by configuring connection strings both in the sending and receiving components:</span></span>

1. <span data-ttu-id="63d39-108">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-108">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="63d39-109">홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-109">In the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="63d39-110">**설정** 아래에서 **공유 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-110">Under **SETTINGS**, click **Shared Access Policies**.</span></span>

1. <span data-ttu-id="63d39-111">정책 목록에서 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-111">In the list of policies, click **RootManageSharedAccessKey**.</span></span>

1. <span data-ttu-id="63d39-112">**기본 연결 문자열** 텍스트 상자 오른쪽에서 **복사하려면 클릭** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-112">To the right of the **Primary Connection string** text box, click the **Click to copy** button.</span></span>

1. <span data-ttu-id="63d39-113">**Visual Studio Code**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-113">Switch to **Visual Studio Code**.</span></span>

1. <span data-ttu-id="63d39-114">**탐색기** 창의 **performancemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-114">In the **Explorer** pane, in the **performancemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="63d39-115">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-115">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="63d39-116">따옴표 사이에 커서를 놓은 다음, **Ctrl+V**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-116">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="63d39-117">**탐색기** 창의 **performancemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-117">In the **Explorer** pane, in the **performancemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="63d39-118">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-118">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="63d39-119">따옴표 사이에 커서를 놓은 다음, **Ctrl+V**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-119">Place the cursor between the quotation marks, and then press **Ctrl+V**.</span></span>

1. <span data-ttu-id="63d39-120">**파일**을 클릭한 다음, **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-120">Click **File**, and then click **Save All**.</span></span>

1. <span data-ttu-id="63d39-121">열려 있는 편집기 창을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-121">Close all open editor windows.</span></span>

## <a name="write-code-that-sends-a-message-to-the-topic"></a><span data-ttu-id="63d39-122">항목에 메시지를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="63d39-122">Write code that sends a message to the topic</span></span>

<span data-ttu-id="63d39-123">영업 실적 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-123">To complete the component that sends messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="63d39-124">Visual Studio Code **탐색기** 창의 **performancemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-124">In Visual Studio Code, in the **Explorer** pane, in the **performancemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="63d39-125">`SendPerformanceMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-125">Locate the `SendPerformanceMessageAsync()` method.</span></span>

1. <span data-ttu-id="63d39-126">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-126">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Topic Client here
    ```

1. <span data-ttu-id="63d39-127">항목 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-127">To create a topic client, replace that line of code with the following code:</span></span>

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. <span data-ttu-id="63d39-128">`try...catch` 블록 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-128">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="63d39-129">큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-129">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="63d39-130">콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-130">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="63d39-131">큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-131">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await topicClient.SendAsync(message);
    ```

1. <span data-ttu-id="63d39-132">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-132">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the topic here
    ```

1. <span data-ttu-id="63d39-133">Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-133">To close the connection to Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await topicClient.CloseAsync();
    ```

1. <span data-ttu-id="63d39-134">Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-134">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="send-a-message-to-the-topic"></a><span data-ttu-id="63d39-135">항목에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="63d39-135">Send a message to the topic</span></span>

<span data-ttu-id="63d39-136">판매 관련 메시지를 보내는 구성 요소를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-136">To run the component that sends a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="63d39-137">Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-137">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="63d39-138">**디버그** 창의 드롭다운 목록에서 **Performance Message Sender 시작**을 선택한 다음, **F5**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-138">In the **Debug** pane, in the drop-down list, select **Launch Performance Message Sender**, and then press **F5**.</span></span> <span data-ttu-id="63d39-139">Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-139">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="63d39-140">프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-140">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="63d39-141">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-141">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="63d39-142">Service Bus 네임스페이스가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음, 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-142">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="63d39-143">**Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **항목**을 클릭한 다음, **salesperformancemessages** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-143">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Topics**, and then click the **salesperformancemessages** topic.</span></span> <span data-ttu-id="63d39-144">구독 목록의 **아메리카** 및 **유럽** 구독에 모두 메시지 하나가 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-144">In the list of subscriptions, there should be one message displayed in both the **Americas** and **Europe** subscriptions.</span></span>

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a><span data-ttu-id="63d39-145">항목 구독에서 메시지를 받는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="63d39-145">Write code that receives a message from a topic subscription</span></span>

<span data-ttu-id="63d39-146">영업 실적 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-146">To complete the component that retrieves messages about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="63d39-147">Visual Studio Code **탐색기** 창의 **performancemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-147">In Visual Studio Code, in the **Explorer** pane, in the **performancemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="63d39-148">`MainAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-148">Locate the `MainAsync()` method.</span></span>

1. <span data-ttu-id="63d39-149">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-149">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a subscription client here
    ```

1. <span data-ttu-id="63d39-150">구독 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-150">To create a subscription client, replace that line with the following code:</span></span>

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
    ```

1. <span data-ttu-id="63d39-151">`RegisterMessageHandler()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-151">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="63d39-152">메시지 처리 옵션을 구성하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-152">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="63d39-153">메시지 처리기를 등록하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-153">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="63d39-154">`ProcessMessagesAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-154">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="63d39-155">이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-155">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="63d39-156">들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-156">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="63d39-157">구독에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-157">To remove the received message from the subscription, on the next line, add the following code:</span></span>

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="63d39-158">`MainAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-158">Return to the `MainAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the subscription here
    ```

1. <span data-ttu-id="63d39-159">Service Bus 연결을 닫으려면 해당 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-159">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. <span data-ttu-id="63d39-160">Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-160">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-a-topic-subscription"></a><span data-ttu-id="63d39-161">항목 구독에서 메시지 검색</span><span class="sxs-lookup"><span data-stu-id="63d39-161">Retrieve a message from a topic subscription</span></span>

<span data-ttu-id="63d39-162">영업 실적 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-162">To run the component that retrieves a message about sales performance, follow these steps:</span></span>

1. <span data-ttu-id="63d39-163">Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-163">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="63d39-164">**디버그** 창의 드롭다운 목록에서 **Performance Message Receiver 시작**을 선택한 다음, **F5**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-164">In the **Debug** pane, in the drop-down list, select **Launch Performance Message Receiver**, and then press **F5**.</span></span> <span data-ttu-id="63d39-165">Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-165">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="63d39-166">프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-166">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="63d39-167">메시지가 수신되어 콘솔에 표시되었으면 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-167">When you see that the message has been received and displayed in the console, on the **Debug** menu, click **Stop Debugging**.</span></span>

1. <span data-ttu-id="63d39-168">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-168">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="63d39-169">Service Bus 네임스페이스가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음, 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-169">If the Service Bus namespace is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="63d39-170">**Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **항목**을 클릭한 다음, **salesperformancemessages** 항목을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-170">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Topics**, and then click the **salesperformancemessages** topic.</span></span> <span data-ttu-id="63d39-171">응용 프로그램이 하나뿐이었던 메시지를 처리하여 제거했으므로 구독 목록의 **아메리카** 구독에는 메시지가 표시되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-171">In the list of subscriptions, there should be zero messages displayed in the **Americas** subscription because your application has processed and removed the only message.</span></span> <span data-ttu-id="63d39-172">**유럽** 구독에는 여전히 메시지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="63d39-172">Notice that the message is still present in the **Europe** subscription.</span></span>
