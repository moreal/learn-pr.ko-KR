보안에서 가장 큰 문제 중 하나를 보호 하 고 취약점을 찾기 위해 해커 수행 전에 해야 하는 모든 영역을 보려면 수 있다는 것입니다. Azure는 Azure Security Center를 호출 하면 훨씬 쉽게 서비스를 제공 합니다.

## <a name="what-is-azure-security-center"></a>Azure Security Center란?

Azure Security Center (ASC)는 Azure 및 온-프레미스 모두에서 서비스의 모든 위협 보호를 제공 하는 모니터링 서비스입니다. 수행할 수 있습니다.

- 구성, 리소스 및 네트워크를 기반으로 보안 권장 사항을 제공 합니다.
- 온-프레미스에서 보안 설정을 모니터링 하 고 클라우드 워크 로드는 온라인으로 새 서비스에 필요한 보안을 자동으로 적용 합니다.
- 지속적으로 모든 서비스를 모니터링 하 고 악용 되기 전에 잠재적인 취약성을 식별 하는 자동 보안 평가 수행 합니다.
- 검색 하 고 서비스 및 가상 컴퓨터에 설치 되는 맬웨어를 차단 하는 데 기계 학습을 사용 합니다. 허용 목록 응용 프로그램을 유효성을 검사 하는 앱만 실행할 수 있도록 할 수도 있습니다.
- 분석 인바운드 공격 가능성를 식별 하 고 위협 및 위반 후 활동 발생 했을 수 있는 조사 하는 데 도움이 됩니다.
- 해야 하는 트래픽을 허용 하는 포트를 네트워크에만 함으로써 하면 공격 노출 영역이 감소에 대 한 just In Time 액세스 제어 합니다.

ASC의 일부인 합니다 [인터넷 보안 센터](https://www.cisecurity.org/cis-benchmarks/) (CI) 권장 사항입니다.

## <a name="activating-azure-security-center"></a>Azure Security Center 활성화

Azure Security Center 통합된 보안 관리 및 하이브리드 클라우드 워크 로드에 대 한 고급 위협 방지를 제공 하 고 두 계층으로 제공 됩니다: 무료 및 표준입니다. 무료 계층 표준 계층 기능, 위협 인텔리전스를 비롯 한 강력한 집합을 제공 하는 동안 보안 정책, 평가 및 권장 사항을 제공 합니다.

ASC의 이점을 들어 회사의 보안 팀 하기로 결정 했습니다 하 수 켜져 있는지 사무실에서 모든 구독에 대 한. 가져온 전자 메일이이 아침 응용 프로그램에 설정 하는 작업을 수행 하는 방법을 살펴보도록 하겠습니다.

1. 엽니다는 [Azure portal](https://portal.azure.com?azure-portal=true) 선택한 **Azure Security Center** 왼쪽 메뉴에서, 표시 되지 않으면 선택할 수 있습니다 **모든 서비스** 찾고  **Security Center** 보안 섹션에서 아래와 같이 합니다.

![Azure 보안 센터 열기](../media-draft/ASC-Menu.png)

2. ASC 되지 열었던 블레이드에 시작 됩니다 합니다 **Getting started** 항목 구독을 업그레이드 하도록 요청할 수도 있습니다. 이제 선택에 대 한 무시 **Skip** 한 다음 선택한 페이지의 맨 아래에 **개요**합니다.
    - 이 구독에서 사용할 수 있는 모든 요소에서 "보안 큰 그림"가 표시 됩니다.
    - 이 많은 유용한 정보를 탐색할 수 있습니다.

3. 다음으로, 선택 **검사**"정책 및 규정 준수" 아래. 구독 요소 표시 대상 (또는 다루지) ACS에서. 여기에 액세스할 수 있는 모든 구독에 대 한 ACS을 켤 수 있습니다. 세 가지 검사 영역 사이 전환 하세요: "다루지", "범위" 기본"및"범위"표준" 합니다.

4. 검사 되지 않은 구독에 ACS를 활성화 하 라는 메시지가 표시를 해야 합니다. 구독에 있는 모든 리소스에 대 한 ACS를 사용 하도록 설정 하려면 "지금 업그레이드" 단추를 눌러 수 있습니다.

![업그레이드 검사](../media-draft/Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a>무료 및 표준 가격 책정 계층

ASC를 사용 하 여 Azure 구독을 무료 계층을 사용할 수 있지만, 평가 및 권장 사항이 Azure 리소스에 제한 됩니다. ASC를 실제로 활용 하려면 위와 같이 표준 계층 구독으로 업그레이드 해야 합니다. "지금 업그레이드" 단추를 통해 구독을 업그레이드할 수는 **검사** 블레이드에서 위에서 설명한 것 처럼 합니다. 으로 전환할 수 있습니다는 **Getting Started** 블레이드에서 ASC 메뉴는 subscription 수준 변경 하는 방법을 안내 합니다. 에 대 한 전체 개요를 얻을 수 있습니다, 가격 및 기능 변경 될 수 있습니다 기반 지역에는 [가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/security-center/)합니다. 

> [!NOTE]
> 구독을 표준 계층으로 업그레이드하려면 구독 소유자, 구독 참가자 또는 보안 관리자의 역할이 할당되어야 합니다.

> [!IMPORTANT]
> 60 일 평가 기간이 끝난 후 ASC 가격이 **$15/노드 / 월** 계정에 청구 됩니다.

## <a name="turning-off-azure-security-center"></a>Azure Security Center 해제

프로덕션 시스템에 대 한 위협에 대 한 모든 리소스를 모니터링할 수 있도록 설정 하는 Azure Security Center를 유지 하려고 확실 하 게 합니다. 그러나 ASC를 사용 하 여 재생 하는 것을 켠 경우 가능성이 하려는 사용 하지 않도록 설정 확인 요금이 부과 되지 않습니다. 지금 수행 하겠습니다.

1. 엽니다는 [Azure portal](https://portal.azure.com?azure-portal=true) 선택한 **Azure Security Center** 왼쪽 메뉴에서, 표시 되지 않으면 선택할 수 있습니다 **모든 서비스** 찾고  **Security Center** 보안 섹션에서 아래와 같이 합니다.

![Azure 보안 센터 열기](../media-draft/ASC-Menu.png)

2. 선택 **보안 정책** 왼쪽 메뉴에서.

3. 다음으로, 선택 **설정 편집 >** 옆 ASC를 다운 그레이드 하려는 구독에 있습니다.

4. 다음 화면에서 왼쪽 메뉴에서 "가격 책정 계층"을 선택 합니다.

5. 새 페이지가 아래 이미지 처럼 보이는 표시 됩니다. "무료 (Azure 리소스에만 해당)" 라는 왼쪽에 있는 상자를 클릭 합니다.

![가격 책정 계층](../media-draft/Pricing-Tier.png)

6. 화면 맨 위에 있는 "저장" 단추를 누릅니다.

이제 구독 Azure Security Center의 무료 계층을 다운 그레이드 합니다.

## <a name="summary"></a>요약

<!-- TODO: need link to module --> 축, 첫 번째 (및 가장 중요 한) 단계에 응용 프로그램, 데이터 및 네트워크를 보호 하기 위해 수행 <!--If you want to learn more about Azure Security Center, you can go through the **Protect your resources with Azure Security Center** learning module.-->
