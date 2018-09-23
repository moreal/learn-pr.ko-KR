<span data-ttu-id="b9fa6-101">마지막 연습에서는 Azure Cosmos DB 데이터베이스에서 책갈피를 조회하는 시나리오를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-101">In our last exercise, we implemented a scenario to look up bookmarks in an Azure Cosmos DB database.</span></span> <span data-ttu-id="b9fa6-102">책갈피 컬렉션에서 데이터를 읽도록 입력 바인딩을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-102">We configured an input binding to read data from our bookmarks collection.</span></span> <span data-ttu-id="b9fa6-103">그러나 더 많은 것을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-103">But, we can do more.</span></span> <span data-ttu-id="b9fa6-104">이제 쓰기를 포함하도록 시나리오를 확장해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-104">Let's expand the scenario to include writing.</span></span> <span data-ttu-id="b9fa6-105">다음 순서도를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-105">Consider the following flowchart:</span></span>

![Cosmos DB 백 엔드에서 책갈피를 찾는 프로세스를 보여 주는 흐름 다이어그램입니다.](../media/7-add-bookmark-flow-small.png)

<span data-ttu-id="b9fa6-110">이 시나리오에서는 책갈피를 컬렉션에 추가하라는 요청을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-110">In this scenario, we'll receive requests to add bookmarks to our collection.</span></span> <span data-ttu-id="b9fa6-111">요청은 책갈피 URL과 함께 원하는 키 또는 ID를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-111">The requests pass in the desired key, or ID, along with the bookmark URL.</span></span> <span data-ttu-id="b9fa6-112">순서도에서 볼 수 있듯이 키가 이미 백 엔드에 있는 경우 오류로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-112">As you can see in the flowchart, we'll respond with an error if the key already exists in our back end.</span></span>

<span data-ttu-id="b9fa6-113">전달된 키가 *없으면* 새 책갈피를 데이터베이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-113">If the key that was passed to us is *not* found, we'll add the new bookmark to our database.</span></span> <span data-ttu-id="b9fa6-114">여기서 중지할 수 있지만 조금 더 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-114">We could stop there, but let's do a little more.</span></span>

<span data-ttu-id="b9fa6-115">순서도에서 또 다른 단계가 눈에 띄나요?</span><span class="sxs-lookup"><span data-stu-id="b9fa6-115">Notice another step in the flowchart?</span></span> <span data-ttu-id="b9fa6-116">지금까지 처리 측면에서 받는 데이터를 별로 다루지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-116">So far we haven't done much with the data that we receive in terms of processing.</span></span> <span data-ttu-id="b9fa6-117">받는 데이터를 데이터베이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-117">We move what we receive into a database.</span></span> <span data-ttu-id="b9fa6-118">그러나 실제 솔루션에서는 특정 방식으로 데이터를 처리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-118">However, in a real solution, it is possible that we'd probably process the data in some fashion.</span></span> <span data-ttu-id="b9fa6-119">동일한 함수에서 모두 처리하도록 결정할 수 있지만, 이 랩에서는 추가 처리를 다른 구성 요소 또는 비즈니스 논리 부분으로 오프로드하는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-119">We can decide to do all processing in the same function, but in this lab we'll show a pattern that offloads further processing to another component or piece of business logic.</span></span>

<span data-ttu-id="b9fa6-120">책갈피 시나리오에서 이러한 작업 오프로딩의 좋은 예는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="b9fa6-120">What might be a good example of this offloading of work in our bookmarks scenario?</span></span> <span data-ttu-id="b9fa6-121">그렇다면, 새 책갈피를 QR 코드 생성 서비스로 보내면 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="b9fa6-121">Well, what if we send the new bookmark to a QR code generation service?</span></span> <span data-ttu-id="b9fa6-122">이 경우 해당 서비스에서 URL에 대한 QR 코드를 생성하고, 이미지를 Blob 저장소에 저장하고, QR 이미지의 주소를 책갈피 컬렉션의 항목에 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-122">That service would, in turn, generate a QR code for the URL, store the image in blob storage, and add the address of the QR image back into the entry in our bookmarks collection.</span></span> <span data-ttu-id="b9fa6-123">QR 이미지를 생성하는 서비스를 호출하는 경우 시간이 많이 걸리므로 결과를 기다리는 대신 해당 결과를 함수에 전달하여 비동기적으로 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-123">Calling a service to generate a QR image is time consuming so, rather than wait for the result, we hand it off to a function and let it take care of this asynchronously.</span></span>

