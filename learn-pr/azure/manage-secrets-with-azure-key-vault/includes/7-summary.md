이 모듈에서는 앱의 비밀 구성을 Azure Key Vault로 보호했습니다. 시작 시 앱 코드가 관리 ID로 자격 증명 모음에 인증되고 자격 증명 모음에서 ASP.NET Core의 구성 시스템으로 비밀을 자동으로 로드합니다.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

Cloud Shell 저장소를 정리하려면 `KeyVaultDemoApp` 디렉터리를 삭제합니다.

## <a name="next-steps"></a>다음 단계

실제 앱인 경우 다음 단계를 무엇일까요?

- 자격 증명 모음에 모든 앱 비밀을 넣으세요! 더 이상 앱 비밀을 구성 파일에 포함할 이유가 없습니다.
- 계속해서 응용 프로그램을 개발합니다. 프로덕션 환경이 모두 설정되어 있으므로 나중에 해당 환경에 배포하기 위해 모든 설정을 반복할 필요가 없습니다.
- 개발을 지원하려면 이름이 동일하지만 값이 다른 비밀을 포함하는 개발 환경을 만듭니다. 개발 팀에 권한을 부여하고 앱의 개발 환경 구성 파일에서 자격 증명 모음 이름을 구성합니다. 개발자가 앱을 로컬로 실행하면 `AddAzureKeyVault`가 Visual Studio 및 Azure CLI의 로컬 설치를 자동으로 검색하고 해당 응용 프로그램에 구성된 Azure 자격 증명을 사용하여 로그인하고 자격 증명 모음에 액세스합니다.
- 사용자 승인 테스트 같은 용도로 추가 환경을 만듭니다.
- 다양한 구독 및/또는 리소스 그룹에서 자격 증명 모음을 분리하여 격리합니다.
- 다른 환경 자격 증명 모음에 대한 액세스 권한을 적절한 사용자에게 부여합니다.

## <a name="further-reading"></a>추가 참고 자료

- [Key Vault 설명서](https://docs.microsoft.com/azure/key-vault/)
- [AddAzureKeyVault 및 해당 고급 옵션에 대한 자세한 정보](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)
- [이 자습서](https://docs.microsoft.com/azure/key-vault/key-vault-use-from-web-application)에서는 관리 ID 대신 클라이언트 비밀을 사용하여 Azure Active Directory에 수동으로 인증하는 작업을 포함하여 `KeyVaultClient`를 사용하는 방법을 살펴봅니다.
- 인증 워크플로를 직접 구현하기 위한 [Azure 리소스 토큰 서비스 설명서에 대한 관리 ID](https://docs.microsoft.com/azure/app-service/app-service-managed-service-identity#using-the-rest-protocol).