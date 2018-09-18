<span data-ttu-id="b7a86-101">텍스트 분석 API 서비스를 호출하여 감정 점수를 가져오도록 함수 구현을 업데이트하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-101">Let's update our function implementation to call the Text Analytics API service and get back a sentiment score.</span></span>

1. <span data-ttu-id="b7a86-102">함수 앱 포털에서 [!INCLUDE [func-name-discover](./func-name-discover.md)] 함수를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-102">Select our function, [!INCLUDE [func-name-discover](./func-name-discover.md)], in the Function Apps portal.</span></span>

1. <span data-ttu-id="b7a86-103">화면 오른쪽에서 **파일 보기** 메뉴를 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-103">Expand the **View files** menu on the right of the screen.</span></span>

1. <span data-ttu-id="b7a86-104">**파일 보기** 탭 아래에서 **index.js**를 선택하여 편집기에서 코드 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-104">Under the **View files** tab, select **index.js** to open the code file in the editor.</span></span>

1. <span data-ttu-id="b7a86-105">코드 파일의 모든 콘텐츠를 다음 JavaScript로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-105">Replace the entire content of the code file with the following JavaScript.</span></span>

[!code-javascript[](../code/discover-sentiment-sort.js?highlight=7)]

<span data-ttu-id="b7a86-106">이 코드에서 어떤 일이 벌어지는지 살펴봅시다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-106">Let's look at what's happening in this code:</span></span>

- <span data-ttu-id="b7a86-107">텍스트 분석 서비스를 호출하려면 코드 조각에서 강조 표시된 `accessKey`를 이전에 저장한 키로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-107">To call the text analytics service, set `accessKey`, highlighted in the code snippet, to the key you saved earlier.</span></span>
- <span data-ttu-id="b7a86-108">해당 지역이 이 예제의 *westus*와 다른 경우 액세스 키를 얻은 지역으로 `uri`을 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-108">Update `uri` to the region from which you obtained your access key, if that region is different than *westus* shown in this example.</span></span>
- <span data-ttu-id="b7a86-109">코드 파일의 맨 아래에서 `documents` 배열을 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-109">At the bottom of the code file, we've defined a `documents` array.</span></span> <span data-ttu-id="b7a86-110">이 배열은 텍스트 분석 서비스로 보내는 페이로드입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-110">This array is the payload we send to the Text Analytics service.</span></span> 
- <span data-ttu-id="b7a86-111">이 예의 `documents` 배열에는 항목이 하나 있는데, 우리 함수를 트리거한 큐 메시지입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-111">The `documents` array has a single entry in this case, which is the queue message that triggered our function.</span></span> <span data-ttu-id="b7a86-112">배열에 문서가 하나밖에 없지만, 솔루션이 메시지를 한 번에 하나씩만 처리할 수 있다는 의미는 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-112">Although we only have one document in our array, it doesn't mean that our solution can only handle one message at a time.</span></span> <span data-ttu-id="b7a86-113">Azure Functions 런타임은 메시지를 일괄적으로 검색 및 처리하고, 함수의 여러 인스턴스를 *병렬로* 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-113">The Azure Functions runtime retrieves and processes messages in batches, calling several instances of our function *in parallel*.</span></span> <span data-ttu-id="b7a86-114">현재 기본 일괄 처리 크기는 16이고 최대 일괄 처리 크기는 32입니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-114">Currently, the default batch size is 16 and the maximum batch size is 32.</span></span>
- <span data-ttu-id="b7a86-115">`id`는 배열 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-115">The `id` must be unique within the array.</span></span> <span data-ttu-id="b7a86-116">`language` 속성은 문서 텍스트의 언어를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-116">The `language` property specifies the language of the document text.</span></span>  
- <span data-ttu-id="b7a86-117">그 후에는 HTTPS 모듈을 사용하여 텍스트 분석 API에 대한 호출을 만드는 `get_sentiments` 메서드를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-117">We then call our method `get_sentiments`, which uses the HTTPS module to make the call to Text Analytics API.</span></span> <span data-ttu-id="b7a86-118">모든 요청의 헤더에 구독 또는 액세스 키를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-118">Notice that we pass our subscription, or access, key in the header of every request.</span></span>
- <span data-ttu-id="b7a86-119">서비스가 반환되면 `response_handler`가 호출되고, `context.log`를 사용하여 콘솔에 대한 응답을 기록합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-119">When the service returns, our `response_handler` is called and we log the response to the console using `context.log`</span></span> 

## <a name="try-it-out"></a><span data-ttu-id="b7a86-120">사용해보기</span><span class="sxs-lookup"><span data-stu-id="b7a86-120">Try it out</span></span>

<span data-ttu-id="b7a86-121">큐 분류를 살펴보기 전에, 무엇을 테스트 실행할 것인지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-121">Before we look at sorting into queues, let's take what we have for a test run.</span></span> 

