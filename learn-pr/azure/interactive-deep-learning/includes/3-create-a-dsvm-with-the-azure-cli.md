회사의 소프트웨어 개발자로서 기술을 성장시키고 사내 AI 팀의 일원이 될 수 있는 기회를 얻었습니다. 흥미로운 새 역할을 강화하는 동안 매일 해야 할 일도 계속 해야 합니다. 팀 내 선임 AI 엔지니어가 이미지 분류 모델을 학습할 수 있는 PyTorch 기반 랩이 있는 유용한 Jupyter notebooks에 대해 얘기했습니다. 흥미로운 도구이지만 개발 장비에 프레임워크 집합을 설치하고 싶지 않습니다. 대신, DSVM(Data Science Virtual Machine) 이미지를 기반으로 가상 머신을 만들기로 합니다. 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a>Azure CLI란?

Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다. **CLI를 사용하여 Azure 서비스 제어** 모듈에서 이 도구의 사용에 대한 전체 내용을 다룹니다.

## <a name="managing-deployments"></a>배포 관리

Azure CLI에는 Azure Resource Manager 배포를 관리하는 `az group deployment` 명령이 포함되어 있습니다. 특정 작업을 수행하는 여러 하위 명령을 제공할 수 있습니다. 가장 일반적인 하위 명령은 다음과 같습니다.

| 하위 명령 | 설명 |
|-------------|-------------|
| `create` | 배포를 시작합니다. |
| `list` | 리소스 그룹의 모든 배포를 가져옵니다. |
| `export` | 배포에 사용된 템플릿을 내보냅니다. |

사용 가능한 배포 명령의 전체 목록은 [az group deployment 명령 참조](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)를 참조하세요.

`az group deployment create`를 사용하여 가상 머신을 프로비전합니다.

## <a name="create-a-json-deployment-parameters-file"></a>JSON 배포 매개 변수 파일 만들기

Azure Resource Manager 템플릿을 사용하여 VM을 만듭니다. 템플릿은 프로비전하려는 Linux DSVM 이미지를 정의합니다. 사용할 VM 크기, 관리자 이름 및 암호, 머신의 호스트 이름 등의 템플릿에 일부 매개 변수를 제공해야 합니다. 

1. 이 단원 오른쪽의 Azure Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다.

    ```bash
    code parameter_file.json
    ```
    <!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> 이 명령이 열리고 `parameter_file.json`이라는 빈 파일이 기본 제공 편집기에서 열립니다. 

1. 다음 JSON 코드 조각을 코드 편집기의 빈 파일에 붙여넣습니다.

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. 편집기에 붙여넣은 JSON에서 다음 매개 변수를 업데이트합니다.

    |매개 변수  |현재 값  |사용자 값  |
    |---------|---------|---------|
    |adminUsername     |  `<USERNAME>`       |    이 새 머신의 관리자 이름을 *azuser*와 같이 선택합니다.     |
    |adminPassword     |  `<PASSWORD>`       |   이 관리자 계정의 암호를 선택합니다. 암호 요구 사항에 대한 자세한 내용은 [Linux Virtual Machines에 대한 질문과 대답](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)을 참조하세요.     |
    |vmName     |   `<HOSTNAME>`      |  새 가상 머신의 이름을 선택합니다. 사용자의 이름은 문자로 시작하고 소문자 및 숫자만 포함해야 합니다. 사용자의 이니셜 및 출생 연도 등을 포함한 고유한 이름을 선택하세요. |
    |vmSize     |  Standard_DS2_v2       |  이 연습에서는 이 VM 크기가 정상적으로 작동하지만 자유롭게 변경할 수 있습니다. 사용 가능한 VM 크기 목록은 [Azure에서 Linux 가상 머신에 대한 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)에서 찾을 수 있습니다.       |

1. 변경 내용을 `parameter_file.json`에 저장하고 텍스트 편집기를 닫습니다.

    > [!IMPORTANT]
    > adminUsername, adminPassword 및 vmName에 대해 선택한 값을 기억해 둡니다. 이 연습에서 해당 값을 다시 사용합니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기 

> [!IMPORTANT]
> 일반적으로 선택한 지역에서 리소스 그룹을 만듭니다. 그러나 현재 작업 중인 샌드박스 세션에서는 사용할 리소스 그룹을 제공합니다. 이 세션의 리소스 그룹은 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 입니다.

## <a name="deploy-the-dsvm-to-your-resource-group"></a>리소스 그룹에 DSVM 배포

