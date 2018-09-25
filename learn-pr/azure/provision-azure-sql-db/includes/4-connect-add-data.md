데이터베이스를 앱에 연결하기 전에 연결할 수 있는지 확인하고, 기본 테이블을 추가하고, 샘플 데이터로 작업을 수행할 수 있습니다.

Microsoft는 Azure SQL Database에 대한 인프라, 소프트웨어 업데이트 및 패치를 유지 관리합니다. 또한 기타 모든 SQL Server 설치와 마찬가지로 Azure SQL Database를 관리할 수 있습니다. 예를 들어, Visual Studio, SQL Server Management Studio, SQL Server Operations Studio 또는 기타 도구를 사용하여 Azure SQL Database를 관리할 수 있습니다.

데이터베이스에 액세스하고 앱에 연결하는 방법은 사용자가 결정합니다. 그러나 여기서는 데이터베이스로 여러 작업을 수행해보기 위해 포털에서 직접 연결하고, 테이블을 만들고, 몇 가지 기본 CRUD 작업을 실행합니다. 다음 내용을 배웁니다.

- Cloud Shell의 정의 및 포털에서 액세스하는 방법
- Azure CLI에서 연결 문자열을 비롯한 데이터베이스에 대한 정보에 액세스하는 방법
- `sqlcmd`를 사용하여 데이터베이스에 연결하는 방법
- 기본 테이블 및 일부 샘플 데이터를 사용하여 데이터베이스를 초기화하는 방법

## <a name="what-is-azure-cloud-shell"></a>Azure Cloud Shell은 무엇인가요?

Azure Cloud Shell은 Azure 리소스를 관리 및 개발하기 위한 브라우저 기반 셸 환경입니다. Cloud Shell을 클라우드에서 실행되는 대화형 콘솔로 생각하세요.

내부적으로, Cloud Shell은 Linux에서 실행됩니다. 그러나 Linux 또는 Windows 환경 중에서 어떤 것을 선호하는지에 따라 Bash 및 PowerShell 두 가지 환경 중에서 선택할 수 있습니다.

