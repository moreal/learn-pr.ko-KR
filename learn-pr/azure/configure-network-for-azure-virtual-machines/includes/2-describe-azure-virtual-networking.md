<span data-ttu-id="d1f83-101">유지하려는 온-프레미스 데이터 센터가 있지만 Azure에서 호스팅된 VM(가상 머신)을 사용하여 급증한 트래픽을 오프로드하기 위해 Azure를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-101">You have an on-premises datacenter that you plan to keep, but you want to use Azure to offload peak traffic using virtual machines (VMs) hosted in Azure.</span></span> <span data-ttu-id="d1f83-102">기존 IP 주소 지정 스키마 및 네트워크 어플라이언스를 유지할 수 있는지를 알고 데이터 전송이 안전한지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-102">You need to know if you can keep your existing IP addressing scheme and network appliances, while ensuring that any data transfer is secure.</span></span>

## <a name="what-is-azure-virtual-networking"></a><span data-ttu-id="d1f83-103">Azure 가상 네트워킹이란?</span><span class="sxs-lookup"><span data-stu-id="d1f83-103">What is Azure virtual networking?</span></span>

<span data-ttu-id="d1f83-104">**Azure 가상 네트워크**를 사용하면 가상 머신, 웹앱 및 데이터베이스와 같은 Azure 리소스가 인터넷의 사용자 및 온-프레미스 클라이언트 컴퓨터와 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-104">**Azure virtual networks** enable Azure resources, such as virtual machines, web apps, and databases, to communicate with: each other, users on the internet, and on-premises client computers.</span></span> <span data-ttu-id="d1f83-105">Azure 네트워크를 다른 Azure 리소스와 연결되는 리소스 집합으로 생각할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-105">You can think of an Azure network as a set of resources that links other Azure resources.</span></span>

<span data-ttu-id="d1f83-106">Azure 가상 네트워크는 주요 네트워킹 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-106">Azure virtual networks provide key networking capabilities:</span></span>

- <span data-ttu-id="d1f83-107">격리 및 구분</span><span class="sxs-lookup"><span data-stu-id="d1f83-107">Isolation and segmentation</span></span>
- <span data-ttu-id="d1f83-108">인터넷 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-108">Internet communications</span></span>
- <span data-ttu-id="d1f83-109">Azure 리소스 간 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-109">Communicate between Azure resources</span></span>
- <span data-ttu-id="d1f83-110">온-프레미스 리소스와 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-110">Communicate with on-premises resources</span></span>
- <span data-ttu-id="d1f83-111">네트워크 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="d1f83-111">Route network traffic</span></span>
- <span data-ttu-id="d1f83-112">네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="d1f83-112">Filter network traffic</span></span>
- <span data-ttu-id="d1f83-113">가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="d1f83-113">Connect virtual networks</span></span>

### <a name="isolation-and-segmentation"></a><span data-ttu-id="d1f83-114">격리 및 구분</span><span class="sxs-lookup"><span data-stu-id="d1f83-114">Isolation and segmentation</span></span>

<span data-ttu-id="d1f83-115">Azure를 사용하면 여러 격리된 가상 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-115">Azure allows you to create multiple isolated virtual networks.</span></span> <span data-ttu-id="d1f83-116">가상 네트워크를 설정할 때 공용 또는 사설 IP 주소 범위를 사용하여 사설 IP(인터넷 프로토콜) 주소 공간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-116">When you set up a virtual network, you define a private Internet Protocol (IP) address space, using either public or private IP address ranges.</span></span> <span data-ttu-id="d1f83-117">그런 다음, 서브넷에 해당 IP 주소 공간을 분할하고, 각 명명된 서브넷에 정의된 주소 공간의 일부를 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-117">You can then segment that IP address space into subnets, and allocate part of the defined address space to each named subnet.</span></span>

<span data-ttu-id="d1f83-118">이름 확인을 위해 Azure에 기본 제공되는 이름 확인 서비스를 사용하거나 내부 또는 외부 DNS(Domain Name System) 서버를 사용하도록 가상 네트워크를 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-118">For name resolution, you can use the name resolution service that's built in to Azure, or you can configure the virtual network to use either an internal or an external Domain Name System (DNS) server.</span></span>

