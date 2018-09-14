이제 새 이벤트 허브를 만들 준비가 되었습니다. 이벤트 허브를 만든 후 Azure Portal을 사용하여 새 허브를 표시합니다.

Azure CLI를 사용하여 이벤트 허브를 만듭니다. 이 연습에서는 Azure CLI 2.0을 사용합니다. 

## <a name="create-an-event-hubs-namespace"></a>Event Hubs 네임스페이스 만들기

[!include[](../../../includes/azure-sandbox-activate.md)]

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Azure Cloud shell에서 지원 되는 bash 셸을 사용 하 여 Event Hubs 네임 스페이스를 만들려면 다음 단계를 사용 합니다.

1. 다음 명령을 사용하여 Event Hubs 네임스페이스를 만듭니다.

    ```azurecli
        az eventhubs namespace create --name <Event Hubs namespace name> --resource-group <rgn>[Sandbox resource group name]</rgn> -l <location>
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--name(필수)      |Event Hubs 네임스페이스에 대한 6-50자 길이의 고유한 이름을 입력합니다. 이 이름에는 문자, 숫자 및 하이픈만 포함해야 합니다. 문자로 시작해야 하고 문자 또는 숫자로 끝나야 합니다.|
    |--resource-group(필수)  |1단계에서 만든 리소스 그룹을 입력합니다.
    |--l(선택 사항)     |가장 가까운 Azure 데이터 센터의 위치를 입력합니다(예: westus).|

1. 다음 명령을 사용하여 Event Hubs 네임스페이스에 대한 연결 문자열을 페치합니다. 이벤트 허브를 사용하여 메시지를 보내고 받도록 응용 프로그램을 구성하려면 필요합니다.

    ```azurecli
        az eventhubs namespace authorization-rule keys list --resource-group <rgn>[Sandbox resource group name]</rgn> --namespace-name <EventHub namespace name> --name RootManageSharedAccessKey
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--resource-group(필수)  |1단계에서 만든 리소스 그룹을 입력합니다.|
    |--namespace-name(필수)      |2단계에서 만든 네임스페이스를 입력합니다.|

    이 명령은 나중에 게시자 및 소비자 응용 프로그램을 구성하는 데 사용할 Event Hubs 네임스페이스에 대한 연결 문자열을 반환합니다. 나중에 사용할 수 있도록 다음 키의 값을 저장합니다.

    - **primaryConnectionString**
    - **primaryKey**

## <a name="create-an-event-hub"></a>이벤트 허브 만들기

다음 단계에 따라 새 이벤트 허브를 만듭니다.

1. 다음 명령을 사용하여 새 이벤트 허브를 만듭니다.

    ```azurecli
        az eventhubs eventhub create --name <event hub name> --resource-group <rgn>[Sandbox resource group name]</rgn> --namespace-name <Event Hubs namespace name>
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--name(필수)  |이벤트 허브 이름을 입력합니다.|
    |--resource-group(필수)  |이전 절차에서 만든 리소스 그룹을 입력합니다.|
    |--namespace-name(필수)      |이전 절차에서 만든 네임스페이스를 입력합니다.|

1. 다음 명령을 사용하여 이벤트 허브의 세부 정보를 봅니다. 

    ```azurecli
        az eventhubs eventhub show --resource-group <rgn>[Sandbox resource group name]</rgn> --namespace-name <Event Hubs namespace name> --name <event hub name>
    ```

    |매개 변수      |설명|
    |---------------|-----------|
    |--resource-group(필수)  |이전 절차에서 만든 리소스 그룹을 입력합니다.|
    |--namespace-name(필수)      |이전 절차에서 만든 네임스페이스를 입력합니다.|
    |--name(필수)|1단계에서 만든 이벤트 허브의 이름을 입력합니다.|

## <a name="view-the-event-hub-in-the-azure-portal"></a>Azure Portal에서 이벤트 허브 보기

다음 단계를 수행하여 Azure Portal에서 이벤트 허브를 봅니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)의 위쪽에 있는 검색 창을 사용하여 Event Hubs 네임스페이스를 찾습니다.

1. 네임스페이스를 클릭하여 엽니다.

1. **Event Hubs 네임스페이스** > **엔터티**에서 **Event Hubs**를 클릭합니다.
    이벤트 허브에 대한 **활성** 상태와 기본값 **메시지 보존**(*7*) 및 **파티션 개수**(*4*)가 표시됩니다.

    ![Azure Portal에 표시된 이벤트 허브](../media-draft/3-event-hub.png)

## <a name="summary"></a>요약

이제 새 이벤트 허브를 만들었으며 게시자 및 소비자 응용 프로그램을 구성하는 데 필요한 모든 정보가 준비되었습니다.
