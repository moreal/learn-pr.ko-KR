스포츠 통계 개발 팀에서는 캐싱이 최근에 요청된 데이터에 필요한 성능을 크게 향상할 수 있다고 판단했습니다. 그래서 다음 단계로 Azure Redis Cache 인스턴스를 만들고 구성하려고 합니다.

## <a name="create-and-configure-the-azure-redis-cache-instance"></a>Azure Redis Cache 인스턴스 만들기 및 구성

Azure portal, Azure CLI 또는 Azure PowerShell을 사용 하 여 Redis cache를 만들 수 있습니다. 용도 맞게 캐시를 제대로 구성 하기 위해 결정 해야 하는 몇 가지 매개 변수가 있습니다.

### <a name="name"></a>이름

Redis cache에는 전역적으로 고유한 이름이 필요 합니다. 이름을 연결한 서비스와 통신에 대 한 공용 URL 생성에 사용 되 고 있으므로 Azure 내에서 고유 해야 합니다.

이름은 문자, 숫자 이루어져 1 자에서 63 자 사이 여야 합니다 및 '-' 문자입니다. 캐시 이름은 ‘-’ 문자로 시작하거나 끝날 수 없으며, 연속되는 ‘-’ 문자는 유효하지 않습니다.

### <a name="resource-group"></a>리소스 그룹

Azure Redis Cache 관리 되는 리소스 이며 요구를 _리소스 그룹_ 소유자입니다. 새 리소스 그룹을 만듭니다 또는 일부인를 susbcription에서 기존 계정을 사용할 수 있습니다.

### <a name="location"></a>위치

Redis cache 배치 될 위치 물리적으로 Azure 지역을 선택 하 여 결정 해야 합니다. 동일한 지역에 항상 캐시 인스턴스 및 응용 프로그램을 배치 해야 합니다. 다른 지역에 캐시를 연결할 수 있습니다 훨씬 대기 시간이 증가할 줄이고 안정성. Azure 외부에서 캐시에 연결 하는 경우에 데이터를 소비 응용 프로그램이 실행 중인 가까운 위치를 선택 합니다.

> [!IMPORTANT]
> Redis cache의 데이터에 가깝게 배치 _소비자_ 있습니다.

### <a name="pricing-tier"></a>가격 책정 계층 

마지막 단위에서 언급 했 듯이 세 가지 가격 책정 계층 Azure Redis Cache를 사용할 수 있습니다.

- **기본**: 기본 캐시 개발/테스트에 이상적입니다. 단일 서버, 53GB의 메모리가, 및 20,000 개 연결으로 제한 됩니다. 이 서비스 계층에 대 한 SLA가 없습니다 있습니다.
- **표준**: 복제를 지원 하며 99.99 %SLA 포함 하는 프로덕션 캐시 합니다. 두 서버 (마스터/슬레이브)를 지원 하 고 기본 계층으로 동일한 메모리/연결 제한이 있습니다.
- **Premium**: Enterprise 계층을 표준 계층에서 빌드하고 지 속성, 클러스터링 및 스케일 아웃 캐시 지원이 포함 되어 있습니다. 최대 530GB의 메모리 및 40,000 개 동시 연결을 사용 하 여 가장 높은 성능의 계층입니다.

각 계층에서 사용 가능한 캐시 메모리 양을 제어할 수 있습니다-Basic/Standard 및 Premium에 대 한 P0 P4 C0 C6 캐시 수준을 선택 하 여이 선택 됩니다. 확인 합니다 [가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/cache/) 전체 세부 정보에 대 한 합니다.

> [!TIP]
> 항상 프로덕션 시스템에 대 한 표준 또는 프리미엄 계층을 사용 하는 것이 좋습니다. 기본 계층은 데이터 복제 및 SLA가 없는 단일 노드 시스템입니다. 또한 C1 이상의 캐시를 사용합니다. C0 캐시를 위한 간단한 개발/테스트 시나리오를 공유 하는 CPU 코어 및 매우 적은 메모리 있기 때문입니다.

프리미엄 계층을 사용 하면 재해 복구를 제공 하는 두 가지 방법에 대 한 데이터를 유지할 수 있습니다.

1. RDB 지속성은 주기적 스냅숏을 만들고 실패가 발생하면 해당 스냅숏을 사용하여 캐시를 다시 빌드할 수 있습니다.

    ![새 Redis Cache 인스턴스에 대한 RDB 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-1.png)

2. AOF 지속성은 초당 한 번 이상 저장되는 로그에 모든 쓰기 작업을 저장합니다. 이렇게 하면 RDB보다 큰 파일이 만들어지지만 데이터 손실은 더 적습니다.

    ![새 Redis Cache 인스턴스에 대한 AOF 지속성 옵션을 보여 주는 Azure Portal의 스크린샷입니다.](../media/3-redis-persistence-2.png)

만 사용할 수 있는 몇 가지 다른 설정이 합니다 **Premium** 계층입니다.

### <a name="virtual-network-support"></a>Virtual Network 지원

프리미엄 계층 Redis cache를 만드는 경우에 클라우드에서 가상 네트워크에 배포할 수 있습니다. 캐시는 동일한 가상 네트워크의 다른 가상 머신 및 응용 프로그램에만 사용할 수 있습니다. Azure에서 호스팅되는 서비스와 캐시 또는 Azure virtual network VPN 통해 연결 된 경우 더 높은 수준의 보안을 제공 합니다.

