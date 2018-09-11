<span data-ttu-id="9a2fa-101">모든 종류의 워크로드 인프라는 관리에 구성 작업이 개입됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-101">Managing the infrastructure of any type of workload involves configuration tasks.</span></span> <span data-ttu-id="9a2fa-102">이 구성을 수동으로 할 수 있지만, 수동 단계는 손이 많이 가고 오류가 발생하기 쉽고 비효율적입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-102">This configuration can be done manually, but manual steps can be labor-intensive, error prone, and inefficient.</span></span> <span data-ttu-id="9a2fa-103">Azure에서 수백 개의 시스템을 배포해야 하는 프로젝트를 맡았다면 어떻게 해야 할까요?</span><span class="sxs-lookup"><span data-stu-id="9a2fa-103">What if you are assigned to lead a project that required the deployment of hundreds of systems on Azure?</span></span> <span data-ttu-id="9a2fa-104">이러한 리소스를 어떻게 빌드하고 구성하시겠습니까?</span><span class="sxs-lookup"><span data-stu-id="9a2fa-104">How would you build and configure these resources?</span></span> <span data-ttu-id="9a2fa-105">시간이 얼마나 걸릴까요?</span><span class="sxs-lookup"><span data-stu-id="9a2fa-105">How long would this take?</span></span> <span data-ttu-id="9a2fa-106">시스템 간에 조금의 편차도 없이 각 시스템을 올바르게 구성할 수 있습니까?</span><span class="sxs-lookup"><span data-stu-id="9a2fa-106">Could you ensure that each system was configured properly, with no variance between them?</span></span> <span data-ttu-id="9a2fa-107">아키텍처 설계에 자동화를 사용하면 이러한 과제를 해결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-107">By using automation in your architecture design, you can work past these challenges.</span></span> <span data-ttu-id="9a2fa-108">Azure에서 자동화할 수 있는 몇 가지 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-108">Let's take a look at some of the ways you can automate on Azure.</span></span>

## <a name="infrastructure-as-code"></a><span data-ttu-id="9a2fa-109">코드로써의 인프라</span><span class="sxs-lookup"><span data-stu-id="9a2fa-109">Infrastructure as code</span></span>

<span data-ttu-id="9a2fa-110">서비스 및 인프라 배포를 자동화할 때 두 가지 방식이 있는데, 하나는 명령적이고 다른 하나는 선언적입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-110">When automating the deployment of services and infrastructure, there are two different approaches you can take: imperative and declarative.</span></span> <span data-ttu-id="9a2fa-111">명령적 방식에서는 원하는 결과를 얻기 위해 실행할 명령을 명시적으로 서술합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-111">In an imperative approach, you explicitly state the commands that are executed to produce the outcome you are looking for.</span></span> <span data-ttu-id="9a2fa-112">선언적 방식에서는 원하는 결과를 얻기 위해 실행할 방법을 지정하는 것이 아니라 어떤 결과를 원하는지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-112">With a declarative approach, you specify what you want the outcome to be instead of specifying how you want it done.</span></span> <span data-ttu-id="9a2fa-113">둘 다 좋은 방법이므로 무엇을 선택해도 괜찮습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-113">Both approaches are valuable, so there's no wrong choice.</span></span> <span data-ttu-id="9a2fa-114">이러한 차이점이 Azure에서 어떤 모습으로 나타날까요? 또 이러한 차이점을 어떻게 이용할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="9a2fa-114">What do these different approaches look like on Azure, and how do you use them?</span></span>

### <a name="imperative-automation"></a><span data-ttu-id="9a2fa-115">명령적 자동화</span><span class="sxs-lookup"><span data-stu-id="9a2fa-115">Imperative automation</span></span>

<span data-ttu-id="9a2fa-116">명령적 자동화부터 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-116">Let's start with imperative automation.</span></span> <span data-ttu-id="9a2fa-117">명령적 자동화에서는 _어떻게_ 할 것인지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-117">With imperative automation, we're specifying _how_ things are to be done.</span></span> <span data-ttu-id="9a2fa-118">일반적으로 이 작업은 언어 또는 SDK 스크립팅을 통해 프로그래밍 방식으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-118">This is typically done programmatically through a scripting language or SDK.</span></span> <span data-ttu-id="9a2fa-119">Azure 리소스의 경우 Azure CLI 또는 Azure PowerShell을 사용 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-119">For Azure resources, we could use the Azure CLI or Azure PowerShell.</span></span> <span data-ttu-id="9a2fa-120">Azure CLI를 사용하여 저장소 계정을 만드는 예제를 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-120">Let's take a look at an example that uses the Azure CLI to create a storage account.</span></span>

