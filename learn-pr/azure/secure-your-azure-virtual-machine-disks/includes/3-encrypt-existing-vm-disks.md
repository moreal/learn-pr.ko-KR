회사에서 모든 VM에 ADE(Azure Disk Encryption)를 구현하기로 결정했다고 가정해 보겠습니다. 이 결정에 따라 기존 VM 볼륨에 암호화 기능을 제공할 방법을 평가해야 합니다.

여기서는 ADE의 요구 사항과 기존 Windows VM의 디스크를 암호화하기 위한 단계를 살펴보겠습니다.

## <a name="azure-disk-encryption-prerequisites"></a>Azure Disk Encryption 필수 구성 요소

첫 번째 VM 디스크를 암호화할 수 있습니다, 전에 해야 합니다.

1. 키 자격 증명 모음을 만듭니다.
1. Azure Active Directory (Azure AD) 응용 프로그램 및 서비스 주체를 설정 합니다.
1. Azure AD 응용 프로그램에 대한 키 자격 증명 모음 액세스 정책을 설정합니다.
1. 키 자격 증명 모음에 대한 고급 액세스 정책을 설정합니다.

### <a name="azure-key-vault"></a>Azure Key Vault

ADE를 사용한 암호화 키를 Azure Key Vault에 저장할 수 있습니다. Azure Key Vault는 비밀을 안전하게 저장하고 액세스하기 위한 도구입니다. 비밀은 API 키, 암호 또는 인증서 등에 대한 액세스를 엄격하게 제어하려는 항목입니다. 항상 사용 가능 하 고 확장 가능한 보안 저장소에서는에서 FIPS Federal Information Processing Standards () 140-2 Level 2 유효성 검사가 하드웨어 보안 모듈 (Hsm). Key Vault를 사용하면 데이터를 암호화하는 데 사용되는 키를 완벽하게 제어할 수 있으며 키 사용을 관리 및 감사할 수 있습니다. 구성 하 고 Azure portal, Azure PowerShell 및 Azure CLI를 사용 하 여 키 자격 증명 모음을 관리할 수 있습니다.

>[!NOTE]
> Azure Disk Encryption에서는 키 자격 증명 모음 및 Vm에 동일한 Azure 지역;에 이렇게 하면 암호화 비밀 지역 경계를 초과 하지 않습니다.

### <a name="azure-ad-application-and-service-principal"></a>Azure AD 응용 프로그램 및 서비스 사용자

스크립트나 코드를 사용하여 VM의 암호화 구성과 같은 리소스에 액세스하거나 리소스를 수정하려는 경우 먼저 **Azure AD(Active Directory) 응용 프로그램**합을 설정해야 합니다. Azure AD는 다중 테 넌 트, 클라우드 기반 디렉터리 및 id 관리 서비스는입니다. 이 솔루션은 핵심 디렉터리 서비스, 응용 프로그램 액세스 관리 및 ID 보호를 하나의 솔루션으로 결합합니다.

또한 Azure **서비스 사용자**도 필요합니다. 서비스 주체는 서비스 계정을 사용 하 여 스크립트 또는 코드를 실행 합니다. 그러면 특정 권한 및 특정 Azure 리소스에 대 한 작업을 실행 하는 데 필요한 범위를 할당할 수 있습니다.

Azure AD에서 두 요소가: 응용 프로그램 개체를 **_정의_** (역할), 응용 프로그램 및 서비스의 사용자가를 **_특정 인스턴스_**  응용 프로그램입니다.

이러한 방식은 앱이 작업을 수행하려면 필요한 최소한의 권한만이 앱에 할당되는 **최소 권한** 원칙과 일치합니다.

구성 및 Azure AD 응용 프로그램 및 Azure portal, Azure PowerShell 및 Azure CLI를 사용 하 여 서비스 주체를 관리할 수 있습니다.

### <a name="key-vault-access-policies"></a>Key Vault 액세스 정책

ADE 세부 정보에서 필요한 key vault에 암호화 키를 저장할 수 있습니다, 전에 **클라이언트 ID** 하며 **클라이언트 암호** key vault에 쓸 허용 되는 Azure AD 응용 프로그램의 합니다.

또한 Key Vault의 암호화 키 액세스 권한을 Azure에 제공해야 합니다. 그래야 VM이 볼륨 부팅 및 암호 해독용으로 해당 암호화 키를 사용할 수 있습니다.

## <a name="set-key-vault-advanced-access-policies"></a>Key Vault 고급 액세스 정책 설정

**고급 액세스 정책**을 설정하면 Key Vault에서 디스크 암호화를 사용할 수 있습니다. 이러한 정책이 없으면 암호화 배포가 실패합니다. 

사용하도록 설정해야 하는 정책은 다음의 세 가지입니다.

- **디스크 암호화에 Key Vault**합니다. Azure Disk Encryption에 필요합니다.
- **배포에 대 한 Key Vault**합니다. Key vault에서 비밀을 검색 하려면 Microsoft.Compute 리소스 공급자를 사용 합니다. VM을 만들 때이 정책이 필요 합니다.
- **필요한 경우 템플릿 배포에 대 한 Key Vault**합니다. Key vault에서 비밀을 가져오기 위해 Azure Resource Manager를 사용 하도록 설정 합니다. VM 배포에 대 한 Azure Resource Manager 템플릿을 사용 하는 경우이 정책은 필수 항목입니다.

Azure Portal, Azure PowerShell 또는 Azure CLI를 사용하여 Key Vault 액세스 정책을 구성하고 관리할 수 있습니다.

### <a name="what-is-the-azure-disk-encryption-prerequisites-configuration-script"></a>Azure Disk Encryption 필수 구성 요소 구성 스크립트는 무엇입니까

합니다 **Azure Disk Encryption 필수 구성 요소 구성 스크립트** 모든 (또는 원하는 만큼) 설정 암호화 필수 구성 요소입니다. 또한 스크립트는 VM 암호화 하는 것과 동일한 지역에 key vault는 확인 합니다. 리소스 그룹 및 주요 자격 증명 모음 만들기 하 고 키 자격 증명 모음 액세스 정책을 설정 합니다. 또한 스크립트는 실수로 삭제되지 않도록 키 자격 증명 모음에 리소스 잠금을 만듭니다.

## <a name="encrypting-an-existing-vm-disk"></a>기존 VM 디스크 암호화

Azure Disk Encryption 필수 구성 요소 구성 스크립트를 사용 하는 경우 기존 VM 디스크를 암호화 하기 위한 두 단계가 있습니다.

1. Azure Disk Encryption 필수 구성 요소 구성 스크립트를 실행 합니다.
1. PowerShell에서 Azure 가상 컴퓨터를 암호화 합니다.