<span data-ttu-id="b9fa6-124">Azure Functions에서 다양한 통합 원본에 대한 입력 바인딩을 지원하는 것처럼 데이터 원본에 데이터를 쉽게 쓸 수 있도록 하는 일단의 출력 바인딩 템플릿도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-124">Just as Azure Functions supports input bindings for various integration sources, it also has a set of output bindings templates to make it easy for you to write data to data sources.</span></span> <span data-ttu-id="b9fa6-125">출력 바인딩은 *function.json* 파일에도 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-125">Output bindings are also configured in the *function.json* file.</span></span>  <span data-ttu-id="b9fa6-126">이 연습에서 살펴보겠지만 함수는 다중 데이터 원본 및 서비스를 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-126">As you'll see in this exercise, we can configure our function to work with multiple data sources and services.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b9fa6-127">이 연습은 이전 연습을 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-127">This exercise builds on the previous one.</span></span> <span data-ttu-id="b9fa6-128">동일한 Azure Cosmos DB 데이터베이스 및 입력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-128">It uses the same Azure Cosmos DB database and input binding.</span></span> <span data-ttu-id="b9fa6-129">해당 단원을 수행하지 않은 경우 이 단원을 진행하기 전에 수행하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-129">If you haven't worked through that unit, we recommend doing so before you proceed with this one.</span></span>

## <a name="create-an-http-triggered-function"></a><span data-ttu-id="b9fa6-130">HTTP-triggered 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="b9fa6-130">Create an HTTP-triggered function</span></span>

1. <span data-ttu-id="b9fa6-131">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-131">Sign into the [Azure portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

2. <span data-ttu-id="b9fa6-132">Azure Portal의 해당 모듈에서 만든 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-132">In the portal, navigate to the function app that you created in this module.</span></span>

3. <span data-ttu-id="b9fa6-133">함수 앱을 확장한 다음, 함수 컬렉션 위에 마우스를 놓고, **함수** 옆에 있는 추가(**+**) 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-133">Expand your function app, then hover over the functions collection and select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="b9fa6-134">이 작업은 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-134">This action starts the function creation process.</span></span> <span data-ttu-id="b9fa6-135">다음 애니메이션에서는 이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-135">The following animation illustrates this action.</span></span>

    ![사용자가 함수 메뉴 항목을 마우스로 가리키면 표시되는 더하기 기호의 애니메이션](../media/3-func-app-plus-hover-small.gif)

4. <span data-ttu-id="b9fa6-137">이 페이지에는 지원되는 트리거의 현재 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-137">The page shows us the current set of supported triggers.</span></span> <span data-ttu-id="b9fa6-138">다음 스크린샷의 첫 번째 항목인 **HTTP 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-138">Select **HTTP trigger**, which is the first entry in the following screenshot.</span></span>

    ![이미지의 왼쪽 위에 TTP 트리거가 먼저 표시된 트리거 템플릿 선택 UI 일부의 스크린샷.](../media/5-trigger-templates-small.PNG)


5. <span data-ttu-id="b9fa6-140">다음 값을 사용하여 오른쪽에 표시되는 **새 함수** 창을 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-140">Fill out the **New Function** pane that's displayed at the right by using the following values:</span></span>

    |<span data-ttu-id="b9fa6-141">필드</span><span class="sxs-lookup"><span data-stu-id="b9fa6-141">Field</span></span>  |<span data-ttu-id="b9fa6-142">값</span><span class="sxs-lookup"><span data-stu-id="b9fa6-142">Value</span></span>  |
    |---------|---------|
    |<span data-ttu-id="b9fa6-143">언어</span><span class="sxs-lookup"><span data-stu-id="b9fa6-143">Language</span></span>     | <span data-ttu-id="b9fa6-144">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-144">**JavaScript**</span></span>        |
    |<span data-ttu-id="b9fa6-145">이름</span><span class="sxs-lookup"><span data-stu-id="b9fa6-145">Name</span></span>     |   [!INCLUDE [func-name-add](./func-name-add.md)]     |
    | <span data-ttu-id="b9fa6-146">권한 부여 수준</span><span class="sxs-lookup"><span data-stu-id="b9fa6-146">Authorization level</span></span> | <span data-ttu-id="b9fa6-147">**Function**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-147">**Function**</span></span> |
    
6. <span data-ttu-id="b9fa6-148">**만들기**를 선택하여 사용자의 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-148">Select **Create** to create your function.</span></span> <span data-ttu-id="b9fa6-149">이 작업은 코드 편집기에서 **index.js** 파일을 열고 HTTP 트리거 함수의 기본 구현을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-149">This action opens the **index.js** file in the code editor and displays a default implementation of the HTTP-triggered function.</span></span>

    > [!NOTE]
    > <span data-ttu-id="b9fa6-150">이 연습에서는 이전 단원의 *코드*와 *구성*을 시작 지점으로 사용하여 작업 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-150">In this exercise, we'll speed up things by using the *code* and *configuration* from the previous unit as a starting point.</span></span>

7. <span data-ttu-id="b9fa6-151">**index.js** 파일의 모든 코드를 다음 코드 조각의 코드로 바꾼 다음, **저장**을 선택하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-151">Replace all code in the **index.js** file with the code from the following snippet, and then select **Save** to save the change:</span></span> 

   [!code-javascript[](../code/find-bookmark-single.js)]

   <span data-ttu-id="b9fa6-152">이 코드가 익숙해 보인다면 이는 [!INCLUDE [func-name-find](./func-name-find.md)] 함수를 구현했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-152">If this code looks familiar, that's because it's the implementation of our [!INCLUDE [func-name-find](./func-name-find.md)] function.</span></span> <span data-ttu-id="b9fa6-153">예상한 대로 함수는 동일한 바인딩을 정의할 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-153">As you would expect, the function won't work until we define the same bindings.</span></span>  

