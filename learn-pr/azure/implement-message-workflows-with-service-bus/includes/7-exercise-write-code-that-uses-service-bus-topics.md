영업용 분산 응용 프로그램에서 Azure Service Bus 항목을 사용하여 영업 실적 관련 메시지를 배포하기로 선택했습니다. 영업 사원이 모바일 장치에서 사용하는 앱이 각 지역과 기간의 판매 수치가 요약된 메시지를 전송하게 됩니다. 이러한 메시지는 아메리카/유럽을 비롯하여 회사가 사업을 운영하는 지역에 있는 웹 서비스로 배포됩니다.

항목과 구독을 포함해 Azure 구독에서 필요한 인프라는 이미 구현한 상태입니다. 이제 메시지를 해당 항목으로 보내고 구독에서 메시지를 검색하는 코드를 작성하려고 합니다.

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Service Bus 네임스페이스에 대한 연결 문자열 구성

먼저 송신 및 수신 구성 요소에서 연결 문자열을 구성합니다.

1. 편집기에서 **performancemessagesender/Program.cs**를 열고 코드의 다음 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    따옴표 사이에 연결 문자열을 붙여넣고 "..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 파일을 저장합니다.

1. **performancemessagereceiver/Program.cs**에서 이전 단계를 반복하여 동일한 연결 문자열 값을 붙여넣고 파일을 저장합니다.

## <a name="write-code-that-sends-a-message-to-the-topic"></a>토픽에 메시지를 보내는 코드 작성

영업 실적 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. 편집기에서 **performancemessagesender/Program.cs**를 엽니다.

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

1. Service Bus 연결을 닫으려면 해당 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    await topicClient.CloseAsync();
    ```

1. 파일을 저장합니다.

## <a name="send-a-message-to-the-topic"></a>항목에 메시지 보내기

영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.

```bash
dotnet run -p performancemessagesender
```

프로그램을 실행하면 메시지를 보내는 중인지 나타내는 출력 메시지가 표시됩니다. 앱을 실행할 때마다 항목에 메시지가 하나씩 더 추가되며 각 구독자는 복사본을 받게 됩니다.

완료되면 다음 명령을 실행하여 아메리카 구독에 얼마나 많은 메시지가 있는지 확인합니다.

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

`Americas`를 `EuropeAndAfrica`로 바꾸면 두 구독에 모두 동일한 수의 메시지가 표시됩니다.

## <a name="write-code-that-receives-a-message-from-a-topic-subscription"></a>항목 구독에서 메시지를 받는 코드 작성

영업 실적 관련 메시지를 검색하는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. 편집기에서 **performancemessagereceiver/Program.cs**를 엽니다.

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

```bash
dotnet run -p performancemessagereceiver
```

프로그램이 메시지를 수신하는 중인 알림의 인쇄를 중지하는 경우 `Enter`를 눌러 앱을 중지합니다. 그런 다음, 전과 동일한 명령을 실행하여 `Americas` 구독에 남은 메시지가 없음을 확인합니다.

```azurecli
az servicebus topic subscription show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --topic-name salesperformancemessages \
    --name Americas \
    --query messageCount
```

`Americas`를 `EuropeAndAfrica`로 바꾸는 경우 메시지 수는 변경되지 않았음을 확인할 수 있습니다. 응용 프로그램은 `Americas` 구독에서만 메시지를 수신했습니다.
