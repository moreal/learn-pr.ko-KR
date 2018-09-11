팀에서는 Azure Event Hubs 기능을 활용하여 시스템을 통해 들어오는 증가하는 트랜잭션 볼륨을 관리하고 처리하기로 했습니다.

이벤트 허브는 Azure 리소스이므로 첫 번째 단계는 Azure에서 새 허브를 만들고 응용 프로그램의 특정 요구 사항을 충족하도록 구성하는 것입니다.

## <a name="what-is-an-azure-event-hub"></a>Azure 이벤트 허브란?

Azure Event Hubs는 초당 수백만 개의 이벤트를 수신하고 처리할 수 있는 클라우드 기반 이벤트 처리 서비스입니다. Event Hubs는 들어오는 데이터를 수신하고 처리 리소스를 사용할 수 있을 때까지 데이터를 저장하는 이벤트 파이프라인의 프런트 도어로 사용됩니다.

Event Hubs로 데이터를 보내는 엔터티를 *게시자*라고 하고 Event Hubs에서 데이터를 읽는 엔터티를 *소비자* 또는 *구독자*라고 합니다. Azure Event Hubs는 이러한 두 엔터티 간에 이벤트 스트림의 프로덕션(게시자의) 및 소비(구독자에 대한)를 나누는 데 사용됩니다. 이 분리는 이벤트 프로덕션의 비율이 소비보다 훨씬 높은 시나리오를 관리하는 데 도움이 됩니다.

![게시자는 하나의 이벤트 허브에 여러 이벤트를 보내고 구독자가 데이터를 사용할 수 있도록 설정](../media-draft/2-event-hub-overview.png "이벤트 허브 개요")

### <a name="events"></a>이벤트

**이벤트**는 변경된 알림을 포함하지만 정확히 변경된 세부 정보를 포함하지 않는 작은 패킷입니다. 일부 형식의 쿼리를 시작하여 세부 정보를 찾도록 소비자 응용 프로그램을 구성할 수 있지만, 이것은 요구 사항이 아니고 Event Hubs는 이를 처리하지 않습니다. 이벤트는 개별 또는 일괄로 게시할 수 있지만, 하나의 게시(개별 또는 일괄)는 256KB를 초과할 수 없습니다.

이와 달리 Azure Service Bus의 메시지 큐에서 **메시지**에는 데이터 및 이벤트가 포함되고, 메시지 게시자는 소비자가 특정 방식으로 메시지를 처리할 것으로 예상합니다.

### <a name="publishers-and-subscribers"></a>게시자 및 구독자

이벤트 게시자는 HTTPS 또는 AQMP(고급 메시지 큐 프로토콜) 1.0을 사용하여 이벤트 데이터를 전송할 수 있는 응용 프로그램 또는 장치입니다. 

데이터를 자주 보내는 게시자의 경우 AMQP 성능이 향상됩니다. 그러나 지속적 양방향 소켓과 TLS(전송 수준 보안) 또는 SSL/TLS가 먼저 설정되어야 하므로 초기 세션 오버헤드가 더 높습니다. 

더 간헐적으로 게시하는 경우 HTTPS가 더 나은 옵션입니다. HTTPS에는 모든 요청에 대한 추가 SSL 오버헤드가 필요하지만 세션 초기화 오버헤드가 발생하지 않습니다.

> [!NOTE] 
> Apache Kafka 1.0 이상 클라이언트 버전을 사용하는 기존 Kafka 기반 응용 프로그램은 Event Hubs 게시자 역할을 할 수도 있습니다.

이벤트 구독자는 두 개의 지원되는 프로그래밍 방식 메서드 중 하나를 사용하여 이벤트 허브에서 이벤트를 수신하고 처리하는 응용 프로그램입니다.

- **EventHubReceiver** - 제한된 관리 옵션을 제공하는 단순 메서드입니다.
- **EventProcessorHost** - 이 모듈에서 나중에 사용할 효율적인 메서드입니다.

### <a name="consumer-groups"></a>소비자 그룹

