
## <a name="what-is-microsoft-cognitive-services"></a><span data-ttu-id="19efc-101">Microsoft Cognitive Services란?</span><span class="sxs-lookup"><span data-stu-id="19efc-101">What is Microsoft Cognitive Services?</span></span>

<span data-ttu-id="19efc-102">Microsoft Cognitive Services는 누구나 사용할 수 있도록 서비스로 제공되는 기계 학습 알고리즘 집합입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-102">Microsoft Cognitive Services is a set of machine learning algorithms available as a service for anyone to use.</span></span> <span data-ttu-id="19efc-103">앱에 사용할 인텔리전스를 처음부터 구축하는 대신 시각, 음성, 언어, 지식 및 검색에 이 서비스를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-103">Instead of building this intelligence for our apps from scratch, we can use these services for vision, speech, language, knowledge, and search.</span></span> <span data-ttu-id="19efc-104">각 서비스를 체험해볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-104">You can try each service for free.</span></span> <span data-ttu-id="19efc-105">서비스를 앱에 통합하기로 결정하면 유료 구독에 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-105">When you decide to integrate a service into your app, you sign up for a paid subscription.</span></span> <span data-ttu-id="19efc-106">이 모델에서는 Computer Vision API에 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-106">We'll focus our attention on the Computer Vision API in this model.</span></span>

