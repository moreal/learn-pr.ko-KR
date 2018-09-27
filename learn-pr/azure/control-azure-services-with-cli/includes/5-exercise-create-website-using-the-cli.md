다음으로 Azure CLI를 사용하여 리소스 그룹을 만든 다음, 이 리소스 그룹에 웹앱을 배포해 보겠습니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="using-a-resource-group"></a>리소스 그룹을 사용하기

사용자 고유의 머신 및 Azure 구독에서 작업하는 경우 `az login` 명령을 사용하여 Azure에 처음으로 로그인해야 합니다. 이 로그인은 Cloud Shell 환경에서는 필요하지 않습니다.

다음으로, 보통 `az group create` 명령과 관련된 모든 Azure 리소스에 대해 리소스 그룹을 만들지만 이러한 연습에서는 하나의 리소스 그룹을 생성했습니다. 리소스 그룹에 대해 **<rgn>[샌드박스 리소스 그룹 이름]</rgn>** 을 사용합니다.

1. 테이블에 모든 리소스 그룹을 나열하도록 Azure CLI에 요청할 수 있습니다. 무료 Azure 샌드박스를 사용하는 동안 하나의 리소스 그룹이 있어야 합니다.

    ```azurecli
    az group list --output table
    ```

    [!include[](../../../includes/azure-cloudshell-copy-paste-tip.md)]

1. Azure 개발과 마찬가지로 여러 리소스 그룹이 생성될 수 있습니다. 그룹 목록에 여러 항목이 있는 경우 `--query` 옵션을 추가하여 반환 값을 필터링할 수 있습니다. 다음 명령을 사용하세요.

    ```azurecli
    az group list --query "[?name == '<rgn>[sandbox resource group name]</rgn>']"
    ```

    쿼리는 JSON 요청에 대한 표준 쿼리 언어인 **JMESPath**를 사용하여 형식이 지정됩니다. 이 강력한 필터 언어에 대한 자세한 내용은 <http://jmespath.org/>를 참조하세요. 또한 **Azure CLI를 사용하여 VM 관리** 모듈에서 쿼리를 더 자세히 다룹니다.

### <a name="steps-to-create-a-service-plan"></a>서비스 계획을 만드는 단계

Azure App Service를 사용하여 Web Apps를 실행하는 경우 앱에서 사용하는 Azure 계산 리소스에 대한 요금이 청구되며, Web Apps와 연결된 App Service 계획에 따라 달라집니다. 서비스 계획은 앱 데이터 센터에 사용되는 지역, 사용되는 VM 수 및 가격 책정 계층을 결정합니다.

1. 앱을 실행할 App Service 계획을 만듭니다. 다음 명령은 가격 책정 계층 또는 VM 인스턴스 세부 정보를 지정하지 않으므로, 기본적으로 **작은** VM 인스턴스 1개가 포함된 **기본** 플랜이 제공됩니다.

    > [!WARNING]
    > 앱 이름과 계획은 _고유_해야 하므로 이름에 접미사를 추가하고 아래 명령에서 `<unique>` 텍스트를 숫자 집합, 이니셜 또는 기타 텍스트 조각으로 바꾸어 모든 Azure에서 고유한지 확인합니다.

    `--location` 매개 변수의 경우 아래 위치 값 중 하나를 사용합니다.

    [!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

    ```azurecli
    az appservice plan create --name popupappplan-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --location <location>
    ```

    이 명령을 완료하는 데 몇 분 정도 걸릴 수 있습니다.

1. 모든 계획을 표에 나열하여 서비스 계획이 성공적으로 생성되었는지 확인합니다.

    ```azurecli
    az appservice plan list --output table
    ```

### <a name="steps-to-create-a-web-app"></a>웹앱을 만드는 단계

이제 서비스 계획에 웹앱을 만들겠습니다. 동시에 코드를 배포할 수 있지만, 예제에서는 별도의 단계로 배포합니다.

1. 웹앱을 만들고 위에서 만든 계획의 이름을 제공합니다. **계획과 마찬가지로 앱 이름은 고유해야 하므로** 일부 텍스트로 `<unique>` 표식을 바꾸어 글로벌로 고유한 이름을 지정합니다.

    ```azurecli
    az webapp create --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --plan popupappplan-<unique>
    ```

1. 모든 앱을 표에 나열하여 앱이 성공적으로 생성되었는지 확인합니다.

    ```azurecli
    az webapp list --output table
    ```

1. 테이블에 나열된 **DefaultHostName**을 기록합니다. 이는 새 웹 사이트에 연결할 수 있는 웹 주소입니다. Azure는 `azurewebsites.net` 도메인에서 고유한 앱 이름을 통해 웹 사이트를 사용할 수 있게 합니다. 예를 들어 앱 이름이 “popupapp-mslearn123”인 경우 웹 사이트 URL은 `http://popupwebapp-mslearn123.azurewebsites.net`입니다.

1. 사이트에는 브라우저에서 또는 CURL을 통해 확인할 수 있는 Azure에서 생성한 "빠른 시작" 페이지가 있으므로 **DefaultHostName**을 사용합니다.

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
### <a name="steps-to-deploy-code-from-github"></a>GitHub에서 코드를 배포하는 단계

1. 최종 단계는 GitHub 리포지토리에서 웹앱으로 코드를 배포하는 것입니다. 실행 시 “HelloWorld!”를 표시하는 Azure 샘플 Github 리포지토리에서 사용 가능한 간단한 PHP 페이지를 사용하겠습니다. 직접 만든 웹앱 이름을 사용해야 합니다.

    ```azurecli
    az webapp deployment source config --name popupwebapp-<unique> --resource-group <rgn>[sandbox resource group name]</rgn> --repo-url "https://github.com/Azure-Samples/php-docs-hello-world" --branch master --manual-integration
    ```

1. 배포되면 브라우저 또는 CURL을 사용하여 사이트를 다시 방문합니다.

    ```bash
    curl popupwebapp-<unique>.azurewebsites.net
    ```
    
    페이지에 "Hello World!"가 표시됩니다.

    ```output
    Hello World!
    ```

이 연습에서는 대화형 Azure CLI 세션의 일반적인 패턴을 살펴보았습니다. 먼저 표준 명령을 사용하여 새 리소스 그룹을 만들었습니다. 그런 다음, 명령 집합을 사용하여 이 리소스 그룹에 리소스(이 예제에서는 웹앱)를 배포했습니다. 이 명령 집합을 셸 스크립트에 쉽게 결합하여, 동일한 리소스를 만들어야 할 때마다 실행할 수 있습니다.