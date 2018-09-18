이 모듈에서는 Azure 디스크 캐싱과 잠재적으로 성능이 향상되는 방법을 알아보았습니다. Azure Portal 및 Azure PowerShell을 사용하여 VM에 대한 디스크 캐싱을 관리했습니다. 

Azure VM 디스크 캐싱 전략을 마련하고 나면 스크립트 및 템플릿을 사용하여 최적의 디스크 캐시 설정으로 새 VM 및 디스크를 빠르고 쉽게 배포할 수 있습니다.

## <a name="further-reading"></a>추가 참고 자료

- [Azure Premium Storage: 고성능을 위한 설계](https://docs.microsoft.com/azure/virtual-machines/windows/premium-storage-performance)
- [Azure PowerShell 시작](https://docs.microsoft.com/powershell/azure/get-started-azureps?view=azurermps-6.8.1)
- [Azure 컴퓨터 Cmdlet 참조](https://docs.microsoft.com/powershell/module/azurerm.compute/?view=azurermps-6.8.1#vm_disks)


## <a name="cleanup"></a>정리
<!---TODO: Update for sandbox?--->

Azure VM을 실행하면 구독에 대한 비용이 발생합니다. 불필요한 비용을 피하려면 불필요한 리소스를 제거합니다. Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하는 것입니다. 해당 그룹을 삭제하면 리소스 그룹에 있는 리소스도 모두 삭제됩니다. 이 모듈을 마치면 다음 Azure PowerShell cmdlet을 실행합니다.

    ```powershell
    Remove-AzureRmResourceGroup -Name "fotoshare-rg"
    ```

삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다. 리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다.
