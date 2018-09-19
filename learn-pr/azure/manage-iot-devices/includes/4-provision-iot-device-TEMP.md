Azure IoT Hub가 Raspberry Pi 같은 IoT 장치에서 데이터를 수집하는 원리를 알아보았으니, 이제 데이터를 보낼 수 있도록 다른 IoT 장치를 프로비전하는 방법으로 넘어가셔도 좋습니다. 소형 프로젝트(장치 1-5대)의 IoT 장치 설정은 1:1로 수행해도 됩니다. 대규모 배포 시 보다 효율적인 프로비전 방법이 필요합니다.

Azure IoT Hub Device Provisioning Service는 고객이 Azure IoT Hub에 무인 장치 프로비전을 구성할 수 있게 해주고, 매우 길고 지루한 순차적 프로세스 대신 클라우드의 확장성을 제공합니다. 프로세스는 공급망이라는 과제를 염두에 두고 설계되었으며, 안전하고 확장 가능한 방식으로 수백만 대의 장치를 프로비전하는 데 필요한 인프라를 제공합니다.

이제 Device Provisioning Service를 사용하는 자동 장치 프로비저닝은 websocket을 통한 HTTP, AMQP, MQTT, AMQP와 websocket을 통한 MQTT를 포함하여 IoT Hub에서 지원하는 모든 프로토콜을 지원합니다. 또한 이 릴리스는 장치 쪽과 클라이언트 쪽의 확장된 SDK 언어 지원에 해당합니다.

## <a name="link-the-device-provisioning-service-to-an-iot-hub"></a>IoT Hub에 Device Provisioning Service 연결

다음 단계는 IoT Hub Device Provisioning Service가 장치를 해당 허브에 연결할 수 있도록 Device Provisioning Service와 IoT Hub를 연결하는 것입니다. 서비스는 장치를 Device Provisioning Service에 연결된 IoT Hub에만 프로비전할 수 있습니다. 다음 단계를 수행합니다.

1.  Azure Portal의 **모든 리소스** 페이지에서 이전에 만든 Device Provisioning Service 인스턴스를 클릭합니다.

2.  Device Provisioning Service 페이지에서 **연결된 IoT Hub**를 클릭합니다.

3.  **추가**를 클릭합니다.

4.  **IoT Hub에 대한 연결 추가** 페이지에서 다음 정보를 입력하고 **저장**을 클릭합니다.

    - **구독:** IoT Hub를 포함하는 구독을 선택해야 합니다. 다른 구독에 상주하는 IoT Hub에 연결할 수 있습니다.

    - **IoT Hub:** 이 Device Provisioning Service 인스턴스와 연결할 IoT Hub 이름을 선택합니다.

    - **액세스 정책:** IoT Hub에 연결하는 데 사용할 자격 증명으로 **iothubowner**를 선택합니다.

![포털에서 DPS에 연결할 허브 이름 연결](../media/ee6e78754a1d39d86de71fb6872723f3.png)

## <a name="set-the-allocation-policy-on-the-device-provisioning-service"></a>Device Provisioning Service에서 할당 정책 설정

할당 정책은 IoT Hub에 장치를 할당하는 방법을 결정하는 IoT Hub Device Provisioning Service 설정입니다. 세 가지의 지원되는 할당 정책이 있습니다.

1. **최소 대기 시간**: 장치가 대기 시간이 가장 낮은 허브를 기준으로 IoT Hub에 프로비전됩니다.

2. **균등 가중치 배포**(기본값): 연결된 IoT Hub들은 동일하게 해당 허브에 프로비전된 장치를 갖게 됩니다. 이 설정은 기본값입니다. 장치를 단 하나의 IoT Hub에 프로비전하려는 경우 이 설정을 유지할 수 있습니다.

3. **등록 목록을 통한 고정 구성**: 등록 목록에서 원하는 IoT Hub의 사양을 Device Provisioning Service 수준 할당 정책보다 우선합니다.

