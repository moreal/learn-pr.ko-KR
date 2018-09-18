현재 유연한 데이터 형식 및 지형 공간 지원을 사용하여 온-프레미스 PostgreSQL 관계형 데이터베이스를 사용한다고 가정해 보겠습니다. 회사에서 확장을 고려하고 있으며, 데이터베이스를 확장할 필요가 있습니다. 추가 하드웨어에 투자하는 대신, 최적의 클라우드 호스팅 데이터베이스 제품을 찾아야 하며, Azure Database for PostgreSQL 서버를 사용하기로 결정했습니다.

## <a name="what-is-an-azure-database-for-postgresql-server"></a>Azure Database for PostgreSQL 서버란?

PostgreSQL 서버는 하나 이상의 데이터베이스에 대한 중앙 관리 지점입니다. Azure에서 PostgreSQL 서비스는 성능을 보장하고 서버 수준의 액세스와 기능을 제공하는 관리되는 리소스입니다.

**Azure Database for PostgreSQL** 서버는 데이터베이스에 대한 부모 _리소스_입니다. _리소스_는 Azure를 통해 사용할 수 있는 관리 가능한 항목입니다. 이 리소스를 만들면 서버 인스턴스를 구성할 수 있습니다.

### <a name="what-is-an-azure-database-for-postgresql-server-resource"></a>Azure Database for PostgreSQL 서버 리소스란?

Azure Database for PostgreSQL 서버 리소스는 서버와 데이터베이스의 수명에 강력한 영향을 주는 컨테이너입니다. 서버 리소스가 삭제되면 모든 데이터베이스도 삭제됩니다. 부모 리소스에 속한 모든 리소스는 동일한 지역에서 호스팅된다는 점에 유의하세요.

서버 리소스 이름은 서버 엔드포인트 이름을 정의하는 데 사용됩니다. 예를 들어 리소스 이름이 **mypgsqlserver**이면 서버 이름은 **mypgsqlserver.postgres.database.azure.com**이 됩니다.

또한 서버 리소스는 해당 데이터베이스에 적용되는 관리 정책에 대한 __연결 범위__를 제공합니다. 예를 들어 로그인, 방화벽, 사용자, 역할 및 구성이 있습니다.

PostgreSQL의 오픈 소스 버전과 마찬가지로, 서버는 여러 버전에서 사용할 수 있으며 확장을 설치할 수 있습니다. 설치할 서버 버전을 선택합니다.

> [!NOTE]
> 확장을 사용하면 여러 SQL 개체를 모두 단일 패키지에 번들로 묶을 수 있으며, 이에 따라 단일 명령으로 로드하거나 제거할 수 있습니다. 확장의 예로 ```chkpass```가 있으며, 이는 자동으로 암호화된 암호에 대한 데이터 형식을 제공합니다.

## <a name="pricing-tiers"></a>가격 책정 계층

Azure Database for PostgreSQL은 계산 성능 및 저장소와 같은 매개 변수를 기반으로 하는 세 가지 가격 책정 계층 중에서 선택할 수 있는 옵션을 제공합니다.

### <a name="basic"></a>기본

**기본** 계층은 간단한 계산 및 I/O 성능이 필요한 워크로드에 적합합니다. 이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.

- 계산 4세대 CPU(Intel E5-2673 v3 (Haswell) 2.4GHz 프로세서 기반, 1-2개의 vCore 구성으로 사용 가능)
- 계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 1-2개의 vCore 구성으로 사용 가능)
- 저장소(최대 1TB)
- 로컬 중복 백업

특정 가격 책정 계층 설정을 사용하여 나중에 예제 서버를 만들 때 특정 시나리오에 대한 지원을 설명합니다. 프로덕션 서버의 경우 사용자 환경에 맞게 가격 책정 계층을 선택할 수 있음에 유의하세요.

### <a name="general-purpose"></a>범용

**범용** 계층은 확장 가능한 I/O 처리량을 갖춘 부하 분산된 계산 및 메모리가 필요한 대부분의 비즈니스 워크로드에 적합합니다. 이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.

- 계산 4세대 CPU(Intel E5-2673 v3 (Haswell) 2.4GHz 프로세서 기반, 2, 4, 8, 18, 32개의 vCore 구성으로 사용 가능)
- 계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 2, 4, 8, 18, 32개의 vCore 구성으로 사용 가능)
- 저장소(최대 4TB)
- 로컬 중복 백업
- 지역 중복 백업

### <a name="memory-optimized"></a>메모리 최적화

**메모리 최적화** 계층은 빠른 트랜잭션 처리와 높은 동시성을 위해 메모리 내 성능이 필요한 고성능 데이터베이스 워크로드에 적합합니다. 이 계층에서 액세스 할 수 있는 하드웨어는 다음과 같습니다.

- 계산 5세대 CPU(Intel E5-2673 v4 (Broadwell) 2.3GHz 프로세서 기반, 2, 4, 8, 16개의 vCore 구성으로 사용 가능)
- 저장소(최대 4TB)
- 로컬 중복 백업
- 지역 중복 백업

## <a name="steps-to-create-an-azure-database-for-postgresql-server"></a>Azure Database for PostgreSQL 서버를 만드는 단계

