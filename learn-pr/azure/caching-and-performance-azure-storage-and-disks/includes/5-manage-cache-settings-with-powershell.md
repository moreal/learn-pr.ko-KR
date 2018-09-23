관리 스크립트 만들기는 워크플로를 최적화하는 강력한 방법입니다. 공통적인 반복 작업을 자동화할 수 있습니다. 스크립트가 확인되면 지속적으로 실행되어 오류가 감소할 수 있습니다. 이전 연습에서는 Azure Portal을 통해서만 VM을 만들고, 데이터 디스크를 추가하고, 캐시 설정을 변경했습니다. 여러 지역에 있는 여러 VM에서 이러한 작업을 반복해야 한다면 어떻게 할까요? Azure PowerShell을 사용하여 수행할 수 있습니다.

> [!TIP]
> **PowerShell을 사용하여 Azure 작업 자동화** 모듈에서 Azure PowerShell을 자세히 다룹니다. PowerShell을 설치하고, 구성하고, 사용하는 방법에 대한 자세한 내용은 해당 모듈을 확인해야 합니다.

## <a name="what-is-azure-powershell"></a>Azure PowerShell이란?

Azure PowerShell은 Azure 구독에 연결하여 리소스를 관리하는 플랫폼 간 명령줄 도구입니다. 명령줄 도구 지원을 제공하는 **PowerShell** 및 Azure에서 작동하도록 명령("cmdlet"이라고도 함)을 제공하는 **AzureRM**이라는 두 가지 기능의 조합입니다. 

Azure PowerShell에는 Azure 리소스의 대부분의 측면을 조작하기 위한 cmdlet이 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다. 다른 학습 모듈에서 이러한 모든 세부 정보를 다룹니다.

### <a name="powershell-cmdlets-for-managing-azure-disk-caching"></a>Azure 디스크 캐싱을 관리하기 위한 PowerShell cmdlet

Azure PowerShell에는 VM 및 디스크를 관리하는 데 도움이 되는 특정 cmdlet이 있습니다.

|명령  | 설명 |
|---------|-------------|
| `Get-AzureRmVM`         | 가상 머신의 속성을 가져옵니다.       |
| `Update-AzureRmVM`      | Azure 가상 머신의 상태를 업데이트합니다.  |
| `New-AzureRmDiskConfig` | 구성 가능한 디스크 개체를 만듭니다.             |
| `Add-AzureRmVMDataDisk` | 데이터 디스크를 가상 머신에 추가합니다.          |

이 기능을 사용하여 Azure Portal에서 수행했던 작업을 모두 수행할 수 있습니다. VM에서 사용하겠습니다.
