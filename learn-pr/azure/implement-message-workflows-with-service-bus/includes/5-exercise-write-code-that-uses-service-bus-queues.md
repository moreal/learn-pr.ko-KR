<span data-ttu-id="756e1-101">Service Bus 큐를 사용하여 영업 사원이 사용하는 모바일 앱과 Azure에서 호스팅되는 웹 서비스(각 판매 관련 세부 정보를 SQL Server Database 인스턴스에 저장함) 간에 개별 판매 관련 메시지를 교환하도록 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-101">You've chosen to use a Service Bus queue to exchange messages about individual sales between the mobile app that your sales personnel use and the web service, hosted in Azure, that will store details about each sale in an Azure SQL Database instance.</span></span>

<span data-ttu-id="756e1-102">Azure 구독에서 필요한 개체는 이미 구현한 상태입니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-102">You've already implemented the necessary objects in your Azure subscription.</span></span> <span data-ttu-id="756e1-103">이제 메시지를 해당 큐로 보내고 메시지를 검색하는 코드를 작성하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-103">Now, you want to write code that sends messages to that queue and retrieves messages.</span></span>

## <a name="clone-and-open-the-starter-application"></a><span data-ttu-id="756e1-104">시작 응용 프로그램 복제 및 열기</span><span class="sxs-lookup"><span data-stu-id="756e1-104">Clone and open the starter application</span></span>

<span data-ttu-id="756e1-105">이 단원에서는 두 개의 콘솔 응용 프로그램을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-105">In this unit, you'll build two console applications.</span></span> <span data-ttu-id="756e1-106">첫 번째 응용 프로그램은 메시지를 Service Bus 큐에 저장하고, 두 번째 응용 프로그램은 메시지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-106">The first application places messages into a Service Bus queue and the second retrieves them.</span></span> <span data-ttu-id="756e1-107">이러한 응용 프로그램은 단일 .NET Core 솔루션의 일부분입니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-107">The applications are part of a single .NET Core solution.</span></span>

1. <span data-ttu-id="756e1-108">먼저 솔루션을 복제합니다. Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-108">Start by cloning the solution: run the following commands in the Cloud Shell:</span></span>

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. <span data-ttu-id="756e1-109">다음으로, 시작 폴더로 디렉터리를 변경하고 Cloud Shell 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-109">Next, change directories into the starter folder and open the Cloud Shell editor.</span></span>

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a><span data-ttu-id="756e1-110">Service Bus 네임스페이스에 대한 연결 문자열 구성</span><span class="sxs-lookup"><span data-stu-id="756e1-110">Configure a connection string to a Service Bus namespace</span></span>

<span data-ttu-id="756e1-111">Service Bus 네임스페이스에 액세스하고 큐를 사용하려면 콘솔 앱에서 두 가지 정보를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-111">In order to access a Service Bus namespace and use a queue, you must configure two pieces of information in your console apps:</span></span>

* <span data-ttu-id="756e1-112">네임스페이스용 엔드포인트</span><span class="sxs-lookup"><span data-stu-id="756e1-112">The endpoint for your namespace</span></span>
* <span data-ttu-id="756e1-113">인증용 공유 액세스 키</span><span class="sxs-lookup"><span data-stu-id="756e1-113">The shared access key for authentication</span></span>

<span data-ttu-id="756e1-114">이 두 값은 전체 연결 문자열 형식으로 Azure Portal에서 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-114">Both of these values can be obtained from the Azure portal in the form of a complete connection string.</span></span>

> [!NOTE]
> <span data-ttu-id="756e1-115">여기서는 작업을 쉽게 수행할 수 있도록 두 콘솔 응용 프로그램의 **Program.cs** 파일에서 연결 문자열을 하드 코드합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-115">For simplicity, you will hard-code the connection string in the **Program.cs** file of both console applications.</span></span> <span data-ttu-id="756e1-116">프로덕션 응용 프로그램에서는 구성 파일이나 Azure Key Vault를 사용하여 연결 문자열을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-116">In a production application, you might use a configuration file or even Azure Key Vault to store the connection string.</span></span>