1. <span data-ttu-id="b9fa6-154">[!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 **function.json** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-154">Open the **function.json** file from the [!INCLUDE [func-name-add](./func-name-add.md)] function.</span></span>

11. <span data-ttu-id="b9fa6-155">이 파일 내용을 다음 JSON으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-155">Replace the contents of this file with the following JSON:</span></span>

    ```json
    {
      "bindings": [
        {
          "authLevel": "function",
          "type": "httpTrigger",
          "direction": "in",
          "name": "req"
        },
        {
          "type": "http",
          "direction": "out",
          "name": "res"
        },
        {
          "type": "documentDB",
          "name": "bookmark",
          "databaseName": "func-io-learn-db",
          "collectionName": "Bookmarks",
          "connection": "unit3test_DOCUMENTDB",
          "direction": "in",
          "id": "{id}"
        }
      ],
      "disabled": false
    }
    ```

12. <span data-ttu-id="b9fa6-156">모든 변경 내용을 **저장**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-156">Make sure to **Save** all changes.</span></span>

<span data-ttu-id="b9fa6-157">이전 단계에서는 다른 함수에서 바인딩 정의를 복사하여 새 함수에 대한 바인딩을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-157">In the preceding steps, you configured bindings for your new function by copying binding definitions from another function.</span></span> <span data-ttu-id="b9fa6-158">물론 UI를 통해 새 바인딩을 만들 수도 있지만, 이 대안을 사용할 수 있음을 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-158">Of course, you could have created a new binding through the UI, but it is good to understand that this alternative is available to you.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="b9fa6-159">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="b9fa6-159">Try it out</span></span>

1. <span data-ttu-id="b9fa6-160">오른쪽 맨 위에서 **함수 URL 가져오기**를 선택하고 **기본값(함수 키)** 을 선택한 다음, **복사**를 선택하여 함수의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-160">Select **Get function URL** at the top right, select **default (Function key)**, and then select **Copy** to copy the function's URL.</span></span>

2. <span data-ttu-id="b9fa6-161">복사한 URL을 브라우저의 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-161">Paste the copied URL into your browser's address bar.</span></span> <span data-ttu-id="b9fa6-162">URL의 끝에 `&id=docs` 쿼리 문자열 값을 추가한 다음, Enter 키를 눌러 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-162">Add the query string value `&id=docs` to the end of the URL, and then press Enter to execute the request.</span></span> <span data-ttu-id="b9fa6-163">모든 작업이 잘 진행되면 해당 리소스에 대한 URL이 포함된 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-163">If all goes well, you should see a response that includes a URL to that resource.</span></span>

<span data-ttu-id="b9fa6-164">그러면 지금은 어디에 있을까요?</span><span class="sxs-lookup"><span data-stu-id="b9fa6-164">So, where are we at?</span></span> <span data-ttu-id="b9fa6-165">글쎄요, 지금까지 이전 랩에서 수행했던 것을 그대로 복제했을 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-165">Well, so far we've really just replicated what we did in the previous lab.</span></span> <span data-ttu-id="b9fa6-166">하지만 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-166">But that's okay.</span></span> <span data-ttu-id="b9fa6-167">이 작업의 시작 지점으로 사용하기 위해 마지막 랩에서 수행한 것을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-167">We're copying what we did in the last lab to serve as a starting point for this one.</span></span> <span data-ttu-id="b9fa6-168">다음에 새로운 기능을 다룰 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-168">We'll work on the new stuff next.</span></span> <span data-ttu-id="b9fa6-169">즉, 데이터베이스에 작성할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-169">That is, we'll write to our database.</span></span> <span data-ttu-id="b9fa6-170">이를 위해 *출력 바인딩*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-170">For that, we'll need an *output binding*.</span></span>

## <a name="define-azure-cosmos-db-output-binding"></a><span data-ttu-id="b9fa6-171">Azure Cosmos DB 출력 바인딩 정의</span><span class="sxs-lookup"><span data-stu-id="b9fa6-171">Define Azure Cosmos DB output binding</span></span>

<span data-ttu-id="b9fa6-172">사용자 인터페이스를 통해 새 출력 바인딩을 정의하는 대신, 구성 파일 *function.json*을 직접 업데이트하여 이 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-172">Rather than define a new output binding by going through the user interface, you'll create this binding by updating the configuration file, *function.json*, by hand.</span></span> 

1. <span data-ttu-id="b9fa6-173">[!INCLUDE [func-name-add](./func-name-add.md)]에 대한 *function.json* 파일이 편집기에서 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-173">Make sure the *function.json* file for [!INCLUDE [func-name-add](./func-name-add.md)] is open in the editor.</span></span>

1. <span data-ttu-id="b9fa6-174">해당 파일에서 이름이 `bookmark`인 바인딩을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-174">Copy the binding that's named `bookmark` in that file.</span></span>

1. <span data-ttu-id="b9fa6-175">닫는 중괄호(}) 바로 뒤에 커서를 놓고 닫는 대괄호(]) 바로 앞에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-175">Place your cursor directly after the closing curly bracket (}), and right before the closing square bracket (]).</span></span> <span data-ttu-id="b9fa6-176">쉼표(,)를 추가한 다음, 여기에 바인딩의 복사본을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-176">Add a comma (,), and then paste the copy of the binding here.</span></span> <span data-ttu-id="b9fa6-177">*function.json* 구성 파일은 이제 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-177">Your *function.json* config file should now look like the following:</span></span>

   [!code-json[](../code/config-new-entry.json?highlight=22-31)]

