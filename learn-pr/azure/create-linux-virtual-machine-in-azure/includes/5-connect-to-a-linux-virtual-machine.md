이제 Azure에서 Linux VM을 만들었으므로, 다음으로는 Azure로 이동하려는 작업용으로 Linux VM을 구성합니다.

Azure에 대해 사이트 간 VPN을 설정하지 않았다면 로컬 네트워크에서 Azure VM에 액세스할 수 없습니다. Azure 사용을 처음 시작하는 경우에는 사이트 간 VPN이 작동하지 않을 가능성이 높습니다. 그렇다면 어떻게 가상 머신에 연결할 수 있을까요?

## <a name="azure-virtual-machines-ip-addresses"></a>Azure Virtual Machines IP 주소

조금 전에 살펴본 것처럼 Azure VM은 가상 네트워크에서 통신을 합니다. 또한 공용 IP 주소(선택 사항)가 할당될 수도 있습니다. 공용 IP가 있으면 인터넷을 통해 VM과 상호 작용할 수 있습니다. 온-프레미스 네트워크를 Azure에 연결하는 VPN(가상 사설망)을 설정할 수도 있습니다. 그러면 공용 IP를 표시하지 않고도 VM에 안전하게 연결할 수 있습니다. 이 방식에 대한 내용은 다른 모듈에 포함되어 있으며, 해당 옵션에 대해 살펴보려는 사용자를 위해 전체 설명이 문서로 작성되어 있습니다.

Azure에서 공용 IP 주소를 사용할 때 기억해야 할 한 가지 사항은, 공용 IP는 동적으로 할당되는 경우가 많다는 것입니다. 즉, 시간이 지나면 IP 주소가 변경될 수 있습니다. VM의 경우에는 VM을 다시 시작하면 IP 주소가 변경됩니다. 이름 대신 특정 IP 주소에 직접 연결하고 IP 주소가 변경되지 않도록 하려는 경우 추가 요금을 결제하고 고정 주소를 할당할 수 있습니다.

## <a name="connect-to-an-azure-linux-virtual-machines-with-ssh"></a>SSH를 사용하여 Azure Linux Virtual Machines 관리

SSH를 사용하면 Azure에서 VM에 손쉽게 연결할 수 있습니다. Azure Portal에서 VM 속성을 열고 위쪽의 **연결**을 클릭합니다. 그러면 VM에 할당된 IP 주소와 SSH의 모든 로그인 세부 정보가 표시됩니다. 

![Linux VM에 대한 SSH 연결 세부 정보](../media-drafts/5-connect-ssh.png)

이러한 세부 정보가 표시되면 다음 명령을 사용하여 Linux VM에 연결할 수 있습니다.

```bash
ssh jim@137.117.101.249
```

처음으로 연결하면 SSH에서 알 수 없는 호스트에 인증할 것인지를 묻는 메시지가 표시됩니다. 그리고 이 서버에 연결한 적이 없다는 알림도 표시됩니다. 해당 서버에 연결한 적이 없다면 이 알림은 정상적인 현상이므로 응답으로 “예”를 선택하여 서버 지문을 알려진 호스트 파일에 저장할 수 있습니다.

```output
The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
```

## <a name="transferring-files-to-the-vm"></a>VM으로 파일 전송

일반적으로 수행하는 또 다른 작업은 로컬 파일 또는 데이터를 서버 간에 복사하는 것입니다. 여기서는 웹 사이트 데이터를 Azure VM에 복사할 것입니다. Linux VM과 SSH를 사용하는 경우 `scp` 명령을 사용할 수 있습니다. 이 명령은 `cp`를 사용하여 로컬 파일을 복사하는 방식과 비슷합니다. 단, 명령에서 원격 사용자와 호스트를 지정해야 합니다. 

예를 들어 현재 디렉터리의 `somefile.txt`를 IP 주소가 `192.168.1.25`인 Linux 머신의 `~/folder`에 복사하려는 경우 다음 명령을 입력하면 됩니다.

```bash
scp somefile.txt someuser@192.168.1.25:~/folder/
```

이 명령을 실행하면 원격 시스템에서 `someuser`로 인증이 진행되어 암호를 입력하거나 SSH 개인 키를 사용하라는 메시지가 표시됩니다. 해당 사용자는 대상 서버의 `~/folder/`에 대한 쓰기 권한이 있어야 합니다.

> [!WARNING]
> 명령줄을 올바르게 입력하지 않으면 `scp`는 로컬 파일 복사를 수행합니다. 가장 흔히 빠뜨리는 부분은 대상 폴더 부분입니다.

SSH를 사용하여 실행 중인 Linux VM에 연결해 보겠습니다.