이제 리소스 그룹이 있으며 `parameter_file.json`이라는 파일에 DSVM Resource Manager 템플릿에 대한 매개 변수를 정의했습니다. 다음으로 `az group deployment create`를 실행하여 가상 머신을 프로비전합니다.

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[Sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    이 명령은 리소스 그룹에 Resource Manager 템플릿 및 매개 변수를 사용하여 가상 머신을 만듭니다. 

2. 가상 머신을 완료하는 데는 몇 분 정도 걸립니다. 작업이 완료될 때까지 콘솔에 ` - Running ..` 메시지가 표시됩니다. 작업이 끝나면 JSON 응답을 화면에 출력됩니다. JSON의 아래쪽으로 스크롤하여 **"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다.

    > [!TIP]
    > 다른 공용 IP에서 DNS 레코드를 이미 사용하고 있다는 오류가 표시되면 `parameter_file.json`에서 **vmName**을 고유한 다른 이름으로 변경해 보세요.

3. 다음 명령을 실행하여 `<HOSTNAME>`을 VM에 대해 정의된 호스트 이름으로 바꾸고 해당 VM에 대한 정보를 가져옵니다.

    ```azurecli
    az vm get-instance-view \
    --name <HOSTNAME> \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query instanceView.statuses[1] \
    --output table
    ```

    이 명령은 VM의 상태를 표시합니다. *VM 실행 중*이라고 표시됩니다.

축하합니다! DSVM 이미지에 기반한 Linux VM을 만들고 배포했습니다.

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a>포트 22에서 ssh 트래픽에 대해 VM 열기

기본적으로 VM은 어떠한 포트도 열려 있지 않습니다. 목표는 Jupyter Notebook 서버에 원격으로 연결하여 시작하고 머신에서 다른 로컬 명령을 실행하는 것입니다. SSH(Secure Shell) 프로토콜을 사용하여 VM에 원격으로 연결하려면 포트를 열어야 합니다. ssh의 기본 포트는 포트 22입니다.  

1. Azure Cloud Shell에서 다음 명령을 실행하여 `<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다. 

    ```azurecli
    az vm open-port \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

이 명령을 완료하는 데 1분 정도 걸릴 수 있습니다. 명령이 완료되면 명령줄에 JSON 응답이 반환됩니다. **"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다. ssh가 작동하는지 간단히 테스트하기 전에 먼저 포트를 하나 더 열겠습니다.

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a>VM을 열어 Jupyter Notebook 서버에 원격으로 액세스

이전에 설명한 대로 DSVM 이미지는 소프트웨어, 도구와 더불어 데이터 과학, 기계 학습 및 딥 러닝 프로젝트를 지원하기 위한 샘플이 미리 설치된 상태로 제공됩니다. Jupyter는 샘플 Notebook과 함께 이미지에 설치됩니다. VM에서 Jupyter Notebook 서버를 시작한 다음, 로컬 머신에서 Notebook 서버에 원격으로 연결할 수 있습니다. 기본적으로 Notebook 서버는 포트 8888에서 실행됩니다. 서버에 원격으로 액세스하려면 VM에서 해당 포트를 열어야 합니다. 

1. Azure Cloud Shell에서 다음 명령을 실행하여 `<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다.

    ```azurecli
    az vm open-port \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

다시 말하지만, 이 명령을 완료하는 데 1분 정도 걸릴 수 있습니다. 명령이 완료되면 명령줄에 JSON 응답이 반환됩니다. **"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다.  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a>ssh(Secure Shell)로 VM에 연결

1. Azure Cloud Shell에서 다음 명령을 실행하여 VM의 공용 IP 주소를 찾습니다. `<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다.

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[Sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다. `<USERNAME>`을 이 연습 시작 시 선택한 사용자 이름으로 바꿉니다. `<IP>`를 이전 단계의 **PublicIPAddresses** 열의 값으로 바꿉니다.

    예를 들어, 선택한 사용자 이름이 *azuser*이고 PublicIPAddresses의 값이 33.165.103.23인 경우 이 명령은 다음과 같이 읽습니다.
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. 메시지가 표시되면 이 연습 시작 시 선택한 관리자 암호를 입력합니다. 성공적으로 로그인한 경우 프롬프트가 `username@hostname` 형식으로 변경됩니다(예: `azuser@js1982`).

다음 단계는 VM에서 Jupyter Notebook 서버를 시작하고 원격으로 Notebook을 여는 것입니다.

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a>VM에서 Jupyter Notebook 서버 시작

VM의 `~/notebooks` 폴더에 일련의 Notebook이 있습니다. SSH 세션을 통해 여전히 로그인되어 있다고 가정하고 Notebook 서버를 시작한 후 이러한 Notebook 중 하나를 열고 모두 작동하는지 확인합니다.


1. VM의 명령 프롬프트에서 다음 명령을 실행합니다.

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> 이 연습에서 Notebook 서버에 대한 액세스는 `http://`를 통해 수행됩니다. 공개된 장소에서 Notebook 서버를 실행하려는 경우는 해당 서버를 보호해야 합니다. Notebook 서버를 보호하는 방법에 대한 자세한 내용은 공식 온라인 Jupyter 설명서를 참조하세요. 

이전 명령에서는 `jupyter notebook` 명령을 사용하여 Jupyter Notebook 서버를 시작합니다. 세 개의 중요한 명령줄 인수가 제공됩니다. 콘솔을 통해 원격으로 이 머신에 로그인했음을 기억하십시오. Notebook은 브라우저에서 제공됩니다. 

 - `--ip=0.0.0.0` 기본적으로 Notebook 서버는 127.0.0.1:8888에서 로컬로 실행되고 localhost에서만 액세스할 수 있습니다. http://127.0.0.1:8888을 사용하여 로컬로 브라우저에서 Notebook 서버에 액세스할 수 있습니다. IP 주소를 0.0.0.0으로 설정하면 서버가 모든 IP 주소에서 트래픽을 수신합니다. Notebook 서버가 0.0.0.0에서 수신 대기를 하는 경우 호스트 머신의 IP 주소를 통해 연결할 수 있습니다.  
 - `--no-browser`  다른 컴퓨터에서 인터넷을 통해 Notebook에 연결하려고 하는 것이므로 Notebook 서버가 브라우저를 열지 않도록 구성합니다(브라우저를 여는 것이 기본 동작입니다). 
 - `--allow-root`  이 연습은 VM에서 관리자 계정만 사용하므로 Notebook이 루트로 실행되도록 하려고 합니다.

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>원격 브라우저에서 Jupyter Notebook 서버에 연결

위의 명령을 VM에서 실행하면 Notebook 서버가 시작되고 브라우저에서 사용할 수 있는 URL이 콘솔에 표시됩니다. 

![실행 중인 Notebook 서버가 호스트 머신에서 서버에 액세스하기 위해 사용하는 URL과 함께 콘솔에 표시하는 메시지의 스크린샷](../media/notebook-url.png)

1. Notebook 서버가 표시하는 URL을 즐겨 사용하는 브라우저의 주소 표시줄에 복사합니다. 기본 브라우저에서 열려는 URL을 클릭할 수도 있습니다. 

    제공된 URL이 호스트 머신에서 Notebook 서버로의 연결을 설정하기 때문에 "사이트에 연결할 수 없습니다"라는 메시지가 표시됩니다.

1. 서버에 원격으로 액세스하려면 URL의 호스트 이름을 이전에 저장된 VM의 IP 주소로 바꿉니다. 

    샘플 Notebook 서버 URL은 다음과 같습니다.

    "http://**ab-dsvm-4**:8888/?token={some token}"

    이 예에서는 **ab-dsvm-4**를 머신의 IP 주소로 바꿉니다. IP 주소가 `52.175.199.43`인 경우 URL은 다음과 같습니다.

    "http://**52.175.199.43**:8888/?token={some token}"

    포트 주소인 `:8888`이 URL에 포함되어 있는지 확인합니다.

    > [!TIP]
    > IP 주소를 사용하지 않으려면 `<HOST NAME>.<REGION>.cloudapp.azure.com` 형식으로 서버의 정규화된 이름을 사용할 수도 있습니다.

    다음 스크린샷에서는 브라우저에 Jupyter 대시보드가 표시되는 모양을 보여 줍니다.

    ![Jupyter Notebook 대시보드를 보여주는 스크린샷입니다. ](../media/jupyter-in-browser.png)

1. **notebooks/IntroToJupyterPython.ipynb**로 이동하여 선택합니다. 이 Notebook이 예상 대로 작동하는지 확인해 봅니다.

    축하합니다! 이제 DSVM 기반 가상 머신이 실행되고 있으며 Jupyter에서 원격으로 작업할 수 있습니다. 이 연습에서는 VM에 설치된 소프트웨어를 실행했습니다. 다음 연습에서는 안정적으로 실험할 수 있도록 VM의 컨테이너에서 소프트웨어를 격리합니다.

4. Notebook을 사용한 작업이 완료된 후에는 Cloud Shell에서 `Control-C`를 사용하여 Jupyter 서버를 중지할 수 있습니다.
