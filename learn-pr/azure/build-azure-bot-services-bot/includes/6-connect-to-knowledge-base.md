<span data-ttu-id="dbfc8-101">이 단원에서는 이전에 빌드한 QnA Maker 기술 자료에 봇을 연결하여 봇이 지능적인 대화를 수행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-101">In this unit, you will connect your bot to the QnA Maker knowledge base you built earlier so the bot can carry on an intelligent conversation.</span></span> <span data-ttu-id="dbfc8-102">기술 자료에 연결하려면 QnA Maker 포털에서 일부 정보를 검색하여 Azure Portal에 복사하고 봇 코드를 업데이트한 후 Azure에 봇을 다시 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-102">Connecting to the knowledge base involves retrieving some information from the QnA Maker portal, copying it into the Azure portal, updating the bot code, and then redeploying the bot to Azure.</span></span>

1. <span data-ttu-id="dbfc8-103">[QnA Maker 포털](https://www.qnamaker.ai/)로 돌아가서 오른쪽 위에 있는 이름을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-103">Return to the [QnA Maker portal](https://www.qnamaker.ai/) and click your name in the upper-right corner.</span></span> <span data-ttu-id="dbfc8-104">드롭다운 메뉴에서 **엔드포인트 키 관리**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-104">Select **Manage endpoint keys** from the menu that drops down.</span></span> <span data-ttu-id="dbfc8-105">**표시**를 클릭하여 기본 엔드포인트 키를 표시하고 **복사**를 클릭하여 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-105">Click **Show** to show the primary endpoint key, and **Copy** to copy it to the clipboard.</span></span> <span data-ttu-id="dbfc8-106">그런 다음 쉽게 바로 검색할 수 있도록 텍스트 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-106">Then, paste it into a text file so you can easily retrieve it in a moment.</span></span>

    ![엔드포인트 키 복사](../media-draft/6-copy-primary-key.png)

1. <span data-ttu-id="dbfc8-108">페이지 맨 위 메뉴에서 **내 기술 자료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-108">Click **My knowledge bases** in the menu at the top of the page.</span></span> <span data-ttu-id="dbfc8-109">그런 다음, 이전에 만든 기술 자료에 대한 **코드 보기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-109">Then, click **View Code** for the knowledge base that you created earlier.</span></span>

    ![기술 자료 열기](../media-draft/6-open-knowledge-base.png)

1. <span data-ttu-id="dbfc8-111">첫 번째 줄의 기술 자료 ID와 두 번째 줄의 호스트 이름을 복사하여</span><span class="sxs-lookup"><span data-stu-id="dbfc8-111">Copy the knowledge base ID from the first line and the host name from the second line.</span></span> <span data-ttu-id="dbfc8-112">텍스트 파일에도 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-112">Paste them into a text file, as well.</span></span> <span data-ttu-id="dbfc8-113">그런 다음, 대화 상자를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-113">Then, close the dialog.</span></span> <span data-ttu-id="dbfc8-114">복사하는 호스트 이름에 “https://” 접두사를 포함하지 **마세요**.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-114">**Do not** include the "https://" prefix in the host name that you copy.</span></span>

    ![기술 자료 ID 및 호스트 이름 복사](../media-draft/6-copy-endpoint-info.png)  

1. <span data-ttu-id="dbfc8-116">Azure Portal의 웹앱 봇으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-116">Return to the web app bot in the Azure portal.</span></span> <span data-ttu-id="dbfc8-117">왼쪽의 메뉴에서 **응용 프로그램 설정**을 클릭하고 이름이 “QnAKnowledgebaseId”, “QnAAuthKey” 및 “QnAEndpointHostName”인 응용 프로그램 설정을 찾을 때까지 아래로 스크롤합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-117">Click **Application settings** in the menu on the left and scroll down until you find application settings named "QnAKnowledgebaseId," "QnAAuthKey," and "QnAEndpointHostName."</span></span> <span data-ttu-id="dbfc8-118">3단계에서 얻은 지식 기반 ID 및 호스트 이름과 1단계에서 얻은 엔드포인트 키를 이러한 필드에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-118">Paste the knowledge base ID and host name obtained in Step 3 and the endpoint key obtained in Step 1 into these fields.</span></span> <span data-ttu-id="dbfc8-119">그런 다음 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-119">Then, click **Save**.</span></span>

    ![응용 프로그램 설정 편집](../media-draft/6-enter-app-settings.png)

1. <span data-ttu-id="dbfc8-121">Visual Studio Code로 돌아가서 **app.js**의 콘텐츠를 아래 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-121">Return to Visual Studio Code and replace the contents of **app.js** with the code below.</span></span> <span data-ttu-id="dbfc8-122">그런 다음 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-122">Then, save the file.</span></span>

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

    <span data-ttu-id="dbfc8-123">30줄에 `QnAMakerDialog` 인스턴스를 만드는 호출을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-123">Note the call to create a `QnAMakerDialog` instance on line 30.</span></span> <span data-ttu-id="dbfc8-124">Azure Bot Service로 빌드된 봇과 기술 자료로 빌드된 Microsoft QnA Maker를 통합하는 대화 상자가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-124">This creates a dialog that integrates a bot built with the Azure Bot Service with a knowledge base built Microsoft QnA Maker.</span></span>
 
1. <span data-ttu-id="dbfc8-125">Visual Studio Code의 작업 막대에서 **소스 제어** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-125">Click the **Source Control** button in the activity bar in Visual Studio Code.</span></span> <span data-ttu-id="dbfc8-126">메시지 상자에 “기술 자료에 연결됨”을 입력하고 확인 표시를 클릭하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-126">Type "Connected to knowledge base" into the message box, and click the check mark to commit your changes.</span></span> <span data-ttu-id="dbfc8-127">그런 다음, 줄임표를 클릭하고 **분기 게시** 명령을 사용하여 이러한 변경 내용을 원격 리포지토리로(따라서, Azure 웹앱으로)</span><span class="sxs-lookup"><span data-stu-id="dbfc8-127">Then, click the ellipsis and use the **Publish Branch** command to push these changes to the remote repository (and therefore.</span></span> <span data-ttu-id="dbfc8-128">푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-128">to the Azure Web App).</span></span>

1. <span data-ttu-id="dbfc8-129">Azure Portal의 웹앱 봇으로 돌아가서 왼쪽의 **웹 채팅에서 테스트**를 클릭하여 테스트 콘솔을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-129">Return to the web app bot in the Azure portal and click **Test in Web Chat** on the left to open the test console.</span></span> <span data-ttu-id="dbfc8-130">“세계에서 가장 인기 있는 소프트웨어 프로그래밍 언어는 무엇인가요?”를</span><span class="sxs-lookup"><span data-stu-id="dbfc8-130">Type "What's the most popular software programming language in the world?"</span></span> <span data-ttu-id="dbfc8-131">채팅창 아래쪽에 있는 상자에 입력하고 **Enter** 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-131">into the box at the bottom of the chat window and press **Enter**.</span></span> <span data-ttu-id="dbfc8-132">봇이 다음과 같이 응답하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-132">Confirm that the bot responds as follows:</span></span>

    ![봇 테스트](../media-draft/6-portal-testing-chat.png)

<span data-ttu-id="dbfc8-134">이제 봇이 기술 자료에 연결되었으므로 마지막 단계로 실제 환경에서 봇을 자유롭게 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-134">Now that the bot is connected to the knowledge base, the final step is to test it in the wild.</span></span> <span data-ttu-id="dbfc8-135">Skype를 사용하면 그 어떤 환경보다도 자유롭게 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dbfc8-135">And what could be wilder than testing it with Skype?</span></span>