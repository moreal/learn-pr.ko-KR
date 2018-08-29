이 연습에서는 로컬 머신에 **Azure PowerShell**을 설치합니다. 운영 체제에 적합한 섹션을 선택하세요.

## <a name="linux-and-mac"></a>Linux 및 Mac
Linux 및 macOS에서의 첫 번째 단계는 **PowerShell Core**를 설치하는 것입니다.

### <a name="linux"></a>Linux
마지막 단원에서 언급한 것처럼 Linux용 PowerShell을 설치하면 패키지 관리자를 사용하게 됩니다. 여기에 나온 예에서는 **Ubuntu 18.04**를 사용하지만, [설명서에 다른 버전 및 배포에 대한 자세한 지침](https://docs.microsoft.com/powershell/scripting/setup/installing-powershell-core-on-linux)이 나와 있습니다.

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

### <a name="macos"></a>macOS
이번에는 Homebrew 패키지 관리자를 사용하여 macOS에 **PowerShell Core**를 설치합니다.

> [!IMPORTANT]
> **brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다. 자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.

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

## <a name="install-azure-powershell"></a>Azure Powershell 설치
기본 **PowerShell** 제품을 설치한 후에는 **Azure PowerShell**을 설치하여 Azure 관련 명령을 추가합니다.

### <a name="windows"></a>Windows
`Install-Module` PowerShell 명령을 사용하여 Windows에 Azure PowerShell을 설치합니다.

> [!IMPORTANT]
> Azure PowerShell을 설치하려면 PowerShell 버전 5.0 이상이 있어야 합니다. PowerShell 버전을 확인하려면 다음 명령을 사용하세요. 
>
> `$PSVersionTable.PSVersion` 
>
>버전 번호가 5.0 미만인 경우 [기존 Windows PowerShell 업그레이드](https://docs.microsoft.com/powershell/scripting/setup/installing-windows-powershell?view=powershell-6#upgrading-existing-windows-powershell)에 대한 지침을 따르세요.

1. **시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다.
2. **Windows PowerShell** 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.
3. **사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.
4. 다음 명령을 입력하고 Enter 키를 누릅니다.

    ```powershell
    Install-Module -Name AzureRM
    ```
5. PSGallery의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.

> [!NOTE]
> Azure Powershell 모듈 버전이 이미 설치되어 있음을 나타내는 오류 메시지가 표시되면 다음 명령을 실행하여 _최신_ 버전으로 업데이트할 수 있습니다.
> 
> `Update-Module -Name AzureRM`
> 
> `Install-Module` 명령과 마찬가지로, 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.

### <a name="linux-or-macos"></a>Linux 또는 macOS
동일한 기본 프로세스를 사용하여 Linux 또는 macOS에 Azure PowerShell을 설치합니다. 이 절차는 두 운영 체제에서 모두 동일합니다. 차이점은 승격된 PowerShell Core 세션을 가져오는 것입니다.

1. 터미널에서 승격된 권한으로 PowerShell Core를 시작하려면 다음 명령을 입력합니다.

    ```bash
    sudo pwsh
    ```

1. Azure PowerShell을 설치하려면 PowerShell Core 프롬프트에서 다음 명령을 실행합니다.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. **PSGallery**의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.

## <a name="summary"></a>요약
Azure PowerShell을 사용하여 Azure 리소스를 관리할 로컬 머신을 설정합니다. 이제 Azure PowerShell을 로컬에서 사용하여 명령을 입력하거나 스크립트를 실행할 수 있습니다. Azure PowerShell이 Azure 데이터 센터로 명령을 전달하면 Azure 구독 내에서 명령이 실행됩니다.