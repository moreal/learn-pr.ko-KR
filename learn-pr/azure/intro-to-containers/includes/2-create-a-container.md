컨테이너를 실행, 나열 및 삭제하는 일반적인 방법 중 일부를 설명하기 전에 Ubuntu VM(가상 머신)에 호스팅되는 Docker 컨테이너에서 실행 중인 기본 Nginx 구성을 살펴보겠습니다.

여기에서는 다음 방법을 학습합니다.

1. VM이 처음 부팅될 때 Docker를 설치하도록 구성된 Linux VM을 만듭니다.
1. VM에 연결하고 Nginx를 실행하는 Docker 컨테이너를 시작합니다.
1. 포트 바인딩을 사용하여 웹 서버가 VM 외부에서 액세스할 수 있게 합니다.

## <a name="what-are-containers"></a>컨테이너란?

컨테이너는 가상화 환경이지만, 가상 머신과는 달리 항상 전체 운영 체제를 포함하지는 않습니다. 대신, 해당 컨테이너를 실행하는 호스팅 환경의 운영 체제를 참조합니다. 예를 들어 특정 Linux 커널이 있는 서버에서 컨테이너 5개를 실행하는 경우 컨테이너 5개가 모두 동일한 커널에서 실행됩니다.

컨테이너를 사용하면 응용 프로그램 및 _컨테이너 이미지_로 알려진 것에서 실행하는 데 필요한 모든 것을 패키징할 수 있습니다. 컨테이너는 격리되어 있습니다. 이는 동일한 시스템에서 실행 중인 다른 모든 컨테이너를 방해하지 않는다는 의미입니다. 컨테이너 이미지는 이식 가능합니다. Docker Hub 또는 Azure Container Registry와 같은 컨테이너 레지스트리에 이미지를 업로드할 수 있습니다. 그런 다음, 클라우드에서 컨테이너를 실행하고 개발 환경에서와 마찬가지로 정확히 동일한 방식으로 컨테이너가 동작하기를 기대할 수 있습니다.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yMhY]

컨테이너는 신속한 반복을 사용합니다. 컨테이너는 운영 체제를 포함할 필요가 없으므로 일반적으로 전체 VM보다 크기가 훨씬 작습니다. 이 컨테이너를 사용하면 몇 초 안에 신속하게 컨테이너를 시작 및 중지할 수 있습니다.

## <a name="understand-the-setup"></a>설정 이해

학습 목적에서 작업할 샌드박스 환경을 제공합니다. 이 환경에는 Azure 리소스를 관리하고 개발하기 위한 브라우저 기반 명령줄 환경인 Azure Cloud Shell이 포함됩니다.

Cloud Shell에서 Docker를 포함하는 Linux VM을 만듭니다. Docker 컨테이너를 대화형으로 만들고 사용할 수 있도록 SSH를 통해 Linux VM에 연결됩니다.

컨테이너에 대해 알아보려면 이 Linux VM을 개발 환경 및 공간으로 생각하세요. 실제로 앱 개발에 사용되는 컴퓨터에 Docker를 설치합니다. Docker는 Windows, macOS 및 Linux에서 실행됩니다.

이 모듈의 끝에 로컬 개발 환경에서 Docker를 실행하는 방법을 자세히 알아볼 수 있는 리소스를 제공합니다.

## <a name="what-is-nginx"></a>Nginx란?

Nginx("엔진-엑스"로 발음)는 인기 있는 무료 오픈 소스 웹 서버로 Unix, Linux, macOS 및 Windows에서 실행됩니다. 웹 서버 구성은 동작 중인 컨테이너를 확인하는 좋은 방법입니다. 여기서는 Nginx를 사용하여 기본 웹 페이지를 작동하겠습니다.

## <a name="what-is-cloud-init"></a>cloud-init란?

Cloud-init를 사용하면 처음 부팅 시 Linux VM을 사용자 지정할 수 있습니다. Cloud-init를 사용하여 패키지를 설치하고 파일을 쓰거나, 사용자 및 보안을 구성할 수 있습니다. 여기에서는 cloud-init 스크립트를 사용하여 VM에 Docker를 설치합니다.

## <a name="what-is-port-binding"></a>포트 바인딩이란?

포트 바인딩을 사용하면 해당 호스트에서 컨테이너로 네트워크 트래픽을 전송할 수 있습니다.

Docker 컨테이너는 컨테이너의 호스트 시스템의 로컬 네트워크에서 실행됩니다. 이 경우 컨테이너의 네트워크는 Linux VM에 있습니다.

알다시피 웹 요청은 일반적으로 포트 80(HTTP)을 통해 실행됩니다. 컨테이너는 VM 내의 로컬 네트워크에서 실행되므로 컨테이너는 외부 환경에 액세스할 수 없습니다.

Docker를 사용하면 VM 외부에서 액세스할 수 있게 하는 포트를 게시하거나 노출할 수 있습니다. 여기에서는 VM의 포트 8080으로 전달되는 네트워크 트래픽을 컨테이너의 포트 80으로 전달할 수 있도록 컨테이너를 구성하겠습니다.

## <a name="create-a-virtual-machine-to-host-docker"></a>Docker를 호스트하기 위한 가상 머신 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="create-the-cloud-init-script"></a>cloud-init 스크립트 만들기

1. **clouddrive** 폴더로 이동합니다.

    ```azurecli
    cd clouddrive
    ```

1. **vm-config**라는 새 폴더를 만듭니다.

    ```azurecli
    mkdir vm-config
    ```

1. 새 폴더로 이동합니다.

    ```azurecli
    cd vm-config
    ```

1. Cloud Shell의 통합 편집기를 사용하여 새 파일을 만듭니다.

    ```azurecli
    code .
    ```