이벤트 허브 **소비자 그룹**은 이벤트 허브 데이터 스트림의 특정 보기를 나타냅니다. 개별 소비자 그룹을 사용하면 여러 구독자 응용 프로그램이 이벤트 스트림을 개별적으로, 다른 응용 프로그램에 영향을 주지 않고 이벤트 스트림을 처리할 수 있습니다. 그러나 여러 소비자 그룹을 사용하는 것은 요구 사항이 아니며 대부분 응용 프로그램의 경우 단일 기본 소비자 그룹이 충분합니다.

### <a name="pricing"></a>가격

Azure Event Hubs에는 세 가지 가격 책정 계층(Basic, Standard 및 Dedicated)이 있습니다. 계층은 지원되는 연결, 사용 가능한 소비자 그룹 수 및 처리량에 따라 다릅니다. Azure CLI를 사용하여 Event Hubs 네임스페이스를 만들 때 가격 책정 계층을 지정하지 않으면 **Standard**(소비자 그룹 20개, 조정된 연결 1000개)의 기본값이 할당됩니다.

## <a name="creating-and-configuring-a-new-azure-event-hubs"></a>새 Azure Event Hubs 만들기 및 구성

새 Azure Event Hubs를 만들고 구성할 때는 두 가지 기본 단계가 있습니다. 첫 번째 단계는 Event Hubs **네임스페이스**를 정의하는 것입니다. 두 번째 단계는 해당 네임스페이스에 이벤트 허브를 만드는 것입니다.

### <a name="defining-an-event-hubs-namespace"></a>Event Hubs 네임스페이스 정의

Event Hubs 네임스페이스는 하나 이상의 Event Hubs를 관리하기 위한 포함 엔터티입니다. 

일반적으로 Event Hubs 네임스페이스 만들기에는 다음이 포함됩니다.

1. 네임스페이스 수준 설정 정의. 네임스페이스 용량(**처리량 단위**를 사용하여 구성됨), 가격 책정 계층 및 성능 메트릭과 같은 특정 설정은 네임스페이스 수준에서 정의됩니다. 이는 해당 네임스페이스 내의 모든 이벤트 허브에 적용 가능합니다. 이러한 설정을 정의하지 않으면 기본값인 *1*(용량) 및 *Standard*(가격 책정 계층)가 사용됩니다.

    처리량 단위를 설정한 후에는 변경할 수 없습니다. 예상 Azure 예산을 기준으로 구성을 조정해야 합니다. 처리량 요구 사항에 따라 서로 다른 이벤트 허브를 구성하는 것이 좋습니다. 예를 들어 판매 데이터 응용 프로그램이 있고 두 개의 Event Hubs를 계획하는 경우 실시간 판매 데이터 원격 분석의 높은 처리량 컬렉션 및 자주 사용하지 않는 이벤트 로그 컬렉션에 하나씩 각 허브에 별도의 네임스페이스를 사용하는 것이 좋습니다. 이 방법은 원격 분석 허브에서 높은 처리량 용량을 구성(및 요금 지급)하는 데만 필요합니다.

1. 네임스페이스의 고유 이름 선택 네임스페이스는 이 URL을 통해 액세스할 수 있습니다. *_namespace_.servicebus.windows.net*

1. 다음 선택적 속성 정의:

    - Kafka 사용. 이 옵션을 사용하면 Kafka 응용 프로그램이 이벤트 허브에 이벤트를 게시할 수 있습니다.
    - 이 네임스페이스를 중복으로 설정. 영역 중복 기능은 자체의 독립적인 전력, 네트워킹, 냉각 인프라를 사용하여 개별 데이터 센터에서 데이터를 복제합니다.
    - 자동 확장 및 자동 확장 최대 처리량 단위 사용. 자동 확장은 처리량 단위 수를 늘려 최댓값까지 늘려 자동 강화 옵션을 제공합니다. 이는 들어오거나 나가는 데이터 속도가 현재 설정된 처리량 단위 수를 초과하는 상황에서 제한을 방지하는 데 유용합니다.

