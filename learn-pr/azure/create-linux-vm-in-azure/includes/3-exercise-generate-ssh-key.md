Azure에서 Linux 가상 머신을 만들려면 먼저 원격 액세스에 대해 고려해야 합니다. Linux 웹 서버에 로그인하여 소프트웨어를 구성하고 유지 관리를 수행할 수 있어야 합니다. Azure에 호스트되는 Linux VM을 관리하는 기본적인 수단은 SSH입니다.

## <a name="what-is-ssh"></a>SSH란?

SSH(Secure Shell)는 암호화된 연결 프로토콜이며, 보안이 설정되지 않은 연결을 통한 보안 로그인을 허용합니다. SSH를 사용하면 네트워크 연결을 사용하여 원격 위치에서 터미널 셸에 연결할 수 있습니다.

SSH 연결을 인증하는 두 가지 방법은 ** 사용자 이름/암호** 또는 **SSH 키 쌍**입니다. 

> [!TIP]
> SSH에서 암호화된 연결을 제공하지만 SSH 연결에 암호를 사용하면 VM이 무차별 암호 대입 공격(brute force attack)이나 암호 추측에 취약해집니다. SSH를 사용하여 Linux VM에 연결하는 보다 안전하고 널리 사용되는 방법은 공개 키-개인 키 쌍(SSH 키라고도 함)입니다.

SSH 키 쌍을 사용하면 Linux 기반 Azure Virtual Machines에 암호 없이 로그인할 수 있습니다. 몇 대의 컴퓨터에서만 로그인할 계획이면 이것이 보다 안전한 방법입니다. 다양한 위치에서 Linux VM에 액세스할 수 있어야 하는 경우에는 사용자 이름과 암호 조합이 더 좋은 방법일 수 있습니다. SSH 키 쌍에는 공개 키와 개인 키라는 두 부분이 있습니다.

* 공개 키는 public-key 암호화를 사용하려는 Linux VM 또는 다른 서비스에 배치됩니다. 이 키는 다른 사람과 공유할 수 있습니다.

* 개인 키는 사용자가 SSH 연결을 수행할 때 자신의 ID를 확인하기 위해 Linux VM에 제출하는 키입니다. 이것은 기밀 정보이며 암호나 기타 개인 데이터처럼 보호해야 합니다.

동일한 단일 공개-개인 키 쌍을 사용하여 여러 Azure VM 및 서비스에 액세스할 수 있습니다.

## <a name="create-the-ssh-key-pair"></a>SSH 키 쌍 만들기

Linux, Windows 10 및 MacOS에서는 기본 제공되는 `ssh-keygen` 명령을 사용하여 공개 키 및 개인 키 파일을 생성할 수 있습니다. 

> [!TIP]
> Windows 10의 경우 **Fall Creators Update**에 SSH 클라이언트가 포함되어 있습니다. 이전 버전의 Windows에서 SSH를 사용하려면 추가 소프트웨어가 필요합니다. [자세한 내용은 설명서를 참조하세요.](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows) 또는 Windows용 Linux 하위 시스템을 설치하고 동일한 기능을 확보할 수 있습니다.

> [!NOTE]
> 여기서는 Azure에서 생성된 키를 개인 저장소 계정에 저장하는 Azure Cloud Shell을 사용하겠습니다. 원하는 경우 다음 명령을 로컬 셸에 직접 입력할 수도 있습니다. 이 방법을 사용하는 경우에는 로컬 세션을 반영하기 위해 이 모듈 전체에서 지침을 조정해야 합니다.

Azure VM에 대한 키 쌍을 생성하는 데 필요한 최소 명령은 다음과 같습니다. 이를 통해 2048비트 길이(최소 길이)의 SSH-2(SSH 프로토콜 2) RSA 공개-개인 키 쌍이 만들어집니다. 

다음 명령을 Cloud Shell에 입력하세요.

```bash
ssh-keygen -t rsa -b 2048
```

