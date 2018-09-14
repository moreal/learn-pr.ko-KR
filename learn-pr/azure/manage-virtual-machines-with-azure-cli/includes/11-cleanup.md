새 Linux 가상 머신을 만들고, 머신의 크기를 변경하고, 머신을 중지했다가 다시 시작하고, Azure CLI로 구성을 업데이트했습니다.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

사용자 고유의 구독에서 작업 하는 경우 리소스 그룹 및 모든 관련된 리소스를 삭제 하려면 다음 Azure CLI 명령을 실행할 수 있습니다.

```azurecli
az group delete --name [resource-group-name] --no-wait
```

표시되는 프롬프트에 “예”로 답하거나 `--yes` 매개 변수를 사용하여 프롬프트에 자동으로 답합니다.

이 명령은 리소스 그룹과 연관된 모든 리소스를 삭제하며, 올바른 순서로 리소스 할당을 취소할 수 있도록 보장합니다. `--no-wait` 매개 변수는 삭제가 수행되는 동안 Azure CLI가 차단되지 않도록 유지합니다. 리소스가 삭제될 때까지 대기하려면 이 매개 변수를 그대로 둡니다. 또는 나중에 스크립트에서 `az group wait -n [resource-group-name] --deleted` 명령을 사용하여 삭제가 완료될 때까지 대기합니다.


## <a name="further-reading"></a>추가 참고 자료

- [Azure CLI 개요](https://docs.microsoft.com/cli/azure/?view=azure-cli-latest)
- [Azure CLI 명령 참조](https://docs.microsoft.com/cli/azure/reference-index?view=azure-cli-latest)
