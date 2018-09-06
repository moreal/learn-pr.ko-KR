<span data-ttu-id="93091-101">Azure Container Registry 빌드가 있으면 로컬 Docker 도구를 사용하지 않고도 클라우드에 컨테이너 이미지를 빌드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93091-101">With Azure Container Registry Build, container images can be built in the cloud, without the need for local Docker tooling.</span></span> <span data-ttu-id="93091-102">Container Registry 빌드를 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와 통합할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="93091-102">Container Registry Build also allows for DevOps process integration with automated build on source code commit.</span></span>

<span data-ttu-id="93091-103">이 단원에서는 Azure Container Registry 빌드를 사용하여 컨테이너 이미지 만들기를 자동화합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-103">In this unit, you automate the creation of a container image using Azure Container Registry Build.</span></span>

## <a name="create-a-container-image-with-build"></a><span data-ttu-id="93091-104">빌드를 사용하여 컨테이너 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="93091-104">Create a container image with Build</span></span>

<span data-ttu-id="93091-105">Azure Container Registry 빌드를 사용하는 경우 표준 Dockerfile이 빌드 지침을 제공하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="93091-105">When using Azure Container Registry Build, a standard Dockerfile is used to provide build instructions.</span></span> <span data-ttu-id="93091-106">다단계 빌드를 포함하여 현재 환경에서 사용되는 모든 Dockerfile은 Azure Container Registry 빌드에서 작동합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-106">Any Dockerfile currently used in your environment, including multistaged builds, works with Azure Container Registry Build.</span></span>

<span data-ttu-id="93091-107">`Dockerfile`이라는 파일을 만들고 텍스트 편집기를 사용하여 엽니다.</span><span class="sxs-lookup"><span data-stu-id="93091-107">Create a file named `Dockerfile` and open it with any text editor.</span></span>

```bash
code Dockerfile
```

<span data-ttu-id="93091-108">다음 콘텐츠에서 복사하고 파일을 저장한 후 텍스트 편집기를 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-108">Copy in the following contents, save the file, and exit the text editor.</span></span> <span data-ttu-id="93091-109">이 Dockerfile은 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가하고 포트 80에서 해당 응용 프로그램을 제공하도록 컨테이너를 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-109">This Dockerfile adds a Node.js application to the `node:9-alpine` image and configures the container to server the application on port 80.</span></span>

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

<span data-ttu-id="93091-110">다음 명령을 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-110">Run the following command to build the container image from the Dockerfile.</span></span>

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
```

<span data-ttu-id="93091-111">이 작업을 실행하면 빌드되어 Container Registry로 푸시되는 이미지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="93091-111">As this operation runs, you will see the image being built and pushed to your container registry.</span></span>

## <a name="verify-the-image"></a><span data-ttu-id="93091-112">이미지 확인</span><span class="sxs-lookup"><span data-stu-id="93091-112">Verify the image</span></span>

<span data-ttu-id="93091-113">빌드 작업이 완료되면 다음 명령을 실행하여 이미지가 만들어졌고 레지스트리에 저장되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-113">When the build operation has completed, run the following command to verify that the image has been created and stored in the registry.</span></span>

```azurecli
az acr repository list --name <acrName> --output table
```

<span data-ttu-id="93091-114">출력은 다음과 비슷해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-114">The output should look similar to the following:</span></span>

```console
Result
-------------
helloacrbuild
```

<span data-ttu-id="93091-115">이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.</span><span class="sxs-lookup"><span data-stu-id="93091-115">The `helloacrbuild` image is now ready to be used.</span></span>

## <a name="summary"></a><span data-ttu-id="93091-116">요약</span><span class="sxs-lookup"><span data-stu-id="93091-116">Summary</span></span>

<span data-ttu-id="93091-117">이 단원에서는 Azure Container Registry 빌드를 사용하여 컨테이너 이미지 만들기를 자동화했습니다.</span><span class="sxs-lookup"><span data-stu-id="93091-117">In this unit, Azure Container Registry Build was used to automate the creation of a container image.</span></span> <span data-ttu-id="93091-118">그런 다음, 해당 이미지를 Azure Container Registry에 저장했습니다.</span><span class="sxs-lookup"><span data-stu-id="93091-118">This image was then stored in the Azure container registry.</span></span> <span data-ttu-id="93091-119">다음 단원에서는 새 컨테이너 이미지 인스턴스를 Azure Container Instances에 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="93091-119">In the next unit, you will deploy an instance of the new container image to Azure Container Instances.</span></span>