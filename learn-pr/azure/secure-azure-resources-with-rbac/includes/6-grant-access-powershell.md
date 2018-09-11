귀하는 Azure Portal에서 **IAM(액세스 제어)** 블레이드를 문제 없이 사용해 왔지만 매일 여러 건의 권한 요청을 받고 있습니다. 액세스 관리 작업을 처리하기 위해 PowerShell을 사용하여 일부 단계를 자동화하기로 합니다.

## <a name="open-cloud-shell-powershell"></a>Cloud Shell PowerShell 열기

1. Azure Portal에 여전히 **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**으로 로그인되어 있는지 확인합니다. 이 창의 상단에 있는 **리소스** 탭에서 사용자 이름과 암호를 확인할 수 있습니다.

1. 포털 상단에서 **Cloud Shell**을 클릭하여 Cloud Shell 창을 엽니다.

    ![Cloud Shell 단추](../media-draft/6-cloud-shell-button.png)

1. Cloud Shell 창 왼쪽 상단에서 **PowerShell**로 설정되어 있는지 확인합니다. **Bash**로 설정된 경우 **PowerShell**로 변경합니다.

    로드하는 데 잠시 시간이 걸릴 수 있습니다. 완료되면 다음과 비슷한 모습이 될 것입니다.

    ![Cloud Shell PowerShell](../media-draft/6-cloud-shell-powershell.png)

## <a name="grant-access"></a>액세스 권한 부여

Azure PowerShell을 사용하여 사용자에게 액세스 권한을 부여하려면 [New-AzureRmRoleAssignment](/powershell/module/azurerm.resources/new-azurermroleassignment) 명령을 사용합니다. 보안 주체, 역할 정의 및 범위를 지정해야 합니다.

리소스 그룹 범위에서 **LabUser-_XXXXXXX_** 사용자에게 Virtual Machine 기여자 역할을 할당하려면 다음 단계를 따르세요.

1. 이 창의 상단에 있는 **리소스** 탭에서 **PowerShell에 액세스 권한 부여** 명령을 복사합니다.

1. PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다. 다음은 명령 예제와 출력을 보여줍니다.

    ```Example
    PS Azure:\> New-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    이 출력은 Virtual Machine 기여자 역할이 FirstUpConsultantsRG1-_XXXXXXX_ 범위의 LabUser-_XXXXXXX_에게 할당되었음을 보여줍니다.

## <a name="list-access"></a>액세스 권한 나열

리소스 그룹에 대한 액세스 권한을 확인하려면 [Get-AzureRmRoleAssignment](/powershell/module/azurerm.resources/get-azurermroleassignment) 명령을 사용하여 역할 할당을 나열합니다.

리소스 그룹 범위에서 **LabUser-XXXXXXX** 사용자에게 할당된 모든 역할을 나열하려면 다음 단계를 따르세요.

1. 이 창의 상단에 있는 **리소스** 탭에서 **PowerShell 액세스 권한 나열** 명령을 복사합니다.

1. PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다. 다음은 명령 예제와 출력을 보여줍니다.

    ```Example
    PS Azure:\> Get-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"

    RoleAssignmentId   : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX/providers/Microsoft.Authorization/roleAssignments/33333333-3333-3333-3333-333333333333
    Scope              : /subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/FirstUpConsultantsRG1-XXXXXXX
    DisplayName        : LabUser-XXXXXXX
    SignInName         : LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com 
    RoleDefinitionName : Virtual Machine Contributor
    RoleDefinitionId   : 9980e02c-c2be-4d73-94e8-173b1dc7cf3c
    ObjectId           : 11111111-1111-1111-1111-111111111111
    ObjectType         : User
    CanDelegate        : False
    ```

    이 출력은 Virtual Machine 기여자 역할이 FirstUpConsultantsRG1-_XXXXXXX_ 범위의 LabUser-_XXXXXXX_에게 할당되었음을 보여줍니다.

    Azure Portal에서 리소스 그룹의 **IAM(액세스 제어)** 블레이드를 새로 고치면 다음과 같이 역할이 할당됩니다.

    ![리소스 그룹에서 사용자의 역할 할당](../media-draft/6-cloud-shell-access-control.png)

## <a name="remove-access"></a>액세스 권한 제거

사용자, 그룹 및 응용 프로그램의 액세스 권한을 제거하려면 [Remove-AzureRmRoleAssignment](/powershell/module/azurerm.resources/remove-azurermroleassignment) 명령을 사용하여 역할 할당을 제거합니다.

리소스 그룹 범위에서 **LabUser-_XXXXXX_** 사용자에게 할당된 Virtual Machine 기여자 역할을 제거하려면 다음 단계를 따르세요.

1. 이 창의 상단에 있는 **리소스** 탭에서 **PowerShell 액세스 권한 제거** 명령을 복사합니다.

1. PowerShell 창에 명령을 붙여넣고 Enter 키를 눌러 실행합니다. 다음은 예제 명령입니다.

    ```Example
    PS Azure:\> Remove-AzureRmRoleAssignment -SignInName LabUser-XXXXXXX@xxxxxxxxxxxx.onmicrosoft.com `
      -RoleDefinitionName "Virtual Machine Contributor" `
      -ResourceGroupName "FirstUpConsultantsRG1-XXXXXXX"
    ```

1. PowerShell 창에서 닫기(**X**) 단추를 클릭하여 창을 닫습니다.

    ![Cloud Shell 닫기 단추](../media-draft/6-cloud-shell-close.png)


## <a name="summary"></a>요약

이 단원에서는 Azure PowerShell을 사용하여 리소스 그룹에 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여하는 방법을 알아보았습니다. 다음 단원에서는 시간별 RBAC 변경 사항을 확인하는 방법을 알아봅니다.