> [!TIP]
> <span data-ttu-id="19efc-107">모든 Cognitive Services 목록을 보려면 [Cognitive Services 디렉터리](https://azure.microsoft.com/services/cognitive-services/directory/)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19efc-107">To see a list of all Cognitive Services, check out the [Cognitive Services Directory](https://azure.microsoft.com/services/cognitive-services/directory/).</span></span> 

## <a name="what-is-the-computer-vision-api"></a><span data-ttu-id="19efc-108">Computer Vision API란?</span><span class="sxs-lookup"><span data-stu-id="19efc-108">What is the Computer Vision API?</span></span>

<span data-ttu-id="19efc-109">Computer Vision API는 이미지를 처리하고 인사이트 반환하는 알고리즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-109">The Computer Vision API provides algorithms to process images and return insights.</span></span> <span data-ttu-id="19efc-110">예를 들어, 이미지에 완성도 높은 콘텐츠가 있는지 알아 내거나 서비스를 사용하여 이미지에 있는 얼굴을 모두 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-110">For example, you can find out if an image has mature content, or can use it to find all the faces in an image.</span></span> <span data-ttu-id="19efc-111">또한 지배적인 색과 강조 색을 판단하고, 이미지의 콘텐츠를 분류하며, 완전한 영어 문장으로 이미지를 기술하는 것과 같은 다른 기능도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-111">It also has other features like estimating dominant and accent colors, categorizing the content of images, and describing an image with complete English sentences.</span></span> <span data-ttu-id="19efc-112">큰 이미지를 효율적으로 표시할 수 있도록 이미지 썸네일을 지능적으로 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-112">Additionally, it can also intelligently generate images thumbnails for displaying large images effectively.</span></span>

> [!TIP]
> <span data-ttu-id="19efc-113">Computer Vision API는 전세계 많은 지역에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-113">The Computer Vision API is available in many regions across the globe.</span></span> <span data-ttu-id="19efc-114">가장 가까운 위치를 찾으려면 [지역별 사용 가능한 제품](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="19efc-114">To find the region nearest you, see the [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=cognitive-services&regions=all).</span></span>

<span data-ttu-id="19efc-115">Computer Vision API를 사용하여 가능한 작업:</span><span class="sxs-lookup"><span data-stu-id="19efc-115">You can use the Computer Vision API to:</span></span>

- <span data-ttu-id="19efc-116">인사이트를 위한 이미지 분석</span><span class="sxs-lookup"><span data-stu-id="19efc-116">Analyze images for insight</span></span>
- <span data-ttu-id="19efc-117">OCR(광학 문자 인식)을 사용한 이미지의 인쇄 텍스트 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-117">Extract printed text from images using optical character recognition (OCR).</span></span>
- <span data-ttu-id="19efc-118">이미지의 인쇄 텍스트 및 필기 텍스트 인식</span><span class="sxs-lookup"><span data-stu-id="19efc-118">Recognize printed and handwritten text from images</span></span>
- <span data-ttu-id="19efc-119">유명인 및 랜드마크 인식</span><span class="sxs-lookup"><span data-stu-id="19efc-119">Recognize celebrities and landmarks</span></span>
- <span data-ttu-id="19efc-120">비디오 분석</span><span class="sxs-lookup"><span data-stu-id="19efc-120">Analyze video</span></span> 
- <span data-ttu-id="19efc-121">이미지의 썸네일 생성</span><span class="sxs-lookup"><span data-stu-id="19efc-121">Generate a thumbnail of an image</span></span> 

## <a name="how-to-call-the-computer-vision-api"></a><span data-ttu-id="19efc-122">Computer Vision API를 호출하는 방법</span><span class="sxs-lookup"><span data-stu-id="19efc-122">How to call the Computer Vision API</span></span>

<span data-ttu-id="19efc-123">클라이언트 라이브러리 또는 REST API를 직접 사용하여 응용 프로그램에서 Computer Vision을 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-123">You call Computer Vision in your application using client libraries or the REST API directly.</span></span> <span data-ttu-id="19efc-124">이 모듈에서는 REST API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-124">We'll call the REST API in this module.</span></span> <span data-ttu-id="19efc-125">호출을 수행하려면:</span><span class="sxs-lookup"><span data-stu-id="19efc-125">To make a call:</span></span>

1. <span data-ttu-id="19efc-126">API 액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="19efc-126">Get an API access key</span></span>

    <span data-ttu-id="19efc-127">Computer Vision 서비스 계정을 등록할 때 액세스 키가 할당됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-127">You are assigned access keys when you sign up for a Computer Vision service account.</span></span> <span data-ttu-id="19efc-128">**모든** 요청의 헤더에는 키가 전달되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-128">A key must be passed in the header of **every** request.</span></span> 

1. <span data-ttu-id="19efc-129">API에 POST 호출 수행</span><span class="sxs-lookup"><span data-stu-id="19efc-129">Make a POST call to the API</span></span>

    <span data-ttu-id="19efc-130">URL을 다음과 같은 형식으로 지정합니다 **지역**.api.cognitive.microsoft.com/vision/v2.0/**리소스**/**[매개 변수]**</span><span class="sxs-lookup"><span data-stu-id="19efc-130">Format the URL as follows: **region**.api.cognitive.microsoft.com/vision/v2.0/**resource**/**[parameters]**</span></span> 

    - <span data-ttu-id="19efc-131">**지역** - 계정을 만든 지역, 예: *westus*.</span><span class="sxs-lookup"><span data-stu-id="19efc-131">**region** - the region where you created the account, for example, *westus*.</span></span>
    - <span data-ttu-id="19efc-132">**리소스** - 호출하는 Computer Vision 리소스(예: `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`)입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-132">**resource** - the Computer Vision resource you are calling such as `analyze`, `describe`, `generateThumbnail`, `ocr`, `models`, `recognizeText`, `tag`.</span></span>

    <span data-ttu-id="19efc-133">처리할 이미지는 원시 이미지 바이너리나 이미지 URL로 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-133">You can supply the image to be processed either as a raw image binary or an image URL.</span></span>

    <span data-ttu-id="19efc-134">요청 헤더에는 구독 키가 있어야 합니다. 구독 키는 이 API에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-134">The request header must contain the subscription key, which provides access to this API.</span></span>

1. <span data-ttu-id="19efc-135">응답 구문 분석</span><span class="sxs-lookup"><span data-stu-id="19efc-135">Parse the response</span></span>

    <span data-ttu-id="19efc-136">응답에는 내 이미지에 대해 Computer Vision API에 있는 인사이트가 JSON 페이로드로 보관됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-136">The response holds the insight the Computer Vision API had about your image as a JSON payload.</span></span>

<span data-ttu-id="19efc-137">`westus` 지역에서 내 Computer Vision 구독을 만들어서 API에 액세스할 구독 키를 확보했다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-137">Suppose you created my Computer Vision subscription in the `westus` region and got a subscription key to access the API.</span></span> <span data-ttu-id="19efc-138">키에 `xxxx-xxxxx-xxxx-xxxx`라는 가상의 값을 부여하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-138">Let's give the key a fictitious value of `xxxx-xxxxx-xxxx-xxxx`.</span></span> <span data-ttu-id="19efc-139">이제 `http://example.com/images/test.jpg`에 있는 이미지의 썸네일을 생성해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-139">You now want to generate a thumbnail for an image located at `http://example.com/images/test.jpg`.</span></span> <span data-ttu-id="19efc-140">`generateThumbnail`을 사용하는 요청은 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-140">Using `generateThumbnail`, the request would look like the following.</span></span>

```
curl POST "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail
-H "Content-Type: application/json"
-H "Ocp-Apim-Subscription-Key: {xxxx-xxxxx-xxxx-xxxx}"
-d "{'url':'http://example.com/images/test.jpg'}"
```

<span data-ttu-id="19efc-141">이 모듈에서는 통합된 Cloud Shell을 사용하여 Azure CLI의 모든 연습을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-141">In this module, we'll run all exercises in the Azure CLI using the integrated Cloud Shell.</span></span> <span data-ttu-id="19efc-142">이 설정에 대해 좀 더 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-142">Let's find out a little more about this setup.</span></span>

## <a name="what-is-the-azure-cli"></a><span data-ttu-id="19efc-143">Azure CLI란?</span><span class="sxs-lookup"><span data-stu-id="19efc-143">What is the Azure CLI</span></span>

<span data-ttu-id="19efc-144">Azure CLI는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-144">The Azure CLI is Microsoft's cross-platform command-line tool for managing Azure resources.</span></span> <span data-ttu-id="19efc-145">macOS, Linux 및 Windows에서 또는 브라우저에서 [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview)을 통해 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-145">It's available for macOS, Linux, and Windows, or in the browser using [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/overview).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="19efc-146">Azure CLI 도구는 현재 Azure CLI 1.0 및 Azure CLI 2.0의 두 가지 버전이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-146">There are two versions of the Azure CLI tool available today: Azure CLI 1.0 and Azure CLI 2.0.</span></span> <span data-ttu-id="19efc-147">레거시 스크립트를 실행하는 경우가 아니라면 최신 버전인 Azure CLI 2.0을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-147">We'll be using Azure CLI 2.0, which is the latest version and is recommended unless you're running legacy scripts.</span></span> <span data-ttu-id="19efc-148">Azure CLI 1.0은 `azure` 명령으로 시작되고 Azure CLI 2.0은 `az` 명령으로 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-148">Azure CLI 1.0 is started with the `azure` command, and Azure CLI 2.0 is started with the `az` command.</span></span>

## <a name="az-cognitiveservices-commands"></a><span data-ttu-id="19efc-149">az cognitiveservices 명령</span><span class="sxs-lookup"><span data-stu-id="19efc-149">az cognitiveservices commands</span></span>

<span data-ttu-id="19efc-150">Azure CLI에는 Azure의 Cognitive Services 계정을 관리하는 `cognitiveservices` 명령이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-150">The Azure CLI includes the `cognitiveservices` command to manage Cognitive Services accounts in Azure.</span></span> <span data-ttu-id="19efc-151">여러 하위 명령을 제공하여 특정 작업을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-151">We can supply several subcommands to do specific tasks.</span></span> <span data-ttu-id="19efc-152">가장 일반적인 하위 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-152">The most common include:</span></span>

| <span data-ttu-id="19efc-153">하위 명령</span><span class="sxs-lookup"><span data-stu-id="19efc-153">Subcommand</span></span> | <span data-ttu-id="19efc-154">설명</span><span class="sxs-lookup"><span data-stu-id="19efc-154">Description</span></span> |
|-------------|-------------|
| `list` | <span data-ttu-id="19efc-155">사용 가능한 Azure Cognitive Services 계정을 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-155">List available Azure Cognitive Services accounts.</span></span> |
| `account show` | <span data-ttu-id="19efc-156">Azure Cognitive Services 계정의 세부 정보를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-156">Get the details of an Azure Cognitive Services account.</span></span> |
| `account create` | <span data-ttu-id="19efc-157">Azure Cognitive Services 계정을 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-157">Create an Azure Cognitive Services account.</span></span> |
| `account delete` | <span data-ttu-id="19efc-158">Azure Cognitive Services 계정을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-158">Delete an Azure Cognitive Services account.</span></span> |
| `keys list` | <span data-ttu-id="19efc-159">Azure Cognitive Services 계정의 키를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-159">List the keys of an Azure Cognitive Services account.</span></span> |

<span data-ttu-id="19efc-160">Azure CLI로 Cognitive Services를 생성해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-160">Let's create a Cognitive Services with the Azure CLI.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-cognitive-services-account"></a><span data-ttu-id="19efc-161">Cognitive Services 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="19efc-161">Create a Cognitive Services account</span></span>

<span data-ttu-id="19efc-162">Computer Vision API를 호출하려면 API 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-162">We need an API access key to make calls to the Computer Vision API.</span></span> <span data-ttu-id="19efc-163">액세스 키를 확보하려면 Computer Vision API에 대한 Cognitive Services 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-163">To get access keys, we need a Cognitive Services account for the Computer Vision API.</span></span> <span data-ttu-id="19efc-164">`az cognitiveservices create`을 사용하여 내 구독에 계정을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-164">We'll use `az cognitiveservices create` to create the account in our subscription.</span></span>

 <span data-ttu-id="19efc-165">`az cognitiveservices create` 명령은 리소스 그룹에 Cognitive Services 계정을 만드는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-165">The command `az cognitiveservices create` is used to create a Cognitive Services account in a resource group.</span></span>  <span data-ttu-id="19efc-166">이 명령을 호출할 때는 다음 다섯 가지 매개 변수를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-166">The following five parameters must be supplied when calling this command.</span></span>

> [!Tip]
> <span data-ttu-id="19efc-167">Azure CLI 매개 변수에 대한 대부분의 플래그는 단일 문자로 축약이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-167">Most flags for Azure CLI parameters can be abbreviated to a single character.</span></span> <span data-ttu-id="19efc-168">예를 들어 `--location` 대신 `-l`이라고 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-168">For example, we could say `-l` instead of `--location`.</span></span> <span data-ttu-id="19efc-169">긴 양식은 명확성을 위해 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-169">The long-form is used for clarity.</span></span>

| <span data-ttu-id="19efc-170">매개 변수</span><span class="sxs-lookup"><span data-stu-id="19efc-170">Parameter</span></span> | <span data-ttu-id="19efc-171">설명</span><span class="sxs-lookup"><span data-stu-id="19efc-171">Description</span></span> |
|-----------|-------------|
| `resource-group` | <span data-ttu-id="19efc-172">Cognitive Services 계정을 소유할 리소스 그룹입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-172">The resource group that will own the cognitive services account.</span></span> <span data-ttu-id="19efc-173">이 대화형 샌드박스 세션에서는 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-173">In this interactive sandbox session, you'll use <rgn>[sandbox resource group name]</rgn></span></span> |
| `kind` | <span data-ttu-id="19efc-174">Cognitive Services 계정의 API 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-174">The API name of cognitive services account.</span></span> |
| `name` | <span data-ttu-id="19efc-175">Cognitive Services 계정 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-175">Cognitive service account name.</span></span> |
| `sku` | <span data-ttu-id="19efc-176">Cognitive Services 계정의 SKU입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-176">The Sku of cognitive services account.</span></span>|
| `location` | <span data-ttu-id="19efc-177">이 API를 호출할 위치 또는 지역입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-177">The location, or region, from which you want to make calls to this API.</span></span> <span data-ttu-id="19efc-178">아래 목록에 있는 위치 중 하나를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-178">Select one of the locations from the list below.</span></span> |

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)] 

