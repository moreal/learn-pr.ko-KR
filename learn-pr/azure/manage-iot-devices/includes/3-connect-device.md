날씨 데이터의 캡처은 중요 한 태스크 난방, 환기 및 공기 조절 (HVAC) 시스템 소매점에서 작동 하는 방법에 대 한 트래픽 패턴에 이르기까지 날씨 영향입니다. 이 연습에서는 시뮬레이션 된 캡처 날씨 데이터를 Azure IoT Hub를 통해 이전 단위에서 배운 온라인 Raspberry Pi 시뮬레이터를 사용 하 여 조작 됩니다.

이 연습에서는 시뮬레이션 된 환경에서 수행 되는, 하는 동안 응용 프로그램이 시뮬레이션된 된 장치에서 실행 전송할 수 있습니다 실제 장치에 나중에.

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

## <a name="create-an-iot-hub"></a>IoT Hub 만들기
Azure IoT Hub는 장치 및 백 엔드 개발자가 강력한 장치 관리 솔루션을 빌드할 수 있도록 하는 기능 및 확장성 모델을 제공합니다. 장치의 범위는 제한된 센서 및 단일 목적 마이크로컨트롤러에서 다수의 장치에 대한 통신을 라우팅하는 강력한 게이트웨이까지를 포함합니다. 또한 IoT 운영자의 사용 사례 및 요구 사항은 여러 산업에 따라 크게 다릅니다. 이 변형에도 불구하고 IoT Hub 장치 관리는 기능, 패턴 및 코드 라이브러리를 다양한 장치 및 최종 사용자에게 제공합니다.

Raspberry Pi 시뮬레이터에서 데이터를 수집 하려면 IoT hub를 만들려면 먼저 지정 해야 합니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)을 엽니다.
2. Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기**를 선택합니다.
3. 선택 **사물 인터넷**를 선택한 후 **IoT Hub**합니다.

![IoT Hub를 탐색하는 Azure Portal 스크린 샷](../media-draft/fa40d1bc51bc4490f657e3c1a8371b5b.png)

4. **IoT Hub** 창에서 IoT Hub에 다음 정보를 입력합니다.
   
   **구독**:이 예제에 대 한 기본 구독을 사용 합니다.
   **리소스 그룹**: IoT 허브를 포함할 리소스 그룹을 만들거나 기존 리소스 그룹을 사용합니다. 모든 관련 리소스를 *TestResources*와 같은 한 그룹에 함께 배치하여 다 함께 관리할 수 있습니다. 예를 들어 리소스 그룹을 삭제하면 해당 그룹에 들어 있는 모든 리소스가 삭제됩니다.
   **지역**: 가장 가까운 위치를 선택합니다.
   **이름**: IoT 허브에 대한 고유한 이름을 만듭니다. 입력한 이름을 사용할 수 있으면 녹색 확인 표시가 나타납니다.

> [!IMPORTANT]
> IoT Hub가 DNS 엔드포인트로 공개적으로 검색할 수 있게 되므로 이름을 지정하는 동안 중요한 정보를 피해야 합니다.

   ![IoT Hub 기본 사항 창](./../media-draft/dbb7319388673b8ee0e0b407536156c0.png)

5. **다음: 크기 및 규모**를 선택하여 IoT Hub를 계속 만듭니다.
6. **가격 책정 및 규모 계층**을 선택합니다. 예를 들어 다음을 선택 합니다 **F1-체험** 계층입니다.

   ![IoT Hub 크기 및 규모 창](../media-draft/b506eb3293fa4aa9d4785ad498fc476c.png)

7. **검토 + 만들기**를 선택합니다.

8. IoT Hub 정보를 검토한 다음, **만들기**를 클릭합니다. IoT Hub를 만드는 데 몇 분 정도 걸릴 수 있습니다. **알림** 창에서 진행 상황을 모니터링할 수 있습니다.

<!--STOPPED HERE-->
<!--
Now that you have created an IoT hub, it's time to locate the important information that you use to connect devices and applications to your IoT hub. In your IoT hub navigation menu, open **Shared access policies**. Select the **iothubowner** policy, and then copy the **Connection string---primary key** of your IoT hub. For more information, see [Control access to IoT Hub](https://docs.microsoft.com/azure/iot-hub/iot-hub-devguide-security).

> [!NOTE]
> You do not need this iothubowner connection string for this set-up tutorial. However, you may need it for some of the tutorials or different IoT scenarios after you complete this set-up.

![Get your IoT hub connection string](../media-draft/a4b41e6ea46ccbef653c411a9829610c.png)
-->

## <a name="register-a-device"></a>장치 등록
연결을 위해 장치를 IoT Hub에 등록해야 합니다.

1. IoT Hub 탐색 메뉴에서 **IoT 장치**를 열고 **추가**를 클릭하여 IoT Hub에 장치를 등록합니다.

   ![IoT 허브의 IoT 장치에 장치 추가](../media-draft/ee5f177abcf06b86dd007fce3b8448ad.png)

2. 새 장치의 **장치 ID**를 입력합니다. 장치 ID는 대/소문자를 구분합니다.

> [!IMPORTANT]
> 고객 지원 및 문제 해결을 위해 수집한 로그에 장치 ID를 표시할 수 있으므로 이름을 지정하는 동안 중요한 정보를 피해야 합니다.

3. **저장**을 클릭합니다.
4. 장치가 만들어진 후 **IoT 장치** 창의 목록에서 장치를 엽니다.
5. 나중에 사용하기 위해 **연결 문자열---기본 키**를 복사합니다.

   ![장치 연결 문자열 가져오기](../media-draft/fba4413dcb652be92a6ab0f6bb638561.png)

## <a name="send-simulated-telemetry"></a>시뮬레이션된 원격 분석 전송

1. 엽니다는 [Azure IoT Raspberry Pi 시뮬레이터](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true)합니다.
2. 방금 복사한 Azure IoT hub 장치 연결 문자열을 사용 하 여 줄 15에서 자리 표시자를 대체 합니다.
3. 클릭 합니다 `Run` 단추나 형식 `npm start` 응용 프로그램을 실행 하려면 콘솔 창에 있습니다.
   
   ![장치 연결 문자열로 대체 합니다.](../media-draft/Line15.png)

센서 데이터와 IoT hub로 전송 되는 메시지를 보여 주는 다음 출력이 표시 됩니다.

![출력 - Raspberry Pi에서 IoT Hub로 전송된 센서 데이터](../media-draft/96b28d30e317b04347abb0d613738117.png)

## <a name="read-the-telemetry-from-your-hub"></a>허브에서 원격 분석 읽기
 따라서 이유가 무엇입니까? IoT hub에 시뮬레이션된 된 장치에서 보낸 장치-클라우드 메시지를 받고 있습니다. 보겠습니다 살펴보겠습니다 빠른 Azure IoT Hub 처리 하는 들어오는 데이터를 보려면. IoT Hub에서 아래의 **모니터링**를 선택 **메트릭**합니다. 그림 되는 데이터에 대 한 대기 하는 대로 잠시 지정 합니다.
   
   ![IoT Hub 메트릭](../media-draft/HubMetrics.png)


<!--Reference links
https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started-->
