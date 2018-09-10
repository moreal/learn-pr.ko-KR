<span data-ttu-id="35aad-101">네트워크 인프라를 계획하고 몇 가지 VM을 식별하여 클라우드로 마이그레이션합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-101">You've planned out the network infrastructure and identified a few VMs to migrate to the cloud.</span></span> <span data-ttu-id="35aad-102">VM을 만들 수 있는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-102">You have several choices for creating your VMs.</span></span> <span data-ttu-id="35aad-103">이러한 옵션은 익숙한 환경에 따라 달라집니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-103">The choice you make depends on the environment you are comfortable with.</span></span> <span data-ttu-id="35aad-104">Azure는 리소스를 만들고 관리하기 위한 웹 기반 포털을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-104">Azure supports a web-based portal for creating and administering resources.</span></span> <span data-ttu-id="35aad-105">또한 MacOS, Windows 및 Linux에서 실행되는 명령줄 도구를 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-105">You can also choose to use command-line tools that run on MacOS, Windows, and Linux.</span></span>

> [!TIP]
> <span data-ttu-id="35aad-106">Microsoft Learn에서 하는 수행하는 모든 연습은 추가 비용이 들지 않지만, 탐색을 직접 시작하면 Azure 구독이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-106">All of the exercises you do in Microsoft Learn are free, but once you start exploring on your own, you will need an Azure subscription.</span></span> <span data-ttu-id="35aad-107">아직 구독이 없는 경우 몇 분 정도 시간을 내어 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-107">If you don't have one yet, take a couple of minutes and create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="35aad-108">먼저 Azure Portal을 살펴보겠습니다. 이는 Azure를 시작하는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-108">Let's explore the Azure portal first - it's the easiest way to start with Azure.</span></span>

## <a name="azure-portal"></a><span data-ttu-id="35aad-109">Azure Portal</span><span class="sxs-lookup"><span data-stu-id="35aad-109">Azure portal</span></span>

<span data-ttu-id="35aad-110">**Azure Portal**은 모든 Azure 리소스를 만들고 관리할 수 있는 사용하기 쉬운 브라우저 기반 사용자 인터페이스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-110">The **Azure portal** provides an easy to use browser-based user interface that allows you to create and manage all your Azure resources.</span></span> <span data-ttu-id="35aad-111">예를 들어 새 데이터베이스를 설정하고, Virtual Machines의 계산 성능을 높이고, 월별 비용을 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-111">For example, you can set up a new database, increase the compute power of your Virtual Machines, and monitor your monthly costs.</span></span> <span data-ttu-id="35aad-112">또한 사용 가능한 모든 리소스를 조사하고 단계별 마법사를 사용하여 필요한 리소스를 만들 수 있으므로 훌륭한 학습 도구이기도 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-112">It's also a great learning tool since you can survey all available resources and use guided wizards to create the ones you need.</span></span>

<span data-ttu-id="35aad-113">로그인하면 두 가지 주요 영역이 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-113">Once logged in, you're presented with two main areas.</span></span> <span data-ttu-id="35aad-114">첫 번째 영역은 리소스를 만들고, 리소스를 모니터링하고, 요금 청구를 관리하는 데 도움이 되는 옵션이 있는 메뉴입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-114">The first is a menu with the options to help you create resources, monitor resources and manage billing.</span></span> <span data-ttu-id="35aad-115">두 번째 영역은 Azure에 배포한 모든 필수 서비스의 스냅숏 보기를 제공하는 사용자 지정 가능한 대시보드입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-115">The second is a customizable dashboard that provides you with a snapshot view of all the essential services you've deployed to Azure.</span></span> <span data-ttu-id="35aad-116">Azure 사용을 시작할 때 가장 편안한 옵션을 사용하여 포털을 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-116">You'll most likely find the portal the most comfortable option to use when you start using Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="35aad-117">포털에서 선택할 때 표시되는 보기를 종종 _블레이드_라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-117">The views that are presented as you make selections in the portal are often called _blades_.</span></span> <span data-ttu-id="35aad-118">블레이드는 메뉴 구조 또는 구성 패널의 역할을 모두 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-118">A blade may act as both a menu structure or a configuration panel.</span></span> <span data-ttu-id="35aad-119">Azure Portal 전체를 탐색할 때 UI는 왼쪽에서 오른쪽으로 누적되며, 웹 뷰포트는 미끄러져 현재 블레이드를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-119">As you navigate throughout the Azure portal, UI will be stacked left-to-right, and the web viewport will slide over to show the current blade.</span></span> <span data-ttu-id="35aad-120">아래쪽의 슬라이더를 사용하여 부모 보기로 빠르게 다시 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-120">You can use the slider at the bottom to quickly move back to parent views.</span></span>

