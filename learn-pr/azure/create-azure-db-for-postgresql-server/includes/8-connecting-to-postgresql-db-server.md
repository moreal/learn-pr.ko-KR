온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다. 표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다. 이제는 Azure에서 동일한 서버 수준 방화벽 규칙을 구성하는 방법에 대해 잘 알고 있습니다.

만든 Azure Database for PostgreSQL 서버 중 하나에 연결해 보겠습니다.

## <a name="allow-azure-service-access"></a>Azure 서비스 액세스 허용

시작하기 전에 PowerShell과 `psql`을 사용하여 서버에 연결하려면 Azure 서비스에 대한 액세스를 허용해야 합니다. 액세스는 두 가지 방법으로 허용할 수 있습니다.

첫 번째 옵션은 **Azure 서비스 방문 허용**을 사용하도록 설정하는 것입니다. 사용자가 만든 사용자 지정 규칙 목록에 규칙이 입력되지 않은 경우에도 액세스를 허용하면 방화벽 규칙이 만들어집니다.

두 번째 옵션은 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 만드는 것입니다. 규칙에는 `psql`을 실행하는 데 사용하는 PowerShell이 실행되는 클라이언트에 대한 IP 주소가 포함됩니다.

또한 **SSL 연결 적용** 옵션은 사용하지 않도록 설정해야 합니다.

### <a name="create-a-firewall-rule"></a>방화벽 규칙을 만들기

1. 샌드박스를 활성화한 동일한 계정을 사용하여 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 방화벽 규칙을 만들려는 서버 리소스로 이동합니다.

1. **연결 보안** 옵션을 선택하여 오른쪽에 [연결 보안] 블레이드를 엽니다.

    ![PostgreSQL 데이터베이스 리소스 블레이드의 연결 보안 섹션을 보여 주는 Azure Portal의 스크린샷](../media/7-db-security-settings.png)

`psql`을 실행하는 PowerShell 클라이언트에 대한 액세스를 허용하려고 합니다.

다음 중 하나를 선택할 수 있습니다.

- **Azure 서비스 방문 허용**을 **켜기**로 설정합니다.
- **SSL 연결 적용**을 **사용 안 함**으로 설정합니다.
- **저장** 단추를 클릭하여 변경 내용을 저장합니다.

또는 모든 IP 주소에 대한 액세스를 허용하는 방화벽 규칙을 추가할 수 있습니다. 다음 값을 사용합니다.

- 규칙 이름: `AllowAll`
- 시작 IP: `0.0.0.0`
- 종료 IP: `255.255.255.255`
- **SSL 연결 적용**을 **사용 안 함**으로 설정합니다.
- **저장** 단추를 클릭하여 변경 내용을 저장합니다.

> [!Warning]
> 이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다. 프로덕션 환경에서는 특정 IP 주소에 대한 액세스만 허용하고자 합니다.

### <a name="connect-to-the-database-with-psql"></a>PSQL로 데이터베이스에 연결

1. 오른쪽의 Azure Cloud Shell에서 다음 명령을 사용하여 PSQL을 서버에 연결합니다. 서버 이름 및 관리자 이름을 바꿔야 합니다.

    ```bash
    psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=postgres
    ```

    `server-name` 및 `admin-user`에 대해 선택한 값을 사용합니다.

1. **postgres**는 각 PostgreSQL 서버를 만들 때마다 포함되는 기본 관리 데이터베이스입니다. 서버를 만들 때 제공한 암호를 묻는 메시지가 표시됩니다.

1. 성공적으로 연결되면 모든 데이터베이스를 나열하는 <kbd>\l</kbd> 명령을 실행합니다. 이 명령을 실행하면 둘 이상의 기본 데이터베이스가 반환됩니다.

1. <kbd>q</kbd>를 눌러 목록을 종료합니다.

1. 다른 PSQL 명령을 사용할 수 있습니다.
    - <kbd>\?</kbd> 도움말 가져오기.
    - <kbd>\dt</kbd> 테이블 나열.

1. 서버에서 PSQL 작업 실행이 완료되면 <kbd>\q</kbd> 명령을 실행하여 PSQL을 종료합니다.
