<span data-ttu-id="c97ca-101">Computer Vision API가 이미지에서 인쇄된 텍스트를 추출하는 방법을 살펴보았습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-101">We saw how the Computer Vision API can extract printed text from images.</span></span> <span data-ttu-id="c97ca-102">이 연습에서는 서비스를 사용하여 필기 텍스트를 감지하는 방법을 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-102">In this exercise, we'll use the service to detect handwritten text.</span></span>

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a><span data-ttu-id="c97ca-103">Computer Vision API를 호출하여 필기 텍스트 추출</span><span class="sxs-lookup"><span data-stu-id="c97ca-103">Calling the Computer Vision API to extract handwritten text</span></span>

<span data-ttu-id="c97ca-104">`recognizeText` 작업을 통해 메모, 문자, 에세이, 화이트보드, 양식 및 기타 소스에서 필기 텍스트를 감지하고 추출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-104">The `recognizeText` operation detects and extracts handwritten text from notes, letters, essays, whiteboards, forms, and other sources.</span></span> <span data-ttu-id="c97ca-105">요청 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-105">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

<span data-ttu-id="c97ca-106">모든 호출은 계정이 생성된 지역에 대해 이루어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-106">All calls must be made to the region where the account was created.</span></span>

<span data-ttu-id="c97ca-107">`mode` 매개 변수가 있는 경우 이 매개 변수는 `Handwritten` 또는 `Printed`로 설정되어야 하며 대/소문자를 구분합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-107">If present, the `mode` parameter must be set to `Handwritten` or `Printed` and is case-sensitive.</span></span> <span data-ttu-id="c97ca-108">매개 변수가 `Handwritten`으로 설정되거나 지정되지 않은 경우에는 필기 인식이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-108">If the parameter is set to `Handwritten` or is not specified, handwriting recognition is performed.</span></span> <span data-ttu-id="c97ca-109">매개 변수가 `Printed`로 설정된 경우에는 인쇄 텍스트 인식이 이루어집니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-109">If the parameter is set to `Printed`, then printed text recognition is performed.</span></span> <span data-ttu-id="c97ca-110">이 호출에서 결과를 가져오는 데 걸리는 시간은 이미지의 쓰기 양에 따라 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-110">The time it takes to get a result from this call depends on the amount of writing in the image.</span></span>

<span data-ttu-id="c97ca-111">이 예제에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-111">In this example, we'll:</span></span>

- <span data-ttu-id="c97ca-112">cUrl의 `-D` 옵션을 사용하여 응답 헤더를 콘솔에 인쇄</span><span class="sxs-lookup"><span data-stu-id="c97ca-112">Print the response headers to the console using cUrl's `-D` option</span></span>
- <span data-ttu-id="c97ca-113">응답에서 수신한 헤더에서 `Operation-Location` 헤더 값 복사</span><span class="sxs-lookup"><span data-stu-id="c97ca-113">Copy the `Operation-Location` header value from the headers we receive in the response</span></span>
- <span data-ttu-id="c97ca-114">몇 초 후, 결과에 대해 `Operation-Location`에서 지정한 URL 확인</span><span class="sxs-lookup"><span data-stu-id="c97ca-114">After a few seconds, check the URL specified by the `Operation-Location` for the results</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a><span data-ttu-id="c97ca-115">이미지에서 필기 텍스트 검색 및 추출</span><span class="sxs-lookup"><span data-stu-id="c97ca-115">Detect and extract handwritten text from an image</span></span>

<span data-ttu-id="c97ca-116">이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-116">We'll use the following image in this example, but you're free to try the same command with URLs to other images.</span></span>

![노트에 필기 샘플이 있는 사진](../media/6-handwriting.jpg)

1. <span data-ttu-id="c97ca-118">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-118">Execute the following commands in Azure Cloud Shell.</span></span> <span data-ttu-id="c97ca-119">명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-119">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

<span data-ttu-id="c97ca-120">위에서는 이 작업의 헤더를 콘솔로 덤프합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-120">The above dumps the headers of this operation to the console.</span></span> <span data-ttu-id="c97ca-121">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-121">Here's an example:</span></span>

```azurecli
HTTP/1.1 202 Accepted
Cache-Control: no-cache
Pragma: no-cache
Content-Length: 0
Expires: -1
Operation-Location: https://westus2.api.cognitive.microsoft.com/vision/v2.0/textOperations/d0e9b397-4072-471c-ae61-7490bec8f077
X-AspNet-Version: 4.0.30319
X-Powered-By: ASP.NET
apim-request-id: f5663487-03c6-4760-9be7-c9157fac10a1
Strict-Transport-Security: max-age=31536000; includeSubDomains; preload
x-content-type-options: nosniff
Date: Wed, 12 Sep 2018 19:22:00 GMT
```

<span data-ttu-id="c97ca-122">`Operation-Location` 헤더는 완료 후에 결과가 게시되는 위치입니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-122">The `Operation-Location` header is where the results will be posted once complete.</span></span>

2. <span data-ttu-id="c97ca-123">`Operation-Location` 헤더 값을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-123">Copy the `Operation-Location` header value.</span></span>
1. <span data-ttu-id="c97ca-124">Azure Cloud Shell에서 `"<Operation-Location>"`을 이전 단계에서 복사한 **Operation-Location** 헤더의 값으로 바꾸는 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-124">Execute the following command in Azure Cloud Shell replacing `"<Operation-Location>"` with the value for the **Operation-Location** header you copied from the preceding step.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

<span data-ttu-id="c97ca-125">작업이 완료되면 필기 인식 요청의 결과를 포함하는 JSON 파일이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="c97ca-125">If the operation has completed, you'll receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="c97ca-126">`recognizeText` 작업에 대한 자세한 내용은 [필기 텍스트 인식](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c97ca-126">For more information about the `recognizeText` operation, see the [Recognize Handwritten Text](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) reference documentation.</span></span>