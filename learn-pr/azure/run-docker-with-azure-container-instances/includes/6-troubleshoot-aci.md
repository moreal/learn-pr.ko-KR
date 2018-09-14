<span data-ttu-id="53fe0-101">여기에서 컨테이너 로그를 컨테이너 이벤트 것과 같은 일부 기본적인 문제 해결 작업을 수행할 됩니다 하 고 컨테이너 인스턴스를 연결 합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-101">Here, you will perform some basic troubleshooting operations such as pulling container logs, container events, and attaching to a container instance.</span></span> <span data-ttu-id="53fe0-102">이 모듈을 마치면 컨테이너 인스턴스 문제 해결을 위한 기본적인 기능을 이해할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-102">By the end of this module, you should understand basic capabilities for troubleshooting container instances.</span></span>

## <a name="create-a-container"></a><span data-ttu-id="53fe0-103">컨테이너 만들기</span><span class="sxs-lookup"><span data-stu-id="53fe0-103">Create a container</span></span>

<span data-ttu-id="53fe0-104">컨테이너를 만들어 시작 합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-104">Start by creating a container.</span></span> <span data-ttu-id="53fe0-105">이 모듈에서 만든 첫 번째 컨테이너가 아직 있는 경우 이 단계를 건너뜁니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-105">If you still have the first container created in this module, skip this step:</span></span>

```azurecli
az container create --resource-group <rgn>[Sandbox resource group name]</rgn> --name mycontainer --image microsoft/aci-helloworld --ports 80 --ip-address Public
```

## <a name="get-logs-from-a-container-instance"></a><span data-ttu-id="53fe0-106">컨테이너 인스턴스에서 로그 가져오기</span><span class="sxs-lookup"><span data-stu-id="53fe0-106">Get logs from a container instance</span></span>

<span data-ttu-id="53fe0-107">컨테이너 내의 응용 프로그램 코드에서 로그를 보려면 `az container logs` 명령을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-107">To view logs from your application code within a container, you can use the `az container logs` command:</span></span>

```azazurecli
az container logs --resource-group <rgn>[Sandbox resource group name]</rgn> --name mycontainer
```

<span data-ttu-id="53fe0-108">다음은 웹앱에 몇 번 액세스한 후 생성된 예제 컨테이너의 로그 출력입니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-108">The following is log output from the example container after the web app has been accessed a few times:</span></span>

```output
listening on port 80
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET / HTTP/1.1" 200 1663 "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:24 +0000] "GET /favicon.ico HTTP/1.1" 404 150 "http://23.101.136.193/" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:25 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
::ffff:0.0.0.0 - - [20/Aug/2018:21:44:27 +0000] "GET / HTTP/1.1" 304 - "-" "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_13_6) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/68.0.3440.106 Safari/537.36"
```

## <a name="get-container-events"></a><span data-ttu-id="53fe0-109">컨테이너 이벤트 가져오기</span><span class="sxs-lookup"><span data-stu-id="53fe0-109">Get container events</span></span>

<span data-ttu-id="53fe0-110">`az container attach` 명령은 컨테이너 시작 중에 진단 정보를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-110">The `az container attach` command provides diagnostic information during container startup.</span></span> <span data-ttu-id="53fe0-111">컨테이너가 시작되면 로컬 콘솔에 STDOUT 및 STDERR도 스트리밍합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-111">Once the container has started, it also streams STDOUT and STDERR to your local console:</span></span>

```azazurecli
az container attach --resource-group <rgn>[Sandbox resource group name]</rgn> --name mycontainer
```

<span data-ttu-id="53fe0-112">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="53fe0-112">Example output:</span></span>


```output
Container 'mycontainer' is in state 'Running'...
(count: 1) (last timestamp: 2018-08-20 21:43:26+00:00) pulling image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:32+00:00) Successfully pulled image "microsoft/aci-helloworld"
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Created container
(count: 1) (last timestamp: 2018-08-20 21:43:33+00:00) Started container

Start streaming logs:
listening on port 80
listening on port 80
```

## <a name="execute-a-command-in-a-container"></a><span data-ttu-id="53fe0-113">컨테이너에서 명령 실행</span><span class="sxs-lookup"><span data-stu-id="53fe0-113">Execute a command in a container</span></span>

<span data-ttu-id="53fe0-114">Azure Container Instances는 실행 중인 컨테이너에서 명령을 실행하도록 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-114">Azure Container Instances supports executing a command in a running container.</span></span> <span data-ttu-id="53fe0-115">시작한 컨테이너에서 명령을 실행하면 응용 프로그램 개발 및 문제 해결 중에 특히 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-115">Running a command in a container you've already started is especially helpful during application development and troubleshooting.</span></span> <span data-ttu-id="53fe0-116">이 기능은 일반적으로 실행 중인 컨테이너에서 문제를 디버그할 수 있도록 대화형 셸을 시작하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-116">The most common use of this feature is to launch an interactive shell, so that you can debug issues in a running container.</span></span>

<span data-ttu-id="53fe0-117">이 예제는 실행 중인 컨테이너를 사용하여 대화형 터미널 세션을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-117">This example starts an interactive terminal session with the running container:</span></span>