1.  <span data-ttu-id="b7a86-122">함수 앱 포털에서 [!INCLUDE [func-name-discover](./func-name-discover.md)] 함수를 선택하고, 맨 왼쪽에서 [테스트] 메뉴 항목을 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-122">With our function, [!INCLUDE [func-name-discover](./func-name-discover.md)], selected in the Function Apps portal, click on the Test menu item on the far left to expand it.</span></span>

2. <span data-ttu-id="b7a86-123">**테스트** 메뉴 항목을 선택하고 테스트 패널을 열었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-123">Select the **Test** menu item and verify that you have the test panel open.</span></span> <span data-ttu-id="b7a86-124">테스트 패널은 다음 스크린샷과 비슷하게 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-124">The following screenshot shows what it should look like.</span></span> 

![확장된 함수 테스트 패널을 보여주는 스크린샷.](../media-draft/test-panel-open-small.png)

3. <span data-ttu-id="b7a86-126">스크린샷처럼 요청 본문에 텍스트 문자열을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-126">Add a string of text into the request body as shown in the screenshot.</span></span> 

1.  <span data-ttu-id="b7a86-127">테스트 패널 아래쪽에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-127">Click **Run** at the bottom of the test panel.</span></span>

1. <span data-ttu-id="b7a86-128">코드 편집기에서 주 화면의 왼쪽 아래에 **로그** 탭이 확장되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-128">Make sure the **Logs** tab is expanded at the bottom left of the main screen, under the code editor.</span></span> 

1. <span data-ttu-id="b7a86-129">**로그** 탭에 함수가 완료되었다는 로그 정보가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-129">Verify that the **Logs** tab displays log information that the function completed.</span></span> <span data-ttu-id="b7a86-130">이 창에는 텍스트 분석 API 호출의 응답도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-130">The window will also display the response from the Text Analytics API call.</span></span> 

![테스트 패널 및 성공한 테스트 결과를 보여주는 스크린샷.](../media-draft/sentiment-response-log1.png)

<span data-ttu-id="b7a86-132">축하합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-132">Congratulations!</span></span> <span data-ttu-id="b7a86-133">[!INCLUDE [func-name-discover](./func-name-discover.md)] 함수가 설계된 대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-133">The [!INCLUDE [func-name-discover](./func-name-discover.md)] works as designed.</span></span> <span data-ttu-id="b7a86-134">이 예제에서는 매우 긍정적인 메시지를 전달하고 0.98이 넘는 점수를 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-134">In  this example, we passed in a very upbeat message and received a score of over 0.98.</span></span> <span data-ttu-id="b7a86-135">덜 긍정적인 메시지로 변경하고, 테스트를 다시 실행한 후 응답을 살펴보세요.</span><span class="sxs-lookup"><span data-stu-id="b7a86-135">Try changing the message to something less optimistic, rerun the test and note the response.</span></span>

## <a name="try-it-out-again-optional"></a><span data-ttu-id="b7a86-136">다시 테스트(선택 사항)</span><span class="sxs-lookup"><span data-stu-id="b7a86-136">Try it out again (optional)</span></span>

<span data-ttu-id="b7a86-137">테스트를 반복하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-137">Let's repeat the test.</span></span> <span data-ttu-id="b7a86-138">이번에는 포털의 테스트 창을 사용하는 대신, 메시지를 입력 큐에 직접 배치하고 어떤 일이 벌어지는지 관찰하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-138">This time, instead of using the Test window of the portal, we'll actually place a message into the input queue and watch what happens.</span></span> 

1. <span data-ttu-id="b7a86-139">포털의 **리소스 그룹** 섹션에서 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-139">Navigate to your resource group in the **Resource Groups** section of the portal.</span></span>

1. <span data-ttu-id="b7a86-140">이 강좌에 사용된 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-140">Select the resource group used in this lesson.</span></span>

1. <span data-ttu-id="b7a86-141">나타나는 **리소스 그룹** 패널에서 저장소 계정 항목을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-141">In the **Resource group** panel that appears, locate the Storage Account entry and select it.</span></span>

![리소스 그룹 창에서 선택한 저장소 계정의 스크린샷.](../media-draft/select-storage-account.png)

1. <span data-ttu-id="b7a86-143">저장소 계정 기본 창의 왼쪽 메뉴에서 **Storage 탐색기(미리 보기)** 를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-143">Select **Storage Explorer (preview)** from the left menu of the Storage Account main window.</span></span>  <span data-ttu-id="b7a86-144">이 작업은 포털 내부에서 Azure Storage 탐색기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-144">This action opens the Azure Storage Explorer inside the portal.</span></span> <span data-ttu-id="b7a86-145">이 단계에서는 화면이 다음 스크린샷과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-145">Your screen should look like the following screenshot at this stage.</span></span> 

![현재 큐가 하나도 없는 저장소 계정을 보여주는 저장소 탐색기의 스크린샷.](../media-draft/sa-no-queue.png)

<span data-ttu-id="b7a86-147">보시다시피, 이 저장소 계정에는 아직 큐가 하나도 없으므로 이 문제를 수정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-147">As you can see, we don't have any queues in this storage account yet, so let's fix that.</span></span>

