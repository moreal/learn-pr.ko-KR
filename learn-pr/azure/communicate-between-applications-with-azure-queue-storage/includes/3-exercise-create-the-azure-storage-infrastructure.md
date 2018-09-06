중간 계층에서 트래픽이 급증할 수 있다는 사실이 확인되었습니다. 이를 처리하기 위해 기사 업로드 응용 프로그램의 프런트 엔드 및 중간 계층 사이에 큐를 추가하기로 했습니다.

큐를 만드는 첫 번째 단계는 데이터를 저장할 Azure Storage 계정을 만드는 것입니다.

## <a name="create-a-storage-account-with-the-azure-cli"></a>Azure CLI를 사용하여 저장소 계정 만들기

시작하기 위해 저장소 계정을 보유할 Azure 리소스 그룹을 만들어보겠습니다.

1. 오른쪽의 Cloud Shell에서 Bash 선택 옵션이 제공되면 Bash를 선택합니다.

2. `az group create` Azure CLI 명령을 사용하여 새 리소스 그룹을 만듭니다. 이름을 **ExerciseResources**로 지정하고 가까운 위치에 둡니다. 
    - 아래 예제에서는 위치로 “eastus”를 사용합니다.

    ```azurecli
    az group create -n ExerciseResources --location eastus
    ```
        
2. 다음으로 `az storage account create` 명령을 사용하여 실제 저장소 계정을 만듭니다. 다음과 같은 몇 가지 매개 변수를 제공해야 합니다.

| 매개 변수 | 값 |
|-----------|-------|
| `--name`  | 이름을 설정합니다. 저장소 계정은 이 이름을 사용하여 공용 URL을 생성하므로 이 이름은 고유해야 합니다. 또한 계정 이름은 3-24자 사이여야 하며 숫자와 소문자만으로 구성되어야 합니다. 접두사 **articles**와 무작위 숫자 접미사로 사용하는 것이 좋지만 어떤 접미사도 사용 가능합니다. |
| `-g`        | 리소스 그룹을 제공하고 값으로 **ExerciseResources**를 사용합니다. |
| `--kind`    | 저장소 계정 유형을 설정합니다. 범용 V2 계정을 생성하려면 **StorageV2**를 사용합니다. |
| `-l`        | 리소스 그룹 소유자는 별도로 위치를 설정합니다. 선택적이지만 리소스 그룹과는 다른 지역에 큐를 배치하는 데 사용할 수 있습니다. |
| `--sku`     | 계정 유형을 설정합니다. 기본 유형은 **Standard_RAGRS**이지만, 이 데모에서는 불필요합니다. 여기서는 데이터 센터 내에서 로컬로만 중복되는 것을 의미하는 **Standard_LRS**를 사용하겠습니다. |

다음은 위의 매개 변수를 사용하는 예제 명령줄입니다. 이 명령을 복사하여 붙여넣으려면 `--name` 매개 변수를 고유한 다른 값으로 변경하세요.

```azurecli
az storage account create --name <name> -g ExerciseResources --kind StorageV2 -l eastus --sku Standard_LRS
```
