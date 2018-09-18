<span data-ttu-id="7f2e1-101">이 단원에서는 이전에 빌드한 QnA Maker 기술 자료에 봇을 연결하여 봇이 지능적인 대화를 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-101">In this unit, you will connect your bot to the QnA Maker knowledge base you built earlier so the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="7f2e1-102">기술 자료에 연결하려면 QnA Maker 포털에서 일부 정보를 검색하여 Azure Portal에 복사하고 봇 코드를 업데이트한 후 Azure에 봇을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-102">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="7f2e1-103">[QnA Maker 포털](https://www.qnamaker.ai/)로 돌아가서 오른쪽 위에 있는 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-103">Return to the [QnA Maker portal](https://www.qnamaker.ai/) and click your name in the upper-right corner.</span></span> <span data-ttu-id="7f2e1-104">드롭다운 메뉴에서 **엔드포인트 키 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-104">Select **Manage endpoint keys** from the menu that drops down.</span></span> <span data-ttu-id="7f2e1-105">**표시**를 클릭하여 기본 엔드포인트 키를 표시하고 **복사**를 클릭하여 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-105">Click **Show** to show the primary endpoint key, and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="7f2e1-106">그런 다음, 쉽게 바로 검색할 수 있도록 텍스트 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-106">Then, paste it into a text file so you can easily retrieve it in a moment.</span></span>

1. <span data-ttu-id="7f2e1-107">페이지 맨 위 메뉴에서 **내 기술 자료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-107">Click **My knowledge bases** in the menu at the top of the page.</span></span> <span data-ttu-id="7f2e1-108">그런 다음, 이전에 만든 기술 자료에 대한 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-108">Then, click **View Code** for the knowledge base that you created earlier.</span></span>

1. <span data-ttu-id="7f2e1-109">첫 번째 줄의 기술 자료 ID와 두 번째 줄의 호스트 이름을 복사하여</span><span class="sxs-lookup"><span data-stu-id="7f2e1-109">Copy the knowledge base ID from the first line and the host name from the second line.</span></span> <span data-ttu-id="7f2e1-110">텍스트 파일에도 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-110">Paste them into a text file, as well.</span></span> <span data-ttu-id="7f2e1-111">그런 다음, 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-111">Then, close the dialog.</span></span> <span data-ttu-id="7f2e1-112">복사하는 호스트 이름에 “https://” 접두사를 포함하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-112">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![엔드포인트 기술 자료 ID와 호스트 이름이 강조 표시된 샘플 HTTP 요청을 보여주는 QnA Maker 포털의 스크린샷.](../media/6-copy-endpoint-info.png)

1. <span data-ttu-id="7f2e1-114">Azure Portal의 웹앱 봇으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-114">Return to the web app bot in the Azure portal.</span></span> <span data-ttu-id="7f2e1-115">왼쪽의 메뉴에서 **응용 프로그램 설정**을 클릭하고 이름이 “QnAKnowledgebaseId”, “QnAAuthKey” 및 “QnAEndpointHostName”인 응용 프로그램 설정을 찾을 때까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-115">Click **Application settings** in the menu on the left and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey," and "QnAEndpointHostName."</span></span> <span data-ttu-id="7f2e1-116">3단계에서 얻은 지식 기반 ID 및 호스트 이름과 1단계에서 얻은 엔드포인트 키를 이러한 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-116">Paste the knowledge base ID and host name obtained in Step 3 and the endpoint key obtained in Step 1 into these fields.</span></span> <span data-ttu-id="7f2e1-117">그런 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-117">Then, click **Save**.</span></span>

    ![응용 프로그램 설정 메뉴 항목과 적절한 설정 키가 강조 표시된 응용 프로그램 설정 세부 정보 및 봇 블레이드를 보여주는 Azure Portal 스크린 샷.](../media/6-enter-app-settings.png)

1. <span data-ttu-id="7f2e1-119">Visual Studio Code로 돌아가서 **app.js**의 콘텐츠를 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-119">Return to Visual Studio Code and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="7f2e1-120">그런 다음, 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-120">Then, save the file.</span></span>

    ```JavaScript
    var restify = require('restify');
    var builder = require('botbuilder');
    var botbuilder_azure = require("botbuilder-azure");
    var builder_cognitiveservices = require("botbuilder-cognitiveservices");

    // Setup Restify Server
    var server = restify.createServer();
    server.listen(process.env.port || process.env.PORT || 3978, function () {
        console.log('%s listening to %s', server.name, server.url);
    });

    // Create chat connector for communicating with the Bot Framework Service
    var connector = new builder.ChatConnector({
        appId: process.env.MicrosoftAppId,
        appPassword: process.env.MicrosoftAppPassword
    });

    // Listen for messages from users
    server.post('/api/messages', connector.listen());

    // Create your bot with a function to receive messages from the user
    var bot = new builder.UniversalBot(connector);

    var recognizer = new builder_cognitiveservices.QnAMakerRecognizer({
        knowledgeBaseId: process.env.QnAKnowledgebaseId,
        authKey: process.env.QnAAuthKey,
        endpointHostName: process.env.QnAEndpointHostName
    });

    var basicQnAMakerDialog = new builder_cognitiveservices.QnAMakerDialog({
        recognizers: [recognizer],
        defaultMessage: "I'm not quite sure what you're asking. Please ask your question again.",
        qnaThreshold: 0.3
    });

    bot.dialog('basicQnAMakerDialog', basicQnAMakerDialog);

    bot.dialog('/',
    [
        function (session) {
            session.replaceDialog('basicQnAMakerDialog');
        }
    ]);
    ```

    > [!Note]
    > <span data-ttu-id="7f2e1-121">30줄에 `QnAMakerDialog` 인스턴스를 만드는 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-121">The call to create a `QnAMakerDialog` instance on line 30.</span></span> <span data-ttu-id="7f2e1-122">Azure Bot Service로 빌드된 봇과 기술 자료로 빌드된 Microsoft QnA Maker를 통합하는 대화 상자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-122">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built Microsoft QnA Maker.</span></span>

1. <span data-ttu-id="7f2e1-123">Visual Studio Code의 작업 막대에서 **소스 제어** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-123">Click the **Source Control** button in the activity bar in Visual Studio Code.</span></span> <span data-ttu-id="7f2e1-124">메시지 상자에 “기술 자료에 연결됨”을 입력하고 확인 표시를 클릭하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-124">Type "Connected to knowledge base" into the message box, and click the check mark to commit your changes.</span></span> <span data-ttu-id="7f2e1-125">그런 다음, 줄임표를 클릭하고 **분기 게시** 명령을 사용하여 이러한 변경 내용을 원격 리포지토리로(따라서, Azure Web App으로)</span><span class="sxs-lookup"><span data-stu-id="7f2e1-125">Then, click the ellipsis and use the **Publish Branch** command to push these changes to the remote repository (and therefore.</span></span> <span data-ttu-id="7f2e1-126">푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-126">to the Azure Web App).</span></span>

1. <span data-ttu-id="7f2e1-127">Azure Portal의 웹앱 봇으로 돌아가서 왼쪽의 **웹 채팅에서 테스트**를 클릭하여 테스트 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-127">Return to the web app bot in the Azure portal and click **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="7f2e1-128">“세계에서 가장 인기 있는 소프트웨어 프로그래밍 언어는 무엇인가요?”를</span><span class="sxs-lookup"><span data-stu-id="7f2e1-128">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="7f2e1-129">채팅창 아래쪽에 있는 상자에 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-129">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="7f2e1-130">봇이 응답하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-130">Confirm that the bot responds.</span></span>

<span data-ttu-id="7f2e1-131">이제 봇이 기술 자료에 연결되었으므로 마지막 단계로 실제 환경에서 봇을 자유롭게 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-131">Now that the bot is connected to the knowledge base, the final step is to test it in the wild.</span></span> <span data-ttu-id="7f2e1-132">Skype를 사용하면 그 어떤 환경보다도 자유롭게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f2e1-132">And what could be wilder than testing it with Skype?</span></span>
