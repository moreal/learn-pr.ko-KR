
이 연습에서는 로컬 머신의 Azure CLI를 사용하여 리소스 그룹을 만든 다음, 이 리소스 그룹에 웹앱을 배포합니다. 

### <a name="steps-to-create-a-resource-group"></a>리소스 그룹을 만드는 단계
1. Linux 또는 macOS에서 bash 셸을 열거나, Windows에서 작업하는 경우 명령 프롬프트 창 또는 PowerShell을 엽니다.

1. Azure CLI를 시작하고 로그인 명령을 실행합니다.

    ```bash
    az login
    ```
    웹 브라우저에 Azure 로그인 페이지가 표시되지 않는 경우 명령줄 지침을 따르고 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.

1. 리소스 그룹을 만듭니다.

    ```bash
    az group create --location westeurope --name popupResGroup
    ```

1. 모든 리소스 그룹을 표에 나열하여 리소스 그룹이 성공적으로 생성되었는지 확인합니다.

    ```bash
    az group list --output table
    ```
1. 필요에 따라 Azure Portal에서 리소스가 생성되었는지 확인합니다. 웹 브라우저를 열고 포털에 로그인한 다음, **리소스 그룹** 섹션으로 이동합니다(아래 참조). 새 리소스 그룹이 목록에 표시되어야 합니다.

![포털을 사용하여 리소스 그룹 나열](../media-drafts/5-listing-resource-groups.png)

### <a name="steps-to-create-a-service-plan"></a>서비스 계획을 만드는 단계
Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다. 서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.

1. 앱을 실행할 App Service 계획을 만듭니다. 앱 및 플랜의 이름은 고유해야 하므로 문자열 “12345”를 임의 숫자로 변경합니다. 다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.

    ```bash
    az appservice plan create --name popupapp12345 --resource-group popupResGroup --location westeurope
    ```

1. 모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.

    ```bash
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>웹앱을 만드는 단계
이제 서비스 계획에 웹앱을 만들겠습니다. 동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.

1. 문자열 “12345”를 이전에 사용한 것과 동일한 임의 번호로 변경하여 웹앱을 만듭니다.
    ```bash
    az webapp create --name popupapp12345 --resource-group popupResGroup --plan popupapp12345
    ```

1. 모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.

    ```bash
    az webapp list --output table
    ```

1. **DefaultHostName**을 적어 둡니다. 나중에 이 이름이 필요합니다.

### <a name="steps-to-deploy-code-from-github"></a>GitHub에서 코드를 배포하는 단계
1. 최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다. 이번에도 문자열 “12345”를 이전에 사용한 것과 동일한 임의 번호로 변경해야 합니다.
    ```bash
    az webapp deployment source config --name popupapp12345 --resource-group popupResGroup --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. 브라우저에 다음 URL을 복사하여 웹앱을 확인합니다.
http://popupapp12345.azurewebsites.net

1. 페이지에 “HelloWorld”가 표시됩니다.

1. 브라우저 창을 닫습니다.

## <a name="summary"></a>요약
이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다. 먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다. 그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다. 이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.
