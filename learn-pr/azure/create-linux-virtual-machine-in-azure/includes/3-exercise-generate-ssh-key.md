Azure에서 Linux 가상 머신을 만들려면 먼저 원격 액세스에 대해 고려해야 합니다. 소프트웨어를 구성 하 고 유지 관리를 수행 하려면 Linux 웹 서버에 로그인 할 수 있도록 하려고 합니다. Azure에 호스트되는 Linux VM을 관리하는 기본적인 수단은 SSH입니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-ssh"></a>SSH란?

SSH(Secure Shell)는 암호화된 연결 프로토콜이며, 보안이 설정되지 않은 연결을 통한 보안 로그인을 허용합니다. SSH를 사용하면 네트워크 연결을 사용하여 원격 위치에서 터미널 셸에 연결할 수 있습니다.

두 가지 방법으로 SSH 연결을 인증에 사용할 수 있습니다: **사용자 이름 및 암호**, 또는 **SSH 키 쌍**합니다.

> [!TIP]
> SSH에 암호화 된 연결을 제공 하지만 SSH 연결과 함께 암호를 사용 하 여 VM에 취약해 무작위 암호 공격입니다. SSH 사용 하 여 Linux VM에 연결 하는 보다 안전 하 고 기본 메서드는 공개-개인 키 쌍을, SSH 키 라고도 합니다.

SSH 키 쌍을 사용하면 Linux 기반 Azure Virtual Machines에 암호 없이 로그인할 수 있습니다. 몇 대의 컴퓨터에서 VM에 로그인 하려는 경우이 방법이 더 안전 합니다. 다양한 위치에서 Linux VM에 액세스할 수 있어야 하는 경우에는 사용자 이름과 암호 조합이 더 좋은 방법일 수 있습니다. SSH 키 쌍을 위한 두 가지: 공개 키와 개인 키입니다.

* 공개 키는 public-key 암호화를 사용하려는 Linux VM 또는 다른 서비스에 배치됩니다. 이 키는 다른 사람과 공유할 수 있습니다.

* 합니다 **개인 키** SSH 연결을 설정 하는 경우 Linux VM에 본인 확인에 제출 됩니다. 이것은 기밀 정보이며 암호나 기타 개인 데이터처럼 보호해야 합니다.

동일한 단일 공개-개인 키 쌍을 사용하여 여러 Azure VM 및 서비스에 액세스할 수 있습니다.

## <a name="create-the-ssh-key-pair"></a>SSH 키 쌍 만들기

Linux, Windows 10 및 MacOS에서는 기본 제공되는 `ssh-keygen` 명령을 사용하여 공개 키 및 개인 키 파일을 생성할 수 있습니다.

> [!TIP]
> Windows 10의 경우 **Fall Creators Update**에 SSH 클라이언트가 포함되어 있습니다. 이전 버전 Windows의 SSH;를 사용 하는 추가 소프트웨어 필요 [에 대 한 자세한 설명서를](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows)입니다. 또는 Windows에 대 한 Linux 하위 시스템을 설치할 수 있으며 동일한 기능을 얻을 수 있습니다.

> [!NOTE]
> 개인 저장소 계정에 Azure에서 생성 된 키를 저장 하는 Azure Cloud Shell을 사용 합니다. 원하는 경우 다음 명령을 로컬 셸에 직접 입력할 수도 있습니다. 이 방법을 사용하는 경우에는 로컬 세션을 반영하기 위해 이 모듈 전체에서 지침을 조정해야 합니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

Azure VM에 대한 키 쌍을 생성하는 데 필요한 최소 명령은 다음과 같습니다. 2048 비트 길이 (최소 길이)를 사용 하 여 SSH 프로토콜을 2 (SSH-2) RSA 공개-개인 키 쌍 만들기는이 합니다.

Cloud Shell에이 명령을 입력 합니다.

```bash
ssh-keygen -t rsa -b 2048
```

이 도구를 파일 이름 및 선택적 암호를 입력 합니다. 기본값을 적용합니다. `~/.ssh` 디렉터리에 `id_rsa` 및 `id_rsa.pub`이라는 두 개의 파일이 만들어집니다. 파일이 있으면 덮어씁니다. 파일 이름 또는 암호를 프롬프트 방지를 제공 하기 위해 사용할 수 있는 다양 한 옵션이 있습니다.

### <a name="private-key-passphrase"></a>개인 키 암호

개인 키를 생성하는 동안 선택적으로 암호를 입력할 수 있습니다. 키를 사용할 때 입력해야 하는 암호입니다. 이 암호는 개인 SSH 키 파일에 액세스하는 데 사용되며 사용자 계정 암호가 아닙니다.

SSH 키를 암호를 추가 하면 128 비트 AES를 사용 하 여 개인 키를 해독 하는 데 암호가 없는 수 있도록 개인 키를 암호화 합니다.

> [!IMPORTANT]
> 암호를 추가하는 것이 **가장** 좋습니다. 공격자가 개인 키를 훔치고 해당 키에 암호가 없는 경우 해당 개인 키를 사용하여 해당하는 공개 키가 있는 서버에 로그인할 수 있습니다. 개인 키, 암호를 보호 하는 경우 공격자가 사용할 수 없습니다. Azure에서 인프라에 대 한 추가 보안 계층을 제공합니다.

다음은 암호를 설정하는 방법을 보여주는 예제입니다. (수도 있지만 하려는 경우)이이 명령을 실행할 필요가 없습니다.

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
| `-C` | 공개 키를 식별하는 데 사용할 수 있는 공개 키에 추가할 선택적인 주석입니다. 일반적으로 전자 메일 주소를 사용 하는 이지만 간단한 텍스트입니다. 결과적으로, 선호 하는 확인 방법을 사용할 수 있습니다. |
| `-f` | 개인 키 파일의 위치와 파일 이름입니다. **.pub**가 추가된 해당 공개 키 파일이 동일한 디렉터리에 생성됩니다. 디렉터리가 있어야 합니다. |
| `-N` | 개인 키를 암호화하는 데 사용되는 암호입니다. |

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a>Azure Linux VM에서 SSH 키 쌍 사용

키 쌍이 생성되면 Azure의 Linux VM에서 사용할 수 있습니다. VM 만드는 동안 공개 키를 제공할 수도 있고 VM이 만들어지면 추가 수도 있습니다.

다음 명령을 사용 하 여 Azure Cloud Shell에서 파일의 내용을 볼 수 있습니다.

```bash
cat ~/.ssh/id_rsa.pub
```

한 줄이며 다음과 같은 모양입니다.

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

다음 연습에서 사용할 수 있도록이 값을 복사 합니다.

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a>Linux VM을 만들 때 SSH 키 사용

새 Linux VM을 만드는 동안 SSH 키를 적용하려면 공개 키의 콘텐츠를 복사하여 Azure Portal에 제공_하거나_ 공개 키 파일을 Azure CLI 또는 Azure PowerShell 명령에 제공합니다. 이 방법은 Linux VM을 만들 때 사용하겠습니다.

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a>기존 Linux VM에 SSH 키 추가

VM을 이미 만든 경우 `ssh-copy-id` 명령으로 Linux VM에 공개 키를 설치할 수 있습니다. SSH에 대한 권한이 키에 부여되면 암호 없이 서버에 대한 액세스 권한이 부여됩니다.

키와 연결할 사용자 이름 및 공개 키 파일을 전달 합니다.

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```

만들었으므로 공개 키를 Azure portal로 전환 하 고 Linux VM 만들기 보겠습니다.
