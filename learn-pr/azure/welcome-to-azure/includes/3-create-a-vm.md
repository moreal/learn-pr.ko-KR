여러분은 기술 전문가로서 특정 영역에 대한 전문 지식을 갖고 있을 것입니다. 저장소 관리자 또는 가상화 전문가인 분도 있고, 최신 보안 사례에 집중하는 분도 있을 것입니다. 아직 학생인 분들 중에는 적성에 맞는 분야를 찾고 있는 분들도 있을 것입니다.

::: zone pivot="windows-cloud"

여러분이 어떤 역할을 맡고 있든, 대부분의 사람들은 가상 머신을 만들어서 클라우드를 시작합니다. 여기서는 Windows Server 2016을 실행하는 가상 머신을 만들겠습니다.

::: zone-end

::: zone pivot="linux-cloud"

여러분이 어떤 역할을 맡고 있든, 대부분의 사람들은 가상 머신을 만들어서 클라우드를 시작합니다. 여기서는 Ubuntu 16.04를 실행하는 가상 머신을 가져오겠습니다.

::: zone-end

Azure에서 가상 머신을 만드는 여러 가지 방법이 있습니다. 여기서는 Cloud Shell이라고 하는 대화형 터미널을 사용하여 Windows 또는 Linux 가상 머신을 가져오겠습니다. 매일 터미널에서 작업하는 분들은 종종 이 방법으로 작업을 가장 빠르게 수행할 수 있다는 사실을 알고 있습니다.

::: zone pivot="windows-cloud"

> [!TIP]
> Linux를 사용하시겠습니까 아니면 뭔가 새로운 것에 도전하시겠습니까? Linux 가상 머신을 실행하려면 이 페이지 맨 위에서 **Linux**를 선택하세요.

::: zone-end

::: zone pivot="linux-cloud"

> [!TIP]
> Windows를 사용하시겠습니까 아니면 뭔가 새로운 것에 도전하시겠습니까? Windows Server 가상 머신을 실행하려면 이 페이지 맨 위에서 **Windows**를 선택하세요.

::: zone-end

몇 가지 기본 용어를 검토하고 첫 번째 가상 머신을 작동하겠습니다.

## <a name="what-is-a-virtual-machine"></a>가상 머신이란?

VM(가상 머신)은 물리적 컴퓨터의 소프트웨어 에뮬레이션입니다. VM은 소프트웨어로 존재하기 때문에 수십, 수백, 심지어 수천 대의 Azure VM을 몇 분 안에 생성할 수 있으며, 더 이상 필요 없을 때 삭제할 수 있습니다. 저렴한 분당 요금이 청구되며, 사용하는 동안 계산 리소스 사용량에 대해서만 요금을 지불하면 됩니다. 또한 여러 가지 방법으로 필요에 맞게 VM을 구성할 수 있습니다.

::: zone pivot="windows-cloud"

실행 중인 VM의 스냅숏을 _이미지_라고 합니다. Azure는 Windows 및 여러 Linux 버전을 위한 이미지를 제공합니다. 또한 미리 구성된 고유의 이미지를 만들어서 배포를 신속하게 진행할 수 있습니다. 여기서는 Microsoft에서 제공하는 Windows Server 2016 VM을 가져오겠습니다.

::: zone-end

::: zone pivot="linux-cloud"

실행 중인 VM의 스냅숏을 _이미지_라고 합니다. Azure는 Windows 및 여러 Linux 버전을 위한 이미지를 제공합니다. 또한 미리 구성된 고유의 이미지를 만들어서 배포를 신속하게 진행할 수 있습니다. 여기서는 Canonical에서 제공하는 Ubuntu 16.04 VM을 가져오겠습니다.

::: zone-end

## <a name="what-defines-a-virtual-machine-on-azure"></a>Azure에서 가상 머신을 정의하는 것은 무엇입니까?

가상 머신은 크기와 위치를 비롯한 여러 요소로 정의됩니다. VM을 가져오기 전에, 어떤 요소가 있는지 간단하게 알아보겠습니다.

