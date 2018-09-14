전문 기술에 있을 가능성이 높습니다 전문 특정 영역에 있습니다. 아마도 저장소 관리자 또는 가상화 전문가 아마도에 집중 한 최신 보안 사례를 것입니다. 학생 인 경우 있습니다 수 여전히 탐색 가장 흥미로운 항목입니다.

::: 영역 피벗 = "windows 클라우드"

역할에 관계 없이 대부분의 사람들이 클라우드를 사용 하 여 가상 머신을 만들어 시작 하세요. 다음 Windows Server 2016을 실행 하는 가상 컴퓨터를 가져옵니다.

::: zone-end

::: 영역 피벗 = "linux 클라우드"

역할에 관계 없이 대부분의 사람들이 클라우드를 사용 하 여 가상 머신을 만들어 시작 하세요. 여기 Ubuntu 16.04를 실행 하는 가상 컴퓨터를 가져옵니다.

::: zone-end

여러 가지 방법으로 Azure에서 가상 컴퓨터를 만들려고 합니다. 여기에서 Cloud Shell을 호출 하는 대화형 터미널을 사용 하 여 Windows 또는 Linux 가상 머신을 가져옵니다. 매일 터미널에서 작업할 가장 빠른 방법은 작업을 수행 하는 것은 종종 알 수 있습니다.

::: 영역 피벗 = "windows 클라우드"

> [!TIP]
> Linux를 사용 또는 새 알려드릴까요? 선택 **Linux** Linux 가상 컴퓨터를 실행 하려면이 페이지의 맨 위에서 합니다.

::: zone-end

::: 영역 피벗 = "linux 클라우드"

> [!TIP]
> Windows를 선호 또는 새 알려드릴까요? 선택 **Windows** Windows Server 가상 컴퓨터를 실행 하려면이 페이지의 맨 위에서 합니다.

::: zone-end

일부 기본 용어를 검토 하 고 실행할 첫 번째 가상 머신 가져오기 보겠습니다.

## <a name="what-is-a-virtual-machine"></a>가상 머신 이란?

가상 컴퓨터 또는 VM에는 물리적 컴퓨터의 소프트웨어 에뮬레이션입니다. Vm 소프트웨어, 수십, 수백 존재 하거나 몇 분 안에 수천 개의 Azure Vm을 생성할 수 있습니다, 때문에 더 이상 필요 하지 않을 때를 삭제 합니다. 저렴 하 고 분당 청구를 사용 하 여 사용 하는 동안 사용 하는 계산 리소스에 대해서만 지불 합니다. 또한 필요에 맞게 Vm을 구성 하는 방법은 여러 가지가 있습니다.

::: 영역 피벗 = "windows 클라우드"

실행 중인 VM의 스냅숏을 호출 되는 _이미지_합니다. Azure는 Windows 및 Linux의 여러 버전에 대 한 이미지를 제공 합니다. 또한 배포를 신속 하 게 진행할 수 있도록 미리 구성 된 사용자 고유의 이미지를 만들 수 있습니다. 다음 Microsoft에서 제공 되는 Windows Server 2016 VM을 가져옵니다.

::: zone-end

::: 영역 피벗 = "linux 클라우드"

실행 중인 VM의 스냅숏을 호출 되는 _이미지_합니다. Azure는 Windows 및 Linux의 여러 버전에 대 한 이미지를 제공 합니다. 또한 배포를 신속 하 게 진행할 수 있도록 미리 구성 된 사용자 고유의 이미지를 만들 수 있습니다. 같습니다 Canonical에서 제공 하는 Ubuntu 16.04 VM을 가져옵니다.

::: zone-end

## <a name="what-defines-a-virtual-machine-on-azure"></a>Azure에서 가상 컴퓨터 정의?

가상 컴퓨터 크기와 위치를 비롯 한 인수의 수로 정의 됩니다. VM 구성 상태로 전환 하기 전에 잠시 살펴봅니다와 관련 된 내용을 합니다.

