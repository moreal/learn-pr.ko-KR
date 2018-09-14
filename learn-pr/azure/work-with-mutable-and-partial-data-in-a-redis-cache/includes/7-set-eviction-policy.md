여기에서 Azure Redis Cache에는 제거 정책을 추가 합니다.

## <a name="set-an-eviction-policy"></a>제거 정책을 설정합니다

Azure에는 제거 정책을 설정 하려면 단순히 사용 드롭 다운 메뉴는 Azure portal에서 합니다.

1. Azure portal에서 Azure Redis Cache를 엽니다.

1. 선택 된 **고급 설정** 블레이드입니다.

1. 사용 된 **maxmemory 정책** 드롭 다운 메뉴에서 선택한 **allkeys 임의**합니다.

1. **저장**을 클릭합니다. 

이 시점에서 메모리 부족 하면 Azure Redis Cache는 무작위 키를 새 데이터에 대 한 공간을 확보 하려면 [삭제]를 선택 합니다.