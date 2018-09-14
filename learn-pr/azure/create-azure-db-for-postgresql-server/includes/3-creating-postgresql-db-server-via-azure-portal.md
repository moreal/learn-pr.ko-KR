유연한 데이터 형식 및 지리 공간 지원을 사용 하 여 온-프레미스 PostgreSQL 관계형 데이터베이스를 현재 사용 하는 경우를 가정해 봅니다. 회사를 보고 확장, 데이터베이스 확장에 필요 합니다. 추가 하드웨어에 투자 하는 대신, 최적의 클라우드에 호스트 된 데이터베이스 제품 찾기 담당 하 고 있습니다. PostgreSQL 서버용 Azure Database를 사용 하기로 합니다.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>PostgreSQL용 Azure 데이터베이스 서버란?

PostgreSQL 서버에는 하나 이상의 데이터베이스에 대 한 중앙 관리 지점입니다. Azure에서 PostgreSQL 서비스는 성능 보장을 제공 하 고 액세스 및 서버 수준에서 기능을 제공 하는 관리 되는 리소스입니다.

**Azure Database for PostgreSQL** 서버는 부모 _리소스_ 데이터베이스에 대 한 합니다. A _리소스_ 는 Azure를 통해 사용할 수 있는 관리 가능한 항목입니다. 이 리소스를 만드는 서버 인스턴스를 구성할 수 있습니다.

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a>Azure Database for PostgreSQL 서버 리소스는 무엇입니까?

Azure Database for PostgreSQL 서버 리소스는 서버 및 데이터베이스에 대 한 강력한 수명 의미를 사용 하 여 컨테이너. 서버 리소스가 삭제 되 면 모든 데이터베이스도 삭제 됩니다. 부모에 속한 모든 리소스가 동일한 지역에 호스트 되는 것을 염두에 두십시오.

서버 리소스 이름은 서버 끝점 이름이 정의 됩니다. 예를 들어가 리소스 이름은 **mypgsqlserver**, 서버 이름을 그러면 **mypgsqlserver.postgres.database.azure.com**합니다.

서버 리소스가 제공 된 __연결 범위__ 해당 데이터베이스에 적용 되는 관리 정책에 대 한 합니다. 예를 들어: 로그인, 방화벽, 사용자, 역할 및 구성 합니다.

PostgreSQL의 오픈 소스 버전인 마찬가지로 서버 여러 버전에서 사용할 수 있으며 확장 설치에 대 한 허용. 서버 버전을 설치를 선택할 수 있습니다.

> [!NOTE]
> 확장을 로드 하거나 단일 명령으로 제거할 수 있는 단일 패키지에서 여러 SQL 개체를 함께 묶음 허용 합니다. 확장의 예로 `chkpass`를 자동으로 암호화 된 암호에 대 한 데이터 형식을 제공 합니다.

## <a name="pricing-tiers"></a>가격 책정 계층

Azure Database for PostgreSQL 성능 및 저장소 계산 하는 수와 같은 매개 변수를 기반으로 하는 세 가지 가격 책정 계층을 선택할 수 있는 옵션을 제공 합니다.

### <a name="basic-tier"></a>기본 계층

합니다 **기본** 계층은 간단한 계산 및 I/O 성능이 필요한 워크 로드에 적합 합니다. 이 계층에서는 다음 하드웨어에 액세스할을 수 있습니다.

- Gen 4 Cpu 기준 Intel E5-2673 v3 (Haswell) 2.4ghz 프로세서를 사용할 수는 1 또는 2 vCore 구성으로 계산 합니다.
- 1 또는 2 vCore 구성으로 사용할 수 있는 (Broadwell) 2.3ghz 프로세서 Intel E5-2673 v4에 기본 Gen 5 Cpu 계산
- 저장소 최대 용량은 1 TB
- 로컬 중복 백업

나중에 예제 서버를 만들 때 특정 시나리오에 대 한 지원을 설명 하기 위해 특정 가격 책정 계층 설정을 사용 합니다. 프로덕션 서버에 대 한 환경에 맞게 가격 책정 계층 선택 됩니다 것을 염두에 두십시오.

### <a name="general-purpose-tier"></a>범용 계층

합니다 **범용** 계층은 부하가 분산 된 계산 및 확장 가능한 I/O 처리량을 사용 하 여 메모리를 필요로 하는 대부분의 비즈니스 워크 로드에 적합 합니다. 이 계층에서는 다음 하드웨어에 액세스할을 수 있습니다.

- Gen 4 Cpu 기반 Intel E5-2673 v3 (Haswell) 2.4ghz 프로세서를 2, 4, 8, 18에서 사용할 수 있는 계산 32 vCore 구성
- Gen 5 Cpu 기반 Intel E5-2673 v4 (Broadwell) 2.3ghz 프로세서 2, 4, 8, 18에서 사용할 수 있는 계산 32 vCore 구성
- 저장소 최대 4TB
- 로컬 중복 백업
- 지리적으로 중복 된 백업

### <a name="memory-optimized-tier"></a>메모리 액세스에 최적화 된 계층

합니다 **메모리 액세스에 최적화 된** 계층 보다 빠른 트랜잭션 처리와 높은 동시성을 위해 메모리 내 성능이 필요한 고성능 데이터베이스 워크 로드에 적합 합니다. 이 계층에서는 다음 하드웨어에 액세스할을 수 있습니다.

- Gen 5 Cpu 기반 Intel E5-2673 v4 (Broadwell) 2.3ghz 프로세서 2, 4, 8에서 사용할 수 있는 계산 16 vCore 구성
- 저장소 최대 4TB
- 로컬 중복 백업
- 지리적으로 중복 된 백업

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a>Azure Database for PostgreSQL 서버를 만드는 방법

