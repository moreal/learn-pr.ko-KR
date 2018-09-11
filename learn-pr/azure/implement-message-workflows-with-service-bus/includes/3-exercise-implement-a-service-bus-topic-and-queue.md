<span data-ttu-id="05579-101">다국적 기업의 영업 팀에서 특정 응용 프로그램을 사용한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-101">Suppose you have an application for the sales team in your global company.</span></span> <span data-ttu-id="05579-102">각 팀 멤버에게는 앱을 설치할 휴대폰이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-102">Each team member has a mobile phone where your app will be installed.</span></span> <span data-ttu-id="05579-103">Azure에서 호스팅되는 웹 서비스가 응용 프로그램의 비즈니스 논리를 구현하고 정보를 Azure SQL Database에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-103">A web service hosted in Azure implements the business logic for your application and stores information in Azure SQL Database.</span></span> <span data-ttu-id="05579-104">각 지역에는 웹 서비스 인스턴스가 하나씩 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-104">There is one instance of the web service for each geographical region.</span></span> <span data-ttu-id="05579-105">모바일 앱과 웹 서비스 간에 메시지를 보내는 용도는 다음과 같이 확인되었습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-105">You have identified the following purposes for sending messages between the mobile app and the web service:</span></span>

- <span data-ttu-id="05579-106">개별 판매와 관련된 메시지는 사용자 지역의 웹 서비스 인스턴스로만 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-106">Messages that relate to individual sales must be sent only to the web service instance in the user's region.</span></span>
- <span data-ttu-id="05579-107">영업 성과 관련 메시지는 웹 서비스의 모든 인스턴스로 전송해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-107">Messages that relate to sales performance must be sent to all instances of the web service.</span></span>

<span data-ttu-id="05579-108">첫 번째 사용 사례에는 Service Bus 큐를, 두 번째 사용 사례에는 Service Bus 항목을 구현하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-108">You have decided to implement a Service Bus queue for the first use case and the Service Bus topic for the second use case.</span></span>

<span data-ttu-id="05579-109">이 연습에서는 구독과 함께 큐와 항목을 모두 포함할 Service Bus 네임스페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="05579-109">In this exercise, you will create a Service Bus namespace, which will contain both a queue and a topic with subscriptions.</span></span>

## <a name="create-a-service-bus-namespace"></a><span data-ttu-id="05579-110">Service Bus 네임스페이스 만들기</span><span class="sxs-lookup"><span data-stu-id="05579-110">Create a Service Bus namespace</span></span>

<span data-ttu-id="05579-111">Azure Service Bus의 네임스페이스는 고유한 정규화된 도메인 이름이 지정된 큐, 항목 및 릴레이용 컨테이너입니다.</span><span class="sxs-lookup"><span data-stu-id="05579-111">In Azure Service Bus, a namespace is a container, with a unique fully qualified domain name, for queues, topics, and relays.</span></span> <span data-ttu-id="05579-112">먼저 네임스페이스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-112">You must start by creating the namespace.</span></span>

<span data-ttu-id="05579-113">각 네임스페이스에는 기본 및 보조 SAS(공유 액세스 서명) 암호화 키도 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-113">Each namespace also has primary and secondary Shared Access Signature (SAS) encryption keys.</span></span> <span data-ttu-id="05579-114">전송 또는 수신 구성 요소는 네임스페이스 내의 개체에 액세스하기 위해 연결할 때 이러한 키를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-114">A sending or receiving component must provide these keys when it connects to gain access to the objects within the namespace.</span></span>

<span data-ttu-id="05579-115">Azure Portal을 사용하여 Service Bus 네임스페이스를 만들려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="05579-115">To create a Service Bus namespace by using the Azure portal, following these steps:</span></span>

