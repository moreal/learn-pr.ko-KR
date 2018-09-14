Azure PowerShell을 자동화 솔루션으로 선택했다고 가정합니다. 관리자는 Azure Cloud Shell 대신 로컬로 스크립트를 실행하는 것을 선호합니다. 팀은 Linux, macOS 및 Windows를 실행하는 컴퓨터를 사용합니다. Azure PowerShell이 모든 장치에서 작동해야 합니다. 

## <a name="what-must-be-installed"></a>무엇을 설치해야 하나요?
다음 단원에서 실제 설치 지침을 살펴보고 Azure PowerShell을 구성하는 두 개의 구성 요소를 살펴보겠습니다.

- **기본 PowerShell 제품** 이 제품에는 Windows용 PowerShell 및 macOS/Linux용 PowerShell Core의 두 가지 변형이 제공됩니다.
- **Azure PowerShell 모듈** PowerShell에 Azure 특정 명령을 추가하려면 이 추가 모듈을 설치해야 합니다.

> [!TIP]
> PowerShell은 Windows에 포함되지만 업데이트가 있을 수 있습니다. Linux 및 macOS에 PowerShell Core를 설치해야 합니다.

기본 제품이 설치되면 설치에 Azure PowerShell 모듈을 추가합니다.

## <a name="how-to-install-powershell-core"></a>PowerShell Core를 설치하는 방법
Linux 및 macOS에서는 둘 다 패키지 관리자를 사용하여 PowerShell Core를 설치합니다. 권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다.

> [!NOTE]
> PowerShell Core는 Microsoft 리포지토리에서 사용할 수 있으므로 먼저 패키지 관리자에 해당 리포지토리를 추가해야 합니다.

### <a name="linux"></a>Linux
Linux에서 패키지 관리자는 선택한 Linux 배포에 따라 변경됩니다.

| 배포  | 패키지 관리자 |
|------------------|-----------------|
| Ubuntu, Debian   | `apt-get`       |
| Red Hat, CentOS  | `yum`           |
| OpenSUSE         | `zypper`        |
| Fedora           | `dnf`           |

### <a name="mac"></a>Mac
macOS에서는 `Homebrew`를 사용하여 PowerShell Core를 설치합니다.

## <a name="summary"></a>요약
Windows에서는 PowerShell이 기본 제공되지만 Azure PowerShell 모듈을 설치해야 합니다. Linux 및 macOS에서는 PowerShell Core 및 Azure PowerShell 모듈을 둘 다 설치해야 합니다. 다음 섹션에서는 몇 가지 일반적인 플랫폼에 대한 자세한 설치 단계를 진행합니다.