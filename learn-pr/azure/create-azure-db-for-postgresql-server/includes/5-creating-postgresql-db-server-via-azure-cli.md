온-프레미스 PostgreSQL 데이터베이스를 사용한다고 가정해 보겠습니다. 현재 회사에서 서버를 Azure로 이동하여 장치 지원, 가용성, 데이터 추적 및 처리 기능을 확장하려고 합니다. Azure Database for PostgreSQL 서버의 생성을 자동화하려면 얼마나 많은 노력이 필요한지 조사해야 합니다.

Azure Portal을 사용하여 단일 Azure Database for PostgreSQL 서버를 쉽게 만들 수 있습니다. 포털만 사용하여 데이터베이스를 두 개 이상 만들고 유지 관리를 지속적으로 실행하는 것은 지루한 일이 될 수 있습니다. 관리 작업을 자동화하려는 경우 Azure CLI를 사용하여 스크립트를 만듭니다.

Azure CLI를 사용하여 Microsoft Azure 내에서 거의 모든 리소스 생성을 자동화할 수 있습니다. 이 단원에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 관리를 자동화하는 방법을 알아보겠습니다.

## <a name="what-is-the-azure-cli"></a>Azure CLI란?

[Azure CLI](https://docs.microsoft.com/cli/azure/)는 Azure 리소스를 관리하기 위한 Microsoft의 플랫폼 간 명령줄 환경입니다. 브라우저에서 Azure Cloud Shell을 통해 Azure CLI를 사용할 수도 있고 Mac OS X, Linux 또는 Windows에 로컬로 Azure CLI를 설치할 수도 있습니다. Azure CLI는 bash 또는 PowerShell을 사용하여 로컬 명령줄에서 실행됩니다. Azure CLI를 로컬로 실행하려면 추가 설정이 필요합니다. 여기서는 Azure Cloud Shell을 사용하여 Azure CLI 명령을 실행하겠습니다.

## <a name="what-is-azure-cloud-shell"></a>Azure Cloud Shell이란?

Azure Cloud Shell은 클라우드에 호스트되는 브라우저 기반 셸 환경으로, 인증된 세션을 사용하여 Azure에 연결할 수 있게 해줍니다. Azure CLI 명령을 실행하여 Azure Database for PostgreSQL 서버 관리를 자동화할 수 있습니다. 계정에서 사용할 수 있도록 공용 Azure CLI 도구가 Cloud Shell에 사전 설치 및 구성되어 있습니다.

> [!NOTE]
> Cloud Shell은 Cloud Shell에서 작업하는 동안 만든 파일을 유지하려면 Azure 저장소 리소스가 필요합니다. 처음 시작하면 Cloud Shell은 사용자를 대신하여 리소스 그룹, 저장소 계정 및 Azure Files 공유를 만들라는 메시지를 표시합니다. 이는 일회성 단계이며 이후의 모든 Cloud Shell 세션에 대해 자동으로 연결됩니다.

## <a name="create-an-azure-database-for-postgresql-server-using-the-azure-cli"></a>Azure CLI를 사용하여 Azure Database for PostgreSQL 서버 만들기

오른쪽에 있는 Azure Cloud Shell 터미널을 사용하여 Azure CLI를 통해 Azure Database for PostgreSQL 서버를 만듭니다.

사용 가능한 모든 매개 변수를 보여 주는 Azure CLI 서버 만들기 명령 사용 도움말은 다음 예제와 같이 표시합니다.

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

선택적 매개 변수는 대괄호로 묶여 있습니다. 몇 가지 일반적인 것들을 살펴보겠습니다.

### <a name="parameters"></a>매개 변수

`--resource-group <resource_group_name>` 매개 변수는 서버를 만들 리소스 그룹을 지정합니다.

여러분이 지정하는 서버 `admin-user` 및 `admin-password`는 서버와 데이터베이스에 로그인하는 데 필요합니다. 나중에 새 서버와 상호 작용할 때 이 정보를 기억하거나 기록해 두세요.

`--sku-name` 매개 변수를 사용하여 가격 책정 계층의 일부(이 경우 계산 리소스)를 지정합니다. 값은 `{pricing tier}_{compute generation}_{vCores}` 규칙을 따릅니다.

예제:

- `--sku-name B_Gen4_4`는 기본, 4세대 및 vCore 4개에 매핑됩니다.
- `--sku-name GP_Gen5_32`는 범용, 5세대 및 vCore 32개에 매핑됩니다.
- `--sku-name MO_Gen5_2`는 메모리 최적화, 5세대 및 2 vCore에 매핑됩니다.

포털을 사용하여 서버를 만드는 단원에서 세 가지 가격 책정 계층에 대해 설명했습니다.

기본, 5세대, 1 vCore 계산 리소스를 사용한다고 가정합니다. 매개 변수를 `--sku-name B_Gen5_1`로 지정합니다.

`--storage-size` 매개 변수를 사용하여 가격 책정 계층의 일부를 지정합니다. 값을 지정하지 않으면 기본값은 5,120MB입니다. 유효한 저장소 크기 범위는 5,120MB부터 1,024MB 단위로 증가하여 1,048,576MB까지 증가합니다.

`--backup-retention` 매개 변수는 일 단위로 지정된 백업 보존 기간을 지정해야 할 때 사용됩니다. 값을 지정하지 않으면 기본값은 7일입니다.

`--version` 매개 변수를 통해 사용하려는 PostgreSQL의 주 버전을 지정합니다.

이제 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버를 만드는 단계를 살펴보았습니다. 다음 단원에서는 Azure CLI를 사용하여 Azure Database for PostgreSQL 서버를 만들겠습니다.