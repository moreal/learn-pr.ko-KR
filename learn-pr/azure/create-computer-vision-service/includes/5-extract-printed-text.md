<span data-ttu-id="34c21-101">이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 이미지에서 텍스트를 추출합니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-101">In this unit, you will extract text from an image with the Computer Vision API service that we created previously.</span></span>

# <a name="extracting-the-text-from-an-image"></a><span data-ttu-id="34c21-102">이미지에서 텍스트 추출</span><span class="sxs-lookup"><span data-stu-id="34c21-102">Extracting the text from an image</span></span>

<span data-ttu-id="34c21-103">`az cognitiveservices account keys list` 명령을 실행하여 API에 인증 하는 데 사용되는 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="34c21-104">해당 명령의 출력은 `key` 변수 내에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="34c21-105">`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행합니다(이전에 선언한 `key` 변수를 재사용함).</span><span class="sxs-lookup"><span data-stu-id="34c21-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reusing the previously declared variable `key`.</span></span>

<span data-ttu-id="34c21-106">OCR(광학 인식)에 사용할 이미지는 [.NET Microservices: Architecture for Containerized .NET Applications(.NET 마이크로 서비스: 컨테이너화된 .NET 응용 프로그램용 아키텍처)](/dotnet/standard/microservices-architecture/)이라는 책의 표지입니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-106">The image we're going to be using for Optical Character Recognition (OCR) is the cover from the book [.NET Microservices: Architecture for Containerized .NET Applications](/dotnet/standard/microservices-architecture/).</span></span>

![전자책 표지](../images/ebook.png)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/ocr" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/ebook.png\"}" | jq '.'
```

<span data-ttu-id="34c21-108">처음 세 속성은 언어, 방향, 텍스트 각도입니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-108">The first three properties are the language, orientation as well as the text angle.</span></span> <span data-ttu-id="34c21-109">그리고 `regions` 속성에는 텍스트 위치(그림 내의 텍스트 위치 및 그림에 포함된 실제 단어)를 표시하는 데 사용되는 값 목록이 포함됩니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-109">Then, the `regions` properties will contain a list of values used to show where the text is, it's position in the picture and the actual words it contains.</span></span>

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

<span data-ttu-id="34c21-110">위의 샘플에서 사용된 URL을 변경하여 다른 이미지에서 다른 결과를 생성하는 과정을 실험해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="34c21-110">Experiment with other images to get different result by changing the URL used in the sample above.</span></span>