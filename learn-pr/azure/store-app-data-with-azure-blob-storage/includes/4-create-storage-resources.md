저장소 계정, 컨테이너 및 Blob에서 데이터를 저장하는 방법을 이해한 후 앱을 지원하기 위해 만들어야 하는 Azure 리소스를 생각할 수 있습니다.

### <a name="storage-accounts"></a>Storage 계정

저장소 계정 만들기는 앱을 배포하고 실행하기 전에 발생하는 관리 작업입니다. 계정은 일반적으로 배포 또는 환경 설정 스크립트, Azure Resource Manager 템플릿을 통해 또는 관리자가 수동으로 만듭니다. 관리 도구 이외의 응용 프로그램에는 일반적으로 저장소 계정을 만들 권한이 없습니다.

### <a name="containers"></a>컨테이너

저장소 계정 만들기와 달리 컨테이너 만들기는 앱 내에서 수행할 수 있는 간단한 작업입니다. 앱이 작업의 일부로 컨테이너를 만들고 삭제하는 것은 일반적이지 않습니다.

하드 코드되거나 미리 구성된 이름이 있는 알려진 컨테이너 집합을 사용하는 앱의 경우 일반적으로 앱에서 필요한 컨테이너를 시작 시 또는 처음 사용 시(컨테이너가 존재하지 않는 경우) 만들도록 합니다. 앱 배포의 일부로 만드는 대신 앱이 컨테이너를 만들도록 하면 응용 프로그램 및 배포 프로세스가 앱에서 사용하는 컨테이너의 이름을 알 필요가 없습니다.

## <a name="exercise"></a>연습

Azure Blob Storage를 사용하도록 코드를 추가하여 완료되지 않은 ASP.NET Core 앱을 완료하겠습니다. 이 연습에서는 조직 및 이름 지정 체계를 디자인하기보다는 Blob Storage API를 살펴보지만, 다음은 앱 및 앱이 데이터를 저장하는 방법에 대한 빠른 개요입니다.

![FileUploader 웹앱 스크린샷](../media/4-fileuploader-with-files.PNG)

앱은 파일 업로드를 허용하고 파일을 다운로드할 수 있는 공유 폴더와 같이 작동합니다. Blob을 구성하는 데 데이터베이스를 사용하지 않고, 대신에 업로드된 파일의 이름을 삭제하고 직접 Blob 이름으로 사용합니다. 모든 업로드된 파일은 단일 컨테이너에 저장됩니다.

먼저 코드를 컴파일하고 실행하지만 데이터 저장 및 로드를 담당하는 파트는 비어 있습니다. 코드를 완료한 후 Azure App Service에 앱을 배포하고 테스트합니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

앱에 대한 저장소 인프라를 설정하겠습니다.

### <a name="storage-account"></a>저장소 계정

Azure CLI와 함께 Azure Cloud Shell을 사용하여 저장소 계정을 만듭니다. 저장소 계정에 고유한 이름을 입력해야 합니다. &mdash; 나중에 사용하기 위해 기록해 둡니다. 아래 예제에서 "미국 동부"를 사용하지만 목록에서 사용 가능한 위치 중 하나로 변경할 수 있습니다.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

다음 명령을 실행하여 저장소 계정을 만듭니다. 

```azurecli
az storage account create --name <your-unique-storage-account-name> --resource-group <rgn>[sandbox resource group name]</rgn> --location eastus --kind StorageV2
```

> [!NOTE]
> `--kind StorageV2`를 사용하는 이유 몇 가지 다른 유형의 저장소 계정이 있습니다. 대부분의 경우 범용 v2 계정을 사용해야 합니다. `--kind StorageV2`를 명시적으로 지정해야 하는 유일한 이유는 범용 v2 계정이 아직도 상당히 새롭고 Azure Portal 또는 Azure CLI에서 기본값으로 설정되지 않았기 때문입니다.

### <a name="container"></a>컨테이너

이 모듈에서 작업하는 앱은 단일 컨테이너를 사용합니다. 앱이 시작 시 컨테이너를 만드는 모범 사례를 따르겠습니다. 그러나 컨테이너 만들기는 Azure CLI에서 수행할 수 있습니다. 설명서를 보려면 Cloud Shell 터미널에서 `az storage container create -h`를 실행합니다.