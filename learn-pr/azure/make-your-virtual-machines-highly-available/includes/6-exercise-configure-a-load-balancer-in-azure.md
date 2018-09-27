<span data-ttu-id="d1223-101">온라인 뱅킹 아키텍처를 위한 주요 리소스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-101">You have created the key resources for your online bank architecture.</span></span> <span data-ttu-id="d1223-102">이 연습에서는 부하 분산 규칙을 구성하여 설치를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-102">In this exercise, you will complete the setup by configuring the load-balancing rules.</span></span>

<span data-ttu-id="d1223-103">설정이 완료되면 풀에서 VM을 제거하고 이 VM에 클라이언트 요청이 더 이상 전송되지 않는지 확인하여 부하 분산 장치를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-103">Once setup is complete, you will test the load balancer by removing a VM from the pool and verifying that client requests are no longer sent to this VM.</span></span>

<span data-ttu-id="d1223-104">부하 분산 장치에서 백 엔드 풀을 정의하여 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-104">We'll start by defining our backend pool in the load balancer.</span></span> <span data-ttu-id="d1223-105">이렇게 하면 인바운드 요청을 라우팅하는 위치가 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-105">This determines where inbound requests are routed.</span></span>

## <a name="create-a-backend-address-pool"></a><span data-ttu-id="d1223-106">백 엔드 주소 풀 만들기</span><span class="sxs-lookup"><span data-stu-id="d1223-106">Create a backend address pool</span></span>

1. <span data-ttu-id="d1223-107">[Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)의 왼쪽 메뉴에서 **모든 리소스**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-107">In the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true), in the left menu, Select **All resources**.</span></span> <span data-ttu-id="d1223-108">그런 다음, 리소스 목록에서 부하 분산 장치(**woodgrove-LB**)를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-108">Then, in the resource list, select your load balancer (**woodgrove-LB**).</span></span>

1. <span data-ttu-id="d1223-109">**설정** > **백 엔드 풀**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-109">Select **Settings** > **Backend pools**.</span></span> <span data-ttu-id="d1223-110">아직 아무 것도 정의되어 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-110">Notice we don't have any defined yet.</span></span>

1. <span data-ttu-id="d1223-111">**추가**를 클릭하여 새 백 엔드 풀을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-111">Click **Add** to add a new backend pool.</span></span>

    ![백 엔드 풀을 추가하는 방법을 보여주는 스크린샷입니다.](../media/6-backend-pools.png)

1. <span data-ttu-id="d1223-113">**백 엔드 풀 추가** 블레이드에서 다음 정보를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-113">On the **Add backend pool** blade, add the following information:</span></span>
    - <span data-ttu-id="d1223-114">이름을 _woodgrove-BEP_로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-114">Name it _woodgrove-BEP_.</span></span>
    - <span data-ttu-id="d1223-115">풀을 **가용성 집합**에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-115">Associated the pool to an **Availability set**.</span></span>
    - <span data-ttu-id="d1223-116">가용성 집합에서는 _woodgrove-AS_를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-116">For the availability set, select _woodgrove-AS_.</span></span>

1. <span data-ttu-id="d1223-117">**대상 네트워크 IP 구성 추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-117">Click **Add a target network IP configuration**.</span></span>

1. <span data-ttu-id="d1223-118">**대상 가상 머신** 목록에서 _woodgrove-VM1_을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-118">In the **Target virtual machine** list, select _woodgrove-VM1_.</span></span>

1. <span data-ttu-id="d1223-119">VM에 대한 **네트워크 IP 구성** 목록에서 VM의 IP 주소 풀을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-119">In the **Network IP configuration** list for the VM, select the VM's IP address pool.</span></span>

1. <span data-ttu-id="d1223-120">이러한 단계를 반복하여 _woodgrove-VM2_ 및 _woodgrove-VM3_를 백 엔드 풀에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-120">Repeat those steps to add _woodgrove-VM2_ and _woodgrove-VM3_ to the backend pool.</span></span>

    ![선택한 세 가지 VM 모두를 사용하여 백 엔드 풀 추가 블레이드를 보여주는 스크린샷.](../media/6-add-backend-pool.png)

1. <span data-ttu-id="d1223-122">**확인**을 클릭하여 블레이드를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-122">Click **OK** to close the blade.</span></span>

<span data-ttu-id="d1223-123">부하 분산 장치 구성이 업데이트될 때까지 기다렸다가 연습을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-123">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="create-a-health-probe-for-the-load-balancer"></a><span data-ttu-id="d1223-124">부하 분산 장치에 대한 상태 프로브 만들기</span><span class="sxs-lookup"><span data-stu-id="d1223-124">Create a health probe for the load balancer</span></span>

