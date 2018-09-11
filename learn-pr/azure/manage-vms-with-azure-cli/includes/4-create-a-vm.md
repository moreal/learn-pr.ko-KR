<span data-ttu-id="bbaa6-101">Azure CLI에는 Azure의 가상 머신에서 작동하는 `vm` 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-101">The Azure CLI includes the `vm` command to work with virtual machines in Azure.</span></span> <span data-ttu-id="bbaa6-102">여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-102">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="bbaa6-103">가장 일반적인 하위 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-103">The most common include:</span></span>

| <span data-ttu-id="bbaa6-104">하위 명령</span><span class="sxs-lookup"><span data-stu-id="bbaa6-104">Sub-command</span></span> | <span data-ttu-id="bbaa6-105">설명</span><span class="sxs-lookup"><span data-stu-id="bbaa6-105">Description</span></span> |
|-------------|-------------|
| `create`    | <span data-ttu-id="bbaa6-106">새 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="bbaa6-106">Create a new virtual machine</span></span> |
| `deallocate` | <span data-ttu-id="bbaa6-107">가상 머신 할당 취소</span><span class="sxs-lookup"><span data-stu-id="bbaa6-107">Deallocate a virtual machine</span></span> |
| `delete` | <span data-ttu-id="bbaa6-108">가상 머신 삭제</span><span class="sxs-lookup"><span data-stu-id="bbaa6-108">Delete a virtual machine</span></span> |
| `list` | <span data-ttu-id="bbaa6-109">구독에 있는 생성된 가상 머신 나열</span><span class="sxs-lookup"><span data-stu-id="bbaa6-109">List the created virtual machines in your subscription</span></span> |
| `open-port` | <span data-ttu-id="bbaa6-110">인바운드 트래픽에 대해 특정 네트워크 포트 열기</span><span class="sxs-lookup"><span data-stu-id="bbaa6-110">Open a specific network port for inbound traffic</span></span> |
| `restart` | <span data-ttu-id="bbaa6-111">가상 머신 다시 시작</span><span class="sxs-lookup"><span data-stu-id="bbaa6-111">Restart a virtual machine</span></span> |
| `show` | <span data-ttu-id="bbaa6-112">가상 머신에 대한 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="bbaa6-112">Get the details for a virtual machine</span></span> |
| `start` | <span data-ttu-id="bbaa6-113">중지된 가상 머신 시작</span><span class="sxs-lookup"><span data-stu-id="bbaa6-113">Start a stopped virtual machine</span></span> |
| `stop` | <span data-ttu-id="bbaa6-114">실행 중인 가상 머신 중지</span><span class="sxs-lookup"><span data-stu-id="bbaa6-114">Stop a running virtual machine</span></span> |
| `update` | <span data-ttu-id="bbaa6-115">가상 머신의 속성 업데이트</span><span class="sxs-lookup"><span data-stu-id="bbaa6-115">Update a property of a virtual machine</span></span> |

> [!NOTE]
> <span data-ttu-id="bbaa6-116">전체 명령 목록은 [Azure CLI 참조 설명서](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)에서 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-116">For a complete list of commands, you can check the [Azure CLI reference documentation](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest).</span></span>

<span data-ttu-id="bbaa6-117">첫 번째 항목(`az vm create`)으로 시작하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-117">Let's start with the first one: `az vm create`.</span></span> <span data-ttu-id="bbaa6-118">이 명령은 리소스 그룹에서 가상 머신을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-118">This command is used to create a virtual machine in a resource group.</span></span> <span data-ttu-id="bbaa6-119">새 VM의 모든 측면을 구성하기 위해 전달할 수 있는 여러 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-119">There are several parameters you can pass to configure all the aspects of the new VM.</span></span> <span data-ttu-id="bbaa6-120">제공해야 하는 세 개의 매개 변수는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-120">The three parameters that must be supplied are:</span></span>

| <span data-ttu-id="bbaa6-121">매개 변수</span><span class="sxs-lookup"><span data-stu-id="bbaa6-121">Parameter</span></span> | <span data-ttu-id="bbaa6-122">설명</span><span class="sxs-lookup"><span data-stu-id="bbaa6-122">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="bbaa6-123">가상 머신을 소유할 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-123">The resource group that will own the virtual machine</span></span> |
| `name` | <span data-ttu-id="bbaa6-124">가상 머신의 이름은 리소스 그룹 내에서 고유해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-124">The name of the virtual machine - must be unique within the resource group</span></span> |
| `image` | <span data-ttu-id="bbaa6-125">VM을 만드는 데 사용할 운영 체제 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-125">The operating system image to use to create the VM</span></span> |

<span data-ttu-id="bbaa6-126">또한 VM이 만들어지는 동안 진행률을 확인하기 위해 `--verbose` 플래그를 추가하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-126">In addition, it's helpful to add the `--verbose` flag to see progress while the VM is being created.</span></span> 

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="bbaa6-127">Linux 가상 머신 만들기</span><span class="sxs-lookup"><span data-stu-id="bbaa6-127">Create a Linux virtual machine</span></span>

<span data-ttu-id="bbaa6-128">새 Linux 가상 머신을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-128">Let's create a new Linux virtual machine.</span></span> <span data-ttu-id="bbaa6-129">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-129">Execute the following command in Azure Cloud Shell:</span></span>

```azurecli
az vm create --resource-group ExerciseResources --name SampleVM --image Debian --admin-username aldis --generate-ssh-keys --verbose 
```

