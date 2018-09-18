<span data-ttu-id="58cfb-101">마지막 연습에서는 Azure Cosmos DB 데이터베이스에서 책갈피를 조회하는 시나리오를 구현했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-101">In our last exercise, we implemented a scenario to look up bookmarks in an Azure Cosmos DB database.</span></span> <span data-ttu-id="58cfb-102">책갈피 컬렉션에서 데이터를 읽도록 입력 바인딩을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-102">We configured an input binding to read data from our bookmarks collection.</span></span> <span data-ttu-id="58cfb-103">그러나 데이터를 읽는 것만으로도 지루하므로 더 많은 작업을 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-103">But just reading data is boring, so let's do more.</span></span> <span data-ttu-id="58cfb-104">이제 쓰기를 포함하도록 시나리오를 확장해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-104">Let's expand the scenario to include writing.</span></span> <span data-ttu-id="58cfb-105">다음 순서도를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-105">Consider the following flowchart.</span></span>

![Cosmos DB 백 엔드에서 책갈피를 추가하는 프로세스를 보여 주는 흐름 다이어그램](../media-draft/add-bookmark-flow-small.png)

<span data-ttu-id="58cfb-107">이 시나리오에서는 책갈피를 목록에 추가하라는 요청을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-107">In this scenario, we'll receive requests to add bookmarks to our list.</span></span> <span data-ttu-id="58cfb-108">요청은 책갈피 URL과 함께 원하는 키 또는 ID를 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-108">The requests pass in the desired key, or ID, along with the bookmark URL.</span></span> <span data-ttu-id="58cfb-109">순서도에서 볼 수 있듯이 키가 이미 백 엔드에 있는 경우 오류로 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-109">As you can see in the flow chart, we'll respond with an error if the key already exists in our back-end.</span></span>

<span data-ttu-id="58cfb-110">전달된 키가 *없으면* 새 책갈피를 데이터베이스에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-110">If the key that was passed to us is *not* found, we'll add the new bookmark to our database.</span></span> <span data-ttu-id="58cfb-111">여기서 중지할 수 있지만 조금 더 수행해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-111">We could stop there, but let's do a little more.</span></span>

<span data-ttu-id="58cfb-112">순서도에서 또 다른 단계가 눈에 띄나요?</span><span class="sxs-lookup"><span data-stu-id="58cfb-112">Notice another step in the flowchart?</span></span> <span data-ttu-id="58cfb-113">지금까지 처리 측면에서 받는 데이터를 별로 다루지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-113">So far we haven't done much with the data that we receive in terms of processing.</span></span> <span data-ttu-id="58cfb-114">받는 데이터를 데이터베이스로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-114">We move what we receive into a database.</span></span> <span data-ttu-id="58cfb-115">그러나 실제 솔루션에서는 특정 방식으로 데이터를 처리할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-115">However, in a real solution, it is possible that we'd probably process the data in some fashion.</span></span> <span data-ttu-id="58cfb-116">동일한 함수에서 모두 처리하도록 결정할 수 있지만, 이 랩에서는 추가 처리를 다른 구성 요소 또는 비즈니스 논리 부분으로 오프로드하는 패턴을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-116">We can decide to do all processing in the same function, but in this lab we'll show a pattern that offloads further processing to another component or piece of business logic.</span></span>

<span data-ttu-id="58cfb-117">책갈피 시나리오에서 이러한 작업 오프로딩의 좋은 예는 무엇일까요?</span><span class="sxs-lookup"><span data-stu-id="58cfb-117">What might be a good example of this offloading of work in our bookmarks scenario?</span></span> <span data-ttu-id="58cfb-118">그렇다면, 새 책갈피를 QR 코드 생성 서비스로 보내면 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="58cfb-118">Well what if we send the new bookmark to a QR code generation service?</span></span> <span data-ttu-id="58cfb-119">이 경우 해당 서비스에서 URL에 대한 QR 코드를 생성하고, 이미지를 Blob 저장소에 저장한 다음, QR 이미지의 주소를 책갈피 컬렉션의 항목에 다시 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-119">That service would, in turn, generate a QR code for the URL, store the image in blob storage, and add the address of the qr image back into the entry in our bookmarks collection.</span></span> <span data-ttu-id="58cfb-120">QR 이미지를 생성하는 서비스를 호출하는 경우 시간이 많이 걸리므로 결과를 기다리는 대신 해당 결과를 함수에 전달하여 비동기적으로 처리하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-120">Calling a service to generate a qr image is time consuming so, rather than wait for the result, we hand it off to a function and let it take care of this asynchronously.</span></span>

