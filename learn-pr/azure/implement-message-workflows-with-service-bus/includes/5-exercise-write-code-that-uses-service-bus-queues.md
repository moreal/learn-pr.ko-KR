<span data-ttu-id="e5584-101">Service Bus 큐를 사용하여 영업 사원이 사용하는 모바일 앱과 Azure에서 호스팅되는 웹 서비스(각 판매 관련 세부 정보를 SQL Server Database에 저장함) 간에 개별 판매 관련 메시지를 교환하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-101">You've chosen to use a Service Bus queue to exchange messages about individual sales between the mobile app that your sales personnel use and the web service, hosted in Azure, that will store details about each sale in an Azure SQL Database.</span></span>

<span data-ttu-id="e5584-102">Azure 구독에서 필요한 개체는 이미 구현한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-102">You've already implemented the necessary objects in your Azure subscription.</span></span> <span data-ttu-id="e5584-103">이제 메시지를 해당 큐로 보내고 메시지를 검색하는 코드를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-103">Now you want to write code that sends messages to that queue and retrieves messages.</span></span>

## <a name="clone-and-open-the-starter-application"></a><span data-ttu-id="e5584-104">시작 응용 프로그램 복제 및 열기</span><span class="sxs-lookup"><span data-stu-id="e5584-104">Clone and open the starter application</span></span>

<span data-ttu-id="e5584-105">이 단원에서는 **Visual Studio Code**에서 콘솔 응용 프로그램 두 개를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-105">In this unit, you'll build two console applications in **Visual Studio Code**.</span></span> <span data-ttu-id="e5584-106">첫 번째 응용 프로그램은 메시지를 Service Bus 큐에 저장하고, 두 번째 응용 프로그램은 메시지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-106">The first places messages into a Service Bus queue and the second retrieves them.</span></span> <span data-ttu-id="e5584-107">이러한 응용 프로그램은 단일 .NET Core 솔루션의 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-107">The applications are part of a single .NET Core solution.</span></span> 

<span data-ttu-id="e5584-108">먼저 솔루션을 복제합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-108">Start by cloning the solution:</span></span>

1. <span data-ttu-id="e5584-109">명령 프롬프트를 시작하여 응용 프로그램의 소스 코드를 호스팅하려는 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-109">Start a command prompt and change to the directory where you want to host the source code for the application.</span></span>

1. <span data-ttu-id="e5584-110">다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-110">Type the following command and then press **Enter**:</span></span>

    ```powershell
    git clone https:\\ <!-- TODO: (add git URL) -->
    ```

1. <span data-ttu-id="e5584-111">복제 작업이 완료되면 시작 폴더로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-111">When the clone operation is complete, change to the starter folder.</span></span>

1. <span data-ttu-id="e5584-112">다음 명령을 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-112">Type the following command and then press **Enter**.</span></span>

    ```powershell
    code .
    ```

1. <span data-ttu-id="e5584-113">종속성을 복원할지 묻는 메시지가 표시되면 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-113">If a message appears asking if you want to restore dependencies, click **Yes**.</span></span>

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="e5584-114">Service Bus 네임스페이스에 대한 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="e5584-114">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="e5584-115">Service Bus 네임스페이스에 액세스하고 큐를 사용하려면 콘솔 앱에서 두 가지 정보를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-115">In order to access a Service Bus namespace and use a queue, you must configure two pieces of information in your console apps:</span></span>

* <span data-ttu-id="e5584-116">네임스페이스용 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="e5584-116">The endpoint for your namespace</span></span>
* <span data-ttu-id="e5584-117">인증용 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="e5584-117">The shared access key for authentication</span></span>

<span data-ttu-id="e5584-118">이 두 값은 전체 연결 문자열 형식으로 Azure Portal에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-118">Both of these values can be obtained from the Azure portal in the form of a complete connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="e5584-119">여기서는 작업을 쉽게 수행할 수 있도록 두 콘솔 응용 프로그램의 **Program.cs**에서 연결 문자열을 하드 코드합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-119">For simplicity, you will hard code the connection string in the **Program.cs** of both console applications.</span></span> <span data-ttu-id="e5584-120">프로덕션 응용 프로그램에서는 구성 파일이나 Azure Key Vault를 사용하여 연결 문자열을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-120">In a production application, you might use a configuration file or even Azure Key Vault to store the connection string.</span></span>

