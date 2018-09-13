로컬 머신에 Azure CLI를 설치한 후에 간단한 명령을 실행하여 설치를 확인합니다. Azure CLI 설치에 사용하는 방법은 컴퓨터의 운영 체제에 따라 다릅니다. 운영 체제에 맞는 단계를 선택하세요.

> [!NOTE]
> 이 연습에서는 Azure CLI 도구를 로컬로 설치하는 과정을 안내합니다. 모듈의 나머지 부분에서는 Microsoft Learn의 무료 구독 지원을 활용할 수 있도록 Azure Cloud Shell을 사용합니다. 이 연습을 선택적 작업으로 고려하고 원하는 경우 지침을 검토할 수 있습니다.

::: zone pivot="linux"

### <a name="linux"></a>Linux

여기서는 고급 패키징 도구(**apt**) 및 Bash 명령줄을 사용하여 **Ubuntu Linux**에 Azure CLI를 설치합니다.

> [!TIP]
> 아래에 나열된 명령은 Ubuntu 버전 18.04용입니다. Linux의 기타 버전 및 분산에는 다양한 지침이 있습니다. 다른 Linux 버전을 사용하는 경우 [공식 설명서](https://docs.microsoft.com/cli/azure/install-azure-cli)를 확인하세요.

1. Microsoft 리포지토리가 등록되도록 소스 목록을 수정하면 패키지 관리자가 Azure CLI 패키지를 찾을 수 있습니다.

    ```bash
    AZ_REPO=$(lsb_release -cs)
    echo "deb [arch=amd64] https://packages.microsoft.com/repos/azure-cli/ $AZ_REPO main" | \
    sudo tee /etc/apt/sources.list.d/azure-cli.list
    ```

1. Microsoft Ubuntu 리포지토리의 암호화 키를 가져옵니다. 이렇게 하면 설치한 Azure CLI 패키지가 Microsoft에서 오는 것인지를 패키지 관리자가 확인할 수 있습니다.

    ```bash
    curl https://packages.microsoft.com/keys/microsoft.asc | sudo apt-key add -
    ```

1. Azure CLI를 설치합니다.

    ```bash
    sudo apt-get install apt-transport-https
    sudo apt-get update && sudo apt-get install azure-cli
    ```

::: zone-end

::: zone pivot="macos"

### <a name="macos"></a>macOS

여기서는 Homebrew 패키지 관리자를 사용하여 macOS에 Azure CLI를 설치합니다.

> [!IMPORTANT]
> **brew** 명령을 사용할 수 없는 경우에는 Homebrew 패키지 관리자를 설치해야 할 수 있습니다. 자세한 내용은 [Homebrew 웹 사이트](https://brew.sh/)를 참조하세요.

1. 최신 Azure CLI 패키지를 가져올 수 있도록 brew 리포지토리를 업데이트합니다.

    ```bash
    brew update
    ```

1. Azure CLI를 설치합니다.

    ```bash
    brew install azure-cli
    ```

::: zone-end

::: zone pivot="windows"

### <a name="windows"></a>Windows

여기서는 MSI 설치 프로그램을 사용하여 Windows에 Azure CLI를 설치합니다.

1. [https://aka.ms/installazurecliwindows](https://aka.ms/installazurecliwindows)로 이동하여 브라우저 보안 대화 상자에서 **실행**을 클릭합니다.
1. 설치 프로그램에서 라이선스 이용 약관에 동의한 후에 **설치**를 클릭합니다.
1. **사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.

::: zone-end

## <a name="running-the-azure-cli"></a>Azure CLI 실행

bash 셸(Linux 및 macOS) 또는 명령 프롬프트나 PowerShell(Windows)을 열어 Azure CLI를 실행합니다.

1. Azure CLI를 시작하고 버전 검사를 실행하여 설치를 확인합니다.

    ```azurecli
    az --version
    ```

::: zone pivot="windows"

> [!TIP]
> PowerShell에서 Azure CLI를 실행하면 Windows 명령 프롬프트에서 Azure CLI를 실행할 때에 비해 몇 가지 장점이 있습니다. PowerShell은 명령 프롬프트에서 사용할 수 있는 탭 완성 기능 외에 일부 탭 완성 기능을 추가로 제공합니다. 

::: zone-end

## <a name="summary"></a>요약

Azure CLI를 사용하여 Azure 리소스를 관리하도록 로컬 머신을 설정합니다. 이제 로컬에서 Azure CLI를 사용하여 명령을 입력하거나 스크립트를 실행할 수 있습니다. Azure CLI가 Azure 데이터 센터로 명령을 전달하면 Azure 구독 내에서 명령이 실행됩니다.