<span data-ttu-id="4004b-101">현장 유통업자가 재고를 보충하는 매장 선반의 이미지를 스캔하여 업로드할 수 있는 사업 부문 앱을 빌드하고 유지 관리해야 하는 Contoso Beverage Distribution의 개발 책임자를 예로 들어보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-101">As a lead developer at Contoso Beverage Distribution, you're responsible for building and maintaining a line-of-business app that lets your frontline distributors scan and upload images of store shelves where they are restocking.</span></span> 

<span data-ttu-id="4004b-102">사용자가 게시하는 모든 이미지가 회사에서 설정한 콘텐츠 규칙을 준수하는지 유효성을 검사하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-102">You want to validate that any images posted by users respect the content rules set by your company.</span></span> <span data-ttu-id="4004b-103">회사는 회사 사이트에 부적절한 콘텐츠가 게시되기를 원치 않습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-103">The company doesn't want inappropriate content posted to company sites.</span></span> <span data-ttu-id="4004b-104">인공 지능의 개선 사항을 기반으로 앱에서 Computer Vision API를 사용하기로 했습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-104">Given the advancements in Artificial Intelligence, you decide to use the Computer Vision API in your app.</span></span> 

<span data-ttu-id="4004b-105">먼저 Azure 구독에서 Computer Vision 계정을 만들고 **분석** 기능 테스트를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-105">To get started, you create a Computer Vision account in your Azure subscription and start testing the **analyze** feature.</span></span>

## <a name="calling-the-computer-vision-api-to-analyze-images"></a><span data-ttu-id="4004b-106">Computer Vision API를 호출하여 이미지 분석</span><span class="sxs-lookup"><span data-stu-id="4004b-106">Calling the Computer Vision API to analyze images</span></span>

