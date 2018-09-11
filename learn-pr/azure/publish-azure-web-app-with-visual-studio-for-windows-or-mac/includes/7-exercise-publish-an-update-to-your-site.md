Alpine Ski House 웹앱이 가동되어 실행 중이지만 이제 상사에게 보여 주어야 합니다. 사이트를 업데이트하고 Azure에 업데이트를 게시해야 합니다.

## <a name="update-your-web-app"></a>웹앱 업데이트

### <a name="replace-the-boilerplate-code"></a>상용구 코드 바꾸기

1. **Pages** 폴더에서 **About.cshtml** 파일을 엽니다.
1. 코드 하단에서 `<p> Use this area to provide additional information. </p>`을 찾습니다.
1. 상용구 텍스트를 `Welcome to the Alpine Ski House!`로 바꿉니다.
1. 파일을 저장합니다.
1. **About.cshtml.cs** 파일을 엽니다.
1. `Message` 문자열을 **Alpine Ski House is the premier ski hill in Northeast.** 로 바꿉니다.
1. 파일을 저장합니다.

### <a name="publish-your-updates"></a>업데이트 게시

1. 솔루션 탐색기에서 프로젝트를 마우스 오른쪽 단추로 클릭합니다.
1. **게시**를 선택합니다. [웹 사이트]-웹 배포를 포함하는 옵션이 있어야 합니다.
1. 사이트를 선택하면 Visual Studio에서 Azure에 변경 내용을 전송합니다.

### <a name="view-your-changes"></a>변경 내용 보기

변경 내용을 게시하면 Visual Studio가 브라우저에서 사이트를 엽니다. **정보** 페이지로 이동하여 변경 내용이 반영되었는지 확인하세요.

## <a name="congrats"></a>축하합니다!

Visual Studio 2017을 사용하여 웹앱을 성공적으로 업데이트했습니다.
