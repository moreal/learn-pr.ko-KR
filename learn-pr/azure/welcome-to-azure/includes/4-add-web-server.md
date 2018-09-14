이제 VM을 실행 했으므로 작업을 수행 하겠습니다. 여기는 웹 서버 설치 및 VM의 호스트 이름을 표시 하는 기본 웹 페이지를 제공 합니다.

VM을 구성 하는 몇 가지 옵션이 있습니다. 직접 연결 하 고 대화형으로 시스템을 구성할 수 있습니다. 예를 들어, Windows 시스템에서 있습니다 앉아 있는 것 처럼 원격 Windows 컴퓨터의 UI에 연결 하려면 원격 데스크톱 세션을 만들 수 있습니다. Linux 시스템에서 터미널에서 원격 Linux 시스템을 사용 하 여 안전 하 게 작업에 대 한 SSH 연결을 만들 수 있습니다.

수동 구성은 좋은 시작 되었지만 시스템에 추가 하면 배포를 자동화할 수 있습니다. 자동화는 프로그램 하기 어려운을 관리 하는 스크립트와 같은 반복 가능한 프로세스를 실행 하는 것입니다.

::: 영역 피벗 = "windows 클라우드"

여기에서 Windows 기반 Azure 가상 머신의 사용자 지정 스크립트 확장 이라는 기능을 사용 하 여 Cloud Shell 세션에서 원격 IIS을 구성할 수 있습니다.

::: zone-end

::: 영역 피벗 = "linux 클라우드"

여기에서 Linux 기반 Azure 가상 머신의 사용자 지정 스크립트 확장 이라는 기능을 사용 하 여 Cloud Shell 세션에서 원격으로 Nginx을 구성할 수 있습니다.

::: zone-end

::: 영역 피벗 = "windows 클라우드"

## <a name="what-is-iis"></a>IIS는 무엇입니까?

인터넷 정보 서비스 또는 IIS는 Windows에서 실행 되는 웹 서버입니다. 표준 웹 콘텐츠 (HTML, CSS 및 JavaScript)를 제공 하거나 ASP.NET 및 다른 종류의 웹 응용 프로그램을 실행 하려면 IIS를 사용할 수 있습니다. Windows Server를 사용 하 여 IIS에는 있지만 웹 페이지를 처리 하려면 활성화 해야 합니다.

## <a name="whats-the-custom-script-extension"></a>사용자 지정 스크립트 확장 이란?

사용자 지정 스크립트 확장은 쉽게 다운로드 하 고 Azure Vm에서 스크립트를 실행 합니다. 해당 VM이 실행 되 면 VM을 구성할 수 있습니다 여러 가지 방법 중 하나일 뿐입니다.

Azure storage 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다. 수동으로 또는 자동화 된 배포의 일부로 스크립트를 실행할 수 있습니다. 여기에서 GitHub에서 PowerShell 스크립트를 다운로드 하 여 VM에서 실행 하는 Azure CLI 명령을 실행 합니다. 스크립트는 IIS를 구성합니다.

## <a name="configure-iis"></a>IIS 구성

다음 Cloud Shell에서 VM에 원격으로 IIS를 구성 하는 사용자 지정 스크립트 확장을 사용 합니다. 또한 포트 80(http)에 대 한 인바운드 네트워크 액세스를 허용 하도록 방화벽을 구성 합니다.

1. Cloud Shell에서 실행이 `az vm extension set` 명령을 다운로드 하 고 IIS를 설치 하 고 기본 홈 페이지를 구성 하는 PowerShell 스크립트를 실행 합니다.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myWindowsVM \
      --name CustomScriptExtension \
      --publisher Microsoft.Compute \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1"]}' \
      --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
    ```

    프로세스를 완료 하려면 몇 분이 걸립니다.

    할 수 있습니다 하는 한편 [PowerShell 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true) 하려는 경우 별도 브라우저 탭에서. 스크립트에서 IIS를 설치 하 고 VM의 컴퓨터 이름 "myWindowsVM"와 함께 시작 메시지를 표시 하려면 홈 페이지를 구성 합니다.

1. 이 실행 `az vm open-port` 명령을 방화벽을 통한 포트 80만 (HTTP)를 엽니다.

    ```azurecli
    az vm open-port \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>구성 확인

IIS를 설정 했으므로 실행 중인지 확인 하겠습니다.

