Lamna Healthcare는 의사들이 환자 건강 데이터를 관리할 수 있는 레거시 내부 응용 프로그램 및 웹 포털을 호스팅합니다. 종종 온-프레미스에서 환자를 돌보는, 따라서 네트워크 외부에 있는 간병인도 이 응용 프로그램을 사용할 수 있게 해달라는 요청이 많이 들어왔습니다. 

최근에 악성 에이전트에 의해 데이터가 유출되는 사건이 발생하면서 병원의 암호 정책이 강화되었습니다. 이제 사용자는 암호를 더 자주 변경해야 하고, 더 길고 복잡한 암호를 사용해야 합니다. 이로 인해 여러 관리 역할에 대해 생성된 여러 자격 증명 집합을 기억하는 데 어려움을 느낀 사용자들이 복잡한 암호를 안전하지 않게 기록해 두는 의도치 않은 부작용이 발생했습니다. 

여기서는 내부 및 외부 응용 프로그램을 위한 보안 계층으로서의 ID, ID 보안을 제공하는 SSO(Single Sign-On) 및 MFA(다단계 인증)의 이점, 온-프레미스 ID를 Azure Active Directory로 복제해야 하는 이유를 알아보겠습니다.

## <a name="identity-as-a-layer-of-security"></a>보안 계층으로서의 ID

디지털 ID는 오늘날 비즈니스 및 소셜 상호 작용 온-프레미스와 온라인에서 없어서는 안되는 요소입니다. 과거에는 ID 및 액세스 서비스는 이 용도로 설계된 Kerberos 및 LDAP 같은 프로토콜을 사용하여 회사 내부 네트워크에서만 작동하도록 제한되었습니다. 최근에는 사람들이 주로 모바일 장치를 사용하여 디지털 서비스와 상호 작용합니다. 고객과 직원 모두 언제, 어디서나 서비스에 액세스할 수 있기를 원하며, 이로 인해 여러 별도의 장치 및 운영 체제에서 인터넷 규모로 작동할 수 있는 ID 프로토콜이 개발되었습니다.

Lamna Healthcare는 아키텍처의 ID 관련 기능을 평가할 때 다음 기능을 응용 프로그램으로 가져오는 방법을 알아보았습니다.

- 응용 프로그램 사용자에게 Single Sign-On 제공
- 최소한의 노력으로 최신 인증을 사용하도록 레거시 응용 프로그램 개선
- 회사 네트워크 외부에서 이루어지는 모든 로그인에 Multi-Factor Authentication 적용
- 환자가 안전하게 등록하고 계정 데이터를 관리할 수 있는 응용 프로그램 개발

## <a name="single-sign-on"></a>Single Sign-On

사용자가 관리할 ID가 많을수록 자격 증명 관련 보안 사건이 발생할 위험이 높습니다. 더 많은 ID는 더 많은 암호를 기억하고 변경해야 한다는 뜻입니다. 암호 정책은 응용 프로그램에 따라 다를 수 있으며, 복잡한 요구 사항이 늘어나면 사용자가 암호를 기억하기가 더 어려워집니다.

반대편에는 모든 ID에 요구되는 관리 업무가 있습니다. 계정 잠금 및 암호 재설정 요청을 처리하는 기술 지원팀의 부담이 가중됩니다. 사용자가 조직을 떠날 때 해당 사용자의 모든 ID를 추적하여 비활성화는 것이 어려울 수 있습니다. ID를 간과하면 제거되었어야 하는 ID를 통해 액세스할 수 있는 문제가 발생할 수 있습니다.

Single Sign-On을 사용하면 사용자는 ID 하나와 암호 하나만 기억하면 됩니다. 응용 프로그램에 대한 액세스 권한이 사용자와 연결된 ID에 부여되므로 보안 모델이 간소화됩니다. 액세스 수정이 단일 ID에 연결되어 있으므로 사용자 역할이 변경되거나 사용자가 조직을 떠날 때 계정을 변경하거나 비활성화하는 과정이 대폭 축소됩니다. 계정에 Single Sign-On을 사용하면 사용자가 ID를 간편하게 관리할 수 있으며, 환경의 보안 기능이 향상됩니다.

