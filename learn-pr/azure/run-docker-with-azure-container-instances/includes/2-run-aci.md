<span data-ttu-id="d3374-101">여기에서는 Azure에서 컨테이너를 만들어야 하 고 정규화 된 도메인 이름 (FQDN)을 사용 하 여 인터넷에 노출 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-101">Here, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span>

## <a name="why-use-azure-container-instances"></a><span data-ttu-id="d3374-102">Azure Container Instances를 사용 하는 이유는?</span><span class="sxs-lookup"><span data-stu-id="d3374-102">Why use Azure Container Instances?</span></span>

<span data-ttu-id="d3374-103">Azure Container Instances는 간단한 응용 프로그램, 작업 자동화를 포함 하 여 격리 된 컨테이너에서 작동 하 고 작업을 빌드할 수 있는 시나리오에 유용 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-103">Azure Container Instances is useful for scenarios that can operate in isolated containers, including simple applications, task automation, and build jobs.</span></span> <span data-ttu-id="d3374-104">Azure Container Instances는 다음과 같은 이점을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-104">Azure Container Instances offers the following benefits:</span></span>

- <span data-ttu-id="d3374-105">**빠른 시작**: 시간 (초)에서 컨테이너를 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-105">**Fast startup**: Launch containers in seconds.</span></span>
- <span data-ttu-id="d3374-106">**초당 청구**: 컨테이너가 실행 되는 동안에 비용이 발생 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-106">**Per second billing**: Incur costs only while the container is running.</span></span>
- <span data-ttu-id="d3374-107">**하이퍼바이저 수준 보안**: 응용 프로그램을 VM의 것과 완전히 격리 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-107">**Hypervisor-level security**: Isolate your application as completely as it would be in a VM.</span></span>
- <span data-ttu-id="d3374-108">**사용자 지정 크기**: CPU 코어 및 메모리에 대 한 정확한 값을 지정 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-108">**Custom sizes**: Specify exact values for CPU cores and memory.</span></span>
- <span data-ttu-id="d3374-109">**영구 저장소**: 검색 및 상태를 유지 하는 컨테이너에 직접 탑재 Azure 파일 공유 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-109">**Persistent storage**: Mount Azure Files shares directly to a container to retrieve and persist state.</span></span>
- <span data-ttu-id="d3374-110">**Linux 및 Windows**: 동일한 API를 사용 하 여 Windows 및 Linux 컨테이너를 예약 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-110">**Linux and Windows**: Schedule both Windows and Linux containers using the same API.</span></span>

<span data-ttu-id="d3374-111">여러 컨테이너 간 서비스 검색, 자동 크기 조정 및 조정된 응용 프로그램 업그레이드를 포함하여 전체 컨테이너 오케스트레이션이 필요한 시나리오에는 AKS(Azure Kubernetes Service)를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-111">For scenarios where you need full container orchestration, including service discovery across multiple containers, automatic scaling, and coordinated application upgrades, we recommend Azure Kubernetes Service (AKS).</span></span>

## <a name="create-a-container"></a><span data-ttu-id="d3374-112">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="d3374-112">Create a container</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="d3374-113">이름, Docker 이미지를 Azure 리소스 그룹을 제공 하 여 컨테이너를 만들어야 합니다 **az 컨테이너 만들기** 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-113">You create a container by providing a name, a Docker image, and an Azure resource group to the **az container create** command.</span></span> <span data-ttu-id="d3374-114">필요에 따라 DNS 이름 레이블을 지정하여 컨테이너를 인터넷에 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-114">You can optionally expose the container to the internet by specifying a DNS name label.</span></span> <span data-ttu-id="d3374-115">이 예제에서는 작은 웹앱을 호스트하는 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-115">In this example, you deploy a container that hosts a small web app.</span></span>

<span data-ttu-id="d3374-116">컨테이너 인스턴스를 시작 하려면 Cloud Shell에서 다음 명령을 실행 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-116">Execute the following command in the Cloud Shell to start a container instance.</span></span> <span data-ttu-id="d3374-117">*--dns-name-label* 값은 인스턴스를 만드는 Azure 지역 내에서 고유해야 하므로 고유성을 유지하기 위해 이 값을 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-117">The *--dns-name-label* value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness:</span></span>

```azurecli
az container create \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label aci-demo
```

<span data-ttu-id="d3374-118">몇 초 안에 요청에 대한 응답이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-118">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="d3374-119">처음에는 컨테이너가 **만드는 중** 상태가 되지만 몇 초 이내 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-119">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="d3374-120">`az container show` 명령을 사용하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-120">You can check the status using the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

<span data-ttu-id="d3374-121">명령을 실행하면 컨테이너의 FQDN(정규화된 도메인 이름) 및 프로비저닝 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-121">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

<span data-ttu-id="d3374-122">컨테이너 전환 되 면 합니다 **Succeeded** 상태, 성공 여부를 확인 하려면 브라우저에서 해당 FQDN으로 이동 합니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-122">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser to verify success.</span></span>

<span data-ttu-id="d3374-123">여기에서 웹 서버 및 응용 프로그램을 실행 하려면 Azure container instance를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-123">Here, you created an Azure container instance to run a web server and application.</span></span> <span data-ttu-id="d3374-124">또한 컨테이너 인스턴스의 FQDN을 사용하여 이 응용 프로그램에 액세스했습니다.</span><span class="sxs-lookup"><span data-stu-id="d3374-124">You also accessed this application using the FQDN of the container instance.</span></span>