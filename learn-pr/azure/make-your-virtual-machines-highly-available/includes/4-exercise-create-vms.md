부하 분산 장치를 인바운드 인터넷 트래픽을 사용하여 라우팅하도록 했습니다. 이제 트래픽을 라우팅할 일부 Azure VM이 필요합니다. 이 예제에서는 Linux를 사용하지만 정확히 동일한 기술이 모든 가상 머신 이미지에서 작동합니다.

## <a name="create-a-set-of-vms"></a>VM 집합 만들기

Azure CLI를 사용하여 세 개의 VM을 만들고 가용성 그룹에 그룹화하겠습니다. 이 작업에서는 포털을 사용할 수 있지만 여러 리소스를 만드는 것이므로 스크립팅 도구를 통해 이 작업을 훨씬 쉽게 수행할 수 있습니다.

_실제로_ Azure Portal을 사용하려면 대안으로 _템플릿_을 사용해야 합니다. 리소스를 배포하는 데 사용할 수 있는 JSON 지침입니다. Azure Portal에서 가상 머신에 대한 템플릿을 정의한 다음, 여러 번 템플릿을 배포할 수 있습니다.

### <a name="create-some-azure-cli-defaults"></a>일부 Azure CLI 기본값 만들기

1. Azure CLI에서 일부 기본값을 설정하기 시작합니다. 사용할 모든 명령에는 _리소스 그룹_ 및 선택적 _위치_가 필요합니다. 매번 입력하지 않고, 기본 매개 변수로 설정할 수 있습니다. 미리 만들어진 Azure 샌드박스 리소스 그룹 및 Azure Load Balancer에 선택한 동일한 위치를 사용합니다. 참고로, 사용 가능한 위치는 다음과 같습니다.

    [!include[](../../../includes/azure-sandbox-regions-note.md)]