<span data-ttu-id="d1223-125">다음으로, 포트 80을 통해 HTTP에 대한 상태 프로브를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-125">Next, add a health probe for HTTP over port 80.</span></span>

1. <span data-ttu-id="d1223-126">**woodgrove-LB** 블레이드의 **설정**에서 **상태 프로브**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-126">On the **woodgrove-LB** blade, under **Settings**, click **Health probes**.</span></span> <span data-ttu-id="d1223-127">현재 비어있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-127">Notice it's currently empty.</span></span>

1. <span data-ttu-id="d1223-128">새 상태 프로브를 추가하려면 **추가**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-128">Click **Add** to add a new health probe.</span></span>

1. <span data-ttu-id="d1223-129">**상태 프로브 추가** 블레이드에서 다음 구성을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-129">On the **Add health probe** blade, set the following configuration:</span></span>
    - <span data-ttu-id="d1223-130">**이름:** _woodgrove-HP_</span><span class="sxs-lookup"><span data-stu-id="d1223-130">**Name:** _woodgrove-HP_</span></span>
    - <span data-ttu-id="d1223-131">**프로토콜:** _HTTP_</span><span class="sxs-lookup"><span data-stu-id="d1223-131">**Protocol:** _HTTP_</span></span>
    - <span data-ttu-id="d1223-132">**포트:** _80_</span><span class="sxs-lookup"><span data-stu-id="d1223-132">**Port:** _80_</span></span>
    - <span data-ttu-id="d1223-133">**경로:** _/_</span><span class="sxs-lookup"><span data-stu-id="d1223-133">**Path:** _/_</span></span>
    - <span data-ttu-id="d1223-134">**간격:** _15_</span><span class="sxs-lookup"><span data-stu-id="d1223-134">**Interval:** _15_</span></span>
    - <span data-ttu-id="d1223-135">**비정상 임계값:** _2_</span><span class="sxs-lookup"><span data-stu-id="d1223-135">**Unhealthy threshold:** _2_</span></span>

1. <span data-ttu-id="d1223-136">**확인**을 클릭하여 변경 내용을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-136">Click **OK** to save the changes.</span></span>

<span data-ttu-id="d1223-137">부하 분산 장치 구성이 업데이트될 때까지 기다렸다가 연습을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-137">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="create-a-load-balancer-rule"></a><span data-ttu-id="d1223-138">부하 분산 장치 규칙 만들기</span><span class="sxs-lookup"><span data-stu-id="d1223-138">Create a load balancer rule</span></span>

<span data-ttu-id="d1223-139">마지막으로 포트 80을 통해 백 엔드 풀을 상태 프로브와 연결하는 HTTP에 대한 부하 분산 규칙을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-139">Finally, create a load-balancing rule for the HTTP over port 80, that associates the backend pool with the health probe.</span></span>

1. <span data-ttu-id="d1223-140">**woodgrove-LB** 블레이드의 **설정**에서 **부하 분산 규칙**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-140">On the **woodgrove-LB** blade, under **Settings**, click **Load balancing rules**.</span></span>

1. <span data-ttu-id="d1223-141">**추가**를 클릭하여 새 규칙을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-141">Click **Add** to add a new rule.</span></span>

1. <span data-ttu-id="d1223-142">**부하 분산 규칙 추가** 블레이드에서 **이름**을 _woodgrove-HTTP-LBRule_로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-142">On the **Add load balancing rule** blade, set the the **Name** to _woodgrove-HTTP-LBRule_.</span></span>

1. <span data-ttu-id="d1223-143">다음 정보가 자동으로 입력되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-143">Verify that the following information has been automatically entered:</span></span>
    - <span data-ttu-id="d1223-144">IP 버전: **IPv4**</span><span class="sxs-lookup"><span data-stu-id="d1223-144">IP Version: **IPv4**</span></span>
    - <span data-ttu-id="d1223-145">프런트 엔드 IP 주소: **LoadBalancerFrontEnd**</span><span class="sxs-lookup"><span data-stu-id="d1223-145">Frontend IP address: **LoadBalancerFrontEnd**</span></span>
    - <span data-ttu-id="d1223-146">프로토콜: **TCP**</span><span class="sxs-lookup"><span data-stu-id="d1223-146">Protocol: **TCP**</span></span>
    - <span data-ttu-id="d1223-147">포트: **80**</span><span class="sxs-lookup"><span data-stu-id="d1223-147">Port: **80**</span></span>
    - <span data-ttu-id="d1223-148">백 엔드 포트: **80**</span><span class="sxs-lookup"><span data-stu-id="d1223-148">Backend port: **80**</span></span>
    - <span data-ttu-id="d1223-149">백 엔드 풀: **woodgrove-BEP**</span><span class="sxs-lookup"><span data-stu-id="d1223-149">Backend pool: **woodgrove-BEP**</span></span>
    - <span data-ttu-id="d1223-150">상태 프로브: **woodgrove-HP**</span><span class="sxs-lookup"><span data-stu-id="d1223-150">Health probe: **woodgrove-HP**</span></span>
    - <span data-ttu-id="d1223-151">세션 지속성: **없음**</span><span class="sxs-lookup"><span data-stu-id="d1223-151">Session persistence: **None**</span></span>
    - <span data-ttu-id="d1223-152">유휴 제한 시간: **4분**</span><span class="sxs-lookup"><span data-stu-id="d1223-152">Idle timeout: **4 minutes**</span></span>
    - <span data-ttu-id="d1223-153">부동 IP: **사용 안 함**</span><span class="sxs-lookup"><span data-stu-id="d1223-153">Floating IP: **Disabled**</span></span>

