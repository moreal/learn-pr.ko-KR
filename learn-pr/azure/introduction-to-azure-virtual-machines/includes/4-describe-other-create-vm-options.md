Azure Portal은 시작할 때 VM과 같은 리소스를 만드는 가장 쉬운 방법입니다. 그러나 Azure를 사용하는 가장 효율적이거나 가장 빠른 방법은 아닙니다. 특히 여러 리소스를 함께 만들어야 하는 경우에는 더욱 그렇습니다. 따라서 여기서는 서로 다른 작업을 처리하는 수십 개의 VM을 만들 것입니다. Azure Portal에서 수동으로 만드는 것은 재미 있는 작업이 아닙니다!

Azure에서 리소스를 만들고 관리하는 몇 가지 다른 방법을 살펴보겠습니다.

- [Azure Resource Manager](#Azure_RM)
- [Azure PowerShell](#Azure_PowerShell)
- [Azure CLI](#Azure_CLI)
- [Azure REST API](#Azure_REST_API)
- [Azure 클라이언트 SDK](#Azure_Client_SDK)
- [Azure VM 확장](#Azure_VMExtensions)
- [Azure Automation Services](#Azure_Automation)

<a name="Azure_RM" />

## <a name="azure-resource-manager"></a>Azure Resource Manager

동일한 설정을 사용하여 VM 복사본을 만들려고 한다고 가정해 보겠습니다. VM 이미지를 만들고, Azure에 업로드하고, 새 VM에 대한 기준으로 참조할 수 있습니다. 이 프로세스는 비효율적이며 시간 소모적입니다. Azure는 정확한 VM 복사본을 만드는 데 사용할 템플릿을 만드는 옵션을 제공합니다.

일반적으로 Azure 인프라에는 많은 리소스가 포함되며, 그 중 대부분은 몇 가지 방식으로 서로 관련되어 있습니다. 예를 들어 여기서 만든 VM에는 WordPress 사이트를 실행하기 위해 함께 만든 가상 머신 자체, 저장소, 네트워크 인터페이스, 웹 서버 및 데이터베이스가 모두 포함됩니다. **Azure Resource Manager**는 이러한 관련 리소스를 더 효율적으로 사용합니다. 모든 리소스를 함께 배포, 업데이트 또는 삭제할 수 있는 명명된 **리소스 그룹**에 리소스를 구성합니다. WordPress 사이트를 만들었을 때 VM 만들기의 일환으로 리소스 그룹을 식별했고 Resource Manager에서 관련 리소스를 동일한 그룹에 배치했습니다.

또한 Resource Manager를 사용하면 특정 구성을 만들고 배포하는 데 사용할 수 있는 _템플릿_을 만들 수 있습니다.

### <a name="what-are-resource-manager-templates"></a>Resource Manager 템플릿이란?

**Resource Manager 템플릿**은 솔루션에 배포해야 하는 리소스를 정의하는 JSON 파일입니다.

Automation 스크립트 옵션을 선택하여 특정 VM에 대한 **설정** 섹션에서 리소스 템플릿을 만들 수 있습니다.

![VM에 대한 Automation 스크립트](../media-draft/4-automation-script.png)

나중에 사용할 리소스 템플릿을 저장하거나 이 템플릿을 기반으로 하여 새 VM을 즉시 배포하는 옵션이 있습니다. 예를 들어 테스트 환경에서 템플릿을 통해 VM을 만들 수 있으며, 온-프레미스 머신을 교체하지 못할 수 있습니다. 리소스 그룹을 삭제하면 모든 리소스를 삭제하고 템플릿을 조정한 다음, 다시 시도할 수 있습니다. 기존의 배포된 리소스만 변경하려는 경우 해당 리소스를 만드는 데 사용된 템플릿을 변경하여 다시 배포할 수 있습니다. Resource Manager는 새 템플릿과 일치하도록 리소스를 변경합니다.

원하는 방식으로 작업한 후에는 해당 템플릿을 가져와서 준비 및 프로덕션과 같은 여러 버전의 인프라를 쉽게 다시 만들 수 있습니다. VM 이름, 네트워크 이름, 저장소 계정 이름 등과 같은 필드를 매개 변수화하고, 다른 매개 변수를 사용하여 각 환경을 사용자 지정하는 템플릿을 반복적으로 로드할 수 있습니다.

Azure CLI, Azure PowerShell 또는 Azure REST API와 같은 자동화 스크립팅 도구를 원하는 프로그래밍 언어와 함께 사용하여 리소스 템플릿을 처리함으로써 인프라를 빠르게 구동할 수 있는 강력한 도구가 될 수 있습니다.

<a name="Azure_PowerShell" />

## <a name="azure-powershell"></a>Azure PowerShell

관리 스크립트를 만드는 것은 워크플로를 최적화하는 강력한 방법입니다. 즉 일상적인 반복 작업을 자동화할 수 있으며, 스크립트가 확인되면 일관되게 실행되어 오류를 줄일 수 있습니다. **Azure PowerShell**은 일회성 대화형 작업 또는 반복 작업 자동화에 적합합니다.

> [!NOTE]
> PowerShell은 셸 창과 명령 구문 분석과 같은 서비스를 제공하는 플랫폼 간 셸입니다. Azure PowerShell은 Azure 관련 명령(**cmdlet**이라고 함)을 추가하는 선택적 추가 기능 패키지입니다. 별도의 학습 모듈에서 Azure PowerShell을 설치하고 사용하는 방법에 대해 자세히 알아볼 수 있습니다.

예를 들어 `New-AzureRmVM` cmdlet을 사용하여 새 Azure Virtual Machine을 만들 수 있습니다. 

```powershell
New-AzureRmVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -OpenPorts 80,3389
```

다음과 같이 다양한 매개 변수를 제공하여 사용 가능한 많은 VM 구성 설정을 처리합니다. 대부분의 매개 변수에는 적절한 값이 있으므로 필요한 매개 변수만 지정하면 됩니다. **PowerShell을 통해 스크립트를 사용하여 Azure 작업 자동화** 모듈에서 Azure PowerShell을 사용하여 VM을 만들고 관리하는 방법에 대해 자세히 알아보세요.
<a name="Azure_CLI" />

## <a name="azure-cli"></a>Azure CLI

스크립팅 및 명령줄 Azure 상호 작용을 위한 또 다른 옵션은 **Azure CLI**입니다.

Azure CLI는 명령줄에서 가상 머신 및 디스크와 같은 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다. Cloud Shell을 통해 macOS, Linux 및 Windows 또는 브라우저에서 사용할 수 있습니다. Azure PowerShell과 마찬가지로 Azure CLI는 관리 워크플로를 간소화할 수 있는 강력한 방법입니다. Azure PowerShell과 달리 Azure CLI는 PowerShell 없이 작동할 수 있습니다.

예를 들어 `az vm create` 명령을 사용하여 Azure VM을 만들 수 있습니다.

```bash
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

Azure CLI는 다른 스크립팅 언어(예: Ruby 및 Python)와 함께 사용할 수 있습니다. 두 언어는 모두 개발자가 PowerShell에 익숙하지 않을 수 있는 비 Windows 기반 머신에서 일반적으로 사용됩니다.

**Azure CLI 도구를 사용하여 가상 머신 관리** 모듈에서 VM을 만들고 관리하는 방법에 대해 자세히 알아보세요.

## <a name="programmatic-apis"></a>프로그래밍 방식(API)

일반적으로 실행할 간단한 스크립트가 있고 명령줄 도구를 사용하려는 경우 Azure PowerShell과 Azure CLI는 모두 적절한 옵션입니다. VM 만들기 및 관리가 복잡한 논리를 사용하는 더 큰 응용 프로그램의 일부를 구성하는 더 복잡한 시나리오에서는 다른 접근 방식이 필요합니다.

Azure에서는 모든 종류의 리소스와 프로그래밍 방식으로 상호 작용할 수 있습니다.

<a name="Azure_REST_API" />

### <a name="azure-rest-api"></a>Azure REST API

Azure REST API는 VM을 만들고 관리하는 기능뿐만 아니라 리소스별로 분류된 개발자 작업도 제공합니다. 작업은 해당 HTTP 메서드(`GET`, `PUT`, `POST`, `DELETE` 및 `PATCH`) 및 해당 응답과 함께 URI로 노출됩니다.

Azure Compute API는 가상 머신 및 지원 리소스에 프로그래밍 방식으로 액세스할 수 있도록 합니다. 이 API를 사용하여 수행할 수 있는 작업은 다음과 같습니다.

- 가용성 집합 만들기 및 관리
- 가상 머신 확장 추가 및 관리
- 관리 디스크, 스냅숏, 이미지 만들기 및 관리
- Azure에서 사용할 수 있는 플랫폼 이미지에 액세스
- 리소스 사용량 정보 검색
- 가상 머신 만들기 및 관리
- 가상 머신 확장 집합 만들기 및 관리

<a name="Azure_Client_SDK" />

### <a name="azure-client-sdk"></a>Azure 클라이언트 SDK

REST API는 플랫폼과 언어에 구속받지 않지만, 대부분의 경우 개발자는 더 높은 수준의 추상화를 추구합니다. Azure 클라이언트 SDK는 Azure REST API를 캡슐화하여 개발자가 Azure와 더 쉽게 상호 작용할 수 있도록 합니다.

Azure 클라이언트 SDK는 C#, Java, Node.js, PHP, Python, Ruby 및 Go와 같은 .NET 기반 언어를 포함한 다양한 언어 및 프레임워크에서 사용할 수 있습니다.

`Microsoft.Azure.Management.Fluent` NuGet 패키지를 사용하여 Azure VM을 만드는 C# 코드 조각의 예제는 다음과 같습니다.

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

**Azure Java SDK**를 사용하는 Java의 동일한 코드 조각은 다음과 같습니다.

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

<a name="Azure_VMExtensions" />

## <a name="azure-vm-extensions"></a>Azure VM 확장

초기 배포 후에 가상 머신에 추가 소프트웨어를 구성하고 설치한다고 가정해 보겠습니다. 이 작업에서는 자동으로 모니터링되고 실행되는 특정 구성을 사용하려고 합니다.

**Azure VM 확장**은 초기 배포 후에 Azure VM에서 작업을 구성하고 자동화할 수 있는 작은 응용 프로그램입니다. **Azure VM 확장**은 Azure CLI, PowerShell, Azure Resource Manager 템플릿 및 Azure Portal을 사용하여 실행할 수 있습니다.

새 VM 배포와 함께 확장을 번들로 제공하거나 기존 시스템에 대해 확장을 실행합니다.

<a name="Azure_Automation" />

## <a name="azure-automation-services"></a>Azure Automation Services

원격 인프라를 관리할 때 마주치는 가장 중요한 운영 관리 과제 중 일부는 시간을 절약하고, 오류를 줄이고, 효율성을 높이는 것입니다. 인프라 서비스가 많은 경우 더 높은 수준에서 운영할 수 있도록 Azure에서 고급 서비스를 사용하는 것이 좋습니다.

**Azure Automation**을 사용하면 빈번하고 시간 소모적이며 오류가 발생하기 쉬운 관리 작업을 쉽게 자동화할 수 있는 서비스를 통합할 수 있습니다. 이러한 서비스에는 **프로세스 자동화**, **구성 관리 및 **업데이트 관리**가 포함됩니다.

- **프로세스 관리**. 특정 오류 이벤트에 대해 모니터링되는 VM이 있다고 가정해 보겠습니다. 작업을 수행하고 보고되는 즉시 문제를 해결하려고 합니다. 프로세스 자동화를 통해 데이터 센터에서 발생할 수 있는 이벤트에 응답할 수 있는 감시자 작업을 설정할 수 있습니다.

- **구성 관리**.  VM에서 실행되는 운영 체제에서 사용할 수 있는 소프트웨어 업데이트를 추적하려고 합니다. 포함하거나 제외할 수 있는 특정 업데이트가 있습니다. 구성 관리를 통해 이러한 업데이트를 추적하고 필요에 따라 작업을 수행할 수 있습니다. **System Center Configuration Manager**를 사용하여 회사의 PC, 서버 및 모바일 장치를 관리합니다. Configuration Manager를 사용하여 이 지원을 Azure VM으로 확장할 수 있습니다.

- **업데이트 관리**. VM에 대한 업데이트 및 패치를 관리하는 데 사용됩니다. 이 서비스를 통해 사용 가능한 업데이트의 상태를 평가하고, 설치를 예약하고, 배포 결과를 검토하여 업데이트가 성공적으로 적용되었는지 확인할 수 있습니다. 업데이트 관리는 프로세스 및 구성 관리를 제공하는 서비스를 통합합니다. **Azure Automation** 계정에서 직접 VM에 대한 업데이트 관리를 사용하도록 설정할 수 있습니다. 또한 포털의 가상 머신 블레이드에서 단일 가상 머신에 대한 업데이트 관리를 허용할 수도 있습니다.

알 수 있듯이, Azure는 리소스를 만들고 관리할 수 있는 다양한 도구를 제공하여 관리 작업을 _사용자에게 적합한_ 프로세스에 통합할 수 있습니다. Azure의 다른 서비스 중 일부에서 인프라 리소스가 원활하게 실행되고 있는지 살펴보겠습니다.
