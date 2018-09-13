<span data-ttu-id="22b83-101">귀하의 회사에서는 컨테이너 이미지를 사용하여 회사의 계산 워크로드를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-101">Your company makes use of container images to manage compute workloads in the company.</span></span> <span data-ttu-id="22b83-102">로컬 Docker 도구를 사용하여 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-102">You use local Docker tooling to build your container images.</span></span> <span data-ttu-id="22b83-103">이제 Azure Container Registry를 사용 하기로 한 결정으로 클라우드에서 컨테이너 이미지를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-103">The decision to make use of an Azure Container Registry now allows you to build container images in the cloud.</span></span> 

<span data-ttu-id="22b83-104">이제 Azure Container Registry Build를 사용하여 이러한 컨테이너를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-104">You can now use Azure Container Registry Build to build these containers.</span></span> <span data-ttu-id="22b83-105">Container Registry Build를 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-105">Container Registry Build also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="22b83-106">Azure Container Registry Build를 사용하여 컨테이너 이미지 만들기를 자동화하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-106">Let's automate the creation of a container image using Azure Container Registry Build.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-build"></a><span data-ttu-id="22b83-107">Azure Container Registry Build를 사용하여 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="22b83-107">Create a container image with Azure Container Registry Build</span></span>

<span data-ttu-id="22b83-108">표준 Dockerfile을 사용하여 빌드 지침을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-108">You use a standard Dockerfile to provide build instructions.</span></span> <span data-ttu-id="22b83-109">Azure Container Registry Build를 사용하면 다단계 빌드를 포함하여 현재 환경에서 모든 Dockerfile을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-109">Azure Container Registry Build allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="22b83-110">예제로 새 Dockerfile을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-110">We'll use new Dockerfile for our example.</span></span> 

<span data-ttu-id="22b83-111">첫 번째 단계는 `Dockerfile`이라는 새 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-111">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="22b83-112">모든 텍스트 편집기를 사용하여 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-112">You can use any text editor to edit the file.</span></span> <span data-ttu-id="22b83-113">이 예제로 Visual Studio Code를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-113">We'll use Visual Studio Code for this example.</span></span>

```bash
code Dockerfile
```

<span data-ttu-id="22b83-114">새 Dockerfile에 다음 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-114">Copy the following contents to your new Dockerfile.</span></span> <span data-ttu-id="22b83-115">파일이 안전한지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-115">Make sure to safe the file.</span></span> 

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="22b83-116">이 구성에서는 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-116">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="22b83-117">그런 다음, *EXPOSE* 명령을 통해 포트 80에서 응용 프로그램을 제공하도록 컨테이너를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-117">Then configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

<span data-ttu-id="22b83-118">이제 Azure CLI 명령 `az acr build`를 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-118">Now run the Azure CLI command, `az acr build`, to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

<span data-ttu-id="22b83-119">명령을 실행할 때 빌드되어 Container Registry로 푸시되는 이미지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-119">You'll see the image being built and pushed to your Container Registry as you run the command.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="22b83-120">이미지 확인</span><span class="sxs-lookup"><span data-stu-id="22b83-120">Verify the image</span></span>

<span data-ttu-id="22b83-121">다음 명령을 실행하여 이미지가 만들어지고 레지스트리에 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-121">Run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="22b83-122">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-122">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrbuild
```

<span data-ttu-id="22b83-123">이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="22b83-123">The `helloacrbuild` image is now ready to be used.</span></span>
