작성하는 다른 모든 응용 프로그램 코드와 마찬가지로, 봇 코드에 대한 변경 사항도 프로덕션에 배포하기 전에 로컬로 테스트하고 디버그해야 합니다. 봇을 디버그하는 데 도움이 되도록 Microsoft는 [Bot Framework Emulator](https://emulator.botframework.com/)를 제공합니다. 이 단원에서는 Visual Studio Code와 에뮬레이터를 사용하여 봇을 디버그하는 방법을 배웁니다.

1. Microsoft Bot Framework Emulator가 설치되어 있지 않은 경우 지금 시간을 내 설치하세요. https://emulator.botframework.com/에서 다운로드할 수 있습니다. Windows, macOS 및 Linux용 버전이 제공되어 있습니다.

1. Visual Studio Code의 통합 터미널에서 다음 명령을 실행하여 RESTful 웹 서비스를 빌드하고 사용하는 데 필요한 인기 Node 패키지인 [Restify](http://restify.com/)를 설치합니다.

    ```
    npm install restify
    ```

1. 다음 명령에 대해 이 단계를 반복하여 [Node.js용 Microsoft Bot Framework Bot Builder SDK](https://docs.microsoft.com/bot-framework/nodejs/bot-builder-nodejs-quickstart)를 설치합니다.

    ```
    npm install botbuilder
    npm install botbuilder-azure
    npm install botbuilder-cognitiveservices
    ```

1. Visual Studio Code 작업 막대에서 **탐색기** 단추를 클릭합니다. 그런 다음, **app.js**를 선택하여 코드 편집기에서 엽니다. 이 파일에는 Azure Bot Service에서 생성되었고 Azure Portal에서 다운로드된, 봇을 구동하는 코드가 포함되어 있습니다.

    ![app.js 열기](../media-draft/5-vs-select-index-js.png)

1. **app.js**의 콘텐츠를 다음 코드로 바꾸고 파일을 저장합니다.

    ```JavaScript
    "use strict";
    var builder = require("botbuilder");
    var botbuilder_azure = require("botbuilder-azure");
    
    var useEmulator = true; 
    var userName = ""; 
    var yearsCoding = ""; 
    var selectedLanguage = "";
    
    var connector = useEmulator ? new builder.ChatConnector() : new botbuilder_azure.BotServiceConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword      
    });
    
    var bot = new builder.UniversalBot(connector);
    
    bot.dialog('/', [
    
    function (session) {
        builder.Prompts.text(session, "Hello, and welcome to QnA Factbot! What's your name?");
    },
    
    function (session, results) {
        userName = results.response;
        builder.Prompts.number(session, "Hi " + userName + ", how many years have you been writing code?"); 
    },
    
    function (session, results) {
        yearsCoding = results.response;
        builder.Prompts.choice(session, "What language do you love the most?", ["C#", "Python", "Node.js", "Visual FoxPro"]);
    },
    
    function (session, results) {
        selectedLanguage = results.response.entity;   
    
        session.send("Okay, " + userName + ", I think I've got it:" +
                    " You've been writing code for " + yearsCoding + " years," +
                    " and prefer to use " + selectedLanguage + ".");
    }]);
     
    var restify = require('restify');
    var server = restify.createServer();

    server.listen(3978, function() {
        console.log('test bot endpoint at http://localhost:3978/api/messages');
    });

    server.post('/api/messages', connector.listen());    
    ```

1. 왼쪽 여백을 클릭하여 줄 20, 25 및 30에 중단점을 설정합니다.
 
    ![app.js에 중단점 추가](../media-draft/5-vs-add-breakpoints.png)

1. 작업 막대에서 **디버그** 단추를 클릭한 후 초록색 화살표를 클릭하여 디버깅 세션을 시작합니다. 디버그 콘솔에 “http://localhost:3978/api/messages의 봇 엔드포인트 테스트”가 표시되는지 확인합니다.
 
    ![디버거 시작](../media-draft/5-vs-launch-debugger.png)

1. 이제 봇 코드가 로컬에서 실행됩니다. Bot Framework Emulator를 시작하고 **새 봇 구성 만들기**를 클릭합니다. 이전 단계의 디버그 콘솔에 표시된 봇 이름과 봇 URL을 입력합니다. **저장 및 연결**을 클릭한 후 선택한 위치에 구성 파일을 저장합니다.

    > 이후에는 “My Bots”(내 봇)에서 봇 이름을 클릭하기만 하면 해당 봇에 다시 연결할 수 있습니다.

    ![봇에 연결](../media-draft/5-new-bot-configuration.png)

1. 에뮬레이터 아래쪽의 상자에 “hi”를 입력하고 **Enter** 키를 누릅니다. Visual Studio Code가 **app.js**의 20번째 줄에서 줄 바꿈하는지 확인합니다. 그런 다음, Visual Studio Code의 디버깅 도구 모음에서 **계속** 단추를 클릭하고 에뮬레이터로 돌아가서 봇의 응답을 확인합니다.
 
    ![디버거에서 계속하기](../media-draft/5-continue-debugging.png)

1. 봇이 일련의 질문을 합니다. 질문에 답하고 중단점에 도달할 때마다 Visual Studio Code에서 **계속**을 클릭합니다. 완료되면 디버깅 도구 모음에서 **중지** 단추를 클릭하여 디버깅 세션을 종료합니다.

이제 봇은 완전히 작동하며 여러분은 Microsoft Bot Framework Emulator에서 봇을 로컬로 실행하여 디버그하는 방법을 알았습니다. 다음 단계에서는 게시한 기술 자료에 봇을 연결하여 더욱 지능적인 봇을 만듭니다.