<span data-ttu-id="19efc-179">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-179">Execute the following command in Azure Cloud Shell.</span></span> <span data-ttu-id="19efc-180">`[location]`은 나와 가까운 위치로 대체해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-180">Make sure to replace `[location]` with a location near you.</span></span>

```azurecli
az cognitiveservices account create \
--kind ComputerVision \
--name ComputerVisionService \
--sku S1 \
--resource-group <rgn>[sandbox resource group name]</rgn> \
--location [location]
```

> [!NOTE]
> <span data-ttu-id="19efc-181">선택한 위치를 기억해 두세요.</span><span class="sxs-lookup"><span data-stu-id="19efc-181">Remember the location you have selected.</span></span> <span data-ttu-id="19efc-182">이 위치에서 API에 대한 모든 호출을 수행하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-182">You'll make all calls to the API from that region.</span></span>

<span data-ttu-id="19efc-183">**ComputerVision** API에 대한 Cognitive Services 계정을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-183">We've created a cognitive services account for the **ComputerVision** API.</span></span> <span data-ttu-id="19efc-184">*S1* sku를 선택하고 해당 계정의 이름을 **ComputerVisionService**로 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-184">We selected the *S1* sku and named our account **ComputerVisionService**.</span></span> <span data-ttu-id="19efc-185">해당 계정은 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 이라는 리소스 그룹이 소유하며 `--location` 매개 변수에 설정한 위치에서 API를 호출합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-185">Our account is owned by the resource group **<rgn>[sandbox resource group name]</rgn>** and we'll call the API from the location we set in the `--location` parameter.</span></span> 