1. 이 실행 `az vm list-ip-addresses` 주소를 VM의 공용 IP를 나열 하는 명령입니다.

    ```azurecli
    az vm list-ip-addresses \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > 이 명령은 특히 매우 복잡 한 `--query` 인수입니다. 하지만의 커뮤니티가 살펴보고 Azure 전문가이 됩니다.

    VM의 공용 IP 주소가 표시 됩니다. 예를 들면 다음과 같습니다.

    ```console
    104.211.9.245
    ```

1. 새 브라우저 탭에서 VM의 IP 주소로 이동 합니다. 시작 메시지 및 VM의 이름이 표시 됩니다.

    ![](../media/iis-browser.png)

::: zone-end

::: 영역 피벗 = "linux 클라우드"

## <a name="what-is-nginx"></a>Nginx 란?

Nginx (발음된 "엔진-x")는 Unix, Linux, macOS 및 Windows에서 실행 되는 인기 있는, 무료, 오픈 소스 웹 서버입니다. 여기 Nginx 기본 웹 페이지를 처리 하는 데 사용 됩니다.

## <a name="whats-the-custom-script-extension"></a>사용자 지정 스크립트 확장 이란?

사용자 지정 스크립트 확장은 쉽게 다운로드 하 고 Azure Vm에서 스크립트를 실행 합니다. 해당 VM이 실행 되 면 VM을 구성할 수 있습니다 여러 가지 방법 중 하나일 뿐입니다.

Azure storage 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다. 수동으로 또는 자동화 된 배포의 일부로 스크립트를 실행할 수 있습니다. 여기에서 GitHub에서 Bash 스크립트를 다운로드 하 여 VM에서 실행 하는 Azure CLI 명령을 실행 합니다. 스크립트는 Nginx를 구성합니다.

## <a name="configure-nginx"></a>Nginx 구성

다음 Cloud Shell에서 VM에 Nginx를 원격으로 구성 하는 사용자 지정 스크립트 확장을 사용 합니다. 또한 포트 80(http)에 대 한 인바운드 네트워크 액세스를 허용 하도록 방화벽을 구성 합니다.

1. Cloud Shell에서 실행이 `az vm extension set` 명령을 다운로드 하 여 Nginx를 설치 하 고 기본 홈 페이지를 구성 하는 Bash 스크립트를 실행 합니다.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myLinuxVM \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh"]}' \
      --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```

    프로세스를 완료 하려면 몇 분이 걸립니다.

    할 수 있습니다 하는 한편 [Bash 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/20fca2517fa5913150abab66b51b0d88aa3077d8/configure-nginx.sh?azure-portal=true) 하려는 경우 별도 브라우저 탭에서. 스크립트는 Nginx를 설치 하 고 VM의 컴퓨터 이름 "myLinuxVM"와 함께 시작 메시지를 표시 하려면 홈 페이지를 구성 합니다.

1. 이 실행 `az vm open-port` 명령을 방화벽을 통한 포트 80만 (HTTP)를 엽니다.

    ```azurecli
    az vm open-port \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>구성 확인

Nginx를 설정 했으므로 실행 중인지 확인 하겠습니다.

1. 이 실행 `az vm list-ip-addresses` 주소를 VM의 공용 IP를 나열 하는 명령입니다.

    ```azurecli
    az vm list-ip-addresses \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > 이 명령은 특히 매우 복잡 한 `--query` 인수입니다. 하지만의 커뮤니티가 살펴보고 Azure 전문가이 됩니다.

    VM의 공용 IP 주소가 표시 됩니다. 예를 들면 다음과 같습니다.

    ```console
    137.135.110.210
    ```

1. 새 브라우저 탭에서 VM의 IP 주소로 이동 합니다. 시작 메시지 및 VM의 이름이 표시 됩니다.

    ![](../media/nginx-browser.png)

::: zone-end

## <a name="summary"></a>요약

VM 실행 되 고 이제 웹 페이지를 제공할 수 있지만 항목에 대 한 의미가 있습니다?

말하지만 모든 경험 기본 기능 및 클라우드에서, 크고 작은 기업에서 거의 모든 유용한 혁신 시작 풋프린트 유사한 설치 프로그램을 시작 합니다. 귀하의 아이디어 진화 함에 따라 사용자가 비즈니스에 긍정적인 영향을 줄 만들기를 시작 합니다.