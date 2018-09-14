Azure에 Linux VM이 준비되었으면, 다음으로 진행할 작업은 Azure로 옮기려는 작업 맞게 VM을 구성하는 것입니다.

사이트 간 VPN을 Azure로 설정하지 않았다면 로컬 네트워크에서 Azure VM에 액세스할 수 없습니다. Azure 사용을 처음 시작하는 경우에는 작동 중인 사이트 간 VPN이 없을 가능성이 높습니다. 그러면 가상 머신에 어떻게 연결할 수 있을까요?

## <a name="azure-vm-ip-addresses"></a>Azure VM IP 주소

조금 전에 봤듯이 Azure VM은 가상 네트워크에서 통신합니다. 또한 선택적인 공용 IP 주소가 할당되어 있을 수 있습니다. 공용 IP가 있으면 인터넷을 통해 VM과 상호 작용이 가능합니다. 온-프레미스 네트워크를 Azure에 연결하는 VPN(가상 사설망)을 설정할 수도 있습니다. 그러면 공용 IP를 노출시키지 않고 VM에 안전하게 연결할 수 있습니다. 이 방식은 다른 모듈에 설명되어 있으며, 해당 옵션에 관심이 있는 사용자를 위해 전체 설명이 문서로 작성되어 있습니다.

Azure의 공용 IP 주소는 동적으로 할당된 경우가 많습니다. VM 다시 시작 되 면 Vm에 대 한 시간별-IP 주소를 변경할 수 있습니다 즉 발생 합니다. 이름 대신 특정 IP 주소에 직접 연결하고 IP 주소가 변경되지 않도록 하려는 경우 추가 요금을 결제하고 정적 주소를 할당할 수 있습니다.

## <a name="connect-to-an-azure-linux-vm-with-ssh"></a>SSH로 Azure Linux VM에 연결

SSH를 사용 하 여 Azure에서 VM에 연결 하는 것은 간단 합니다. Azure 포털의 맨 위에 있는 VM의 속성을 열고, 클릭 **Connect**합니다. 그러면 VM에 할당된 IP 주소와 SSH의 모든 로그인 세부 정보가 표시됩니다. 

![새로 만든된 Linux VM에 SSH를 통해 연결 하도록 구성 된 가상 머신 블레이드로 연결을 보여주는 Azure portal의 스크린샷.](../media/5-connect-ssh.png)

세부 정보가 표시되면 다음 명령을 사용하여 Linux VM에 연결할 수 있습니다.

```bash
ssh jim@137.117.101.249
```

처음으로 연결하면 SSH는 알려지지 않은 호스트에 대한 인증을 요청합니다. 이 서버에 연결한 적이 없다는 알림도 표시됩니다. 이것이 사실 고은 지극히 정상적으로 응답할 수 있습니다 하는 경우 **예** 서버의 지문이 알려진된 호스트 파일에 저장 합니다.

```output
The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
```

## <a name="transferring-files-to-the-vm"></a>VM으로 파일 전송

일반적으로 수행하는 또 다른 작업은 로컬 파일 또는 데이터를 서버 간에 복사하는 것입니다. 여기서는 웹 사이트 데이터를 Azure VM에 복사할 것입니다. Linux VM과 SSH를 사용하는 경우 `scp` 명령을 사용하면 됩니다. 이 명령은 `cp`를 사용하여 로컬 파일을 복사하는 방식과 비슷합니다. 단, 명령에 원격 사용자와 호스트를 지정해야 합니다.

예를 들어 현재 디렉터리의 `somefile.txt`를 IP 주소가 `192.168.1.25`인 Linux 머신의 `~/folder`에 복사하려는 경우 다음 명령을 입력하면 됩니다.

```bash
scp somefile.txt someuser@192.168.1.25:~/folder/
```

그러면 원격 시스템에서 `someuser`로 인증이 진행되어 암호를 입력하라는 메시지가 표시되거나 SSH 개인 키가 사용됩니다. 해당 사용자는 대상 서버의 `~/folder/`에 대한 쓰기 권한이 있어야 합니다.

> [!WARNING]
> 명령줄을 올바르게 입력하지 않으면 `scp`는 로컬 파일 복사를 수행합니다. 가장 자주 빠뜨리는 부분은 대상 폴더입니다.

SSH를 사용하여 실행 중인 Linux VM에 연결해 보겠습니다.