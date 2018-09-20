구성 요소의 MEAN 스택에는 서버가 필요합니다. 사용자 고유의 서버실에서 실행 중인 가상 머신 또는 Linux 머신일 수 있으며 클라우드 기반 가상 머신에서 구성될 수 있습니다. 이 모듈에서는 Azure에서 실행 중인 Ubuntu Linux 가상 머신에서 실행할 스택을 설정합니다.

이 단원에서는 Azure에 호스트되는 새로운 Ubuntu Linux 가상 머신을 만듭니다. 또한 기존 가상 머신 또는 물리적 호스트 머신에서 MEAN 스택 구성 요소를 설치할 수도 있습니다. 이 연습으로 새 항목을 작성하면 모든 구성 요소를 Azure 리소스 그룹에 연결하여 연습을 완료한 후 관리 및 정리를 쉽게 할 수 있습니다.

## <a name="provision-an-ubuntu-linux-vm"></a>Ubuntu Linux VM 프로비전

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="creating-a-resource-group"></a>리소스 그룹을 만들기

일반적으로 새 리소스 집합을 만들 때 가장 먼저 할일은 모든 리소스를 소유할 _리소스 그룹_을 만드는 것입니다. 이 작업은 Azure 샌드박스에서 불필요한 단계일 수 있지만 사용자 고유의 구독에서 작업할 때 다음 명령을 사용하여 사용자에게서 가까운 위치에 리소스 그룹을 만듭니다.

```azurecli
az group create --name <resource-group-name> --location <resource-group-location>
```

> [!IMPORTANT]
> Azure 샌드박스를 사용하여 리소스 그룹을 만들 필요가 없습니다. 대신, **<rgn>[샌드박스 리소스 그룹]</rgn>** 이라는 미리 생성된 리소스 그룹을 사용합니다.

1. 오른쪽에 있는 Cloud Shell에서 다음 명령을 입력하여 새 Ubuntu Linux VM을 만듭니다. `<vm-admin-username>` 및 `<vm-admin-password>`를 기본 설정된 관리자 사용자 이름 및 암호로 바꿉니다.

    ```azurecli
    az vm create \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
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
        "location": "<resource group location>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<rgn>[Sandbox resource group name]</rgn>",
        "zones": ""
    }
    ```

    또한 VM에 연결하기 위해 새로 생성된 VM의 공용 IP 주소도 저장하려고 합니다.

1. 새 VM에 연결을 시도하세요.

    Cloud Shell에서 다음 명령을 실행합니다. `<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공개 IP 주소로 바꿉니다.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    처음 머신에 연결할 때 원격 머신을 신뢰하는지 묻는 메시지가 나타납니다. `yes`로 응답하면 머신의 ECDSA 키 지문이 로컬에 저장되어 후속 연결을 신뢰하게 됩니다. 그러면 연결할 때마다 암호를 확인하는 메시지가 표시되는 것을 보게 됩니다.

    모든 항목이 문제없으면 `exit`를 입력하여 SSH 세션을 닫습니다.

1. 새로 만들 웹 응용 프로그램에 들어오는 HTTP 트래픽을 허용하도록 VM에서 포트 80을 엽니다.

    ``` bash
    az vm open-port --port 80 --resource-group <rgn>[Sandbox resource group name]</rgn> --name MeanDemo
    ```

    이 명령은 생성될 때 "MeanDemo"라는 이름이 지정된 VM에서 HTTP 포트를 엽니다.

## <a name="summary"></a>요약

새로운 Ubuntu Linux VM을 사용할 준비가 되었으므로 이제 이를 연결하여 MEAN 스택의 다양한 구성 요소를 설치할 수 있습니다.