:::row:::
    :::column:::
        **크기**
    :::column-end:::
    :::column span="3"::: VM의 _크기_는 프로세서 속도, 메모리 양, 초기 저장소 양, 예상 네트워크 대역폭을 정의합니다. 일부 크기에는 그래픽 집약적 렌더링 및 비디오 편집용 GPU 같은 특수 하드웨어까지 포함됩니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **Azure 지역**
    :::column-end:::
    :::column span="3"::: Azure는 전 세계에 분산된 데이터 센터로 구성됩니다. _Azure 지역_은 명명된 지리적 위치에 있는 Azure 데이터 센터의 집합입니다. 가상 머신을 비롯한 모든 Azure 리소스에는 Azure 지역이 할당됩니다. Azure 지역의 예로 미국 동부, 북유럽 등이 있습니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **네트워크**
    :::column-end:::
    :::column span="3"::: _가상 네트워크_란 Azure에서 논리적으로 격리된 네트워크입니다. Azure의 각 가상 머신은 가상 네트워크와 연결됩니다. Azure는 가상 네트워크에 _네트워크 보안 그룹_이라고 하는 클라우드 수준 방화벽을 제공합니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **리소스 그룹**
    :::column-end:::
    :::column span="3"::: 가상 머신 및 기타 클라우드 리소스는 _리소스 그룹_이라고 하는 논리적 컨테이너로 그룹화됩니다. 그룹은 일반적으로 응용 프로그램 또는 서비스의 일부로 함께 배포되는 리소스 집합을 구성하는 데 사용됩니다. 리소스 그룹은 이름을 사용하여 나타냅니다.
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a>Azure Cloud Shell이란?

Azure Cloud Shell은 Azure 리소스를 관리하고 개발하기 위한 브라우저 기반 명령줄 환경입니다. Cloud Shell을 클라우드에서 실행되는 대화형 콘솔이라고 생각하시면 됩니다.

Cloud Shell은 Bash와 PowerShell의 두 가지 환경 중에 선택할 수 있습니다. 두 환경 모두 Azure의 명령줄 인터페이스인 Azure CLI에 대한 액세스를 제공합니다.

Azure Portal, Azure CLI, Azure PowerShell을 비롯한 모든 Azure 관리 인터페이스를 사용하여 모든 종류의 VM을 관리할 수 있습니다. 여기서는 학습이 목적이기 때문에 Azure CLI를 사용하여 Windows 또는 Linux VM을 만들고 관리하겠습니다.

::: zone pivot="windows-cloud"

## <a name="create-a-windows-vm"></a>Windows VM 만들기

Windows VM을 실행해 보겠습니다.

1. 이 페이지 오른쪽의 Cloud Shell에서 `az group create` 명령을 실행하여 미국 동부 지역에 **myResourceGroup**이라는 리소스 그룹을 만듭니다.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. `az vm create` 명령을 실행하여 VM을 만듭니다. 아래의 암호를 나중에 기억하기 쉬운 암호로 변경하는 것이 좋습니다.

      > [!NOTE]
    > 대문자와 소문자, 숫자 및 기호의 조합으로 이루어진 8자 이상의 암호를 선택해야 합니다.

    ```azurecli
    az vm create \
      --name myWindowsVM \
      --resource-group myResourceGroup \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --location eastus \
      --admin-username azureuser \
      --admin-password "Password1234&"
    ```

    > [!TIP]
    > **복사** 단추를 사용하여 각 명령을 복사할 수 있습니다. 붙여넣으려면 Cloud Shell 창에서 새 줄을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.

    VM이 나타날 때까지 4~5분 정도 걸립니다. 랙 시스템을 구입하여 데이터 센터에서 구성하는 데 걸리는 시간과 비교해 보세요. 하늘과 땅 차이죠!

기다리는 동안 방금 실행한 명령을 검토해 보겠습니다.

* VM 이름은 **myWindowsVM**입니다. 이 이름은 Azure에서 VM을 식별합니다. 또한 VM의 내부 호스트 이름 또는 머신 이름이 됩니다.
* 리소스 그룹 또는 VM의 논리적 컨테이너는 **myResourceGroup**입니다.
* **Win2016Datacenter**는 Windows Server 2016 VM 이미지를 지정합니다.
* **Standard_DS2_v2**는 VM 크기를 나타냅니다. 현재 이 크기는 가상 CPU 2대와 7GB 메모리를 제공합니다.
* VM은 **미국 동부** 위치 또는 Azure 지역에 있습니다.
* 사용자 이름 및 암호를 사용하여 나중에 VM에 연결할 수 있습니다. 예를 들어 원격 데스크톱 또는 WinRM을 통해 연결하여 시스템을 사용하고 구성할 수 있습니다.

