사진작가로서 그날그날의 사진을 게시하는 웹 사이트를 가지고 있다고 상상해 보세요. 바빠서 사진 업로드 일정이 일관되지 않지만, 사진을 올리면 팬에게 알림을 보내고 싶습니다. Azure Storage Blob 컨테이너에 이미지를 업로드할 때마다 자동으로 트윗을 전송하도록 하는 Azure 함수를 만들려고 합니다.

여기서는 Blob 트리거를 만들고 Azure Storage Blob 컨테이너 내 특정 위치를 모니터링하도록 이 트리거에 지시하는 방법을 배웁니다.

## <a name="what-is-azure-storage"></a>Azure Storage란?

Azure Storage는 Blob, 큐 및 NoSQL을 비롯한 모든 형식의 데이터를 지원하는 Microsoft 클라우드 저장소 솔루션입니다. Azure Storage의 목표는 다음과 같은 데이터 저장소를 제공하는 것입니다.

- 고가용성
- 보안
- 확장성
- 관리

Azure Storage 자체에 너무 집중하지 않겠습니다. 대신, Azure Storage를 사용하여 함수 실행을 트리거할 Blob을 만들겠습니다.

## <a name="what-is-azure-blob-storage"></a>Azure Blob Storage란?

Azure Blob Storage는 구조화되지 않은 데이터를 대량으로 저장하도록 설계된 개체 저장소 솔루션입니다. 

예를 들어 Azure Blob Storage는 다음과 같은 작업을 수행하는 데 적합합니다.

- 파일 저장
- 파일 제공
- 동영상 및 오디오 스트리밍
- 데이터 기록

**블록 Blob**, **추가 Blob** 및 **페이지 Blob** 등 세 가지 Blob 유형이 있습니다. 블록 Blob은 가장 일반적인 유형으로, 이를 통해 텍스트 또는 이진 데이터를 효율적으로 저장할 수 있습니다. 추가 Blob은 블록 Blob과 비슷하지만, 지속적으로 업데이트되는 로그 파일을 만드는 등의 추가 작업을 위해 고안되었습니다. 마지막으로, 페이지 Blob은 페이지로 구성되며 빈번한 임의의 읽기 및 쓰기 작업에 맞게 고안되었습니다.

## <a name="what-is-a-blob-trigger"></a>Blob 트리거란?

Blob 트리거는 Azure Blob Storage에서 파일이 업로드되거나 업데이트될 때 함수를 실행하는 트리거입니다. Blob 트리거를 만들려면 Azure Storage 계정을 만들고 트리거의 모니터링 대상이 되는 위치를 제공합니다.

## <a name="how-to-create-a-blob-trigger"></a>Blob 트리거를 만드는 방법

지금까지 알아본 다른 트리거와 마찬가지로 Blob 트리거도 Azure Portal에서 만듭니다. Azure 함수 내의 미리 정의된 트리거 형식 목록에서 **Blob 트리거**를 선택합니다. 그런 다음, Blob이 만들어지거나 업데이트될 때 실행할 논리를 입력합니다.

한 가지 확인해야 할 설정이 **경로**입니다. **경로**는 Blob이 업로드되거나 업데이트되었는지 여부를 확인하기 위해 모니터링할 Blob 트리거를 나타냅니다. 기본적으로 **경로** 값은 다음과 같습니다. 

> samples-workitems/{name}

이 개념을 *samples-workitems* 및 *{name}* 의 두 부분으로 나누어 보겠습니다. 첫 번째 부분인 *samples-workitems*는 트리거가 모니터링하는 Blob 컨테이너를 나타냅니다. 두 번째 부분인 *{name}* 은 모든 형식의 파일이 트리거로 하여금 함수를 호출하게 만드는 것을 의미합니다. 필터가 없으므로 함수가 호출됩니다. 예를 들어, 다음과 같은 구문을 사용하면 PNG 파일이 추가될 때만 트리거가 함수를 호출하도록 만들 수 있습니다.

> samples-workitems/{name}.png

이 개념에서 마지막으로 가장 중요한 정보는 *name*이라는 텍스트입니다. *name*은 추가된 파일의 이름을 수신하는 Azure 함수 내의 매개 변수를 나타냅니다. 예를 들어 *resume.txt*라는 파일을 업로드하는 경우 Azure 함수는 해당 값을 *name*이라는 매개 변수를 통해 문자열로 수신합니다.

## <a name="summary"></a>요약

Blob 트리거는 Azure Storage Blob 계정의 특정 위치에 활동이 확인되면 Azure 함수를 호출합니다. Azure Portal에서 **경로** 값을 수정하여 모니터링할 위치를 설정합니다.
