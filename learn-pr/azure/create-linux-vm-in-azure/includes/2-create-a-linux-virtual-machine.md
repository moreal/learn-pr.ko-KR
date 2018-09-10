<span data-ttu-id="be127-101">로컬 Ubuntu Linux 서버에서 실행 중인 기존 웹 사이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-101">We have an existing website running on a local Ubuntu Linux server.</span></span> <span data-ttu-id="be127-102">최신 Ubuntu 이미지를 사용하여 Azure VM(Virtual Machine)을 만들고 사이트를 클라우드로 마이그레이션하는 것이 목표입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-102">Our goal is to create an Azure Virtual Machine (VM), using the latest Ubuntu image and migrate the site to the cloud.</span></span> <span data-ttu-id="be127-103">이 단위에서는 Azure에서 가상 머신을 만들 때 결정해야 하는 옵션에 대해 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="be127-103">In this unit, you will learn about the options you will need to decide when creating a virtual machine in Azure.</span></span>

## <a name="introduction-to-azure-virtual-machines"></a><span data-ttu-id="be127-104">Azure Virtual Machines 소개</span><span class="sxs-lookup"><span data-stu-id="be127-104">Introduction to Azure Virtual Machines</span></span>

<span data-ttu-id="be127-105">Azure VM은 요청 시 확장 가능한 클라우드 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-105">Azure VMs are an on-demand scalable cloud computing resource.</span></span> <span data-ttu-id="be127-106">여기에는 프로세서, 메모리, 저장소 및 네트워킹 리소스가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-106">They include processor, memory, storage, and networking resources.</span></span> <span data-ttu-id="be127-107">마음대로 가상 머신을 시작하고 중지할 수 있으며, Azure Portal 또는 Azure CLI를 통해 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-107">You can start and stop virtual machines at will, and manage them from the Azure portal or with the Azure CLI.</span></span> <span data-ttu-id="be127-108">원격 SSH(Secure Shell)를 사용하여 실행 중인 VM에 직접 연결하고 로컬 컴퓨터에서 작업하듯이 명령을 실행할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-108">You can also use a remote secure shell (SSH) to connect directly to the running VM and execute commands as if you are on a local computer.</span></span>

### <a name="running-linux-in-azure"></a><span data-ttu-id="be127-109">Azure에서 실행 중인 Linux</span><span class="sxs-lookup"><span data-stu-id="be127-109">Running Linux in Azure</span></span>

<span data-ttu-id="be127-110">Azure에서 Linux 기반 VM을 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-110">Creating Linux-based VMs in Azure is easy.</span></span> <span data-ttu-id="be127-111">Microsoft는 유수의 Linux 공급 업체와 협력하여 해당사의 배포판이 Azure 플랫폼에 대해 최적화될 수 있도록 하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-111">Microsoft has partnered with prominent Linux vendors to ensure their distributions are optimized for the Azure platform.</span></span> <span data-ttu-id="be127-112">SUSE, Red Hat 및 Ubuntu와 같이 많이 사용되는 다양한 Linux 배포판에 대해 미리 빌드된 이미지로부터 가상 머신을 만들거나 클라우드에서 실행할 자체 Linux 배포판을 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-112">You can create virtual machines from pre-built images for a variety of popular Linux distributions such as SUSE, Red Hat, and Ubuntu or build your own Linux distribution to run in the cloud.</span></span>

## <a name="creating-an-azure-vm"></a><span data-ttu-id="be127-113">Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="be127-113">Creating an Azure VM</span></span>

<span data-ttu-id="be127-114">VM은 Azure에서 여러 가지 방법, 즉 Azure Portal, 스크립트(Azure CLI 또는 Azure PowerShell 사용) 또는 Azure Resource Manager 템플릿을 통해 정의하고 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-114">VMs can be defined and deployed on Azure in several ways: the Azure portal, a script (using the Azure CLI or Azure PowerShell), or through an Azure Resource Manager template.</span></span> <span data-ttu-id="be127-115">모든 경우에 곧 설명할 몇 가지 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-115">In all cases, you will need to supply several pieces of information which we'll cover shortly.</span></span>

<span data-ttu-id="be127-116">또한 Azure Marketplace는 특정 시나리오에 맞게 설치된 OS 및 즐겨 찾는 소프트웨어 도구를 모두 포함하는 미리 구성된 이미지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-116">The Azure Marketplace also provides pre-configured images that include both an OS and favorite software tools installed for specific scenarios.</span></span>

