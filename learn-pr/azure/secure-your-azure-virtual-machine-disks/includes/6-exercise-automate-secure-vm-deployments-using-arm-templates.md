이 단원에서는 Azure Resource Manager 템플릿을 사용하여 앞서 만든 Windows VM의 암호를 해독합니다. Windows VM에서 OS 드라이브를 암호화했습니다. 그러나 OS 드라이브에는 기밀 정보가 없으므로 암호화되지 않은 상태로 내버려둘 수 있습니다. 템플릿을 사용하여 OS 드라이브의 암호를 해독해 보겠습니다.

## <a name="configure-and-deploy-a-new-vm-using-an-azure-resource-manager-template"></a>Azure Resource Manager 템플릿을 사용하여 새 VM 구성 및 배포

Microsoft가 Github에 게시한 템플릿을 사용하여 기본적으로 암호화가 작동되는 새 VM을 만들 예정입니다.

1. 샌드박스를 활성화한 동일한 계정으로 [Azure Portal](https://portal.azure.com/learn.docs.microsoft.com?azure-portal=true)에 로그인합니다.

1. 왼쪽 사이드바에서 **리소스 만들기**를 클릭합니다.

1. 검색 상자에 **템플릿**을 입력합니다.

1. 결과 목록에서 **템플릿 배포**를 선택하고 **만들기**를 클릭합니다.

    ![강조 표시된 만들기 단추를 사용하여 선택한 템플릿 배포 항목을 보여 주는 스크린샷](../media/6-create-template.png)

1. **템플릿을 선택** 검색 상자에서 "201-암호 해독" 입력을 시작하고 "201-decrypt-running-windows-vm-without-aad" 템플릿을 선택합니다.

    ![자동 완성을 사용하여 템플릿 검색 상자 선택을 보여 주는 스크린샷](../media/6-custom-deployment.png)

1. **템플릿 선택**을 클릭하여 템플릿 실행기를 시작합니다.

1. 설정 보기에 다음 정보를 입력합니다.
    - **구독**에 대해 _컨시어지 구독_을 선택합니다.
    - 샌드박스에서 만든 리소스 그룹을 선택합니다.
    - VM을 만든 위치를 선택합니다.
    - **VM 이름**에 "fmdata-vm01"을 입력합니다.
    - **볼륨 형식**을 _모두_로 유지합니다.

1. **사용 약관에 동의함** 확인란을 선택합니다.
1. **구매**를 클릭하여 템플릿을 실행합니다. 이 템플릿에 대한 비용은 없습니다 - 이것은 표준 단추입니다.

배포가 완료될 때까지 몇 분 정도 걸릴 수 있습니다.

## <a name="verify-the-encryption-status-of-the-vm"></a>VM의 암호화 상태를 확인

1. Azure Portal의 사이트바에서 **가상 머신**을 클릭하고 VM **fmdata-vm01**을 선택합니다. 또는 **모든 리소스**에서 이름으로 VM을 검색할 수 있습니다.

1. **가상 머신** 블레이드의 **설정**에서 **디스크**를 클릭합니다.

1. **디스크** 블레이드에서 OS 디스크 암호화 상태가 **사용 안 함**인지 확인합니다.
