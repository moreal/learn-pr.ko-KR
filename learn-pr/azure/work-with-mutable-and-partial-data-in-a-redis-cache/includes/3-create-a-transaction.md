이제 Azure Redis Cache의 인스턴스를 만들어 시작한 다음 캐시에 두 개의 데이터 값을 삽입 하는 간단한 트랜잭션을 만듭니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-an-azure-redis-cache"></a>Azure Redis Cache 만들기

Azure CLI를 사용 하 여 Azure Redis Cache를 만들어 보겠습니다. Azure와 상호작용 하는 브라우저 창의 오른쪽에 Cloud Shell을 사용 합니다.

사용 하 여는 `azure rediscache create` 새 Azure Redis Cache를 만드는 명령입니다. 여러 매개 변수를 사용 합니다. (전체 목록을 가져오려면, 설명서를 참조)에 가장 일반적인 다음과 같습니다.

> [!div class="mx-tableFixed"]
> | 매개 변수 | 설명 |
> |-----------|-------------|
> | `--name`    | -캐시의 이름을 고유 하 고 문자, 숫자 및 대시 구성 이어야 합니다. |
> | `--resource-group` | 미리 만든된 리소스 그룹을 사용 <rgn>[샌드박스 리소스 그룹 이름]</rgn>, Azure Sandbox의 일부인 합니다. |
> | `--location` | 여기서 캐시를 배치할 위치를 지정 합니다. 일반적으로 데이터 소비자 가까운 위치를 선택 합니다. 이 경우 Azure 샌드박스에서 사용할 수 있는 위치 제한 됩니다. 가장 가까운를 선택 합니다. |
> | `--size` | Azure Redis Cache의 크기입니다. 유효한 값 이며 [C0, C1, C2, C3, C4, C5, C6, P1, P2, P3, P4] |
> | `--sku` | Azure Redis 캐시 SKU입니다. 유효한 값 [Basic, Standard, Premium] 됩니다. |
> | `--enable-non-ssl-port` | 캐시에 대해 비 SSL 포트를 사용 하도록 설정 하려는 경우이 플래그를 추가 합니다. |

### <a name="selecting-a-location"></a>위치 선택
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

1. 다음 옵션을 사용 하 여 캐시를 만듭니다.
    - 크기: C0
    - SKU: 기본
    - EnableNonSslPort
    
1. 명령줄 예는 다음과 같습니다. 바꿔야 합니다 **[name]** 하 고 **[위치]** 유효한 값을 사용 하 여 합니다.

    ```azurecli
    azure rediscache create \
        --name [name] \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location [location] \
        --size C0 --sku Basic
    ```

캐시를 만드는 데는 몇 분 정도 걸립니다.

## <a name="create-a-net-core-console-application"></a>.NET Core 콘솔 응용 프로그램 만들기

다음으로 Azure Redis Cache에 데이터 값을 삽입 하는 데 사용할.NET Core C# 기반 콘솔 응용 프로그램을 만듭니다.

1. 오른쪽 창에서 통합된 Cloud Shell을 사용 하 여 새.NET Core 응용 프로그램을 만듭니다. "RedisData" 이름을 지정 합니다.

    ```bash
    dotnet new console --name RedisData
    ```
    
1. 만든 앱에 대 한 새 디렉터리를 변경 합니다.

    ```bash
    cd RedisData
    ```
    
1. 프로젝트 파일 및 단일 찾아야 **Program.cs** 소스 파일입니다.

1. "Hello, World!"를 출력 하도록-빌드 및 응용 프로그램 실행

    ```bash
    dotnet run
    ```
    
## <a name="add-the-servicestackredis-nuget-package"></a>ServiceStack.Redis NuGet 패키지 추가

콘솔 응용 프로그램을 만들었으므로 이제 해당 추가 해야 합니다 **ServiceStack.Redis** NuGet 패키지. 이렇게 하면 Azure Redis Cache 및 C#에서 명령을 실행에 연결할 수 있습니다.

1. NuGet 패키지 추가 **ServiceStack.Redis** 터미널 셸을 사용 합니다.

    ```bash
    dotnet add package ServiceStack.Redis
    ```
    
1. 빌드하고 응용 프로그램 모두 제대로 컴파일되는지 확인을 다시 실행 합니다. "Hello, World!"가 여전히 출력

## <a name="get-your-azure-redis-cache-connection-string"></a>Azure Redis Cache 연결 문자열 가져오기

