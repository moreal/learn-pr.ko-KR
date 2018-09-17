분산 응용 프로그램에서는 받는 사람 구성 요소 하나로 보내야 하는 메시지도 있고, 여러 대상으로 보내야 하는 메시지도 있습니다.

사용자가 피자 주문을 취소하는 경우 발생하는 상황을 살펴보겠습니다. 이 상황은 초기 주문을 할 때와는 약간 다릅니다. 초기 주문의 경우 주문을 다른 단계(예: 해당 지역 상점에서 피자를 준비 및 요리하는 단계)로 보내기 전에 주문에서 결제 처리가 완료될 때까지 기다려야 합니다. 그러나 취소 작업의 경우에는 상점 *및* 결제 처리 업체에 동시에 알림을 보내야 합니다. 이 방식을 사용하는 경우 식자재 또는 배달 차량 운전자의 시간 낭비 가능성을 최소화할 수 있습니다.

여러 구성 요소가 같은 메시지를 받을 수 있도록 하기 위해 Azure Service Bus 항목을 사용할 것입니다.

## <a name="how-code-that-uses-topics-differs-from-queues"></a>항목을 사용하는 코드와 큐의 차이점

항목으로 보내는 모든 메시지가 모든 구독 구성 요소에 배달되도록 하려는 경우에 항목을 사용합니다. 항목을 사용하는 코드를 작성하는 것은 큐를 대체하는 방법입니다. 이 경우에도 같은 **Microsoft.Azure.ServiceBus** NuGet 패키지를 사용하고, 연결 문자열을 구성하고, 비동기 프로그래밍 패턴을 사용합니다.

그러나 `QueueClient` 클래스 대신 `TopicClient` 클래스를 사용하여 메시지를 보내며 `SubscriptionClient` 클래스를 사용하여 메시지를 받습니다.

## <a name="setting-filters-on-subscriptions"></a>구독에 대해 필터 설정

항목으로 전송되는 메시지가 배달되는 구독을 제어하려는 경우 항목의 각 구독에 대해 필터를 적용할 수 있습니다. 예를 들어, 피자 응용 프로그램의 경우 상점에서는 UWP(Universal Windows Platform) 응용 프로그램을 실행합니다. 각 매장은 “OrderCancellation” 항목을 구독하되 고유한 StoreID를 필터로 사용할 수 있습니다. 이 경우 멀리 떨어져 있는 매장 위치로 불필요한 메시지가 전송되지 않으므로 인터넷 대역폭도 절약됩니다. 단, 결제 처리 구성 요소는 모든 취소 메시지를 구독합니다.

필터는 다음의 세 가지 유형 중 하나일 수 있습니다.

- **부울 필터.** `TrueFilter`를 사용하면 항목으로 보내는 모든 메시지가 현재 구독으로 배달됩니다. `FalseFilter`는 현재 구독에 배달된 메시지가 없음을 확인합니다. (이로 인해 구독이 효과적으로 차단되거나 해제됩니다.)
- **SQL 필터.** SQL 필터는 SQL 쿼리의 `WHERE` 절과 같은 구문을 사용하여 조건을 지정합니다. 이 구독을 기준으로 평가했을 때 `True`를 반환하는 메시지만 구독자에게 배달됩니다.
- **상관관계 필터.** 상관관계 필터는 각 메시지 속성과의 일치 여부를 비교하는 조건 집합을 포함합니다. 필터의 속성과 메시지의 속성 값이 같으면 두 속성은 일치하는 것으로 간주됩니다.

StoreId 필터의 경우 SQL 필터를 사용할 수 *있습니다*. 이러한 필터는 가장 유연하지만 계산 비용이 가장 많이 들고 Service Bus 처리 속도가 느려질 수 있습니다. 그러므로 여기서는 상관관계 필터를 대신 선택합니다. 

## <a name="topicclient-example"></a>TopicClient 예제

모든 전송 또는 수신 구성 요소에서 Service Bus 항목을 호출하는 코드 파일에 다음의 `using` 문을 추가해야 합니다.

```C#
using System.Threading;
using System.Threading.Tasks;
using Microsoft.Azure.ServiceBus;
```

메시지를 보내려면 먼저 새 `TopicClient` 개체를 만들어 연결 문자열과 항목 이름을 전달합니다.

```C#
topicClient = new TopicClient(TextAppConnectionString, "GroupMessageTopic");
```

`TopicClient.SendAsync()` 메서드를 호출하고 메시지를 전달하면 항목에 메시지를 보낼 수 있습니다. 큐와 마찬가지로 메시지는 UTF-8 인코딩 문자열 형식이어야 합니다.

```C#
string message = "Cancel! I can't believe you use canned mushrooms!";
var encodedMessage = new Message(Encoding.UTF8.GetBytes(message));
await topicClient.SendAsync(encodedMessage);
```

메시지를 받으려면 `TopicClient` 개체가 아닌 `SubscriptionClient` 개체를 만들어 연결 문자열, 항목의 이름 **및** 구독 이름을 전달해야 합니다.

```C#
subscriptionClient = new SubscriptionClient(ServiceBusConnectionString, "GroupMessageTopic", "NorthAmerica");
```

그런 다음 메시지 처리기를 등록합니다. 메시지 처리기는 검색된 메시지를 처리하는 코드의 비동기 메서드입니다.

```C#
subscriptionClient.RegisterMessageHandler(MessageHandler, messageHandlerOptions);
```

메시지 처리기 내에서 `SubscriptionClient.CompleteAsync()` 메서드를 호출하여 큐에서 메시지를 제거합니다.

```C#
await subscriptionClient.CompleteAsync(message.SystemProperties.LockToken);
```