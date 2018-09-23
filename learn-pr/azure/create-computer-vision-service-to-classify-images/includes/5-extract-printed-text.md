현장 배포자가 서버에 게시하는 재고 이미지에서 텍스트를 읽으려고 하는 경우를 가정하겠습니다. 특히, 판매 가격이 표시된 홍보용 스티커를 찾기 위해 제품을 스캔하려고 합니다. Computer Vision API의 OCR(광학 인식) 기능을 사용해 보겠습니다. 

## <a name="calling-the-computer-vision-api-to-extract-printed-text"></a>Computer Vision API를 호출하여 인쇄된 텍스트 추출

`ocr` 작업은 이미지의 텍스트를 감지하고, 인식된 문자를 머신에서 사용 가능한 문자 스트림으로 추출합니다. 요청 URL의 형식은 다음과 같습니다.

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr?language=<...>&detectOrientation=<...>`

평소대로 모든 호출은 계정이 생성된 지역에 대해 이루어져야 합니다. 호출은 두 개의 선택적 매개 변수를 허용합니다.

- **언어**: 이미지에서 감지할 텍스트의 언어 코드입니다. 기본값은 `unk` 또는 알 수 없음입니다. 이렇게 하면 서비스가 이미지에서 텍스트의 언어를 자동으로 감지합니다.
- **detectOrientation**: true인 경우, 서비스는 이미지 방향을 감지하고 이미지 뒤집기 등의 추가 처리를 위해 이미지를 수정합니다. 

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="extract-printed-text-from-an-image-using-ocr"></a>OCR을 사용하여 이미지에서 인쇄 텍스트 추출

OCR(광학 인식)에 사용할 이미지는 *.NET Microservices: Architecture for Containerized .NET Applications*(.NET 마이크로 서비스: 컨테이너화된 .NET 응용 프로그램용 아키텍처)라는 책의 표지입니다.

![ebook .NET 마이크로 서비스: 컨테이너화된 .NET 응용 프로그램을 위한 아키텍처의 표지 사진](../media/5-ebook.png)

1. Cloud Shell에서 다음 명령을 실행합니다. 명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/ocr" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json"  \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/ebook.png'}" \
 | jq '.'
```

다음 JSON은 이 호출에서 받은 응답의 예입니다. 코드 조각이 페이지에 더 잘 맞도록 일부 JSON 행이 제거되었습니다.

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

이 응답을 자세히 살펴보겠습니다. 

- 서비스는 텍스트를 영어로 식별했습니다. `language` 필드의 값에는 이미지에서 감지된 텍스트의 BCP-47 언어 코드가 포함되어 있습니다. 이 예제에서는 **en** 또는 영어입니다. 
- `orientation`은 **위쪽**으로 감지되었습니다. 이 속성은 감지된 텍스트 각도에 따라 이미지가 중심 기준으로 회전한 후 인식된 텍스트의 맨 위가 향하고 있는 방향입니다. 
- `textAngle`은 가로 또는 세로가 되도록 텍스트가 회전해야 하는 각도입니다. 이 예제에서는 텍스트가 완전히 가로이므로 반환된 값은 **0**입니다.  
- `regions` 속성에는 텍스트의 위치, 그림에서의 텍스트 위치 및 이미지의 해당 부분에 있는 단어를 표시하는 데 사용되는 값 목록이 포함되어 있습니다. 
- `boundingBox` 값의 정수 4개는 다음과 같습니다. 
    - 왼쪽 가장자리의 X 좌표 
    - 위쪽 가장자리의 Y 좌표
    - 경계 상자의 폭
    - 경계 상자의 높이. 
   
    이 값을 사용하여 이미지에 있는 모든 텍스트를 둘러싼 상자를 그릴 수 있습니다.

이 연습에서 볼 수 있듯이 `ocr` 서비스는 이미지의 인쇄 텍스트에 대한 자세한 정보를 제공합니다. 

`ocr` 작업에 대한 자세한 내용은 [OCR](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fc) 참조 문서를 참조하세요.