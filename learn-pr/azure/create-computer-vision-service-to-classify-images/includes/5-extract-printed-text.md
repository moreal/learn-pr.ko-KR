<span data-ttu-id="e3223-101">현장 배포자가 서버에 게시하는 재고 이미지에서 텍스트를 읽으려고 하는 경우를 가정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-101">Suppose you now want to read text from the stock images that your frontline distributors post to your server.</span></span> <span data-ttu-id="e3223-102">특히, 판매 가격이 표시된 홍보용 스티커를 찾기 위해 제품을 스캔하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-102">In particular, you want to scan product looking for promotional stickers that containing sale prices.</span></span> <span data-ttu-id="e3223-103">Computer Vision API의 OCR(광학 인식) 기능을 사용해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-103">It's time to try the optical character recognition (OCR) feature of the Computer Vision API.</span></span> 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a><span data-ttu-id="e3223-104">Computer Vision API를 호출하여 인쇄된 텍스트 추출</span><span class="sxs-lookup"><span data-stu-id="e3223-104">Calling the Computer Vision API to extract printed text</span></span>

<span data-ttu-id="e3223-105">`ocr` 작업은 이미지의 텍스트를 감지하고, 인식된 문자를 머신에서 사용 가능한 문자 스트림으로 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-105">The `ocr` operation detects text in an image and extracts the recognized characters into a machine-usable character stream.</span></span> <span data-ttu-id="e3223-106">요청 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-106">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

<span data-ttu-id="e3223-107">평소대로 모든 호출은 계정이 생성된 지역에 대해 이루어져야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-107">As usual, all calls must be made to the region where the account was created.</span></span> <span data-ttu-id="e3223-108">호출은 두 개의 선택적 매개 변수를 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-108">The call accepts two optional parameters:</span></span>

- <span data-ttu-id="e3223-109">**언어**: 이미지에서 감지할 텍스트의 언어 코드입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-109">**language**: The language code of the text to be detected in the image.</span></span> <span data-ttu-id="e3223-110">기본값은 `unk` 또는 알 수 없음입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-110">The default value is `unk`,or unknown.</span></span> <span data-ttu-id="e3223-111">이렇게 하면 서비스가 이미지에서 텍스트의 언어를 자동으로 감지합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-111">This let's the service auto detect the language of the text in the image.</span></span>
- <span data-ttu-id="e3223-112">**detectOrientation**: true인 경우, 서비스는 이미지 방향을 감지하고 이미지 뒤집기 등의 추가 처리를 위해 이미지를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-112">**detectOrientation**: When true, the service  tries to detect the image orientation and correct it before further processing, for example, whether the image is upside-down.</span></span> 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a><span data-ttu-id="e3223-113">OCR을 사용하여 이미지에서 인쇄 텍스트 추출</span><span class="sxs-lookup"><span data-stu-id="e3223-113">Extract printed text from an image using OCR</span></span>

<span data-ttu-id="e3223-114">OCR(광학 인식)에 사용할 이미지는 *.NET Microservices: Architecture for Containerized .NET Applications*(.NET 마이크로 서비스: 컨테이너화된 .NET 응용 프로그램용 아키텍처)라는 책의 표지입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-114">The image we're going to be using for Optical Character Recognition (OCR) is the cover from the book *.NET Microservices: Architecture for Containerized .NET Applications*.</span></span>

![ebook .NET 마이크로 서비스: 컨테이너화된 .NET 응용 프로그램을 위한 아키텍처의 표지 사진](../media/5-ebook.png)

1. <span data-ttu-id="e3223-116">Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-116">Execute the following command in Cloud Shell.</span></span> <span data-ttu-id="e3223-117">명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-117">Replace `<region>` in the command with the region of your cognitive services account.</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

<span data-ttu-id="e3223-118">다음 JSON은 이 호출에서 받은 응답의 예입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-118">The following JSON is an example of the response we get from this call.</span></span> <span data-ttu-id="e3223-119">코드 조각이 페이지에 더 잘 맞도록 일부 JSON 행이 제거되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-119">Some lines of JSON have been removed to make the snippet fit better on the page.</span></span>

