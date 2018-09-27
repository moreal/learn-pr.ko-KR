일반적으로 사용되는 값을 저장하고 반환하는 Azure Redis Cache 인스턴스를 만들겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-redis-cache-in-azure"></a>Azure에서 Redis Cache 만들기

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. **리소스 만들기**, **데이터베이스**, **Redis Cache**를 차례로 클릭합니다.

    다음 스크린샷은 Azure Portal의 다양한 데이터베이스 리소스 옵션 내 Redis Cache 위치를 보여줍니다.

    ![리소스 만들기, 데이터베이스, Redis Cache 옵션이 강조되어 있는 Azure Portal 데이터베이스 옵션을 보여 주는 스크린샷입니다.](../media/4-create-a-cache-1.png)

### <a name="configure-your-cache"></a>캐시 구성

캐시에서 다음 설정을 적용합니다.

1. **DNS 이름:** **ContosoSportsApp[nnn]** 과 같은 전역적으로 고유한 이름을 만듭니다. 여기서 `[nnn]`은 임의의 숫자로 바꿉니다.

1. **구독:** 컨시어지 구독을 선택합니다.

1. **리소스 그룹:** 리소스 그룹에 대해 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 선택합니다.

1. **위치:** 일반적으로 고객과 가까운 위치를 선택합니다. 이 경우 동부 해안입니다.

    [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]

5. **가격 책정 계층:** **기본 C0**을 선택합니다. 사용할 수 있는 가장 낮은 계층입니다. 프로덕션 앱은 더 많은 데이터를 저장하기를 원하고 더 높은 계층이 필요한 클러스터링 같은 일부 프리미엄 기능을 활용하려 합니다.

1. **만들기**를 클릭합니다. Azure에서 자동으로 Redis Cache 인스턴스를 생성 및 배포합니다.

    > [!IMPORTANT]
    > 일반적으로 Redis Cache 리소스가 생성되고 Azure Portal에서 매우 신속하게 볼 수 있지만 캐시 자체는 몇 분간 볼 수 없습니다. 다음 단계에서는 캐시의 상태를 확인하는 방법을 보여줍니다.

## <a name="verify-your-data"></a>데이터 확인

Redis Cache 인스턴스가 생성된 후 Azure Portal의 **콘솔** 기능을 사용하여 이에 대한 명령을 실행할 수 있습니다.

1. 왼쪽 사이드바에서 **모든 리소스**를 선택하거나 배포가 완료되면 표시되는 **알림** 팝업을 통해 Redis Cache를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Redis Cache 인스턴스를 선택합니다. 또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.

1. Redis Cache 인스턴스를 선택합니다.

1. "상태" 필드 값을 확인합니다. 상태가 "실행 중"이어야 캐시가 준비됩니다. 계속하기 전에 몇 분 정도 기다려야 할 수 있습니다.

1. 캐시가 실행되면 Redis Cache의 **개요** 블레이드에서 `>_ Console` 단추를 클릭합니다. 하위 수준 Redis 명령을 입력할 수 있는 Redis 콘솔이 열립니다. 다음을 시도해 보세요.

    ```console
    ping
    ```

    ```output
    PONG
    ```

    ```console
    set test one
    ```

    ```output
    OK
    ```

    ```console
    get test
    ```

    ```output
    "one"
    ```

상단의 이동 경로 탐색 막대를 통해 **개요** 패널로 다시 전환하거나 스크롤 막대를 사용하여 보기를 다시 왼쪽으로 밉니다.

## <a name="retrieve-the-access-keys-and-host-name"></a>선택키 및 호스트 이름 검색

1. **설정** > **선택키**를 선택합니다.

1. **기본 연결 문자열(StackExchange.Redis)** 을 안전한 장소에 복사합니다. 그 다음 연습에서 필요합니다.

    이 키는 우리가 사용하려는 **StackExchange.Redis** 패키지의 응용 프로그램 설정 내에서 사용할 전체 연결 문자열의 기본 키와 호스트 이름을 포함하고 있습니다.

다음으로, 캐시를 조사하는 데 사용할 수 있는 명령을 알아보겠습니다.