### <a name="internet-communications"></a><span data-ttu-id="d1f83-119">인터넷 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-119">Internet communications</span></span>

<span data-ttu-id="d1f83-120">Azure의 VM은 기본적으로 인터넷을 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-120">A VM in Azure can connect to the internet by default.</span></span> <span data-ttu-id="d1f83-121">그러나 Azure CLI, RDP(원격 데스크톱 프로토콜) 또는 SSH(Secure Shell) 중 하나를 사용하여 해당 VM에 연결하고 제어해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-121">However, you need to connect to and control that VM, with either the Azure CLI, Remote Desktop Protocol (RDP), or Secure Shell (SSH).</span></span> <span data-ttu-id="d1f83-122">공용 IP 주소 또는 공용 부하 분산 장치를 정의하여 들어오는 통신을 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-122">You can enable incoming communications by defining a public IP address or a public load balancer.</span></span>

### <a name="communicate-between-azure-resources"></a><span data-ttu-id="d1f83-123">Azure 리소스 간 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-123">Communicate between Azure resources</span></span>

<span data-ttu-id="d1f83-124">Azure 리소스를 사용하여 서로 안전하게 통신할 수 있도록 설정하려 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-124">You will want to enable Azure resources to communicate securely with each other.</span></span> <span data-ttu-id="d1f83-125">다음 두 가지 방법 중 하나를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-125">You can do that in one of two ways:</span></span>

- <span data-ttu-id="d1f83-126">**가상 네트워크**</span><span class="sxs-lookup"><span data-stu-id="d1f83-126">**Virtual networks**</span></span>
    
    <span data-ttu-id="d1f83-127">가상 네트워크는 VM뿐만 아니라 App Service Environments, Azure Kubernetes Service 및 Azure 가상 머신 확장 집합과 같은 다른 Azure 리소스도 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-127">Virtual networks can connect not only VMs, but other Azure resources, such as the App Service Environment, Azure Kubernetes Service, and Azure virtual machine scale sets.</span></span>

- <span data-ttu-id="d1f83-128">**서비스 엔드포인트**</span><span class="sxs-lookup"><span data-stu-id="d1f83-128">**Service endpoints**</span></span>
     
     <span data-ttu-id="d1f83-129">서비스 엔드포인트를 사용하여 Azure SQL Databases 및 저장소 계정과 같은 다른 Azure 리소스 형식에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-129">You can use service endpoints to connect to other Azure resource types, such as Azure SQL databases and storage accounts.</span></span> <span data-ttu-id="d1f83-130">이 방법을 사용하면 가상 네트워크에 여러 Azure 리소스를 연결하여 보안을 개선하고 리소스 간에 최적의 라우팅을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-130">This approach enables you to link multiple Azure resources to virtual networks, thereby improving security and providing optimal routing between resources.</span></span>

### <a name="communicate-with-on-premises-resources"></a><span data-ttu-id="d1f83-131">온-프레미스 리소스와 통신</span><span class="sxs-lookup"><span data-stu-id="d1f83-131">Communicate with on-premises resources</span></span>

<span data-ttu-id="d1f83-132">Azure 가상 네트워크를 사용하면 온-프레미스 환경 및 Azure 구독 내에서 리소스를 함께 연결하여 실제로 로컬 및 클라우드 환경에 걸쳐 있는 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-132">Azure virtual networks enable you to link resources together in your on-premises environment and within your Azure subscription, in effect creating a network that spans both your local and cloud environments.</span></span> <span data-ttu-id="d1f83-133">이 연결을 수행하는 세 가지 메커니즘이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-133">There are three mechanisms for you to achieve this connectivity:</span></span>

