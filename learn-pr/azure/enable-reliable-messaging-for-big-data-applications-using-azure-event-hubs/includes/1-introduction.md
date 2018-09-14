빅 데이터 응용 프로그램은 증가한 트랜잭션 볼륨에 맞게 규모를 확장하여 증가한 처리량을 처리하는 기능이 있어야 합니다.

은행의 신용 카드 부서에서 근무한다고 가정합니다. 각 트랜잭션을 승인 또는 거부할지 결정하기 위해 사기 테스트를 담당하는 시스템을 관리하는 팀의 팀원입니다. 시스템은 트랜잭션 스트림을 수신하고 실시간으로 처리해야 합니다.

시스템의 부하는 주말 및 휴일 중에 급증할 수 있습니다. 따라서 증가한 처리량을 효율적으로 정확하게 처리할 수 있어야 합니다. 트랜잭션의 민감한 특성을 고려하면 최소한의 오류도 큰 영향을 줄 수 있습니다.

Azure Event Hubs는 많은 트랜잭션을 수신하고 처리할 수 있습니다. 또한 증가한 처리량을 처리하기 위해 필요할 때 동적으로 크기를 조정하도록 구성할 수도 있습니다.
이 모듈에서는 Event Hubs를 응용 프로그램에 연결하고 대량의 트랜잭션 볼륨을 안정적으로 처리하는 방법을 알아봅니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Azure CLI를 사용하여 이벤트 허브를 만듭니다.
- 이벤트 허브를 통해 메시지를 보내거나 받도록 응용 프로그램을 구성합니다.
- Azure Portal을 사용하여 이벤트 허브 성능을 평가합니다.

## <a name="prerequisites"></a>필수 구성 요소

- Azure Portal을 사용하여 리소스를 만들고 관리한 경험.
- Azure CLI 2.0을 사용하여 Azure에 로그인하고 리소스 만들기
- 스트리밍 및 이벤트 처리와 같은 기본 빅 데이터 개념에 대한 지식.