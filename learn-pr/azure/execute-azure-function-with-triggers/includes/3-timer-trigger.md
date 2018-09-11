<span data-ttu-id="5a1c2-101">일반적으로 논리는 설정 간격으로 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-101">It's common to execute a piece of logic at a set interval.</span></span> <span data-ttu-id="5a1c2-102">블로그 소유자이며 구독자가 가장 최근 게시물을 읽지 못하는 것을 알았다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-102">Imagine you're a blog owner and you notice that your subscribers aren't reading your most recent posts.</span></span> <span data-ttu-id="5a1c2-103">구독자에게 블로그를 확인하도록 미리 알리기 위해 매주 한 번 메일을 보내는 것이 가장 적합하다고 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-103">You decide that the best action is to send an email once a week to remind them to check your blog.</span></span> <span data-ttu-id="5a1c2-104">_타이머 트리거_와 함께 Azure 함수를 사용하여 이 논리를 구현하고 매주 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-104">You implement this logic using an Azure function with a _timer trigger_ to invoke your function weekly.</span></span>

## <a name="what-is-a-timer-trigger"></a><span data-ttu-id="5a1c2-105">타이머 트리거란?</span><span class="sxs-lookup"><span data-stu-id="5a1c2-105">What is a timer trigger?</span></span>

<span data-ttu-id="5a1c2-106">타이머 트리거는 일정 간격으로 함수를 실행하는 트리거입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-106">A timer trigger is a trigger that executes a function at a consistent interval.</span></span> <span data-ttu-id="5a1c2-107">타이머 트리거를 만들려면 두 가지 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-107">To create a timer trigger, you need to supply two pieces of information.</span></span> 

1. <span data-ttu-id="5a1c2-108">*타임스탬프 매개 변수 이름* - 코드의 트리거에 액세스하기 위한 식별자입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-108">A *Timestamp parameter name*, which is simply an identifier to access the trigger in code.</span></span> 
2. <span data-ttu-id="5a1c2-109">*일정* - 타이머의 간격을 설정하는 *CRON 식*입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-109">A *Schedule*, which is a *CRON expression* that sets the interval for the timer.</span></span>

## <a name="what-is-a-cron-expression"></a><span data-ttu-id="5a1c2-110">CRON 식이란?</span><span class="sxs-lookup"><span data-stu-id="5a1c2-110">What is a CRON expression?</span></span>

<span data-ttu-id="5a1c2-111">*CRON 식*은 시간 집합을 나타내는 6개의 필드로 구성된 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-111">A *CRON expression* is a string that consists of six fields that represent a set of times.</span></span>

<span data-ttu-id="5a1c2-112">Azure에서 6개 필드의 순서는 `{second} {minute} {hour} {day} {month} {day of the week}`입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-112">The order of the six fields in Azure is: `{second} {minute} {hour} {day} {month} {day of the week}`.</span></span>

<span data-ttu-id="5a1c2-113">예를 들어 5분마다 실행되는 트리거를 만드는 *CRON 식*은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-113">For example, a *CRON expression* to create a trigger that executes every five minutes looks like:</span></span>

```
0 */5 * * * *
```

<span data-ttu-id="5a1c2-114">처음에는 이 문자열이 혼동될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-114">At first, this string may look confusing.</span></span> <span data-ttu-id="5a1c2-115">돌아와서 ‘CRON 식’을 더 자세히 살펴볼 때 이러한 개념을 분류해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-115">We'll come back and break down these concepts when we have a deeper look at *CRON expressions*.</span></span>

<span data-ttu-id="5a1c2-116">‘CRON 식’을 빌드하려면 일부 특수 문자를 기본적으로 이해해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-116">To build a *CRON expression*, you need to have a basic understanding of some of the special characters.</span></span>

| <span data-ttu-id="5a1c2-117">특수 문자</span><span class="sxs-lookup"><span data-stu-id="5a1c2-117">Special character</span></span> | <span data-ttu-id="5a1c2-118">의미</span><span class="sxs-lookup"><span data-stu-id="5a1c2-118">Meaning</span></span> | <span data-ttu-id="5a1c2-119">예</span><span class="sxs-lookup"><span data-stu-id="5a1c2-119">Example</span></span> |
| ------------- | ------------- | ------------- |
| *      | <span data-ttu-id="5a1c2-120">필드에서 모든 값 선택</span><span class="sxs-lookup"><span data-stu-id="5a1c2-120">Selects every value in a field</span></span> | <span data-ttu-id="5a1c2-121">요일 필드의 별표 “\*”는 ‘매’일을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-121">An asterisk "\*" in the day of the week field means *every* day.</span></span> |
| <span data-ttu-id="5a1c2-122">.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-122">,</span></span>      | <span data-ttu-id="5a1c2-123">목록에서 항목 구분</span><span class="sxs-lookup"><span data-stu-id="5a1c2-123">Separates items in a list</span></span> | <span data-ttu-id="5a1c2-124">요일 필드의 쉼표 “1,3”은 월요일(1일) 및 수요일(3일)을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-124">A comma "1,3" in the day of the week field means just Mondays (day 1) and Wednesdays (day 3).</span></span> |
| -      | <span data-ttu-id="5a1c2-125">범위 지정</span><span class="sxs-lookup"><span data-stu-id="5a1c2-125">Specifies a range</span></span> | <span data-ttu-id="5a1c2-126">시간 필드의 하이픈 “10-12”는 시간 10, 11 및 12를 포함하는 범위를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-126">A hyphen "10-12" in the hour field means a range that includes the hours 10, 11, and 12.</span></span> |
| /      | <span data-ttu-id="5a1c2-127">증분 지정</span><span class="sxs-lookup"><span data-stu-id="5a1c2-127">Specifies an increment</span></span> | <span data-ttu-id="5a1c2-128">분 필드의 슬래시 “\*/10”은 10분마다 발생하는 증분을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-128">A slash "\*/10" in the minutes field means an increment of every 10 minutes.</span></span> |

