이전 연습에서는 디렉터리를 만들고, 사용자 및 그룹을 만들고, Azure Portal에 액세스할 때 Azure Multi-Factor Authentication을 요구하는 조건부 액세스 규칙을 만들었습니다. 이제는 리소스에 액세스할 수 있는지 테스트해 보겠습니다.

## <a name="test-access-to-resources"></a>리소스에 대한 액세스 테스트

사용자가 MyApps 포털을 사용하여 로그인하고 모든 SaaS 응용 프로그램에 액세스할 수 있음을 알고 있으므로 이를 테스트해 보겠습니다.

1. InPrivate 브라우저 창을 엽니다.

1. https://myapps.microsoft.com으로 이동합니다.

1. 3단원에서 만든 사용자로 로그인합니다.

   * Multi-Factor Authentication을 요구하지 않고 포털에 로그인됩니다.

1. 동일한 브라우저 창에서 https://portal.azure.com으로 이동합니다.

   * 이제 계정을 안전하게 유지하기 위해 더 많은 정보를 제공해야 합니다. 이 인터럽트는 만든 조건부 액세스 정책으로 인해 Azure Multi-Factor Authentication이 시작됩니다. 이 시점에서 중지하고 브라우저 창을 닫을 수 있습니다.