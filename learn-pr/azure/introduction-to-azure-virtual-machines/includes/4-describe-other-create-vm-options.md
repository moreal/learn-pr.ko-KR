<span data-ttu-id="e668c-101">Azure Portal은 시작할 때 VM과 같은 리소스를 만드는 가장 쉬운 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-101">The Azure portal is the easiest way to create resources such as VMs when you are getting started.</span></span> <span data-ttu-id="e668c-102">그러나 Azure를 사용하는 가장 효율적이거나 가장 빠른 방법은 아닙니다. 특히 여러 리소스를 함께 만들어야 하는 경우에는 더욱 그렇습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-102">However, it's not necessarily the most efficient or quickest way to work with Azure, particularly if you need to create several resources together.</span></span> <span data-ttu-id="e668c-103">따라서 여기서는 서로 다른 작업을 처리하는 수십 개의 VM을 만들 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-103">In our case, we will eventually be creating dozens of VMs to handle different tasks.</span></span> <span data-ttu-id="e668c-104">Azure Portal에서 수동으로 만드는 것은 재미 있는 작업이 아닙니다!</span><span class="sxs-lookup"><span data-stu-id="e668c-104">Creating them manually in the Azure portal wouldn't be a fun task!</span></span>

<span data-ttu-id="e668c-105">Azure에서 리소스를 만들고 관리하는 몇 가지 다른 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-105">Let's look at some other ways to create and administer resources in Azure:</span></span>