```azure-cli
az group create --name storage-resource-group --location westus
az storage account create --resource-group storage-resource-group --name mystorageaccount --kind BlobStorage --access-tier hot
```

<span data-ttu-id="9a2fa-121">이 예제에서는 이러한 리소스를 만드는 방법을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-121">In this example, we're specifying how to create these resources.</span></span> <span data-ttu-id="9a2fa-122">리소스 그룹을 만드는 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-122">Execute a command to create a resource group.</span></span> <span data-ttu-id="9a2fa-123">저장소 계정을 만드는 또 다른 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-123">Execute another command to create a storage account.</span></span> <span data-ttu-id="9a2fa-124">원하는 결과를 얻기 위해 어떤 명령을 실행할 것인지 Azure에 명시적으로 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-124">We're explicitly telling Azure what commands to run to produce the output we need.</span></span>

<span data-ttu-id="9a2fa-125">이 방식을 사용하면 인프라를 완전히 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-125">With this approach, we're able to fully automate our infrastructure.</span></span> <span data-ttu-id="9a2fa-126">입력 및 출력에 대한 영역을 제공할 수 있고, 매번 동일한 명령이 실행되게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-126">We can provide areas for input and output, and can ensure that the same commands are executed every time.</span></span> <span data-ttu-id="9a2fa-127">리소스를 자동화하여 프로세스에서 수동 단계를 제거하고, 리소스 관리가 보다 효율적으로 운영되도록 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-127">By automating our resources, we've taken the manual steps out of the process, making resource administration operationally more efficient.</span></span> <span data-ttu-id="9a2fa-128">그러나 이 방식에는 몇 가지 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-128">There are some downsides to this approach though.</span></span> <span data-ttu-id="9a2fa-129">아키텍처가 복잡해지면 리소스를 만드는 스크립트가 금방 복잡해질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-129">Scripts to create resources can quickly become complex as the architecture becomes more complex.</span></span> <span data-ttu-id="9a2fa-130">완전 실행을 보장하기 위해 오류 처리 및 입력 유효성 검사를 추가해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-130">Error handling and input validation may need to be added to ensure full execution.</span></span> <span data-ttu-id="9a2fa-131">명령이 변경될 수 있고, 스크립트의 지속적인 유지 관리가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-131">Commands may change, requiring ongoing maintenance of the scripts.</span></span>

### <a name="declarative-automation"></a><span data-ttu-id="9a2fa-132">선언적 자동화</span><span class="sxs-lookup"><span data-stu-id="9a2fa-132">Declarative automation</span></span>

<span data-ttu-id="9a2fa-133">선언적 자동화를 사용하는 경우 _어떤 결과_를 원하는지를 지정하고, 구체적인 실행 방법은 사용하는 시스템에 맡겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-133">With declarative automation, we're specifying _what_ we want our result to be, leaving the details of how it's done to the system we're using.</span></span> <span data-ttu-id="9a2fa-134">Azure에서 선언적 자동화는 Azure Resource Manager 템플릿을 사용하여 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-134">On Azure, declarative automation is done through the use of Azure Resource Manager templates.</span></span>

