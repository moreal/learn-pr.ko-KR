이제 이벤트 허브에 대한 게시자 및 소비자 응용 프로그램을 구성할 준비가 되었습니다.

이 단원에서는 이벤트 허브를 통해 메시지를 보내거나 받도록 이러한 응용 프로그램을 구성합니다. 이러한 응용 프로그램은 GitHub 리포지토리에 저장됩니다.

두 개의 개별 응용 프로그램을 구성합니다. 하나는 메시지 발신자(**SimpleSend**)로 사용되고 다른 하나는 메시지 수신자(**EventProcessorSample**)로 사용됩니다. 이는 브라우저 내에서 모든 작업을 수행할 수 있는 Java 응용 프로그램입니다. 그러나 .NET과 같은 모든 플랫폼에 대한 동일한 구성이 필요합니다.

## <a name="create-a-general-purpose-standard-storage-account"></a>범용 표준 저장소 계정 만들기

이 단원에서 구성하는 Java 수신자 응용 프로그램은 Azure Blob Storage에 메시지를 저장합니다. Blob Storage를 사용하려면 저장소 계정이 필요합니다.

1. 다음 명령을 사용하여 리소스 그룹에서 저장소 계정(범용 V2)을 만듭니다.

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name>  --location <location> --sku Standard_RAGRS --encryption blob
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--name(필수)  |저장소 계정의 이름을 입력합니다.|
    |--resource-group(필수)  |이전 단원에서 만든 리소스 그룹을 입력합니다.|
    |--location(선택)    |이전 단원에서 리소스 그룹을 만드는 데 사용한 위치를 입력합니다.|

1. 다음 명령을 사용하여 저장소 계정과 연결된 모든 액세스 키를 나열합니다.

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--account-name(필수)  |저장소 계정의 이름을 입력합니다.|
    |--resource-group(필수)  |이전 단원에서 만든 리소스 그룹을 입력합니다.|

     저장소 계정과 연결된 액세스 키가 나열됩니다. 나중에 사용할 수 있도록 **key** 값을 복사하고 저장합니다. 저장소 계정에 액세스하려면 이 키가 필요합니다.

1. 다음 명령을 사용하여 저장소 계정의 연결 문자열을 봅니다.

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |-n(필수)  |저장소 계정의 이름을 입력합니다.|
    |-g(필수)  |리소스 그룹의 이름을 입력합니다.|

    이 명령은 저장소 계정의 연결 세부 정보를 반환합니다. **connectionString** 값을 복사하고 저장합니다.

1. 다음 명령을 사용하여 저장소 계정에서 **messages**라는 컨테이너를 만듭니다. 이전 단계에서 복사한 **connectionString**을 사용합니다.

    ```azurecli
    az storage container create -n messages --connection-string "<connection string>"
    ```

## <a name="clone-the-event-hubs-github-repository"></a>Event Hubs GitHub 리포지토리 복제

다음 단계를 사용하여 Event Hubs GitHub 리포지토리를 복제합니다.

1. Azure Cloud Shell(Bash)에 로그인합니다.

