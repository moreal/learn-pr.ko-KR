대부분의 개발자 프레임 워크 및 라이브러리를 사용 하 여 해당 소프트웨어 기능 또는 개인 기본 설정으로 기본적으로 결정 하려면 빌드를 사용 하 여는 것이 좋습니다. 그러나 선택 하는 프레임 워크는에서 디자인 및 기능 측면에서 뿐만 아니라 중요 한 결정을 한 _보안_ 관점입니다. 최신 보안 기능을 사용 하 여 프레임 워크를 선택 하 고 최신 상태로 유지 하는 앱이 보안 확인에 대 한 가장 좋은 방법 중 하나입니다.

## <a name="choose-your-framework-carefully"></a>프레임 워크를 신중 하 게 선택

보안 프레임 워크를 선택 하 여 지원 되는 정도 대 한 가장 중요 한 요소는 것입니다. 최고의 프레임 워크 보안 정렬을 언급 및 개선 하 고 프레임 워크를 테스트 하는 대규모 커뮤니티에서 지원 됩니다. 소프트웨어도 버그 해제 하거나 완전히 안전 100% 이지만 특정 닫힙니다 또는 신속 하 게 제공 해결 방법이 있을 수 있도록 할 취약점 식별 될 때.

종종 "도 지원 되는"은 "최신"으로 합니다. 이전 프레임 워크를 교체 또는 널리 사용 되 고 결국 페이드 경향이 있습니다. 중요 한 경험이 있는 경우에 또는 또는 이전 프레임 워크에서 작성 된 많은 앱 수 선택 해야 하는 기능이 있는 최신 라이브러리는 것이 좋습니다. 최신 프레임 워크를 선택 하 새 앱에 대 한 위협에 노출 영역 축소의 형태는 이전 반복에서 학습 한 정보를 토대로 경향이 있습니다. 레거시 응용 프로그램에서 작성 된 이전 프레임 워크에서 발견 되는 경우에 대 한 걱정 작은 앱을 하나 있습니다.

<!-- TODO: add link; Should we be pointing to other modules? -->
<!--
For more information on secure design and reducing threat surface, please see [Design For Security in Azure](../../design-for-security-in-azure/index.yml).
-->

## <a name="keep-your-framework-updated"></a>업데이트 된 프레임 워크를 유지 합니다.

Java Spring 및.NET Core와 같은 소프트웨어 개발 프레임 워크를 정기적으로 업데이트 및 새 버전 릴리스 합니다. 이러한 업데이트는 새로운 기능, 이전 기능 및 보안 수정 사항을 자주 또는 향상 된 기능을 제거를 포함 합니다. 만료 되려면 프레임 워크를 허용 하는 경우 "기술 부채" 만듭니다. 더 오래 된, 최신 버전 코드를 가져올 수 어렵고 더 위험 합니다. 또한 유지 이전 버전의 framework 열기 하는 프레임 워크의 최신 릴리스에서 수정 되었습니다 자세한 보안 위협을까지 초기 프레임 워크 선택, 마찬가지로 합니다.

