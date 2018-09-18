이 모듈에서는 Azure Blob Storage를 사용하여 웹 응용 프로그램 데이터를 저장하는 방법을 알아보았습니다. 웹앱에서 Blob Storage를 사용하는 전략을 만들기 위한 팁과 .NET Core용 Azure Storage SDK를 사용하여 Blob에 쓰고 읽는 방법을 설명했습니다. 여기서 만든 앱은 사용자로부터 업로드된 파일을 수락하고 이를 Blob Storage에 저장하며 다운로드할 수 있습니다.

## <a name="clean-up"></a>정리
<!---TODO: Update for sandbox?--->

Azure 구독을 정리하려면 Azure Cloud Shell에서 다음을 실행하여 이 모듈에서 만든 모든 리소스가 포함된 리소스 그룹을 삭제합니다.

```console
az group delete --name blob-exercise-group --yes --no-wait
```

Cloud Shell 저장소를 정리하려면 `mslearn-store-data-in-azure` 디렉터리를 삭제합니다.

## <a name="further-reading"></a>추가 참고 자료

- **연결 문자열처럼 비밀을 안전하게 저장**: 비밀 구성 값을 저장하기 위한 가장 강력한 종단 간 솔루션은 Azure Key Vault입니다. ASP.NET Core 응용 프로그램에서 Key Vault를 사용하는 방법에 대한 자세한 내용은 [여기](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x)를 참조하세요. 또는 연결 문자열을 App Service 응용 프로그램 설정에 안전하게 저장하고 [ASP.NET Core 비밀 관리자 도구](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows)를 사용하여 개발자 환경을 지원할 수 있습니다.
- [ASP.NET Core에서 스트리밍을 통해 대용량 파일 업로드](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
- [Blob concurrency: AccessConditions and blob leases](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)(Blob 동시성: AccessConditions 및 Blob 임대)
- [공유 액세스 서명을 사용하여 Azure Storage 개체에 제한된 액세스 권한 부여](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Azure Search로 Blob Storage 인덱싱](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
- [Container and blob name restrictions](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)(컨테이너 및 Blob 이름 제한 사항)