<span data-ttu-id="5a1c2-129">이제 원래 CRON 식 예제로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-129">Now we'll go back to the original CRON expression example.</span></span> <span data-ttu-id="5a1c2-130">필드별로 필드를 분류하여 더 잘 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-130">Let’s try to understand it better by breaking it down field by field.</span></span>

```
0 */5 * * * *
```

<span data-ttu-id="5a1c2-131">**첫 번째 필드**는 초를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-131">The **first field** represents seconds.</span></span> <span data-ttu-id="5a1c2-132">이 필드는 0-59 값을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-132">This field supports the values 0-59.</span></span> <span data-ttu-id="5a1c2-133">필드에 0이 포함되어 있으므로 첫 번째 가능한 값(1초)을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-133">Because the field contains a zero, it selects the first possible value, which is one second.</span></span>

<span data-ttu-id="5a1c2-134">**두 번째 필드**는 분을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-134">The **second field** represents minutes.</span></span> <span data-ttu-id="5a1c2-135">“\*/5” 값에는 두 개의 특수 문자가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-135">The value "\*/5" contains two special characters.</span></span> <span data-ttu-id="5a1c2-136">먼저 별표(\*)는 “필드에서 모든 값 선택”을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-136">First, the asterisk (\*) means "select every value within the field."</span></span> <span data-ttu-id="5a1c2-137">이 필드는 분을 나타내므로 가능한 값은 0-59입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-137">Because this field represents minutes, the possible values are 0-59.</span></span> <span data-ttu-id="5a1c2-138">두 번째 특수 문자는 증분을 나타내는 슬래시(/)입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-138">The second special character is the slash (/), which represents an increment.</span></span> <span data-ttu-id="5a1c2-139">이들 문자를 결합하면 모든 값 0-59에서 매 5번째 값을 선택함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-139">When you combine these characters together, it means for all values 0-59, select every fifth value.</span></span> <span data-ttu-id="5a1c2-140">간단하게 말하면 “5분마다”입니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-140">An easier way to say that is simply "every five minutes."</span></span>

<span data-ttu-id="5a1c2-141">**나머지 4개 필드**는 시간, 날짜, 월 및 요일을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-141">The **remaining four fields** represent the hour, day, month, and weekday of the week.</span></span> <span data-ttu-id="5a1c2-142">이러한 필드의 별표는 모든 가능한 값을 선택함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-142">An asterisk for these fields means to select every possible value.</span></span> <span data-ttu-id="5a1c2-143">이 예제에서는 “매월 매일 매시간”을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-143">In this example, we select "every hour of every day of every month."</span></span>

<span data-ttu-id="5a1c2-144">모든 필드를 함께 넣으면 식은 “매월 매일 매시간 5분마다 첫 번째 1초”를 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-144">When you put all the fields together, the expression is read as "on the first second, of every fifth minute of every hour, of every day, of every month".</span></span>

## <a name="how-to-create-a-timer-trigger"></a><span data-ttu-id="5a1c2-145">타이머 트리거를 만드는 방법</span><span class="sxs-lookup"><span data-stu-id="5a1c2-145">How to create a timer trigger</span></span>

<span data-ttu-id="5a1c2-146">타이머 트리거는 완전히 Azure Portal에서 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-146">A timer trigger can be created completely within the Azure portal.</span></span> <span data-ttu-id="5a1c2-147">Azure 함수의 미리 정의된 트리거 형식 목록에서 **타이머 트리거**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-147">In your Azure function, select **timer trigger** from the list of predefined trigger types.</span></span> <span data-ttu-id="5a1c2-148">실행할 논리를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-148">Enter the logic that you want to execute.</span></span> <span data-ttu-id="5a1c2-149">**타임스탬프 매개 변수 이름** 및 **CRON 식**을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-149">Supply a **Timestamp parameter name** and the **CRON expression**.</span></span>

## <a name="summary"></a><span data-ttu-id="5a1c2-150">요약</span><span class="sxs-lookup"><span data-stu-id="5a1c2-150">Summary</span></span>

<span data-ttu-id="5a1c2-151">타이머 트리거는 지정된 일정으로 Azure 함수를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-151">A timer trigger invokes an Azure function on a consistent schedule.</span></span> <span data-ttu-id="5a1c2-152">타이머 트리거의 일정을 정의하려면 시간 집합을 나타내는 문자열인 ‘CRON 식’을 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="5a1c2-152">To define the schedule for a timer trigger, we build a *CRON expression*, which is a string that represents a set of times.</span></span>

