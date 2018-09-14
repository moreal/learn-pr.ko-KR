Face api 때문에 해당 감정 가져올를 사람이 하지 않기 때문에 모의 이미지를 전달할 수 없습니다 했습니다. 각이 모 지에 대 한 프록시를 사람이 필요 했습니다 me.

스스로의 사진을 취했습니다 _정확 하 게_ 각이 모 지를 모방 하 고 사용 합니다 _감정적인 지점_ 이 모에 대 한 프록시로 해당 이미지에 대 한 합니다. 같은 유지 하기 위해 흥미로운도 모 지를 사용 하 여 연결 및 필자 팀에서 사용자를 선택 합니다.

![팀 문자](/media-drafts/team.jpg)

이 모 지 각에 대 한 프록시 이미지의 목록을 볼 수 있습니다는 `bin/proxy-images` 이 자습서를 사용 하 여 연결 된 샘플 코드에서는 폴더입니다.

## <a name="goal"></a>목표

이 챕터에서는 Azure의 Face API를 사용 하 고 다음 Face API를 사용 하 여으로 프록시 설정 된 이미지를 사용 하 여 모든이 모 지 보정할 수 있도록 필요한 인증 키를 생성 합니다.

## <a name="learning-objectives"></a>학습 목표

- API를 생성 하는 방법을 Cognitive Services 사용에 대 한 키입니다.
- Face API를 통해 이미지를 실행 하 고 감정 정보를 추출 하는 방법.

## <a name="generate-an-azure-face-api-key"></a>Azure의 Face API 키를 생성 합니다.

Azure의 Face API를 사용 하려면 키를 인증 해야 합니다.

키를 가져오는 가장 빠른 방법은로는 통해 https://azure.microsoft.com/try/cognitive-services/?api=face-api 및 평가판 Face API를 등록 합니다.

한 번 있습니다 등록은 몇 가지를 나중에 저장 해야 하는 정보만 제공 합니다.

1. 가져오기의 _끝점_합니다. 와 같이 표시 됩니다. https://westcentralus.api.cognitive.microsoft.com/face/v1.0

2. 두 API 키, 저장소 중 하나 (하나는 중요 하지 않습니다) 나중에 사용할 표시

## <a name="setup-the-environment-variables"></a>환경 변수를 설정 합니다.

응용 프로그램을 실행 하려는 하드 코딩 환경 변수를 사용 하려면 터미널에서 다음이 명령을 실행 하겠습니다 스크립트에서 이러한 보다는 보정 스크립트가 올바른 호출을 위해 Face API URL 및 키를 알아야 합니다.

```bash
export FACE_API_URL=<the-face-api-url>
export FACE_API_KEY=<your-face-api-key>
```

라는 패키지 사용도 `dotenv` 노드 응용 프로그램에서 합니다. 이 패키지 보겠습니다 사용 하 여 환경 변수를 로컬로 저장 라는 파일에 `.env`입니다. `dotenv` 패키지는이 파일에 모든 변수를 로드 하 고 응용 프로그램에 대 한 환경 변수로를 표시 합니다.

> **참고**
>
> 체크 인 되지 `.env` 소스 제어에 파일입니다.

Azure Functions를 통해 환경 변수를 처리 하는 다른 방법은 해당 `local.settings.json` 파일을 나중에 자세히 설명 합니다.

## <a name="create-some-proxy-images-for-emojis"></a>이 모 지에 대 한 일부 프록시 이미지 만들기

저 있지만 자유롭게 직접 생성 하는 모든 프록시 이미지 제공한!

이 모 지 각에 대 한는 `bin/proxy-images` 폴더는이 모 지를 모방 직접 사진 및 이미지를 사용 하 여 이미지를 대체 합니다.

## <a name="try-it-out"></a>체험

이제 부터가 흥미로운 부분! 각 이미지를 실행 하려고 합니다 `bin/proxy-images` 에이 모 지에 대 한 감정적인 지점을 계산 하려면 Face API를 통해 _감정적인 공간_실행:

```bash
node bin/calibrate.js
```

이 명령의 출력은 비슷해야 다음과 같이 합니다.

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

먼저이 모의 처리 되 고 그런 다음 마지막으로 출력 콘솔에 정의 하는 배열을 출력 합니다 `EmotivePoint` 모든이 모 지입니다. 이 같은 형식으로 배열 `shared/mojis.ts`합니다.

복사의 관련 섹션에이 스크립트의 출력 프록시 이미지 중 일부를 변경한 경우 `mojis.ts`
