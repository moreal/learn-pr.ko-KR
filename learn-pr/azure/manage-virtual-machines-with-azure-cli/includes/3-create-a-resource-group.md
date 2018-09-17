<span data-ttu-id="fa213-101">목표는 새로운 Azure 가상 머신을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="fa213-102">리소스 위치, 사용할 OS 및 VM에 필요한 하드웨어 구성을 식별하기 위해 몇 가지 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="fa213-103">**리소스 그룹**부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="fa213-104">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="fa213-104">Create a resource group</span></span>

<span data-ttu-id="fa213-105">Azure는 _리소스 그룹_을 사용하여 가상 머신 및 데이터베이스와 같은 관련 리소스를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="fa213-106">또한 리소스 그룹은 리소스가 배치되는 데이터 센터를 결정하는 특정 위치(“지역”이라고 함)를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

> [!NOTE]
> <span data-ttu-id="fa213-107">Azure 샌드박스는 <rgn>[샌드박스 리소스 그룹 이름]</rgn>이라는 미리 생성된 리소스 그룹을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-107">The Azure sandbox provides a pre-created resource group named <rgn>[Sandbox resource group name]</rgn>.</span></span> <span data-ttu-id="fa213-108">이러한 단계를 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-108">You do not need to execute these steps.</span></span> <span data-ttu-id="fa213-109">그러나 실제 프로젝트를 위해 _고유_ 리소스를 만들 때 수행해야 하는 명령이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-109">However, when you are creating your _own_ resources for real projects, these will be the commands you will need to perform.</span></span> <span data-ttu-id="fa213-110">Azure 샌드박스에서는 리소스 그룹을 직접 만들 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-110">The Azure sandbox does not allow you to create resource groups directly.</span></span>

<span data-ttu-id="fa213-111">예를 들어 Azure Cloud Shell에 다음 Azure CLI 명령을 입력하여 **미국 동부** 지역에 리소스 구분을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-111">As an example, you could type the following Azure CLI command in Azure Cloud Shell to create a resource group in the **East US** region.</span></span> <span data-ttu-id="fa213-112">**[리소스 그룹]** 을 고유한 활성 구독 내에서 유효한 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-112">You would replace **[resource-group]** with a valid name that is unique within the active subscription.</span></span>

```azurecli
az group create --name [resource-group] --location eastus
```

<span data-ttu-id="fa213-113">이렇게 하면 리소스 그룹이 생성되었음을 나타내는 JSON 블록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-113">This would return a JSON block indicating the resource group has been created.</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/<resourcegroup>",
  "location": "eastus",
  "managedBy": null,
  "name": "<resourcegroup>",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="fa213-114">응답의 일부로 구독 고유 식별자, 위치 및 이름이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-114">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="fa213-115">이들 항목을 사용하여 리소스 그룹이 적절한 구독 및 위치에서 생성되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-115">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="fa213-116">이제 리소스 그룹을 만드는 방법을 알았으므로 가상 머신을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="fa213-116">Now that we know how to create a resource group, let's create a new virtual machine.</span></span>