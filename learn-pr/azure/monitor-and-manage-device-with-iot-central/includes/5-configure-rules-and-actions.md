<span data-ttu-id="8d1c4-101">지금까지 커피 머신을 Azure IoT Central 응용 프로그램에 연결하여 데이터를 교환하여 커피 머신을 관리하고 모니터링할 수 있게 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-101">So far, you've connected your coffee machine to the Azure IoT Central application, enabling the exchange of data that allows you to monitor and manage your coffee machine.</span></span> <span data-ttu-id="8d1c4-102">이 단원에서는 커피 머신의 수온이 정상 범위를 벗어나는 경우 작업을 트리거하는 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-102">In this unit, you create rules that trigger actions when the water temperature of the coffee machine is outside the normal range.</span></span> 

## <a name="create-rules-in-iot-central-with-email-as-the-action"></a><span data-ttu-id="8d1c4-103">이메일을 보내는 작업을 추가하여 IoT Central에서 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="8d1c4-103">Create rules in IoT Central with email as the action</span></span>

<span data-ttu-id="8d1c4-104">Azure IoT Central에는 알림을 전송하기 위한 기본적인 메일 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-104">Azure IoT Central has its native email capabilities to send notifications.</span></span> <span data-ttu-id="8d1c4-105">이 시나리오에서는 최적 온도 범위를 벗어나는 커피 머신이 보증을 통해 보호되지 않는 경우 IoT Central에서 고객의 유지 관리 부서로 이메일이 전송됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-105">In this scenario, if the coffee machine is outside the optimal temperature range and is not protected by the warranty, an email is sent by IoT Central to the client’s maintenance department.</span></span>

1. <span data-ttu-id="8d1c4-106">이 단위에서는 연습에 대한 **규칙** 페이지로 이동하고 오른쪽에서 **템플릿 편집**을 선택하여 편집 모드로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-106">Navigate to the **Rules** page for the exercises in this unit and enter edit mode by selecting **Edit Template** on the right.</span></span> 
1. <span data-ttu-id="8d1c4-107">**+ 새 규칙 만들기**, **원격 분석**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-107">Select **+ New Rule** and then **Telemetry**.</span></span> 

1. <span data-ttu-id="8d1c4-108">`Coffee Maker Water Too Cold (Expired)`의 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-108">Enter the name `Coffee Maker Water Too Cold (Expired)`</span></span>

1. <span data-ttu-id="8d1c4-109">**조건**의 오른쪽에 더하기(**+**) 기호를 선택하여 다음과 같은 조건을 규칙에 추가한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-109">Add the following conditions to the rule by selecting the plus (**+**) sign to the right of **Conditions**, and then click **Save**:</span></span>      
    - <span data-ttu-id="8d1c4-110">수온이 커피 메이커 최소 온도보다 낮음</span><span class="sxs-lookup"><span data-stu-id="8d1c4-110">Water Temperature is less than Coffee Maker's Min Temperature</span></span>
    - <span data-ttu-id="8d1c4-111">장치 보증 만료 = 1</span><span class="sxs-lookup"><span data-stu-id="8d1c4-111">Device Warranty Expired equals 1</span></span>

    ![규칙 사용](../media/5-flow-a.png)

1. <span data-ttu-id="8d1c4-113">**원격 분석 규칙 구성** 패널에서 아래로 스크롤하여 **작업** 옆에 있는 **+** 를 선택한 다음, **이메일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-113">Scroll down on the **Configure Telemetry Rule** panel and choose **+** next to **Actions**, and then choose **Email**.</span></span>

1. <span data-ttu-id="8d1c4-114">IoT Central 응용 프로그램에 로그인하는 데 사용한 이메일 주소를 입력하고 다음 메모를 추가합니다. `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span><span class="sxs-lookup"><span data-stu-id="8d1c4-114">Enter the email address that you used to sign in to the IoT Central application and add the note `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span></span>

1. <span data-ttu-id="8d1c4-115">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-115">Choose **Save**.</span></span> <span data-ttu-id="8d1c4-116">**규칙** 페이지에 규칙이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-116">Your rule is listed on the **Rules** page.</span></span>

<span data-ttu-id="8d1c4-117">이제 물이 뜨거운 경우 이 단계를 반복하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-117">Now let's repeat these steps for the case when the water is too hot.</span></span> 

1. <span data-ttu-id="8d1c4-118">**+ 새 규칙 만들기**, **원격 분석**을 차례로 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-118">Select **+ New Rule** and then **Telemetry**.</span></span>

1. <span data-ttu-id="8d1c4-119">새 규칙을 추가하고 이름을 `Coffee Maker Water Too Hot (Expired)`으로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-119">Add a new rule and give it the name `Coffee Maker Water Too Hot (Expired)`</span></span>

1. <span data-ttu-id="8d1c4-120">**조건**의 오른쪽에 더하기(**+**) 기호를 선택하여 다음과 같은 조건을 규칙에 추가한 다음, **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-120">Add the following conditions to the rule by selecting the plus (**+**) sign to the right of **Conditions**, and then click **Save**:</span></span>      
    - <span data-ttu-id="8d1c4-121">수온이 커피 메이커 최대 온도보다 높음</span><span class="sxs-lookup"><span data-stu-id="8d1c4-121">Water Temperature is greater than Coffee Makers Max Temperature</span></span>
    - <span data-ttu-id="8d1c4-122">장치 보증 만료 = 1</span><span class="sxs-lookup"><span data-stu-id="8d1c4-122">Device Warranty Expired equals 1</span></span>

1. <span data-ttu-id="8d1c4-123">**원격 분석 규칙 구성** 패널에서 아래로 스크롤하여 **작업** 옆에 있는 **+** 를 선택한 다음, **이메일**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-123">Scroll down on the **Configure Telemetry Rule** panel and choose **+** next to **Actions**, and then choose **Email**.</span></span>

1. <span data-ttu-id="8d1c4-124">IoT Central 응용 프로그램에 로그인하는 데 사용한 이메일 주소를 입력하고 다음 메모를 추가합니다. `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span><span class="sxs-lookup"><span data-stu-id="8d1c4-124">Enter the email address that you used to sign in to the IoT Central application and add the note `Coffee maker's water is too cold. Maintenance is required.  Warranty has expired.`</span></span>

1. <span data-ttu-id="8d1c4-125">**저장**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-125">Choose **Save**.</span></span> <span data-ttu-id="8d1c4-126">**규칙** 페이지에 규칙이 나열됩니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-126">Your rule is listed on the **Rules** page.</span></span>

<span data-ttu-id="8d1c4-127">규칙을 트리거하려면 **속성**에서 지정한 범위를 벗어나는 최적 온도를 **설정**에서 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-127">To trigger the rule, set the optimal temperature in **Settings** outside the range that you specified under **Properties**.</span></span> <span data-ttu-id="8d1c4-128">유효성 검사를 완료하면 받은 편지함에 이메일이 너무 많이 수신되지 않도록 규칙을 해제합니다.</span><span class="sxs-lookup"><span data-stu-id="8d1c4-128">Once you are done with the validation, turn off the rules to avoid flooding your inbox with emails.</span></span>