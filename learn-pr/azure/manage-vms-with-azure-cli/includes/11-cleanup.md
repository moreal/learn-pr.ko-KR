새 Linux 가상 머신을 만들고, 머신의 크기를 변경하고, 머신을 중지했다가 다시 시작하고, Azure CLI로 구성을 업데이트했습니다.

## <a name="cleanup"></a>정리

이제 VM 사용을 마쳤으며 더 이상 VM이 필요하지 않으므로 리소스를 삭제하겠습니다. 정리는 계정에 대해 계속 비용이 청구될 수 있는 계산 및 저장소 리소스에 중요합니다. 

`delete` 명령을 사용하여 개별 리소스를 삭제할 수 있지만, 모든 리소스를 제거하는 가장 손쉬운 방법은 `az group delete`를 사용하는 것입니다. Azure CLI에서 다음 명령을 실행합니다.

```azurecli
az group delete --name ExerciseResources --no-wait
```

표시되는 프롬프트에 “예”로 답하거나 `--yes` 매개 변수를 사용하여 프롬프트에 자동으로 답합니다.

이 명령은 리소스 그룹과 연관된 모든 리소스를 삭제하며, 올바른 순서로 리소스 할당을 취소할 수 있도록 보장합니다. `--no-wait` 매개 변수는 삭제가 수행되는 동안 Azure CLI가 차단되지 않도록 유지합니다. 리소스가 삭제될 때까지 대기하려면 이 매개 변수를 그대로 둡니다. 또는 나중에 스크립트에서 `az group wait -n ExerciseResources --deleted` 명령을 사용하여 삭제가 완료될 때까지 대기합니다.


## <a name="further-reading"></a>추가 참고 자료

- [Azure CLI 개요](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
