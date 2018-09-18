<span data-ttu-id="32b92-101">보안과 관련된 가장 큰 문제 중 하나는 보호할 모든 영역을 살펴보고 해커보다 먼저 취약점을 찾아내는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-101">One of the biggest problems with security is being able to see all the areas you need to protect and to find vulnerabilities before hackers do.</span></span> <span data-ttu-id="32b92-102">Azure는 이 작업을 훨씬 쉽게 할 수 있는 Azure Security Center라고 하는 서비스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-102">Azure provides a service which makes this much easier called Azure Security Center.</span></span>

## <a name="what-is-azure-security-center"></a><span data-ttu-id="32b92-103">Azure Security Center란?</span><span class="sxs-lookup"><span data-stu-id="32b92-103">What is Azure Security Center?</span></span>

<span data-ttu-id="32b92-104">ASC(Azure Security Center)는 Azure와 온-프레미스의 모든 서비스에 대한 위협 보호를 제공하는 모니터링 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-104">Azure Security Center (ASC) is a monitoring service that provides threat protection across all of your services both in Azure, and on-premises.</span></span> <span data-ttu-id="32b92-105">다음과 같은 기능이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-105">It can:</span></span>

- <span data-ttu-id="32b92-106">구성, 리소스 및 네트워크를 기반으로 보안 권장 사항을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-106">Provide security recommendations based on your configurations, resources, and networks.</span></span>
- <span data-ttu-id="32b92-107">온-프레미스 및 클라우드 워크로드의 보안 설정을 모니터링하면서 새 서비스가 온라인으로 전환되면 필요한 보안을 자동으로 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-107">Monitor security settings across on-premises and cloud workloads and automatically apply required security to new services as they come online.</span></span>
- <span data-ttu-id="32b92-108">모든 서비스를 지속적으로 모니터링하면서 자동 보안 평가를 수행하여 잠재적 취약점이 악용되기 전에 미리 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-108">Continuously monitor all your services and perform automatic security assessments to identify potential vulnerabilities before they can be exploited.</span></span>
- <span data-ttu-id="32b92-109">기계 학습을 사용하여 맬웨어를 검색하고 서비스 및 가상 머신에 설치되지 않도록 차단합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-109">Use machine learning to detect and block malware from being installed in your services and virtual machines.</span></span> <span data-ttu-id="32b92-110">또한 유효성을 검사한 앱만 실행할 수 있도록 응용 프로그램 허용 목록을 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-110">You can also white-list applications to ensure that only the apps you validate are allowed to execute.</span></span>
- <span data-ttu-id="32b92-111">잠재적 인바운드 공격을 분석 및 식별하고, 발생했을지도 모르는 위협 및 게시물 보안 위반 활동을 조사합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-111">Analyze and identify potential inbound attacks and help to investigate threats and any post-breach activity which might have occurred.</span></span>
- <span data-ttu-id="32b92-112">포트에 대한 Just-In-Time 액세스 제어를 통해 필요한 트래픽만 네트워크에서 허용하여 공격 노출 영역을 줄입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-112">Just-In-Time access control for ports, reducing your attack surface by ensuring the network only allows traffic you require.</span></span>

