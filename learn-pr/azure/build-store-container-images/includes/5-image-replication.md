이미지가 실행되는 각 지역에 컨테이너 레지스트리를 배치하면 네트워크와 가까운 곳에서 작업하여 이미지 레이어를 가장 빠르고 안정적으로 전송할 수 있습니다. 지역 복제를 사용하면 Azure Container Registry가 단일 레지스트리로 기능하여 다중 마스터 지역 레지스트리가 있는 둘 이상의 지역에 서비스를 제공할 수 있습니다.

지역에서 복제된 레지스트리는 다음과 같은 이점을 제공합니다.

* 둘 이상의 지역에서 단일 레지스트리/이미지/태그 이름 사용 가능
* 지역별 배포 환경에서 네트워크와 가까운 곳에 위치한 레지스트리에 액세스 가능
* 컨테이너 호스트와 동일한 지역에 있는 복제된 로컬 레지스트리에서 이미지를 끌어오므로 추가 송신 요금이 부과되지 않음
* 둘 이상의 지역에서 레지스트리를 단일하게 관리

## <a name="replicate-image-to-multiple-locations"></a>여러 위치에 이미지 복제

`az acr replication create` 명령을 사용하여 컨테이너 이미지를 다른 지역에 복제합니다. 이 예에서는 `japaneast` 지역에 대한 복제가 만들어집니다. 컨테이너 레지스트리 이름으로 `<acrName>`을 업데이트합니다.

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

모든 컨테이너 이미지 복제본의 목록을 보려면 `az acr replication list` 명령을 사용합니다. 컨테이너 레지스트리 이름으로 `<acrName>`을 업데이트합니다.

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

이 연습에서는 Azure Portal을 사용하지 않았지만 포털 환경을 확인하는 것이 좋습니다.

Azure Portal 내에서 Azure Container Registry에 대해 `Replications`를 선택하면 현재 복제를 자세히 설명하는 맵이 표시됩니다. 맵에서 지역을 선택하여 컨테이너 이미지를 추가 지역으로 복제할 수 있습니다.

![Azure Portal에 표시되는 컨테이너 복제 맵](../media/replication-map.png)

## <a name="clean-up"></a>정리

Azure Container Registry 학습 모듈의 마지막 단원입니다. 이제 리소스 그룹을 삭제하여 만든 리소스를 정리할 수 있습니다. 이렇게 하려면 `az group delete` 명령을 사용합니다.

```azurecli
az group delete --name myResourceGroup --no-wait
```

## <a name="summary"></a>요약

이 모듈에서는 Azure CLI를 사용하여 여러 Azure 지역에 컨테이너 이미지를 복제했습니다.