1. <span data-ttu-id="d1223-154">**확인**을 클릭하여 규칙을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-154">Click **OK** to save the rule.</span></span>

<span data-ttu-id="d1223-155">부하 분산 장치 구성이 업데이트될 때까지 기다렸다가 연습을 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-155">Wait until the load balancer configuration has updated before proceeding with the exercise.</span></span>

## <a name="test-the-load-balancer"></a><span data-ttu-id="d1223-156">부하 분산 장치 테스트</span><span class="sxs-lookup"><span data-stu-id="d1223-156">Test the load balancer</span></span>

1. <span data-ttu-id="d1223-157">부하 분산 장치의 **개요** 페이지로 다시 전환하고 해당 페이지에서 **공용 IP 주소** 링크를 클릭하여 할당된 IP 주소를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-157">Switch back to the **Overview** page of the load balancer and click the **Public IP address** link on the page to get to the IP address assigned.</span></span> <span data-ttu-id="d1223-158">또는 **모든 리소스**를 사용한 다음, 리소스 목록에서 **woodgrove-LB-ip**를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-158">Alternatively, you can use **All resources** and then in the resource list, select **woodgrove-LB-ip**.</span></span>

1. <span data-ttu-id="d1223-159">**개요** 블레이드에서 **IP 주소**를 선택하고 그 옆에 있는 **복사** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-159">On the **Overview** blade, select the **IP address**, and click the **Copy** button next to it.</span></span> <span data-ttu-id="d1223-160">이 IP 주소는 부하 분산 장치에 대한 _공용_ IP 주소입니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-160">This is the _public_ IP address for the load balancer.</span></span>

    ![공용 IP 주소 개요 패널을 보여주는 스크린샷](../media/6-public-ip.png)

1. <span data-ttu-id="d1223-162">새 브라우저 탭을 열고 IP 주소를 브라우저의 주소 표시줄에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-162">Open a new browser tab and paste the IP address into the address bar of your browser.</span></span> <span data-ttu-id="d1223-163">서버의 이름을 확인하고 이 탭을 열어 둡니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-163">Note the name of the server and keep this tab open.</span></span>

1. <span data-ttu-id="d1223-164">Azure Portal의 왼쪽 메뉴에서 **모든 리소스**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-164">In the Azure portal, in the left menu, click **All resources**.</span></span> <span data-ttu-id="d1223-165">그런 다음, 리소스 목록에서 위에서 확인한 서버를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-165">Then, in the resource list, click the server you noted above.</span></span>

1. <span data-ttu-id="d1223-166">**개요** 블레이드에서 **중지**을 클릭한 다음, **예**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-166">On the **Overview** blade, click **Stop**, and then click **Yes**.</span></span>

1. <span data-ttu-id="d1223-167">VM이 중지될 때까지 기다린 다음, 3단계에서 본 탭으로 전환합니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-167">Wait until the VM has stopped, and then switch to the tab you viewed in step 3.</span></span> <span data-ttu-id="d1223-168">페이지를 새로 고칩니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-168">Refresh the page.</span></span>

1. <span data-ttu-id="d1223-169">이제 부하 분산 장치가 HTTP 요청을 다른 VM 중 하나로 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-169">The load balancer will now send your HTTP request to one of your other VMs.</span></span>

<span data-ttu-id="d1223-170">이 연습에서는 백 엔드 VM과 부하 분산 장치의 배포를 완료했습니다.</span><span class="sxs-lookup"><span data-stu-id="d1223-170">In this exercise, you completed the deployment of your backend VMs and the load balancer.</span></span>
