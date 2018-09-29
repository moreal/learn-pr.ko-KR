<span data-ttu-id="8fcc3-101">Azure Database for PostgreSQL 서버를 만들어 실행기의 적합성 장치에서 캡처한 경로를 저장하기로 결정했습니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-101">You decide to create an Azure Database for PostgreSQL server to store routes captured from runners' fitness devices.</span></span> <span data-ttu-id="8fcc3-102">기록이 캡처되는 데이터 볼륨에 따라 서버 저장소 요구 사항을 20GB로 설정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-102">Based on historic captured data volumes, you know your server storage requirements should be set at 20 GB.</span></span> <span data-ttu-id="8fcc3-103">처리 요구 사항을 지원하려면 1개 vCore를 갖춘 5세대 계산을 지원해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-103">To support your processing requirements, you need compute Gen 5 support with 1 vCore.</span></span> <span data-ttu-id="8fcc3-104">또한 데이터 백업에는 15일의 보존 기간이 필요하다는 것도 알고 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-104">You also know that you require a retention period of 15 days for data backups.</span></span>

## <a name="create-an-azure-postgresql-database-with-the-azure-cli"></a><span data-ttu-id="8fcc3-105">Azure CLI를 사용하여 Azure PostGreSQL 데이터베이스 만들기</span><span class="sxs-lookup"><span data-stu-id="8fcc3-105">Create an Azure PostGreSQL database with the Azure CLI</span></span>

<span data-ttu-id="8fcc3-106">서버 저장소 크기를 20GB로 설정하고, 1 vCore로 5세대 지원을 계산하고, 데이터 백업을 위한 15일의 보존 기간을 지정하고자 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-106">Keep in mind you want to set your server storage size at 20 GB, compute Gen 5 support with 1 vCore and a retention period of 15 days for data backups.</span></span>

1. <span data-ttu-id="8fcc3-107">`az postgres server create` 메서드를 사용하여 새 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-107">Use the `az postgres server create` method to create a new database.</span></span> <span data-ttu-id="8fcc3-108">지정할 몇 가지 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-108">There are several parameters that you'll specify:</span></span>
    - `--resource-group <resource_group_name>`
    - `--name <new_server_name>`
    - `--location <location>`
    - `--admin-user <admin_user_name>`
    - `--admin-password <server_admin_password>`
    - `--sku-name <sku>`
    - `--storage-size <size>`
    - `--backup-retention <days>`
    - `--version <version_number>`
    
2. <span data-ttu-id="8fcc3-109">아래 솔루션을 살펴보지 않고도 명령을 빌드하고 매개 변수를 완료할 수 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-109">See if you can build the command and complete the parameters without looking at the solution below.</span></span> <span data-ttu-id="8fcc3-110">다음은 몇 가지 팁입니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-110">Here are some tips.</span></span>
    - <span data-ttu-id="8fcc3-111">`<values>`를 고유의 값으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-111">Replace the `<values>` with your own values.</span></span> 
    - <span data-ttu-id="8fcc3-112">서버 이름은 소문자 'a'-'z', 숫자 0-9 및 하이픈으로 구성되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-112">Remember that the server name must be  made up of lowercase letters 'a'-'z', the numbers 0-9 and the hyphen.</span></span>
    - <span data-ttu-id="8fcc3-113"><rgn>[샌드박스 리소스 그룹 이름]</rgn>을 리소스 그룹으로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-113">Use <rgn>[sandbox resource group name]</rgn> as the resource group.</span></span>
    - <span data-ttu-id="8fcc3-114">[!include[](../../../includes/azure-sandbox-regions-note.md)] 목록의 위치를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-114">Use a location from the following list:   [!include[](../../../includes/azure-sandbox-regions-note.md)]</span></span>
    
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

<span data-ttu-id="8fcc3-115">시스템은 실행 시 정보를 처리하는 데 몇 분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-115">The system will take a few moments to process the information when executed.</span></span> <span data-ttu-id="8fcc3-116">명령이 완료될 때까지 계속해서 기다립니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-116">Go ahead and wait for the command to complete.</span></span>

<span data-ttu-id="8fcc3-117">완료되면 해당 서버를 설명하는 JSON(JavaScript Object Notation) 문자열이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-117">Once it's done, a JavaScript Object Notation (JSON) string that describes the server is returned.</span></span> <span data-ttu-id="8fcc3-118">실패한 경우 오류 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-118">If there was a failure, an error message is displayed.</span></span> <span data-ttu-id="8fcc3-119">이 오류 정보를 사용하여 명령 매개 변수를 검토하고 수정한 후 다시 시도할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-119">You can use this error information to review and fix your command parameters and try again.</span></span>

<span data-ttu-id="8fcc3-120">JSON 개체는 다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-120">The JSON object will look something like:</span></span>

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

<span data-ttu-id="8fcc3-121">Azure CLI를 사용하여 PostgreSQL 서버를 성공적으로 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-121">You've successfully created a PostgreSQL server using the Azure CLI.</span></span> <span data-ttu-id="8fcc3-122">다음 단원에서는 서버의 보안 설정을 구성하는 방법을 알아봅니다.</span><span class="sxs-lookup"><span data-stu-id="8fcc3-122">In the next unit, you'll see how to configure your server's security settings.</span></span>
