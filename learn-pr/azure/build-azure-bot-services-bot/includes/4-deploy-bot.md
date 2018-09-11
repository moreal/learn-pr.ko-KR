<span data-ttu-id="ac97b-101">[연습 1](#Exercise1)에서 Azure 웹앱 봇을 만들 때 해당 봇을 호스트할 Azure 웹앱이 배포되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-101">When you created an Azure web app bot in [Exercise 1](#Exercise1), an Azure web app was deployed to host it.</span></span> <span data-ttu-id="ac97b-102">그러나 아직 봇에는 일부 코드가 필요하며 해당 코드가 Azure 웹앱에 배포되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-102">But the bot does require some code, and it still needs to be deployed to the Azure web app.</span></span> <span data-ttu-id="ac97b-103">다행히 코드는 Azure Bot Service에 의해 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-103">Fortunately, the code was generated for you by the Azure Bot Service.</span></span> <span data-ttu-id="ac97b-104">이 연습에서는 Visual Studio Code를 사용하여 해당 코드를 로컬 Git 리포지토리에 배치하고, 변경 내용을 로컬 리포지토리에서 봇을 호스팅하는 Azure 웹앱에 연결된 원격 리포지토리로 푸시하여 Azure에 봇을 게시합니다. 이러한 프로세스를 [연속 통합](https://en.wikipedia.org/wiki/Continuous_integration)이라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-104">In this unit, you will use Visual Studio Code to place the code in a local Git repository and publish the bot to Azure by pushing changes from the local repository to a remote repository connected to the Azure web app that hosts the bot — a process known as [continuous integration](https://en.wikipedia.org/wiki/Continuous_integration).</span></span>

1. <span data-ttu-id="ac97b-105">[Git](https://git-scm.com/)이 PC에 설치되어 있지 않으면 https://git-scm.com/downloads로 이동하여 운영 체제에 맞는 Git 클라이언트를 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="ac97b-105">If [Git](https://git-scm.com/) isn't installed on your PC, go to https://git-scm.com/downloads and install the Git client for your operating system.</span></span> <span data-ttu-id="ac97b-106">Git은 무료 오픈 소스 분산 버전 제어 시스템으로, Visual Studio Code와 원활하게 통합됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-106">Git is a free and open-source distributed version control system, and it integrates seamlessly into Visual Studio Code.</span></span> <span data-ttu-id="ac97b-107">Git이 설치되어 있는지 잘 모르는 경우 명령 프롬프트 또는 터미널 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-107">If you aren't sure whether Git is installed, open a Command Prompt or terminal window and execute the following command:</span></span>

    ``` 
    git --version
    ```

    <span data-ttu-id="ac97b-108">버전 번호가 표시되면 Git 클라이언트가 설치되어 있는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-108">If a version number is displayed, then the Git client is installed.</span></span>

1. <span data-ttu-id="ac97b-109">Node.js가 PC에 설치되어 있지 않으면 https://nodejs.org/로 이동하여 최신 LTS 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-109">If Node.js isn't installed on your PC, go to https://nodejs.org/ and install the latest LTS version.</span></span> <span data-ttu-id="ac97b-110">명령 프롬프트 또는 터미널 창을 열고 다음 명령을 입력하면 Node.js가 설치되어 있는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-110">You can determine whether Node.js is installed by opening a Command Prompt or terminal window and typing the following command:</span></span>

    ```
    node --version
    ```

    <span data-ttu-id="ac97b-111">Node가 설치되어 있으면 버전 번호가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-111">If Node is installed, the version number will be displayed.</span></span>

1. <span data-ttu-id="ac97b-112">Visual Studio Code가 PC에 설치되어 있지 않으면 지금 https://code.visualstudio.com/으로 이동하여 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="ac97b-112">If Visual Studio Code isn't installed on your PC, go to https://code.visualstudio.com/ and install it now.</span></span>

1. <span data-ttu-id="ac97b-113">봇의 소스 코드를 보관하도록 하드 디스크의 선택한 위치에 “Factbot”이라는 폴더를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-113">Create a folder named "Factbot" in the location of your choice on your hard disk to hold the bot's source code.</span></span>

1. <span data-ttu-id="ac97b-114">Azure Portal로 돌아가서 “factbot-rg” 리소스 그룹을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-114">Return to the Azure portal and open the "factbot-rg" resource group.</span></span> <span data-ttu-id="ac97b-115">그런 다음, [연습 1](#Exercise1)에서 만든 웹앱 봇을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-115">Then, click the web app bot you created in [Exercise 1](#Exercise1).</span></span>

    ![웹앱 봇 열기](../media-draft/4-open-web-app-bot.png)

1. <span data-ttu-id="ac97b-117">왼쪽 메뉴에서 **빌드**를 클릭한 후 **zip 파일 다운로드**를 클릭하여 봇의 소스 코드가 포함된 zip 파일을 준비합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-117">Click **Build** in the menu on the left, and then click **Download zip file** to prepare a zip file containing the bot's source code.</span></span> <span data-ttu-id="ac97b-118">zip 파일이 준비되면 **zip 파일 다운로드** 단추를 클릭하여 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-118">Once the zip file is prepared, click the **Download zip file** button to download it.</span></span> <span data-ttu-id="ac97b-119">다운로드가 완료되면 zip 파일의 콘텐츠를 4단계에서 만든 “Factbot” 폴더로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-119">When the download is complete, copy the contents of the zip file to the "Factbot" folder that you created in Step 4.</span></span>

    ![소스 코드 다운로드](../media-draft/4-download-source.png)

1. <span data-ttu-id="ac97b-121">계속 “빌드” 블레이드에서 **연속 배포 구성**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-121">Still on the "Build" blade, click **Configure continuous deployment**.</span></span> <span data-ttu-id="ac97b-122">뒤이은 블레이드의 맨 위에서 **설정**을 클릭한 후 **원본 선택**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-122">Click **Setup** at the top of the ensuing blade, followed by **Choose Source**.</span></span> <span data-ttu-id="ac97b-123">그런 다음, **로컬 Git 리포지토리**를 배포 원본으로 선택하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-123">Then, select **Local Git Repository** as the deployment source and click **OK**.</span></span> 

    ![로컬 Git 리포지토리를 배포 원본으로 지정](../media-draft/4-portal-set-local-git.png)

1. <span data-ttu-id="ac97b-125">“배포” 블레이드를 닫고 왼쪽 메뉴에서 **모든 App Service 설정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-125">Close the "Deployments" blade and click **All App service settings** in the menu on the left.</span></span>

1. <span data-ttu-id="ac97b-126">**배포 자격 증명**을 클릭한 후 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-126">Click **Deployment credentials**, and then enter a user name and password.</span></span> <span data-ttu-id="ac97b-127">사용자 이름은 Azure 내에서 고유해야 하므로 “FactbotAdministrator” 이외의 이름을 입력해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-127">You will probably have to enter a user name other than "FactbotAdministrator" because the name must be unique within Azure.</span></span> <span data-ttu-id="ac97b-128">그런 다음, **저장**을 클릭하고 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-128">Then, click **Save** and close the blade.</span></span>

    ![배포 자격 증명 입력](../media-draft/4-portal-enter-ci-creds.png)

1. <span data-ttu-id="ac97b-130">Visual Studio Code를 시작하고 **파일** > **폴더 열기...** 명령을 사용하여 6단계에서 봇의 소스 코드를 복사한 “Factbot” 폴더를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-130">Start Visual Studio Code and use the **File** > **Open Folder...** command to open the "Factbot" folder that you copied the bot's source code to in Step 6.</span></span>

1. <span data-ttu-id="ac97b-131">Visual Studio Code 왼쪽의 작업 막대에서 **원본 제어** 단추를 클릭하고 맨 위에서 **리포지토리 초기화** 아이콘을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-131">Click the **Source Control** button in the activity bar on the left side of Visual Studio Code, and click the **Initialize Repository** icon at the top.</span></span> <span data-ttu-id="ac97b-132">뒤이은 대화 상자에서 **리포지토리 초기화** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-132">Then, click the **Initialize Repository** button in the ensuing dialog.</span></span>

    ![로컬 Git 리포지토리 초기화](../media-draft/4-vs-init-git-repo.png)

1. <span data-ttu-id="ac97b-134">“첫 번째 커밋”을</span><span class="sxs-lookup"><span data-stu-id="ac97b-134">Type "First commit."</span></span> <span data-ttu-id="ac97b-135">메시지 상자에 입력한 후 확인 표시를 클릭하여 변경 내용을 커밋합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-135">into the message box, and then click the check mark to commit your changes.</span></span>

    ![로컬 리포지토리에 변경 내용 커밋](../media-draft/4-vs-first-git-commit.png)

1. <span data-ttu-id="ac97b-137">Visual Studio Code의 **보기** 메뉴에서 **통합 터미널**을 선택하여 통합 터미널을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-137">Select **Integrated Terminal** from Visual Studio Code's **View** menu to open an integrated terminal.</span></span> <span data-ttu-id="ac97b-138">그런 다음, 통합 터미널에서 다음 명령을 실행하여 두 위치의 BOT_NAME을 연습 1, 3단계에서 입력한 봇 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-138">Then, execute the following command in the integrated terminal, replacing BOT_NAME in two places with the bot name you entered in Exercise 1, Step 3.</span></span>

    ```
    git remote add qna-factbot https://BOT_NAME.scm.azurewebsites.net:443/BOT_NAME.git
    ```

1. <span data-ttu-id="ac97b-139">원본 제어 패널 맨 위의 줄임표(세 개의 점)를 클릭하고 메뉴에서 **분기 게시**를 선택하여 로컬 리포지토리에서 Azure로 봇 코드를 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-139">Click the ellipsis (the three dots) at the top of the SOURCE CONTROL panel and select **Publish Branch** from the menu to push the bot code from the local repository to Azure.</span></span> <span data-ttu-id="ac97b-140">자격 증명을 입력하라는 메시지가 표시되면 이 연습의 9단계에서 지정한 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-140">If prompted for credentials, enter the user name and password you specified in Step 9 of this exercise.</span></span>

<span data-ttu-id="ac97b-141">봇이 Azure에 게시되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-141">Your bot has been published to Azure.</span></span> <span data-ttu-id="ac97b-142">그러나 봇을 테스트하기 전에 로컬에서 봇을 실행하고 Visual Studio Code에서 디버그하는 방법을 배워보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ac97b-142">But before you test it there, let's run it locally and learn how to debug it in Visual Studio Code.</span></span>