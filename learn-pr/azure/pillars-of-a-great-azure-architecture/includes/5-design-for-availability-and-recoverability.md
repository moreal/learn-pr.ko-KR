<span data-ttu-id="a31d8-101">조직의 임상 전문가는 가동 중지 시간을 허용하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-101">Clinicians at your organization have little tolerance for downtime.</span></span> <span data-ttu-id="a31d8-102">응용 프로그램은 사용자에게 영향을 최소화하면서 오류를 처리할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-102">Applications must be able to handle failures with minimal impact to their users.</span></span> <span data-ttu-id="a31d8-103">해당 응용 프로그램이 지역화된 인시던트 및 대규모 재해 모두에 대해 작동을 유지하도록 어떻게 보장하나요?</span><span class="sxs-lookup"><span data-stu-id="a31d8-103">How do they ensure their applications remain operational, both for localized incidents and large-scale disasters?</span></span> 

<span data-ttu-id="a31d8-104">여기에서 아키텍처 설계에 가용성 및 복구 기능을 포함시키는 방법을 설명하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-104">Here, we'll talk through how to include availability and recoverability in your architecture design.</span></span>

## <a name="availability-and-recoverability"></a><span data-ttu-id="a31d8-105">가용성 및 복구 기능</span><span class="sxs-lookup"><span data-stu-id="a31d8-105">Availability and recoverability</span></span>

<span data-ttu-id="a31d8-106">복잡한 응용 프로그램의 많은 작업은 규모에 관계 없이 잘못될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-106">In a complex application, any number of things can go wrong at any scale.</span></span> <span data-ttu-id="a31d8-107">개별 서버 및 하드 드라이브가 실패할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-107">Individual servers and hard drives can fail.</span></span> <span data-ttu-id="a31d8-108">배포 문제로 인해 데이터베이스의 모든 테이블이 의도치 않게 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-108">A deployment issue could unintentionally drop all tables in a database.</span></span> <span data-ttu-id="a31d8-109">전체 데이터 센터에 연결할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-109">Whole datacenters may become unreachable.</span></span> <span data-ttu-id="a31d8-110">랜섬웨어 인시던트는 모든 데이터를 악의적으로 암호화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-110">A ransomware incident could maliciously encrypt all your data.</span></span>

<span data-ttu-id="a31d8-111">*가용성*을 위한 설계는 부분 네트워크 중단 같은 소규모 인시던트 및 임시 조건을 통해 작동 시간을 유지하는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-111">Designing for *availability* focuses on maintaining uptime through small-scale incidents and temporary conditions like partial network outages.</span></span> <span data-ttu-id="a31d8-112">고가용성을 응용 프로그램의 각 구성 요소에 통합하고 단일 실패 지점을 제거하여 응용 프로그램이 지역화된 오류를 처리할 수 있도록 보장합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-112">You can ensure your application can handle localized failures by integrating high availability into each component of an application and eliminating single points of failure.</span></span> <span data-ttu-id="a31d8-113">또한 이러한 설계는 인프라 유지 관리의 영향을 최소화합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-113">Such a design also minimizes the impact of infrastructure maintenance.</span></span> <span data-ttu-id="a31d8-114">고가용성 설계는 일반적으로 신속하고 자동으로 문제를 해결하는 것을 목적으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-114">High-availability designs typically aim to solve problems quickly and automatically.</span></span>

<span data-ttu-id="a31d8-115">*복구 기능*을 위한 설계는 데이터 손실 및 더 큰 규모의 재해에서의 복구에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-115">Designing for *recoverability* focuses on recovery from data loss and from larger scale disasters.</span></span> <span data-ttu-id="a31d8-116">이러한 유형의 인시던트에서의 복구는 자동이 아니며, 어느 정도의 가동 중지 시간 또는 영구적인 데이터 손실로 이어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-116">Recovery from these types of incidents isn't automatic, and may result in some amount of downtime or permanently lost data.</span></span> <span data-ttu-id="a31d8-117">재해 복구는 실행 못지않게 신중한 계획이 중요합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-117">Disaster recovery is as much about careful planning as it is about execution.</span></span>

<span data-ttu-id="a31d8-118">아키텍처 설계에 고가용성 및 복구 기능을 포함시키면 사업을 가동 중지 시간 및 손실된 데이터로 인한 재정적 손실에서 보호해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-118">Including high availability and recoverability in the design of your architecture protects your business from financial losses resulting from downtime and lost data.</span></span> <span data-ttu-id="a31d8-119">사용자의 명성이 고객의 신뢰 상실로 부정적 영향을 받지 않도록 보장해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-119">They ensure your reputation isn't negatively impacted by a loss of trust from your customers.</span></span>

## <a name="architecting-for-availability-and-recoverability"></a><span data-ttu-id="a31d8-120">가용성 및 복구 기능을 위한 아키텍처</span><span class="sxs-lookup"><span data-stu-id="a31d8-120">Architecting for availability and recoverability</span></span>

