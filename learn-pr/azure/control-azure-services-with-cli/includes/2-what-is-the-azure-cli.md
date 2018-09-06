Azure CLI는 Azure에 연결하고 Azure 리소스에서 관리 명령을 실행하는 명령줄 프로그램입니다. Linux, macOS 및 Windows에서 실행되며 관리자와 개발자가 이를 사용하여 웹 브라우저 대신 터미널 또는 명령줄 프롬프트(또는 스크립트)를 통해 명령을 실행할 수 있습니다. 예를 들어 VM(가상 머신)을 다시 시작하려면 다음과 같은 명령을 사용합니다.

 ```bash
 az vm restart -g MyResourceGroup -n MyVm
 ```

Azure CLI는 Azure 리소스를 관리하기 위한 플랫폼 간 명령줄 도구를 제공하며 Linux, Mac 또는 Windows 컴퓨터에 로컬로 설치할 수 있습니다. Azure CLI는 Azure Cloud Shell을 통해 브라우저에서도 사용할 수 있습니다. 두 경우에 모두 대화형으로 사용하거나 스크립팅할 수 있습니다. 대화형 사용의 경우 먼저 Windows에서 cmd.exe와 같은 셸을 먼저 시작하거나 Linux 또는 macOS에서 Bash를 시작한 후 셸 프롬프트에서 명령을 실행합니다. 반복 작업을 자동화하려면 선택한 셸의 스크립트 구문을 사용하여 셸 스크립트로 CLI 명령을 어셈블한 후 스크립트를 실행합니다.

## <a name="how-to-install-azure-cli"></a>Azure CLI를 설치하는 방법

Linux 및 macOS에서는 둘 다 패키지 관리자를 사용하여 PowerShell Core를 설치합니다. 권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다.
- Linux: **apt-get**(Ubuntu), **yum**(Red Hat) 및 **zypper**(OpenSUSE)
- Mac: **Homebrew**

Azure CLI는 Microsoft 리포지토리에서 사용할 수 있으므로 먼저 패키지 관리자에 해당 리포지토리를 추가해야 합니다.

Windows에서는 MSI 파일을 다운로드하고 실행하여 Azure CLI를 설치합니다.

## <a name="using-the-azure-cli-in-scripts"></a>스크립트에서 Azure CLI 사용

스크립트에서 Azure CLI 명령을 사용하려면 스크립트 실행에 사용되는 “셸” 또는 환경에 관련된 문제를 알고 있어야 합니다. 예를 들어 bash 셸에서는 변수를 설정할 때 다음 구문이 사용됩니다.

 ```bash
 variable="value"
 variable=integer
 ```

Azure CLI 스크립트를 실행하는 데 PowerShell 환경을 사용하는 경우 변수에 이 구문을 사용해야 합니다.

 ```powershell
 $variable="value"
 $variable=integer
 ```

## <a name="summary"></a>요약

로컬 컴퓨터에서 Azure 리소스를 관리하는 데 사용하려면 먼저 Azure CLI를 설치해야 합니다. 설치 단계는 Windows, Linux 및 macOS에 따라 다르지만, 설치된 후에 명령은 전체 플랫폼에서 공통적입니다. 
