AngularJS는 명확하고 간결한 동적 웹 응용 프로그램을 만들기 위한 프레임워크입니다. 콘텐츠 템플릿 언어에 HTML을 사용하지만 데이터 바인딩 구문으로 HTML을 확장합니다. 데이터 바인딩 및 종속성 삽입에 AngularJS를 사용하면 콘텐츠 업데이트를 관리하는 데 필요한 많은 코드를 작성하지 않아도 됩니다. 사용자 콘텐츠가 브라우저 내에서 업데이트되므로 AngularJS를 서버 쪽 호스팅 기술과 연결할 수 있습니다.

## <a name="what-must-be-installed"></a>무엇을 설치해야 하나요?

AngularJS는 응용 프로그램에 액세스하는 클라이언트에만 사용할 수 있도록 설정해야 하는 프런트 엔드 JavaScript 프레임워크입니다. 여러 가지 방법으로 이를 수행할 수 있습니다.

1. CDN(콘텐츠 배달 네트워크)을 통해 AngularJS를 참조합니다.
1. 패키지 관리자로 npm을 사용하여 호스트된 콘텐츠에서 AngularJS를 Node.js 패키지로 사용합니다.
1. 호스트된 콘텐츠에서 AngularJS를 Bower 패키지로 사용합니다.

간단히 말해, 이 모듈에 CDN에서 직접 AngularJS를 사용합니다. 이렇게 하면 서버 콘텐츠에서 직접 관리하는 대신 스크립트 파일 종속성이 CDN에 전달되므로, 제공된 리소스에 사용된 CDN의 속도 및 지리적 배포에 따라 다운로드 속도가 향상될 수도 있습니다.

> [!Note]
> AngularJS는 웹 응용 프로그램 플랫폼을 완전히 다시 작성한 Angular의 선행 작업입니다. 대부분의 개념은 두 버전 간에 유사하지만 지금은 별도의 프로젝트입니다. Angular의 버전은 2.x.y 이상이지만, AngularJS의 버전은 1.x.y로 끝납니다. AngularJS는 여전히 웹 응용 프로그램 시나리오에 일반적으로 사용됩니다.

## <a name="how-to-install-angularjs-via-cdn"></a>CDN을 통해 AngularJS를 설치하는 방법

    You don't really _install_ AngularJS; you just add a reference to the JavaScript file via a script tag in you HTML page. Since AngularJS is critical to any functionality of our web application, we include it within the `<head>` tag like this (as compared to later loading of JavaScript files toward the end of the `<body>` tag).

    ```html
    <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
    ```