Cloud Shell은 어디에서나 액세스할 수 있습니다. 포털 외에도 [shell.azure.com](https://shell.azure.com/), Azure 모바일 앱 또는 Visual Studio Code에서 Cloud Shell에 액세스할 수 있습니다. 오른쪽 패널은 이 연습을 진행하는 동안 사용할 수 있는 Cloud Shell 터미널입니다.

Cloud Shell에는 인기 있는 도구 및 텍스트 편집기가 포함되어 있습니다. 현재 작업에 사용할 세 가지 도구인 `az`, `jq` 및 `sqlcmd`의 대략적인 모습은 다음과 같습니다.

- `az`를 Azure CLI라고도 합니다. Azure 리소스로 작업하기 위한 명령줄 인터페이스입니다. 이 도구를 사용하여 연결 문자열을 포함하여 데이터베이스에 대한 정보를 가져옵니다.
- `jq`는 명령줄 JSON 파서입니다. `az` 명령의 출력을 이 도구로 파이프하여 JSON 출력에서 중요한 필드를 추출합니다.
- `sqlcmd`를 사용하면 SQL Server에서 명령문을 실행할 수 있습니다. `sqlcmd`를 사용하여 Azure SQL Database와의 대화형 세션을 만듭니다.

## <a name="get-information-about-your-azure-sql-database"></a>Azure SQL Database에 대한 정보 가져오기

데이터베이스에 연결하기 전에 해당 데이터베이스가 존재하고 온라인 상태인지 확인하는 것이 좋습니다.

여기서는 `az` 유틸리티를 사용하여 데이터베이스를 나열하고, 최대 크기 및 상태를 비롯한 **Logistics** 데이터베이스 관련 정보를 표시합니다.

1. 실행할 `az` 명령에는 리소스 그룹의 이름과 Azure SQL 논리 서버의 이름이 필요합니다. 나중에 다시 입력하지 않으려면 이 `azure configure` 명령을 실행하여 기본값으로 지정합니다.
    `<server-name>`를 Azure SQL 논리 서버의 이름으로 바꿉니다. 포털에 현재 열려 있는 블레이드에 따라 이 이름이 FQDN(servername.database.windows.net)으로 표시될 수 있지만 .database.windows.net 접미사가 없는 논리적 이름만 필요합니다.

    ```azurecli
    az configure --defaults group=<rgn>[sandbox resource group name]</rgn> sql-server=<server-name>
    ```

1. `az sql db list`를 실행하여 Azure SQL 논리 서버의 모든 데이터베이스를 나열합니다.

    ```azurecli
    az sql db list
    ```
    JSON의 대형 블록이 출력으로 표시됩니다.

1. 데이터베이스 이름만 필요하면 이 명령을 한 번 더 실행합니다. 이번에는 출력을 `jq`로 파이프하여 이름 필드만 출력합니다.
   
     ```azurecli
    az sql db list | jq '[.[] | {name: .name}]'
    ```
    
    다음 출력이 표시됩니다.
    
    ```json
    [
      {
        "name": "Logistics"
      },
      {
        "name": "master"
      }
    ]
    ```

    **물류**는 데이터베이스입니다. SQL Server와 마찬가지로 **master**에는 로그인 계정 및 시스템 구성 설정과 같은 서버 메타데이터가 포함됩니다.

1. 이 `az sql db show` 명령을 실행하여 **물류** 데이터베이스에 대한 세부 정보를 가져옵니다.

    ```azurecli
    az sql db show --name Logistics
    ```

    앞의 경우처럼 JSON의 대형 블록이 출력으로 표시됩니다.

1. 이 명령을 한 번 더 실행합니다. 이번에는 출력을 `jq`로 파이프하여 출력을 **Logistics** 데이터베이스의 이름, 최대 크기 및 상태로만 제한합니다.

    ```azurecli
    az sql db show --name Logistics | jq '{name: .name, maxSizeBytes: .maxSizeBytes, status: .status}'
    ```

    데이터베이스가 온라인 상태이며 약 2GB의 데이터를 보유할 수 있다고 표시됩니다.

    ```json
    {
      "name": "Logistics",
      "maxSizeBytes": 2147483648,
      "status": "Online"
    }
    ```

## <a name="connect-to-your-database"></a>데이터베이스 연결

데이터베이스를 어느 정도 이해했으므로 `sqlcmd`를 사용하여 연결하고, 운송 기사에 대한 정보를 포함하는 테이블을 만들고, 몇 가지 기본 CRUD 작업을 수행해보겠습니다.

CRUD는 **만들기**, **읽기**, **업데이트** 및 **삭제**를 의미합니다. 이러한 용어는 테이블 데이터에서 수행하는 작업을 의미하며, 앱에 필요한 네 가지 기본 작업에 해당합니다. 이제 각 작업을 수행할 수 있는지 확인해보겠습니다.

1. 이 `az sql db show-connection-string` 명령을 실행하여 연결 문자열을 `sqlcmd`에서 사용할 수 있는 형식으로 **Logistics** 데이터베이스에 가져옵니다.

    ```azurecli
    az sql db show-connection-string --client sqlcmd --name Logistics
    ```

    출력은 다음과 비슷합니다.

    ```output
    "sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U <username> -P <password> -N -l 30"
    ```

1. 이전 단계의 출력에 있는 `sqlcmd` 문을 실행하여 대화형 세션을 만듭니다. 따옴표를 제거하고 `<username>` 및 `<password>`를 사용자가 데이터베이스를 만들 때 지정한 사용자 이름과 암호로 바꿉니다. 예를 들면 다음과 같습니다.

    ```console
    sqlcmd -S tcp:contoso-1.database.windows.net,1433 -d Logistics -U martina -P "password1234$" -N -l 30
    ```

    > [!TIP]
    > “&” 및 기타 특수 문자가 처리 명령으로 해석되지 않도록 암호를 따옴표로 묶습니다.

1. `sqlcmd` 세션에서 `Drivers`라는 테이블을 만듭니다.

    ```sql
    CREATE TABLE Drivers (DriverID int, LastName varchar(255), FirstName varchar(255), OriginCity varchar(255));
    GO
    ```

    이 테이블에는 4개의 열인 고유 ID, 기사의 이름과 성, 기사의 출생 도시가 포함됩니다.

    > [!NOTE]
    > 여기에 표시되는 언어는 Transact-SQL 또는 T-SQL입니다.

1. `Drivers` 테이블이 있는지 확인합니다.

    ```sql
    SELECT name FROM sys.tables;
    GO
    ```

    다음 출력이 표시됩니다.

    ```output
    name
    --------------------------------------------------------------------------------------------------------------------------------
    Drivers

    (1 rows affected)
    ```

1. 이 `INSERT` T-SQL 문을 실행하여 테이블에 샘플 행을 추가합니다. 이것은 **만들기** 작업입니다.

    ```sql
    INSERT INTO Drivers (DriverID, LastName, FirstName, OriginCity) VALUES (123, 'Zirne', 'Laura', 'Springfield');
    GO
    ```

    작업이 성공했음을 나타내기 위해 다음이 표시됩니다.

    ```output
    (1 rows affected)
    ```

1. 이 `SELECT` T-SQL 문을 실행하여 테이블의 모든 행에 있는 `DriverID` 및 `OriginCity` 열을 나열합니다. 이것은 **읽기** 작업입니다.

    ```sql
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    이전 단계에서 만든 행의 `DriverID` 및 `OriginCity`가 포함된 하나의 결과가 표시됩니다.

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Springfield

    (1 rows affected)
    ```

1. 이 `UPDATE` T-SQL 문을 실행하여 `DriverID`가 123인 기사의 출생 도시를 “Springfield”에서 “Boston”으로 변경합니다. 이것은 **업데이트** 작업입니다.

    ```sql
    UPDATE Drivers SET OriginCity='Boston' WHERE DriverID=123;
    GO
    SELECT DriverID, OriginCity FROM Drivers;
    GO
    ```

    다음 출력이 표시되어야 합니다. `OriginCity`에 Boston에 대한 업데이트가 어떻게 반영되었는지 확인하세요.

    ```output
    DriverID    OriginCity
    ----------- --------------------------
            123 Boston

    (1 rows affected)
    ```

1. 이 `DELETE` T-SQL 문을 실행하여 레코드를 삭제합니다. 이것은 **삭제** 작업입니다.

    ```sql
    DELETE FROM Drivers WHERE DriverID=123;
    GO
    ```

    ```output
    (1 rows affected)
    ```

1. 이 `SELECT` T-SQL 문을 실행하여 `Drivers` 테이블이 비어 있는지 확인합니다.

    ```sql
    SELECT COUNT(*) FROM Drivers;
    GO
    ```

    테이블에 행이 없는 것을 볼 수 있습니다.

    ```output
    -----------
              0

    (1 rows affected)
    ```

Cloud Shell에서 Azure SQL Database에 대한 작업 방법을 살펴보았으므로 즐겨 사용하는 SQL 관리 도구(SQL Server Management Studio, Visual Studio 또는 기타)에 대한 연결 문자열을 가져올 수 있습니다.

Cloud Shell을 사용하면 Azure 리소스에 쉽게 액세스하고 관련 작업을 수행할 수 있습니다. Cloud Shell은 브라우저 기반이므로 Windows, macOS 또는 Linux &ndash; 특히 웹 브라우저가 있는 모든 시스템에서 Cloud Shell에 액세스할 수 있습니다.

Azure CLI 명령을 실행하여 Azure SQL Database에 대한 정보를 가져오는 방법에 대한 몇 가지 실습 경험을 했습니다. 추가로 T-SQL 기술도 연습해보았습니다.

마지막으로, 데이터베이스를 중단하는 방법을 알아보겠습니다.