### <a name="sso-with-azure-active-directory"></a>Azure Active Directory를 사용한 SSO

Azure AD(Active Directory)는 클라우드 기반 ID 서비스입니다. 기존 온-프레미스 Active Directory와 동기화하거나 독립 실행형으로 사용할 수 있도록 기본 제공되는 지원입니다. 즉, 온-프레미스든, 클라우드든(Office 365 포함), 모바일이든 관계없이 모든 응용 프로그램이 동일한 자격 증명을 공유할 수 있습니다. 관리자와 개발자는 중앙 집중식 규칙과 Azure AD에서 구성한 정책을 사용하여 데이터 및 응용 프로그램에 대한 액세스를 제어할 수 있습니다.

또한 SSO에 Azure AD를 활용하면 여러 데이터 원본을 지능형 보안 그래프로 결합할 수 있습니다. 이 보안 그래프를 통해 온-프레미스 AD에서 동기화된 계정을 포함하여 Azure AD의 모든 계정에 위협 분석 및 실시간 ID 보호 기능을 제공할 수 있습니다. 중앙 집중식 ID 공급자를 사용하면 ID 인프라의 보안 제어, 보고, 경고 및 관리를 중앙 집중화할 수 있습니다.

### <a name="synchronize-directories-with-ad-connect"></a>AD Connect를 사용하여 디렉터리 동기화

Azure AD Connect는 온-프레미스 디렉터리와 Azure Active Directory를 통합합니다. Azure AD Connect는 최신 기능을 제공하며 DirSync 및 Azure AD Sync 같은 이전 버전의 ID 통합 도구를 대체합니다.

동기화 및 로그인에 대해 간편한 배포 환경을 제공하는 단일 도구입니다.

![Azure AD 연결을 보여 주는 일러스트레이션은 Azure Active directory 및 Azure 클라우드의 앱과 온-프레미스 디렉터리를 동기화하는 데 사용합니다. 이를 통해 사용자는 Azure 클라우드 내의 모든 응용 프로그램에 대한 공용 기호를 가질 수 있습니다.](../media/AADCONNECTxprs_960.png)

Lamna Healthcare는 인증이 주로 온-프레미스 DC에 대해 발생하기를 요구하지만, 재해 복구 시나리오에서는 클라우드 인증을 요구합니다. 아직 Azure AD에서 지원하지 않는 요구 사항은 없습니다.

Lamna Healthcare는 다음과 같은 구성을 사용하여 시스템을 개선하기로 했습니다.

- Azure AD Connect를 사용하여 온-프레미스 Active Directory에 저장된 그룹, 사용자 계정 및 암호 해시를 Azure AD와 동기화
  - 통과 인증을 사용할 수 없는 경우 백업으로 사용 가능
- 온-프레미스 Windows Server에 설치된 온-프레미스 인증 에이전트를 사용하여 통과 인증 구성
- Azure AD의 원활한 Single Sign-On 기능을 사용하여 온-프레미스 도메인에 조인된 PC의 사용자를 자동으로 로그인
  - 여러 인증 요청을 억제하여 사용자 마찰 감소

## <a name="authentication--access"></a>인증 및 액세스

Lamna Healthcare의 보안 정책에 따라 병원의 경계 네트워크 외부에서 발생하는 모든 로그인은 추가 인증 단계를 사용하여 인증해야 합니다. 이 요구 사항은 Azure AD 서비스의 다단계 인증과 조건부 액세스 정책을 결합한 것입니다.

### <a name="multi-factor-authentication"></a>다단계 인증

MFA(다단계 인증)는 전체 인증에 2개 이상의 요소를 요구하여 ID를 추가로 보호합니다. 이러한 요소는 세 가지 범주로 분류됩니다.

- *사용자가 알고 있는 것*
- *사용자가 소유하고 있는 것*
- *사용자의 신원 정보*

