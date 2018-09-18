여기서는 Azure Redis Cache에 제거 정책을 추가합니다.

## <a name="set-an-eviction-policy"></a>제거 정책 설정

Azure에서 제거 정책을 설정하려면 포털에서 간단히 드롭다운 메뉴를 사용합니다.

1. Azure Portal에서 Redis Cache를 엽니다.

1. **고급 설정** 블레이드를 선택합니다.

1. **maxmemory-policy** 드롭다운 메뉴를 사용하여 **allkeys-random**을 선택합니다.

1. **저장**을 클릭합니다. 

이 시점에서 메모리가 부족하게 되면 Redis가 새 데이터를 위한 공간을 확보하기 위해 임의의 키를 선택하여 삭제합니다.