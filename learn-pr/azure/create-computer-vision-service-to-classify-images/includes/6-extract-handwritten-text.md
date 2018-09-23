Computer Vision API가 이미지에서 인쇄된 텍스트를 추출하는 방법을 살펴보았습니다. 이 연습에서는 서비스를 사용하여 필기 텍스트를 감지하는 방법을 알아보겠습니다.

## <a name="calling-the-computer-vision-api-to-extract-handwritten-text"></a>Computer Vision API를 호출하여 필기 텍스트 추출

`recognizeText` 작업을 통해 메모, 문자, 에세이, 화이트보드, 양식 및 기타 소스에서 필기 텍스트를 감지하고 추출할 수 있습니다. 요청 URL의 형식은 다음과 같습니다.

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=<...>`

모든 호출은 계정이 생성된 지역에 대해 이루어져야 합니다.

`mode` 매개 변수가 있는 경우 이 매개 변수는 `Handwritten` 또는 `Printed`로 설정되어야 하며 대/소문자를 구분합니다. 매개 변수가 `Handwritten`으로 설정되거나 지정되지 않은 경우에는 필기 인식이 이루어집니다. 매개 변수가 `Printed`로 설정된 경우에는 인쇄 텍스트 인식이 이루어집니다. 이 호출에서 결과를 가져오는 데 걸리는 시간은 이미지의 쓰기 양에 따라 다릅니다.

이 예제에서는 다음을 수행합니다.

- cUrl의 `-D` 옵션을 사용하여 응답 헤더를 콘솔에 인쇄
- 응답에서 수신한 헤더에서 `Operation-Location` 헤더 값 복사
- 몇 초 후, 결과에 대해 `Operation-Location`에서 지정한 URL 확인

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="detect-and-extract-handwritten-text-from-an-image"></a>이미지에서 필기 텍스트 검색 및 추출

이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.

![노트에 필기 샘플이 있는 사진](../media/6-handwriting.jpg)

1. Azure Cloud Shell에서 다음 명령을 실행합니다. 명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/recognizeText?mode=Handwritten" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/handwriting.jpg'}" \
-D - 
```

위에서는 이 작업의 헤더를 콘솔로 덤프합니다. 예를 들면 다음과 같습니다.

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

`Operation-Location` 헤더는 완료 후에 결과가 게시되는 위치입니다.

2. `Operation-Location` 헤더 값을 복사합니다.
1. Azure Cloud Shell에서 `"<Operation-Location>"`을 이전 단계에서 복사한 **Operation-Location** 헤더의 값으로 바꾸는 다음 명령을 실행합니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" "<Operation-Location>" | jq '.'
```

작업이 완료되면 필기 인식 요청의 결과를 포함하는 JSON 파일이 수신됩니다.

`recognizeText` 작업에 대한 자세한 내용은 [필기 텍스트 인식](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/587f2c6a154055056008f200) 참조 문서를 참조하세요.