### <a name="create-an-azure-vm-with-the-azure-portal"></a><span data-ttu-id="35aad-121">Azure Portal을 사용하여 Azure VM 만들기</span><span class="sxs-lookup"><span data-stu-id="35aad-121">Create an Azure VM with the Azure portal</span></span>

<span data-ttu-id="35aad-122">WordPress 웹 사이트를 실행하는 VM을 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-122">Let's assume you want to create a VM running a WordPress website.</span></span> <span data-ttu-id="35aad-123">사이트를 설정하는 것은 어렵지 않지만 몇 가지 사항을 명심해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-123">Setting up a site isn't difficult, but there are a couple of things to keep in mind.</span></span> <span data-ttu-id="35aad-124">운영 체제를 설치 및 구성하고, 웹 사이트를 구성하고, 데이터베이스를 설치하고, 방화벽과 같은 것에 대해 걱정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-124">You need to install and configure an operating system, configure a website, install a database, and worry about things like firewalls.</span></span> <span data-ttu-id="35aad-125">다음 몇 가지 모듈에서 VM을 만드는 방법을 다루겠지만, 여기서는 VM을 만들어 이 작업이 얼마나 쉬운지 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-125">We're going to cover creating VMs in the next few modules, but let's create one here to see how easy it is.</span></span> <span data-ttu-id="35aad-126">모든 옵션을 살펴보지 않는 대신, **VM 만들기** 모듈 중 하나를 확인하여 각 옵션에 대한 전체 자세한 정보를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-126">We won't go through all the options - check out one of the **Create a VM** modules to get complete details on each option.</span></span>