예를 들어, 2016-2017에서 [30 개 이상의 취약점으로 인 한](https://www.cvedetails.com/product/6117/Apache-Struts.html?vendor_id=45) Apache Struts framework에서 찾을 수 없습니다. 개발 팀에서 신속 하 게 처리 된이 있지만 일부 회사에서는 패치를 적용 하지 않은 하 고 [데이터 위반의 형태로 가격을 지불](https://www.zdnet.com/article/equifax-confirms-apache-struts-flaw-it-failed-to-patch-was-to-blame-for-data-breach/)합니다. **프레임 워크 및 라이브러리를 최신 상태로 유지 하도록 해야**합니다.

### <a name="how-do-i-update-my-framework"></a>필자의 프레임 워크를 업데이트 하려면 어떻게 해야 하나요?

Java 또는.NET과 같은 일부 프레임 워크를 설치 해야 하 고 알려진 주기로 릴리스 하는 경향이 있습니다. 새 릴리스에 대 한 보기를 사용해 해제 될 때까지 코드를 분기 하는 것이 좋습니다. 예를 들어,.NET Core 유지 관리를 [릴리스 정보 페이지](https://github.com/dotnet/core/tree/master/release-notes) 는 사용 가능한 최신 버전을 찾으려면 확인할 수 있습니다.

JavaScript 프레임 워크 등의 라이브러리를 더욱 특수화 된 또는 패키지 관리자를 통해.NET 구성 요소를 업데이트할 수 있습니다. **NPM** 하 고 **Bower** 웹 프로젝트에 널리 사용 되는 및 대부분의 Ide 지 또는 빌드 도구입니다. .NET을 사용 하 여 **NuGet** 구성 요소 종속성을 관리 합니다. 훨씬 핵심 프레임 워크 업데이트와 같은 코드를 분기, 구성 요소를 업데이트 및 테스트는 새 버전을 종속성의 유효성을 검사 하는 데 유용한 기술입니다.

> [!NOTE]
> `dotnet` 명령줄 도구에는 `add package` 하 고 `remove package` 옵션을 추가 하거나 제거할 NuGet 패키지 하지만 해당 필요는 없습니다 `update package` 명령입니다. 그러나 사실은 실행할 수 있습니다 `dotnet add package <package-name>` 프로젝트에는 자동으로 _업그레이드_ 패키지를 최신 버전입니다. 이 IDE를 열지 않고도 종속성을 업데이트 하는 쉬운 방법을 합니다.

## <a name="take-advantage-of-built-in-security"></a>기본 제공 보안 활용

보안 프레임 워크 제품 기능을 확인 하려면 항상 확인 합니다. **되지** 표준 기술을 또는 기능이 기본적으로 제공 하는 경우 사용자 고유의 보안을 배포 합니다. 또한 입증 된 알고리즘을 사용 하 고 워크플로 많은 전문가에서 철저 종종 이러한 때문에 평가 대상이 하도록 보장할 수는 안정적이 고 보안을 강화 합니다.

.NET Core 프레임 워크는 수많은 보안 기능, 문서의 위치를 시작 하는 몇 가지 core는 다음과 같습니다.
* [Authentication -Identity Management](https://docs.microsoft.com/aspnet/core/security/authentication/index?view=aspnetcore-2.1)
* [권한 부여](https://docs.microsoft.com/aspnet/core/security/authorization/index?view=aspnetcore-2.1)
* [Data Protection](https://docs.microsoft.com/aspnet/core/security/data-protection/index?view=aspnetcore-2.1)
* [보안 구성](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/index?view=aspnetcore-2.1)
* [보안 확장성 Api](https://docs.microsoft.com/aspnet/core/security/data-protection/extensibility/index?view=aspnetcore-2.1)

이러한 기능의 각각 해당 분야의 전문가 의해 작성 되었으며 의도 대로 작동 하는지 확인 하는 테스트와 의도 한 대로 다음 손상 된 합니다. 다른 프레임 워크 제품 유사한 기능-각 범주에 있는 확인 하기 위해 프레임 워크를 제공 하는 공급 업체를 사용 하 여 확인 합니다.

> [!WARNING]
> 프레임 워크에서 제공 하는 사용 하는 대신 사용자 지정 보안 컨트롤 작성은 없습니다만 시간을 낭비 하, 보안 수준이 낮습니다.


## <a name="azure-security-center"></a>Azure Security Center

웹 응용 프로그램을 호스팅할 Azure를 사용 하 여 Security Center에서 경고 메시지가 권장 구성 탭의 일부로 프레임 워크는 만료 하는 경우.  앱에 관련 된 모든 경고가 있는지 확인 하려면에서 찾는 것을 잊지 마세요.

![Azure Security Center 프레임 워크 업그레이드를 권장 합니다.](../media-draft/ASCFramework.png)


## <a name="summary"></a>요약

가능 하면 앱을 빌드, 항상 기본 제공 보안 기능을 사용 하 고 최신 상태로 유지 해야 하는 최신 프레임 워크를 선택 합니다. 이러한 간단한 규칙 견고한 기반 응용 프로그램을 시작 하도록 도와줍니다.
