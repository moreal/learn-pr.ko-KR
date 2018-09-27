<span data-ttu-id="58a46-101">이 단원에서는 Node.js에 호스트된 간단한 AngularJS 응용 프로그램을 만들고 경로 지정을 위해 Express를 사용하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-101">In this unit, you're going to create a simple AngularJS application hosted in Node.js and use Express for routing.</span></span> <span data-ttu-id="58a46-102">백 엔드에서는 MongoDB가 데이터 저장소로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-102">On the back end, MongoDB will serve as your data store.</span></span> <span data-ttu-id="58a46-103">이 응용 프로그램은 도서를 나열하고, 추가하고, 삭제할 수 있는 도서 데이터베이스입니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-103">The application is a book database, where you will be able to list, add, and delete books.</span></span>

> [!Important]
> <span data-ttu-id="58a46-104">간단한 응용 프로그램이며,</span><span class="sxs-lookup"><span data-stu-id="58a46-104">This is a simple application.</span></span> <span data-ttu-id="58a46-105">새로 설치된 MEAN 스택을 테스트하기 위한 목적으로 설계되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-105">Its purpose is to test the newly installed MEAN stack.</span></span> <span data-ttu-id="58a46-106">이 응용 프로그램은 프로덕션에 사용하기에는 보안이나 준비가 충분하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-106">This application is not sufficiently secure or ready for production use.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="58a46-107">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="58a46-107">Create the application</span></span>

<span data-ttu-id="58a46-108">먼저, 응용 프로그램에 사용할 코드, 스크립트 및 HTML 파일을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-108">First, we're going to create the code, script and HTML files for our application.</span></span> <span data-ttu-id="58a46-109">Cloud Shell 편집기에서 이 작업을 수행한 다음, VM에 파일을 복사하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-109">We'll do this in the Cloud Shell editor then copy the files to the VM.</span></span>

1. <span data-ttu-id="58a46-110">Cloud Shell에서 여전히 VM에 SSH된 경우 `exit` 명령을 사용하여 Cloud Shell 파일 시스템으로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-110">In Cloud Shell, if you are still SSHed into your VM, use `exit` to return to the Cloud Shell filesystem.</span></span>

    ```bash
    exit
    ```

1. <span data-ttu-id="58a46-111">응용 프로그램에 사용할 폴더 및 파일을 만들고 Cloud Shell 편집기에서 엽니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-111">Create the folders and files for your application and open them in the Cloud Shell editor.</span></span>

    ```bash
    cd ~
    mkdir Books
    mkdir Books/app
    mkdir Books/public
    touch Books/app/model.js
    touch Books/app/routes.js
    touch Books/server.js
    touch Books/public/script.js
    touch Books/public/index.html
    code Books
    ```

    <span data-ttu-id="58a46-112">그러면 프로젝트의 앱 및 해당 종속성을 포함하는 "Books"라는 폴더가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-112">This creates a folder called "Books" to contain your project's app and its dependencies.</span></span> <span data-ttu-id="58a46-113">해당 폴더에서 모든 응용 프로그램 리소스와 스크립트가 포함되는 "app" 폴더를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-113">Within that folder, you created an "app" folder to contain all your application resources and scripts.</span></span> <span data-ttu-id="58a46-114">마지막으로 적절한 HTTP 요청에 직접 제공될 클라이언트 쪽 파일이 모두 포함되는 "public" 폴더도 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-114">Finally, we will also create a "public" folder to hold all of the client-side files that will be served up directly to appropriate HTTP requests.</span></span>

## <a name="create-the-application"></a><span data-ttu-id="58a46-115">응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="58a46-115">Create the application</span></span>