도구에 파일 이름 및 선택적 암호를 입력하라는 메시지가 표시됩니다. 기본값을 적용합니다. `~/.ssh` 디렉터리에 `id_rsa` 및 `id_rsa.pub`라는 두 개의 파일이 만들어집니다. 파일이 있으면 덮어씁니다. 프롬프트를 방지하기 위해 파일 이름이나 암호를 제공하는 데 사용할 수 있는 다양한 옵션이 있습니다.

### <a name="private-key-passphrase"></a>개인 키 암호

개인 키를 생성하는 동안 선택적으로 암호를 입력할 수 있습니다. 키를 사용할 때 입력해야 하는 암호입니다. 이 암호는 개인 SSH 키 파일에 액세스하는 데 사용되며 사용자 계정 암호가 아닙니다. 

SSH 키에 암호를 추가하면 128비트 AES를 사용하여 개인 키가 암호화되기 때문에 암호화를 해독할 암호가 없으면 개인 키는 쓸모가 없습니다. 

> [!IMPORTANT]
> 암호를 추가하는 것이 **가장** 좋습니다. 공격자가 개인 키를 훔치고 해당 키에 암호가 없는 경우 해당 개인 키를 사용하여 해당하는 공개 키가 있는 서버에 로그인할 수 있습니다. 개인 키를 암호로 보호하면 공격자가 개인 키를 사용할 수 없기 때문에 Azure의 인프라에 대해 보안 계층이 추가로 제공됩니다.

다음은 암호를 설정하는 방법을 보여주는 예제입니다. 이 명령은(원하면 실행해도 되지만) 실행할 필요가 없습니다.

```bash
ssh-keygen -t rsa -b 4096 \
    -C "azureuser@myserver" \
    -f ~/.ssh/mykeys/myprivatekey \
    -N someReallySecurePhraseYouWillRemember
```

| 매개 변수 | 기능 |
|-----------|--------------|
| `-t` | 생성하는 키의 유형입니다. **rsa**여야 합니다. |
| `-b` | 키의 비트 수입니다. 최소 길이는 2048, 최대 길이는 4096입니다. |
| `-C` | 공개 키를 식별하는 데 사용할 수 있는 공개 키에 추가할 선택적인 주석입니다. 일반적으로 이메일 주소이지만 간단한 텍스트로 원하는 식별 방법을 사용할 수 있습니다. |
| `-f` | 개인 키 파일의 위치 및 이름입니다. **.pub**가 추가된 해당 공개 키 파일이 동일한 디렉터리에 생성됩니다. 디렉터리가 있어야 합니다. |
| `-N` | 개인 키를 암호화하는 데 사용되는 암호입니다. |

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a>Azure Linux VM에서 SSH 키 쌍 사용

키 쌍이 생성되면 Azure의 Linux VM에서 사용할 수 있습니다. VM을 생성하는 동안 공개 키를 제공하거나 VM을 만든 후에 공개 키를 추가할 수 있습니다. 

다음 명령을 사용하여 Azure Cloud Shell에서 파일의 콘텐츠를 볼 수 있습니다.

```bash
cat ~/.ssh/id_rsa.pub
```

한 줄이며 다음과 같은 모양입니다.

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

다음 연습에서 사용할 수 있도록 이 값을 복사하세요.

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a>Linux VM을 만들 때 SSH 키 사용

새 Linux VM을 만드는 동안 SSH 키를 적용하려면 공개 키의 콘텐츠를 복사하여 Azure Portal에 제공_하거나_ 공개 키 파일을 Azure CLI 또는 Azure PowerShell 명령에 제공합니다. 이 방법은 Linux VM을 만들 때 사용하겠습니다.

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a>기존 Linux VM에 SSH 키 추가

VM을 이미 만든 경우 `ssh-copy-id` 명령으로 Linux VM에 공개 키를 설치할 수 있습니다. SSH에 대한 권한이 키에 부여되면 암호 없이 서버에 대한 액세스 권한이 부여됩니다.

이것을 키와 연결할 사용자 이름 및 공개 키 파일에 전달합니다.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```
공개 키가 확보되었으면 Azure Portal로 전환하여 Linux VM을 만들겠습니다.

