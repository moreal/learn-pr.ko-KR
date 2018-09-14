CRM(고객 관계 관리) 시스템을 테스트하는 데 사용되는 Azure 리소스를 관리하는 도구를 선택해야 한다고 가정합니다. 테스트를 사용 하면 리소스 그룹을 만들고 가상 머신 (Vm)를 프로 비전 해야 합니다.

원하는 것에 대해 알아보려면 관리자에 대 한 간단 하지만 설치 및 설정 여러 virtual machines의 자동화 스크립트는 전체 응용 프로그램 환경에 수 있을 만큼 강력 합니다. 사용 가능한 여러 도구가 있고, 사용자와 작업에 가장 적합한 도구를 찾아야 합니다.

## <a name="what-tools-are-available"></a>어떤 도구를 사용할 수 있나요?
Azure는 다음과 같이 선택 가능한 세 가지 관리 도구를 제공합니다.

- Azure Portal
- Azure CLI
- Azure PowerShell

이러한 도구는 모두 대략적으로 동일한 정도의 제어를 제공하고, 도구 중 하나로 수행할 수 있는 작업은 다른 두 개의 도구로도 수행할 수 있습니다. 세 가지 도구는 모두 Windows, macOS 및 Linux에서 실행되는 플랫폼 간 도구입니다. 이러한 도구의 구문, 설정 요구 사항 및 자동화 지원 여부는 서로 다릅니다.

여기서는 세 가지 옵션을 각각 설명하고 그중에서 결정하는 방법에 대한 지침을 제공합니다. 

## <a name="what-is-the-azure-portal"></a>Azure Portal이란?
Azure Portal은 Azure 구독에서 리소스를 만들고, 구성하고, 변경할 수 있는 웹 사이트입니다. 포털은 편리하게 필요한 리소스를 찾고 필요한 변경을 실행할 수 있는 GUI(그래픽 사용자 인터페이스)입니다. 또한 마법사 및 도구 설명을 제공하여 복잡한 관리 작업을 안내합니다.

포털은 반복 작업을 자동화하는 방법을 제공하지 않습니다. 예를 들어 15개 VM을 설정하려면 각 VM에 대한 마법사를 완료하여 VM을 하나씩 만들어야 합니다. 복잡한 작업인 경우 이 방법은 시간이 오래 걸리고 오류가 발생할 수 있습니다. 

## <a name="what-is-the-azure-cli"></a>Azure CLI란?
Azure CLI는 Azure에 연결하고 Azure 리소스에서 관리 명령을 실행하는 플랫폼 간 명령줄 프로그램입니다. 예를 들어 VM을 만들려면 다음과 같은 명령을 사용합니다.

```azurecli
az vm create \
  --resource-group CrmTestingResourceGroup \
  --name CrmUnitTests \
  --image UbuntuLTS
  ...
```

Azure CLI는 Azure Cloud Shell을 통해 브라우저 내부에서 또는 Linux, Mac 또는 Windows의 로컬 설치로 사용할 수 있습니다. 두 경우에 모두 대화형으로 사용하거나 스크립팅할 수 있습니다. 대화형 사용의 경우 먼저 Windows에서 `cmd.exe`와 같은 셸을 먼저 시작하거나 Linux 또는 macOS에서 Bash를 시작한 후 셸 프롬프트에서 명령을 실행합니다. 반복 작업을 자동화하려면 선택한 셸의 스크립트 구문을 사용하여 셸 스크립트로 명령을 어셈블한 후 스크립트를 실행합니다.

## <a name="what-is-azure-powershell"></a>Azure PowerShell이란?
Azure PowerShell은 Windows PowerShell 또는 PowerShell Core에 추가하여 Azure 구독에 연결하고 리소스를 관리할 수 있는 모듈입니다. Azure PowerShell을 사용하려면 PowerShell이 작동해야 합니다. PowerShell은 셸 창, 명령 구문 분석 등과 같은 서비스를 제공합니다. Azure PowerShell은 Azure 특정 명령을 추가합니다.

