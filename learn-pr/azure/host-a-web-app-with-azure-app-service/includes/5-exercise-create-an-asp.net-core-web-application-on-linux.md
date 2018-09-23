이 단원에서는 ASP.NET Core 웹앱을 만듭니다.

## <a name="create-a-new-web-project"></a>새 웹 프로젝트 만들기

.NET CLI 도구의 핵심은 `dotnet` 명령줄 도구입니다. 이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.

오른쪽의 Cloud Shell에서 새 ASP.NET Core MVC 응용 프로그램을 만듭니다. "BestBikeApp"이라는 이름을 지정합니다.

```bash
dotnet new mvc --name BestBikeApp
```

이 명령은 "BestBikeApp"이라는 새 폴더를 만들어서 프로젝트를 보관합니다. 여기서 `cd`는 응용 프로그램을 빌드하고 실행하여 완료되었는지 확인합니다.

```bash
cd BestBikeApp
dotnet run
```

다음과 유사한 결과를 얻습니다.

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

출력은 앱을 시작한 후에 발생하는 상황을 설명합니다. 응용 프로그램이 실행 중이고 포트 5000에서 수신 대기 중입니다.

고유한 머신에서 앱을 실행한 경우 http://localhost:5000에 대해 브라우저를 열 수 없습니다. Azure Cloud Shell에서 작업하므로 공용 엔드포인트를 포함하는 위치에 앱을 배포해야 합니다. 앞에서 만든 App Service 인스턴스가 가장 적합합니다.