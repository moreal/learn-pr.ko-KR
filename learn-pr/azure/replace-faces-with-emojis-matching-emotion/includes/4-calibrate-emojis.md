<span data-ttu-id="dcf4c-101">이모지는 인간이 아니기 때문에 이모지 이미지를 Face API에 전달하여 감정을 가져올 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-101">We can’t pass an image of the emoji to the Face API to get it’s emotion because, well because it’s not human.</span></span> <span data-ttu-id="dcf4c-102">따라서 각 이모지에 인간 프록시, 즉 제가 필요했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-102">So for each emoji, I needed a human proxy, me.</span></span>

<span data-ttu-id="dcf4c-103">저는 제 사진을 찍어서 각 이모지를 _정확하게_ 모방했으며, 해당 이미지의 _감정 지점_을 이모지의 프록시로 사용했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-103">I took pictures of myself _accurately_ mimicking each emoji, and used the _emotional point_ for that image as the proxy for the emoji.</span></span> <span data-ttu-id="dcf4c-104">또한 지루해지는 것을 막기 위해, 다음과 같이 팀에서 사람들을 선택하여 이모지에 연결했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-104">To keep things interesting I also chose people from my team and associated them with emojis as well, like so:</span></span>

![팀 Moji](/media-drafts/team.jpg)