일반적으로 Azure Portal을 사용하여 Azure Database for PostgreSQL 서버를 만듭니다. 수행할 단계를 살펴보겠습니다.

먼저 Azure Portal에 로그인한 다음, **리소스 만들기**를 클릭합니다.

**데이터베이스**와 **Azure Database for PostgreSQL**을 선택합니다. [검색] 기능을 사용하여 이 범주를 찾을 수도 있습니다.

포털에는 선택 작업을 수행할 수 있는 PostgreSQL 서버 구성 화면(블레이드라고도 함)이 표시됩니다.

![Azure Portal - PostgreSQL 서버 만들기 사용자 인터페이스 블레이드](../media-draft/4-create-blade.png)

블레이드의 모든 항목에 값을 제공해야 하므로 각 항목에 대해 살펴보겠습니다.

### <a name="server-name"></a>서버 이름

앞에서 설명한 대로 서버 리소스를 만듭니다 서버 이름은 이 리소스를 지정하는 항목입니다. 결과적으로 서버에 대한 고유한 이름을 선택해야 합니다. 서버 이름은 모두 소문자여야 하며, 숫자와 하이픈을 포함할 수 있습니다.

_Adventure Works 추적_ 서버의 이름을 지정한다고 가정해 보겠습니다. 그러면 이름을 ```adventure-works-tracking```으로 설정합니다. 이미 있는 동일한 이름의 서버를 만들려고 하면 해당 결과에 오류가 발생합니다.

### <a name="subscription"></a>구독

구독 필드는 요금 청구에 사용됩니다. 사용할 수 있는 구독이 둘 이상 있는 경우 특정 구독을 선택합니다.

### <a name="resource-group"></a>리소스 그룹

서버와 관련된 모든 리소스를 관리하려면 리소스 그룹을 사용합니다. 새 리소스 그룹을 만들거나 기존 리소스 그룹을 다시 사용할 수 있습니다.

### <a name="source"></a>원본

서버는 _비어 있음_ 기본 옵션을 선택하거나 기존 백업에서 처음부터 만들 수 있습니다. [백업] 옵션을 사용하면 기존 Azure Database for PostgreSQL 서버의 지역 백업을 복원할 수 있습니다.

### <a name="server-admin-login-name"></a>서버 관리자 로그인 이름

서버 관리자 사용자를 만듭니다. 새 서버에 대한 관리자 로그인으로 사용할 로그인 이름을 선택합니다. 관리자 로그인 이름은 azure_superuser, azure_pg_admin, admin, administrator, root, guest 또는 public이 될 수 없습니다. pg_로 시작할 수 없습니다. 나중에 사용하기 위해 이 이름을 기억하거나 적어 두세요.

### <a name="password"></a>암호

위의 관리자 로그인 이름과 함께 사용할 암호를 선택합니다. 암호에는 영어 대문자, 영어 소문자, 숫자(0-9) 및 영숫자가 아닌 문자(!, $, #, % 등)의 세 가지 범주에 속한 문자가 포함되어야 합니다. 나중에 사용하기 위해 이 암호를 기억하거나 적어 두세요.

### <a name="confirm-password"></a>암호 확인

확인을 위해 암호를 다시 입력합니다.

### <a name="location"></a>위치

위치 옵션을 사용하면 서버가 물리적으로 만들어지는 위치를 지정할 수 있습니다. 사용자에게 가장 가까운 지리적 위치를 선택합니다. 실제 시나리오에서 위치는 대다수의 사용자에게 가장 가까운 위치여야 합니다.

### <a name="version"></a>버전

사용할 PostgreSQL 버전을 지정할 수 있습니다. Microsoft는 PostgreSQL의 현재 버전과 두 개의 이전 버전을 지원하는 것을 목표로 합니다. 그러면 프로덕션 환경에 맞는 버전을 선택할 수 있습니다.

> [!NOTE]
> 자세한 내용은 다음 자료를 참조하세요.
> - [지원되는 PostgreSQL 데이터베이스 버전](https://docs.microsoft.com/azure/postgresql/concepts-supported-versions)
> - [버전 관리 정책](https://www.postgresql.org/support/versioning/)

### <a name="pricing-tier"></a>가격 책정 계층

서버의 워크로드를 지원하는 가격 책정 계층을 선택할 수 있습니다. 세 가지 계층 중에서 선택할 수 있습니다. 앞에서 살펴본 대로 이러한 계층 각각에서는 계산 및 저장소 옵션을 구성할 수 있습니다. 예를 들어 다음은 5세대 계산 및 25일 백업 보존 기간을 갖춘 기본 가격 계층을 선택한 경우입니다.

![가격 책정 계층](../media-draft/4-azure-db-pricing-tier.png)

이제 입력한 값을 검토하고, 나중에 필요할 수 있는 메모를 작성하고, 만들기 단추를 클릭하여 서버를 만드는 것만 남아 있습니다.

서버를 배포하는 데는 몇 분이 걸립니다. 배포가 완료되면 알림을 받게 됩니다. 알림에서 새로 만든 서버로 이동할 수 있습니다.

이제까지 Azure Database for PostgreSQL을 만드는 데 필요한 단계를 살펴보았습니다. 다음 단원에서는 사용자 고유의 Azure Database for PostgreSQL 서버를 만들어 보겠습니다.
