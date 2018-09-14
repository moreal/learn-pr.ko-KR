<span data-ttu-id="3ae36-101">결국 클라우드 내의 코드를 호스트 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-101">Eventually, we need to host our code somewhere in the cloud.</span></span> <span data-ttu-id="3ae36-102">Azure 기술을 사용 하 여이 작업을 수행 하려는 경우 Azure Functions</span><span class="sxs-lookup"><span data-stu-id="3ae36-102">The Azure technology we are going to use to do this is Azure Functions.</span></span>

<span data-ttu-id="3ae36-103">이 강의에 배웁니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-103">In this lecture you will learn:</span></span>

- <span data-ttu-id="3ae36-104">Azure 함수 앱을 만드는 방법 및 `JavaScript` Http 트리거.</span><span class="sxs-lookup"><span data-stu-id="3ae36-104">How to create an Azure Function App and `JavaScript` Http Trigger.</span></span>
- <span data-ttu-id="3ae36-105">실행 및 Azure 함수를 로컬로 디버그 하는 방법.</span><span class="sxs-lookup"><span data-stu-id="3ae36-105">How to run and debug an Azure Function locally.</span></span>

## <a name="create-an-azure-function-project"></a><span data-ttu-id="3ae36-106">Azure 함수 프로젝트 만들기</span><span class="sxs-lookup"><span data-stu-id="3ae36-106">Create an Azure Function Project</span></span>

<span data-ttu-id="3ae36-107">Azure 함수 프로젝트는 여러 함수에 대 한 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-107">An Azure Function Project is a container for multiple Functions.</span></span> <span data-ttu-id="3ae36-108">다양 한 방법으로;에서 트리거되는 함수 함수 HTTP 요청을 만들어 트리거 수 됩니다 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-108">Functions are triggered in different ways; we'll be triggering our functions by making a HTTP request.</span></span>

<span data-ttu-id="3ae36-109">여러 가지 방법으로 Azure 함수를 만들려면 이 모듈에서 이전에 설치한는 Azure Functions 확장을 사용 하 여 Visual Studio Code를 사용 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-109">There are many ways to create Azure Functions; we are going to use Visual Studio Code with the Azure Functions Extension which we installed earlier on in this module.</span></span>

<span data-ttu-id="3ae36-110">함수 프로젝트를 먼저 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-110">Let's first create our Function Project.</span></span>

1. <span data-ttu-id="3ae36-111">형식 <kbd>Ctrl</kbd>+<kbd>P</kbd> 여 명령 팔레트를 열고 다음에 대 한 검색 및 선택 `Azure Functions: Create New Project...`</span><span class="sxs-lookup"><span data-stu-id="3ae36-111">Type <kbd>Ctrl</kbd>+<kbd>P</kbd> to open up the command palette, then search for and select `Azure Functions: Create New Project...`</span></span>

   > <span data-ttu-id="3ae36-112">**참고**</span><span class="sxs-lookup"><span data-stu-id="3ae36-112">**NOTE**</span></span>
   >
   > <span data-ttu-id="3ae36-113">와 같은 일부 파일을 덮어쓸 것인지 궁금할 `.gitignore`, 답변 **없습니다** 모든!</span><span class="sxs-lookup"><span data-stu-id="3ae36-113">It might ask if you want to overwrite some files such as `.gitignore`, answer **no** to all!</span></span>

   ![새 프로젝트 만들기](/media-drafts/7.create-new-project.png)

2. <span data-ttu-id="3ae36-115">(첫 번째 옵션은 현재 폴더 라고 하는 데 사용) 하 여 함수 앱을 만드는 폴더 선택</span><span class="sxs-lookup"><span data-stu-id="3ae36-115">Select the folder where you want to create the function app (the first option is the current folder)</span></span>

   ![폴더 선택](/media-drafts/7.select-folder.png)

3. <span data-ttu-id="3ae36-117">선택 `JavaScript` 원하는 언어입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-117">Choose `JavaScript` as the desired language.</span></span>

   ![언어 선택](/media-drafts/7.select-language.png)

4. <span data-ttu-id="3ae36-119">위의 완료 하는 경우 표시 됩니다는 아래 폴더에 생성 된 파일</span><span class="sxs-lookup"><span data-stu-id="3ae36-119">If the above completed successfully you should see the below files created in the folder</span></span>

   ![만든 앱](/media-drafts/7.app-created.png)

