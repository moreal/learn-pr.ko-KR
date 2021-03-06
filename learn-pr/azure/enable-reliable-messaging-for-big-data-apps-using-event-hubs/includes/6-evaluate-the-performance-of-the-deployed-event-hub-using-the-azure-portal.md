Event Hubs를 사용할 경우 허브를 모니터링하여 예상대로 작동하는지 확인해야 합니다.

계속해서 은행 예제에서, Azure Event Hubs를 배포하고 발신자 및 수신자 응용 프로그램을 구성했다고 가정합니다. 응용 프로그램이 결제 처리 솔루션을 테스트할 준비가 되었습니다. 발신자 응용 프로그램은 고객의 신용 카드 데이터를 수집하고, 수신자 응용 프로그램은 신용 카드가 유효한지 확인합니다. 회사 비즈니스의 민감한 특성으로 인해 결제 처리는 일시적으로 사용할 수 없는 경우에도 강력하고 안정적이어야 합니다.

Event Hub가 예상대로 데이터를 처리하고 있는지 테스트하여 Event Hub를 평가해야 합니다. Event Hubs에서 사용 가능한 메트릭을 사용하면 제대로 작동하는지 확인할 수 있습니다.

## <a name="how-do-you-use-the-azure-portal-to-view-your-event-hub-activity"></a>Azure Portal을 사용하여 Event Hub 작업을 보려면 어떻게 해야 하나요?

Azure Portal > Event Hub 개요 페이지에 메시지 개수가 표시됩니다. 이러한 메시지 개수는 Event Hub가 수신 및 전송한 데이터(이벤트)를 나타냅니다. 이러한 이벤트를 보기 위한 시간 간격을 선택할 수 있습니다.

![메시지 개수가 포함된 Event Hub 네임스페이스를 표시하는 Azure Portal의 스크린샷.](../media/6-view-messages.png)

## <a name="how-can-you-test-event-hub-resilience"></a>Event Hub 복원력을 테스트하려면 어떻게 해야 하나요?

Azure Event Hubs는 사용할 수 없는 경우에도 발신자 응용 프로그램에서 메시지를 계속 수신합니다. 이 기간에 받은 메시지는 허브를 사용할 수 있게 되는 즉시 성공적으로 전송됩니다.

이 기능을 테스트하려면 Azure Portal을 사용하여 Event Hub를 사용하지 않도록 설정하면 됩니다.

Event Hub를 다시 사용하도록 설정하면 수신자 응용 프로그램을 다시 실행하고 네임스페이스에 대한 Event Hubs 메트릭을 사용하여 모든 발신자 메시지가 성공적으로 전송되고 수신되었는지 확인할 수 있습니다.

Event Hubs에서 사용 가능한 기타 유용한 메트릭은 다음과 같습니다.

- 제한된 요청: 처리량 단위 사용량이 초과되었기 때문에 제한된 요청 수입니다.
- ActiveConnections: 네임스페이스 또는 Event Hub의 활성 연결 수입니다.
- 들어오는/나가는 바이트: 지정된 기간에 Event Hubs 서비스에서 보내거나 받은 바이트 수입니다.

## <a name="summary"></a>요약

Azure Portal은 Event Hubs에 대한 상태 검사로 사용할 수 있는 메시지 개수와 기타 메트릭을 제공합니다.
