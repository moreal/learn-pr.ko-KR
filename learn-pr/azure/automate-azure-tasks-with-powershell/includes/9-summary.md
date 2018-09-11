이 모듈에서는 여러 VM 만들기를 자동화하는 스크립트를 작성했습니다. 스크립트가 비교적 짧은 경우에도 Azure PowerShell에서 cmdlet을 사용하여 PowerShell에서 루프, 변수 및 함수를 결합할 때 잠재적인 능력을 확인할 수 있습니다.

PowerShell 경험이 있는 관리자는 자동화에 Azure PowerShell을 사용하는 것이 좋습니다. 정리된 구문 및 강력한 스크립팅 언어를 함께 사용하는 방법은 PowerShell을 처음 사용할 경우에도 고려할 만합니다. 시간이 오래 걸리고 오류가 발생하기 쉬운 작업에 이 자동화 수준을 사용하면 관리 시간을 줄이고 품질을 개선할 수 있습니다.

## <a name="clean-up-your-resources"></a>리소스 정리
<!---TODO: Do we need to include cleanup for the free education tier?--->

프로비전되어 실행 중인 VM을 사용하면 구독에 대한 비용이 발생합니다. 불필요한 비용을 방지하려면 불필요한 VM을 제거해야 합니다. Azure 구독을 정리하는 가장 쉬운 방법은 연결된 리소스 그룹을 제거하는 것입니다. 이렇게 하면 그룹의 모든 VM도 삭제됩니다. PowerShell에서 이 작업을 수행할 수 있습니다. 완료되면 다음 Azure PowerShell cmdlet을 실행하세요.

```powershell
Remove-AzureRmResourceGroup -Name TrialsResourceGroup
```

삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다. 명령을 완료하는 데는 몇 분 정도 걸릴 수 있습니다.