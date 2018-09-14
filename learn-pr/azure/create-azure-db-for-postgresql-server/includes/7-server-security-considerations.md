온-프레미스 PostgreSQL 데이터베이스를 사용 하는 경우를 가정해 봅니다. 모든 보안 측면을 관리 하 고 및 표준 PostgreSQL 서버 수준 방화벽 규칙을 사용 하는 서버에 대 한 모든 액세스 잠겨 했습니다. 서버 수준 동일한 구성할 수 있는지 확인 하려면 지금 Azure 방화벽 규칙입니다.

## <a name="server-security-considerations-and-connection-methods"></a>서버 보안 고려 사항 및 연결 메서드

다양 한 Azure Database for PostgreSQL 서버 및 데이터베이스에 대 한 액세스를 제한 하는 옵션을 해야 합니다. 네트워크 액세스는 네트워크, 서버 또는 데이터베이스 수준에서 제한할 수 있습니다. 다음 옵션 중 하나를 사용할 수 있습니다.

- 데이터베이스 액세스를 제한 하려면 사용자 계정
- 가상 네트워크에 대 한 네트워크 액세스 제한
- 서버 액세스를 제한 하는 방화벽 규칙

### <a name="authentication-and-authorization"></a>인증 및 권한 부여

Azure Database for PostgreSQL 서버는 네이티브 PostgreSQL 인증을 지원합니다. 연결 하 고 서버 관리자 로그인을 사용 하 여 서버에 인증할 수 있습니다. 사용자가 액세스를 제한 하는 특정 데이터베이스에 연결할도 만들어야 합니다.

### <a name="what-is-a-virtual-network"></a>가상 네트워크란?

가상 네트워크는 Azure 네트워크 내에서 만든 논리적으로 격리 된 네트워크입니다. 다른 리소스에 연결 하는 Azure 리소스 수를 제어 하는 가상 네트워크를 사용할 수 있습니다.

데이터베이스에 연결 하는 웹 응용 프로그램을 실행 중인 한다고 가정 합니다. 네트워크의 다른 부분을 격리 서브넷을 사용 합니다. 서브넷의 IP 주소 범위를 기반으로 하는 네트워크의 일부인 합니다.

이러한 서브넷을 구성 하려면 가상 네트워크를 만들고 네트워크 서브넷으로 세분화 합니다. 하나의 서브넷에서 다른 서브넷에 있는 데이터베이스에 웹 응용 프로그램을 작동 합니다. 각 서브넷에 다른 네트워크에서 통신에 대 한 규칙을 직접 해야 합니다. 이러한 규칙 데이터베이스에서 웹 응용 프로그램에 대 한 액세스를 제한 하는 기능을 제공 합니다.

가상 네트워크를 만드는이 모듈의 범위를 벗어납니다. 에 자세한 정보가 필요한 경우에 가상 네트워크와 관련 된 다른 학습 모듈을 탐색 하세요.

### <a name="what-is-a-firewall"></a>방화벽 이란?

방화벽은 각 요청의 원래 IP 주소를 기반으로 하는 서버 액세스 권한을 부여 하는 서비스. IP 주소 범위를 지정 하는 방화벽 규칙을 만듭니다. 이러한 클라이언트 중 하나만 부여 IP 주소는 서버에 액세스할 수 합니다. 방화벽 규칙을 일반적으로 특정 네트워크 프로토콜 및 포트 정보도 포함 합니다. 예를 들어, 기본적으로 PostgreSQL 서버는 5432 포트에서 TCP 요청에 수신 대기합니다.

### <a name="azure-database-for-postgresql-server-firewall"></a>PostgreSQL 서버 방화벽에 대 한 azure 데이터베이스

Azure Database for PostgreSQL 서버 방화벽 권한이 있는 컴퓨터를 지정할 때까지 데이터베이스 서버에 대 한 모든 액세스를 방지 합니다. 방화벽 구성에는 서버에 연결할 수 있는 범위의 IP 주소를 지정할 수 있습니다. 서버는 항상 기본 PostgreSQL 연결 정보를 사용합니다.

![Azure 방화벽 기능 다이어그램](../media-draft/7-firewall-diagram.png)

### <a name="azure-database-for-postgresql-server-ssl-connections"></a>PostgreSQL 서버 SSL 연결에 대 한 azure 데이터베이스

