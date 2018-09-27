<span data-ttu-id="22ea2-101">회사에서 클라우드로 전환하는 과정의 일환으로 여러 서버를 배포하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-101">Suppose your company is deploying several servers as part of their cloud transition.</span></span> <span data-ttu-id="22ea2-102">디스크가 항상 취약성이 없는 상태로 유지되도록 배포 중에 VM 디스크를 암호화해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-102">VM disks must be encrypted during the deployment, so there's no time when the disks are vulnerable.</span></span> <span data-ttu-id="22ea2-103">이 프로세스를 자동화하고 암호화를 자동으로 사용하도록 Azure Resource Manager 템플릿을 수정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-103">You want to automate this process, and have to modify the Azure Resource Manager templates to automatically enable encryption.</span></span>

<span data-ttu-id="22ea2-104">여기서는 Azure Resource Manager 템플릿을 사용하여 새 Windows VM에 대한 암호화를 자동으로 활성화하는 방법을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-104">Here, we'll look at how to use an Azure Resource Manager template to automatically enable encryption for new Windows VMs.</span></span>

## <a name="what-are-azure-resource-manager-templates"></a><span data-ttu-id="22ea2-105">Azure Resource Manager 템플릿이란?</span><span class="sxs-lookup"><span data-stu-id="22ea2-105">What are Azure Resource Manager templates?</span></span>

<span data-ttu-id="22ea2-106">Resource Manager 템플릿은 Azure에 배포할 리소스 집합을 정의하는 데 사용되는 JSON 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-106">Resource Manager templates are JSON files used to define a set of resources to deploy to Azure.</span></span> <span data-ttu-id="22ea2-107">템플릿을 새로 작성할 수도 있고, VM을 비롯한 일부 Azure 리소스의 경우에는 Azure Portal을 사용하여 템플릿을 생성할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-107">You can write them from scratch, and for some Azure resources, including VMs, you can use the Azure portal to generate them.</span></span> <span data-ttu-id="22ea2-108">수동 VM 배포에 필요한 정보 작성을 완료해야 하지만 VM을 Azure에 배포하는 대신 템플릿을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-108">You'll need to complete the required information for a manual VM deployment, but instead of deploying the VM to Azure, you save the template.</span></span> <span data-ttu-id="22ea2-109">그런 다음, 해당 특정 VM 구성을 만들려면 템플릿을 _다시 사용_할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-109">You can then _reuse_ the template to create that specific VM configuration.</span></span>

<span data-ttu-id="22ea2-110">모든 종류의 관리 태스크를 자동화하기 위해 [문서에서 사용 가능한 예제 템플릿](https://azure.microsoft.com/resources/templates)이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-110">There are [example templates available in docs](https://azure.microsoft.com/resources/templates) to automate all sorts of administrative tasks.</span></span> <span data-ttu-id="22ea2-111">실제로 수동으로 관리한 VM을 암호화하려면 이러한 템플릿 중 하나를 사용했을 수 있습니다!</span><span class="sxs-lookup"><span data-stu-id="22ea2-111">In fact, we could have used one of these templates to encrypt our VM that we just did manually!</span></span>

![Azure 템플릿을 보여 주는 스크린샷](../media/5-browse-templates.png)

## <a name="using-github-templates"></a><span data-ttu-id="22ea2-113">GitHub 템플릿 사용</span><span class="sxs-lookup"><span data-stu-id="22ea2-113">Using GitHub templates</span></span>

<span data-ttu-id="22ea2-114">실제 템플릿 원본은 GitHub에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-114">The actual template source is stored in GitHub.</span></span> <span data-ttu-id="22ea2-115">GitHub의 템플릿으로 이동하고 페이지에서 Azure로 바로 배포할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-115">You can browse to a template in GitHub and deploy right to Azure from the page.</span></span>

![강조 표시된 Azure 단추에 배포되는 GitHub 템플릿을 보여 주는 스크린샷](../media/5-deploy-from-github.png)

<span data-ttu-id="22ea2-117">템플릿이 배포될 때 Azure는 필수 입력 필드 목록을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-117">When the template is deployed, Azure will display a list of required input fields.</span></span>

![Azure Portal에서 템플릿을 보여 주는 스크린샷](../media/5-fill-in-template.png)

<span data-ttu-id="22ea2-119">그런 다음, 템플릿을 실행하여 리소스를 만들거나 수정하거나 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-119">You can then execute the template to create, modify, or remove resources.</span></span>

### <a name="running-templates-in-the-azure-portal"></a><span data-ttu-id="22ea2-120">Azure Portal에서 템플릿 실행</span><span class="sxs-lookup"><span data-stu-id="22ea2-120">Running templates in the Azure portal</span></span>

<span data-ttu-id="22ea2-121">사용하려는 템플릿을 이미 알고 있거나 Azure 계정에 템플릿을 저장한 경우 **리소스 만들기** > **템플릿 배포** 리소스를 사용하여 포털에서 정의된 템플릿을 찾아 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-121">If you already know the template you want to use, or you have saved templates in your Azure account, you can use the **Create a resource** > **Template Deployment** resource to locate and run defined templates in the portal.</span></span> <span data-ttu-id="22ea2-122">이름으로 템플릿을 검색할 수 있으며, GUI에서 템플릿을 실행하고 매개 변수 또는 동작을 변경하기 위해 템플릿을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-122">You can search through templates by name, edit a template to change the parameters or behavior, and execute the template right from the GUI.</span></span>

### <a name="running-templates-from-the-command-line"></a><span data-ttu-id="22ea2-123">명령줄에서 템플릿 실행</span><span class="sxs-lookup"><span data-stu-id="22ea2-123">Running templates from the command line</span></span>

<span data-ttu-id="22ea2-124">템플릿에 URL을 지정하면 Azure PowerShell에서 템플릿을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-124">Given a URL to a template, you can execute it with Azure PowerShell.</span></span> <span data-ttu-id="22ea2-125">예를 들어 다음과 같은 PowerShell 명령을 사용하여 디스크 암호화 템플릿을 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-125">For example, we could run the disk encryption template with the following PowerShell command:</span></span>

```powershell
New-AzureRmResourceGroupDeployment `
    -Name encrypt-disk `
    -ResourceGroupName <resource-group-name> `
    -TemplateUri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

<span data-ttu-id="22ea2-126">또는 Azure CLI를 선호하는 경우 `group deployment create` 명령을 사용하여 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22ea2-126">Or, if you prefer the Azure CLI, with the `group deployment create` command.</span></span>

```azurecli
azure config mode arm
azure group deployment create <my-resource-group> <my-deployment-name> \ 
    --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-encrypt-running-windows-vm-without-aad/azuredeploy.json
```

