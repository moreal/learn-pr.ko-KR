<span data-ttu-id="05b66-101">마지막 연습에서 Custom Vision Service 포털의 **빠른 테스트** 기능을 사용하여 학습된 모델을 테스트하였습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-101">In the last exercise, we tested our trained model using the **Quick Test** feature of the Custom Vision Service portal.</span></span> <span data-ttu-id="05b66-102">이 방법은 몇 가지 테스트 이미지를 사용하여 모델의 정확도를 신속하게 확인할 수 있는 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-102">This is a great way to quickly check the accuracy of the model with some test images.</span></span> <span data-ttu-id="05b66-103">조금 더 진도를 나가 HTTP를 통한 모델의 예측 엔드포인트를 호출해보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-103">Let's go a little further and make calls to the prediction endpoint of our model over HTTP.</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

1. <span data-ttu-id="05b66-104">Custom Vision Service 포털에서 *아트워크*\* 프로젝트로 돌아가서 **성능** 탭을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-104">Returning to your *Artworks*\* project in the Custom Vision Service portal, select the  **Performance** tab.</span></span>

    ![성능 탭 선택](../media/5-performance-tab.png)

1. <span data-ttu-id="05b66-106">**기본값으로 설정**을 선택하여 모델의 최신 반복이 기본 반복인지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-106">Select **Make default** to make sure the latest iteration of the model is the default iteration.</span></span>

1. <span data-ttu-id="05b66-107">**예측 URL**을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-107">Select **Prediction URL**.</span></span> <span data-ttu-id="05b66-108">그러면 호출하는 데 필요한 정보의 대화 상자가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-108">This displays a dialog of the information we need to make our calls.</span></span> 

    ![예측 URL 정보 보기](../media/5-portal-prediction-url.png)

    <span data-ttu-id="05b66-110">대화 상자에 표시된 것처럼 예측 엔드포인트를 호출하고 이미지 URL을 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-110">As the dialog shows, we can call the prediction endpoint and pass it an image URL.</span></span> <span data-ttu-id="05b66-111">또한 원시 이미지를 요청 본문의 엔드포인트로 전달할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-111">We can also pass a raw image to the endpoint in the body of the request.</span></span>

    <span data-ttu-id="05b66-112">이 대화 상자에서 세 가지 정보를 기록해둡니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-112">Take note of three pieces of information from this dialog.</span></span>
     - <span data-ttu-id="05b66-113">**예측-키**: 이 키는 모든 요청에서 헤더로 설정돼야 합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-113">**Prediction-Key**: This key has to be set as a header in all requests.</span></span> <span data-ttu-id="05b66-114">그렇게 해서 엔드포인트에 대한 액세스 권한을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-114">That's what gives us access to the endpoint.</span></span>
    - <span data-ttu-id="05b66-115">**요청 URL**: 대화 상자에 두 가지 다른 URL이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-115">**Request URL**: The dialog shows two different URLs.</span></span> <span data-ttu-id="05b66-116">이미지 URL을 게시하는 경우 `/url`에서 종료되는 첫 번째 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-116">If we're posting an image URL, then use the first URL, which ends in `/url`.</span></span> <span data-ttu-id="05b66-117">요청 본문의 원시 이미지를 게시하려는 경우 `/image`에서 종료되는 두 번째 URL을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-117">If we want to post a raw image in the body of our request, we use the second URL, which ends in `/image`.</span></span>
    - <span data-ttu-id="05b66-118">**콘텐츠-형식**: 원시 이미지를 게시하는 경우 요청 본문을 `application/octet-stream`에 대한 콘텐츠 형식과 이미지의 이진 표현으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-118">**Content-Type**: If we're posting a raw image, we set the body of the request to the binary representation of the image and the content type to `application/octet-stream`.</span></span> <span data-ttu-id="05b66-119">이미지 URL을 게시하는 경우 본문에 JSON으로 삽입하고 콘텐츠 유형을 `application/json`으로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-119">If we're posting an image URL, we put that as JSON in the body and set the content type to `application/json`.</span></span>
    

3. <span data-ttu-id="05b66-120">**예측 API 사용 방법** 대화 상자에서 첫 번째 URL 및 `Prediction-Key` 값을 복사하고 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-120">Copy and save the first URL and the `Prediction-Key` value from the **How to use the Prediction API** dialog.</span></span> 