- <span data-ttu-id="d1f83-134">**지점 및 사이트 간 VPN**</span><span class="sxs-lookup"><span data-stu-id="d1f83-134">**Point-to-site VPNs**</span></span>

   <span data-ttu-id="d1f83-135">이 방법은 반대 방향으로 작동한다는 점을 제외하고 조직 외부의 컴퓨터가 회사 네트워크에 다시 연결하는 VPN 연결과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-135">This approach is like a VPN connection that a computer outside your organization makes back into your corporate network, except that it's working in the opposite direction.</span></span> <span data-ttu-id="d1f83-136">이 경우에 클라이언트 컴퓨터는 Azure에 암호화된 VPN 연결을 시작하여 해당 컴퓨터를 Azure 가상 네트워크에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-136">In this case, the client computer initiates an encrypted VPN connection to Azure, connecting that computer to the Azure virtual network.</span></span>

- <span data-ttu-id="d1f83-137">**사이트 간 VPN** 사이트 간 VPN은 온-프레미스 VPN 장치 또는 게이트웨이를 가상 네트워크의 Azure VPN 게이트웨이에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-137">**Site-to-site VPNs** A site-to-site VPN links your on-premises VPN device or gateway to the Azure VPN gateway in a virtual network.</span></span> <span data-ttu-id="d1f83-138">실제로 Azure의 장치는 로컬 네트워크에 있는 것으로 표시될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-138">In effect, the devices in Azure can appear as being on the local network.</span></span> <span data-ttu-id="d1f83-139">연결은 암호화되고 인터넷에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-139">The connection is encrypted and works over the internet.</span></span>

- <span data-ttu-id="d1f83-140">**Azure ExpressRoute**</span><span class="sxs-lookup"><span data-stu-id="d1f83-140">**Azure ExpressRoute**</span></span>

    <span data-ttu-id="d1f83-141">큰 대역폭과 더 높은 수준의 보안이 필요한 환경의 경우 Azure ExpressRoute를 사용하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-141">For environments where you need greater bandwidth and even higher levels of security, Azure ExpressRoute is the best approach.</span></span> <span data-ttu-id="d1f83-142">Azure ExpressRoute는 인터넷을 통해 이동하지 않는 Azure에 개인 전용 연결을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-142">Azure ExpressRoute provides dedicated private connectivity to Azure that does not travel over the internet.</span></span>

### <a name="route-network-traffic"></a><span data-ttu-id="d1f83-143">네트워크 트래픽 라우팅</span><span class="sxs-lookup"><span data-stu-id="d1f83-143">Route network traffic</span></span>

<span data-ttu-id="d1f83-144">기본적으로 Azure에서는 연결된 가상 네트워크의 서브넷, 온-프레미스 네트워크 및 인터넷 간에 트래픽을 라우팅합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-144">By default, Azure will route traffic between subnets on any connected virtual networks, on-premises networks, and the internet.</span></span> <span data-ttu-id="d1f83-145">그러나 다음과 같이 라우팅을 제어하고 해당 설정을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-145">However, you can control routing and override those settings as follows:</span></span>

- <span data-ttu-id="d1f83-146">**경로 테이블**</span><span class="sxs-lookup"><span data-stu-id="d1f83-146">**Route tables**</span></span>

    <span data-ttu-id="d1f83-147">경로 테이블을 사용하면 트래픽이 전달되어야 하는 방법에 대한 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-147">A route table allows you to define rules as to how traffic should be directed.</span></span> <span data-ttu-id="d1f83-148">서브넷 간에 패킷이 라우팅되는 방법을 제어하는 사용자 지정 경로 테이블을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-148">You can create custom route tables that control how packets are routed between subnets.</span></span>

- <span data-ttu-id="d1f83-149">**Border Gateway Protocol**</span><span class="sxs-lookup"><span data-stu-id="d1f83-149">**Border Gateway Protocol**</span></span>

    <span data-ttu-id="d1f83-150">BGP(Border Gateway Protocol)는 Azure VPN 게이트웨이 또는 ExpressRoute와 함께 작동하여 온-프레미스 BGP 경로를 Azure 가상 네트워크로 전파합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-150">Border Gateway Protocol (BGP) works with Azure VPN gateways or ExpressRoute to propagate on-premises BGP routes to Azure virtual networks.</span></span>

### <a name="filter-network-traffic"></a><span data-ttu-id="d1f83-151">네트워크 트래픽 필터링</span><span class="sxs-lookup"><span data-stu-id="d1f83-151">Filter network traffic</span></span>

