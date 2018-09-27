Azure에서는 Azure VM 디스크를 보호하기 위해 SSE(저장소 서비스 암호화) 및 ADE(Azure Disk Encryption) 기술이 제공됩니다. 이러한 기술은 서로 연동되어 Azure VM 디스크 보호를 위한 심층 방어 방식의 일환으로 강력한 256비트 암호화를 제공합니다. 디스크 암호화를 사용하려면 Azure Disk Encryption 필수 구성 요소를 완료해야 합니다. Azure Disk Encryption 필수 구성 요소 구성 스크립트는 이 프로세스를 자동화할 수 있습니다. 새 Vm에서 암호화를 사용하도록 설정하는 경우 Azure Resource Manager 템플릿을 사용할 수 있습니다. 이렇게 하면 배포 시점에서 데이터가 암호화되어 취약점이 발생하지 않습니다.

<!-- Cleanup sandbox -->
[!include[](../../../includes/azure-sandbox-cleanup.md)]

## <a name="additional-resources"></a>추가 리소스

- [Azure VM 디스크 암호화 문제 해결](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-tsg)
- [Azure에서 Linux 가상 머신을 암호화하는 방법](https://docs.microsoft.com/azure/virtual-machines/linux/encrypt-disks)
- [Azure Disk Encryption 개요](https://docs.microsoft.com/azure/security/azure-security-disk-encryption-overview)
- [Azure Disk Encryption은 어떤 Linux 배포판을 지원하나요?](https://docs.microsoft.com/en-us/azure/security/azure-security-disk-encryption-faq#bkmk_LinuxOSSupport)
- [GitHub의 Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates)