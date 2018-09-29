<span data-ttu-id="f0656-101">여기에서는 Azure에서 컨테이너를 만들어서 FQDN(정규화된 도메인 이름)으로 인터넷에 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-101">Here, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="why-use-azure-container-instances"></a><span data-ttu-id="f0656-102">Azure Container Instances를 사용하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="f0656-102">Why use Azure Container Instances?</span></span>

<span data-ttu-id="f0656-103">Azure Container Instances는 간단한 응용 프로그램, 작업 자동화 및 빌드 작업 등 격리된 컨테이너에서 작동할 수 있는 시나리오에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-103">Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="f0656-104">Azure Container Instances는 다음과 같은 혜택을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-104">Azure Container Instances offers the following benefits:</span></span>

- <span data-ttu-id="f0656-105">**빠른 시작**: 몇 초 내에 컨테이너를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-105">**Fast startup**: Launch containers in seconds.</span></span>
- <span data-ttu-id="f0656-106">**초당 청구**: 컨테이너가 실행되는 동안에만 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-106">**Per second billing**: Incur costs only while the container is running.</span></span>
- <span data-ttu-id="f0656-107">**하이퍼바이저 수준 보안**: 응용 프로그램을 VM에서처럼 완전히 격리합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-107">**Hypervisor-level security**: Isolate your application as completely as it would be in a VM.</span></span>
- <span data-ttu-id="f0656-108">**사용자 지정 크기**: CPU 코어 및 메모리에 대한 정확한 값을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-108">**Custom sizes**: Specify exact values for CPU cores and memory.</span></span>
- <span data-ttu-id="f0656-109">**영구 저장소**: 컨테이너에 직접 Azure 파일 공유를 탑재하여 상태를 검색하고 유지합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-109">**Persistent storage**: Mount Azure Files shares directly to a container to retrieve and persist state.</span></span>
- <span data-ttu-id="f0656-110">**Linux 및 Windows**: 동일한 API를 사용하여 Windows 및 Linux 컨테이너를 모두 예약합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-110">**Linux and Windows**: Schedule both Windows and Linux containers using the same API.</span></span>

<span data-ttu-id="f0656-111">여러 컨테이너 간 서비스 검색, 자동 크기 조정 및 조정된 응용 프로그램 업그레이드를 포함하여 전체 컨테이너 오케스트레이션이 필요한 시나리오에는 AKS(Azure Kubernetes Service)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-111">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend Azure Kubernetes Service (AKS).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="f0656-112">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="f0656-112">Create a container</span></span>

<span data-ttu-id="f0656-113">**az container create** 명령에 이름, Docker 이미지 및 Azure 리소스 그룹을 입력하여 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-113">You create a container by providing a name, a Docker image, and an Azure resource group to the **az container create** command.</span></span> <span data-ttu-id="f0656-114">필요에 따라 DNS 이름 레이블을 지정하여 컨테이너를 인터넷에 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-114">You can optionally expose the container to the Internet by specifying a DNS name label.</span></span> <span data-ttu-id="f0656-115">이 예제에서는 작은 웹앱을 호스트하는 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-115">In this example, you deploy a container that hosts a small web app.</span></span> <span data-ttu-id="f0656-116">이미지를 배치할 위치를 선택할 수도 있습니다. 아래에서는 "미국 동부"를 기본값으로 지정했지만 다음 목록에서 사용자에게 가까운 위치로 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-116">You can also select the location to place the image - we're defaulting to "East US" below, but you can change it to a location close to you from the following list.</span></span>

<span data-ttu-id="f0656-117"><!-- TODO: fix region list so it's not hardcoded here --> 무료 샌드박스를 사용하면 Azure 글로벌 지역의 일부에서 리소스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-117"><!-- TODO: fix region list so it's not hardcoded here --> The free sandbox allows you to create resources in a subset of Azure's global regions.</span></span> <span data-ttu-id="f0656-118">리소스를 만들 때 다음 목록에서 지역을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-118">Select a region from the following list when creating any resources:</span></span>

:::row:::
    :::column:::
        <span data-ttu-id="f0656-119">- westus2 - centralus - eastus - westeurope - southeastasia</span><span class="sxs-lookup"><span data-stu-id="f0656-119">- westus2 - centralus - eastus - westeurope - southeastasia</span></span> :::column-end:::
:::row-end:::

<span data-ttu-id="f0656-120">Cloud Shell에서 다음 명령을 실행하여 컨테이너 인스턴스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-120">Execute the following command in the Cloud Shell to start a container instance.</span></span> <span data-ttu-id="f0656-121">`--dns-name-label` 값은 인스턴스를 만드는 Azure 지역 내에서 고유해야 합니다. 따라서 `[dns-name]`을 고유한 내용으로 바꿔야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-121">The `--dns-name-label` value must be unique within the Azure region you create the instance, so you will need to replace `[dns-name]` with something unique.</span></span>

```azurecli
az container create \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label [dns-name] \
    --location eastus
```

<span data-ttu-id="f0656-122">몇 초 안에 요청에 대한 응답이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-122">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="f0656-123">처음에는 컨테이너가 **만드는 중** 상태가 되지만 몇 초 이내 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-123">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="f0656-124">`az container show` 명령을 사용하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-124">You can check the status using the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

<span data-ttu-id="f0656-125">명령을 실행하면 컨테이너의 FQDN(정규화된 도메인 이름) 및 프로비전 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-125">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

<span data-ttu-id="f0656-126">컨테이너가 **성공** 상태로 전환되면 브라우저에서 해당 FQDN으로 이동하여 성공을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-126">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser to verify success.</span></span>

<span data-ttu-id="f0656-127">여기에서는 웹 서버 및 응용 프로그램을 실행하는 Azure 컨테이너 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-127">Here, you created an Azure container instance to run a web server and application.</span></span> <span data-ttu-id="f0656-128">또한 컨테이너 인스턴스의 FQDN을 사용하여 이 응용 프로그램에 액세스했습니다.</span><span class="sxs-lookup"><span data-stu-id="f0656-128">You also accessed this application using the FQDN of the container instance.</span></span>