<span data-ttu-id="d1f83-152">Azure 가상 네트워크를 사용하면 다음 방법을 사용하여 서브넷 간 트래픽을 필터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-152">Azure virtual networks enable you to filter traffic between subnets by using the following approaches:</span></span>

- <span data-ttu-id="d1f83-153">**네트워크 보안 그룹**</span><span class="sxs-lookup"><span data-stu-id="d1f83-153">**Network security groups**</span></span>

    <span data-ttu-id="d1f83-154">네트워크 보안 그룹은 Azure 리소스로서 여러 인바운드 및 아웃바운드 보안 규칙을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-154">A network security group is an Azure resource that can contain multiple inbound and outbound security rules.</span></span> <span data-ttu-id="d1f83-155">원본 및 대상 IP 주소, 포트 및 프로토콜과 같은 요인에 따라 트래픽을 허용하거나 차단하도록 이러한 규칙을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-155">You can define these rules to allow or block traffic, based on factors such as source and destination IP address, port, and protocol.</span></span>

- <span data-ttu-id="d1f83-156">**네트워크 가상 어플라이언스**</span><span class="sxs-lookup"><span data-stu-id="d1f83-156">**Network virtual appliances**</span></span>
    
    <span data-ttu-id="d1f83-157">네트워크 가상 어플라이언스는 강화된 네트워크 어플라이언스와 비교될 수 있는 특수한 VM입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-157">A network virtual appliance is a specialized VM that can be compared to a hardened network appliance.</span></span> <span data-ttu-id="d1f83-158">네트워크 가상 어플라이언스는 방화벽 실행 또는 WAN 최적화 수행과 같은 특정 네트워크 기능을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-158">A network virtual appliance carries out a particular network function, such as running a firewall or performing WAN optimization.</span></span>

## <a name="connect-virtual-networks"></a><span data-ttu-id="d1f83-159">가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="d1f83-159">Connect virtual networks</span></span>

<span data-ttu-id="d1f83-160">가상 네트워크 _피어링_을 사용하여 가상 네트워크를 함께 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-160">You can link virtual networks together using virtual network _peering_.</span></span> <span data-ttu-id="d1f83-161">피어링을 사용하면 각 가상 네트워크의 리소스가 서로 통신할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-161">Peering enables resources in each virtual network to communicate with each other.</span></span> <span data-ttu-id="d1f83-162">이러한 가상 네트워크는 별도 지역에 위치하여 Azure를 통해 상호 연결된 글로벌 네트워크를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-162">These virtual networks can be in separate regions, allowing you to create a global interconnected network through Azure.</span></span>

## <a name="azure-virtual-network-settings"></a><span data-ttu-id="d1f83-163">Azure 가상 네트워크 설정</span><span class="sxs-lookup"><span data-stu-id="d1f83-163">Azure virtual network settings</span></span>

<span data-ttu-id="d1f83-164">Azure Portal, 로컬 컴퓨터의 Azure PowerShell 또는 Azure Cloud Shell에서 Azure 가상 네트워크를 만들고 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-164">You can create and configure Azure virtual networks from the Azure portal, Azure PowerShell on your local computer, or Azure Cloud Shell.</span></span>

### <a name="create-a-virtual-network"></a><span data-ttu-id="d1f83-165">가상 네트워크 만들기</span><span class="sxs-lookup"><span data-stu-id="d1f83-165">Create a virtual network</span></span>

<span data-ttu-id="d1f83-166">Azure 가상 네트워크를 만들 때 다양한 기본 설정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-166">When you create an Azure virtual network, you configure a number of basic settings.</span></span> <span data-ttu-id="d1f83-167">여러 서브넷, DDoS(분산 서비스 거부) 보호 및 서비스 엔드포인트와 같은 고급 설정을 구성하는 옵션도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-167">You also have the option to configure advanced settings, such as multiple subnets, distributed denial of service (DDoS) protection, and service endpoints.</span></span>

![가상 네트워크 블레이드 필드 만들기의 예를 보여주는 Azure Portal의 스크린샷입니다.](../media/2-create-virtual-network.PNG)

<span data-ttu-id="d1f83-169">기본 가상 네트워크에 대해 구성해야 하는 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-169">Settings that you need to configure for a basic virtual network are:</span></span>

