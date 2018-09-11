<span data-ttu-id="11ca7-101">조사 팀이 계산을 많이 사용하는 데이터 처리를 수행해야 하는데 작업을 수행할 장비가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-101">Your research team needs to perform computationally intense data processing and doesn't have the equipment to do the work.</span></span> <span data-ttu-id="11ca7-102">이 때문에 Azure를 사용하여 데이터 분석을 수행하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-102">They've decided to use Azure to do the data analysis.</span></span>

## <a name="what-is-azure-compute"></a><span data-ttu-id="11ca7-103">Azure 계산이란?</span><span class="sxs-lookup"><span data-stu-id="11ca7-103">What is Azure compute?</span></span>
<span data-ttu-id="11ca7-104">Azure 계산은 클라우드 기반 응용 프로그램을 실행하기 위한 주문형 컴퓨팅 리소스 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-104">Azure compute is an on-demand computing resource service for running cloud-based applications.</span></span> <span data-ttu-id="11ca7-105">가상 머신 및 컨테이너를 통해 멀티 코어 프로세서, 슈퍼 컴퓨터 등의 컴퓨팅 리소스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-105">It provides computing resources like multi-core processors and supercomputers via virtual machines and containers.</span></span> <span data-ttu-id="11ca7-106">또한 인프라 설정 또는 구성 없이 앱을 실행할 수 있도록 하는 서버리스 컴퓨팅을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-106">It also provides serverless computing to enable running apps without requiring infrastructure setup or configuration.</span></span> <span data-ttu-id="11ca7-107">리소스는 요청 시 제공되며, 일반적으로 수분 또는 수초 이내에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-107">The resources are available on-demand and can typically be created in minutes or even seconds.</span></span> <span data-ttu-id="11ca7-108">사용하는 리소스에 대해 사용 기간에 대한 요금만 지불하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-108">You pay only for the resources you use and only for as long as you're using them.</span></span>

<span data-ttu-id="11ca7-109">Azure에서 계산을 수행하는 일반적인 기술에는 다음 세 가지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-109">There are three common techniques for performing compute in Azure:</span></span>
1. <span data-ttu-id="11ca7-110">가상 머신</span><span class="sxs-lookup"><span data-stu-id="11ca7-110">Virtual machines</span></span>
1. <span data-ttu-id="11ca7-111">컨테이너</span><span class="sxs-lookup"><span data-stu-id="11ca7-111">Containers</span></span>
1. <span data-ttu-id="11ca7-112">서버리스 컴퓨팅</span><span class="sxs-lookup"><span data-stu-id="11ca7-112">Serverless computing</span></span>

## <a name="what-are-virtual-machines"></a><span data-ttu-id="11ca7-113">가상 머신이란?</span><span class="sxs-lookup"><span data-stu-id="11ca7-113">What are virtual machines?</span></span>

<span data-ttu-id="11ca7-114">**VM(가상 머신)** 은 물리적 컴퓨터의 소프트웨어 에뮬레이션입니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-114">A **virtual machine (VM)** is a software emulation of a physical computer.</span></span> <span data-ttu-id="11ca7-115">VM에는 가상 프로세서, 메모리, 저장소 및 네트워킹 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-115">They include a virtual processor, memory, storage, and networking resources.</span></span> <span data-ttu-id="11ca7-116">운영 체제를 호스트하며, 물리적 컴퓨터처럼 소프트웨어를 설치 및 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-116">They host an operating system, and you're able to install and run software just like a physical computer.</span></span> <span data-ttu-id="11ca7-117">또한 원격 데스크톱 클라이언트를 사용하여, 물리적 터미널 앞에 앉아 있는 것처럼 가상 머신을 사용하고 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-117">And by using a remote desktop client, you can use and control the virtual machine as if you were sitting in front of a physical terminal.</span></span>

### <a name="virtual-machines-in-azure"></a><span data-ttu-id="11ca7-118">Azure의 가상 머신</span><span class="sxs-lookup"><span data-stu-id="11ca7-118">Virtual machines in Azure</span></span>

<span data-ttu-id="11ca7-119">Azure에서 가상 머신을 만들고 호스트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-119">Virtual machines can be created and hosted in Azure.</span></span> <span data-ttu-id="11ca7-120">미리 구성된 가상 머신 이미지를 선택하면 일반적으로 수분 이내에 새 가상 머신을 만들고 프로비전할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-120">New virtual machines can typically be created and provisioned in minutes by selecting a pre-configured virtual machine image.</span></span>

<span data-ttu-id="11ca7-121">이미지 선택은 VM을 만들 때 필요한 가장 중요한 결정 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-121">Selecting an image is one of the most important decisions you'll need to make when creating a VM.</span></span> <span data-ttu-id="11ca7-122">이미지는 가상 머신을 만드는 데 사용되는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-122">An image is a template used to create a virtual machine.</span></span> <span data-ttu-id="11ca7-123">이러한 템플릿에는 이미 OS(운영 체제)가 포함되어 있으며, 개발 도구 또는 웹 호스팅 환경과 같은 기타 소프트웨어가 포함된 경우도 많습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-123">These templates already include an operating system (OS) and often other software, such as development tools or web hosting environments.</span></span>

