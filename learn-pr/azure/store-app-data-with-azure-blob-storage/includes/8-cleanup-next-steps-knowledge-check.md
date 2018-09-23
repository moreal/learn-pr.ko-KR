이 모듈에서는 Azure Blob Storage를 사용하여 웹 응용 프로그램 데이터를 저장하는 방법을 알아보았습니다. 웹앱에서 Blob Storage를 사용하는 전략을 만들기 위한 팁과 .NET Core용 Azure Storage SDK를 사용하여 Blob에 쓰고 읽는 방법을 설명했습니다. 여기서 만든 앱은 사용자로부터 업로드된 파일을 수락하고 이를 Blob Storage에 저장하며 다운로드할 수 있습니다.

[!include[](../../../includes/azure-sandbox-cleanup.md)]

Cloud Shell 저장소를 정리하려면 `mslearn-store-data-in-azure` 디렉터리를 삭제합니다.

<!---TODO: Remove further reading
## Further reading

- **Securely storing secrets like connection strings**: The most robust end-to-end solution for storing secret configuration values is Azure Key Vault. See [here](https://docs.microsoft.com/aspnet/core/security/key-vault-configuration?view=aspnetcore-2.1&tabs=aspnetcore2x) for information about using Key Vault in an ASP.NET Core application. Alternatively, you can safely store connection strings in App Service application settings and use the [ASP.NET Core Secret Manager tool](https://docs.microsoft.com/aspnet/core/security/app-secrets?view=aspnetcore-2.1&tabs=windows) to support developer environments.
- [Uploading large files with streaming in ASP.NET Core](https://docs.microsoft.com/aspnet/core/mvc/models/file-uploads?view=aspnetcore-2.1#uploading-large-files-with-streaming)
- [Blob concurrency: AccessConditions and blob leases](https://azure.microsoft.com/blog/managing-concurrency-in-microsoft-azure-storage-2/)
- [Granting limited access to Azure Storage object with shared access signatures](https://docs.microsoft.com/azure/storage/common/storage-dotnet-shared-access-signature-part-1)
- [Indexing Blob storage with Azure Search](https://docs.microsoft.com/azure/search/search-howto-indexing-azure-blob-storage)
- [Container and blob name restrictions](https://docs.microsoft.com/rest/api/storageservices/naming-and-referencing-containers--blobs--and-metadata#resource-names)
--->