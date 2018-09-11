<span data-ttu-id="f1a65-101">이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 이미지에서 필기를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-101">In this unit, you will extract hand writing from an image with the Computer Vision API service that we created previously.</span></span>

# <a name="extracting-the-hand-writing--from-an-image"></a><span data-ttu-id="f1a65-102">이미지에서 필기 추출</span><span class="sxs-lookup"><span data-stu-id="f1a65-102">Extracting the hand writing  from an image</span></span>

<span data-ttu-id="f1a65-103">`az cognitiveservices account keys list` 명령을 실행하여 API에 인증 하는 데 사용되는 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="f1a65-104">해당 명령의 출력은 `key` 변수 내에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="f1a65-105">`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행합니다(이전에 선언한 `key` 변수를 재사용함).</span><span class="sxs-lookup"><span data-stu-id="f1a65-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reusing the previously declared variable `key`.</span></span>

<span data-ttu-id="f1a65-106">필기 인식에 사용할 이미지는 이 메모 게시판의 사진입니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-106">The image we're going to be using for hand writing recognition is a picture of this note board.</span></span>

![필기](../images/handwriting.jpg)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/handwriting.jpg\"}" -D -
```

<span data-ttu-id="f1a65-108">위 명령은 헤더를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-108">The command above will output the headers.</span></span> <span data-ttu-id="f1a65-109">`Operation-Location` 헤더 값을 아래 명령에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-109">Copy the `Operation-Location` header value into the command below.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>"
```

<span data-ttu-id="f1a65-110">그러면 필기 인식 요청 결과가 포함된 JSON 파일이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-110">You will now receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="f1a65-111">위의 샘플에서 사용된 URL을 변경하여 다른 이미지에서 다른 결과를 생성하는 과정을 실험해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="f1a65-111">Experiment with other images to get different result by changing the URL used in the sample above.</span></span>