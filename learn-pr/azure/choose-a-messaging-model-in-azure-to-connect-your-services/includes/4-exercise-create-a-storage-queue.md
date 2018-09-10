이 연습에서는 Azure 구독에서 새 저장소 계정을 만듭니다. 그런 다음, Azure Cloud Shell을 사용하여 새 큐를 만들고 이 큐에 메시지를 추가한 후 해당 메시지를 읽고 큐에서 제거합니다.

이는 분산 응용 프로그램 내의 구성 요소가 수행하는 것과 동일한 작업입니다. 예를 들어 모바일 앱은 메시지를 큐에 추가할 수 있으며 여기서 웹 서비스가 메시지를 검색하고 처리할 때까지 기다립니다.

## <a name="create-a-storage-account"></a>저장소 계정 만들기

Azure Storage 큐는 Azure 범용 저장소 계정의 일부이므로 먼저 저장소 계정을 만들어야 합니다.

1. 브라우저에서 [Azure Portal](https://portal.azure.com?azure-portal=true)로 이동하여 기본 자격 증명으로 로그인합니다.

2. 왼쪽 위에서 **모든 서비스**를 클릭합니다.

3. 아래로 스크롤하여 **저장소** 섹션으로 이동한 후 **저장소 계정**을 클릭합니다.

4. **저장소 계정** 블레이드의 왼쪽 위에서 **추가**를 클릭합니다.

  ![추가를 강조 표시한 저장소 계정 블레이드 스크린샷](../media-draft/4-create-a-storage-account-1.png)

5. 결과 대화 상자에서 다음 정보를 입력하면 포털의 각 옵션에 `(i)` 아이콘이 표시되며, 이 아이콘을 사용하여 옵션의 기능에 대해 자세히 알아볼 수 있습니다.
    - **이름** 텍스트 상자에 저장소 계정의 고유한 이름을 입력합니다.
    - **배포 모델**에서 **Resource Manager**가 선택되었는지 확인합니다.
    - **계정 종류** 드롭다운 목록에서 **저장소(범용 v2)** 를 선택합니다.
    - **위치** 드롭다운 목록에서 인근 지역을 선택합니다.
    - **복제** 드롭다운 목록에서 **LRS(로컬 중복 저장소)** 를 선택합니다.
    - **성능**에서 **표준**을 선택합니다.
    - **액세스 계층**에서 **쿨**을 선택합니다.
    - **보안 전송 필요**에서 **사용 안 함**을 선택합니다.
    - **구독** 아래에서 구독을 선택합니다.
    - **리소스 그룹**에서 **새로 만들기**를 선택합니다. 텍스트 상자에 **MusicSharingResourceGroup**을 입력합니다.
    - **가상 네트워크**에서 **사용 안 함**을 선택합니다. 

    ![저장소 계정 만들기 대화 상자 스크린샷](../media-draft/4-create-a-storage-account-2.png)

6. **만들기**를 클릭하면 Azure가 새 리소스 그룹 및 새 리소스 그룹과 연결된 새 저장소 계정을 만듭니다.

    ![만들기를 강조 표시한 저장소 계정 만들기 대화 상자의 스크린샷](../media-draft/4-create-a-storage-account-3.png)

## <a name="create-a-queue"></a>큐 만들기

이제 저장소 계정을 만들었으므로 이 계정에 새 큐를 추가할 수 있습니다. PowerShell 명령을 사용하여 큐를 만들어야 합니다.

1. 포털의 오른쪽 위에서 **Cloud Shell** 링크 `(>)`를 클릭합니다.

    ![Cloud Shell 아이콘을 강조 표시한 Azure Portal 스크린샷](../media-draft/4-create-a-storage-queue-1.png)

2. **Azure Cloud Shell 시작** 화면에서 **PowerShell(Linux)** 을 클릭합니다.

3. **You have no storage mounted**(탑재된 저장소가 없음) 화면이 나타나는 경우 **저장소 만들기**를 클릭합니다.

4. `PS Azure` 프롬프트가 나타날 때 저장소 계정을 얻으려면 다음 명령을 입력합니다. `<storageaccountname>`을 위에서 만든 저장소 계정의 고유 이름으로 바꾸고 **Enter** 키를 누릅니다. 결과 개체를 `$storageaccount`라는 변수에 할당해야 합니다.

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

5. 다음으로 저장소 계정 _컨텍스트_를 가져와야 하는데, 이것은 반환된 개체의 속성입니다. `$context`라는 다른 변수에 할당하겠습니다.

    ```powershell
    $context = $storageaccount.Context
    ```

6. 이제 큐를 만들 준비가 완료되었습니다. `New-AzureStorageQueue` 명령을 사용하여 `$messageQueue` 변수에 할당합니다.
    - `musicsharingmessages` 값을 사용하여 `-Name` 매개 변수를 전달합니다.
    - 이전 단계에서 검색한 값을 사용하여 `-Context` 매개 변수를 전달합니다.

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>큐에 메시지 추가

이제 저장소 계정에서 큐를 만들었으므로, 이 큐에 메시지를 추가할 수 있습니다.

1. 새 메시지를 만들려면 `New-Object` 메서드를 사용하여 문자열 기반 인수로 .NET `CloudQueueMessage`를 만듭니다.

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

2. 새 메시지를 새 큐에 추가하려면 앞에서 만든 `CloudQueueMessage`를 `$messageQueue` 큐의 `AddMessageAsync` 메서드에 전달합니다.

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

## <a name="verify-the-message-was-queued"></a>메시지가 큐에 추가되었는지 확인

**Storage 탐색기**를 사용하여 큐를 작업할 수 있습니다. 다음과 같은 두 가지 변형을 사용할 수 있습니다.

- 다운로드할 수 있는 Linux, macOS 및 Windows용 플랫폼 간 데스크톱 앱.
- Azure Portal의 미리 보기 웹 버전. 여기서는 이 방법을 사용하지만, 원한다면 데스크톱 버전을 설치해도 되며 설치 방법도 매우 간단합니다.

1. Azure Portal의 왼쪽 탐색에서 **모든 리소스**를 클릭합니다.

2. 리소스 목록에서 앞부분에서 만든 저장소 계정을 클릭합니다.

3. 저장소 계정 블레이드에서 **저장소 탐색기(미리 보기)** 를 클릭합니다.

4. 저장소 탐색기의 **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다. 방금 추가한 메시지가 Storage 탐색기에 표시됩니다.

## <a name="retrieve-and-remove-the-message"></a>메시지 검색 및 제거

저장소 큐의 메시지에 대한 대상 구성 요소는 큐의 맨 앞에 있는 메시지를 검색해야 합니다. 그런 다음, 대상 구성 요소는 메시지를 처리하고 다른 구성 요소가 이를 검색하지 않도록 큐에서 삭제해야 합니다.

1. 큐에서 `GetMessageAsync` 메서드를 사용하여 PowerShell의 첫 번째 사용 가능 메시지를 검색할 수 있습니다. 이것은 비동기 .NET 메서드입니다. `Result` 속성을 사용하여 반환 값을 가져올 수 있을 때까지 기다려야 하기 때문입니다. 이렇게 하면 매개 변수에 할당할 수 있는 메시지를 나타내는 개체가 반환됩니다.

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

2. `AsString`을 호출하여 메시지의 텍스트 버전을 얻을 수 있으며, 콘솔에 값이 출력됩니다.

    ```powershell
    $retrievedMessage.AsString
    ```

3. 또는 간단하게 변수 이름을 입력하고 **Enter** 키를 눌러서 메시지의 모든 속성을 표시할 수 있습니다.

    ```powershell
    $retrievedMessage
    ```

4. `GetMessageAsync`는 메시지를 제거하지 *않고* 단순히 반환합니다. 즉, 메시지를 다시 처리할 수는 있다는 뜻입니다. 큐에서 메시지를 제거하려면 큐에서 `DeleteMessageAsync` 메서드를 사용하면 됩니다. 이렇게 하려면 제거하려는 메시지를 전달해야 합니다.

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

5. 메시지가 사라졌는지 확인하려면 Storage 계정 블레이드로 이동한 후 **개요 > Storage 탐색기**를 선택하여 Azure Portal에서 큐 표시를 새로 고칩니다. **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다. 유일한 메시지를 제거했기 때문에, Storage 탐색기는 큐가 비어 있다고 표시합니다.


## <a name="summary"></a>요약
저장소 계정 큐는 배포 응용 프로그램의 구성 요소 간에 _메시지_를 전달하려는 경우에 유용한 솔루션입니다. 전송을 보장하거나 보낸 순서대로 메시지가 전송되게 만들려는 경우에 적합한 선택입니다. 그러나 큐는 발신자와 수신자가 전달되는 데이터의 형식을 이해함을 나타내며, 발신자와 수신자 사이에는 통신 서비스 간에 약간의 "결합"을 추가하는 암시적 데이터 계약이 있습니다.

모든 아키텍처가 포맷된 데이터 블록을 전달할 필요는 없으며, 일부 아키텍처는 메시지 처리 방법을 알 필요 없이 파이어 앤 포켓 방식의 간단한 메시지만 필요합니다. 이러한 시나리오에서는 큐가 적합하지 않습니다. 이 유형의 통신과 잘 어울리는 다른 메시지 전략을 살펴보겠습니다.