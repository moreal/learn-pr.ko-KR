솔루션 아키텍처를 다시 살펴보겠습니다.

![피드백 정렬 아키텍처의 개념적 다이어그램](../media/proposed-solution.PNG)

이 다이어그램의 오른쪽에 보이는 것처럼 세 개의 큐에 메시지를 보내려고 합니다. 따라서 해당 연결을 함수의 출력 바인딩으로 정의하겠습니다. 이러한 바인딩은 **출력 바인딩** UI를 통해 만들 수 있습니다. 그러나 시간을 절약하기 위해 config 파일을 직접 편집하겠습니다.

## <a name="add-output-bindings-to-functionjson"></a>function.json에 출력 바인딩 추가

1. 함수 앱 포털에서 [!INCLUDE [func-name-discover](./func-name-discover.md)] 함수를 선택합니다.

1. 화면 오른쪽에서 **파일 보기** 메뉴를 확장합니다.

1. **파일 보기** 탭 아래에서 **function.json**을 선택하여 편집기에서 config 파일을 엽니다.

1. **function.json**의 전체 내용을 다음 JSON으로 바꾸고, **저장**을 선택합니다.

[!code-json[](../code/function.json)]

config 파일에 세 개의 바인딩을 새로 추가했습니다.

- 각 바인딩은 `queue` 형식입니다. 본사에서 피드백의 감정을 알게 되면 피드백 메시지로 채울 세 개의 큐에 이러한 바인딩을 사용합니다.
- 메시지를 이러한 큐에 게시하게 되므로 각 바인딩에서 방향이 `out`으로 정의되어 있습니다.
- 각 바인딩은 저장소 계정에 동일한 연결을 사용합니다.
- 각 바인딩에는 고유한 `queueName` 및 `name`이 있습니다.

메시지를 간단하게 큐에 게시할 수 있습니다(예: `context.bindings.negativeFeedbackQueueItem = "<message>"`).

## <a name="update-the-function-implementation-to-sort-feedback-into-queues-based-on-sentiment-score"></a>함수 구현을 업데이트하여 감정 점수를 기준으로 피드백 정렬

피드백 분류기는 피드백을 긍정적, 중립적, 부정적이라는 세 가지 버킷으로 분류하기 위해 사용됩니다. 현재까지 입력 큐, 텍스트 분석 API를 호출하는 코드, 출력 큐를 정의했습니다. 이 섹션에서는 감정에 따라 메시지를 이러한 큐로 이동하는 논리를 추가하겠습니다.

1. [!INCLUDE [func-name-discover](./func-name-discover.md)] 함수로 이동하고, 다시 코드 편집기에서 `index.js`를 엽니다.

1. 구현을 다음 코드로 바꿉니다.

[!code-javascript[](../code/discover-sentiment+sort.js?highlight=26-48)]

강조 표시된 코드를 구현에 추가했습니다. 이 코드는 텍스트 분석 API Cognitive Services의 응답을 구문 분석합니다. 감정 점수에 따라 메시지가 세 출력 큐 중 하나로 전달됩니다. 메시지를 게시하는 코드는 올바른 바인딩 매개 변수를 설정할 뿐입니다.

## <a name="try-it-out"></a>사용해보기

업데이트된 구현을 테스트하기 위해 Storage 탐색기로 돌아가겠습니다.

1. 포털의 **리소스 그룹** 섹션에서 리소스 그룹으로 이동합니다.

1. 이 단원에 사용된 리소스 그룹인 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 선택합니다.

1. 열린 **리소스 그룹** 패널에서 저장소 계정 항목을 찾아 선택합니다.
    ![리소스 그룹 창에서 선택한 저장소 계정의 스크린샷](../media/select-storage-account.png)

1. 저장소 계정 기본 창의 왼쪽 메뉴에서 **Storage 탐색기(미리 보기)** 를 선택합니다. 이 작업은 포털 내부에서 Azure Storage 탐색기를 엽니다.

    ![현재 큐가 하나 있는 저장소 계정을 보여주는 저장소 탐색기의 스크린샷](../media/storage-explorer-menu-inputq.png)

    **큐** 컬렉션 아래에 큐가 하나 나열되어 있습니다. 이 큐는 이 모듈의 이전 테스트 섹션에서 정의한 입력 큐인 [!INCLUDE [input-q](./q-name-input.md)]입니다.        

