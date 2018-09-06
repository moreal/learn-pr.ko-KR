### <a name="exercise-5-create-a-nodejs-app-that-uses-the-model"></a><span data-ttu-id="1855a-101">연습 5: 모델을 사용하는 Node.js 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="1855a-101">Exercise 5: Create a Node.js app that uses the model</span></span>

<span data-ttu-id="1855a-102">Microsoft Custom Vision Service의 진정한 강점은 개발자가 [Custom Vision 예측 API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814)를 사용하여 자신의 응용 프로그램에 편리하게 인텔리전스를 통합할 수 있다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-102">The true power of the Microsoft Custom Vision Service is the ease with which developers can incorporate its intelligence into their own applications using the [Custom Vision Prediction API](https://southcentralus.dev.cognitive.microsoft.com/docs/services/eb68250e4e954d9bae0c2650db79c653/operations/58acd3c1ef062f0344a42814).</span></span> <span data-ttu-id="1855a-103">이 연습에서는 Visual Studio Code를 사용하여 이전 연습에서 빌드하여 학습한 모델을 사용하도록 Artwork라는 앱을 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-103">In this exercise, you will use Visual Studio Code to modify an app named Artwork to use the model you built and trained in previous exercises.</span></span>

1. <span data-ttu-id="1855a-104">Node.js가 시스템에 설치되어 있지 않으면 https://nodejs.org로 이동하여 사용 중인 운영 체제에 대한 최신 LTS 버전을 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-104">If Node.js isn't installed on your system, go to https://nodejs.org and install the latest LTS version for your operating system.</span></span>

    > <span data-ttu-id="1855a-105">Node.js가 설치되어 있는지 잘 모르는 경우 명령 프롬프트 또는 터미널 창을 열고 **node -v**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-105">If you aren't sure whether Node.js is installed, open a Command Prompt or terminal window and type **node -v**.</span></span> <span data-ttu-id="1855a-106">Node.js 버전 번호가 표시되지 않으면 Node.js가 설치되지 않은 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-106">If you don't see a Node.js version number, then Node.js isn't installed.</span></span> <span data-ttu-id="1855a-107">6.0보다 오래된 Node.js 버전이 설치되어 있는 경우 최신 버전을 다운로드하여 설치하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-107">If a version of Node.js older than 6.0 is installed, it is highly recommend that you download and install the latest version.</span></span>

1. <span data-ttu-id="1855a-108">Visual Studio Code가 워크스테이션에 설치되어 있지 않으면 지금 http://code.visualstudio.com으로 이동하여 설치하세요.</span><span class="sxs-lookup"><span data-stu-id="1855a-108">If Visual Studio Code isn't installed on your workstation, go to http://code.visualstudio.com and install it now.</span></span>

1. <span data-ttu-id="1855a-109">Visual Studio Code를 시작하고 **파일** 메뉴에서 **폴더 열기...** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-109">Start Visual Studio Code and select **Open Folder...** from the **File** menu.</span></span> <span data-ttu-id="1855a-110">다음 대화 상자에서 랩 리소스에 포함된 “Client\Artworks” 폴더를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-110">In the ensuing dialog, select the "Client\Artworks" folder included in the lab resources.</span></span>

    ![Artworks 폴더 선택](../images/fe-select-folder.png)

    <span data-ttu-id="1855a-112">_Artworks 폴더 선택_</span><span class="sxs-lookup"><span data-stu-id="1855a-112">_Selecting the Artworks folder_</span></span> 

1. <span data-ttu-id="1855a-113">**보기** > **통합 터미널** 명령을 사용하여 Visual Studio Code에서 통합 터미널 창을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-113">Use the **View** > **Integrated Terminal** command to open an integrated terminal window in Visual Studio Code.</span></span> <span data-ttu-id="1855a-114">그런 다음, 통합 터미널에서 다음 명령을 실행하여 앱에 필요한 패키지를 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-114">Then execute the following command in the integrated terminal to load the packages required by the app:</span></span>

    ```
    npm install
    ```

1. <span data-ttu-id="1855a-115">Custom Vision Service 포털의 Artwork 프로젝트로 돌아가서 **성능**을 클릭한 후 **기본값으로**를 클릭하여 모델의 최근 반복을 기본 반복으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-115">Return to the Artwork project in the Custom Vision Service portal, click **Performance**, and then click **Make default** to make sure the latest iteration of the model is the default iteration.</span></span> 

    ![기본 반복 지정](../images/portal-make-default.png)

    <span data-ttu-id="1855a-117">_기본 반복 지정_</span><span class="sxs-lookup"><span data-stu-id="1855a-117">_Specifying the default iteration_</span></span> 

1. <span data-ttu-id="1855a-118">앱을 실행하고 이를 사용하여 Custom Vision Service를 호출하기 전에, 엔드포인트 및 권한 부여 정보를 포함하도록 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-118">Before you can run the app and use it to call the Custom Vision Service, it must be modified to include endpoint and authorization information.</span></span> <span data-ttu-id="1855a-119">이를 위해 **예측 URL**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-119">To that end, click **Prediction URL**.</span></span>

    ![예측 URL 정보 보기](../images/portal-prediction-url.png)

    <span data-ttu-id="1855a-121">_예측 URL 정보 보기_</span><span class="sxs-lookup"><span data-stu-id="1855a-121">_Viewing Prediction URL information_</span></span> 