할당 정책을 설정하려면 Device Provisioning Service 페이지에서 **할당 정책 관리**를 클릭합니다. 할당 정책이 **균등 가중치 배포**(기본값)로 설정되어 있는지 확인합니다. 변경하려면 변경 후 **저장**을 클릭합니다.

![할당 정책 관리](../media/0c5fa5193156f17b4f5d64aab65a414d.png)

## <a name="enroll-the-device"></a>장치 등록

이 단계에서는 Device Provisioning Service에 장치 고유의 보안 아티팩트를 추가하는 것이 포함됩니다. 이러한 보안 아티팩트는 다음과 같은 장치의 [증명 메커니즘](https://docs.microsoft.com/azure/iot-dps/concepts-device#attestation-mechanism)을 기반으로 합니다.

TPM 기반 장치의 경우 다음과 같은 항목이 필요합니다.

- TPM 칩 제조업체에서 얻은 각 TPM 칩 또는 시뮬레이션에 고유한 *인증 키*. 자세한 정보는 [TPM 인증 키 이해](https://docs.microsoft.com/windows-server/identity/ad-ds/manage/component-updates/tpm-key-attestation#terminology)를 읽어보세요.

- 네임스페이스/범위에서 장치를 고유하게 식별하는 데 사용되는 *등록 ID*입니다. 이 ID는 장치 ID와 같을 수도 있고 다를 수도 있습니다. ID는 모든 장치에 필수입니다. TPM 기반 장치의 경우 등록 ID는 TPM 인증 키의 SHA-256 해시와 같이 TPM 자체에서 파생될 수도 있습니다.

![포털에서 TPM에 대한 등록 정보](../media/11db90b7128e1cf222a4da45de7cbac8.png)

X.509 기반 장치의 경우 다음과 같은 항목이 필요합니다.

- [X.509에 발급된 인증서](https://docs.microsoft.com/windows/desktop/SecCertEnroll/about-x-509-public-key-certificates) 칩 또는 시뮬레이션입니다. 형식은 *.pem* 또는 *.cer* 파일 중 하나입니다. 개별 등록은 X.509 시스템에 대한 장치별 *서명자 인증서*를, 등록 그룹의 경우 *루트 인증서*를 사용해야 합니다.

   ![포털에서 X.509 증명에 대한 개별 등록 추가](../media/8d56752f453f27e55dd15b7c894ae406.png)

Device Provisioning Service에 장치를 등록하는 방법은 두 가지가 있습니다.

- **등록 그룹** 특정 증명 메커니즘을 공유하는 장치의 그룹을 나타냅니다. 원하는 초기 구성을 공유하는 장치 수가 많은 경우 또는 장치가 모두 동일한 테넌트로 이동하는 경우 등록 그룹을 사용하는 것이 좋습니다. 등록 그룹의 Id 증명에 대한 자세한 내용은 [보안](https://docs.microsoft.com/azure/iot-dps/concepts-security#controlling-device-access-to-the-provisioning-service-with-x509-certificates)을 참조하세요.

   ![포털에 X.509 증명에 대한 그룹 등록 추가](../media/4a9d9ea822887c70f1ff1e4b64b138f1.png)

- **개별 등록** Device Provisioning Service에 등록할 수도 있는 단일 장치에 대한 항목을 나타냅니다. 개별 등록은 증명 메커니즘으로 x509 인증서 또는 SAS 토큰(실제 또는 가상 TPM) 중 하나를 사용할 수 있습니다. 고유한 초기 구성이 필요한 장치 및 증명 메커니즘으로 TPM 또는 가상 TPM을 통해 SAS 토큰만을 사용할 수 있는 장치의 경우 개별 등록을 사용하는 것이 좋습니다. 개별 등록에는 원하는 IoT Hub 장치 ID가 지정될 수 있습니다.

이제 장치의 증명 메커니즘에 따라 필요한 보안 아티팩트를 사용하여 장치를 Device Provisioning Service 인스턴스에 등록합니다.

1. Azure Portal에 로그인하고, 왼쪽 메뉴에서 **모든 리소스** 단추를 클릭하고, Device Provisioning Service를 엽니다.

2. Device Provisioning Service 요약 블레이드에서 **등록 관리**를 선택합니다. **개별 등록** 탭 또는 **등록 그룹** 탭 중 하나를 장치 설정에 따라 탭합니다. 위쪽에 있는 **추가** 단추를 클릭합니다. **TPM** 또는 **X.509**를 ID 증명 *메커니즘*으로 선택하고, 이전에 설명된 대로 적절한 보안 아티팩트를 입력합니다. 새 **IoT Hub 장치 ID**를 입력할 수도 있습니다. 완료되면 **저장** 단추를 클릭합니다.

3. 장치를 성공적으로 등록하면 포털에 다음과 같은 화면이 표시됩니다.

![포털에서 성공적인 TPM 등록](../media/cb277b2e5bc21cd02669775d536e89c0.png)

등록 후 프로비전 서비스는 향후 특정한 시점에 이러한 장치가 부팅 및 연결될 때까지 대기합니다. 장치를 처음으로 부팅하는 경우 클라이언트 SDK 라이브러리는 칩과 상호 작용하여 장치에서 보안 아티팩트를 추출하고, Device Provisioning Service에 등록을 확인합니다.

## <a name="start-the-iot-device"></a>IoT 장치 시작

IoT 장치는 실제 장치일 수도 있고 시뮬레이션된 장치일 수도 있습니다. IoT 장치가 장치 프로비전 서비스 인스턴스에 등록되었으니, 이제 장치를 부팅하고, 증명 메커니즘을 사용하여 프로비전 서비스를 호출하고 인식할 수 있습니다. 프로비전 서비스에서 장치를 인식하면 장치가 IoT Hub에 할당됩니다.

TPM 및 X.509 증명을 사용하여 시뮬레이션된 장치 예제가 C, Java, C\#, Node.js 및 Python용으로 포함되어 있습니다. 예를 들어 TPM 및 [Azure IoT C SDK](https://github.com/Azure/azure-iot-sdk-c)를 사용하여 시뮬레이션된 장치는 [장치의 첫 번째 부팅 시퀀스 시뮬레이션](https://docs.microsoft.com/azure/iot-dps/quick-create-simulated-device#simulate-first-boot-sequence-for-the-device) 섹션에 설명된 프로세스를 따릅니다. X.509 인증서 증명을 사용하는 동일한 장치는 이 [부팅 시퀀스](https://docs.microsoft.com/azure/iot-dps/quick-create-simulated-device-x509#simulate-first-boot-sequence-for-the-device) 섹션을 참조하세요.

실제 장치의 예제는 [MXChip Iot DevKit에 대한 방법 가이드](https://docs.microsoft.com/azure/iot-dps/how-to-connect-mxchip-iot-devkit)를 참조하세요.

장치를 시작하고 장치의 클라이언트 응용 프로그램이 Device Provisioning Service에 등록할 수 있도록 허용하세요.

## <a name="verify-the-device-is-registered"></a>장치가 등록되어 있는지 확인

장치가 부팅되면 다음 작업을 수행해야 합니다.

1. 장치가 Device Provisioning Service에 등록 요청을 보냅니다.

2. TPM 장치의 경우 Device Provisioning Service에서 장치가 응답하는 등록 챌린지를 다시 보냅니다.

3. 등록에 성공하면 Device Provisioning Service는 IoT Hub URI, 장치 ID 및 암호화된 키를 장치로 다시 보냅니다.

4. 그러면 장치의 IoT Hub 클라이언트 응용 프로그램이 사용자 허브에 연결됩니다.

5. 허브에 성공적으로 연결되면 IoT Hub의 **IoT 장치** 탐색기에 장치가 표시됩니다.

![포털에서 허브에 연결 성공](../media/12ea6da6eef9bf96be6bd80aa1721173.png)

<!--Reference links

-   <https://docs.microsoft.com/azure/iot-dps/tutorial-set-up-cloud>

-   <https://docs.microsoft.com/azure/iot-dps/tutorial-provision-device-to-hub>-->