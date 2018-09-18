Azure Storage 계정 만들기 및 연결에 대한 기본 사항을 알아보았습니다. 간단한 응용 프로그램을 작성하여 저장소 계정에 연결하고 Blob 컨테이너를 만들었습니다. 이 학습 경로의 다른 모듈에서는 해당 지식을 기반으로 Blob Storage 및 큐를 사용하여 데이터를 저장하고 앱을 함께 연결하는 방법을 보여 줍니다.

여기서는 JavaScript 및 C#의 예제만 사용했지만, Azure는 다양한 다른 언어를 지원합니다. 공식 [SDK Tools 설명서 페이지](https://docs.microsoft.com/azure/#pivot=sdkstools)를 확인하여 현재 지원되는 모든 언어의 클라이언트 라이브러리에 대한 공식 링크 목록을 찾으세요.

## <a name="additional-resources"></a>추가 리소스

- [Azure Storage 서비스 REST API 참조](https://docs.microsoft.com/rest/api/storageservices/)
- [공유 액세스 서명을 사용하여 저장소 계정에 대한 제한된 액세스 권한 제공](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Azure Key Vault를 사용하여 비밀 관리](https://docs.microsoft.com/learn/modules/manage-secrets-with-azure-key-vault/)
- [서버 앱과 함께 Azure Key Vault 저장소 계정 키 사용](https://docs.microsoft.com/azure/key-vault/key-vault-ovw-storage-keys)
- [.NET Azure SDK의 소스 코드](https://github.com/Azure/azure-sdk-for-net)
- [JavaScript용 Azure Storage 클라이언트 라이브러리](https://github.com/Azure/azure-storage-node#azure-storage-javascript-client-library-for-browsers)

## <a name="clean-up"></a>정리
<!---TODO: Update for sandbox?--->

작업을 완료하면 Azure에서 리소스를 정리하는 것이 좋습니다. 무료 샌드박스를 사용하는 경우에는 이 단계를 수행할 필요가 없지만, 구독에서 불필요한 비용을 피하려면 사용되지 않는 리소스를 삭제해야 합니다. 이를 수행하는 가장 쉬운 방법은 모든 리소스를 포함한 리소스 그룹을 삭제하는 것입니다. 이 작업은 Azure Portal 또는 명령줄에서 수행할 수 있습니다.