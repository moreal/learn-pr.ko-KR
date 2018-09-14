많은 양의 최신 응용 프로그램에 있는 코드에는 라이브러리 및 선택한 종속성: 개발자. 이것이 시간과 돈을 절약할 수 있는 일반적인 사례입니다. 그러나 단점은 담당 하는 이제이 코드를 다른 사용자가 작성 한 후 프로젝트에서 사용 했기 때문에 경우에입니다. 연구원 (또는 더 심한 경우 해커가) 이러한 타사 라이브러리 중 하나에서 취약성 검색 한 다음 동일한 결함 될 가능성이 큽니다 또한 앱에 합니다.

구성 요소를 사용 하 여 알려진된 취약점을 사용 하 여 하는 것은 업계에서 큰 문제입니다. 즉 하므로 문제가 있는 것 했습니다 합니다 [OWASP 상위 10 개 목록](https://www.owasp.org/index.php/Category:OWASP_Top_Ten_Project) 최악의 웹 응용 프로그램의 취약성을 #9 년 동안 보유 하 고 합니다.

## <a name="track-known-security-vulnerabilities"></a>알려진된 보안 문제를 추적 합니다.

문제가 발견 되는 경우 문제가 있다고 알아야 합니다. 우리의 라이브러리 및 종속성을 유지 하는 업데이트 (# 4의 목록!) 물론 도움이 되겠지만 응용 프로그램에 영향을 줄 수 있는 식별 된 취약성을 추적 하는 것이 좋습니다.

> [!IMPORTANT]
> 시스템에는 알려진된 취약점으로 인 한 경우에 사용자는 해당 시스템을 공격 하는 데 사용할 수 있는 사용 가능한 코드를 악용 하 가능성이 훨씬 더 높습니다. 악용 공용 이루어지는 경우 것이 중요 영향을 받는 모든 시스템 즉시 업데이트 됩니다.

**Mitre** 는 유지 관리 하는 비영리 조직 합니다 [Common Vulnerabilities and Exposures 목록](https://cve.mitre.org)합니다. 이 목록은 앱, 라이브러리 및 프레임 워크에 알려진된 사이버 보안 취약점의 공개적으로 검색할 수 있는 집합입니다. **취약점에 알려진 CVE 데이터베이스에 라이브러리 또는 구성 요소를 찾을 경우**합니다.

문제는 제품 또는 구성 요소에서 보안 결함이 발견 되 면 보안 커뮤니티에서 전송 됩니다. 게시 된 각 문제는 취약점에 대 한 설명을 검색 날짜를 포함 및 문제에 대 한 공급 업체 문이나 게시 된 해결 방법에 대 한 참조는 ID가 할당 됩니다.

### <a name="how-to-verify-if-you-have-known-vulnerabilities-in-your-3rd-party-components"></a>에 타사 구성 요소에서 취약점으로 인 한 알려진 있는 경우를 확인 하는 방법

일별 작업을 이동 하 고이 목록을 확인 하려면 휴대폰에 배치할 수 있습니다 하지만 다행히 우리에 게 있어 많은 도구가 존재 종속성 취약 한 경우를 확인할 수 있습니다. 코드 베이스에 대해 이러한 도구를 실행할 수도 있고, 더 나아가 문제에 대 한 개발 프로세스의 일부로 자동으로 확인 하 여 CI/CD 파이프라인에 추가할 수 있습니다.

- [OWASP 종속성 확인](https://www.owasp.org/index.php/OWASP_Dependency_Check)에 있는 한 [Jenkins 플러그 인](https://wiki.jenkins.io/display/JENKINS/OWASP+Dependency-Check+Plugin)
- [OWASP SonarQube](https://www.owasp.org/index.php/OWASP_SonarQube_Project)
- [Synk](https://snyk.io), GitHub에서 오픈 소스 리포지토리에 대 한 무료
- [Black Duck](https://www.blackducksoftware.com) 대부분의 기업에서 사용 되는
- [RubySec](https://rubysec.com) Ruby에 대 한 자문 데이터베이스를
- [Retire.js](https://github.com/retirejs/retire.js/) 확인 하기 위한 도구 JavaScript 라이브러리 만료; 경우으로 사용할 수 플러그 인을 비롯 한 다양 한 도구에 대 한 [Burp Suite](https://www.portswigger.net)

정적 코드 분석을 위해 특별히 일부 도구는 물론이 사용할 수 있습니다.

- [Roslyn 경비원](https://dotnet-security-guard.github.io)
- [Puma 검색](https://pumascan.com)
- [PT 응용 프로그램 관리자](https://www.ptsecurity.com/ww-en/products/ai/)
- [Apache Maven 종속성 플러그 인](http://maven.apache.org/plugins/maven-dependency-plugin/)
- [원본 지우기](https://www.sourceclear.com)
- [Sonatype](https://ossindex.sonatype.org)
- [노드 보안 플랫폼](https://nodesecurity.io)
- [WhiteSource](https://www.whitesourcesoftware.com/what-is-whitesource/)
- [Hdiv](https://hdivsecurity.com)
- [더 많은 기능...](https://www.owasp.org/index.php/Source_Code_Analysis_Tools)

취약 한 구성 요소를 사용 하 여 관련 된 위험에 대 한 자세한 내용은 참조는 [OWASP 페이지](https://www.owasp.org/index.php/Top_10-2017_A9-Using_Components_with_Known_Vulnerabilities) 이 항목에서는 전용입니다.

## <a name="summary"></a>요약

모든 위험에도 수행 하는 응용 프로그램의 일부로 라이브러리 또는 다른 타사 구성 요소를 사용 하는 경우 있을 수 있습니다. 이 위험을 줄이는 가장 좋은 방법은 없는 알려진된 취약점을 상호 연결 되는 구성 요소 에서만 사용할 수 있도록 됩니다.
