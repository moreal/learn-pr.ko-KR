이제 Event Hub에 대한 게시자 및 소비자 응용 프로그램을 구성할 준비가 되었습니다.

이 단원에서는 Event Hub를 통해 메시지를 보내거나 받도록 이러한 응용 프로그램을 구성하겠습니다. 이러한 응용 프로그램은 GitHub 리포지토리에 저장됩니다.

두 개의 개별 응용 프로그램을 구성합니다. 하나는 메시지 발신자(**SimpleSend**)로 사용되고 다른 하나는 메시지 수신자(**EventProcessorSample**)로 사용됩니다. 이는 브라우저 내에서 모든 작업을 수행할 수 있는 Java 응용 프로그램입니다. 그러나 .NET과 같은 모든 플랫폼에 대한 동일한 구성이 필요합니다.

## <a name="create-a-general-purpose-standard-storage-account"></a>범용 표준 저장소 계정 만들기

이 단원에서 구성하는 Java 수신자 응용 프로그램은 Azure Blob Storage에 메시지를 저장합니다. Blob Storage를 사용하려면 저장소 계정이 필요합니다.

1. `storage account create` 명령을 사용하여 저장소 계정(범용 V2)을 만듭니다. 기본 리소스 그룹 및 위치를 설정했으므로 해당 매개 변수가 일반적으로 _필요_하더라도 해제한 상태로 유지해도 됩니다.

    |매개 변수      |설명|
    |---------------|-----------|
    |--name(필수)  | 저장소 계정의 이름입니다. |
    |--resource-group(필수)  |리소스 그룹 소유자입니다. 미리 생성된 샌드박스 리소스 그룹을 사용하겠습니다.|
    |--location(선택 사항)    |특정 위치 및 리소스 그룹 위치에서 저장소 계정을 사용하려는 경우 선택 사항 위치입니다.|

    저장소 계정 이름을 변수로 설정합니다. 하이픈 구분 기호가 허용되고 모든 소문자, 숫자로 구성되어야 합니다. 또한 Azure 내에서 고유해야 합니다.

    ```azurecli
    STORAGE_NAME=[name]
    ```

    그런 다음, 이 명령을 사용하여 저장소 계정을 만듭니다.

    ```azurecli
    az storage account create --name $STORAGE_NAME --sku Standard_RAGRS --encryption blob
    ```

    > [!TIP]
    > 저장소 계정 만들기에 실패하면 환경 변수를 변경하고 다시 시도하세요.

1. `account keys list` 명령을 사용하여 저장소 계정과 연결된 모든 액세스 키를 나열합니다. 사용자 계정 이름 및 리소스 그룹을 사용합니다(기본 설정됨).

    ```azurecli
    az storage account keys list --account-name $STORAGE_NAME
    ```

     저장소 계정과 연결된 액세스 키가 나열됩니다. 나중에 사용할 수 있도록 **key** 값을 복사하고 저장합니다. 저장소 계정에 액세스하려면 이 키가 필요합니다.

1. 다음 명령을 사용하여 저장소 계정의 연결 문자열을 봅니다.

    ```azurecli
    az storage account show-connection-string -n $STORAGE_NAME
    ```

    이 명령은 저장소 계정의 연결 세부 정보를 반환합니다. **connectionString** _값_을 복사하고 저장합니다. 다음과 같이 표시됩니다.

    ```output
    "DefaultEndpointsProtocol=https;EndpointSuffix=core.windows.net;AccountName=storage_account_name;AccountKey=VZjXuMeuDqjCkT60xX6L5fmtXixYuY2wiPmsrXwYHIhwo736kSAUAj08XBockRZh7CZwYxuYBPe31hi8XfHlWw=="
    ```

1. 다음 명령을 사용하여 저장소 계정에서 **messages**라는 컨테이너를 만듭니다. 이전 단계에서 복사한 **connectionString**을 사용합니다.

    ```azurecli
    az storage container create -n messages --connection-string "<connection string here>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a>Event Hubs GitHub 리포지토리 복제

`git`를 사용하여 Event Hubs GitHub 리포지토리를 복제하려면 다음 단계를 사용합니다. 이 권한을 Cloud Shell에서 실행할 수 있습니다.

1. 이 단원에서 빌드할 응용 프로그램의 원본 파일은 [GitHub 리포지토리](https://github.com/Azure/azure-event-hubs)에 위치합니다. 다음 명령을 사용하여 Cloud Shell의 홈 디렉터리에 있는지 확인한 다음, 다음 리포지토리를 복제합니다.

    ```bash
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    리포지토리는 홈 폴더에 복제됩니다.

