응용 프로그램을 클라우드 플랫폼에 호스트하면 기존 온-프레미스 배포보다 훨씬 많은 장점이 있습니다. 클라우드의 공유 책임 모델에는 실제 네트워크, 빌드 및 클라우드 공급자의 컨트롤에서 호스트 수준에서 보안을 이동합니다. 이 수준에서 플랫폼을 약화시키려고 시도하는 공격자는 얻는 것이 점점 줄어드는 데 반해, 공급자는 인프라를 보호하고 모니터링하기 위해 상장한 투자를 하고 인사이트를 얻습니다.

그러므로 공격자는 응용 프로그램 수준에서 클라우드 플랫폼 고객 때문에 생기는 취약성을 노리는 것이 훨씬 더 효과적입니다. 또한 PaaS(Platform as a Service)를 도입하여 응용 프로그램을 호스트하는 고객은 운영 체제 보안을 관리하는 데 사용되는 리소스를 회수하여 응용 프로그램 코드를 강화하고 응용 프로그램 주변의 ID 경계를 모니터링하는 데 배포할 수 있습니다. 이 섹션에서는 설계를 통해 응용 프로그램 보안을 강화하는 몇 가지 방법을 살펴보겠습니다.

## <a name="scenario"></a>시나리오

Lamna Healthcare 고객은 온라인 웹 포털을 통해 개인 의료 기록에 액세스할 수 있어야 합니다. Health Insurance Portability and Accountability Act (HIPAA)를 사용 하 여 규정 준수는 필수 이며 개인 데이터 위반을 발생 하는 경우 중요 한 재무 처벌을 받을 위험이 회사 배치 따라서 응용 프로그램과 상호 작용 하는 개인 데이터 보호 보다 중요 합니다.

고객 응용 프로그램과 관련된 기본 영역은 다음과 같습니다.

- 응용 프로그램 설계 보안
- 데이터 보안
- ID 및 액세스 관리
- 엔드포인트 보안

## <a name="security-development-lifecycle"></a>보안 개발 수명 주기