1. <span data-ttu-id="1855a-122">다음에 표시되는 대화 상자에는 URL을 통해 이미지를 업로드하기 위한 URL과 로컬 이미지를 업로드하기 위한 URL이 각각 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-122">The ensuing dialog lists two URLs: one for uploading images via URL, and another for uploading local images.</span></span> <span data-ttu-id="1855a-123">이미지 파일의 예측 API URL을 클립보드로 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-123">Copy the Prediction API URL for image files to the clipboard.</span></span> 

    ![예측 API URL 복사](../images/copy-prediction-url.png)

    <span data-ttu-id="1855a-125">_예측 API URL 복사_</span><span class="sxs-lookup"><span data-stu-id="1855a-125">_Copying the Prediction API URL_</span></span> 

1. <span data-ttu-id="1855a-126">Visual Studio Code로 돌아가서 **predict.js**를 클릭하여 코드 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-126">Return to Visual Studio Code and click **predict.js** to open it in the code editor.</span></span>

    ![predict.js 열기](../images/vs-predict-file.png)

    <span data-ttu-id="1855a-128">_predict.js 열기_</span><span class="sxs-lookup"><span data-stu-id="1855a-128">_Opening predict.js_</span></span> 

1. <span data-ttu-id="1855a-129">줄 3의 “PREDICTION_ENDPOINT”를 클립보드의 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-129">Replace "PREDICTION_ENDPOINT" in line 3 with the URL on the clipboard.</span></span>

    ![예측 API URL 추가](../images/vs-prediction-endpoint.png)

    <span data-ttu-id="1855a-131">_예측 API URL 추가_</span><span class="sxs-lookup"><span data-stu-id="1855a-131">_Adding the Prediction API URL_</span></span> 

1. <span data-ttu-id="1855a-132">Custom Vision Service 포털로 돌아가서 예측 API 키를 클립보드에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-132">Return to the Custom Vision Service portal and copy the Prediction API key to the clipboard.</span></span> 

    ![예측 API 키 복사](../images/copy-prediction-key.png)

    <span data-ttu-id="1855a-134">_예측 API 키 복사_</span><span class="sxs-lookup"><span data-stu-id="1855a-134">_Copying the Prediction API key_</span></span> 

1. <span data-ttu-id="1855a-135">Visual Studio Code로 돌아가서 **predict.js**의 줄 4에 있는 “PREDICTION_KEY”를 클립보드의 API 키로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-135">Return to Visual Studio Code and replace "PREDICTION_KEY" in line 4 of **predict.js** with the API key on the clipboard.</span></span>

    ![예측 API 키 추가](../images/vs-prediction-key.png)

    <span data-ttu-id="1855a-137">_예측 API 키 추가_</span><span class="sxs-lookup"><span data-stu-id="1855a-137">_Adding the Prediction API key_</span></span> 

1. <span data-ttu-id="1855a-138">**predict.js**에서 아래로 스크롤하고 줄 34부터 시작되는 코드 블록을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-138">Scroll down in **predict.js** and examine the block of code that begins on line 34.</span></span> <span data-ttu-id="1855a-139">이 부분은 AJAX를 사용하여 Custom Vision Service 호출을 수행하는 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-139">This is the code that calls out to the Custom Vision Service using AJAX.</span></span> <span data-ttu-id="1855a-140">Custom Vision Service API를 사용하는 것은 REST 엔드포인트에 대해 인증된 단순 POST를 수행하는 것만큼 쉽습니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-140">Using the Custom Vision Prediction API is as easy as making a simple, authenticated POST to a REST endpoint.</span></span>

    ![예측 API 호출](../images/vs-code-block.png)

    <span data-ttu-id="1855a-142">_예측 API 호출_</span><span class="sxs-lookup"><span data-stu-id="1855a-142">_Making a call to the Prediction API_</span></span> 

1. <span data-ttu-id="1855a-143">Visual Studio Code의 통합 터미널로 돌아가서 다음 명령을 실행하여 앱을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-143">Return to the integrated terminal in Visual Studio Code and execute the following command to start the app:</span></span>

    ```
    npm start
    ```

1. <span data-ttu-id="1855a-144">Artworks 앱이 시작되고 다음과 같은 창을 표시하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-144">Confirm that the Artworks app starts and displays a window like this one:</span></span>

    ![Artworks 앱](../images/app-startup.png)

    <span data-ttu-id="1855a-146">_Artworks 앱_</span><span class="sxs-lookup"><span data-stu-id="1855a-146">_The Artworks app_</span></span> 

<span data-ttu-id="1855a-147">Artworks는 Node.js 및 [Electron](https://electron.atom.io/)으로 작성한 플랫폼 간 앱입니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-147">Artworks is a cross-platform app written with Node.js and [Electron](https://electron.atom.io/).</span></span> <span data-ttu-id="1855a-148">따라서 Windows, macOS 및 Linux에서 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-148">As such, it is equally capable of running on Windows, macOS, and Linux.</span></span> <span data-ttu-id="1855a-149">다음 연습에서 이 앱을 사용하여 이미지를 해당 이미지를 그린 화가별로 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="1855a-149">In the next exercise, you will use it to classify images by the artists who painted them.</span></span>