:::row:::
    :::column:::
        **크기**
    :::column-end:::
    ::: 열 범위 = "3"::: VM의 _크기_ 해당 프로세서 속도, 메모리의 양, 저장소 및 예상된 네트워크 대역폭의 초기 크기를 정의 합니다. 일부 크기에는 고급 그래픽 렌더링 및 비디오 편집에 대 한 특별 한 하드웨어 Gpu 등도 포함 됩니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **지역**
    :::column-end:::
    ::: 열 범위 = "3"::: Azure 데이터 센터를 전 세계에 걸쳐 이루어집니다. A _지역_ 명명 된 지리적 위치에 대 한 Azure 데이터 센터의 집합이 있습니다. Virtual machines를 비롯 한 모든 Azure 리소스, 지역을 할당 됩니다. 미국 동부 및 북유럽 지역에 속합니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **네트워크**
    :::column-end:::
    ::: 열 범위 = "3"::: A _가상 네트워크_ Azure에서 논리적으로 격리 된 네트워크입니다. Azure에서 각 가상 머신을 가상 네트워크와 연결 됩니다. Azure는 클라우드 수준 방화벽 이라는 가상 네트워크에 대 한 제공 _네트워크 보안 그룹_합니다.
    :::column-end:::
:::row-end:::

:::row:::
    :::column:::
        **리소스 그룹**
    :::column-end:::
    ::: 열 범위 = "3"::: Virtual machines 및 다른 클라우드 리소스 이라는 논리적 컨테이너로 그룹화 됩니다 _리소스 그룹_합니다. 그룹 응용 프로그램 또는 서비스의 일부로 함께 배포 되는 리소스의 집합을 구성 하려면 일반적으로 사용 됩니다. 이름을 사용 하 여 리소스 그룹에 참조 합니다.
    :::column-end:::
:::row-end:::

## <a name="what-is-azure-cloud-shell"></a>Azure Cloud Shell은 무엇인가요?

Azure Cloud Shell은 관리 및 Azure 리소스를 개발 하기 위한 브라우저 기반 명령줄 환경입니다. Cloud Shell은 클라우드에서 실행 되는 대화형 콘솔으로 간주 합니다.

Cloud Shell에서 선택할 수 있는 두 가지 환경 제공: Bash 및 PowerShell. Azure CLI, azure 명령줄 인터페이스에 대 한 액세스 포함 되어 있습니다.

모든 종류의 VM 관리 하려면 Azure portal, Azure CLI 및 Azure PowerShell을 포함 하 여 모든 Azure 관리 인터페이스를 사용할 수 있습니다. 학습 목적인 경우 여기 사용할지 Azure CLI를 만들고 Windows 또는 Linux VM을 관리 합니다.

::: 영역 피벗 = "windows 클라우드"

## <a name="create-a-windows-vm"></a>Windows VM 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

실행 중인 Windows VM에 알아보겠습니다.

<!--

TODO: Omitted for sandbox. Possibly re-insert later for non-sandbox workflow.

