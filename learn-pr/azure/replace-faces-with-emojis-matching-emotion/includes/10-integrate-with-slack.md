<span data-ttu-id="7f7c9-101">필요한 모든 Azure 기능을 만들었습니다 및 로컬로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-101">We have created all the required Azure functions, and we can run them locally.</span></span>

<span data-ttu-id="7f7c9-102">이 강의에 Slack을 사용 하 여 Azure 함수를 연결 하 고 만들기를 Slack _슬래시_ Azure 함수를 호출 하 고 slack 창의 결과 mojified 이미지를 표시 하는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-102">In this lecture, we connect our Azure Functions with Slack and create a Slack _slash_ command which calls our Azure Function and displays the resulting mojified image in the slack window.</span></span>

<span data-ttu-id="7f7c9-103">이 강의의 끝에서 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-103">By the end of this lecture you will learn:</span></span>

- <span data-ttu-id="7f7c9-104">Slack 앱을 만들고 Azure Function 끝점과 슬래시 명령을 연결 하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-104">How to create a Slack app and connect a slash command with an Azure Function endpoint.</span></span>
- <span data-ttu-id="7f7c9-105">클라우드로 배포 하지 않고 슬래시 명령을 로컬로, 테스트 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-105">How to test your slash command locally, without deploying to the cloud.</span></span>

## <a name="using-ngrok-to-develop-with-slash-commands"></a><span data-ttu-id="7f7c9-106">Ngrok를 사용한 개발 슬래시 명령을 사용 하 여</span><span class="sxs-lookup"><span data-stu-id="7f7c9-106">Using ngrok to develop with slash commands</span></span>

<span data-ttu-id="7f7c9-107">이 Azure functions는 현재 프로그램만; 로컬로 실행 그러나 slack 클라우드, 인터넷에서에서 실행 됩니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-107">Our Azure functions are currently only running locally; however, slack runs in the cloud, on the internet.</span></span>

<span data-ttu-id="7f7c9-108">Slack 설정할 때 _슬래시_ 슬래시 명령을 다른 사용자가 실행 될 때마다 호출 되는 공용 URL을 요청 하려는 다음 섹션에서는 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-108">When we set up a slack _slash_ command in the next section, it's going to ask for a public URL which it calls whenever someone executes a slash command.</span></span>

<span data-ttu-id="7f7c9-109">제공 하려는 우리의 `RespondToSlackCommand` 있지만 URL이 로컬 컴퓨터에만 존재 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-109">We want to give them our `RespondToSlackCommand` URL, but that only exists on our local computer.</span></span>

<span data-ttu-id="7f7c9-110">수 부여 어떻게 서비스 클라우드 액세스의 리소스에 로컬 컴퓨터의 개발에 대 한?</span><span class="sxs-lookup"><span data-stu-id="7f7c9-110">How can you give services in the cloud access to resources on your local computer for development?</span></span>

<span data-ttu-id="7f7c9-111">이 문제에 적합 한 솔루션은 `ngrok` 인터넷에서 로컬 컴퓨터에 보안 터널을 만드는 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-111">A great solution to this conundrum is `ngrok` this is a tool which creates secure tunnels to your local machine from the internet.</span></span>

1. <span data-ttu-id="7f7c9-112">방문 https://ngrok.com/download</span><span class="sxs-lookup"><span data-stu-id="7f7c9-112">Visit https://ngrok.com/download</span></span>
2. <span data-ttu-id="7f7c9-113">다운로드 및 설치 지침에 따라는 `ngrok` 로컬 컴퓨터에 패키지 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-113">Follow the instructions to download and install the `ngrok` package to your local machine.</span></span>
3. <span data-ttu-id="7f7c9-114">실행 `ngrok http 7071` 터미널에서.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-114">Run `ngrok http 7071` in a terminal.</span></span>
   <span data-ttu-id="7f7c9-115">![ngrok](/media-drafts/9.ngrok.png)</span><span class="sxs-lookup"><span data-stu-id="7f7c9-115">![ngrok](/media-drafts/9.ngrok.png)</span></span>
