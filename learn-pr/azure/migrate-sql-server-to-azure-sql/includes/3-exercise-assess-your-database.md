이 단원에서는 Data Migration Assistant를 사용하여 기존 데이터베이스를 평가하고, 로컬 SQL Server 인스턴스에서 사용되었지만 현재 Azure SQL Database에서는 지원되지 않는 기능을 검토합니다.

## <a name="setup"></a>설정

1. [**Data Migration Assistant**](https://www.microsoft.com/download/details.aspx?id=53595)를 아직 설치하지 않았으면 설치합니다.

1. SQL Server 인스턴스가 실행 중이어야 합니다. 연결 세부 정보를 사용할 수 있는지 확인하세요.

<!-- 1. [**** likely replace with an LOD VM *****] TODO: -->

1. 인터넷 브라우저를 시작하여 https://docs.microsoft.com/sql/samples/adventureworks-install-configure?view=sql-server-2017로 이동합니다.

1. **OLTP 다운로드**에서 **AdventureWorks2008R2.bak**를 클릭하여 로컬 컴퓨터에 해당 파일을 저장합니다.

1. Management Studio에서 *AdventureWorks 2008R2*를 기본 인스턴스로 복원합니다.

## <a name="create-an-assessment"></a>평가 만들기

1. **Microsoft Data Migration Assistant**를 시작합니다.

1. 앱의 왼쪽 탐색 영역에서 __+__ 를 클릭하여 새 Data Migration Assistant 프로젝트를 만듭니다.

1. 다음 옵션을 지정합니다.

    - **프로젝트 형식** - *평가*를 선택합니다.
    - **프로젝트 이름** - 프로젝트 이름을 "자전거 DB 평가"와 같이 입력합니다.
    - **원본 서버 유형** - *SQL Server*를 선택합니다.
    - **대상 서버 유형** - *Azure SQL Database*를 선택합니다.

1. **만들기**를 클릭합니다.
    ![AdventureWorks SQL Server 데이터에 대해 설명한 구성이 적용된 Data Migration Assistant를 보여 주는 스크린샷.](../media-draft/3-create-assessment.png)

1. 평가 보고서 종류를 선택합니다. 다음 두 항목을 모두 선택합니다.
    - 데이터베이스 호환성 확인
    - 기능 패리티 확인

1. **다음**을 클릭합니다.

## <a name="add-databases-to-assess"></a>평가할 데이터베이스 추가

1. **원본 추가**를 클릭하여 연결 메뉴를 엽니다.

1. 다음을 수행합니다.

    - 기존 SQL server 인스턴스 이름 입력
    - **인증 유형**을 선택합니다.
    - 서버의 연결 속성 지정

1. **연결**을 클릭합니다.

1. **원본 추가**에서 평가할 데이터베이스를 선택합니다. 이 연습에서는 **AdventureWorks2008R2**를 선택합니다.

1. **추가**를 클릭합니다.
    > [!NOTE]
    > 여러 SQL Server 인스턴스에서 데이터베이스를 추가하려면 **원본 추가** 단추를 사용합니다. 여러 데이터베이스를 제거하려면 Shift+Ctrl을 누른 상태로 제거할 데이터베이스를 선택한 다음 **원본 제거**를 클릭합니다.

1. **평가 시작**을 클릭합니다.

## <a name="view-results"></a>결과 보기

데이터베이스가 여러 개이면 각 데이터베이스의 결과가 사용 가능해지는 즉시 표시됩니다. 모든 데이터베이스 평가가 완료될 때까지 기다릴 필요는 없습니다.

1. **AdventureWorks**의 평가가 완료되면 **호환성 문제** 및 **기능 권장 사항**을 클릭하여 결과를 확인합니다.

    - SQL Server 기능 패리티 범주에는 완전히 지원되지 않을 수도 있는 기능과 이러한 문제를 해결하기 위한 단계가 나열됩니다. 기능 패리티 문제가 있어도 마이그레이션이 중지되지는 않습니다.
    - 호환성 문제 범주에는 마이그레이션을 차단하는 기능과 이러한 문제를 해결하기 위한 단계가 나열됩니다.

## <a name="summary"></a>요약

이 단원에서는 로컬에 설치된 SQL Server 데이터베이스를 평가하여 Azure SQL Database로 해당 데이터베이스를 마이그레이션하면 사용할 수 없는 기능이 있는지를 확인했습니다.