1. <span data-ttu-id="35aad-127">[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-127">Sign in to [the Azure portal](https://portal.azure.com?azure-portal=true).</span></span> <span data-ttu-id="35aad-128">Azure 리소스 만들기 및 관리 메뉴가 왼쪽에 표시되고, 나머지 화면에는 대시보드가 채워집니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-128">You'll see Azure resource creation and management menu on your left and the dashboard filling the rest of the screen.</span></span>

    ![기본 Azure Portal 대시보드](../media-draft/3-dashboard-page.png)

1. <span data-ttu-id="35aad-130">포털 페이지의 왼쪽 위 모서리에서 **리소스 만들기** 옵션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-130">Click on the **Create a resource** option in the top left corner of the portal page.</span></span> <span data-ttu-id="35aad-131">그러면 Azure Marketplace 블레이드가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-131">This will open the Azure Marketplace blade.</span></span> <span data-ttu-id="35aad-132">왼쪽 사이드바가 접히면 녹색 '더하기' 기호가 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-132">If the left-hand sidebar is collapsed, it will be a green "plus".</span></span> <span data-ttu-id="35aad-133">위의 이미지와 같이 전체 텍스트를 보려면 확장 캐럿을 클릭하여 사이드바를 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-133">You can expand the sidebar by clicking the expand caret to see the full text as shown in the image above.</span></span>

    ![Azure Marketplace](../media-draft/3-create-new-resource.png)

    <span data-ttu-id="35aad-135">알 수 있듯이, 선택 가능한 옵션이 많이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-135">As you can see, there are many selectable options.</span></span> <span data-ttu-id="35aad-136">WordPress 웹 사이트를 실행하는 VM을 만들려고 한다는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="35aad-136">Remember we want to create VM running a WordPress website.</span></span> <span data-ttu-id="35aad-137">VM은 Azure 계산 리소스이므로 사용 가능한 목록에서 **계산** 옵션을 선택한 다음, WordPress VM 이미지를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-137">VMs are Azure compute resources, so select the **Compute** option on the available list and then search for WordPress VM images.</span></span>

1. <span data-ttu-id="35aad-138">**Marketplace 검색** 검색 창을 사용하여 "WordPress"를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-138">Use the **Search the Marketplace** search bar and look for "WordPress".</span></span> <span data-ttu-id="35aad-139">이제 옵션 목록이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-139">You should now see a list of options.</span></span> <span data-ttu-id="35aad-140">**WordPress Certified by Bitnami**(Bitnami 인증 WordPress)라는 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-140">Select the option that reads **WordPress Certified by Bitnami**.</span></span>

    ![Azure Marketplace 검색](../media-draft/3-search-vm-image.png)

    <span data-ttu-id="35aad-142">다음에 열리는 블레이드에서 사용하려는 이미지에 대한 라이선스 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-142">The blade that opens next will present licensing information for the image we're about to use.</span></span> <span data-ttu-id="35aad-143">**만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-143">Click on **Create**.</span></span>

    ![WordPress 사이트 선택 및 만들기](../media-draft/3-create-vm-image.png)

1. <span data-ttu-id="35aad-145">**가상 머신 만들기 블레이드**가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-145">You're presented with the **Create virtual machine blade**.</span></span> <span data-ttu-id="35aad-146">VM을 구성하는 데 사용할 수 있는 마법사 기반 방법에 유의하세요.</span><span class="sxs-lookup"><span data-stu-id="35aad-146">Notice the wizard-based approach we can use to configure the VM.</span></span>

    ![구성 단계 1](../media-draft/3-create-vm-1.png)

    <span data-ttu-id="35aad-148">WordPress 가상 머신의 기본 매개 변수를 구성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-148">We need to configure the basic parameters of our WordPress virtual machine.</span></span> <span data-ttu-id="35aad-149">이 시점에서 옵션 중 일부에 익숙하지 않더라도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-149">If some of the options at this point are unfamiliar to you, that is ok.</span></span> <span data-ttu-id="35aad-150">이후의 모듈에서 이러한 옵션 모두에 대해 설명한다는 것을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="35aad-150">Remember, we're going to discuss all of these options in a future module.</span></span> <span data-ttu-id="35aad-151">여기서 사용된 값을 복사하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-151">You're welcome to copy the values used here.</span></span>

<!-- TODO: fix subscription + resource group -->
1. <span data-ttu-id="35aad-152">**기본 사항** 탭에서 다음 값을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-152">Use the following values on the **Basics** tab.</span></span>
    - <span data-ttu-id="35aad-153">체험 구독 및 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-153">Select the free subscription and a Resource Group.</span></span>
    - <span data-ttu-id="35aad-154">VM에 대한 **이름**을 입력합니다. 여기서는 `test-wp1-eus-vm`을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-154">Enter a **Name** for the VM: here we've used `test-wp1-eus-vm`.</span></span>
    - <span data-ttu-id="35aad-155">가까운 **지역**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-155">Select a **Region** close to you.</span></span> <span data-ttu-id="35aad-156">드롭다운 목록을 사용하여 위치를 선택할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-156">You can use the drop-down list to select the location.</span></span>
    - <span data-ttu-id="35aad-157">가용성 옵션에 대해 **없음**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-157">Choose **None** for the availability options.</span></span> <span data-ttu-id="35aad-158">이 옵션은 다른 모듈에서 다루는 고가용성을 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-158">This is for high-availability which we cover in another module.</span></span>
    - <span data-ttu-id="35aad-159">**이미지**는 마켓플레이스에서 선택한 **WordPress by Bitnami**(Bitnami 인증 WordPress) 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-159">The **Image** should be the **Wordpress by Bitnami** option we selected from the marketplace.</span></span>
    - <span data-ttu-id="35aad-160">**크기**를 기본값으로 둡니다. 1개 코어와 3.5GB 메모리를 제공하므로 간단한 웹 사이트에는 충분합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-160">Leave the **Size** as the default - it will give you a single core and 3.5 GB of memory which should be sufficient for a simple website.</span></span>
    - <span data-ttu-id="35aad-161">인증 유형에 대해 **암호**로 전환하고, 사용자 이름과 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-161">Switch to **Password** for the authentication type and enter a username and password.</span></span>
    - <span data-ttu-id="35aad-162">**공용 인바운드 포트 선택** 드롭다운 목록을 열고 아래와 같이 **http**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-162">Open the **Select public inbound ports** drop-down list and select **http** as shown below.</span></span>

    ![HTTP 포트 열기](../media-draft/3-open-http-port.png)

1. <span data-ttu-id="35aad-164">VM을 만드는 중에 영향을 줄 수 있는 설정을 확인하기 위해 탐색할 수 있는 몇 가지 다른 탭이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-164">There are several other tabs you can explore to see the settings you can influence during the VM creation.</span></span> <span data-ttu-id="35aad-165">탐색이 완료되면 **검토 + 만들기**를 클릭하여 설정을 검토하고 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-165">Once you are finished exploring, click **Review + create** to review and validate the settings.</span></span>

    ![구성 단계 2](../media-draft/3-review-create-vm.png)

1. <span data-ttu-id="35aad-167">Azure는 검토 화면에서 설정을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-167">On the review screen, Azure will validate your settings.</span></span> <span data-ttu-id="35aad-168">모든 설정이 원하는 방식으로 설정되었는지 확인한 다음, **만들기**를 클릭하여 VM을 배포 및 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-168">Verify all the settings are set the way you want and then click **Create** to deploy and create the VM.</span></span>

1. <span data-ttu-id="35aad-169">배포는 **알림** 패널을 통해 모니터링할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-169">You can monitor the deployment through the **Notifications** panel.</span></span> <span data-ttu-id="35aad-170">위쪽 도구 모음에서 아이콘을 클릭하여 패널을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-170">Click the icon in the top toolbar to display the panel.</span></span>

    ![배포 진행률 모니터링](../media-draft/3-deploying.png)

1. <span data-ttu-id="35aad-172">VM 배포 프로세스를 완료하는 데 몇 분이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-172">The VM deployment process takes a few minutes to complete.</span></span> <span data-ttu-id="35aad-173">배포가 성공했다고 알려주는 알림을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-173">You'll receive a notification informing you that the deployment succeeded.</span></span> <span data-ttu-id="35aad-174">메시지를 클릭하여 VM에 대해 만들어진 모든 요소가 포함된 리소스 그룹으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-174">Click on the message to go to the resource group with all the elements that were created for your VM.</span></span>

    ![배포된 VM](../media-draft/3-deployment-succeeded.png)

1. <span data-ttu-id="35aad-176">VM 항목을 선택합니다. 첫 번째 항목이어야 하며, 지정한 이름이 적용되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-176">Select the VM entry - it should be the first one, it will have the name you specified.</span></span>

    ![리소스 그룹에서 VM 선택](../media-draft/3-open-vm-properties.png)

1. <span data-ttu-id="35aad-178">그러면 만든 가상 머신의 **개요**로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-178">That will navigate to the **Overview** of the virtual machine you have created.</span></span> <span data-ttu-id="35aad-179">여기서는 새로 만들어진 WordPress VM에 대한 모든 정보와 구성 옵션을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-179">Here you can see all the information and configuration options for your newly created WordPress VM.</span></span> <span data-ttu-id="35aad-180">정보 요소 중 하나는 **공용 IP 주소**입니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-180">One of the pieces of information is the **Public IP Address**.</span></span>

    ![VM에 공용 IP 주소 가져오기](../media-draft/3-public-ip-address.png)

1. <span data-ttu-id="35aad-182">IP 주소를 복사하고, 브라우저에서 새 탭을 연 다음, 이 IP 주소를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-182">Copy the IP address, open a new tab in your browser, and paste it in.</span></span> <span data-ttu-id="35aad-183">완전히 새로운 WordPress 사이트로 이동해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-183">It should browse to a brand new Wordpress site.</span></span>

    ![활성 상태의 새 WordPress 사이트](../media-draft/3-my-new-blog.png)

<span data-ttu-id="35aad-185">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="35aad-185">Congratulations!</span></span> <span data-ttu-id="35aad-186">몇 가지 단계를 통해 Linux를 실행하는 VM을 배포하고, 데이터베이스를 설치하고, 작동하는 웹 사이트를 구축했습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-186">With a few steps, you deployed a VM that runs Linux, has a database installed and a functional website.</span></span> <span data-ttu-id="35aad-187">VM을 만들 수 있는 몇 가지 다른 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="35aad-187">Let's explore some other ways we could have created a VM.</span></span>