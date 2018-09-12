<span data-ttu-id="8ee2e-101">Azure Container Instances를 사용하면 가상 머신을 프로비전하거나 상위 수준 서비스를 도입하지 않고도 Azure에서 Docker 컨테이너를 쉽게 만들고 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-101">Azure Container Instances makes it easy to create and manage Docker containers in Azure, without having to provision virtual machines or adopt a higher-level service.</span></span> <span data-ttu-id="8ee2e-102">이 단원에서는 Azure에서 컨테이너를 만들어서 FQDN(정규화된 도메인 이름)으로 인터넷에 노출합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-102">In this unit, you create a container in Azure and expose it to the internet with a fully qualified domain name (FQDN).</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="8ee2e-103">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="8ee2e-103">Create a resource group</span></span>

<span data-ttu-id="8ee2e-104">모든 Azure 리소스와 마찬가지로 Azure Container Instances는 Azure 리소스를 배포하고 관리하는 논리적 컬렉션인 리소스 그룹에 배치되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-104">Azure Container Instances, like all Azure resources, must be placed in a resource group, a logical collection into which Azure resources are deployed and managed.</span></span>

<span data-ttu-id="8ee2e-105">`az group create` 명령을 사용하여 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-105">Create a resource group with the `az group create` command.</span></span>

<span data-ttu-id="8ee2e-106">다음 예제에서는 *eastus* 위치에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-106">The following example creates a resource group named *myResourceGroup* in the *eastus* location:</span></span>

```azurecli
az group create --name myResourceGroup --location eastus
```

## <a name="create-a-container"></a><span data-ttu-id="8ee2e-107">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="8ee2e-107">Create a container</span></span>

<span data-ttu-id="8ee2e-108">**az container create** 명령에 이름, Docker 이미지 및 Azure 리소스 그룹을 제공하여 컨테이너를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-108">You can create a container by providing a name, a Docker image, and an Azure resource group to the **az container create** command.</span></span> <span data-ttu-id="8ee2e-109">필요에 따라 DNS 이름 레이블을 지정하여 컨테이너를 인터넷에 노출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-109">You can optionally expose the container to the internet by specifying a DNS name label.</span></span> <span data-ttu-id="8ee2e-110">이 예제에서는 작은 웹앱을 호스트하는 컨테이너를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-110">In this example, you deploy a container that hosts a small web app.</span></span>

<span data-ttu-id="8ee2e-111">컨테이너 인스턴스를 시작하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-111">Execute the following command to start a container instance.</span></span> <span data-ttu-id="8ee2e-112">*--dns-name-label* 값은 인스턴스를 만드는 Azure 지역 내에서 고유해야 하므로 고유성을 유지하기 위해 이 값을 수정해야 할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-112">The *--dns-name-label* value must be unique within the Azure region you create the instance, so you might need to modify this value to ensure uniqueness:</span></span>

```azurecli
az container create \
    --resource-group myResourceGroup \
    --name mycontainer \
    --image microsoft/aci-helloworld \
    --ports 80 \
    --dns-name-label aci-demo
```

<span data-ttu-id="8ee2e-113">몇 초 안에 요청에 대한 응답이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-113">Within a few seconds, you should get a response to your request.</span></span> <span data-ttu-id="8ee2e-114">처음에는 컨테이너가 **만드는 중** 상태가 되지만 몇 초 이내 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-114">Initially, the container is in the **Creating** state, but it should start within a few seconds.</span></span> <span data-ttu-id="8ee2e-115">`az container show` 명령을 사용하여 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-115">You can check the status using the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer \
    --query "{FQDN:ipAddress.fqdn,ProvisioningState:provisioningState}" \
    --out table
```

<span data-ttu-id="8ee2e-116">명령을 실행하면 컨테이너의 FQDN(정규화된 도메인 이름) 및 프로비저닝 상태가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-116">When you run the command, the container's fully qualified domain name (FQDN) and its provisioning state are displayed:</span></span>

```output
FQDN                                    ProvisioningState
--------------------------------------  -------------------
aci-demo.eastus.azurecontainer.io       Succeeded
```

<span data-ttu-id="8ee2e-117">컨테이너가 **성공** 상태로 전환되면 브라우저에서 해당 FQDN으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-117">Once the container moves to the **Succeeded** state, navigate to its FQDN in your browser:</span></span>

![Azure 컨테이너 인스턴스에서 실행되는 응용 프로그램을 보여주는 브라우저 스크린샷](../media-draft/aci-app-browser.png)

## <a name="summary"></a><span data-ttu-id="8ee2e-119">요약</span><span class="sxs-lookup"><span data-stu-id="8ee2e-119">Summary</span></span>

<span data-ttu-id="8ee2e-120">이 단원에서는 웹 서버 및 응용 프로그램을 실행하는 Azure 컨테이너 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-120">In this unit, you created an Azure container instance that is running a web server and application.</span></span> <span data-ttu-id="8ee2e-121">또한 컨테이너 인스턴스의 FQDN을 사용하여 이 응용 프로그램에 액세스했습니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-121">You also accessed this application using the FQDN of the container instance.</span></span>

<span data-ttu-id="8ee2e-122">다음 단원에서는 컨테이너 인스턴스 다시 시작 정책을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="8ee2e-122">In the next unit, you will configure container instance restart policies.</span></span>