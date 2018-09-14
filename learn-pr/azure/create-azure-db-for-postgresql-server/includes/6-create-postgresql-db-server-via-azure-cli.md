실행 기의 적합성에 대 한 장치에서 캡처된 경로 저장 하는 Azure Database for PostgreSQL 서버 만들기로 결정 합니다. 기록 캡처된 데이터 볼륨에 따라 알고 20GB에 서버 저장소 요구 사항을 설정 해야 합니다. 처리 요구를 지원 하려면 1 vCore 사용 하 여 Gen 5 지원을 계산 해야 합니다. 또한 데이터 백업의 보존 기간을 15 일로 필요한를 파악 합니다.

시작 해 보겠습니다.

에 20GB에 서버 저장소 크기를 설정, Gen 5 지원 vCore 1 개 및 데이터 백업에 대 한 일의 보존 기간을 사용 하 여 계산를 하려고 합니다.

지정 하는 여러 매개 변수를 가지 있습니다.

- `--resource-group <resource_group_name>`
- `--name <new_server_name>`
- `--location <location>`
- `--admin-user <admin_user_name>`
- `--admin-password <server_admin_password>`
- `--sku-name <sku>`
- `--storage-size <size>`
- `--backup-retention <days>`
- `--version <version_number>`

명령을 작성 하 고 아래 솔루션 확인 하지 않고 매개 변수를 완료할 수 하는 경우를 참조 하세요. 값을 바꾸는 `<>` 를 고유한 값입니다.

> [!NOTE]
> 이 명령을 사용 하 여 모든 위치 목록을 검색할 수 있습니다 `az account list-locations`합니다. 선택 합니다 `displayName` 또는 `name` 에 대 한 사용을 `<location>` 매개 변수입니다.

```bash
az postgres server create --resource-group <rgn>[Sandbox resource group name]</rgn> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
```

시스템 정보를 실행 하는 경우를 처리 하는 데 몇 분 정도 볼 수 있습니다. 서버를 만든 경우 서버를 설명 하는 개체 JSON (JavaScript Notation) 문자열로 반환 됩니다. 서버 생성 되지 않습니다 하는 경우 오류 메시지가 표시 됩니다. 이 오류 정보를 사용 하 여 검토 하 고 명령 매개 변수를 수정 하겠습니다.

Azure CLI를 사용 하 여 PostgreSQL 서버를 성공적으로 만들었습니다. 다음 단위에 있는 서버의 보안 설정을 구성 하는 방법을 배웁니다.