### <a name="azure-cli-commands-for-creating-an-event-hubs-namespace"></a>Event Hubs 네임스페이스를 만들기 위한 Azure CLI 명령

새 Event Hubs 네임스페이스를 만들려면 다음 명령을 사용합니다.

1. 용이한 관리를 위해 Azure에서 리소스 그룹은 관련 Azure 솔루션을 보유하는 컨테이너입니다. 필요한 경우 이벤트 허브에 대한 새 리소스 그룹을 만듭니다.

    ```azurecli
    az group create --name <resource group name> --location <location>
    ```

1. 이전 단계에서와 동일한 리소스 그룹 및 위치를 사용하여 Event Hubs 네임스페이스를 만듭니다.

    ```azurecli
    az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <resource group name> -l <location>
    ```

1. 동일한 Event Hubs 네임스페이스 내의 모든 Event Hubs는 공통 연결 자격 증명을 공유합니다. 이벤트 허브를 사용하여 메시지를 보내고 받도록 응용 프로그램을 구성할 때 이러한 자격 증명이 필요합니다. 이전과 동일한 리소스 그룹 및 Event Hubs 네임스페이스 이름을 사용하여 Event Hubs 네임스페이스에 대한 연결 문자열을 반환하려면 다음 명령을 사용합니다.

    ```azurecli
    az eventhubs namespace authorization-rule keys list --resource-group <resource group name> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

### <a name="configuring-a-new-event-hub"></a>새 이벤트 허브 구성

Event Hubs 네임스페이스를 만든 후 이벤트 허브를 만들 수 있습니다. 새 이벤트 허브를 만들 경우 몇 가지 필수 매개 변수가 있습니다.

이벤트 허브를 만들려면 다음 매개 변수가 필요합니다.

- **이벤트 허브 이름** - 구독 내에서 고유하고 다음에 해당하는 이벤트 허브 이름입니다.
  - 1-50자 사이의 길이
  - 문자, 숫자, 마침표, 하이픈 및 밑줄만 포함
  - 문자 또는 숫자로 시작하고 끝남
- **파티션 수** - 이벤트 허브에 필요한 파티션 수입니다(2-32 사이). 이는 예상되는 동시 소비자 수와 직접적으로 관련되어야 합니다. 허브가 작성된 후에는 이를 변경할 수 없습니다. 파티션은 메시지 스트림을 분리하므로 해당 소비자 또는 수신자 응용 프로그램이 데이터 스트림의 특정 하위 집합만 읽어야 합니다. 정의되지 않은 경우 기본값 *4*가 사용됩니다.
- **메시지 보존** - 어떤 이유로 데이터 스트림을 재생해야 하는 경우 메시지를 계속 사용할 수 있는 기간(일)(1-7 사이)입니다. 정의되지 않은 경우 기본값 *7*이 사용됩니다.

필요한 경우 Azure Blob Storage 또는 Azure Data Lake Store 계정에 데이터를 스트리밍하도록 이벤트 허브를 구성할 수도 있습니다.

### <a name="azure-cli-commands-for-creating-an-event-hub"></a>이벤트 허브를 만들기 위한 Azure CLI 명령

새 이벤트 허브를 만들려면 다음 명령을 사용합니다.

1. 네임스페이스를 만들 때 사용한 것과 동일한 리소스 그룹 및 위치를 사용하여 이벤트 허브를 만듭니다.

    ```azurecli
    az eventhubs eventhub create --name <event hub name> --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name>
    ```

1. 이전과 동일한 리소스 그룹과 이벤트 허브 이름 및 네임스페이스 이름을 사용하여 네임스페이스에서 이벤트 허브의 세부 정보를 확인합니다.

    ```azurecli
    az eventhubs eventhub show --resource-group <Resource Group name> --namespace-name <Event Hubs namespace name> --name <event hub name>

## Summary

To deploy Azure Event Hubs, you must configure an Event Hubs namespace and then configure the event hub itself. In the next section, you will go through the detailed configuration steps to create a new namespace and event hub.