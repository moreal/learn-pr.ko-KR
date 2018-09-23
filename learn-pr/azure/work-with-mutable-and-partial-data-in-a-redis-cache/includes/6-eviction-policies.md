Azure Redis Cache는 메모리 내 데이터베이스이므로 메모리가 가장 중요한 리소스입니다. 사용 가능한 메모리 크기를 초과하는 데이터를 추가하기 시작하면 문제가 발생할 수 있습니다. Azure Redis Cache는 메모리가 부족할 때 데이터를 처리하는 방법을 나타내는 제거 정책을 지원합니다.

여기서는 최대 메모리 크기를 초과했을 때 데이터가 수행해야 할 작업을 결정하는 제거 정책을 설정합니다.

## <a name="what-is-an-eviction-policy"></a>제거 정책이란?

제거 정책은 사용 가능한 최대 메모리 크기를 초과했을 때 데이터를 관리하는 방식을 결정하는 계획입니다. 예를 들어 제거 정책을 사용하여 Azure Redis Cache에 임의의 키를 삭제하도록 지시하여 새 데이터를 삽입할 공간을 확보할 수 있습니다.

### <a name="types-of-eviction-policies"></a>제거 정책 유형

Azure Redis Cache는 여섯 가지 제거 정책을 제공합니다. 메모리 부족 시 데이터 삽입을 시도하면 이러한 모든 값이 작업을 수행합니다.

* **noeviction:** 제거 정책이 없습니다. 데이터를 삽입하려고 하면 오류 메시지를 반환합니다.

* **allkeys lru:** 가장 오래 전에 사용한 키를 제거합니다.

* **allkeys-random:** 임의의 키를 제거합니다.

* **volatile-lru:** 만료 설정이 있는 모든 키 중에 가장 오래 전에 사용한 키를 제공합니다.

* **volatile-ttl:** 만료 설정을 기준으로 가장 짧은 시간을 갖는 키를 제거합니다.

* **volatile-random:** 만료 설정이 있는 임의의 키를 제거합니다.

## <a name="how-to-set-an-eviction-policy"></a>제거 정책 설정 방법

Azure는 Azure Redis Cache에 대해 제거 정책을 설정하는 간단한 드롭다운 메뉴를 제공합니다. **고급 설정**을 선택하고 **maxmemory-policy** 드롭다운 메뉴를 사용합니다.

Azure Redis Cache에는 메모리가 중요하기 때문에 제거 정책을 지원합니다. 제거 정책은 메모리가 부족할 때 새 데이터 삽입을 시도하면 기존 데이터를 어떻게 처리할지 결정합니다.