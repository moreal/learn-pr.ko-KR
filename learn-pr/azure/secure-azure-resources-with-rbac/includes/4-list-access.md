귀하는 First Up Consultants에서 마케팅 팀의 Azure 구독 액세스 권한을 부여받았습니다. 귀하는 Azure Portal 사용법을 숙지하고 현재 할당된 역할을 확인하려고 합니다.

## <a name="list-role-assignments-for-yourself"></a>사용자에 대한 역할 할당 목록

현재 사용자에게 할당된 역할을 확인하려면 다음 단계를 따릅니다.

1. [Azure Portal](https://portal.azure.com/?azure-portal=true)로 이동합니다.

1. 탐색 목록에서 **Azure Active Directory**를 클릭합니다.

1. **사용자**를 클릭하여 **모든 사용자**를 엽니다.

    ![Azure Active Directory 사용자](../media-draft/4-aad-all-users.png)

1. **LabAdmin-_XXXXXXX_** 사용자 이름을 찾아 클릭합니다.

    ![Azure Active Directory 랩 사용자](../media-draft/4-aad-all-users-lab.png)

1. **관리** 섹션에서 **Azure 리소스**를 클릭합니다.

    ![Azure 리소스](../media-draft/4-aad-user-azure-resources.png)

    Azure 리소스 블레이드에서 액세스 가능한 리소스와 역할을 확인할 수 있습니다. 목록은 사용자별로 다르게 표시될 수 있습니다.

## <a name="list-role-assignments-for-a-resource-group"></a>리소스 그룹에 대한 역할 할당 목록

리소스 그룹 범위에서 할당된 역할을 확인하려면 다음 단계를 수행합니다.

1. 탐색 목록에서 **리소스 그룹**을 클릭합니다.

   ![리소스 그룹](../media-draft/4-resource-groups.png)

1. **FirstUpConsultantsRG1-_XXXXXXX_** 라는 리소스 그룹을 클릭합니다.

1. **액세스 제어(IAM)** 를 클릭합니다.

   액세스 제어(IAM) 블레이드에서 이 리소스 그룹에 대한 액세스 권한이 있는 사용자를 볼 수 있습니다. 일부 역할의 범위는 **이 리소스**이지만 나머지는 부모 범위에서 **(상속)** 됩니다.

   ![리소스 그룹의 액세스 제어(IAM)](../media-draft/4-resource-group-access-control.png)

## <a name="list-roles"></a>역할 나열

이전 단원에서 살펴본 것처럼 역할은 권한 컬렉션입니다. Azure에는 역할 할당에 사용할 수 있는 기본 제공 역할이 70개 이상 있습니다. 역할을 나열하려면 다음 단계를 따르세요.

- 액세스 제어(IAM) 블레이드 맨 위에 있는 **역할**을 클릭하여 모든 기본 제공 역할 및 사용자 지정 역할의 목록을 봅니다.

   ![역할 옵션](../media-draft/4-roles-option.png)

   각 역할에 할당된 사용자 및 그룹 수를 볼 수 있습니다.

   ![역할 목록](../media-draft/4-roles-list.png)

## <a name="summary"></a>요약

이 단원에서는 Azure Portal에서 직접 역할 할당을 나열하는 방법을 알아보았습니다. 또한 서로 다른 범위에서 역할 할당을 나열하는 방법도 알아보았습니다. 다음 단원에서는 다음 단계로 가서 RBAC를 사용하여 사용자에게 액세스 권한을 부여합니다.