<span data-ttu-id="19efc-186">명령을 통해 Cognitive Services 계정이 생성되면, **Succeeded**로 설정된 **provisioningState** 속성이 포함된 JSON 응답을 받게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-186">Once the command finishes creating the cognitive services account, you'll get a JSON response, which includes **provisioningState** property set to **Succeeded**.</span></span>

## <a name="get-an-access-key"></a><span data-ttu-id="19efc-187">액세스 키 가져오기</span><span class="sxs-lookup"><span data-stu-id="19efc-187">Get an access key</span></span>

<span data-ttu-id="19efc-188">계정이 성공적으로 만들어지면 이 계정에 대한 구독 키 또는 액세스 키를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-188">Once we have our account successfully created we can retrieve the subscription keys, or access keys, for this account.</span></span>

1. <span data-ttu-id="19efc-189">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-189">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn>
    ```
    
    <span data-ttu-id="19efc-190">위의 명령은 주어진 리소스 그룹이 소유하는 **ComputerVisionService**라는 Cognitive Services 계정과 연결된 키를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-190">The above command returns the keys associated with the cognitive services account called **ComputerVisionService**, which is owned by the given resource group.</span></span> <span data-ttu-id="19efc-191">두 가지 키가 반환되며 그 중 하나는 여분의 키입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-191">It returns two keys - one is a spare key.</span></span> <span data-ttu-id="19efc-192">키는 기억하기 어려우니 첫 번째 키를 API에 대한 모든 호출에 사용할 변수에 저장하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-192">The keys are difficult to remember, so we'll store the first key in a variable that we'll use for all calls to the API.</span></span>

2.  <span data-ttu-id="19efc-193">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-193">Execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    key=$(az cognitiveservices account keys list \
    --name ComputerVisionService \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --query key1 -o tsv)
    ```
    
    <span data-ttu-id="19efc-194">Azure CLI 2.0은 `--query` 인수를 사용하여 명령의 결과에 대해 JMESPath 쿼리를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-194">The Azure CLI 2.0 uses the `--query` argument to execute a JMESPath query on the results of commands.</span></span> <span data-ttu-id="19efc-195">JMESPath는 JSON의 쿼리 언어이며, CLI 출력의 데이터를 선택하고 표시하는 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-195">JMESPath is a query language for JSON, giving you the ability to select and present data from CLI output.</span></span> <span data-ttu-id="19efc-196">다른 표시 형식 전에 이러한 쿼리를 JSON 출력에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-196">These queries are executed on the JSON output before any display formatting.</span></span>
    <span data-ttu-id="19efc-197">`--query` 인수는 Azure CLI의 모든 명령에서 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-197">The `--query` argument is supported by all commands in the Azure CLI.</span></span> 
    
    <span data-ttu-id="19efc-198">이 예제에서는 "key1" 항목에 대한 키 목록을 쿼리하고 그 결과를 **tsv** 형식으로 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-198">In our example, we query the list of keys for an entry named "key1" and output the result to **tsv** format.</span></span> <span data-ttu-id="19efc-199">이 형식은 문자열 값을 묶는 따옴표를 제거합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-199">This format removes quotations around the string value.</span></span> <span data-ttu-id="19efc-200">결과는 변수 **키**에 할당합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-200">We assign the result to a variable **key**.</span></span>
    
    > [!IMPORTANT]
    > <span data-ttu-id="19efc-201">이 키는 모듈 전반에서 사용되기 때문에 변수 내에 저장하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-201">We're going to use this key throughout the module, so saving it in a variable is a good idea.</span></span> <span data-ttu-id="19efc-202">값을 잊어버리거나 변수에 대한 설정이 해제되면 명령을 다시 실행하여 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-202">If you lose the value or the variable becomes unset, run the command again to set it.</span></span>  

3. <span data-ttu-id="19efc-203">키의 값을 보려면 Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-203">To see the value of our key, execute the following command in Azure Cloud Shell:</span></span>

    ```azurecli
    echo $key
    ```

<span data-ttu-id="19efc-204">계정과 키가 준비되었으면 API에 호출을 보낼 차례입니다.</span><span class="sxs-lookup"><span data-stu-id="19efc-204">Now that we have an account and a key, it's time to make some calls to the API.</span></span>