![Azure Marketplace Virtual Machines](../media-drafts/2-marketplace-vm-choices.png)

## <a name="resources-used-in-a-linux-vm"></a><span data-ttu-id="be127-118">Linux VM에서 사용되는 리소스</span><span class="sxs-lookup"><span data-stu-id="be127-118">Resources used in a Linux VM</span></span>

<span data-ttu-id="be127-119">Azure에서 Linux VM을 만드는 경우 VM을 호스팅할 리소스도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="be127-119">When creating a Linux VM in Azure, you also create resources to host the VM.</span></span> <span data-ttu-id="be127-120">이러한 리소스는 함께 작동하여 컴퓨터를 가상화하고 Linux 운영 체제를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-120">These resources work together to virtualize a computer and run the Linux operating system.</span></span> <span data-ttu-id="be127-121">다음 리소스는 존재해야 하거나(VM을 만드는 중에 선택함) VM과 함께 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="be127-121">These must either exist (and be selected during VM creation), or they will be created with the VM.</span></span>

- <span data-ttu-id="be127-122">CPU 및 메모리 리소스를 제공하는 가상 머신</span><span class="sxs-lookup"><span data-stu-id="be127-122">A virtual machine that provides CPU and memory resources</span></span>
- <span data-ttu-id="be127-123">가상 하드 디스크를 보관하는 Azure Storage 계정</span><span class="sxs-lookup"><span data-stu-id="be127-123">An Azure Storage account to hold the virtual hard disks</span></span>
- <span data-ttu-id="be127-124">OS, 응용 프로그램 및 데이터를 보관하는 가상 디스크</span><span class="sxs-lookup"><span data-stu-id="be127-124">Virtual disks to hold the OS, applications, and data</span></span>
- <span data-ttu-id="be127-125">VM을 다른 Azure 서비스 또는 자체 온-프레미스 하드웨어에 연결하는 VNet(가상 네트워크)</span><span class="sxs-lookup"><span data-stu-id="be127-125">A virtual network (VNet) to connect the VM to other Azure services or your on-premise hardware</span></span>
- <span data-ttu-id="be127-126">VNet과 통신하는 네트워크 인터페이스</span><span class="sxs-lookup"><span data-stu-id="be127-126">A network interface to communicate with the VNet</span></span>
- <span data-ttu-id="be127-127">VM에 액세스할 수 있도록 하는 선택적인 공용 IP 주소</span><span class="sxs-lookup"><span data-stu-id="be127-127">An optional public IP address so you can access the VM</span></span>

<span data-ttu-id="be127-128">다른 Azure 서비스와 마찬가지로 VM이 포함되는 **리소스 그룹**이 필요합니다(필요한 경우 관리를 위해 이러한 리소스를 그룹화함).</span><span class="sxs-lookup"><span data-stu-id="be127-128">Like other Azure services, you'll need a **Resource Group** to contain the VM (and optionally group these resources for administration).</span></span> <span data-ttu-id="be127-129">새 VM을 만드는 경우 기존 리소스 그룹을 사용하거나 리소스 그룹을 새로 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-129">When you create a new VM, you can either use an existing resource group or create a new one.</span></span>

## <a name="choose-the-vm-image"></a><span data-ttu-id="be127-130">VM 이미지 선택</span><span class="sxs-lookup"><span data-stu-id="be127-130">Choose the VM image</span></span>

<span data-ttu-id="be127-131">이미지 선택은 VM을 만들 때 처음 내리는 가장 중요한 결정 중 하나입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-131">Selecting an image is one of the first and most important decisions you'll make when creating a VM.</span></span> <span data-ttu-id="be127-132">이미지는 VM을 만드는 데 사용되는 템플릿입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-132">An image is a template that's used to create a VM.</span></span> <span data-ttu-id="be127-133">이러한 템플릿에는 OS가 포함되어 있으며, 개발 도구 또는 웹 호스팅 환경과 같은 기타 소프트웨어가 포함된 경우도 많습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-133">These templates include an OS and often other software, such as development tools or web hosting environments.</span></span>

