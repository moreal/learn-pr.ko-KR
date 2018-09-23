Azure Redis Cache 인스턴스를 만든 다음, 이 캐시에 두 개의 데이터 값을 삽입하는 간단한 트랜잭션을 만들어 보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Azure Redis Cache 만들기

먼저 Azure CLI를 사용하여 Azure Redis Cache를 만들겠습니다. 브라우저 창의 오른쪽에서 Cloud Shell을 사용하여 Azure와 상호작용합니다.

`az redis create` 명령을 사용하여 새 Azure Redis Cache를 만들 것입니다. 여러 매개 변수가 사용됩니다. 다음은 가장 일반적인 매개 변수입니다(전체 목록은 설명서 확인).

> [!div class="mx-tableFixed"]
> | 매개 변수 | 설명 |
> |-----------|-------------|
> | `--name`    | 캐시 이름 - 전역적으로 고유해야 하며 문자, 숫자, 대시로 구성됩니다. |
> | `--resource-group` | Azure 샌드박스의 일부인 미리 생성된 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 리소스 그룹을 사용합니다. |
> | `--location` | 캐시를 배치할 위치를 지정합니다. 일반적으로 데이터 소비자와 가까운 위치를 선택합니다. 이 예에서는 Azure 샌드박스에서 사용할 수 있는 위치로 제한됩니다. 가장 가까운 위치를 선택합니다. |
> | `--size` | Azure Redis Cache의 크기입니다. 유효한 값은 [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4]입니다. |
> | `--sku` | Azure Redis Cache SKU입니다. 유효한 값은 [기본, 표준, 프리미엄]입니다. |

### <a name="select-a-location"></a>위치 선택
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. 다음 옵션을 사용하여 캐시를 만듭니다.
    - 크기: C0
    - SKU: 기본

1. 명령줄 예는 다음과 같습니다. `[name]` 매개 변수를 고유한 이름으로 바꿔야 합니다. 미국 동부 대신 다른 지역을 원하는 경우 위치를 바꾸면 됩니다.

    ```azurecli
    REDIS_NAME=[name]

    az redis create \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location eastus \
        --vm-size C0 \
        --sku Basic \
    ```

## <a name="create-a-net-core-console-application"></a>.NET Core 콘솔 응용 프로그램 만들기

다음으로, Azure Redis Cache에 데이터 값을 삽입하는 데 사용할 .NET Core 콘솔 응용 프로그램을 만듭니다.

1. 창 오른쪽의 통합 Cloud Shell을 사용하여 새 .NET Core 응용 프로그램을 만듭니다. 이름을 "RedisData"로 지정합니다.

    ```bash
    cd ~
    dotnet new console --name RedisData
    ```

1. 앱에 대해 만든 새 디렉터리로 변경합니다.

    ```bash
    cd RedisData
    ```

1. 응용 프로그램을 빌드하고 실행하면 "Hello World!"가 출력됩니다.

    ```bash
    dotnet run
    ```

## <a name="add-the-servicestackredis-nuget-package"></a>ServiceStack.Redis NuGet 패키지 추가

콘솔 응용 프로그램이 생겼으니, **ServiceStack.Redis** NuGet 패키지를 추가해야 합니다. 그러면 Azure Redis Cache에 연결하고 C#에서 명령을 실행할 수 있습니다.

1. 터미널 셸을 사용하여 NuGet 패키지 **ServiceStack.Redis**를 추가합니다.

    ```bash
    dotnet add package ServiceStack.Redis
    ```

1. 응용 프로그램을 다시 빌드하고 실행하여 모두 컴파일되는지 확인합니다. 여전히 "Hello World!"가 출력되어야 합니다.

## <a name="get-your-azure-redis-cache-connection-string"></a>Azure Redis Cache 연결 문자열 가져오기

Azure Redis Cache에 연결하려면 암호 및 URL을 포함하고 있는 연결 문자열이 필요합니다. **ServiceStack.Redis**는 `[password]@[hostname]:[sslport]?ssl=true` 형식의 고유한 연결 문자열을 갖고 있습니다.

Azure Portal 또는 명령줄을 사용하여 암호를 검색할 수 있습니다. "Redis로 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화"에서 포털을 사용했으니, 여기서는 명령줄을 사용하겠습니다.

