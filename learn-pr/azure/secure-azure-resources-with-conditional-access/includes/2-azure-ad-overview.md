Azure AD(Azure Active Directory)는 클라우드에서 단순히 도메인 컨트롤러만이 아닙니다. Azure AD는 다중 테넌트 클라우드 기반의 디렉터리 및 ID 관리 서비스입니다. 이 솔루션은 핵심 디렉터리 서비스, 응용 프로그램 액세스 관리 및 ID 보호를 하나의 솔루션으로 결합합니다. Azure AD는 Azure AD Connect를 통해 기존 Windows Server Active Directory 환경과 함께 작동할 수 있으므로 기존 온-프레미스 ID 투자를 활용할 수 있습니다.

Azure AD는 네 가지 버전으로 제공됩니다. 이 연습에서는 Azure AD Premium P1 및 P2 버전의 기능만 중점적으로 다룹니다.

이 모듈에서는 온-프레미스 디렉터리와 비슷하게 모든 사용자와 그룹이 활성 상태인 Azure AD 디렉터리를 만듭니다.

디렉터리가 만들어지면 계정이 자동으로 글로벌 관리자가 됩니다. 글로벌 관리자 권한이 있는 계정은 모든 Azure AD 관리 기능에 대한 모든 권한을 가지므로 규제되어야 합니다. 둘 이상의 글로벌 관리자가 있을 수 있지만 글로벌 관리자만 다른 관리자 역할을 사용자에게 할당할 수 있습니다.

## <a name="how-can-azure-ad-help-you-protect-access-to-applications"></a>Azure AD에서 응용 프로그램에 대한 액세스를 보호하려면 어떻게 해야 할까요?

Azure AD Premium에는 Multi-Factor Authentication 및 조건부 액세스 정책과 같은 기능이 포함되어 있습니다. 응용 프로그램에 대한 액세스를 보호할 때 이러한 기능을 함께 사용하면 가장 세분화된 기능이 제공됩니다.

조건부 액세스 정책을 구성하는 항목은 다음과 같습니다.

- 사용자 또는 그룹
- 액세스하려는 응용 프로그램
- 수행할 제어(예: Multi-Factor Authentication)

## <a name="summary"></a>요약

이 단원에서는 Azure AD의 기본 사항과 응용 프로그램에 대한 액세스를 보호하는 데 사용할 수 있는 기능을 알아보았습니다. 했으므로 기본 사항으로, 시작 Azure AD를 사용 하 여 합니다. 이 모듈의 나머지 부분에서는 조건부 액세스를 사용하여 Multi-Factor Authentication을 사용하도록 설정하고 테스트할 수 있는 실습을 제공합니다.
