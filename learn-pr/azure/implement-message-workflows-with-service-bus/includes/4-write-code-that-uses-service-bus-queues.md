분산 응용 프로그램은 대상 구성 요소로 전송 대기 중인 메시지를 임시로 저장하는 위치로 Service Bus 큐 등의 큐를 사용합니다. 큐를 통해 메시지를 보내고 받으려면 원본 및 대상 구성 요소에서 코드를 작성해야 합니다.

Contoso Slices 응용 프로그램의 예를 고려해 보겠습니다. 고객이 웹 사이트 또는 모바일 앱을 통해 주문을 합니다. 웹 사이트 및 모바일 앱은 고객 장치에서 실행되므로 한 번에 들어올 수 있는 주문 수에는 실제로 제한이 없습니다. 모바일 앱과 웹 사이트에서 큐에 주문을 보관하도록 하면 백 엔드 구성 요소(웹앱)가 해당 큐에서 적절한 속도로 주문을 처리하도록 할 수 있습니다.

실제로 Contoso Slices 응용 프로그램은 몇 단계를 통해 새 주문을 처리합니다. 하지만 모든 주문을 처리하려면 먼저 결제가 승인되어야 하므로, 여기서는 큐를 사용하겠습니다. 수신 구성 요소에서는 먼저 결제를 처리합니다.

Contoso는 모바일 앱과 웹 사이트에서 메시지를 큐에 추가하는 코드를 작성해야 합니다. 메시지를 큐에서 선택하는 코드를 백 엔드 웹앱에서 작성합니다.

여기서는 해당 코드를 작성하는 방법을 배웁니다.

## <a name="the-microsoftazureservicebus-nuget-package"></a>Microsoft.Azure.ServiceBus NuGet 패키지

Service Bus를 통해 메시지를 보내고 받는 코드를 쉽게 작성할 수 있도록 Microsoft에서는 .NET 클래스 라이브러리를 제공합니다. 이 라이브러리는 모든 .NET Framework 언어에서 Service Bus 큐, 항목 또는 릴레이와 상호 작용하는 데 사용할 수 있습니다. **Microsoft.Azure.ServiceBus** NuGet 패키지를 추가하여 응용 프로그램에 이 라이브러리를 포함할 수 있습니다.

큐의 경우 이 라이브러리에서 가장 중요한 클래스는 `QueueClient` 클래스입니다. 먼저 전송 구성 요소와 수신 구성 요소 둘 다에서 이 클래스를 인스턴스화해야 합니다.

## <a name="connection-strings-and-keys"></a>연결 문자열 및 키

Service Bus 네임스페이스에서 큐에 연결하려면 원본 구성 요소와 대상 구성 요소 둘 다에 두 가지 정보가 필요합니다.

- Service Bus 네임스페이스 위치(**엔드포인트**라고도 함). 이 위치는 **servicebus.windows.net** 도메인 내에서 정규화된 도메인 이름으로 지정됩니다. 예를 들면 **pizzaService.servicebus.windows.net**과 같습니다.
- 액세스 키. Service Bus는 액세스 키를 요구하는 방식으로 큐/항목/릴레이 액세스를 제한합니다.

이 두 정보는 모두 연결 문자열 형식으로 `QueueClient` 개체에 제공됩니다. 네임스페이스에 대한 올바른 연결 문자열은 Azure Portal에서 가져올 수 있습니다.

## <a name="calling-methods-asynchronously"></a>비동기식 메서드 호출

Azure의 큐는 전송 및 수신 구성 요소에서 매우 멀리 떨어져 있을 수도 있습니다. 그리고 실제 위치가 가깝더라도 연결 속도가 느리고 대역폭 경합이 발생하는 경우에는 구성 요소가 큐에 대해 메서드를 호출하는 과정이 지연될 수 있습니다. 이러한 이유로 인해 Service Bus 클라이언트 라이브러리는 큐와 상호 작용할 수 있도록 `async` 메서드를 제공합니다. 여기서는 호출이 완료되기를 기다리는 동안 스레드가 차단되지 않도록 이러한 메서드를 사용할 것입니다.

예를 들어 큐에 메시지를 보낼 때는 `await` 키워드가 포함된 `QueueClient.SendAsync()` 메서드를 사용합니다.

## <a name="write-code-that-sends-to-queues"></a>큐로 정보를 보내는 코드 작성 

모든 전송 또는 수신 구성 요소에서 Service Bus 큐를 호출하는 코드 파일에 다음의 `using` 문을 추가해야 합니다.

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

그런 다음, 새 `QueueClient` 개체를 만들어 연결 문자열과 큐 이름을 전달합니다.

```C#
queueClient = new QueueClient(TextAppConnectionString, "PrivateMessageQueue");
```

`QueueClient.SendAsync()` 메서드를 호출하고 UTF-8 인코딩 문자열 형식으로 메시지를 전달하여 큐에 메시지를 보낼 수 있습니다.

```C#
string message = "Sure would like a large pepperoni!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await queueClient.SendAsync(encodedMessage);
```

## <a name="receive-messages-from-queue"></a>큐에서 메시지 받기

메시지를 받으려면 먼저 메시지 처리기(큐에 사용 가능한 메시지가 있을 때 호출되는 코드의 메서드)를 등록해야 합니다.

```C#
queueClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

처리 작업을 수행합니다. 그런 다음, 메시지 처리기 내에서 `QueueClient.CompleteAsync()` 메서드를 호출하여 큐에서 메시지를 제거합니다.

```C#
await queueClient.CompleteAsync(message.SystemProperties.LockToken);
```
    