### <a name="exercise-5-create-a-nodejs-app-that-uses-the-model"></a>연습 5: 모델을 사용하는 Node.js 앱 만들기

Microsoft Custom Vision Service의 진정한 강점은 개발자가 [Custom Vision 예측 API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)를 사용하여 자신의 응용 프로그램에 편리하게 인텔리전스를 통합할 수 있다는 것입니다. 이 연습에서는 Visual Studio Code를 사용하여 이전 연습에서 빌드하여 학습한 모델을 사용하도록 Artwork라는 앱을 수정합니다.

1. Node.js가 시스템에 설치되어 있지 않으면 https://nodejs.org로 이동하여 사용 중인 운영 체제에 대한 최신 LTS 버전을 설치합니다.

    > Node.js가 설치되어 있는지 잘 모르는 경우 명령 프롬프트 또는 터미널 창을 열고 **node -v**를 입력합니다. Node.js 버전 번호가 표시되지 않으면 Node.js가 설치되지 않은 것입니다. 6.0보다 오래된 Node.js 버전이 설치되어 있는 경우 최신 버전을 다운로드하여 설치하는 것이 좋습니다.

1. Visual Studio Code가 워크스테이션에 설치되어 있지 않으면 지금 http://code.visualstudio.com으로 이동하여 설치하세요.

1. Visual Studio Code를 시작하고 **파일** 메뉴에서 **폴더 열기...** 를 선택합니다. 다음 대화 상자에서 랩 리소스에 포함된 “Client\Artworks” 폴더를 선택합니다.

    ![Artworks 폴더 선택](../images/fe-select-folder.png)

    _Artworks 폴더 선택_ 

1. **보기** > **통합 터미널** 명령을 사용하여 Visual Studio Code에서 통합 터미널 창을 엽니다. 그런 다음, 통합 터미널에서 다음 명령을 실행하여 앱에 필요한 패키지를 로드합니다.

    ```
    npm install
    ```

1. Custom Vision Service 포털의 Artwork 프로젝트로 돌아가서 **성능**을 클릭한 후 **기본값으로**를 클릭하여 모델의 최근 반복을 기본 반복으로 지정합니다. 

    ![기본 반복 지정](../images/portal-make-default.png)

    _기본 반복 지정_ 

1. 앱을 실행하고 이를 사용하여 Custom Vision Service를 호출하기 전에, 엔드포인트 및 권한 부여 정보를 포함하도록 수정해야 합니다. 이를 위해 **예측 URL**을 클릭합니다.

    ![예측 URL 정보 보기](../images/portal-prediction-url.png)

    _예측 URL 정보 보기_ 

1. 다음에 표시되는 대화 상자에는 URL을 통해 이미지를 업로드하기 위한 URL과 로컬 이미지를 업로드하기 위한 URL이 각각 표시됩니다. 이미지 파일의 예측 API URL을 클립보드로 복사합니다. 

    ![예측 API URL 복사](../images/copy-prediction-url.png)

    _예측 API URL 복사_ 

1. Visual Studio Code로 돌아가서 **predict.js**를 클릭하여 코드 편집기에서 엽니다.

    ![predict.js 열기](../images/vs-predict-file.png)

    _predict.js 열기_ 

1. 줄 3의 “PREDICTION_ENDPOINT”를 클립보드의 URL로 바꿉니다.

    ![예측 API URL 추가](../images/vs-prediction-endpoint.png)

    _예측 API URL 추가_ 

1. Custom Vision Service 포털로 돌아가서 예측 API 키를 클립보드에 복사합니다. 

    ![예측 API 키 복사](../images/copy-prediction-key.png)

    _예측 API 키 복사_ 

1. Visual Studio Code로 돌아가서 **predict.js**의 줄 4에 있는 “PREDICTION_KEY”를 클립보드의 API 키로 바꿉니다.

    ![예측 API 키 추가](../images/vs-prediction-key.png)

    _예측 API 키 추가_ 

1. **predict.js**에서 아래로 스크롤하고 줄 34부터 시작되는 코드 블록을 검사합니다. 이 부분은 AJAX를 사용하여 Custom Vision Service 호출을 수행하는 코드입니다. Custom Vision Service API를 사용하는 것은 REST 엔드포인트에 대해 인증된 단순 POST를 수행하는 것만큼 쉽습니다.

    ![예측 API 호출](../images/vs-code-block.png)

    _예측 API 호출_ 

1. Visual Studio Code의 통합 터미널로 돌아가서 다음 명령을 실행하여 앱을 시작합니다.

    ```
    npm start
    ```

1. Artworks 앱이 시작되고 다음과 같은 창을 표시하는지 확인합니다.

    ![Artworks 앱](../images/app-startup.png)

    _Artworks 앱_ 

Artworks는 Node.js 및 [Electron](https://electron.atom.io/)으로 작성한 플랫폼 간 앱입니다. 따라서 Windows, macOS 및 Linux에서 실행할 수 있습니다. 다음 연습에서 이 앱을 사용하여 이미지를 해당 이미지를 그린 화가별로 분류합니다.