## <a name="create-an-azure-function"></a><span data-ttu-id="3ae36-121">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="3ae36-121">Create an Azure Function</span></span>

<span data-ttu-id="3ae36-122">다음 보겠습니다 설정 함수를 만드는 Azure 자체에 HTTP 요청에 응답 하는 코드 조각입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-122">Next up let's create the Azure Function itself, the piece of code that responds to a HTTP request.</span></span>

<span data-ttu-id="3ae36-123">다시 Visual Studio 코드 확장을 사용 하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-123">Again we are going to use the Visual Studio Code Extention.</span></span>

1.  <span data-ttu-id="3ae36-124">형식 <kbd>Ctrl</kbd>+<kbd>P</kbd> 여 명령 팔레트를 열고 다음에 대 한 검색 및 선택 `Azure Functions: Create Function...`</span><span class="sxs-lookup"><span data-stu-id="3ae36-124">Type <kbd>Ctrl</kbd>+<kbd>P</kbd> to open up the command palette, then search for and select `Azure Functions: Create Function...`</span></span>

    ![새 함수 만들기](/media-drafts/7.create-function.png)

2.  <span data-ttu-id="3ae36-126">함수 프로젝트를 이전에 만든 위치 폴더를 선택 (첫 번째 옵션은 현재 폴더 라고 하는 데 사용)</span><span class="sxs-lookup"><span data-stu-id="3ae36-126">Select the folder where you created the function project previously (the first option is the current folder)</span></span>

    ![폴더 선택](/media-drafts/7.select-current-project.png)

3.  <span data-ttu-id="3ae36-128">에 만들기는 _HTTP 트리거_, 이므로 해당 옵션을 선택 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-128">We are creating a _HTTP Trigger_, so select that option.</span></span>

    ![폴더 선택](/media-drafts/7.select-trigger.png)

4.  <span data-ttu-id="3ae36-130">입력 `MojifyImage` 만들려는 함수의 이름으로</span><span class="sxs-lookup"><span data-stu-id="3ae36-130">Type in `MojifyImage` as the name of the Function you want to create</span></span>

    ![이름 선택](/media-drafts/7.choose-function-name.png)

5.  <span data-ttu-id="3ae36-132">선택 `Anonymous` 인증 수준으로</span><span class="sxs-lookup"><span data-stu-id="3ae36-132">Choose `Anonymous` as the authentication level</span></span>

    > <span data-ttu-id="3ae36-133">참고: 선택 하 여 `Anonymous` 함수 전 세계에 개방 되어 안전 하지 않은 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-133">NOTE: By choosing `Anonymous` the function is open to the world and insecure.</span></span>

    ![이름 선택](/media-drafts/7.choose-auth-level.png)

## <a name="run-the-function-locally"></a><span data-ttu-id="3ae36-135">로컬에서 함수 실행</span><span class="sxs-lookup"><span data-stu-id="3ae36-135">Run the function locally</span></span>

<span data-ttu-id="3ae36-136">사용 하 여 함수 프로젝트를 시작 프로젝트를 변환한 다음이 명령을 성공적으로 완료 되 면을 _HTTP 트리거_ 함수 호출 `MojifyImage`합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-136">Once these commands complete successfully you have converted the starter project to a function project with a _HTTP Trigger_ function called `MojifyImage`.</span></span>

<span data-ttu-id="3ae36-137">모든 항목이 작동 하도록 함수 앱을 실행할 수 로컬에서 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-137">To ensure everything is working you can run the function app locally, like so:</span></span>

```bash
func host start
```

<span data-ttu-id="3ae36-138">함수 런타임에서 로컬로;이 시작 유사한 결과가 표시 됩니다 모든는 최종적으로 올바르게 작동 하는 경우는 아래이 콘솔에 인쇄 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-138">This starts the function's runtime locally; if it all works correctly eventually you should see something like the below printed to the console:</span></span>

