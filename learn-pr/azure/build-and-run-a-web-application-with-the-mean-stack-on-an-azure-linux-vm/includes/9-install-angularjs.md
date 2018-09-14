AngularJS는 명확하고 간결한 동적 웹 응용 프로그램을 만들기 위한 프레임워크입니다. 콘텐츠 템플릿 언어에 HTML을 사용하지만 데이터 바인딩 구문으로 HTML을 확장합니다. 데이터 바인딩 및 종속성 삽입에 AngularJS를 사용하면 콘텐츠 업데이트를 관리하기 위해 작성해야 하는 많은 코드를 작성하지 않아도 됩니다. 사용자 콘텐츠가 브라우저 내에서 업데이트되므로 AngularJS를 서버 쪽 호스팅 기술과 연결할 수 있습니다.

## <a name="angularjs-information"></a>Angular.js 정보

AngularJS는 프런트 엔드 JavaScript 프레임워크이므로 응용 프로그램에 액세스하는 클라이언트에만 사용할 수 있도록 설정해야 합니다. 이 설정은 여러 가지 방법으로 수행할 수 있습니다.

- CDN(콘텐츠 배달 네트워크)을 통해 AngularJS를 참조합니다.
- 패키지 관리자로 npm을 사용하여 호스트된 콘텐츠에서 AngularJS를 Node.js 패키지로 사용합니다.
- 호스팅된 콘텐츠에서 AngularJS를 Bower 패키지로 사용합니다.

간소화하기 위해 이 모듈에 대해 CDN에서 직접 AngularJS를 사용합니다. 이러한 방식을 통해 서버 콘텐츠에서 스크립트 파일 종속성을 직접 관리하지 않고 CDN에 전달합니다. 또한 이러한 방식은 지정된 리소스에 사용되는 CDN의 지리적 분포 및 속도에 따라 다운로드 속도를 향상시킬 수도 있습니다.

> [!NOTE]
> AngularJS는 완전히 다시 작성한 웹 응용 프로그램 플랫폼인 Angular의 이전 버전입니다. 대부분의 개념은 두 버전 간에 유사하지만 지금은 별도의 프로젝트입니다. Angular의 버전은 2.x.y 이상이지만, AngularJS의 버전은 1.x.y로 끝납니다. AngularJS는 여전히 웹 응용 프로그램 시나리오에 일반적으로 사용됩니다.

## <a name="how-to-install-angularjs-via-cdn"></a>CDN을 통해 AngularJS를 설치하는 방법

실제로 AngularJS를 _설치_하지 않습니다. HTML 페이지의 스크립트 태그를 통해 JavaScript 파일에 참조를 추가합니다. AngularJS는 웹 응용 프로그램의 모든 기능에 중요하므로 다음과 같은 `<head>` 태그 내에(`<body>` 태그의 끝에 JavaScript 파일의 이후 로딩과 비교하여) AngularJS를 포함시킵니다.

```html
<script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
```
