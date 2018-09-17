회사에서 모든 VM에 ADE(Azure Disk Encryption)를 구현하기로 결정했다고 가정해 보겠습니다. 이 결정에 따라 기존 VM 볼륨에 암호화 기능을 제공할 방법을 평가해야 합니다.

여기서는 ADE의 요구 사항과 기존 Windows VM의 디스크를 암호화하기 위한 단계를 살펴보겠습니다.

## <a name="azure-disk-encryption-prerequisites"></a>Azure Disk Encryption 필수 구성 요소

첫 번째 VM 디스크를 암호화하려면 먼저 다음을 수행해야 합니다.

1. Key Vault를 만듭니다.
1. Azure AD(Active Directory) 응용 프로그램 및 서비스 주체를 설정합니다.
1. Azure AD 앱에 대한 Key Vault 액세스 정책을 설정합니다.
1. Key Vault에 대한 고급 액세스 정책을 설정합니다.

### <a name="azure-key-vault"></a>Azure Key Vault

ADE에 사용되는 암호화 키를 Azure Key Vault에 저장할 수 있습니다. Azure Key Vault는 비밀을 안전하게 저장하고 액세스하기 위한 도구입니다. 비밀은 API 키, 암호 또는 인증서 등에 대한 액세스를 엄격하게 제어하려는 항목입니다. 비밀을 활용하는 경우 FIPS(Federal Information Processing Standard) 140-2 수준 2 유효성이 검사된 HSM(하드웨어 보안 모듈)에서 가용성과 확장성이 뛰어난 보안 저장소가 제공됩니다. Key Vault를 사용하면 데이터를 암호화하는 데 사용되는 키를 완벽하게 제어할 수 있으며 키 사용을 관리 및 감사할 수 있습니다. Azure Portal, Azure PowerShell 및 Azure CLI를 사용하여 Key Vault를 구성하고 관리할 수 있습니다.

>[!NOTE]
> Azure Disk Encryption을 사용하려면 Key Vault와 VM이 같은 Azure 지역에 있어야 합니다. 그래야 암호화 비밀이 다른 지역에 노출되지 않습니다.

### <a name="azure-ad-application-and-service-principal"></a>Azure AD 응용 프로그램 및 서비스 주체

스크립트나 코드를 사용하여 VM의 암호화 구성과 같은 리소스에 액세스하거나 리소스를 수정하려는 경우 먼저 **Azure AD(Active Directory) 응용 프로그램**을 설정해야 합니다. Azure AD는 다중 테넌트, 클라우드 기반의 디렉터리 및 ID 관리 서비스입니다. 이 솔루션은 핵심 디렉터리 서비스, 응용 프로그램 액세스 관리 및 ID 보호를 하나의 솔루션으로 결합합니다.

Azure **서비스 주체**도 필요합니다. 서비스 주체는 스크립트나 코드를 실행하는 데 사용하는 서비스 계정입니다. 특정 Azure 리소스에 대해 작업을 실행하는 데 필요한 특정 권한과 범위를 할당할 수 있습니다.

Azure AD에는 응용 프로그램 개체가 응용 프로그램의 **_정의_**(응용 프로그램이 수행하는 작업)이며 서비스 주체가 응용 프로그램의 **_특정 인스턴스_** 인 두 가지 요소가 있습니다.

이러한 방식은 앱이 작업을 수행하려면 필요한 최소한의 권한만이 앱에 할당되는 **최소 권한** 원칙과 일치합니다.

Azure Portal, Azure PowerShell 및 Azure CLI를 사용하여 Azure AD 응용 프로그램 및 서비스 주체를 구성하고 관리할 수 있습니다.

### <a name="key-vault-access-policies"></a>Key Vault 액세스 정책

Key Vault에 암호화 키를 저장하려면 Key Vault에 쓸 수 있는 Azure AD 응용 프로그램의 **클라이언트 ID** 및 **클라이언트 비밀** 관련 세부 정보를 ADE에 제공해야 합니다.

또한 Key Vault의 암호화 키 액세스 권한을 Azure에 제공해야 합니다. 그래야 VM이 볼륨 부팅 및 암호 해독용으로 해당 암호화 키를 사용할 수 있습니다.

## <a name="set-key-vault-advanced-access-policies"></a>Key Vault 고급 액세스 정책 설정

**고급 액세스 정책**을 설정하면 Key Vault에서 디스크 암호화를 사용할 수 있습니다. 이러한 정책이 없으면 암호화 배포가 실패합니다. 

사용하도록 설정해야 하는 정책은 다음의 세 가지입니다.

- **디스크 암호화에 대한 Key Vault** Azure Disk Encryption에 필요합니다.
- **배포에 대한 Key Vault**. Microsoft.Compute 리소스 공급자가 Key Vault에서 비밀을 검색할 수 있도록 합니다. 이 정책은 VM을 만들 때 필요합니다.
- **필요한 경우 템플릿 배포를 위한 Key Vault**. Azure Resource Manager가 Key vault에서 비밀을 가져올 수 있도록 합니다. 이 정책은 VM 배포에 Azure Resource Manager 템플릿을 사용하는 경우에 필요합니다.

Azure Portal, Azure PowerShell 또는 Azure CLI를 사용하여 Key Vault 액세스 정책을 구성하고 관리할 수 있습니다.

### <a name="what-is-the-azure-disk-encryption-prerequisites-configuration-script"></a>Azure Disk Encryption 필수 구성 요소 구성 스크립트란?

**Azure Disk Encryption 필수 구성 요소 구성 스크립트**를 사용하면 암호화 필수 구성 요소를 모두(또는 원하는 만큼) 설정할 수 있습니다. 또한 암호화하려는 VM과 Key Vault가 같은 지역에 있는지도 확인할 수 있습니다. 이 스크립트는 리소스 그룹과 Key Vault를 만들고 Key Vault 액세스 정책을 설정합니다. 또한 스크립트는 실수로 삭제되지 않도록 Key Vault에 리소스 잠금을 만듭니다.

## <a name="encrypting-an-existing-vm-disk"></a>기존 VM 디스크 암호화

Azure Disk Encryption 필수 구성 요소 구성 스크립트를 사용할 때 기존 VM 디스크를 암호화하는 두 단계가 있습니다.

1. Azure Disk Encryption 필수 구성 요소 구성 스크립트를 실행합니다.
1. PowerShell에서 Azure 가상 머신을 암호화합니다.
