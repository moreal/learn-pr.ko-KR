필요한 모든 Azure 기능을 만들었습니다 및 로컬로 실행할 수 있습니다.

이 강의에 Slack을 사용 하 여 Azure 함수를 연결 하 고 만들기를 Slack _슬래시_ Azure 함수를 호출 하 고 slack 창의 결과 mojified 이미지를 표시 하는 명령입니다.

이 강의의 끝에서 배웁니다.

- Slack 앱을 만들고 Azure Function 끝점과 슬래시 명령을 연결 하는 방법입니다.
- 클라우드로 배포 하지 않고 슬래시 명령을 로컬로, 테스트 하는 방법.

## <a name="using-ngrok-to-develop-with-slash-commands"></a>Ngrok를 사용한 개발 슬래시 명령을 사용 하 여

이 Azure functions는 현재 프로그램만; 로컬로 실행 그러나 slack 클라우드, 인터넷에서에서 실행 됩니다.

Slack 설정할 때 _슬래시_ 슬래시 명령을 다른 사용자가 실행 될 때마다 호출 되는 공용 URL을 요청 하려는 다음 섹션에서는 명령입니다.

제공 하려는 우리의 `RespondToSlackCommand` 있지만 URL이 로컬 컴퓨터에만 존재 합니다.

수 부여 어떻게 서비스 클라우드 액세스의 리소스에 로컬 컴퓨터의 개발에 대 한?

이 문제에 적합 한 솔루션은 `ngrok` 인터넷에서 로컬 컴퓨터에 보안 터널을 만드는 도구입니다.

1. Visit https://ngrok.com/download
2. 다운로드 및 설치 지침에 따라는 `ngrok` 로컬 컴퓨터에 패키지 합니다.
3. 실행 `ngrok http 7071` 터미널에서.
   ![ngrok](/media-drafts/9.ngrok.png)
4. 이 끝나는 공용 URL을 출력 `ngrok.io` 예: `http://bbade778.ngrok.io`를 적어이 경우 다음 섹션에서 필요 합니다.

> **참고**
>
> 이렇게 `http://*.ngrock.io` 사용한 처럼 사용할 수 있는 URL `http://localhost:7071`, 이미지를 사용 하 여 사용해 같이 `http://[ngrok-url]/api/MojifyImage?imageUrl=[url-to-an-image]`

## <a name="create-a-slack-app"></a>Slack 앱 만들기

슬래시 명령을 slack 앱에서 slack의 일부로 존재 _bot_합니다.

방문 [Slack 앱 만들기](https://api.slack.com/apps/new)

선택는 `App Name` 와 연결 된 `Workspace` 누릅니다 하 고이 자습서의 시작 부분에 만든 `Create App`, 다음과 같이:

![Slack 앱 만들기](/media-drafts/9.create-slack-app.png)

만든 후 다음 슬래시 명령을 만들고 slack 앱으로 이동 해야 합니다.

## <a name="create-a-slash-command"></a>슬래시 명령 만들기

클릭 된 `Slash Commands` 메뉴 항목입니다.

![슬래시 명령](/media-drafts/9.slash-commands.png)

`Create New Command`을 클릭합니다.

- 슬래시 명령에 대해 원하는 어떤 이름이 입력 된 `command` 필드입니다.
- ngrok 공용 URL을 입력 합니다 `Request URL` 필드

  > **중요 한**
  >
  > 추가 해야 `/api/RespondToSlackCommand` url

- 짧은 설명 및 사용 현황 힌트를 추가 합니다.
- 키를 누릅니다 `Save`

![슬래시 명령](/media-drafts/9.create-slash-command.png)

한 번 저장 화면 표시 다음과 같이 합니다.

![슬래시 명령 성공](/media-drafts/9.create-slash-commands-success.png)

## <a name="install-the-slack-app-to-the-workspace"></a>작업 영역에 slack 앱을 설치 합니다.

Slack 앱이 작업 영역에서 사용할 수 있습니다, 전에 설치 해야 합니다.

1. 선택 된 `Basic Information` 메뉴 항목

2. 확장 된 `Install your app to your workspace` 옵션과 키를 눌러를 `Install app to workspace` 단추입니다.

   ![작업 영역에 앱을 설치 합니다.](/media-drafts/9.install-app-to-workspace.png)

3. 응용 프로그램을 인증 하도록 요청할 수 있습니다이 다음과 같이 합니다.

   ![앱 작업 영역에 인증](/media-drafts/9.authenticate-slack-app.png)

## <a name="try-it-out"></a>체험

슬래시 명령을 만들고 보겠습니다 ngrok 링크를 통해 Azure Functions는 로컬로 실행 중인 인스턴스에 연결 된 테스트 합니다.

1. Slack 앱과 연결한 slack 작업 영역으로 이동 합니다.
2. 모든 형식과 채팅 창으로 이동 `/mojify` (또는 앱에 부여 했습니다 이름)
3. 모든 것이 제대로 작동 하는 경우 표시 됩니다 `mojify` 옵션으로

   ![Mojify 확인](/media-drafts/9.slack-check-mojify.png)

4. 이제 입력 `/mojify` enter, 이미지 URL을 추가 하 고 다음과 같이 합니다.

   ![형식 Mojify](/media-drafts/9.slack-type-mojify.png)