<span data-ttu-id="a31d8-121">가용성 및 복구 기능을 위한 아키텍처는 응용 프로그램이 고객에게 한 약속을 충족할 수 있도록 보장해줍니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-121">Architecting for availability and recoverability ensures that your application can meet the commitments you make to your customers.</span></span>

<span data-ttu-id="a31d8-122">가용성의 경우에는 커밋하고 있는 SLA(서비스 수준 약정)를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-122">For availability, identify the service-level agreement (SLA) you're committing to.</span></span> <span data-ttu-id="a31d8-123">SLA 관련 응용 프로그램의 잠재적인 고가용성 기능을 검사하고 적절한 검사가 있는지 및 개선해야 하는지 여부를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-123">Examine the potential high-availability capabilities of your application relative to your SLA, and identify where you have proper coverage and where you'll need to make improvements.</span></span> <span data-ttu-id="a31d8-124">아키텍처의 구성 요소에 중복성을 추가하는 것이 목표이므로 중단이 발생할 가능성이 별로 없습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-124">The goal is to add redundancy to components of the architecture so that you are less likely to experience an outage.</span></span> <span data-ttu-id="a31d8-125">고가용성 설계 구성 요소의 예제로는 클러스터링 및 부하 분산이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-125">Examples of high-availability design components include clustering and load balancing.</span></span> <span data-ttu-id="a31d8-126">클러스터링은 단일 VM을 조정된 VM 집합으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-126">Clustering replaces a single VM with a set of coordinated VMs.</span></span> <span data-ttu-id="a31d8-127">하나의 VM이 실패하거나 연결될 수 없는 경우 서비스는 요청을 처리할 수 있는 다른 VM을 장애 조치(failover)할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-127">When one VM fails or becomes unreachable, services can fail over to another one that can service the requests.</span></span> <span data-ttu-id="a31d8-128">부하 분산은 서비스의 많은 인스턴스에 요청을 분산하면서 실패한 인스턴스를 검색하고 해당 인스턴스로 요청이 라우팅되지 않도록 방지합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-128">Load balancing spreads requests across many instances of a service, detecting failed instances and preventing requests from being routed to them.</span></span>

<span data-ttu-id="a31d8-129">복구 기능의 경우에는 가능한 데이터 손실 및 주요 가동 중지 시간 시나리오를 검사하는 분석을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-129">For recoverability, perform an analysis that examines possible data loss and major downtime scenarios.</span></span> <span data-ttu-id="a31d8-130">분석에는 복구 전략에 대한 탐색 및 각 전략에 대한 비용과 편익 간 균형 유지가 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-130">The analysis should include an exploration of recovery strategies and the cost-benefit tradeoff for each.</span></span> <span data-ttu-id="a31d8-131">이 연습에서는 조직의 우선 순위에 대한 중요한 인사이트를 제공하며 응용 프로그램의 역할을 명확하게 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-131">This exercise will give you important insight into your organization's priorities and help clarify the role of your application.</span></span> <span data-ttu-id="a31d8-132">결과에는 응용 프로그램의 복구 지점 목표(RPO) 및 복구 시간 목표(RTO) 또는 재해 복구에 대한 투자를 고려해 볼 때 허용될 수 있는 최고 수준의 데이터 손실 및 가동 중지 시간이 포함되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-132">The results should include the application's recovery point objective (RPO) and recovery time objective (RTO), or the maximum levels of data loss and downtime deemed acceptable given the investment made in disaster recovery.</span></span> <span data-ttu-id="a31d8-133">RPO 및 RTO를 정의했으면 백업을 설계하고, 기능을 데이터 손실을 보호하는 아키텍처 및 가동 중지 시간을 완화하는 복제로 복구할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-133">With RPO and RTO defined, you can design backup and restore capabilities into your architecture to cover for data loss, and replication to mitigate downtime.</span></span>

<span data-ttu-id="a31d8-134">모든 클라우드 공급자는 응용 프로그램의 가용성 및 복구 기능을 개선하는 데 사용할 수 있는 서비스 및 기능 모음을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-134">Every cloud provider offers a suite of services and features you can use to improve your application's availability and recoverability.</span></span> <span data-ttu-id="a31d8-135">가능하면 기존 서비스 및 모범 사례를 사용하고 직접 만들어 사용하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="a31d8-135">When possible, use existing services and best practices, and try to resist creating your own.</span></span>

<span data-ttu-id="a31d8-136">하드 드라이브에 장애가 발생할 수 있고, 데이터 센터에 연결할 수 없고, 해커의 공격이 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-136">Hard drives can fail, datacenters can become unreachable, and hackers can attack.</span></span> <span data-ttu-id="a31d8-137">가용성 및 복구 기능을 사용하여 고객과 좋은 평판을 유지 관리하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-137">It's important that you maintain a good reputation with your customers using availability and recoverability.</span></span> <span data-ttu-id="a31d8-138">가용성은 네트워크 중단 등의 조건을 통한 가동 시간의 유지 관리에 중점을 두며, 복구 기능은 재해 발생 후 데이터 검색에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="a31d8-138">Availability focuses on maintaining uptime through conditions like network outages, and recoverability focuses on retrieving data after a disaster.</span></span>