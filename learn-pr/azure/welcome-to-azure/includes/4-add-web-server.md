이제 VM이 실행 중이므로 VM을 사용해 보겠습니다. 여기서는 웹 서버를 설치하고 VM의 호스트 이름을 표시하는 기본 웹 페이지를 운영하겠습니다.

VM을 구성하는 몇 가지 옵션이 있습니다. 직접 연결하고 대화형으로 시스템을 구성할 수 있습니다. 예를 들어 Windows 시스템에서 원격 데스크톱 세션을 만들어서 마치 Windows 머신에 앉아 있는 것처럼 원격 Windows 머신의 UI에 연결할 수 있습니다. Linux 시스템에서, SSH 연결을 만들어서 터미널에서 원격 Linux 시스템을 안전하게 사용할 수 있습니다.

수동 구성은 처음에는 좋지만, 이후에 시스템을 추가하면서 배포를 자동화할 수 있습니다. 힘든 작업을 알아서 처리하는 프로그램 및 스크립트처럼 반복 가능한 프로세스의 실행도 자동화의 범위에 포함됩니다.

::: zone pivot="windows-cloud"

여기서는 사용자 지정 스크립트 확장이라고 하는 Windows 기반 Azure 가상 머신의 기능을 사용하여 Cloud Shell 세션에서 원격으로 IIS를 구성하겠습니다.

::: zone-end

::: zone pivot="linux-cloud"

여기서는 사용자 지정 스크립트 확장이라고 하는 Linux 기반 Azure 가상 머신의 기능을 사용하여 Cloud Shell 세션에서 원격으로 Nginx를 구성하겠습니다.

::: zone-end

::: zone pivot="windows-cloud"

## <a name="what-is-iis"></a>IIS란?

IIS(인터넷 정보 서비스)는 Windows에서 실행되는 웹 서버입니다. IIS를 사용하여 표준 웹 콘텐츠(HTML, CSS 및 JavaScript)를 제공하거나 ASP.NET 및 다른 종류의 웹 응용 프로그램을 실행할 수 있습니다. IIS는 Windows Server가 함께 제공되지만 웹 페이지 서비스를 시작하려면 먼저 활성화해야 합니다.

## <a name="whats-the-custom-script-extension"></a>사용자 지정 스크립트 확장이란?

사용자 지정 스크립트 확장은 Azure VM에서 간편하게 스크립트를 다운로드하고 실행할 수 있는 방법입니다. VM이 실행 중이면 시스템을 구성할 수 있는 여러 방법 중 하나일 뿐입니다.

Azure 저장소 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다. 스크립트를 수동으로 실행할 수도 있고 자동화된 배포의 일부로 실행할 수도 있습니다. 여기서는 GitHub에서 PowerShell 스크립트를 다운로드하여 VM에서 실행하는 Azure CLI 명령을 실행하겠습니다. 이 스크립트는 IIS를 구성합니다.

## <a name="configure-iis"></a>IIS 구성

<!-- TODO: https://github.com/MicrosoftDocs/learn-pr/issues/1864 -->

여기서는 사용자 지정 스크립트 확장을 사용하여 Cloud Shell을 통해 원격으로 VM에서 IIS를 구성하겠습니다. 또한 포트 80(HTTP)에 대한 인바운드 네트워크 액세스를 허용하도록 방화벽을 구성하겠습니다.

1. Cloud Shell에서 이 `az vm extension set` 명령을 실행하여 IIS를 설치하고 기본 홈페이지를 구성하는 PowerShell 스크립트를 다운로드하고 실행합니다.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myVM \
      --name CustomScriptExtension \
      --publisher Microsoft.Compute \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1"]}' \
      --protected-settings '{"commandToExecute": "powershell -ExecutionPolicy Unrestricted -File configure-iis.ps1"}'
    ```

    Nginx를 구성하고, 홈페이지의 내용을 설정하고, 서비스를 시작하는 프로세스를 완료하려면 몇 분이 걸립니다.

    그 사이에 원한다면 별도의 브라우저 탭에서 [PowerShell 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-iis.ps1?azure-portal=true)할 수 있습니다. 이 스크립트는 IIS를 설치하고, VM의 컴퓨터 이름인 "myVM"과 함께 시작 메시지를 표시하도록 홈페이지를 구성합니다.

1. 이 `az vm open-port` 명령을 실행하여 방화벽을 통해 포트 80(HTTP)을 엽니다.

    ```azurecli
    az vm open-port \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>구성 확인

IIS를 설정했으니, 실행 중인지 확인하겠습니다.

