Linux 관리 도구 모음을 만드는 회사에서 일한다고 가정해 보겠습니다. 담당 업무는 잠재 고객이 소프트웨어를 구입하기 전에 사용해 보도록 지원하는 것입니다. 소프트웨어는 루트 수준에서 OS를 변경하므로 각 평가판 고객을 위한 Linux VM을 만들기로 했습니다. 필요에 따라 VM을 만들고 평가판 구독이 끝나면 해당 VM을 삭제합니다. 이런 식으로 각 고객은 초기 버전의 OS로 시작합니다. 

이러한 VM을 회사에서 내부 테스트용으로 사용하는 VM과구분하려면 VM을 포함할 전용 리소스 그룹을 만듭니다. 리소스 그룹은 하나만 필요하므로 대화형 모드의 Azure PowerShell을 이 작업에 사용하는 것이 합리적입니다.

## <a name="steps-to-create-a-resource-group"></a>리소스 그룹을 만드는 단계
<!---TODO: Update for sandbox.--->

1. PowerShell을 시작합니다.

1. Azure cmdlet에 액세스할 수 있도록 모듈을 현재 세션으로 가져옵니다.

   ```powershell
   Import-Module AzureRM
   ```

1. 아래 표시된 명령을 사용하여 Azure에 연결합니다. 명령을 입력한 후 Azure 자격 증명을 제공하여 인증합니다.

   ```powershell
   Connect-AzureRmAccount
   ```

1. 리소스 그룹을 만듭니다.

    ```powershell
    New-AzureRmResourceGroup -Name "TrialsResourceGroup" -Location "East US"
    ```

1. 리소스 그룹이 성공적으로 만들어졌는지 확인합니다.

    ```powershell
    Get-AzureRmResource | Format-Table
    ```

리소스 그룹이 성공적으로 만들어졌는지 확인하는 또 다른 방법은 Azure Portal을 사용하는 것입니다. 이렇게 하려면 포털에 로그인하고 **리소스 그룹** 섹션(아래 참조)으로 이동합니다. 새 리소스 그룹이 목록에 표시되어야 합니다.

다음 스크린샷은 Azure Portal에서 리소스 그룹 범주의 위치를 보여 줍니다.

![리소스 그룹 범주가 강조 표시된 Azure Portal 즐겨찾기 블레이드의 스크린샷입니다.](../media/6-listing-resource-groups.png)

## <a name="summary"></a>요약
이 연습에서는 대화형 PowerShell 세션의 일반적인 패턴을 보여 줍니다. 표준 cmdlet을 사용하여 AzureRM 모듈을 가져온 후에 Azure PowerShell cmdlet을 사용하여 특정 작업을 수행했습니다. 이제 구독에 리소스 그룹이 있으며 VM을 만들 준비가 되었습니다.