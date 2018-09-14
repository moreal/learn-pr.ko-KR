결국 클라우드 내의 코드를 호스트 해야 합니다. Azure 기술을 사용 하 여이 작업을 수행 하려는 경우 Azure Functions

이 강의에 배웁니다.

- Azure 함수 앱을 만드는 방법 및 `JavaScript` Http 트리거.
- 실행 및 Azure 함수를 로컬로 디버그 하는 방법.

## <a name="create-an-azure-function-project"></a>Azure 함수 프로젝트 만들기

Azure 함수 프로젝트는 여러 함수에 대 한 컨테이너입니다. 다양 한 방법으로;에서 트리거되는 함수 함수 HTTP 요청을 만들어 트리거 수 됩니다 것입니다.

여러 가지 방법으로 Azure 함수를 만들려면 이 모듈에서 이전에 설치한는 Azure Functions 확장을 사용 하 여 Visual Studio Code를 사용 하려고 합니다.

함수 프로젝트를 먼저 만들어 보겠습니다.

1. 형식 <kbd>Ctrl</kbd>+<kbd>P</kbd> 여 명령 팔레트를 열고 다음에 대 한 검색 및 선택 `Azure Functions: Create New Project...`

   > **참고**
   >
   > 와 같은 일부 파일을 덮어쓸 것인지 궁금할 `.gitignore`, 답변 **없습니다** 모든!

   ![새 프로젝트 만들기](/media-drafts/7.create-new-project.png)

2. (첫 번째 옵션은 현재 폴더 라고 하는 데 사용) 하 여 함수 앱을 만드는 폴더 선택

   ![폴더 선택](/media-drafts/7.select-folder.png)

3. 선택 `JavaScript` 원하는 언어입니다.

   ![언어 선택](/media-drafts/7.select-language.png)

4. 위의 완료 하는 경우 표시 됩니다는 아래 폴더에 생성 된 파일

   ![만든 앱](/media-drafts/7.app-created.png)

## <a name="create-an-azure-function"></a>Azure Function 만들기

다음 보겠습니다 설정 함수를 만드는 Azure 자체에 HTTP 요청에 응답 하는 코드 조각입니다.

다시 Visual Studio 코드 확장을 사용 하는 것입니다.

1.  형식 <kbd>Ctrl</kbd>+<kbd>P</kbd> 여 명령 팔레트를 열고 다음에 대 한 검색 및 선택 `Azure Functions: Create Function...`

    ![새 함수 만들기](/media-drafts/7.create-function.png)

2.  함수 프로젝트를 이전에 만든 위치 폴더를 선택 (첫 번째 옵션은 현재 폴더 라고 하는 데 사용)

    ![폴더 선택](/media-drafts/7.select-current-project.png)

3.  에 만들기는 _HTTP 트리거_, 이므로 해당 옵션을 선택 합니다.

    ![폴더 선택](/media-drafts/7.select-trigger.png)

4.  입력 `MojifyImage` 만들려는 함수의 이름으로

    ![이름 선택](/media-drafts/7.choose-function-name.png)

5.  선택 `Anonymous` 인증 수준으로

    > 참고: 선택 하 여 `Anonymous` 함수 전 세계에 개방 되어 안전 하지 않은 합니다.

    ![이름 선택](/media-drafts/7.choose-auth-level.png)

## <a name="run-the-function-locally"></a>로컬에서 함수 실행

사용 하 여 함수 프로젝트를 시작 프로젝트를 변환한 다음이 명령을 성공적으로 완료 되 면을 _HTTP 트리거_ 함수 호출 `MojifyImage`합니다.

모든 항목이 작동 하도록 함수 앱을 실행할 수 로컬에서 다음과 같이 합니다.

```bash
func host start
```

함수 런타임에서 로컬로;이 시작 유사한 결과가 표시 됩니다 모든는 최종적으로 올바르게 작동 하는 경우는 아래이 콘솔에 인쇄 합니다.

```
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

> **참고**
>
> Azure Functions 런타임 설치의 장점 중 하나 이며 프로덕션에서 함수를 실행 하는 동일한 기본 기술을 사용 하 여 로컬로 함수를 실행할 수 있도록 합니다.

함수가 제대로 실행 되도록이 브라우저 창에서 출력 콘솔에 인쇄 된 URL를 방문 합니다.

![작동 하는 함수 앱](/media-drafts/7.default-function-app-working.png)

## <a name="debug-the-function-locally"></a>함수를 로컬로 디버그

> **중요**
>
> 종료 했는지를 `func host start` Visual Studio Code를 사용 하 여 디버그 하기 전에 방금 실행 한 명령입니다.

또한 실행할 수 있습니다 _디버그 및_ visual studio 코드 내에서 응용 프로그램입니다.

중단점을 추가 합니다 `index.js` JavaScript 함수의 맨 위에 있는 파일을 다음과 같이 합니다.

![중단점 추가](/media-drafts/7.add-breakpoint.png)

디버그 메뉴에서 디버그 모드를 처음 방문할에서 함수를 실행 하려면 <kbd>Cmd<kbd> + <kbd>Shift<kbd> + <kbd>D<kbd>합니다.

선택 `Attach to JavaScript Functions` 마지막 디버그 세션을 시작 하려면 녹색 삼각형을 누르기 전에 디버그 구성에서 합니다.

> **참고**
>
> `Attach to JavaScript Functions` 함수 프로젝트를 만들 때 디버그 구성이 자동으로 추가 되었습니다.

또는 눌러 수 있습니다 <kbd>F5<kbd> 에서 아무 곳 이나 응용 프로그램에서이 마지막 디버그 구성을 실행 합니다.

`func host start` 터미널 열어야 결국를 사용 하 여 동일한 위와 같이 출력; 명령을 실행할 수 있습니다.

```
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

디버그 메뉴 표시줄 나타납니다도 참조 디버깅 하는 것 이므로 다음과 같이 합니다.

![디버그 메뉴](/media-drafts/7.debug-menu-bar.png)

이제 중단점에서 중단 위의 URL를 방문할 때 지정한 함수를 단계별로 실행할 수 있습니다.

<!-- TODO Find Link -->

할 수 있습니다 [자세한](https://code.visualstudio.com/docs/editor/debugging) Visual Studio Code에서 디버깅 하는 방법에 대 한
