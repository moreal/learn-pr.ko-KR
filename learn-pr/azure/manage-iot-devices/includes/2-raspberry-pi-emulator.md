Raspberry Pi 보드는 최근에 이론 테스트용으로 또는 멋진 작업을 수행하는 용도로 관심을 끌고 있습니다. 이 보드의 비용은 상당히 저렴하지만, 구매 전에 Raspberry Pi 기능을 테스트하고 싶은 분들도 있을 것입니다.

Microsoft는 사용자가 코드를 통해 에뮬레이트된 하드웨어를 제어할 수 있는 온라인 [Raspberry Pi Azure IoT 시뮬레이터](https://azure-samples.github.io/raspberry-pi-web-simulator?azure-portal=true)를 개발했습니다. 에뮬레이터는 회로를 서로 유선으로 연결할 수 있는 실험용 회로판을 통해 온도, 습도, 압력 센서와 연결된 Raspberry Pi의 그래픽과 빨간색 LED를 표시합니다. 표시된 측면 패널을 통해 사용자는 LED를 제어하고 시뮬레이트된 센서에서 더미 데이터를 수집하는 Node.js JavaScript 코드를 입력할 수 있습니다.

![Raspberry Pi 시뮬레이터](../media/RaspberryPiSimulator.png)

## <a name="raspberry-pi-azure-iot-online-simulator"></a>Raspberry Pi Azure IoT 온라인 시뮬레이터

시뮬레이터를 처음으로 실행하면 시뮬레이터는 명령줄을 통해 표시되는 온도 캡처 프로그램 샘플이 작동합니다. 시뮬레이터는 사람이 코드를 테스트한 후 실제 장치에 전송할 수 있도록 설계되었기 때문에 동일한 샘플 응용 프로그램을 실제 Pi에서 실행할 수도 있습니다.

웹 시뮬레이터에는 세 가지 영역이 있습니다.

1. **어셈블리 영역**. 여기서 장치 상태를 볼 수 있습니다. 기본적으로 이것은 BME280 센서 및 LED 조명을 연결하는 Pi입니다. 이 구성은 현재 사용자 지정할 수 없습니다.
2. **코딩 영역**. Node.js로 Raspberry Pi에서 앱을 만들 수 있는 온라인 코드 편집기입니다. 기본 샘플 응용 프로그램을 사용하여 BME280 센서에서 센서 데이터를 손쉽게 수집한 후 Azure IoT Hub로 보낼 수 있습니다.
3. **통합된 콘솔 창**. 여기서 앱의 출력을 볼 수 있습니다. 콘솔 내에는 세 가지 함수가 있습니다.
    - `run` - 샘플 코드를 실행합니다(샘플을 실행 중에는 코드가 읽기 전용임).
    - `Stop` - 샘플 코드 실행을 중지합니다.
    - `Reset` - 코드를 다시 설정합니다.

Raspberry Pi 시뮬레이터에 대한 개요를 살펴보았으면 Azure의 IoT Hub를 살펴보겠습니다. 여기서는 시뮬레이터의 데이터를 캡처할 새 리소스를 생성하겠습니다.

<!-- Reference links 
-   Online Raspberry Pi Emulator:
    <https://docs.microsoft.com/azure/iot-hub/iot-hub-raspberry-pi-web-simulator-get-started>
-   <https://azure-samples.github.io/raspberry-pi-web-simulator/#GetStarted>-->