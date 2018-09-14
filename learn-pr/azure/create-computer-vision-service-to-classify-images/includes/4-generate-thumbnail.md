귀하의 제품 메일용 배포자 검색 및 재입고는 이러한 저장소 눈앞의 이미지를 업로드 합니다. 회사에서 수석 개발자, 하면서 이미지의 축소판 그림 만듭니다. 미리 보기는 영업 팀에 만든 온라인 보고서에 사용 됩니다. 최근 판매 관리자 하나로 보고서에 이미지를 흐리게 표시 됩니다 수 있으며 종종 없는 제품 앞, center, 큰 보고서를 검색 하기가 어렵습니다. 가 상황을 개선할 수 있습니다.

Computer Vision API의 미리 보기 생성 기능을 사용 하기로 했습니다. 아마도 작성 한 크기 조정 함수 보다 더 효율적으로 가능 합니다.

Computer Vision 먼저 고품질 미리 보기를 생성 하 고 (ROI) 관심 영역을 결정 하는 이미지 내의 개체를 분석 합니다. 그런 다음, Computer Vision은 ROI의 요구 사항에 맞게 이미지를 자릅니다. 생성된 썸네일은 필요에 따라 원래 이미지의 가로 세로 비율과 다른 가로 세로 비율을 사용하여 표시할 수 있습니다. 작동을 확인합니다.

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a>미리 보기를 생성 하려면 Computer Vision API를 호출 합니다.

`generateThumbnail` 작업은 사용자 지정 너비와 높이 사용 하 여 썸네일 이미지를 만듭니다. 기본적으로 서비스 이미지 분석, (ROI) 관심 영역을 식별 및 ROI를 기반으로 하는 스마트 자르기 좌표를 생성 합니다. 스마트 자르기 입력된 이미지의 가로 세로 비율이 다른 가로 세로 비율을 지정 하는 경우는 데 도움이 됩니다. 요청 URL의 형식은:

`https://[location].api.cognitive.microsoft.com/vision/v2.0/generateThumbnail[?width][&height][&smartCropping]`

API에 각기 다른 매개 변수를 제공하여 필요에 따라 적합한 미리 보기를 생성할 수 있습니다. 합니다 `width` 고 `height` 매개 변수는 필수입니다. 특정 이미지에 필요한 크기 API를 알려줍니다. `smartCropping` 미리 보기 내에 유지 되도록 이미지에서 관심 영역을 분석 하 여 스마트 자르기 매개 변수를 생성 합니다. 예를 들어 스마트 자르기를 사용 하도록 설정 된 자른된 프로필 사진을 못하도록 그림 프레임 내에서 사람의 얼굴도 이미지는 여러 가지 측면 사이 있는 경우.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a>썸네일 생성

이 예제에서는 다음 이미지 사용 하지만 다른 이미지에 Url 사용 하 여 동일한 명령을 시도 하도록 합니다. 

![녹색 잔디에 쓴 귀여운 제 white dog의 사진입니다.](../media/4-dog.png)

1. Azure Cloud Shell에서 다음 명령을 실행 합니다.

```azurecli
curl "https://westus2.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

이 예제에서는 100 x 100는 미리 보기를 만들려면 서비스를 요청 했습니다. 스마트 자르기를 사용 됩니다. 응답에 성공 하면 미리 보기 이미지 이진 thumbnail.jpg 라는 파일에 쓰는 것을 포함 합니다.  

> [!CAUTION]
> `-o` 매개 변수 파일에 출력을 리디렉션합니다. 파일을 항상 덮어씁니다, 그리고 따라서이 명령은 동안 둘 이상의 축소판 둘레 유지 하려는 경우 파일 이름을 변경 합니다.

## <a name="downloading-the-thumbnail"></a>미리 보기 다운로드

Azure Cloud Shell 저장소 계정에 생성된 된 미리 보기를 찾을 수 있습니다. 파일 이름을 **thumbnail.jpg**합니다. 

1. 파일이 있는지 확인 하려면 Azure Cloud Shell에서 다음 명령을 실행 **thumbnail.jg** 홈 폴더에 있습니다.

```azurecli
cd ~
ls -l
```
2. Cloud Shell 메뉴에서 선택 **파일 업로드/다운로드**를 선택한 후 **다운로드** 드롭다운 메뉴에서.

3. 에 **파일을 다운로드** 대화 상자가 나타나면 입력 **thumbnail.jpg** 필수 필드에 선택 **다운로드**합니다. 로컬 컴퓨터에이 이미지의 다운로드를 시작합니다.

4. 다운로드 한 이미지를 찾으려면 **thumbnail.jpg** 다운로드 폴더에 있습니다. 생성 된 미리 보기를 보려는 즐겨 찾는 이미지 뷰어에서 이미지를 엽니다.

`generateThumbnail` 작업이 미리 보기에는 지역의 관심 (ROI)의 이미지를 유지 하는 수 있는 강력한 썸네일 생성기입니다. 

에 대 한 자세한 내용은 합니다 `generateThumbnails` 작업 참조를 [가져오기 미리 보기](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) 설명서를 참조 합니다.