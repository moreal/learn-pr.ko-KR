데이터는 항상 영구적으로 적용 하 고 특정 시간에 삭제 하려는 경우가 있습니다. 예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자 그룹 채팅의 표시 이름을 설정할 수 있습니다. 그러나 원하는 1 시간 후 다시 설정 하는 이름입니다. 시간 타이머를 설정 하 고 이름을 삭제 하는 고유한 서버 쪽 논리를 작성 하 여이 수행할 수 있습니다. 그러나 Azure Redis Cache에는 추가 논리를 작성 하지 않고도이 작업을 자동으로 수행 하는 기능인 데이터 만료를 지원 합니다.

여기에서 데이터 만료를 구현 하는 일반적인 Redis 명령에 대 한 알아봅니다.

## <a name="what-is-data-expiration"></a>데이터 만료 란?

데이터 만료는 일정 시간 후 캐시에서 값을 키에 자동으로 삭제할 수 있는 기능입니다.

## <a name="why-use-data-expiration"></a>데이터 만료를 사용 하는 이유는?

데이터 만료 데이터를 저장 하는 수명이 짧은 경우 일반적으로 사용 됩니다.  이 Azure Redis Cache는 메모리 내 데이터베이스 및 많은 메모리를 디스크에 저장 하는 경우 처럼 사용할 수 없는 중요 합니다. Azure Redis Cache를 사용 하 여 저장소를 제한 하므로 중요 한 데이터를 저장만 하 고 있는지 확인 하려고 합니다. 데이터 오랜 시간 동안 해결 되지 않아도, 만료 날짜를 설정 해야 합니다.

## <a name="how-to-use-data-expiration-in-azure-redis-cache"></a>Azure Redis Cache에서 데이터 만료를 사용 하는 방법

구현 하 고 Azure Redis Cache에서 데이터 만료를 관리 하는 다른 명령입니다.

- `EXPIRE`: 시간 (초)에서 키의 제한 시간을 설정합니다.
- `PEXIRE`: 밀리초에서 키의 제한 시간을 설정합니다.
- `EXPIREAT`: 시간 (초)의 절대 Unix 타임 스탬프를 사용 하 여 키의 제한 시간을 설정 합니다.
- `PEXPIREAT`: 밀리초에서 절대 Unix 타임 스탬프를 사용 하 여 키의 제한 시간을 설정 합니다.
- `TTL`: 초에 키에 남아 있는 시간을 반환 합니다.
- `PTTL`: 남아 있는 시간 (밀리초)에 키가 시간을 반환 합니다.
- `PERSIST`: 만료 되지 않도록 키를 수 있습니다.

가장 일반적인 명령입니다 `EXPIRE`,이 모듈에서 사용 하 고 있습니다.

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>데이터 만료 C# 및 ServiceStack.Redis의 예

와 같은 클라이언트 라이브러리를 사용 하는 경우 **ServiceStack.Redis**, 낮은 수준의 Azure Redis Cache 명령 저장에 대해 걱정할 필요가 없습니다. 대신 간단한 C# 메서드를 사용할 수 있습니다.

```csharp
public static void SetGroupChatName(string groupChatID, string chatName)
{
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create a key for group chat display names
        string key = groupChatID + "displayName";

        //Set the group chat display name
        redisClient.Set(key, chatName);

        //Set the expiration for one hour
        redisClient.Expire(key, 3600);
    }
}
```

Azure Redis Cache를 사용 하면 데이터 만료를 사용 하 여 시간을 설정 후 자동으로 데이터를 삭제할 수 있습니다. 이 Azure Redis Cache는 메모리 내 데이터베이스를 사용할 수 있는 만큼 메모리를 디스크에 데이터를 저장 하는 경우 없는 되므로 중요 합니다. 오랜 시간 동안로 데이터를 저장 하는 필요 하지 않은, 경우 만료 날짜를 설정 해야 합니다.