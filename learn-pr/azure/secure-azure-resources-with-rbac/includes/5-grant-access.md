First Up Consultants의 Alain이라는 동료가 현재 진행 중인 프로젝트를 위한 가상 머신을 만들고 관리할 수 있는 기능을 필요로 합니다. 관리자가 귀하에게 이 요청을 처리해 달라고 요청했습니다. 모범 사례를 사용 하 여 작업을 완료 하려면 최소한의 권한을 사용자에 게 부여를 Alain 리소스 그룹에 대 한 Virtual Machine 참여자 역할을 할당 하려면 하기로 했습니다.

## <a name="sign-in-to-the-azure-portal"></a>Azure Portal에 로그인

- Azure Portal에 여전히 **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_.onmicrosoft.com**으로 로그인되어 있는지 확인합니다. 이 창의 상단에 있는 **리소스** 탭에서 사용자 이름과 암호를 확인할 수 있습니다.

## <a name="grant-access"></a>액세스 권한 부여

리소스 그룹 범위에서 사용자에게 Virtual Machine 기여자 역할을 할당하려면 다음 단계를 따르세요.

1. 탐색 목록에서 **리소스 그룹**을 클릭합니다.

1. **FirstUpConsultantsRG1-_XXXXXXX_** 리소스 그룹을 찾아 클릭합니다.

1. **액세스 제어(IAM)** 를 클릭하면 현재 역할 할당 목록을 볼 수 있습니다.

   ![액세스 제어-리소스 그룹에 대 한 역할 할당](../media/5-resource-group-role-assignment.png)

1. 상단에서 **추가**를 클릭하여 **권한 추가** 창을 엽니다.

   ![권한 추가 창](../media/5-add-permissions.png)

1. **역할** 드롭다운 목록에서 **Virtual Machine 기여자**를 선택합니다.

1. **선택** 목록에서 **LabUser-_XXXXXXX_** 를 선택합니다.

   ![완성된 권한 추가 창](../media/5-add-permissions-save.png)

1. **저장**을 클릭하여 역할 할당을 만듭니다.

   잠시 후 **LabUser-_XXXXXXX_** 사용자에게 **FirstUpConsultantsRG1-_XXXXXXX_** 리소스 그룹 범위의 Virtual Machine 기여자 역할이 할당됩니다. 이제 사용자는 이 리소스 그룹 내에서만 가상 머신을 만들고 관리할 수 있습니다.

   ![Virtual Machine 기여자 역할 할당](../media/5-vm-contributor-assignment.png)

## <a name="remove-access"></a>액세스 권한 제거

RBAC에서 액세스 권한을 제거하려면 역할 할당을 제거해야 합니다.

1. 역할 할당 목록에서 Virtual Machine 기여자 역할이 할당된 **LabUser-_XXXXXXX_** 사용자를 선택합니다.

1. **제거**를 클릭합니다.

   ![역할 할당 제거 메시지](../media/5-remove-role-assignment.png)

1. **표시되는 역할 할당 제거** 메시지에서 **예**를 클릭합니다.

## <a name="summary"></a>요약

이 단원에서는 Azure Portal을 사용하여 리소스 그룹에 가상 머신을 만들고 관리할 수 있는 액세스 권한을 사용자에게 부여하는 방법을 알아보았습니다. 다음 단원에서는 시간별 RBAC 변경 사항을 확인하는 방법을 알아봅니다.
