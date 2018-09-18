Azure Database for PostgreSQL을 만들어 주자의 체력 장치에서 캡처된 경로를 저장하기로 결정했습니다. 기록이 캡처되는 데이터 볼륨에 따라 서버 저장소 요구 사항을 20GB로 설정해야 합니다. 처리 요구 사항을 지원하려면 1개 vCore를 갖춘 5세대 계산을 지원해야 합니다. 또한 데이터 백업에는 15일의 보존 기간이 필요하다는 것도 알고 있습니다.

> [!TIP]
> Microsoft Learn에서 수행하는 모든 연습에는 추가 비용이 들지 않지만, 직접 탐색을 시작하면 Azure 구독이 필요합니다. 아직 구독이 없는 경우 몇 분 정도 시간을 내어 [체험 계정](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)을 만듭니다.

시작해 보겠습니다.

[Azure Portal](https://portal.azure.com?azure-portal=true)에 로그인합니다.

Azure Cloud Shell 세션을 시작해야 합니다. 화면 위쪽에 있는 Cloud Shell 아이콘을 선택하여 세션을 시작합니다.

![Cloud Shell 단추](../media-draft/cloud-shell-button.png)

Cloud Shell에서 사용할 저장소 계정이 아직 없으면 첫 번째 액세스 권한으로 저장소 계정을 만들어야 합니다. 포털 인터페이스에서 저장소 계정을 만드는 프로세스를 안내합니다.

이 랩에서는 `bash`를 명령줄 환경으로 사용합니다.

1. 서버를 만드는 데 사용할 구독을 선택합니다.

    구독이 여러 개 있는 경우 다음 명령을 사용하여 해당 구독을 활성화하여 0을 사용자의 구독 식별자로 바꿔야 합니다.

    ``` bash
    az account set --subscription "00000000-0000-0000-0000-000000000000"
    ```

    `az account list --output table` 명령을 사용하여 모든 구독을 나열할 수 있습니다. 이 목록에서 사용하려는 구독 식별자를 선택합니다.

1. 이전 단원에서 리소스 그룹을 아직 만들지 않았으면 하나를 만듭니다. 다음 명령을 실행합니다.

    ```bash
    az group create --name <resource_group_name> --location <location>
    ```

    > [!Note]
    > `az account list-locations` 명령을 사용하여 모든 위치에 대한 목록을 검색할 수 있습니다. `displayName` 또는 `name` 값을 선택하고, `<location>` 매개 변수에 이 값을 사용합니다.

1. 이제 `az postgres server create` 명령을 실행할 준비가 되었습니다.

    서버 저장소 크기를 20GB로 설정하고, 1개의 vCore 및 15일의 데이터 백업 보존 기간을 갖춘 계산 5세대를 지원하려고 한다는 것을 명심하세요.

    지정할 몇 가지 매개 변수가 있습니다.

    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`

    아래의 솔루션을 살펴보지 않고도 명령을 작성하고 매개 변수를 완성할 수 있는지 확인합니다. `<>`의 값을 사용자 고유의 값으로 바꿉니다.

    > [!NOTE]
    > `az account list-locations` 명령을 사용하여 모든 위치에 대한 목록을 검색할 수 있습니다. `displayName` 또는 `name` 값을 선택하고, `<location>` 매개 변수에 이 값을 사용합니다.

    ```bash
    az postgres server create --resource-group <resource_group_name> --name <unique_server_name>  --location "UK West" --admin-user <server_admin_login_id> --admin-password <server_admin_password> --sku-name B_Gen5_1 --storage-size 20480 --backup-retention 15 --version 10
    ```

실행되면 시스템에서 정보를 처리하는 데 몇 분이 걸립니다. 서버가 만들어진 경우 해당 서버를 설명하는 JSON(Java Script Object Notation) 문자열이 반환됩니다. 서버가 만들어지지 않은 경우 오류 메시지가 표시됩니다. 이 오류 정보를 사용하여 명령 매개 변수를 검토하고 수정합니다.

Azure CLI를 사용하여 PostgreSQL 서버를 성공적으로 만들었습니다. 다음 단원에서는 서버의 보안 설정을 구성하는 방법을 알아봅니다.
