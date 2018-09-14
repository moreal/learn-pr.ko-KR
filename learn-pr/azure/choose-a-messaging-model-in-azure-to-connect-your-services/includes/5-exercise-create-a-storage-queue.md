이 연습에서는 Azure 구독에서 새 저장소 계정을 만듭니다. 그런 다음, Azure Cloud Shell을 사용하여 새 큐를 만들고 이 큐에 메시지를 추가한 후 해당 메시지를 읽고 큐에서 제거합니다.

이는 분산 응용 프로그램 내의 구성 요소가 수행하는 것과 동일한 작업입니다. 예를 들어 모바일 앱은 메시지를 큐에 추가할 수 있으며 여기서 웹 서비스가 메시지를 검색하고 처리할 때까지 기다립니다.

## <a name="create-a-storage-account"></a>저장소 계정 만들기

Azure Storage 큐는 Azure 범용 저장소 계정의 일부이므로 먼저 저장소 계정을 만들어야 합니다.

1. 브라우저에서 [Azure Portal](http://portal.azure.com)로 이동하여 기본 자격 증명으로 로그인합니다.
1. 왼쪽 위에서 **모든 서비스**를 클릭합니다.
1. 아래로 스크롤하여 **저장소** 섹션으로 이동한 후 **저장소 계정**을 클릭합니다.
1. **저장소 계정** 블레이드의 왼쪽 위에서 **추가**를 클릭합니다.

    ![추가를 강조 표시한 저장소 계정 블레이드 스크린샷](../images/5-create-a-storage-account-1.png)

1. **이름** 텍스트 상자에 저장소 계정의 고유한 이름을 입력합니다.
1. **배포 모델**에서 **리소스 관리자**가 선택되었는지 확인합니다.
1. **계정 종류** 드롭다운 목록에서 **저장소(범용 v2)** 를 선택합니다.
1. **위치** 드롭다운 목록에서 인근 지역을 선택합니다.
1. **복제** 드롭다운 목록에서 **LRS(로컬 중복 저장소)** 를 선택합니다.
1. **성능**에서 **표준**을 선택합니다.
1. **액세스 계층**에서 **쿨**을 선택합니다.
1. **보안 전송 필요**에서 **사용 안 함**을 선택합니다.
1. **구독** 아래에서 구독을 선택합니다.

    ![저장소 계정 만들기 대화 상자 스크린샷](../images/5-create-a-storage-account-2.png)

1. **리소스 그룹**에서 **새로 만들기**를 선택합니다. 텍스트 상자에 **MusicSharingResourceGroup**을 입력합니다.
1. **가상 네트워크**에서 **사용 안 함**을 선택한 후 **만들기**를 클릭합니다.

    ![만들기를 강조 표시한 저장소 계정 만들기 대화 상자의 스크린샷](../images/5-create-a-storage-account-3.png)

Azure가 새 저장소 계정과 새 리소스 그룹을 만듭니다.

## <a name="create-a-queue"></a>큐 만들기

이제 저장소 계정을 만들었으므로 이 계정에 새 큐를 추가할 수 있습니다. PowerShell 명령을 사용하여 큐를 만들어야 합니다.

1. 포털의 오른쪽 위에서 **Cloud Shell** 링크를 클릭합니다.

    ![Cloud Shell 아이콘을 강조 표시한 Azure Portal 스크린샷](../images/5-create-a-storage-queue-1.png)

1. **Azure Cloud Shell 시작** 화면에서 **PowerShell(Linux)** 을 클릭합니다.
1. **You have no storage mounted**(탑재된 저장소가 없음) 화면이 나타나는 경우 **저장소 만들기**를 클릭합니다.
1. `PS Azure` 프롬프트가 나타날 때 저장소 계정을 얻으려면 다음 명령을 입력합니다. `<storageaccountname>`을 저장소 계정의 고유 이름으로 대체한 후 Enter 키를 누릅니다.

    ```powershell
    $storageaccount = Get-AzureRmStorageAccount -Name <storageaccountname> -ResourceGroup  MusicSharingResourceGroup
    ```

1. 저장소 계정의 컨텍스트를 가져오려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $context = $storageaccount.Context
    ```

1. 새 큐를 만들려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $messageQueue = New-AzureStorageQueue -Name musicsharingmessages -Context $context
    ```

## <a name="add-a-message-to-the-queue"></a>큐에 메시지 추가

이제 저장소 계정에서 큐를 만들었으므로, 이 큐에 메시지를 추가할 수 있습니다.

1. 새 메시지를 작성하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $newSongMessage = New-Object -TypeName Microsoft.WindowsAzure.Storage.Queue.CloudQueueMessage -ArgumentList "A new song has been added."
    ```

1. 새 메시지를 새 큐에 추가하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $messageQueue.CloudQueue.AddMessageAsync($newSongMessage)
    ```

1. Azure Portal의 왼쪽 탐색에서 **모든 리소스**를 클릭합니다.
1. 리소스 목록에서 앞부분에서 만든 저장소 계정을 클릭합니다.
1. 저장소 계정 블레이드에서 **저장소 탐색기(미리 보기)** 를 클릭합니다.
1. 저장소 탐색기의 **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다. 방금 추가한 메시지가 저장소 탐색기에 표시됩니다.

## <a name="retrieve-and-remove-the-message"></a>메시지 검색 및 제거

저장소 큐의 메시지에 대한 대상 구성 요소는 큐의 맨 앞에 있는 메시지를 검색해야 합니다. 그런 다음, 대상 구성 요소는 메시지를 처리하고 다른 구성 요소가 이를 검색하지 않도록 큐에서 삭제해야 합니다.

1. Cloud Shell에서 큐의 맨 앞에 있는 메시지를 가져오려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $retrievedMessage = $messageQueue.CloudQueue.GetMessageAsync().Result
    ```

1. 메시지를 표시하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $retrievedMessage.AsString
    ```

1. 메시지의 모든 속성을 표시하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $retrievedMessage
    ```

1. 큐에서 메시지를 제거하려면 다음 명령을 입력한 후 Enter 키를 누릅니다.

    ```powershell
    $messageQueue.CloudQueue.DeleteMessageAsync($retrievedMessage)
    ```

1. Azure Portal에서 큐 표시를 새로 고치려면 저장소 계정 블레이드로 이동합니다. **개요**를 클릭한 후 **Storage 탐색기**를 클릭합니다.
1. **QUEUES** 아래에서 **musicsharingmessages**를 클릭합니다. 유일한 메시지를 제거했기 때문에, 저장소 탐색기는 큐가 비어 있음을 표시합니다.

## <a name="cleanup"></a>정리

이 연습 중에 생성한 모든 리소스를 제거하려면 Cloud Shell에서 다음 명령을 입력합니다. 
```powershell
Remove-AzureRmResourceGroup -Name "MusicSharingResourceGroup" -Force
```


## <a name="summary"></a>요약

여기서는 Azure 구독에서 저장소 계정을 만들고 이 계정에서 새 큐를 만들었습니다. 또한 PowerShell을 사용하여 큐에 메시지를 추가한 후 이 메시지를 검색 및 제거함으로써 분산 응용 프로그램 구성 요소의 작업을 시뮬레이트했습니다.

저장소 계정 큐는 배포 응용 프로그램의 구성 요소 간에 메시지를 전달하려는 경우에 유용한 솔루션입니다. 이벤트를 게시하려는 경우에는 저장소 큐를 선택하지 마세요.