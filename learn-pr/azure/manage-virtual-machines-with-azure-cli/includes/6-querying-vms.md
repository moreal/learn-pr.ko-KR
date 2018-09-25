이제 가상 머신이 생성되었으므로 다른 명령을 통해 가상 머신에 대한 정보를 가져올 수 있습니다.

먼저 `vm list`를 살펴보겠습니다.

```azurecli
az vm list
```

이 명령은 이 구독에 정의된 ‘모든’ 가상 머신을 반환합니다. `--resource-group` 매개 변수를 통해 출력을 특정 리소스 그룹으로 필터링할 수 있습니다. 

## <a name="output-types"></a>출력 형식
지금까지 수행한 모든 명령의 기본 응답 유형은 JSON입니다. 이는 스크립팅에 적합하지만 대부분의 사용자가 읽기 어렵습니다. `--output` 플래그를 통해 응답의 출력 스타일을 변경할 수 있습니다. 예를 들어 Azure Cloud Shell에서 다음 명령을 시도하여 다른 출력 스타일을 확인합니다.

```azurecli
az vm list --output table
```

`table`과 함께 `json`(기본값), `jsonc`(색으로 표시된 JSON) 또는 `tsv`(테이블로 구분된 값)를 지정할 수 있습니다. 위 명령에서 몇 가지 변형을 시도하여 차이를 확인합니다.

## <a name="getting-the-ip-address"></a>IP 주소 가져오기

또 다른 유용한 명령은 `vm list-ip-addresses`로, VM의 공용 및 개인 IP 주소를 나열합니다. 주소가 변경되거나 만드는 동안 주소를 캡처하지 않은 경우 언제든지 주소를 검색할 수 있습니다.

```azurecli
az vm list-ip-addresses -n SampleVM -o table
```

반환 결과

```
VirtualMachine    PublicIPAddresses    PrivateIPAddresses
----------------  -------------------  --------------------
SampleVM          168.61.54.62         10.0.0.4
```

> [!TIP]
> `--output` 플래그의 줄임 구문을 `-o`로 사용하고 있습니다. Azure CLI 명령에 대한 대부분의 매개 변수는 하나의 대시 및 문자로 줄일 수 있습니다. 예를 들어 `--name`은 `-n`으로 줄이고 `--resource-group`은 `-g`로 줄일 수 있습니다. 이는 편리하게 입력할 수 있지만 분명하게 하기 위해 스크립트에서는 전체 옵션 이름을 사용하는 것이 좋습니다. 각 명령에 대한 자세한 내용은 설명서를 확인하세요.

## <a name="getting-vm-details"></a>VM 세부 정보 가져오기

`vm show` 명령을 사용하여 이름 또는 ID별로 특정 가상 머신에 대한 자세한 정보를 가져올 수 있습니다.

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM
```

이 명령은 연결된 저장소 장치, 네트워크 인터페이스 및 VM이 연결된 리소스의 모든 개체 ID를 포함하여 VM에 대한 모든 종류의 정보가 포함된 상당히 큰 JSON 블록을 반환합니다. 다시 표 형식으로 변경할 수 있지만 이렇게 하면 거의 모든 흥미로운 데이터가 생략됩니다. 대신에 [JMESPath](http://jmespath.org/)라는 JSON의 기본 제공 쿼리 언어로 전환할 수 있습니다.

## <a name="adding-filters-to-queries-with-jmespath"></a>JMESPath를 사용하여 쿼리에 필터 추가

JMESPath는 JSON 개체를 중심으로 빌드되는 업계 표준 쿼리 언어입니다. 가장 단순한 쿼리는 JSON 개체에서 키를 선택하는 _ID_를 지정하는 것입니다.

예를 들어 다음과 같은 개체가 제공됩니다.

```json
{
  "people": [
    {
      "name": "Fred",
      "age": 28
    },
    {
      "name": "Barney",
      "age": 25
    },
    {
      "name": "Wilma",
      "age": 27
    }
  ]
}
```

쿼리 `people`을 사용하여 `people` 배열에 대한 값 배열을 반환할 수 있습니다. 사용자 중 ‘한 명’만 필요한 경우 인덱서를 사용할 수 있습니다. 예를 들어 `people[1]`은 다음을 반환합니다.

```json
{
    "name": "Barney",
    "age": 25
}
```

또한 몇 가지 조건에 따라 개체의 하위 집합을 반환하는 특정 한정자를 추가할 수 있습니다. 예를 들어, 한정자 `people[?age > '25']`을 추가하면 다음을 반환합니다.

```json
[
  {
    "name": "Fred",
    "age": 28
  },
  {
    "name": "Wilma",
    "age": 27
  }
]
```

마지막으로 이름만 반환하는 select: `people[?age > '25'].[name]`을 추가하여 결과를 제약할 수 있습니다.

```json
[
  [
    "Fred"
  ],
  [
    "Wilma"
  ]
]
```

JMESQuery에는 여러 가지 다른 흥미로운 쿼리 기능이 있습니다. 시간이 있는 경우 [JMESPath.org](http://jmespath.org/) 사이트에서 사용 가능한 [온라인 자습서](http://jmespath.org/tutorial.html)를 확인하세요.

## <a name="filtering-our-azure-cli-queries"></a>Azure CLI 쿼리 필터링

JMES 쿼리를 기본적으로 이해하면 `vm show` 명령과 같은 쿼리에서 반환되는 데이터에 파일러(filer)를 추가할 수 있습니다. 예를 들어 관리 사용자 이름을 검색할 수 있습니다.

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "osProfile.adminUsername"
```

VM에 할당된 크기를 가져올 수 있습니다.

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query hardwareProfile.vmSize
```

또는 네트워크 인터페이스의 모든 ID를 검색하려면 다음 쿼리를 사용하면 됩니다.

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id"
```

이 쿼리 방법은 Azure CLI 명령과 함께 작동하며 명령줄에서 특정 데이터를 끌어오는 데 사용할 수 있습니다. 이 방법은 스크립팅에 유용합니다. 예를 들어 Azure 계정에서 값을 끌어오고 이를 환경 또는 스크립트 변수에 저장할 수 있습니다. 이 방법으로 사용하기로 한 경우 추가할 유용한 플래그는 `--output tsv` 매개 변수(`-o tsv`로 줄일 수 있음)입니다. 이 매개 변수는 탭 구분 기호와 함께 실제 데이터 값만 포함하는 탭으로 구분된 값으로 결과를 반환합니다.

예를 들어

```azurecli
az vm show --resource-group <rgn>[sandbox resource group name]</rgn> --name SampleVM --query "networkProfile.networkInterfaces[].id" -o tsv
```

`/subscriptions/20f4b944-fc7a-4d38-b02c-900c8223c3a0/resourceGroups/2568d0d0-efe3-4d04-a08f-df7f009f822a/providers/Microsoft.Network/networkInterfaces/SampleVMVMNic` 텍스트를 반환합니다.
