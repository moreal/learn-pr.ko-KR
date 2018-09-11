스포츠 통계 개발 팀에서는 캐싱이 최근에 요청된 데이터에 필요한 성능을 크게 향상할 수 있다고 판단했습니다. 그래서 다음 단계로 Azure Redis Cache 인스턴스를 만들고 구성하려고 합니다.

### <a name="create-and-configure-the-azure-redis-cache-instance"></a>Azure Redis Cache 인스턴스 만들기 및 구성

1. Azure Portal의 데이터베이스 리소스에서 Azure Redis Cache 인스턴스를 추가할 수 있습니다.

1. 전역적으로 고유한 이름을 제공합니다. 이름은 1-63자의 문자열로, 숫자, 영문자 및 ‘-’ 문자만 포함할 수 있습니다. 캐시 이름은 ‘-’ 문자로 시작하거나 끝날 수 없으며, 연속되는 ‘-’ 문자는 유효하지 않습니다.

1. 이 새로운 Azure Redis Cache 인스턴스가 만들어지는 구독을 제공합니다.

1. 캐시를 만들 리소스 그룹의 이름을 지정합니다. 앱의 모든 리소스를 한 그룹에 배치하여 다 함께 관리할 수 있습니다.

1. 데이터 소비자에게 가까운 위치를 선택합니다.

    > [!NOTE]
    > 캐시가 데이터 저장소보다 데이터 소비자에게 가까운 것보다 훨씬 더 중요합니다.

1. 가격 책정 계층을 선택합니다. 데이터 지속성을 활용하려면 프리미엄 계층을 선택해야 합니다.

    - 프리미엄 계층을 사용하면 다음 두 가지 방법 중 하나로 데이터를 유지하여 재해 복구를 제공할 수 있습니다.

        - RDB 지속성은 주기적 스냅숏을 만들고 실패가 발생하면 해당 스냅숏을 사용하여 캐시를 다시 빌드할 수 있습니다.

            ![새 Redis Cache 인스턴스에 대한 RDB 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-1.png)

        - AOF 지속성은 초당 한 번 이상 저장되는 로그에 모든 쓰기 작업을 저장합니다. 이렇게 하면 RDB보다 큰 파일이 만들어지지만 데이터 손실은 더 적습니다.

            ![새 Redis Cache 인스턴스에 대한 AOF 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-2.png)

    - 가상 네트워크로 캐시를 보호합니다.
      프리미엄 계층 Redis Cache가 있는 경우 클라우드의 가상 네트워크에 배포할 수 있습니다. 캐시는 동일한 가상 네트워크의 다른 가상 머신 및 응용 프로그램에만 사용할 수 있습니다.

    - 클러스터링을 통해 캐시를 배포합니다.
      프리미엄 계층 Redis Cache를 사용하면 여러 노드에 데이터 집합을 자동으로 분할하도록 클러스터링을 구현할 수 있습니다. 클러스터링을 구현하려면 최대 10까지 분할 수를 지정합니다. 비용은 원래 노드에 분할 수를 곱한 비용입니다.

    - Azure Managed Cache Service에서 마이그레이션합니다.
      사용하는 Managed Cache Service 기능에 따라 응용 프로그램 변경을 최소화하여 Azure Managed Cache Service 사용 응용 프로그램을 Azure Redis Cache로 마이그레이션할 수 있습니다. API가 정확하게 동일하지는 않더라도 비슷합니다. Managed Cache Service를 사용하여 캐시에 액세스하는 기존 코드의 대부분은 최소한의 변경만으로 재사용할 수 있습니다.

### <a name="configure-your-client"></a>클라이언트 구성

클라이언트 응용 프로그램은 Redis Cache를 사용하도록 구성되어야 합니다. .NET 언어를 위한 인기 있는 고성능 Redis 클라이언트는 **StackExchange.Redis**입니다. Visual Studio에서 **NuGet 패키지 관리자**를 사용하는 Redis 클라이언트는 **Install-Package** 명령을 사용하여 추가합니다.

그런 다음, 캐시에 연결하도록 클라이언트를 구성해야 합니다. 호스트 이름과 기본 또는 보조 키 설정이 포함된 **.config** 파일 확장을 사용하여 텍스트 파일을 만듭니다. 파일의 구조는 다음과 같습니다.

```XML
    <appSettings>
        <add key="CacheConnection" value="HOST-NAME.redis.cache.windows.net,abortConnect=false,ssl=true,password=PRIMARY-KEY"/>
    </appSettings>
```

**App.config** 파일을 편집하고 방금 만든 구성 파일을 참조하는 **appSettings** 파일 특성을 포함하도록 업데이트합니다.

### <a name="what-are-access-keys"></a>액세스 키란?

Azure Redis Cache 인스턴스에 연결할 때 캐시 클라이언트에 캐시의 호스트 이름, 포트 및 키가 필요합니다. 이 정보는 Azure Portal에서 검색할 수 있습니다.

### <a name="connection-settings"></a>연결 설정

Azure Redis Cache에 연결하려면 호스트 이름과 액세스 키가 필요합니다. 호스트 이름은 캐시의 인터넷 주소입니다(예: *sportsresults.redis.cache.windows.net*). 액세스 키는 캐시의 암호 역할을 합니다. 기본 및 보조 액세스 키가 있습니다. 둘 중 어느 것이든 사용할 수 있지만 기본 키를 변경해야 하는 경우에는 둘 다 입력됩니다. 모든 클라이언트를 보조 키로 전환한 후 기본 키를 변경하면 서비스 손실을 예방할 수 있습니다.
