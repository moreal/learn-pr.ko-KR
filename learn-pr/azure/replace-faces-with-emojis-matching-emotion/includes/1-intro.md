TheMojifier 되는 Slack _슬래시_ 해당 감정 일치 하는 모 지를 사용 하 여 이미지에서 얼굴 행위를 대체 하는 명령은 다음과 같이 합니다.

![예제 이미지](/media-drafts/example-mojify-image.png)

사용자 지정 명령으로 Slack에서 작동 하도록 설계 되었습니다. 원하는 어떤 명령 이름을 수 있지만이 모듈에 대 한 이라고 `mojify`합니다.

명령을 실행 하려면 입력 `/mojify <image to mojify>`:

![예제 이미지](/media-drafts/9.slack-type-mojify.png)

Mojifier 다음 됩니다.

  1.  모든 사용자 이미지에서 감정을 계산합니다
  2.  이 모 지를 감정을 일치합니다
  3.  이 모 지를 사용 하 여 이미지에서 얼굴을 대체합니다.
  4.  업데이트 된 이미지를 응답으로 Slack에 게시

TypeScript 및 포함 하 여 여러 Azure 기술을 사용 하 여 Mojifier 쓰여질 [Azure Functions](https://azure.microsoft.com/services/functions/) 하 고 [Azure Cognitive Services](https://azure.microsoft.com/services/cognitive-services/)합니다. 이러한의 고유한 버전을 확인 하는 데 사용 됩니다 _TheMojifier_합니다. 

> [!NOTE] 
> Mojifier에 대 한 모든 코드는에서 사용할 수 있습니다 [GitHub](https://github.com/microsoftdocs/mslearn-the-mojifier)합니다.

## <a name="tools-youll-use"></a>도구를 사용 하 여

### <a name="azure-cognitive-services"></a>Azure Cognitive Services

Azure Cognitive Services는 신속 하 게 앱에 고급 AI (인공 지능) 기능을 추가 하 여 상위 수준 Api 집합입니다. HTTP 요청을 수행 하는 방법의 이름을 알고 있는 경우 Cognitive Services를 사용할 수 있습니다.

### <a name="azure-functions"></a>Azure Functions

이벤트 또는 HTTP 요청에 응답할 수 있는 코드 조각을 호스팅할 azure Functions 수입니다. Azure 자동 크기 조정 문제를 처리 하 고 사용한 만큼만 지불 합니다. 로 Microsoft 학습에서 아무 것도 사용 하 여 비용을 발생를에서 다루게 학습 환경입니다.