일반적으로 Azure portal을 사용 하 여 PostgreSQL 서버용 Azure 데이터베이스를 만듭니다. 수행할 단계를 살펴보겠습니다.

먼저 Azure portal에 로그인 됩니다 하 고 클릭 한 다음 **리소스 만들기**합니다.

선택 **데이터베이스** 하 고 **Azure Database for PostgreSQL**합니다. 사용할 수도 있습니다는 **검색** 기능이이 범주를 찾으려고 합니다.

포털 블레이드, 라고도 PostgreSQL 서버 구성 화면에 표시 됩니다 하 고 선택 항목을 확인 합니다.

![새 데이터베이스의 PostgreSQL 만들기 블레이드를 보여 주는 Azure portal의 스크린샷](../media-draft/4-create-blade.png)

블레이드에서 모든 항목에 대 한 값을 지정 하려면 각 보도록 하겠습니다 해야 합니다.

### <a name="server-name"></a>서버 이름

앞서 설명한 대로 서버 리소스를 만듭니다. 서버 이름이이 리소스를 지정 하는 항목입니다. 결과적으로, 서버에 대 한 고유한 이름을 선택 해야 합니다. 서버 이름을 모두 소문자 여야 하 고 숫자 및 하이픈만 포함할 수 있습니다.

서버 이름을 원한다고 가정해 보겠습니다 _Adventure Works 추적_합니다. 다음 설정 하는 이름으로 `adventure-works-tracking`입니다. 서버를 만들려면 이미 존재 하는 이름으로 시도 하면 그 결과 오류가 표시 됩니다.

### <a name="subscription"></a>구독

구독 필드는 청구에 사용 됩니다. 둘 이상의 구독을 사용할 수 있는 경우 특정 구독을 선택 합니다.

### <a name="resource-group"></a>리소스 그룹

리소스 그룹을 사용 하 여 서버와 관련 된 모든 리소스를 관리할 수 됩니다. 새 리소스 그룹을 만들거나 기존 리소스 그룹을 다시 사용할 수 있습니다.

### <a name="source"></a>원본

선택 하 여 처음부터 중 하나는 서버를 만들 수 있습니다 합니다 _빈_ 기본 옵션 또는 기존 백업 합니다. 합니다 **백업** 옵션은 기존 Azure Database for PostgreSQL 서버를의 기회 복원을 지역 백업을 제공 합니다.

### <a name="server-admin-login-name"></a>서버 관리자 로그인 이름

서버 관리자 사용자를 만듭니다. 새 서버에 대 한 관리자 로그인으로 사용 하는 로그인 이름을 선택 합니다. 관리자 로그인 이름은 azure_superuser, azure_pg_admin, 관리자, 관리자, 루트, guest 또는 공용 수 없습니다. P g _ '를 사용 하 여 시작할 수 없습니다. 기억 하거나 나중에 사용 하기 위해이 이름을 적어 둡니다.

### <a name="password"></a>암호

위의 관리자 로그인 이름을 사용 하는 데 암호가 있습니다. 암호에는 다음 범주 중 세 범주의 문자를 포함 해야 합니다.
- 영어 대문자
- 영어 소문자
- 숫자 (0-9)
- 영숫자 이외의 문자 (!, $, #, %, 및 등)

기억 하거나 나중에 사용이이 암호를 적어 둡니다.

### <a name="confirm-password"></a>암호 확인

확인 암호를 다시 입력 하십시오.

### <a name="location"></a>위치

위치 옵션을 사용 하면 서버를 물리적으로 만들 위치를 지정할 수 있습니다. 가장 가까운 지리적 위치를 선택 합니다. 실제 시나리오에서는 위치에 대부분의 사용자에 게 가장 가까운 위치 해야 합니다.

### <a name="version"></a>버전

사용 하 여 PostgreSQL의 버전을 지정할 수 있습니다. Microsoft는 현재 버전 및 PostgreSQL의 두 이전 버전을 지원 하려고 합니다. 프로덕션 환경에 맞는 버전을 선택할 수 있습니다.

> [!NOTE]
> 자세한 내용은 다음을 참조 합니다.
> - [지원 되는 PostgreSQL 데이터베이스 버전](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions)
> - [버전 관리 정책](https://www.postgresql.org/support/versioning/)

### <a name="pricing-tier"></a>가격 책정 계층 

서버의 워크 로드를 지 원하는 가격 책정 계층을 선택할 수 있습니다. 세 가지 계층에서 선택 해야 한다는 사실을 기억 하십시오. 앞에서 살펴본 것 처럼 계산 및 저장소 옵션을 구성할 수 있습니다 이러한 각 계층. 선택한 기본 가격 계층, Gen 5 계산 및 25 일 백업 보존 기간을 사용 하 여 예제는 다음과 같습니다.

![가격 책정 계층을 새 PostgreSQL 데이터베이스에 대 한 데이터베이스를 보여 주는 Azure portal의 스크린샷](../media-draft/4-azure-db-pricing-tier.png)

입력 한 값을 검토, 나중에 필요 하 고 클릭 수 있습니다 모든 메모를 이제 남았습니다 **만들기** 여 서버를 만듭니다.

서버를 배포 하는 몇 분 소요 됩니다. 배포가 완료 되 면 알림을 받게 됩니다. 알림에서 새로 만든된 서버를 이동할 수 있습니다.

이제 Azure Database for PostgreSQL 서버를 만드는 단계를 확인 했습니다. 다음 단위에 있는 사용자 고유의 Azure Database for PostgreSQL 서버를 만들 수가 있습니다.
