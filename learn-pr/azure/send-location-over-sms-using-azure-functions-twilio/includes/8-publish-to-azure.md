이제 앱과 Azure Function이 완료되어 로컬에서 실행되고 있습니다. 이 단원에서는 함수를 Azure에 게시하여 클라우드에서 실행합니다.

> [!Note]
> Visual Studio에서 함수를 게시합니다. 이는 개념 증명, 프로토타입 및 학습용으로 시작하는 데 유용한 방법이지만, 프로덕션 품질 앱의 경우 이 방법을 사용하면 **안 됩니다**. CI 기반 배포 형식을 사용해야 합니다. [Azure Functions 배포 문서](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment?azure-portal=true)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다.

## <a name="publishing-your-app-to-azure"></a>Azure에 앱 게시

Visual Studio 내부에서 Azure에 Azure 함수를 게시할 수 있습니다.

1. 이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.

1. 솔루션 탐색기에서 `ImHere.Functions` 앱을 마우스 오른쪽 단추로 클릭하고 *게시...* 를 선택합니다.

    ![Functions 앱에서 마우스 오른쪽 단추를 클릭하여 게시](../media/8-right-click-publish.png)

1. **게시 대상 선택** 대화 상자에서 ‘Azure 함수 앱’을 선택하고 **Azure App Service**에 대해 *새로 만들기*를 선택합니다. **게시**를 클릭합니다.

    ![게시할 새 Azure App Service 만들기](../media/8-pick-publish-target.png)

1. 이러한 지침의 **리소스** 탭에서 사용자 이름 및 암호를 사용하여 Azure에 로그인합니다. VM을 사용하는 대신 로컬로 이 앱을 빌드하는 경우 Azure 계정으로 로그인하고, 대화 상자에서 링크를 사용하는 데 필요한 경우 새 계정을 만듭니다.

1. Functions 앱을 실행하는 데 필요한 모든 인프라를 만들므로 모든 값을 기본값으로 내버려 둡니다.

1. **만들기**를 클릭하여 Azure에 모든 리소스를 프로비전하고 Azure Functions 앱을 게시합니다.

    ![App Service 만들기](../media/8-create-app-service.png)

1. Azure에서 함수 버전을 업데이트하려는지를 묻는 메시지가 표시될 수 있습니다. 이 대화 상자가 나타나면 **예**를 선택하여 함수 앱이 최신 Azure Functions 런타임 버전을 사용하여 게시됐는지 확인합니다.
    ![Azure Functions 업데이트 대화 상자](../media/8-update-functions-on-azure.png)

프로비저닝을 완료하는 데 몇 분 정도 걸립니다. 다음 리소스가 프로비전됩니다.

- Azure Functions 앱에 필요한 파일을 저장할 저장소 계정
- Azure Functions 앱에 필요한 계산 리소스를 관리할 App Service 계획
- Azure 함수를 실행하는 App Service

이제 함수가 게시되어 **https://\<your-app-name\>.azurewebsites.net/api/SendLocation**에서 호출할 수 있습니다.

## <a name="configuring-your-app"></a>앱 구성

Azure 함수가 로컬에서 실행되었을 때는 `local.settings.json` 파일에 저장된 Twilio 자격 증명을 사용하고 있었습니다. 이름에서 알 수 있듯이, 이 파일은 Azure 설정이 아닌 로컬 설정에 사용됩니다. Azure 내부에서 Azure 함수를 호출하려면 먼저 `TwilioAccountSid` 및 `TwilioAuthToken` 설정을 구성해야 합니다.

1. 게시 탭에서 **응용 프로그램 설정 관리** 옵션을 클릭합니다.

    ![응용 프로그램 설정 관리 옵션](../media/8-application-settings-option.png)

1. **응용 프로그램 설정** 대화 상자에는 로컬 및 원격 값 모두를 포함한 응용 프로그램 설정이 표시됩니다. 로컬 값은 `local.settings.json` 파일에서 제공되며 원격 값은 Azure에서 호스팅될 때 사용자 함수가 사용할 값입니다. **TwilioAccountSid** 및 **TwilioAuthToken** 값의 경우 *로컬*에서 *원격* 상자로 값을 복사합니다.

    ![응용 프로그램 설정에서 Twilio 자격 증명 설정](../media/8-set-creds-in-app-settings.png)

1. **확인**을 클릭합니다. 그러면 Azure 함수 앱에 값이 게시됩니다.

## <a name="pointing-the-mobile-app-to-azure"></a>모바일 앱에서 Azure 가리키기

1. 게시 탭에서 값 옆에 있는 **클립보드로 복사** 단추를 사용하여 **사이트 URL**을 복사합니다.

    ![게시 탭에서 사이트 URL 복사](../media/8-copy-site-url.png)

1. `ImHere` 프로젝트에서 `MainViewModel`을 엽니다.

1. `baseUrl` 필드의 값이 게시 탭에서 복사한 사이트 URL이 되도록 업데이트합니다.

## <a name="test-it-out"></a>테스트

1. `ImHere.UWP` 앱을 시작 앱으로 설정하고 실행합니다.

1. 전화 번호를 입력하고 **위치 보내기** 단추를 클릭합니다.

1. 위치가 SMS 메시지로 수신되어야 합니다.

1. *사용할 수 없는 서비스* 오류가 다시 발생하면 함수 앱에서 사용 중인 "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet 패키지의 버전을 확인합니다. 해당 버전은 3.0.0이 아니라 3.0.0-rc1이어야 합니다.
1. *사용할 수 없는 서비스* 오류가 다시 발생하면 함수 앱에서 사용 중인 "Microsoft.Azure.WebJobs.Extensions.Twilio" NuGet 패키지의 버전을 확인합니다. 해당 버전은 3.0.0이 **아니라** 3.0.0-rc1이어야 합니다.

## <a name="summary"></a>요약

이 단원에서는 Visual Studio 내부에서 Azure에 Azure Functions 프로젝트를 게시하고 응용 프로그램 설정을 구성하는 방법을 배웠습니다.