1. <span data-ttu-id="58a46-116">Mongoose 데이터 모델을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-116">Create the Mongoose data model.</span></span> <span data-ttu-id="58a46-117">편집기에서 `app/model.js` 파일을 열고 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-117">In the editor, open `app/model.js` and paste in the following code.</span></span>

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

    > [!IMPORTANT]
    > <span data-ttu-id="58a46-118">편집기에서 파일에 코드를 붙여넣거나 코드를 변경할 때마다 "..." 메뉴 또는 바로 가기 키(Windows 및 Linux는 <kbd>Ctrl+S</kbd>, macOS는 <kbd>Cmd+S</kbd>)를 사용하여 저장하세요.</span><span class="sxs-lookup"><span data-stu-id="58a46-118">Whenever you paste or change code into a file in the editor, make sure to save afterwards using the "..." menu, or the accelerator key (<kbd>Ctrl+S</kbd> on Windows and Linux, <kbd>Cmd+S</kbd> on macOS).</span></span>

    <span data-ttu-id="58a46-119">이 코드는 로컬 VM의 MongoDB 서버에 있는 "Books"라는 데이터베이스에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-119">This code is connecting to a database called "Books" on the local VM's MongoDB server.</span></span> <span data-ttu-id="58a46-120">그런 다음, `bookSchema` 변수로 정의된 스키마를 사용하여 "Books"라는 데이터베이스 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-120">It then creates a database document called "Book" with the schema defined by the `bookSchema` variable.</span></span>

2. <span data-ttu-id="58a46-121">HTTP 요청을 처리할 Express 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-121">Create the Express routes that will handle HTTP requests.</span></span> <span data-ttu-id="58a46-122">편집기에서 `app/routes.js` 파일을 열고 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-122">Open `app/routes.js` in the editor and paste in the following code.</span></span>

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

    <span data-ttu-id="58a46-123">이 코드는 본 응용 프로그램에 대해 4개의 경로를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-123">This code will create four routes for our application.</span></span> <span data-ttu-id="58a46-124">처음 세 개 경로는 사용자가 API GET, POST 또는 DELETE 요청을 `/book` 리소스로 보내는 경우 수행할 작업을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-124">The first three specify what to do when someone sends an API GET, POST, or DELETE request to the `/book` resource.</span></span> <span data-ttu-id="58a46-125">마지막 한 개 경로는 요청자를 인덱스 페이지로 보내는 catch-all 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-125">The last one is a catch-all route to send the requester to the index page.</span></span>

    <span data-ttu-id="58a46-126">Express는 경로 처리 코드에 직접 HTTP 응답을 제공하거나 파일의 정적 콘텐츠를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-126">Express can serve up HTTP responses directly in the route handling code, or it can serve up static content from files.</span></span> <span data-ttu-id="58a46-127">이 샘플 웹 응용 프로그램에서 둘 다 수행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-127">We are doing both in this sample web application.</span></span> <span data-ttu-id="58a46-128">API 요청에 대한 JSON 데이터 및 index.html 파일에서 직접 HTML 데이터를 사용하여 응답합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-128">We respond with JSON data for book API requests and with HTML data direct from the index.html file.</span></span>

3. <span data-ttu-id="58a46-129">응용 프로그램을 호스트할 Express 서버를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-129">Create the Express server to host the application.</span></span> <span data-ttu-id="58a46-130">편집기에서 `server.js` 파일을 열고 다음 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-130">Open `server.js` in the editor and paste in the following code:</span></span>

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

    <span data-ttu-id="58a46-131">이 코드는 웹 응용 프로그램 자체를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-131">This code creates the web application itself.</span></span> <span data-ttu-id="58a46-132">이름이 **public**인 폴더(다음에 만듦)의 정적 파일을 사용하며 이전 단계에서 정의된 경로를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-132">It will serve static files from a folder named **public** (created next) and will use the routes defined in the previous step.</span></span>

