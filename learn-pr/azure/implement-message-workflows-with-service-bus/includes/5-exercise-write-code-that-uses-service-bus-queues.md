Service Bus 큐에 판매 직원이 사용 하는 모바일 앱 및 Azure SQL Database 인스턴스에서 각 판매에 대 한 정보를 저장 하는 Azure에 호스트 된 웹 서비스 간에 개별 판매에 대 한 메시지를 교환 하는 데 선택 했습니다.

Azure 구독에서 필요한 개체는 이미 구현한 상태입니다. 이제 큐에 메시지를 보내고 메시지를 검색 하는 코드를 작성 하려고 합니다.

## <a name="clone-and-open-the-starter-application"></a>시작 응용 프로그램 복제 및 열기

이 단원에서는 **Visual Studio Code**에서 콘솔 응용 프로그램 두 개를 빌드합니다. 첫 번째 응용 프로그램을 Service Bus 큐에 메시지를 배치 하 고 두 번째 검색 합니다. 이러한 응용 프로그램은 단일 .NET Core 솔루션의 일부분입니다. 

먼저 솔루션을 복제합니다.

1. 명령 프롬프트를 시작하여 응용 프로그램의 소스 코드를 호스팅하려는 디렉터리로 변경합니다.

1. 다음 명령을 입력 한 다음 **Enter**:

    ```powershell
    git clone https:\\ <!-- TODO: (add git URL) -->
    ```

1. 복제 작업이 완료되면 시작 폴더로 변경합니다.

1. 다음 명령을 입력 한 다음 **Enter**합니다.

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
> 간단히 하기 위해에서는 하드 코드에서 연결 문자열을 **Program.cs** 모두 콘솔 응용 프로그램의 파일입니다. 프로덕션 응용 프로그램에서는 구성 파일이나 Azure Key Vault를 사용하여 연결 문자열을 저장할 수 있습니다.

1. Azure Portal로 전환합니다.

1. 홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.

1. **설정** 아래에서 **공유 액세스 정책**을 클릭합니다.

1. 정책 목록에서 **RootManageSharedAccessKey**를 클릭합니다.

1. 오른쪽에는 **기본 연결 문자열** 텍스트 상자 클릭 합니다 **복사 하려면 클릭** 단추입니다.

1. **Visual Studio Code**로 전환합니다.

1. **탐색기** 창의 **privatemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이 커서를 놓고 누릅니다 **Ctrl + V**합니다.

1. **탐색기** 창의 **privatemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이 커서를 놓고 누릅니다 **Ctrl + V**합니다.

1. 클릭 **파일**를 클릭 하 고 **모두 저장**합니다.

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

1. 에 **디버그** 창의 드롭 다운 목록에서 **개인 메시지 보낸 사람 시작**를 누릅니다 **F5**합니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임 스페이스 표시 되지 않으면 홈 페이지에서 클릭 **모든 리소스**, 그런 다음 앞에서 만든 Service Bus 네임 스페이스를 클릭 합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음 **salesmessages** 큐를 클릭합니다. **활성 메시지 수**에 메시지 1개가 큐에 추가되었음이 표시되어야 합니다.

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

1. Service Bus에 대 한 연결을 닫으려면 해당 줄을 다음 코드로 바꿉니다.

    ```C#
    await queueClient.CloseAsync();
    ```

1. Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.

## <a name="retrieve-a-message-from-the-queue"></a>큐에서 메시지 검색

판매 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.

1. 에 **디버그** 창의 드롭 다운 목록에서 **시작 개인 메시지 받는 사람**, 누릅니다 **F5**합니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. 메시지가 수신되어 콘솔에 표시되었으면 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임 스페이스 표시 되지 않으면 홈 페이지에서 클릭 **모든 리소스**, 그런 다음 앞에서 만든 Service Bus 네임 스페이스를 클릭 합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **큐**를 클릭한 다음 **salesmessages** 큐를 클릭합니다. **활성 메시지 수**에 메시지가 큐에서 제거되었음이 표시되어야 합니다.

Service Bus 큐에 개별 판매 관련 메시지를 보내는 코드를 작성했습니다. 영업 분산 응용 프로그램에서는 영업 직원이 장치에서 사용 하는 모바일 앱에서이 코드를 작성 해야 합니다.

또한 Service Bus 큐에서 메시지를 수신 하는 코드를 작성 했습니다. 영업용 분산 응용 프로그램에서는 Azure에서 실행되며 받은 메시지를 처리하는 웹 서비스에서 이 코드를 작성해야 합니다.
