대체로, 복잡하거나 반복적인 작업을 관리하려면 오랜 시간이 걸립니다. 조직은 이러한 작업을 자동화하여 비용을 줄이고 오류를 방지하려고 합니다.

이는 CRM(고객 관계 관리) 회사 예제에서 중요합니다. 해당 예제에서는 계속해서 삭제하고 다시 만들어야 하는 소프트웨어를 여러 Linux VM(Virtual Machines)에서 테스트합니다. PowerShell 스크립트를 사용하여 VM 생성을 자동화하려고 합니다.

VM을 만드는 핵심 작업 외에도 스크립트에 대한 몇 가지 추가 요구 사항이 있습니다. 
- 여러 개의 VM을 만들기 때문에 생성 작업을 루프 안에 넣으려고 합니다.
- 세 개의 리소스 그룹에 VM을 만들어야 하므로 리소스 그룹 이름이 스크립트에 매개 변수로 전달되어야 합니다.

이 섹션에서는 이러한 요구 사항을 충족하는 Azure PowerShell 스크립트를 작성하고 실행하는 방법을 설명합니다.

## <a name="what-is-a-powershell-script"></a>PowerShell 스크립트란?
PowerShell 스크립트는 명령 및 제어 구문을 포함하는 텍스트 파일입니다. 명령은 cmdlet 호출입니다. 제어 구문은 PowerShell에서 제공하는 루프, 변수, 매개 변수, 주석 등의 프로그래밍 기능입니다.

PowerShell 스크립트 파일에는 **.ps1** 파일 확장명이 있습니다. 텍스트 편집기를 사용하여 이러한 파일을 만들고 저장할 수 있습니다. 

> [!TIP]
> Windows에서 PowerShell 스크립트를 작성하는 경우 Windows PowerShell ISE(통합 스크립팅 환경)를 사용할 수 있습니다. 이 편집기는 구문 색 지정, 사용 가능한 cmdlet 목록 등의 기능을 제공합니다.
>
다음 스크린샷은 Azure에 연결하고 Azure에서 가상 머신을 만들기 위한 샘플 스크립트를 포함하는 Windows PowerShell ISE(통합 스크립팅 환경)를 보여 줍니다.

>![가상 머신을 만드는 스크립트가 편집 창에서 열려 있는 Windows PowerShell 통합 스크립팅 환경 스크린샷](../media/7-windows-powershell-ise-screenshot.png)

스크립트를 작성한 후 파일 이름 앞에 점과 백슬래시를 추가해서 전달하여 PowerShell 명령줄에서 스크립트를 실행합니다.

```powershell
.\myScript.ps1
```

## <a name="powershell-techniques"></a>PowerShell 기술
PowerShell에는 일반 프로그래밍 언어에서 제공되는 많은 기능이 있습니다. 변수를 정의하고, 분기 및 루프를 사용하고, 명령줄 매개 변수를 캡처하고, 함수를 작성하고, 주석을 추가할 수 있습니다. 예제 스크립트에는 변수, 루프 및 매개 변수의 세 가지 기능이 필요합니다.

### <a name="variables"></a>variables
PowerShell은 변수를 지원합니다. **$** 를 사용하여 변수를 선언하고, **=** 를 사용하여 값을 할당합니다. 예:

```powershell
$loc = "East US"
$iterations = 3
```

변수는 개체 포함할 수 있습니다. 예를 들어 다음 정의는 **adminCredential** 변수를 **Get-Credential** cmdlet에서 반환된 개체로 설정합니다.

```powershell
$adminCredential = Get-Credential
```

변수에 저장된 값을 얻으려면 아래와 같이 **$** 접두어 및 해당 이름을 사용하세요. 

```powershell
$loc = "East US"
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location $loc
```

### <a name="loops"></a>루프
PowerShell에는 **For**, **Do...While**, **For...Each** 등의 여러 루프가 있습니다. 예제에서는 고정된 횟수만큼 cmdlet을 실행하므로 **For** 루프가 요구에 가장 적합합니다.

코어 구문은 아래에 나와 있습니다. 예제는 두 개의 반복을 실행하고 매번 **i** 값을 출력합니다. 비교 연산자는 **-lt**(“보다 작음”), **-le**(“작거나 같음”), **eq**(“같음”), **ne**(“같지 않음”) 등으로 작성됩니다.

```powershell
For ($i = 1; $i -lt 3; $i++)
{
    $i
}
```

### <a name="parameters"></a>매개 변수
스크립트를 실행할 때 명령줄에서 인수를 전달할 수 있습니다. 스크립트가 값을 추출하는 데 도움이 되도록 각 매개 변수의 이름을 지정할 수 있습니다. 예: 

```powershell
.\setupEnvironment.ps1 -size 5 -location "East US"
```

스크립트 내에서 값을 변수에 캡처합니다. 이 예제에서는 매개 변수가 이름으로 일치됩니다.

```powershell
param([string]$location, [int]$size)
```

명령줄에서 이름을 생략할 수 있습니다. 예: 

```powershell
.\setupEnvironment.ps1 5 "East US"
```

스크립트 내에서 매개 변수가 명명되지 않은 경우 위치를 일치에 사용합니다.

```powershell
param([int]$size, [string]$location)
```

## <a name="how-to-create-a-linux-virtual-machine"></a>Linux 가상 머신을 만드는 방법
Azure PowerShell은 가상 머신을 만드는 **New-AzureRmVm** cmdlet을 제공합니다. 이 cmdlet에는 많은 VM 구성 설정을 처리할 수 있는 여러 매개 변수가 있습니다. 대부분의 매개 변수에 적절한 기본값이 있으므로 다음 5개 매개 변수만 지정하면 됩니다.

- **ResourceGroupName**: 새 VM이 배치될 리소스 그룹입니다.
- **Name**: Azure의 VM 이름입니다.
- **Location**: VM이 프로비전될 지리적 위치입니다.
- **Credential**: VM 관리자 계정의 사용자 이름과 암호를 포함하는 개체입니다. 여기서는 **Get-Credential** cmdlet을 사용하여 사용자 이름과 암호를 묻는 메시지를 표시합니다. **Get-Credential**은 사용자 이름과 암호를 자격 증명 개체로 패키징하고 결과로 반환합니다.
- **Image**: VM에 사용할 운영 체제의 ID입니다. 여기서는 “UbuntuLTS”를 사용합니다.

cmdlet 구문은 다음과 같습니다.

```powershell
   New-AzureRmVm 
       -ResourceGroupName <resource group name> 
       -Name <machine name> 
       -Credential <credentials object> 
       -Location <location> 
       -Image <image name>
```

## <a name="summary"></a>요약
PowerShell 및 Azure PowerShell을 조합하면 Azure를 자동화하는 데 필요한 모든 도구가 제공됩니다. CRM 예제에서는 매개 변수를 사용해서 스크립트를 제네릭으로 유지하고 루프를 사용해서 반복 코드를 방지하여 여러 개의 Linux VM을 만들 수 있습니다. 이는 이전의 복잡한 작업을 이제 하나의 단계로 실행할 수 있음을 의미합니다.