1. <span data-ttu-id="756e1-117">Cloud Shell에서 Service Bus 네임스페이스에 대한 기본 연결 문자열을 표시하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-117">In the Cloud Shell, run the following command to display the primary connection string for your Service Bus namespace.</span></span> <span data-ttu-id="756e1-118">`<namespace-name>`를 Service Bus 네임스페이스의 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-118">Replace `<namespace-name>` with the name of your Service Bus namespace.</span></span>

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --namespace-name <namespace-name> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv
    ```

    <span data-ttu-id="756e1-119">이 모듈 전체에서 이 연결 문자열이 여러 번 필요하므로 간편하게 사용할 수 있도록 어딘가에 붙여넣어 둘 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-119">You'll be needing this connection string multiple times throughout this module, so you might want to paste it somewhere handy.</span></span>

1. <span data-ttu-id="756e1-120">Cloud Shell에서 키를 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-120">Copy the key from Cloud Shell.</span></span> <span data-ttu-id="756e1-121">편집기에서 **privatemessagesender/Program.cs**를 열고 코드의 다음 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-121">In the editor, open **privatemessagesender/Program.cs** and locate the following line of code:</span></span>

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    <span data-ttu-id="756e1-122">연결 문자열을 따옴표 사이에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-122">Paste the connection string between the quotation marks.</span></span> <span data-ttu-id="756e1-123"><kbd>Ctrl+S</kbd>로 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-123">Save the file with <kbd>Ctrl+S</kbd>.</span></span>

1. <span data-ttu-id="756e1-124">**privatemessagereceiver/Program.cs**에서 이전 단계를 반복하여 동일한 연결 문자열 값을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-124">Repeat the previous step in **privatemessagereceiver/Program.cs**, pasting in the same connection string value.</span></span> <span data-ttu-id="756e1-125">"..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-125">Save the file either through the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

## <a name="write-code-that-sends-a-message-to-the-queue"></a><span data-ttu-id="756e1-126">큐에 메시지를 보내는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="756e1-126">Write code that sends a message to the queue</span></span>

<span data-ttu-id="756e1-127">영업 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-127">To complete the component that sends messages about sales, follow these steps:</span></span>

1. <span data-ttu-id="756e1-128">편집기에서 **privatemessagesender/Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-128">Open **privatemessagesender/Program.cs** in the editor</span></span>

1. <span data-ttu-id="756e1-129">`SendSalesMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-129">Locate the `SendSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="756e1-130">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-130">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="756e1-131">큐 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-131">To create a queue client, replace that line of code with the following code:</span></span>

    ```C#
    var queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="756e1-132">`try...catch` 블록 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-132">Within the `try...catch` block, locate the following line of code:</span></span>

    ```C#
    // Create and send a message here
    ```

1. <span data-ttu-id="756e1-133">큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-133">To create and format a message for the queue, replace that line of code with the following code:</span></span>

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. <span data-ttu-id="756e1-134">콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-134">To display the message in the console, on the next line, add the following code:</span></span>

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. <span data-ttu-id="756e1-135">큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-135">To send the message to the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.SendAsync(message);
    ```

1. <span data-ttu-id="756e1-136">다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-136">Locate the following line of code:</span></span>

    ```C#
    // Close the connection to the queue here
    ```

1. <span data-ttu-id="756e1-137">Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-137">To close the connection the Service Bus, replace that line of code with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="756e1-138">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-138">Save the file.</span></span>

## <a name="send-a-message-to-the-queue"></a><span data-ttu-id="756e1-139">큐에 메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="756e1-139">Send a message to the queue</span></span>

<span data-ttu-id="756e1-140">영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-140">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> <span data-ttu-id="756e1-141">이 연습 중에 앱을 실행하면 `dotnet`에서 처음 실행할 때 원격 원본에서 패키지를 복원하고 앱을 빌드해야 하므로 시작하는 데 시간이 좀 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-141">The apps you run during this exercise may take a moment to start up, as `dotnet` has to restore packages from remote sources and build the apps the first time they are run.</span></span>

<span data-ttu-id="756e1-142">프로그램을 실행하면 메시지를 보내는 중인지 나타내는 출력 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-142">As the program executes, you'll see messages printed indicating that it's sending a message.</span></span> <span data-ttu-id="756e1-143">앱을 실행할 때마다 큐에 메시지가 하나씩 더 추가됩니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-143">Each time you run the app, one additional message will be added to the queue.</span></span>

<span data-ttu-id="756e1-144">완료되면 다음 명령을 실행하여 큐에 얼마나 많은 메시지가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-144">Once it's finished, run the following command to see how many messages are in the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a><span data-ttu-id="756e1-145">큐에서 메시지를 받는 코드 작성</span><span class="sxs-lookup"><span data-stu-id="756e1-145">Write code that receives a message from the queue</span></span>

