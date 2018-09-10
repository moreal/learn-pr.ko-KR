이제 앱과 Azure Function이 완료되어 로컬에서 실행되고 있습니다. 이 단원에서는 함수를 Azure에 게시하여 클라우드에서 실행합니다.

> 이 단원에서는 Visual Studio에서 함수를 게시합니다. 이는 개념 증명, 프로토타입 및 학습용으로 시작하는 데 유용한 방법이지만, 프로덕션 품질 앱의 경우 이 방법을 사용하면 **안 됩니다**. CI 기반 배포 형식을 사용해야 합니다. [Azure Functions 배포 문서](https://docs.microsoft.com/azure/azure-functions/functions-continuous-deployment)에서 이 작업을 수행하는 방법을 자세히 알아볼 수 있습니다.
>

## <a name="publishing-your-app-to-azure"></a>Azure에 앱 게시

Visual Studio 내부에서 Azure에 Azure 함수를 게시할 수 있습니다.

1. 이전 단원에서 로컬 Azure Functions 런타임이 계속 실행 중인 경우 해당 런타임을 중지합니다.

1. 솔루션 탐색기에서 `ImHere.Functions` 앱을 마우스 오른쪽 단추로 클릭하고 *게시...* 를 선택합니다.

    ![Functions 앱에서 마우스 오른쪽 단추를 클릭하여 게시](../media-drafts/8-right-click-publish.png)

1. **게시 대상 선택** 대화 상자에서 ‘Azure 함수 앱’을 선택하고 **Azure App Service**에 대해 *새로 만들기*를 선택합니다. **게시**를 클릭합니다.

    ![게시할 새 Azure App Service 만들기](../media-drafts/8-pick-publish-target.png)

1. Azure 계정이 두 개 이상 있고 올바른 계정이 선택되지 않은 경우 오른쪽 위 모서리에 있는 드롭다운에서 Azure 계정을 선택합니다.

1. Functions 앱에 이름을 지정합니다. 이 이름은 Azure의 모든 Functions 앱에서 전체적으로 고유해야 하므로 “ImHere-\<YourName\>”과 같은 이름을 사용합니다.

1. 이 Functions 앱을 만드는 데 사용할 구독을 선택합니다.

1. **리소스 그룹** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하고 “ImHere”와 같은 이름을 지정하여 이 Functions 앱에 대한 새 리소스 그룹을 만듭니다. 리소스 그룹 이름은 Azure 전체에서 고유할 필요는 없지만 구독에서 고유해야 합니다. 그런 다음 **확인**을 클릭합니다.

    ![새 리소스 그룹 만들기](../media-drafts/8-create-new-resource-group.png)

   새 리소스 그룹을 만들면 나중에 쉽게 정리할 수 있습니다. 리소스 그룹을 삭제하면 이 Functions 앱에 대해 만든 모든 항목이 동시에 삭제됨을 알 수 있습니다.

1. **호스팅 플랜** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하여 새 호스팅 플랜을 만듭니다. App Service 계획 이름은 기본적으로 앱 이름의 끝에 “Plan”을 추가하여 지정됩니다. **위치**를 가장 가까운 위치로 설정하고 **크기**가 사용량에 맞게 설정되었는지 확인합니다. 그런 다음 **확인**을 클릭합니다.

    ![호스팅 플랜 구성](../media-drafts/8-configure-hosting-plan.png)

1. **저장소 계정** 드롭다운 옆에 있는 **새로 만들기...** 단추를 클릭하여 새 저장소 계정을 만듭니다. 기본 이름이 제공되므로 모든 기본값을 유지하고 **확인**을 클릭합니다.

    ![저장소 계정 만들기](../media-drafts/8-create-storage-account.png)

1. **만들기**를 클릭하여 Azure에 모든 리소스를 프로비전하고 Azure Functions 앱을 게시합니다.

    ![App Service 만들기](../media-drafts/8-create-app-service.png)

프로비저닝을 실행하는 데 몇 분 정도 걸립니다. 다음 리소스가 프로비전됩니다.

- Azure Functions 앱에 필요한 파일을 저장할 저장소 계정
- Azure Functions 앱에 필요한 계산 리소스를 관리할 App Service 계획
- Azure 함수를 실행하는 App Service

이제 함수가 게시되어 https://<your-app-name>.azurewebsites.net/api/SendLocation에서 호출할 수 있습니다.

## <a name="configuring-your-app"></a>앱 구성

Azure 함수가 로컬에서 실행되었을 때는 `local.settings.json` 파일에 저장된 Twilio 자격 증명을 사용하고 있었습니다. 이름에서 알 수 있듯이, 이 파일은 Azure 설정이 아닌 로컬 설정에 사용됩니다. Azure 내부에서 Azure 함수를 호출하려면 먼저 `TwilioAccountSid` 및 `TwilioAuthToken` 설정을 구성해야 합니다.

1. 게시 탭에서 **응용 프로그램 설정 관리** 옵션을 클릭합니다.

    ![응용 프로그램 설정 관리 옵션](../media-drafts/8-application-settings-option.png)

1. **추가** 단추를 클릭하여 새 설정을 추가합니다. 이름을 “TwilioAccountSid”로 지정하고 값을 Twilio 계정 SID로 설정합니다. “TwilioAuthToken” 이름을 사용하여 인증 토큰에 대해 이 단계를 반복합니다.

    ![응용 프로그램 설정에서 Twilio 자격 증명 설정](../media-drafts/8-set-creds-in-app-settings.png)

1. **확인**을 클릭합니다.

1. **게시**를 클릭하여 새 응용 프로그램 설정으로 Azure Functions 앱을 다시 게시합니다.

    ![게시 단추](../media-drafts/8-publish-application-button.png)

## <a name="pointing-the-mobile-app-to-azure"></a>모바일 앱에서 Azure 가리키기

1. 게시 탭에서 값 옆에 있는 복사 단추를 사용하여 **사이트 URL**을 복사합니다.

    ![게시 탭에서 사이트 URL 복사](../media-drafts/8-copy-site-url.png)

1. `ImHere` 프로젝트에서 `MainViewModel`을 엽니다.

1. `baseUrl` 필드의 값을 게시 탭에서 복사한 사이트 URL로 업데이트합니다.

1. 이 값의 프로토콜을 `http`에서 `https`로 변경합니다. 사이트 URL은 항상 HTTP를 사용하여 제공되지만, Azure 함수를 호출하려면 HTTPS를 사용해야 합니다.

## <a name="test-it-out"></a>테스트

1. `ImHere.UWP` 앱을 시작 앱으로 설정하고 실행합니다.

1. 전화 번호를 입력하고 **위치 보내기** 단추를 클릭합니다.

1. 위치가 SMS 메시지로 수신됩니다.

## <a name="summary"></a>요약

이 단원에서는 Visual Studio 내부에서 Azure에 Azure Functions 프로젝트를 게시하고 응용 프로그램 설정을 구성하는 방법을 배웠습니다.