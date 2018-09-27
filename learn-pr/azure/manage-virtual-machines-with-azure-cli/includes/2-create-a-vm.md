<span data-ttu-id="5e795-101">Azure Virtual Machine 만들기라는 가장 확실한 작업을 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-101">Let's start with the most obvious task: creating an Azure Virtual Machine.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="logins-subscriptions-and-resource-groups"></a><span data-ttu-id="5e795-102">로그인, 구독 및 리소스 그룹</span><span class="sxs-lookup"><span data-stu-id="5e795-102">Logins, subscriptions, and resource groups</span></span>

<span data-ttu-id="5e795-103">오른쪽의 Azure Cloud Shell에서 작업하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-103">You'll be working in the Azure Cloud Shell on the right.</span></span> <span data-ttu-id="5e795-104">샌드박스를 활성화하면 Microsoft Learn에 의해 관리되는 무료 구독을 사용하여 Azure에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-104">Once you activate the sandbox, you'll be logged into Azure with a free subscription managed by Microsoft Learn.</span></span> <span data-ttu-id="5e795-105">직접 Azure에 로그인하거나 구독을 선택하지 않아도 됩니다. 이 작업은 자동으로 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-105">You don't have to log into Azure on your own, or select a subscription - this will be done for you.</span></span> <span data-ttu-id="5e795-106">또한 일반적으로 새 리소스를 보유하려면 _리소스 그룹_을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-106">In addition, normally you would create a _resource group_ to hold new resources.</span></span> <span data-ttu-id="5e795-107">이 모듈에서 Azure 샌드박스는 모든 명령을 실행하는 데 사용할 수 있는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-107">In this module, the Azure sandbox will create a resource group for you which will be used to execute all the commands.</span></span>

## <a name="create-a-linux-vm-with-the-azure-cli"></a><span data-ttu-id="5e795-108">Azure CLI를 사용하여 Linux VM 만들기</span><span class="sxs-lookup"><span data-stu-id="5e795-108">Create a Linux VM with the Azure CLI</span></span>

<span data-ttu-id="5e795-109">Azure CLI에는 Azure의 가상 머신에서 작동하는 `vm` 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-109">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="5e795-110">여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-110">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="5e795-111">가장 일반적인 하위 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-111">The most common include:</span></span>

