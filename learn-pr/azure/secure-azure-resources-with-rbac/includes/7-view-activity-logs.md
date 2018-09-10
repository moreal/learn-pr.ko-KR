First Up Consultants에서는 감사 및 문제 해결을 위해 RBAC(역할 기반 액세스 제어) 변경 사항을 분기별로 검토합니다. 아시다시피 변경 사항은 [Azure 활동 로그](/azure/monitoring-and-diagnostics/monitoring-overview-activity-logs)에 로깅됩니다. 관리자가 귀하에게 지난달의 역할 할당 및 사용자 지정 역할 변경 사항에 대한 보고서를 생성해 줄 수 있는지 물었습니다.

## <a name="view-activity-logs"></a>활동 로그 보기

가장 손쉽게 시작할 수 있는 방법은 Azure Portal을 사용하여 활동 로그를 보는 것입니다.

1. **모든 서비스**를 클릭한 다음, **활동 로그**를 찾습니다.

    ![포털을 사용한 활동 로그](../media-draft/7-all-services-activity-log.png)

1. **활동 로그**를 클릭합니다.

    ![포털을 사용한 활동 로그](../media-draft/7-activity-log-portal.png)

1. **시간 간격** 필터를 **지난달**로 설정합니다.

1. **이벤트 범주** 필터를 **관리**로 설정합니다.

1. **작업** 필터에서 **역할**을 입력하여 목록을 필터링합니다.

1. 다음 RBAC 작업을 선택합니다.

    - 역할 할당 만들기(roleAssignments)
    - 역할 할당 삭제(roleAssignments)
    - 사용자 지정 역할 정의 만들기 또는 업데이트(roleDefinitions)
    - 사용자 지정 역할 정의 삭제(roleDefinitions)

    ![작업 필터](../media-draft/7-operation-filter.png)

1. **적용**을 클릭하여 필터를 적용합니다.

    지난달의 모든 역할 할당 및 역할 정의 작업이 표시됩니다. 또한 활동 로그를 CSV 파일로 다운로드하는 링크도 포함되어 있습니다.

    ![RBAC 활동 로그](../media-draft/7-activity-log-portal-filter.png)

## <a name="end-lab"></a>랩 종료

1. 랩을 종료하려면 이 창의 오른쪽 위 모서리에 있는 햄버거 메뉴를 클릭한 다음, **종료**를 클릭합니다.

1. **예, 랩을 종료합니다**를 클릭합니다.

## <a name="summary"></a>요약

이 단원에서는 Azure 활동 로그를 사용하여 포털의 RBAC 변경 사항을 나열하고 간단한 보고서를 생성하는 방법을 알아보았습니다.