Azure Database for PostgreSQL 클라이언트 응용 프로그램 보안 소켓 레이어 (SSL)를 사용 하 여 PostgreSQL 서비스에 연결 하는 것을 선호 합니다. 데이터베이스 서버와 클라이언트 응용 프로그램 간 SSL 연결 적용는 "man-in-the-middle" 으로부터 보호 하 고 서버와 클라이언트 간에 데이터를 암호화 하 여 비슷한 공격입니다. SSL을 사용 하도록 설정 하면 엄격한 클라이언트와 서버 간의 인증 연결에 대 한 작업 및 키 교환이 필요 합니다. SSL을 사용 하는 방법에 대 한 자세한 내용은이 학습 모듈의 범위를 벗어납니다. 에 자세한 정보가 필요한 경우 SSL과 관련 된 다른 학습 모듈을 탐색 하세요.

## <a name="configure-connection-security"></a>연결 보안 구성

결정 사항 및 Azure Database for PostgreSQL 서버 방화벽을 구성 하는 단계에 살펴보겠습니다. 또한 이전에 만든 서버에 연결 하는 방법을 표시 됩니다.

먼저 엽니다는 [Azure portal](https://portal.azure.com?azure-portal=true) 방화벽 규칙을 만들려면 하려는 서버가 리소스를 이동 합니다.

그런 다음, 선택 하는 **연결 보안** 옵션 오른쪽 연결 보안 블레이드를 엽니다.

![PostgreSQL 데이터베이스 리소스 블레이드의 연결 보안 섹션을 보여 주는 Azure portal의 스크린샷](../media-draft/7-db-security-settings.png)

이 화면에는 몇 가지 옵션이 있습니다. 다음을 수행할 수 있습니다.

- 클릭 하 여 방화벽 항목으로 포털에 액세스 하는 데 사용할 수 있는 IP 주소를 추가 합니다 **클라이언트 IP 추가** 단추입니다.
- Azure 서비스에 대 한 액세스를 허용 합니다. 기본적으로 모든 Azure 서비스 **하지** PostgreSQL 서버에 액세스할 수 있습니다.
- IP 주소 범위를 입력 하 여 방화벽 규칙을 추가 합니다.
- SSL 연결을 적용 합니다. 이 옵션에는 SSL 인증서를 사용 하 여 서버에 연결 하도록 클라이언트를 실행 하도록 합니다.

클릭을 항상 기억 합니다 **저장** 변경한 후 업데이트 된 구성을 저장 하려면 입력 필드 위에 아이콘입니다.

### <a name="allow-access-to-azure-services"></a>Azure 서비스에 대한 액세스 허용

Azure Cloud Shell에 액세스 하거나 서버를 구성 하는 데 사용 하려면 확인을 사용 하도록 **Azure 서비스에 대 한 액세스 허용**합니다. 이 단계는 Cloud Shell에서 액세스를 허용 하도록 서버 구성에 방화벽 규칙을 추가할 예정입니다. 이 규칙은 추가 하는 사용자 지정 규칙 중 하나로 표시 되지 않습니다.

사용 하지 않도록 설정 해야 **SSL 연결 적용**합니다. PowerShell은 SSL 클라이언트 연결에 필요한 경우 서버에 연결할 수 없습니다.

두이 옵션 모두에 명령줄에 표시 된 구성 되지 않은 경우 올바르게 오류 메시지가 발생 합니다.

예를 들어 액세스는 Azure 서비스에 허용 되지 않으며 SSL 연결 적용 하는 경우 사용 되, 방화벽에서 액세스를 차단 하는 경우이 오류와 유사한 화면이 표시 됩니다.

> psql: FATAL: 호스트 "123.45.67.89" 사용자 "adminuser"에 대 한 pg_hba.conf 항목이 데이터베이스 "postgres", SSL on FATAL: SSL 연결이 필요 합니다. SSL 옵션을 지정하고 다시 시도하십시오.

### <a name="create-a-firewall-rule-using-the-portal"></a>포털을 사용 하 여 방화벽 규칙 만들기

모든 IP 주소에서 액세스를 제공 하는 방화벽 규칙을 만들려는 경우를 가정해 봅니다.

> [!WARNING]
> 이 방화벽 규칙을 만드는 모든 IP 주소에서 인터넷을 통해 서버에 연결 하려고 하면 있습니다. 있어도 클라이언트 서버일 수도 있고 액세스할 수 없는 사용자 이름 및 암호를 없습니다, 그리고 주의 해 서이 규칙을 사용 및 보안에 미치는 영향을 이해 해야 합니다.

다음 데이터를 레이블이 지정 된 필드에 입력 하 여 새 방화벽 규칙을 만듭니다.

- 규칙 이름: `AllowAll`
- 시작 IP: `0.0.0.0`
- 끝 IP: `255.255.255.255`

방화벽 규칙을 제거 하려면 삭제 하려는 규칙의 끝에 줄임표 (...)를 클릭 하겠습니다. 클릭 합니다 **삭제** 규칙을 삭제 하는 단추입니다.

클릭 합니다 **저장** 커밋을 삭제 규칙의 입력 필드 위에 아이콘.

### <a name="create-a-firewall-rule-using-the-azure-cli"></a>Azure CLI를 사용 하 여 방화벽 규칙 만들기

Azure CLI를 사용 하 여 방화벽 규칙을 사용 하 여 서버를 추가 하는 `az postgres server firewall-rule create` Azure cloud Shell을 사용 하 여 명령입니다.

위와 동일한 규칙을 만들려는 경우를 가정해 봅니다. 다음 명령을 사용할 수 있습니다.

  ```azurecli
  az postgres server firewall-rule create --resource-group <resource_group_name> --server <server-name> --name AllowAll --start-ip-address 0.0.0.0 --end-ip-address 255.255.255.255
  ```

명령 사용 하 여 서버에서 방화벽 규칙을 제거 하면 `az postgres server firewall-rule delete`합니다.

사용자가 만든 방화벽을 삭제 하려는 경우를 가정해 봅니다. 다음 명령을 사용 합니다.

  ```azurecli
  az postgres server firewall-rule delete --name AllowAll --resource-group <resource_group_name> --server-name <server-name>
  ```

## <a name="connecting-to-your-server"></a>서버에 연결

모든 최신 데이터베이스와 같은 PostgreSQL에는 최상의 성능을 얻으려면 일반 서버 관리가 필요 합니다. 다양 한 옵션이 연결 및 Azure Database for PostgreSQL 서버를 관리 해야 합니다. 사용 하 여 `psql` 서버에 연결 합니다.

### <a name="what-is-psql"></a>Psql 란?

명령줄 도구 라는 `psql` 은 PostgreSQL에 PostgreSQL 서버 및 데이터베이스 작업을 위한 대화형 터미널 분산 합니다. `psql` Azure database for PostgreSQL 동일 하 게 작동 다른 PostgreSQL 구현 하 고 Azure Cloud Shell을 사용 하 여 포함 됩니다. `psql` 도구를 사용 하면 데이터베이스를 관리할 수 있을 뿐만 아니라 이러한 데이터베이스에 대 한 구조 쿼리를 실행할 수 있습니다.

사용 하 여 `psql` PostgreSQL 서버에 성공적으로 연결 해야 합니다. 여러 가지 명령줄 매개 변수 사용에 대 한 사용 가능한 작업할 때 `psql`합니다.

- `--host` -호스트를 연결 하려는입니다.
- `--username` -사용자 이름/i d 연결 하는 데 사용 합니다.
- `--dbname` -연결할 데이터베이스의 이름입니다.

> [!Note]
> 일반적으로 연결할 수는 `postgres` 관리 데이터베이스 서버 액세스 및 데이터베이스 구성에 사용자를 관리 하는 경우.

전체 명령은 다음과 같습니다.

  ```bash
  psql --host=<server-name>.postgres.database.azure.com --username=<admin-user>@<server-name> --dbname=<database>
  ```

연결 되 면 명령 프롬프트가 표시 됩니다 하 고 서버 및 데이터베이스에 명령을 실행할 수 있습니다.

이제 Azure Database for PostgreSQL 보안 설정을 구성 하기 위해 수행 하는 단계를 살펴보았습니다. 다음 단위에 있는 PostgreSQL 보안 설정에 대 한 Azure Database를 구성 합니다. Cloud Shell을 사용 하 여 서버에 연결할 수 있습니다.
