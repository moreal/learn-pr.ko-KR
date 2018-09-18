관리 스크립트 만들기는 워크플로를 최적화하는 강력한 방법입니다. 공통적인 반복 작업을 자동화할 수 있습니다. 스크립트가 확인된 후에는 지속적으로 실행되어 오류가 감소할 수 있습니다. 이전 연습에서는 Azure Portal을 통해서만 VM을 만들고, 데이터 디스크를 추가하고, 캐시 설정을 변경했습니다. 여러 지역에 있는 여러 VM에서 이러한 작업을 반복해야 한다면 어떻게 할까요? Azure PowerShell을 사용해 보겠습니다.

## <a name="what-is-azure-powershell"></a>Azure PowerShell이란?
Azure PowerShell은 PowerShell에 추가하여 Azure 구독에 연결하고 리소스를 관리할 수 있는 모듈입니다. Azure PowerShell을 사용하려면 PowerShell이 작동해야 합니다. PowerShell은 셸 창, 명령 구문 분석 등과 같은 서비스를 제공합니다. Azure PowerShell은 Azure 특정 명령을 추가합니다.

예를 들어 Azure PowerShell은 Azure 구독 내에서 가상 머신을 만드는 **New-AzureRmVM** 명령을 제공합니다. 이 명령을 사용하려면 PowerShell 응용 프로그램을 시작한 후 예제와 같이 명령을 실행합니다.

```powershell
New-AzureRmVm `
    -ResourceGroupName "CrmTestingResourceGroup" `
    -Name "CrmUnitTests" `
    -Image "UbuntuLTS"
    ...
```

Azure PowerShell은 Azure Cloud Shell을 통해 브라우저 내부에서 또는 Linux, Mac 또는 Windows의 로컬 설치로 사용할 수 있습니다.

## <a name="what-are-powershell-cmdlets"></a>PowerShell cmdlet이란?

PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다. cmdlet은 단일 기능을 조작하는 명령입니다. **cmdlet**이란 용어는 “작은 명령”을 의미하는 것입니다. 규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.

기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다. PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다. 예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.

cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다. 동사 선택 규칙도 있습니다. “get”은 데이터를 검색하고, “set”은 데이터를 삽입하거나 업데이트하고, “format”은 데이터 서식을 지정하고, “out”은 출력을 대상으로 보냅니다.

cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다. **Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다.

```
Get-Help <cmdlet-name> -detailed
```
## <a name="what-is-azurerm"></a>AzureRM이란?

**AzureRM**은 Azure 기능을 사용하는 cmdlet 집합이 포함된 Azure PowerShell 모듈의 정식 이름입니다(이름에 포함된 **RM**은 **Resource Manager**를 나타냄). 여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다.

## <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>Azure 디스크 캐싱을 관리하기 위한 PowerShell cmdlet

Azure PowerShell에는 VM 및 디스크를 관리하는 데 도움이 되는 특정 cmdlet이 있습니다. 

다음 표에는 다음 연습에서 사용할 일부 cmdlet이 나와 있습니다.

|명령  |설명  |
|---------|---------|
|`Get-AzureRmVM`     |  가상 머신의 속성을 가져옵니다.       |        $myVM
|`Update-AzureRmVM`     |  Azure 가상 머신의 상태를 업데이트합니다.       |        
|`New-AzureRmDiskConfig`     |  구성 가능한 디스크 개체를 만듭니다.       |        
|`Add-AzureRmVMDataDisk`     |  데이터 디스크를 가상 머신에 추가합니다.   |      


다음 연습에서는 이러한 cmdlet을 사용하여 VM의 캐싱을 관리해 보겠습니다.