1. 이 단원에서 빌드할 응용 프로그램의 원본 파일은 [GitHub 리포지토리](https://github.com/Azure/azure-event-hubs)에 있습니다. 다음 명령을 사용하여 Cloud Shell의 홈 디렉터리에 있는지 확인한 후 이 리포지토리를 복제합니다.

    ```azurecli
    cd ~
    git clone https://github.com/Azure/azure-event-hubs.git
    ```
    리포지토리는 `/home/<username>/azure-event-hubs`에 복제됩니다.

## <a name="use-nano-to-edit-simplesendjava"></a>nano를 사용하여 SimpleSend.java 편집

**nano** 편집기를 사용하여 SimpleSend 응용 프로그램을 편집하고 Event Hubs 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키를 추가합니다. 기본 명령은 편집기 창의 맨 아래에 표시됩니다. 이 단원에서는 Ctrl+O를 사용하여 편집한 내용을 작성하고 Enter 키를 눌러 출력 파일 이름을 확인한 다음, Ctrl+X를 사용하여 편집기를 종료해야 합니다.

1. 다음 명령을 사용하여 **SimpleSend** 폴더로 변경합니다.

    ```azurecli
    cd azure-event-hubs/samples/Java/Basic/SimpleSend/src/main/java/com/microsoft/azure/eventhubs/samples/SimpleSend
    ```

1. 다음 명령을 사용하여 **nano** 편집기에서 **SimpleSend.java** 파일을 엽니다.

    ```azurecli
    nano SimpleSend.java
    ```

1. nano 편집기에서 다음 문자열을 찾아서 바꿉니다.

    - `"Your Event Hubs namespace name"`을 이벤트 허브 네임스페이스의 이름으로 바꿉니다.
    - `"Your event hub"`를 이벤트 허브 이름으로 바꿉니다.
    - `"Your primary SAS key"`를 이전에 저장한 이벤트 허브 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.
    - `"Your policy name"`을 **RootManageSharedAccessKey**로 바꿉니다.
 
        Event Hubs 네임스페이스를 만들 때 **RootManageSharedAccessKey**라는 256비트 SAS 키가 만들어지고, 여기에는 네임스페이스에 대해 전송, 수신 대기 및 관리 권한을 부여하는 연결된 기본 및 보조 키 쌍이 포함됩니다. 이전 단원에서 Azure CLI 명령을 사용하여 키를 표시했고, Azure Portal의 Event Hubs 네임스페이스에 대한 **공유 액세스 정책** 페이지를 열어 이 키를 찾을 수도 있습니다.

    ![발신자 응용 프로그램에 대한 구성 세부 정보](../media-draft/5-sender-configure.png)

1. 다음 명령을 사용하여 **SimpleSend.java**를 저장하고 nano를 종료합니다.

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-simplesendjava"></a>Maven을 사용하여 SimpleSend.java 빌드

이제 **mvn** 명령을 사용하여 Java 응용 프로그램을 빌드합니다.

1. 다음 명령을 사용하여 기본 **SimpleSend** 폴더로 변경합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    ```

1. 다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다. 이렇게 하면 응용 프로그램이 이벤트 허브에 대한 연결 세부 정보를 사용합니다.

    ```azurecli
    mvn clean package -DskipTests
    ```

    빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다. 계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.

    ![발신자 응용 프로그램에 대한 빌드 결과](../media-draft/5-sender-build.png)

## <a name="use-nano-to-edit-eventprocessorsamplejava"></a>nano를 사용하여 EventProcessorSample.java 편집

이벤트 허브에서 데이터를 수집하도록 **수신자**(**구독자** 또는 **소비자**라고도 함) 응용 프로그램을 구성합니다.

수신자 응용 프로그램의 경우 두 개의 메서드인 **EventHubReceiver** 및 **EventProcessorHost**를 사용할 수 있습니다. EventProcessorHost는 EventHubReceiver의 맨 위에 빌드되지만 EventHubReceiver보다 더 단순한 프로그래밍 인터페이스를 제공합니다. EventProcessorHost는 동일한 저장소 계정을 사용하여 EventProcessorHost의 여러 인스턴스에서 자동으로 메시지 파티션을 배포할 수 있습니다.

이 단원에서는 EventProcessorHost 메서드를 사용합니다. 다시 nano를 사용하고 EventProcessorSample 응용 프로그램을 편집하여 Event Hubs 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키, 저장소 계정 이름, 연결 문자열, 컨테이너 이름을 추가합니다.

1. 다음 명령을 사용하여 **EventProcessorSample** 폴더로 변경합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample/src/main/java/com/microsoft/azure/eventhubs/samples/eventprocessorsample
    ```

1. 다음 명령을 사용하여 **nano** 편집기에서 **EventProcessorSample.java** 파일을 엽니다.

    ```azurecli
    nano EventProcessorSample.java
    ```
1. nano 편집기에서 다음 문자열을 찾아서 바꿉니다.

    - `----ServiceBusNamespaceName----`을 Event Hubs 네임스페이스 이름으로 바꿉니다.
    - `----EventHubName----`를 이벤트 허브 이름으로 바꿉니다.
    - `----SharedAccessSignatureKeyName----`을 **RootManageSharedAccessKey**로 바꿉니다.
    - `----SharedAccessSignatureKey----`를 이전에 저장한 Event Hubs 네임스페이스에 대한 **primaryKey** 키 값으로 바꿉니다.
    - `----AzureStorageConnectionString----`을 이전에 저장한 저장소 계정 연결 문자열로 바꿉니다.
    - `----StorageContainerName----`을 **messages**로 바꿉니다.
    - `----HostNamePrefix----`를 저장소 계정 이름으로 바꿉니다.

    ![수신자 응용 프로그램에 대한 구성 세부 정보](../media-draft/5-receiver-configure.png)

1. 다음 명령을 사용하여 **EventProcessorSample.java**를 저장하고 nano를 종료합니다.

    ```azurecli
    CTRL +O
    ENTER
    CTRL +X
    ```

## <a name="use-maven-to-build-eventprocessorsamplejava"></a>Maven을 사용하여 EventProcessorSample.java 빌드

1. 다음 명령을 사용하여 기본 **EventProcessorSample** 폴더로 변경합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    ```

1. 다음 명령을 사용하여 Java SimpleSend 응용 프로그램을 빌드합니다. 이렇게 하면 응용 프로그램이 이벤트 허브에 대한 연결 세부 정보를 사용합니다.

    ```azurecli
    mvn clean package -DskipTests
    ```

    빌드 프로세스를 완료하는 데 몇 분이 걸릴 수 있습니다. 계속하기 전에 **[정보] 빌드 성공** 메시지가 표시되는지 확인합니다.

    ![수신자 응용 프로그램에 대한 빌드 결과](../media-draft/5-receiver-build.png)

## <a name="start-the-sender-and-receiver-apps"></a>발신자 및 수신자 앱 시작

1. **java** 명령을 사용하고 .jar 패키지를 지정하여 명령줄에서 Java 응용 프로그램을 실행합니다. 다음 명령을 사용하여 SimpleSend 응용 프로그램을 시작합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/SimpleSend
    java -jar ./target/simplesend-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. **보내기 완료...** 가 표시되면 Enter 키를 누릅니다.

    ![발신자 응용 프로그램에 대한 실행 결과](../media-draft/5-sender-run.png)

1. 다음 명령을 사용하여 EventProcessorSample 응용 프로그램을 시작합니다.

    ```azurecli
    cd ~
    cd azure-event-hubs/samples/Java/Basic/EventProcessorSample
    java -jar ./target/eventprocessorsample-1.0.0-jar-with-dependencies.jar
    ENTER
    ```

1. 메시지가 콘솔에 표시되는 작업이 중지하면 Enter 키를 누릅니다.

    ![수신자 응용 프로그램에 대한 실행 결과](../media-draft/5-receiver-run.png)

## <a name="summary"></a>요약

이제 이벤트 허브로 메시지를 보낼 수 있도록 발신자 응용 프로그램이 구성되었습니다. 이제 이벤트 허브에서 메시지를 받을 수 있도록 수신자 응용 프로그램이 구성되었습니다.