Azure Redis Cache에 연결 하려면 암호 및 URL을 포함 하는 연결 문자열이 필요 합니다. 이 연결 문자열은 고유한 **ServiceStack.Redis**의 형태로 이며: `[password]@[host name]:[port]`합니다.

Azure portal을 사용 하 여 또는 명령줄을 사용 하 여이 키를 검색할 수 있습니다. "Redis 사용 하 여 읽기 전용 데이터를 캐시 하 여 웹 응용 프로그램을 최적화 합니다." 모듈의 포털 접근 방식 사용 했으므로 후자 여기서를 사용해 보겠습니다.

사용 된 `azure rediscache list-keys` 액세스 키를 가져오는 명령입니다. 아래와 같이 이름 및 리소스 그룹을 제공 해야 합니다.

```azurecli
azure rediscache list-keys \
    --name [name] \
    --resource-group <rgn>[Sandbox resource group name]</rgn>
```

다음과 유사한 출력이 반환 합니다.

```output
Primary Key   : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
Secondary Key : XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX=
```

1. 복사 하 **기본** 클립보드로 키입니다.

1. 호스트 이름 접미사를 사용 하 여, 만든 시 캐시에 지정한 이름이 됩니다 `.redis.cache.windows.net`합니다.

1. 포트 **6379**합니다.

1. 모든 사용 하 여 콘솔에서 해당 정보를 확인할 수 있습니다는 `azure rediscache list` 명령입니다. 이 명령은 (이 예제의 경우 Azure 샌드박스)에 현재 구독에서 Azure Redis Cache의 모든 인스턴스를 표시 합니다.

## <a name="add-the-connection-string-to-your-app"></a>앱에 연결 문자열 추가

1. 앱 폴더에 있는지 확인 합니다. 합니다 **Program.cs** 입력 하는 경우 현재 폴더에 있어야 `ls` 또는 `dir`합니다.

1. 입력 하 여 기본 제공 편집기를 열고 `code .` 앱 폴더에 있습니다.

1. 선택 된 **Program.cs** 소스 파일입니다.

1. 다음 필드는 `Program` 클래스입니다.

    ```csharp
    static string redisConnectionString = "";
    ```

1. 연결 문자열에 붙여넣기를 **redisConnectionString** 방금 만든 필드를 사용 하 여 **6379** 포트 번호로으로 합니다. 연결 문자열의 형태로: `[password]@[host name]:[port]`합니다.

연결 문자열의 예는 다음과 같이 보입니다.

```output
ToOosHLZw9Gwyr46ZlxcNeCCIzS35IBkEtwsCt1Xu4c=@myname.redis.cache.windows.net:6379
```
    
## <a name="insert-two-data-values-into-your-azure-redis-cache"></a>Azure Redis Cache에 두 개의 데이터 값을 삽입

마지막으로, Azure Redis Cache에 데이터를 추가 하려고 합니다.

1. 다음을 추가 합니다 `using` 의 맨 위에 문을 합니다 **Program.cs** 파일입니다.

    ```csharp
    using ServiceStack.Redis;
    ```

1. 코드의 다음 코드 조각을 추가 하 **Main** 메서드. 두 값 transitionally 추가 됩니다.

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
1. 편집기 창의 맨 아래에서 명령 프롬프트를 통해 응용 프로그램을 실행 하 고 콘솔에 표시 됩니다는 확인 **커밋된 트랜잭션이**합니다. 

    ```bash
    dotnet run
    ```
    
## <a name="verify-your-data"></a>데이터 확인

를 완료 하려면 보겠습니다 Azure Redis Cache에 추가한 데이터를 확인 합니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

1. 선택 하 여 Azure Redis Cache를 찾습니다 **모든 리소스** 에 왼쪽 세로 막대를 왼쪽에서 필터 상자를 사용 하 여 Azure Redis Cache 인스턴스를 선택 합니다. 또는 맨 위에 있는 검색 상자를 사용할 수 있으며 캐시의 이름을 입력 합니다.

1. Azure Redis Cache 인스턴스를 선택 합니다.

1. 에 **개요** Azure Redis Cache 선택에 대 한 블레이드 **콘솔**합니다. 낮은 수준의 Azure Redis Cache 명령을 입력할 수 있습니다는 Azure Redis Cache 콘솔이 열립니다.

1. Type **get MyKey1**. 반환 된 값이 인지 확인 **MyValue1**합니다.

1. 형식 **MyKey2 가져오기**합니다. 반환 된 값이 인지 확인 **MyValue2**합니다.

    ![Azure Redis Cache 콘솔 MyKey1 및 MyKey2 값을 보여 주는 스크린샷.](../media/4-redis-console.png)