Xamarin 및 Azure 함수와 Twilio 바인딩을 사용하여 플랫폼 간 모바일 앱을 만들었습니다.

## <a name="clean-up"></a>정리

<!---TODO: Update for sandbox?--->

이 Azure Functions 응용 프로그램의 작업이 완료되면 Azure Portal에서 자습서 중에 만들어진 모든 리소스를 삭제할 수 있습니다.

1. Visual Studio에서 ‘보기->클라우드 탐색기’를 선택합니다.**

1. 이 패널의 맨 위 드롭다운에서 ‘리소스 그룹’을 선택합니다.**

1. 리소스 그룹을 만드는 데 사용한 구독을 확장합니다. “ImHere” 리소스 그룹을 마우스 오른쪽 단추로 클릭하고 ‘포털에서 열기’를 선택합니다.**

    ![클라우드 탐색기 창에서 포털의 리소스 그룹을 엽니다.](../media/9-open-resource-group-in-portal.png)

1. 필요한 경우 브라우저에서 Azure Portal에 로그인합니다.

1. 포털이 “ImHere” 리소스 그룹에서 열립니다. **리소스 그룹 삭제** 단추를 클릭합니다.

1. 리소스 그룹의 이름을 입력하여 삭제를 확인하고 **삭제**를 클릭합니다.

## <a name="summary"></a>요약

이 모듈에서는 다음을 수행하는 방법을 알아보았습니다.

- Xamarin.Essentials를 사용하는 플랫폼 간 Xamarin.Forms 앱을 만듭니다.
- ViewModel에서 응용 프로그램 논리와 함께 XAML을 사용하여 플랫폼 간 UI를 만들고 ViewModel의 속성을 UI에 바인딩합니다.
- 사용자 위치를 감지합니다.
- HTTP 트리거를 사용하여 Azure 함수를 만들고 로컬에서 실행합니다.
- 모바일 앱에서 Azure 함수를 호출하고 데이터를 JSON으로 전달합니다.
- Azure 함수를 Twilio에 바인딩하여 SMS 메시지를 보냅니다.
- Azure 함수를 Azure에 게시합니다.