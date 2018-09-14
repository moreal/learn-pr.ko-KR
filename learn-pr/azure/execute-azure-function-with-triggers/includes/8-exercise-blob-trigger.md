이 연습에서는 만들거나 업데이트될 때 Blob의 이름과 크기를 표시하는 Azure 함수를 만들겠습니다. 

> [!NOTE]
> 이 연습을 완료하려면 유효한 계정으로 [Azure Portal](https://portal.azure.com/)에 로그인했는지 확인하세요.

## <a name="create-a-blob-trigger"></a>Blob 트리거 만들기

다시 기존 Azure Functions 응용 프로그램을 계속 사용하고 Blob 트리거를 추가해 보겠습니다.

1. **함수**를 가리키고 더하기(+) 아이콘을 선택합니다.

    ![함수를 가리키고 더하기 선택](../media-drafts/4-hover-function.png)

1. **Blob 트리거**를 선택합니다.

1. 언어로 **C#** 을 선택합니다. 

1. **이름**은 기본값으로 그대로 둡니다.

1. **경로**는 기본값으로 그대로 둡니다.

1. 기존 Azure Storage 계정을 선택하거나, Azure에서 새 계정을 만들려면 **만들기**를 선택합니다.

## <a name="download-storage-explorer"></a>Storage 탐색기 다운로드

이제 Blob 트리거를 만들었으므로 Blob을 쉽게 만들 수 있는 Storage 탐색기를 다운로드해 보겠습니다.

- [Storage 탐색기](http://storageexplorer.com)를 다운로드합니다.

## <a name="connect-to-your-azure-storage-account"></a>Azure Storage 계정에 연결

이제 Storage 탐색기를 다운로드했습니다. 제공된 자격 증명을 사용하여 로그인해 보겠습니다.

1. Storage 탐색기에서 왼쪽에 있는 더하기(+) 아이콘을 선택합니다.

1. **저장소 계정 이름 및 키 사용**을 선택합니다.

1. **다음**을 선택합니다.

1. Azure의 Blob 트리거 아래에서 **통합**을 선택합니다.

1. **문서**를 선택하여 보기를 확장합니다.

1. **계정 이름** 및 **계정 키**를 복사합니다.

1. Storage 탐색기로 돌아가 **계정 이름** 및 **계정 키**에 붙여넣습니다.

1. **표시 이름**을 입력합니다. 이 값은 Storage 탐색기의 연결 이름입니다.

1. **다음**을 선택합니다.

1. **연결**을 선택합니다. 

## <a name="create-a-blob-container"></a>Blob 컨테이너 만들기

Azure Storage 계정에 연결되어 있지 않습니다. Blob 트리거는 **경로** 필드에 설명된 위치만 모니터링합니다. 기본적으로 경로는 다음과 같아야 합니다.

> samples-workitems/{name}

**samples-workitems**라는 컨테이너를 만들어야 합니다.

1. Storage 탐색기에서 저장소 계정을 확장합니다. 이름은 연결 프로세스 중에 제공한 **표시 이름**이어야 합니다.

1. **Blob 컨테이너**를 마우스 오른쪽 단추로 클릭하고 **Blob 컨테이너 만들기**를 선택합니다.

1. **samples-workitems**를 입력합니다.

## <a name="turn-on-your-blob-trigger"></a>Blob 트리거 켜기

이제 모니터링할 컨테이너를 만들었으므로 Blob을 만들 때 출력을 볼 수 있도록 함수를 실행해 보겠습니다.

1. Blob 트리거를 선택하여 코드 화면을 엽니다.

1. **실행**을 선택합니다.

## <a name="create-a-blob"></a>Blob 만들기

이제 Blob 트리거가 시작되어 작업을 수신 대기합니다. 로그 메시지를 가져올지 확인하는 Blob을 만들어 보겠습니다.

1. Storage 탐색기에서 **samples-workitems** 컨테이너를 선택합니다.

1. **업로드**를 선택합니다. 

1. **파일 업로드**를 선택합니다.

1. 컴퓨터에서 파일을 선택합니다.

1. **업로드**를 선택합니다.

1. Azure로 돌아갑니다. 로그에서 업로드된 파일을 표시하는 메시지를 확인합니다.

## <a name="clean-up"></a>정리

이 함수에 대해 요금이 청구되지 않도록 하려면 로그 창 위에 있는 **일시 중지**를 선택합니다.

![일시 중지](../media-drafts/4-pause-timer.png)