1. <span data-ttu-id="b9fa6-178">다음과 같은 변경 내용으로 붙여넣은 바인딩을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-178">Edit the binding you pasted, with the following changes:</span></span>

    |<span data-ttu-id="b9fa6-179">속성</span><span class="sxs-lookup"><span data-stu-id="b9fa6-179">Property</span></span>   |<span data-ttu-id="b9fa6-180">이전 값</span><span class="sxs-lookup"><span data-stu-id="b9fa6-180">Old value</span></span>  |<span data-ttu-id="b9fa6-181">새 값</span><span class="sxs-lookup"><span data-stu-id="b9fa6-181">New value</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="b9fa6-182">name</span><span class="sxs-lookup"><span data-stu-id="b9fa6-182">name</span></span>     |   <span data-ttu-id="b9fa6-183">bookmark</span><span class="sxs-lookup"><span data-stu-id="b9fa6-183">bookmark</span></span>      |  <span data-ttu-id="b9fa6-184">**newbookmark**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-184">**newbookmark**</span></span>       |
    |<span data-ttu-id="b9fa6-185">direction</span><span class="sxs-lookup"><span data-stu-id="b9fa6-185">direction</span></span>     |   <span data-ttu-id="b9fa6-186">in</span><span class="sxs-lookup"><span data-stu-id="b9fa6-186">in</span></span>      |   <span data-ttu-id="b9fa6-187">**out**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-187">**out**</span></span>      |
    |<span data-ttu-id="b9fa6-188">id</span><span class="sxs-lookup"><span data-stu-id="b9fa6-188">id</span></span>     |      <span data-ttu-id="b9fa6-189">{id}</span><span class="sxs-lookup"><span data-stu-id="b9fa6-189">{id}</span></span>   |   <span data-ttu-id="b9fa6-190">**이 속성은 삭제합니다. 출력 바인딩에는 존재하지 않기 때문입니다.**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-190">**delete this property. It does not exist for the output binding.**</span></span>      |

1. <span data-ttu-id="b9fa6-191">이렇게 변경한 후에 파일이 다음 JSON과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-191">After you've made these changes, your file looks like the following JSON:</span></span>

    [!code-json[](../code/config-q-complete.json?highlight=22-30)]

<span data-ttu-id="b9fa6-192">이는 구성 파일에서 직접 바인딩을 만드는 방법을 보여 주는 데모일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-192">That was just a demo of how you can also create bindings directly in the configuration file.</span></span> <span data-ttu-id="b9fa6-193">이 예제에서는 다른 바인딩의 속성을 다시 사용하기 때문에 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-193">In this example, it makes sense because you are reusing the properties from another binding.</span></span> <span data-ttu-id="b9fa6-194">즉, Azure Cosmos DB 입력 바인딩에 대해 이미 구성한 `databaseName`, `collectionName` 및 `connection`을 재사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-194">That is, you're reusing the `databaseName`, `collectionName`, and `connection` that you already configured for your Azure Cosmos DB input binding.</span></span>

> [!NOTE]
> <span data-ttu-id="b9fa6-195">앞의 JSON 파일에서 `connection`의 실제 값은 연결을 만들 때 지정한 연결 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-195">The actual value of `connection` in the preceding JSON file is whatever name your connection was given when it was created.</span></span>

<span data-ttu-id="b9fa6-196">코드를 업데이트하기 전에 큐에 메시지를 게시할 수 있게 하는 바인딩을 하나 더 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-196">Before we update our code, let's add one more binding that will enable us to post messages to a queue.</span></span>

## <a name="define-azure-queue-storage-output-binding"></a><span data-ttu-id="b9fa6-197">Azure Queue Storage 출력 바인딩 정의</span><span class="sxs-lookup"><span data-stu-id="b9fa6-197">Define Azure Queue Storage output binding</span></span>