1. 이 명령을 오른쪽의 Cloud Shell에 입력하여 `<location>` 자리 표시자를 Azure Load Balancer에 사용한 위치로 바꿉니다.

    ```azurecli
    az configure --defaults group=<rgn>[sandbox Resource Group</rgn> location=<location>
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

### <a name="create-an-availability-set"></a>가용성 집합 만들기

_가용성 집합_을 만들어 시작해 보겠습니다.

가상 머신을 그룹화하는 데 가용성 집합이 필요합니다. `vm availability-set` 명령을 사용하여 가용성 집합을 만들 수 있습니다. 이름만 필요한 경우 **woodgrove-avail-set**을 사용합니다.

```azurecli
az vm availability-set create --name woodgrove-avail-set
```

### <a name="create-a-configuration-script"></a>구성 스크립트 만들기

각 VM에 대해 동일한 기본 구성을 사용하려고 합니다.

    - Ubuntu Linux
    - Nginx 웹 서버
    - Node.js
    - 테스트할 단일 페이지를 포함한 기본 웹 사이트

OS는 선택한 이미지를 기반으로 선택하지만 다른 구성 요소에는 일부 스크립팅이 필요합니다. Cloud Shell에 로컬 파일을 만들어 웹 서버를 설치하고 기본 사이트를 사용하여 구성하겠습니다.

1. 터미널에서 `code`를 입력하여 Cloud Shell 편집기를 엽니다.

    ```bash
    code
    ```

    이 편집기는 Cloud Shell 환경에서 직접 파일을 만들고 편집하는 데 사용할 수 있는 기본 제공 편집기입니다. 파일은 Cloud Shell 환경을 실행했을 때 만든 Azure Storage 계정에 저장됩니다.

1. 다음 스크립트를 복사하고 편집기 창에 붙여넣습니다.

    ```script
    #cloud-config
    package_upgrade: true
    packages:
      - nginx
      - nodejs
      - npm
    write_files:
      - owner: www-data:www-data
      - path: /etc/nginx/sites-available/default
        content: |
          server {
            listen 80;
            location / {
              proxy_pass http://localhost:3000;
              proxy_http_version 1.1;
              proxy_set_header Upgrade $http_upgrade;
              proxy_set_header Connection keep-alive;
              proxy_set_header Host $host;
              proxy_cache_bypass $http_upgrade;
            }
          }
      - owner: azureuser:azureuser
      - path: /home/azureuser/myapp/index.js
        content: |
          var express = require('express')
          var app = express()
          var os = require('os');
          app.get('/', function (req, res) {
            res.send('Hello World from host ' + os.hostname() + '!')
          })
          app.listen(3000, function () {
            console.log('Hello world app listening on port 3000!')
          })
    runcmd:
      - service nginx restart
      - cd "/home/azureuser/myapp"
      - npm init
      - npm install express -y
      - nodejs index.js
    ```

1. 파일을 저장하고 이름을 **cloud-init.txt**로 지정합니다. 편집기의 위쪽/오른쪽 모서리에서 "..." 상황에 맞는 메뉴를 사용하거나 Windows 및 Linux에서 <kbd>Ctrl+S</kbd>를 사용하고 macOS에서 <kbd>Cmd+S</kbd>를 사용할 수 있습니다.

1. 편집기를 종료합니다. 다시 "..." 상황에 맞는 메뉴 또는 바로 가기 키(<kbd>Ctrl+Q</kbd>)를 사용할 수 있습니다.

1. 파일이 파일 시스템에 있어야 합니다. `ls` 명령을 사용하여 폴더의 내용을 나열합니다. 파일을 `cat`하여 내용을 확인할 수도 있습니다.

### <a name="create-the-virtual-machines"></a>가상 머신 만들기

다음으로, Azure CLI를 사용하여 세 대의 Ubuntu Linux 가상 머신을 만들겠습니다. 여기에서는 이 옵션을 다루지 않지만 CLI를 사용한 VM 관리에 대해 자세히 알아보려면 **Azure CLI를 사용하여 가상 머신 관리** 모듈을 확인하세요.

각 VM에 대한 가상 네트워크 인터페이스도 만들어야 합니다. 루프를 사용하고 함께 만들 수 있습니다.

1. `vm-create` 명령을 사용하여 루프에서 세 대의 가상 머신을 만듭니다. 다음 코드를 사용하여 수행할 수 있습니다.
    - _woodgrove_NicX_(여기서 X는 [1,2,3])라는 NIC 만들기
    - _woodgrove-VMX_(여기서 X는 [1,2,3])라는 VM 만들기
    - 각 NIC를 만든 VNET에 연결
    - 각 VM을 NIC 및 가용성 집합에 연결

    ```azurecli
    for i in `seq 1 3`; do

        az network nic create --name woodgrove-Nic$i \
            --vnet-name woodgrove-VNET \
            --subnet backendSubnet

        az vm create --name woodgrove-VM$i \
            --availability-set woodgrove-avail-set \
            --nics woodgrove-Nic$i \
            --image UbuntuLTS \
            --admin-username azureuser \
            --generate-ssh-keys \
            --custom-data cloud-init.txt \
            --no-wait
    done
    ```
    > [!TIP]
    > 이 명령은 여기에서 관리자 이름을 "azureuser"로 설정하지만 원하는 값으로 변경할 수 있습니다. SSH 키보다 사용자 이름/암호를 선호하는 경우 암호를 입력할 수도 있습니다.

1. 이 작업을 실행하는 데 시간이 걸립니다. 루프가 완료되더라도 VM을 사용할 수 없게 됩니다. Azure Portal로 전환하고 **모든 리소스**를 사용하여 만든 리소스를 표시할 수 있습니다.

1. `vm list` 명령을 사용하여 배포된 VM 수를 확인할 수도 있습니다.

    ```azurecli
    az vm list -o table
    ```

다음으로, 부하 분산 장치를 구성하는 방법을 알아보겠습니다.