현장 유통업자가 재고를 보충하는 매장 선반의 이미지를 스캔하여 업로드할 수 있는 사업 부문 앱을 빌드하고 유지 관리해야 하는 Contoso Beverage Distribution의 개발 책임자를 예로 들어보겠습니다. 

사용자가 게시하는 모든 이미지가 회사에서 설정한 콘텐츠 규칙을 준수하는지 유효성을 검사하고자 합니다. 회사는 회사 사이트에 부적절한 콘텐츠가 게시되기를 원치 않습니다. 인공 지능의 개선 사항을 기반으로 앱에서 Computer Vision API를 사용하기로 했습니다. 

먼저 Azure 구독에서 Computer Vision 계정을 만들고 **분석** 기능 테스트를 시작합니다.

## <a name="calling-the-computer-vision-api-to-analyze-images"></a>Computer Vision API를 호출하여 이미지 분석

`analyze` 작업은 이미지 콘텐츠를 기준으로 다양한 시각적 기능 집합을 추출합니다. 요청 URL의 형식은 다음과 같습니다.

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=<...>&details=<...>&language=<...>`

서비스로 전송되는 매개 변수는 `visualFeatures`, `details` 및 `languages`입니다. `details` 매개 변수를 `Landmarks` 또는 `Celebrities`로 설정하면 랜드마크나 유명인을 쉽게 확인할 수 있습니다. `visualFeatures`를 사용하는 경우에는 서비스가 반환할 정보의 종류를 식별할 수 있습니다. `Categories` 옵션은 나무, 건물 등과 같은 이미지 콘텐츠를 분류합니다. `Faces`는 사람의 얼굴을 식별하여 성별과 나이를 제공합니다.

Computer Vision API의 모든 작업에서는 처리하는 이미지에 다음 제한 사항이 있습니다.

- 지원되는 이미지 형식: JPEG, PNG, GIF, BMP 
- 이미지 파일 크기는 4MB 미만이어야 합니다.
- 이미지 크기는 최소 50 x 50이어야 합니다.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="identify-landmarks-in-an-image"></a>이미지에서 랜드마크 식별하기

이미지에서 랜드마크를 찾기 위해 호출로 시작해 보겠습니다. 이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다. 

![눈 덮인 산 위에 파란 하늘이 펼쳐진 산맥 그림.](../media/3-mountains.jpg)

Azure Cloud Shell에서 다음 명령을 실행합니다. 명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Categories,Description&details=Landmarks" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/mountains.jpg'}" \
| jq '.'
```

- 이 호출은 이미지 URL에 의해 지정된 이미지에서 랜드마크를 찾습니다. 분석 중인 이미지는 이 예제에 대한 GitHub 리포지토리에 저장됩니다. 
- 또한 호출은 서비스가 범주 정보 및 이미지 설명을 반환할 것을 요청합니다. 설명은 완전한 영어 문장으로 반환됩니다. 
- API에 대한 모든 호출에는 액세스 키가 필요합니다. 이것은 요청의 `Ocp-Apim-Subscription-Key` 헤더에 설정됩니다. 

> [!TIP]
> 요청 결과는 `url`에서 그림을 설명하는 원시 JSON입니다. 명령의 끝에 ` | jq '.'`를 추가하여 JSON 출력을 말끔하게 표시했습니다.

이 호출의 JSON 응답은 다음을 반환합니다.

- 이미지가 지정된 범주에 속한다는 사실을 서비스가 얼마나 확신하는지 나타내는 0에서 1 사이의 점수와 함께, 감지된 모든 이미지 범주를 나열하는 `categories` 배열.
- 이미지와 관련된 태그 또는 단어의 배열을 포함하는 `description` 항목.
- 이미지에 포함된 항목을 영어로 설명하는 텍스트 필드가 있는 `captions` 항목. 텍스트에도 확실성 점수가 있는지 관찰합니다. 이 점수는 이 분석과 함께 다음에 수행할 작업을 결정하는 데 도움이 될 수 있습니다.


## <a name="check-for-inappropriate-content-in-an-image"></a>이미지에서 부적절한 콘텐츠 확인

이 예에서는 성인 콘텐츠에 대한 이미지를 분석해 보겠습니다. 신뢰도 점수는 이미지에 성인 콘텐츠 또는 자극적 콘텐츠가 포함될 가능성을 나타냅니다. 

이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다. 

![웃고 있는 가족사진.](../media/3-people.png)

1. Azure Cloud Shell에서 다음 명령을 실행하여 URL의 `<region>`을 바꿉니다.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/analyze?visualFeatures=Adult,Description" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/people.png'}" \
| jq '.'
```

이 예에서는 `visualFeatures`를 `Adult,Description`으로 설정합니다. 

응답은 두 가지 신뢰도 점수를 제공합니다. 하나는 자극적 콘텐츠 점수이며 다른 하나는 성인 콘텐츠 점수입니다. 이러한 점수와 이미지 설명 및 기타 시각적 기능을 사용하여 서버에 게시된 이미지에 대한 플래그 지정을 시작할 수 있습니다.

이 연습에서 시도한 예제는 `analyze` 작업으로 수행할 수 있는 분석 유형에 대한 아이디어를 제공합니다. 다른 이미지로 분석을 시도하고 시각적 기능, 세부 사항 및 언어 매개 변수의 다양한 조합을 시도해 보세요.

`analyze` 작업에 대한 자세한 내용은 [이미지 분석](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fa) 참조 문서를 참조하세요.