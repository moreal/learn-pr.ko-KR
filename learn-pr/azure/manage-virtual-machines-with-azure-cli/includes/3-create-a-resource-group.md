<span data-ttu-id="ecd88-101">목표는 새로운 Azure 가상 머신을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-101">Our goal is to create a new Azure virtual machine.</span></span> <span data-ttu-id="ecd88-102">리소스 위치, 사용할 OS 및 VM에 필요한 하드웨어 구성을 식별하기 위해 몇 가지 정보를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-102">We'll need to supply several pieces of information to identify the resource location, OS to use, and the hardware configuration needed for the VM.</span></span> <span data-ttu-id="ecd88-103">**리소스 그룹**부터 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-103">Let's start with the **resource group**.</span></span>

## <a name="create-a-resource-group"></a><span data-ttu-id="ecd88-104">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="ecd88-104">Create a resource group</span></span>

<span data-ttu-id="ecd88-105">Azure는 _리소스 그룹_을 사용하여 가상 머신 및 데이터베이스와 같은 관련 리소스를 그룹화합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-105">Azure uses _resource groups_ to group related resources such as virtual machines and databases together.</span></span> <span data-ttu-id="ecd88-106">또한 리소스 그룹은 리소스가 배치되는 데이터 센터를 결정하는 특정 위치(“지역”이라고 함)를 식별합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-106">The resource group also identifies a specific location (called a "region") which will decide what data center the resource is placed into.</span></span>

<span data-ttu-id="ecd88-107">실험을 진행하고 있으므로 먼저 `ExerciseResources`라는 새 리소스 그룹을 만들고 `eastus` 지역에 배치합니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-107">Since we're experimenting, start by creating a new resource group named `ExerciseResources` and place it into the `eastus` region.</span></span>

<!-- TODO: replace with free ed-tier -->

<span data-ttu-id="ecd88-108">Azure Cloud Shell에 다음 Azure CLI 명령을 입력하여 구독에서 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-108">Type the following Azure CLI command in Azure Cloud Shell to create the resource group in your subscription.</span></span>

```azurecli
az group create --name ExerciseResources --location eastus
```

<span data-ttu-id="ecd88-109">이렇게 하면 리소스 그룹이 생성되었음을 나타내는 JSON 블록이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-109">This will return a JSON block indicating the resource group has been created.</span></span> <span data-ttu-id="ecd88-110">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-110">It should look something like:</span></span>

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/ExerciseResources",
  "location": "eastus",
  "managedBy": null,
  "name": "ExerciseResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

<span data-ttu-id="ecd88-111">응답의 일부로 구독 고유 식별자, 위치 및 이름이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-111">Notice that it returns the subscription unique identifier, location, and name as part of the response.</span></span> <span data-ttu-id="ecd88-112">이들 항목을 사용하여 리소스 그룹이 적절한 구독 및 위치에서 생성되었는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-112">You can use these to verify it got created in the proper subscription and location.</span></span>

<span data-ttu-id="ecd88-113">이제 리소스 그룹이 있으므로 새 가상 머신을 만들어 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ecd88-113">Now that we have a resource group, let's create a new virtual machine.</span></span>