- [<span data-ttu-id="e668c-106">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e668c-106">Azure Resource Manager</span></span>](#Azure_RM)
- [<span data-ttu-id="e668c-107">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e668c-107">Azure PowerShell</span></span>](#Azure_PowerShell)
- [<span data-ttu-id="e668c-108">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e668c-108">Azure CLI</span></span>](#Azure_CLI)
- [<span data-ttu-id="e668c-109">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="e668c-109">Azure REST API</span></span>](#Azure_REST_API)
- [<span data-ttu-id="e668c-110">Azure 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="e668c-110">Azure Client SDK</span></span>](#Azure_Client_SDK)
- [<span data-ttu-id="e668c-111">Azure VM 확장</span><span class="sxs-lookup"><span data-stu-id="e668c-111">Azure VM Extensions</span></span>](#Azure_VMExtensions)
- [<span data-ttu-id="e668c-112">Azure Automation Services</span><span class="sxs-lookup"><span data-stu-id="e668c-112">Azure Automation Services</span></span>](#Azure_Automation)

<a name="Azure_RM" />

## <a name="azure-resource-manager"></a><span data-ttu-id="e668c-113">Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="e668c-113">Azure Resource Manager</span></span>

<span data-ttu-id="e668c-114">동일한 설정을 사용하여 VM 복사본을 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-114">Let's assume you want to create a copy of a VM with the same settings.</span></span> <span data-ttu-id="e668c-115">VM 이미지를 만들고, Azure에 업로드하고, 새 VM에 대한 기준으로 참조할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-115">You could create a VM image, upload it to Azure and reference it as the basis for your new VM.</span></span> <span data-ttu-id="e668c-116">이 프로세스는 비효율적이며 시간 소모적입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-116">This process is inefficient and time-consuming.</span></span> <span data-ttu-id="e668c-117">Azure는 정확한 VM 복사본을 만드는 데 사용할 템플릿을 만드는 옵션을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-117">Azure provides you with the option to create a template from which to create an exact copy of a VM.</span></span>

<span data-ttu-id="e668c-118">일반적으로 Azure 인프라에는 많은 리소스가 포함되며, 그 중 대부분은 몇 가지 방식으로 서로 관련되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-118">Typically, your Azure infrastructure will contain many resources, many of them related to one another in some way.</span></span> <span data-ttu-id="e668c-119">예를 들어 여기서 만든 VM에는 WordPress 사이트를 실행하기 위해 함께 만든 가상 머신 자체, 저장소, 네트워크 인터페이스, 웹 서버 및 데이터베이스가 모두 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-119">For example, the VM we created has the virtual machine itself, storage, network interface, web server, and a database - all created together to run the WordPress site.</span></span> <span data-ttu-id="e668c-120">**Azure Resource Manager**는 이러한 관련 리소스를 더 효율적으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-120">**Azure Resource Manager** makes working with these related resources more efficient.</span></span> <span data-ttu-id="e668c-121">모든 리소스를 함께 배포, 업데이트 또는 삭제할 수 있는 명명된 **리소스 그룹**에 리소스를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-121">It organizes resources into named **Resource Groups** that let you deploy, update, or delete all of the resources together.</span></span> <span data-ttu-id="e668c-122">WordPress 사이트를 만들었을 때 VM 만들기의 일환으로 리소스 그룹을 식별했고 Resource Manager에서 관련 리소스를 동일한 그룹에 배치했습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-122">When we created the WordPress site, we identified the Resource Group as part of the VM creation, and Resource Manager placed the associated resources into the same group.</span></span>

<span data-ttu-id="e668c-123">또한 Resource Manager를 사용하면 특정 구성을 만들고 배포하는 데 사용할 수 있는 _템플릿_을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-123">Resource Manager also allows you to create _templates_ which can be used to create and deploy specific configurations.</span></span>

### <a name="what-are-resource-manager-templates"></a><span data-ttu-id="e668c-124">Resource Manager 템플릿이란?</span><span class="sxs-lookup"><span data-stu-id="e668c-124">What are Resource Manager templates?</span></span>

<span data-ttu-id="e668c-125">**Resource Manager 템플릿**은 솔루션에 배포해야 하는 리소스를 정의하는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-125">**Resource Manager templates** are JSON files that define the resources you need to deploy for your solution.</span></span>

<span data-ttu-id="e668c-126">Automation 스크립트 옵션을 선택하여 특정 VM에 대한 **설정** 섹션에서 리소스 템플릿을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-126">You can create resource templates from the **Settings** section for a specific VM by selecting the Automation script option.</span></span>

![VM에 대한 Automation 스크립트](../media-draft/4-automation-script.png)

<span data-ttu-id="e668c-128">나중에 사용할 리소스 템플릿을 저장하거나 이 템플릿을 기반으로 하여 새 VM을 즉시 배포하는 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-128">You have the option to save the resource template for later use or immediately deploy a new VM based on this template.</span></span> <span data-ttu-id="e668c-129">예를 들어 테스트 환경에서 템플릿을 통해 VM을 만들 수 있으며, 온-프레미스 머신을 교체하지 못할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-129">For example, you might create a VM from a template in a test environment and find it doesn’t quite work to replace your on-premise machine.</span></span> <span data-ttu-id="e668c-130">리소스 그룹을 삭제하면 모든 리소스를 삭제하고 템플릿을 조정한 다음, 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-130">You can delete the resource group, which deletes all of the resources, tweak the template and try again.</span></span> <span data-ttu-id="e668c-131">기존의 배포된 리소스만 변경하려는 경우 해당 리소스를 만드는 데 사용된 템플릿을 변경하여 다시 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-131">If you only want to make changes to the existing deployed resources, you can change the template used to create it and deploy it again.</span></span> <span data-ttu-id="e668c-132">Resource Manager는 새 템플릿과 일치하도록 리소스를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-132">Resource Manager will change the resources to match the new template.</span></span>

<span data-ttu-id="e668c-133">원하는 방식으로 작업한 후에는 해당 템플릿을 가져와서 준비 및 프로덕션과 같은 여러 버전의 인프라를 쉽게 다시 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-133">Once you have it working the way you want it, you can take that template and easily re-create multiple versions of your infrastructure, such as staging and production.</span></span> <span data-ttu-id="e668c-134">VM 이름, 네트워크 이름, 저장소 계정 이름 등과 같은 필드를 매개 변수화하고, 다른 매개 변수를 사용하여 각 환경을 사용자 지정하는 템플릿을 반복적으로 로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-134">You can parameterize fields such as the VM name, network name, storage account name, etc., and load the template repeatedly, using different parameters to customize each environment.</span></span>

<span data-ttu-id="e668c-135">Azure CLI, Azure PowerShell 또는 Azure REST API와 같은 자동화 스크립팅 도구를 원하는 프로그래밍 언어와 함께 사용하여 리소스 템플릿을 처리함으로써 인프라를 빠르게 구동할 수 있는 강력한 도구가 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-135">You can use automation scripting tools such as the Azure CLI, Azure PowerShell, or even the Azure REST APIs with your favorite programming language to process resource templates making this a powerful tool for quickly spinning up your infrastructure.</span></span>

<a name="Azure_PowerShell" />

## <a name="azure-powershell"></a><span data-ttu-id="e668c-136">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="e668c-136">Azure PowerShell</span></span>

<span data-ttu-id="e668c-137">관리 스크립트를 만드는 것은 워크플로를 최적화하는 강력한 방법입니다. 즉 일상적인 반복 작업을 자동화할 수 있으며, 스크립트가 확인되면 일관되게 실행되어 오류를 줄일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-137">Creating administration scripts is a powerful way to optimize your workflow, you can automate everyday, repetitive tasks, and once a script has been verified, it will run consistently, likely reducing errors.</span></span> <span data-ttu-id="e668c-138">**Azure PowerShell**은 일회성 대화형 작업 또는 반복 작업 자동화에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-138">**Azure PowerShell** is ideal for one-off interactive tasks and or the automate of repeated tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="e668c-139">PowerShell은 셸 창과 명령 구문 분석과 같은 서비스를 제공하는 플랫폼 간 셸입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-139">PowerShell is a cross-platform shell that provides services like the shell window and command parsing.</span></span> <span data-ttu-id="e668c-140">Azure PowerShell은 Azure 관련 명령(**cmdlet**이라고 함)을 추가하는 선택적 추가 기능 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-140">Azure PowerShell is an optional add-on package which adds the Azure-specific commands (referred to as **cmdlets**).</span></span> <span data-ttu-id="e668c-141">별도의 학습 모듈에서 Azure PowerShell을 설치하고 사용하는 방법에 대해 자세히 알아볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-141">You can learn more about installing and using Azure PowerShell in a separate training module.</span></span>

<span data-ttu-id="e668c-142">예를 들어 `New-AzureRmVM` cmdlet을 사용하여 새 Azure Virtual Machine을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-142">For example, you can use the `New-AzureRmVM` cmdlet to create a new Azure Virtual Machine.</span></span> 

```powershell
New-AzureRmVm `
    -ResourceGroupName "TestResourceGroup" `
    -Name "test-wp1-eus-vm" `
    -Location "East US" `
    -VirtualNetworkName "test-wp1-eus-network" `
    -SubnetName "default" `
    -SecurityGroupName "test-wp1-eus-nsg" `
    -PublicIpAddressName "test-wp1-eus-pubip" `
    -OpenPorts 80,3389
```

<span data-ttu-id="e668c-143">다음과 같이 다양한 매개 변수를 제공하여 사용 가능한 많은 VM 구성 설정을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-143">As shown here, you supply various parameters to handle the large number of VM configuration settings available.</span></span> <span data-ttu-id="e668c-144">대부분의 매개 변수에는 적절한 값이 있으므로 필요한 매개 변수만 지정하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-144">Most of the parameters have reasonable values; you only need to specify the required parameters.</span></span> <span data-ttu-id="e668c-145">**PowerShell을 통해 스크립트를 사용하여 Azure 작업 자동화** 모듈에서 Azure PowerShell을 사용하여 VM을 만들고 관리하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e668c-145">Learn more about creating and managing VMs with Azure PowerShell in the **Automate Azure tasks using scripts with PowerShell** module.</span></span>
<a name="Azure_CLI" />

## <a name="azure-cli"></a><span data-ttu-id="e668c-146">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="e668c-146">Azure CLI</span></span>

<span data-ttu-id="e668c-147">스크립팅 및 명령줄 Azure 상호 작용을 위한 또 다른 옵션은 **Azure CLI**입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-147">Another option for scripting and command-line Azure interaction is the **Azure CLI**.</span></span>

<span data-ttu-id="e668c-148">Azure CLI는 명령줄에서 가상 머신 및 디스크와 같은 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-148">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources such as virtual machines and disks from the command line.</span></span> <span data-ttu-id="e668c-149">Cloud Shell을 통해 macOS, Linux 및 Windows 또는 브라우저에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-149">It's available for macOS, Linux, and Windows, or in the browser using the Cloud Shell.</span></span> <span data-ttu-id="e668c-150">Azure PowerShell과 마찬가지로 Azure CLI는 관리 워크플로를 간소화할 수 있는 강력한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-150">Like Azure PowerShell, the Azure CLI is a powerful way to streamline your administrative workflow.</span></span> <span data-ttu-id="e668c-151">Azure PowerShell과 달리 Azure CLI는 PowerShell 없이 작동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-151">Unlike Azure PowerShell, the Azure CLI does not need PowerShell to function.</span></span>

<span data-ttu-id="e668c-152">예를 들어 `az vm create` 명령을 사용하여 Azure VM을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-152">For example, you can create an Azure VM with the `az vm create` command.</span></span>

```bash
az vm create \
    --resource-group TestResourceGroup \
    --name test-wp1-eus-vm \
    --image win2016datacenter \
    --admin-username jonc \
    --admin-password aReallyGoodPasswordHere
```

<span data-ttu-id="e668c-153">Azure CLI는 다른 스크립팅 언어(예: Ruby 및 Python)와 함께 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-153">The Azure CLI can be used with other scripting languages, for example, Ruby and Python.</span></span> <span data-ttu-id="e668c-154">두 언어는 모두 개발자가 PowerShell에 익숙하지 않을 수 있는 비 Windows 기반 머신에서 일반적으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-154">Both languages are commonly used on non-windows based machines where the developer may not be familiar with PowerShell.</span></span>

<span data-ttu-id="e668c-155">**Azure CLI 도구를 사용하여 가상 머신 관리** 모듈에서 VM을 만들고 관리하는 방법에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="e668c-155">Learn more about creating and managing VMs in the **Manage virtual machines with the Azure CLI tool** module.</span></span>

## <a name="programmatic-apis"></a><span data-ttu-id="e668c-156">프로그래밍 방식(API)</span><span class="sxs-lookup"><span data-stu-id="e668c-156">Programmatic (APIs)</span></span>

<span data-ttu-id="e668c-157">일반적으로 실행할 간단한 스크립트가 있고 명령줄 도구를 사용하려는 경우 Azure PowerShell과 Azure CLI는 모두 적절한 옵션입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-157">Generally speaking, both Azure PowerShell and Azure CLI are good options if you have simple scripts to run and want to stick to command-line tools.</span></span> <span data-ttu-id="e668c-158">VM 만들기 및 관리가 복잡한 논리를 사용하는 더 큰 응용 프로그램의 일부를 구성하는 더 복잡한 시나리오에서는 다른 접근 방식이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-158">When it comes to more complex scenarios where the creation and management of VM form part of a larger application with complex logic, another approach is needed.</span></span>

<span data-ttu-id="e668c-159">Azure에서는 모든 종류의 리소스와 프로그래밍 방식으로 상호 작용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-159">You can interact with every type of resource in Azure programmatically.</span></span>

<a name="Azure_REST_API" />

### <a name="azure-rest-api"></a><span data-ttu-id="e668c-160">Azure REST API</span><span class="sxs-lookup"><span data-stu-id="e668c-160">Azure REST API</span></span>

<span data-ttu-id="e668c-161">Azure REST API는 VM을 만들고 관리하는 기능뿐만 아니라 리소스별로 분류된 개발자 작업도 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-161">The Azure REST API provides developers operations categorized by resource as well as the ability to create and manage VMs.</span></span> <span data-ttu-id="e668c-162">작업은 해당 HTTP 메서드(`GET`, `PUT`, `POST`, `DELETE` 및 `PATCH`) 및 해당 응답과 함께 URI로 노출됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-162">Operations are exposed as URIs with corresponding HTTP methods (`GET`, `PUT`, `POST`, `DELETE`, and `PATCH`) and a corresponding response.</span></span>

<span data-ttu-id="e668c-163">Azure Compute API는 가상 머신 및 지원 리소스에 프로그래밍 방식으로 액세스할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-163">The Azure Compute APIs give you programmatic access to virtual machines and their supporting resources.</span></span> <span data-ttu-id="e668c-164">이 API를 사용하여 수행할 수 있는 작업은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-164">With this API, you have operations to:</span></span>

- <span data-ttu-id="e668c-165">가용성 집합 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e668c-165">Create and manage availability sets</span></span>
- <span data-ttu-id="e668c-166">가상 머신 확장 추가 및 관리</span><span class="sxs-lookup"><span data-stu-id="e668c-166">Add and manage virtual machine extensions</span></span>
- <span data-ttu-id="e668c-167">관리 디스크, 스냅숏, 이미지 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e668c-167">Create and manage managed disks, snapshots, and images</span></span>
- <span data-ttu-id="e668c-168">Azure에서 사용할 수 있는 플랫폼 이미지에 액세스</span><span class="sxs-lookup"><span data-stu-id="e668c-168">Access the platform images available in Azure</span></span>
- <span data-ttu-id="e668c-169">리소스 사용량 정보 검색</span><span class="sxs-lookup"><span data-stu-id="e668c-169">Retrieve usage information of your resources</span></span>
- <span data-ttu-id="e668c-170">가상 머신 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e668c-170">Create and manage virtual machines</span></span>
- <span data-ttu-id="e668c-171">가상 머신 확장 집합 만들기 및 관리</span><span class="sxs-lookup"><span data-stu-id="e668c-171">Create and manage virtual machine scale sets</span></span>

<a name="Azure_Client_SDK" />

### <a name="azure-client-sdk"></a><span data-ttu-id="e668c-172">Azure 클라이언트 SDK</span><span class="sxs-lookup"><span data-stu-id="e668c-172">Azure Client SDK</span></span>

<span data-ttu-id="e668c-173">REST API는 플랫폼과 언어에 구속받지 않지만, 대부분의 경우 개발자는 더 높은 수준의 추상화를 추구합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-173">Even though the REST API is platform and language agnostic, most often developers will look towards a higher level of abstraction.</span></span> <span data-ttu-id="e668c-174">Azure 클라이언트 SDK는 Azure REST API를 캡슐화하여 개발자가 Azure와 더 쉽게 상호 작용할 수 있도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-174">The Azure Client SDK encapsulates the Azure REST API making it much easier for developers to interact with Azure.</span></span>

<span data-ttu-id="e668c-175">Azure 클라이언트 SDK는 C#, Java, Node.js, PHP, Python, Ruby 및 Go와 같은 .NET 기반 언어를 포함한 다양한 언어 및 프레임워크에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-175">The Azure Client SDKs are available for a variety of languages and frameworks including .NET based languages such as C#, Java, Node.js, PHP, Python, Ruby, and Go.</span></span>

<span data-ttu-id="e668c-176">`Microsoft.Azure.Management.Fluent` NuGet 패키지를 사용하여 Azure VM을 만드는 C# 코드 조각의 예제는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-176">Here's an example snippet of C# code to create an Azure VM using the `Microsoft.Azure.Management.Fluent` NuGet package:</span></span>

```csharp
var azure = Azure
    .Configure()
    .WithLogLevel(HttpLoggingDelegatingHandler.Level.Basic)
    .Authenticate(credentials)
    .WithDefaultSubscription();
// ...
var vmName = "test-wp1-eus-vm";

azure.VirtualMachines.Define(vmName)
    .WithRegion(Region.USEast)
    .WithExistingResourceGroup("TestResourceGroup")
    .WithExistingPrimaryNetworkInterface(networkInterface)
    .WithLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .WithAdminUsername("jonc")
    .WithAdminPassword("aReallyGoodPasswordHere")
    .WithComputerName(vmName)
    .WithSize(VirtualMachineSizeTypes.StandardDS1)
    .Create();
```

<span data-ttu-id="e668c-177">**Azure Java SDK**를 사용하는 Java의 동일한 코드 조각은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-177">Here's the same snippet in Java using the **Azure Java SDK**:</span></span>

```java
String vmName = "test-wp1-eus-vm";
// ...
VirtualMachine virtualMachine = azure.virtualMachines()
    .define(vmName)
    .withRegion(Region.US_EAST)
    .withExistingResourceGroup("TestResourceGroup")
    .withExistingPrimaryNetworkInterface(networkInterface)
    .withLatestWindowsImage("MicrosoftWindowsServer", "WindowsServer", "2012-R2-Datacenter")
    .withAdminUsername("jonc")
    .withAdminPassword("aReallyGoodPasswordHere")
    .withComputerName(vmName)
    .withSize("Standard_DS1")
    .create();
```

<a name="Azure_VMExtensions" />

## <a name="azure-vm-extensions"></a><span data-ttu-id="e668c-178">Azure VM 확장</span><span class="sxs-lookup"><span data-stu-id="e668c-178">Azure VM Extensions</span></span>

<span data-ttu-id="e668c-179">초기 배포 후에 가상 머신에 추가 소프트웨어를 구성하고 설치한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-179">Let's assume you want to configure and install additional software on your virtual machine after the initial deployment.</span></span> <span data-ttu-id="e668c-180">이 작업에서는 자동으로 모니터링되고 실행되는 특정 구성을 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-180">You want this task to use a specific configuration, monitored and executed automatically.</span></span>

<span data-ttu-id="e668c-181">**Azure VM 확장**은 초기 배포 후에 Azure VM에서 작업을 구성하고 자동화할 수 있는 작은 응용 프로그램입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-181">**Azure VM extensions** are small applications that allow you to configure and automate tasks on Azure VMs after initial deployment.</span></span> <span data-ttu-id="e668c-182">**Azure VM 확장**은 Azure CLI, PowerShell, Azure Resource Manager 템플릿 및 Azure Portal을 사용하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-182">**Azure VM extensions** can be run with the Azure CLI, PowerShell, Azure Resource Manager templates, and the Azure portal.</span></span>

<span data-ttu-id="e668c-183">새 VM 배포와 함께 확장을 번들로 제공하거나 기존 시스템에 대해 확장을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-183">You bundle extensions with a new VM deployment or run them against an existing system.</span></span>

<a name="Azure_Automation" />

## <a name="azure-automation-services"></a><span data-ttu-id="e668c-184">Azure Automation Services</span><span class="sxs-lookup"><span data-stu-id="e668c-184">Azure Automation Services</span></span>

<span data-ttu-id="e668c-185">원격 인프라를 관리할 때 마주치는 가장 중요한 운영 관리 과제 중 일부는 시간을 절약하고, 오류를 줄이고, 효율성을 높이는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-185">Saving time, reducing errors, and increasing efficiency are some of the most significant operational management challenges faced when managing remote infrastructure.</span></span> <span data-ttu-id="e668c-186">인프라 서비스가 많은 경우 더 높은 수준에서 운영할 수 있도록 Azure에서 고급 서비스를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-186">If you have a lot of infrastructure services, you might want to consider using higher-level services in Azure to help you operate from a higher level.</span></span>

<span data-ttu-id="e668c-187">**Azure Automation**을 사용하면 빈번하고 시간 소모적이며 오류가 발생하기 쉬운 관리 작업을 쉽게 자동화할 수 있는 서비스를 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-187">**Azure Automation** allows you to integrate services that allow you to automate frequent, time-consuming and error-prone management tasks with ease.</span></span> <span data-ttu-id="e668c-188">이러한 서비스에는 **프로세스 자동화**, \*\*구성 관리 및 **업데이트 관리**가 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-188">These services include **process automation**, \*\*configuration management, and **update management**.</span></span>

- <span data-ttu-id="e668c-189">**프로세스 관리**.</span><span class="sxs-lookup"><span data-stu-id="e668c-189">**Process Management**.</span></span> <span data-ttu-id="e668c-190">특정 오류 이벤트에 대해 모니터링되는 VM이 있다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-190">Let's assume you have a VM that is monitored for a specific error event.</span></span> <span data-ttu-id="e668c-191">작업을 수행하고 보고되는 즉시 문제를 해결하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-191">You want to take action and fix the problem as soon as it's reported.</span></span> <span data-ttu-id="e668c-192">프로세스 자동화를 통해 데이터 센터에서 발생할 수 있는 이벤트에 응답할 수 있는 감시자 작업을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-192">Process automation allows you to set up watcher tasks that can respond to events that may occur in your datacenter.</span></span>

- <span data-ttu-id="e668c-193">**구성 관리**.</span><span class="sxs-lookup"><span data-stu-id="e668c-193">**Configuration Management**.</span></span>  <span data-ttu-id="e668c-194">VM에서 실행되는 운영 체제에서 사용할 수 있는 소프트웨어 업데이트를 추적하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-194">Perhaps you want to track software updates that become available for the operating system that runs on your VM.</span></span> <span data-ttu-id="e668c-195">포함하거나 제외할 수 있는 특정 업데이트가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-195">There are specific updates you may want to include or exclude.</span></span> <span data-ttu-id="e668c-196">구성 관리를 통해 이러한 업데이트를 추적하고 필요에 따라 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-196">Configuration management allows you to track these updates and take action as required.</span></span> <span data-ttu-id="e668c-197">**System Center Configuration Manager**를 사용하여 회사의 PC, 서버 및 모바일 장치를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-197">You use **System Center Configuration Manager** to manage your company's PC, servers, and mobile devices.</span></span> <span data-ttu-id="e668c-198">Configuration Manager를 사용하여 이 지원을 Azure VM으로 확장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-198">You can extend this support to your Azure VMs with Configuration Manager.</span></span>

- <span data-ttu-id="e668c-199">**업데이트 관리**.</span><span class="sxs-lookup"><span data-stu-id="e668c-199">**Update Management**.</span></span> <span data-ttu-id="e668c-200">VM에 대한 업데이트 및 패치를 관리하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-200">This is used to manage updates and patches for your VMs.</span></span> <span data-ttu-id="e668c-201">이 서비스를 통해 사용 가능한 업데이트의 상태를 평가하고, 설치를 예약하고, 배포 결과를 검토하여 업데이트가 성공적으로 적용되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-201">With this service, you're able to assess the status of available updates, schedule installation, and review deployment results to verify updates applied successfully.</span></span> <span data-ttu-id="e668c-202">업데이트 관리는 프로세스 및 구성 관리를 제공하는 서비스를 통합합니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-202">Update management incorporates services that provide process and configuration management.</span></span> <span data-ttu-id="e668c-203">**Azure Automation** 계정에서 직접 VM에 대한 업데이트 관리를 사용하도록 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-203">You enable update management for a VM directly from your **Azure Automation** account.</span></span> <span data-ttu-id="e668c-204">또한 포털의 가상 머신 블레이드에서 단일 가상 머신에 대한 업데이트 관리를 허용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-204">You can also allow update management for a single virtual machine from the virtual machine blade in the portal.</span></span>

<span data-ttu-id="e668c-205">알 수 있듯이, Azure는 리소스를 만들고 관리할 수 있는 다양한 도구를 제공하여 관리 작업을 _사용자에게 적합한_ 프로세스에 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-205">As you can see, Azure provides a variety of tools to create and administer resources so you can integrate management operations into a process _that works for you_.</span></span> <span data-ttu-id="e668c-206">Azure의 다른 서비스 중 일부에서 인프라 리소스가 원활하게 실행되고 있는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e668c-206">Let's examine some of the other services Azure to make sure your infrastructure resources are running smoothly.</span></span>