**사용자가 알고 있는 것**은 암호이거나 보안 질문에 대한 대답입니다. **사용자가 소유하고 있는 것**은 알림을 받는 모바일 앱 또는 토큰 생성 장치일 수 있습니다. **사용자의 신원 정보**는 여러 모바일 장치에서 사용되는 지문 또는 얼굴 검사처럼 일반적으로 생체 인식 속성의 일종입니다.

Multi-factor Authentication을 사용하면 자격 증명 노출의 영향이 제한되므로 ID 보안이 향상됩니다. 사용자의 암호를 알고 있는 공격자가 완벽하게 인증하려면 사용자의 전화기를 소유하고 있거나 사용자의 얼굴이 필요합니다. 단일 요소의 확인을 거친 인증만으로는 부족하며 공격자는 이러한 자격 증명을 사용하여 인증할 수 없습니다. 이렇게 하면 엄청난 보안 이점이 있으며, 가능한 모든 곳에 MFA를 사용할 수 있습니다.

Azure AD는 MFA 기능이 기본 제공되며, 다른 타사 MFA 공급자와 통합됩니다. 글로벌 관리자는 매우 중요한 계정이므로 Azure AD에서 글로벌 관리자 역할이 할당된 모든 사용자에게 무료로 제공됩니다. 그 외의 계정은 이 기능이 포함된 라이선스를 구입하고 계정에 라이선스를 할당하여 MFA를 사용할 수 있습니다.

### <a name="conditional-access-policies"></a>조건부 액세스 정책

MFA와 함께, 액세스 권한을 부여하기 전에 추가 요구 사항을 충족하게 하면 보호 계층을 추가할 수 있습니다. 의심스러운 IP 주소의 로그인을 차단하거나 맬웨어 보호 기능이 없는 장치의 액세스를 거부하면 위험한 로그인의 액세스를 제한할 수 있습니다.

Azure Active Directory는 그룹, 위치 또는 장치 상태 기반의 액세스 정책을 지원하는 CAP(조건부 액세스 정책) 기능을 제공합니다. 위치 기능을 사용하면 Lamna는 병원 네트워크에 속하지 않는 IP 주소를 구분하고 이와 같은 위치에서는 다단계 인증을 사용하도록 요구하여 보안 정책을 충족할 수 있습니다.

