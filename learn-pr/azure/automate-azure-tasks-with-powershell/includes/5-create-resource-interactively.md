PowerShell을 사용하면 명령을 작성하고 즉시 실행할 수 있습니다. 이를 **대화형 모드**라고 합니다.

CRM(고객 관계 관리) 예제의 전반적인 목표는 VM을 포함하는 세 개의 테스트 환경을 만드는 것입니다. 리소스 그룹을 사용하여 VM이 유닛 테스트용, 통합 테스트용, 수용 테스트용 개별 환경으로 구성되도록 합니다. 리소스 그룹을 한 번만 만들기만 하면 되기 때문에 PowerShell의 대화형 모드를 사용하는 것이 좋습니다.

PowerShell 명령을 입력하면 요청한 작업을 수행하는 _cmdlet_에 일치시킵니다. 사용할 수 있는 일부 공통 명령을 찾아본 다음, PowerShell에 Azure 지원을 설치하는 방법을 확인하겠습니다.

## <a name="what-are-powershell-cmdlets"></a>PowerShell cmdlet이란?
PowerShell 명령을 **cmdlet**(“커맨드렛”으로 발음)이라고 합니다. cmdlet은 단일 기능을 조작하는 명령입니다. **cmdlet**이란 용어는 “작은 명령”을 의미하는 것입니다. 규칙에 따라 cmdlet 작성자는 cmdlet을 단일 용도로 단순하게 만드는 것이 좋습니다.

기본 PowerShell 제품에는 세션 및 백그라운드 작업과 같은 기능을 사용하는 cmdlet이 포함되어 있습니다. PowerShell 설치에 모듈을 추가하여 다른 기능을 조작하는 cmdlet을 가져옵니다. 예를 들어 ftp 작업, 운영 체제 관리, 파일 시스템 액세스 등을 지원하는 타사 모듈이 있습니다.

cmdlet은 **Get-Process**, **Format-Table**, **Start-Service** 등의 동사-명사 명명 규칙을 따릅니다. 동사 선택 규칙도 있습니다. “get”은 데이터를 검색하고, “set”은 데이터를 삽입하거나 업데이트하고, “format”은 데이터 서식을 지정하고, “out”은 출력을 대상으로 보냅니다.

cmdlet 작성자는 각 cmdlet에 대한 도움말 파일을 포함하는 것이 좋습니다. **Get-Help** cmdlet은 cmdlet에 대한 도움말 파일을 표시합니다. 예를 들어 다음 명령문을 사용하여 `Get-ChildItem` cmdlet에 대한 도움말을 가져올 수 있습니다.

```powershell
Get-Help Get-ChildItem -detailed
```

## <a name="what-is-a-powershell-module"></a>PowerShell 모듈이란?

Cmdlet은 _모듈_에서 제공됩니다. PowerShell 모듈은 사용할 수 있는 각 cmdlet을 처리하는 코드를 포함하는 DLL입니다. 포함된 모듈을 로드하여 PowerShell에 cmdlet을 로드합니다. `Get-Module` 명령을 사용하여 로드된 모듈 목록을 가져올 수 있습니다.

```powershell
Get-Module
```

그러면 다음과 같이 출력됩니다.

```output
ModuleType Version    Name                                ExportedCommands
---------- -------    ----                                ----------------
Manifest   3.1.0.0    Microsoft.PowerShell.Management     {Add-Computer, Add-Content, Checkpoint-Computer, Clear-Con...
Manifest   3.1.0.0    Microsoft.PowerShell.Utility        {Add-Member, Add-Type, Clear-Variable, Compare-Object...}
Binary     1.0.0.1    PackageManagement                   {Find-Package, Find-PackageProvider, Get-Package, Get-Pack...
Script     1.0.0.1    PowerShellGet                       {Find-Command, Find-DscResource, Find-Module, Find-RoleCap...
Script     2.0.0      PSReadline                          {Get-PSReadLineKeyHandler, Get-PSReadLineOption, Remove-PS...
```

