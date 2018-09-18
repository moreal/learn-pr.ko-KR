온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다. 표준 PostgreSQL 서버 수준 방화벽 규칙을 사용하여 모든 보안 측면을 관리하고 서버에 대한 모든 액세스를 잠급니다. 이제 Azure에서 동일한 서버 수준 방화벽 규칙을 구성할 수 있는지 확인하려고 합니다.

## <a name="server-security-considerations-and-connection-methods"></a>서버 보안 고려 사항 및 연결 방법

Azure Database for PostgreSQL 서버 및 데이터베이스에 대한 액세스를 제한하는 여러 가지 옵션이 있습니다. 네트워크 액세스는 네트워크, 서버 또는 데이터베이스 수준에서 제한할 수 있습니다. 다음 옵션 중 하나를 사용할 수 있습니다.

- 데이터베이스 액세스를 제한하는 사용자 계정
- 네트워크 액세스를 제한하는 가상 네트워크
- 서버 액세스를 제한하는 방화벽 규칙

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

Azure Database for PostgreSQL 서버는 원시 PostgreSQL 인증을 지원합니다. 서버의 관리자 로그인을 사용하여 서버에 연결하고 인증할 수 있습니다. 또한 특정 데이터베이스에 연결하는 사용자를 만들어 액세스를 제한할 수도 있습니다.

### <a name="what-is-a-virtual-network"></a>가상 네트워크란?

가상 네트워크는 Azure 네트워크 내에 만들어진 논리적으로 격리된 네트워크입니다. 가상 네트워크를 사용하여 다른 리소스에 연결할 수 있는 Azure 리소스를 제어할 수 있습니다.

데이터베이스에 연결하는 웹 응용 프로그램을 실행한다고 가정합니다. 서브넷을 사용하여 네트워크의 다른 부분을 격리합니다. 서브넷은 IP 주소 범위를 기반으로 하는 네트워크의 일부입니다.

이러한 서브넷을 구성하려면 가상 네트워크를 만든 다음, 네트워크를 서브넷으로 세분화합니다. 웹 응용 프로그램은 한 서브넷과 다른 서브넷의 데이터베이스에서 작동합니다. 각 서브넷에는 다른 네트워크와의 통신을 위한 자체의 규칙이 있습니다. 이러한 규칙은 데이터베이스에서 웹 응용 프로그램으로의 액세스를 제한하는 기능을 제공합니다.

가상 네트워크를 만드는 것은 이 모듈의 범위를 벗어납니다. 자세한 정보가 필요하면 가상 네트워크와 관련된 다른 학습 모듈을 살펴보세요.

### <a name="what-is-a-firewall"></a>방화벽이란?

방화벽은 각 요청의 원래 IP 주소에 따라 서버 액세스 권한을 부여하는 서비스입니다. IP 주소 범위를 지정하는 방화벽 규칙을 만듭니다. 이러한 규칙을 통해 부여된 IP 주소의 클라이언트만 서버에 액세스할 수 있습니다. 또한 일반적으로 말하는 방화벽 규칙에는 특정 네트워크 프로토콜 및 포트 정보도 포함됩니다. 예를 들어 PostgreSQL 서버는 기본적으로 5432 포트에서 TCP 요청을 수신 대기합니다.

### <a name="azure-database-for-postgresql-server-firewall"></a>Azure Database for PostgreSQL 서버 방화벽

Azure Database for PostgreSQL 서버 방화벽은 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버에 대한 모든 액세스를 차단합니다. 방화벽 구성을 통해 서버에 연결할 수 있는 IP 주소의 범위를 지정할 수 있습니다. 서버는 항상 기본 PostgreSQL 연결 정보를 사용합니다.

