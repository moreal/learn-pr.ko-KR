<span data-ttu-id="ce8b0-101">제품의 현장 배포자는 반납하는 매장 선반의 이미지를 스캔하여 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-101">Frontline distributors of your products scan and upload images of store shelves they're restocking.</span></span> <span data-ttu-id="ce8b0-102">회사의 대표 개발자는 이미지의 썸네일을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-102">As a lead developer at your company, you are responsible for creating thumbnails of the images.</span></span> <span data-ttu-id="ce8b0-103">썸네일은 영업 팀을 위해 작성한 온라인 보고서에 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-103">The thumbnails are used in the online reports you create for the sales team.</span></span> <span data-ttu-id="ce8b0-104">최근에 영업 관리자가 보고서의 이미지가 흐릿하고 대개 제품 전면과 가운데 부분이 없다고 말했기 때문에 큰 보고서를 스캔하기 어렵습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-104">Recently, the sales manager said that the images in the report are blurry and often don't have the product front and center, making it difficult to scan the large report.</span></span> <span data-ttu-id="ce8b0-105">상황을 개선하는 것은 사용자에게 달려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-105">It's up to you to improve the situation.</span></span>

<span data-ttu-id="ce8b0-106">Computer Vision API의 썸네일 생성 기능을 사용해 보기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-106">You decide to try the thumbnail generation feature of the Computer Vision API.</span></span> <span data-ttu-id="ce8b0-107">이는 크기 조정 기능보다 더 나을 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-107">Perhaps it can do a better job than the resizing function you wrote.</span></span>

<span data-ttu-id="ce8b0-108">Computer Vision은 먼저 고품질 썸네일을 생성한 다음, 이미지 내의 개체를 분석하여 ROI(관심 영역)를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-108">Computer Vision first generates a high-quality thumbnail and then analyzes the objects within the image to determine the region of interest (ROI).</span></span> <span data-ttu-id="ce8b0-109">그런 다음, Computer Vision은 ROI의 요구 사항에 맞게 이미지를 자릅니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-109">Computer Vision then crops the image to fit the requirements of the region of interest.</span></span> <span data-ttu-id="ce8b0-110">생성된 썸네일은 필요에 따라 원래 이미지의 가로 세로 비율과 다른 가로 세로 비율을 사용하여 표시할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-110">The generated thumbnail can be presented using an aspect ratio that is different from the aspect ratio of the original image, depending on your needs.</span></span> <span data-ttu-id="ce8b0-111">작동을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-111">Let's see it in action.</span></span>

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a><span data-ttu-id="ce8b0-112">Computer Vision API를 호출하여 썸네일 생성</span><span class="sxs-lookup"><span data-stu-id="ce8b0-112">Calling the Computer Vision API to generate a thumbnail</span></span>

