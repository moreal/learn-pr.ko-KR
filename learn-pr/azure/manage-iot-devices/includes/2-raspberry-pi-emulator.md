Raspberry Pi 보드 테스트 이론 또는 멋진 작업을 수행 하는 이벤트에 대 한 후기 이자를 투입 있어야 합니다. 이 보드에서 비용을 상당히 낮음을 중일 일부 관심 하나에 투자 하기 전에 Raspberry Pi 기능을 테스트 합니다.

Microsoft 온라인 형성한 [Raspberry Pi Azure IoT 시뮬레이터](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true) 사용자가 코드를 통해 에뮬레이트된 하드웨어를 제어 하도록 허용 합니다. 에뮬레이터에는 온도, 습도, 압력 센서 및 함께 연결 될를 통해 회로 허용 하는 실험용 회로판 빨간색 LED에 연결 하는 Raspberry Pi의 그래픽을 나타냅니다. 표시 된 측면 패널을 LED를 제어 하 고 시뮬레이트된 센서에서 더미 데이터를 수집 하는 Node.js JavaScript 코드를 입력할 수 있습니다.

![Raspberry Pi 시뮬레이터](../media-draft/RaspberryPiSimulator.png)

## <a name="raspberry-pi-azure-iot-online-simulator"></a>Raspberry Pi Azure IoT에 대 한 온라인 시뮬레이터

시뮬레이터는 처음 실행할 때 명령줄을 통해 표시 되는 샘플 온도 캡처 프로그램을 작동 합니다. 시뮬레이터는 사람이 실제 장치에 전송 하기 전에 코드를 테스트할 수 있도록 설계 된 대로 동일한 샘플 응용 프로그램 실제 Pi에서 실행할 수도 있습니다.

웹 시뮬레이터에는 세 가지 영역이 있습니다.

1. **어셈블리 영역**합니다. 이 여기서 장치 상태를 볼 수 있습니다. 기본적으로이 Pi를 BME280 센서 및 LED light를 사용 하 여 연결 합니다. 지금은이 구성을 사용자 지정할 수 없습니다.
2. **코딩 영역**합니다. Node.js 사용 하 여 Raspberry Pi에서 앱을 확인 하는 온라인 코드 편집기입니다. 기본 샘플 응용 프로그램 BME280 센서에서 센서 데이터를 수집 하는 데 도움이 및 Azure IoT Hub로 보냅니다.
3. **통합된 콘솔 창**합니다. 이 앱의 출력을 볼 수 있습니다. 콘솔 내에서 세 가지 함수:
    - `run` --샘플 코드를 실행 하는 중 (샘플을 실행할 때 코드는 읽기 전용).
    - `Stop` -실행 되는 샘플 코드를 중지 합니다.
    - `Reset` -코드를 다시 설정합니다.

이제 Raspberry Pi 시뮬레이터 개요 했으므로 살펴보겠습니다 Azure에서 IoT Hub는 시뮬레이터에서 데이터를 캡처하려면 새 리소스가 만들어집니다.

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/en-us/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>
-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->