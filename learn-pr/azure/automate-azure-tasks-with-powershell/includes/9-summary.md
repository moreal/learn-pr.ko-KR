이 모듈에서는 여러 VM 만들기를 자동화하는 스크립트를 작성했습니다. 스크립트가 비교적 짧은 경우에도 Azure PowerShell에서 cmdlet을 사용하여 PowerShell에서 루프, 변수 및 함수를 결합할 때 잠재적인 능력을 확인할 수 있습니다.

PowerShell 경험이 있는 관리자는 자동화에 Azure PowerShell을 사용하는 것이 좋습니다. 정리된 구문 및 강력한 스크립팅 언어를 함께 사용하는 방법은 PowerShell을 처음 사용할 경우에도 고려할 만합니다. 시간이 오래 걸리고 오류가 발생하기 쉬운 작업에 이 자동화 수준을 사용하면 관리 시간을 줄이고 품질을 개선할 수 있습니다.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

고유한 구독에서 실행하는 경우 다음 PowerShell cmdlet을 사용하여 리소스 그룹(및 모든 관련 리소스)을 삭제할 수 있습니다.

```powershell
Remove-AzureRmResourceGroup -Name MyResourceGroupName
```

삭제를 확인하는 메시지가 나타나면 **예**로 답하거나, `-Force` 매개 변수를 추가하여 프롬프트를 건너뛸 수 있습니다. 명령을 완료하는 데는 몇 분 정도 걸릴 수 있습니다.