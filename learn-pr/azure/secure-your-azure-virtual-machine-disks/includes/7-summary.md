Azure에서는 Azure VM 디스크를 보호하는 데 사용할 수 있는 SSE(저장소 서비스 암호화) 및 ADE(Azure Disk Encryption) 기술이 제공됩니다. 이 두 기술은 서로 연동되어 Azure VM 디스크 보호를 위한 심층 방어 방식의 일환으로 강력한 256비트 암호화를 제공합니다. 디스크 암호화를 사용하도록 설정하려면 Azure Disk Encryption 필수 구성 요소를 완료해야 합니다. Azure Disk Encryption 필수 구성 요소 구성 스크립트를 사용하면 이 프로세스를 자동화할 수 있습니다. 새 VM에서 암호화를 사용하도록 설정할 때는 ARM 템플릿을 사용할 수 있습니다. 그러면 배포 시점에 데이터가 암호화되므로 취약성이 발생하지 않습니다.

## <a name="cleanup"></a>정리
<!---TODO: Do we need to include cleanup for the free education tier?--->

Azure VM 및 연결된 저장소를 실행하면 구독에서 비용이 발생합니다. 불필요한 비용을 피하려면 불필요한 리소스를 제거합니다. Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하는 것입니다. 이렇게 하면 해당 그룹의 모든 리소스도 삭제됩니다. 이 모듈을 마치면 다음 Azure PowerShell cmdlet을 실행합니다.

   ```powershell
   Remove-AzureRmResourceGroup -Name moneyapprg
   ```

삭제를 확인하라는 메시지가 표시되면 **예**를 선택합니다. 리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다. 

삭제 실패 메시지가 표시되는 경우 리소스 그룹을 삭제하려면 Key Vault의 잠금을 해제해야 할 수 있습니다.
