Service Bus 큐를 사용하여 영업 사원이 사용하는 모바일 앱과 Azure에서 호스팅되는 웹 서비스(각 판매 관련 세부 정보를 SQL Server Database 인스턴스에 저장함) 간에 개별 판매 관련 메시지를 교환하도록 선택했습니다.

Azure 구독에서 필요한 개체는 이미 구현한 상태입니다. 이제 메시지를 해당 큐로 보내고 메시지를 검색하는 코드를 작성하려고 합니다.

## <a name="clone-and-open-the-starter-application"></a>시작 응용 프로그램 복제 및 열기

이 단원에서는 두 개의 콘솔 응용 프로그램을 빌드합니다. 첫 번째 응용 프로그램은 메시지를 Service Bus 큐에 저장하고, 두 번째 응용 프로그램은 메시지를 검색합니다. 이러한 응용 프로그램은 단일 .NET Core 솔루션의 일부분입니다.

1. 먼저 솔루션을 복제합니다. Cloud Shell에서 다음 명령을 실행합니다.

```bash
cd ~
git clone https://github.com/MicrosoftDocs/mslearn-connect-services-together.git
```

2. 다음으로, 시작 폴더로 디렉터리를 변경하고 Cloud Shell 편집기를 엽니다.

```bash
cd mslearn-connect-services-together/implement-message-workflows-with-service-bus/src/start
code .
```

## <a name="configure-a-connection-string-to-a-service-bus-namespace"></a>Service Bus 네임스페이스에 대한 연결 문자열 구성

Service Bus 네임스페이스에 액세스하고 큐를 사용하려면 콘솔 앱에서 두 가지 정보를 구성해야 합니다.

* 네임스페이스용 엔드포인트
* 인증용 공유 액세스 키

이 두 값은 전체 연결 문자열 형식으로 Azure Portal에서 가져올 수 있습니다.

> [!NOTE]
> 여기서는 작업을 쉽게 수행할 수 있도록 두 콘솔 응용 프로그램의 **Program.cs** 파일에서 연결 문자열을 하드 코드합니다. 프로덕션 응용 프로그램에서는 구성 파일이나 Azure Key Vault를 사용하여 연결 문자열을 저장할 수 있습니다.

1. Cloud Shell에서 Service Bus 네임스페이스에 대한 기본 연결 문자열을 표시하려면 다음 명령을 실행합니다. `<namespace-name>`를 Service Bus 네임스페이스의 이름으로 바꿉니다.

    ```azurecli
    az servicebus namespace authorization-rule keys list \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --namespace-name <namespace-name> \
        --name RootManageSharedAccessKey \
        --query primaryConnectionString \
        --output tsv
    ```

    이 모듈 전체에서 이 연결 문자열이 여러 번 필요하므로 간편하게 사용할 수 있도록 어딘가에 붙여넣어 둘 수 있습니다.

1. Cloud Shell에서 키를 복사합니다. 편집기에서 **privatemessagesender/Program.cs**를 열고 코드의 다음 줄을 찾습니다.

    ```C#
    const string ServiceBusConnectionString = "";
    ```

    연결 문자열을 따옴표 사이에 붙여넣습니다. <kbd>Ctrl+S</kbd>로 파일을 저장합니다.

1. **privatemessagereceiver/Program.cs**에서 이전 단계를 반복하여 동일한 연결 문자열 값을 붙여넣습니다. "..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 파일을 저장합니다.

## <a name="write-code-that-sends-a-message-to-the-queue"></a>큐에 메시지를 보내는 코드 작성

영업 관련 메시지를 보내는 구성 요소를 완성하려면 다음 단계를 수행합니다.

1. 편집기에서 **privatemessagesender/Program.cs**를 엽니다.

1. `SendSalesMessageAsync()` 메서드를 찾습니다.

1. 이 메서드 내에서 다음 코드 줄을 찾습니다.

    ```C#
    // Create a queue client here
    ```

1. 큐 클라이언트를 만들려면 이 코드 줄을 다음 코드로 바꿉니다.

    ```C#
    var queueClient = new QueueClient(ServiceBusConnectionString, QueueName);
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

1. 파일을 저장합니다.

## <a name="send-a-message-to-the-queue"></a>큐에 메시지 보내기

영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.

```bash
dotnet run -p privatemessagesender
```

> [!NOTE]
> 이 연습 중에 앱을 실행하면 `dotnet`에서 처음 실행할 때 원격 원본에서 패키지를 복원하고 앱을 빌드해야 하므로 시작하는 데 시간이 좀 걸릴 수 있습니다.

프로그램을 실행하면 메시지를 보내는 중인지 나타내는 출력 메시지가 표시됩니다. 앱을 실행할 때마다 큐에 메시지가 하나씩 더 추가됩니다.

완료되면 다음 명령을 실행하여 큐에 얼마나 많은 메시지가 있는지 확인합니다.

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

## <a name="write-code-that-receives-a-message-from-the-queue"></a>큐에서 메시지를 받는 코드 작성

1. 편집기에서 **privatemessagereceiver/Program.cs**를 엽니다.

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

1. 파일을 저장합니다.

## <a name="retrieve-a-message-from-the-queue"></a>큐에서 메시지 검색

영업 관련 메시지를 보내는 구성 요소를 실행하려면 Cloud Shell에서 다음 명령을 실행합니다.

```bash
dotnet run -p privatemessagereceiver
```

메시지가 수신되어 콘솔에 표시되었으면 `Enter`를 눌러 앱을 중지합니다. 그런 다음, 전과 동일한 명령을 실행하여 모든 메시지가 큐에서 제거되었는지 확인합니다.

```azurecli
az servicebus queue show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --namespace-name <namespace-name> \
    --name salesmessages \
    --query messageCount
```

모든 메시지가 제거된 경우에는 `0`이 표시됩니다.

Service Bus 큐에 개별 영업 관련 메시지를 보내는 코드를 작성했습니다. 영업용 분산 응용 프로그램에서는 영업 사원이 장치에서 사용하는 모바일 앱에서 이 코드를 작성해야 합니다.

Service Bus 큐에서 메시지를 수신하는 코드도 작성했습니다. 영업용 분산 응용 프로그램에서는 Azure에서 실행되며 받은 메시지를 처리하는 웹 서비스에서 이 코드를 작성해야 합니다.
