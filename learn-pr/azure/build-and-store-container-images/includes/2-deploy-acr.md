이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만듭니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]
 
## <a name="create-an-azure-container-registry"></a>Azure Container Registry 만들기

무료 샌드박스에서 작업할 것이므로 고유한 리소스 그룹을 만들 필요가 없습니다. `az acr create` 명령을 사용하여 Azure Container Registry를 만듭니다. 컨테이너 레지스트리 이름은 Azure 내에서 고유해야 하며, 5~50자 사이의 영숫자를 포함해야 합니다. `<acrName>`를 레지스트리의 고유한 이름으로 바꿉니다.

이 예제에서는 프리미엄 레지스트리 SKU가 배포됩니다. 프리미엄 SKU는 지역 복제에 필요합니다. 다음 명령을 Cloud Shell 편집기에 입력합니다.

```azurecli
az acr create --resource-group <rgn>[sandbox resource group name]</rgn> --name <acrName> --sku Premium
```

다음은 새 Azure 컨테이너 레지스트리의 출력 예제입니다.

```output
{
  "adminUserEnabled": false,
  "creationDate": "2018-08-15T19:19:07.042178+00:00",
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myACR0007",
  "location": "eastus",
  "loginServer": "myacr.azurecr.io",
  "name": "myACR",
  "provisioningState": "Succeeded",
  "resourceGroup": "myResourceGroup",
  "sku": {
    "name": "Premium",
    "tier": "Premium"
  },
  "status": null,
  "storageAccount": null,
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries"
}
```

이 모듈의 나머지 부분에서는 `<acrName>`을 이 단계에서 선택하는 컨테이너 레지스트리 이름의 자리 표시자로 참조합니다.

이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만들었습니다.