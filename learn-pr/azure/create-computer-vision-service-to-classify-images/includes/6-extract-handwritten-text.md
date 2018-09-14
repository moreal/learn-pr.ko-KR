Computer Vision API 이미지에서 인쇄 된 텍스트를 추출할 수 있습니다 하는 방법에 대해 살펴보았습니다. 이 연습에서는 필기 한 텍스트를 검색할 서비스를 사용 하겠습니다.

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a>필기 한 텍스트를 추출 하려면 Computer Vision API를 호출 합니다.

`recognizeText` 작업을 검색 하 고 정보, 문자, 세이, 화이트 보드, 양식 및 기타 원본에서 필기 한 텍스트를 추출 합니다. 요청 URL의 형식은:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/recognizeText[?mode] `

늘 그렇듯이 계정이 만들어진 위치에 대 한 모든 호출 수 있어야 합니다. 경우는 `mode` ust에서는 매개 변수 설정할 `Handwritten` 또는 `Printed` 및 대/소문자 구분 합니다. 매개 변수 설정 된 경우 `Handwritten` 이거나 지정 하지 않으면 필기 인식을 수행 됩니다. 그렇지 않은 경우 매개 변수를 설정한 `Printed` 인쇄 된 텍스트 인식 OCR 작업을 호출 하 여 수행 됩니다.

이 호출에서 결과 산출 하는 데 걸리는 시간 필기 이미지에서의 양에 따라 달라 집니다. 따라서 몇 초 동안 대기 해야 합니다. 따라서이 예제에서는 합니다.

- CUrl의를 사용 하 여 콘솔 응답 헤더를 덤프 `-D` 옵션
- 복사를 `Operation-Location` 응답에서 수신 하는 헤더에서 헤더 값
- 몇 초 후 확인 하 여 지정 된 URL을 `Operation-Location` 결과 얻으려면

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a>이미지에서 필기된 텍스트 검색 및 추출

이 예제에서는 다음 이미지 사용 하지만 다른 이미지에 Url 사용 하 여 동일한 명령을 시도 하도록 합니다.

![필기 샘플 그림](../media/6-handwriting.jpg)

1. Azure Cloud Shell에서 다음 명령을 실행 합니다.

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

위의 콘솔에이 작업의 헤더를 덤프합니다. 예를 들면 다음과 같습니다.

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

`Operation-Location` 헤더는 결과 완료 되 면 게시 됩니다.

2. 복사를 `Operation-Location` 헤더 값입니다.
1. 대체 하는 Azure Cloud Shell에서 다음 명령을 실행 `"<Operation-Location>"` 값으로는 **작업 위치** 이전 단계에서 복사한 헤더입니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

작업이 완료 되 면 필기 인식 요청의 결과 포함 하는 JSON 파일을 받을 수 있습니다.

에 대 한 자세한 내용은 합니다 `recognizeText` 작업 참조를 [필기 한 텍스트 인식](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) 설명서를 참조 합니다.