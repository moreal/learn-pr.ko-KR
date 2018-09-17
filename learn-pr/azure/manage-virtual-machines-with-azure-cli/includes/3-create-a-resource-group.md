목표는 새로운 Azure 가상 머신을 만드는 것입니다. 리소스 위치, 사용할 OS 및 VM에 필요한 하드웨어 구성을 식별하기 위해 몇 가지 정보를 제공해야 합니다. **리소스 그룹**부터 살펴보겠습니다.

## <a name="create-a-resource-group"></a>리소스 그룹 만들기

Azure는 _리소스 그룹_을 사용하여 가상 머신 및 데이터베이스와 같은 관련 리소스를 그룹화합니다. 또한 리소스 그룹은 리소스가 배치되는 데이터 센터를 결정하는 특정 위치(“지역”이라고 함)를 식별합니다.

> [!NOTE]
> Azure 샌드박스는 <rgn>[샌드박스 리소스 그룹 이름]</rgn>이라는 미리 생성된 리소스 그룹을 제공합니다. 이러한 단계를 실행할 필요가 없습니다. 그러나 실제 프로젝트를 위해 _고유_ 리소스를 만들 때 수행해야 하는 명령이 됩니다. Azure 샌드박스에서는 리소스 그룹을 직접 만들 수 없습니다.

예를 들어 Azure Cloud Shell에 다음 Azure CLI 명령을 입력하여 **미국 동부** 지역에 리소스 구분을 만들 수 있습니다. **[리소스 그룹]** 을 고유한 활성 구독 내에서 유효한 이름으로 바꿉니다.

```azurecli
az group create --name [resource-group] --location eastus
```

이렇게 하면 리소스 그룹이 생성되었음을 나타내는 JSON 블록이 반환됩니다.

```json
{
  "id": "/subscriptions/abc13b0c-d2c4-64b2-9ac5-2f4cb819b752/resourceGroups/<resourcegroup>",
  "location": "eastus",
  "managedBy": null,
  "name": "<resourcegroup>",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null
}
```

응답의 일부로 구독 고유 식별자, 위치 및 이름이 반환됩니다. 이들 항목을 사용하여 리소스 그룹이 적절한 구독 및 위치에서 생성되었는지 확인할 수 있습니다.

이제 리소스 그룹을 만드는 방법을 알았으므로 가상 머신을 만들어 보겠습니다.