이 단원에서는 로컬 머신에 **PowerShell**을 설치합니다.

> [!NOTE]
> 이 연습에서는 PowerShell 도구를 로컬로 설치하는 단계를 설명합니다. 모듈의 나머지 부분에서는 Microsoft Learn의 무료 구독 지원을 활용할 수 있도록 Azure Cloud Shell을 사용합니다. 이 연습을 선택적 작업으로 고려하고 원하는 경우 지침을 검토할 수 있습니다.

::: zone pivot="linux"

## <a name="linux"></a>Linux

Linux용 PowerShell을 설치하면 패키지 관리자를 사용하게 됩니다. 여기 예제에서는 **Ubuntu 18.04**를 사용하지만, [설명서에 다른 버전 및 배포에 대한 자세한 지침](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)이 나와 있습니다.

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

macOS에서 첫 번째 단계는 **PowerShell Core**를 설치하는 것입니다. Homebrew 패키지 관리자를 사용하여 수행합니다.

> [!IMPORTANT]
> **brew** 명령을 사용할 수 없는 경우 Homebrew 패키지 관리자를 설치해야 합니다. 자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.

1. PowerShell Core 패키지를 포함하여 추가 패키지를 얻으려면 Homebrew-Cask를 설치하세요.

    ```bash
    brew tap caskroom/cask
    ```

1. PowerShell Core 설치:

    ```bash
    brew cask install powershell
    ```

1. PowerShell Core를 시작하여 성공적으로 설치되었는지 확인합니다.

    ```bash
    pwsh
    ```

::: zone-end

::: zone pivot="windows"

## <a name="windows"></a>Windows
PowerShell은 Windows에 포함되지만 머신에 사용할 수 없는 업데이트가 있을 수 있습니다. 사용하려는 Azure 지원에는 PowerShell 버전 5.0 이상이 필요합니다. 다음 단계를 통해 설치된 버전을 확인할 수 있습니다.

1. **시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다. 여러 바로 가기 링크를 사용할 수 있습니다.
    - Windows PowerShell - 64비트 버전이며 일반적으로 선택해야 합니다.
    - Windows PowerShell(x86) - 64비트 Windows에 설치된 32비트 버전입니다.
    - Windows PowerShell ISE - ISE(통합 스크립팅 환경)는 PowerShell에서 스크립트를 작성하는 데 사용됩니다. 
    - Windows PowerShell ISE(x86) - 32비트 버전의 ISE입니다.

1. Windows PowerShell 아이콘을 선택합니다.

1. 다음 명령을 입력하여 설치된 PowerShell 버전을 확인합니다.

    ```powershell
    $PSVersionTable.PSVersion
    ```
    
버전 번호가 5.0 미만인 경우 [기존 Windows PowerShell을 업그레이드](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)하기 위한 이러한 지침을 따르세요.

::: zone-end

PowerShell을 지원하도록 로컬 머신을 설정해야 합니다. 다음으로, Azure 모듈을 포함하여 추가할 수 있는 추가 명령에 대해 다루겠습니다.