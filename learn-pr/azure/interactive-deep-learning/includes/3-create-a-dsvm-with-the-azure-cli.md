<span data-ttu-id="e7d76-101">회사의 소프트웨어 개발자로서 기술을 성장시키고 사내 AI 팀의 일원이 될 수 있는 기회를 얻었습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-101">As a software developer at your company, you've the opportunity to grow your skills and become part of the in-house AI team.</span></span> <span data-ttu-id="e7d76-102">흥미로운 새 역할을 강화하는 동안 매일 해야 할 일도 계속 해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-102">While you ramp-up on this exciting new role, you still have your day job to do.</span></span> <span data-ttu-id="e7d76-103">팀 내 선임 AI 엔지니어가 이미지 분류 모델을 학습할 수 있는 PyTorch 기반 랩이 있는 유용한 Jupyter notebooks에 대해 얘기했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-103">The senior AI engineer on your team has told you about some useful Jupyter notebooks that have PyTorch-based labs to train an image classification model.</span></span> <span data-ttu-id="e7d76-104">흥미로운 도구이지만 개발 장비에 프레임워크 집합을 설치하고 싶지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-104">Exciting stuff, but you don't want to install a set of frameworks onto your dev rig.</span></span> <span data-ttu-id="e7d76-105">대신, DSVM(Data Science Virtual Machine) 이미지를 기반으로 가상 머신을 만들기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-105">Instead, you decide to create a virtual machine based on the Data Science Virtual Machine (DSVM) image.</span></span> 

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="e7d76-106">Azure CLI란?</span><span class="sxs-lookup"><span data-stu-id="e7d76-106">What is the Azure CLI</span></span>

<span data-ttu-id="e7d76-107">Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-107">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="e7d76-108">macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-108">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span> <span data-ttu-id="e7d76-109">**CLI를 사용하여 Azure 서비스 제어** 모듈에서 이 도구의 사용에 대한 전체 내용을 다룹니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-109">We have complete coverage of using this tool in the **Control Azure services with the CLI** module.</span></span>

## <a name="managing-deployments"></a><span data-ttu-id="e7d76-110">배포 관리</span><span class="sxs-lookup"><span data-stu-id="e7d76-110">Managing deployments</span></span>

<span data-ttu-id="e7d76-111">Azure CLI에는 Azure Resource Manager 배포를 관리하는 `az group deployment` 명령이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-111">The Azure CLI includes the `az group deployment` command to manage Azure Resource Manager deployments.</span></span> <span data-ttu-id="e7d76-112">특정 작업을 수행하는 여러 하위 명령을 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-112">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="e7d76-113">가장 일반적인 하위 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-113">The most common include:</span></span>

| <span data-ttu-id="e7d76-114">하위 명령</span><span class="sxs-lookup"><span data-stu-id="e7d76-114">Subcommand</span></span> | <span data-ttu-id="e7d76-115">설명</span><span class="sxs-lookup"><span data-stu-id="e7d76-115">Description</span></span> |
|-------------|-------------|
| `create` | <span data-ttu-id="e7d76-116">배포를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-116">Start a deployment.</span></span> |
| `list` | <span data-ttu-id="e7d76-117">리소스 그룹의 모든 배포를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-117">Get all the deployments for a resource group.</span></span> |
| `export` | <span data-ttu-id="e7d76-118">배포에 사용된 템플릿을 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-118">Export the template used for a deployment.</span></span> |

