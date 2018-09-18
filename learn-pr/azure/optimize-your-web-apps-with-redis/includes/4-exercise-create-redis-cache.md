일반적으로 사용되는 값을 저장하고 반환하는 Azure Redis Cache 인스턴스를 만들겠습니다.

<!-- TODO: do we need to activate the sandbox here? -->

## <a name="create-a-redis-cache-in-azure"></a>Azure에서 Redis 캐시 만들기

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. **리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.

    다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여줍니다.

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조 표시된 Azure Portal 데이터베이스 옵션을 보여주는 스크린샷.](../media/4-create-a-cache-1.png)

### <a name="identify-the-location-for-the-cache"></a>캐시의 위치 식별

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="configure-your-cache"></a>캐시 구성

캐시에서 다음 설정을 적용합니다.

1. **DNS 이름:** **ContosoSportsApp1028**처럼 전역적으로 고유한 이름을 만듭니다.

1. **구독**: Azure 샌드박스 구독을 선택합니다.

1. **리소스 그룹**: 리소스 그룹의 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 선택합니다.

1. **위치:** 일반적으로 고객과 가까운 위치를 선택합니다. 이 예에서는 동부 해안입니다. 그러나 위에서 언급했듯이 Azure 샌드박스는 특정 지역만 허용합니다. 다음 위치 중 하나를 선택하세요.

1. **가격 책정 계층:** **기본 C0**을 선택합니다. 사용할 수 있는 가장 낮은 계층입니다. 프로덕션 앱은 더 많은 데이터를 저장하기를 원하고 더 높은 계층이 필요한 클러스터링 같은 일부 프리미엄 기능을 활용하려 합니다.

1. **만들기**를 클릭합니다.

    다음 스크린샷은 새 Redis Cache 리소스를 만드는 데 사용되는 대표적인 구성을 보여줍니다. Azure 샌드박스 때문에 여러분의 구성과 약간 다를 것입니다.

    ![구성 DNS 이름, 구독, 새 리소스 그룹, 위치, 가격 책정 계층 예제로 채워진 새 Redis Cache 리소스를 만들 때 Azure Portal 블레이드의 모습을 보여주는 스크린샷.](../media/4-create-a-cache-2.png)

> [!IMPORTANT]
> 계속하기 전에 캐시가 배포될 때까지 기다려야 합니다. 이 프로세스는 시간이 약간 걸릴 수 있습니다.

## <a name="retrieve-the-access-keys-and-host-name"></a>액세스 키 및 호스트 이름 검색

1. Azure Portal에서 새 캐시 인스턴스를 찾아서 **설정** > **액세스 키**를 선택합니다. 

1. **기본 연결 문자열(StackExchange.Redis)** 을 안전한 장소에 복사합니다. 그 다음 연습에서 필요합니다.

    이 키는 우리가 사용하려는 **StackExchange.Redis** 패키지의 응용 프로그램 설정 내에서 사용할 전체 연결 문자열의 기본 키와 호스트 이름을 포함하고 있습니다.

다음으로, 캐시를 조사하는 데 사용할 수 있는 명령을 알아보겠습니다.