<span data-ttu-id="b9fa6-198">Azure Queue 저장소는 전 세계 어디서나 액세스할 수 있는 메시지를 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-198">Azure Queue storage is a service for storing messages that can be accessed from anywhere in the world.</span></span> <span data-ttu-id="b9fa6-199">단일 메시지의 크기는 최대 64KB까지 가능하며, 큐에는 정의된 저장소 계정의 총 용량 한도까지 수백만 개의 메시지&mdash;가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-199">The size of a single message can be as much as 64 KB, and a queue can contain millions of messages&mdash;up to the total capacity of the storage account in which it is defined.</span></span> <span data-ttu-id="b9fa6-200">다음 다이어그램에서는 이 시나리오에서 큐를 사용하는 방법을 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-200">The following diagram shows at a high level how a queue is used in our scenario:</span></span>

![저장소 큐 및 두 개의 함수 중 하나에 푸시하고 큐에 다른 팝업 메시지를 보여 주는 일러스트레이션](../media/7-q-logical-small.png)

<span data-ttu-id="b9fa6-202">여기에서 새 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 메시지를 큐에 추가하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-202">Here you can see that the new function, [!INCLUDE [func-name-add](./func-name-add.md)], adds messages to a queue.</span></span> <span data-ttu-id="b9fa6-203">다른 함수, &mdash;예를 들어 *gen-qr-code*라는 가상의 함수&mdash;는 동일한 큐에서 메시지를 팝하고 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-203">Another function&mdash;for example, a fictitious function called *gen-qr-code*&mdash;will pop messages from the same queue and process the request.</span></span>  <span data-ttu-id="b9fa6-204">[!INCLUDE [func-name-add](./func-name-add.md)]에서 큐에 메시지를 쓰거나 *푸시*하므로 솔루션에 새 출력 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-204">Since we write, or *push*, messages to the queue from [!INCLUDE [func-name-add](./func-name-add.md)], we'll add a new output binding to your solution.</span></span> <span data-ttu-id="b9fa6-205">이번에는 포털 UI를 통해 바인딩을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-205">Let's create the binding through the portal UI this time.</span></span>

1. <span data-ttu-id="b9fa6-206">왼쪽 함수 메뉴에서 **통합**을 선택하여 통합 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-206">Select **Integrate** in the left function menu to open the integration tab.</span></span>

2. <span data-ttu-id="b9fa6-207">**출력** 열에서 **새 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-207">Select **New Output** in the **Outputs** column.</span></span>  
    <span data-ttu-id="b9fa6-208">가능한 모든 출력 바인딩 형식 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-208">A list of all possible output binding types is displayed.</span></span>

3. <span data-ttu-id="b9fa6-209">목록에서 **Azure Queue Storage**를 선택한 다음, **선택**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-209">In the list, select **Azure Queue Storage**, then select **Select**.</span></span>  
    <span data-ttu-id="b9fa6-210">그러면 Azure Queue Storage 출력 구성 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-210">This action opens the Azure Queue Storage output configuration page.</span></span>

   <span data-ttu-id="b9fa6-211">다음으로, 저장소 계정 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-211">Next, we'll set up a storage account connection.</span></span> <span data-ttu-id="b9fa6-212">여기서 큐가 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-212">This is where our queue will be hosted.</span></span>

4. <span data-ttu-id="b9fa6-213">**저장소 계정 연결** 필드의 오른쪽에 있는 **새로 만들기**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-213">To the right of the **Storage account connection** field, select **new**.</span></span>  
   <span data-ttu-id="b9fa6-214">**저장소 계정** 선택 창이 열립니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-214">The **Storage Account** selection pane opens.</span></span> 

5. <span data-ttu-id="b9fa6-215">이 모듈을 시작하고 함수 앱을 만들었을 때 저장소 계정도 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-215">When we started this module and you created your function app, a storage account was also created at that time.</span></span> <span data-ttu-id="b9fa6-216">이 창에 나열되어 있으므로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-216">It's listed in this pane, so select it.</span></span> <span data-ttu-id="b9fa6-217">**저장소 계정 연결** 필드가 연결 이름으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-217">The **Storage account connection** field is populated with the name of a connection.</span></span> <span data-ttu-id="b9fa6-218">연결 문자열 값을 보려면 **값 표시**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-218">If you want to see the connection string value, select **show value**.</span></span>

