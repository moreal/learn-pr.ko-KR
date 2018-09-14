이제 앱을 만들었으므로 Azure storage 계정을 사용 해야 합니다. Azure portal을 사용 하 여 만든 합니다 **Azure storage 계정 만들기** 모듈입니다. 이 이번에 Azure CLI를 사용 합니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="use-the-azure-cli-to-create-an-azure-storage-account"></a>Azure CLI를 사용 하 여 Azure storage 계정을 만들려면

사용 하 여는 `az storage account create` 새 저장소 계정을 만드는 명령입니다. 에서는 제공 해야 (또는 해야)는 여러 매개 변수를 사용 하려면 원하는 방식으로 구성 합니다.

> [!div class="mx-tableFixed"]
> | 옵션 | 설명 |
> |--------|-------------|
> | `--name` | A **저장소 계정 이름**합니다. 계정에서 데이터에 액세스 하는 데 공용 URL을 생성 하는 이름 사용 됩니다. Azure의 모든 기존 저장소 계정 이름에서 고유 해야 합니다. 3 ~ 24 자 여야 하 고 소문자와 숫자만 포함할 수 있습니다. |
> | `--resource-group` | 사용 하 여 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 무료 샌드박스를 저장소 계정에 배치할 수 있습니다. |
> | `--location` | 가까운 위치를 선택 하 고 (아래 참조) 키를 누릅니다. |
> | `--kind` | 이 저장소 계정에 따라 결정 _형식_합니다. 옵션에 포함 됩니다 `BlobStorage`, `Storage`, 및 `StorageV2`합니다. |
> | `--sku` | 이 저장소 계정의 성능 및 복제 모델을 결정합니다. 옵션에 포함 됩니다 `Premium_LRS`, `Standard_GRS`를 `Standard_LRS`를 `Standard_RAGRS`, 및 `Standard_ZRS`합니다. |
> | `--access-tier` | 합니다 **액세스 계층** 는 사용 가능한 옵션은 [Blob 저장소에 대 한 사용만`Cool` | `Hot`]. 합니다 **핫 액세스 계층** 자주 액세스 하는 데이터에 적합 하며 **쿨 액세스 계층** 자주 액세스 하지 않는 데이터에 대 한 것이 좋습니다. 이 설정 하는 참고 합니다 _기본_ 값&mdash;Blob을 만들 때 데이터에 대 한 다른 값을 설정할 수 있습니다. |
    
위의 표를 사용 하 여 계정을 만들려면 오른쪽 Cloud Shell에서 명령줄을 만들 수 있습니다.
- 고유한 이름을 사용합니다. "Photostore" 난수 이니셜에 숫자와 같은 것이 좋습니다. 고유 하지 않은 경우 오류를 받습니다.
- 일반적으로 앱 리소스를 보유 하지만 경우 샌드박스 리소스 그룹을 사용 하 여 새 리소스 그룹을 만듭니다.
- 에 대 한 "Standard_LRS"를 사용 합니다 **sku**합니다. 이 사용할지 표준 저장소 지역 복제를 사용 하 여이 예제에 대 한 것입니다.
- 에 대 한 "콜드"를 사용 합니다 **액세스 계층**합니다.

### <a name="selecting-a-location"></a>위치 선택
<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

### <a name="example-command"></a>예제 명령

```azurecli
az storage account create \
        --name <name> \
        --resource-group <rgn>[Sandbox resource group name]</rgn> \
        --location <region> \
        --kind StorageV2 \
        --sku Standard_LRS \ 
        --access-tier Cool
```

> [!TIP]
> 저장소 계정에 대 한 옵션을 살펴보려는 경우 진행할 수 있는지 확인 합니다 **Azure storage 계정 만들기** 갈 통해 방어 합니다.

계정 배포 하려면 몇 분 정도 걸립니다. Azure에 작동 하는 동안이 계정으로 사용 하는 Api를 살펴보겠습니다.