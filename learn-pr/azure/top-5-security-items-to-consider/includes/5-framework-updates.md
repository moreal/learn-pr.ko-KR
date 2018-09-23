많은 개발자들은 소프트웨어를 빌드하는 데 사용할 프레임워크 및 라이브러리를 주로 기능 또는 개인적 기호에 따라 결정합니다. 그러나 프레임워크 선택은 디자인과 기능의 관점뿐 아니라 _보안_의 관점에서도 중요합니다. 최신 보안 기능이 탑재된 프레임워크를 선택하여 최신 상태로 유지하는 것은 앱을 안전하게 보호하는 가장 좋은 방법 중 하나입니다.

## <a name="choose-your-framework-carefully"></a>신중하게 프레임워크 선택

프레임워크를 선택할 때 보안과 관련된 가장 중요한 요소는 프레임워크가 얼마나 잘 지원되는가 입니다. 보안 대책이 마련되어 있고 프레임워크를 테스트하고 개선하는 대규모 커뮤니티의 지원을 받는 프레임워크가 가장 좋습니다. 버그가 하나도 없거나 100% 안전한 소프트웨어는 없지만, 취약점이 발견되면 신속하게 해결되거나 해결 방법이 제공된다는 확신이 필요합니다.

"잘 지원된다"는 말은 종종 "최신"과 동의어입니다. 기존 프레임워크는 최신 프레임워크로 교체되거나 결국 인기가 떨어집니다. 기존 프레임워크에 상당한 경험을 갖고 있거나 여러 앱이 기존 프레임워크로 작성되었더라도 필요한 기능을 탑재한 최신 라이브러리를 선택하는 것이 좋습니다. 최신 프레임워크는 과거의 반복적 경험을 통해 새 앱을 선택하는 것이 위협 노출 영역을 줄이는 방법이라는 교훈을 바탕으로 개발됩니다. 레거시 응용 프로그램이 작성된 기존 프레임워크에서 취약점이 발견된다면 걱정할 앱이 하나 줄어드는 것입니다.

보안 설계 및 위협에 대한 노출을 줄이는 방법에 대한 자세한 내용은 [Azure의 보안을 위한 설계](../../design-for-security-in-azure/index.yml)를 참조하세요.

## <a name="keep-your-framework-updated"></a>프레임워크를 최신 상태로 유지

Java Spring, .NET Core 등의 소프트웨어 개발 프레임워크는 정기적으로 업데이트 및 새 버전이 출시됩니다. 이러한 업데이트에는 새로운 기능이 포함되거나, 기존 기능이 제거되거나, 종종 보안 픽스 또는 개선 사항이 포함됩니다. 프레임워크가 오래 되도록 내버려 두면 "기술적인 문제"가 발생합니다. 프레임워크가 오래 될수록 코드를 최신 버전으로 업데이트하기가 더 어렵고 위험합니다. 또한 처음에 프레임워크를 선택할 때와 마찬가지로 이전 버전의 프레임워크를 계속 유지하면 최신 릴리스에서는 수정된 보안 위협에 노출됩니다.