6. <span data-ttu-id="b9fa6-219">다른 모든 필드에 기본값을 그대로 둘 수 있지만 다음 항목을 변경하여 속성에 더 많은 의미를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-219">Although we could keep the default values in all the other fields, let's change the following to lend more meaning to the properties:</span></span>

    |<span data-ttu-id="b9fa6-220">속성</span><span class="sxs-lookup"><span data-stu-id="b9fa6-220">Property</span></span>  |<span data-ttu-id="b9fa6-221">이전 값</span><span class="sxs-lookup"><span data-stu-id="b9fa6-221">Old value</span></span>  |<span data-ttu-id="b9fa6-222">새 값</span><span class="sxs-lookup"><span data-stu-id="b9fa6-222">New value</span></span>  | <span data-ttu-id="b9fa6-223">설명</span><span class="sxs-lookup"><span data-stu-id="b9fa6-223">Description</span></span> |
    |---------|---------|---------|---------|
    |<span data-ttu-id="b9fa6-224">큐 이름</span><span class="sxs-lookup"><span data-stu-id="b9fa6-224">Queue name</span></span>     |    <span data-ttu-id="b9fa6-225">outqueue</span><span class="sxs-lookup"><span data-stu-id="b9fa6-225">outqueue</span></span>     |  <span data-ttu-id="b9fa6-226">**bookmarks-post-process**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-226">**bookmarks-post-process**</span></span>      | <span data-ttu-id="b9fa6-227">책갈피를 배치하여 다른 함수에서 추가로 처리할 수 있도록 하는 큐의 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-227">The name of the queue where we're placing bookmarks so that they can be processed further by another function.</span></span> |
    | <span data-ttu-id="b9fa6-228">메시지 매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="b9fa6-228">Message parameter name</span></span>    |  <span data-ttu-id="b9fa6-229">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="b9fa6-229">outputQueueItem</span></span>       |   <span data-ttu-id="b9fa6-230">**newmessage**</span><span class="sxs-lookup"><span data-stu-id="b9fa6-230">**newmessage**</span></span>      | <span data-ttu-id="b9fa6-231">코드에서 사용할 바인딩 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-231">The binding property we'll use in code.</span></span> |

7. <span data-ttu-id="b9fa6-232">**저장**을 선택하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-232">Remember to select **Save** to save your changes.</span></span>

## <a name="update-function-implementation"></a><span data-ttu-id="b9fa6-233">업데이트 함수 구현</span><span class="sxs-lookup"><span data-stu-id="b9fa6-233">Update function implementation</span></span>

<span data-ttu-id="b9fa6-234">이제 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에 대한 모든 바인딩이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-234">We now have all our bindings set up for the [!INCLUDE [func-name-add](./func-name-add.md)] function.</span></span> <span data-ttu-id="b9fa6-235">함수에서 이러한 바인딩을 사용할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-235">It's time to use them in our function.</span></span>

1.  <span data-ttu-id="b9fa6-236">[!INCLUDE [func-name-add](./func-name-add.md)] 함수를 선택하여 코드 편집기에서 **index.js** 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-236">Select your function, [!INCLUDE [func-name-add](./func-name-add.md)], to open the **index.js** file in the code editor.</span></span>

2. <span data-ttu-id="b9fa6-237">*index.js* 파일의 모든 코드를 다음 코드 조각의 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-237">Replace all the code in the *index.js* file with the code from the following snippet:</span></span>

   [!code-javascript[](../code/add-bookmark.js)]

<span data-ttu-id="b9fa6-238">이 코드의 기능을 분석해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-238">Let's break down what this code does:</span></span>

* <span data-ttu-id="b9fa6-239">이 함수는 데이터를 변경하므로 HTTP 요청이 POST이고 책갈피 데이터가 요청 본문에 포함될 것으로 예상합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-239">Because this function changes our data, we expect the HTTP request to be a POST and the bookmark data to be part of the request body.</span></span>
* <span data-ttu-id="b9fa6-240">Azure Cosmos DB 입력 바인딩은 수신한 `id`를 사용하여 문서 또는 책갈피를 검색하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-240">Our Azure Cosmos DB input binding attempts to retrieve a document, or bookmark, by using the `id` that we receive.</span></span> <span data-ttu-id="b9fa6-241">항목을 찾으면 `bookmark` 개체가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-241">If it finds an entry, the `bookmark` object will be set.</span></span> <span data-ttu-id="b9fa6-242">`if(bookmark)` 조건은 항목이 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-242">The `if(bookmark)` condition checks to see whether an entry was found.</span></span>
* <span data-ttu-id="b9fa6-243">데이터베이스에 추가하는 것은 `context.bindings.newbookmark` 바인딩 매개 변수를 JSON 문자열로 만든 새 책갈피 항목으로 설정하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-243">Adding to the database is as simple as setting the `context.bindings.newbookmark` binding parameter to the new bookmark entry, which we have created as a JSON string.</span></span>
* <span data-ttu-id="b9fa6-244">메시지를 큐에 게시하는 것은 `context.bindings.newmessage parameter`를 설정하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-244">Posting a message to our queue is as simple as setting the  `context.bindings.newmessage parameter`.</span></span>

> [!NOTE]
> <span data-ttu-id="b9fa6-245">수행한 유일한 작업은 큐 바인딩을 만드는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-245">The only task you performed was to create a queue binding.</span></span> <span data-ttu-id="b9fa6-246">큐는 명시적으로 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-246">You never created the queue explicitly.</span></span> <span data-ttu-id="b9fa6-247">지금 바인딩의 능력을 목격하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-247">You are witnessing the power of bindings!</span></span> <span data-ttu-id="b9fa6-248">다음 설명선에서 볼 수 있듯이 큐가 없으면 자동으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-248">As the following callout says, the queue is automatically created for you if it doesn't exist.</span></span>