## <a name="what-is-azurerm"></a>AzureRM이란?
**AzureRM**은 Azure 기능을 사용하는 cmdlet이 포함된 Azure PowerShell 모듈의 정식 이름입니다(이름에 포함된 **RM**은 **리소스 관리자**를 나타냄). 여기에는 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있는 수백 개의 cmdlet이 포함되어 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure Active Directory, 컨테이너, 기계 학습 등을 사용할 수 있습니다. 이 모듈은 [GitHub에서 사용할 수 있는](https://github.com/Azure/azure-powershell) 오픈 소스 구성 요소입니다.

> [!NOTE]
> Azure PowerShell 모듈은 선택적 설치입니다. cmdlet은 모듈을 가져올 때까지 사용할 수 없습니다.

### <a name="install-the-azurerm-module"></a>AzureRM 모듈 설치

AzureRM 모듈은 PowerShell 갤러리라는 글로벌 리포지토리에서 사용할 수 있습니다. `Install-Module` 명령을 통해 로컬 머신에 모듈을 설치할 수 있습니다. PowerShell 갤러리에서 모듈을 설치하려면 관리자 권한의 PowerShell 쉘이 필요합니다. 

::: zone pivot="windows"

Azure PowerShell 모듈을 설치하려면 다음 명령을 실행합니다.

1. **시작** 메뉴를 열고 **Windows PowerShell**을 입력합니다.

1. **Windows PowerShell** 아이콘을 마우스 오른쪽 단추로 클릭하고 **관리자 권한으로 실행**을 선택합니다.

1. **사용자 계정 컨트롤** 대화 상자에서 **예**를 선택합니다.

1. 다음 명령을 입력한 다음, Enter 키를 누릅니다.

    ```powershell
    Install-Module -Name AzureRM
    ```

그러면 기본적으로 모든 사용자에 대해 모듈을 설치합니다(범위 매개 변수에 의해 제어됨). 

명령은 NuGet을 사용하여 구성 요소를 검색합니다. 설치한 NuGet 버전에 따라 최신 버전의 NuGet을 다운로드하여 설치하라는 메시지가 표시될 수 있습니다.

```output
NuGet provider is required to continue
PowerShellGet requires NuGet provider version '2.8.5.201' or newer to interact with NuGet-based repositories. The NuGet
 provider must be available in 'C:\Program Files (x86)\PackageManagement\ProviderAssemblies' or
'C:\Users\<username>\AppData\Local\PackageManagement\ProviderAssemblies'. You can also install the NuGet provider by running
'Install-PackageProvider -Name NuGet -MinimumVersion 2.8.5.201 -Force'. Do you want PowerShellGet to install and import
 the NuGet provider now?
```

기본적으로 PowerShell 갤러리는 PowerShellGet에 대해 신뢰할 수 있는 리포지토리로 구성되지 않습니다. PSGallery를 처음 사용할 때는 다음과 같은 메시지가 표시됩니다.

```output
You are installing the modules from an untrusted repository. If you trust this repository, change its
InstallationPolicy value by running the Set-PSRepository cmdlet. Are you sure you want to install the modules from
'PSGallery'?
```

#### <a name="script-execution-failed"></a>스크립트 실행 실패
보안 구성에 따라 `Import-Module`은 다음과 같이 실패할 수 있습니다.

```output
import-module : File C:\Program Files (x86)\WindowsPowerShell\Modules\azurerm\6.8.1\AzureRM.psm1 cannot be loaded
because running scripts is disabled on this system. For more information, see about_Execution_Policies at
https:/go.microsoft.com/fwlink/?LinkID=135170.
At line:1 char:1
+ import-module azurerm
+ ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo          : SecurityError: (:) [Import-Module], PSSecurityException
    + FullyQualifiedErrorId : UnauthorizedAccess,Microsoft.PowerShell.Commands.ImportModuleCommand
```

일반적으로 실행 정책이 "restricted"되었음을 나타냅니다. 즉, PowerShell 갤러리를 비롯한 외부 원본에서 다운로드하는 모듈을 실행할 수 없습니다. `Get-ExecutionPolicy` 명령을 실행하여 대/소문자인지 여부를 확인할 수 있습니다. "Restricted"를 반환하는 경우 다음을 수행합니다.

1. 관리자 권한으로 PowerShell 명령 프롬프트를 엽니다.
1. `SetExecutionPolicy` cmdlet을 사용하여 정책을 "RemoteSigned"로 변경합니다.

```powershell
Set-ExecutionPolicy RemoteSigned
```

그러면 사용 권한을 묻는 프롬프트가 표시됩니다.

```output
The execution policy helps protect you from scripts that you do not trust. Changing the execution policy might expose
you to the security risks described in the about_Execution_Policies help topic at
https:/go.microsoft.com/fwlink/?LinkID=135170. Do you want to change the execution policy?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help (default is "N"): Y
```

`Import-Module`을 사용하여 cmdlet을 로드할 수 있습니다.

:::zone-end

::: zone pivot="linux,macos"

동일한 명령을 사용하여 Linux 또는 macOS에 Azure PowerShell을 설치합니다.

1. 터미널에서 관리자 권한으로 PowerShell Core를 시작하려면 다음 명령을 입력합니다.

    ```bash
    sudo pwsh
    ```

1. Azure PowerShell을 설치하려면 PowerShell Core 프롬프트에서 다음 명령을 실행합니다.

    ```powershell
    Install-Module AzureRM.NetCore
    ```

1. **PSGallery**의 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다.

:::zone-end

### <a name="update-a-module"></a>모듈 업데이트

Azure PowerShell 모듈 버전이 이미 설치되어 있음을 나타내는 경고 또는 오류 메시지가 표시되면 다음 명령을 실행하여 _최신_ 버전으로 업데이트할 수 있습니다.

:::zone pivot="windows"

```powershell
Update-Module -Name AzureRM
```

:::zone-end

::: zone pivot="linux,macos"

```powershell
Update-Module -Name AzureRM.NetCore
```

:::zone-end

`Install-Module` 명령과 마찬가지로, 모듈을 신뢰하는지 묻는 메시지가 표시되면 **예** 또는 **모두 예**를 선택합니다. `Update-Module` 명령을 사용하여 이 문제가 발생하는 경우 모듈을 다시 설치할 수도 있습니다.

## <a name="example-how-to-create-a-resource-group-with-azure-powershell"></a>예제: Azure PowerShell을 사용하여 리소스 그룹을 만드는 방법
Azure 모듈을 로드하면 Azure로 작업을 시작할 수 있습니다. 일반 작업을 수행하겠습니다. 리소스 그룹을 만듭니다. 알아본 대로 리소스 그룹을 사용하여 관련된 리소스를 함께 관리합니다. 새 리소스 그룹을 만드는 것은 새 Azure 솔루션을 시작할 때 수행할 첫 번째 작업 중 하나입니다.

네 단계를 수행해야 합니다.

1. Azure cmdlet을 가져옵니다.

1. Azure 구독에 연결합니다.

1. 리소스 그룹을 만듭니다.

1. 생성이 성공했는지 확인합니다(아래 참조).

다음 그림은 이러한 단계의 개요를 보여줍니다.

![리소스 그룹을 만드는 단계를 보여주는 그림입니다.](../media/5-create-resource-overview.png)

각 단계는 다른 cmdlet에 해당합니다.

### <a name="import-the-azure-cmdlets"></a>Azure cmdlet 가져오기
시작 시 PowerShell은 기본적으로 핵심 cmdlet만 로드합니다. 따라서 Azure에서 작업해야 하는 cmdlet은 로드되지 않습니다. 필요한 cmdlet을 로드하는 가장 신뢰할 수 있는 방법은 PowerShell 세션을 시작할 때 수동으로 가져오는 것입니다.

**Import-Module** cmdlet을 사용하여 모듈을 로드합니다. 이 cmdlet에는 다양한 상황을 처리하는 많은 매개 변수가 있습니다. 예를 들어 여러 모듈, 특정 모듈 버전, 모듈의 일부 등을 로드할 수 있습니다.

예를 들어, **관리자 권한의 PowerShell 세션에서** 다음 명령을 사용하여 AzureRM에 대한 모든 cmdlet을 로드할 수 있습니다.

:::zone pivot="windows"

```powershell
Import-Module AzureRM
```

:::zone-end

::: zone pivot="linux,macos"

```powershell
Import-Module AzureRM.NetCore
```

:::zone-end

> [!TIP]
> Azure PowerShell을 자주 사용하는 경우 모듈 로드 프로세스를 자동화하는 두 가지 방법이 있습니다. PowerShell 프로필에 항목을 추가하여 시작 시 Azure 모듈을 가져오거나, cmdlet을 사용할 때 자동으로 포함된 모듈을 로드하는 최신 버전의 PowerShell을 사용할 수 있습니다.

### <a name="connect"></a>연결
Azure PowerShell의 로컬 설치를 사용하는 경우 Azure 명령을 실행하기 전에 먼저 인증해야 합니다. **Connect-AzureRmAccount** cmdlet은 Azure 자격 증명을 묻는 메시지를 표시한 다음, Azure 구독에 연결합니다. 여기에는 많은 선택적 매개 변수가 있지만, 대화형 프롬프트만 필요한 경우에는 매개 변수가 필요하지 않습니다.

```powershell
Connect-AzureRmAccount
```

이 모듈이 핵심 집합의 일부가 아니므로 모든 새 PowerShell 세션에 대해 이러한 단계를 반복해야 합니다.


### <a name="working-with-subscriptions"></a>구독 작업
Azure를 처음 접하는 경우 아마도 단일 구독만 보유할 것입니다. 하지만 한동안 Azure를 사용한 경우 Azure 구독을 여러 개 만들었을 수 있습니다. 특정 구독에 대해 명령을 실행하도록 Azure PowerShell을 구성할 수 있습니다.

한 번에 하나의 구독에서만 작업할 수 있습니다. `Get-AzureRmContext` cmdlet을 사용하여 활성 구독을 확인합니다. 이 올바른 구독이 아닌 경우 변경할 수 있습니다.

1. `Get-AzureRmSubscription` 명령을 사용하여 계정에 모든 구독 이름 목록을 가져옵니다. 

2. 선택한 구독 이름을 전달하여 구독을 변경합니다.

```powershell
Select-AzureRmSubscription -Subscription "Visual Studio Enterprise"
```

### <a name="get-a-list-of-all-resource-groups"></a>모든 리소스 그룹 목록 가져오기

활성 구독에서 모든 리소스 그룹 목록을 검색할 수 있습니다.

```powershell
Get-AzureRmResourceGroup
```

보다 간결하게 표시하려면 파이프 '|'를 사용하여 `Get-AzureRmResourceGroup`의 출력을 `Format-Table` cmdlet으로 보낼 수 있습니다.

```powershell
Get-AzureRmResourceGroup | Format-Table
```

그러면 다음과 같이 출력됩니다.

```output
ResourceGroupName                  Location       ProvisioningState Tags TagsTable ResourceId
-----------------                  --------       ----------------- ---- --------- ----------
cloud-shell-storage-southcentralus southcentralus Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
ExerciseResources                  eastus         Succeeded                        /subscriptions/xxxxxxxx-d3ce-4172...
```

### <a name="create-a-resource-group"></a>리소스 그룹 만들기

알아본 대로 Azure에서 리소스를 만드는 경우 항상 관리 목적을 위해 리소스 그룹에 배치합니다. 리소스 그룹은 새 응용 프로그램을 시작할 때 만들 첫 번째 작업 중 하나입니다.

`New-AzureRmResourceGroup` cmdlet을 사용하여 리소스 그룹을 만들 수 있습니다. 이름 및 위치를 지정해야 합니다. 이름은 구독 내에서 고유해야 합니다. 위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다(규정 준수에 중요할 수 있음). "미국 서부", "북유럽" 또는 "인도 서부"와 같은 문자열을 사용하여 위치를 지정합니다. 대부분의 Azure cmdlet과 마찬가지로 `New-AzureRmResourceGroup`에는 많은 선택적 매개 변수가 있지만 핵심 구문은 다음과 같습니다.

```powershell
New-AzureRmResourceGroup -Name <name> -Location <location>
```

> [!NOTE]
> 리소스 그룹을 만드는 Azure 샌드박스에서 작업할 예정입니다. 위의 명령은 고유한 구독에서 작업하는 경우에 사용됩니다.

### <a name="verify-the-resources"></a>리소스 확인
`Get-AzureRmResource`는 Azure 리소스를 나열합니다. 이 cmdlet은 리소스 그룹 생성에 성공했는지 여부를 확인하는 데 유용합니다.

```powershell
Get-AzureRmResource
```

`Get-AzureRmResourceGroup` 명령과 같이 `Format-Table` cmdlet을 통해 좀 더 간략히 볼 수 있습니다. 여기에서는 약식 버전 `ft`을 사용합니다.

```powershell
Get-AzureRmResource | ft
```

특정 리소스 그룹으로 필터링하여 그룹과 연결된 리소스만 나열할 수 있습니다.

```powershell
Get-AzureRmResource -ResourceGroup ExerciseResources
```

### <a name="creating-an-azure-virtual-machine"></a>Azure Virtual Machine 만들기

PowerShell을 사용하여 수행할 수 있는 일반적인 작업은 다른 VM을 만드는 것입니다.

Azure PowerShell은 가상 머신을 만드는 `New-AzureRmVm` cmdlet을 제공합니다. 이 cmdlet에는 많은 VM 구성 설정을 처리할 수 있는 여러 매개 변수가 있습니다. 대부분의 매개 변수에 적절한 기본값이 있으므로 다음 5개 매개 변수만 지정하면 됩니다.

- **ResourceGroupName**: 새 VM이 배치될 리소스 그룹입니다.
- **Name**: Azure의 VM 이름입니다.
- **Location**: VM이 프로비전될 지리적 위치입니다.
- **Credential**: VM 관리자 계정의 사용자 이름과 암호를 포함하는 개체입니다. `Get-Credential` cmdlet을 사용하겠습니다. 이 cmdlet은 사용자 이름 및 암호를 묻는 메시지를 표시하고 자격 증명 개체에 패키지합니다.
- **Image**: VM에 사용할 운영 체제 이미지입니다. Linux 배포 또는 Windows Server인 경우가 많습니다.

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

위에 표시된 대로 이러한 매개 변수를 cmdlet에 직접 제공할 수 있습니다. 또는 `Set-AzureRmVMOperatingSystem`, `Set-AzureRmVMSourceImage`, `Add-AzureRmVMNetworkInterface` 및 `Set-AzureRmVMOSDisk`와 같은 가상 머신을 구성하는 데 다른 cmdlet를 사용할 수 있습니다.

`-Credential` 매개 변수와 함께 `Get-Credential` cmdlet을 이어 놓은 예제는 다음과 같습니다.

```powershell
New-AzureRmVM -Name MyVm -ResourceGroupName ExerciseResources -Credential (Get-Credential) ...
```

`AzureRmVM` 접미사는 PowerShell의 VM 기반 명령에 따라 다릅니다. 사용할 수 있는 다른 방법은 다음과 같습니다.

| 명령 | 설명 |
|---------|-------------|
| `Remove-AzureRmVM` | Azure VM을 삭제합니다. |
| `Start-AzureRmVM` | 중지된 VM을 시작합니다. |
| `Stop-AzureRmVM` | 실행 중인 VM을 중지합니다. |
| `Restart-AzureRmVM` | VM을 다시 시작합니다. |
| `Update-AzureRmVM` | VM에 대한 구성을 업데이트합니다. |

#### <a name="example-getting-the-information-for-a-vm"></a>예제: VM에 대한 정보 가져오기

`Get-AzureRmVM -Status` 명령을 사용하여 구독에서 VM을 표시할 수 있습니다. `-Name` 속성을 사용하여 VM을 지정할 수도 있습니다. 여기에서는 PowerShell 변수에 할당합니다.

```powershell
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName ExerciseResources
```

흥미로운 것은 상호 작용할 수 있는 _개체_라는 점입니다. 예를 들어, 해당 개체를 사용하고, 변경한 다음, `Update-AzureRmVM` 명령을 사용하여 Azure에 변경 내용을 다시 푸시할 수 있습니다.

```powershell
$ResourceGroupName = "ExerciseResources"
$vm = Get-AzureRmVM  -Name MyVM -ResourceGroupName $ResourceGroupName
$vm.HardwareProfile.vmSize = "Standard_DS3_v2"

Update-AzureRmVM -ResourceGroupName $ResourceGroupName  -VM $vm
```

PowerShell의 대화형 모드는 일회성 작업에 적합합니다. 예제에서는 프로젝트 수명 동안 동일한 리소스 그룹을 사용할 가능성이 높으므로 대화형으로 만드는 것이 좋습니다. 이 작업에는 스크립트를 작성하고 해당 스크립트를 한 번만 실행하는 것보다 대화형 모드를 사용하는 것이 더 빠르고 편리한 경우가 많습니다.