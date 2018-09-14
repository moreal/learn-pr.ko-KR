Azure CLI를 사용하면 명령줄에서 명령을 입력하고 바로 실행할 수 있습니다. 소프트웨어 개발 예제의 전반적인 목표는 테스트할 새로운 웹앱 빌드를 배포하는 것임을 잊지 마세요. Azure CLI로 수행할 수 있는 작업 종류에 대해 알아보겠습니다.

## <a name="what-azure-resources-can-be-managed-using-the-azure-cli"></a>Azure CLI를 사용하여 관리할 수 있는 Azure 리소스는 무엇인가요?

Azure CLI를 사용하면 모든 Azure 리소스의 거의 모든 측면을 제어할 수 있습니다. 리소스 그룹, 저장소, 가상 머신, Azure AD(Azure Active Directory), 컨테이너, 기계 학습 등을 사용할 수 있습니다.

CLI의 명령은 _그룹_ 및 _하위 그룹_으로 구조화됩니다. 각 그룹은 Azure에서 제공되는 서비스를 나타내며, 하위 그룹은 이러한 서비스에 대한 명령을 논리적 그룹으로 나눕니다. 예를 들어 `storage` 그룹에는  **계정**, **BLOB**, **저장소** 및 **큐** 등의 하위 그룹이 있습니다.

그러면 필요한 특정 명령을 찾는 방법은 무엇인가요? 한 가지 방법은 `az find`를 사용하는 것입니다. 예를 들어 저장소 BLOB을 관리하는 데 도움이 되는 명령을 찾으려면 다음 find 명령을 사용합니다.

```azurecli
az find -q blob
```

원하는 명령의 이름을 이미 알고 있는 경우 해당 명령의 `--help` 인수를 사용하면 명령에 대한 자세한 정보가 표시되고, 명령 그룹에 이 인수를 사용하면 사용 가능한 하위 명령 목록이 표시됩니다. 이 저장소 예제에서 Blob Storage 관리를 위한 하위 그룹 및 명령 목록을 가져올 방법은 다음과 같습니다.

```azurecli
az storage blob --help
```

## <a name="how-to-create-an-azure-resource"></a>Azure 리소스를 만드는 방법

새 Azure 리소스를 만드는 3단계는 일반적으로 Azure 구독에 연결하고, 리소스를 만들고, 리소스가 제대로 만들어졌는지 확인하는 것입니다. 다음 그림은 프로세스의 상위 수준 개요를 표시합니다.

![명령줄 인터페이스를 사용하여 Azure 리소스를 만드는 단계를 보여 주는 그림](../media/4-create-resources-overview.png)

각 단계는 다른 Azure CLI 명령에 해당합니다.

### <a name="connect"></a>연결

로컬에 설치한 Azure CLI를 사용하므로 Azure CLI **login** 명령을 사용하여 Azure 명령을 실행하기 전에 먼저 인증해야 합니다.

```azurecli
az login
```

Azure CLI에서는 일반적으로 기본 브라우저가 시작되어 Azure 로그인 페이지가 열립니다. 그러지 않는 경우 명령줄 지침에 따라 [https://aka.ms/devicelogin](https://aka.ms/devicelogin)에 인증 코드를 입력합니다.

로그인이 성공하면 Azure 구독에 연결됩니다.

### <a name="create"></a>만들기

새 Azure 서비스를 만들려면 먼저 새 리소스 그룹을 만들어야 하므로 CLI에서 Azure 리소스를 만드는 방법을 보여 주는 예로 리소스 그룹을 사용하겠습니다.

Azure CLI **group create** 명령은 리소스 그룹을 만듭니다. 이름 및 위치를 지정해야 합니다. 이름은 구독 내에서 고유해야 합니다. 위치는 리소스 그룹의 메타데이터가 저장되는 위치를 결정합니다. “미국 서부”, “북유럽” 또는 “인도 서부” 같은 문자열을 사용하여 위치를 지정합니다. westus, northeurope 또는 westindia 같이 동일한 의미의 단일 단어를 사용할 수도 있습니다. 핵심 구문은 다음과 같습니다.

```azurecli
az group create --name <name> --location <location>
```

### <a name="verify"></a>확인

Azure CLI는 여러 Azure 리소스에 대해 리소스 세부 정보를 표시하는 **list** 하위 명령을 제공합니다. 예를 들어 Azure CLI **group list** 명령은 Azure 리소스 그룹을 나열합니다. 여기서는 리소스 그룹 만들기가 성공했는지 확인하는 데 유용합니다.

```azurecli
az group list
```

뷰를 더 간결하게 하려면 출력을 간단한 테이블로 형식 지정할 수 있습니다.

```azurecli
az group list --output table
```