<span data-ttu-id="dcf4c-106">사랑에 빠진 눈(😍)을 나타내는 이모지로는 제 부인의 사진(❤️)을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-106">For the emoji of love eyes (😍) I chose a picture of my wife ❤️.</span></span> <span data-ttu-id="dcf4c-107">[스티븐 호킹](https://en.wikipedia.org/wiki/Stephen_Hawking) 박사를 추모하는 의미로 🤔를 나타내는 스티븐 호킹 박사의 사진을 선택했습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-107">In memory of [Stephen Hawking](https://en.wikipedia.org/wiki/Stephen_Hawking) I picked a picture of him to represent 🤔.</span></span>

<span data-ttu-id="dcf4c-108">이 자습서와 연결된 샘플 코드의 `bin/proxy-images` 폴더에서 각 이모지의 프록시 이미지 목록을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-108">You can see the list of proxy images for each emoji in the `bin/proxy-images` folder in the sample code associated with this tutorial.</span></span>

<span data-ttu-id="dcf4c-109">이 챕터에서는 Azure Face API를 사용할 수 있도록 키를 생성한 다음, Face API를 사용하여 저를 대신하는 이미지를 통해 모든 이모지를 보정하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-109">In this chapter you will generate a key so you can use the Azure Face API and then use the Face API to calibrate all the emojies using proxied images of me.</span></span>

## <a name="generate-an-azure-face-api-key"></a><span data-ttu-id="dcf4c-110">Azure Face API 키 생성</span><span class="sxs-lookup"><span data-stu-id="dcf4c-110">Generate an Azure Face API Key</span></span>

<!-- To make calls to the Azure Face API we will need a special authorization key.

We are going to create one using the `az` CLI. -->

<span data-ttu-id="dcf4c-111">Azure Face API를 사용하려면 특별한 인증 키가 필요합니다. https://azure.microsoft.com/try/cognitive-services/로 이동하여 평가판 Face API에 등록하세요.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-111">To use the Azure Face API we need a special authentication key, head over to https://azure.microsoft.com/try/cognitive-services/ and signup to trial the Face API.</span></span>

![팀 Moji](/media-drafts/4.calibrating-emojis.get-face-api.png)

> <span data-ttu-id="dcf4c-113">TODO: faceAPI를 만들고 키를 가져오는 az 명령 찾기</span><span class="sxs-lookup"><span data-stu-id="dcf4c-113">TODO: Find az commands to create faceAPI and grab keys</span></span>

<!-- > NOTE the Azure Face API doesn't return the emotion information by default, we need to switch on this behavior by setting some query parameters, like so:
> https://westeurope.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion -->

## <a name="setup-the-environment-variables"></a><span data-ttu-id="dcf4c-114">환경 변수 설정</span><span class="sxs-lookup"><span data-stu-id="dcf4c-114">Setup the environment variables</span></span>

<span data-ttu-id="dcf4c-115">환경 변수를 사용할 스크립트에 하드 코딩하지 않고 호출을 올바르게 수행하고, 응용 프로그램을 실행할 것으로 예상되는 터미널에서 다음 명령을 실행하려면 보정 스크립트가 Face API URL 및 키를 알고 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-115">The calibration script needs to know your Face API URL and Key in order to make the correct calls, rather than hardcoding these in the script we are going to use environment varialbes, run these commands in the terminal you expect to run the application in:</span></span>

```bash
FACE_API_URL=<the-face-api-url>
FACE_API_KEY=<your-face-api-key>
```

<!-- > NOTE
> Don't forget to add the query param returnFaceAttributes=emotion to ensure the Face API returns emotion as well -->

## <a name="create-some-proxy-images-for-emojis"></a><span data-ttu-id="dcf4c-116">이모지에 대한 프록시 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="dcf4c-116">Create some proxy images for emojis</span></span>

<span data-ttu-id="dcf4c-117">저는 모든 프록시 이미지를 직접 입력했지만, 얼마든지 자유롭게 생성하셔도 됩니다!</span><span class="sxs-lookup"><span data-stu-id="dcf4c-117">I've provided all the proxy images myself, but feel free to generate your own!</span></span>

<span data-ttu-id="dcf4c-118">`bin/proxy-images` 폴더의 각 이모지에 대해, 해당 이모지를 모방하는 여러분의 사진을 찍어서 이미지를 그 사진으로 바꿀 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-118">For each emoji in the `bin/proxy-images` folder, take a picture of yourself mimicking that emoji and replace the image with your image.</span></span>

## <a name="try-it-out"></a><span data-ttu-id="dcf4c-119">사용해보기</span><span class="sxs-lookup"><span data-stu-id="dcf4c-119">Try it out</span></span>

<span data-ttu-id="dcf4c-120">지금부터 흥미로운 부분입니다!</span><span class="sxs-lookup"><span data-stu-id="dcf4c-120">Now comes the fun part!</span></span> <span data-ttu-id="dcf4c-121">Face API를 통해 `bin/proxy-images`의 각 이미지를 실행하여 _감정 공간_의 해당 이모지에 대한 감정 지점을 계산하고, 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-121">We are going to run each of the images in the `bin/proxy-images` through the Face API to calculate an emotional point for that emoji in _emotional space_, run:</span></span>

```bash
node bin/calibrate.js
```

<span data-ttu-id="dcf4c-122">이 명령의 출력은 다음과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-122">The output of this command should look something like so:</span></span>

```json
...
Processing 🤓
Processing 🤔
Processing 🦄
Processing 😃
Processing 😆
...
{
    emotiveValues: new EmotivePoint({
        anger: 0,
        contempt: 0.005,
        disgust: 0.001,
        fear: 0,
        happiness: 0,
        neutral: 0.922,
        sadness: 0.071,
        surprise: 0
    }),
    emojiIcon: "😴"
}
```

<span data-ttu-id="dcf4c-123">먼저 처리 중인 이모지를 출력한 다음, 최종적으로 모든 이모지의 `EmotivePoint`를 정의하는 배열을 콘솔에 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-123">It will first print out the emoji's it is processing and then finally print out to the console an array which defines the `EmotivePoint` of all the emoji's.</span></span> <span data-ttu-id="dcf4c-124">`shared/mojis.ts`의 배열과 같은 형식입니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-124">This is the same format as the array in `shared/mojis.ts`.</span></span>

<span data-ttu-id="dcf4c-125">대체 이미지를 변경한 경우 이 스크립트의 출력을 `mojis.ts`의 관련 섹션에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="dcf4c-125">If you changed some of the proxied images then copy the output of this script to the relevant section of `mojis.ts`</span></span>