```azurecli
az container exec --resource-group <rgn>[Sandbox resource group name]</rgn> --name mycontainer --exec-command /bin/sh
```

<span data-ttu-id="53fe0-118">이 명령이 완료되면 컨테이너 내부에서 효과적으로 작업할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-118">Once the command has completed, you are effectively working inside of the container.</span></span> <span data-ttu-id="53fe0-119">이 예제에서 `ls` 명령을 실행하여 작업 디렉터리의 내용을 표시하였습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-119">In this example, the `ls` command was run to display the contents of the working directory:</span></span>

```output
usr/src/app # ls
index.html         node_modules       package.json
index.js           package-lock.json
```

<span data-ttu-id="53fe0-120">`exit`를 입력하여 원격 세션을 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-120">Enter `exit` to stop the remote session.</span></span>

## <a name="monitor-container-cpu-and-memory"></a><span data-ttu-id="53fe0-121">컨테이너 CPU 및 메모리 모니터링</span><span class="sxs-lookup"><span data-stu-id="53fe0-121">Monitor container CPU and memory</span></span>

<span data-ttu-id="53fe0-122">CPU 및 메모리 사용량에 대한 메트릭을 끌어올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-122">You may want to pull metrics on CPU and memory usage.</span></span> <span data-ttu-id="53fe0-123">이렇게 하려면 먼저 Azure 컨테이너 인스턴스의 ID를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-123">To do so, first get the ID of the Azure container instance.</span></span> <span data-ttu-id="53fe0-124">이 예제에서 이 ID는 `CONTAINER_ID` 변수에 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-124">In this example, the ID is placed in a variable named `CONTAINER_ID`:</span></span>

```azurecli
CONTAINER_ID=$(az container show --resource-group <rgn>[Sandbox resource group name]</rgn> --name mycontainer --query id --output tsv)
```

<span data-ttu-id="53fe0-125">이제 `az monitor metrics list` 명령을 사용하여 CPU 사용량 정보를 다시 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-125">Now, use the `az monitor metrics list` command to pull back CPU usage information:</span></span>

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric CPUUsage --output table
```

<span data-ttu-id="53fe0-126">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="53fe0-126">Example output:</span></span>

```output
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:39:00  CPU Usage
2018-08-20 21:40:00  CPU Usage
2018-08-20 21:41:00  CPU Usage
2018-08-20 21:42:00  CPU Usage
2018-08-20 21:43:00  CPU Usage      0.375
2018-08-20 21:44:00  CPU Usage      0.875
2018-08-20 21:45:00  CPU Usage      1
2018-08-20 21:46:00  CPU Usage      3.625
2018-08-20 21:47:00  CPU Usage      1.5
2018-08-20 21:48:00  CPU Usage      2.75
2018-08-20 21:49:00  CPU Usage      1.625
2018-08-20 21:50:00  CPU Usage      0.625
2018-08-20 21:51:00  CPU Usage      0.5
2018-08-20 21:52:00  CPU Usage      0.5
2018-08-20 21:53:00  CPU Usage      0.5
```

<span data-ttu-id="53fe0-127">다음 명령을 사용하여 메모리 사용량 정보를 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-127">The following command can be used to get memory usage information:</span></span>

```azurecli
az monitor metrics list --resource $CONTAINER_ID --metric MemoryUsage --output table
```

<span data-ttu-id="53fe0-128">예제 출력:</span><span class="sxs-lookup"><span data-stu-id="53fe0-128">Example output:</span></span>

```output
Timestamp            Name              Average
-------------------  ------------  -----------
2018-08-20 21:43:00  Memory Usage
2018-08-20 21:44:00  Memory Usage  0.0
2018-08-20 21:45:00  Memory Usage  15917056.0
2018-08-20 21:46:00  Memory Usage  16744448.0
2018-08-20 21:47:00  Memory Usage  16842752.0
2018-08-20 21:48:00  Memory Usage  17190912.0
2018-08-20 21:49:00  Memory Usage  17506304.0
2018-08-20 21:50:00  Memory Usage  17702912.0
2018-08-20 21:51:00  Memory Usage  17965056.0
2018-08-20 21:52:00  Memory Usage  18509824.0
2018-08-20 21:53:00  Memory Usage  18649088.0
2018-08-20 21:54:00  Memory Usage  18845696.0
2018-08-20 21:55:00  Memory Usage  19181568.0
```

<span data-ttu-id="53fe0-129">이 정보는 Azure Portal에서도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="53fe0-129">This information is also available in the Azure portal.</span></span> <span data-ttu-id="53fe0-130">CPU 및 메모리 사용량 정보의 그래픽 표시를 보려면 컨테이너 인스턴스에 대한 Azure Portal 개요 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="53fe0-130">To see graphical representation of CPU and memory usage information, visit the Azure portal overview page for a container instance.</span></span>

![Azure Container Instances CPU 및 메모리 사용량 정보의 Azure Portal 보기](../media-draft/cpu-memory.png)

[!include[](../../../includes/azure-sandbox-cleanup.md)]