1. From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```
-->

1. 이 페이지의 오른쪽에 Cloud Shell에서 실행 된 `az vm create` VM을 만드는 명령입니다. 나중에 다시 하나로 아래에 표시 된 암호를 변경 하는 것이 좋습니다.

      > [!NOTE]
    > 위 조합 하 고 소문자, 숫자 및 기호를 사용 하 여 적어도 8 자를 포함 하는 암호를 선택 합니다.

    ```azurecli
    az vm create \
      --name myWindowsVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image Win2016Datacenter \
      --size Standard_DS2_v2 \
      --admin-username azureuser \
      --admin-password "Password1234&"
    ```

    > [!TIP]
    > 사용할 수는 **복사** 각 명령을 복사 하는 단추입니다. 붙여, Cloud Shell 창에 새 줄을 마우스 오른쪽 단추로 클릭 하 고 선택 **붙여**합니다.

    VM을 합하여 4 ~ 5 분을 소요 됩니다. 비교 하 여 구매, 랙, 및 데이터 센터에서 시스템을 구성 하는 데 걸리는 시간입니다. 상당히 차이점!

대기 하는 동안에 방금 실행 한 명령을 검토해 보겠습니다.

* VM 이름은 **myWindowsVM**합니다. 이 이름은 Azure에서 VM을 식별합니다. 또한 VM의 내부 호스트 이름 또는 컴퓨터 이름이 됩니다.
* 리소스 그룹 또는 VM의 논리적 컨테이너 이름이  **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 합니다.
* **Win2016Datacenter** Windows Server 2016 VM 이미지를 지정 합니다.
* **포함 한 Standard_DS2_v2** VM의 크기를 나타냅니다. 이 크기는 두 개의 가상 Cpu와 7GB 메모리에 있습니다.
* 사용자 이름 및 암호를 나중에 VM에 연결할 수 있습니다. 예를 들어 작업 하 고 시스템을 구성 하는 원격 데스크톱 또는 WinRM을 통해 연결할 수 있습니다.

기본적으로 Azure VM에 공용 IP 주소를 할당합니다. 인터넷 또는 내부 네트워크 에서만에서 액세스할 수 있도록 VM을 구성할 수 있습니다.

Vm 만들기 및 관리 해야 하는 옵션 중 일부에 대 한이 짧은 비디오도 확인할 수 있습니다.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

VM 준비 되 면 정보가 표시 됩니다. 예를 들면 다음과 같습니다.

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

::: 영역 피벗 = "linux 클라우드"

## <a name="create-a-linux-vm"></a>Linux VM 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

실행 하 여 Linux VM을 살펴보겠습니다.

<!--

TODO: Omitted for sandbox. Possibly re-insert later for non-sandbox workflow.
 
1. From Cloud Shell on the right side of this page, run the `az group create` command to create a resource group named **myResourceGroup** in the East US region.

    ```azurecli
    az group create \
      --location eastus \
      --name myResourceGroup
    ```
-->

1. 이 페이지의 오른쪽에 Cloud Shell에서 실행 된 `az vm create` VM을 만드는 명령입니다.

    ```azurecli
    az vm create \
      --name myLinuxVM \
      --resource-group <rgn>[Sandbox resource group name]</rgn> \
      --image UbuntuLTS \
      --size Standard_DS2_v2 \
      --generate-ssh-keys
    ```

    > [!TIP]
    > 사용할 수는 **복사** 각 명령을 복사 하는 단추입니다. 붙여, Cloud Shell 창에 새 줄을 마우스 오른쪽 단추로 클릭 하 고 선택 **붙여**합니다.

    VM을 합하여 약 2 분 정도 걸립니다. 비교 하 여 구매, 랙, 및 데이터 센터에서 시스템을 구성 하는 데 걸리는 시간입니다. 상당히 차이점!

대기 하는 동안에 방금 실행 한 명령을 검토해 보겠습니다.

* VM 이름은 **myLinuxVM**합니다. 이 이름은 Azure에서 VM을 식별합니다. 또한 VM의 내부 호스트 이름 또는 컴퓨터 이름이 됩니다.
* 리소스 그룹 또는 VM의 논리적 컨테이너 이름이  **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 합니다.
* **UbuntuLTS** Ubuntu 16.04 LTS VM 이미지를 지정 합니다.
* **포함 한 Standard_DS2_v2** VM의 크기를 나타냅니다. 이 크기는 두 개의 가상 Cpu와 7GB 메모리에 있습니다.
* `--generate-ssh-keys` 옵션은 VM에 로그인 할 수 있도록 SSH 키 쌍을 만듭니다.

기본적으로 Azure VM에 공용 IP 주소를 할당합니다. 인터넷 또는 내부 네트워크 에서만에서 액세스할 수 있도록 VM을 구성할 수 있습니다.

Vm 만들기 및 관리 해야 하는 옵션 중 일부에 대 한이 짧은 비디오도 확인할 수 있습니다.

> [!VIDEO https://www.microsoft.com/videoplayer/embed/RE2yJKx]

VM 준비 되 면 정보가 표시 됩니다. 예를 들면 다음과 같습니다.

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

살펴본 몇 가지 개념을 면 몇 분만에 Azure에서 VM을 스핀업 할 수 있습니다. 다양 한 VM의 크기 및 방화벽 규칙 같은 이러한 개념을 익숙할 수 있습니다.에 이미 있습니다.

다음으로, 웹 서버 VM에 설치 하 고 기본 웹 사이트를 처리 하기 위해 웹 서버를 구성 합니다.