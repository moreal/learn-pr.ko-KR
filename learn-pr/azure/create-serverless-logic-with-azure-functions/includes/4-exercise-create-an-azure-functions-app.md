이 연습에서는 Azure 함수 앱을 만듭니다.

1. Azure 계정을 사용하여 [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.
1. Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 후 **계산 > 함수 앱**을 선택하여 함수 앱 ‘만들기’ 블레이드를 엽니다.
  ![차례로 선택된 *리소스 만들기*, *계산*, *함수 앱*을 강조 표시하는 Azure Portal의 스크린샷입니다.](../images/4-create-function-app-blade.png)
1. 전역으로 고유한 앱 이름을 선택합니다. 서비스의 기준 URL 역할을 합니다. 예를 들어 **escalator-functions-xxxxxxx**로 이름을 지정할 수 있습니다. 여기서 xxxxxxx는 이니셜 및 출생 연도로 바꿀 수 있습니다. 이 값이 전역적으로 고유하지 않은 경우 다른 조합을 사용해 볼 수 있습니다. 유효한 문자는 a-z, 0-9 및 -입니다.
1. 함수 앱을 호스트할 Azure 구독을 선택합니다.
1. **escalator-functions-group**이라는 새 리소스 그룹을 만듭니다. 리소스 그룹을 사용하여 이 모듈에서 사용되는 모든 리소스를 저장하면 나중에 정리에 도움이 됩니다.
1. OS로 **Windows**를 선택합니다.
1. Azure의 서버리스 기능을 활용할 수 있도록, **호스팅 플랜**으로 **소비 플랜**을 선택합니다.
1. 자신 또는 고객과 가장 가까운 지역을 선택합니다.
1. 새 저장소 계정을 만들고 이름을 **escalator functions**로 지정합니다.
1. Azure Application Insights가 **켜져** 있는지 확인하고 자신(또는 고객)과 가장 가까운 지역을 선택합니다.
완료한 후 구성이 다음 스크린샷의 구성과 유사해야 합니다.

  ![이전 지침에 따라 모든 필드가 구성된 함수 앱 *만들기* 구성 화면의 스크린샷입니다.](../images/4-create-function-app-settings.png)

1. **만들기**를 선택합니다. 배포에 몇 분 정도 걸립니다. 완료되면 알림이 표시됩니다.

## <a name="verify-your-azure-function-app"></a>Azure 함수 앱 확인

1. Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 선택합니다. 그러면 사용 가능한 그룹 목록에 **escalator-functions-group**이 표시됩니다.
  ![Azure Portal의 보기에 **escalator-functions-group** 리소스 그룹이 있는 리소스 그룹 화면의 스크린샷입니다.](../images/4-resource-group.png)
1. **escalator-functions-group**을 선택합니다. 그러면 다음과 유사한 리소스 목록이 표시됩니다.
  ![App Service 계획, 저장소 계정, Application Insights 및 App Service에 대한 항목을 포함하여 **escalator-functions-group** 그룹에 있는 모든 리소스의 스크린샷입니다.](../images/4-resource-list.png)

App Service로 나열된 번개 모양 아이콘이 있는 항목은 새로운 함수 앱입니다. 