```output
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

> <span data-ttu-id="3ae36-139">**참고**</span><span class="sxs-lookup"><span data-stu-id="3ae36-139">**Note**</span></span>
>
> <span data-ttu-id="3ae36-140">Azure Functions 런타임 설치의 장점 중 하나 이며 프로덕션에서 함수를 실행 하는 동일한 기본 기술을 사용 하 여 로컬로 함수를 실행할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-140">This is one of the advantages of installing the Azure Functions runtime, it allows us to run the function locally using the same underlying technology that would be used to run the function in production.</span></span>

<span data-ttu-id="3ae36-141">함수가 제대로 실행 되도록이 브라우저 창에서 출력 콘솔에 인쇄 된 URL를 방문 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-141">To ensure the function is working correctly, visit the URL printed to the console, this prints in the browser window:</span></span>

![작동 하는 함수 앱](/media-drafts/7.default-function-app-working.png)

## <a name="debug-the-function-locally"></a><span data-ttu-id="3ae36-143">함수를 로컬로 디버그</span><span class="sxs-lookup"><span data-stu-id="3ae36-143">Debug the function locally</span></span>

> <span data-ttu-id="3ae36-144">**중요**</span><span class="sxs-lookup"><span data-stu-id="3ae36-144">**Important**</span></span>
>
> <span data-ttu-id="3ae36-145">종료 했는지를 `func host start` Visual Studio Code를 사용 하 여 디버그 하기 전에 방금 실행 한 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-145">Make sure you exit the `func host start` command you just ran before trying to debug it using Visual Studio Code.</span></span>

<span data-ttu-id="3ae36-146">또한 실행할 수 있습니다 _디버그 및_ visual studio 코드 내에서 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-146">Additionally, we can run _and debug_ the application inside visual studio code.</span></span>

<span data-ttu-id="3ae36-147">중단점을 추가 합니다 `index.js` JavaScript 함수의 맨 위에 있는 파일을 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-147">Add a breakpoint to the `index.js` file, at the top of the JavaScript function, like so:</span></span>

![중단점 추가](/media-drafts/7.add-breakpoint.png)

<span data-ttu-id="3ae36-149">디버그 메뉴에서 디버그 모드를 처음 방문할에서 함수를 실행 하려면 <kbd>Cmd<kbd> + <kbd>Shift<kbd> + <kbd>D<kbd>합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-149">To run the function in debug mode first visit the debug menu, <kbd>Cmd<kbd> + <kbd>Shift<kbd> + <kbd>D<kbd>.</span></span>

<span data-ttu-id="3ae36-150">선택 `Attach to JavaScript Functions` 마지막 디버그 세션을 시작 하려면 녹색 삼각형을 누르기 전에 디버그 구성에서 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-150">Then pick `Attach to JavaScript Functions` from the debug configuration before finally pressing the green triangle to start the debug session.</span></span>

> <span data-ttu-id="3ae36-151">**참고**</span><span class="sxs-lookup"><span data-stu-id="3ae36-151">**Note**</span></span>
>
> <span data-ttu-id="3ae36-152">`Attach to JavaScript Functions` 함수 프로젝트를 만들 때 디버그 구성이 자동으로 추가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-152">The `Attach to JavaScript Functions` debug configuration was added automatically when you created the Function Project.</span></span>

<span data-ttu-id="3ae36-153">또는 눌러 수 있습니다 <kbd>F5<kbd> 에서 아무 곳 이나 응용 프로그램에서이 마지막 디버그 구성을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-153">Alternatively, you can press <kbd>F5<kbd> from anywhere in the application; this runs the last debug configuration.</span></span>

<span data-ttu-id="3ae36-154">`func host start` 터미널 열어야 결국를 사용 하 여 동일한 위와 같이 출력; 명령을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-154">The `func host start` command is run for you; a terminal should open with eventually the same output as above:</span></span>

```output
Http Functions:

        MojifyImage: http://localhost:7071/api/MojifyImage
```

<span data-ttu-id="3ae36-155">디버그 메뉴 표시줄 나타납니다도 참조 디버깅 하는 것 이므로 다음과 같이 합니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-155">Since we are debugging you also see the debug menu bar appear, like so:</span></span>

![디버그 메뉴](/media-drafts/7.debug-menu-bar.png)

<span data-ttu-id="3ae36-157">이제 중단점에서 중단 위의 URL를 방문할 때 지정한 함수를 단계별로 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3ae36-157">Now when you visit the URL above it breaks at the breakpoint you specified, and you can step through the function.</span></span>

<!-- TODO Find Link -->

<span data-ttu-id="3ae36-158">할 수 있습니다 [자세한](https://code.visualstudio.com/docs/editor/debugging) Visual Studio Code에서 디버깅 하는 방법에 대 한</span><span class="sxs-lookup"><span data-stu-id="3ae36-158">You can [learn more](https://code.visualstudio.com/docs/editor/debugging) about debugging in Visual Studio Code</span></span>
