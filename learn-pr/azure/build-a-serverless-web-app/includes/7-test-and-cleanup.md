<span data-ttu-id="1b07d-101">Azure 서비스를 사용하여 모든 기능을 갖춘 서버리스 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-101">You've successfully created a full-featured, serverless application using Azure services.</span></span>

## <a name="clean-up"></a><span data-ttu-id="1b07d-102">정리</span><span class="sxs-lookup"><span data-stu-id="1b07d-102">Clean up</span></span>
<!---TODO: Update for sandbox--->

<span data-ttu-id="1b07d-103">이 응용 프로그램의 작업이 완료되면 다음 명령을 사용하여 자습서 중에 만들어진 모든 리소스를 삭제할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-103">When you are done working with this application, you can use the following command to delete all resources created during the tutorial:</span></span>

```azurecli
az group delete --name first-serverless-app
```

<span data-ttu-id="1b07d-104">메시지가 표시되면 `y`를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-104">Type `y` when prompted.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="1b07d-105">다음 단계</span><span class="sxs-lookup"><span data-stu-id="1b07d-105">Next steps</span></span>

<span data-ttu-id="1b07d-106">이 모듈에서는 다음을 수행하는 방법을 알아보았습니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-106">In this module, you learned how to:</span></span>
  - <span data-ttu-id="1b07d-107">정적 웹 사이트 및 업로드된 이미지를 호스트하도록 Azure Blob Storage를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-107">Configure Azure Blob storage to host a static website and uploaded images.</span></span>
  - <span data-ttu-id="1b07d-108">Azure Functions를 사용하여 Azure Blob Storage에 이미지를 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-108">Upload images to Azure Blob storage using Azure Functions.</span></span>
  - <span data-ttu-id="1b07d-109">Azure Functions를 사용하여 이미지의 크기를 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-109">Resize images using Azure Functions.</span></span>
  - <span data-ttu-id="1b07d-110">Azure Cosmos DB에서 이미지 메타데이터를 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-110">Store image metadata in Azure Cosmos DB.</span></span> 
  - <span data-ttu-id="1b07d-111">Cognitive Services Computer Vision API를 사용하여 이미지 캡션을 자동 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-111">Use the Cognitive Services Computer Vision API to auto-generate image captions.</span></span>
  - <span data-ttu-id="1b07d-112">사용자를 인증하여 웹앱을 보호하도록 Azure Active Directory를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-112">Use Azure Active Directory to secure the web app by authenticating users.</span></span>

<span data-ttu-id="1b07d-113">Functions에 추가 서비스를 연결하는 방법을 알아보려면 [Logic Apps를 사용하는 함수](https://docs.microsoft.com/azure/azure-functions/functions-twitter-email) 자습서를 진행합니다.</span><span class="sxs-lookup"><span data-stu-id="1b07d-113">To learn how to connect even more services to Functions, continue to the [Functions with Logic Apps](https://docs.microsoft.com/azure/azure-functions/functions-twitter-email) tutorial.</span></span>