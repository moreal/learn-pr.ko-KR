이모지는 인간이 아니기 때문에 이모지 이미지를 Face API에 전달하여 감정을 가져올 수 없습니다. 따라서 각 이모지에 인간 프록시, 즉 제가 필요했습니다.

저는 제 사진을 찍어서 각 이모지를 _정확하게_ 모방했으며, 해당 이미지의 _감정 지점_을 이모지의 프록시로 사용했습니다. 또한 지루해지는 것을 막기 위해, 다음과 같이 팀에서 사람들을 선택하여 이모지에 연결했습니다.

![팀 Moji](/media-drafts/team.jpg)

사랑에 빠진 눈(😍)을 나타내는 이모지로는 제 부인의 사진(❤️)을 선택했습니다. [스티븐 호킹](https://en.wikipedia.org/wiki/Stephen_Hawking) 박사를 추모하는 의미로 🤔를 나타내는 스티븐 호킹 박사의 사진을 선택했습니다.

이 자습서와 연결된 샘플 코드의 `bin/proxy-images` 폴더에서 각 이모지의 프록시 이미지 목록을 볼 수 있습니다.

이 챕터에서는 Azure Face API를 사용할 수 있도록 키를 생성한 다음, Face API를 사용하여 저를 대신하는 이미지를 통해 모든 이모지를 보정하겠습니다.

## <a name="generate-an-azure-face-api-key"></a>Azure Face API 키 생성

<!-- To make calls to the Azure Face API we will need a special authorization key.

We are going to create one using the `az` CLI. -->

Azure Face API를 사용하려면 특별한 인증 키가 필요합니다. https://azure.microsoft.com/try/cognitive-services/로 이동하여 평가판 Face API에 등록하세요.

![팀 Moji](/media-drafts/4.calibrating-emojis.get-face-api.png)

> TODO: faceAPI를 만들고 키를 가져오는 az 명령 찾기

<!-- > NOTE the Azure Face API doesn't return the emotion information by default, we need to switch on this behavior by setting some query parameters, like so:
> https://westeurope.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion -->

## <a name="setup-the-environment-variables"></a>환경 변수 설정

환경 변수를 사용할 스크립트에 하드 코딩하지 않고 호출을 올바르게 수행하고, 응용 프로그램을 실행할 것으로 예상되는 터미널에서 다음 명령을 실행하려면 보정 스크립트가 Face API URL 및 키를 알고 있어야 합니다.

```bash
FACE_API_URL=<the-face-api-url>
FACE_API_KEY=<your-face-api-key>
```

<!-- > NOTE
> Don't forget to add the query param returnFaceAttributes=emotion to ensure the Face API returns emotion as well -->

## <a name="create-some-proxy-images-for-emojis"></a>이모지에 대한 프록시 이미지 만들기

저는 모든 프록시 이미지를 직접 입력했지만, 얼마든지 자유롭게 생성하셔도 됩니다!

`bin/proxy-images` 폴더의 각 이모지에 대해, 해당 이모지를 모방하는 여러분의 사진을 찍어서 이미지를 그 사진으로 바꿀 수 있습니다.

## <a name="try-it-out"></a>사용해보기

지금부터 흥미로운 부분입니다! Face API를 통해 `bin/proxy-images`의 각 이미지를 실행하여 _감정 공간_의 해당 이모지에 대한 감정 지점을 계산하고, 다음 명령을 실행합니다.

```bash
node bin/calibrate.js
```

이 명령의 출력은 다음과 비슷합니다.

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

먼저 처리 중인 이모지를 출력한 다음, 최종적으로 모든 이모지의 `EmotivePoint`를 정의하는 배열을 콘솔에 출력합니다. `shared/mojis.ts`의 배열과 같은 형식입니다.

대체 이미지를 변경한 경우 이 스크립트의 출력을 `mojis.ts`의 관련 섹션에 복사합니다.