> [!TIP]
> <span data-ttu-id="05b66-121">**cURL**은 파일을 보내거나 받는 데 사용할 수 있는 명령줄 도구입니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-121">**cURL** is a command line tool that can be used to send or receive files.</span></span> <span data-ttu-id="05b66-122">Linux, macOS 및 Windows 10에 포함되어 있으며 대부분의 다른 운영 체제에 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-122">It's included with Linux, macOS, and Windows 10, and can be downloaded for most other operating systems.</span></span> <span data-ttu-id="05b66-123">cURL은 HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3 등과 같은 많은 프로토콜을 지원합니다. 자세한 내용은 아래 링크를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="05b66-123">cURL supports numerous protocols like HTTP, HTTPS, FTP, FTPS, SFTP, LDAP, TELNET, SMTP, POP3, etc. For more information, refer to the links below:</span></span>
>
>- <https://en.wikipedia.org/wiki/CURL>
>- <https://curl.haxx.se/docs/> 
> 
> <span data-ttu-id="05b66-124">cURL은 샌드박스의 Azure Cloud Shell에 이미 설치되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-124">cURL is already installed in the Azure Cloud Shell in the sandbox.</span></span> <span data-ttu-id="05b66-125">따라서 이 연습에서는 해당 엔드포인트에 대해 HTTP를 호출하기 위해 cURL을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-125">So, we'll cURL in this exercise to make HTTP calls to our endpoint.</span></span>

2. <span data-ttu-id="05b66-126">Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-126">Execute the following command in the Cloud Shell.</span></span> <span data-ttu-id="05b66-127">**[엔드포인트-URL]** 을 마지막 단계에서 저장한 URL로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-127">Replace **[endpoint-URL]** with the URL you saved from the last step.</span></span> <span data-ttu-id="05b66-128">**[예측-키]** 를 마지막 단계에서 저장한 `Prediction-Key`의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-128">Replace **[Prediction-Key]** with the value of `Prediction-Key` you saved from the last step.</span></span> 

    ```azurecli
    curl [endpoint-URL] \
    -H "Prediction-Key: [Prediction-Key]" \
    -H "Content-Type: application/json" \
    -d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/VanGoghTest_02.jpg'}" \
    | jq '.'
    ```

    <span data-ttu-id="05b66-129">명령이 완료되면 다음 스크린샷과 유사한 JSON 응답이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-129">When the command completes, you'll see a JSON response similar to the following screenshot.</span></span> <span data-ttu-id="05b66-130">API는 모델의 모든 태그에 대한 확률을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-130">The API returns a probability for every tag in the model.</span></span> <span data-ttu-id="05b66-131">알 수 있듯이 `"painting"` **tagName** 값에 대해 1에 가까운 확률로 이 이미지는 명백하게 그림입니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-131">As you can see, with a probability close to 1 for the `"painting"` **tagName** value, this image is definitely a painting.</span></span> <span data-ttu-id="05b66-132">그러나 해당 모델을 학습한 아티스트가 그린 그림은 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-132">However, it's not a painting by any of the artists with which we trained our model.</span></span> 

    ![피카소 테스트 이미지 썸네일](../media/5-prediction-json.png) 

3. <span data-ttu-id="05b66-134">위의 요청 본문의 URL을 다음 표의 URL로 바꿔 더 자주 예측을 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-134">Try more predictions by replacing the URL in the request body above, with the URLs in the following table.</span></span> 

    |<span data-ttu-id="05b66-135">이미지</span><span class="sxs-lookup"><span data-stu-id="05b66-135">Image</span></span>  | <span data-ttu-id="05b66-136">URL</span><span class="sxs-lookup"><span data-stu-id="05b66-136">URL</span></span>  |
    |---------|---------|
    |![피카소 테스트 이미지 썸네일](../media/picasso-test-02-thumb.jpg)     | `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PicassoTest_02.jpg`        |
    |![렘브란트 테스트 이미지 썸네일](../media/rembrandt-test-01-thumb.jpg)     |  `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/RembrandtTest_01.jpg`       |
    |![폴록 테스트 이미지 썸네일](../media/pollock-test-01-thumb.jpg)  |   `https://raw.githubusercontent.com/MicrosoftDocs/mslearn-classify-images-with-the-custom-vision-service/master/test-images/PollockTest_01.jpg`     |
   

<span data-ttu-id="05b66-140">해당 예측 엔드포인트가 예상대로 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-140">Our prediction endpoint is working as expected.</span></span> <span data-ttu-id="05b66-141">API를 호출하는 것은 예측-키 및 이미지 URL을 사용하여 엔드포인트에 대해 HTTP 요청을 하는 것만큼 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="05b66-141">Calling the API is as simple as making a HTTP request to the endpoint with a Prediction-Key and an image URL.</span></span>