기본적으로 Azure는 VM에 공용 IP 주소를 할당합니다. 인터넷에서 또는 오직 내부 네트워크에서만 액세스할 수 있도록 VM을 구성할 수 있습니다.

VM을 만들고 관리하는 데 사용되는 옵션을 설명하는 이 짧은 비디오도 시청하세요.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

VM이 준비되면 VM 관련 정보가 표시됩니다. 예를 들면 다음과 같습니다.

```console
{
  "fqdns": "",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myWindowsVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1E-1B-3B",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.5",
  "publicIpAddress": "104.211.9.245",
  "resourceGroup": "myResourceGroup",
  "zones": ""
}
```

::: zone-end

::: zone pivot="linux-cloud"

## <a name="create-a-linux-vm"></a>Linux VM 만들기

Linux VM을 실행해 보겠습니다.

1. 이 페이지 오른쪽의 Cloud Shell에서 `az group create` 명령을 실행하여 미국 동부 지역에 **myResourceGroup**이라는 리소스 그룹을 만듭니다.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```

1. `az vm create` 명령을 실행하여 VM을 만듭니다.

    ```azurecli
    az vm create \
      --name myLinuxVM \
      --resource-group myResourceGroup \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --location eastus \
      --generate-ssh-keys
    ```

    > [!TIP]
    > **복사** 단추를 사용하여 각 명령을 복사할 수 있습니다. 붙여넣으려면 Cloud Shell 창에서 새 줄을 마우스 오른쪽 단추로 클릭하고 **붙여넣기**를 선택합니다.

    VM이 나타날 때까지 약 2분이 걸립니다. 랙 시스템을 구입하여 데이터 센터에서 구성하는 데 걸리는 시간과 비교해 보세요. 하늘과 땅 차이죠!

기다리는 동안 방금 실행한 명령을 검토해 보겠습니다.

* VM 이름은 **myLinuxVM**입니다. 이 이름은 Azure에서 VM을 식별합니다. 또한 VM의 내부 호스트 이름 또는 머신 이름이 됩니다.
* 리소스 그룹 또는 VM의 논리적 컨테이너는 **myResourceGroup**입니다.
* **UbuntuLTS**는 Ubuntu 16.04 LTS VM 이미지를 지정합니다.
* **Standard_DS2_v2**는 VM 크기를 나타냅니다. 현재 이 크기는 가상 CPU 2대와 7GB 메모리를 제공합니다.
* VM은 **미국 동부** 위치 또는 Azure 지역에 있습니다.
* `--generate-ssh-keys` 옵션은 VM에 로그인할 수 있도록 SSH 키 쌍을 만듭니다.

기본적으로 Azure는 VM에 공용 IP 주소를 할당합니다. 인터넷에서 또는 오직 내부 네트워크에서만 액세스할 수 있도록 VM을 구성할 수 있습니다.

VM을 만들고 관리하는 데 사용되는 옵션을 설명하는 이 짧은 비디오도 시청하세요.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

VM이 준비되면 VM 관련 정보가 표시됩니다. 예를 들면 다음과 같습니다.

```console
{
    "fqdns": "",
    "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.Compute/virtualMachines/myLinuxVM",
    "location": "eastus",
    "macAddress": "00-0D-3A-1D-EB-02",
    "powerState": "VM running",
    "privateIpAddress": "10.0.0.4",
    "publicIpAddress": "137.135.110.210",
    "resourceGroup": "myResourceGroup",
    "zones": ""
}
```

::: zone-end

## <a name="summary"></a>요약

몇 가지 개념을 살펴보았으니, 이제 몇 분 안에 Azure에서 VM을 실행할 수 있을 것입니다. 여러분은 VM의 크기 및 방화벽 규칙을 포함한 여러 개념에 이미 익숙할 것입니다.

다음으로, VM에 웹 서버를 설치하고 기본 웹 사이트 역할을 하도록 웹 서버를 구성하겠습니다.