<span data-ttu-id="be127-134">컴퓨터에서 설치할 수 있는 모든 요소가 이미지에 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-134">Anything that a computer can have installed can be included in an image.</span></span> <span data-ttu-id="be127-135">Apache 서버에 웹앱을 호스팅하는 것처럼 필요한 작업에 맞게 미리 구성된 이미지에서 VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-135">You can create a VM from an image that's pre-configured to precisely the tasks you need, such as hosting a web app on Apache server.</span></span>

> [!TIP]
> <span data-ttu-id="be127-136">사용자 지정 디스크 이미지를 만들고 업로드할 수도 있으며, 자세한 내용은 설명서를 참조하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-136">You can also create and upload custom disk images, check the documentation for more information.</span></span>

## <a name="sizing-your-vm"></a><span data-ttu-id="be127-137">VM 크기 지정</span><span class="sxs-lookup"><span data-stu-id="be127-137">Sizing your VM</span></span>
<span data-ttu-id="be127-138">물리적 머신과 마찬가지로 가상 머신에는 일정한 양의 메모리와 CPU 처리 능력이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-138">Just as a physical machine has a certain amount of memory and CPU power, so does a virtual machine.</span></span> <span data-ttu-id="be127-139">Azure는 크기와 가격이 다양한 여러 VM을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-139">Azure offers a range of VMs of differing sizes at different price points.</span></span> <span data-ttu-id="be127-140">선택하는 크기에 따라 VM 처리 능력, 메모리 및 최대 저장소 용량이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-140">The size that you choose will determine the VMs processing power, memory, and max storage capacity.</span></span>

