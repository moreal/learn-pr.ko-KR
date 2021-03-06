## <a name="creating-key-vaults-for-your-applications"></a>응용 프로그램에 대한 Key Vault 만들기

개발, 테스트, 프로덕션과 같이 각 응용 프로그램의 각 배포 환경을 위한 별도의 자격 증명 모음을 만드는 것이 좋습니다. 자격 증명 모음을 사용하여 여러 앱 간에 비밀을 공유할 수 있지만, 공격자가 자격 증명 모음에 대한 읽기 권한을 얻으면 자격 증명 모음의 비밀 수가 증가합니다.

> [!TIP]
> 응용 프로그램에 대한 서로 다른 환경에서 비밀에 동일한 이름을 사용하는 경우 앱의 환경 관련 구성에서는 자격 증명 모음 URL만 변경하면 됩니다.

자격 증명 모음을 만드는 데 초기 구성이 필요하지 않습니다. 사용자 ID에 전체 비밀 관리 권한 집합이 자동으로 부여되므로 즉시 비밀 추가를 시작할 수 있습니다. 자격 증명 모음이 있으면 Azure Portal, Azure CLI 및 Azure PowerShell 등 모든 Azure 관리 인터페이스에서 비밀을 추가하고 관리할 수 있습니다. 자격 증명 모음을 사용하도록 응용 프로그램을 설정할 경우 응용 프로그램에 올바른 권한을 할당해야 합니다. 다음 단원에서 확인해 보겠습니다.

## <a name="vault-authentication-and-permissions"></a>자격 증명 모음 인증 및 권한

Azure Key Vault의 API는 Azure Active Directory를 사용하여 사용자와 응용 프로그램을 인증합니다. 자격 증명 모음 액세스 정책은 ‘작업’을 기반으로 하고 전체 자격 증명 모음에 적용됩니다. 예를 들어 자격 증명 모음에 대한 **Get**(비밀 값 읽기), **List**(모든 비밀의 이름 나열) 및 **Set**(비밀 값 만들기 또는 업데이트) 권한을 가진 응용 프로그램은 비밀을 만들고, 모든 비밀 이름을 나열하고, 해당 자격 증명 모음의 모든 비밀 값을 가져오고 설정할 수 있습니다.

자격 증명 모음에서 수행되는 ‘모든’ 작업에는 인증과 권한 부여가 필요합니다. 어떤 종류든 익명 액세스 권한을 부여할 방법은 없습니다.

> [!TIP]
> 개발자 및 앱에 대한 자격 증명 모음 액세스 권한을 부여할 경우 필요한 최소 권한 집합만 부여합니다. 권한 제한 사항을 적용하면 코드 버그로 인해 발생하는 사고를 방지하고 앱에 삽입되는 도난 당한 자격 증명 또는 악의적인 코드의 영향을 줄일 수 있습니다.

일반적으로 개발자는 개발 환경 자격 증명 모음에 대한 **Get** 및 **List** 권한만 필요합니다. 책임 또는 선임 개발자는 필요한 경우 비밀을 변경하고 추가하기 위해 자격 증명 모음에 대한 전체 권한이 필요합니다. 일반적으로 프로덕션 환경 자격 증명 모음에 대한 전체 권한은 선임 작업 직원용으로 예약되어 있습니다.

앱의 경우 일반적으로 **Get** 권한만 필요합니다. 일부 앱의 경우 앱이 구현되는 방식에 따라 **List**가 필요할 수 있습니다. 이 모듈의 연습에서 구현하는 앱의 경우 앱이 자격 증명 모음에서 비밀을 읽는 데 사용하는 방법 때문에 **List** 권한이 필요합니다.

응용 프로그램 비밀과 관련하여 회사에서 발생하는 모든 문제의 경우 관리 부서에서는 다른 개발자에게 올바른 경로를 제시할 수 있는 작은 시작 앱을 만들도록 요청했습니다. 앱에서는 가능한 한 간단하고 안전하게 비밀을 관리하는 모범 사례를 제시해야 합니다.

## <a name="create-the-vault-and-store-the-secret-in-it"></a>자격 증명 모음을 만들고 그 안에 비밀을 저장합니다.
시작하려면 자격 증명 모음을 만들고 하나의 비밀을 저장합니다.

###  <a name="create-the-vault"></a>자격 증명 모음 만들기

먼저 자격 증명 모음을 만들고 그 안에 비밀을 저장합니다.

[!include[](../../../includes/azure-sandbox-activate.md)]

**Key Vault 이름은 전역적으로 고유해야 하므로 고유 이름을 선택해야 합니다**. 자격 증명 모음 이름은 3-24자로, 영숫자 및 대시만 포함해야 합니다. 선택하는 자격 증명 모음 이름을 기록해 두세요. 이 연습에서 필요합니다.

[!include[](../../../includes/azure-sandbox-regions-first-mention-note.md)]

Cloud Shell에서 다음 명령을 실행하여 자격 증명 모음을 만듭니다. 위의 섹션에서 다른 위치에 배치하려면 `--location` 값을 변경하면 됩니다.

```azurecli
az keyvault create \
    --name <your-unique-vault-name> \
    --resource-group <rgn>[sandbox resource group name]</rgn> \
    --location eastus
```

완료되면 새 자격 증명 모음을 설명하는 JSON 출력이 표시됩니다.

> [!TIP]
> 명령에는 **<rgn>[샌드박스 리소스 그룹]</rgn>** 이라는 미리 생성된 리소스 그룹을 사용되었습니다. 사용자 고유의 구독에서 작업하는 경우 새 리소스 그룹을 만들거나 이전에 만든 기존 리소스 그룹을 사용할 수 있습니다.

### <a name="add-the-secret"></a>비밀 추가

이제 비밀을 추가합니다. 여기서 사용할 비밀의 이름은 **SecretPassword**이고 값은 **reindeer_flotilla**입니다.

```azurecli
az keyvault secret set \
    --name SecretPassword \
    --value reindeer_flotilla \
    --vault-name <your-unique-vault-name>
```

잠시 후 응용 프로그램의 코드를 작성하겠지만, 그 전에 앱이 자격 증명 모음에 인증되는 원리를 간략하게 알아보겠습니다.