전문 스포츠 통계를 추적하고 결과를 쿼리할 앱과 API를 제공하는 회사에서 일한다고 가정하겠습니다. 이 회사는 스포츠 팬들이 실시간/과거 게임 및 기록을 추적하고 검토하는 데 도움을 줍니다. 사용자는 “John Smith가 왼손 투수를 상대로 홈런을 친 횟수는 몇 번인가요?”와 같은 자연어 검색을 사용하여 팀 통계를 요청할 수도 있습니다.

플레이오프 기간과 같은 최대 수요 기간에는 백 엔드 서비스 용량이 수요를 맞추지 못하므로 서비스 응답 시간이 느려집니다. 사용자를 위해 성능을 향상하고 백 엔드 및 데이터 저장소 서비스의 워크로드를 줄이려고 합니다. 메트릭에 따르면 반환된 데이터의 50%에서 80%가 읽기 전용이거나 최근에 요청된 값입니다. 일반적으로 사용되는 데이터의 캐시를 구현하면 성능을 향상하고 대기 시간을 줄일 수 있습니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Redis Cache란 무엇이며 Redis Cache를 사용하여 수행할 수 있는 작업은 무엇인지 설명합니다.
- Redis Cache를 사용하기 위한 디자인과 플랜을 만듭니다.
- Azure에서 Redis Cache를 프로비전합니다.
- 웹앱을 캐시에 연결합니다.

## <a name="prerequisites"></a>필수 조건

- 앱 개발 경험
- 앱에서 데이터를 사용해 본 경험