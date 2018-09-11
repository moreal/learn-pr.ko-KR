<span data-ttu-id="3aaa5-101">이 연습에서는 타이머 트리거를 사용하여 20초마다 호출되는 Azure 함수를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-101">In this exercise, we create an Azure function that's invoked every 20 seconds using a timer trigger.</span></span>

> [!NOTE] 
> <span data-ttu-id="3aaa5-102">이 연습을 완료하려면 유효한 계정으로 [Azure Portal](https://portal.azure.com/)에 로그인했는지 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-102">To complete this exercise, make sure you're logged into the [Azure portal](https://portal.azure.com/) with a valid account.</span></span>

## <a name="create-an-azure-function"></a><span data-ttu-id="3aaa5-103">Azure Function 만들기</span><span class="sxs-lookup"><span data-stu-id="3aaa5-103">Create an Azure function</span></span>

<span data-ttu-id="3aaa5-104">먼저 포털에서 Azure 함수를 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-104">Let’s start by creating an Azure function in the portal.</span></span>

1. <span data-ttu-id="3aaa5-105">왼쪽 탐색에서 **리소스 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-105">In the left navigation, select **Create a resource**.</span></span>

1. <span data-ttu-id="3aaa5-106">**계산**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-106">Select **Compute**.</span></span>

1. <span data-ttu-id="3aaa5-107">**함수 앱**을 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-107">Locate and select **Function App**.</span></span> <span data-ttu-id="3aaa5-108">필요한 경우 검색 창을 사용하여 템플릿을 찾을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-108">You can also optionally use the search bar to locate the template.</span></span>

    ![함수 앱 선택](../media-drafts/4-click-function-app.png)

1. <span data-ttu-id="3aaa5-110">고유한 **앱 이름**을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-110">Enter a unique **App name**.</span></span>

1. <span data-ttu-id="3aaa5-111">**구독**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-111">Select a **Subscription**.</span></span>

1. <span data-ttu-id="3aaa5-112">새 **리소스 그룹**을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-112">Create a new **Resource Group**.</span></span>

1. <span data-ttu-id="3aaa5-113">**OS**로 **Windows**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-113">Choose **Windows** as your **OS**.</span></span>

1. <span data-ttu-id="3aaa5-114">**호스팅 플랜**에 대한 **사용 플랜**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-114">Choose **Consumption Plan** for your **Hosting Plan**.</span></span> <span data-ttu-id="3aaa5-115">각 함수 실행에 대한 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-115">You're charged for each execution of your function.</span></span> <span data-ttu-id="3aaa5-116">리소스는 응용 프로그램 워크로드에 따라 자동으로 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-116">Resources are automatically allocated based on your application workload.</span></span>

1. <span data-ttu-id="3aaa5-117">**위치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-117">Select a **Location**.</span></span>

1. <span data-ttu-id="3aaa5-118">새 **저장소** 계정을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-118">Create a new **Storage** account.</span></span> <span data-ttu-id="3aaa5-119">이 값은 필수이나 앞으로 사용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-119">(This value is required, but we're not going to use it.)</span></span>

1. <span data-ttu-id="3aaa5-120">**Application Insights**를 끕니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-120">Turn off **Application Insights**.</span></span>

1. <span data-ttu-id="3aaa5-121">**만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-121">Select **Create**.</span></span>

## <a name="create-a-timer-trigger"></a><span data-ttu-id="3aaa5-122">타이머 트리거 만들기</span><span class="sxs-lookup"><span data-stu-id="3aaa5-122">Create a timer trigger</span></span>

<span data-ttu-id="3aaa5-123">이제 Azure 함수 내에 타이머 트리거를 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-123">Now we're going to create a timer trigger inside our Azure function.</span></span>

1. <span data-ttu-id="3aaa5-124">Azure 함수를 만든 후 왼쪽 탐색에서 **모든 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-124">After the Azure function is created, select **All resources** from the left navigation.</span></span>

1. <span data-ttu-id="3aaa5-125">Azure 함수를 찾아 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-125">Locate and select your Azure function.</span></span>

1. <span data-ttu-id="3aaa5-126">새 블레이드에서 **함수**를 가리키고 더하기(+) 아이콘을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-126">On the new blade, point to **Functions** and select the plus (+) icon.</span></span>

    ![함수를 가리키고 더하기 선택](../media-drafts/4-hover-function.png)

1. <span data-ttu-id="3aaa5-128">**타이머**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-128">Select **Timer**.</span></span>

1. <span data-ttu-id="3aaa5-129">언어로 **CSharp**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-129">Select **CSharp** as the language.</span></span>

1. <span data-ttu-id="3aaa5-130">**이 함수 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-130">Select **Create this function**.</span></span>

## <a name="configure-the-timer-trigger"></a><span data-ttu-id="3aaa5-131">타이머 트리거 구성</span><span class="sxs-lookup"><span data-stu-id="3aaa5-131">Configure the timer trigger</span></span>

<span data-ttu-id="3aaa5-132">로그 창에 메시지를 인쇄하는 논리가 포함된 Azure 함수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-132">We have an Azure function with logic to print a message to the log window.</span></span> <span data-ttu-id="3aaa5-133">20초마다 실행하도록 타이머 일정을 설정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-133">We're going to set the schedule of the timer to execute every 20 seconds.</span></span>

1. <span data-ttu-id="3aaa5-134">**통합**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-134">Select **Integrate**.</span></span>

1. <span data-ttu-id="3aaa5-135">**일정** 상자에 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-135">Enter the following value into the **Schedule** box:</span></span>

    ```
    */20 * * * * *
    ```

1. <span data-ttu-id="3aaa5-136">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-136">Select **Save**.</span></span>

## <a name="start-the-timer"></a><span data-ttu-id="3aaa5-137">타이머 시작</span><span class="sxs-lookup"><span data-stu-id="3aaa5-137">Start the timer</span></span>

<span data-ttu-id="3aaa5-138">이제 타이머를 구성했으므로 시작할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-138">Now that we've configured the timer, we're ready to start it.</span></span>

1. <span data-ttu-id="3aaa5-139">**TimerTriggerCSharp1**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-139">Select **TimerTriggerCSharp1**.</span></span> 

    > [!NOTE]
    > <span data-ttu-id="3aaa5-140">**TimerTriggerCSharp1**은 기본 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-140">**TimerTriggerCSharp1** is a default name.</span></span> <span data-ttu-id="3aaa5-141">트리거를 만들 때 자동으로 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-141">It's automatically selected when you create the trigger.</span></span>

1. <span data-ttu-id="3aaa5-142">**실행**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-142">Select **Run**.</span></span> 

<span data-ttu-id="3aaa5-143">이때 로그 창에 20초마다 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-143">At this point, you should see a message every 20 seconds in the log window.</span></span>

## <a name="clean-up"></a><span data-ttu-id="3aaa5-144">정리</span><span class="sxs-lookup"><span data-stu-id="3aaa5-144">Clean up</span></span>

<span data-ttu-id="3aaa5-145">이 함수에 대해 요금이 청구되지 않도록 하려면 로그 창 위에 있는 **일시 중지**를 선택하여 타이머를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="3aaa5-145">To ensure that you aren't charged for this function, above the log window, select **Pause** to stop the timer.</span></span>

![일시 중지](../media-drafts/4-pause-timer.png)


