이제 앱이 있으므로 사용할 Azure 저장소 계정이 필요합니다. Azure Portal을 사용하여 **Azure 저장소 계정 만들기** 모듈에서 계정을 만들었습니다. 이번에는 Azure CLI를 사용해 보겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>Azure CLI를 사용하여 Azure 저장소 계정 만들기

`az storage account create` 명령을 사용하여 새 저장소 계정을 만듭니다. 원하는 방식으로 구성하는 데 필요한 몇 가지 매개 변수를 제공하거나 제공해야 합니다.

> [!div class="mx-tableFixed"]
> | 옵션 | 설명 |
> |--------|-------------|
> | `--name` | **저장소 계정 이름**입니다. 이름은 계정의 데이터에 액세스하는 데 사용되는 공용 URL을 생성하는 데 사용됩니다. 이름은 Azure의 모든 기존 저장소 계정 이름 중에서 고유해야 합니다. 3-24자여야 하며, 소문자와 숫자만 포함할 수 있습니다. |
> | `--resource-group` | <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용하여 저장소 계정을 무료 샌드박스에 배치합니다. |
> | `--location` | 사용자에게 가까운 위치를 선택합니다. |
> | `--kind` | 저장소 계정 _유형_을 결정합니다. 옵션으로 BlobStorage, Storage 및 StorageV2가 있습니다. |
> | `--sku` | 저장소 계정 성능 및 복제 모델을 결정합니다. 옵션으로 Premium_LRS, Standard_GRS, Standard_LRS, Standard_RAGRS 및 Standard_ZRS가 있습니다. |
> | `--access-tier` | **액세스 계층**은 Blob 저장소에만 사용되며, 사용 가능한 옵션으로 쿨 및 핫이 있습니다. **핫 액세스 계층**은 자주 액세스하는 데이터에 적합하며, **쿨 액세스 계층**은 자주 액세스하지 않는 데이터에 더 적합합니다. 여기서는 _기본_ 값만 설정합니다. Blob을 만들 때 데이터에 대한 다른 값을 설정할 수 있습니다. |
    
위의 표를 사용하여 오른쪽의 Cloud Shell에서 계정을 만드는 명령줄을 작성합니다.
- 고유한 이름을 사용합니다. 이니셜과 임의의 숫자로 된 "photostore"와 같은 이름을 사용하는 것이 좋습니다. 고유하지 않으면 오류가 발생합니다.
- 샌드박스 리소스 그룹을 사용하는 경우 일반적으로 응용 프로그램 리소스를 보관할 새 리소스 그룹을 만듭니다.
- **sku**에 대해 "Standard_LRS"를 사용합니다. 이 예에서는 로컬 복제가 있는 표준 저장소를 사용합니다.
- **액세스 계층**에 대해 "콜드"를 사용합니다.

### <a name="selecting-a-location"></a>위치 선택
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a>명령 예제

```bash
az storage account create \
        --name <name> \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \ 
        --access-tier Cold
```

> [!TIP]
> 저장소 계정에 대한 옵션을 알아보려면 **Azure 저장소 계정 만들기**로 이동하여 자세히 살펴보세요.

계정을 배포하는 데는 몇 분이 걸립니다. Azure에서 이 작업을 수행하는 동안 이 계정에서 사용할 API를 살펴보겠습니다.