이 모듈에서는 Azure Storage 계정의 큐가 분산 응용 프로그램의 구성 요소 간에 메시지를 전달하는 데 사용되는 방법을 알아보았습니다. 이 방식으로 큐를 사용하면 오류가 발생하는 경우와 수요가 높은 기간에 분산 응용 프로그램을 더 안정적이고 만들고, 복원력을 높이는 데 도움이 될 수 있습니다. .NET용 Microsoft Azure Storage 클라이언트 라이브러리를 사용하는 경우 큐를 만들거나, 메시지를 추가하거나, 큐에서 메시지를 가져와 제거하는 C# 또는 VB.NET 코드를 쉽게 작성할 수 있습니다.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

자신의 구독에서 작업하는 경우 다음 Azure CLI 명령을 실행하여 리소스 그룹 및 모든 관련 리소스를 삭제할 수 있습니다.

```azurecli
az group delete --name [resource-group-name] --yes --no-wait
```

선택적 `--no-wait` 옵션은 Azure가 작업을 완료할 때까지 기다리지 않도록 셸에 지시합니다.