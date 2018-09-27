이제 새 Event Hub를 만들 준비가 되었습니다. Event Hub를 만든 후 Azure Portal을 사용하여 새 허브를 표시합니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="set-some-defaults-in-the-azure-cli"></a>Azure CLI에서 일부 기본값 설정

Cloud Shell에서 Azure CLI에 대한 일부 기본 값을 제공하는 것으로 시작하겠습니다. 이렇게 하면 매번 입력하지 않아도 됩니다. 특히 _리소스 그룹_ 및 _위치_를 설정합니다. 다음 목록에서 위치를 선택합니다.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

그런 다음, Azure CLI로 다음 명령을 입력하여 가까운 위치로 바꿉니다.

```azurecli
az configure --defaults group=<rgn>[sandbox Resource Group]</rgn> location=westus2
```

## <a name="create-an-event-hubs-namespace"></a>Event Hubs 네임스페이스 만들기

다음 단계를 수행하여 Azure Cloud Shell에서 지원하는 bash 셸을 사용하여 Event Hubs 네임스페이스를 만듭니다.

1. `az eventhubs namespace create` 명령을 사용하여 Event Hubs 네임스페이스를 만듭니다. 다음 매개 변수를 사용합니다.

    > [!div class="mx-tableFixed"]
    > |매개 변수      |설명|
    > |---------------|-----------|
    > |--name(필수)      |Event Hubs 네임스페이스에 대한 6-50자 길이의 고유한 이름을 입력합니다. 이 이름에는 문자, 숫자 및 하이픈만 포함해야 합니다. 문자로 시작해야 하고 문자 또는 숫자로 끝나야 합니다.|
    > |--resource-group(필수) | 이 이름은 기본값에서 제공되는 미리 만들어진 Azure 샌드박스 리소스 그룹입니다. |
    > |--l(선택 사항)     |가장 가까운 Azure 데이터 센터의 위치를 입력합니다(기본값이 사용됨).|
    > |--sku(선택 사항) | 네임스페이스의 가격 책정 계층[기본 | 표준]은 기본값이 _표준_입니다. 이는 연결 및 소비자 임계값을 결정합니다. |

    재사용할 수 있도록 이름을 환경 변수로 설정합니다.

    ```azurecli
    NS_NAME=myEvt-HubNs1
    ````

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

    ```azurecli
    az eventhubs namespace create --name $NS_NAME
    ```

    > [!NOTE]
    > Azure는 이름에 대해 매우 까다로우며 CLI에서 이름이 존재하거나 유효하지 않은 경우 **잘못된 요청**을 반환합니다. 환경 변수를 변경하고 명령을 다시 실행하여 다른 이름을 지정합니다.


1. 다음 명령을 사용하여 Event Hubs 네임스페이스에 대한 연결 문자열을 페치합니다. Event Hub를 사용하여 메시지를 보내고 받도록 응용 프로그램을 구성하려면 이 작업이 필요합니다.

    ```azurecli
    az eventhubs namespace authorization-rule keys list --name RootManageSharedAccessKey --namespace-name $NS_NAME
    ```

    > [!div class="mx-tableFixed"]
    > |매개 변수      |설명|
    > |---------------|-----------|
    > |--resource-group(필수)  | 이 이름은 기본값에서 제공되는 미리 만들어진 Azure 샌드박스 리소스 그룹입니다. |
    > |--namespace-name(필수)  | 만든 네임스페이스의 이름을 입력합니다. |

    이 명령은 나중에 게시자 및 소비자 응용 프로그램을 구성하는 데 사용할 Event Hubs 네임스페이스에 대한 연결 문자열이 포함된 JSON 블록을 반환합니다. 나중에 사용할 수 있도록 다음 키의 값을 저장합니다.

    - **primaryConnectionString**
    - **primaryKey**

## <a name="create-an-event-hub"></a>Event Hub 만들기

다음 단계에 따라 새 Event Hub를 만듭니다.

1. `eventhub create` 명령을 사용하여 새 Event Hub를 만듭니다. 다음 매개 변수가 필요합니다.

    > [!div class="mx-tableFixed"]
    > |매개 변수      |설명|
    > |---------------|-----------|
    > |--name(필수)  |Event Hub 이름을 입력합니다.|
    > |--resource-group(필수)  |리소스 그룹 소유자.|
    > |--namespace-name(필수)      |만든 네임스페이스를 입력합니다.|

    먼저 환경 변수에 Event Hub 이름을 정의해 보겠습니다.

    ```azurecli
    HUB_NAME=[name]
    ```

    ```azurecli
    az eventhubs eventhub create --name $HUB_NAME --namespace-name $NS_NAME
    ```

1. `eventhub show` 명령을 사용하여 Event Hub의 세부 정보를 봅니다. 다음을 수행합니다.

    > [!div class="mx-tableFixed"]
    > |매개 변수      |설명|
    > |---------------|-----------|
    > |--resource-group(필수)  |리소스 그룹 소유자.|
    > |--namespace-name(필수)      |만든 네임스페이스를 입력합니다.|
    > |--name(필수)|Event Hub의 이름입니다.|

    ```azurecli
    az eventhubs eventhub show --namespace-name $NS_NAME --name $HUB_NAME
    ```

## <a name="view-the-event-hub-in-the-azure-portal"></a>Azure Portal에서 Event Hub 보기

그런 다음, Azure Portal에서 어떻게 표시하는지 확인해 보겠습니다.

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 포털의 위쪽에 있는 검색 창을 사용하여 Event Hubs 네임스페이스를 찾습니다.

1. 네임스페이스를 선택하여 엽니다.

1. **엔터티** 섹션 아래에서 **Event Hubs 네임스페이스**를 선택합니다.

1. **Event Hubs**를 클릭합니다.

    Event Hub에 대한 **활성** 상태와 기본값 **메시지 보존**(*7*) 및 **파티션 개수**(*4*)가 표시됩니다.

    ![Azure Portal에 표시된 Event Hub](../media/3-event-hub.png)

## <a name="summary"></a>요약

이제 새 Event Hub를 만들었으며 게시자 및 소비자 응용 프로그램을 구성하는 데 필요한 모든 정보가 준비되었습니다.
