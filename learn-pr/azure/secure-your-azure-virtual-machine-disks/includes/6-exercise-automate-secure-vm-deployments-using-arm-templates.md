매우 중요한 고객 정보를 처리하는 금융 업체에서 VM 디스크 배포를 비롯하여 디스크를 항상 암호화된 상태로 유지하고자 합니다. 이를 위해 회사 데이터를 보호하기 위한 보안 VM 배포를 자동화하는 작업을 맡게 되었습니다.

이 단원에서는 Azure Resource Manager 템플릿을 사용하여 새 Windows VM에 대한 암호화를 자동으로 사용하도록 설정합니다.

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 새 VM 구성 및 배포

1. [GitHub의 Resource Manager 템플릿](https://github.com/Azure/azure-quickstart-templates/tree/master/201-encrypt-create-new-vm-gallery-image)으로 이동한 다음, **Azure에 배포**를 클릭합니다.
1. Azure Portal의 **Azure 빠른 시작 템플릿** 블레이드에서 **리소스 그룹** 아래의 **기존 항목 사용**을 선택합니다. 목록에서 **moneyapprg**를 선택합니다.
1. **설정** 섹션에서 다음 정보를 입력합니다.

   - VM 이름: **moneyappsvr02**
   - **관리자 사용자 이름**: 이전 연습에서 사용한 것과 동일합니다.
   - **관리자 암호**: 이전 연습에서 사용한 것과 동일합니다.
   - **새 저장소 계정 이름**: 고유한 이름을 입력합니다.
   - **VM 크기**: **Standard_B1s**와 같이 이전 연습에서 사용한 것과 같은 크기로 바꿉니다(동일한 Azure 지역을 사용하므로 현재 지역에서 해당 크기를 사용할 수 있는지 확인해야 함).
   - **가상 네트워크 이름**: **moneyapprg-vnet**
   - **서브넷 이름**: **default**
   - **AAD 클라이언트 ID**: 메모장에 붙여넣은 정보를 복사합니다.
   - **AAD 클라이언트 비밀**: 메모장에 붙여넣은 정보를 복사합니다.
   - **Key Vault 이름**: **moneyappkv**
   - **Key Vault 리소스 그룹**: **moneyapprg**
   - **키 암호화 키 URL**: 메모장에 붙여넣은 정보를 복사합니다.
1. **사용 약관에 동의함** 확인란을 선택한 다음, **구매**를 클릭합니다.

배포가 완료되려면 5~10분이 걸릴 수 있습니다.

## <a name="verify-encryption-status-of-new-vm"></a>새 VM의 암호화 상태 확인

1. Azure Portal의 사이드바에서 **가상 머신**을 클릭합니다.

1. **가상 머신** 블레이드에서 **moneyappsvr02**를 클릭합니다.

1. **가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.

1. **디스크** 블레이드에서 OS 디스크 암호화 상태가 **사용**인지 확인합니다.