<span data-ttu-id="e7d76-119">사용 가능한 배포 명령의 전체 목록은 [az group deployment 명령 참조](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d76-119">For a complete list of available deployment commands, see the [az group deployment command reference](https://docs.microsoft.com/cli/azure/group/deployment?view=azure-cli-latest#az-group-deployment-create)</span></span>

<span data-ttu-id="e7d76-120">`az group deployment create`를 사용하여 가상 머신을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-120">We'll use `az group deployment create` to provision our virtual machine.</span></span>

## <a name="create-a-json-deployment-parameters-file"></a><span data-ttu-id="e7d76-121">JSON 배포 매개 변수 파일 만들기</span><span class="sxs-lookup"><span data-stu-id="e7d76-121">Create a JSON deployment parameters file</span></span>

<span data-ttu-id="e7d76-122">Azure Resource Manager 템플릿을 사용하여 VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-122">We're going to create our VM using an Azure Resource Manager template.</span></span> <span data-ttu-id="e7d76-123">템플릿은 프로비전하려는 Linux DSVM 이미지를 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-123">The template defines the Linux DSVM image we want to provision.</span></span> <span data-ttu-id="e7d76-124">사용할 VM 크기, 관리자 이름 및 암호, 머신의 호스트 이름 등의 템플릿에 일부 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-124">We need to supply some parameters to the template, such as the VM size we want to use, the admin username and password, and the host name of our machine.</span></span> 

1. <span data-ttu-id="e7d76-125">이 단원 오른쪽의 Azure Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-125">Execute the following command in Azure Cloud Shell to the right of this unit:</span></span>

    ```bash
    code parameter_file.json
    ```
    <span data-ttu-id="e7d76-126"><!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> 이 명령이 열리고 `parameter_file.json`이라는 빈 파일이 기본 제공 편집기에서 열립니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-126"><!-- TODO add a link to official doc that explains the built-in editor when it becomes available --> This command opens and empty file called `parameter_file.json` in the built-in editor.</span></span> 

1. <span data-ttu-id="e7d76-127">다음 JSON 코드 조각을 코드 편집기의 빈 파일에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-127">Paste the following JSON snippet into the empty file into the code editor.</span></span>

    ```json
    { 
      "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
      "contentVersion": "1.0.0.0",
      "parameters": {
         "adminUsername": { "value" : "<USERNAME>"},
         "adminPassword": { "value" : "<PASSWORD>"},
         "vmName": { "value" : "<HOSTNAME>"},
         "vmSize": { "value" : "Standard_DS2_v2"},
      }
    }
    ```

1. <span data-ttu-id="e7d76-128">편집기에 붙여넣은 JSON에서 다음 매개 변수를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-128">Update the following parameters in the JSON you pasted in the editor:</span></span>

    |<span data-ttu-id="e7d76-129">매개 변수</span><span class="sxs-lookup"><span data-stu-id="e7d76-129">Parameter</span></span>  |<span data-ttu-id="e7d76-130">현재 값</span><span class="sxs-lookup"><span data-stu-id="e7d76-130">Current value</span></span>  |<span data-ttu-id="e7d76-131">사용자 값</span><span class="sxs-lookup"><span data-stu-id="e7d76-131">Your value</span></span>  |
    |---------|---------|---------|
    |<span data-ttu-id="e7d76-132">adminUsername</span><span class="sxs-lookup"><span data-stu-id="e7d76-132">adminUsername</span></span>     |  `<USERNAME>`       |    <span data-ttu-id="e7d76-133">이 새 머신의 관리자 이름을 *azuser*와 같이 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-133">Choose a name for the admin user of this new machine, such as, *azuser*.</span></span>     |
    |<span data-ttu-id="e7d76-134">adminPassword</span><span class="sxs-lookup"><span data-stu-id="e7d76-134">adminPassword</span></span>     |  `<PASSWORD>`       |   <span data-ttu-id="e7d76-135">이 관리자 계정의 암호를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-135">Choose a password for this admin user account.</span></span> <span data-ttu-id="e7d76-136">암호 요구 사항에 대한 자세한 내용은 [Linux Virtual Machines에 대한 질문과 대답](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d76-136">To learn more about password requirements, see [Frequently asked question about Linux Virtual Machines](https://docs.microsoft.com/azure/virtual-machines/linux/faq?azure-portal=true)</span></span>     |
    |<span data-ttu-id="e7d76-137">vmName</span><span class="sxs-lookup"><span data-stu-id="e7d76-137">vmName</span></span>     |   `<HOSTNAME>`      |  <span data-ttu-id="e7d76-138">새 가상 머신의 이름을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-138">Choose a name for the new virtual machine.</span></span> <span data-ttu-id="e7d76-139">사용자의 이름은 문자로 시작하고 소문자 및 숫자만 포함해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-139">Your name must begin with a letter and contain only lowercase letters and numbers.</span></span> <span data-ttu-id="e7d76-140">사용자의 이니셜 및 출생 연도 등을 포함한 고유한 이름을 선택하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d76-140">Try to choose a unique name, such as one that includes your initials and your birth year.</span></span> |
    |<span data-ttu-id="e7d76-141">vmSize</span><span class="sxs-lookup"><span data-stu-id="e7d76-141">vmSize</span></span>     |  <span data-ttu-id="e7d76-142">Standard_DS2_v2</span><span class="sxs-lookup"><span data-stu-id="e7d76-142">Standard_DS2_v2</span></span>       |  <span data-ttu-id="e7d76-143">이 연습에서는 이 VM 크기가 정상적으로 작동하지만 자유롭게 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-143">This VM size will work fine for this exercise, but you are free to change it.</span></span> <span data-ttu-id="e7d76-144">사용 가능한 VM 크기 목록은 [Azure에서 Linux 가상 머신에 대한 크기](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-144">A list of available vm sizes can be found here [Sizes for Linux virtual machines in Azure](https://docs.microsoft.com/azure/virtual-machines/linux/sizes?azure-portal=true)</span></span>       |

1. <span data-ttu-id="e7d76-145">변경 내용을 `parameter_file.json`에 저장하고 텍스트 편집기를 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-145">Save your changes in `parameter_file.json` and close the text editor.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="e7d76-146">adminUsername, adminPassword 및 vmName에 대해 선택한 값을 기억해 둡니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-146">Remember the values you chose for adminUsername, adminPassword and vmName.</span></span> <span data-ttu-id="e7d76-147">이 연습에서 해당 값을 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-147">We'll use them again in this exercise.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="e7d76-148">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e7d76-148">Create a resource group</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="e7d76-149">일반적으로 선택한 지역에서 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-149">Normally you'd create a resource group in a region of your choice.</span></span> <span data-ttu-id="e7d76-150">그러나 현재 작업 중인 샌드박스 세션에서는 사용할 리소스 그룹을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-150">However, the sandbox session you are currently in supplies a resource group for you to use.</span></span> <span data-ttu-id="e7d76-151">이 세션의 리소스 그룹은 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-151">Your resource group for this session is **<rgn>[sandbox resource group name]</rgn>**.</span></span>

## <a name="deploy-the-dsvm-to-your-resource-group"></a><span data-ttu-id="e7d76-152">리소스 그룹에 DSVM 배포</span><span class="sxs-lookup"><span data-stu-id="e7d76-152">Deploy the DSVM to your resource group</span></span>

<span data-ttu-id="e7d76-153">이제 리소스 그룹이 있으며 `parameter_file.json`이라는 파일에 DSVM Resource Manager 템플릿에 대한 매개 변수를 정의했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-153">We now have a resource group and have defined parameters for the DSVM Resource Manager template in a file called `parameter_file.json`.</span></span> <span data-ttu-id="e7d76-154">다음으로 `az group deployment create`를 실행하여 가상 머신을 프로비전합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-154">We'll run the `az group deployment create` next to provision our virtual machine.</span></span>

1. <span data-ttu-id="e7d76-155">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-155">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az group deployment create \
    --resource-group  <rgn>[sandbox resource group name]</rgn> \
    --template-uri https://raw.githubusercontent.com/Azure/DataScienceVM/master/Scripts/CreateDSVM/Ubuntu/azuredeploy.json \
    --parameters parameter_file.json
    ```

    <span data-ttu-id="e7d76-156">이 명령은 리소스 그룹에 Resource Manager 템플릿 및 매개 변수를 사용하여 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-156">The command uses the Resource Manager template and our parameters to create the virtual machine in our resource group.</span></span> 

2. <span data-ttu-id="e7d76-157">가상 머신을 완료하는 데는 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-157">Deploying a virtual machine takes a few minutes to complete.</span></span> <span data-ttu-id="e7d76-158">작업이 완료될 때까지 콘솔에 ` - Running ..` 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-158">The console displays ` - Running ..` and not much else until the operation completes.</span></span> <span data-ttu-id="e7d76-159">작업이 끝나면 JSON 응답을 화면에 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-159">When the operation finishes, a JSON response is output to the screen.</span></span> <span data-ttu-id="e7d76-160">JSON의 아래쪽으로 스크롤하여 **"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-160">Scroll to the bottom of the JSON and check that the field **"provisioningState"** has the value *Succeeded*.</span></span>

    > [!TIP]
    > <span data-ttu-id="e7d76-161">다른 공용 IP에서 DNS 레코드를 이미 사용하고 있다는 오류가 표시되면 `parameter_file.json`에서 **vmName**을 고유한 다른 이름으로 변경해 보세요.</span><span class="sxs-lookup"><span data-stu-id="e7d76-161">If you get an error stating that the DNS record is already used by another public IP, try changing **vmName** in `parameter_file.json` to another name that's unique.</span></span>

3. <span data-ttu-id="e7d76-162">다음 명령을 실행하여 `<HOSTNAME>`을 VM에 대해 정의된 호스트 이름으로 바꾸고 해당 VM에 대한 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-162">Execute the following command to get information about the VM, replacing `<HOSTNAME>` with the host name you defined for your VM.</span></span>

    ```azurecli
    az vm get-instance-view \
    --name <HOSTNAME> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query instanceView.statuses[1] \
    --output table
    ```

    <span data-ttu-id="e7d76-163">이 명령은 VM의 상태를 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-163">This command displays the status of the VM.</span></span> <span data-ttu-id="e7d76-164">*VM 실행 중*이라고 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-164">It should say *VM running*.</span></span>

<span data-ttu-id="e7d76-165">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="e7d76-165">Congratulations!</span></span> <span data-ttu-id="e7d76-166">DSVM 이미지에 기반한 Linux VM을 만들고 배포했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-166">You've created and deployed a Linux VM based on the DSVM image.</span></span>

## <a name="open-the-vm-to-ssh-traffic-on-port-22"></a><span data-ttu-id="e7d76-167">포트 22에서 ssh 트래픽에 대해 VM 열기</span><span class="sxs-lookup"><span data-stu-id="e7d76-167">Open the VM to ssh traffic on port 22</span></span>

<span data-ttu-id="e7d76-168">기본적으로 VM은 어떠한 포트도 열려 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-168">By default, our VM doesn't have any ports open.</span></span> <span data-ttu-id="e7d76-169">목표는 Jupyter Notebook 서버에 원격으로 연결하여 시작하고 머신에서 다른 로컬 명령을 실행하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-169">Our goal is to connect remotely, start a Jupyter Notebook server and run other local commands on the machine.</span></span> <span data-ttu-id="e7d76-170">SSH(Secure Shell) 프로토콜을 사용하여 VM에 원격으로 연결하려면 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-170">To remote into the VM using the Secure Shell (SSH) protocol, we need to open a port.</span></span> <span data-ttu-id="e7d76-171">ssh의 기본 포트는 포트 22입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-171">Port 22 is the default port for ssh.</span></span>  

1. <span data-ttu-id="e7d76-172">Azure Cloud Shell에서 다음 명령을 실행하여 `<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-172">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` wit the name you gave your DSV virtual machine during setup.</span></span> 

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 22 \
    --priority 900
    ```

<span data-ttu-id="e7d76-173">이 명령을 완료하는 데 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-173">This command can take up to a minute to complete.</span></span> <span data-ttu-id="e7d76-174">명령이 완료되면 명령줄에 JSON 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-174">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="e7d76-175">**"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-175">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span> <span data-ttu-id="e7d76-176">ssh가 작동하는지 간단히 테스트하기 전에 먼저 포트를 하나 더 열겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-176">We'll test that ssh works shortly, but first let's open one more port.</span></span>

## <a name="open-the-vm-to-access-the-jupyter-notebook-server-remotely"></a><span data-ttu-id="e7d76-177">VM을 열어 Jupyter Notebook 서버에 원격으로 액세스</span><span class="sxs-lookup"><span data-stu-id="e7d76-177">Open the VM to access the Jupyter Notebook server remotely</span></span>

<span data-ttu-id="e7d76-178">이전에 설명한 대로 DSVM 이미지는 소프트웨어, 도구와 더불어 데이터 과학, 기계 학습 및 딥 러닝 프로젝트를 지원하기 위한 샘플이 미리 설치된 상태로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-178">As mentioned previously, the DSVM image comes pre-installed with software, tools, and samples to help you with your data science, machine learning, and deep learning projects.</span></span> <span data-ttu-id="e7d76-179">Jupyter는 샘플 Notebook과 함께 이미지에 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-179">Jupyter is installed in the image, along with sample notebooks.</span></span> <span data-ttu-id="e7d76-180">VM에서 Jupyter Notebook 서버를 시작한 다음, 로컬 머신에서 Notebook 서버에 원격으로 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-180">We want to start a Jupyter notebook server on the VM and then remotely connect to the notebook server from our local machine.</span></span> <span data-ttu-id="e7d76-181">기본적으로 Notebook 서버는 포트 8888에서 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-181">By default, the notebook server runs on port 8888.</span></span> <span data-ttu-id="e7d76-182">서버에 원격으로 액세스하려면 VM에서 해당 포트를 열어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-182">To access the server remotely, we need to open that port on our VM.</span></span> 

1. <span data-ttu-id="e7d76-183">Azure Cloud Shell에서 다음 명령을 실행하여 `<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-183">Execute the following command in Azure Cloud Shell, replacing `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm open-port \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --port 8888 \
    --priority 901
    ```

<span data-ttu-id="e7d76-184">다시 말하지만, 이 명령을 완료하는 데 1분 정도 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-184">Again, this command can take up to a minute to complete.</span></span> <span data-ttu-id="e7d76-185">명령이 완료되면 명령줄에 JSON 응답이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-185">When the command finishes, it returns a JSON response to the command line.</span></span> <span data-ttu-id="e7d76-186">**"provisioningState"** 필드의 값이 *Succeeded*인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-186">Check that the field **"provisioningState"** has the value *Succeeded*.</span></span>  

## <a name="connect-to-the-vm-with-secure-shell-ssh"></a><span data-ttu-id="e7d76-187">ssh(Secure Shell)로 VM에 연결</span><span class="sxs-lookup"><span data-stu-id="e7d76-187">Connect to the VM with Secure Shell (ssh)</span></span>

1. <span data-ttu-id="e7d76-188">Azure Cloud Shell에서 다음 명령을 실행하여 VM의 공용 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-188">Execute the following command in Azure Cloud Shell to find the public IP address of the VM.</span></span> <span data-ttu-id="e7d76-189">`<HOSTNAME>`을 설정 중에 DSVM 가상 머신에 제공한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-189">Replace `<HOSTNAME>` with the name you gave your DSVM virtual machine during setup.</span></span>

    ```azurecli
    az vm list-ip-addresses \
    -g <rgn>[sandbox resource group name]</rgn> \
    -n <HOSTNAME> \
    --output table
    ```

1. <span data-ttu-id="e7d76-190">Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-190">Execute the following command in the Cloud Shell to sign into the VM.</span></span> <span data-ttu-id="e7d76-191">`<USERNAME>`을 이 연습 시작 시 선택한 사용자 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-191">Replace `<USERNAME>` with the username you chose at the start of this exercise.</span></span> <span data-ttu-id="e7d76-192">`<IP>`를 이전 단계의 **PublicIPAddresses** 열의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-192">Replace `<IP>`  with the value from the **PublicIPAddresses** column of the previous step.</span></span>

    <span data-ttu-id="e7d76-193">예를 들어, 선택한 사용자 이름이 *azuser*이고 PublicIPAddresses의 값이 33.165.103.23인 경우 이 명령은 다음과 같이 읽습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-193">For example, if the username you chose was *azuser* and the PublicIPAddresses had a value of 33.165.103.23, then this command would read:</span></span>
    
    `ssh azuser@33.165.103.23`
    
    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 

1. <span data-ttu-id="e7d76-194">메시지가 표시되면 이 연습 시작 시 선택한 관리자 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-194">When prompted, enter the password for the admin user you chose at the start of this exercise.</span></span> <span data-ttu-id="e7d76-195">성공적으로 로그인한 경우 프롬프트가 `username@hostname` 형식으로 변경됩니다(예: `azuser@js1982`).</span><span class="sxs-lookup"><span data-stu-id="e7d76-195">When you've signed in successfully, your prompt should change to the format `username@hostname`, for example, `azuser@js1982`.</span></span>

<span data-ttu-id="e7d76-196">다음 단계는 VM에서 Jupyter Notebook 서버를 시작하고 원격으로 Notebook을 여는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-196">The next step is to start the Jupyter notebook server on our VM and open a notebook remotely.</span></span>

## <a name="start-the-jupyter-notebook-server-on-the-vm"></a><span data-ttu-id="e7d76-197">VM에서 Jupyter Notebook 서버 시작</span><span class="sxs-lookup"><span data-stu-id="e7d76-197">Start the Jupyter notebook server on the VM</span></span>

<span data-ttu-id="e7d76-198">VM의 `~/notebooks` 폴더에 일련의 Notebook이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-198">There's a set of notebooks in the `~/notebooks` folder of your VM.</span></span> <span data-ttu-id="e7d76-199">SSH 세션을 통해 여전히 로그인되어 있다고 가정하고 Notebook 서버를 시작한 후 이러한 Notebook 중 하나를 열고 모두 작동하는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-199">Assuming you are still logged in through an SSH session,  start the notebook server and open one of these notebooks to make sure everything is working.</span></span>


1. <span data-ttu-id="e7d76-200">VM의 명령 프롬프트에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-200">Run the following command at the command prompt of your VM:</span></span>

    ```bash
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root
    ```

> [!CAUTION]
> <span data-ttu-id="e7d76-201">이 연습에서 Notebook 서버에 대한 액세스는 `http://`를 통해 수행됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-201">Access to the notebook server in this exercise happens over `http://`.</span></span> <span data-ttu-id="e7d76-202">공개된 장소에서 Notebook 서버를 실행하려는 경우는 해당 서버를 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-202">If you want to run a notebook server in public, you should secure it.</span></span> <span data-ttu-id="e7d76-203">Notebook 서버를 보호하는 방법에 대한 자세한 내용은 공식 온라인 Jupyter 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e7d76-203">For more information about securing a notebook server, see the official Jupyter documentation online.</span></span> 

<span data-ttu-id="e7d76-204">이전 명령에서는 `jupyter notebook` 명령을 사용하여 Jupyter Notebook 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-204">In the preceding command, we start the Jupyter Notebook server with the `jupyter notebook` command.</span></span> <span data-ttu-id="e7d76-205">세 개의 중요한 명령줄 인수가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-205">We supply three important command-line arguments.</span></span> <span data-ttu-id="e7d76-206">콘솔을 통해 원격으로 이 머신에 로그인했음을 기억하십시오.</span><span class="sxs-lookup"><span data-stu-id="e7d76-206">Remember, we're logged into this machine remotely through a console.</span></span> <span data-ttu-id="e7d76-207">Notebook은 브라우저에서 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-207">Notebooks are served in a browser.</span></span> 

 - <span data-ttu-id="e7d76-208">`--ip=0.0.0.0` 기본적으로 Notebook 서버는 127.0.0.1:8888에서 로컬로 실행되고 localhost에서만 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-208">`--ip=0.0.0.0` By default, a notebook server runs locally at 127.0.0.1:8888 and is accessible only from localhost.</span></span> <span data-ttu-id="e7d76-209">http://127.0.0.1:8888을 사용하여 로컬로 브라우저에서 Notebook 서버에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-209">You can access the notebook server from the browser locally using http://127.0.0.1:8888.</span></span> <span data-ttu-id="e7d76-210">IP 주소를 0.0.0.0으로 설정하면 서버가 모든 IP 주소에서 트래픽을 수신합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-210">Setting the IP Address to 0.0.0.0 tells the server to listen for traffic on all IPs.</span></span> <span data-ttu-id="e7d76-211">Notebook 서버가 0.0.0.0에서 수신 대기를 하는 경우 호스트 머신의 IP 주소를 통해 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-211">If the notebook server listens on 0.0.0.0, it will be reachable through the IP address of the host machine.</span></span>  
 - <span data-ttu-id="e7d76-212">`--no-browser`  다른 컴퓨터에서 인터넷을 통해 Notebook에 연결하려고 하는 것이므로 Notebook 서버가 브라우저를 열지 않도록 구성합니다(브라우저를 여는 것이 기본 동작입니다).</span><span class="sxs-lookup"><span data-stu-id="e7d76-212">`--no-browser`  Because we want to connect to the notebook from another computer over the internet, we configure the notebook server to not open the browser, which is the default behavior.</span></span> 
 - <span data-ttu-id="e7d76-213">`--allow-root`  이 연습은 VM에서 관리자 계정만 사용하므로 Notebook이 루트로 실행되도록 하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-213">`--allow-root`  In this exercise, we only have an admin account on the VM, so  we want to be able to run notebooks as root.</span></span>

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="e7d76-214">원격 브라우저에서 Jupyter Notebook 서버에 연결</span><span class="sxs-lookup"><span data-stu-id="e7d76-214">Connect to the Jupyter Notebook server from a remote browser</span></span>

<span data-ttu-id="e7d76-215">위의 명령을 VM에서 실행하면 Notebook 서버가 시작되고 브라우저에서 사용할 수 있는 URL이 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-215">When the above command runs on the VM, the notebook server starts and the console displays a URL for you to use in a browser.</span></span> 

![실행 중인 Notebook 서버가 호스트 머신에서 서버에 액세스하기 위해 사용하는 URL과 함께 콘솔에 표시하는 메시지의 스크린샷](../media/notebook-url.png)

1. <span data-ttu-id="e7d76-217">Notebook 서버가 표시하는 URL을 즐겨 사용하는 브라우저의 주소 표시줄에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-217">Copy the URL the notebook server displays into the address bar of your favorite browser.</span></span> <span data-ttu-id="e7d76-218">기본 브라우저에서 열려는 URL을 클릭할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-218">You can also click on the URL to open in your default browser.</span></span> 

    <span data-ttu-id="e7d76-219">제공된 URL이 호스트 머신에서 Notebook 서버로의 연결을 설정하기 때문에 "사이트에 연결할 수 없습니다"라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-219">You will receive a "Site can't be reached" message because the URL you were given is the connection to the notebook server from the host machine.</span></span>

1. <span data-ttu-id="e7d76-220">서버에 원격으로 액세스하려면 URL의 호스트 이름을 이전에 저장된 VM의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-220">To access the server remotely,  replace the hostname in the URL with the IP address of the VM you saved earlier.</span></span> 

    <span data-ttu-id="e7d76-221">샘플 Notebook 서버 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-221">Here's a sample notebook server URL.</span></span>

    <span data-ttu-id="e7d76-222">"http://**ab-dsvm-4**:8888/?token={some token}"</span><span class="sxs-lookup"><span data-stu-id="e7d76-222">"http://**ab-dsvm-4**:8888/?token={some token}"</span></span>

    <span data-ttu-id="e7d76-223">이 예에서는 **ab-dsvm-4**를 머신의 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-223">In this case, we would replace **ab-dsvm-4** with IP address of the machine.</span></span> <span data-ttu-id="e7d76-224">IP 주소가 `52.175.199.43`인 경우 URL은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-224">If our IP address is `52.175.199.43`, then the URL becomes:</span></span>

    <span data-ttu-id="e7d76-225">"http://**52.175.199.43**:8888/?token={some token}"</span><span class="sxs-lookup"><span data-stu-id="e7d76-225">"http://**52.175.199.43**:8888/?token={some token}"</span></span>

    <span data-ttu-id="e7d76-226">포트 주소인 `:8888`이 URL에 포함되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-226">Make sure `:8888`, the port address, is kept in the URL.</span></span>

    > [!TIP]
    > <span data-ttu-id="e7d76-227">IP 주소를 사용하지 않으려면 `<HOST NAME>.<REGION>.cloudapp.azure.com` 형식으로 서버의 정규화된 이름을 사용할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-227">If you don't want to use the IP address, you can also use the fully qualified name of your server which is in the form `<HOST NAME>.<REGION>.cloudapp.azure.com`</span></span>

    <span data-ttu-id="e7d76-228">다음 스크린샷에서는 브라우저에 Jupyter 대시보드가 표시되는 모양을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-228">The following  screenshot shows what the Jupyter dashboard looks like in your browser.</span></span>

    ![<span data-ttu-id="e7d76-229">Jupyter Notebook 대시보드를 보여주는 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-229">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/jupyter-in-browser.png)

1. <span data-ttu-id="e7d76-230">**notebooks/IntroToJupyterPython.ipynb**로 이동하여 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-230">Navigate to **notebooks/IntroToJupyterPython.ipynb** and select it.</span></span> <span data-ttu-id="e7d76-231">이 Notebook이 예상 대로 작동하는지 확인해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-231">Try out this notebook to verify everythin  works as expected.</span></span>

    <span data-ttu-id="e7d76-232">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="e7d76-232">Congratulations!</span></span> <span data-ttu-id="e7d76-233">이제 DSVM 기반 가상 머신이 실행되고 있으며 Jupyter에서 원격으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-233">You now have a running DSVM-based virtual machine running and can work remotely with Jupyter.</span></span> <span data-ttu-id="e7d76-234">이 연습에서는 VM에 설치된 소프트웨어를 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-234">In this exercise, we're running the software that was installed on the VM.</span></span> <span data-ttu-id="e7d76-235">다음 연습에서는 안정적으로 실험할 수 있도록 VM의 컨테이너에서 소프트웨어를 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-235">In the next exercise, we'll isolate the software in a container on the VM so we can experiment with confidence.</span></span>

4. <span data-ttu-id="e7d76-236">Notebook을 사용한 작업이 완료된 후에는 Cloud Shell에서 `Control-C`를 사용하여 Jupyter 서버를 중지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e7d76-236">When you have finished with the notebook, you can stop the Jupyter server with `Control-C` in the Cloud Shell.</span></span>