예를 들어 2016-2017년에 Apache Struts 프레임워크에서 [30개가 넘는 취약점](https://www.cvedetails.com/product/6117/Apache-Struts.html?vendor_id=45)이 발견되었습니다. 개발 팀에서 신속하게 해결했지만, 일부 회사는 패치를 적용하지 않아 [데이터 보안 위반이라는 대가](https://www.zdnet.com/article/equifax-confirms-apache-struts-flaw-it-failed-to-patch-was-to-blame-for-data-breach/)를 치러야 했습니다. **프레임워크 및 라이브러리를 최신 상태로 유지하세요**.

### <a name="how-do-i-update-my-framework"></a>프레임워크를 업데이트하려면 어떻게 할까요?

Java 또는 .NET 같은 일부 프레임워크는 설치가 필요하며 알려진 주기로 릴리스되는 경향이 있습니다. 새 릴리스가 출시될 때까지 기다렸다가 코드를 분기하는 계획을 세우는 것이 좋습니다. 예를 들어 .NET Core는 사용 가능한 최신 버전을 확인할 수 있는 [릴리스 정보 페이지](https://github.com/dotnet/core/tree/master/release-notes)를 유지 관리합니다.

JavaScript 프레임워크 또는 .NET 구성 요소처럼 보다 특수한 라이브러리는 패키지 관리자를 통해 업데이트할 수 있습니다. **NPM** 및 **Bower**는 웹 프로젝트에 널리 사용되며 대부분의 IDE 또는 빌드 도구에서 지원됩니다. .NET에서는 **NuGet**을 사용하여 구성 요소 종속성을 관리합니다. 코어 프레임워크 업데이트와 마찬가지로, 코드를 분기하고 구성 요소를 업데이트하고 테스트하는 것은 새로운 버전의 종속성을 확인하는 유용한 기술입니다.

> [!NOTE]
> `dotnet` 명령줄 도구는 NuGet 패키지를 추가 또는 제거하는 `add package` 및 `remove package` 옵션을 제공하지만 해당하는 `update package` 명령은 없습니다. 그러나 사실은 프로젝트에서 `dotnet add package <package-name>` 명령을 실행할 수 있으며 그러면 패키지가 자동으로 최신 버전으로 _업그레이드_됩니다. 이것은 IDE를 열지 않고 종속성을 업데이트하는 손쉬운 방법입니다.

## <a name="take-advantage-of-built-in-security"></a>기본 보안 활용

항상 프레임워크에서 제공하는 보안 기능을 확인하세요. 표준 기술 또는 기능이 기본적으로 제공되는 경우 **절대로** 자체 보안을 배포하지 마세요. 또한 검증된 알고리즘과 워크플로를 사용하세요. 수많은 전문가들의 검증과 비평을 거쳐 보완되었기 때문에 믿을 수 있고 안전합니다.

.NET Core 프레임워크는 수많은 보안 기능을 제공하며, 다음은 이 문서의 주요 시작 위치입니다.
* [인증 - ID 관리](https://docs.microsoft.com/aspnet/core/security/authentication/index?view=aspnetcore-2.1)
* [권한 부여](https://docs.microsoft.com/aspnet/core/security/authorization/index?view=aspnetcore-2.1)
* [데이터 보호](https://docs.microsoft.com/aspnet/core/security/data-protection/index?view=aspnetcore-2.1)
* [구성 보안](https://docs.microsoft.com/aspnet/core/security/data-protection/configuration/index?view=aspnetcore-2.1)
* [보안 확장성 API](https://docs.microsoft.com/aspnet/core/security/data-protection/extensibility/index?view=aspnetcore-2.1)

각 기능은 해당 분야의 전문가에 의해 개발되었으며 의도한 대로, 의도한 대로만 작동하도록 수많은 테스트를 거쳤습니다. 다른 프레임워크도 비슷한 기능을 제공합니다. 프레임워크를 제공하는 공급 업체에 문의하여 각 범주에 어떤 기능이 있는지 알아보세요.

> [!WARNING]
> 프레임워크에서 제공하는 보안 컨트롤 대신 자체 컨트롤을 작성하는 것은 시간 낭비일 뿐 아니라 안전하지도 않습니다.


## <a name="azure-security-center"></a>Azure Security Center

Azure를 사용하여 웹 응용 프로그램을 호스트할 경우 프레임워크가 오래 되면 Security Center에서 권장 사항 탭의 일부로 이 사실을 경고합니다.  종종 권장 사항 탭을 살펴보고 앱과 관련된 경고가 있는지 확인하세요.

![프레임워크 업그레이드를 권장하는 Azure Security Center.](../media/5-ASCFramework.png)


## <a name="summary"></a>요약

되도록이면 최신 프레임워크를 선택하여 앱을 빌드하고, 항상 기본 제공 보안 기능을 사용하고, 최신 상태로 유지해야 합니다. 이처럼 간단한 규칙만 준수해도 견고한 기반 위에서 응용 프로그램을 시작할 수 있습니다.