## <a name="what-are-containers"></a><span data-ttu-id="11ca7-124">컨테이너란?</span><span class="sxs-lookup"><span data-stu-id="11ca7-124">What are containers?</span></span>

<span data-ttu-id="11ca7-125">컨테이너는 가상화 환경이지만, 가상 머신과는 달리 운영 체제를 포함하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-125">Containers are a virtualization environment but, unlike a virtual machine, they do not include an operating system.</span></span> <span data-ttu-id="11ca7-126">대신 컨테이너를 실행하는 호스트 환경의 운영 체제를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-126">Instead, they reference the operating system of the host environment that runs the container.</span></span> <span data-ttu-id="11ca7-127">예를 들어 특정 Linux 커널이 있는 서버에서 컨테이너 5개를 실행하는 경우 컨테이너 5개가 모두 동일한 커널에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-127">For example, if five containers are running on a server with a specific Linux kernel, all five containers are running on that same kernel.</span></span> 

<span data-ttu-id="11ca7-128">일반적으로 컨테이너에는 사용자가 작성하는 응용 프로그램이 포함되며, 호스트 환경의 커널에서 응용 프로그램을 실행하는 데 필요한 모든 라이브러리가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-128">Containers typically contain an application that you write and will include any libraries required for your application to run on the host environment's kernel.</span></span> 

<span data-ttu-id="11ca7-129">컨테이너는 기본적으로 경량이며, 환경 및 수요의 변화에 따라 동적으로 생성, 확장 및 중지되도록 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-129">Containers are meant to be lightweight and are designed to be created, scaled out, and stopped dynamically and environment and demand change.</span></span>

<span data-ttu-id="11ca7-130">컨테이너를 사용할 경우 가상 머신에서 여러 개의 격리된 응용 프로그램을 실행할 수 있다는 혜택이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-130">A benefit of using containers is the ability to run multiple isolated applications on a virtual machine.</span></span> <span data-ttu-id="11ca7-131">컨테이너 자체가 보안이 유지되고 격리되므로 워크로드마다 별도의 VM을 만들지 않아도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-131">Since containers themselves are secured and isolated, you don't necessarily need separate VMs for separate workloads.</span></span>

<span data-ttu-id="11ca7-132">Azure는 Docker 컨테이너 및 이러한 컨테이너를 관리하는 여러 가지 방법을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-132">Azure supports Docker containers and several ways to manage those containers.</span></span> <span data-ttu-id="11ca7-133">컨테이너는 수동으로 관리하거나, Azure Kubernetes Service와 같은 Azure 서비스를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-133">Containers can be managed manually or with Azure services such as Azure Kubernetes Service.</span></span>

### <a name="what-is-serverless-computing"></a><span data-ttu-id="11ca7-134">서버리스 컴퓨팅이란?</span><span class="sxs-lookup"><span data-stu-id="11ca7-134">What is serverless computing?</span></span>

<span data-ttu-id="11ca7-135">서버리스 컴퓨팅은 코드를 실행하는, 클라우드에 호스트된 실행 환경이지만 기본 호스팅 환경을 완전히 추상화합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-135">Serverless computing is a cloud-hosted execution environment that runs your code but completely abstracts the underlying hosting environment.</span></span> <span data-ttu-id="11ca7-136">서비스 인스턴스를 만들고 코드를 추가하기만 하면 됩니다. 인프라 구성 또는 유지 관리가 필요하지 않거나 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-136">You create an instance of the service, and you add your code; no infrastructure configuration or maintenance is required, or even allowed.</span></span>

<span data-ttu-id="11ca7-137">이벤트에 응답하도록 서버리스 앱을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-137">You configure your serverless apps to respond to events.</span></span> <span data-ttu-id="11ca7-138">이벤트는 REST 엔드포인트, 타이머 또는 다른 Azure 서비스로부터 받은 메시지일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-138">This could be a REST end point, a timer, or a message received from another Azure service.</span></span> <span data-ttu-id="11ca7-139">서버리스 앱은 이벤트에 의해 트리거된 경우에만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-139">The serverless app runs only when it's triggered by an event.</span></span> 

<span data-ttu-id="11ca7-140">인프라는 사용자의 책임이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-140">Infrastructure isn't your responsibly.</span></span> <span data-ttu-id="11ca7-141">크기 조정 및 성능이 자동으로 처리되며, 사용하는 리소스에 대해서만 요금이 청구됩니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-141">Scaling and performance are handled automatically, and you are billed only for the exact resources you use.</span></span> <span data-ttu-id="11ca7-142">용량을 예약할 필요도 없습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-142">There's no need to even reserve capacity.</span></span>

<span data-ttu-id="11ca7-143">Azure에는 두 가지 서버리스 계산 구현이 있습니다. **Azure Functions**는 거의 모든 최신 언어로 코드를 실행할 수 있고, **Azure Logic Apps**는 코드를 작성하지 않고 Azure 서비스에서 트리거된 논리를 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="11ca7-143">Azure has two implementations of serverless compute: **Azure Functions**, which can execute code in almost any modern language, and **Azure Logic Apps**, which allows you to execute logic triggered by Azure services without writing code.</span></span>