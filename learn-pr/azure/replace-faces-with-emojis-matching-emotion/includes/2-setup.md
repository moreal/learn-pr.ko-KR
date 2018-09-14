먼저 먼저 몇 가지 계정으로 설정 하 고 시작 코드를 로컬에 복제 되었는지 확인 해야 합니다.

## <a name="create-an-azure-account"></a>Azure 계정 만들기

Azure 계정이 필요 합니다. 아직 없는 경우 등록 하면이 링크를 수행 하 여 서비스의 무료 일년을 받고:

[Azure 계정을 만들려면](https://azure.microsoft.com/free)

## <a name="create-a-slack-workspace"></a>Slack 작업 영역 만들기

Slack 명령을 만든 작업 영역을 slack에 대 한 관리자 권한이 필요 합니다.

따라서 새로운 slack 작업 영역을 만들거나 기존 작업 영역에 대 한 관리자 권한이 있는지 확인 해야 하거나 다음과 같이 합니다.

[Slack 작업 영역을 만들려면](https://slack.com/create)

## <a name="clone-the-starter-code"></a>시작 코드를 복제 합니다.

이 모듈에서 최대한, 시작 코드를 복제 하 고 단계별 지침에 따라 권장 합니다.

시작 하기 위한 몇 가지 초기 부트스트랩 코드 뿐만 아니라 응용 프로그램을 완료 하는 데 필요한 모든 코드가 제공 됩니다.

시작 하려면이 항목을 복제 _stater_ 로컬 컴퓨터에는 코드입니다.

```bash
git clone https://github.com/jawache/mojifier-slack.git
```

사용 하 여 필요한 패키지를 설치 합니다.

```bash
npm install
```

이 모듈을 단계별로 수행 하는 것이 좋습니다. 그러나 고정 될 도움이 필요한 경우 다음 있습니다에서 완성 된 코드는 `completed` 분기 같이:

```bash
git checkout completed
```

사용 하 여 응용 프로그램을 작성 하려는 `TypeScript`합니다. NodeJS 알 수 없습니다 하는 방법 **실행** `TypeScript`우리가 개발 하는 대로 변환 해야 하므로, 우리의 `TypeScript` 코드를 `JavaScript`합니다. 변환을 수행 하는 필수 도구 모든 변환 하도록 위의 단계에서 설치한는 `TypeScript` 이 명령을 실행 합니다.

```bash
npm run build
```

위의 명령은 다음에 성공적으로 실행 된 경우에 `*.ts` 파일에 표시 됩니다 `*.js` 및 `*.map` 파일입니다.

> **참고**
>
> 이 명령은 터미널 셸에서 실행 유지,이 TypeScript 파일에 변경 내용을 감시 하 고 JavaScript 파일에 변환 합니다.
>
> 파일이 어떤 이유로 변환 시작 다음 콘솔 터미널 창에서 출력을 확인 하는 경우에 TypeScript 코드에 오류가 나타날 수 있습니다.

## <a name="install-visual-studio-code--azure-functions-extention"></a>Visual Studio Code 및 Azure Functions 확장 설치

여러 가지 방법으로 Visual Studio Code 및 연결 된 Azure Functions 확장 플러그 인을 사용 하 여 Azure에이 모듈에서는 Azure에서 상호 작용할 수 있습니다.

1. 다운로드 하 여 visual studio code 설치 https://code.visualstudio.com/

2. 다음 지침에 따라 Azure 함수 코드 확장을 설치 합니다. https://code.visualstudio.com/tutorials/functions-extension/getting-started