1. <span data-ttu-id="05579-116">브라우저에서 [Azure Portal](https://portal.azure.com/)로 이동한 다음 평상시에 사용하는 Azure 계정 자격 증명을 사용하여 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-116">In a browser, navigate the to [Azure portal](https://portal.azure.com/) and log in with your usual Azure account credentials.</span></span>

1. <span data-ttu-id="05579-117">왼쪽 탐색 영역에서 **모든 서비스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-117">In the navigation on the left, click **All services**.</span></span>

1. <span data-ttu-id="05579-118">**모든 서비스** 블레이드에서 아래쪽의 **통합** 섹션으로 스크롤한 다음 **Service Bus**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-118">In the **All Services** blade, scroll down to the **INTEGRATION** section and then click **Service Bus**.</span></span>

    ![Service Bus 네임스페이스 만들기](../media-draft/3-create-namespace-1.png)

1. <span data-ttu-id="05579-120">**Service Bus** 블레이드의 왼쪽 위에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-120">In the top left of the **Service Bus** blade, click **Add**.</span></span>

1. <span data-ttu-id="05579-121">**이름** 텍스트 상자에 네임스페이스의 고유한 이름을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-121">In the **Name** textbox, type a unique name for the namespace.</span></span> <span data-ttu-id="05579-122">예를 들어 "salesteamapp" + *사용자 이니셜* + *현재 날짜*를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-122">For example "salesteamapp" + *your initials* + *current date*</span></span>

1. <span data-ttu-id="05579-123">**가격 책정 계층** 드롭다운 목록에서 **Standard**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-123">In the **Pricing tier** drop-down list, select **Standard**.</span></span>

1. <span data-ttu-id="05579-124">**구독** 드롭다운 목록에서 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-124">In the **Subscription** drop-down list, select your subscription.</span></span>

1. <span data-ttu-id="05579-125">**리소스 그룹**에서 **새로 만들기**를 선택하고 **SalesTeamAppRG**를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-125">Under **Resource group** select **Create new**, and then type **SalesTeamAppRG**.</span></span>

1. <span data-ttu-id="05579-126">**위치** 드롭다운 목록에서 사용자 지역과 가까운 위치를 선택하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-126">In the **Location** drop-down list, select a location near you and then click **Create**.</span></span> <span data-ttu-id="05579-127">새 Service Bus 네임스페이스가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-127">Azure creates the new Service Bus namespace.</span></span>

    ![Service Bus 네임스페이스 만들기](../media-draft/3-create-namespace-2.png)

## <a name="create-a-service-bus-queue"></a><span data-ttu-id="05579-129">Service Bus 큐 만들기</span><span class="sxs-lookup"><span data-stu-id="05579-129">Create a Service Bus queue</span></span>

<span data-ttu-id="05579-130">이제 네임스페이스를 만들었으므로 개별 판매 관련 메시지용으로 큐를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-130">Now that you have a namespace, you can create a queue for messages about individual sales.</span></span> <span data-ttu-id="05579-131">이렇게 하려면 다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="05579-131">To do this, follow these steps:</span></span>

1. <span data-ttu-id="05579-132">**Service Bus** 블레이드에서 **새로 고침**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-132">In the **Service Bus** blade, click **Refresh**.</span></span> <span data-ttu-id="05579-133">방금 만든 네임스페이스가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-133">The namespace you just created is displayed.</span></span>

1. <span data-ttu-id="05579-134">방금 만든 네임스페이스를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-134">Click the namespace you just created.</span></span>

1. <span data-ttu-id="05579-135">네임스페이스 블레이드의 왼쪽 위에서 **+ 큐**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-135">In the top left of the namespace blade, click **+ Queue**.</span></span>

1. <span data-ttu-id="05579-136">**큐 만들기** 블레이드의 **이름** 텍스트 상자에 **salesmessages**를 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-136">In the **Create queue** blade, in the **Name** textbox type **salesmessages**, and then click **Create**.</span></span> <span data-ttu-id="05579-137">네임스페이스에 큐가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-137">Azure creates the queue in your namespace.</span></span>

    ![큐 만들기](../media-draft/3-create-queue.png)

## <a name="create-a-service-bus-topic-and-subscriptions"></a><span data-ttu-id="05579-139">Service Bus 항목과 구독 만들기</span><span class="sxs-lookup"><span data-stu-id="05579-139">Create a Service Bus topic and subscriptions</span></span>

<span data-ttu-id="05579-140">영업 성과 관련 메시지에 사용할 항목도 만들려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-140">You also want to create a topic that will be used for messages that relate to sales performance.</span></span> <span data-ttu-id="05579-141">그러면 여러 국가에서 사용되는 비즈니스 논리 웹 서비스의 복수 인스턴스가 이 항목을 구독하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-141">Multiple instances of the business logic web service will subscribe to this topic from different countries.</span></span> <span data-ttu-id="05579-142">각 메시지는 여러 인스턴스로 배달됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-142">Each message will be delivered to multiple instances.</span></span>

<span data-ttu-id="05579-143">다음 단계를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="05579-143">Follow these steps:</span></span>

1. <span data-ttu-id="05579-144">**Service Bus 네임스페이스** 블레이드에서 **+ 항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-144">In the **Service Bus Namespace** blade, click **+ Topic**.</span></span>

1. <span data-ttu-id="05579-145">**항목 만들기** 블레이드의 **이름** 텍스트 상자에 **salesperformancemessages**를 입력하고 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-145">In the **Create topic** blade, in the **Name** textbox type **salesperformancemessages**, and then click **Create**.</span></span> <span data-ttu-id="05579-146">네임스페이스에 항목이 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="05579-146">Azure creates the topic in your namespace.</span></span>

    ![항목 만들기](../media-draft/3-create-topic.png)

1. <span data-ttu-id="05579-148">항목이 생성되면 **Service Bus 네임스페이스** 블레이드의 **엔터티** 아래에서 **항목**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-148">When the topic has been created, in the **Service Bus Namespace** blade, under **Entities** click **Topics**.</span></span>

1. <span data-ttu-id="05579-149">항목 목록에서 **salesperformancemessages**를 클릭한 다음 **+ 구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-149">In the list of topics, click **salesperformancemessages** and then click **+ Subscription**.</span></span>

1. <span data-ttu-id="05579-150">**이름** 텍스트 상자에 **Americas**를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-150">In the **Name** textbox, type **Americas** and then click **Create**.</span></span>

1. <span data-ttu-id="05579-151">**+ 구독**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-151">Click **+ Subscription**.</span></span>

1. <span data-ttu-id="05579-152">**이름** 텍스트 상자에 **EuropeAndAfrica**를 입력한 다음 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-152">In the **Name** textbox, type **EuropeAndAfrica** and then click **Create**.</span></span>

<span data-ttu-id="05579-153">영업용 분산 응용 프로그램의 복원 기능을 개선하기 위해 Service Bus를 사용하는 데 필요한 인프라를 빌드했습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-153">You have built the infrastructure required to use Service Bus to increase the resilience of your sales force distributed application.</span></span> <span data-ttu-id="05579-154">그리고 개별 판매 관련 메시지용 큐와 영업 성과 관련 메시지용 항목을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="05579-154">You have created a queue for messages about individual sales and a topic for messages about sales performance.</span></span> <span data-ttu-id="05579-155">항목으로 전송되는 메시지는 전 세계의 여러 받는 사람 웹 서비스로 배달될 수 있으므로, 항목은 여러 구독을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="05579-155">The topic includes multiple subscriptions because messages sent to that topic can be delivered to multiple recipient web services around the world.</span></span>