```json
{
  "language": "en",
  "orientation": "Up",
  "textAngle": 0,
  "regions" : [
        /*... snipped*/
        {
          "boundingBox": "766,1419,302,33",
          "words": [
            {
              "boundingBox": "766,1419,126,25",
              "text": "Microsoft"
            },
            {
              "boundingBox": "903,1420,165,32",
              "text": "Corporation"
            }
          ]
        }]
}
```

<span data-ttu-id="e3223-120">이 응답을 자세히 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-120">Let's examine this response in more detail.</span></span> 

- <span data-ttu-id="e3223-121">서비스는 텍스트를 영어로 식별했습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-121">The service identified the text as being English.</span></span> <span data-ttu-id="e3223-122">`language` 필드의 값에는 이미지에서 감지된 텍스트의 BCP-47 언어 코드가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-122">The value of the `language` field contains the BCP-47 language code of the text detected in the image.</span></span> <span data-ttu-id="e3223-123">이 예제에서는 **en** 또는 영어입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-123">In this example it is **en**, or English.</span></span> 
- <span data-ttu-id="e3223-124">`orientation`은 **위쪽**으로 감지되었습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-124">The `orientation` was detected as **up**.</span></span> <span data-ttu-id="e3223-125">이 속성은 감지된 텍스트 각도에 따라 이미지가 중심 기준으로 회전한 후 인식된 텍스트의 맨 위가 향하고 있는 방향입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-125">This property is the direction that the top of the recognized text is facing, after the image has been rotated around its center according to the detected text angle.</span></span> 
- <span data-ttu-id="e3223-126">`textAngle`은 가로 또는 세로가 되도록 텍스트가 회전해야 하는 각도입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-126">The `textAngle` is the angle by which the text must be rotated to become horizontal or vertical.</span></span> <span data-ttu-id="e3223-127">이 예제에서는 텍스트가 완전히 가로이므로 반환된 값은 **0**입니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-127">In this example, the text was perfectly horizontal, so the value returned is **0**.</span></span>  
- <span data-ttu-id="e3223-128">`regions` 속성에는 텍스트의 위치, 그림에서의 텍스트 위치 및 이미지의 해당 부분에 있는 단어를 표시하는 데 사용되는 값 목록이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-128">The `regions` property contains a list of values used to show where the text is, its position in the picture, and the word found in that part of the image.</span></span> 
- <span data-ttu-id="e3223-129">`boundingBox` 값의 정수 4개는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-129">The four integers of the `boundingBox` value are:</span></span> 
    - <span data-ttu-id="e3223-130">왼쪽 가장자리의 X 좌표</span><span class="sxs-lookup"><span data-stu-id="e3223-130">the x-coordinate of the left edge</span></span> 
    - <span data-ttu-id="e3223-131">위쪽 가장자리의 Y 좌표</span><span class="sxs-lookup"><span data-stu-id="e3223-131">the y-coordinate of the top edge</span></span>
    - <span data-ttu-id="e3223-132">경계 상자의 폭</span><span class="sxs-lookup"><span data-stu-id="e3223-132">the width of the bounding box</span></span>
    - <span data-ttu-id="e3223-133">경계 상자의 높이.</span><span class="sxs-lookup"><span data-stu-id="e3223-133">the height of the bounding box,</span></span> 
   
    <span data-ttu-id="e3223-134">이 값을 사용하여 이미지에 있는 모든 텍스트를 둘러싼 상자를 그릴 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-134">You can use these values to draw boxes around every piece of text found in the image.</span></span>

<span data-ttu-id="e3223-135">이 연습에서 볼 수 있듯이 `ocr` 서비스는 이미지의 인쇄 텍스트에 대한 자세한 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e3223-135">As you can see in this exercise, the `ocr` service gives detailed information about the printed text in an image.</span></span> 

<span data-ttu-id="e3223-136">`ocr` 작업에 대한 자세한 내용은 [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e3223-136">For more information about the `ocr` operation, see the [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) reference documentation.</span></span>