1. <span data-ttu-id="756e1-146">편집기에서 **privatemessagereceiver/Program.cs**를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-146">Open **privatemessagereceiver/Program.cs** in the editor</span></span>

1. <span data-ttu-id="756e1-147">`ReceiveSalesMessageAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-147">Locate the `ReceiveSalesMessageAsync()` method.</span></span>

1. <span data-ttu-id="756e1-148">이 메서드 내에서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-148">Within that method, locate the following line of code:</span></span>

    ```C#
    // Create a queue client here
    ```

1. <span data-ttu-id="756e1-149">큐 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-149">To create a queue client, replace that line with the following code:</span></span>

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. <span data-ttu-id="756e1-150">`RegisterMessageHandler()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-150">Locate the `RegisterMessageHandler()` method.</span></span>

1. <span data-ttu-id="756e1-151">메시지 처리 옵션을 구성하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-151">To configure message handling options, replace all the code within that method with the following code:</span></span>

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. <span data-ttu-id="756e1-152">메시지 처리기를 등록하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-152">To register the message handler, on the next line, add the following code:</span></span>

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. <span data-ttu-id="756e1-153">`ProcessMessagesAsync()` 메서드를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-153">Locate the `ProcessMessagesAsync()` method.</span></span> <span data-ttu-id="756e1-154">이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-154">You have registered this method as the one that handles incoming messages.</span></span>

1. <span data-ttu-id="756e1-155">들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-155">To display incoming messages in the console, replace all the code within that method with the following code:</span></span>

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. <span data-ttu-id="756e1-156">큐에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-156">To remove the received message from the queue, on the next line, add the following code:</span></span>

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. <span data-ttu-id="756e1-157">`ReceiveSalesMessageAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-157">Return to the `ReceiveSalesMessageAsync()` method and locate the following line of code:</span></span>

    ```C#
    // Close the queue here
    ```

1. <span data-ttu-id="756e1-158">Service Bus 연결을 닫으려면 해당 줄을 다음 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-158">To close the connection to Service Bus, replace that line with the following code:</span></span>

    ```C#
    await queueClient.CloseAsync();
    ```

1. <span data-ttu-id="756e1-159">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-159">Save the file.</span></span>

## <a name="retrieve-a-message-from-the-queue"></a><span data-ttu-id="756e1-160">큐에서 메시지 검색</span><span class="sxs-lookup"><span data-stu-id="756e1-160">Retrieve a message from the queue</span></span>

<span data-ttu-id="756e1-161">영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-161">To run the component that sends a message about a sale, run this command in the Cloud Shell:</span></span>

```bash
dotnet run -p privatemessagereceiver
```

<span data-ttu-id="756e1-162">메시지가 수신되어 콘솔에 표시되었으면 `Enter`를 눌러 앱을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-162">When you see that the message has been received and displayed in the console, press `Enter` to stop the app.</span></span> <span data-ttu-id="756e1-163">그런 다음, 전과 동일한 명령을 실행하여 모든 메시지가 큐에서 제거되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-163">Then, run the same command as before to confirm that all of the messages have been removed from the queue:</span></span>

```azurecli
az servicebus queue show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

<span data-ttu-id="756e1-164">모든 메시지가 제거된 경우에는 `0`이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-164">This will show `0` if all the messages have been removed.</span></span>

<span data-ttu-id="756e1-165">Service Bus 큐에 개별 영업 관련 메시지를 보내는 코드를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-165">You have written code that sends a message about individual sales to a Service Bus queue.</span></span> <span data-ttu-id="756e1-166">영업용 분산 응용 프로그램에서는 영업 사원이 장치에서 사용하는 모바일 앱에서 이 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-166">In the sales force distributed application, you should write this code in the mobile app that sales personnel use on devices.</span></span>

<span data-ttu-id="756e1-167">Service Bus 큐에서 메시지를 수신하는 코드도 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-167">You have also written code that receives a message from the Service Bus queue.</span></span> <span data-ttu-id="756e1-168">영업용 분산 응용 프로그램에서는 Azure에서 실행되며 받은 메시지를 처리하는 웹 서비스에서 이 코드를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="756e1-168">In the sales force distributed application, you should write this code in the web service that runs in Azure and processes received messages.</span></span>
