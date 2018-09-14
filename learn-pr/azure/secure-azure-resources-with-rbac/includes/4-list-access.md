첫 번째 등록 컨설턴트에 부여 된 액세스 마케팅 팀에 대 한 리소스 그룹에 있습니다. 귀하는 Azure Portal 사용법을 숙지하고 현재 할당된 역할을 확인하려고 합니다.

## <a name="launch-lab-and-sign-in-to-the-azure-portal"></a>Azure portal에 로그인 하 고 랩 시작

1. 랩 시작 하려면 위의 링크를 클릭 합니다.

1. Azure portal에 로그인 **LabAdmin-_XXXXXXX_@_xxxxxxxxxxxx_. onmicrosoft.com**합니다. 이 창의 상단에 있는 **리소스** 탭에서 사용자 이름과 암호를 확인할 수 있습니다.

## <a name="list-role-assignments-for-yourself"></a>사용자에 대한 역할 할당 목록

현재 사용자에게 할당된 역할을 확인하려면 다음 단계를 수행합니다.

1. Azure portal의 오른쪽 위 모퉁이에서 메뉴를 열고 하려면 사용자 이름을 클릭 합니다.

    ![내 사용 권한 메뉴](../media/4-my-permissions-menu.png)

1. 클릭 **내 사용 권한** 열려는 내 권한 창입니다.

    ![내 권한 창](../media/4-my-permissions-pane.png)

    에 내 권한 창 범위 및 할당 된 역할 목록을 볼 수 있습니다. 목록은 사용자별로 다르게 표시될 수 있습니다.

## <a name="list-role-assignments-for-a-resource-group"></a>리소스 그룹에 대한 역할 할당 목록

리소스 그룹 범위에서 할당된 역할을 확인하려면 다음 단계를 수행합니다.

1. 탐색 목록에서 **리소스 그룹**을 클릭합니다.

   ![리소스 그룹](../media/4-resource-groups.png)

1. 찾기 및 명명 된 리소스 그룹을 클릭 **FirstUpConsultantsRG1-_XXXXXXX_** 합니다.

1. **액세스 제어(IAM)** 를 클릭합니다.

   ![리소스 그룹에 대 한 액세스 제어](../media/4-resource-group-access-control.png)

1. 클릭 **역할 할당**합니다.

    이 리소스 그룹에 대 한 액세스 권한이 있는 사용자를 볼 수 있습니다. 일부 역할의 범위는 **이 리소스**이지만 나머지는 부모 범위에서 **(상속)** 됩니다.

   ![액세스 제어-리소스 그룹에 대 한 역할 할당](../media/4-resource-group-role-assignment.png)

## <a name="list-roles"></a>역할 나열

이전 단원에서 살펴본 것처럼 역할은 권한 컬렉션입니다. Azure에는 역할 할당에 사용할 수 있는 기본 제공 역할이 70개 이상 있습니다. 역할을 나열 하려면이 단계를 수행 합니다.

- 역할 할당, 클릭 **역할** 모든 기본 및 사용자 지정 역할의 목록을 보려면.

   각 역할에 할당된 사용자 및 그룹 수를 볼 수 있습니다.

   ![역할 목록](../media/4-roles-list.png)

## <a name="summary"></a>요약

이 단원에서는 Azure Portal에서 직접 역할 할당을 나열하는 방법을 알아보았습니다. 리소스 그룹에 대 한 역할 할당을 나열 하는 방법을 알아보았습니다. 다음 단원에서는 다음 단계로 가서 RBAC를 사용하여 사용자에게 액세스 권한을 부여합니다.
