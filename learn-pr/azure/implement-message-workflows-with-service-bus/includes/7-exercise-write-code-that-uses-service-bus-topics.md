영업 분산 응용 프로그램에서 판매 실적에 대 한 메시지를 분산 하는 Azure Service Bus 토픽을 사용 하기로 했습니다. 앱 판매 직원이 모바일 장치에서 사용 하는 각 영역과 시간 기간에 대 한 판매 수치를 요약 하는 메시지를 보낼 됩니다. 이러한 메시지는 아메리카/유럽을 비롯하여 회사가 사업을 운영하는 지역에 있는 웹 서비스로 배포됩니다.

항목과 구독을 포함해 Azure 구독에서 필요한 인프라는 이미 구현한 상태입니다. 이제 토픽에 메시지를 전송 하 고 각 구독에서 메시지를 검색 하는 코드를 작성 하려고 합니다.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Service Bus 네임스페이스에 대한 연결 문자열 구성

송신 및 수신 구성 요소에서 연결 문자열 모두를 구성 하 여 시작 합니다.

1. Azure Portal로 전환합니다.

1. 홈페이지에서 **모든 리소스**를 클릭한 다음 앞에서 만든 Service Bus 네임스페이스를 클릭합니다.

1. **설정** 아래에서 **공유 액세스 정책**을 클릭합니다.

1. 정책 목록에서 **RootManageSharedAccessKey**를 클릭합니다.

1. 오른쪽에는 **기본 연결 문자열** 텍스트 상자 클릭 합니다 **복사 하려면 클릭** 단추입니다.

1. **Visual Studio Code**로 전환합니다.

1. **탐색기** 창의 **performancemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이 커서를 놓고 누릅니다 **Ctrl + V**합니다.

1. **탐색기** 창의 **performancemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. 다음 코드 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

1. 따옴표 사이 커서를 놓고 누릅니다 **Ctrl + V**합니다.

1. 클릭 **파일**를 클릭 하 고 **모두 저장**합니다.

1. 열려 있는 편집기 창을 모두 닫습니다.

## <a name="write-code-that-sends-a-message-to-the-topic"></a>항목에 메시지를 보내는 코드 작성

영업 실적 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. Visual Studio Code **탐색기** 창의 **performancemessagesender** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. `SendPerformanceMessageAsync()` 메서드를 찾습니다.

1. 이 메서드 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create a Topic Client here
    ```

1. 항목 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    topicClient = new TopicClient(ServiceBusConnectionString, TopicName);
    ```

1. `try...catch` 블록 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create and send a message here
    ```

1. 큐용 메시지를 만들고 메시지 서식을 지정하려면 해당 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    string messageBody = $"Total sales for Brazil in August: $13m.";
    var message = new Message(Encoding.UTF8.GetBytes(messageBody));
    ```

1. 콘솔에서 메시지를 표시하려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    Console.WriteLine($"Sending message: {messageBody}");
    ```

1. 큐에 메시지를 보내려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    await topicClient.SendAsync(message);
    ```

1. 다음 코드 줄을 찾습니다.

    ```C#
    // Close the connection to the topic here
    ```

1. Service Bus에 대 한 연결을 닫으려면이 코드 줄을을 다음 코드로 바꿉니다.

    ```C#
    await topicClient.CloseAsync();
    ```

1. Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.

## <a name="send-a-message-to-the-topic"></a>항목에 메시지 보내기

판매 관련 메시지를 보내는 구성 요소를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.

1. 에 **디버그** 창의 드롭 다운 목록에서 **시작 성능 메시지 보낸 사람**을 누릅니다 **F5**합니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임 스페이스 표시 되지 않으면 홈 페이지에서 클릭 **모든 리소스**, 그런 다음 앞에서 만든 Service Bus 네임 스페이스를 클릭 합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **항목**을 클릭한 다음 **salesperformancemessages** 항목을 클릭합니다. 구독 목록의 **아메리카** 및 **유럽** 구독에 모두 메시지 하나가 표시되어야 합니다.

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a>항목 구독에서 메시지를 받는 코드 작성

영업 실적 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. Visual Studio Code **탐색기** 창의 **performancemessagereceiver** 폴더에서 **Program.cs** 파일을 클릭합니다.

1. `MainAsync()` 메서드를 찾습니다.

1. 이 메서드 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create a subscription client here
    ```

1. 구독 클라이언트를 만들려면 해당 줄을 다음 코드로 바꿉니다.

    ```C#
    subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, TopicName, SubscriptionName);
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
    subscriptionClient.RegisterMessageHandler(ProcessMessagesAsync, messageHandlerOptions);
    ```

1. `ProcessMessagesAsync()` 메서드를 찾습니다. 이 메서드는 들어오는 메시지를 처리하는 메서드로 등록했습니다.

1. 들어오는 메시지를 콘솔에 표시하려면 해당 메서드 내의 모든 코드를 다음 코드로 바꿉니다.

    ```C#
    Console.WriteLine($"Received sale performance message: SequenceNumber:{message.SystemProperties.SequenceNumber} Body:{Encoding.UTF8.GetString(message.Body)}");
    ```

1. 구독에서 수신된 메시지를 제거하려면 다음 줄에 아래 코드를 추가합니다.

    ```C#
    await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
    ```

1. `MainAsync()` 메서드로 돌아와서 다음 코드 줄을 찾습니다.

    ```C#
    // Close the subscription here
    ```

1. Service Bus 연결을 닫으려면 해당 코드를 다음 코드로 바꿉니다.

    ```C#
    await subscriptionClient.CloseAsync();
    ```

1. Visual Studio Code에서 편집기 창을 모두 닫고 변경된 파일을 모두 저장합니다.

## <a name="retrieve-a-message-from-a-topic-subscription"></a>항목 구독에서 메시지 검색

영업 실적 관련 메시지를 검색하는 구성 요소를 실행하려면 다음 단계를 수행합니다.

1. Visual Studio Code의 **보기** 메뉴에서 **디버그**를 클릭합니다.

1. 에 **디버그** 창의 드롭 다운 목록에서 **시작 성능 메시지 받는 사람**를 누릅니다 **F5**합니다. Visual Studio Code가 디버깅 모드에서 콘솔 응용 프로그램을 빌드하고 실행합니다.

1. 프로그램이 실행되면 **디버그 콘솔**에서 메시지를 검사합니다.

1. 메시지가 수신되어 콘솔에 표시되었으면 **디버그** 메뉴에서 **디버깅 중지**를 클릭합니다.

1. Azure Portal로 전환합니다.

1. Service Bus 네임 스페이스 표시 되지 않으면 홈 페이지에서 클릭 **모든 리소스**, 그런 다음 앞에서 만든 Service Bus 네임 스페이스를 클릭 합니다.

1. **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **항목**을 클릭한 다음 **salesperformancemessages** 항목을 클릭합니다. 응용 프로그램이 하나뿐이었던 메시지를 처리하여 제거했으므로 구독 목록의 **아메리카** 구독에는 메시지가 표시되지 않아야 합니다. **유럽** 구독에는 여전히 메시지가 있습니다.
