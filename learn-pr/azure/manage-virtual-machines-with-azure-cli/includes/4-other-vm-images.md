가상 머신을 만들기 위한 이미지에 `Debian`을 사용했습니다. Azure에는 가상 머신을 만드는 데 사용할 수 있는 여러 가지 표준 VM 이미지가 있습니다. 

## <a name="listing-images"></a>이미지 나열

다음 명령을 사용하여 사용 가능한 VM 이미지 목록을 가져올 수 있습니다. 

```azurecli
az vm image list --output table
```

이렇게 하면 Azure CLI에 빌드된 오프라인 목록에 일부인 가장 인기 있는 이미지가 출력됩니다. 그러나 Azure Marketplace에는 사용 가능한 _수백_ 개의 이미지 옵션이 있습니다. 

## <a name="getting-all-images"></a>모든 이미지 가져오기

명령에 `--all` 플래그를 추가하여 전체 목록을 가져올 수 있습니다. Marketplace의 이미지 목록은 매우 크기 때문에 `--publisher`, `--sku` 또는 `–-offer` 옵션으로 목록을 필터링하는 것이 좋습니다.

예를 들어, 다음 명령을 실행하여 사용 가능한 _모든_ Wordpress 이미지를 확인합니다.

```azurecli
az vm image list --sku Wordpress --output table --all
```

또는 이 명령을 사용하여 Microsoft에서 제공하는 모든 이미지를 확인합니다.

```azurecli
az vm image list --publisher Microsoft --output table --all
```

## <a name="location-specific-images"></a>위치별 이미지

일부 이미지는 특정 위치에서만 사용할 수 있습니다. 가상 머신을 만들려는 영역에서 사용 가능한 것으로 결과의 범위를 지정하려면 명령에 `--location [location]` 플래그를 추가하세요. 예를 들어 `eastus` 영역에서 사용할 수 있는 이미지 목록을 가져오려면 Azure Cloud Shell에 다음을 입력하세요.

```azurecli
az vm image list --location eastus --output table
```

사용 가능한 다른 Azure 샌드박스 위치에서 일부 이미지를 확인합니다.

[!include[](../../../includes/azure-sandbox-regions-note.md)]

> [!TIP]
> 다음은 Azure에서 제공하는 표준 이미지입니다. 고유한 구성, 덜 일반적인 버전 또는 운영 체제의 배포를 기반으로 VM을 만들려면 [고유한 사용자 지정 이미지를 만들고 업로드](https://docs.microsoft.com/azure/virtual-machines/linux/tutorial-custom-images)할 수도 있습니다.

이제 아마도 명령 창이 가득 차 있을 것입니다. 원하는 경우 `clear`를 입력하여 화면을 지울 수 있습니다.