- <span data-ttu-id="d1f83-170">**네트워크 이름**</span><span class="sxs-lookup"><span data-stu-id="d1f83-170">**Network name**</span></span>

    <span data-ttu-id="d1f83-171">이 이름은 구독에서 고유해야 하지만 전세계에서 고유할 필요는 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-171">This name must be unique in your subscription but does not need to be globally unique.</span></span> <span data-ttu-id="d1f83-172">다른 가상 네트워크와 구분하고 기억하기 쉽도록 설명이 포함된 이름을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-172">Make the name a descriptive one that is easy to remember and distinguish from other virtual networks.</span></span>

- <span data-ttu-id="d1f83-173">**주소 공간**</span><span class="sxs-lookup"><span data-stu-id="d1f83-173">**Address space**</span></span>
    
    <span data-ttu-id="d1f83-174">가상 네트워크를 설정할 때 CIDR(Classless Interdomain Routing) 형식으로 내부 주소 공간을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-174">When you set up a virtual network, you define the internal address space in Classless Interdomain Routing (CIDR) format.</span></span> <span data-ttu-id="d1f83-175">이 주소 공간은 구독 내에서 고유해야 합니다. 그래서, 예를 들어 10.1.0.0/8 네트워크가 10.0.0.0/24와 겹치므로, 하나의 가상 네트워크에 대해 10.0.0.0/24, 그리고 또다른 가상 네트워크에 대해 10.1.0.0/8이라는 주소 공간을 정의할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-175">This address space needs to be unique within your subscription, so you cannot define an address space of, say, 10.0.0.0/24 for one virtual network and then 10.1.0.0/8 for another, as the 10.1.0.0/8 network will overlap 10.0.0.0/24.</span></span> <span data-ttu-id="d1f83-176">그러나 10.0.0.0/16 및 10.1.0.0/16 등을 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-176">However, you can have 10.0.0.0/16 and 10.1.0.0/16, etc.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="d1f83-177">가상 네트워크를 만든 후에 주소 공간을 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-177">You can add address spaces after creating the virtual network.</span></span>

- <span data-ttu-id="d1f83-178">**구독**</span><span class="sxs-lookup"><span data-stu-id="d1f83-178">**Subscription**</span></span>

    <span data-ttu-id="d1f83-179">선택할 여러 구독이 있는 경우에만 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-179">Only applies if you have multiple subscriptions to choose from.</span></span>

- <span data-ttu-id="d1f83-180">**리소스 그룹**</span><span class="sxs-lookup"><span data-stu-id="d1f83-180">**Resource group**</span></span>
    
    <span data-ttu-id="d1f83-181">다른 Azure 리소스와 마찬가지로 가상 네트워크는 리소스 그룹에 존재해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-181">Like any other Azure resource, a virtual network needs to exist in a resource group.</span></span> <span data-ttu-id="d1f83-182">기존 리소스 그룹을 선택하거나 새 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-182">You can either select an existing RG or create a new one.</span></span>
    
- <span data-ttu-id="d1f83-183">**위치**</span><span class="sxs-lookup"><span data-stu-id="d1f83-183">**Location**</span></span>

    <span data-ttu-id="d1f83-184">가상 네트워크가 존재할 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-184">Select the location where you want the virtual network to exist.</span></span>

- <span data-ttu-id="d1f83-185">**서브넷**</span><span class="sxs-lookup"><span data-stu-id="d1f83-185">**Subnet**</span></span>
    
    <span data-ttu-id="d1f83-186">각 가상 네트워크 주소 범위 내에서 가상 네트워크의 주소 공간을 분할하는 하나 이상의 서브넷을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-186">Within each virtual network address range, you can create one or more subnets that partition the virtual network's address space.</span></span> <span data-ttu-id="d1f83-187">서브넷 간의 라우팅은 기본 트래픽 경로에 따라 다르거나 사용자 지정 경로를 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-187">Routing between subnets will then depend on the default traffic routes, or you can define custom routes.</span></span> <span data-ttu-id="d1f83-188">또는 모든 가상 네트워크의 주소 범위를 포함하는 하나의 서브넷을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-188">Alternatively, you can define one subnet that encompasses all the virtual networks' address ranges.</span></span>

    > [!NOTE]
    > <span data-ttu-id="d1f83-189">서브넷 이름은 영문, 숫자, 밑줄, 마침표 또는 하이픈만 포함할 수 있습니다. 단 영문이나 숫자로 시작하고 영문, 숫자 또는 하이픈으로 끝나야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-189">Subnet names must begin with a letter or number, end with a letter, number or underscore, and may contain only letters, numbers, underscores, periods, or hyphens.</span></span>

