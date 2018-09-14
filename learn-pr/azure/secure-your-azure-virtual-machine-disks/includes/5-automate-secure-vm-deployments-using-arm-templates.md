회사에서 클라우드로 전환하는 과정의 일환으로 여러 서버를 배포하는 경우를 가정해 보겠습니다. 디스크가 항상 취약성이 없는 상태로 유지되도록 배포 중에 VM 디스크를 암호화해야 합니다. 이 프로세스를 자동화 하려면 하 고이 정보를 자동으로 암호화를 사용 하려면 Azure Resource Manager 템플릿을 수정 해야 합니다.

여기에서 Azure Resource Manager 템플릿을 사용 하 여 자동으로 새 Windows Vm에 암호화를 사용 하는 방법을 살펴보겠습니다.

## <a name="what-are-azure-resource-manager-templates"></a>Azure Resource Manager 템플릿 무엇입니까?

이러한 템플릿은 가상 머신 처럼 azure에 배포할 리소스를 정의 하는 데 사용 되는 JSON 파일에 설명 합니다. 템플릿을 새로 작성할 수도 있고, VM을 비롯한 일부 Azure 리소스의 경우에는 Azure Portal을 사용하여 템플릿을 생성할 수도 있습니다. 수동 VM 배포의 경우에는 필요한 정보를 작성해야 합니다. 하지만 VM을 Azure에 배포하는 대신 템플릿을 저장할 수 있습니다.

예제 템플릿은 GitHub에서 제공됩니다.

## <a name="using-github-templates"></a>GitHub 템플릿 사용

GitHub에 템플릿이 이라는 암호화를 사용 하도록 설정 합니다 **실행 중인 Windows VM ARM에서 암호화 사용**. 이 템플릿은 [Azure 빠른 시작 템플릿](https://github.com/Azure/azure-quickstart-templates) 리포지토리에 있습니다. 템플릿에 대 한 추가 정보 페이지를 제공 된 **Azure에 배포** 단추는 다음 Azure portal에서 템플릿을 엽니다.

이 템플릿을 사용하면 암호화가 사용하도록 미리 설정된 상태로 Windows Server VM을 배포할 수 있습니다. 서식 파일을 사용 하기 전에 모든 암호화 필수 구성 요소가 충족 되는지 확인 해야 합니다. Azure Active Directory 클라이언트 ID 및 Azure Active Directory 클라이언트 암호와 같은 필수 구성 요소 스크립트를 제공 하는 구성 정보를 해야 합니다.

템플릿에서 필수 정보를 입력하여 새 VM을 만듭니다. 그런 다음 **구매**를 클릭하여 배치를 시작합니다. 해당 비용은 대개 일반 Azure 계산 저장소 요금입니다.

## <a name="deploy-an-encrypted-vm-by-using-a-template"></a>템플릿을 사용하여 암호화된 VM 배포

템플릿을 사용하여 암호화된 VM을 배포할 때 수행하는 주요 단계는 다음과 같습니다.

1. GitHub에서 **실행 중인 Windows VM ARM에서 암호화 사용** 템플릿에 액세스하여 해당 템플릿을 실행합니다.

1. 스크립트 구성 페이지에서 필요한 세부 정보를 추가합니다.

1. **구매**를 클릭해 스크립트를 사용하여 새 VM을 배포합니다.

1. Azure Portal을 사용하여 디스크 암호화 상태를 확인합니다.
