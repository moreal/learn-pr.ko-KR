보안과 관련된 가장 큰 문제 중 하나는 보호할 모든 영역을 살펴보고 해커보다 먼저 취약점을 찾아내는 것입니다. Azure는 이 작업을 훨씬 쉽게 할 수 있는 Azure Security Center라고 하는 서비스를 제공합니다.

## <a name="what-is-azure-security-center"></a>Azure Security Center란?

ASC(Azure Security Center)는 Azure와 온-프레미스의 모든 서비스에 대한 위협 보호를 제공하는 모니터링 서비스입니다. 다음과 같은 기능이 있습니다.

- 구성, 리소스 및 네트워크를 기반으로 보안 권장 사항을 제공합니다.
- 온-프레미스 및 클라우드 워크로드의 보안 설정을 모니터링하면서 새 서비스가 온라인으로 전환되면 필요한 보안을 자동으로 적용합니다.
- 모든 서비스를 지속적으로 모니터링하면서 자동 보안 평가를 수행하여 잠재적 취약점이 악용되기 전에 미리 식별합니다.
- 기계 학습을 사용하여 맬웨어를 검색하고 서비스 및 가상 머신에 설치되지 않도록 차단합니다. 또한 유효성을 검사한 앱만 실행할 수 있도록 응용 프로그램 허용 목록을 작성할 수 있습니다.
- 잠재적 인바운드 공격을 분석 및 식별하고, 발생했을지도 모르는 위협 및 게시물 보안 위반 활동을 조사합니다.
- 포트에 대한 Just-In-Time 액세스 제어를 통해 필요한 트래픽만 네트워크에서 허용하여 공격 노출 영역을 줄입니다.

ASC는 [CIS(Center for Internet Security)](https://www.cisecurity.org/cis-benchmarks/) 권장 사항의 일부입니다.

## <a name="activating-azure-security-center"></a>Azure Security Center 활성화

ASC의 이점을 고려하여 회사의 보안 팀에서는 사무실의 모든 구독에서 ASC를 켜기로 결정했습니다. 여러분은 오늘 아침에 응용 프로그램에서 ASC를 켜라는 이메일을 받았습니다. 지금부터 그 방법을 살펴보겠습니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 왼쪽 메뉴에서 **Azure Security Center**를 선택합니다. 이 위치에서 Azure Security Center가 보이지 않으면 아래 그림처럼 보안 섹션에서 **모든 서비스**를 선택하고 **Security Center**를 찾아봅니다.

![Azure Security Center 열기](../media-draft/ASC-Menu.png)

2. ASC를 한 번도 열지 않은 경우 블레이드가 **시작** 항목에서 시작되고 구독을 업그레이드하라는 요청이 표시될 수 있습니다. 지금은 이 요청을 무시하고, 페이지 맨 아래에서 **건너뛰기**를 선택한 다음, **개요**를 선택합니다.
    - 그러면 구독에서 사용할 수 있는 모든 요소에서 "보안 큰 그림"이 표시됩니다.
    - 여기서 수많은 유용한 정보를 탐색할 수 있습니다.

3. 다음으로, "정책 및 규정 준수" 아래에서 **적용 범위**를 선택합니다. 그러면 ACS의 범위에 포함되는(또는 포함되지 않는) 구독 요소가 표시됩니다. 여기서 액세스 권한이 있는 구독에 대해 ACS을 켤 수 있습니다. "포함되지 않음", "기본 범위", "표준 범위"의 세 가지 범위 영역 사이에서 전환해 보세요.

4. 포함되지 않는 구독에는 ACS를 활성화하라는 프롬프트가 생길 것입니다. "지금 업그레이드" 단추를 눌러 구독의 모든 리소스에 ACS를 사용하도록 설정할 수 있습니다.

![적용 범위 업그레이드](../media-draft/Upgrade-Now.png)

### <a name="free-vs-standard-pricing-tier"></a>체험 계층과 표준 계층의 차이점

ASC에 Azure 체험 계층을 사용할 수 있지만, Azure 리소스의 평가 및 권장 사항으로 제한됩니다. ASC를 제대로 활용하려면 위와 같이 표준 계층 구독으로 업그레이드해야 합니다. 위에서 언급했듯이 **적용 범위** 블레이드의 "지금 업그레이드" 단추를 통해 구독을 업그레이드할 수 있습니다. 구독 수준을 변경하는 방법을 안내하는 ASC 메뉴에서 **시작** 블레이드로 전환할 수도 있습니다. 가격 및 기능은 지역에 따라 달라질 수 있으며, 전체 내용은 [가격 책정 페이지](https://azure.microsoft.com/en-us/pricing/details/security-center/)에서 확인할 수 있습니다. 

> [!NOTE]
> 구독을 표준 계층으로 업그레이드하려면 구독 소유자, 구독 기여자 또는 보안 관리자 역할이 할당되어야 합니다.

> [!IMPORTANT]
> 60일 평가판 기간이 끝나면 **노드당 매월 $15**의 ASC 사용 요금이 계정에 청구됩니다.

## <a name="turning-off-azure-security-center"></a>Azure Security Center 끄기

프로덕션 시스템의 경우 모든 리소스를 모니터링하여 위협을 감지할 수 있도록 Azure Security Center를 계속 사용할 것입니다. 하지만 ASC를 시험해 보려고 잠시 켠 경우 요금이 부과되지 않도록 다시 끄는 것이 좋습니다. 그 방법을 알아보겠습니다.

1. [Azure Portal](https://portal.azure.com?azure-portal=true)을 열고 왼쪽 메뉴에서 **Azure Security Center**를 선택합니다. 이 위치에서 Azure Security Center가 보이지 않으면 아래 그림처럼 보안 섹션에서 **모든 서비스**를 선택하고 **Security Center**를 찾아봅니다.

![Azure Security Center 열기](../media-draft/ASC-Menu.png)

2. 왼쪽 메뉴에서 **보안 정책**을 선택합니다.

3. 다음으로, ASC를 다운그레이드할 구독 옆에서 **설정 편집 >** 을 선택합니다.

4. 그 다음 화면의 왼쪽 메뉴에서 "가격 책정 계층"을 선택합니다.

5. 아래 이미지와 비슷한 새 페이지가 나타납니다. 왼쪽에서 "체험(Azure 리소스만 해당)"이라고 적힌 상자를 클릭합니다.

![가격 책정 계층](../media-draft/Pricing-Tier.png)

6. 화면 위쪽에서 "저장" 단추를 누릅니다.

이제 구독이 Azure Security Center 체험 계층으로 다운그레이드되었습니다.

## <a name="knowledge-check"></a>지식 검사
<!-- TODO: move into yaml --> ASC 기능을 모두 선택하세요.

* 권장 사항(정답)
* 마이그레이션(오답)
* 방어(오답)
* Just In Time(정답)
* 위협 검색(정답)

## <a name="summary"></a>요약

<!-- TODO: need link to module --> 축하합니다. 응용 프로그램, 데이터 및 네트워크를 보호하기 위한 첫 번째(그리고 가장 중요한) 단계가 끝났습니다. <!--If you want to learn more about Azure Security Center, you can go through the **Protect your resources with Azure Security Center** learning module.-->
