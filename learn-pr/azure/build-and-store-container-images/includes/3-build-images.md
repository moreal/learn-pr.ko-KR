<span data-ttu-id="9a6d1-101">귀하의 회사에서는 컨테이너 이미지를 사용하여 계산 워크로드를 관리한다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-101">Suppose your company makes use of container images to manage compute workloads.</span></span> <span data-ttu-id="9a6d1-102">로컬 Docker 도구를 사용하여 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-102">You use the local Docker tooling to build your container images.</span></span>

<span data-ttu-id="9a6d1-103">이제 Azure Container Registry 작업을 사용하여 이러한 컨테이너를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-103">You can now use Azure Container Registry Tasks to build these containers.</span></span> <span data-ttu-id="9a6d1-104">Container Registry 작업을 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와도 통합할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-104">Container Registry Tasks also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="9a6d1-105">Azure Container Registry 작업을 사용하여 컨테이너 이미지 만들기를 자동화하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-105">Let's automate the creation of a container image using Azure Container Registry Tasks.</span></span>

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a><span data-ttu-id="9a6d1-106">Azure Container Registry 작업을 사용하여 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="9a6d1-106">Create a container image with Azure Container Registry Tasks</span></span>

<span data-ttu-id="9a6d1-107">빌드 지침을 제공하는 표준 Dockerfile입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-107">A standard Dockerfile to provides build instructions.</span></span> <span data-ttu-id="9a6d1-108">Azure Container Registry 작업을 사용하면 다단계 빌드를 포함하여 현재 환경에서 모든 Dockerfile을 다시 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-108">Azure Container Registry Tasks allows you to reuse any Dockerfile currently in your environment, including multi-staged builds.</span></span>

<span data-ttu-id="9a6d1-109">이 예제에서는 새 Dockerfile을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-109">We'll use a new Dockerfile for our example.</span></span>

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

<span data-ttu-id="9a6d1-110">첫 번째 단계는 이름이 `Dockerfile`인 새 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-110">The first step is to create a new file named `Dockerfile`.</span></span> <span data-ttu-id="9a6d1-111">모든 텍스트 편집기를 사용하여 파일을 편집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-111">You can use any text editor to edit the file.</span></span> <span data-ttu-id="9a6d1-112">이 예제에는 Cloud Shell 편집기를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-112">We'll use Cloud Shell Editor for this example.</span></span> <span data-ttu-id="9a6d1-113">다음 명령을 Cloud Shell 창에 입력하여 편집기를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-113">Enter the following command into the Cloud Shell window to open the editor.</span></span>

```bash
code
```

<span data-ttu-id="9a6d1-114">새 Dockerfile에 다음 내용을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-114">Copy the following contents to your new Dockerfile.</span></span> <span data-ttu-id="9a6d1-115">파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-115">Make sure to save the file.</span></span>

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="9a6d1-116">키 조합 <kbd>Ctrl+S</kbd>를 사용하여 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-116">Use the key combination <kbd>Ctrl+S</kbd> to save.</span></span> <span data-ttu-id="9a6d1-117">메시지가 표시되면 `Dockerfile` 파일의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-117">Name the file `Dockerfile` when prompted.</span></span>

<span data-ttu-id="9a6d1-118">이 구성은 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-118">This configuration adds a Node.js application to the `node:9-alpine` image.</span></span> <span data-ttu-id="9a6d1-119">그런 다음, *EXPOSE* 명령을 통해 포트 80에서 응용 프로그램을 제공하도록 컨테이너를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-119">After that, it configures the container to serve the application on port 80 via the *EXPOSE* instruction.</span></span>

<span data-ttu-id="9a6d1-120">이제 Azure CLI 명령 `az acr build`를 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-120">Now run the Azure CLI command `az acr build` to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrtasks:v1 .
```

<span data-ttu-id="9a6d1-121">명령을 실행할 때 빌드되어 Container Registry로 푸시되는 이미지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-121">You'll see the image being built and pushed to your Container Registry as you run the command.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="9a6d1-122">이미지 확인</span><span class="sxs-lookup"><span data-stu-id="9a6d1-122">Verify the image</span></span>

<span data-ttu-id="9a6d1-123">다음 명령을 실행하여 이미지가 만들어지고 레지스트리에 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-123">Run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="9a6d1-124">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-124">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrtasks
```

<span data-ttu-id="9a6d1-125">이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="9a6d1-125">The `helloacrbuild` image is now ready to be used.</span></span>