## <a name="edit-simplesendjava"></a>SimpleSend.java 편집

기본 제공 Cloud Shell 코드 편집기를 사용하겠습니다. Monaco 편집기를 기반으로 하며, Visual Studio Code와 비슷하지만 완전히 온라인 상태입니다.

편집기를 사용하여 SimpleSend 응용 프로그램을 수정하고 Event Hubs 네임스페이스, Event Hub 이름, 공유 액세스 정책 이름 및 기본 키를 추가합니다. 주요 명령은 편집기 창의 맨 아래에 표시됩니다. 

<kbd>Ctrl+O</kbd>를 사용하여 편집한 내용을 작성한 다음, <kbd>ENTER</kbd> 키를 눌러 출력 파일 이름을 확인하고, <kbd>Ctrl+X</kbd>를 사용하여 편집기를 종료해야 합니다. 편집기에는 모든 편집 명령의 위쪽/오른쪽 모서리에서 "..." 메뉴도 있습니다.

1. **SimpleSend** 폴더로 변경합니다

    ```bash
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. 현재 폴더에서 코드 편집기를 엽니다. 그러면 왼쪽에 있는 파일의 목록 및 오른쪽에 있는 편집기 공간을 표시합니다.

    ```bash
    code .
    ```

1. 파일 목록에서 **SimpleSend.java** 파일을 선택하여 엽니다.

1. 편집기에서 다음 문자열을 찾아서 바꿉니다.

    - `"Your Event Hubs namespace name"`을 Event Hub 네임스페이스의 이름으로 바꿉니다.
    - `"Your Event Hub"`를 Event Hub 이름으로 바꿉니다.
    - `"Your policy name"`을 **RootManageSharedAccessKey**로 바꿉니다.
    - `"Your primary SAS key"`를 이전에 저장한 Event Hub 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.
 
    > [!TIP]
    > 터미널 창과 달리 편집기는 OS에서 일반적인 복사/붙여넣기 키보드 액셀러레이터 키를 사용할 수 있습니다.

    일부 작업을 잊은 경우 편집기 아래에 있는 터미널 창으로 전환하고 `echo` 명령을 사용하여 환경 변수 중 하나를 나열할 수 있습니다. 예:

    ```bash
    echo $NS_NAME
    ```
    Event Hubs 네임스페이스를 만들 때 **RootManageSharedAccessKey**라는 256비트 SAS 키가 만들어지고, 여기에는 네임스페이스에 대해 전송, 수신 대기 및 관리 권한을 부여하는 연결된 기본 키 및 보조 키 쌍이 포함됩니다. 이전 단원에서 Azure CLI 명령을 사용하여 키를 표시했으므로 Azure Portal의 Event Hubs 네임스페이스에 대한 **공유 액세스 정책** 페이지를 열어 이 키를 찾을 수도 있습니다.

1. "..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 **SimpleSend.java**를 저장합니다.

1. "..." 메뉴 또는 액셀러레이터 키(<kbd>CTRL+Q</kbd>)를 통해 편집기를 닫습니다.

## <a name="use-maven-to-build-simplesendjava"></a>Maven을 사용하여 SimpleSend.java 빌드

이제 **mvn** 명령을 사용하여 Java 응용 프로그램을 빌드하겠습니다.

1. 기본 **SimpleSend** 폴더로 다시 변경합니다.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. Java SimpleSend 응용 프로그램을 빌드합니다. 이렇게 하면 응용 프로그램이 Event Hub에 대한 연결 세부 정보를 사용합니다.

    ```bash
    mvn clean package -DskipTests
    ```

    빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다. 계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.

    ![발신자 응용 프로그램에 대한 빌드 결과](../media/5-sender-build.png)

## <a name="edit-eventprocessorsamplejava"></a>EventProcessorSample.java 편집

Event Hub에서 데이터를 수집하도록 **수신자**(**구독자** 또는 **소비자**라고도 함) 응용 프로그램을 구성하겠습니다.

수신자 응용 프로그램의 경우 **EventHubReceiver** 및 **EventProcessorHost**라는 두 개의 메서드를 사용할 수 있습니다. EventProcessorHost는 EventHubReceiver의 맨 위에 빌드되지만 EventHubReceiver보다 더 단순한 프로그래밍 인터페이스를 제공합니다. EventProcessorHost는 동일한 저장소 계정을 사용하여 EventProcessorHost의 여러 인스턴스에서 자동으로 메시지 파티션을 배포할 수 있습니다.

이 단원에서는 EventProcessorHost 메서드를 사용하겠습니다. EventProcessorSample 응용 프로그램을 편집하여 Event Hubs 네임스페이스, Event Hub 이름, 공유 액세스 정책 이름 및 기본 키, 저장소 계정 이름, 연결 문자열, 컨테이너 이름을 추가합니다.

1. 다음 명령을 사용하여 **EventProcessorSample** 폴더로 변경합니다.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. 코드 편집기를 엽니다.

    ```bash
    code .
    ```
    
1. **EventProcessorSample.java** 파일을 선택합니다

1. 편집기에서 다음 문자열을 찾아서 바꿉니다.

    - `----ServiceBusNamespaceName----`을 Event Hubs 네임스페이스 이름으로 바꿉니다.
    - `----EventHubName----`를 Event Hub 이름으로 바꿉니다.
    - `----SharedAccessSignatureKeyName----`을 **RootManageSharedAccessKey**로 바꿉니다.
    - `----SharedAccessSignatureKey----`를 이전에 저장한 Event Hubs 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.
    - `----AzureStorageConnectionString----`을 이전에 저장한 저장소 계정 연결 문자열로 바꿉니다.
    - `----StorageContainerName----`을 **messages**로 바꿉니다.
    - `----HostNamePrefix----`를 저장소 계정 이름으로 바꿉니다.

1. "..." 메뉴 또는 액셀러레이터 키(Windows 및 Linux에서는 <kbd>Ctrl+S</kbd>, macOS에서는 <kbd>Cmd+S</kbd>)를 통해 **EventProcessorSample.java**를 저장합니다.

1. 편집기를 닫습니다.

## <a name="use-maven-to-build-eventprocessorsamplejava"></a>Maven을 사용하여 EventProcessorSample.java 빌드

1. 다음 명령을 사용하여 기본 **EventProcessorSample** 폴더로 변경합니다.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. 다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다. 이렇게 하면 응용 프로그램이 Event Hub에 대한 연결 세부 정보를 사용합니다.

    ```bash
    mvn clean package -DskipTests
    ```

    빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다. 계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.

    ![수신자 응용 프로그램에 대한 빌드 결과](../media/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a>발신자 및 수신자 앱 시작

1. **java** 명령을 사용하고 .jar 패키지를 지정하여 명령줄에서 Java 응용 프로그램을 실행합니다. 다음 명령을 사용하여 SimpleSend 응용 프로그램을 시작합니다.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ```

