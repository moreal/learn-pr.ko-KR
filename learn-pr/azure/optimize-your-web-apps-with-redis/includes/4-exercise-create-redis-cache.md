저장 하 고 자주 사용 되는 값을 반환 하는 Azure Redis Cache 인스턴스를 만들어 보겠습니다.

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a>Azure에서 Redis cache 만들기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. 클릭 **리소스 만들기**, 클릭 **데이터베이스**를 클릭 하 고 **Redis Cache**합니다.

    다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여 줍니다.

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조되어 있는 Azure Portal 데이터베이스 옵션을 보여 주는 스크린샷입니다.](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a>캐시의 위치를 식별 합니다.

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a>캐시 구성

캐시에서 다음 설정을 적용 합니다.

1. **DNS 이름:** **ContosoSportsApp1028**과 같이 전역적으로 고유한 이름을 만듭니다.

1. **구독:** Azure 샌드박스 구독을 선택 합니다.

1. **리소스 그룹:** 선택 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 리소스 그룹에 대 한 합니다.

1. **위치:** 고객과-이 경우 동부 해안 근처 위치를 선택은 일반적으로 합니다. 그러나 Azure 샌드박스를 위에서 설명한 것 처럼 리소스에 대 한 선택 해야 하는 특정 지역 에서만 허용 합니다. 이러한 위치 중 하나를 선택 하십시오.

1. **가격 책정 계층:** **기본 C0**을 선택합니다. 사용할 수는 가장 낮은 계층입니다. 프로덕션 앱은 더 많은 데이터를 저장 하 고 더 높은 계층 선택 해야 하는 클러스터링 같은 프리미엄 기능 중 일부를 활용 하 경우가 많습니다.

1. **만들기**를 클릭합니다.

    다음 스크린샷은 새 Redis Cache 리소스를 만드는 데 사용되는 대표적인 구성을 보여 줍니다. 참고 사용자 Azure 샌드박스로 인해 약간 다른 됩니다.

    ![구성 DNS 이름, 구독, 새 리소스 그룹, 위치, 가격 책정 계층 예제가 채워져 있는, 새 Redis Cache 리소스를 만드는 경우의 Azure Portal 블레이드를 보여 주는 스크린샷입니다.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> 계속하기 전에 캐시가 배포될 때까지 기다려야 합니다. 이 프로세스는 시간이 약간 걸릴 수 있습니다.

## <a name="verify-your-data"></a>데이터 확인

사용할 수는 **콘솔** Redis cache 인스턴스에 생성 된 후 명령 실행 하려면 Azure portal의 기능입니다.

1. 선택 하 여 Redis cache를 찾습니다 **모든 리소스** 인스턴스 왼쪽 사이드바 및 왼쪽에서 필터 상자를 사용 하 여 Redis Cache를 선택 합니다. 또는 맨 위에 있는 검색 상자를 사용할 수 있으며 캐시의 이름을 입력 합니다.

1. Redis 캐시 인스턴스를 선택 합니다.

1. 에 **개요** Redis Cache, 선택에 대 한 블레이드 **콘솔**합니다. 하위 수준 Redis 명령을 입력할 수 있는 Redis 콘솔을 열립니다.

1. 형식 **ping**합니다. 반환 된 값이 인지 확인 **핑퐁**합니다.

1. 형식 **하나 집합 테스트**합니다. 반환 된 값이 인지 확인 **확인**합니다.

1. 형식 **테스트**합니다. 반환 된 값이 인지 확인 **한쪽**합니다.

1. 다시 전환 합니다 **개요** 패널 맨 위에서 이동 경로 탐색 막대를 통해 또는 스크롤 막대를 사용 하 여 뷰 왼쪽으로 슬라이드 합니다.

## <a name="retrieve-the-access-keys-and-host-name"></a>액세스 키 및 호스트 이름 검색

1. 선택 **설정을** > **선택키가**합니다. 

1. 복사 합니다 **기본 연결 문자열 (StackExchange.Redis)** 을 안전한 장소에 해야 다음 연습에 대 한 합니다.

    이 키에 대 한 응용 프로그램 설정 내에서 사용 하 여 전체 연결 문자열의 기본 키와 호스트 이름이 포함 된 **StackExchange.Redis** 패키지 사용 하겠습니다.

다음으로, 캐시를 조사 하는을 사용 하 여 명령 중 일부에 대해 알아보겠습니다.