<span data-ttu-id="5d7e1-101">이 단원에서는 단일 문자열이 포함된 HTTP 요청을 허용하는 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-101">In this unit, we're going to create an Azure function that accepts an HTTP request with a single string.</span></span> <span data-ttu-id="5d7e1-102">함수는 성공 또는 실패를 표시하기 위해 문자열을 호출자에게 다시 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-102">The function returns a string back to the caller to represent success or failure.</span></span> <span data-ttu-id="5d7e1-103">이전 연습에서 학습한 함수에서 작동하는 법을 계속합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-103">We'll continue working on the function from the previous exercise.</span></span>

## <a name="create-an-http-trigger"></a><span data-ttu-id="5d7e1-104">HTTP 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="5d7e1-104">Create an HTTP trigger</span></span>

<span data-ttu-id="5d7e1-105">기존 Azure Functions 응용 프로그램을 계속 사용하고 HTTP 트리거를 추가해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-105">Let's continue using our existing Azure Functions application and add an HTTP trigger.</span></span>

1. <span data-ttu-id="5d7e1-106">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-106">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>

1. <span data-ttu-id="5d7e1-107">**모든 리소스** 화면으로 이동하고 함수 앱을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-107">Navigate to the **All resources** screen and select your function app.</span></span>

1. <span data-ttu-id="5d7e1-108">**Functions**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-108">Point to **Functions** and select the plus (+) icon.</span></span>

1. <span data-ttu-id="5d7e1-109">**HTTP 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-109">Select **HTTP trigger**.</span></span>

1. <span data-ttu-id="5d7e1-110">언어로 **C#** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-110">Select **C#** as the language.</span></span>

1. <span data-ttu-id="5d7e1-111">**이름**은 기본값으로 그대로 둡니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-111">Leave the **Name** set to the default value.</span></span>

1. <span data-ttu-id="5d7e1-112">**권한 수준**을 **익명**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-112">Set the **Authorization level** to **Anonymous**.</span></span>

1. <span data-ttu-id="5d7e1-113">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-113">Select **Create**.</span></span>

1. <span data-ttu-id="5d7e1-114">자동 생성 코드를 빠르게 검토하여 상황을 파악할 아이디어를 얻습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-114">Take a quick look at the auto-generated code to get an idea about what's going on.</span></span> <span data-ttu-id="5d7e1-115">*req* 매개 변수는 들어오는 요청을 나타내며 *name* 매개 변수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-115">The *req* parameter represents the incoming request and contains a *name* parameter.</span></span> <span data-ttu-id="5d7e1-116">*name*에 값이 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-116">We check to see if *name* has a value.</span></span> <span data-ttu-id="5d7e1-117">값이 있는 경우 인사말을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-117">If it does, we return a greeting.</span></span> <span data-ttu-id="5d7e1-118">값이 없다면 오류 메시지를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-118">Otherwise, we return an error message.</span></span>

## <a name="get-your-function-url"></a><span data-ttu-id="5d7e1-119">함수 URL 가져오기</span><span class="sxs-lookup"><span data-stu-id="5d7e1-119">Get your function URL</span></span>

<span data-ttu-id="5d7e1-120">HTTP 트리거를 만들었으므로 이제 요청 수행을 시작할 수 있도록 함수 URL을 가져오겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-120">Now that we've created the HTTP trigger, let's get the function URL so we can begin to make a request.</span></span>

1. <span data-ttu-id="5d7e1-121">HTTP 트리거를 선택하여 코드 화면을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-121">Select your HTTP trigger to open the code screen.</span></span>

1. <span data-ttu-id="5d7e1-122">**실행**의 오른쪽에서 **함수 URL 가져오기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-122">To the right of **Run**, select **Get function URL**.</span></span>

1. <span data-ttu-id="5d7e1-123">**복사**를 선택한 다음, 함수 URL 팝업 창을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-123">Select **Copy**, then close the function URL popup.</span></span>

## <a name="issue-a-get-request-to-your-http-trigger"></a><span data-ttu-id="5d7e1-124">HTTP 트리거에 대한 GET 요청 실행</span><span class="sxs-lookup"><span data-stu-id="5d7e1-124">Issue a GET request to your HTTP trigger</span></span>

<span data-ttu-id="5d7e1-125">이제 함수 URL을 클립보드에 복사했습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-125">We now have our function URL copied to our clipboard.</span></span> <span data-ttu-id="5d7e1-126">응답을 받는지 확인하기 위해 GET 요청을 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-126">Let's issue a GET request to see if we get a response.</span></span>

1. <span data-ttu-id="5d7e1-127">웹 브라우저에서 새 탭을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-127">Open a new tab in your web browser.</span></span>

1. <span data-ttu-id="5d7e1-128">URL을 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-128">Paste the URL into the address bar.</span></span>

1. <span data-ttu-id="5d7e1-129">예를 들어 이름을 사용하여 *name*이라는 쿼리 문자열 매개 변수를 추가 `.../api/HttpTriggerCSharp1?name=Jesse`</span><span class="sxs-lookup"><span data-stu-id="5d7e1-129">Add a query string parameter called *name* with your name for example `.../api/HttpTriggerCSharp1?name=Jesse`</span></span>

1. <span data-ttu-id="5d7e1-130"><kbd>ENTER</kbd> 키를 눌러 요청을 제출합니다.</span><span class="sxs-lookup"><span data-stu-id="5d7e1-130">Press <kbd>ENTER</kbd> to submit the request.</span></span>