1. VM의 공용 IP 주소를 나열하는 이 `az vm list-ip-addresses` 명령을 실행합니다.

    ```azurecli
    az vm list-ip-addresses \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > 이 `--query` 인수를 사용하면 이 명령이 조금 복잡해집니다. 하지만 여러분은 Azure를 열심히 공부하고 있으니 이 명령의 전문가가 될 것입니다.

    VM의 공용 IP 주소가 보입니다. 예를 들면 다음과 같습니다.

    ```output
    104.211.9.245
    ```

1. 새 브라우저 탭에서 VM의 IP 주소로 이동합니다. 시작 메시지와 VM 이름이 표시됩니다.

    ![](../media/4-iis-browser.png)

::: zone-end

::: zone pivot="linux-cloud"

## <a name="what-is-nginx"></a>Nginx란?

Nginx(발음은 "엔진-엑스")는 인기 있는 무료 오픈 소스 웹 서버로 Unix, Linux, macOS 및 Windows에서 실행됩니다. 여기서는 Nginx를 사용하여 기본 웹 페이지를 작동하겠습니다.

## <a name="whats-the-custom-script-extension"></a>사용자 지정 스크립트 확장이란?

사용자 지정 스크립트 확장은 Azure VM에서 간편하게 스크립트를 다운로드하고 실행할 수 있는 방법입니다. VM이 실행 중이면 시스템을 구성할 수 있는 여러 방법 중 하나일 뿐입니다.

Azure 저장소 또는 GitHub와 같은 공용 위치에 스크립트를 저장할 수 있습니다. 스크립트를 수동으로 실행할 수도 있고 자동화된 배포의 일부로 실행할 수도 있습니다. 여기서는 GitHub에서 Bash 스크립트를 다운로드하여 VM에서 실행하는 Azure CLI 명령을 실행하겠습니다. 이 스크립트는 Nginx를 구성합니다.

## <a name="configure-nginx"></a>Nginx 구성

<!-- TODO: https://github.com/MicrosoftDocs/learn-pr/issues/1864 -->

여기서는 사용자 지정 스크립트 확장을 사용하여 Cloud Shell을 통해 원격으로 VM에서 Nginx를 구성하겠습니다. 또한 포트 80(HTTP)에 대한 인바운드 네트워크 액세스를 허용하도록 방화벽을 구성하겠습니다.

1. Cloud Shell에서 이 `az vm extension set` 명령을 실행하여 Nginx를 설치하고 기본 홈페이지를 구성하는 Bash 스크립트를 다운로드하고 실행합니다.

    ```azurecli
    az vm extension set \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --vm-name myVM \
      --name customScript \
      --publisher Microsoft.Azure.Extensions \
      --settings '{"fileUris":["https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-nginx.sh"]}' \
      --protected-settings '{"commandToExecute": "./configure-nginx.sh"}'
    ```

    IIS를 구성하고, 홈페이지의 내용을 설정하고, 서비스를 시작하는 프로세스를 완료하려면 몇 분이 걸립니다.

    그 사이에 원한다면 별도의 브라우저 탭에서 [Bash 스크립트를 검사](https://gist.githubusercontent.com/tpetchel/26f9dab2628a80bf87a33caeed1b6ded/raw/69e5d9250b9dcd7e7eece4b0ea3c3a8cd1b4fcd7/configure-nginx.sh?azure-portal=true)할 수 있습니다. 이 스크립트는 Nginx를 설치하고, VM의 컴퓨터 이름인 "myVM"과 함께 시작 메시지를 표시하도록 홈페이지를 구성합니다.

1. 이 `az vm open-port` 명령을 실행하여 방화벽을 통해 포트 80(HTTP)을 엽니다.

    ```azurecli
    az vm open-port \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --port 80
    ```

## <a name="verify-the-configuration"></a>구성 확인

Nginx를 설정했으니, 실행 중인지 확인하겠습니다.

1. VM의 공용 IP 주소를 나열하는 이 `az vm list-ip-addresses` 명령을 실행합니다.

    ```azurecli
    az vm list-ip-addresses \
      --name myVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --query "[].virtualMachine.network.publicIpAddresses[0].ipAddress" \
      --output tsv
    ```

    > [!NOTE]
    > 이 `--query` 인수를 사용하면 이 명령이 조금 복잡해집니다. 하지만 여러분은 Azure를 열심히 공부하고 있으니 이 명령의 전문가가 될 것입니다.

    VM의 공용 IP 주소가 보입니다. 예를 들면 다음과 같습니다.

    ```output
    137.135.110.210
    ```

1. 새 브라우저 탭에서 VM의 IP 주소로 이동합니다. 시작 메시지와 VM 이름이 표시됩니다.

    ![](../media/4-nginx-browser.png)

::: zone-end

## <a name="summary"></a>요약

이제 VM이 실행 중이고 웹 페이지를 제공할 수 있는데, 이것이 여러분에게는 어떤 의미일까요?

모든 변화는 기본에서 시작하며, 클라우드에서 이루어진 크고 작은 기업의 위대한 혁신은 거의 대부분 여러분과 비슷한 설정에서 시작되었습니다. 여러분의 아이디어가 발전할수록 비즈니스와 사용자에게 긍정적인 영향을 미치기 시작합니다.