<span data-ttu-id="58cfb-121">Azure Functions에서 다양한 통합 원본에 대한 입력 바인딩을 지원하는 것처럼 데이터 원본에 데이터를 쉽게 쓸 수 있도록 하는 일단의 출력 바인딩 템플릿도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-121">Just as Azure Functions supports input bindings for different integration sources, it also has a set of output bindings templates to make it easy for you to write data to data sources.</span></span> <span data-ttu-id="58cfb-122">출력 바인딩은 *function.json* 파일에도 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-122">Output bindings are also configured in the *function.json* file.</span></span>  <span data-ttu-id="58cfb-123">이 연습에서 살펴보겠지만 함수는 다중 데이터 원본 및 서비스를 사용하도록 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-123">As we'll see in this exercise, we can configure our function to work with multiple data sources and services.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="58cfb-124">이 연습은 마지막 단원의 연습을 기반으로 하고 있습니다. 즉, 동일한 Azure Cosmos DB 데이터베이스와 입력 바인딩을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-124">This exercise builds on the exercise in the last unit, namely, it uses the same Azure Cosmos DB database and input binding.</span></span> <span data-ttu-id="58cfb-125">해당 단원을 수행하지 않은 경우 이 랩으로 계속 진행하기 전에 그렇게 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-125">If you haven't worked through that unit, we recommend doing so before proceeding  with this lab.</span></span>

## <a name="create-an-httptriggered-function"></a><span data-ttu-id="58cfb-126">HTTP_triggered 함수 만들기</span><span class="sxs-lookup"><span data-stu-id="58cfb-126">Create an HTTP_triggered Function</span></span>

