Azure PowerShell을 사용하면 명령을 작성하고 즉시 실행할 수 있습니다. 이를 **대화형 모드**라고 합니다.

CRM(고객 관계 관리) 예제의 전반적인 목표는 VM을 포함하는 세 개의 테스트 환경을 만드는 것입니다. 리소스 그룹을 사용하여 VM이 유닛 테스트용, 통합 테스트용, 수용 테스트용 개별 환경으로 구성되도록 합니다. 리소스 그룹을 한 번만 만들면 되기 때문에 PowerShell의 대화형 모드를 사용하는 것이 좋습니다.

이 섹션에서는 PowerShell을 대화형으로 사용하여 Azure 구독에 로그온하고 리소스 그룹을 만드는 방법의 몇 가지 예를 보여 줍니다.

## <a name="what-are-powershell-cmdlets"></a>PowerShell cmdlet이란?
PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다. cmdlet은 단일 기능을 조작하는 명령입니다. **cmdlet**이란 용어는 “작은 명령”을 의미하는 것입니다. 규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.

기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다. PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다. 예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.

cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다. 동사 선택 규칙도 있습니다. “get”은 데이터를 검색하고, “set”은 데이터를 삽입하거나 업데이트하고, “format”은 데이터 서식을 지정하고, “out”은 출력을 대상으로 보냅니다.

cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다. **Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다.

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>AzureRM이란?
**AzureRM**은 Azure 기능을 사용하는 cmdlet이 포함된 Azure PowerShell 모듈의 정식 이름입니다(이름에 포함된 **RM**은 **리소스 관리자**를 나타냄). 여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다.

## <a name="how-to-create-a-resource-group"></a>리소스 그룹을 만드는 방법
이제 Azure PowerShell의 로컬 설치를 사용하여 리소스 그룹을 만들겠습니다. 

이 프로세스는 다음 4단계로 구성됩니다. 

1. Azure cmdlet을 가져옵니다.

1. Azure 구독에 연결합니다.

1. 리소스 그룹을 만듭니다.

1. 생성이 성공했는지 확인합니다(아래 참조).

다음 그림은 이러한 단계의 개요를 보여줍니다.

![리소스 그룹을 만드는 단계를 보여주는 그림입니다.](../media/5-create-resource-overview.png)

각 단계는 다른 cmdlet에 해당합니다.

### <a name="import"></a>가져오기
시작 시 PowerShell은 기본적으로 핵심 cmdlet만 로드합니다. 따라서 Azure에서 작업해야 하는 cmdlet은 로드되지 않습니다. 필요한 cmdlet을 로드하는 가장 신뢰할 수 있는 방법은 PowerShell 세션을 시작할 때 수동으로 가져오는 것입니다.

**Import-Module** cmdlet을 사용하여 모듈을 로드합니다. 이 cmdlet에는 다양한 상황을 처리하는 많은 매개 변수가 있습니다. 예를 들어 여러 모듈, 특정 모듈 버전, 모듈의 일부 등을 로드할 수 있습니다. 하나의 모듈 전체를 로드하기 위한 구문은 다음과 같습니다.

```powershell
Import-Module <module-name>
```

> [!TIP]
> Azure PowerShell을 자주 사용하는 경우 모듈 로드 프로세스를 자동화하는 두 가지 방법이 있습니다. PowerShell 프로필에 항목을 추가하여 시작 시 Azure 모듈을 가져오거나, cmdlet을 사용할 때 자동으로 포함된 모듈을 로드하는 최신 버전의 PowerShell을 사용할 수 있습니다.

### <a name="connect"></a>연결
Azure PowerShell의 로컬 설치를 사용하므로 Azure 명령을 실행하기 전에 먼저 인증해야 합니다. **Connect-AzureRmAccount** cmdlet은 Azure 자격 증명을 묻는 메시지를 표시하고 Azure 구독에 연결합니다. 여기에는 많은 선택적 매개 변수가 있지만, 대화형 프롬프트만 필요한 경우에는 매개 변수가 필요하지 않습니다.

```powershell
Connect-AzureRmAccount
```

### <a name="create"></a>생성
**New-AzureRmResourceGroup** cmdlet은 리소스 그룹을 만듭니다. 이름 및 위치를 지정해야 합니다. 이름은 구독 내에서 고유해야 합니다. 위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다(규정 준수에 중요할 수 있음). “미국 서부”, “북유럽” 또는 “인도 서부”와 같은 문자열을 사용하여 위치를 지정합니다. 대부분의 Azure cmdlet과 마찬가지로 **New-AzureRmResourceGroup**에는 많은 선택적 매개 변수가 있지만 핵심 구문은 다음과 같습니다.

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

### <a name="verify"></a>Verify
**Get-AzureRmResource**는 Azure 리소스를 나열합니다. 이 cmdlet은 리소스 그룹 생성에 성공했는지 여부를 확인하는 데 유용합니다.

```powershell
Get-AzureRmResource
```

보다 간결하게 표시하려면 파이프 ‘|’를 사용하여 **Get-AzureRmResource**의 출력을 **Format-Table** cmdlet으로 보낼 수 있습니다.

```powershell
Get-AzureRmResource | Format-Table
```

## <a name="summary"></a>요약
PowerShell의 대화형 모드는 일회성 작업에 적합합니다. 예제에서는 프로젝트 수명 동안 동일한 리소스 그룹을 사용하므로 대화형으로 만드는 것이 좋습니다. 대체로, 이 작업에는 스크립트를 작성하고 해당 스크립트를 한 번만 실행하는 것보다 대화형 모드를 사용하는 것이 더 빠르고 편리합니다.