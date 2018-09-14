사용 하기 전에 구현을 심층적으로, 보겠습니다 먼저 몇 가지 질문 더 높은 수준입니다.

## <a name="how-to-calculate-the-emotion-of-a-face"></a>얼굴 감정을 계산 하는 방법

계산 emotion에는 응용 프로그램의 가장 액세스 하기 쉬운 부분 중 하나입니다. 사용 합니다 [FaceAPI](https://azure.microsoft.com/services/cognitive-services/face/)Azure Cognitive Services 제품의 일부인 합니다.

모든 얼굴, 이미지에서 얼굴의 위치를 검색 하 고 요청 하는 경우를 포함 하 여 이미지에 대 한 이미지 및 반환 정보를 계산 하 고도 얼굴의 감정을 반환 하는 입력으로 FaceAPI 가져오고 다음과 같이 합니다.

```json
{
  "anger": 0.572,
  "contempt": 0.025,
  "disgust": 0.242,
  "fear": 0.001,
  "happiness": 0.014,
  "neutral": 0.111,
  "sadness": 0.033,
  "surprise": 0.003
}
```

이 이미지를 예를 들어 수행 합니다.

![예제 얼굴](/media-drafts/example-face.jpg)

이 이미지를 처리 하려면 다음과 같은 API 끝점에 POST 요청을 해야 합니다.

https://xxxxxxxxx.api.cognitive.microsoft.com/face/v1.0/detect?returnFaceId=false&returnFaceLandmarks=false&returnFaceAttributes=emotion

본문에 이미지에서는 다음과 같이 합니다.

```json
{
  "url": "<path-to-image>"
}
```

> **참고**
>
> 기본적으로 API emotion을 반환 하지 않으면 명시적으로 지정 해야 쿼리 매개 변수 `returnFaceAttributes=emotion`

비밀 키를 사용 하는 API를 인증합니다. 헤더를 사용 하 여이 키를 송신 해야 합니다.

```
Ocp-Apim-Subscription-Key: <your-subscription-key>
```

위의 쿼리 매개 변수를 사용 하 여 API는 JSON을 반환 다음과 같이 합니다.

```json
[
  {
    "faceRectangle": {
      "top": 207,
      "left": 198,
      "width": 229,
      "height": 229
    },
    "faceAttributes": {
      "emotion": {
        "anger": 0.001,
        "contempt": 0.014,
        "disgust": 0,
        "fear": 0,
        "happiness": 0.306,
        "neutral": 0.675,
        "sadness": 0.003,
        "surprise": 0.001
      }
    }
  }
]
```

이미지에서 검색 된 얼굴에 하나씩 결과의 배열을 반환 합니다. 각 면에 대해으로 글꼴의 크기/위치가 반환 `faceRectangle` 및 0에서을 1로 숫자로 나타낸 감정은 `faceAttributes`합니다.

> **팁**
>
> Cognitive Services를 사용 하 여도 생길 시작할 수 있습니다 _없이_ 로 Azure 계정에 있는 [이 페이지](https://azure.microsoft.com/try/cognitive-services/?api=face-api&WT.mc_id=mojifier-sandbox-ashussai) 평가판 이용 하려면 전자 메일 주소를 입력 합니다.

## <a name="how-to-map-an-emotion-to-an-emoji"></a>Emotion이 발생 하는 모 지를 매핑하려면 어떻게 하나요?

두 개의 감정과 걱정 0에서 1 사이의 값을 사용 하 여 행복, 있었습니다 한다고 가정 합니다. 다음 모든 얼굴 2D에 그릴 수 없습니다 _감정적인 공간_ 사용자의 emotion에 따라 다음과 같이:

![유클리드 거리 1](/media-drafts/graph-1.jpg)

또한 각이 모 지에 대 한 감정적인 지점을 파악 하 고도 2D 감정적인 공간에서 표시 한 다음 한다고 가정 합니다. 모든 다른이 모 지 emotion에는 가장 가까운이 모 지를 알아낼 수이 2D 감정적인 공간에 얼굴이 사이의 거리를 계산 하는 경우 다음 다음과 같이 합니다.

![유클리드 거리 2](/media-drafts/graph-2.png)

이 계산 라고는 `euclidian distance`를 사용한 것 이지만 (분노, 경 멸, 혐오, 공포, 행복, 중립, 슬픔, 놀람)를 사용 하 여 8d 감정적인 공간의 아닌 2D 감정적인 공간 및 합니다.

> **팁**
>
> 유클리드 거리를 호출 하는 npm 패키지를 쉽게 사용 하는 같은 있도록 <https://www.npmjs.com/package/euclidean-distance>입니다.

## <a name="shared-code"></a>공유 코드

샘플 시작 프로젝트에는 이미 많은 위의 사용 사례를 처리 하는 코드를 사용 하 여 공유 폴더와 함께 제공 됩니다.

### <a name="emotivepoint"></a>EmotivePoint

자세히 살펴보면 경우 합니다 `EmotivePoint` 클래스의 `shared/emmotive-point.ts` 몇 가지를 알 수 있습니다.

Emotive 정보와 로컬 멤버 변수로 저장이 포함 된 개체는 입력으로 생성자는 다음과 같이 합니다.

```typescript
 constructor({
    anger,
    contempt,
    disgust,
    fear,
    happiness,
    neutral,
    sadness,
    surprise
  }) {
    this.anger = anger;
    this.contempt = contempt;
    this.disgust = disgust;
    this.fear = fear;
    this.happiness = happiness;
    this.neutral = neutral;
    this.sadness = sadness;
    this.surprise = surprise;
  }
```

역시 emotive 두 점 사이의 유클리드 거리를 계산 하는 데 사용 수 거리 라는 함수를 다음과 같이 합니다.

```typescript
  distance(other) {
    let myPoint = this.toArray();
    let otherPoint = other.toArray();
    return distance(myPoint, otherPoint);
  }
```

따라서에서는 두 emotive 포인트를 만들고 얼마나 가까이 계산 수 다음과 같이 합니다.

```typescript
let a = new EmotivePoint({
  /* ... */
});
let b = new EmotivePoint({
  /* ... */
});
let distance = a.distance(b);
```

### <a name="face"></a>Face

다른 도우미 클래스는 합니다 `Face` 클래스 비롯 한 몇 가지 다른 속성을 결합이 `EmotivePoint` 얼굴, 이미지에서 얼굴을 정의 하는 사각형을 사용 하 여는 `Rect` 클래스에 대 한 합니다.

살펴보면 하는 경우는 `Face` 클래스 생성자에서 `shared/face.ts` 코드이 줄이 표시 됩니다.

```typescript
this.moji = this.chooseMoji(this.emotivePoint);
```

`emotivePoint` 얼굴 자체의 emotive 지점이입니다.
`chooseMoji` 적절 한이 모 지 면의 emotivePoint 기반을 반환 합니다.

```typescript
  chooseMoji(point) {
    let closestMoji = null;
    let closestDistance = Number.MAX_VALUE;
    for (let moji of MOJIS) {
      let emoPoint = moji.emotiveValues;
      let distance = emoPoint.distance(point);
      if (distance < closestDistance) {
        closestMoji = moji;
        closestDistance = distance;
      }
    }
    return closestMoji;
  }
```

`MOJIS` 목록에 다음 강의 생성 하는 방법에 대 한 모든이 모 지 emotive 요소의 하겠습니다.

`chooseMoji` 이 얼굴 및 모든이 모 지를 가장 가까운 것 반환 사이의 거리를 계산 하는 함수입니다.

# <a name="summary"></a>요약

시점의 각이 모 지에 대 한 계산 _감정적인_ 공간을이 라고 _보정_ 에서는이 다음 장에서 설명 하 고 합니다.

Azure의 Face API를 사용 하 여 다음의 각 얼굴의 감정적인 지점과 이미지에서 얼굴의 목록을 가져옵니다. 그런 다음 유클리드 거리 알고리즘을 사용 하 여 각 얼굴의 가장 가까운이 모 지를 찾을 수 있습니다.
