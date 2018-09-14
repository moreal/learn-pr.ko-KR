중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다. 이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.

큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="create-a-storage-account-with-the-azure-cli"></a>Azure CLI를 사용하여 저장소 계정 만들기

> [!TIP] 
> 일반적으로 새 프로젝트를 만드는 것으로 시작 된 _리소스 그룹_ 연결 된 모든 리소스를 보유 하 합니다. 이 경우 사용할 것 이라는 리소스 그룹을 제공 하는 Azure 샌드박스에 <rgn>[샌드박스 리소스 그룹 이름]</rgn>합니다.

1. 오른쪽의 Cloud Shell에서 Bash 선택 옵션이 제공되면 Bash를 선택합니다.

1. 사용 하 여는 `az storage account create` 저장소 계정을 만드는 명령입니다. 다음과 같은 몇 가지 매개 변수를 제공해야 합니다.

| 매개 변수 | 값 |
|-----------|-------|
| `--name`  | 이름을 설정합니다. 저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다. 또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다. 접두사 **articles**와 무작위 숫자 접미사로 사용하는 것이 좋지만 어떤 접미사도 사용 가능합니다. |
| `-g`        | 제공 된 **리소스 그룹**를 사용 하 여 <rgn>[샌드박스 리소스 그룹 이름]</rgn> 값으로. |
| `--kind`    | 설정 된 **저장소 계정 유형** -사용 _StorageV2_ 범용 V2 계정을 만들려면. |
| `-l`        | 설정 된 **위치** 리소스 그룹 소유자와 무관 합니다. 선택적이지만 리소스 그룹과는 다른 지역에 큐를 배치하는 데 사용할 수 있습니다. |
| `--sku`     | 집합을 **복제 및 저장소 형식**을 기본값으로 _Standard_RAGRS_합니다. 여기서는 데이터 센터 내에서 로컬로만 중복되는 것을 의미하는 _Standard_LRS_를 사용하겠습니다. |

<!-- Resource selection -->
[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

다음은 위의 매개 변수를 사용하는 예제 명령줄입니다. 변경 해야 합니다 `--name` 및 `--location` 로 복사/붙여넣기이 명령 결정 하는 경우 매개 변수입니다.

```azurecli
az storage account create --name [unique-name] -g <rgn>[Sandbox resource group name]</rgn> --kind StorageV2 -l [location-name] --sku Standard_LRS
```