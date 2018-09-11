이 단원에서는 Ubuntu 머신에서 .NET CLI를 사용하여 ASP.NET Core 웹앱을 만듭니다.

## <a name="aspnet-core-installation-on-linux-environment"></a>Linux 환경의 ASP.NET Core 설치

Microsoft [.NET 다운로드 페이지](https://www.microsoft.com/net/download)를 방문하여 .NET Core SDK 페이지에 언급된 것과 동일한 단계를 따릅니다. 단계는 다음과 같습니다. 명령을 실행하려면 새 **터미널** 명령줄 인스턴스를 열어야 합니다.

### <a name="register-microsoft-key-and-feed"></a>Microsoft 키 및 피드 등록

.NET을 설치하기 전에 Microsoft 키를 등록하고, 제품 리포지토리를 등록하고, 필수 종속성을 설치해야 합니다. 머신당 한 번만 수행하면 됩니다.

```console
~$ wget -q https://packages.microsoft.com/config/ubuntu/18.04/packages-microsoft-prod.deb
~$ sudo dpkg -i packages-microsoft-prod.deb
```

## <a name="install-the-net-sdk"></a>.NET SDK 설치

설치할 수 있는 제품을 업데이트한 후 .NET SDK를 설치합니다.

명령 프롬프트에서 다음 명령을 실행합니다.

```console
sudo apt-get install apt-transport-https
sudo apt-get update
sudo apt-get install dotnet-sdk-2.1
```

설치 프로세스 중에 계정 암호를 입력하라는 메시지가 표시될 수 있습니다. 암호를 입력하고 Enter 키를 눌러 계속합니다.

설치를 확인하려면 다음을 입력합니다.

```console
dotnet --version
```

표시되는 출력은 다음과 같습니다.

```console
2.1.302
```

이제 .NET Core SDK가 설치되었으므로 ASP.NET Core도 설치되어 있습니다. .NET CLI를 사용하여 방금 알아본 명령을 통해 새 ASP.NET Core 프로젝트를 만드는 방법을 살펴보겠습니다.

## <a name="open-a-terminal-window"></a>터미널 창 열기

먼저 터미널 창을 열어야 합니다. 터미널 창에서 명령을 실행할 수 있고 이 창은 Windows 명령 프롬프트 창과 유사한 역할을 할 수 있습니다.

## <a name="create-a-new-web-project"></a>새 웹 프로젝트 만들기

.NET CLI 도구의 핵심은 *dotnet* 드라이버 도구입니다. 이 명령을 사용하여 새 ASP.NET Core 웹 프로젝트를 만듭니다.

새 ASP.NET Core MVC 응용 프로그램을 만들려면 다음 명령을 입력하면 됩니다.

```console
cd ~/Documents
mkdir BestBikeApp   # Hit Enter
cd BestBikeApp      # Hit Enter
dotnet new mvc      # Hit Enter
```

위 명령은 *Documents* 루트 폴더로 이동한 후 새 폴더를 만듭니다. 그런 다음 해당 폴더 내로 이동합니다. 마지막으로 .NET CLI 명령을 실행하여 모든 패키지가 복원된 새 ASP.NET MVC 응용 프로그램을 생성합니다.

```console
The template "ASP.NET Core Web App (Model-View-Controller)" was created successfully.
This template contains technologies from parties other than Microsoft, see https://aka.ms/aspnetcore-template-3pn-210 for details.

Processing post-creation actions...
Running 'dotnet restore' on /home/your-user/Documents/BestBikeApp/BestBikeApp.csproj...
...
```

이제 다음 명령을 실행하여 응용 프로그램을 실행하면 됩니다.

```console
dotnet run
```

‘터미널’에서 *dotnet* 명령은 실행 중인 앱에 대한 몇 가지 유용한 정보를 표시합니다.

```console
Using launch settings from /home/your-user/Documents/BestBikeApp/Properties/launchSettings.json...
...
Hosting environment: Development
Content root path: /home/your-user/Documents/BestBikeApp
Now listening on: https://localhost:5001
Now listening on: http://localhost:5000
Application started. Press Ctrl+C to shut down.
```

출력은 앱을 시작한 후에 발생하는 상황을 설명합니다. 응용 프로그램이 실행 중이고 포트 5001 및 5002에서 수신 대기 중입니다(HTTPS 사용).

개발 모드의 머신에서 HTTPS를 로컬로 실행하려면 **자체 서명된 인증서**를 만들고 신뢰해야 합니다.

## <a name="create-a-self-signed-certificate"></a>자체 서명된 인증서 만들기

다음 명령을 실행하여 개발 자체 서명 인증서를 생성합니다.

```console
dotnet dev-certs https -v
```

명령을 실행하면 다음이 반환됩니다.

```console
The HTTPS developer certificate was generated successfully.
```

## <a name="run-the-application"></a>응용 프로그램 실행

이 데모에서는 Firefox 브라우저를 사용하고 있습니다.

브라우저를 열고 주소로 `http://localhost:5001`을 입력하여 응용 프로그램이 정상적으로 실행되고 있는지 확인합니다.

![ASP.NET Core MVC 템플릿 기본 웹 페이지의 웹 브라우저 보기를 보여 주는 스크린샷.](../media/5-asp-core-mvc-default-template.PNG)

> [!NOTE]
> 개발 자체 서명 인증서는 Firefox에서 확인할 수 없으므로 응용 프로그램 URL에 대한 **예외를 추가**해야 합니다.