1. **보내기 완료...** 가 표시되면 <kbd>ENTER</kbd> 키를 누릅니다.

    ```output
    jar-with-dependencies.jar
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    2018-09-18T19:42:15.146Z: Send Complete...
    ```

1. 다음 명령을 사용하여 EventProcessorSample 응용 프로그램을 시작합니다.

    ```bash
    cd ~/azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ```

1. 메시지가 콘솔에 표시되지 않으면 <kbd>ENTER</kbd> 키나 <kbd>CTRL+C</kbd>를 눌러서 프로그램을 종료합니다.

    ```output
    ...
    SAMPLE: Partition 0 checkpointing at 1064,19
    SAMPLE (3,1120,20): "Message 80"
    SAMPLE (3,1176,21): "Message 84"
    SAMPLE (3,1232,22): "Message 88"
    SAMPLE (3,1288,23): "Message 92"
    SAMPLE (3,1344,24): "Message 96"
    SAMPLE: Partition 3 checkpointing at 1344,24
    SAMPLE (2,1120,20): "Message 83"
    SAMPLE (2,1176,21): "Message 87"
    SAMPLE (2,1232,22): "Message 91"
    SAMPLE (2,1288,23): "Message 95"
    SAMPLE (2,1344,24): "Message 99"
    SAMPLE: Partition 2 checkpointing at 1344,24
    SAMPLE: Partition 1 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE (0,1120,20): "Message 81"
    SAMPLE (0,1176,21): "Message 85"
    SAMPLE: Partition 0 batch size was 10 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 got event batch
    SAMPLE (0,1232,22): "Message 89"
    SAMPLE (0,1288,23): "Message 93"
    SAMPLE (0,1344,24): "Message 97"
    SAMPLE: Partition 0 checkpointing at 1344,24
    SAMPLE: Partition 3 batch size was 8 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 2 batch size was 9 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    SAMPLE: Partition 0 batch size was 3 for host mystorageacct2018-46d60a17-7060-4b53-b0e0-cca70c970a47
    ```

## <a name="summary"></a>요약

이제 Event Hub로 메시지를 보낼 수 있도록 발신자 응용 프로그램이 구성되었습니다. 이제 Event Hub에서 메시지를 받을 수 있도록 수신자 응용 프로그램이 구성되었습니다.