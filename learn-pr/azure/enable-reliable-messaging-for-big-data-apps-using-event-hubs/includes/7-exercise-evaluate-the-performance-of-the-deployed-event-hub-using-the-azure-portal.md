이 단원에서는 Azure Portal을 사용하여 이벤트 허브가 예상대로 작동하는지 확인합니다. 또한 일시적으로 사용할 수 없을 때 이벤트 허브 메시징이 어떻게 작동하는지 테스트하고 Event Hubs 메트릭을 사용하여 이벤트 허브의 성능을 확인합니다.

## <a name="view-event-hub-activity"></a>이벤트 허브 활동 보기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. 검색 창을 사용하여 이벤트 허브를 찾아 엽니다.

1. 개요 페이지에서 메시지 개수를 확인합니다.

    ![이벤트 허브 메시지 보기](../media-draft/6-view-messages.png)

1. SimpleSend 및 EventProcessorSample 응용 프로그램은 100개의 메시지를 보내거나 받도록 구성됩니다. 이벤트 허브가 SimpleSend 응용 프로그램에서 100개의 메시지를 처리했고 100개의 메시지를 EventProcessorSample 응용 프로그램으로 전송했음을 알 수 있습니다.

## <a name="test-event-hub-resilience"></a>이벤트 허브 복원력 테스트

다음 단계를 사용하여 일시적으로 사용할 수 없는 동안 응용 프로그램이 이벤트 허브에 메시지를 보내면 어떻게 되는지 확인합니다.

1. SimpleSend 응용 프로그램을 사용하여 이벤트 허브로 메시지를 다시 보냅니다. 다음 명령을 사용합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. **보내기 완료...** 가 표시되면 Enter 키를 누릅니다.

1. Azure Portal에서 **Event Hubs 인스턴스** > **설정** > **속성**을 클릭합니다.

1. 이벤트 허브 상태에서 **사용 안 함**을 클릭합니다.

    ![이벤트 허브 사용 안 함](../media-draft/7-disable-event-hub.png)

5분 이상 기다립니다.

1. 이벤트 허브 상태에서 **활성**을 클릭하여 이벤트 허브를 다시 사용하고 변경 내용을 저장합니다.

1. EventProcessorSample 응용 프로그램을 다시 실행하여 메시지를 수신합니다. 다음 명령을 사용합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. 메시지가 콘솔에 표시되는 작업이 중지하면 Enter 키를 누릅니다.

1. Azure Portal에서 이벤트 허브 **‘네임스페이스’** 를 찾아 엽니다. 

1. **Event Hubs 네임스페이스** > **모니터링** > **메트릭(미리 보기)** 을 클릭합니다.

    ![이벤트 허브 메트릭 사용](../media-draft/7-event-hub-metrics.png)

1. **메트릭** 목록에서 **들어오는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.

1. **메트릭** 목록에서 **보내는 메시지**를 선택하고 **메트릭 추가**를 클릭합니다.

1. 차트의 맨 위에서 **최근 24시간(자동)** 을 클릭하여 기간을 **지난 30분**으로 변경합니다.

1. **적용**을 클릭합니다.

일정 기간에 이벤트 허브를 오프라인으로 전환하기 전에 메시지가 전송되었지만 100개의 모든 메시지가 성공적으로 전송되었음을 확인할 수 있습니다.

## <a name="summary"></a>요약

이 단원에서는 Event Hubs 메트릭을 사용하여 이벤트 허브가 보내고 받는 메시지를 성공적으로 처리하고 있는지 테스트했습니다.