4. <span data-ttu-id="7f7c9-116">이 끝나는 공용 URL을 출력 `ngrok.io` 예: `http://bbade778.ngrok.io`를 적어이 경우 다음 섹션에서 필요 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-116">This prints out a public URL ending in `ngrok.io` e.g. `http://bbade778.ngrok.io`, make a note of this you need it in the next section.</span></span>

> <span data-ttu-id="7f7c9-117">**참고**</span><span class="sxs-lookup"><span data-stu-id="7f7c9-117">**Note**</span></span>
>
> <span data-ttu-id="7f7c9-118">이렇게 `http://*.ngrock.io` 사용한 처럼 사용할 수 있는 URL `http://localhost:7071`, 이미지를 사용 하 여 사용해 같이 `http://[ngrok-url]/api/MojifyImage?imageUrl=[url-to-an-image]`</span><span class="sxs-lookup"><span data-stu-id="7f7c9-118">This `http://*.ngrock.io` URL you can use just as you used `http://localhost:7071`, try it out with an image like so `http://[ngrok-url]/api/MojifyImage?imageUrl=[url-to-an-image]`</span></span>

## <a name="create-a-slack-app"></a><span data-ttu-id="7f7c9-119">Slack 앱 만들기</span><span class="sxs-lookup"><span data-stu-id="7f7c9-119">Create a slack app</span></span>

<span data-ttu-id="7f7c9-120">슬래시 명령을 slack 앱에서 slack의 일부로 존재 _bot_합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-120">A slash command exists as part of a slack app, a slack _bot_.</span></span>

