<span data-ttu-id="66923-101">부하 분산 장치가 올바르게 작동하려면 부하 분산 장치의 동작을 제어하는 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-101">Before the load balancer will function correctly, you must configure settings that control the load balancer's behavior.</span></span> <span data-ttu-id="66923-102">여기서는 네트워크, 상태 프로브, 보안 규칙, 부하 분산 장치 규칙 및 서버 풀을 구성하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="66923-102">Here, you will look at configuring the network, health probe, security rules, load-balancing rules, and server pool.</span></span>

## <a name="steps-for-configuring-a-basic-public-load-balancer"></a><span data-ttu-id="66923-103">기본 공용 부하 분산 장치 구성 단계</span><span class="sxs-lookup"><span data-stu-id="66923-103">Steps for configuring a basic public load balancer</span></span>

<span data-ttu-id="66923-104">다음은 기본 공용 부하 분산 장치에 대한 기본 구성 단계의 개요입니다.</span><span class="sxs-lookup"><span data-stu-id="66923-104">The following is an overview of the main configuration steps for a basic public load balancer.</span></span> <span data-ttu-id="66923-105">표준 부하 분산 장치 및 내부 부하 분산 장치의 단계는 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-105">The steps for a standard load balancer and for an internal load balancer will be similar.</span></span> <span data-ttu-id="66923-106">기본적으로 설정해야 할 네 가지 사항은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="66923-106">There are essentially four things we need to setup:</span></span>

- <span data-ttu-id="66923-107">요청을 처리하기 위한 백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="66923-107">Backend servers to process requests</span></span>
- <span data-ttu-id="66923-108">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="66923-108">Public IP address</span></span>
- <span data-ttu-id="66923-109">상태 프로브</span><span class="sxs-lookup"><span data-stu-id="66923-109">Health probe</span></span>
- <span data-ttu-id="66923-110">부하 분산 장치 규칙</span><span class="sxs-lookup"><span data-stu-id="66923-110">Load balancer rules</span></span>

### <a name="backend-servers"></a><span data-ttu-id="66923-111">백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="66923-111">Backend servers</span></span>

<span data-ttu-id="66923-112">먼저 백 엔드 VM 풀을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-112">First, you need to configure your backend VM pool.</span></span> <span data-ttu-id="66923-113">VM은 동일한 가용성 집합에 있고 고유한 공용 IP 주소를 가져야 합니다(실제로 공용 엔드포인트에서 사용되지는 않음).</span><span class="sxs-lookup"><span data-stu-id="66923-113">The VMs should be in the same availability set and have their own public IP address (although this will not actually be used by your public endpoints).</span></span>

<span data-ttu-id="66923-114">새 가상 네트워크를 만들고 사용할 VM 풀의 서브넷을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-114">You must create a new virtual network and define a subnet for the VM pool to use.</span></span>

 <span data-ttu-id="66923-115">동일한 서비스를 제공하는 VM이 여러 개 있는 경우 실제 부하 분산 장치의 일부가 아니더라도 VM 풀에서 동일한 방화벽 규칙이 적용되도록 **NSG(네트워크 보안 그룹)** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-115">When you have multiple VMs providing the same services, you should use a **network security group (NSG)** to ensure that the same firewall rules are in place across the VM pool (although this is not part of the actual load-balancing process).</span></span> <span data-ttu-id="66923-116">예를 들어 웹 응용 프로그램을 호스트하는 VM의 경우 HTTP용 포트 80 또는 HTTPS용 포트 8080에서 인바운드 보안 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-116">For example, for VMs hosting web applications, you will need to create inbound security rules on port 80 for HTTP or port 8080 for HTTPS.</span></span>

### <a name="public-ip-address"></a><span data-ttu-id="66923-117">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="66923-117">Public IP address</span></span>

<span data-ttu-id="66923-118">포털을 사용하여 공용 기본 부하 분산 장치를 만들 때 부하 분산 장치 프런트 엔드로 **공용 IP 주소**가 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="66923-118">When you create a public basic load balancer using the portal, the **public IP address** is automatically configured as the load balancer front end.</span></span>

<span data-ttu-id="66923-119">부하 분산 장치를 구성할 때 **백 엔드 주소 풀**도 구성해야 합니다. 이 풀은 부하 분산 장치에 연결되고 VM에 트래픽을 분산하는 데 사용되는 각 VM의 가상 NIC IP 주소를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="66923-119">Part of the configuration of the load balancer is the **backend address pool**, containing the IP addresses of each VM's virtual NICs that are connected to the load balancer and used to distribute traffic to the VMs.</span></span>

### <a name="health-probe"></a><span data-ttu-id="66923-120">상태 프로브</span><span class="sxs-lookup"><span data-stu-id="66923-120">Health probe</span></span>

<span data-ttu-id="66923-121">상태 프로브는 상태 검사에 따라 부하 분산 장치 순환에서 VM을 동적으로 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-121">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span> <span data-ttu-id="66923-122">기본적으로 프로브 시도 간격은 15초입니다.</span><span class="sxs-lookup"><span data-stu-id="66923-122">By default, there are 15 seconds between probe attempts.</span></span> <span data-ttu-id="66923-123">두 번의 연속적인 프로브 실패 후 VM은 비정상으로 간주되고 서버가 다시 온라인 상태가 될 때까지 트래픽은 라우팅되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="66923-123">After two consecutive probe failures, a VM is considered unhealthy and traffic won't be routed there until the server comes back online.</span></span>

### <a name="rules"></a><span data-ttu-id="66923-124">규칙</span><span class="sxs-lookup"><span data-stu-id="66923-124">Rules</span></span>

<span data-ttu-id="66923-125">부하 분산 장치 규칙은 부하 분산 장치가 수신 대기 중인 포트와 트래픽을 백 엔드 VM 집합으로 보내는 데 사용되는 포트를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-125">The load balancer rules identify the port(s) that the load balancer is listening on, and the port(s) used to send traffic to the back end set of VMs.</span></span> <span data-ttu-id="66923-126">트래픽을 라우팅하려면 하나 이상의 규칙이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="66923-126">You need at least one rule to route traffic.</span></span>