<span data-ttu-id="32b92-113">ASC는 [CIS(Center for Internet Security)](https://www.cisecurity.org/cis-benchmarks/) 권장 사항의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-113">ASC is part of the [Center for Internet Security](https://www.cisecurity.org/cis-benchmarks/) (CIS) recommendations.</span></span>

## <a name="activating-azure-security-center"></a><span data-ttu-id="32b92-114">Azure Security Center 활성화</span><span class="sxs-lookup"><span data-stu-id="32b92-114">Activating Azure Security Center</span></span>

<span data-ttu-id="32b92-115">ASC의 이점을 고려하여 회사의 보안 팀에서는 사무실의 모든 구독에서 ASC를 켜기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-115">Given the benefits of ASC, the security team at your company has decided that it be turned on for all subscriptions at your office.</span></span> <span data-ttu-id="32b92-116">여러분은 오늘 아침에 응용 프로그램에서 ASC를 켜라는 이메일을 받았습니다. 지금부터 그 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-116">You got an email this morning to turn it on for your applications - so let's look at how to do that.</span></span>

1. <span data-ttu-id="32b92-117">[Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 왼쪽 메뉴에서 **Azure Security Center**를 선택합니다. 이 위치에서 Azure Security Center가 보이지 않으면 아래 그림처럼 보안 섹션에서 **모든 서비스**를 선택하고 **Security Center**를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-117">Open the [Azure portal](https://portal.azure.com?azure-portal=true) and select **Azure Security Center** from the left hand menu, if you don't see it there, you can select **All services** and find **Security Center** in the security section as shown below.</span></span>

![Azure Security Center 열기](../media-draft/ASC-Menu.png)

2. <span data-ttu-id="32b92-119">ASC를 한 번도 열지 않은 경우 블레이드가 **시작** 항목에서 시작되고 구독을 업그레이드하라는 요청이 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-119">If you have never opened ASC, the blade will start on the **Getting started** entry which might ask you to upgrade your subscription.</span></span> <span data-ttu-id="32b92-120">지금은 이 요청을 무시하고, 페이지 맨 아래에서 **건너뛰기**를 선택한 다음, **개요**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-120">Ignore that for now, select **Skip** at the bottom of the page, and then select **Overview**.</span></span>
    - <span data-ttu-id="32b92-121">그러면 구독에서 사용할 수 있는 모든 요소에서 "보안 큰 그림"이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-121">This will display the "big security picture" across all the elements available in your subscription.</span></span>
    - <span data-ttu-id="32b92-122">여기서 수많은 유용한 정보를 탐색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-122">This has a ton of great information you can explore.</span></span>

3. <span data-ttu-id="32b92-123">다음으로, "정책 및 규정 준수" 아래에서 **적용 범위**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-123">Next, select **Coverage**, under "Policy and Compliance".</span></span> <span data-ttu-id="32b92-124">그러면 ACS의 범위에 포함되는(또는 포함되지 않는) 구독 요소가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-124">This will display what subscription elements are being covered (or not covered) by ACS.</span></span> <span data-ttu-id="32b92-125">여기서 액세스 권한이 있는 구독에 대해 ACS을 켤 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-125">Here you can turn on ACS for any subscription you have access to.</span></span> <span data-ttu-id="32b92-126">"포함되지 않음", "기본 범위", "표준 범위"의 세 가지 범위 영역 사이에서 전환해 보세요.</span><span class="sxs-lookup"><span data-stu-id="32b92-126">Try switching between the three coverage areas: "Not covered", "Basic coverage" and "Standard coverage".</span></span>

4. <span data-ttu-id="32b92-127">포함되지 않는 구독에는 ACS를 활성화하라는 프롬프트가 생길 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-127">Subscriptions that are not covered will have a prompt to activate ACS.</span></span> <span data-ttu-id="32b92-128">"지금 업그레이드" 단추를 눌러 구독의 모든 리소스에 ACS를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-128">You can press the "Upgrade Now" button to enable ACS for all the resources in the subscription.</span></span>

![적용 범위 업그레이드](../media-draft/Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a><span data-ttu-id="32b92-130">체험 계층과 표준 계층의 차이점</span><span class="sxs-lookup"><span data-stu-id="32b92-130">Free vs. Standard pricing tier</span></span>

<span data-ttu-id="32b92-131">ASC에 Azure 체험 계층을 사용할 수 있지만, Azure 리소스의 평가 및 권장 사항으로 제한됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-131">While you can use a free Azure subscription tier with ASC, it is limited to assessments and recommendations of Azure resources only.</span></span> <span data-ttu-id="32b92-132">ASC를 제대로 활용하려면 위와 같이 표준 계층 구독으로 업그레이드해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-132">To really leverage ASC, you will need to upgrade to a Standard tier subscription as shown above.</span></span> <span data-ttu-id="32b92-133">위에서 언급했듯이 **적용 범위** 블레이드의 "지금 업그레이드" 단추를 통해 구독을 업그레이드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-133">You can upgrade your subscription through the "Upgrade Now" button in the **Coverage** blade as noted above.</span></span> <span data-ttu-id="32b92-134">구독 수준을 변경하는 방법을 안내하는 ASC 메뉴에서 **시작** 블레이드로 전환할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-134">You can also switch to the **Getting Started** blade in the ASC menu which will walk you through changing your subscription level.</span></span> <span data-ttu-id="32b92-135">가격 및 기능은 지역에 따라 달라질 수 있으며, 전체 내용은 [가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/security-center/)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-135">The pricing and features may change based on the region, you can get a full overview on the [pricing page](https://azure.microsoft.com/en-us/pricing/details/security-center/).</span></span> 

> [!NOTE]
> <span data-ttu-id="32b92-136">구독을 표준 계층으로 업그레이드하려면 구독 소유자, 구독 기여자 또는 보안 관리자 역할이 할당되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-136">To upgrade a subscription to the Standard tier, you must be assigned the role of Subscription Owner, Subscription Contributor, or Security Admin.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="32b92-137">60일 평가판 기간이 끝나면 **노드당 매월 $15**의 ASC 사용 요금이 계정에 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-137">After the 60-day trial period is over, ASC is priced at **$15/node per month** and will be billed to your account.</span></span>

## <a name="turning-off-azure-security-center"></a><span data-ttu-id="32b92-138">Azure Security Center 끄기</span><span class="sxs-lookup"><span data-stu-id="32b92-138">Turning off Azure Security Center</span></span>

<span data-ttu-id="32b92-139">프로덕션 시스템의 경우 모든 리소스를 모니터링하여 위협을 감지할 수 있도록 Azure Security Center를 계속 사용할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-139">For production systems, you will definitely want to keep Azure Security Center turned on so it can monitor all your resources for threats.</span></span> <span data-ttu-id="32b92-140">하지만 ASC를 시험해 보려고 잠시 켠 경우 요금이 부과되지 않도록 다시 끄는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-140">However, if you are just playing with ASC and turned it on, you will likely want to disable it to ensure you are not charged.</span></span> <span data-ttu-id="32b92-141">그 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-141">Let's do that now.</span></span>

1. <span data-ttu-id="32b92-142">[Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 왼쪽 메뉴에서 **Azure Security Center**를 선택합니다. 이 위치에서 Azure Security Center가 보이지 않으면 아래 그림처럼 보안 섹션에서 **모든 서비스**를 선택하고 **Security Center**를 찾아봅니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-142">Open the [Azure portal](https://portal.azure.com?azure-portal=true) and select **Azure Security Center** from the left hand menu, if you don't see it there, you can select **All services** and find **Security Center** in the security section as shown below.</span></span>

![Azure Security Center 열기](../media-draft/ASC-Menu.png)

2. <span data-ttu-id="32b92-144">왼쪽 메뉴에서 **보안 정책**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-144">Select **Security Policy** from the left hand menu.</span></span>

3. <span data-ttu-id="32b92-145">다음으로, ASC를 다운그레이드할 구독 옆에서 **설정 편집 >** 을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-145">Next, select **Edit settings >**, next to the subscription for which you want to downgrade ASC.</span></span>

4. <span data-ttu-id="32b92-146">그 다음 화면의 왼쪽 메뉴에서 "가격 책정 계층"을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-146">On the next screen select "Pricing Tier" from the left hand menu.</span></span>

5. <span data-ttu-id="32b92-147">아래 이미지와 비슷한 새 페이지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-147">A new page will appear that looks like the image below.</span></span> <span data-ttu-id="32b92-148">왼쪽에서 "체험(Azure 리소스만 해당)"이라고 적힌 상자를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-148">Click on the box on the left that says "Free (for Azure resources only)".</span></span>

![가격 책정 계층](../media-draft/Pricing-Tier.png)

6. <span data-ttu-id="32b92-150">화면 위쪽에서 "저장" 단추를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-150">Press the "save" button at the top of the screen.</span></span>

<span data-ttu-id="32b92-151">이제 구독이 Azure Security Center 체험 계층으로 다운그레이드되었습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-151">You have now downgraded your subscription to the free tier of Azure Security Center.</span></span>

## <a name="knowledge-check"></a><span data-ttu-id="32b92-152">지식 검사</span><span class="sxs-lookup"><span data-stu-id="32b92-152">Knowledge Check</span></span>
<span data-ttu-id="32b92-153"><!-- TODO: move into yaml --> ASC 기능을 모두 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="32b92-153"><!-- TODO: move into yaml --> Put a checkmark next to all ASC features.</span></span>

* <span data-ttu-id="32b92-154">권장 사항(정답)</span><span class="sxs-lookup"><span data-stu-id="32b92-154">Recommendations (correct)</span></span>
* <span data-ttu-id="32b92-155">마이그레이션(오답)</span><span class="sxs-lookup"><span data-stu-id="32b92-155">Mitigations (false)</span></span>
* <span data-ttu-id="32b92-156">방어(오답)</span><span class="sxs-lookup"><span data-stu-id="32b92-156">Defenses (false)</span></span>
* <span data-ttu-id="32b92-157">Just In Time(정답)</span><span class="sxs-lookup"><span data-stu-id="32b92-157">Just In Time (True)</span></span>
* <span data-ttu-id="32b92-158">위협 검색(정답)</span><span class="sxs-lookup"><span data-stu-id="32b92-158">Threat Detection (true)</span></span>

## <a name="summary"></a><span data-ttu-id="32b92-159">요약</span><span class="sxs-lookup"><span data-stu-id="32b92-159">Summary</span></span>

<span data-ttu-id="32b92-160"><!-- TODO: need link to module --> 축하합니다. 응용 프로그램, 데이터 및 네트워크를 보호하기 위한 첫 번째(그리고 가장 중요한) 단계가 끝났습니다.</span><span class="sxs-lookup"><span data-stu-id="32b92-160"><!-- TODO: need link to module --> Congratulations, you have taken your first (and most important) step to securing your application, data and network!</span></span> <!--If you want to learn more about Azure Security Center, you can go through the **Protect your resources with Azure Security Center** learning module.-->
