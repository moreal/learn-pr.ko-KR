TheMojifier는 다음과 같이 이미지의 사람 얼굴을 감정과 일치하는 이모지로 바꾸는 Slack _slash_ 명령입니다.

![예제 이미지](/media-drafts/example-mojify-image.png)

Slack에서 사용자 지정 명령으로 작동하도록 설계되었으며, 명령의 이름을 원하는 대로 지정할 수 있습니다. 이 문서에서는 `mojify`라고 지정했습니다.

명령을 실행하려면 다음과 같이 `/mojify <image to mojify>`를 입력합니다.

![예제 이미지](/media-drafts/9.slack-type-mojify.png)

그러면 mojifier가 다음 작업을 수행합니다.

1.  이미지 속 사람의 감정을 계산합니다.
2.  감정을 이모지와 일치시킵니다.
3.  얼굴을 이모지로 바꿉니다.
4.  이미지를 다시 Twitter에 응답으로 게시합니다.

TheMojifier는 [Azure Functions](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai) 및 [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)를 포함한 여러 Azure 기술과 TypeScript를 사용하여 작성됩니다.

이 자습서에서는 TheMojifier를 만드는 방법을 설명하고 Azure 기술을 사용하여 사용자 고유의 Slack 명령을 만드는 방법을 보여드리겠습니다.

> TODO, 여기서는 어디일까요?
> Mojifier의 모든 코드는 [GitHub](https://github.com/jawache/mojifier)에서 사용할 수 있습니다.

# <a name="requirements"></a>요구 사항

mojifier을 빌드하려면 여러 Azure 서비스를 사용해야 합니다.

## <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services는 신속하게 응용 프로그램에 고급 AI 기능을 추가하는 데 사용할 수 있는 고급 API 집합입니다. HTTP 요청을 만들 수 있으면 Cognitive Services를 사용할 수 있습니다.

[자세한 정보](https://azure.microsoft.com/services/cognitive-services/?WT.mc_id=mojifier-sandbox-ashussai)

## <a name="azure-functions"></a>Azure Functions

Logic Apps만큼 강력하기 때문에 때로는 프로그래밍 언어의 전체 표현을 사용하여 비즈니스 논리를 작성해야 합니다. Azure Functions는 이벤트 또는 HTTP 요청에 응답할 수 있는 코드 조각을 호스트하는 기술입니다. Azure가 모든 크기 조정 문제를 자동으로 처리하므로 사용자는 사용한 만큼 요금을 지불하기만 하면 됩니다.

[자세한 정보](https://azure.microsoft.com/services/functions/&WT.mc_id=mojifier-sandbox-ashussai)
