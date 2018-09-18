<span data-ttu-id="b8767-101">이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 이미지에서 손으로 쓴 글자를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-101">In this unit, you will extract handwriting from an image with the Computer Vision API service that we created previously.</span></span>

# <a name="extracting-the-handwriting-from-an-image"></a><span data-ttu-id="b8767-102">이미지에서 손으로 쓴 글자 추출</span><span class="sxs-lookup"><span data-stu-id="b8767-102">Extracting the handwriting from an image</span></span>

<span data-ttu-id="b8767-103">`az cognitiveservices account keys list` 명령을 실행하여 API에 인증하는 데 사용되는 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="b8767-104">해당 명령의 출력을 `key` 변수 내에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="b8767-105">`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행하고 이전에 선언한 `key` 변수를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reuse the previously declared variable `key`.</span></span>

<span data-ttu-id="b8767-106">손으로 쓴 글자 인식에 사용할 이미지는 이 메모 게시판의 사진입니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-106">The image we're going to be using for handwriting recognition is a picture of this note board.</span></span>

![손으로 쓴 글자](../images/handwriting.jpg)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/handwriting.jpg\"}" -D -
```

<span data-ttu-id="b8767-108">위 명령은 헤더를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-108">The command above will output the headers.</span></span> <span data-ttu-id="b8767-109">`Operation-Location` 헤더 값을 아래 명령에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-109">Copy the `Operation-Location` header value into the command below.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>"
```

<span data-ttu-id="b8767-110">그러면 손으로 쓴 글자 인식 요청 결과가 포함된 JSON 파일이 수신됩니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-110">You will now receive a JSON file containing the result of the handwriting recognition request.</span></span>

<span data-ttu-id="b8767-111">위의 샘플에서 사용된 URL을 변경하여 다른 이미지에서 다른 결과를 얻는 과정을 실험해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="b8767-111">Experiment with other images to get different results by changing the URL used in the sample above.</span></span>