4. <span data-ttu-id="58a46-133">클라이언트 쪽 JavaScript 응용 프로그램을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-133">Create the client-side JavaScript application.</span></span> <span data-ttu-id="58a46-134">편집기에서 `public/script.js` 파일을 열고 이 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-134">Open `public/script.js` in the editor and paste in this code:</span></span>

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

    <span data-ttu-id="58a46-135">이 클라이언트 쪽 AngularJS 코드는 `myCtrl`이라는 하나의 컨트롤러를 포함하는 새 Angular 응용 프로그램 `myApp`을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-135">This client-side AngularJS code creates a new angular application `myApp` containing one controller `myCtrl`.</span></span> <span data-ttu-id="58a46-136">뷰어 브라우저에서 응용 프로그램이 실행되면 HTTP GET 요청을 실행하여 데이터베이스의 도서 목록을 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-136">When the application is run in the viewer's browser, it will issue an HTTP GET request to retrieve the list of books in the database.</span></span>

5. <span data-ttu-id="58a46-137">앱용 사용자 인터페이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-137">Create the user interface for the app.</span></span> <span data-ttu-id="58a46-138">편집기에서 `public/index.html` 파일을 열고 이 코드를 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-138">Open `public/index.html` in the editor and paste in this code:</span></span>

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

    <span data-ttu-id="58a46-139">이 코드는 새 도서 데이터를 제출할 필드가 4개인 간단한 HTML 양식과 데이터베이스에 이미 저장된 모든 도서를 표시할 테이블을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-139">This code will create a simple HTML form with four fields to submit new book data and a table to display all the books already stored in the database.</span></span> <span data-ttu-id="58a46-140">다양한 `ng-` HTML 특성이 AngularJS 코드를 UI에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-140">The various `ng-` HTML attributes will wire up the AngularJS code to the UI.</span></span>

6. <span data-ttu-id="58a46-141">파일 편집이 완료되었습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-141">We're done editing files.</span></span> <span data-ttu-id="58a46-142">모든 파일을 저장하고, 다음 명령을 실행하여 VM에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-142">Make sure you have saved all of them, then run the following command to copy them to the VM.</span></span> <span data-ttu-id="58a46-143">메시지가 표시되면 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-143">Enter your password when prompted.</span></span>

    ```bash
    scp -r ~/Books <vm-admin-username>@<vm-public-ip>:~/Books
    ```

## <a name="install-node-packages"></a><span data-ttu-id="58a46-144">Node 패키지 설치</span><span class="sxs-lookup"><span data-stu-id="58a46-144">Install Node packages</span></span>

1. <span data-ttu-id="58a46-145">VM으로 다시 SSH 합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-145">SSH back into your VM.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. <span data-ttu-id="58a46-146">디렉터리를 `Books` 디렉터리로 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-146">Change directories to the `Books` directory.</span></span>

    ```bash
    cd ~/Books
    ```

1. <span data-ttu-id="58a46-147">**Express**를 설치하여 HTTP 요청 라우팅을 처리하고 웹 응용 프로그램 사용자에게 반환할 콘텐츠를 결정합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-147">Install **Express** to handle routing of your HTTP requests, to decide what content to return to a user of your web application.</span></span>

    <span data-ttu-id="58a46-148">다음 명령을 실행하여, 사용할 웹 응용 프로그램 패키지로 Express를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-148">Run the following command to add Express as a package for your web application to use.</span></span>

    ```bash
    npm install express
    ```

1. <span data-ttu-id="58a46-149">**Mongoose**를 설치하여 MongoDB와 HTTP 요청 경로 지정 간에 도서데이터를 릴레이하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-149">Install **Mongoose** to help relay your book data between MongoDB and the HTTP request routing.</span></span>

    <span data-ttu-id="58a46-150">도서 정보는 REST API 요청을 통해 쿼리됩니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-150">The book information will be queried via REST API requests.</span></span> <span data-ttu-id="58a46-151">MongoDB와 API 사이의 데이터 전송을 간소화하려면 Mongoose를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-151">To simplify the transfer of data in and out of MongoDB to our API, we will use Mongoose.</span></span> <span data-ttu-id="58a46-152">Mongoose는 데이터를 모델링하기 위한 스키마 기반 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-152">Mongoose is a schema-based system for modeling data.</span></span> <span data-ttu-id="58a46-153">여기서는 다양한 GET, POST 및 DELETE HTTP 요청에서 데이터 모델이 일관성을 유지하도록 샘플 응용 프로그램에서 Mongoose를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-153">We will be using it in our sample application to keep our data models consistent through the various GET, POST, and DELETE HTTP requests.</span></span>

    <span data-ttu-id="58a46-154">다음 명령을 실행하여, 사용할 웹 응용 프로그램 패키지로 Mongoose를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-154">Run the following command to add Mongoose as a package for your web application to use.</span></span>

      ```bash
      npm install mongoose
      ```