- <span data-ttu-id="d1f83-190">**DDoS 보호**</span><span class="sxs-lookup"><span data-stu-id="d1f83-190">**DDoS protection**</span></span>

    <span data-ttu-id="d1f83-191">기본 또는 표준 DDoS 보호 중 하나를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-191">You can select either Basic or Standard DDoS protection.</span></span> <span data-ttu-id="d1f83-192">표준 DDoS Protection은 프리미엄 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-192">Standard DDoS Protection is a premium service.</span></span> <span data-ttu-id="d1f83-193">표준 DDoS 보호에 대한 자세한 내용입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-193">For more information on Standard DDoS protection.</span></span>

- <span data-ttu-id="d1f83-194">**서비스 엔드포인트**</span><span class="sxs-lookup"><span data-stu-id="d1f83-194">**Service Endpoints**</span></span>
    
    <span data-ttu-id="d1f83-195">여기서는 서비스 엔드포인트를 설정한 다음, 목록에서 사용하려는 Azure 서비스 엔드포인트를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-195">Here, you enable service endpoints, and then select from the list which Azure service endpoints you want to enable.</span></span> <span data-ttu-id="d1f83-196">옵션에는 Azure Cosmos DB, Azure Service Bus, Azure Key Vault 등이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-196">Options include Azure Cosmos DB, Azure Service Bus, Azure Key Vault, and so on.</span></span>

<span data-ttu-id="d1f83-197">이러한 설정을 구성한 경우 **만들기** 단추를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-197">When you have configured these settings, click the **Create** button.</span></span>

### <a name="define-additional-settings"></a><span data-ttu-id="d1f83-198">추가 설정 정의</span><span class="sxs-lookup"><span data-stu-id="d1f83-198">Define additional settings</span></span>

<span data-ttu-id="d1f83-199">가상 네트워크를 만든 후에 추가 설정을 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-199">After creating a virtual network, you can then define further settings.</span></span> <span data-ttu-id="d1f83-200">추가 설정은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-200">These include:</span></span>

- <span data-ttu-id="d1f83-201">**네트워크 보안 그룹**</span><span class="sxs-lookup"><span data-stu-id="d1f83-201">**Network security group**</span></span>
    
    <span data-ttu-id="d1f83-202">네트워크 보안 그룹에는 가상 네트워크 서브넷 및 네트워크 인터페이스 내외부로 이동할 수 있는 네트워크 트래픽 유형을 필터링할 수 있는 보안 규칙이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-202">Network security groups have security rules that enable you to filter the type of network traffic that can flow in and out of virtual network subnets and network interfaces.</span></span> <span data-ttu-id="d1f83-203">네트워크 보안 그룹을 별도로 만든 다음, 가상 네트워크와 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-203">You create the network security group separately, and then associate it with the virtual network.</span></span>

- <span data-ttu-id="d1f83-204">**경로 테이블**</span><span class="sxs-lookup"><span data-stu-id="d1f83-204">**Route table**</span></span>

    <span data-ttu-id="d1f83-205">Azure는 Azure 가상 네트워크 내의 각 서브넷에 대한 경로 테이블을 자동으로 만들고 시스템 기본 경로를 테이블에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-205">Azure automatically creates a route table for each subnet within an Azure virtual network and adds system default routes to the table.</span></span> <span data-ttu-id="d1f83-206">그러나 사용자 지정 경로 테이블을 추가하여 가상 네트워크 간에 트래픽을 수정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-206">However, you can add custom route tables to modify traffic between virtual networks.</span></span>