<span data-ttu-id="ce8b0-113">`generateThumbnail` 작업은 사용자 지정 폭 및 높이의 썸네일 이미지를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-113">The `generateThumbnail` operation creates a thumbnail image with the user-specified width and height.</span></span> <span data-ttu-id="ce8b0-114">기본적으로 서비스는 이미지를 분석하고 ROI(관심 영역)를 식별하며 ROI를 기반으로 스마트 자르기 좌표를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-114">By default, the service analyzes the image, identifies the region of interest (ROI), and generates smart cropping coordinates based on the ROI.</span></span> <span data-ttu-id="ce8b0-115">스마트 자르기는 입력 이미지의 가로 세로 비율과 다른 가로 세로 비율을 지정할 때 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-115">Smart cropping helps when you specify an aspect ratio that differs from aspect ratio of the input image.</span></span> <span data-ttu-id="ce8b0-116">요청 URL의 형식은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-116">The request URL has the following format:</span></span>

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=<...>&height=<...>&smartCropping=<...>`

<span data-ttu-id="ce8b0-117">API에 각기 다른 매개 변수를 제공하여 필요에 따라 적합한 썸네일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-117">Different parameters can be provided to the API to generate the proper thumbnail for your needs.</span></span> <span data-ttu-id="ce8b0-118">`width` 및 `height` 매개 변수는 필수 항목입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-118">The `width` and `height` parameters are required.</span></span> <span data-ttu-id="ce8b0-119">이들 매개 변수는 특정 이미지에 필요한 크기를 API에 알려 줍니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-119">They tell the API which size you need for a specific image.</span></span> <span data-ttu-id="ce8b0-120">`smartCropping` 매개 변수는 썸네일 내에 보관하기 위해 이미지에서 관심 영역을 분석하여 더 스마트한 자르기를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-120">The `smartCropping` parameter generates smarter cropping by analyzing the region of interest in your image to keep it within the thumbnail.</span></span> <span data-ttu-id="ce8b0-121">예를 들어 스마트 자르기를 사용하도록 설정한 상태에서 프로필 사진을 자르면 사진의 가로 세로 비율이 다르더라도 사진 프레임 내에 사람의 얼굴이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-121">As an example, with smart cropping enabled, a cropped profile picture would keep someone's face within the picture frame even when the picture has a different aspect ratio.</span></span>

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a><span data-ttu-id="ce8b0-122">썸네일 생성</span><span class="sxs-lookup"><span data-stu-id="ce8b0-122">Generate a thumbnail</span></span>

<span data-ttu-id="ce8b0-123">이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-123">We'll use the following image in this example, but you're free to try the same command with URLs to other images.</span></span>

![풀밭에 앉아 있는 귀여운 흰 강아지의 사진.](../media/4-dog.png)

1. <span data-ttu-id="ce8b0-125">Azure Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-125">Execute the following commands in Azure Cloud Shell.</span></span> <span data-ttu-id="ce8b0-126">명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-126">Replace `<region>` in the command with the region of your cognitive services account</span></span>

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

<span data-ttu-id="ce8b0-127">이 예제에서는 100x100 크기의 썸네일을 만들도록 서비스에 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-127">In this example, we ask the service to create a thumbnail that is 100x100.</span></span> <span data-ttu-id="ce8b0-128">스마트 자르기가 사용 설정되었습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-128">Smart cropping is enabled.</span></span> <span data-ttu-id="ce8b0-129">성공적인 응답에는 thumbnail.jpg라는 파일에 쓰는 이진 썸네일 이미지가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-129">A successful response contains the thumbnail image binary, which we write to a file called thumbnail.jpg.</span></span>

> [!CAUTION]
> <span data-ttu-id="ce8b0-130">`-o` 매개 변수는 출력을 파일로 재전송합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-130">The `-o` parameter redirects the output to a file.</span></span> <span data-ttu-id="ce8b0-131">파일은 항상 덮어쓰여지므로 이 명령을 시도하는 동안 둘 이상의 썸네일을 유지하려는 경우에는 파일 이름을 변경하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-131">The file is always overwritten, so if you want to keep around  more than one thumbnail while trying this command, change the file name.</span></span>

## <a name="view-the-generated-thumbnail"></a><span data-ttu-id="ce8b0-132">생성된 썸네일 보기</span><span class="sxs-lookup"><span data-stu-id="ce8b0-132">View the generated thumbnail</span></span>

<span data-ttu-id="ce8b0-133">생성된 썸네일은 Azure Cloud Shell 저장소 계정에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-133">The generated thumbnail will be found in your Azure Cloud Shell storage account.</span></span> <span data-ttu-id="ce8b0-134">파일 이름을 **thumbnail.jpg**로 지정했습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-134">We named the file **thumbnail.jpg**.</span></span>

<span data-ttu-id="ce8b0-135">Microsoft Learn의 Cloud Shell에는 파일을 다운로드하는 기능이 없지만 다음 지침에 따라 Azure Portal을 통해 썸네일을 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-135">The Cloud Shell in Microsoft Learn doesn't have the ability to download files, but you can follow these instructions to download the thumbnail through the Azure portal.</span></span>

1. <span data-ttu-id="ce8b0-136">Azure Cloud Shell에서 다음 명령을 실행하여 **thumbnail.jpg** 파일이 홈 폴더에 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-136">Execute the following commands in Azure Cloud Shell to confirm that the file **thumbnail.jpg** exists in your home folder.</span></span>

    ```azurecli
    cd ~
    ls -l
    ```



1. <span data-ttu-id="ce8b0-137">다음 명령을 실행하여 `thumbnail.jpg`를 clouddrive 폴더로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-137">Execute the following command to move `thumbnail.jpg` into the clouddrive folder.</span></span>

    ```azurecli
    mv ~/thumbnail.jpg ~/clouddrive
    ```
1. <span data-ttu-id="ce8b0-138">샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-138">Sign into the [Azure portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true) using the same account you activated the sandbox with.</span></span>
1. <span data-ttu-id="ce8b0-139">포털 대시보드의 **모든 리소스** 패널에서 이름이 `cloudshell`로 시작되는 저장소 계정을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-139">In the **All resources** panel of the portal dashboard, select the storage account with name beginning with `cloudshell`.</span></span>
1. <span data-ttu-id="ce8b0-140">저장소 계정 창에서 **Storage 탐색기**를 선택한 다음, **파일 공유**를 선택하고 해당 컬렉션에서 이름이 \*\*cloudshellfiles\*\*\*로 시작되는 파일 공유를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-140">In the Storage account panel, select **Storage Explorer**, then **FILE SHARES** and then the file share in that collection with the name beginning with \*\*cloudshellfiles\*\*\*.</span></span>
1. <span data-ttu-id="ce8b0-141">*thunbnail.jpg* 파일을 선택한 다음, 맨 위 메뉴에서 **다운로드**를 선택하여 이미지를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-141">Select the *thunbnail.jpg* file and then **Download** from the top menu to see the image.</span></span>

<span data-ttu-id="ce8b0-142">`generateThumbnail` 작업은 썸네일에서 이미지의 ROI(관심 영역)를 유지할 수 있는 강력한 썸네일 생성기입니다.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-142">The `generateThumbnail` operation is a powerful thumbnail generator that is capable of keeping the Region Of Interest (ROI) of an image in the thumbnail.</span></span>

<span data-ttu-id="ce8b0-143">`generateThumbnails` 작업에 대한 자세한 내용은 [썸네일 가져오기](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) 참조 문서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ce8b0-143">For more information about the `generateThumbnails` operation, see the [Get Thumbnail](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) reference documentation.</span></span>