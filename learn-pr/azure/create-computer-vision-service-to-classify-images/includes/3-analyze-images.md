Contoso Beverage 배포에서 수석 개발자 건물에 대 한 책임을 유지 관리 메일용 유통업 있도록 기간 업무 앱을 검색 하 고 저장소 선반 재입고 되는 위치의 이미지를 업로드. 

사용자가 게시 하는 모든 이미지에서 회사 콘텐츠 규칙을 준수 하는지 유효성을 검사 해야 합니다. 회사는 회사 사이트에 게시 된 부적절 한 콘텐츠를 원하지 않습니다. Computer Vision API를 사용 하 여 앱에서 하기로 인공 지능에 개선 사항을 지정 합니다. 

시작 하려면 Azure 구독에 Computer Vision 계정을 만들 하 고이 테스트를 시작 합니다 **분석** 기능입니다.

## <a name="calling-the-computer-vision-api-to-analyze-images"></a>이미지를 분석 하려면 Computer Vision API를 호출 합니다.

`analyze` 작업 다양 한 이미지 콘텐츠를 기반으로 하는 시각적 기능을 추출 합니다.  요청 URL의 형식은:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/analyze[?visualFeatures][&details][&language] `

서비스로 전송되는 매개 변수는 `visualFeatures`, `details` 및 `languages`입니다. 설정 된 `details` 매개 변수를 `Landmarks` 또는 `Celebrities` 랜드마크 또는 유명인 200,000 명을 식별할 수 있도록 합니다. `visualFeatures`를 사용하는 경우에는 서비스에서 반환하도록 할 정보의 종류를 식별할 수 있습니다. `Categories` 옵션 트리, 건물, 등과 같은 이미지의 콘텐츠를 분류 합니다. `Faces`는 사람의 얼굴을 식별하여 성별과 나이를 제공합니다.

Computer Vision API에 대 한 모든 작업을 처리 하도록 요청 하면 이미지에 연결할 때 다음과 같은 제한이:

- 지원되는 이미지 형식: JPEG, PNG, GIF, BMP 
- 이미지 파일 크기는 4MB 미만 이어야 합니다.
- 이미지 크기는 50 x 50 이상 이어야 합니다.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a>이미지에서 랜드마크를 식별 합니다.

이미지에서 랜드마크 찾기에 대 한 호출을 사용 하 여 시작 해 보겠습니다. 예를 들어 다음 이미지 사용 하지만 다른 이미지에 Url 사용 하 여 동일한 명령을 시도 하도록 합니다. 

![Snow-capped 산 위의 파란색 하늘이 mountain 범위의 사진입니다.](../media/3-mountains.jpg)

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

<!-- TODO Replace image URL with one that points to an image in the sample repo -->
```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

이미지 URL에 의해 지정 된 이미지의 랜드마크가이 호출을 찾습니다. 또한 호출 범주 정보 및 이미지의 설명을 반환 하는 서비스를 요청 합니다. 설명은 영어 되거나 전체 문장으로 반환 됩니다. 여러분도 알다시피 API 호출할 때마다 선택키가 필요 합니다. 모든 호출에서 설정 된 `Ocp-Apim-Subscription-Key` 헤더입니다. 

> [!TIP]
> 요청 결과는 `url`에서 그림을 설명하는 원시 JSON입니다. 추가한 ` | jq '.'` JSON을 꾸밀 명령의 끝에 출력 합니다.

이 예제 JSON 응답을 반환 합니다.

- `categories` 0-1 얼마나 자신 서비스가 이미지 지정한 범주에 속해 있는지의 점수와 함께 검색 된 모든 이미지 범주를 나열 하는 배열입니다.
- `description` 태그 또는 이미지와 관련 된 단어의 배열을 포함 하는 항목입니다.
- `captions` 이미지에는 무엇이 영어 설명 하는 텍스트 필드를 사용 하 여 입력 합니다. 텍스트의 확신도 점수를 확인 합니다. 이 점수는이 분석을 사용 하 여 다음 작업을 결정할 수 있습니다.


## <a name="check-for-inappropriate-content-in-an-image"></a>이미지에서 부적절 한 콘텐츠로부터 확인

이 예제에서는 성인 콘텐츠에 대 한 이미지를 분석 합니다. 신뢰성 점수는 이미지 성인 / 외설 콘텐츠를 포함 하는 가능성을 평가 합니다. 

예를 들어 다음 이미지 사용 하지만 다른 이미지에 Url 사용 하 여 동일한 명령을 시도 하도록 합니다. 

![웃는 제품군의 사진입니다.](../media/3-people.png)

1. Azure Cloud Shell에서 다음 명령을 실행합니다.

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

이 예에서는 설정 합니다 `visualFeatures` 에 `Adult,Description`입니다. 응답을 보면 두 외설 콘텐츠에 대 한 한 성인 콘텐츠에 대 한 신뢰성 점수입니다. 이러한 점수와 이미지 설명 및 기타 시각적 기능 사용 플래그를 서버에 게시 하는 이미지를 시작할 수 있습니다.

이 연습에서 노력 예제 알 수 있습니다 사용 하 여 수행할 수 있는 분석 형식의 `analyze` 작업 합니다. 다양 한 조합을 visualFeatures, 정보 및 언어 매개 변수를 시도 다양 한 이미지를 사용 하 여 분석을 사용해 보십시오.

에 대 한 자세한 내용은 합니다 `analyze` 작업 참조를 [이미지 분석](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) 설명서를 참조 합니다.