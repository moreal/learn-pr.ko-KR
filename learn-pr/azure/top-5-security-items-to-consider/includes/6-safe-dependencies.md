최신 응용 프로그램에 있는 대부분의 코드는 개발자가 선택한 라이브러리와 종속성입니다. 이러한 코드는 시간과 돈을 절약하는 일반적인 사례입니다. 그러나 단점은 다른 사용자가 작성했음에도 불구하고 사용자가 프로젝트에서 이러한 코드를 사용했으므로 현재 이 사용자에게 해당 코드에 대한 책임이 있다는 것입니다. 연구원(더 나쁘게는, 해커)이 이러한 타사 라이브러리 중 하나에서 취약성을 발견하면 앱에도 동일한 결함이 나타날 수 있습니다.

알려진 취약성이 있는 구성 요소를 사용하는 것은 업계에서 큰 문제입니다. 최악의 웹 응용 프로그램 취약성에 대한 [OWASP 상위 10개 목록](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project)에서 몇 년 동안 9위를 차지한 것은 매우 문제가 있습니다.

## <a name="track-known-security-vulnerabilities"></a>알려진 보안 취약성 추적

당면한 문제는 문제가 언제 발견되는지를 아는 것입니다. 라이브러리와 종속성을 업데이트된 상태로 유지하면(목록의 4번) 당연히 도움이 되겠지만, 응용 프로그램에 영향을 줄 수 있는 식별된 취약성을 추적하는 것이 좋습니다.

> [!IMPORTANT]
> 시스템에 알려진 취약성이 있는 경우 사용자가 해당 시스템을 공격하는 데 사용할 수 있는 코드를 악용할 가능성이 훨씬 더 높습니다. 악용이 공개되면 영향을 받는 모든 시스템을 즉시 업데이트해야 합니다.

**Mitre**는 [CVE(Common Vulnerabilities and Exposures) 목록](https://cve.mitre.org)을 유지 관리하는 비영리 조직입니다. 이 목록은 앱, 라이브러리 및 프레임워크에서 알려진 사이버 보안 취약성의 집합으로 공개적으로 검색할 수 있습니다. **CVE 데이터베이스에 있는 라이브러리 또는 구성 요소가 발견되면 알려진 취약성이 있습니다**.

제품이나 구성 요소에서 보안 결함이 발견되면 보안 커뮤니티에서 문제를 제출합니다. 게시된 각 문제에는 ID가 할당되며, 발견된 날짜, 취약성에 대한 설명 및 해당 문제에 대한 게시된 해결 방법 또는 공급업체에 대한 참조가 포함되어 있습니다.

### <a name="how-to-verify-if-you-have-known-vulnerabilities-in-your-3rd-party-components"></a>타사 구성 요소에서 알려진 취약성이 있는지 확인하는 방법

휴대폰에 일별 작업을 배치하여 이 목록으로 이동하고 확인할 수도 있지만, 다행히도 종속성이 취약한지를 확인할 수 있는 도구가 많이 있습니다. 이러한 도구를 코드베이스에 대해 실행하거나 더 나은 방법으로 CI/CD 파이프라인에 추가하여 개발 프로세스의 일부로 문제를 자동으로 확인할 수 있습니다.

- [OWASP 종속성 확인](https://www.owasp.org/index.php/OWASP_Dependency_Check) - [Jenkins 플러그 인](https://wiki.jenkins.io/display/JENKINS/OWASP+Dependency-Check+Plugin)이 있습니다.
- [OWASP SonarQube](https://www.owasp.org/index.php/OWASP_SonarQube_Project)
- [Synk](https://snyk.io) - GitHub의 오픈 소스 리포지토리에서 무료입니다.
- [Black Duck](https://www.blackducksoftware.com) - 많은 기업에서 사용합니다.
- [RubySec](https://rubysec.com) - Ruby 전용 자문 데이터베이스입니다.
- [Retire.js](https://github.com/retirejs/retire.js/) - 만료된 JavaScript 라이브러리인지 확인하는 도구입니다. [Burp Suite](https://www.portswigger.net)를 포함하여 다양한 도구에 대한 플러그 인으로 사용할 수 있습니다.

정적 코드 분석을 위해 특별히 만든 일부 도구도 이 용도로 사용할 수 있습니다.

- [Roslyn Security Guard](https://dotnet-security-guard.github.io)
- [Puma Scan](https://pumascan.com)
- [PT Application Inspector](https://www.ptsecurity.com/ww-en/products/ai/)
- [Apache Maven Dependency Plugin](https://maven.apache.org/plugins/maven-dependency-plugin/)
- [Source Clear](https://www.sourceclear.com)
- [Sonatype](https://ossindex.sonatype.org)
- [Node Security Platform](https://nodesecurity.io)
- [WhiteSource](https://www.whitesourcesoftware.com/what-is-whitesource/)
- [Hdiv](https://hdivsecurity.com)
- [기타 등등...](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)

취약한 구성 요소 사용과 관련된 위험에 대한 자세한 내용은 이 항목 전용의 [OWASP 페이지](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities)를 참조하세요.

## <a name="summary"></a>요약

응용 프로그램의 일부로 라이브러리 또는 다른 타사 구성 요소를 사용하는 경우 발생할 수 있는 위험도 감수해야 합니다. 이러한 위험을 줄이는 가장 좋은 방법은 알려진 관련 취약성이 없는 구성 요소만 사용하도록 하는 것입니다.