1. <span data-ttu-id="e5584-121">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-121">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="e5584-122">홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-122">In the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="e5584-123">**설정** 아래에서 **공유 액세스 정책**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-123">Under **SETTINGS**, click **Shared Access Policies**.</span></span>

1. <span data-ttu-id="e5584-124">정책 목록에서 **RootManageSharedAccessKey**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-124">In the list of policies, click **RootManageSharedAccessKey**.</span></span>

1. <span data-ttu-id="e5584-125">**기본 연결 문자열** 텍스트 상자 오른쪽에서 **복사하려면 클릭** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-125">To the right of the **Primary Connection string** textbox, click the **Click to copy** button.</span></span>

1. <span data-ttu-id="e5584-126">**Visual Studio Code**로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-126">Switch to **Visual Studio Code**.</span></span>

1. <span data-ttu-id="e5584-127">**탐색기** 창의 **privatemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-127">In the **Explorer** pane, in the **privatemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="e5584-128">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-128">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="e5584-129">따옴표 사이에 커서를 놓고 **Ctrl+V**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-129">Place the cursor between the quotation marks and then press **Ctrl-V**.</span></span>

1. <span data-ttu-id="e5584-130">**탐색기** 창의 **privatemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-130">In the **Explorer** pane, in the **privatemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="e5584-131">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-131">Locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. <span data-ttu-id="e5584-132">따옴표 사이에 커서를 놓고 **Ctrl+V**를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-132">Place the cursor between the quotation marks and then press **Ctrl-V**.</span></span>

1. <span data-ttu-id="e5584-133">**파일**을 클릭한 다음 **모두 저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-133">Click **File** and then click **Save All**.</span></span>

1. <span data-ttu-id="e5584-134">열려 있는 편집기 창을 모두 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-134">Close all open editor windows.</span></span>

## <a name="write-code-that-sends-a-message-to-the-queue"></a><span data-ttu-id="e5584-135">큐에 메시지를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="e5584-135">Write code that sends a message to the queue</span></span>

<span data-ttu-id="e5584-136">판매 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-136">To complete the component that sends messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="e5584-137">Visual Studio Code **탐색기** 창의 **privatemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-137">In Visual Studio Code, in the **Explorer** pane, in the **privatemessagesender** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="e5584-138">`SendSalesMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-138">Locate the `SendSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="e5584-139">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-139">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Queue Client here
    ```

1. <span data-ttu-id="e5584-140">큐 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-140">To create a queue client, replace that line of code with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="e5584-141">`try...catch` 블록 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-141">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="e5584-142">큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-142">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="e5584-143">콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-143">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="e5584-144">큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-144">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.SendAsync(message);
    ```

1. <span data-ttu-id="e5584-145">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-145">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the queue here
    ```

1. <span data-ttu-id="e5584-146">Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-146">To close the connection the Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="e5584-147">Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-147">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="send-a-message-to-the-queue"></a><span data-ttu-id="e5584-148">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="e5584-148">Send a message to the queue</span></span>

<span data-ttu-id="e5584-149">판매 관련 메시지를 보내는 구성 요소를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-149">To run the component that sends a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="e5584-150">Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-150">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="e5584-151">**디버그** 창의 드롭다운 목록에서 **Private Message Sender 시작**을 선택하고 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-151">In the **Debug** pane, in the drop-down list, select **Launch Private Message Sender** and then press **F5**.</span></span> <span data-ttu-id="e5584-152">Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-152">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="e5584-153">프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-153">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="e5584-154">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-154">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="e5584-155">Service Bus가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-155">If the Service Bus is not displayed, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="e5584-156">**Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음 **salesmessages** 큐를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-156">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Queues**, and then click the **salesmessages** queue.</span></span> <span data-ttu-id="e5584-157">**활성 메시지 수**에 메시지 1개가 큐에 추가되었음이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-157">The **ACTIVE MESSAGE COUNT** should indicate that one message has been added to the queue.</span></span>

## <a name="write-code-that-receives-a-message-from-the-queue"></a><span data-ttu-id="e5584-158">큐에서 메시지를 받는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="e5584-158">Write code that receives a message from the queue</span></span>

<span data-ttu-id="e5584-159">판매 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-159">To complete the component that retrieves messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="e5584-160">Visual Studio Code **탐색기** 창의 **privatemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-160">In Visual Studio Code, in the **Explorer** pane, in the **privatemessagereceiver** folder, click the **Program.cs** file.</span></span>

1. <span data-ttu-id="e5584-161">`ReceiveSalesMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-161">Locate the `ReceiveSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="e5584-162">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-162">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a Queue Client here
    ```

1. <span data-ttu-id="e5584-163">큐 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-163">To create a queue client, replace that line with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="e5584-164">`RegisterMessageHandler()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-164">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="e5584-165">메시지 처리 옵션을 구성하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-165">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="e5584-166">메시지 처리기를 등록하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-166">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="e5584-167">`ProcessMessagesAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-167">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="e5584-168">이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-168">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="e5584-169">들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-169">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="e5584-170">큐에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-170">To remove the received message from the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="e5584-171">`ReceiveSalesMessageAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-171">Return to the `ReceiveSalesMessageAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the queue here
    ```