![큐를 자동으로 만들도록 호출하는 스크린샷.](../media/7-q-auto-create-small.png)

<span data-ttu-id="b9fa6-250">이것으로 끝입니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-250">So, that's it.</span></span> <span data-ttu-id="b9fa6-251">다음 섹션에서 진행 중인 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-251">Let's see our work in action in the next section.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="b9fa6-252">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="b9fa6-252">Try it out</span></span>

<span data-ttu-id="b9fa6-253">이제 여러 개의 출력 바인딩이 있으므로 테스트가 좀 더 까다로워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-253">Now that we have multiple output bindings, testing becomes a little trickier.</span></span> <span data-ttu-id="b9fa6-254">이전 랩에서는 HTTP 요청과 쿼리 문자열을 보내 테스트하는 데 만족했지만 이번에는 HTTP 게시를 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-254">In previous labs we were content to test by sending an HTTP request and a query string, but we'll want to perform an HTTP post this time.</span></span> <span data-ttu-id="b9fa6-255">또한 메시지에서 이 게시를 큐에 넣는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-255">We also need to check to see whether messages are making it into a queue.</span></span>

1. <span data-ttu-id="b9fa6-256">함수 앱 포털에서 선택한 [!INCLUDE [func-name-add](./func-name-add.md)] 함수를 사용하여 맨 왼쪽에 있는 테스트 메뉴 항목을 선택하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-256">With our function, [!INCLUDE [func-name-add](./func-name-add.md)], selected in the Function Apps portal, select the Test menu item at the far left to expand it.</span></span>

2. <span data-ttu-id="b9fa6-257">**테스트** 메뉴 항목을 선택하고, 테스트 창이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-257">Select the **Test** menu item, and verify that you have the test pane open.</span></span> <span data-ttu-id="b9fa6-258">다음 스크린샷에서는 다음과 같이 표시되는 것을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-258">The following screenshot shows what it should look like:</span></span> 

    ![확장된 함수 테스트 패널을 보여주는 스크린샷.](../media/7-test-panel-open-small.png)

    > [!IMPORTANT]
    > <span data-ttu-id="b9fa6-260">HTTP 메서드 드롭다운 목록에서 **POST**가 선택되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-260">Make sure that **POST** is selected in the HTTP method drop-down list.</span></span>

3. <span data-ttu-id="b9fa6-261">요청 본문의 내용을 다음 JSON 페이로드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-261">Replace the content of the request body with the following JSON payload:</span></span>

    ```json
    {
        "id": "docs",
        "url": "https://docs.microsoft.com/azure"
    }
    ```

4. <span data-ttu-id="b9fa6-262">테스트 창 아래쪽에서 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-262">Select **Run** at the bottom of the test pane.</span></span> 

5. <span data-ttu-id="b9fa6-263">다음 다이어그램에 표시된 대로 **출력** 창에 "책갈피가 이미 존재함"이라는 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-263">Verify that the **Output** window displays the "Bookmark already exists" message, as shown in the following diagram:</span></span> 

    ![테스트 패널 및 실패한 테스트의 결과를 보여 주는 스크린샷.](../media/7-test-exists-small.png)

6. <span data-ttu-id="b9fa6-265">요청 본문을 다음 페이로드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-265">Replace the request body with the following payload:</span></span> 

    ```json
    {
        "id": "github",
        "url": "https://www.github.com"
    }
    ```
7. <span data-ttu-id="b9fa6-266">테스트 창 아래쪽에서 **실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-266">Select **Run** at the bottom of the test pane.</span></span>

8. <span data-ttu-id="b9fa6-267">다음 다이어그램에 표시된 대로 *출력* 상자에 "책갈피 추가됨"이라는 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-267">Verify the that *Output* box displays the "bookmark added" message as shown in the following diagram.</span></span>

    ![테스트 패널 및 성공한 테스트의 결과를 보여 주는 스크린샷](../media/7-test-success-small.png)

<span data-ttu-id="b9fa6-269">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="b9fa6-269">Congratulations!</span></span> <span data-ttu-id="b9fa6-270">[!INCLUDE [func-name-add](./func-name-add.md)]는 설계한 대로 작동하지만 코드에 있던 큐 작업은 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="b9fa6-270">The [!INCLUDE [func-name-add](./func-name-add.md)] works as designed, but what about that queue operation we had in the code?</span></span> <span data-ttu-id="b9fa6-271">그럼, 큐에 어떤 것이 쓰여 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-271">Well, let's go see whether something was written to a queue.</span></span>

### <a name="verify-that-a-message-is-written-to-the-queue"></a><span data-ttu-id="b9fa6-272">메시지가 큐에 쓰여 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-272">Verify that a message is written to the queue</span></span>