> [!WARNING]
> <span data-ttu-id="be127-141">VM을 만드는 데 영향을 줄 수 있는 각 구독에 대한 할당량 한도가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-141">There are quota limits on each subscription that can impact VM creation.</span></span> <span data-ttu-id="be127-142">기본적으로 한 지역 내의 모든 VM에서 20개를 초과하는 가상 _코어_를 사용할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-142">By default, you cannot have more than 20 virtual _cores_ across all VMs within a region.</span></span> <span data-ttu-id="be127-143">지역 간에 VM을 분할하거나 [온라인 요청](https://docs.microsoft.com/en-us/azure/azure-supportability/resource-manager-core-quotas-request)을 제출하여 한도를 늘릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-143">You can either split up VMs across regions or file an [online request](https://docs.microsoft.com/en-us/azure/azure-supportability/resource-manager-core-quotas-request) to increase your limits.</span></span>

<span data-ttu-id="be127-144">VM 크기는 기본 테스트를 위한 B 시리즈부터 시작하여 대규모 컴퓨팅 작업을 위한 H 시리즈까지의 범주로 그룹화됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-144">VM sizes are grouped into categories, starting with the B-series for basic testing and running up to the H-series for massive computing tasks.</span></span> <span data-ttu-id="be127-145">수행하려는 워크로드에 따라 VM의 크기를 선택해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-145">You should select the size of the VM based on the workload you want to perform.</span></span> <span data-ttu-id="be127-146">VM을 만든 후에 크기를 변경할 수는 있지만 VM을 먼저 중지해야 하므로 가능하면 처음부터 적절하게 크기를 정하는 것이 가장 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-146">It is possible to change the size of a VM after it's been created, but the VM must be stopped first, so it's best to size it appropriately from the start if possible.</span></span>

#### <a name="here-are-some-guidelines-based-on-the-scenario-you-are-targeting"></a><span data-ttu-id="be127-147">다음은 대상으로 하는 시나리오에 기반한 몇 가지 지침입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-147">Here are some guidelines based on the scenario you are targeting.</span></span>

| <span data-ttu-id="be127-148">수행하는 작업</span><span class="sxs-lookup"><span data-stu-id="be127-148">What are you doing?</span></span> | <span data-ttu-id="be127-149">다음과 같이 크기를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-149">Consider these sizes</span></span>
|-------|------------------|
| <span data-ttu-id="be127-150">**범용 컴퓨팅/웹** 테스트 및 개발, 중소형 데이터베이스 또는 중소 규모 트래픽 웹 서버</span><span class="sxs-lookup"><span data-stu-id="be127-150">**General use computing/web** Testing and development, small to medium databases, or low to medium traffic web servers.</span></span> | <span data-ttu-id="be127-151">B, Dsv3, Dv3, DSv2, Dv2</span><span class="sxs-lookup"><span data-stu-id="be127-151">B, Dsv3, Dv3, DSv2, Dv2</span></span> |
| <span data-ttu-id="be127-152">**과도한 계산 작업** 중간 규모 트래픽 웹 서버, 네트워크 어플라이언스, 일괄 처리 프로세스 및 응용 프로그램 서버</span><span class="sxs-lookup"><span data-stu-id="be127-152">**Heavy computational tasks** Medium traffic web servers, network appliances, batch processes, and application servers.</span></span> | <span data-ttu-id="be127-153">Fsv2, Fs, F</span><span class="sxs-lookup"><span data-stu-id="be127-153">Fsv2, Fs, F</span></span> |
| <span data-ttu-id="be127-154">**대용량 메모리 사용** 관계형 데이터베이스 서버, 중대형 캐시 및 메모리 내 분석</span><span class="sxs-lookup"><span data-stu-id="be127-154">**Large memory usage** Relational database servers, medium to large caches, and in-memory analytics.</span></span> | <span data-ttu-id="be127-155">Esv3, Ev3, M, GS, G, DSv2, Dv2</span><span class="sxs-lookup"><span data-stu-id="be127-155">Esv3, Ev3, M, GS, G, DSv2, Dv2</span></span> |
| <span data-ttu-id="be127-156">**데이터 저장소 및 처리** 높은 디스크 처리량 및 IO가 필요한 빅 데이터, SQL 및 NoSQL 데이터베이스</span><span class="sxs-lookup"><span data-stu-id="be127-156">**Data storage and processing** Big Data, SQL, and NoSQL databases which need high disk throughput and IO.</span></span> | <span data-ttu-id="be127-157">Ls</span><span class="sxs-lookup"><span data-stu-id="be127-157">Ls</span></span> |
| <span data-ttu-id="be127-158">**고급 그래픽 렌더링** 또는 비디오 편집 및 딥 러닝을 통한 모델 ND(학습 및 추론)</span><span class="sxs-lookup"><span data-stu-id="be127-158">**Heavy graphics rendering** or video editing, as well as model training and inferencing (ND) with deep learning.</span></span> | <span data-ttu-id="be127-159">NV, NC, NCv2, NCv3, ND</span><span class="sxs-lookup"><span data-stu-id="be127-159">NV, NC, NCv2, NCv3, ND</span></span> |
| <span data-ttu-id="be127-160">**HPC(고성능 컴퓨팅)** 선택적인 높은 처리량 네트워크 인터페이스를 갖춘 가장 빠르고 강력한 CPU 가상 머신이 필요한 경우</span><span class="sxs-lookup"><span data-stu-id="be127-160">**High-performance computing (HPC)** If you need the fastest and most powerful CPU virtual machines with optional high-throughput network interfaces.</span></span> | <span data-ttu-id="be127-161">H</span><span class="sxs-lookup"><span data-stu-id="be127-161">H</span></span> |

## <a name="choosing-storage-options"></a><span data-ttu-id="be127-162">저장소 옵션 선택</span><span class="sxs-lookup"><span data-stu-id="be127-162">Choosing storage options</span></span>

<span data-ttu-id="be127-163">다음과 같은 결정은 저장소를 고려하여 내려집니다.</span><span class="sxs-lookup"><span data-stu-id="be127-163">The next set of decisions revolve around storage.</span></span> <span data-ttu-id="be127-164">우선, 디스크 기술을 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-164">First, you can choose the disk technology.</span></span> <span data-ttu-id="be127-165">옵션으로는 기존의 플래터 기반 HDD(하드 디스크 드라이브) 또는 최신 SSD(반도체 드라이브)가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-165">Options include a traditional platter-based hard disk drive (HDD) or a more modern solid-state drive (SSD).</span></span> <span data-ttu-id="be127-166">구매한 하드웨어와 마찬가지로 SSD 저장소의 경우 더 많은 비용을 들이지만 더 나은 성능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-166">Just like the hardware you purchase, SSD storage costs more but provides better performance.</span></span>

> [!TIP]
> <span data-ttu-id="be127-167">사용 가능한 SSD 저장소에는 표준 및 프리미엄이라는 두 가지 수준이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-167">There are two levels of SSD storage available: standard and premium.</span></span> <span data-ttu-id="be127-168">워크로드는 정상이지만 더 나은 성능을 원하는 경우 표준 SSD 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-168">Choose Standard SSD disks if you have normal workloads but want better performance.</span></span> <span data-ttu-id="be127-169">데이터를 매우 빠르게 처리해야 하는 I/O 집약적인 워크로드 또는 중요 업무용 시스템이 있는 경우 프리미엄 SSD 디스크를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-169">Choose Premium SSD disks if you have I/O intensive workloads or mission-critical systems that need to process data very quickly.</span></span>

### <a name="mapping-storage-to-disks"></a><span data-ttu-id="be127-170">저장소를 디스크에 매핑</span><span class="sxs-lookup"><span data-stu-id="be127-170">Mapping storage to disks</span></span>

<span data-ttu-id="be127-171">Azure는 VHD(가상 하드 디스크)를 사용하여 VM의 실제 디스크를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be127-171">Azure uses Virtual hard disks (VHDs) to represent physical disks for the VM.</span></span> <span data-ttu-id="be127-172">VHD는 디스크 드라이브의 논리 형식과 데이터를 복제하지만 Azure Storage 계정에 페이지 Blob으로 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-172">VHDs replicate the logical format and data of a disk drive but are stored as page blobs in an Azure Storage account.</span></span> <span data-ttu-id="be127-173">사용해야 하는 저장소 유형은 디스크별로(SSD 또는 HDD) 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-173">You can choose on a per-disk basis what type of storage it should use (SSD or HDD).</span></span> <span data-ttu-id="be127-174">이렇게 하면 수행할 I/O에 따라 각 디스크의 성능을 제어할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-174">This allows you to control the performance of each disk, likely based on the I/O you plan to perform on it.</span></span>

<span data-ttu-id="be127-175">Linux VM에 대해 기본적으로 다음 두 개의 VHD(가상 하드 디스크)가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="be127-175">By default, two virtual hard disks (VHDs) will be created for your Linux VM:</span></span>

1. <span data-ttu-id="be127-176">**운영 체제 디스크**.</span><span class="sxs-lookup"><span data-stu-id="be127-176">The **Operating System disk**.</span></span> <span data-ttu-id="be127-177">기본 드라이브이며, 최대 용량은 2,048GB입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-177">This is your primary drive and has a maximum capacity of 2048 GB.</span></span> <span data-ttu-id="be127-178">기본적으로 `/dev/sda`라는 레이블이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-178">It will be labeled as `/dev/sda` by default.</span></span>

1. <span data-ttu-id="be127-179">**임시 디스크**.</span><span class="sxs-lookup"><span data-stu-id="be127-179">A **Temporary disk**.</span></span> <span data-ttu-id="be127-180">OS 또는 앱을 위한 임시 저장소를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-180">This provides temporary storage for the OS or any apps.</span></span> <span data-ttu-id="be127-181">Linux 가상 머신에서 디스크는 일반적으로 `/dev/sdb`이며, Azure Linux 에이전트에 의해 `/mnt`로 포맷되고 마운트됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-181">On Linux virtual machines, the disk is `/dev/sdb` and is formatted and mounted to `/mnt` by the Azure Linux Agent.</span></span> <span data-ttu-id="be127-182">VM 크기에 기반하여 크기가 지정되며 스왑 파일을 저장하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-182">It is sized based on the VM size and is used to store the swap file.</span></span> 

> [!WARNING]
> <span data-ttu-id="be127-183">임시 디스크는 영구적이지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-183">The temporary disk is not persistent.</span></span> <span data-ttu-id="be127-184">이 디스크에는 시스템에 중요하지 않은 데이터만 기록해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-184">You should only write data to this disk that is not critical to the system.</span></span>

#### <a name="what-about-data"></a><span data-ttu-id="be127-185">데이터의 경우는 어떨까요?</span><span class="sxs-lookup"><span data-stu-id="be127-185">What about data?</span></span>

<span data-ttu-id="be127-186">OS와 함께 기본 드라이브에 데이터를 저장할 수 있지만, 더 나은 방법은 전용 _데이터 디스크_를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-186">You can store data on the primary drive along with the OS, but a better approach is to create dedicated _data disks_.</span></span> <span data-ttu-id="be127-187">추가 디스크를 만들고 VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-187">You can create and attach additional disks to the VM.</span></span> <span data-ttu-id="be127-188">각 디스크에는 최대 4,095GB의 데이터를 저장할 수 있으며, 선택한 VM 크기에 따라 최대 저장 용량이 결정됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-188">Each disk can hold up to 4095 GB of data, with the maximum amount of storage determined by the VM size you select.</span></span>

> [!NOTE]
> <span data-ttu-id="be127-189">흥미로운 기능은 실제 디스크에서 VHD 이미지를 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-189">An interesting capability is to create a VHD image from a real disk.</span></span> <span data-ttu-id="be127-190">이 기능을 사용하면 _기존_ 정보를 온-프레미스 컴퓨터에서 클라우드로 쉽게 마이그레이션할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-190">This allows you to easily migrate _existing_ information from an on-premise computer to the cloud.</span></span>

### <a name="unmanaged-vs-managed-disks"></a><span data-ttu-id="be127-191">관리되지 않는 VM - 관리 디스크</span><span class="sxs-lookup"><span data-stu-id="be127-191">Unmanaged vs. managed disks</span></span>

<span data-ttu-id="be127-192">최종적으로, 저장소에서 **관리되지 않는** 디스크 또는 **관리** 디스크를 사용할지 여부를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-192">The final storage choice you'll make is whether to use **unmanaged** or **managed** disks.</span></span>

<span data-ttu-id="be127-193">관리되지 않는 디스크의 경우 VM 디스크에 해당하는 VHD를 유지하는 데 사용되는 저장소 계정을 사용자가 관리해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-193">With unmanaged disks, you are responsible for the storage accounts that are used to hold the VHDs that correspond to your VM disks.</span></span> <span data-ttu-id="be127-194">사용하는 공간에 대한 저장소 계정 요금을 사용자가 지불해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-194">You pay the storage account rates for the amount of space you use.</span></span> <span data-ttu-id="be127-195">단일 저장소 계정의 고정 속도 제한은 20,000 I/O 작업 수/초입니다. 즉 하나의 저장소 계정이 전체 제한에서 40개의 표준 가상 하드 디스크를 지원할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-195">A single storage account has a fixed rate limit of 20,000 I/O operations/sec. This means that a single storage account is capable of supporting 40 standard virtual hard disks at full throttle.</span></span> <span data-ttu-id="be127-196">규모를 확장해야 하는 경우에는 저장소 계정이 둘 이상 필요하기 때문에 복잡해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-196">If you need to scale out, then you need more than one storage account, which can get complicated.</span></span>

<span data-ttu-id="be127-197">관리 디스크는 권장되는 최신 디스크 저장소 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-197">Managed disks are the newer and recommended disk storage model.</span></span> <span data-ttu-id="be127-198">저장소 계정을 관리하는 부담이 Azure에서 해결되기 때문에 복잡한 업무가 원활하게 해결됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-198">They elegantly solve this complexity by putting the burden of managing the storage accounts onto Azure.</span></span> <span data-ttu-id="be127-199">사용자가 디스크 유형(프리미엄 또는 표준)과 디스크 크기를 지정하면, Azure에서 사용되는 디스크와 저장소가 _모두_ 만들어지고 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-199">You specify the disk type (Premium or Standard), and the size of the disk and Azure creates and manages both the disk _and_ the storage it uses.</span></span> <span data-ttu-id="be127-200">저장소 계정 제한에 대해 걱정할 필요가 없으므로 규모 확장이 쉬워집니다. 또한 여러 가지 다른 이점도 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="be127-200">You don't have to worry about storage account limits, which makes them easier to scale out. They also offer several other benefits:</span></span>

- <span data-ttu-id="be127-201">**안정성 향상**: Azure는 비슷한 수준의 탄력성을 제공하기 위해 안정성이 높은 VM과 연결된 VHD가 Azure 저장소의 다른 부분에 배치되도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-201">**Increased reliability**: Azure ensures that VHDs associated with high-reliability VMs will be placed in different parts of Azure storage to provide similar levels of resilience.</span></span>
- <span data-ttu-id="be127-202">**보안 강화**: 관리 디스크는 리소스 그룹에서 실제 관리되는 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="be127-202">**Better security**: Managed disks are real managed resources in the resource group.</span></span> <span data-ttu-id="be127-203">즉 역할 기반 액세스 제어를 사용하여 VHD 데이터로 작업할 수 있는 사용자를 제한할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-203">This means they can use role-based access control to restrict who can work with the VHD data.</span></span>
- <span data-ttu-id="be127-204">**스냅숏 지원**: 스냅숏을 사용하여 VHD의 읽기 전용 복사본을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-204">**Snapshot support**: Snapshots can be used to create a read-only copy of a VHD.</span></span> <span data-ttu-id="be127-205">소유하는 VM을 종료해야 하지만 스냅숏을 만드는 데는 몇 초 밖에 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-205">You have to shut down the owning VM but creating the snapshot only takes a few seconds.</span></span> <span data-ttu-id="be127-206">작업이 완료되면 VM의 전원을 켜고 스냅숏을 사용하여 복제된 VM을 만들어서 프로덕션 문제를 해결하거나 스냅숏을 만든 시점으로 VM을 롤백할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-206">Once it's done, you can power on the VM and use the snapshot to create a duplicate VM to troubleshoot a production issue or rollback the VM to the point in time that the snapshot was taken.</span></span>
- <span data-ttu-id="be127-207">**백업 지원**: 관리 디스크는 VM의 서비스에 영향을 주지 않으면서 Azure Backup을 사용하여 재해 복구를 위해 다른 지역에 자동으로 백업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-207">**Backup support**: Managed disks can be automatically backed up to different regions for disaster recovery with Azure Backup all without affecting the service of the VM.</span></span>

## <a name="network-communication"></a><span data-ttu-id="be127-208">네트워크 통신</span><span class="sxs-lookup"><span data-stu-id="be127-208">Network communication</span></span>

<span data-ttu-id="be127-209">가상 머신은 VNet(가상 네트워크)을 사용하여 외부 리소스와 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-209">Virtual machines communicate with external resources using a virtual network (VNet).</span></span> <span data-ttu-id="be127-210">VNet은 리소스가 통신하는 단일 지역의 사설 네트워크를 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="be127-210">The VNet represents a private network in a single region that your resources communicate on.</span></span> <span data-ttu-id="be127-211">가상 네트워크는 온-프레미스에서 관리하는 네트워크와 같습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-211">A virtual network is just like the networks you manage on-premises.</span></span> <span data-ttu-id="be127-212">가상 네트워크를 서브넷으로 분할하여 리소스를 격리시키고, 다른 네트워크(온-프레미스 네트워크 포함)에 연결하고, 인바운드 및 아웃바운드 연결을 제어하는 트래픽 규칙을 적용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-212">You can divide them up with subnets to isolate resources, connect them to other networks (including your on-premises networks), and apply traffic rules to govern inbound and outbound connections.</span></span>

### <a name="planning-your-network"></a><span data-ttu-id="be127-213">네트워크 계획</span><span class="sxs-lookup"><span data-stu-id="be127-213">Planning your network</span></span>

<span data-ttu-id="be127-214">새 VM을 만들 때 새 가상 네트워크를 만들거나 해당 지역의 기존 VNet을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-214">When you create a new VM, you will have the option of creating a new virtual network or using an existing VNet in your region.</span></span>

<span data-ttu-id="be127-215">Azure에서 VM과 함께 네트워크가 생성되도록 하는 것이 간단하지만 대부분의 시나리오에 적합하지 않을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-215">Having Azure create the network together with the VM is simple, but it's likely not ideal for most scenarios.</span></span> <span data-ttu-id="be127-216">아키텍처의 모든 구성 요소에 대한 네트워크 요구 사항을 _미리_ 계획하고, VNet 구조를 별도로 만드는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-216">It's better to plan your network requirements _up-front_ for all the components in your architecture and create the VNet structure separately.</span></span> <span data-ttu-id="be127-217">그런 다음, VM을 만들어서 이미 만들어진 VNet에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-217">Then create the VMs and place them into the already-created VNets.</span></span> <span data-ttu-id="be127-218">이 모듈의 뒷부분에서 가상 네트워크를 더 자세히 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-218">We'll look more at virtual networks later in this module.</span></span>

<span data-ttu-id="be127-219">가상 머신을 만들기 전에 VM을 어떻게 관리할지 결정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="be127-219">Before we create a virtual machine, we need to decide how we'd like to administer the VM.</span></span> <span data-ttu-id="be127-220">이제 옵션을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="be127-220">Let's look at our options.</span></span>