<span data-ttu-id="4004b-107">`analyze` 작업은 이미지 콘텐츠를 기준으로 다양한 시각적 기능 집합을 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-107">The `analyze` operation extracts a rich set of visual features based on the image content.</span></span> <span data-ttu-id="4004b-108">요청 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-108">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=<...>&details=<...>&language=<...>`

<span data-ttu-id="4004b-109">서비스로 전송되는 매개 변수는 `visualFeatures`, `details` 및 `languages`입니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-109">The parameters that are sent to the service are `visualFeatures`, `details`, and `languages`.</span></span> <span data-ttu-id="4004b-110">`details` 매개 변수를 `Landmarks` 또는 `Celebrities`로 설정하면 랜드마크나 유명인을 쉽게 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-110">Set the `details` parameter to `Landmarks` or `Celebrities` to help you identify landmarks or celebrities.</span></span> <span data-ttu-id="4004b-111">`visualFeatures`를 사용하는 경우에는 서비스가 반환할 정보의 종류를 식별할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-111">`visualFeatures` identify what kind of information you want the service to return you.</span></span> <span data-ttu-id="4004b-112">`Categories` 옵션은 나무, 건물 등과 같은 이미지 콘텐츠를 분류합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-112">The `Categories` option will categorize the content of the images like trees, buildings, and more.</span></span> <span data-ttu-id="4004b-113">`Faces`는 사람의 얼굴을 식별하여 성별과 나이를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-113">`Faces` will identify people's faces and give you their gender and age.</span></span>

<span data-ttu-id="4004b-114">Computer Vision API의 모든 작업에서는 처리하는 이미지에 다음 제한 사항이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-114">All operations on the Computer Vision API have the following restrictions when it comes to the images you ask it to process:</span></span>

- <span data-ttu-id="4004b-115">지원되는 이미지 형식: JPEG, PNG, GIF, BMP</span><span class="sxs-lookup"><span data-stu-id="4004b-115">Supported image formats: JPEG, PNG, GIF, BMP.</span></span> 
- <span data-ttu-id="4004b-116">이미지 파일 크기는 4MB 미만이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-116">Image file size must be less than  4 MB.</span></span>
- <span data-ttu-id="4004b-117">이미지 크기는 최소 50 x 50이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-117">Image dimensions must be at least 50 x 50.</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a><span data-ttu-id="4004b-118">이미지에서 랜드마크 식별하기</span><span class="sxs-lookup"><span data-stu-id="4004b-118">Identify landmarks in an image</span></span>

<span data-ttu-id="4004b-119">이미지에서 랜드마크를 찾기 위해 호출로 시작해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-119">Let's start with a call to find landmarks in an image.</span></span> <span data-ttu-id="4004b-120">이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-120">We'll use the following image for this example, but you're free to try the same command with URLs to other images.</span></span> 

![눈 덮인 산 위에 파란 하늘이 펼쳐진 산맥 그림.](../media/3-mountains.jpg)

<span data-ttu-id="4004b-122">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-122">Execute the following command in Azure Cloud Shell.</span></span> <span data-ttu-id="4004b-123">명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-123">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

- <span data-ttu-id="4004b-124">이 호출은 이미지 URL에 의해 지정된 이미지에서 랜드마크를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-124">This call looks for landmarks in the image specified by the image URL.</span></span> <span data-ttu-id="4004b-125">분석 중인 이미지는 이 예제에 대한 GitHub 리포지토리에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-125">The image we are analyzing is stored in a GitHub repo for this exercise.</span></span> 
- <span data-ttu-id="4004b-126">또한 호출은 서비스가 범주 정보 및 이미지 설명을 반환할 것을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-126">The call also asks the service to return category information and a description of the image.</span></span> <span data-ttu-id="4004b-127">설명은 완전한 영어 문장으로 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-127">The description is returned as a complete English sentence.</span></span> 
- <span data-ttu-id="4004b-128">API에 대한 모든 호출에는 액세스 키가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-128">As you know, every call to the API needs an access key.</span></span> <span data-ttu-id="4004b-129">이것은 요청의 `Ocp-Apim-Subscription-Key` 헤더에 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-129">This is set in the `Ocp-Apim-Subscription-Key` header of the request.</span></span> 

> [!TIP]
> <span data-ttu-id="4004b-130">요청 결과는 `url`에서 그림을 설명하는 원시 JSON입니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-130">The result of the request is the raw JSON describing the picture in the `url`.</span></span> <span data-ttu-id="4004b-131">명령의 끝에 ` | jq '.'`를 추가하여 JSON 출력을 말끔하게 표시했습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-131">We added ` | jq '.'` at the end of the command to prettify the JSON output.</span></span>

<span data-ttu-id="4004b-132">이 호출의 JSON 응답은 다음을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-132">The JSON response from this call returns the following:</span></span>

- <span data-ttu-id="4004b-133">이미지가 지정된 범주에 속한다는 사실을 서비스가 얼마나 확신하는지 나타내는 0에서 1 사이의 점수와 함께, 감지된 모든 이미지 범주를 나열하는 `categories` 배열.</span><span class="sxs-lookup"><span data-stu-id="4004b-133">A `categories` array listing all image categories that were detected, along with a score between 0 and 1 of how confident the service is that the image belongs in the specified category.</span></span>
- <span data-ttu-id="4004b-134">이미지와 관련된 태그 또는 단어의 배열을 포함하는 `description` 항목.</span><span class="sxs-lookup"><span data-stu-id="4004b-134">A `description` entry containing an array of tags or words that are related to the image.</span></span>
- <span data-ttu-id="4004b-135">이미지에 포함된 항목을 영어로 설명하는 텍스트 필드가 있는 `captions` 항목.</span><span class="sxs-lookup"><span data-stu-id="4004b-135">A `captions` entry with a text field that describes in English what is in the image.</span></span> <span data-ttu-id="4004b-136">텍스트에도 확실성 점수가 있는지 관찰합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-136">Observe that the text also has a certainty score.</span></span> <span data-ttu-id="4004b-137">이 점수는 이 분석과 함께 다음에 수행할 작업을 결정하는 데 도움이 될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-137">This score can help you decide what to do next with this analysis.</span></span>


## <a name="check-for-inappropriate-content-in-an-image"></a><span data-ttu-id="4004b-138">이미지에서 부적절한 콘텐츠 확인</span><span class="sxs-lookup"><span data-stu-id="4004b-138">Check for inappropriate content in an image</span></span>

<span data-ttu-id="4004b-139">이 예에서는 성인 콘텐츠에 대한 이미지를 분석해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-139">In this example, we'll analyze an image for adult content.</span></span> <span data-ttu-id="4004b-140">신뢰도 점수는 이미지에 성인 콘텐츠 또는 자극적 콘텐츠가 포함될 가능성을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-140">The confidence score rates the likelihood that the image contains either adult or racy content.</span></span> 

<span data-ttu-id="4004b-141">이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-141">We'll use the following image for this example, but you're free to try the same command with URLs to other images.</span></span> 

![웃고 있는 가족사진.](../media/3-people.png)

1. <span data-ttu-id="4004b-143">Azure Cloud Shell에서 다음 명령을 실행하여 URL의 `<region>`을 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-143">Execute the following command in Azure Cloud Shell, replacing `<region>` in the URL.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

<span data-ttu-id="4004b-144">이 예에서는 `visualFeatures`를 `Adult,Description`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-144">In this example, we set the `visualFeatures` to `Adult,Description`.</span></span> 

<span data-ttu-id="4004b-145">응답은 두 가지 신뢰도 점수를 제공합니다. 하나는 자극적 콘텐츠 점수이며 다른 하나는 성인 콘텐츠 점수입니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-145">The response gives us two confidence scores, one for racy content and one for adult content.</span></span> <span data-ttu-id="4004b-146">이러한 점수와 이미지 설명 및 기타 시각적 기능을 사용하여 서버에 게시된 이미지에 대한 플래그 지정을 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-146">Using these scores plus the image description and other visual features, you can start to flag images posted to your server.</span></span>

<span data-ttu-id="4004b-147">이 연습에서 시도한 예제는 `analyze` 작업으로 수행할 수 있는 분석 유형에 대한 아이디어를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4004b-147">The examples we tried in this exercise give you an idea of the type of analysis that you can do with the `analyze` operation.</span></span> <span data-ttu-id="4004b-148">다른 이미지로 분석을 시도하고 시각적 기능, 세부 사항 및 언어 매개 변수의 다양한 조합을 시도해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4004b-148">Try out the analysis with different images and try different combinations of visualFeatures, details, and languages parameters.</span></span>

<span data-ttu-id="4004b-149">`analyze` 작업에 대한 자세한 내용은 [이미지 분석](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4004b-149">For more information about the `analyze` operation, see the [Analyze Image](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) reference documentation.</span></span>