<span data-ttu-id="9a2fa-135">Resource Manager 템플릿은 무엇을 만들 것인지를 지정하는 JSON 구조 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-135">Resource Manager templates are JSON-structured files that specify what we want created.</span></span> <span data-ttu-id="9a2fa-136">아래 예제에서는 우리가 지정하는 이름과 속성을 사용하여 저장소 계정을 만들도록 Azure에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-136">In the example below, we're telling Azure to create a storage account with the names and properties that we specify.</span></span> <span data-ttu-id="9a2fa-137">이 저장소 계정을 만들기 위해 실행되는 실제 단계는 Azure에 맡겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-137">The actual steps that are executed to create this storage account are left to Azure.</span></span> <span data-ttu-id="9a2fa-138">템플릿에는 매개 변수, 변수, 리소스 및 출력의 4개 섹션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-138">Templates have four sections: parameters, variables, resources, and outputs.</span></span> <span data-ttu-id="9a2fa-139">매개 변수는 템플릿 내에서 사용할 입력을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-139">Parameters handle input to be used within the template.</span></span> <span data-ttu-id="9a2fa-140">변수는 템플릿 전체에서 사용할 값을 저장하는 방법을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-140">Variables provide a way to store values for use throughout the template.</span></span> <span data-ttu-id="9a2fa-141">리소스는 생성된 것이고, 출력은 생성된 것에 대한 세부 정보를 사용자에게 제공하는 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-141">Resources are the things that are being created, and outputs are a way to provide details to the user of what was created.</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "name": {
            "type": "string"
        },
        "location": {
            "type": "string"
        },
        "accountType": {
            "type": "string",
            "defaultValue": "Standard_RAGRS"
        },
        "kind": {
            "type": "string"
        },
        "accessTier": {
            "type": "string"
        },
        "httpsTrafficOnlyEnabled": {
            "type": "bool",
            "defaultValue": true
        }
    },
    "variables": {
    },
    "resources": [
        {
            "apiVersion": "2018-02-01",
            "name": "[parameters('name')]",
            "location": "[parameters('location')]",
            "type": "Microsoft.Storage/storageAccounts",
            "sku": {
                "name": "[parameters('accountType')]"
            },
            "kind": "[parameters('kind')]",
            "properties": {
                "supportsHttpsTrafficOnly": "[parameters('httpsTrafficOnlyEnabled')]",
                "accessTier": "[parameters('accessTier')]",
                "encryption": {
                    "services": {
                        "blob": {
                            "enabled": true
                        },
                        "file": {
                            "enabled": true
                        }
                    },
                    "keySource": "Microsoft.Storage"
                }
            },
            "dependsOn": []
        }
    ],
    "outputs": {
        "storageAccountName": {
            "type": "string",
            "value": "[parameters('name')]"
        }
    }
}
```

<span data-ttu-id="9a2fa-142">템플릿은 Azure에서 모든 서비스를 만들고 조작하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-142">Templates can be used to create and manipulate every service on Azure.</span></span> <span data-ttu-id="9a2fa-143">코드 리포지토리 및 제어되는 소스에 저장할 수 있으며, 개발 중인 인프라가 실제로 프로덕션 중인 인프라와 일치하도록 환경 간에 공유됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-143">They can be stored in code repositories and source controlled, and shared across environments to ensure that the infrastructure being developed against matches what's actually in production.</span></span> <span data-ttu-id="9a2fa-144">배포를 자동화하고 일관성을 유지하고 배포 구성 오류를 제거하고 작업 속도를 높일 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-144">They are a great way to automate deployments and help ensure consistency, eliminate deployment misconfigurations, and can increase operational speed.</span></span>

<span data-ttu-id="9a2fa-145">인프라 배포 자동화는 훌륭한 첫 번째 단계이지만, 가상 머신을 배포하는 경우 할 일이 더 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-145">Automating your infrastructure deployment is a great first step, but when deploying virtual machines, there's still more work to do.</span></span> <span data-ttu-id="9a2fa-146">배포 후 구성을 자동화화는 몇 가지 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-146">Let's take a look at a couple of approaches to automating configuration post deployment.</span></span>

## <a name="vm-customization-images-vs-post-deployment-configuration"></a><span data-ttu-id="9a2fa-147">VM 사용자 지정: 이미지 vs 배포 후 구성</span><span class="sxs-lookup"><span data-stu-id="9a2fa-147">VM customization: images vs. post-deployment configuration</span></span>

<span data-ttu-id="9a2fa-148">많은 가상 머신 배포에서, 머신이 실행 중인 동안에는 작업이 수행되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-148">For many virtual machine deployments, the job isn't done when the machine is running.</span></span> <span data-ttu-id="9a2fa-149">VM이 실제로 목표를 달성하려면 추가 구성이 필요할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-149">It's likely there's additional configuration that's needed before the VM can actually serve its intended purpose.</span></span> <span data-ttu-id="9a2fa-150">디스크 추가 시 포맷이 필요할 수 있고, VM을 도메인에 조인해야 할 수 있고, 관리 소프트웨어용 에이전트를 설치해야 할 수 있고, 실제 워크로드를 설치하고 구성해야 할 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-150">Additional disks might need formatting, the VM might need to be joined to a domain, maybe an agent for a management software needs to be installed, and most likely the actual workload requires installation and configuration as well.</span></span>

<span data-ttu-id="9a2fa-151">VM 자체의 구성으로 간주되는 구성 작업에 적용되는 두 가지 일반적인 전략이 있는데, 전략마다 장점과 단점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-151">There are two common strategies applied for the configuration work considered to be part the configuration of the VM itself, both of which have advantages and disadvantages:</span></span>

* <span data-ttu-id="9a2fa-152">사용자 지정 이미지</span><span class="sxs-lookup"><span data-stu-id="9a2fa-152">Custom images</span></span>
* <span data-ttu-id="9a2fa-153">배포 후 스크립팅</span><span class="sxs-lookup"><span data-stu-id="9a2fa-153">Post-deployment scripting</span></span>

<span data-ttu-id="9a2fa-154">가상 머신을 배포한 후 실행 중인 인스턴스에서 소프트웨어를 구성 또는 설치하면 사용자 지정 이미지가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-154">Custom images are generated by deploying a virtual machine and then configuring or installing software on that running instance.</span></span> <span data-ttu-id="9a2fa-155">모든 것을 올바르게 구성한 후 머신을 종료하면 VM에서 이미지가 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-155">When everything is configured correctly, the machine can be shut down, and an image is created from the VM.</span></span> <span data-ttu-id="9a2fa-156">생성된 이미지를 다른 새 가상 머신의 기준으로 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-156">The image can then be used as a base for other new virtual machines.</span></span> <span data-ttu-id="9a2fa-157">사용자 지정 이미지를 사용하면 전체 배포 시간을 줄일 수 있습니다. 가상 머신을 배포하고 실행하면 추가 구성이 필요 없기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-157">Working with custom images can speed up the overall time of your deployment as once the virtual machine is deployed and running, no additional configuration would be needed.</span></span> <span data-ttu-id="9a2fa-158">배포 속도가 중요한 경우 사용자 지정 이미지를 잘 살펴볼 필요가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-158">If deployment speed is an important factor, custom images are definitely worth exploring.</span></span>

<span data-ttu-id="9a2fa-159">배포 후 스크립팅은 일반적으로 기본 기준 이미지를 활용하며, VM이 배포된 후에는 스크립팅 또는 구성 관리 플랫폼을 사용하여 구성 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-159">Post-deployment scripting typically leverages a basic base image, then relies on scripting or a configuration management platform to do configuration after the VM is deployed.</span></span> <span data-ttu-id="9a2fa-160">Azure 스크립트 확장을 통해 VM에서 스크립트를 실행하여 또는 Azure Automation DSC(Desired State Configuration) 같은 견고한 솔루션을 활용하여 배포 후 스크립트를 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-160">The post-deployment scripting could be done by executing a script on the VM through the Azure Script Extension or by leveraging a more robust solution such as Azure Automation Desired State Configuration (DSC).</span></span>

<span data-ttu-id="9a2fa-161">방법마다 고려해야 할 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-161">Each approach has some considerations to keep in mind.</span></span> <span data-ttu-id="9a2fa-162">이미지를 사용하는 경우 이미지 업데이트, 보안 패치 및 이미지 자체의 인벤토리 관리를 처리하기 위한 프로세스가 있는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-162">When using images, you'll need to ensure there's a process to handle image updates, security patches, and inventory management of the images themselves.</span></span> <span data-ttu-id="9a2fa-163">배포 후 스크립팅을 사용하는 경우 빌드가 완료되기 전에는 실시간 워크로드에 VM을 추가할 수 없으므로 빌드 시간이 길어질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-163">With post-deployment scripting, build times can be extended since the VM can't be added to live workloads until the build is complete.</span></span> <span data-ttu-id="9a2fa-164">독립 실행형 시스템에서는 이것이 별 문제가 아닐 수 있지만, 가상 머신 확장 집합처럼 자동으로 크기가 조정되는 서비스를 사용하는 경우 빌드 시간이 길어지면 크기 조정 시간에 영향을 줄 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-164">This may not be a significant issue for standalone systems, but when using services that autoscale (such as virtual machine scale sets), this extended build time can impact how quickly you can scale.</span></span> <span data-ttu-id="9a2fa-165">두 방법 모두 구성 드리프트를 해결해야 합니다. 새 구성이 롤아웃되면 그에 따라 기존 시스템을 업데이트해야 하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-165">With both approaches, you'll want to ensure you address configuration drift; as new configuration is rolled out, you'll need to ensure that existing systems are updated accordingly.</span></span>

<span data-ttu-id="9a2fa-166">리소스 배포를 자동화하면 환경에 엄청난 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-166">Automating resource deployment can be a massive benefit to your environment.</span></span> <span data-ttu-id="9a2fa-167">배포 시간이 단축되고 오류가 줄어들면 운영 역량이 한 수준 높아질 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-167">The amount of time saved and error reduced can move your operational capabilities to another level.</span></span>

## <a name="automation-of-operational-tasks"></a><span data-ttu-id="9a2fa-168">운영 작업의 자동화</span><span class="sxs-lookup"><span data-stu-id="9a2fa-168">Automation of operational tasks</span></span>

<span data-ttu-id="9a2fa-169">솔루션이 시작 및 실행되면 지속적인 운영 작업을 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-169">Once your solutions are up and running, there are ongoing operational activities that can also be automated.</span></span> <span data-ttu-id="9a2fa-170">Azure Automation을 사용하여 이러한 작업을 자동화하면 수동 워크로드가 감소하고, 계산 리소스의 구성 및 업데이트 관리를 사용할 수 있고, 일정/자격 증명/인증서 같은 공유 리소스를 중앙 집중화하고, 모든 종류의 Azure 작업을 실행하는 프레임워크가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-170">Automating these tasks with Azure Automation reduces manual workloads, enables configuration and update management of compute resources, centralizes shared resources such as schedules, credentials, and certificates, and provides a framework for running any type of Azure task.</span></span>

<span data-ttu-id="9a2fa-171">Lamna Healthcare 작업의 경우 다음이 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-171">For your Lamna Healthcare work, this might include:</span></span>
- <span data-ttu-id="9a2fa-172">분리된 디스크를 주기적으로 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-172">Periodically searching for orphaned disks.</span></span>
- <span data-ttu-id="9a2fa-173">VM에 최신 보안 패치를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-173">Installing the latest security patches on VMs.</span></span>
- <span data-ttu-id="9a2fa-174">업무 외 시간에 가상 머신을 검색하고 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-174">Searching for and shutting down virtual machines in off-hours.</span></span>
- <span data-ttu-id="9a2fa-175">고위 임원에게 보고할 일일 보고서를 실행하고 대시보드를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-175">Running daily reports and producing a dashboard to report to senior management.</span></span>

![VM 전원 상태 자동화](../media-draft/automation-vm-power-state.png)

## <a name="automating-development-environments"></a><span data-ttu-id="9a2fa-177">개발 환경 자동화</span><span class="sxs-lookup"><span data-stu-id="9a2fa-177">Automating development environments</span></span>

<span data-ttu-id="9a2fa-178">클라우드 인프라의 반대편 파이프라인에는 개발자가 비즈니스의 핵심이 되는 응용 프로그램 및 서비스를 작성하기 위해 사용하는 개발 머신이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-178">At the other end of the pipeline of your cloud infrastructure are the development machines used by developers to write the applications and services that are the core of your business.</span></span> <span data-ttu-id="9a2fa-179">개발자는 적절한 도구 및 필요한 리포지토리와 함께 Azure DevTest Labs를 사용하여 VM에 스탬프를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-179">You can use Azure DevTest Labs to stamp out VMs with all of the correct tools and repositories that they need.</span></span> <span data-ttu-id="9a2fa-180">여러 서비스를 작업하는 개발자는 새 머신을 직접 프로비전할 필요 없이 개발 환경 간에 전환할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-180">Developers working on multiple services can switch between development environments without having to provision a new machine themselves.</span></span> <span data-ttu-id="9a2fa-181">이러한 개발 환경은 사용하지 않을 때에는 종료하고 다시 필요하게 되면 다시 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-181">These development environments can be shut down when not in use and restarted when they are required again.</span></span>

## <a name="automation-at-lamna-healthcare"></a><span data-ttu-id="9a2fa-182">Lamna Healthcare의 자동화</span><span class="sxs-lookup"><span data-stu-id="9a2fa-182">Automation at Lamna Healthcare</span></span>

<span data-ttu-id="9a2fa-183">Lamna Healthcare가 자동화를 사용한 후 어떻게 달라졌는지 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-183">Let's take a look at how Lamna Healthcare has improved by using automation.</span></span> <span data-ttu-id="9a2fa-184">자동화를 처음 시작할 당시에는 인프라 배포 및 서버 빌드가 완전히 수동이었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-184">When you started your journey, infrastructure deployment and server builds were entirely manual.</span></span> <span data-ttu-id="9a2fa-185">엔지니어들은 포털을 통해 모든 것을 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-185">Engineers were deploying everything through the portal.</span></span> <span data-ttu-id="9a2fa-186">테스트 및 프로덕션 환경 간에 편차와 오류가 발생했으며, 이러한 편차로 인해 코드를 프로덕션하기 전에는 문제를 감지할 수 없었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-186">This was introducing variance and errors between test and production environments, and the differences were hindering their ability to detect problems before code hit production.</span></span>

<span data-ttu-id="9a2fa-187">이제 Lamna Healthcare는 Resource Manager 템플릿을 통해 모든 인프라를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-187">They now deploy all their infrastructure through Resource Manager templates.</span></span> <span data-ttu-id="9a2fa-188">이러한 템플릿은 GitHub 리포지토리에 체크 인 되고, 배포용으로 릴리스되기 전에 미리 코드를 검토합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-188">These templates are checked into a GitHub repository, and a code review happens before they are released for deployment.</span></span> <span data-ttu-id="9a2fa-189">또한 개발, 테스트 및 프로덕션 환경에서 똑같은 인프라를 빌드할 수 있으므로 모든 환경에서 구성의 유효성을 검사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-189">They're also able to build the same infrastructure between dev, test, and production, ensuring they have validated their configuration across all environments.</span></span>

<span data-ttu-id="9a2fa-190">가상 머신을 사용하는 대부분의 서비스에서, 표준 기본 이미지를 보유하고 있으며 DSC를 사용하여 배포 후 시스템을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-190">For most services using virtual machines, they have a standard base image and use DSC to configure the systems post deployment.</span></span> <span data-ttu-id="9a2fa-191">가상 머신 확장 집합의 확장성이 필요한 웹 팜의 경우 코드를 체크 인하고 새 이미지를 빌드하는 프로세스를 완전히 자동화하고, 필요한 구성을 모두 내장하여 확장 집합에서 사용할 수 있게 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-191">For web farms where they need the scalability of virtual machine scale sets, they have a fully automated process to check in code and build a new image with all required configuration built in before making it available in their scale sets.</span></span>

<span data-ttu-id="9a2fa-192">업무 외 시간에는 식별된 가상 머신을 종료하는 자동화 작업을 통해 비용을 줄였으며, VM 패치도 자동화했습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-192">They have an Automation job to shut down identified virtual machines in off-hours to reduce costs and have automated their VM patching as well.</span></span>

<span data-ttu-id="9a2fa-193">이제 개발자는 최신 이미지 및 구성을 통해 개발할 수 있는 DevTest Labs에서 셀프 서비스 환경을 사용하므로 이들이 개발하는 것이 프로덕션의 구성과 일치합니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-193">Developers now have a self-service environment in DevTest Labs where they can develop against the latest images and configuration, ensuring that what they develop against matches the configuration in production.</span></span>

<span data-ttu-id="9a2fa-194">이를 위해 약간의 사전 노력이 필요했지만, 결국에는 노력에 대한 보상을 충분히 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-194">All of this took some up-front effort, but the benefits have paid off in the long run.</span></span> <span data-ttu-id="9a2fa-195">운영 팀이 환경을 유지하기 위해 드는 노력과 오류 발생률이 현저하게 감소했습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-195">They've dramatically reduced error and the effort required by their operations teams to maintain their environments.</span></span> <span data-ttu-id="9a2fa-196">개발자는 개발에 필요한 리소스를 간편하게 프로비전할 수 있게 되어, 환경을 만들기 위해 왔다 갔다 할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-196">Developers love that they can easily go provision resources to develop against, eliminating the back and forth to get environments created.</span></span>

## <a name="summary"></a><span data-ttu-id="9a2fa-197">요약</span><span class="sxs-lookup"><span data-stu-id="9a2fa-197">Summary</span></span>

<span data-ttu-id="9a2fa-198">아키텍처에 자동화 기능을 도입하는 여러 가지 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-198">We've taken a look at a number of ways to bring automation capabilities into your architecture.</span></span> <span data-ttu-id="9a2fa-199">인프라를 코드로 배포할 수 있는 점부터 랩 환경을 통해 개발자 생산성을 높일 수 있는 점까지, 환경을 자동화하여 얻을 수 있는 수많은 이점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-199">From deploying infrastructure as code, to improving developer productivity with lab environments, there's a ton of benefit from taking time to automate your environment.</span></span> <span data-ttu-id="9a2fa-200">오류를 줄이고, 편차를 줄이고, 운영 비용을 절감할 수 있다는 것은 조직에 엄청난 이점을 주며 클라우드 환경을 한 차원 높은 수준으로 발전시킬 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a2fa-200">Reducing error, reducing variance, and saving operational costs can be a significant benefit to your organization and help take your cloud environment to the next level.</span></span>