1. <span data-ttu-id="58a46-155">**body-parser**를 설치하여 Express 경로 지정에 사용할 JSON 요청 데이터를 사전 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-155">Install **body-parser** to pre-process JSON request data for use in our Express routing.</span></span>

    <span data-ttu-id="58a46-156">백 엔드에서는 `body-parser`가 들어오는 JSON 요청 데이터를 구문 분석하기 위한 Node.js 및 Express 간 미들웨어 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-156">On the back end, `body-parser` will serve as a middleware between Node.js and Express for parsing incoming JSON request data.</span></span>

    <span data-ttu-id="58a46-157">다음 명령을 실행하여 `body-parser`를 사용할 웹 응용 프로그램 패키지로 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-157">Run the following command to add `body-parser` as a package for your web application to use.</span></span>

      ```bash
      npm install body-parser
      ```

    > [!TIP]
    > <span data-ttu-id="58a46-158">여러 npm 패키지를 설치하는 경우 다음과 같은 단일 명령에 모두 포함할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-158">When installing multiple npm packages, you can include them all in a single command such as this:</span></span>
    >
    > ```bash
    > npm install express mongoose body-parser
    > ```

## <a name="test-the-application"></a><span data-ttu-id="58a46-159">응용 프로그램 테스트</span><span class="sxs-lookup"><span data-stu-id="58a46-159">Test the application</span></span>

1. <span data-ttu-id="58a46-160">다음 명령으로 Node.js를 사용하는 응용 프로그램을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-160">Start the application with Node.js with the following command.</span></span>

    ```bash
    sudo node server.js
    ```

    <span data-ttu-id="58a46-161">그러면 응용 프로그램 백 엔드가 시작되고, 포트 80에서 들어오는 HTTP 요청 수신 대기를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-161">This will start the back end of our application, which will then start listening on port 80 for incoming HTTP requests.</span></span>

1. <span data-ttu-id="58a46-162">응용 프로그램 기능을 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-162">Test the application functionality.</span></span>

    <span data-ttu-id="58a46-163">선호하는 브라우저를 열고 URL([http://X.X.X.X](http://X.X.X.X))로 Azure VM의 공용 IP 주소를 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-163">Open your preferred browser, and navigate to the public IP address of your Azure VM as the URL ([http://X.X.X.X](http://X.X.X.X)).</span></span>

    <span data-ttu-id="58a46-164">모든 사항이 순서대로 있으면 다음과 유사한 화면이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-164">If everything is in order, you should see a screen similar to this:</span></span>

    <span data-ttu-id="58a46-165">다음 스크린샷은 MongoDB 데이터베이스에 저장할 도서 세부 정보를 제출하는 사용자 인터페이스를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-165">The following screenshot displays the user interface to submit book details for storage in the MongoDB database.</span></span>

    ![도서를 추가하는 데이터 입력 양식을 보여 주는 웹 브라우저 스크린샷입니다.](../media/10-book-page.png)

    <span data-ttu-id="58a46-167">이제 MongoDB 데이터베이스에 저장할 도서를 제출할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-167">You should now be able to submit books to save to the MongoDB database.</span></span> <span data-ttu-id="58a46-168">데이터베이스에서 로드된 전체 도서 목록도 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58a46-168">As well, you can see the full list of books loaded from the database.</span></span>