<span data-ttu-id="bbaa6-130">이 명령은 이름이 `SampleVM`인 새 **Debian** Linux 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-130">This command will create a new **Debian** Linux virtual machine with the name `SampleVM`.</span></span> <span data-ttu-id="bbaa6-131">VM을 만드는 동안 Azure CLI 도구가 차단되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-131">Notice that the Azure CLI tool is blocked while the VM is being created.</span></span> <span data-ttu-id="bbaa6-132">기다리지 않으려면 `--no-wait` 옵션을 사용하여 즉시 반환하도록 Azure CLI 도구에 지시할 수 있습니다(예: 스크립트에서 명령을 실행 중인 경우).</span><span class="sxs-lookup"><span data-stu-id="bbaa6-132">If you would prefer not to wait, you can use the `--no-wait` option to tell the Azure CLI tool to return immediately, for example if you're executing the command in a script.</span></span> <span data-ttu-id="bbaa6-133">스크립트의 뒷부분에서 `azure vm wait --name [vm-name]` 명령을 사용하여 VM이 만들어질 때까지 기다리세요.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-133">Later in the script, use the `azure vm wait --name [vm-name]` command to wait for the VM to finish being created.</span></span>

<span data-ttu-id="bbaa6-134">자세한 응답 내용을 살펴보면 VM에 대한 다양한 종속성을 명명하는 데 `SampleVM` 이름이 사용되는 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-134">If you look at the verbose responses, you will also see that the `SampleVM` name is used to name various dependencies for the VM.</span></span>

```
Succeeded: SampleVMNSG (Microsoft.Network/networkSecurityGroups)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMPublicIP (Microsoft.Network/publicIPAddresses)
Accepted: SampleVMVNET (Microsoft.Network/virtualNetworks)
Succeeded: SampleVMVNET (Microsoft.Network/virtualNetworks)
Accepted: vm_deploy_vzKnQDyyq48yPUO4VrSDfFIi81vHKZ9g (Microsoft.Resources/deployments)
```

<span data-ttu-id="bbaa6-135">자동 생성된 이러한 리소스 이름을 재정의하려면 `vm create`에 대한 선택적 매개 변수(예: `--vnet-name` 및 `--public-ip-address-dns-name`)를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-135">You can override these auto-generated resource names using optional parameters to `vm create`, such as `--vnet-name` and `--public-ip-address-dns-name`.</span></span>

<span data-ttu-id="bbaa6-136">여기서는 `admin-username` 플래그를 통해 관리자 계정 이름을 “aldis”로 지정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-136">Notice that we are specifying the admin account name through the `admin-username` flag to be "aldis".</span></span> <span data-ttu-id="bbaa6-137">이를 생략하면 `vm create` 명령이 _현재 사용자 이름_을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-137">If you omit this, the `vm create` command will use your _current user name_.</span></span> <span data-ttu-id="bbaa6-138">계정 이름에 대한 규칙이 OS마다 다르므로 고유한 이름을 지정하는 것이 안전합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-138">Since the rules for account names are different for each OS, it's safer to specify a specific name.</span></span> <span data-ttu-id="bbaa6-139">“root” 및 “admin”과 같은 일반적인 이름은 대부분의 이미지에서 허용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-139">Common names such as "root" and "admin" are not allowed for most images.</span></span>

<span data-ttu-id="bbaa6-140">현재 `generate-ssh-keys` 플래그도 사용하고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-140">We are also using the `generate-ssh-keys` flag.</span></span> <span data-ttu-id="bbaa6-141">이 매개 변수는 Linux 배포에 사용되며, `ssh` 도구를 사용하여 원격으로 가상 머신에 액세스할 수 있도록 보안 키 쌍을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-141">This parameter is used for Linux distributions and creates a pair of security keys so we can use the `ssh` tool to access the virtual machine remotely.</span></span> <span data-ttu-id="bbaa6-142">두 파일은 사용자 머신의 `.ssh` 폴더와 VM에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-142">The two files are placed into the `.ssh` folder on your machine and in the VM.</span></span> <span data-ttu-id="bbaa6-143">대상 폴더에 이미 `id_rsa`라는 SSH 키가 있는 경우 새 키를 생성하는 대신 이 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-143">If you already have an SSH key named `id_rsa` in the target folder, then it will be used rather than having a new key generated.</span></span>

<span data-ttu-id="bbaa6-144">VM 만들기가 완료되면, 가상 머신의 현재 상태와 Azure에서 할당한 공용 및 개인 IP 주소를 포함하는 JSON 응답을 가져올 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-144">Once it finishes creating the VM, you will get a JSON response which includes the current state of the virtual machine and its public and private IP addresses assigned by Azure:</span></span>

```json
{
  "fqdns": "",
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources/providers/Microsoft.Compute/virtualMachines/SampleVM",
  "location": "eastus",
  "macAddress": "00-0D-3A-1A-D9-74",
  "powerState": "VM running",
  "privateIpAddress": "10.0.0.4",
  "publicIpAddress": "168.61.54.62",
  "resourceGroup": "ExerciseResources",
  "zones": ""
}
```

> [!NOTE]
> <span data-ttu-id="bbaa6-145">VM이 **eastus** 위치에 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-145">Notice that the VM was created in the **eastus** location.</span></span> <span data-ttu-id="bbaa6-146">기본적으로 가상 머신은 소유 지역으로 식별되는 위치에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-146">By default, the virtual machine is created in the location identified by the owning region.</span></span> <span data-ttu-id="bbaa6-147">그러나 경우에 따라 VM을 기존 지역과 연결하려고 할 수 있지만 실제로는 전 세계의 다른 곳으로 스핀업하도록 합니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-147">However, sometimes you might want to associate the VM with an existing region, but actually have it spin up somewhere else in the world.</span></span> <span data-ttu-id="bbaa6-148">`az vm create` 명령의 부분으로 옵션 `--location` 매개 변수를 지정하여 이 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bbaa6-148">You can do this by specifying the option `--location` parameter as part of the `az vm create` command.</span></span>