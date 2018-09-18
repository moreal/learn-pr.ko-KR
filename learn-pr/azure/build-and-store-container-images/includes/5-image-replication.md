회사가 계산 워크로드를 여러 지역에 배포하여 분산된 고객층에게 제공하는 로컬 서비스가 있는지 확인합니다. 

이미지를 실행하는 각 지역에 컨테이너 레지스트리를 배치하려고 합니다. 네트워크에 가까운 작업에 대해 이 전략을 허용하면 신속하게 신뢰할 수 있는 이미지 계층을 전송할 수 있습니다. 

지역 복제를 사용하면 Azure Container Registry가 단일 레지스트리로 기능하여 다중 마스터 지역 레지스트리가 있는 여러 지역에 서비스를 제공할 수 있습니다.

지역에서 복제된 레지스트리는 다음과 같은 이점을 제공합니다.

- 둘 이상의 지역에서 단일 레지스트리/이미지/태그 이름 사용 가능
- 지역별 배포 환경에서 네트워크와 가까운 곳에 위치한 레지스트리에 액세스 가능
- 컨테이너 호스트와 동일한 지역에 있는 복제된 로컬 레지스트리에서 이미지를 가져오므로 추가 송신 요금이 부과되지 않음
- 둘 이상의 지역에서 레지스트리를 단일하게 관리

## <a name="replicate-an-image-to-multiple-locations"></a>여러 위치에 이미지 복제

`az acr replication create` Azure CLI 명령을 사용하여 컨테이너 이미지를 지역 간에 복제합니다. 이 예제에서는 `japaneast` 지역에 대한 복제를 만듭니다. Container Registry 이름으로 `<acrName>`을 업데이트합니다.

```azurecli
az acr replication create --registry <acrName> --location japaneast
```

출력은 다음과 비슷해야 합니다.

```console
{
  "id": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/myresourcegroup/providers/Microsoft.ContainerRegistry/registries/myACR0007/replications/japaneast",
  "location": "japaneast",
  "name": "japaneast",
  "provisioningState": "Succeeded",
  "resourceGroup": "myresourcegroup",
  "status": {
    "displayStatus": "Syncing",
    "message": null,
    "timestamp": "2018-08-15T20:22:09.275792+00:00"
  },
  "tags": {},
  "type": "Microsoft.ContainerRegistry/registries/replications"
}
```

마지막 단계입니다. 만든 모든 컨테이너 이미지 복제본을 검색할 수 있습니다. `az acr replication list` 명령을 사용하여 이 목록을 검색합니다. Container Registry 이름으로 `<acrName>`을 업데이트합니다.

```azurecli
az acr replication list --registry <acrName> --output table
```

출력은 다음과 비슷해야 합니다.

```console
NAME       LOCATION    PROVISIONING STATE    STATUS
---------  ----------  --------------------  --------
japaneast  japaneast   Succeeded             Ready
eastus     eastus      Succeeded             Ready
```

이미지 복제본을 나열하는 Azure CLI로 제한되지 않습니다. Azure Portal 내에서 Azure Container Registry에 대해 `Replications`를 선택하면 현재 복제를 자세히 설명하는 맵이 표시됩니다. 맵에서 지역을 선택하여 컨테이너 이미지를 추가 지역으로 복제할 수 있습니다.

![Azure Portal에 표시되는 컨테이너 복제 맵](../media/replication-map.png)

## <a name="clean-up"></a>정리
<!---TODO: Update for sandbox?--->

이제 리소스 그룹을 삭제하여 만든 리소스를 정리할 수 있습니다. 이렇게 하려면 `az group delete` 명령을 사용합니다.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a>요약

이제 Azure CLI를 사용하여 여러 Azure 데이터 센터에 컨테이너 이미지를 성공적으로 복제했습니다. 