1. <span data-ttu-id="58cfb-127">이 모듈에서 사용한 것과 동일한 Azure 계정을 사용하여 [https://portal.azure.com](https://portal.azure.com?azure-portal=true)의 Azure Portal에 로그인했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-127">Make sure you are signed in to the Azure portal at [https://portal.azure.com](https://portal.azure.com?azure-portal=true) with the same Azure account you've used throughout this module.</span></span>

2. <span data-ttu-id="58cfb-128">Azure Portal에서 이 모듈에서 만든 함수 앱으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-128">In the Azure portal, navigate to the function app you created in this module.</span></span>

3. <span data-ttu-id="58cfb-129">함수 앱을 펼친 다음, 함수 컬렉션 위를 마우스로 가리키고, **함수** 옆에 있는 추가(**+**) 단추를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-129">Expand your function app, then hover over the functions collection and select the Add (**+**) button next to **Functions**.</span></span> <span data-ttu-id="58cfb-130">이 작업은 함수 만들기 프로세스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-130">This action starts the function creation process.</span></span> <span data-ttu-id="58cfb-131">다음 애니메이션에서는 이 작업을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-131">The following animation illustrates this action.</span></span>

![사용자가 함수 메뉴 항목을 마우스로 가리키면 표시되는 더하기 기호의 애니메이션](../media-draft/func-app-plus-hover-small.gif)

4. <span data-ttu-id="58cfb-133">이 페이지에는 지원되는 트리거의 현재 집합을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-133">The page shows us the current set of supported triggers.</span></span> <span data-ttu-id="58cfb-134">다음 스크린샷의 첫 번째 항목인 **HTTP 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-134">Select **HTTP trigger**, which is the first entry in the following screenshot.</span></span>

![이미지의 왼쪽 위에 HTTP 트리거가 먼저 표시된 트리거 템플릿 선택 UI 일부의 스크린샷](../media-draft/trigger-templates-small.PNG)

5. <span data-ttu-id="58cfb-136">다음 값을 사용하여 오른쪽에 나타나는 **새 함수** 대화 상자를 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-136">Fill out the **New Function** dialog that appears to the right  using the following values.</span></span>

|<span data-ttu-id="58cfb-137">필드</span><span class="sxs-lookup"><span data-stu-id="58cfb-137">Field</span></span>  |<span data-ttu-id="58cfb-138">값</span><span class="sxs-lookup"><span data-stu-id="58cfb-138">Value</span></span>  |
|---------|---------|
|<span data-ttu-id="58cfb-139">언어</span><span class="sxs-lookup"><span data-stu-id="58cfb-139">Language</span></span>     | <span data-ttu-id="58cfb-140">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="58cfb-140">**JavaScript**</span></span>        |
|<span data-ttu-id="58cfb-141">이름</span><span class="sxs-lookup"><span data-stu-id="58cfb-141">Name</span></span>     |   [!INCLUDE [func-name-add](./func-name-add.md)]     |
| <span data-ttu-id="58cfb-142">권한 부여 수준</span><span class="sxs-lookup"><span data-stu-id="58cfb-142">Authorization level</span></span> | <span data-ttu-id="58cfb-143">**함수**</span><span class="sxs-lookup"><span data-stu-id="58cfb-143">**Function**</span></span> |

5. <span data-ttu-id="58cfb-144">**만들기**를 선택하여 코드 편집기에서 index.js 파일을 열고 HTTP 트리거 함수의 기본 구현을 표시하는 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-144">Select **Create** to create our function, which opens the index.js file in the code editor and displays a default implementation of the HTTP-triggered function.</span></span>

<span data-ttu-id="58cfb-145">이 연습에서는 이전 단원의 *코드*와 *구성*을 시작 지점으로 사용하여 작업 속도를 높입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-145">In this exercise, we'll speed up things by using the *code* and *configuration* from the previous unit as a starting point.</span></span>

6. <span data-ttu-id="58cfb-146">index.js의 모든 코드를 다음 코드 조각의 코드로 바꾸고, **저장**을 클릭하여 이 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-146">Replace all code in index.js with the code from the following snippet and click **Save** to save this change.</span></span> 

[!code-javascript[](../code/find-bookmark-single.js)]

<span data-ttu-id="58cfb-147">이 코드가 익숙해 보이는 경우 이는 [!INCLUDE [func-name-find](./func-name-find.md)] 함수를 구현했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-147">If this code looks familiar, that's because it's the implementation of our [!INCLUDE [func-name-find](./func-name-find.md)] function.</span></span> <span data-ttu-id="58cfb-148">예상한 대로 함수는 동일한 바인딩을 정의할 때까지 작동하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-148">As you would expect, the function won't work until we define the same bindings.</span></span>  

7. <span data-ttu-id="58cfb-149">[!INCLUDE [func-name-find](./func-name-find.md)] 함수에서 *function.json* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-149">Open the *function.json* file from the [!INCLUDE [func-name-find](./func-name-find.md)] function.</span></span> <span data-ttu-id="58cfb-150">코드 편집기의 오른쪽에 있는 **파일 보기** 메뉴를 열어서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-150">You'll find it by opening the **View files** menu to the right of the code editor.</span></span>

8. <span data-ttu-id="58cfb-151">이 파일의 전체 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-151">Copy the entire contents of this file.</span></span>

9. <span data-ttu-id="58cfb-152">[!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 *function.json* 파일을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-152">Open the *function.json* file from the [!INCLUDE [func-name-add](./func-name-add.md)] function.</span></span>

10. <span data-ttu-id="58cfb-153">이 파일의 내용을 [!INCLUDE [func-name-find](./func-name-find.md)] 함수와 연결된 *function.json* 파일에서 복사한 내용으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-153">Replace the contents of this file with the content you copied from the *function.json* file associated with the [!INCLUDE [func-name-find](./func-name-find.md)] function.</span></span> <span data-ttu-id="58cfb-154">완료되면 function.json에 다음 JSON이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-154">When you're done, your function.json should contain the following JSON.</span></span>

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

11. <span data-ttu-id="58cfb-155">모든 변경 내용을 **저장**해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-155">Make sure to **Save** all changes.</span></span>

<span data-ttu-id="58cfb-156">이전 단계에서는 다른 함수에서 바인딩 정의를 복사하여 새 함수에 대한 바인딩을 구성했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-156">In the preceding steps, we configured bindings for our new function by copying binding definitions from another.</span></span> <span data-ttu-id="58cfb-157">물론 UI를 통해 새 바인딩을 만들 수도 있지만, 이 대안을 사용할 수 있다는 것을 이해하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-157">We could, of course, created a new binding through the UI, but it is good to understand that this alternative is available to you.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="58cfb-158">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="58cfb-158">Try it out</span></span>

1. <span data-ttu-id="58cfb-159">평소와 같이 오른쪽 맨 위에서 **</> 함수 URL 가져오기**를 클릭하고, **기본값(함수 키)** 을 선택한 다음, **복사**를 클릭하여 함수의 URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-159">As usual, click **</> Get function URL** at the top right, select **default (Function key)**, and then click **Copy** to copy the function's URL.</span></span>

2. <span data-ttu-id="58cfb-160">복사한 함수 URL을 브라우저의 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-160">Paste the function URL you copied into your browser's address bar.</span></span> <span data-ttu-id="58cfb-161">이 URL의 끝에 `&id=docs` 쿼리 문자열 값을 추가하고, 키보드에서 `Enter` 키를 눌러 요청을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-161">Add the query string value `&id=docs` to the end of this URL and press the `Enter` key on your keyboard to execute the request.</span></span> <span data-ttu-id="58cfb-162">모든 작업이 잘 진행되면 해당 리소스에 대한 URL이 포함된 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-162">All going well, you should see a response that includes a URL to that resource.</span></span>

<span data-ttu-id="58cfb-163">그러면 지금은 어디에 있을까요?</span><span class="sxs-lookup"><span data-stu-id="58cfb-163">So, where are we at?</span></span> <span data-ttu-id="58cfb-164">글쎄, 지금까지 이전 랩에서 수행했던 것을 그대로 복제했을 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-164">Well, so far we've really just replicated what we did in the previous lab.</span></span> <span data-ttu-id="58cfb-165">하지만 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-165">But that's ok.</span></span> <span data-ttu-id="58cfb-166">이 작업의 시작 지점으로 사용하기 위해 마지막 랩에서 수행한 것을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-166">We're copying what we did in the last lab to serve as a starting point for this one.</span></span> <span data-ttu-id="58cfb-167">그 다음에 새로운 것들, 즉 데이터베이스에 쓰기 작업을 수행할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-167">We'll work on the new stuff next, namely, writing to our database.</span></span> <span data-ttu-id="58cfb-168">이를 위해 *출력 바인딩*이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-168">For that, we'll need an *output binding*.</span></span>

## <a name="define-azure-cosmos-db-output-binding"></a><span data-ttu-id="58cfb-169">Azure Cosmos DB 출력 바인딩 정의</span><span class="sxs-lookup"><span data-stu-id="58cfb-169">Define Azure Cosmos DB output binding</span></span>

<span data-ttu-id="58cfb-170">사용자 인터페이스를 통해 새 출력 바인딩을 정의하는 대신, *function.json* 구성 파일을 직접 업데이트하여 이 바인딩을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-170">Rather than define a new output binding by going through the user interface, we'll create this binding by updating the configuration file, *function.json*, by hand.</span></span> 

1. <span data-ttu-id="58cfb-171">이 함수에 대한 **function.json** 파일을 **파일 보기** 목록에서 선택하여 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-171">Open the **function.json** file for this function in the editor by selecting it in the **View files** list.</span></span>

2. <span data-ttu-id="58cfb-172">해당 파일에서 이름이 `bookmark`인 바인딩을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-172">Copy the binding with the name `bookmark` in that file.</span></span>

3. <span data-ttu-id="58cfb-173">닫는 중괄호 바로 뒤 및 닫는 대괄호 바로 앞에 커서를 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-173">Place your cursor directly after the closing curly bracket, right before the closing square bracket.</span></span> <span data-ttu-id="58cfb-174">쉼표(`,`)를 추가한 다음, 여기에 바인딩의 복사본을 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-174">Add a comma `,` and then paste the copy of the binding here.</span></span> <span data-ttu-id="58cfb-175">*function.json* 설정은 이제 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-175">Your *function.json* config should now look like the following.</span></span>

[!code-json[](../code/config-new-entry.json?highlight=22-31)]

4. <span data-ttu-id="58cfb-176">다음과 같은 변경 내용을 사용하여 붙여넣은 바인딩을 편집합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-176">Edit the binding we pasted, with the following changes.</span></span>


|<span data-ttu-id="58cfb-177">속성</span><span class="sxs-lookup"><span data-stu-id="58cfb-177">Property</span></span>   |<span data-ttu-id="58cfb-178">이전 값</span><span class="sxs-lookup"><span data-stu-id="58cfb-178">Old value</span></span>  |<span data-ttu-id="58cfb-179">새 값</span><span class="sxs-lookup"><span data-stu-id="58cfb-179">New value</span></span>  |
|---------|---------|---------|
|<span data-ttu-id="58cfb-180">name</span><span class="sxs-lookup"><span data-stu-id="58cfb-180">name</span></span>     |   <span data-ttu-id="58cfb-181">bookmark</span><span class="sxs-lookup"><span data-stu-id="58cfb-181">bookmark</span></span>      |  <span data-ttu-id="58cfb-182">**newbookmark**</span><span class="sxs-lookup"><span data-stu-id="58cfb-182">**newbookmark**</span></span>       |
|<span data-ttu-id="58cfb-183">direction</span><span class="sxs-lookup"><span data-stu-id="58cfb-183">direction</span></span>     |   <span data-ttu-id="58cfb-184">in</span><span class="sxs-lookup"><span data-stu-id="58cfb-184">in</span></span>      |   <span data-ttu-id="58cfb-185">**out**</span><span class="sxs-lookup"><span data-stu-id="58cfb-185">**out**</span></span>      |
|<span data-ttu-id="58cfb-186">id</span><span class="sxs-lookup"><span data-stu-id="58cfb-186">id</span></span>     |      <span data-ttu-id="58cfb-187">{id}</span><span class="sxs-lookup"><span data-stu-id="58cfb-187">{id}</span></span>   |   <span data-ttu-id="58cfb-188">**이 속성은 삭제합니다. 출력 바인딩에는 존재하지 않기 때문입니다.**</span><span class="sxs-lookup"><span data-stu-id="58cfb-188">**delete this property. It does not exist for the output binding.**</span></span>      |

<span data-ttu-id="58cfb-189">이렇게 변경하면 다음 JSON과 같은 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-189">When you make these changes, you end up with a file that looks like the following JSON.</span></span>

[!code-json[](../code/config-q-complete.json?highlight=22-30)]

<span data-ttu-id="58cfb-190">이는 구성 파일에서 직접 바인딩을 만드는 방법을 보여 주는 데모일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-190">That was just a demo of how you can also create bindings directly in the configuration file.</span></span> <span data-ttu-id="58cfb-191">이 예에서는 Cosmos DB 입력 바인딩에 대해 이미 구성한 다른 바인딩의 속성 즉, `databaseName`, `collectionName` 및 `connection`을 다시 사용하므로 의미가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-191">In this example, it makes sense because we are reusing the properties from another binding, namely, the `databaseName`, `collectionName` and `connection` that we already configured for our Cosmos DB input binding.</span></span>

> [!NOTE]
> <span data-ttu-id="58cfb-192">앞의 JSON 파일에서 `connection`의 실제 값은 연결을 만들 때 지정한 연결 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-192">The actual value of `connection` in the preceding JSON file will be whatever name your connection was given when it was created.</span></span>

<span data-ttu-id="58cfb-193">코드를 업데이트하기 전에 큐에 메시지를 게시할 수 있게 하는 바인딩을 하나 더 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-193">Before we update our code, let's add one more binding that will enable us to post messages to a queue.</span></span>

## <a name="define-azure-queue-storage-output-binding"></a><span data-ttu-id="58cfb-194">Azure Queue Storage 출력 바인딩 정의</span><span class="sxs-lookup"><span data-stu-id="58cfb-194">Define Azure Queue Storage output binding</span></span>

<span data-ttu-id="58cfb-195">Azure Queue Storage는 전 세계 어디서나 액세스할 수 있는 메시지를 저장하는 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-195">Azure Queue storage is a service for storing messages that can be accessed from anywhere in the world.</span></span> <span data-ttu-id="58cfb-196">단일 메시지는 최대 64KB까지 가능하며, 큐에는 정의된 저장소 계정의 총 용량 한도까지 수백만 개의 메시지가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-196">A single message can be up to 64 KB and a queue can contain millions of messages up to the total capacity limit of the storage account in which it is defined.</span></span> <span data-ttu-id="58cfb-197">다음 다이어그램에서는 이 시나리오에서 큐를 사용하는 방법을 개략적으로 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-197">The following diagram shows at a high level how a queue will be used in our scenario.</span></span>

![저장소 큐 및 큐에 메시지를 푸시하고 팝하는 두 함수의 개념을 보여 주는 다이어그램](../media-draft/q-logical-small.png)

<span data-ttu-id="58cfb-199">이제 새 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에서 메시지를 큐에 추가하는 것을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-199">Here we can see that our new function, [!INCLUDE [func-name-add](./func-name-add.md)], adds messages to a queue.</span></span> <span data-ttu-id="58cfb-200">다른 함수, 예를 들어 *gen-qr-code*와 같은 가상의 함수는 동일한 큐에서 메시지를 팝하고 요청을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-200">Another function, for example a fictitious function called *gen-qr-code*, will pop messages from the same queue and process the request.</span></span>  <span data-ttu-id="58cfb-201">[!INCLUDE [func-name-add](./func-name-add.md)]에서 큐에 메시지를 쓰거나 *푸시*하므로 솔루션에 새 출력 바인딩을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-201">Since we write, or *push*, messages to the queue from [!INCLUDE [func-name-add](./func-name-add.md)], we'll add a new  output binding to our solution.</span></span> <span data-ttu-id="58cfb-202">이번에는 UI를 통해 바인딩을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-202">Let's create the binding through the UI this time.</span></span>

1. <span data-ttu-id="58cfb-203">왼쪽의 함수 메뉴에서 **통합**을 선택하여 [통합] 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-203">Select **Integrate** in the function menu on the left to open the integration tab.</span></span>

2. <span data-ttu-id="58cfb-204">**출력** 열 아래에서 **+ 새 출력**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-204">Select **+ New Output** under the **Outputs** column.</span></span> <span data-ttu-id="58cfb-205">가능한 모든 출력 바인딩 형식 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-205">A list of all possible output binding types is displayed.</span></span>

3. <span data-ttu-id="58cfb-206">목록에서 **Azure Queue Storage**를 클릭한 다음, **선택** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-206">Click on **Azure Queue Storage** from the list and then the **Select** button.</span></span> <span data-ttu-id="58cfb-207">그러면 Azure Queue Storage 출력 구성 페이지가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-207">This action opens the Azure Queue Storage output configuration page.</span></span>

<span data-ttu-id="58cfb-208">다음으로, 저장소 계정 연결을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-208">Next, we'll set up a storage account connection.</span></span> <span data-ttu-id="58cfb-209">여기서 큐가 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-209">This is where our queue will be hosted.</span></span>

4. <span data-ttu-id="58cfb-210">이 페이지의 **저장소 계정 연결** 필드에서 빈 필드 오른쪽의 *새로 만들기*를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-210">In the field named **Storage account connection** on this page, click on *new* to the right of the empty field.</span></span> <span data-ttu-id="58cfb-211">그러면 **저장소 계정** 선택 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-211">This action opens the **Storage Account** selection dialog.</span></span> 

5. <span data-ttu-id="58cfb-212">이 모듈을 시작하고 함수 앱을 만들었을 때 저장소 계정도 만들어졌습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-212">When we started this module and created our function app, a storage account was also created at that time.</span></span> <span data-ttu-id="58cfb-213">이 대화 상자에는 해당 저장소 계정이 표시되므로 계속 진행하여 이를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-213">It will be listed in this dialog, so go ahead and select it.</span></span> <span data-ttu-id="58cfb-214">**저장소 계정 연결** 필드가 연결 이름으로 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-214">The **Storage account connection** field is populated with the name of a connection.</span></span> <span data-ttu-id="58cfb-215">연결 문자열 값을 보려면 **값 표시**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-215">If you want to see the connection string value, click on **show value**.</span></span>

6. <span data-ttu-id="58cfb-216">이 페이지의 다른 모든 필드는 기본값으로 그대로 둘 수 있지만 다음 항목을 변경하여 속성에 더 많은 의미를 부여할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-216">Although we could leave all other fields on this page with their default values, let's change the following to lend more meaning to the properties.</span></span>


|<span data-ttu-id="58cfb-217">속성</span><span class="sxs-lookup"><span data-stu-id="58cfb-217">Property</span></span>  |<span data-ttu-id="58cfb-218">이전 값</span><span class="sxs-lookup"><span data-stu-id="58cfb-218">Old value</span></span>  |<span data-ttu-id="58cfb-219">새 값</span><span class="sxs-lookup"><span data-stu-id="58cfb-219">New value</span></span>  | <span data-ttu-id="58cfb-220">설명</span><span class="sxs-lookup"><span data-stu-id="58cfb-220">Description</span></span> |
|---------|---------|---------|---------|
|<span data-ttu-id="58cfb-221">큐 이름</span><span class="sxs-lookup"><span data-stu-id="58cfb-221">Queue name</span></span>     |    <span data-ttu-id="58cfb-222">outqueue</span><span class="sxs-lookup"><span data-stu-id="58cfb-222">outqueue</span></span>     |  <span data-ttu-id="58cfb-223">**bookmarks-post-process**</span><span class="sxs-lookup"><span data-stu-id="58cfb-223">**bookmarks-post-process**</span></span>      | <span data-ttu-id="58cfb-224">책갈피를 배치하는 데 사용하는 큐의 이름으로, 다른 함수에서 추가로 처리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-224">This is the name of the queue we are using to place bookmarks into so that they can be processed further by another function.</span></span> |
| <span data-ttu-id="58cfb-225">메시지 매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="58cfb-225">Message parameter name</span></span>    |  <span data-ttu-id="58cfb-226">outputQueueItem</span><span class="sxs-lookup"><span data-stu-id="58cfb-226">outputQueueItem</span></span>       |   <span data-ttu-id="58cfb-227">**newmessage**</span><span class="sxs-lookup"><span data-stu-id="58cfb-227">**newmessage**</span></span>      | <span data-ttu-id="58cfb-228">코드에서 사용할 바인딩 속성입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-228">This is the binding property we'll use in code.</span></span> |


7. <span data-ttu-id="58cfb-229">**저장**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-229">Remember to click **Save** to save your changes.</span></span>

## <a name="update-function-implementation"></a><span data-ttu-id="58cfb-230">업데이트 함수 구현</span><span class="sxs-lookup"><span data-stu-id="58cfb-230">Update function implementation</span></span>

<span data-ttu-id="58cfb-231">이제 [!INCLUDE [func-name-add](./func-name-add.md)] 함수에 대한 모든 바인딩이 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-231">We now have all our bindings set up for the [!INCLUDE [func-name-add](./func-name-add.md)] function.</span></span> <span data-ttu-id="58cfb-232">함수에서 이러한 바인딩을 사용할 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-232">It's time to use them in our function.</span></span>

1.  <span data-ttu-id="58cfb-233">[!INCLUDE [func-name-add](./func-name-add.md)] 함수를 클릭하여 코드 편집기에서 *index.js*를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-233">Click on our function, [!INCLUDE [func-name-add](./func-name-add.md)], to open up *index.js* in the code editor.</span></span>

2. <span data-ttu-id="58cfb-234">index.js의 모든 코드를 다음 코드 조각의 코드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-234">Replace all code in index.js with the code from the following snippet.</span></span>

[!code-javascript[](../code/add-bookmark.js)]

<span data-ttu-id="58cfb-235">이 코드의 기능을 분석해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-235">Let's breakdown what this code does.</span></span>

* <span data-ttu-id="58cfb-236">이 함수는 데이터를 변경하므로 HTTP 요청이 POST이고 책갈피 데이터가 요청 본문에 포함될 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-236">Since this function changes our data, we expect the HTTP request to be a POST and the bookmark data to be part of the request body.</span></span>
* <span data-ttu-id="58cfb-237">Cosmos DB 입력 바인딩은 받은 `id`를 사용하여 문서 또는 책갈피를 검색하려고 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-237">Our Cosmos DB input binding attempts to retrieve a document, or bookmark, using the `id` that we receive.</span></span> <span data-ttu-id="58cfb-238">항목을 찾으면 `bookmark` 개체가 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-238">If it finds an entry, the `bookmark` object will be set.</span></span> <span data-ttu-id="58cfb-239">`if(bookmark)` 조건으로 항목이 있는지 여부를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-239">The `if(bookmark)` condition checks whether an entry was found.</span></span>
* <span data-ttu-id="58cfb-240">데이터베이스에 추가하는 것은 `context.bindings.newbookmark` 바인딩 매개 변수를 JSON 문자열로 만든 새 책갈피 항목으로 설정하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-240">Adding to the database is a simple as setting the `context.bindings.newbookmark` binding parameter to the new bookmark entry, which we have created as a JSON string.</span></span>
* <span data-ttu-id="58cfb-241">메시지를 큐에 게시하는 것은 `context.bindings.newmessage parameter`를 설정하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-241">Posting a message to our queue is as simple as setting the  `context.bindings.newmessage parameter`.</span></span>

> [!NOTE]
> <span data-ttu-id="58cfb-242">수행한 유일한 작업은 큐 바인딩을 만드는 것이었습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-242">The only task we performed was to create a queue binding.</span></span> <span data-ttu-id="58cfb-243">여기서 큐는 명시적으로 만들지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-243">We never created the queue explicitly.</span></span> <span data-ttu-id="58cfb-244">지금 바인딩의 능력을 목격하고 있습니다!</span><span class="sxs-lookup"><span data-stu-id="58cfb-244">You are witnessing the power of bindings!</span></span> <span data-ttu-id="58cfb-245">다음 설명선에서 볼 수 있듯이 큐가 없으면 자동으로 만들어집니다!</span><span class="sxs-lookup"><span data-stu-id="58cfb-245">As the following callout says, the queue is automatically created for you if it doesn't exist!</span></span>

![큐를 자동으로 만들도록 호출하는 스크린샷](../media-draft/q-auto-create-small.png)

<span data-ttu-id="58cfb-247">이제 끝났습니다. 다음 섹션에서 진행 중인 작업을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-247">So, that's it - let's see our work in action in the next section.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="58cfb-248">사용해 보기</span><span class="sxs-lookup"><span data-stu-id="58cfb-248">Try it out</span></span>

<span data-ttu-id="58cfb-249">이제 여러 개의 출력 바인딩이 있으므로 테스트가 좀 더 까다로워졌습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-249">Now that we have multiple output bindings, our testing becomes a little trickier.</span></span> <span data-ttu-id="58cfb-250">이전 랩에서는 HTTP 요청과 쿼리 문자열을 보내 테스트하는 데 만족했지만 이번에는 HTTP 게시를 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-250">Whereas in previous labs we were content to test by sending an HTTP request and a query string, we'll want to perform an HTTP Post this time.</span></span> <span data-ttu-id="58cfb-251">또한 메시지에서 이 게시를 큐에 넣는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-251">We also need to check whether messages are making it into a queue.</span></span>

1.  <span data-ttu-id="58cfb-252">함수 앱 포털에서 [!INCLUDE [func-name-add](./func-name-add.md)] 함수를 선택한 경우 왼쪽 끝에 있는 [테스트] 메뉴 항목을 클릭하여 확장합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-252">With our function, [!INCLUDE [func-name-add](./func-name-add.md)], selected in the Function Apps portal, click on the Test menu item on the far left to expand it.</span></span>

2. <span data-ttu-id="58cfb-253">**테스트** 메뉴 항목을 선택하고, 테스트 패널이 열려 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-253">Select the **Test** menu item and verify that you have the test panel open.</span></span> <span data-ttu-id="58cfb-254">다음 스크린샷에서는 열려 있는 테스트 패널을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-254">The following screenshot shows what it should look like.</span></span> 

![테스트 패널이 확장된 함수를 보여 주는 스크린샷](../media-draft/test-panel-open-small.png)

> [!IMPORTANT]
> <span data-ttu-id="58cfb-256">HTTP 메서드 드롭다운에서 **POST**가 선택되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-256">Make sure **POST** is selected in the HTTP method dropdown.</span></span>

3. <span data-ttu-id="58cfb-257">요청 본문의 내용을 다음 JSON 페이로드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-257">Replace the content of the request body with the following JSON payload.</span></span>

```json
  {
      "id": "docs",
      "url": "https://docs.microsoft.com/azure"
  }
  ```

4. <span data-ttu-id="58cfb-258">테스트 패널의 아래쪽에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-258">Click **Run** at the bottom of the test panel.</span></span> 

5. <span data-ttu-id="58cfb-259">다음 다이어그램과 같이 *출력* 창에 "책갈피가 이미 있습니다."라는</span><span class="sxs-lookup"><span data-stu-id="58cfb-259">Verify that the *Output* window displays the "Bookmark already exists."</span></span> <span data-ttu-id="58cfb-260">메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-260">message as shown in the following diagram.</span></span> 

![테스트 패널 및 실패한 테스트의 결과를 보여 주는 스크린샷](../media-draft/test-exists-small.png)

6. <span data-ttu-id="58cfb-262">이제 요청 본문을 다음 페이로드로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-262">Now replace the Request body with the following payload.</span></span> 

```json
  {
      "id": "github",
      "URL": "https://www.github.com"
  }
  ```
7. <span data-ttu-id="58cfb-263">테스트 패널의 아래쪽에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-263">Click **Run** at the bottom of the test panel.</span></span>

8. <span data-ttu-id="58cfb-264">다음 다이어그램과 같이 *출력* 상자에 "책갈피 추가됨"이라는 메시지가 표시되는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-264">Verify the that *Output* box displays the "bookmark added" message as shown in the following diagram.</span></span>

![테스트 패널 및 성공한 테스트의 결과를 보여 주는 스크린샷](../media-draft/test-success-small.png)

<span data-ttu-id="58cfb-266">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="58cfb-266">Congratulations!</span></span> <span data-ttu-id="58cfb-267">[!INCLUDE [func-name-add](./func-name-add.md)]는 설계한 대로 작동하지만 코드에 있던 큐 작업은 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="58cfb-267">The [!INCLUDE [func-name-add](./func-name-add.md)] works as designed, but what about that queue operation we had in the code?</span></span> <span data-ttu-id="58cfb-268">그럼, 큐에 어떤 것이 쓰여 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-268">Well, let's go see if something was written to a queue.</span></span>

### <a name="verify-that-a-message-is-written-to-our-queue"></a><span data-ttu-id="58cfb-269">메시지가 큐에 쓰여 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-269">Verify that a message is written to our queue</span></span>

<span data-ttu-id="58cfb-270">Azure Queue Storage 큐는 저장소 계정에서 호스팅됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-270">Azure Queue Storage queues are hosted in a storage account.</span></span> <span data-ttu-id="58cfb-271">이 연습에서는 출력 바인딩을 만들 때 이미 저장소 계정을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-271">You selected the storage account in this exercise  already when creating the output binding.</span></span> 

1. <span data-ttu-id="58cfb-272">Azure Portal의 기본 검색 상자에서 *저장소 계정*을 입력하고, 검색 결과의 *서비스* 범주 아래에서 **저장소 계정**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-272">In the main search box in the Azure portal, type *storage accounts* and in the search results select **Storage accounts** under the *Services* category.</span></span> <span data-ttu-id="58cfb-273">이는 다음 스크린샷에 설명되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-273">This is illustrated in the following screenshot.</span></span> 

![기본 검색 상자에서 저장소 계정에 대한 검색 결과를 보여 주는 스크린샷](../media-draft/search-for-sa-small.png)

2. <span data-ttu-id="58cfb-275">반환된 저장소 계정 목록에서 **newmessage** 출력 바인딩을 만드는 데 사용한 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-275">In the list of storage accounts that are returned, select the storage account you used to create the **newmessage** output binding.</span></span> <span data-ttu-id="58cfb-276">저장소 계정 설정이 포털의 주 창에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-276">The storage account settings are displayed in the main window the portal.</span></span>

3. <span data-ttu-id="58cfb-277">[서비스] 목록에서 **큐** 항목을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-277">Select the **Queues** item from the Services list.</span></span> <span data-ttu-id="58cfb-278">그러면 이 저장소 계정에서 호스팅하는 큐의 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-278">This displays a list of queues hosted by this storage account.</span></span> <span data-ttu-id="58cfb-279">다음 스크린샷과 같이 **bookmarks-post-process** 큐가 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-279">Verify that the **bookmarks-post-process** queue exists, as shown in the following screenshot.</span></span>

![이 저장소 계정에서 호스팅하는 큐 목록에서 큐를 보여 주는 스크린샷](../media-draft/q-in-list-small.png)

4. <span data-ttu-id="58cfb-281">**bookmarks-post-process**를 클릭하여 해당 큐를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-281">Click on **bookmarks-post-process** to open the queue.</span></span> <span data-ttu-id="58cfb-282">큐에 있는 메시지가 목록에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-282">The messages that are in the queue are displayed in a list.</span></span> <span data-ttu-id="58cfb-283">모두 계획에 따라 진행되었다면 데이터베이스에 책갈피를 추가할 때 게시한 메시지가 큐에 있어야 하며 다음 항목처럼 보입니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-283">If all went according to plan, the message we posted when we added a bookmark to our database should be in the queue and will look like the following entry.</span></span> 

![큐의 메시지를 보여 주는 스크린샷](../media-draft/message-in-q-small.png)

<span data-ttu-id="58cfb-285">이 예에서는 메시지에 고유한 ID가 지정되어 있고 **메시지 텍스트** 필드에 책갈피가 JSON 문자열 형식으로 표시된다는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-285">In this example, you can see that the message was given a unique ID and the **MESSAGE TEXT** field displays our bookmark in JSON string format.</span></span>

5. <span data-ttu-id="58cfb-286">테스트 패널에서 요청 본문을 새 ID/URL 집합으로 변경하고 함수를 실행하여 함수를 추가로 테스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-286">You can test the function further by changing the request body in the Test panel with new id/url sets and running the function.</span></span> <span data-ttu-id="58cfb-287">이 큐를 조사하여 더 많은 메시지가 도착하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-287">Watch this queue to see more messages arrive.</span></span> <span data-ttu-id="58cfb-288">또한 데이터베이스를 보고 새 항목이 추가되었는지 확인할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-288">You can also look at the database to verify new entries have been added.</span></span> 

<span data-ttu-id="58cfb-289">이 랩에서는 바인딩 지식을 출력 바인딩으로 확대하고 Azure Cosmos DB에 데이터를 기록했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-289">In this lab, we expanded our knowledge of bindings to output bindings, writing data to our Azure Cosmos DB.</span></span> <span data-ttu-id="58cfb-290">더 나아가 Azure 큐에 메시지를 게시하는 또 다른 출력 바인딩을 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-290">We went further and added another output binding to post messages to an Azure queue.</span></span> <span data-ttu-id="58cfb-291">여기서는 들어오는 원본에서 데이터를 만들고 다양한 대상으로 이동하는 데 도움이 되는 바인딩의 진정한 능력을 보여 주었습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-291">This demonstrates the true power of bindings to help you shape and move data from incoming sources to a variety of destinations.</span></span> <span data-ttu-id="58cfb-292">데이터베이스 코드를 작성하지 않았거나 연결 문자열을 직접 관리해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-292">We haven't written any database code or had to manage connection strings ourselves.</span></span> <span data-ttu-id="58cfb-293">그 대신에 바인딩을 선언적으로 구성하고 플랫폼이 연결 보안, 함수 크기 조정 및 연결 크기 조정을 처리하도록 했습니다.</span><span class="sxs-lookup"><span data-stu-id="58cfb-293">Instead, we configured bindings declaratively and let the platform take care of securing connections, scaling our function and scaling our connections.</span></span>