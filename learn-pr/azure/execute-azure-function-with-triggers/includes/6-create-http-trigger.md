<span data-ttu-id="a894e-101">이 연습에서는 단일 문자열이 포함된 HTTP 요청을 허용하는 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-101">In this exercise, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="a894e-102">함수는 성공 또는 실패를 표시하는 문자열을 호출자에게 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-102">The function returns a string back to the caller to represent success or failure.</span></span>

> [!NOTE]
> <span data-ttu-id="a894e-103">이 연습을 완료하려면 유효한 계정으로 [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="a894e-103">To complete this exercise, make sure you're signed into the [Azure portal](https://portal.azure.com?azure-portal=true) with a valid account.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="a894e-104">HTTP 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="a894e-104">Create an HTTP trigger</span></span>

<span data-ttu-id="a894e-105">기존 Azure Functions 응용 프로그램을 계속 사용하고 HTTP 트리거를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="a894e-106">**함수**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-106">Point to **Functions** and select the plus (+) icon.</span></span>

    ![함수를 가리키고 더하기를 마우스로 가리켜 선택](../media-drafts/4-hover-function.png)

2. <span data-ttu-id="a894e-108">**HTTP 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-108">Select **HTTP trigger**.</span></span>

3. <span data-ttu-id="a894e-109">언어로 **C#** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-109">Select **C#** as the language.</span></span> 

4. <span data-ttu-id="a894e-110">**이름**은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-110">Leave the **Name** set to the default value.</span></span>

5. <span data-ttu-id="a894e-111">**권한 수준**을 **익명**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-111">Set the **Authorization level** to **Anonymous**.</span></span>

6. <span data-ttu-id="a894e-112">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-112">Select **Create**.</span></span>

7. <span data-ttu-id="a894e-113">자동 생성 코드를 빠르게 검토하여 상황을 파악할 아이디어를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-113">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="a894e-114">*req* 매개 변수는 들어오는 요청을 나타내며 *name* 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-114">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="a894e-115">*name*에 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-115">We check to see if *name* has a value.</span></span> <span data-ttu-id="a894e-116">값이 있는 경우 인사말을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-116">If it does, we return a greeting.</span></span> <span data-ttu-id="a894e-117">값이 없다면 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-117">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="a894e-118">함수 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="a894e-118">Get your function URL</span></span>

<span data-ttu-id="a894e-119">HTTP 트리거를 만들었으므로 이제 요청 수행을 시작할 수 있도록 함수 URL을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-119">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="a894e-120">HTTP 트리거를 선택하여 코드 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-120">Select your HTTP trigger to open the code screen.</span></span>

2. <span data-ttu-id="a894e-121">**실행**의 오른쪽에서 **함수 URL 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-121">To the right of **Run**, select **Get function URL**.</span></span>

3. <span data-ttu-id="a894e-122">**복사**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-122">Select **Copy**.</span></span>

4. <span data-ttu-id="a894e-123">**실행**을 선택하여 함수를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-123">Select **Run** to start your function.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="a894e-124">HTTP 트리거에 대한 GET 요청 실행</span><span class="sxs-lookup"><span data-stu-id="a894e-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="a894e-125">이제 함수 URL을 클립보드에 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="a894e-126">응답을 받는지 확인하기 위해 GET 요청을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="a894e-127">웹 브라우저에서 새 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-127">Open a new tab in your web browser.</span></span>

2. <span data-ttu-id="a894e-128">URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-128">Paste the URL into the address bar.</span></span>

3. <span data-ttu-id="a894e-129">이름을 사용하여 *name*이라는 쿼리 문자열 매개 변수를 다음과 같이 추가합니다. `.../api/HttpTriggerCSharp1?name=Jesse`</span><span class="sxs-lookup"><span data-stu-id="a894e-129">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

4. <span data-ttu-id="a894e-130">Enter 키를 선택하여 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-130">Select ENTER to submit the request.</span></span>

## <a name="clean-up"></a><span data-ttu-id="a894e-131">정리</span><span class="sxs-lookup"><span data-stu-id="a894e-131">Clean up</span></span>

<span data-ttu-id="a894e-132">이 함수에 대해 요금이 청구되지 않도록 하려면 로그 창 위에 있는 **일시 중지**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="a894e-132">To ensure that you aren't charged for this function, select **Pause** above the log window.</span></span>

![일시 중지](../media-drafts/4-pause-timer.png)