1. 이 cloud-init 스크립트를 편집기에 붙여 넣습니다.

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```yaml
    #cloud-config
    package_upgrade: true
    write_files:
      - path: /etc/systemd/system/docker.service.d/docker.conf
        content: |
          [Service]
          ExecStart=
          ExecStart=/usr/bin/dockerd
      - path: /etc/docker/daemon.json
        content: |
          {
            "hosts": ["fd://","tcp://127.0.0.1:2375"]
          }
    runcmd:
      - curl -sSL https://get.docker.com/ | sh
      - usermod -aG docker azureuser
    ```

1. 파일을 **docker-vm-config.txt**(<kbd>Ctrl+S</kbd> 또는 **저장**을 마우스 오른쪽 단추로 클릭하고 선택)로 저장합니다.

1. 편집기를 닫습니다(<kbd>Ctrl+Q</kbd> 또는 **끝내기**를 마우스 오른쪽 단추로 클릭하고 선택).

### <a name="create-the-vm"></a>VM 만들기

> [!IMPORTANT]
> 일반적으로 `az group create` 명령과 관련된 모든 Azure 리소스에 대한 리소스 그룹을 만들지만 이 실습에서는 하나의 리소스만 생성했습니다. 모든 단계의 리소스 그룹으로 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.

1. `az vm create` 명령을 실행하여 Linux VM을 만듭니다.

    ```azurecli
    az vm create \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --image UbuntuLTS \
      --admin-username azureuser \
      --generate-ssh-keys \
      --custom-data docker-vm-config.txt
    ```

`--custom-data` 인수는 VM이 처음 부팅될 때 Docker를 설치하는 cloud-init 스크립트를 지정합니다. 프로세스를 완료하는 데 몇 분 정도 걸립니다.

## <a name="connect-to-the-vm"></a>VM에 연결

여기에서는 연결을 구성할 수 있도록 VM에 대한 SSH 연결을 만듭니다.

1. 이 `az vm show` 명령을 실행하여 VM의 IP 주소를 가져옵니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. VM에 SSH 연결합니다. **ip-address**를 사용자의 IP 주소로 바꿉니다.

    ```bash
    ssh azureuser@ip-address
    ```

1. Docker 버전을 확인합니다.

    ```bash
    docker version
    ```

    > [!NOTE]
    > 명령이 실패하거나 Docker 디먼 소켓에 연결하는 방법에 대한 오류 메시지가 표시되는 경우는 cloud-init 스크립트 아직 완료되지 않았다는 뜻입니다. 스크립트 완료를 대기하는 몇몇 방법이 있기는 하지만 현재로서는 `exit`를 실행하여 SSH 세션을 종료하고 1~2분 뒤 다시 연결을 시도합니다.

## <a name="start-nginx"></a>Nginx 시작

여기에서는 Nginx를 실행하는 Docker 컨테이너를 시작합니다.

1. 이 `docker run` 명령을 실행하여 Nginx를 실행하는 Docker 컨테이너를 시작합니다.

    ```bash
    docker run -d -p 8080:80 --name nginx nginx
    ```

    이 명령은 [Docker 허브](https://hub.docker.com/_/nginx?azure-portal=true)에서 Nginx로 미리 구성된 Docker 이미지를 다운로드합니다.

    `--name` 인수는 나중에 작업할 수 있도록 Docker 컨테이너에 "nginx"라는 이름을 할당합니다.

    `-p` 인수는 VM의 포트 8080으로 전달되는 네트워크 트래픽을 컨테이너의 포트 80으로 전달합니다.

1. `curl`을 실행하여 Nginx가 실행 중이며 액세스할 수 있는지 확인합니다.

    ```bash
    curl http://localhost:8080
    ```

1. SSH 세션을 종료합니다.

    ```bash
    exit
    ```

## <a name="access-your-web-server-from-a-web-browser"></a>웹 브라우저에서 웹 서버에 액세스

앞서 언급한 것처럼 포트 8080으로 전달되는 네트워크 트래픽이 컨테이너의 포트 80으로 전달될 수 있도록 컨테이너를 구성했습니다.

동작 중인 포트 매핑을 확인하려면 여기서는 Azure 방화벽을 통해 VM의 포트 8080을 엽니다. 그러면 브라우저에서 웹 서버에 액세스됩니다.

1. 이 `az vm open-port` 명령을 실행하여 방화벽을 통해 VM에서 포트 8080을 엽니다.

    ```azurecli
    az vm open-port \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --port 8080 \
      --priority 1001
    ```

1. 웹 브라우저에서 VM의 IP 주소로 이동합니다. 포트 8080, 예를 들어 **http://40.121.106.164:8080**을 포함해야 합니다.

    기본 홈 페이지가 표시됩니다.

    ![브라우저에서 실행 중인 웹 사이트](../media/2-nginx-browser.png)

## <a name="stop-the-container"></a>컨테이너 중지

이제 컨테이너를 중지하겠습니다.

1. 먼저 VM에 다시 로그인합니다. 배운 내용을 떠올려 보겠습니다.

    IP 주소를 가져옵니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

    VM에 SSH 연결합니다. **ip-address**를 사용자의 IP 주소로 바꿉니다.

    ```bash
    ssh azureuser@ip-address
    ```

1. `docker stop nginx`을 실행하여 "nginx"라는 컨테이너를 중지합니다.

    ```bash
    docker stop nginx
    ```

다음을 위해 SSH 연결을 열어 둡니다.

축하합니다! 성공적으로 가상 머신을 만들어 Nginx 컨테이너화된 웹 서버를 호스팅하는 데 사용했습니다.