1. <span data-ttu-id="b7a86-148">기억하실지 모르겠지만, 이 강좌의 앞부분에서 **new-feedback-q** 트리거와 연결된 큐 이름을 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-148">If you remember from earlier in this lesson, we named the queue associated with our trigger **new-feedback-q**.</span></span> <span data-ttu-id="b7a86-149">저장소 탐색기에서 **큐** 항목을 마우스 오른쪽 단추로 클릭하고 *큐 만들기*를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-149">Right-click on the **Queues** item in the storage explorer and select *Create Queue*.</span></span>

1. <span data-ttu-id="b7a86-150">열리는 대화 상자에서 **new-feedback-q**를 입력하고 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-150">In the dialog that opens, enter **new-feedback-q** and click **OK**.</span></span> <span data-ttu-id="b7a86-151">입력 큐가 하나 생겼습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-151">We now have our input queue.</span></span> 

1. <span data-ttu-id="b7a86-152">왼쪽 메뉴에서 새 큐를 선택하여 이 큐의 데이터 탐색기를 살펴봅니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-152">Select the new queue in the left-hand menu to see the data explorer for this queue.</span></span> <span data-ttu-id="b7a86-153">예상대로 큐가 비어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-153">As expected, the queue is empty.</span></span> <span data-ttu-id="b7a86-154">창 맨 위에 있는 **메시지 추가** 명령을 사용하여 큐에 메시지를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-154">Let's add a message to the queue using the **Add Message** command at the top of the window.</span></span>

1. <span data-ttu-id="b7a86-155">**메시지 추가** 대화 상자에서, "이 메시지는 입력 큐 new-feedback-q에서 온 것"이라고 **메시지 텍스트** 필드에 입력하고 대화 상자의 맨 아래에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-155">In the **Add Message** dialog, enter "This message came from our input queue, new-feedback-q" into the **Message text** field and click **OK** at the bottom of the dialog.</span></span> 

1. <span data-ttu-id="b7a86-156">데이터 탐색기에서 다음 스크린샷과 비슷한 메시지를 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-156">Observe the message, similar to the message in the following screenshot, in the data explorer.</span></span>
<span data-ttu-id="b7a86-157">![큐에서 만든 메시지가 있는 저장소 계정을 보여주는 저장소 탐색기의 스크린샷.](../media-draft/message-in-input-queue.png)</span><span class="sxs-lookup"><span data-stu-id="b7a86-157">![Screenshot of storage explorer showing our storage account, with the message we created in the queue.](../media-draft/message-in-input-queue.png)</span></span>

1. <span data-ttu-id="b7a86-158">몇 초 후, **새로 고침**을 클릭하여 큐 보기를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-158">After a few seconds, click **Refresh** to refresh the view of the queue.</span></span> <span data-ttu-id="b7a86-159">큐가 비어 있는 것을 다시 한 번 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-159">Observe that the queue is empty once again.</span></span> <span data-ttu-id="b7a86-160">무언가가 큐에서 메시지를 읽은 것이 분명합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-160">Something must have read the message from the queue.</span></span> 

1. <span data-ttu-id="b7a86-161">포털에서 함수로 돌아가서 **모니터링** 탭을 엽니다. 목록에서 최신 메시지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-161">Navigate back to our function in the portal and open the **Monitor** tab. Select the newest message and in the list.</span></span> <span data-ttu-id="b7a86-162">new-feedback-q에 게시된 큐 메시지를 함수가 처리한 것을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-162">Observe that our function processed the queue message we had posted to the new-feedback-q.</span></span>

![new-feedback-q에 게시된 큐 메시지를 함수가 처리한 사실을 알려주는 항목을 표시하는 [모니터링] 대시보드의 스크린샷.](../media-draft/message-in-monitor.png)

<span data-ttu-id="b7a86-164">이 테스트에서는 큐에 항목을 게시하고 함수가 해당 항목을 처리하는 모습을 살펴보는 완전한 왕복 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-164">In this test, we did a complete round trip of posting something into our queue and then seeing the function process it.</span></span>

<span data-ttu-id="b7a86-165">우리 솔루션이 점점 발전하고 있습니다!</span><span class="sxs-lookup"><span data-stu-id="b7a86-165">We're making progress with our solution!</span></span> <span data-ttu-id="b7a86-166">이 함수는 이제 유용한 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-166">Our function is now doing something useful.</span></span> <span data-ttu-id="b7a86-167">입력 큐에서 텍스트를 받은 후 텍스트 분석 API 서비스를 호출하여 감정 점수를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-167">It's receiving text from our input queue and then calling out to the Text Analytics API service to get a sentiment score.</span></span>  <span data-ttu-id="b7a86-168">또한 Azure Portal 및 Storage 탐색기를 통해 함수를 테스트하는 방법을 배웠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-168">We've also learned how to test our function through the Azure portal and the Storage Explorer.</span></span> <span data-ttu-id="b7a86-169">다음 연습에서는 출력 바인딩을 사용하여 큐에 얼마나 간단하게 쓸 수 있는지 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b7a86-169">In the next exercise, we'll see how easy it is to write to queues using output bindings.</span></span>