Lamna Healthcare는 회사 네트워크 외부의 IP 주소에서 응용 프로그램에 액세스하는 사용자가 MFA를 사용하기 어려운 [조건부 액세스 정책](https://docs.microsoft.com/azure/active-directory/conditional-access/overview)을 만들었습니다.

![조건부 액세스 정책 및 다단계 인증의 샘플 구현을 보여 주는 일러스트레이션입니다. 온-프레미스 및 클라우드 응용 프로그램 액세스에 대한 사용자 요청은 먼저 조건 목록에 대해 확인합니다. 요청은 액세스가 허용되거나, 다단계 인증을 통과하도록 강제되거나, 충족되는 조건에 따라 차단됩니다.](../media/conditional-access.png)

## <a name="securing-legacy-applications"></a>레거시 응용 프로그램 보호

Lamna Healthcare 직원은 온-프레미스에 호스트되는 관리 응용 프로그램에 대한 보안 원격 액세스를 요구합니다. 사용자들은 현재 병원 방화벽으로 보호되는 도메인 조인 머신에서 WIA(Windows 통합 인증)를 사용하여 응용 프로그램에 인증합니다. 응용 프로그램에 최신 인증 메커니즘을 통합하는 프로젝트가 계획되었지만, 원격 액세스 기능을 최대한 빨리 사용하게 해 달라는 비즈니스 압력을 심하게 받고 있습니다. Azure 응용 프로그램 프록시는 코드 변경 없이 원격으로 빠르고 쉽고 안전하게 응용 프로그램에 액세스할 수 있습니다.

다음은 Azure AD 응용 프로그램 프록시의 특징입니다.

- 단순함
  - 응용 프로그램 프록시를 사용하도록 응용 프로그램을 변경하거나 업데이트할 필요가 없습니다.
  - 사용자에게 일관된 인증 환경이 제공됩니다. MyApps 포털을 사용하여 클라우드 및 앱 온-프레미스의 SaaS 앱에 Single Sign-On을 가져올 수 있습니다.
- 안전
  - Azure AD 응용 프로그램 프록시를 사용하여 앱을 게시하면 Azure의 다양한 권한 부여 제어 및 보안 분석을 이용할 수 있습니다. 조건부 액세스 및 2단계 인증과 같은 클라우드 규모 보안 및 Azure 보안 기능이 제공됩니다.
  - 사용자에게 원격 액세스를 제공하기 위해 방화벽을 통해 모든 인바운드 연결을 열 필요가 없습니다.
- 경제성
  - 응용 프로그램 프록시는 클라우드에서 작업하므로 시간과 비용을 절약할 수 있습니다. 온-프레미스 솔루션을 사용하려면 일반적으로 DMZ, 에지 서버 또는 기타 복잡한 인프라를 설정하고 유지 관리해야 합니다.

Azure AD 응용 프로그램 프록시는 두 개의 구성 요소로 구성됩니다. 하나는 회사 네트워크 내부의 Windows 서버에 위치하는 커넥터 에이전트이고, 다른 하나는 외부 엔드포인트(MyApps 포털 또는 외부 URL)입니다. 사용자는 엔드포인트를 탐색할 때 Azure AD로 인증하며 커넥터 에이전트를 통해 온-프레미스 응용 프로그램으로 라우팅됩니다.

## <a name="working-with-consumer-identities"></a>소비자 ID 사용

최신 인증을 기존 응용 프로그램과 통합하고 얼마 지나지 않아 Lamna Healthcare는 Azure AD 같은 관리 ID 시스템이 조직에 제공하는 강력한 성능을 체험했습니다. 현재 리더십 팀은 Microsoft ID 서비스로 비즈니스 가치를 추가할 수 있는 다른 방법을 찾고 있습니다. 이제 외부 고객 그리고 기존 고객 상호 작용을 현대화하여 Google, Facebook, LinkedIn 같은 타사 ID 공급자와 긴밀하게 통합하는 방법에 집중하고 있습니다.

Azure AD B2C는 Azure Active Directory의 견고한 기반을 바탕으로 제작된 ID 관리 서비스로, 응용 프로그램을 사용할 때 고객이 자신의 프로필을 등록, 로그인 및 관리하는 방법을 사용자 지정하고 제어할 수 있습니다. 여기에는 iOS, Android 및 .NET용으로 개발된 응용 프로그램이 포함됩니다. Azure AD B2C는 소셜 ID 로그인 환경을 제공하는 동시에 고객 ID 프로필 정보를 보호합니다. Azure AD B2C 디렉터리는 표준 Azure AD 디렉터리와 다르며 Azure Portal에서 만들 수 있습니다.

## <a name="identity-management-at-lamna-healthcare"></a>Lamna Healthcare의 ID 관리

Lamna Healthcare가 Azure에서 ID 관리 솔루션을 사용하여 환경의 보안을 개선한 방법을 살펴보았습니다. 먼저 사용자에게 Single Sign-On 환경을 제공하여 사용자가 처리해야 하는 계정을 최소화하고, 계정이 가져오는 운영 복잡성을 줄였습니다. 응용 프로그램 액세스에 MFA를 적용했으며, 최소한의 노력으로 최신 인증을 사용하도록 레거시 응용 프로그램을 업데이트했습니다. 또한 소비자 ID를 다루는 기능을 개선하여 환자에 대한 응용 프로그램의 유용성을 향상시킬 수 있는 방법을 배웠습니다.

## <a name="summary"></a>요약

이 섹션에서는 다양한 Azure Active Directory 기능을 결합하여 위치에 관계없이 응용 프로그램에 안전하게 액세스할 수 있는 견고한 ID 솔루션을 제공하는 방법을 살펴보았습니다. ID는 중요한 보안 계층입니다. 적절하게 설계하여 아키텍처에 포함하면 환경을 안전하게 보호할 수 있습니다.