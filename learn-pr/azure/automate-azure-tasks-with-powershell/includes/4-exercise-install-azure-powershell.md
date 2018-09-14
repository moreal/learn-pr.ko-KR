이 장치에 설치할지 **PowerShell** 로컬 컴퓨터에 있습니다.

> [!NOTE]
> 이 연습에서는 PowerShell 도구를 로컬로 설치 하는 과정을 안내 합니다. 모듈의 나머지 부분에서는 Microsoft Learn의 무료 구독 지원을 활용할 수 있도록 Azure Cloud Shell을 사용합니다. 이 연습을 선택적 작업으로 고려하고 원하는 경우 지침을 검토할 수 있습니다.

::: zone pivot="linux"

## <a name="linux"></a>Linux

Linux 용 PowerShell 설치 패키지 관리자를 사용 하 여 포함 됩니다. 여기에 나온 예에서는 **Ubuntu 18.04**를 사용하지만, [설명서에 다른 버전 및 배포에 대한 자세한 지침](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)이 나와 있습니다.

여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 Ubuntu Linux에 PowerShell Core를 설치합니다. 

1. Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다. 이렇게 하면 설치한 PowerShell Core 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. 패키지 관리자가 PowerShell Core 패키지를 찾을 수 있도록 **Microsoft Ubuntu 리포지토리**를 등록합니다.

    ```bash
    sudo curl -o /etc/apt/sources.list.d/microsoft.list https://packages.microsoft.com/config/ubuntu/18.04/prod.list
    ```

1. 패키지 목록을 업데이트합니다.

    ```bash
    sudo apt-get update
    ```

1. PowerShell Core를 설치합니다.

    ```bash
    sudo apt-get install -y powershell
    ```

1. PowerShell을 시작하여 성공적으로 설치되었는지 확인합니다.

    ```bash
    pwsh
    ```
::: zone-end

::: zone pivot="macos"

## <a name="macos"></a>MacOS

MacOS에서 설치 하는 첫 번째 단계입니다 **PowerShell Core**합니다. 이렇게 Homebrew 패키지 관리자를 사용 하 여 합니다.

> [!IMPORTANT]
> **brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다. 자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.

1. PowerShell Core 패키지를 포함하여 추가 패키지를 얻으려면 Homebrew-Cask를 설치하세요.

    ```bash
    brew tap caskroom/cask
    ```

1. PowerShell Core 설치:

    ```bash
    brew cask installs powershell
    ```

1. PowerShell Core를 시작하여 성공적으로 설치되었는지 확인합니다.

    ```bash
    pwsh
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a>Windows
PowerShell은 Windows, 그러나 못할 업데이트로 컴퓨터에 대 한 포함 됩니다. 사용 하려는 Azure 지원에는 PowerShell 버전 5.0 이상이 필요 합니다. 다음 단계를 통해 설치 된 버전을 확인할 수 있습니다.

1. **시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다. 사용할 수 있습니다 여러 바로 가기 링크:
    - Windows PowerShell-이 고 64 비트 버전을 일반적으로 선택 해야 합니다.
    - Windows PowerShell (x86)-64 비트 Windows에 설치 하는 32 비트 버전입니다.
    - Windows PowerShell ISE-통합 스크립팅 환경 (ISE) PowerShell에서 스크립트 작성에 사용 됩니다. 
    - Windows PowerShell ISE (x86)-32 비트 버전의 ISE입니다.

1. Windows PowerShell 아이콘을 선택 합니다.

1. 설치 된 powershell 버전을 확인 하려면 다음 명령을 입력 합니다.

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
버전 번호를 5.0 보다 낮은 경우를 위한이 지침을 따릅니다 [기존 Windows PowerShell 업그레이드](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)합니다.

::: zone-end

## <a name="summary"></a>요약
설치 프로그램이 로컬 컴퓨터에 PowerShell을 지원 해야 합니다. 다음으로, Azure 모듈을 포함 하 여 추가할 수 있습니다 하는 추가 명령에 대 한 설명 합니다.