응용 프로그램 설계 단계에서 [Microsoft SDL(Security Development Lifecycle)](https://www.microsoft.com/sdl) 프로세스를 사용하여 소프트웨어 개발 수명 주기에 보안 문제를 통합할 수 있습니다. 보안 및 규정 준수 문제는 응용 프로그램을 설계할 때 훨씬 쉽게 해결할 수 있으며 최종 제품의 보안 결함으로 이어질 수 있는 여러 일반 오류를 완화할 수 있습니다. 또한 소프트웨어 개발 과정의 초기에 문제를 해결하면 비용이 훨씬 적게 듭니다. 소프트웨어 프로젝트에서 사용할 수는 SDL 단계의 일반적인 순서는 다음과 같습니다.

1. 교육

    - 핵심 보안 교육

1. 요구 사항

    - 요구 사항 및 품질 게이트 정의
    - 보안 및 개인 정보 위험 분석
 
1. 설계

    - 공격 노출 영역 분석
    - 위협 모델링
 
1. 구현

    - 코드 품질을 측정할 수 있도록 도구 지정
    - 금지 된 Api 및 함수를 적용 합니다.
    - 정적 코드 분석 수행
    - 저장된 비밀의 리포지토리 검색
 
1. 확인

    - 동적/퍼지 테스트
    - 위협 모델/공격 노출 영역 확인
 
1. 릴리스

    - 보안 응답 계획 작성
    - 최종 보안 검토 수행
    - 릴리스 보관
 
1. 응답 

    - 위협 대응 실행

![보안 개발 수명 주기](../media/sdl.png)

SDL은 프로세스 또는 도구 집합이므로 문화적 측면이 강합니다. 여기서 보안은 기본 포커스 하 고 발전 하는 보안 기능을 조직의 모든 응용 프로그램 개발 요구 사항 멀었다고 수행할 수는 문화권을 빌드합니다.

<!-- Bear in mind that the migration of un-modified applications (especially COTS procured software systems) will not be able to perform many of the steps listed above.
 -->

## <a name="operational-security-assessment"></a>운영 보안 평가

응용 프로그램을 배포한 후에 해당 보안 상태를 평가 하 고 지속적으로,를 검색 하는 소프트웨어 개발 주기를 다시 기술 자료를 피드 하는 모든 문제를 완화 하는 방법을 결정에 필수적입니다. 이 작업을 수행하는 깊이는 데이터 개인 정보 보호 요구 사항뿐 아니라 소프트웨어 개발 및 운영 팀의 완성도 수준을 측정하는 요소입니다.

보안 취약성 검색 소프트웨어 서비스를 사용하면 이 프로세스를 자동화하여 팀에 침투 테스트처럼 비용이 많이 드는 수동 프로세스를 수행해야 하는 부담을 지우지 않고 주기적으로 보안 문제를 평가할 수 있습니다.

Azure Security Center는 이제 모든 Azure 구독에 기본적으로 사용되는 무료 서비스로 Azure Application Gateway 및 Azure 웹 응용 프로그램 방화벽 같은 다른 Azure 응용 프로그램 수준 서비스와 밀접하게 통합됩니다. 이러한 서비스의 로그를 분석 하 여 ASC 실시간으로 알려진된 취약성에 대해 보고할 수 응답을 완화 하는 것이 좋습니다 및도 자동으로 공격에 대 한 응답에서 플레이 북을 실행 하도록 구성할 수 있습니다.

<!-- SDL culture
Key Vault / MSI
CSE = App  -> DB & App Storage
Mention approach of code scanning & SDL
Scanning for passwords - Git
 -->

## <a name="identity-as-the-perimeter"></a>경계로써의 ID

ID 유효성 검사는 응용 프로그램에 대한 공격을 방어하는 첫 번째 방어선입니다. 세션을 인증하고 권한을 부여하여 웹 응용 프로그램 액세스를 제한하면 공격 노출 영역을 대폭 줄일 수 있습니다. Azure AD 및 Azure AD B2C는 ID 책임을 오프로드하고 완전히 관리되는 서비스에 액세스하는 효과적인 방법을 제공합니다. Azure AD 조건부 액세스 정책, privileged identity management 및 Id 보호 컨트롤 추가 무단된 액세스를 방지 하 고 변경 내용을 감사 하는 고객의 기능을 향상.

## <a name="data-protection"></a>데이터 보호

웹 응용 프로그램에 대한 모든 공격이 그런 것은 아니지만, 대부분의 경우 고객 데이터가 목표입니다. 응용 프로그램과 데이터 저장 레이어 간에 데이터를 안전하게 저장하고 전송하는 것이 중요합니다.

Lamna Healthcare는 매우 중요한 환자 의료 기록 데이터를 저장하고 액세스합니다. 미국 의회가 1996년에 시행한 HIPAA는 의료 서비스 공급자 및 고용주의 전자 의료 트랜잭션에 대한 국가 표준을 정의합니다. Lamna 환자는 의사와 같은 권한 있는 당사자에 게 의료 데이터에 대 한 보안 액세스를 확인 해야 합니다.

이러한 요구 사항을 준수 하려면 Lamna Healthcare가 모든 환자 데이터 전송 중 및 미사용 암호화 하는 응용 프로그램 수정 했습니다. 예를 들어 TLS(전송 계층 보안)를 사용하여 웹 응용 프로그램과 백 엔드 SQL 데이터베이스 간에 교환되는 데이터를 암호화합니다. Transparent Data Encryption (TDE)를 사용 하 여, 환경 손상 된 경우에 데이터는 올바른 암호 해독 키가 없는 모든 사용자에 게 효과적으로 쓸모 없는 SQL Server에서 미사용 데이터 암호화도 됩니다.

Blob 저장소에 저장 된 데이터를 암호화 하려면 클라이언트 쪽 암호화는 저장소 서비스에 기록 되기 전에 메모리에 데이터를 암호화를 사용할 수 있습니다. 이 암호화를 지원하는 라이브러리는 .NET, Java 및 Python에 사용할 수 있으며 데이터 암호화를 응용 프로그램에 직접 통합하여 데이터 무결성을 강화할 수 있습니다.

### <a name="secure-key-and-secret-storage"></a>보안 키 및 비밀 저장소

응용 프로그램 비밀(연결 문자열, 암호 등) 및 암호화 키를 데이터 액세스에 사용되는 응용 프로그램과 분리하는 것이 매우 중요합니다. 암호화 키 및 응용 프로그램 비밀을 구성 파일의 응용 프로그램 코드에 저장하면 절대 안 됩니다. 대신, Azure Key Vault 같은 안전한 저장소를 사용해야 합니다. 중요 한 데이터에 대 한 액세스 관리 서비스 Id를 통해 응용 프로그램 id로 제한 될 수 있습니다 하 고 암호화 키 누출의 경우 노출을 제한 하는 정기적으로 키를 회전할 수 있습니다. 고객은 온-프레미스 하드웨어 보안 모듈 (HSM)을 생성 한 자체 암호화 키를 사용 하 고도 Azure Key Vault 인스턴스는 단일 테 넌 트에 구현 되도록을 위임 하도록 선택할 수도 불연속 Hsm 합니다.

<!-- ### Secure and immutable file storage

All Azure storage accounts are encrypted by default using Microsoft managed keys. Azure customers also have the ability to use their own encryption keys (BYOK) to encrypt blob, file and queue data so that even the hosting provider has no access to unencrypted data. Data immutability is often required for auditing purposes or when legal disputes call for data to be effectively frozen for a determined amount of time. Azure has recently introduced an [immutable data storage](https://docs.microsoft.com/azure/storage/blobs/storage-blob-immutable-storage) option known as Write-Once, Read many (WORM) for this scenario. -->
