Azure Database for PostgreSQL 서버를 만들어 실행기의 적합성 장치에서 캡처한 경로를 저장하기로 결정했습니다. 기록이 캡처되는 데이터 볼륨에 따라 서버 저장소 요구 사항을 20GB로 설정해야 합니다. 처리 요구 사항을 지원하려면 1개 vCore를 갖춘 5세대 계산을 지원해야 합니다. 또한 데이터 백업에는 15일의 보존 기간이 필요하다는 것도 알고 있습니다.

## <a name="create-an-azure-postgresql-database-with-the-azure-cli"></a>Azure CLI를 사용하여 Azure PostGreSQL 데이터베이스 만들기

서버 저장소 크기를 20GB로 설정하고, 1 vCore로 5세대 지원을 계산하고, 데이터 백업을 위한 15일의 보존 기간을 지정하고자 합니다.

1. `az postgres server create` 메서드를 사용하여 새 데이터베이스를 만듭니다. 지정할 몇 가지 매개 변수가 있습니다.
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`
    
2. 아래 솔루션을 살펴보지 않고도 명령을 빌드하고 매개 변수를 완료할 수 있는지 확인합니다. 다음은 몇 가지 팁입니다.
    - `<values>`를 고유의 값으로 바꿉니다. 
    - 서버 이름은 소문자 'a'-'z', 숫자 0-9 및 하이픈으로 구성되어야 합니다.
    - <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 리소스 그룹으로 사용합니다.
    - [!include[](../../../includes/azure-sandbox-regions-note.md)] 목록의 위치를 사용합니다.
    
```bash
az postgres server create --name <unique_server_name> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \ 
    --location eastus \
    --sku-name B_Gen5_1 \
    --storage-size 20480 \
    --backup-retention 15 \
    --version 10 \
    --admin-user <admin_user_name> \
    --admin-password <server_admin_password>
```

시스템은 실행 시 정보를 처리하는 데 몇 분 정도 걸립니다. 명령이 완료될 때까지 계속해서 기다립니다.

완료되면 해당 서버를 설명하는 JSON(JavaScript Object Notation) 문자열이 반환됩니다. 실패한 경우 오류 메시지가 표시됩니다. 이 오류 정보를 사용하여 명령 매개 변수를 검토하고 수정한 후 다시 시도할 수 있습니다.

JSON 개체는 다음과 같이 표시됩니다.

```json
{
  "administratorLogin": "azureuser",
  "earliestRestoreDate": "2018-09-17T00:35:50.170000+00:00",
  "fullyQualifiedDomainName": "secondserver8.postgres.database.azure.com",
  "id": "/subscriptions/xxxxx/resourceGroups/<rgn>[sandbox Resource Group]</rgn>/providers/Microsoft.DBforPostgreSQL/servers/secondserver8",
  "location": "eastus",
  "name": "secondserver8",
  "resourceGroup": "<rgn>[sandbox Resource Group]</rgn>",
  "sku": {
    "capacity": 1,
    "family": "Gen5",
    "name": "B_Gen5_1",
    "size": null,
    "tier": "Basic"
  },
  "sslEnforcement": "Enabled",
  "storageProfile": {
    "backupRetentionDays": 15,
    "geoRedundantBackup": "Disabled",
    "storageMb": 20480
  },
  "tags": null,
  "type": "Microsoft.DBforPostgreSQL/servers",
  "userVisibleState": "Ready",
  "version": "10"
}
```

Azure CLI를 사용하여 PostgreSQL 서버를 성공적으로 만들었습니다. 다음 단원에서는 서버의 보안 설정을 구성하는 방법을 알아봅니다.
