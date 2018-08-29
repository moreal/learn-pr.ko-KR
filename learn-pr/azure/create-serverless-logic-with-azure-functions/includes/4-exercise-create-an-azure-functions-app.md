이 연습에서는 Azure 함수 앱을 만듭니다.

1. Azure 계정을 사용하여 [Azure Portal](https://portal.azure.com)에 로그인합니다.
1. Azure Portal의 왼쪽 위 모서리에서 **리소스 만들기** 단추를 선택한 후 **계산 > 함수 앱**을 선택합니다.
  ![함수 앱 리소스 만들기](../images/4-create-function-app-blade.png)
1. 전역으로 고유한 앱 이름을 선택합니다. 서비스의 기준 URL 역할을 합니다. **escalator-functions-xxxxxxx**로 명명할 수 있습니다. 여기서 xxxxxxx는 이니셜 및 출생 연도로 바꿀 수 있습니다. 이 값이 전역적으로 고유하지 않은 경우 다른 조합을 사용해 볼 수 있습니다. 유효한 문자는 a-z, 0-9 및 -입니다.
1. 함수 앱을 호스트할 Azure 구독을 선택합니다.
1. **escalator-functions-group**이라는 새 리소스 그룹을 만듭니다. 나중에 정리하는 데 유용합니다.
1. OS로 **Windows**를 선택합니다.
1. Azure의 서버리스 기능을 활용할 수 있도록, **호스팅 플랜**으로 **소비 플랜**을 선택합니다.
1. 자신 또는 고객과 가장 가까운 지역을 선택합니다.
1. 새 저장소 계정을 만들고 이름을 **escalatorfunctions**로 지정합니다.
1. Azure Application Insights가 **설정** 상태인지 확인하고 가장 가까운 지역을 선택합니다.
1. **만들기**를 선택합니다. 배포에 몇 분 정도 걸립니다. 완료되면 알림이 표시됩니다.
  ![함수 앱 설정](../images/4-create-function-app-settings.png)

## <a name="verify-your-azure-function-app"></a>Azure 함수 앱 확인

1. Azure Portal의 왼쪽 메뉴에서 **리소스 그룹**을 선택합니다. 그러면 사용 가능한 그룹 목록에 **escalator-functions-group**이 표시됩니다.
  ![리소스 그룹](../images/4-resource-group.png)
1. **escalator-functions-group**을 선택합니다. 그러면 다음과 유사한 리소스 목록이 표시됩니다. ![리소스 목록](../images/4-resource-list.png)