<span data-ttu-id="d1f83-207">서비스 엔드포인트를 수정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-207">You can also amend the service endpoints.</span></span>

![가상 네트워크 설정을 편집하기 위한 예제 블레이드를 보여주는 Azure Portal의 스크린샷.](../media/2-virtual-network-additional-settings.PNG)

### <a name="configure-virtual-networks"></a><span data-ttu-id="d1f83-209">가상 네트워크 구성</span><span class="sxs-lookup"><span data-stu-id="d1f83-209">Configure virtual networks</span></span>

<span data-ttu-id="d1f83-210">가상 네트워크를 만들면 Azure Portal의 Virtual Networks 블레이드에서 추가 설정을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-210">When you have created a virtual network, you can change any further settings from the Virtual Networks blade in the Azure portal.</span></span> <span data-ttu-id="d1f83-211">또는 PowerShell 명령이나 Cloud Shell의 명령을 사용하여 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-211">Alternatively, you can use PowerShell commands or commands in Cloud Shell to make changes.</span></span>

![가상 네트워크 구성을 위한 예제 블레이드를 보여주는 Azure Portal의 스크린샷.](../media/2-configure-virtual-network.PNG)

<span data-ttu-id="d1f83-213">그런 다음, 추가 하위 블레이드에서 설정을 검토하고 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-213">You can then review and change settings in further sub-blades.</span></span>
<span data-ttu-id="d1f83-214">이러한 설정에는 다음이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-214">These settings include:</span></span>

- <span data-ttu-id="d1f83-215">주소 공간</span><span class="sxs-lookup"><span data-stu-id="d1f83-215">Address spaces</span></span>

    <span data-ttu-id="d1f83-216">초기 정의에 추가 주소 공간 추가 가능</span><span class="sxs-lookup"><span data-stu-id="d1f83-216">You can add further address spaces to the initial definition</span></span>

- <span data-ttu-id="d1f83-217">연결된 장치</span><span class="sxs-lookup"><span data-stu-id="d1f83-217">Connected devices</span></span>

    <span data-ttu-id="d1f83-218">가상 네트워크를 사용하여 머신 연결</span><span class="sxs-lookup"><span data-stu-id="d1f83-218">Use the virtual network to connect machines</span></span>

- <span data-ttu-id="d1f83-219">서브넷</span><span class="sxs-lookup"><span data-stu-id="d1f83-219">Subnets</span></span>

    <span data-ttu-id="d1f83-220">추가 서브넷 추가</span><span class="sxs-lookup"><span data-stu-id="d1f83-220">Add further subnets</span></span>

- <span data-ttu-id="d1f83-221">피어링</span><span class="sxs-lookup"><span data-stu-id="d1f83-221">Peerings</span></span>

    <span data-ttu-id="d1f83-222">피어링 배열에서 가상 네트워크 연결</span><span class="sxs-lookup"><span data-stu-id="d1f83-222">Link virtual networks in peering arrangements</span></span>

<span data-ttu-id="d1f83-223">가상 네트워크를 모니터링하고 문제를 해결하거나 자동화 스크립트를 만들어서 현재 가상 네트워크를 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-223">You can also monitor and troubleshoot virtual networks, or create an automation script to generate the current virtual network.</span></span>

## <a name="summary"></a><span data-ttu-id="d1f83-224">요약</span><span class="sxs-lookup"><span data-stu-id="d1f83-224">Summary</span></span>

<span data-ttu-id="d1f83-225">가상 네트워크는 Azure에서 엔터티를 연결하기 위한 강력하고 구성 가능한 메커니즘입니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-225">Virtual networks are powerful and highly configurable mechanisms for connecting entities in Azure.</span></span> <span data-ttu-id="d1f83-226">Azure 리소스를 서로 또는 온-프레미스의 리소스에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-226">You can connect Azure resources to one another or to resources you have on-premises.</span></span> <span data-ttu-id="d1f83-227">네트워크 트래픽을 격리, 필터링 및 라우팅할 수 있으며, Azure를 사용하면 필요한 경우 보안을 강화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d1f83-227">You can isolate, filter and route your network traffic, and Azure allows you to increase security where you feel you need it.</span></span>
