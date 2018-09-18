중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다. 이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.

큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a>Azure CLI를 사용하여 저장소 계정 만들기

> [!TIP] 
> 일반적으로 모든 연결된 리소스를 포함할 _리소스 그룹_을 만들어 새 프로젝트를 시작합니다. 이 경우 <rgn>[샌드박스 리소스 그룹 이름]</rgn>이라는 리소스 그룹을 제공하는 Azure 샌드박스를 사용합니다.

1. 오른쪽의 Cloud Shell에서 Bash 선택 옵션이 제공되면 Bash를 선택합니다.

1. `az storage account create` 명령을 사용하여 저장소 계정을 만듭니다. 다음과 같은 몇 가지 매개 변수를 제공해야 합니다.

| 매개 변수 | 값 |
|-----------|-------|
| `--name`  | 이름을 설정합니다. 저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다. 또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다. 접두사 **articles**와 무작위 숫자 접미사로 사용하는 것이 좋지만 어떤 접미사도 사용 가능합니다. |
| `-g`        | **리소스 그룹**을 제공하고 값으로 <rgn>[샌드박스 리소스 그룹 이름]</rgn>을 사용합니다. |
| `--kind`    | **저장소 계정 유형**을 설정합니다. _StorageV2_를 사용하여 범용 V2 계정을 만듭니다. |
| `-l`        | 리소스 그룹 소유자와 관계없이 **위치**를 설정합니다. 선택적이지만 리소스 그룹과는 다른 지역에 큐를 배치하는 데 사용할 수 있습니다. |
| `--sku`     | **복제 및 저장소 유형**을 설정합니다. 기본값인 _Standard_RAGRS_로 설정됩니다. 여기서는 데이터 센터 내에서 로컬로만 중복되는 것을 의미하는 _Standard_LRS_를 사용하겠습니다. |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

다음은 위의 매개 변수를 사용하는 예제 명령줄입니다. 이 명령을 복사하여 붙여넣으려면 `--name` 및 `--location` 매개 변수를 변경해야 합니다.

```azurecli
az storage account create --name [unique-name] -g <rgn>[Sandbox resource group name]</rgn> --kind StorageV2 -l [location-name] --sku Standard_LRS
```