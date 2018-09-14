이 단위에 ASP.NET Core 웹 앱을 만들게 됩니다.

## <a name="create-a-new-web-project"></a>새 웹 프로젝트 만들기

.NET CLI 도구의 핵심은는 `dotnet` 명령줄 도구입니다. 이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.

1. 오른쪽에서 Cloud Shell에서 새 ASP.NET Core MVC 응용 프로그램을 만듭니다. "BestBikeApp" 이름을 지정 합니다.

```bash
dotnet new mvc -name BestBikeApp
```

1. 명령은 "BestBikeApp" 라는 새 폴더를 만듭니다. 프로젝트를 보관 하 합니다. 해당 폴더를 변경 합니다.

1. 빌드 및 완료 되었는지 확인 하려면 응용 프로그램을 실행 합니다.

```bash
dotnet run
```

같은 결과 얻게 됩니다.

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Production
Content root path: /home/your-user/BestBikeApp
Now listening on: http://localhost:5000
Application started.
```

출력 앱을 시작한 후 상황에 설명 합니다: 응용 프로그램을 실행 하 고 5000 포트에서 수신 대기 합니다.

브라우저를 열 수 없게 하겠습니다 고유한 컴퓨터에서 앱을 실행 된 경우 http://localhost:5000합니다. 위치에 앱을 배포 해야 하므로 Azure Cloud Shell에서 우리가 공용 끝점을 사용 합니다. 앞에서 만든 App Service 인스턴스를 가장 하는 적합 합니다.