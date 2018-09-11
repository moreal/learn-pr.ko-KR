<span data-ttu-id="bc416-101">Azure Event Hubs는 대량의 데이터를 처리할 수 있는 기능을 빅 데이터 응용 프로그램에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-101">Azure Event Hubs provides big data applications the capability to process large volume of data.</span></span> <span data-ttu-id="bc416-102">특별히 수요가 높은 기간에, 그리고 필요할 때 규모를 확장하는 기능도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-102">It also has the ability to scale out during exceptionally high- demand periods as and when required.</span></span> <span data-ttu-id="bc416-103">Azure Event Hubs는 데이터 처리를 관리하기 위해 보내는 메시지와 받는 메시지를 분리합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-103">Azure Event Hubs decouple the sending and receiving messages to manage the data processing.</span></span> <span data-ttu-id="bc416-104">이렇게 하면 계획되지 않은 중단으로 인한 엄청난 소비자 응용 프로그램 및 데이터 손실의 위험을 방지할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-104">This helps eliminate the risk of overwhelming consumer application and data loss due to any unplanned interruptions.</span></span>

<span data-ttu-id="bc416-105">이 모듈에서는 Azure Event Hubs를 이벤트 처리 솔루션의 일부로 배포하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-105">In this module, you've seen how to deploy Azure Event Hubs as part of an event processing solution.</span></span> <span data-ttu-id="bc416-106">다음 방법에 대해 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-106">You learned how to:</span></span>

- <span data-ttu-id="bc416-107">Azure CLI 명령을 사용하여 Event Hubs 네임스페이스와 해당 네임스페이스의 이벤트 허브를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-107">Use the Azure CLI commands to create an Event Hubs namespace and an event hub in that namespace.</span></span> 
- <span data-ttu-id="bc416-108">이벤트 허브를 통해 메시지를 보내고 받도록 발신자 및 수신자 응용 프로그램을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-108">Configure sender and receiver applications to send and receive messages through the event hub.</span></span>
- <span data-ttu-id="bc416-109">Azure Portal을 사용하여 이벤트 허브 상태 및 성능을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-109">Use the Azure portal to view your event hub status and performance.</span></span>

## <a name="clean-up"></a><span data-ttu-id="bc416-110">정리</span><span class="sxs-lookup"><span data-stu-id="bc416-110">Clean up</span></span> 
<!---TODO: Do we need to include cleanup for the free education tier?--->

<span data-ttu-id="bc416-111">이벤트 허브 테스트에 사용한 리소스에서 구독에 대한 비용이 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-111">The resources you've used for your event hub testing will incur costs against your subscription.</span></span> <span data-ttu-id="bc416-112">이벤트 허브 사용을 완료했으면 불필요한 요금 청구를 방지하기 위해 이러한 리소스를 제거해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-112">When you've have finished with the event hub, remember to remove these resources in order to avoid unnecessary charges.</span></span>

<span data-ttu-id="bc416-113">동일한 리소스 그룹에 허브, 네임스페이스 및 저장소를 만들기 때문에 Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하여 해당 내용을 모두 제거하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-113">Because you create the hub, namespace, and storage in the same resource group, the easiest way to cleanup your Azure subscription is to remove the resource group, which will remove all its contents.</span></span> 

<span data-ttu-id="bc416-114">다음 명령을 실행하여 리소스 그룹, 네임스페이스, 저장소 계정 및 모든 관련된 리소스를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-114">Run the following command to remove the resource group, namespace, storage account, and all related resources.</span></span> <span data-ttu-id="bc416-115">만든 리소스 그룹의 이름으로 `myResourceGroup`을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-115">Replace `myResourceGroup` with the name of the resource group you created:</span></span>

```azurecli
az group delete --resource-group myResourceGroup
```

<span data-ttu-id="bc416-116">삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-116">When you are asked to confirm the delete, answer **Yes**.</span></span>

<span data-ttu-id="bc416-117">리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bc416-117">The command may take several minutes to complete as resources are deleted.</span></span>
