시작하기 전에 Azure CLI 도구의 구문을 검토해 보겠습니다. **Azure CLI를 사용하여 Azure 서비스 제어** 모듈을 사용해봤다면 Azure CLI 명령이 다음과 같은 형식임을 알 수 있을 것입니다.

```azurecli
az [command] [subcommand] [--parameter --parameter]
```

`[command]`는 제어할 Azure의 특정 영역을 식별합니다. 예를 들어 `account` 명령을 사용하여 구독 정보를 관리하거나 `sql` 명령을 사용하여 SQL 데이터베이스를 관리할 수 있습니다. `[subcommand]` 및 `[--parameters]`는 작업 중인 명령에 따라 다릅니다. 

부분 명령을 입력하여 명령, 하위 명령 및 매개 변수의 목록을 볼 수 있습니다. 예를 들어, 명령줄에 `az`를 입력하면 최상위 레벨 도움말 화면이 표시되고, `az vm`을 입력하면 가상 머신에 대한 모든 하위 명령이 표시됩니다. 이 접근법은 Azure CLI 도구를 탐색하는 훌륭한 방법입니다.

> [!NOTE]
> Azure CLI 작업을 위해 브라우저 기반의 Azure Cloud Shell을 사용하려고 합니다. 로컬 머신에서 작업하는 것이 편한 경우, [Azure CLI를 설치](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)하면 여기에서 다루는 모든 명령을 명령줄에서 실행할 수 있습니다. 이 작업에 설명 했습니다 합니다 **Azure CLI를 사용 하 여 컨트롤 Azure services** 모듈입니다.

## <a name="login-to-azure"></a>Azure에 로그인

일반적으로 가장 먼저 Azure CLI를 사용 하 여 작업 하는 경우 작업을 수행 Azure 계정에 로그인 됩니다. 이 작업은 `az login` 명령을 통해 수행됩니다. 이 명령을 실행하면 브라우저 창이 열리며, 여기에서 사용할 Microsoft 계정을 선택할 수 있습니다. 이 단계가 필요 하지 않습니다. Azure 샌드박스를 사용 하 고 있으므로 Azure 샌드박스를 활성화 해야 대신 합니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

## <a name="working-with-subscriptions"></a>구독 작업

이 모듈에서는 임시 구독에서 작업 하지만 사용자 고유의 계정에서 구독을 일반적으로 사용 됩니다. 둘 이상의 구독이 있는 경우 `az account list --output table` 문을 사용하여 명확하게 서식이 지정된 구독 목록을 가져올 수 있습니다.

```
Name                                  CloudName    SubscriptionId                        State    IsDefault
------------------------------------  -----------  ------------------------------------  -------  -----------
Contoso Legacy Resources              AzureCloud   abc13b0c-d2c4-64b2-9ac5-2f4cb819b752  Enabled  True
Visual Studio Enterprise              AzureCloud   233aebce-23c2-4572-c056-c029449e93ed  Enabled  False
```

이 명령은 또한 모든 명령이 적용되는 _기본_ 구독을 식별합니다. 다른 구독으로 작업하려면 `az account set --subscription "[name]"` 명령을 사용할 수 있습니다. 예를 들어 다음 명령을 통해 현재 구독을 위 목록에서 `Visual Studio Enterprise`로 설정할 수 있습니다.

```azurecli
az account set --subscription "Visual Studio Enterprise"
```