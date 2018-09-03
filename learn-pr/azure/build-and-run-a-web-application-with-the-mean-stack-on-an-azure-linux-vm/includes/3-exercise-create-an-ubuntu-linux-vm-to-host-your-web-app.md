구성 요소의 MEAN 스택에는 서버가 필요합니다. 사용자 고유의 서버실에서 실행 중인 가상 머신 또는 Linux 머신일 수 있으며 클라우드 기반 가상 머신에서 구성될 수 있습니다. 이 모듈에서는 Azure에서 실행 중인 Ubuntu Linux 가상 머신에서 실행할 스택을 설정합니다.

이 연습에서는 Azure에서 호스팅되는 새로운 Ubuntu Linux 가상 머신을 만듭니다. 또한 기존 가상 머신 또는 물리적 호스트 머신에서 MEAN 스택 구성 요소를 설치할 수도 있습니다. 이 연습으로 새 항목을 작성하면 모든 구성 요소를 Azure 리소스 그룹에 연결하여 연습을 완료한 후 관리 및 정리를 쉽게 할 수 있습니다.

Azure Portal에 통합된 Cloud Shell 명령줄을 사용하여 Linux VM을 만듭니다.

## <a name="provision-an-ubuntu-linux-vm"></a>Ubuntu Linux VM 프로비전

1. [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동합니다.
1. Azure Portal 도구 모음의 `>_` 아이콘에서 Cloud Shell을 엽니다.
1. Cloud Shell 내에서 해당 명령을 실행하여 VM을 포함할 Azure 리소스 그룹을 만듭니다. `<resource-group-name>`을 사용자 고유의 리소스 그룹 이름으로, `<resource-group-location>`을 원하는 Azure 위치(예: `westus`)로 바꿉니다.

    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    다른 명령에서 사용할 수 있으므로 리소스 그룹 이름을 기억하세요.

1. Cloud Shell에서 다음 명령을 실행하여 새로운 Ubuntu Linux VM을 만듭니다. `<resource-group-name>`을 사용자 고유의 리소스 그룹 이름으로, `<vm-admin-username>` 및 `<vm-admin-password>`를 기본 설정된 관리자 사용자 이름 및 암호로 바꿉니다.

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    나중에 이 VM에 연결할 수 있도록 관리자 사용자 이름과 암호를 기록해 두세요.

    이 명령은 완료되는 데 약 2분 정도 걸립니다. 명령이 완료되면 결과 출력은 다음과 유사합니다.

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    또한 VM에 연결하기 위해 새로 생성된 VM의 공용 IP 주소도 저장하려고 합니다.

1. 새 VM에 연결을 다시 시도하세요.

    명령 프롬프트/터미널 창을 열고 다음 명령을 실행합니다. `<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공개 IP 주소로 바꿉니다.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    처음 머신에 연결할 때 원격 머신을 신뢰하는지 묻는 메시지가 나타납니다. `yes`로 응답하면 머신의 ECDSA 키 지문이 로컬에 저장되어 후속 연결을 신뢰하게 됩니다.

    문제 없이 모든 항목이 진행되면 `exit`를 입력하여 SSH 세션을 닫습니다.

1. 새로 만들 웹 응용 프로그램에 들어오는 HTTP 트래픽을 허용하도록 포트 80을 엽니다.

    Azure Portal의 Cloud Shell로 돌아가 `<resource-group-name>`에 대한 원본 리소스 그룹 이름을 사용하여 다음 명령을 실행합니다.

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    그러면 생성될 때 "MeanDemo"라는 이름의 VM에서 HTTP 포트가 열립니다.

## <a name="summary"></a>요약

새로운 Ubuntu Linux VM을 사용할 준비가 되었으므로 이제 이를 연결하여 MEAN 스택의 다양한 구성 요소를 설치할 수 있습니다.
