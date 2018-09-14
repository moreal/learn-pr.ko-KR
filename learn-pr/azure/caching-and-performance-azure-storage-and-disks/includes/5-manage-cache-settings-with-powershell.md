관리 스크립트 만들기는 워크플로를 최적화하는 강력한 방법입니다. 일반적이 고 반복적인 작업을 자동화할 수 있습니다. 스크립트를이 확인 되 면 실행 됩니다 일관 되 게 오류 가능성이 줄어듭니다입니다. 이전 연습에서 VM을 만들고, 데이터 디스크를 추가 하 고 Azure 포털을 통해 캐시 설정을 변경 합니다. 여러 지역에서 여러 Vm에서 이러한 태스크를 반복 해야 하는 경우에 어떻게 했습니다? Azure PowerShell을 사용 하겠습니다.

## <a name="what-is-azure-powershell"></a>Azure PowerShell이란?

Azure PowerShell은 Azure 구독에 연결 하 고 리소스를 관리할 수 있도록 Windows PowerShell에 추가 하는 모듈입니다. Azure PowerShell 함수를 Windows PowerShell이 필요 합니다. Windows PowerShell 셸 창, 명령, 구문 분석 및 등과 같은 서비스를 제공 합니다. Azure PowerShell은 Azure 특정 명령을 추가합니다.

예를 들어, Azure PowerShell은 제공 된 **New-azurermvm** Azure 구독 내의 가상 컴퓨터를 만드는 명령입니다. 를 사용 하려면 PowerShell 응용 프로그램을 시작 하는 다음이 예제와 같이 명령을 실행 합니다.

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell은 사용할 수 있는 두 가지 방법: Azure Cloud Shell을 통해 또는 Linux, Mac 또는 Windows에서 로컬 설치를 사용 하 여 브라우저 내에서.

## <a name="what-are-powershell-cmdlets"></a>PowerShell cmdlet이란?

PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다. cmdlet은 단일 기능을 조작하는 명령입니다. 용어 **cmdlet** "작은 명령입니다."를 의미 하기 것 규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.

기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다. PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다. 예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.

cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다. 또한 동사 선택에 대 한 규칙: "get" 데이터를 검색 하려면 "설정"을 삽입 하거나 "out" 형식 데이터에 데이터를 "format" 업데이트 등을 대상에 직접 출력 합니다.

cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다. **Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다.

```powershell
Get-Help <cmdlet-name> -detailed
```

## <a name="what-is-azurerm"></a>AzureRM이란?

**AzureRM** cmdlet의 집합을 Azure 기능을 사용 해야 하는 Azure PowerShell 모듈에 대 한 정식 이름 (합니다 **RM** 이름에는 **Resource Manager**). 여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다.

## <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>Azure 디스크 캐싱의 관리용 PowerShell cmdlet

Azure PowerShell에는 Vm 및 디스크를 관리할 수 있도록 특정 cmdlet에 있습니다.

다음 표에서 다음 연습에서에서는 cmdlet 중 일부를 나열 합니다.

|명령  |설명  |
|---------|---------|
|`Get-AzureRmVM`     |  가상 머신의 속성을 가져옵니다.       |
|`Update-AzureRmVM`     |  Azure 가상 머신의 상태를 업데이트합니다.       |
|`New-AzureRmDiskConfig`     |  구성 가능한 디스크 개체를 만듭니다.       |
|`Add-AzureRmVMDataDisk`     |  가상 머신에 데이터 디스크를 추가합니다.   |

VM에 캐싱을 관리 하는 다음 연습에서 이러한 cmdlet을 사용해 보겠습니다.
