이제 Azure에서 앱을 실행해 보겠습니다. Azure App Service 앱 만들기, 관리 되는 id와 자격 증명 모음 구성, 설정 및 코드를 배포 해야 합니다.

## <a name="create-the-app-service-plan-and-app"></a>App Service 계획 및 앱 만들기

App Service 만들기는 ‘계획’을 만든 후 ‘앱’을 만드는 2단계 프로세스입니다.****

‘플랜’ 이름은 구독 내에서만 고유해야 하므로 이전에 사용했던 동일한 이름을 사용할 수 있습니다. **keyvault-exercise-plan**.** 앱 이름은 전역적으로 고유해야 하므로 사용자가 자신만의 이름을 선택해야 합니다.

Azure Cloud Shell에서 다음을 실행합니다.

```azurecli
az appservice plan create --name keyvault-exercise-plan --resource-group keyvault-exercise-group
az webapp create --name <your-unique-app-name> --plan keyvault-exercise-plan --resource-group keyvault-exercise-group
```

## <a name="add-configuration-to-the-app"></a>앱에 구성 추가

Azure에 배포하려면 구성 파일 대신 응용 프로그램 설정에 VaultName 구성을 넣는 App Service 모범 사례를 따릅니다.

```azurecli
az webapp config appsettings set --name <your-unique-app-name> --resource-group keyvault-exercise-group --settings VaultName=<your-unique-vault-name>
```

## <a name="enable-managed-identity"></a>관리 되는 id를 사용 하도록 설정

One-liner는 앱에서 관리 되는 id를 사용 하도록 설정 합니다.

```azurecli
az webapp identity assign --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

결과로 생성되는 JSON 출력에서 **principalId** 값을 복사합니다. PrincipalId는 Azure Active Directory에서 앱의 새 ID 중 고유 ID이며 다음 단계에서 이 ID를 사용하려고 합니다.

## <a name="grant-access-to-the-vault"></a>자격 증명 모음에 대한 액세스 권한 부여

이제 앱 ID 권한을 제공하여 프로덕션 환경 자격 증명 모음의 비밀을 가져오고 나열해야 합니다. 이전 단계에서 복사한 **principalId** 값을 아래 명령에서 **object-id**의 값으로 사용합니다.

```azurecli
az keyvault set-policy --name <your-unique-vault-name> --object-id <your-managed-identity-principleid> --secret-permissions get list
```

## <a name="deploy-the-app-and-try-it-out"></a>앱을 배포하고 사용해 보기

모든 구성이 설정되고 배포할 준비가 되었습니다. 아래 명령은 사이트를 `pub` 폴더에 게시하고, `site.zip`으로 압축하고, 해당 Zip 파일을 App Service에 배포합니다.

> [!NOTE]
> 아직 이동하지 않은 경우에는 `cd`를 실행하여 다시 KeyVaultDemoApp 디렉터리로 이동해야 합니다.

```azurecli
dotnet publish -o pub
zip -j site.zip pub/*
az webapp deployment source config-zip --src site.zip --name <your-unique-app-name> --resource-group keyvault-exercise-group
```

사이트가 배포되었음을 나타내는 결과가 표시되면 브라우저에서 `https://<your-unique-app-name>.azurewebsites.net/api/SecretTest`를 엽니다. 비밀 값 **reindeer_flotilla**가 표시됩니다.

앱이 완료되어 배포되었습니다.