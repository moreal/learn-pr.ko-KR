<span data-ttu-id="9b9ec-101">가상 머신을 만들기 위한 이미지에 `Debian`을 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-101">We used `Debian` for the image to create the virtual machine.</span></span> <span data-ttu-id="9b9ec-102">Azure에는 가상 머신을 만드는 데 사용할 수 있는 여러 가지 표준 VM 이미지가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-102">Azure has several standard VM images you can use to create a virtual machine.</span></span> 

## <a name="listing-images"></a><span data-ttu-id="9b9ec-103">이미지 나열</span><span class="sxs-lookup"><span data-stu-id="9b9ec-103">Listing images</span></span>

<span data-ttu-id="9b9ec-104">다음 명령을 사용하여 사용 가능한 VM 이미지 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-104">You can get a list of the available VM images using the following command.</span></span> 

```azurecli
az vm image list --output table
```

<span data-ttu-id="9b9ec-105">이렇게 하면 Azure CLI에 빌드된 오프라인 목록에 일부인 가장 인기 있는 이미지가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-105">This will output the most popular images that are part of an offline list built into the Azure CLI.</span></span> <span data-ttu-id="9b9ec-106">그러나 Azure Marketplace에는 사용 가능한 _수백_ 개의 이미지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-106">However, there are _hundreds_ of image options available in the Azure Marketplace.</span></span> 

## <a name="getting-all-images"></a><span data-ttu-id="9b9ec-107">모든 이미지 가져오기</span><span class="sxs-lookup"><span data-stu-id="9b9ec-107">Getting all images</span></span>

<span data-ttu-id="9b9ec-108">명령에 `--all` 플래그를 추가하여 전체 목록을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-108">You can get a full list by adding the `--all` flag to the command.</span></span> <span data-ttu-id="9b9ec-109">Marketplace의 이미지 목록은 매우 크기 때문에 `--publisher`, `--sku` 또는 `–-offer` 옵션으로 목록을 필터링하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-109">Since the list of images in the Marketplace is very large, it is helpful to filter the list with the `--publisher`, `--sku` or `–-offer` options.</span></span>

<span data-ttu-id="9b9ec-110">예를 들어, 다음 명령을 실행하여 사용 가능한 _모든_ Wordpress 이미지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-110">For example, try the following command to see _all_ Wordpress images available:</span></span>

```azurecli
az vm image list --sku Wordpress --output table --all
```

<span data-ttu-id="9b9ec-111">또는 이 명령을 사용하여 Microsoft에서 제공하는 모든 이미지를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-111">Or this command to see all images provided by Microsoft:</span></span>

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a><span data-ttu-id="9b9ec-112">위치별 이미지</span><span class="sxs-lookup"><span data-stu-id="9b9ec-112">Location-specific images</span></span>

<span data-ttu-id="9b9ec-113">일부 이미지는 특정 위치에서만 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-113">Some images are only available in certain locations.</span></span> <span data-ttu-id="9b9ec-114">가상 머신을 만들려는 영역에서 사용 가능한 것으로 결과의 범위를 지정하려면 명령에 `--location [location]` 플래그를 추가하세요.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-114">Try adding the `--location [location]` flag to the command to scope the results to ones available in the region where you want to create the virtual machine.</span></span> <span data-ttu-id="9b9ec-115">예를 들어 `eastus` 지역에서 사용할 수 있는 이미지 목록을 가져오려면 Azure Cloud Shell에 다음을 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-115">For example, type the following into Azure Cloud Shell to get a list of images available in the `eastus` region.</span></span>

```azurecli
az vm image list --location eastus --output table
```

<span data-ttu-id="9b9ec-116">사용 가능한 다른 Azure 샌드박스 위치에서 일부 이미지를 확인하세요.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-116">Try checking some of the images in the other Azure sandbox available locations:</span></span>

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> <span data-ttu-id="9b9ec-117">다음은 Azure에서 제공하는 표준 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-117">These are the standard images that are provided by Azure.</span></span> <span data-ttu-id="9b9ec-118">고유한 구성, 덜 일반적인 버전 또는 운영 체제의 배포를 기반으로 VM을 만들려면 [고유한 사용자 지정 이미지를 만들고 업로드](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images)할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-118">Keep in mind that you can also [create and upload your own custom images](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images) to create VMs based on unique configurations or less common versions or distributions of an operating system.</span></span>

<span data-ttu-id="9b9ec-119">이제 아마도 명령 창이 가득 차 있을 것입니다. 원하는 경우 `clear`를 입력하여 화면을 지울 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9b9ec-119">Your command window is probably full now, you can type `clear` to clear the screen if you like.</span></span>