`az redis list-keys` 명령을 사용하여 액세스 키를 가져옵니다. 다음 명령을 실행하여 기본 키를 가져오고, `REDIS_KEY` 변수에 저장하고, 표시합니다.

```azurecli
REDIS_KEY=$(az redis list-keys \
    --name "$REDIS_NAME" \
    --resource-group <rgn>[Sandbox resource group name]</rgn> \
    --query primaryKey \
    --output tsv)

echo $REDIS_KEY
```

다음으로, 이 명령을 실행하여 연결 문자열을 결합하 고 명령줄에 표시합니다. 호스트 이름은 `.redis.cache.windows.net` 다음의 캐시 이름이고, 포트는 기본 Redis SSL 포트인 **6380**입니다.

```bash
echo "$REDIS_KEY"@"$REDIS_NAME".redis.cache.windows.net:6380?ssl=true
```

다음 단계에서 사용할 연결 문자열을 &mdash; 클립보드에 복사합니다.

## <a name="add-the-connection-string-to-your-app"></a>앱에 연결 문자열 추가

1. 응용 프로그램 폴더에서 Cloud Shell 편집기를 엽니다.

    ```bash
    cd ~/RedisData
    code .
    ```

1. **Program.cs** 소스 파일을 선택합니다.

1. `Program` 클래스에 다음 필드를 만들고 연결 문자열에 값으로 붙여넣습니다.

    ```csharp
    static string redisConnectionString = "<connection string>";
    ```

    예를 들면 다음과 같습니다.

    ```csharp
    static string redisConnectionString = "ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6380?ssl=true";
    ```

## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Azure Redis Cache에 두 개의 데이터 값을 삽입

마지막으로, Azure Redis Cache에 데이터를 추가하겠습니다.

1. **Program.cs** 파일 위쪽에 다음 `using` 문을 추가합니다.

    ```csharp
    using ServiceStack.Redis;
    ```

1. `Main` 메서드의 콘텐츠를 다음 코드로 바꿉니다. 이렇게 하면 트랜잭션을 사용하여 두 값을 추가합니다.

    ```csharp
    bool transactionResult = false;

    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    using (var transaction = redisClient.CreateTransaction())
    {
        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        transactionResult = transaction.Commit();
    }

    if (transactionResult)
    {
        Console.WriteLine("Transaction committed");
    }
    else
    {
        Console.WriteLine("Transaction failed to commit");
    }
    ```

1. 응용 프로그램을 빌드하고 실행하기 전에, Redis 캐시가 완전하게 프로비전되었는지 확인합니다. `az redis create` 명령이 완료된 후 몇 분 정도 걸릴 수 있습니다. 다음 명령을 실행하여 상태를 확인합니다.

    ```azcli
    az redis show \
        --name "$REDIS_NAME" \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --query provisioningState
    ```

    상태가 `Creating`이면 몇 분 후에 다시 확인하세요. 완료되면 `Succeeded`로 표시됩니다.

1. 응용 프로그램을 실행하고 콘솔에 **트랜잭션 커밋됨**으로 표시되는지 확인합니다.

    ```bash
    dotnet run
    ```

## <a name="verify-your-data"></a>데이터 확인

마지막 마무리로, 추가한 데이터가 Azure Redis Cache에 있는지 확인하겠습니다.

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/triplecrownlabs.onmicrosoft.com?azure-portal=true)에 로그인합니다.

1. 왼쪽 사이드바에서 **모든 리소스**를 선택하여 Azure Redis Cache를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Azure Redis Cache 인스턴스를 선택합니다. 또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.

1. Azure Redis Cache 인스턴스를 선택합니다.

1. Azure Redis Cache의 **개요** 블레이드에서 **콘솔**을 선택합니다. 하위 수준 Azure Redis Cache 명령을 입력할 수 있는 Azure Redis Cache 콘솔이 열립니다.

1. **get MyKey1**을 입력합니다. 반환된 값이 **MyValue1**인지 확인합니다.

1. **get MyKey2**를 입력합니다. 반환된 값이 **MyValue2**인지 확인합니다.

    ![값 MyKey1 및 MyKey2를 보여주는 Azure Redis Cache 콘솔 스크린샷.](../media/4-redis-console.png)