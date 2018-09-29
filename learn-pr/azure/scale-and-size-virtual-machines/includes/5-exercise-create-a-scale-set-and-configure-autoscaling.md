<span data-ttu-id="d910f-101">이 연습에서는 Azure Portal을 사용하여 자동 크기 조정 규칙이 포함된 가상 머신 확장 집합을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-101">In this exercise, you will use the Azure portal to create a virtual machine scale set with rules for autoscaling.</span></span>

## <a name="create-a-virtual-machine-scale-set"></a><span data-ttu-id="d910f-102">가상 머신 확장 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="d910f-102">Create a virtual machine scale set</span></span>

1. <span data-ttu-id="d910f-103">[Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에서 **리소스 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-103">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), click **Create a resource**.</span></span>

1. <span data-ttu-id="d910f-104">검색 상자에서 **확장 집합**을 입력하고 <kbd>ENTER</kbd> 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-104">In the search box, type **scale set** and press <kbd>ENTER</kbd>.</span></span> <span data-ttu-id="d910f-105">**결과** 블레이드에서 **가상 머신 확장 집합**을 클릭하고, **가상 머신 확장 집합** 블레이드에서 **만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-105">On the **Results** blade, click **Virtual machine scale set**, and on the **Virtual machine scale set** blade, click **Create**.</span></span>

1. <span data-ttu-id="d910f-106">**가상 머신 확장 집합 만들기** 블레이드에서 다음 값을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-106">On the **Create virtual machine scale set** blade, enter the following values.</span></span>
    - <span data-ttu-id="d910f-107">**이름**에 _WebServerSS_를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-107">Use _WebServerSS_ for the **Name**.</span></span>
    - <span data-ttu-id="d910f-108">**운영 체제 디스크 이미지**에 대해 _Windows Server 2016 Datacenter_를 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-108">Leave _Windows Server 2016 Datacenter_ for the **Operating system disk image**.</span></span>
    - <span data-ttu-id="d910f-109">**구독**에 대해 _컨시어지 구독_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-109">Use _Concierge Subscription_ for the **Subscription**.</span></span>
    - <span data-ttu-id="d910f-110">**리소스 그룹**에 대해 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-110">Select **<rgn>[sandbox resource group name]</rgn>** for the **Resource group**.</span></span>
    - <span data-ttu-id="d910f-111">[!include[](../../../includes/azure-sandbox-regions-note-friendly.md)] 목록의 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-111">Pick a location from the following list:   [!include[](../../../includes/azure-sandbox-regions-note-friendly.md)]</span></span>

    - <span data-ttu-id="d910f-112">유효한 **사용자 이름** 및 **암호**를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-112">Set a valid **Username** and **Password**.</span></span> <span data-ttu-id="d910f-113">(나중에 사용할 수 있게 적어둡니다)</span><span class="sxs-lookup"><span data-stu-id="d910f-113">(Note these for later use)</span></span>
    - <span data-ttu-id="d910f-114">**인스턴스 수**를 _2_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-114">Set the **Instance count** to _2_.</span></span>
    - <span data-ttu-id="d910f-115">**인스턴스 크기**를 _D2s_v3_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-115">Set the **Instance size** to _D2s_v3_.</span></span>
    - <span data-ttu-id="d910f-116">**자동 크기 조정**을 _사용하지 않음_으로 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-116">Leave **Autoscale** as _Disabled_.</span></span>
    - <span data-ttu-id="d910f-117">**부하 분산 장치**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-117">Select **Load balancer**.</span></span>
    - <span data-ttu-id="d910f-118">**공용 IP 주소 이름**에 _WebServerPubIP_를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-118">Enter _WebServerPubIP_ for the **Public IP address name**.</span></span>
    - <span data-ttu-id="d910f-119">**도메인 이름 레이블**이 고유하도록 이니셜 + 날짜 + 시간을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-119">Use your initials + date + time for the **Domain name label** so it's unique.</span></span>
    - <span data-ttu-id="d910f-120">**가상 네트워크**에 대해 **새로 만들기**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-120">For **Virtual network** select **Create new**.</span></span> <span data-ttu-id="d910f-121">가상 네트워크의 이름을 **SSVNet**으로 지정하고 **만들기**를 클릭하여 VNet을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-121">Name it **SSVNet** and click **Create** to create the VNet.</span></span>

1. <span data-ttu-id="d910f-122">**만들기**를 클릭하여 확장 집합을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-122">Click **Create** to deploy the scale set.</span></span>

1. <span data-ttu-id="d910f-123">확장 집합이 만들어질 때까지 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-123">Wait for the scale set to be created.</span></span>

## <a name="create-and-apply-autoscale-rules"></a><span data-ttu-id="d910f-124">자동 크기 조정 규칙 만들기 및 적용</span><span class="sxs-lookup"><span data-stu-id="d910f-124">Create and apply autoscale rules</span></span>

1. <span data-ttu-id="d910f-125">왼쪽 사이드바에서 **리소스 그룹**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-125">Click **Resource Groups** in the left sidebar.</span></span>

1. <span data-ttu-id="d910f-126">리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-126">Select the **<rgn>[sandbox resource group name]</rgn>** resource group.</span></span>

1. <span data-ttu-id="d910f-127">**<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 블레이드에서 **WebServerSS** 개체를 클릭하여 확장 집합 엽니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-127">On the **<rgn>[sandbox resource group name]</rgn>** blade, click the **WebServerSS** object to open the scale set.</span></span>

1. <span data-ttu-id="d910f-128">**WebServerSS** 블레이드의 **설정**에서 **인스턴스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-128">On the **WebServerSS** blade, under **Settings**, click **Instances**.</span></span> <span data-ttu-id="d910f-129">확장 집합 내에서 실행되는 두 개의 가상 머신 인스턴스에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="d910f-129">Note the two virtual machine instances running within the scale set.</span></span>

1. <span data-ttu-id="d910f-130">**WebServerSS** 블레이드에서 **크기 조정**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-130">On the **WebServerSS** blade, click **Scaling**.</span></span>

1. <span data-ttu-id="d910f-131">**WebServerSS - 크기 조정** 블레이드에서 **자동 크기 조정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-131">On the **WebServerSS - Scaling** blade, click **Enable autoscale**.</span></span>

1. <span data-ttu-id="d910f-132">구성 화면에서 이름을 **WebAutoscaleSetting**으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-132">On configuration screen, set the name to **WebAutoscaleSetting**.</span></span>

1. <span data-ttu-id="d910f-133">기본 조건에서 **인스턴스 제한**을 찾아 다음 값을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-133">In the default condition, locate the **Instance limits**, set the following values.</span></span>

    |<span data-ttu-id="d910f-134">설정</span><span class="sxs-lookup"><span data-stu-id="d910f-134">Setting</span></span>|<span data-ttu-id="d910f-135">값</span><span class="sxs-lookup"><span data-stu-id="d910f-135">Value</span></span>|
    |---|---|
    |<span data-ttu-id="d910f-136">최소</span><span class="sxs-lookup"><span data-stu-id="d910f-136">Minimum</span></span>|<span data-ttu-id="d910f-137">2</span><span class="sxs-lookup"><span data-stu-id="d910f-137">2</span></span>|
    |<span data-ttu-id="d910f-138">최대</span><span class="sxs-lookup"><span data-stu-id="d910f-138">Maximum</span></span>|<span data-ttu-id="d910f-139">8</span><span class="sxs-lookup"><span data-stu-id="d910f-139">8</span></span>|
    |<span data-ttu-id="d910f-140">기본값</span><span class="sxs-lookup"><span data-stu-id="d910f-140">Default</span></span>|<span data-ttu-id="d910f-141">2</span><span class="sxs-lookup"><span data-stu-id="d910f-141">2</span></span>|

1. <span data-ttu-id="d910f-142">**규칙 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-142">Click **Add a rule**.</span></span>

1. <span data-ttu-id="d910f-143">**크기 조정 규칙** 블레이드에서 다음 정보를 입력하여 평균 CPU 사용량이 5분 동안 75%를 초과하면 두 개의 가상 머신을 추가로 스케일 아웃하는 규칙을 만든 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-143">On the **Scale rule** blade, enter the following information to create a rule to scale out an extra two virtual machines when average CPU usage is more than 75% over a five-minute period, and then click **Add**.</span></span>

    |<span data-ttu-id="d910f-144">설정</span><span class="sxs-lookup"><span data-stu-id="d910f-144">Setting</span></span>|<span data-ttu-id="d910f-145">값</span><span class="sxs-lookup"><span data-stu-id="d910f-145">Value</span></span>|
    |---|---|
    |<span data-ttu-id="d910f-146">시간 집계</span><span class="sxs-lookup"><span data-stu-id="d910f-146">Time aggregation</span></span>|<span data-ttu-id="d910f-147">평균</span><span class="sxs-lookup"><span data-stu-id="d910f-147">Average</span></span>|
    |<span data-ttu-id="d910f-148">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="d910f-148">Metric name</span></span>|<span data-ttu-id="d910f-149">CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="d910f-149">Percentage CPU</span></span>|
    |<span data-ttu-id="d910f-150">시간 조직 통계</span><span class="sxs-lookup"><span data-stu-id="d910f-150">Time grain statistic</span></span>|<span data-ttu-id="d910f-151">평균</span><span class="sxs-lookup"><span data-stu-id="d910f-151">Average</span></span>|
    |<span data-ttu-id="d910f-152">연산자</span><span class="sxs-lookup"><span data-stu-id="d910f-152">Operator</span></span>|<span data-ttu-id="d910f-153">보다 큼</span><span class="sxs-lookup"><span data-stu-id="d910f-153">Greater than</span></span>|
    |<span data-ttu-id="d910f-154">임계값</span><span class="sxs-lookup"><span data-stu-id="d910f-154">Threshold</span></span>|<span data-ttu-id="d910f-155">75</span><span class="sxs-lookup"><span data-stu-id="d910f-155">75</span></span>|
    |<span data-ttu-id="d910f-156">기간(분)</span><span class="sxs-lookup"><span data-stu-id="d910f-156">Duration (in minutes)</span></span>|<span data-ttu-id="d910f-157">5</span><span class="sxs-lookup"><span data-stu-id="d910f-157">5</span></span>|
    |<span data-ttu-id="d910f-158">작업</span><span class="sxs-lookup"><span data-stu-id="d910f-158">Operation</span></span>|<span data-ttu-id="d910f-159">다음을 기준으로 개수 늘이기</span><span class="sxs-lookup"><span data-stu-id="d910f-159">Increase count by</span></span>|
    |<span data-ttu-id="d910f-160">인스턴트 수</span><span class="sxs-lookup"><span data-stu-id="d910f-160">Instance count</span></span>|<span data-ttu-id="d910f-161">2</span><span class="sxs-lookup"><span data-stu-id="d910f-161">2</span></span>|
    |<span data-ttu-id="d910f-162">정지 시간(분)</span><span class="sxs-lookup"><span data-stu-id="d910f-162">Cool down (minutes)</span></span>|<span data-ttu-id="d910f-163">5</span><span class="sxs-lookup"><span data-stu-id="d910f-163">5</span></span>|

1. <span data-ttu-id="d910f-164">이번에는 다른 규칙을 추가하고 다음 정보를 입력하여 평균 CPU 사용량이 5분 동안 30% 미만이면 한 번에 하나의 서버를 스케일 인하는 규칙을 만든 다음, **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-164">Add another rule, this time, enter the following information to create a rule to scale in one server at a time when average CPU usage is below 30% over a five-minute period, and then click **Add**.</span></span>

    |<span data-ttu-id="d910f-165">설정</span><span class="sxs-lookup"><span data-stu-id="d910f-165">Setting</span></span>|<span data-ttu-id="d910f-166">값</span><span class="sxs-lookup"><span data-stu-id="d910f-166">Value</span></span>|
    |---|---|
    |<span data-ttu-id="d910f-167">시간 집계</span><span class="sxs-lookup"><span data-stu-id="d910f-167">Time aggregation</span></span>|<span data-ttu-id="d910f-168">평균</span><span class="sxs-lookup"><span data-stu-id="d910f-168">Average</span></span>|
    |<span data-ttu-id="d910f-169">메트릭 이름</span><span class="sxs-lookup"><span data-stu-id="d910f-169">Metric name</span></span>|<span data-ttu-id="d910f-170">CPU 사용률</span><span class="sxs-lookup"><span data-stu-id="d910f-170">Percentage CPU</span></span>|
    |<span data-ttu-id="d910f-171">시간 조직 통계</span><span class="sxs-lookup"><span data-stu-id="d910f-171">Time grain statistic</span></span>|<span data-ttu-id="d910f-172">평균</span><span class="sxs-lookup"><span data-stu-id="d910f-172">Average</span></span>|
    |<span data-ttu-id="d910f-173">연산자</span><span class="sxs-lookup"><span data-stu-id="d910f-173">Operator</span></span>|<span data-ttu-id="d910f-174">보다 작음</span><span class="sxs-lookup"><span data-stu-id="d910f-174">Less than</span></span>|
    |<span data-ttu-id="d910f-175">임계값</span><span class="sxs-lookup"><span data-stu-id="d910f-175">Threshold</span></span>|<span data-ttu-id="d910f-176">30</span><span class="sxs-lookup"><span data-stu-id="d910f-176">30</span></span>|
    |<span data-ttu-id="d910f-177">기간(분)</span><span class="sxs-lookup"><span data-stu-id="d910f-177">Duration (in minutes)</span></span>|<span data-ttu-id="d910f-178">5</span><span class="sxs-lookup"><span data-stu-id="d910f-178">5</span></span>|
    |<span data-ttu-id="d910f-179">작업</span><span class="sxs-lookup"><span data-stu-id="d910f-179">Operation</span></span>|<span data-ttu-id="d910f-180">다음을 기준으로 개수 줄이기</span><span class="sxs-lookup"><span data-stu-id="d910f-180">Decrease count by</span></span>|
    |<span data-ttu-id="d910f-181">인스턴트 수</span><span class="sxs-lookup"><span data-stu-id="d910f-181">Instance count</span></span>|<span data-ttu-id="d910f-182">1</span><span class="sxs-lookup"><span data-stu-id="d910f-182">1</span></span>|
    |<span data-ttu-id="d910f-183">정지 시간(분)</span><span class="sxs-lookup"><span data-stu-id="d910f-183">Cool down (minutes)</span></span>|<span data-ttu-id="d910f-184">5</span><span class="sxs-lookup"><span data-stu-id="d910f-184">5</span></span>|

1. <span data-ttu-id="d910f-185">규칙은 다음과 같이 표시되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-185">Your rules should look something like this:</span></span>

    ![VM 확장 집합에 적용된 자동 크기 조정 규칙 집합의 스크린샷](../media/5-scale-rules.png)

1. <span data-ttu-id="d910f-187">**저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-187">Click **Save**.</span></span>

## <a name="generate-load-to-demonstrate-autoscaling"></a><span data-ttu-id="d910f-188">로드를 생성하여 자동 크기 조정 시연</span><span class="sxs-lookup"><span data-stu-id="d910f-188">Generate load to demonstrate autoscaling</span></span>

<span data-ttu-id="d910f-189">이제 SysInternals **CPUStress.exe** 도구를 사용하여 확장 집합의 가상 머신에서 로드를 생성하고 자동 스케일 아웃을 시연합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-189">Now you will use the SysInternals **CPUStress.exe** tool to generate load on the virtual machines in the scale set and demonstrate automatic scaling out.</span></span>

<span data-ttu-id="d910f-190">해당 VM에서 이 도구를 실행하므로 이를 위한 Windows는 필요가 없습니다. 그러나 원격 데스크톱 클라이언트는 _반드시_ 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-190">We will run this on our VM - you do not need to have Windows for this, however you _do_ need a Remote Desktop Client.</span></span> <span data-ttu-id="d910f-191">Microsoft에는 macOS 및 Windows용 클라이언트가 있으며, 다양한 Linux 분산에도 클라이언트가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-191">Microsoft has one for macOS and Windows, and various distributions of Linux include a client as well.</span></span>

1. <span data-ttu-id="d910f-192">연결할 공용 IP 주소를 확인하려면 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-192">To determine the public IP address to connect to, browse to the **<rgn>[sandbox resource group name]</rgn>** resource group.</span></span> <span data-ttu-id="d910f-193">**<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 블레이드에서 **WebServerSSlb** 개체를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-193">On the **<rgn>[sandbox resource group name]</rgn>** blade, click the **WebServerSSlb** object.</span></span>

1. <span data-ttu-id="d910f-194">**WebServerSSlb** 블레이드에서 **프런트 엔드 IP 구성**을 클릭하고 표시된 공용 IP 주소를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-194">On the **WebServerSSlb** blade, click **Frontend IP configuration** and make a note of the public IP address shown.</span></span> <span data-ttu-id="d910f-195">**LoadBalancerFrontEnd** 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-195">Close the **LoadBalancerFrontEnd** blade.</span></span>

1. <span data-ttu-id="d910f-196">연결할 포트 번호를 확인하려면 **WebServerSSlb** 블레이드에서 **인바운드 NAT 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-196">To determine the port number to connect to, on the **WebServerSSlb** blade, click **Inbound NAT rules**.</span></span> <span data-ttu-id="d910f-197">각 가상 머신에 대한 [서비스] 열의 사용자 지정 포트 번호를 적어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-197">Note down the custom port number in the Service column for each virtual machine.</span></span>

1. <span data-ttu-id="d910f-198">로컬 컴퓨터에서 **원격 데스크톱 연결**을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-198">On your local computer, start the **Remote Desktop Connection**.</span></span> <span data-ttu-id="d910f-199">**컴퓨터** 상자에서 부하 분산 장치의 공용 IP 주소, 콜론 및 인스턴스 0에 대한 포트 번호 값을 차례로 입력한 다음(예: 40.67.191.221:50000), **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-199">In the **Computer** box, type the public IP address of the load balancer, followed by a colon and then the port number value for Instance 0 (for example, 40.67.191.221:50000), and then click **Connect**.</span></span>

1. <span data-ttu-id="d910f-200">**Windows 보안** 대화 상자에서 **추가 선택**을 클릭한 다음, **다른 계정 사용**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-200">In the **Windows Security** dialog box, click **More choices**, and then click **Use a different account**.</span></span> <span data-ttu-id="d910f-201">**사용자 이름** 및 **암호** 상자에 확장 집합을 만들 때 위에서 지정한 자격 증명을 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-201">In the **User name** and **Password** boxes, type enter the credentials you specified above when you created the scale set.</span></span>

1. <span data-ttu-id="d910f-202">**원격 데스크톱 연결** 대화 상자에서 **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-202">In the **Remote Desktop Connection** dialog box, click **Yes**.</span></span>

1. <span data-ttu-id="d910f-203">가상 머신 원격 데스크톱에서 Internet Explorer를 열고, **Internet Explorer 설정** 대화 상자에서 **확인**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-203">In the virtual machine remote desktop, open Internet Explorer, and in the **Set up Internet Explorer** dialog box, click **OK**.</span></span>

1. <span data-ttu-id="d910f-204">**Internet Explorer**의 주소 표시줄에서 **http://download.sysinternals.com/files/CPUSTRES.zip**을 입력하고 <kbd>ENTER</kbd> 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-204">In **Internet Explorer**, in the address bar, type **http://download.sysinternals.com/files/CPUSTRES.zip** and press <kbd>ENTER</kbd>.</span></span> <span data-ttu-id="d910f-205">**Internet Explorer** 대화 상자에서 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-205">In the **Internet Explorer** dialog box, click **Add**.</span></span> <span data-ttu-id="d910f-206">**신뢰할 수 있는 사이트** 대화 상자에서 **추가**를 클릭한 다음, **닫기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-206">In the **Trusted Sites** dialog box, click **Add** and then click **Close**.</span></span>

1. <span data-ttu-id="d910f-207">다운로드 프롬프트가 자동으로 표시되지 않으면 URL을 다시 입력하고 <kbd>ENTER</kbd> 키를 눌러야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-207">If the download prompt does not appear automatically, you may need to enter the URL again and press <kbd>ENTER</kbd>.</span></span> <span data-ttu-id="d910f-208">**Internet Explorer** 대화 상자에서 **저장**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-208">In the **Internet Explorer** dialog box, click **Save**.</span></span> <span data-ttu-id="d910f-209">다운로드가 완료되면 **폴더 열기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-209">Once the download is complete, click **Open folder**.</span></span>

1. <span data-ttu-id="d910f-210">**다운로드** 폴더에서 **CPUSTRES**를 두 번 클릭한 다음, **CPUSTRES** 응용 프로그램을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-210">In the **Downloads** folder, double-click **CPUSTRES**, and then double-click the **CPUSTRES** application.</span></span> <span data-ttu-id="d910f-211">**압축(ZIP) 폴더** 대화 상자에서 **실행**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-211">In the **Compressed (zipped) folders** dialog box, click **Run**.</span></span>

1. <span data-ttu-id="d910f-212">**CPU 스트레스** 창에 있는 **스레드 1** 아래의 **활동** 드롭다운에서 **최대**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-212">In the **CPU Stress** window, under **Thread 1**, in the **Activity** drop-down, select **Maximum**.</span></span> <span data-ttu-id="d910f-213">**스레드 2** 아래에서 **활동** 확인란을 클릭하고, **활동** 드롭다운에서 드롭다운 내의 아래로 화살표를 클릭하고 **최대**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-213">Under **Thread 2**, click the **Active** checkbox, and in the **Activity** drop-down, click the down arrorw inside the drop-down and select **Maximum**.</span></span> <span data-ttu-id="d910f-214">이러한 설정은 즉시 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-214">These settings take effect immediately.</span></span>

1. <span data-ttu-id="d910f-215">Windows 시작 단추를 클릭한 다음, **작업 관리자**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-215">Click the Windows Start button, then click **Task Manager**.</span></span> <span data-ttu-id="d910f-216">작업 관리자에서 **자세한 내용**을 클릭하고, CPU가 75%를 초과하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-216">In Task Manager, click **More details**, and confirm that the CPU is over 75%.</span></span>

1. <span data-ttu-id="d910f-217">확장 집합의 다른 가상 머신에서 **CPUSTRES**의 설치 및 시작을 **반복**한 다음, 5분 동안 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-217">**Repeat** the installation and launch of **CPUSTRES** on the other virtual machine in the scale set, and then wait for five minutes.</span></span>

1. <span data-ttu-id="d910f-218">Azure Portal에서 리소스 그룹 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-218">In the Azure portal, browse to the **<rgn>[sandbox resource group name]</rgn>** resource group.</span></span> <span data-ttu-id="d910f-219">**<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 블레이드에서 **WebServerSS** 개체를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-219">On the **<rgn>[sandbox resource group name]</rgn>** blade, click the **WebServerSS** object.</span></span> <span data-ttu-id="d910f-220">**WebServerSS** 블레이드에서 **인스턴스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-220">On the **WebServerSS** blade, click **Instances**.</span></span> <span data-ttu-id="d910f-221">확장 집합 내에 표시되는 가상 머신 인스턴스의 수와 상태를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-221">Note how many virtual machine instances are displayed within the scale set and the status.</span></span>

<span data-ttu-id="d910f-222">여기서는 두 개의 가상 머신이 포함된 가상 머신 확장 집합을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-222">Here, you created a virtual machine scale set with two virtual machines.</span></span> <span data-ttu-id="d910f-223">그런 다음, 확장 집합을 자동으로 스케일 아웃 및 스케일 인하는 규칙을 만들고, 해당 규칙을 자동 크기 조정 프로필에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="d910f-223">You then created rules to automatically scale out and scale in the scale set, and you added the rules to an autoscale profile.</span></span>
