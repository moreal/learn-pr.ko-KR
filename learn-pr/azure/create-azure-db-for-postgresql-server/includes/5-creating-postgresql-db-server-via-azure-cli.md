온-프레미스 PostgreSQL 데이터베이스를 사용 하는 경우를 가정해 봅니다. 회사 이제를 보고 서버를 Azure로 이동 하 여 장치 지원, 가용성, 데이터 추적 및 처리 기능을 확장 합니다. Azure Database for PostgreSQL 서버 만들기를 자동화 하는 데 걸리는 작업의 양을 조사할 수 있습니다.

Azure portal을 사용 하 여 PostgreSQL 서버용 단일 Azure Database 만들기 쉽습니다. 둘 이상의 데이터베이스를 만들고 포털만을 사용 하 여 지속적으로 유지 관리 실행 지루한 될 수 있습니다. 관리 작업을 자동화 하려는 경우 스크립트를 만들려면 Azure CLI를 사용 합니다.

Microsoft Azure 내에서 거의 모든 리소스를 만드는 Azure CLI를 사용 하 여 자동화할 수 있습니다. 이 단위는 Azure CLI를 사용 하 여 PostgreSQL 서버용 Azure Database의 관리를 자동화 하는 방법에 알아봅니다.

## <a name="what-is-the-azure-cli"></a>Azure CLI란?

합니다 [Azure CLI](https://docs.microsoft.com/cli/azure/) Azure 리소스 관리를 위한 Microsoft의 플랫폼 간 명령줄 환경입니다. Azure CLI를 사용 하 여 Azure Cloud Shell을 사용 하 여 브라우저에서 또는 Mac OS X, Linux 또는 Windows에서 Azure CLI를 로컬로 설치할 수 있습니다. Azure CLI는 bash 또는 PowerShell을 사용 하 여 로컬 명령줄에서 실행 됩니다. Azure CLI를 로컬로 실행 추가 설정이 필요 합니다. Azure CLI 명령을 실행 하는 것에 대 한 Azure Cloud Shell 사용 하겠습니다.

## <a name="what-is-azure-cloud-shell"></a>Azure Cloud Shell은 무엇인가요?

Azure Cloud Shell에는 클라우드에서 호스트 되는 인증된 된 세션을 사용 하 여 Azure에 연결할 수 있도록 브라우저 기반 셸 환경입니다. Azure Database for PostgreSQL 서버는 관리를 자동화 하려면 Azure CLI 명령을 실행할 수 있습니다. 일반적인 Azure CLI 도구는 미리 설치 되 고 Cloud shell에 계정을 사용 하 여 사용 하 여 구성 합니다.

> [!NOTE]
> Cloud Shell에는 Cloud Shell에서 작업 하는 동안 만든 모든 파일을 유지 하려면 Azure storage 리소스를 필요 합니다. 처음으로 실행 Cloud Shell 만들라는 메시지가 표시 됩니다는 리소스 그룹, 저장소 계정 및 사용자를 대신해 Azure Files 공유 합니다. 일회성 단계 이며 앞으로 모든 클라우드 셸 세션에 대 한 자동으로 연결 됩니다.

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a>Azure CLI를 사용 하 여 PostgreSQL 서버용 Azure Database 만들기

Azure CLI를 사용 하 여 PostgreSQL 서버용 Azure Database를 만드는 오른쪽에 Azure Cloud Shell 터미널을 사용 합니다.

Azure CLI 서버 생성 사용량 help 명령을 모든 사용 가능한 매개 변수를 보여 주는 다음 예제에서는 다음과 같습니다.

   ```azurecli
   az postgres server create [-h] [--verbose] [--debug]
                             [--output {json,jsonc,table,tsv}]
                             [--query JMESPATH]
                              --resource-group RESOURCE_GROUP_NAME --name SERVER_NAME
                              --sku-name SKU_NAME [--location LOCATION]
                              --admin-user ADMINISTRATOR_LOGIN
                              [--admin-password ADMINISTRATOR_LOGIN_PASSWORD]
                              [--backup-retention BACKUP_RETENTION]
                              [--geo-redundant-backup GEO_REDUNDANT_BACKUP]
                              [--ssl-enforcement {Enabled,Disabled}]
                              [--storage-size STORAGE_MB]
                              [--tags [TAGS [TAGS ...]]]
                              [--version VERSION]
                              [--subscription _SUBSCRIPTION]

   ```

다음 명령줄은 필요한 Azure Database for PostgreSQL 서버를 만들려면 매개 변수 집합을 보여 줍니다. 일부 매개 변수가 선택 사항 이므로 표시 되지 않습니다 알 수 있습니다.

   ```azurecli
   az postgres server create --resource-group <resource_group_name> --name <new_server_name> --admin-user <admin_user_name> --admin-password <server_admin_password> --sku-name <sku> --version <version_number>  --location <region_name> --storage-size <size> --backup-retention <days>
   ```

### <a name="parameter-descriptions"></a>매개 변수 설명

`--resource-group <resource_group_name>` 매개 변수는 서버를 만드는 리소스 그룹을 지정 합니다.

서버 `admin-user` 고 `admin-password` 서버 및 해당 데이터베이스에 로그인 하려면 반드시 지정 해야 합니다. 기억 하거나 새 서버와 상호 작용 하는 경우 나중에 대 한이 정보를 기록 합니다.

사용 된 `--sku-name` 계산 리소스를이 경우 가격 책정 계층의 일부를 지정 하려면 매개 변수입니다. 값은 규칙을 따릅니다. `{pricing tier}_{compute generation}_{vCores}`합니다.

예제:

- `--sku-name B_Gen4_4`는 기본, 4세대 및 vCore 4개에 매핑됩니다.
- `--sku-name GP_Gen5_32`는 범용, 5세대 및 vCore 32개에 매핑됩니다.
- `--sku-name MO_Gen5_2`는 메모리 최적화, 5세대 및 vCore 2개에 매핑됩니다.

포털을 사용 하 여 만든 단위에서 세 가지 가격 책정 계층을 설명한 것을 기억 하십시오.

Basic, Gen 5를 사용 하 고 1 vCore 계산 리소스를 가정해 보겠습니다. 로 매개 변수가 지정 `--sku-name B_Gen5_1`합니다.

사용 된 `--storage-size` 가격 책정 계층의 일부로 지정 하려면 매개 변수입니다. 값을 지정 하지 않으면 다음 기본값으로 5,120MB입니다. 올바른 저장소 5,120MB 이르는 크기 및 최대 1,024MB의 단위로 증가 1,048,576 MB입니다.

`--backup-retention` 일에 지정 된 백업에 대 한 보존 기간을 지정 해야 할 경우 매개 변수를 사용 합니다. 값을 지정 하지 않으면 다음 기본적으로 7 일입니다.

사용 된 `--version` 매개 변수를 사용 하려는 PostgreSQL의 주 버전을 지정 합니다.

이제 Azure CLI를 사용 하 여 PostgreSQL 서버용 Azure Database를 만드는 단계를 확인 했습니다. 다음 장치, Azure CLI를 사용 하 여 PostgreSQL 서버용 Azure 데이터베이스를 만들어야 합니다.