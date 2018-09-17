Service Bus 큐를 사용하여 영업 사원이 사용하는 모바일 앱과 Azure에서 호스팅되는 웹 서비스(각 판매 관련 세부 정보를 SQL Server Database 인스턴스에 저장함) 간에 개별 판매 관련 메시지를 교환하도록 선택했습니다.

Azure 구독에서 필요한 개체는 이미 구현한 상태입니다. 이제 메시지를 해당 큐로 보내고 메시지를 검색하는 코드를 작성하려고 합니다.

## <a name="clone-and-open-the-starter-application"></a>시작 응용 프로그램 복제 및 열기

이 단원에서는 **Visual Studio Code**에서 콘솔 응용 프로그램 두 개를 빌드합니다. 첫 번째 응용 프로그램은 메시지를 Service Bus 큐에 저장하고, 두 번째 응용 프로그램은 메시지를 검색합니다. 이러한 응용 프로그램은 단일 .NET Core 솔루션의 일부분입니다. 

먼저 솔루션을 복제합니다.

1. 명령 프롬프트를 시작하여 응용 프로그램의 소스 코드를 호스팅하려는 디렉터리로 변경합니다.

1. 다음 명령을 입력한 다음, **Enter** 키를 누릅니다.

    ```powershell
    git clone https:\\ <!-- TODO: (add git URL) -->
    ```

1. 복제 작업이 완료되면 시작 폴더로 변경합니다.

1. 다음 명령을 입력한 다음, **Enter** 키를 누릅니다.

    ```powershell
    code .
    ```

1. 종속성을 복원할지 묻는 메시지가 표시되면 **예**를 클릭합니다.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Service Bus 네임스페이스에 대한 연결 문자열 구성

Service Bus 네임스페이스에 액세스하고 큐를 사용하려면 콘솔 앱에서 두 가지 정보를 구성해야 합니다.

* 네임스페이스용 엔드포인트
* 인증용 공유 액세스 키

이 두 값은 전체 연결 문자열 형식으로 Azure Portal에서 가져올 수 있습니다.

> [!NOTE]
> 여기서는 작업을 쉽게 수행할 수 있도록 두 콘솔 응용 프로그램의 **Program.cs** 파일에서 연결 문자열을 하드 코드합니다. 프로덕션 응용 프로그램에서는 구성 파일이나 Azure Key Vault를 사용하여 연결 문자열을 저장할 수 있습니다.

1. Azure Portal로 전환합니다.

1. 홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.

1. **설정** 아래에서 **공유 액세스 정책**을 클릭합니다.

1. 정책 목록에서 **RootManageSharedAccessKey**를 클릭합니다.

1. **기본 연결 문자열** 텍스트 상자 오른쪽에서 **복사하려면 클릭** 단추를 클릭합니다.

1. **Visual Studio Code**로 전환합니다.

1. **탐색기** 창의 **privatemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이에 커서를 놓은 다음, **Ctrl+V**를 누릅니다.

1. **탐색기** 창의 **privatemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이에 커서를 놓은 다음, **Ctrl+V**를 누릅니다.

1. **파일**을 클릭한 다음, **모두 저장**을 클릭합니다.

1. 열려 있는 편집기 창을 모두 닫습니다.

## <a name="write-code-that-sends-a-message-to-the-queue"></a>큐에 메시지를 보내는 코드 작성

판매 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. Visual Studio Code **탐색기** 창의 **privatemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. `SendSalesMessageAsync()` 메서드를 찾습니다.

1. 이 메서드 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create a queue client here
    ```

1. 큐 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. `try...catch` 블록 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create and send a message here
    ```

1. 큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    string messageBody = $"$10,000 order for bicycle parts from retailer Adventure Works.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. 콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. 큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    await queueClient.SendAsync(message);
    ```

1. 다음 코드 줄을 찾습니다.

    ```C#
    // Close the connection to the queue here
    ```

1. Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    await queueClient.CloseAsync();
    ```

1. Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.

## <a name="send-a-message-to-the-queue"></a>큐에 메시지 보내기

판매 관련 메시지를 보내는 구성 요소를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.

1. **디버그** 창의 드롭다운 목록에서 **Private Message Sender 시작**을 선택한 다음, **F5**를 누릅니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임스페이스가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음, 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음, **salesmessages** 큐를 클릭합니다. **활성 메시지 수**에 메시지 1개가 큐에 추가되었음이 표시되어야 합니다.

## <a name="write-code-that-receives-a-message-from-the-queue"></a>큐에서 메시지를 받는 코드 작성

판매 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. Visual Studio Code **탐색기** 창의 **privatemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. `ReceiveSalesMessageAsync()` 메서드를 찾습니다.

1. 이 메서드 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create a queue client here
    ```

1. 큐 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.

    ```C#
    queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
    ```

1. `RegisterMessageHandler()` 메서드를 찾습니다.

1. 메시지 처리 옵션을 구성하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.

    ```C#
    var messageHandlerOptions = new MessageHandlerOptions(ExceptionReceivedHandler)
    {
        MaxConcurrentCalls = 1,
        AutoComplete = false
    };
    ```

1. 메시지 처리기를 등록하려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    queueClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. `ProcessMessagesAsync()` 메서드를 찾습니다. 이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.

1. 들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.

    ```C#
    Console.WriteLine($"Received message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. 큐에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    await queueClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. `ReceiveSalesMessageAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.

    ```C#
    // Close the queue here
    ```

1. Service Bus 연결을 닫으려면 해당 줄을 다음 코드로 바꿉니다.

    ```C#
    await queueClient.CloseAsync();
    ```

1. Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.

## <a name="retrieve-a-message-from-the-queue"></a>큐에서 메시지 검색

판매 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.

1. **디버그** 창의 드롭다운 목록에서 **Private Message Receiver 시작**을 선택한 다음, **F5**를 누릅니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. 메시지가 수신되어 콘솔에 표시되었으면 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임스페이스가 표시되지 않으면 홈페이지에서 **모든 리소스**를 클릭한 다음, 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음, **salesmessages** 큐를 클릭합니다. **활성 메시지 수**에 메시지가 큐에서 제거되었음이 표시되어야 합니다.

Service Bus 큐에 개별 판매 관련 메시지를 보내는 코드를 작성했습니다. 영업용 분산 응용 프로그램에서는 영업 사원이 장치에서 사용하는 모바일 앱에서 이 코드를 작성해야 합니다.

Service Bus 큐에서 메시지를 수신하는 코드도 작성했습니다. 영업용 분산 응용 프로그램에서는 Azure에서 실행되며 받은 메시지를 처리하는 웹 서비스에서 이 코드를 작성해야 합니다.