<span data-ttu-id="7f7c9-121">방문 [Slack 앱 만들기](https://api.slack.com/apps/new)</span><span class="sxs-lookup"><span data-stu-id="7f7c9-121">Visit [Create Slack App](https://api.slack.com/apps/new)</span></span>

<span data-ttu-id="7f7c9-122">선택는 `App Name` 와 연결 된 `Workspace` 누릅니다가 연습을 시작할 때 만든 `Create App`, 다음과 같이:</span><span class="sxs-lookup"><span data-stu-id="7f7c9-122">Choose an `App Name` and associate it with the `Workspace` you created at the start of this exercise and then press `Create App`, like so:</span></span>

![Slack 앱 만들기](/media-drafts/9.create-slack-app.png)

<span data-ttu-id="7f7c9-124">만든 후 다음 슬래시 명령을 만들고 slack 앱으로 이동 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-124">Once that's created we then need to go into our slack app and create a slash command.</span></span>

## <a name="create-a-slash-command"></a><span data-ttu-id="7f7c9-125">슬래시 명령 만들기</span><span class="sxs-lookup"><span data-stu-id="7f7c9-125">Create a slash command</span></span>

<span data-ttu-id="7f7c9-126">클릭 된 `Slash Commands` 메뉴 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-126">Click on the `Slash Commands` menu item.</span></span>

![슬래시 명령](/media-drafts/9.slash-commands.png)

<span data-ttu-id="7f7c9-128">`Create New Command`을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-128">Click `Create New Command`</span></span>

- <span data-ttu-id="7f7c9-129">슬래시 명령에 대해 원하는 어떤 이름이 입력 된 `command` 필드입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-129">Enter whatever name you want for your slash command in the `command` field.</span></span>
- <span data-ttu-id="7f7c9-130">ngrok 공용 URL을 입력 합니다 `Request URL` 필드</span><span class="sxs-lookup"><span data-stu-id="7f7c9-130">Enter the ngrok public URL into the `Request URL` field</span></span>

  > <span data-ttu-id="7f7c9-131">**중요 한**</span><span class="sxs-lookup"><span data-stu-id="7f7c9-131">**IMPORTANT**</span></span>
  >
  > <span data-ttu-id="7f7c9-132">추가 해야 `/api/RespondToSlackCommand` url</span><span class="sxs-lookup"><span data-stu-id="7f7c9-132">Remember to append `/api/RespondToSlackCommand` to the URL</span></span>

- <span data-ttu-id="7f7c9-133">짧은 설명 및 사용 현황 힌트를 추가 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-133">Add a short description and usage hint.</span></span>
- <span data-ttu-id="7f7c9-134">키를 누릅니다 `Save`</span><span class="sxs-lookup"><span data-stu-id="7f7c9-134">Press `Save`</span></span>

![슬래시 명령](/media-drafts/9.create-slash-command.png)

<span data-ttu-id="7f7c9-136">한 번 저장 화면 표시 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-136">Once saved you should see a screen like so:</span></span>

![슬래시 명령 성공](/media-drafts/9.create-slash-commands-success.png)

## <a name="install-the-slack-app-to-the-workspace"></a><span data-ttu-id="7f7c9-138">작업 영역에 slack 앱을 설치 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-138">Install the slack app to the workspace</span></span>

<span data-ttu-id="7f7c9-139">Slack 앱이 작업 영역에서 사용할 수 있습니다, 전에 설치 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-139">Before we can use our slack app in our workspace, we need to install it.</span></span>

1. <span data-ttu-id="7f7c9-140">선택 된 `Basic Information` 메뉴 항목</span><span class="sxs-lookup"><span data-stu-id="7f7c9-140">Select the `Basic Information` menu item</span></span>

2. <span data-ttu-id="7f7c9-141">확장 된 `Install your app to your workspace` 옵션과 키를 눌러를 `Install app to workspace` 단추입니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-141">Expand out the `Install your app to your workspace` option and press the `Install app to workspace` button.</span></span>

   ![작업 영역에 앱을 설치 합니다.](/media-drafts/9.install-app-to-workspace.png)

3. <span data-ttu-id="7f7c9-143">응용 프로그램을 인증 하도록 요청할 수 있습니다이 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-143">It may ask you to authenticate your application like so:</span></span>

   ![앱 작업 영역에 인증](/media-drafts/9.authenticate-slack-app.png)

## <a name="try-it-out"></a><span data-ttu-id="7f7c9-145">체험</span><span class="sxs-lookup"><span data-stu-id="7f7c9-145">Try it out</span></span>

<span data-ttu-id="7f7c9-146">슬래시 명령을 만들고 보겠습니다 ngrok 링크를 통해 Azure Functions는 로컬로 실행 중인 인스턴스에 연결 된 테스트 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-146">Now that your slash command has been created and connected to our locally running instance of Azure Functions via the ngrok link let's test it.</span></span>

1. <span data-ttu-id="7f7c9-147">Slack 앱과 연결한 slack 작업 영역으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-147">Go to the slack workspace you associated with your slack app.</span></span>
2. <span data-ttu-id="7f7c9-148">모든 형식과 채팅 창으로 이동 `/mojify` (또는 앱에 부여 했습니다 이름)</span><span class="sxs-lookup"><span data-stu-id="7f7c9-148">Go to any chat window and type `/mojify` (or whatever name you gave the app)</span></span>
3. <span data-ttu-id="7f7c9-149">모든 것이 제대로 작동 하는 경우 표시 됩니다 `mojify` 옵션으로</span><span class="sxs-lookup"><span data-stu-id="7f7c9-149">If everything has worked correctly, you should see `mojify` as an option</span></span>

   ![Mojify 확인](/media-drafts/9.slack-check-mojify.png)

4. <span data-ttu-id="7f7c9-151">이제 입력 `/mojify` enter, 이미지 URL을 추가 하 고 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="7f7c9-151">Now type `/mojify` and add an image URL then press enter, like so:</span></span>

   ![형식 Mojify](/media-drafts/9.slack-type-mojify.png)
