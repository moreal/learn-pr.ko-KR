이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 이미지에서 필기를 추출합니다.

# <a name="extracting-the-handwriting-from-an-image"></a>이미지에서 필기 추출

`az cognitiveservices account keys list` 명령을 실행하여 API에 대해 인증하는 데 사용되는 키를 검색합니다. 해당 명령의 출력은 `key` 변수 내에 저장합니다.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행하고 이전에 선언한 `key` 변수를 다시 사용합니다.

필기 인식에 사용할 이미지는 이 메모 게시판의 사진입니다.

![필기](../images/handwriting.jpg)

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/recognizeText?handwriting=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/handwriting.jpg\"}" -D -
```

위 명령은 헤더를 출력합니다. `Operation-Location` 헤더 값을 아래 명령에 복사합니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>"
```

이제 필기 인식 요청 결과가 포함된 JSON 파일이 수신됩니다.

위의 샘플에서 사용된 URL을 변경하여 다른 이미지에서 다른 결과를 생성하는 과정을 실험해 봅니다.