1. 왼쪽 메뉴에서 [!INCLUDE [input-q](./q-name-input.md)]를 선택하여 이 큐의 데이터 탐색기를 살펴봅니다. 예상대로 큐에 데이터가 없습니다. 창 맨 위에 있는 **메시지 추가** 명령을 사용하여 큐에 메시지를 추가해 보겠습니다.

1. **메시지 추가** 대화 상자에서 "이 연습이 즐겁다!"를 **메시지 텍스트** 필드에 입력하고, 대화 상자의 맨 아래에서 **확인**을 클릭합니다.

1. [!INCLUDE [input-q](./q-name-input.md)]의 데이터 창에 메시지가 표시됩니다. 몇 초 후, 데이터 보기 맨 위에서 **새로 고침**을 클릭하여 큐 보기를 새로 고칩니다. 잠시 후 메시지가 사라집니다. 이 메시지는 어디로 갔을까요?

1. 왼쪽 메뉴에서 **큐** 컬렉션을 마우스 오른쪽 단추로 클릭합니다. *새* 큐가 나타납니다.
    ![컬렉션에 새 큐가 만들어진 것을 보여주는 Storage 탐색기의 스크린샷 큐에 하나의 메시지가 있습니다.](../media/sa-new-output-q.png)

    [!INCLUDE [positive-q](./q-name-positive.md)] 큐는 메시지가 처음으로 게시될 때 자동으로 생성 되었습니다. Azure Functions 큐 출력 바인딩을 사용하면 큐에 게시하기 전에 출력 큐를 수동으로 만들 필요가 없습니다! 들어오는 메시지가 함수에 의해 [!INCLUDE [positive-q](./q-name-positive.md)]로 분류되는 것을 확인했으니, 다음 메시지가 어디로 도착하는지 살펴보겠습니다.    

1. 위와 동일한 단계를 사용하여 다음 메시지를 [!INCLUDE [input-q](./q-name-input.md)]에 추가합니다.

    - "나는 브로콜리를 싫어합니다!"
    - "Microsoft는 회사입니다."

1. [!INCLUDE [input-q](./q-name-input.md)]가 다시 비워질 때까지 **새로 고침**을 클릭합니다. 이 프로세스는 몇 분 정도 걸릴 수 있으며, 새로 고침을 여러 번 수행해야 합니다.

1. **큐** 컬렉션을 마우스 오른쪽 단추로 클릭하고 큐 2개가 더 나타나는 것을 확인합니다. 큐 이름은 [!INCLUDE [neutral-q](./q-name-neutral.md)] 및 [!INCLUDE [negative-q](./q-name-negative.md)]로 지정됩니다. 이 작업은 몇 초 정도 걸릴 수 있으므로 새 큐가 나타날 때까지 **큐** 컬렉션을 계속 새로 고칩니다. 작업이 완료되면 다음과 비슷한 큐 목록이 나타납니다.

    ![큐 컬렉션에 4개의 큐가 있음을 보여주는 Storage 탐색기의 스크린샷.](../media/sa-final-q-list.png)

1. 목록의 각 큐를 클릭하여 메시지가 있는지 확인합니다. 제안된 메시지를 추가한 경우 [!INCLUDE [positive-q](./q-name-positive.md)], [!INCLUDE [neutral-q](./q-name-neutral.md)] 및 [!INCLUDE [negative-q](./q-name-negative.md)]에 하나가 표시됩니다.

축하합니다! 작동하는 피드백 분류기가 완성되었습니다! 입력 큐에 메시지가 도착하면 함수에서 텍스트 분석 API 서비스를 사용하여 감정 점수를 가져옵니다. 이 점수에 따라 함수가 메시지를 적절한 큐에 전달합니다. 함수가 큐 항목을 한 번에 하나씩 처리하는 것처럼 보이지만, Azure Functions 런타임은 큐 항목의 일괄 처리를 읽고 함수의 다른 인스턴스를 스핀업하여 병렬로 처리합니다.