![Azure 방화벽 기능 다이어그램](../media-draft/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a>Azure Database for PostgreSQL 서버 SSL 연결

Azure Database for PostgreSQL은 기본적으로 클라이언트 응용 프로그램에서 SSL(Secure Sockets Layer)을 사용하여 PostgreSQL 서비스에 연결하도록 설정합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간에 SSL 연결을 적용하면 서버와 응용 프로그램 간의 데이터를 암호화하여 "메시지 가로채기(man in the middle)" 공격 및 이와 유사한 공격으로부터 보호할 수 있습니다. SSL을 사용하려면 클라이언트와 서버 간에 키와 엄격한 인증을 교환하여 연결이 작동해야 합니다. SSL을 사용하는 방법에 대한 자세한 내용은 이 학습 모듈의 범위를 벗어납니다. 자세한 정보가 필요하면 SSL과 관련된 다른 학습 모듈을 살펴보세요.

## <a name="configure-connection-security"></a>연결 보안 구성

Azure Database for PostgreSQL 서버 방화벽을 구성하기 위해 수행하는 결정과 단계를 살펴보겠습니다. 또한 이전에 만든 서버에 연결하는 방법도 볼 수 있습니다.

먼저 [Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 방화벽 규칙을 만들려는 서버 리소스로 이동합니다.

그런 다음, **연결 보안** 옵션을 선택하여 오른쪽에 [연결 보안] 블레이드를 엽니다.

![PostgreSQL 데이터베이스 보안 설정](../media-draft/7-db-security-settings.png)

이 화면에는 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

- **+ 클라이언트 IP 추가** 단추를 클릭하여 포털에 액세스하는 데 사용하는 IP 주소를 방화벽 항목으로 추가합니다
- Azure 서비스 방문 허용. 모든 Azure 서비스는 기본적으로 PostgreSQL 서버에 **액세스할 수 없습니다**.
- IP 주소 범위를 입력하여 방화벽 규칙 추가
- SSL 연결 적용. 이 옵션은 클라이언트에서 SSL 인증서를 사용하여 서버에 연결하도록 합니다.

변경한 후에 업데이트된 구성을 저장하려면 항상 입력 필드 위에 있는 **저장** 아이콘을 클릭해야 합니다.

### <a name="allow-access-to-azure-services"></a>Azure 서비스 방문 허용

Azure Cloud Shell을 사용하여 서버에 액세스하거나 구성하려면 **Azure 서비스 방문 허용**을 사용하도록 설정해야 합니다. 이 단계에서는 Cloud Shell에서 액세스할 수 있도록 허용하는 방화벽 규칙을 서버 구성에 추가합니다. 이 규칙은 추가하는 사용자 지정 규칙 중 하나로 표시되지 않습니다.

또한 **SSL 연결 적용**은 사용하지 않도록 설정해야 합니다. 클라이언트 연결에 SSL이 필요한 경우 PowerShell에서 서버에 연결할 수 없습니다.

이 두 옵션이 모두 올바르게 구성되지 않으면 명령줄에 오류 메시지가 표시됩니다.

예를 들어 Azure 서비스에 대한 액세스가 허용되지 않고 SSL 연결 적용을 사용하도록 설정되는 경우 방화벽에서 액세스를 차단할 때 다음 오류와 비슷한 내용이 표시됩니다.

> psql: FATAL: "123.45.67.89" 호스트, "adminuser" 사용자, "postgres" 데이터베이스에 대한 pg_hba.conf 항목이 없습니다. SSL on FATAL: SSL 연결이 필요합니다. SSL 옵션을 지정하고 다시 시도하십시오.

### <a name="create-a-firewall-rule-using-the-portal"></a>포털을 사용하여 방화벽 규칙 만들기

모든 IP 주소에서 액세스를 제공하는 방화벽 규칙을 만들려고 한다고 가정해 보겠습니다.

> [!WARNING]
> 이 방화벽 규칙을 만들면 인터넷의 모든 IP 주소에서 서버에 연결하려고 시도할 수 있습니다. 클라이언트에서 사용자 이름과 암호를 사용하여 서버에 액세스 할 수 있는 경우에도 이 규칙을 신중하게 사용하도록 설정하고 보안에 미치는 영향을 이해해야 합니다.

레이블이 지정된 필드에서 다음 데이터를 입력하여 새 방화벽 규칙을 만듭니다.

- 규칙 이름: `AllowAll`
- 시작 IP: `0.0.0.0`
- 종료 IP: `255.255.255.255`

방화벽 규칙을 제거하려면 삭제하려는 규칙 끝에 있는 줄임표를 클릭합니다. [삭제] 단추를 클릭하여 규칙을 삭제합니다.

입력 필드 위에 있는 **저장** 아이콘을 클릭하여 규칙 삭제를 커밋합니다.

### <a name="create-a-firewall-rule-using-the-azure-cli"></a>Azure CLI를 사용하여 방화벽 만들기

Azure CLI를 사용하여 Azure CloudShell에서 `az postgres server firewall-rule create` 명령으로 서버에 방화벽 규칙을 추가합니다.

다음 명령을 사용하여 위와 동일한 규칙을 만들려고 한다고 가정해 보겠습니다.

  ```bash
  az postgres server firewall-rule create --resource-group <resource_group_name> --server <server-name> --name AllowAll --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
  ```

`az postgres server firewall-rule delete` 명령을 사용하여 서버에서 방화벽 규칙을 제거합니다.

만든 방화벽을 삭제하고 나서 다음 명령을 사용하려고 한다고 가정해 보겠습니다.

  ```bash
  az postgres server firewall-rule delete --name AllowAll --resource-group <resource_group_name> --server-name <server-name>
  ```

## <a name="connecting-to-your-server"></a>서버에 연결

모든 최신 데이터베이스와 마찬가지로, PostgreSQL도 최상의 성능을 얻기 위해 정기적으로 서버를 관리해야 합니다. Azure Database for PostgreSQL 서버를 연결하고 관리하는 여러 가지 옵션이 있습니다. `psql`을 사용하여 서버에 연결합니다.

### <a name="what-is-psql"></a>psql이란?

`psql`이라는 명령줄 도구는 PostgreSQL 서버 및 데이터베이스 작업을 위한 PostgreSQL 분산 대화형 터미널입니다. `psql`은 다른 PostgreSQL 구현과 마찬가지로 Azure Database for PostgreSQL에서 작동하며 Azure Cloud Shell에 포함되어 있습니다. `psql` 도구를 사용하면 데이터베이스를 관리할 수 있을 뿐만 아니라 이러한 데이터베이스에 대한 구조 쿼리도 실행할 수 있습니다.

`psql`을 사용하려면 PostgreSQL 서버에 성공적으로 연결되어 있어야 합니다. `psql`을 사용할 때 사용할 수 있는 여러 가지 명령줄 매개 변수가 있습니다.

- `--host` - 연결하려는 호스트
- `--username` - 연결하는 데 사용할 사용자 이름/ID
- `--dbname` - 연결할 데이타베이스의 이름

> [!Note]
> 서버 액세스 및 데이터베이스 구성을 관리하는 경우 일반적으로 `postgres` 관리 데이터베이스에 연결합니다.

전체 명령은 다음과 같습니다.

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=<database>
  ```

연결되면 명령 프롬프트가 표시되고 서버와 데이터베이스에 명령을 실행할 수 있습니다.

이제 Azure Database for PostgreSQL 보안 설정을 구성하는 단계를 살펴보았습니다. 다음 단원에서는 Azure Database for PostgreSQL 보안 설정을 구성합니다. 또한 Cloud Shell을 사용하여 서버에 연결합니다.