예를 들어, Azure PowerShell은 제공 된 **New-azurermvm** Azure 구독 내의 가상 컴퓨터를 만드는 명령입니다. 이 명령을 사용하려면 PowerShell 응용 프로그램을 시작한 후 다음과 같은 명령을 실행합니다.

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell은 Azure Cloud Shell을 통해 브라우저 내부에서 또는 Linux, Mac 또는 Windows의 로컬 설치로도 사용할 수 있습니다. 두 경우에 모두 선택할 수 있는 두 가지 모드가 있습니다. 한 번에 하나의 명령을 수동으로 실행하는 대화형 모드에서 사용하거나, 여러 명령으로 구성된 스크립트를 실행하는 스크립팅 모드에서 사용할 수 있습니다.

## <a name="how-to-choose-an-administrative-tool"></a>관리 도구를 선택하는 방법
포털, Azure CLI 및 Azure PowerShell 간에는 관리할 수 있는 Azure 개체 및 만들 수 있는 구성과 관련하여 대략적인 패리티가 있습니다. 또한 모두 플랫폼 간 도구입니다. 이는 일반적으로 선택할 때 몇 가지 다른 요인을 고려함을 의미합니다.

- **자동화**: 복잡하거나 반복적인 작업 집합을 자동화해야 하나요? Azure PowerShell 및 Azure CLI는 이 기능을 지원하지만 포털은 지원하지 않습니다.

- **학습 곡선**: 새 명령이나 구문 없이 작업을 빠르게 완료해야 하나요? Azure Portal에서는 구문을 학습하거나 명령을 기억할 필요가 없습니다. Azure PowerShell 및 Azure CLI에서는 사용하는 각 명령에 대한 자세한 구문을 알고 있어야 합니다.

- **팀 기능**: 팀에 기존 전문가가 있나요? 예를 들어 팀이 Windows를 관리하는 데 PowerShell을 사용했을 수 있습니다. 이 경우 Azure PowerShell에 신속하게 익숙해질 수 있습니다.

## <a name="example"></a>예
CRM 응용 프로그램에 대한 테스트 환경을 만들기 위해 관리 도구를 선택 중이라는 점을 상기하세요. 관리자는 다음과 같은 두 개의 특정 Azure 작업을 수행해야 합니다.

1. 테스트의 각 범주(유닛, 통합 및 수용)에 대한 하나의 리소스 그룹을 만듭니다.
2. 테스트를 매번 시작하기 전에 각 리소스 그룹에 여러 VM을 만듭니다.

리소스 그룹을 만들려면 Azure Portal은 합리적인 선택입니다. 이 작업은 일회성 작업이므로 작업을 수행하는 데 스크립트가 필요하지 않습니다.

VM을 만드는 가장 적합한 도구를 찾는 것은 더 어려운 결정입니다. 여러 VM을 만들어야 하고 이 작업을 매주 여러 번 반복적으로 수행해야 할 수 있습니다. 이는 자동화가 필요함을 의미하므로 Azure Portal은 좋은 선택이 아님을 의미합니다. 이 경우 Azure PowerShell 또는 Azure CLI가 요구 사항을 충족합니다. 팀 구성원이 이미 PowerShell을 어느 정도 알고 있는 경우 Azure PowerShell이 가장 적합한 도구일 수 있습니다. Azure PowerShell은 관리 팀이 사용하는 운영 체제에서 사용할 수 있고, 자동화를 지원하며, 팀이 빠르게 배울 수 있어야 합니다.

## <a name="summary"></a>요약
대부분의 관리자가 처음 사용하는 Azure 환경은 포털입니다. 포털은 깨끗하고 잘 구조화된 그래픽 인터페이스를 제공하지만 자동화에 대한 제한된 옵션을 제공하므로 시작할 수 있는 좋은 위치입니다. 자동화가 필요한 경우 Azure는 PowerShell 경험이 있는 관리자를 위한 Azure PowerShell 및 모든 사용자를 위한 Azure CLI의 두 가지 옵션을 제공합니다.

실제로 비즈니스에는 일반적으로 일회성 및 반복적인 작업이 함께 포함됩니다. 이는 포털과 스크립트 솔루션을 둘 다 사용하는 것이 일반적임을 의미합니다. CRM 예제에서는 포털을 통해 리소스 그룹을 만들고 PowerShell을 통해 VM 만들기를 자동화하는 것이 적절합니다.

이 모듈의 나머지 부분에서는 Azure PowerShell 설치 및 사용을 중점적으로 설명합니다.