1. <span data-ttu-id="e5584-172">Service Bus 연결을 닫으려면 해당 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-172">To close the connection to Service Bus, replace that code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="e5584-173">Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-173">In Visual Studio Code, close all editor windows and save all changed files.</span></span>

## <a name="retrieve-a-message-from-the-queue"></a><span data-ttu-id="e5584-174">큐에서 메시지 검색</span><span class="sxs-lookup"><span data-stu-id="e5584-174">Retrieve a message from the queue</span></span>

<span data-ttu-id="e5584-175">판매 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-175">To run the component that retrieves a message about a sale, follow these steps:</span></span>

1. <span data-ttu-id="e5584-176">Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-176">In Visual Studio Code, on the **View** menu, click **Debug**.</span></span>

1. <span data-ttu-id="e5584-177">**디버그** 창의 드롭다운 목록에서 **Private Message Receiver 시작**을 선택하고 **F5** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-177">In the **Debug** pane, in the drop-down list, select **Launch Private Message Receiver** and then press **F5**.</span></span> <span data-ttu-id="e5584-178">Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-178">Visual Studio Code builds and runs the console application in debugging mode.</span></span>

1. <span data-ttu-id="e5584-179">프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-179">As the program executes, examine the messages in the **Debug Console**.</span></span>

1. <span data-ttu-id="e5584-180">메시지가 수신되어 콘솔에 표시되었으면 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-180">When you see that the message has been received and displayed in the console, on the **Debug** menu, click **Stop Debugging**.</span></span>

1. <span data-ttu-id="e5584-181">Azure Portal로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-181">Switch to the Azure portal.</span></span>

1. <span data-ttu-id="e5584-182">Service Bus가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-182">If the Service Bus is not display, in the home page, click **All Resources**, and then click the Service Bus namespace you created earlier.</span></span>

1. <span data-ttu-id="e5584-183">**Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음 **salesmessages** 큐를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-183">In the **Service Bus Namespace** blade, under **ENTITIES**, click **Queues**, and then click the **salesmessages** queue.</span></span> <span data-ttu-id="e5584-184">**활성 메시지 수**에 메시지가 큐에서 제거되었음이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-184">The **ACTIVE MESSAGE COUNT** should indicate that the message has been removed from the queue.</span></span>

<span data-ttu-id="e5584-185">Service Bus 큐에 개별 판매 관련 메시지를 보내는 코드를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-185">You have written code that sends a message about individual sales to a Service Bus queue.</span></span> <span data-ttu-id="e5584-186">영업용 분산 응용 프로그램에서는 영업 사원이 장치에서 사용하는 모바일 앱에서 이 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-186">In the sales force distributed application, you should write this code in the mobile app that Sales personnel use on the devices.</span></span>

<span data-ttu-id="e5584-187">또한 Service Bus 큐에서 메시지를 수신하는 코드도 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-187">You have also written code that receives a message from Service Bus queue.</span></span> <span data-ttu-id="e5584-188">영업용 분산 응용 프로그램에서는 Azure에서 실행되며 받은 메시지를 처리하는 웹 서비스에서 이 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e5584-188">In the sales force distributed application, you should write this code in the web service that runs in Azure and processes received messages.</span></span>
