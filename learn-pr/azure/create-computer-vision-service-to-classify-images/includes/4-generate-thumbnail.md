이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 원본 이미지에서 미리 보기를 생성합니다.

# <a name="generate-a-thumbnail-from-an-image-with-computer-vision-api"></a>Computer Vision API를 사용하여 이미지에서 미리 보기 생성

`az cognitiveservices account keys list` 명령을 실행하여 API에 인증 하는 데 사용되는 키를 검색합니다. 해당 명령의 출력을 `key` 변수 내에 저장합니다.

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행하고 이전에 선언한 `key` 변수를 다시 사용합니다.

API에 각기 다른 매개 변수를 제공하여 필요에 따라 적합한 미리 보기를 생성할 수 있습니다. `width` 및 `height`는 필수 항목으로서 특정 이미지에 필요한 크기를 API에 알려줍니다. 마지막으로, `smartCropping` 매개 변수는 이미지에서 원하는 영역을 분석하여 더 스마트한 자르기를 생성함으로써 해당 영역을 미리 보기 내에 유지합니다. 예를 들어 스마트 자르기를 사용하도록 설정한 상태에서 프로필 사진을 자르면 사진 비율이 원래 요청했던 것과 다르더라도 사진 프레임 내에 사람의 얼굴이 유지됩니다.

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?width=100&height=100&smartCropping=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" -o clouddrive/thumbnail.jpg
```

# <a name="downloading-the-thumbnail"></a>미리 보기 다운로드

생성된 미리 보기는 `cloud-shell-storage-<region>` 리소스 그룹 내의 Azure Cloud Shell 저장소 계정에 있습니다.

1. 자동으로 생성된 저장소 계정으로 이동합니다.

![이미지](../images/storage-account.png)

2. 파일 섹션을 클릭합니다.

![이미지](../images/storage-account-click-on-files.png)

3. 컨테이너의 루트에 미리 보기가 있습니다.

![이미지](../images/storage-account-thumbnail.png)

4. 파일을 클릭하여 다운로드합니다.

다운로드 폴더 내에서 모든 이미지 뷰어를 사용하여 `100x100`픽셀 이미지를 열 수 있습니다.