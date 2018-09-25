제품의 현장 배포자는 반납하는 매장 선반의 이미지를 스캔하여 업로드합니다. 회사의 대표 개발자는 이미지의 썸네일을 만들어야 합니다. 썸네일은 영업 팀을 위해 작성한 온라인 보고서에 사용됩니다. 최근에 영업 관리자가 보고서의 이미지가 흐릿하고 대개 제품 전면과 가운데 부분이 없다고 말했기 때문에 큰 보고서를 스캔하기 어렵습니다. 상황을 개선하는 것은 사용자에게 달려 있습니다.

Computer Vision API의 썸네일 생성 기능을 사용해 보기로 합니다. 이는 크기 조정 기능보다 더 나을 수도 있습니다.

Computer Vision은 먼저 고품질 썸네일을 생성한 다음, 이미지 내의 개체를 분석하여 ROI(관심 영역)를 결정합니다. 그런 다음, Computer Vision은 ROI의 요구 사항에 맞게 이미지를 자릅니다. 생성된 썸네일은 필요에 따라 원래 이미지의 가로 세로 비율과 다른 가로 세로 비율을 사용하여 표시할 수 있습니다. 작동을 확인합니다.

## <a name="calling-the-computer-vision-api-to-generate-a-thumbnail"></a>Computer Vision API를 호출하여 썸네일 생성

`generateThumbnail` 작업은 사용자 지정 폭 및 높이의 썸네일 이미지를 생성합니다. 기본적으로 서비스는 이미지를 분석하고 ROI(관심 영역)를 식별하며 ROI를 기반으로 스마트 자르기 좌표를 생성합니다. 스마트 자르기는 입력 이미지의 가로 세로 비율과 다른 가로 세로 비율을 지정할 때 도움이 됩니다. 요청 URL의 형식은 다음과 같습니다.

`https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=<...>&height=<...>&smartCropping=<...>`

API에 각기 다른 매개 변수를 제공하여 필요에 따라 적합한 썸네일을 생성할 수 있습니다. `width` 및 `height` 매개 변수는 필수 항목입니다. 이들 매개 변수는 특정 이미지에 필요한 크기를 API에 알려 줍니다. `smartCropping` 매개 변수는 썸네일 내에 보관하기 위해 이미지에서 관심 영역을 분석하여 더 스마트한 자르기를 생성합니다. 예를 들어 스마트 자르기를 사용하도록 설정한 상태에서 프로필 사진을 자르면 사진의 가로 세로 비율이 다르더라도 사진 프레임 내에 사람의 얼굴이 유지됩니다.

[!INCLUDE [get-key-note](./get-key.md)]

## <a name="generate-a-thumbnail"></a>썸네일 생성

이 예에서는 다음 이미지를 사용하지만 다른 이미지의 URL에 대해 동일한 명령을 시도해 볼 수 있습니다.

![풀밭에 앉아 있는 귀여운 흰 강아지의 사진.](../media/4-dog.png)

1. Azure Cloud Shell에서 다음 명령을 실행합니다. 명령에서 `<region>`을 Cognitive Services 계정의 지역으로 바꿉니다.

```azurecli
curl "https://<region>.api.cognitive.microsoft.com/vision/v2.0/generateThumbnail?width=100&height=100&smartCropping=true" \
-H "Ocp-Apim-Subscription-Key: $key" \
-H "Content-Type: application/json" \
-d "{'url' : 'https://raw.githubusercontent.com/MicrosoftDocs/mslearn-process-images-with-the-computer-vision-service/master/images/dog.png'}" \
-o  thumbnail.jpg
```

이 예제에서는 100x100 크기의 썸네일을 만들도록 서비스에 요청합니다. 스마트 자르기가 사용 설정되었습니다. 성공적인 응답에는 thumbnail.jpg라는 파일에 쓰는 이진 썸네일 이미지가 포함되어 있습니다.

> [!CAUTION]
> `-o` 매개 변수는 출력을 파일로 재전송합니다. 파일은 항상 덮어쓰여지므로 이 명령을 시도하는 동안 둘 이상의 썸네일을 유지하려는 경우에는 파일 이름을 변경하세요.

## <a name="view-the-generated-thumbnail"></a>생성된 썸네일 보기

생성된 썸네일은 Azure Cloud Shell 저장소 계정에서 찾을 수 있습니다. 파일 이름을 **thumbnail.jpg**로 지정했습니다.

Microsoft Learn의 Cloud Shell에는 파일을 다운로드하는 기능이 없지만 다음 지침에 따라 Azure Portal을 통해 썸네일을 다운로드할 수 있습니다.

1. Azure Cloud Shell에서 다음 명령을 실행하여 **thumbnail.jpg** 파일이 홈 폴더에 있는지 확인합니다.

    ```azurecli
    cd ~
    ls -l
    ```



1. 다음 명령을 실행하여 `thumbnail.jpg`를 clouddrive 폴더로 이동합니다.

    ```azurecli
    mv ~/thumbnail.jpg ~/clouddrive
    ```
1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.
1. 포털 대시보드의 **모든 리소스** 패널에서 이름이 `cloudshell`로 시작되는 저장소 계정을 선택합니다.
1. 저장소 계정 창에서 **Storage 탐색기**를 선택한 다음, **파일 공유**를 선택하고 해당 컬렉션에서 이름이 **cloudshellfiles***로 시작되는 파일 공유를 선택합니다.
1. *thunbnail.jpg* 파일을 선택한 다음, 맨 위 메뉴에서 **다운로드**를 선택하여 이미지를 봅니다.

`generateThumbnail` 작업은 썸네일에서 이미지의 ROI(관심 영역)를 유지할 수 있는 강력한 썸네일 생성기입니다.

`generateThumbnails` 작업에 대한 자세한 내용은 [썸네일 가져오기](https://westus.dev.cognitive.microsoft.com/docs/services/5adf991815e1060e6355ad44/operations/56f91f2e778daf14a499e1fb) 참조 문서를 참조하세요.