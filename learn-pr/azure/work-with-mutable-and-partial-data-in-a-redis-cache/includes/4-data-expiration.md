데이터가 항상 영구적인 것은 아니며 특정 시점에는 삭제가 필요하기도 합니다. 예를 들어, 인스턴트 메시징 응용 프로그램에서 사용자가 그룹 채팅의 표시 이름을 설정하고 한 시간 뒤 이 이름을 재설정하려 할 수 있습니다. 시간 타이머를 설정하고 이름을 삭제하는 자체 서버 측 논리를 작성하여 이를 수행할 수 있습니다.  그러나 Redis는 추가 논리 작성 없이 자동으로 이를 수행하는 기능인 데이터 만료를 지원합니다.

여기에서 데이터 만료를 구현하는 일반적인 Redis 명령에 대해 알아봅니다.

## <a name="what-is-data-expiration"></a>데이터 만료란?

데이터 만료는 일정 시간 후 캐시에서 자동으로 키와 값을 삭제할 수 있는 기능입니다.

## <a name="why-use-data-expiration"></a>데이터 만료를 사용하는 이유

데이터 만료는 저장하는 데이터가 짧은 기간 동안만 유효한 경우에 일반적으로 사용됩니다.  이 점은 Redis가 메모리 내 데이터베이스이고 디스크에 저장하는 것만큼의 가용 메모리가 사용하지 않기 때문에 중요합니다. Redis에서는 저장소가 제한되므로 중요한 데이터만 저장하도록 합니다. 오래 지속될 저장할 필요가 없는 데이터의 경우 만료를 설정합니다.

## <a name="how-to-use-data-expiration-in-redis"></a>Redis에서 데이터 만료를 사용하는 방법

Redis에서 다양한 명령으로 데이터 만료를 구현 및 관리할 수 있습니다.

- `EXPIRE`: 키 제한 시간(초) 설정
- `PEXIRE`: 키 제한 시간(밀리초) 설정
- `EXPIREAT`: 절대 Unix 타임스탬프를 사용하여 키 제한 시간(초) 설정
- `PEXPIREAT`: 절대 Unix 타임스탬프를 사용하여 키 제한 시간(밀리초) 설정
- `TTL`: 키가 만료되기 전까지 남은 시간(초) 반환
- `PTTL`: 키가 만료되기 전까지 남은 시간(밀리초) 반환
- `PERSIST`: 키가 만료되지 않음

가장 일반적인 명령은 `EXPIRE`이며 이 모듈 전체에서 이 명령을 사용합니다.

### <a name="example-of-data-expiration-using-c-and-servicestackredis"></a>C# 및 ServiceStack.Redis를 사용한 데이터 만료의 예

**ServiceStack.Redis** 같은 클라이언트 라이브러리를 사용할 때는 낮은 수준의 Redis 명령에 대해서는 염려할 필요가 없습니다. 대신 간단한 C# 메서드를 사용할 수 있습니다.

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

Redis를 사용하면 데이터 만료를 통해 일정 시간 이후 데이터를 자동으로 삭제할 수 있습니다. 이 점은 Redis가 메모리 내 데이터베이스이고 디스크에 데이터를 저장하는 것만큼의 가용 메모리가 필요하지 않기 때문에 중요합니다. 오랜 시간 동안 저장할 필요가 없는 데이터의 경우 만료를 설정합니다.