<span data-ttu-id="b9fa6-273">Azure Queue Storage 큐는 저장소 계정에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-273">Azure Queue Storage queues are hosted in a storage account.</span></span> <span data-ttu-id="b9fa6-274">이 연습에서는 출력 바인딩을 만들 때 이미 저장소 계정을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-274">You already selected the storage account in this exercise when you created the output binding.</span></span> 

1. <span data-ttu-id="b9fa6-275">Azure Portal의 기본 검색 상자에서 **저장소 계정**을 입력하고, 결과 목록의 **서비스**에서 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-275">In the main search box in the Azure portal, type **storage accounts**, and in the results list, under **Services**, select **Storage accounts**.</span></span> 

      ![기본 검색 상자에서 저장소 계정에 대한 검색 결과를 보여 주는 스크린샷.](../media/7-search-for-sa-small.png)

2. <span data-ttu-id="b9fa6-277">반환된 저장소 계정 목록에서 **newmessage** 출력 바인딩을 만드는 데 사용한 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-277">In the list of storage accounts that are returned, select the storage account that you used to create the **newmessage** output binding.</span></span>  
   <span data-ttu-id="b9fa6-278">저장소 계정 설정은 포털의 주 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-278">The storage account settings are displayed in the main window of the portal.</span></span>

3. <span data-ttu-id="b9fa6-279">**서비스** 목록에서 **큐** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-279">In the **Services** list, select the **Queues** item.</span></span>  
   <span data-ttu-id="b9fa6-280">이 저장소 계정에서 호스팅하는 큐의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-280">A list of queues hosted by this storage account is displayed.</span></span> <span data-ttu-id="b9fa6-281">다음 스크린샷과 같이 **bookmarks-post-process** 큐가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-281">Verify that the **bookmarks-post-process** queue exists, as shown in the following screenshot:</span></span>

      ![이 저장소 계정에서 호스팅하는 큐 목록에서 큐를 보여 주는 스크린샷](../media/7-q-in-list-small.png)

4. <span data-ttu-id="b9fa6-283">**bookmarks-post-process**를 선택하여 큐를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-283">Select **bookmarks-post-process** to open the queue.</span></span>  
   <span data-ttu-id="b9fa6-284">큐에 있는 메시지가 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-284">The messages that are in the queue are displayed in a list.</span></span> <span data-ttu-id="b9fa6-285">모두 계획에 따라 진행된 경우, 데이터베이스에 책갈피를 추가할 때 게시한 메시지가 큐에 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-285">If all went according to plan, the queue includes the message that you posted when you added a bookmark to the database.</span></span> <span data-ttu-id="b9fa6-286">다음과 같아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-286">It should look like the following:</span></span> 

    ![큐의 메시지를 보여 주는 스크린샷](../media/7-message-in-q-small.png)    

   <span data-ttu-id="b9fa6-288">이 예제에서는 메시지에 고유한 ID가 지정되어 있고 **메시지 텍스트** 필드에 책갈피가 JSON 문자열 형식으로 표시된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-288">In this example, you can see that the message was given a unique ID, and the **MESSAGE TEXT** field displays your bookmark in JSON string format.</span></span>

5. <span data-ttu-id="b9fa6-289">테스트 창에서 요청 본문을 새 ID/URL 집합으로 변경하고 함수를 실행하여 함수를 추가로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-289">You can test the function further by changing the request body in the test pane with new id/url sets and running the function.</span></span> <span data-ttu-id="b9fa6-290">이 큐를 조사하여 더 많은 메시지가 도착하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-290">Watch this queue to see more messages arrive.</span></span> <span data-ttu-id="b9fa6-291">데이터베이스를 보고 새 항목이 추가되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-291">You can also look at the database to verify that new entries have been added.</span></span> 

<span data-ttu-id="b9fa6-292">이 랩에서는 바인딩 지식을 출력 바인딩으로 확장하고 Azure Cosmos DB에 데이터를 작성했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-292">In this lab, we expanded your knowledge of bindings to output bindings, writing data to your Azure Cosmos DB.</span></span> <span data-ttu-id="b9fa6-293">더 나아가 Azure 큐에 메시지를 게시하는 또 다른 출력 바인딩을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-293">We went further and added another output binding to post messages to an Azure queue.</span></span> <span data-ttu-id="b9fa6-294">여기서는 들어오는 원본에서 데이터를 만들고 다양한 대상으로 이동하는 데 도움이 되는 바인딩의 진정한 능력을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-294">This demonstrates the true power of bindings to help you shape and move data from incoming sources to a variety of destinations.</span></span> <span data-ttu-id="b9fa6-295">데이터베이스 코드를 작성하지 않았거나 연결 문자열을 직접 관리해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-295">We haven't written any database code or had to manage connection strings ourselves.</span></span> <span data-ttu-id="b9fa6-296">대신 바인딩을 선언적으로 구성하고 플랫폼이 연결 보안, 함수 크기 조정 및 연결 크기 조정을 처리하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="b9fa6-296">Instead, we configured bindings declaratively and let the platform take care of securing connections, scaling our function, and scaling our connections.</span></span>