| <span data-ttu-id="5e795-112">하위 명령</span><span class="sxs-lookup"><span data-stu-id="5e795-112">Sub-command</span></span> | <span data-ttu-id="5e795-113">설명</span><span class="sxs-lookup"><span data-stu-id="5e795-113">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="5e795-114">새 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="5e795-114">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="5e795-115">가상 머신 할당 취소</span><span class="sxs-lookup"><span data-stu-id="5e795-115">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="5e795-116">가상 머신 삭제</span><span class="sxs-lookup"><span data-stu-id="5e795-116">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="5e795-117">구독에 있는 생성된 가상 머신 나열</span><span class="sxs-lookup"><span data-stu-id="5e795-117">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="5e795-118">인바운드 트래픽에 대해 특정 네트워크 포트 열기</span><span class="sxs-lookup"><span data-stu-id="5e795-118">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="5e795-119">가상 머신 다시 시작</span><span class="sxs-lookup"><span data-stu-id="5e795-119">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="5e795-120">가상 머신에 대한 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="5e795-120">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="5e795-121">중지된 가상 머신 시작</span><span class="sxs-lookup"><span data-stu-id="5e795-121">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="5e795-122">실행 중인 가상 머신 중지</span><span class="sxs-lookup"><span data-stu-id="5e795-122">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="5e795-123">가상 머신의 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="5e795-123">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="5e795-124">전체 명령 목록은 [Azure CLI 참조 설명서](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-124">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="5e795-125">첫 번째 항목(`az vm create`)으로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-125">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="5e795-126">이 명령은 리소스 그룹에서 가상 머신을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-126">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="5e795-127">새 VM의 모든 측면을 구성하기 위해 전달할 수 있는 여러 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-127">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="5e795-128">제공해야 하는 세 개의 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-128">The three parameters that must be supplied are:</span></span>

> [!div class="mx-tableFixed"]
> | <span data-ttu-id="5e795-129">매개 변수</span><span class="sxs-lookup"><span data-stu-id="5e795-129">Parameter</span></span> | <span data-ttu-id="5e795-130">설명</span><span class="sxs-lookup"><span data-stu-id="5e795-130">Description</span></span> |
> |-----------|-------------|
> | `resource-group` | <span data-ttu-id="5e795-131">가상 머신을 소유할 리소스 그룹은 **<rgn>[샌드박스 리소스 그룹]</rgn>** 을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-131">The resource group that will own the virtual machine, use **<rgn>[sandbox Resource Group]</rgn>**.</span></span> |
> | `name` | <span data-ttu-id="5e795-132">가상 머신의 이름은 리소스 그룹 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-132">The name of the virtual machine - must be unique within the resource group.</span></span> |
> | `image` | <span data-ttu-id="5e795-133">VM을 만드는 데 사용할 운영 체제 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-133">The operating system image to use to create the VM.</span></span> |
> | `location` | <span data-ttu-id="5e795-134">VM을 배치할 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-134">The region to place the VM in.</span></span> <span data-ttu-id="5e795-135">지역은 일반적으로 VM의 소비자와 가깝습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-135">Typically this would be close to the consumer of the VM.</span></span> <span data-ttu-id="5e795-136">이 연습에서는 다음 목록 중 가까운 위치를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-136">In this exercise, choose a location nearby from the following list.</span></span> |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

<span data-ttu-id="5e795-137">또한 VM이 만들어지는 동안 진행률을 확인하기 위해 `--verbose` 플래그를 추가하는 것이 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-137">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="5e795-138">Linux 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="5e795-138">Create a Linux virtual machine</span></span>

<span data-ttu-id="5e795-139">새 Linux 가상 머신을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-139">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="5e795-140">Azure Cloud Shell에서 다음 명령을 실행하여 "미국 서부" 위치에서 Debian Linux 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-140">Execute the following command in Azure Cloud Shell to create a Debian Linux machine in the "West US" location.</span></span> <span data-ttu-id="5e795-141">가까이에 없으면 위치를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-141">Change the location if that one isn't nearby.</span></span>

```azurecli
az vm create --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --location westus --verbose 
```

[!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]


<span data-ttu-id="5e795-142">이 명령은 이름이 `SampleVM`인 새 **Debian** Linux 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-142">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="5e795-143">VM을 만드는 동안 Azure CLI 도구가 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-143">Notice that the Azure CLI tool waits while the VM is being created.</span></span> <span data-ttu-id="5e795-144">`--no-wait` 옵션을 추가하여 Azure CLI 도구가 즉시 반환되도록 지시하고 Azure가 백그라운드에서 VM을 계속 만들도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-144">You can add the `--no-wait` option to tell the Azure CLI tool to return immediately and have Azure continue creating the VM in the background.</span></span> <span data-ttu-id="5e795-145">스크립트에서 명령을 실행하는 경우에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-145">This is useful if you're executing the command in a script.</span></span> <span data-ttu-id="5e795-146">스크립트의 뒷부분에서 `azure vm wait --name [vm-name]` 명령을 사용하여 VM이 만들어질 때까지 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="5e795-146">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="5e795-147">자세한 응답 내용을 살펴보면 VM에 대한 다양한 종속성을 명명하는 데 `SampleVM` 이름이 사용되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-147">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```output
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="5e795-148">`vm create`에 대한 선택적 매개 변수(예: `--vnet-name` 및 `--public-ip-address-dns-name`)를 사용하여 자동 생성된 이러한 리소스 이름을 재정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-148">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="5e795-149">여기서는 `admin-username` 플래그를 통해 관리자 계정 이름을 **"aldis"** 로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-149">We are specifying the administrator account name through the `admin-username` flag to be **"aldis"**.</span></span> <span data-ttu-id="5e795-150">이를 생략하면 `vm create` 명령이 _현재 사용자 이름_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-150">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="5e795-151">계정 이름에 대한 규칙이 OS마다 다르므로 고유한 이름을 지정하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-151">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> 

> [!NOTE]
> <span data-ttu-id="5e795-152">“root” 및 “admin”과 같은 일반적인 이름은 대부분의 이미지에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-152">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="5e795-153">현재 `generate-ssh-keys` 플래그도 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-153">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="5e795-154">이 매개 변수는 Linux 배포에 사용되며, `ssh` 도구를 사용하여 원격으로 가상 머신에 액세스할 수 있도록 보안 키 쌍을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-154">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="5e795-155">두 파일은 사용자 머신의 `.ssh` 폴더와 VM에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-155">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="5e795-156">대상 폴더에 이미 `id_rsa`라는 SSH 키가 있는 경우 새 키를 생성하는 대신 이 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-156">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="5e795-157">VM 만들기가 완료되면, 가상 머신의 현재 상태와 Azure에서 할당한 공용 및 개인 IP 주소를 포함하는 JSON 응답을 가져올 것입니다.</span><span class="sxs-lookup"><span data-stu-id="5e795-157">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "westus",
  "macAddress": "00-0D-3A-58-F8-45",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "40.83.165.85",
  "resourceGroup": "2568d0d0-efe3-4d04-a08f-df7f009f822a",
  "zones": ""
}
```
