Azure에서 Redis 캐시 인스턴스를 만든 다음, 캐시에 두 개의 데이터 값을 삽입하는 간단한 트랜잭션을 만들어 보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Azure Redis Cache 만들기

먼저 Azure CLI를 사용하여 Azure Redis Cache를 만들겠습니다. 브라우저 창의 오른쪽에서 Cloud Shell을 사용하여 Azure와 상호작용합니다.

`azure rediscache create` 명령을 사용하여 새 Azure Redis Cache를 만들 것입니다. 여러 매개 변수가 사용됩니다. 다음은 가장 일반적인 매개 변수입니다(전체 목록은 설명서 확인).

> [!div class="mx-tableFixed"]
> | 매개 변수 | 설명 |
> |-----------|-------------|
> | `--name`    | 캐시 이름 - 전역적으로 고유해야 하며 문자, 숫자, 대시로 구성됩니다. |
> | `--resource-group` | Azure 샌드박스의 일부인 미리 생성된 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 리소스 그룹을 사용합니다. |
> | `--location` | 캐시를 배치할 위치를 지정합니다. 일반적으로 데이터 소비자와 가까운 위치를 선택합니다. 이 예에서는 Azure 샌드박스에서 사용할 수 있는 위치로 제한됩니다. 가장 가까운 위치를 선택합니다. |
> | `--size` | Redis Cache의 크기입니다. 유효한 값 [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
> | `--sku` | Redis SKU입니다. 유효한 값은 [기본, 표준, 프리미엄] |
> | `--enable-non-ssl-port` | 캐시에 대해 비 SSL 포트를 사용하도록 설정하려는 경우 이 플래그를 추가합니다. |

### <a name="selecting-a-location"></a>위치 선택
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. 다음 옵션을 사용하여 캐시를 만듭니다.
    - 크기: C0
    - SKU: 기본
    - EnableNonSslPort
    
1. 다음 예제 명령줄에서 **[name]** 및 **[location]** 을 유효한 값으로 바꿔야 합니다.

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

1. 캐시가 생성될 때까지 몇 분 정도 걸립니다.

## <a name="create-a-net-core-console-application"></a>.NET Core 콘솔 응용 프로그램 만들기

다음으로, Azure Redis Cache에 데이터 값을 삽입하는 데 사용할 .NET Core C# 기반 콘솔 응용 프로그램을 만듭니다.

1. 창 오른쪽의 통합 Cloud Shell을 사용하여 새 .NET Core 응용 프로그램을 만듭니다. 이름을 "RedisData"로 지정합니다.

    ```bash
    dotnet new console --name RedisData
    ```
    
1. 앱에 대해 만든 새 디렉터리로 변경합니다.

    ```bash
    cd RedisData
    ```
    
1. 프로젝트 파일 하나와 단일 **Program.cs** 소스 파일이 있을 것입니다.

1. 응용 프로그램을 빌드하고 실행하면 "Hello, World!"가 출력됩니다.

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a>ServiceStack.Redis NuGet 패키지 추가

콘솔 응용 프로그램이 생겼으니, **ServiceStack.Redis** NuGet 패키지를 추가해야 합니다. 그러면 Redis Cache에 연결하고 C#에서 명령을 실행할 수 있습니다.

1. 터미널 셸을 사용하여 NuGet 패키지 **ServiceStack.Redis**를 추가합니다.

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. 응용 프로그램을 다시 빌드하고 실행하여 모두 컴파일되는지 확인합니다. 여전히 "Hello, World!"가 출력되어야 합니다.

## <a name="get-your-azure-redis-cache-connection-string"></a>Azure Redis Cache 연결 문자열 가져오기

Azure Redis Cache에 연결하려면 암호 및 URL을 포함하고 있는 연결 문자열이 필요합니다. 이 연결 문자열은 **ServiceStack.Redis**에 대해 고유하며 `[password]@[host name]:[port]` 형식입니다.

Azure Portal 또는 명령줄을 사용하여 이 키를 검색할 수 있습니다. **Redis로 읽기 전용 데이터를 캐시하여 웹 응용 프로그램 최적화**에서 포털을 사용했으니, 여기서는 명령줄을 사용하겠습니다.

`azure rediscache list-keys` 명령을 사용하여 액세스 키를 가져옵니다. 아래와 같이 이름 및 리소스 그룹을 제공해야 합니다.

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

그러면 다음과 같은 결과가 반환됩니다.

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. **기본 키**를 클립보드에 복사합니다.

1. 캐시를 만들 때 캐시 이름에 `.redis.cache.windows.net` 접미사를 붙여서 지정한 이름이 호스트 이름이 됩니다.

1. 포트는 **6379**입니다.

1. 이 모든 정보는 콘솔에서 `azure rediscache list` 명령을 사용하여 확인할 수 있습니다. 이 명령은 활성 구독(여기서는 Azure 샌드박스)의 모든 Redis 캐시 인스턴스를 보여줍니다.

## <a name="add-the-connection-string-to-your-app"></a>앱에 연결 문자열 추가

1. 앱 폴더에 있어야 합니다. `ls` 또는 `dir`을 입력하는 경우 **Program.cs**가 현재 폴더에 있어야 합니다.

1. 앱 폴더에서 `code .`를 입력하여 기본 제공 편집기를 엽니다.

1. **Program.cs** 소스 파일을 선택합니다.

1. `Program` 클래스에서 다음 필드를 만듭니다.

    ```csharp
    static string redisConnectionString = "";
    ```

1. 방금 만든 **redisConnectionString** 필드의 연결 문자열에 붙여넣고 포트 번호로 **6379**를 사용합니다. 기억하세요. 연결 문자열은 `[password]@[host name]:[port]` 형식입니다.

예제 연결 문자열은 다음과 비슷합니다.

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Azure Redis Cache에 두 개의 데이터 값을 삽입

마지막으로, Azure Redis Cache에 데이터를 추가하겠습니다.

1. **Program.cs** 파일 맨 위에 다음 using 문을 추가합니다.

    ```csharp
    using ServiceStack.Redis;
    ```

1. **Main** 메서드에 다음 코드 조각을 추가합니다. 두 값이 일시적으로 추가됩니다.

    ```csharp
    using (RedisClient redisClient = new RedisClient(redisConnectionString))
    {
        //Create the transaction
        var transaction = redisClient.CreateTransaction();

        //Add multiple operations to the transaction
        transaction.QueueCommand(c => c.Set("MyKey1", "MyValue1"));
        transaction.QueueCommand(c => c.Set("MyKey2", "MyValue2"));

        //Commit and get result of transaction
        var transactionResult = transaction.Commit();

        if(transactionResult)
            Console.WriteLine("Transaction committed");
        else
            Console.WriteLine("Transaction failed to commit");
    }
    ```
1. 편집기 창 맨 아래에 있는 명령 프롬프트를 통해 응용 프로그램을 실행하고 콘솔에 **트랜잭션 커밋됨**이라고 나오는지 확인합니다. 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a>데이터 확인

마지막 마무리로, 추가한 데이터가 Azure Redis Cache에 있는지 확인하겠습니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. 왼쪽 사이드바에서 **모든 리소스**를 선택하여 Redis 캐시를 찾은 다음, 왼쪽의 필터 상자를 사용하여 Redis Cache 인스턴스를 선택합니다. 또는 맨 위에 있는 검색 상자를 사용하여 캐시 이름을 입력합니다.

1. Redis 캐시 인스턴스를 선택합니다.

1. Redis Cache의 **개요** 블레이드에서 **콘솔**을 선택합니다. 하위 수준 Redis 명령을 입력할 수 있는 Redis 콘솔이 열립니다.

1. **get MyKey1**을 입력합니다. 반환된 값이 **MyValue1**인지 확인합니다.

1. **get MyKey2**를 입력합니다. 반환된 값이 **MyValue2**인지 확인합니다.

    ![값 MyKey1 및 MyKey2를 보여주는 Azure Redis 콘솔 스크린샷.](../media/4-redis-console.png)