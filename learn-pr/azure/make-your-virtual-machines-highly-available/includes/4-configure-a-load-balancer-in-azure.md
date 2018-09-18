<span data-ttu-id="77753-101">부하 분산 장치가 올바르게 작동하려면 부하 분산 장치의 동작을 제어하는 설정을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-101">Before the load balancer will function correctly, you must configure settings that control the load balancer's behavior.</span></span> <span data-ttu-id="77753-102">여기서는 네트워크, 상태 프로브, 보안 규칙, 부하 분산 규칙 및 서버 풀을 구성하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="77753-102">Here, you will look at configuring the network, health probe, security rules, load-balancing rules, and server pool.</span></span>

## <a name="steps-to-configure-a-basic-public-load-balancer"></a><span data-ttu-id="77753-103">기본 공용 Load Balancer를 구성하는 단계</span><span class="sxs-lookup"><span data-stu-id="77753-103">Steps to configure a Basic Public Load Balancer</span></span>

<span data-ttu-id="77753-104">다음은 기본 공용 Load balancer의 주요 구성 단계 개요입니다. 표준 Load Balancer와 내부용 Load Balancer의 단계는 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-104">The following is an overview of the main configuration steps for a Basic Public Load balancer; the steps for a Standard Load Balancer, and for an internal Load Balancer will be similar.</span></span>

### <a name="backend-servers"></a><span data-ttu-id="77753-105">백 엔드 서버</span><span class="sxs-lookup"><span data-stu-id="77753-105">Backend servers</span></span>

<span data-ttu-id="77753-106">먼저 백 엔드 VM 풀을 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-106">First, you need to configure your backend VM pool.</span></span> <span data-ttu-id="77753-107">VM이 동일한 가용성 집합에 있고 고유한 공용 IP 주소를 가져야 합니다(실제로 공용 엔드포인트에서 사용되지는 않음).</span><span class="sxs-lookup"><span data-stu-id="77753-107">The VMs should be in the same availability set and have their own public IP address (although this will not actually be used by your public endpoints).</span></span>

<span data-ttu-id="77753-108">새 가상 네트워크(vNet)를 만들고, 사용할 VM 풀의 서브넷을 정의해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-108">You must create a new virtual network (vNet), and define a subnet for the VM pool to use.</span></span>

<span data-ttu-id="77753-109">부하 분산에 직접 포함되지는 않지만, 동일한 서비스를 제공하는 VM이 여러 개 있는 경우 VM 풀에서 동일한 방화벽 규칙이 적용되도록 **NSG(네트워크 보안 그룹)** 를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-109">While not part of load balancing directly, when you have multiple VMs providing the same services, you should use a **Network Security Group (NSG)** to ensure that the same firewall rules are in place across the VM pool.</span></span> <span data-ttu-id="77753-110">예를 들어 웹 응용 프로그램을 호스트하는 VM의 경우 HTTP용 포트 80 또는 HTTPS용 포트 8080에서 인바운드 보안 규칙을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-110">For example, for VMs hosting web applications, you will need to create inbound security rules on port 80 for HTTP or port 8080 for HTTPS.</span></span>

### <a name="public-ip-address"></a><span data-ttu-id="77753-111">공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="77753-111">Public IP address</span></span>

<span data-ttu-id="77753-112">포털을 사용하여 공용 기본 부하 분산 장치를 만들 때 부하 분산 장치의 프런트 엔드로 **공용 IP 주소**가 자동으로 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="77753-112">When you create a public Basic load balancer using the portal, the **public IP address** is automatically configured as the load balancer's front end.</span></span>

<span data-ttu-id="77753-113">부하 분산 장치를 구성할 때 **백 엔드 주소 풀**도 구성해야 합니다. 이 풀은 부하 분산 장치에 연결되고 VM에 트래픽을 분산하는 데 사용되는 각 VM의 가상 NIC IP 주소를 포함하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="77753-113">Part of the configuration of the load balancer is the **backend address pool**, containing the IP addresses of each VM's virtual NICs that are connected to the load balancer and used to distribute traffic to the VMs.</span></span> 

### <a name="health-probe"></a><span data-ttu-id="77753-114">상태 프로브</span><span class="sxs-lookup"><span data-stu-id="77753-114">Health probe</span></span>

<span data-ttu-id="77753-115">상태 프로브는 상태 검사에 따라 부하 분산 장치 순환에서 VM을 동적으로 추가하거나 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-115">The health probe dynamically adds or removes VMs from the load balancer rotation based on their response to health checks.</span></span>
<span data-ttu-id="77753-116">기본적으로 15초 간격으로 프로브 시도가 이루어지며 두 개의 프로브가 연속으로 실패하면 VM이 비정상 상태로 간주됩니다.</span><span class="sxs-lookup"><span data-stu-id="77753-116">By default, there are 15 seconds between probe attempts, and after two consecutive probe failures a VM is considered unhealthy.</span></span>

### <a name="rules"></a><span data-ttu-id="77753-117">규칙</span><span class="sxs-lookup"><span data-stu-id="77753-117">Rules</span></span>

<span data-ttu-id="77753-118">부하 분산 장치 규칙은 프런트 엔드가 수신 대기하는 포트와 백 엔드에 트래픽을 보내는 데 사용되는 포트를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="77753-118">The load balancer rule specifies the port that the frontend is listening on, and the port used to send traffic to the backend.</span></span>