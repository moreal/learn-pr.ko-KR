이 단원에서는 이전 단계에서 만든 Computer Vision API 서비스를 사용하여 이미지를 분석합니다.

# <a name="analyzing-an-image-with-computer-vision-api"></a>Computer Vision API를 사용하여 이미지 분석

`az cognitiveservices account keys list` 명령을 실행하여 API에 인증 하는 데 사용되는 키를 검색합니다. 해당 명령의 출력은 `key` 변수 내에 저장합니다.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행하고 이전에 선언한 `key` 변수를 다시 사용합니다.

서비스로 전송되는 매개 변수는 `visualFeatures`, `details` 및 `languages`입니다. 이러한 매개 변수가 없어도 서비스는 계속 작동하지만, 매개 변수가 있으면 이미지의 콘텐츠에 대한 힌트가 서비스에 제공됩니다. 예를 들어 `details`를 `Landmarks` 또는 `Celebrities`로 설정하면 이정표나 유명인을 쉽게 확인할 수 있습니다. `visualFeatures`를 사용하는 경우에는 서비스가 반환할 정보의 종류를 식별할 수 있습니다. `Categories` 옵션은 나무, 건물 등과 같은 이미지 콘텐츠를 분류합니다. `Faces`는 사람의 얼굴을 식별하여 성별과 나이를 제공합니다.

자세한 내용은 [설명서](https://westus.dev.cognitive.microsoft.com/docs/services/56f91f2d778daf23d8ec6739/operations/56f91f2e778daf14a499e1fa)를 참조하세요.

일단은 이정표를 식별하고 서비스가 `Categories` 및 `Description`을 반환하도록 설정해 보겠습니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Categories,Description&details=Landmarks" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}"
```

요청 결과는 `url`에서 그림을 설명하는 원시 JSON입니다. 끝에 ` | jq '.'`를 추가하여 JSON 출력을 말끔하게 표시할 수도 있습니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/analyze?visualFeatures=Categories,Description&details=Landmarks&language=en" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" | jq '.'
```

온라인에서 찾은 다른 이미지 링크를 복사하여 위 명령의 URL을 바꾸는 방법으로 서비스에서 이미지를 분석해 보세요.