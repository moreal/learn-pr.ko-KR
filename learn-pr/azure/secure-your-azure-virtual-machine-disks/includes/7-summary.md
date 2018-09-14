Azure에서는 Azure VM 디스크를 보호하는 데 사용할 수 있는 SSE(저장소 서비스 암호화) 및 ADE(Azure Disk Encryption) 기술이 제공됩니다. 이러한 기술이 함께 작동 하의 Azure VM 디스크 보호를 위한 심층 방어 접근 방법의 일부로 강력한 256 비트 암호화를 제공 합니다. 디스크 암호화를 사용 하도록 설정 하려면 Azure Disk Encryption 필수 구성 요소를 완료 하는 필수 항목입니다. Azure Disk Encryption 필수 구성 요소 구성 스크립트는이 프로세스를 자동화할 수 있습니다. 새 Vm에서 암호화를 사용 하도록 설정한 경우에 Azure Resource Manager 템플릿을 사용할 수 있습니다. 이 암호화 되도록 하 데이터 배치를 없습니다 취약점으로 인 한 시점입니다.

## <a name="clean-up"></a>정리
<!---TODO: Update for sandbox?---> 구독에 대해 비용이 Azure Vm 및 연결된 된 저장소를 실행 합니다. 불필요한 비용을 피하려면 불필요한 리소스를 제거합니다. Azure 구독을 정리하는 가장 쉬운 방법은 리소스 그룹을 제거하는 것입니다. 이렇게 하면 해당 그룹의 모든 리소스도 삭제됩니다. 이 모듈을 마치면 다음 Azure PowerShell cmdlet을 실행합니다.

   ```powershell
   Remove-AzureRmResourceGroup -Name moneyapprg
   ```

삭제를 확인 하는 메시지가 나타나면, 답변 **예**합니다. 리소스가 삭제될 때 명령을 완료하는 데 몇 분이 걸릴 수 있습니다. 

삭제 하지 못했습니다. 메시지를 받게 되 면 리소스 그룹을 삭제 하기 전에 키 자격 증명 모음에 대 한 잠금을 제거 해야 합니다.
