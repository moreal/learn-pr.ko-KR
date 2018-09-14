이 단원에서는 Node.js에 호스트된 간단한 AngularJS 응용 프로그램을 만들고 경로 지정을 위해 Express를 사용하려고 합니다. 백 엔드에서는 MongoDB가 데이터 저장소로 제공됩니다. 이 응용 프로그램은 도서를 나열하고, 추가하고, 삭제할 수 있는 도서 데이터베이스입니다.

> [!Important]
> 간단한 응용 프로그램이며, 새로 설치된 MEAN 스택을 테스트하기 위한 목적으로 설계되었습니다. 이 응용 프로그램은 프로덕션에 사용하기에는 보안이나 준비가 충분하지 않습니다.

## <a name="connect-to-the-vm"></a>VM에 연결

아직 VM에 연결되지 않은 경우 다음 명령을 실행합니다. `<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공용 IP 주소로 바꿉니다.

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="create-the-back-end"></a>백 엔드 만들기

1. 다음 명령을 사용하여 새 샘플 응용 프로그램의 폴더 구조를 만듭니다.

    ```bash
    mkdir ~/Books
    mkdir ~/Books/app
    mkdir ~/Books/public
    ```

    관리 사용자의 홈 위치에서 프로젝트 앱 및 해당 종속성이 포함되는 “Books” 폴더를 만들었습니다. 해당 폴더에서 모든 응용 프로그램 리소스와 스크립트가 포함되는 “app” 폴더를 만들었습니다. 마지막으로 적절한 HTTP 요청에 직접 제공될 클라이언트 쪽 파일이 모두 포함되는 "public" 폴더도 만들겠습니다.

1. **Express**를 설치하여 HTTP 요청 경로 지정을 처리하고 웹 응용 프로그램 사용자에게 반환할 콘텐츠를 결정합니다.

    다음 명령을 실행하여 Express를 사용할 웹 응용 프로그램 패키지로 추가합니다.

      ```bash
      npm install express
      ```

1. **Mongoose**를 설치하여 MongoDB와 HTTP 요청 경로 지정 간에 도서데이터를 릴레이하도록 지원합니다.

    도서 정보는 REST API 요청을 통해 쿼리됩니다. MongoDB와 API 사이의 데이터 전송을 간소화하려면 Mongoose를 사용합니다. Mongoose는 데이터를 모델링하기 위한 스키마 기반 시스템입니다. 여기서는 다양한 GET, POST 및 DELETE HTTP 요청에서 데이터 모델이 일관성을 유지하도록 샘플 응용 프로그램에서 Mongoose를 사용합니다.

    다음 명령을 실행하여, 사용할 웹 응용 프로그램 패키지로 Mongoose를 추가합니다.

      ```bash
      npm install mongoose
      ```

1. **body-parser**를 설치하여 ExpressRoute 지정에 사용할 JSON 요청 데이터를 사전 처리합니다.

    백 엔드에서는 `body-parser`가 들어오는 JSON 요청 데이터를 구문 분석하기 위한 Node.js 및 Express 간 미들웨어 역할을 합니다.

    다음 명령을 실행하여 `body-parser`를 사용할 웹 응용 프로그램 패키지로 추가합니다.

      ```bash
      npm install body-parser
      ```

    > [!TIP]
    > 여러 npm 패키지를 설치하는 경우 다음과 같은 단일 명령에 모두 포함할 수도 있습니다.
    > ```bash
    > npm install express mongoose body-parser
    > ```

1. Mongoose를 사용하여 도서 웹 응용 프로그램에 대한 데이터 모델 백 엔드를 만듭니다.

    1. **Books** 응용 프로그램 폴더 내의 **app** 폴더에 도서의 Mongoose 기반 데이터 모델을 포함할 **model.js**라는 새 JavaScript 파일을 만듭니다.

        ```bash
        nano ~/Books/app/model.js
        ```

    1. Mongoose를 사용하여 도서 스키마를 만들기 위해 이러한 새 파일에 다음 코드를 붙여넣습니다.

        ```javascript
        var mongoose = require('mongoose');
        var dbHost = 'mongodb://localhost:27017/Books';
        mongoose.connect(dbHost,  { useNewUrlParser: true } );
        mongoose.connection;
        mongoose.set('debug', true);
        var bookSchema = mongoose.Schema( {
            name: String,
            isbn: {type: String, index: true},
            author: String,
            pages: Number
        });
        var Book = mongoose.model('Book', bookSchema);
        module.exports = Book // mongoose.model('Book', bookSchema);
        ```

        > [!TIP]
        > 현재 파일을 **nano**에 저장하려면 **Ctrl**+**O**를 눌러야 합니다. **nano**를 종료하려면 **Ctrl**+**X**를 눌러야 합니다.

        이 코드는 로컬 VM의 MongoDB 서버에 있는 "Books"라는 데이터베이스에 연결합니다. 그런 다음, `bookSchema` 변수로 정의된 스키마를 사용하여 "Books"라는 데이터베이스 문서를 만듭니다.

1. 응용 프로그램에 대한 ExpressRoute를 만들어 다양한 HTTP 요청을 처리합니다.

    1. **app** 폴더 내에서 **routes.js**라는 새 JavaScript 파일을 만듭니다.

        ```bash
        nano ~/Books/app/routes.js
        ```

    1. 이러한 새 파일에 다음 코드를 붙여넣고 Express를 사용하여 경로를 설정합니다.

        ```javascript
        var path = require('path');
        var Book = require('./model');
        var routes = function(app) {
            app.get('/book', function(req, res) {
                Book.find({}, function(err, result) {
                    if ( err ) throw err;
                    res.json(result);
                });
            });
            app.post('/book', function(req, res) {
                var book = new Book( {
                    name:req.body.name,
                    isbn:req.body.isbn,
                    author:req.body.author,
                    pages:req.body.pages
                });
                book.save(function(err, result) {
                    if ( err ) throw err;
                    res.json( {
                        message:"Successfully added book",
                        book:result
                    });
                });
            });
            app.delete("/book/:isbn", function(req, res) {
                Book.findOneAndRemove(req.query, function(err, result) {
                    if ( err ) throw err;
                    res.json( {
                        message: "Successfully deleted the book",
                        book: result
                    });
                });
            });
            app.get('*', function(req, res) {
                res.sendFile(path.join(__dirname + '/public', 'index.html'));
            });
        };
        module.exports = routes;
        ```

        이 코드는 본 응용 프로그램에 대해 4개의 경로를 만듭니다. 처음 세 개 경로는 사용자가 API GET, POST 또는 DELETE 요청을 `/book` 리소스로 보내는 경우 수행할 작업을 지정합니다. 마지막 한 개 경로는 요청자를 인덱스 페이지로 보내는 모든 경로를 포착합니다.

        Express는 경로 처리 코드에 직접 HTTP 응답을 제공하거나 파일의 정적 콘텐츠를 제공할 수 있습니다. 이 예제 웹 응용 프로그램에서 둘 다 수행하려고 합니다. API 요청에 대한 JSON 데이터 및 index.html 파일에서 직접 HTML 데이터를 사용하여 응답합니다.

1. **Books** 폴더에 **server.js** 파일을 만들어 Node.js 호스팅을 구성합니다(ExpressRoute 사용).

    1. 응용 프로그램 루트 **Books** 폴더로 돌아가서 **server.js**라는 새 JavaScript 파일을 만듭니다.

        ```bash
        nano ~/Books/server.js
        ```

    1. 이러한 새 파일에 다음 코드를 붙여넣어 웹 응용 프로그램을 구성하고 기본 HTTP 포트 수신 대기를 시작합니다.

        ```javascript
        var express = require('express');
        var bodyParser = require('body-parser');
        var app = express();
        app.use(express.static(__dirname + '/public'));
        app.use(bodyParser.json());
        require('./app/routes')(app);
        app.set('port', 80);
        app.listen(app.get('port'), function() {
            console.log('Server up: http://localhost:' + app.get('port'));
        });
        ```

        이 코드는 웹 응용 프로그램 자체를 만듭니다. 이름이 **public**인 폴더(다음에 만듦)의 정적 파일을 사용하며 이전 단계에서 정의된 경로를 사용합니다.

1. 프런트 엔드 HTML 및 클라이언트 쪽 JavaScript 응용 프로그램을 만듭니다.

    1. **public** 콘텐츠 폴더 내에서 **script.js**라는 새 JavaScript 파일을 만듭니다.

        ```bash
        nano ~/Books/public/script.js
        ```

    1. 이러한 새 파일에 다음 코드를 붙여넣어 웹 서버와의 통신을 처리하도록 클라이언트 쪽 웹 응용 프로그램을 구성합니다.

        ```javascript
        var app = angular.module('myApp', []);
        app.controller('myCtrl', function($scope, $http) {
            var getData = function() {
                return $http( {
                    method: 'GET',
                    url: '/book'
                }).then(function successCallback(response) {
                    $scope.books = response.data;
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
            getData();
            $scope.del_book = function(book) {
                $http( {
                    method: 'DELETE',
                    url: '/book/:isbn',
                    params: {'isbn': book.isbn}
                }).then(function successCallback(response) {
                    console.log(response);
                    return getData();
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
            $scope.add_book = function() {
                var body = '{ "name": "' + $scope.Name +
                '", "isbn": "' + $scope.Isbn +
                '", "author": "' + $scope.Author +
                '", "pages": "' + $scope.Pages + '" }';
                $http({
                    method: 'POST',
                    url: '/book',
                    data: body
                }).then(function successCallback(response) {
                    console.log(response);
                    return getData();
                }, function errorCallback(response) {
                    console.log('Error: ' + response);
                });
            };
        });
        ```

        이 클라이언트 쪽 AngularJS 코드는 `myCtrl`이라는 하나의 컨트롤러를 포함하는 새 Angular 응용 프로그램 `myApp`을 만듭니다. 뷰어 브라우저에서 응용 프로그램이 실행되면 HTTP GET 요청을 실행하여 데이터베이스의 도서 목록을 검색합니다.

    1. 또한 **public** 콘텐츠 폴더 내에서 **index.html**이라는 새 HTML 파일을 만듭니다.

        ```bash
        nano ~/Books/public/index.html
        ```

    1. 이러한 새 파일에 다음 태그를 붙여넣어 웹 응용 프로그램의 HTML 사용자 인터페이스를 설정합니다.

        ```html
        <!doctype html>
        <html ng-app="myApp" ng-controller="myCtrl">
        <head>
            <script src="https://ajax.googleapis.com/ajax/libs/angularjs/1.7.2/angular.min.js"></script>
            <script src="script.js"></script>
        </head>
        <body>
            <div>
            <table>
                <tr>
                <td>Name:</td>
                <td><input type="text" ng-model="Name"></td>
                </tr>
                <tr>
                <td>Isbn:</td>
                <td><input type="text" ng-model="Isbn"></td>
                </tr>
                <tr>
                <td>Author:</td>
                <td><input type="text" ng-model="Author"></td>
                </tr>
                <tr>
                <td>Pages:</td>
                <td><input type="number" ng-model="Pages"></td>
                </tr>
            </table>
            <button ng-click="add_book()">Add</button>
            </div>
            <hr>
            <div>
            <table>
                <tr>
                <th>Name</th>
                <th>Isbn</th>
                <th>Author</th>
                <th>Pages</th>
                </tr>
                <tr ng-repeat="book in books">
                <td><input type="button" value="Delete" data-ng-click="del_book(book)"></td>
                <td>{{book.name}}</td>
                <td>{{book.isbn}}</td>
                <td>{{book.author}}</td>
                <td>{{book.pages}}</td>
                </tr>
            </table>
            </div>
        </body>
        </html>
        ```

        이 코드는 새 도서 데이터를 제출할 필드가 4개인 간단한 HTML 양식 및 데이터베이스에 이미 저장된 모든 도서를 표시할 테이블을 만듭니다. 다양한 `ng-` HTML 특성이 AngularJS 코드를 UI에 연결합니다.

1. 전체 도서 웹 응용 프로그램을 테스트합니다.

    1. 다음 명령으로 Node.js를 사용하는 응용 프로그램을 시작합니다.

        ```bash
        sudo node ~/Books/server.js
        ```

        그러면 응용 프로그램 백 엔드가 시작되고, 포트 80에서 들어오는 HTTP 요청 수신 대기를 시작합니다.

    1. 응용 프로그램 기능을 테스트합니다.

        선호하는 브라우저를 열고 URL로 Azure VM의 공용 IP 주소를 탐색합니다.

        ```bash
        http://<vm-public-ip>
        ```

        모든 사항이 순서대로 있으면 다음과 비슷한 화면이 표시됩니다.

        다음 스크린샷은 MongoDB 데이터베이스에 저장할 도서 세부 정보를 제출하는 사용자 인터페이스를 보여 줍니다.


        ![도서를 추가하는 데이터 입력 양식을 보여 주는 웹 브라우저 스크린샷입니다.](../media-draft/10-book-page.png)

    이제 MongoDB 데이터베이스에 저장할 도서를 제출할 수 있습니다. 데이터베이스에서 로드된 전체 도서 목록도 볼 수 있습니다.