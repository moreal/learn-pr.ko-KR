<span data-ttu-id="4e910-101">이 단원에서는 이전에 만든 Computer Vision API 서비스를 사용하여 원본 이미지에서 미리 보기를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-101">In this unit, you will generate thumbnails from a source image with the Computer Vision API service that we created previously.</span></span>

# <a name="generate-a-thumbnail-from-an-image-with-computer-vision-api"></a><span data-ttu-id="4e910-102">Computer Vision API를 사용하여 이미지에서 미리 보기 생성</span><span class="sxs-lookup"><span data-stu-id="4e910-102">Generate a thumbnail from an image with Computer Vision API</span></span>

<span data-ttu-id="4e910-103">`az cognitiveservices account keys list` 명령을 실행하여 API에 인증 하는 데 사용되는 키를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-103">Execute the `az cognitiveservices account keys list` command to retrieve a key used to authenticate against the API.</span></span> <span data-ttu-id="4e910-104">해당 명령의 출력은 `key` 변수 내에 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-104">Store the output of that command within the `key` variable.</span></span>

```azurecli
key=$(az cognitiveservices account keys list -g ComputerVisionRG --name ComputerVisionService --query key1 -o tsv)
```

<span data-ttu-id="4e910-105">`curl` 명령을 실행하여 Computer Vision API에 대해 HTTP 요청을 수행하고 이전에 선언한 `key` 변수를 다시 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-105">Execute a `curl` command to do an HTTP request against the Computer Vision API and reuse the previously declared variable `key`.</span></span>

<span data-ttu-id="4e910-106">API에 각기 다른 매개 변수를 제공하여 필요에 따라 적합한 미리 보기를 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-106">Different parameters can be provided to the API to generate the proper thumbnail for your needs.</span></span> <span data-ttu-id="4e910-107">`width` 및 `height`는 필수 항목으로서 특정 이미지에 필요한 크기를 API에 알려줍니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-107">`width` and `height` are required and will tell the API which size you need for a specific image.</span></span> <span data-ttu-id="4e910-108">마지막으로, `smartCropping` 매개 변수는 미리 보기 내에 보관하기 위해 이미지에서 관심 영역을 분석하여 더 스마트한 자르기를 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-108">Finally, the `smartCropping` parameter generates smarter cropping by analyzing the region of interest in your image to keep it within the thumbnail.</span></span> <span data-ttu-id="4e910-109">예를 들어 스마트 자르기를 사용하도록 설정한 상태에서 프로필 사진을 자르면 사진 비율이 원래 요청했던 것과 다르더라도 사진 프레임 내에 사람의 얼굴이 유지됩니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-109">As an example, with smart cropping enabled, a cropped profile picture would keep someone's face within the picture frame even when the picture isn't in the same ratio as the one that we asked.</span></span>

```azurecli
curl -H "Ocp-Apim-Subscription-Key: $key" -H "Content-Type: application/json" "https://westus2.api.cognitive.microsoft.com/vision/v1.0/generateThumbnail?width=100&height=100&smartCropping=true" -d "{\"url\":\"https://docs.microsoft.com/en-us/learn/modules/create-computer-vision-service/mountains.jpg\"}" -o clouddrive/thumbnail.jpg
```

# <a name="downloading-the-thumbnail"></a><span data-ttu-id="4e910-110">미리 보기 다운로드</span><span class="sxs-lookup"><span data-stu-id="4e910-110">Downloading the thumbnail</span></span>

<span data-ttu-id="4e910-111">생성된 미리 보기는 `cloud-shell-storage-<region>`이라는 리소스 그룹 내의 Azure Cloud Shell 저장소 계정에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-111">The generated thumbnail will be found in your Azure Cloud Shell storage account within a resource group named `cloud-shell-storage-<region>`.</span></span>

1. <span data-ttu-id="4e910-112">자동으로 생성된 저장소 계정으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-112">Get into the automatically generated storage account.</span></span>

![이미지](../images/storage-account.png)

2. <span data-ttu-id="4e910-114">파일 섹션을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-114">Click on the files section.</span></span>

![이미지](../images/storage-account-click-on-files.png)

3. <span data-ttu-id="4e910-116">컨테이너의 루트에 미리 보기가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-116">You will find the thumbnail at the root of the container.</span></span>

![이미지](../images/storage-account-thumbnail.png)

4. <span data-ttu-id="4e910-118">파일을 클릭한 다음, 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-118">Click on the file, and then download it.</span></span>

<span data-ttu-id="4e910-119">다운로드 폴더 내에서 모든 이미지 뷰어를 사용하여 `100x100`-픽셀 이미지를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4e910-119">From within your download folder, you can open the `100x100`-pixels image with any image viewer.</span></span>