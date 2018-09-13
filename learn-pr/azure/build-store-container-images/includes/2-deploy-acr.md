이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만듭니다.

## <a name="create-an-azure-container-registry"></a>Azure Container Registry 만들기

Azure Container Registry를 만들려면 이것을 배포할 *리소스 그룹*이 필요합니다. 리소스 그룹은 모든 Azure 리소스가 배포되고 관리되는 논리적 컬렉션입니다.

`az group create` 명령을 사용하여 리소스 그룹을 만듭니다. 다음 예제에서는 *eastus* 지역에 *myResourceGroup*이라는 리소스 그룹을 만듭니다.

```azurecli
az group create --name myResourceGroup --location eastus
```

리소스 그룹을 만들었으면 `az acr create` 명령을 사용하여 Azure Container Registry를 만듭니다. 컨테이너 레지스트리 이름은 Azure 내에서 고유해야 하며, 5~50자 사이의 영숫자만 포함해야 합니다. `<acrName>`를 레지스트리의 고유한 이름으로 바꿉니다.

이 예제에서는 프리미엄 레지스트리 SKU가 배포됩니다. 프리미엄 SKU는 지역 복제에 필요합니다. Container Registry SKU에 대한 자세한 내용은 [Azure Container Registry SKU](https://docs.microsoft.com/azure/container-registry/container-registry-skus)를 참조하세요.

```azurecli
az acr create --resource-group myResourceGroup --name <acrName> --sku Premium
```

다음은 새 Azure Container Registry의 출력 예제입니다.

```console
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

이 모듈의 나머지 부분에서는 이 단계에서 선택하는 컨테이너 레지스트리 이름의 자리 표시자로 `<acrName>`을 참조합니다.

## <a name="summary"></a>요약

이 단원에서는 Azure CLI를 사용하여 Azure Container Registry를 만들었습니다.