<span data-ttu-id="45bf4-101">Azure Container Instances에서는 컨테이너를 배포하기가 쉽고 빠르므로 컨테이너 인스턴스에서 빌드, 테스트 및 이미지 렌더링과 같은 일회성 작업을 실행하기 위한 강력한 플랫폼을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-101">The ease and speed of deploying containers in Azure Container Instances provides a compelling platform for executing run-once tasks like build, test, and image rendering in a container instance.</span></span>

<span data-ttu-id="45bf4-102">구성 가능한 다시 시작 정책을 사용하면 프로세스가 완료될 때 컨테이너가 중지되도록 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-102">With a configurable restart policy, you can specify that your containers are stopped when their processes have completed.</span></span> <span data-ttu-id="45bf4-103">컨테이너 인스턴스는 초 단위로 비용이 청구되기 때문에 작업을 실행하는 컨테이너가 실행되는 동안 사용된 계산 리소스에 대해서만 요금이 부과됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-103">Because container instances are billed by the second, you're charged only for the compute resources used while the container executing your task is running.</span></span>

## <a name="container-restart-policies"></a><span data-ttu-id="45bf4-104">컨테이너 다시 시작 정책</span><span class="sxs-lookup"><span data-stu-id="45bf4-104">Container restart policies</span></span>

<span data-ttu-id="45bf4-105">Azure Container Instances에서 컨테이너를 만들 때 세 가지 다시 시작 정책 설정 중 하나를 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-105">When you create a container in Azure Container Instances, you can specify one of three restart policy settings:</span></span>

| <span data-ttu-id="45bf4-106">다시 시작 정책</span><span class="sxs-lookup"><span data-stu-id="45bf4-106">Restart policy</span></span>   | <span data-ttu-id="45bf4-107">설명</span><span class="sxs-lookup"><span data-stu-id="45bf4-107">Description</span></span> |
| ---------------- | :---------- |
| `Always` | <span data-ttu-id="45bf4-108">컨테이너 그룹의 컨테이너가 항상 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-108">Containers in the container group are always restarted.</span></span> <span data-ttu-id="45bf4-109">컨테이너를 만들 때 다시 시작 정책이 지정되지 않은 경우 적용되는 **기본** 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-109">This is the **default** setting applied when no restart policy is specified at container creation.</span></span> |
| `Never` | <span data-ttu-id="45bf4-110">컨테이너 그룹의 컨테이너가 절대로 다시 시작되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-110">Containers in the container group are never restarted.</span></span> <span data-ttu-id="45bf4-111">컨테이너가 한 번만 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-111">The containers run at most once.</span></span> |
| `OnFailure` | <span data-ttu-id="45bf4-112">컨테이너 그룹의 컨테이너가 컨테이너에서 실행된 프로세스가 실패할 때만(0이 아닌 종료 코드로 종료될 때) 다시 시작됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-112">Containers in the container group are restarted only when the process executed in the container fails (when it terminates with a nonzero exit code).</span></span> <span data-ttu-id="45bf4-113">컨테이너가 한 번 이상 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-113">The containers are run at least once.</span></span> |

<span data-ttu-id="45bf4-114">이 모듈의 이전 단원에서는 지정된 다시 시작 정책 없이 컨테이너가 생성되었습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-114">In the previous unit of this module, a container was created without a specified restart policy.</span></span> <span data-ttu-id="45bf4-115">기본적으로 이 컨테이너는 *Always* 다시 시작 정책을 받았습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-115">By default, this container received the *Always* restart policy.</span></span> <span data-ttu-id="45bf4-116">컨테이너의 워크로드가 장기 실행되므로(웹 서버) 이 정책이 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-116">Because the workload in the container is long running (a web server), this policy makes sense.</span></span>

## <a name="run-to-completion"></a><span data-ttu-id="45bf4-117">완료될 때까지 실행</span><span class="sxs-lookup"><span data-stu-id="45bf4-117">Run to completion</span></span>

<span data-ttu-id="45bf4-118">다시 시작 정책의 작동 방식을 보려면 *microsoft/aci-wordcount* 이미지에서 컨테이너 인스턴스를 만들고 *OnFailure* 다시 시작 정책을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-118">To see the restart policy in action, create a container instance from the *microsoft/aci-wordcount* image and specify the *OnFailure* restart policy.</span></span> <span data-ttu-id="45bf4-119">이 예제 컨테이너는 셰익스피어의 Hamlet 텍스트를 분석하고, 가장 많이 쓰이는 10개의 단어를 STDOUT에 쓰고 종료하는 Python 스크립트를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-119">This example container runs a Python script that analyzes the text of Shakespeare's Hamlet, writes the 10 most common words to STDOUT, and then exits.</span></span>

<span data-ttu-id="45bf4-120">다음 `az container create` 명령을 사용하여 예제 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-120">Run the example container with the following `az container create` command:</span></span>

```azureclu
az container create \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --image microsoft/aci-wordcount:latest \
    --restart-policy OnFailure
```

<span data-ttu-id="45bf4-121">Azure Container Instances는 컨테이너를 시작한 다음, 응용 프로그램(또는 이 경우 스크립트)이 종료될 때 컨테이너를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-121">Azure Container Instances starts the container and then stops it when its application (or script, in this case) exits.</span></span> <span data-ttu-id="45bf4-122">Azure Container Instances가 다시 시작 정책이 *Never* 또는 *OnFailure*인 컨테이너를 중지하면 컨테이너의 상태가 **Terminated**로 설정됩니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-122">When Azure Container Instances stops a container whose restart policy is *Never* or *OnFailure*, the container's status is set to **Terminated**.</span></span>

<span data-ttu-id="45bf4-123">다음과 같이 `az container show` 명령으로 컨테이너의 상태를 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-123">You can check a container's status with the `az container show` command:</span></span>

```azurecli
az container show \
    --resource-group myResourceGroup \
    --name mycontainer-restart-demo \
    --query containers[0].instanceView.currentState.state
```

<span data-ttu-id="45bf4-124">예제 컨테이너의 상태가 **Terminated**로 표시되면 컨테이너 로그를 확인하여 작업 출력을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-124">Once the example container's status shows **Terminated**, you can see its task output by viewing the container logs.</span></span> <span data-ttu-id="45bf4-125">스크립트의 출력을 보려면 **az container logs** 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-125">Run the **az container logs** command to view the script's output:</span></span>

```azurecli
az container logs --resource-group myResourceGroup --name mycontainer-restart-demo
```

<span data-ttu-id="45bf4-126">출력:</span><span class="sxs-lookup"><span data-stu-id="45bf4-126">Output:</span></span>

```bash
[('the', 990),
 ('and', 702),
 ('of', 628),
 ('to', 610),
 ('I', 544),
 ('you', 495),
 ('a', 453),
 ('my', 441),
 ('in', 399),
 ('HAMLET', 386)]
```

## <a name="summary"></a><span data-ttu-id="45bf4-127">요약</span><span class="sxs-lookup"><span data-stu-id="45bf4-127">Summary</span></span>

<span data-ttu-id="45bf4-128">이 단원에서는 다시 시작 정책 *OnFailure*를 사용하여 컨테이너 인스턴스를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-128">In this unit, you created a container instance with a restart policy of *OnFailure*.</span></span> <span data-ttu-id="45bf4-129">이 구성은 단기 작업을 실행하는 컨테이너에 적합합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-129">This configuration works well for containers that run short-lived tasks.</span></span>

<span data-ttu-id="45bf4-130">다음 단원에서는 Azure Container Instance에서 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="45bf4-130">In the next unit, you will set environment variables in Azure Container Instances.</span></span>