### <a name="clustering-support"></a>클러스터링 지원

프리미엄 계층 Redis Cache를 사용하면 여러 노드에 데이터 집합을 자동으로 분할하도록 클러스터링을 구현할 수 있습니다. 클러스터링을 구현하려면 최대 10까지 분할 수를 지정합니다. 분할 된 데이터베이스 수를 곱하고 원래 노드의 비용은 발생 하는 비용입니다.

## <a name="accessing-the-redis-instance"></a>Redis 인스턴스에 액세스

Redis 집합을 지 원하는 [알려진 명령](https://redis.io/commands)입니다. 일반적으로 명령으로 발생 `COMMAND parameter1 parameter2 parameter3`합니다.

다음은 사용할 수 있는 몇 가지 일반적인 명령입니다.

| 명령 | 설명 |
|---------|-------------|
| `ping` | 서버를 ping 합니다. "퐁"를 반환. |
| `set [key] [value]` | 캐시에 키/값을 설정합니다. 성공 시 "확인"을 반환합니다. |
| `get [key]` | 캐시에서 값을 가져옵니다. |
| `exists [key]` | '1'을 반환 합니다 **키** 그렇지 않은 경우 '0' 캐시에 존재 합니다. |
| `type [key]` | 값에 연결 된 형식을 반환 합니다는 주어진 **키**합니다. |
| `incr [key]` | 연결 된 지정된 된 값을 증가 **키** '1'. 값은 정수 또는 double 값 이어야 합니다. 이 새 값을 반환합니다. |
| `incrby [key] [amount]` | 연결 된 지정된 된 값을 증가 **키** 지정 된 크기입니다. 값은 정수 또는 double 값 이어야 합니다. 이 새 값을 반환합니다. |
| `del [key]` | 연관 된 값을 삭제 합니다 **키**합니다. |
| `flushdb` | 삭제할 _모든_ 키 및 데이터베이스의 값입니다. |

Redis 명령줄 도구는 (**redis cli**)이 명령을 사용 하 여 직접 실험에 사용할 수 있습니다. 다음은 몇 가지 예제입니다.

```output
> set somekey somevalue
OK
> get somekey
"somevalue"
> exists somekey
(string) 1
> del somekey
(string) 1
> exists somekey
(string) 0
```

작업의 예로 `INCR` 명령입니다. 원자성 증가 하기 때문에 편리한 이들은 _여러 응용 프로그램에서_ 캐시를 사용 하는 합니다.

```output
> set counter 100
OK
> incr counter
(integer) 101
> incrby counter 50
(integer) 151
> type counter
(integer)
```

### <a name="adding-an-expiration-time-to-values"></a>값에는 만료 시간 추가

있도록 하기 때문에 일반적으로 사용 되는 저장소 값을 메모리에 캐시 하는 것이 중요 합니다. 그러나 또한 유효 하지 않은 경우 이러한 값을 만료 방법이 필요 합니다. Redis에 적용 하면 됩니다는 _time-to-live_ (TTL) 키입니다.

TTL이 경과 하면 키가 자동으로 DEL 명령을 발급 된 것 처럼 정확 하 게 삭제 됩니다. TTL 만료에 몇 가지 참고 사항 다음과 같습니다.

- 만료 시간 (밀리초) 또는 초 전체 자릿수를 사용 하 여 설정할 수 있습니다.
- 만료 시간 확인은 항상 1 밀리초입니다.
- 만료에 대 한 내용은 복제 및 유지 디스크에 실제로 전달 Redis 서버 그대로 유지 됩니다 (이 즉, Redis는 키가 만료 될 날짜를 저장)를 중지 하는 경우.

만료 날짜의 예는 다음과 같습니다.

```output
> set counter 100
OK
> expire counter 5
(integer) 1
> get counter
100
... wait ...
> get counter
(nil)
```

## <a name="accessing-a-redis-cache-from-a-client"></a>클라이언트에서 Redis cache에 액세스

Azure Redis Cache 인스턴스에 연결할 일부의 정보를 해야 합니다. 클라이언트 캐시에 대 한 호스트 이름, 포트 및 액세스 키를 해야합니다. Azure portal에서이 정보를 검색할 수는 **설정 > 액세스 키** 페이지입니다. 

- 호스트 이름에는 캐시의 이름을 사용 하 여 만든 캐시의 공용 인터넷 주소입니다. 예: `sportsresults.redis.cache.windows.net`.

- 액세스 키는 캐시의 암호 역할을 합니다. 두 개의 키 생성: 기본 및 보조 합니다. 키 중 하나를 사용할 수 있습니다, 두 개의 기본 키를 변경 해야 할 경우 제공 됩니다. 보조 키로 전환 하는 모든 클라이언트를 기본 키 다시 생성 합니다. 이 원래 기본 키를 사용 하 여 응용 프로그램 차단 됩니다. 개인 암호 처럼 훨씬 키-주기적으로 다시 생성 하는 것이 좋습니다.

> [!WARNING]
> 액세스 키 기밀 정보 처리를 같이 하는 암호를 고려해 야 합니다. 캐시에서 모든 작업을 수행할 수는 선택키가 있으면 누구라도!
