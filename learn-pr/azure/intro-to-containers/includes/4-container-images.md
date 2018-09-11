<span data-ttu-id="d848a-101">지난 섹션에서는 미리 만들어진 컨테이너 이미지를 사용하여 몇 가지 기본적인 Docker 작업을 수행했습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-101">In the last unit, you worked with pre-created container images to perform some basic Docker operations.</span></span> <span data-ttu-id="d848a-102">이번 섹션에서는 사용자 지정 컨테이너 이미지를 만들고, 이러한 이미지를 공용 컨테이너 레지스트리에 푸시하고, 이러한 이미지에서 컨테이너를 실행하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-102">In this unit, you will create custom container images, push these images to a public container registry, and run containers from these images.</span></span>

<span data-ttu-id="d848a-103">컨테이너 이미지를 직접 만들어도 되고 Dockerfile을 사용하여 프로세스를 자동화해도 됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-103">Container images can be created by hand or using what's called a Dockerfile to automate the process.</span></span> <span data-ttu-id="d848a-104">사람들이 선호하는 방법은 Dockerfile이지만, 이번 섹션에서는 두 가지 방법을 모두 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-104">The preferred method is using a Dockerfile, but this unit will demonstrate both methods.</span></span> <span data-ttu-id="d848a-105">수동 프로세스를 이해하면 Dockerfile을 사용하여 자동화할 때 어떤 일이 발생하는지 이해하는 데 도움이 되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-105">The intention is that having an understanding of the manual process will help you to better understand what's occurring when using a Dockerfile for automation.</span></span>

## <a name="manual-image-creation"></a><span data-ttu-id="d848a-106">수동으로 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d848a-106">Manual image creation</span></span>

<span data-ttu-id="d848a-107">컨테이너 이미지를 수동으로 만들 때에는 다음 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-107">When manually creating a container image, the following actions are taken:</span></span>

- <span data-ttu-id="d848a-108">컨테이너 인스턴스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-108">Start an instance of a container.</span></span>
- <span data-ttu-id="d848a-109">컨테이너와 터미널 세션을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-109">Establish a terminal session with the container.</span></span>
- <span data-ttu-id="d848a-110">소프트웨어를 설치하고 구성을 변경하여 컨테이너를 수정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-110">Modify the container by installing software and making configuration changes.</span></span>
- <span data-ttu-id="d848a-111">`docker capture` 명령을 사용하여 컨테이너를 새 이미지에 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-111">Capturing the container into a new image using the `docker capture` command.</span></span>

<span data-ttu-id="d848a-112">첫 번째 예제에서는 Python을 실행하는 컨테이너 인스턴스를 시작하고, Hello world 응용 프로그램을 만들고, 컨테이너를 새 이미지에 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-112">In this first example, you start an instance of a container that's running Python, create a hello world application, and then capture the container to a new image.</span></span>

<span data-ttu-id="d848a-113">먼저 NGINX 이미지에서 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-113">First, run a container from the NGINX image.</span></span> <span data-ttu-id="d848a-114">이 명령은 이전 섹션에서 실행한 명령과 약간 다르게 보입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-114">This command looks a bit different from the commands that you ran in the previous unit.</span></span> <span data-ttu-id="d848a-115">실행 중인 컨테이너와 터미널 세션을 설정하려는 것이기 때문에 `-t` 및 `-i` 인수를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-115">Because you want to establish a terminal session with the running container, the `-t` and `-i` arguments are provided.</span></span> <span data-ttu-id="d848a-116">두 인수는 함께 사용할 경우 실행 중 상태를 유지하는 의사 터미널을 할당하라고 Docker에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-116">Together, these arguments instruct Docker to allocate a pseudo terminal that will remain in a runnings state.</span></span> <span data-ttu-id="d848a-117">즉, `-t` 및 `-i` 인수는 실행 중인 컨테이너와 대화형 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-117">In other words, the `-t` and `-i` arguments create an interactive session with the running container.</span></span>

<span data-ttu-id="d848a-118">그런 다음, `python` 컨테이너 이미지를 사용하고 컨테이너 내부에서 `bash` 프로세스를 실행하도록 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-118">You then specify that the `python` container image is used, and the process to run inside of the container is `bash`.</span></span>

```bash
docker run --name python-demo -ti python bash
```

<span data-ttu-id="d848a-119">명령을 실행하면 터미널 세션이 컨테이너 의사 터미널로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-119">After the command is run, your terminal session should switch to the containers pseudo terminal.</span></span> <span data-ttu-id="d848a-120">이것은 터미널 프롬프트에서 확인할 수 있으며, 다음과 비슷하게 변경되었을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-120">This can be seen by the terminal prompt, which should have changed to something similar to the following:</span></span>

```bash
root@d8ccada9c61e:/#
```

<span data-ttu-id="d848a-121">지금은 컨테이너 내부에서 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-121">At this point, you're working inside the container.</span></span> <span data-ttu-id="d848a-122">컨테이너 내부에서 작업하는 것은 가상 또는 물리적 시스템 내부에서 작업하는 것과 비슷합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-122">You should find that working inside a container is much like working inside a virtual or physical system.</span></span> <span data-ttu-id="d848a-123">예를 들어 파일을 나열, 생성 및 삭제하고, 소프트웨어를 설치하고, 구성을 변경할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-123">For instance, you can list, create, and delete files, install software, and make configuration changes.</span></span> <span data-ttu-id="d848a-124">이 간단한 예제에서는 Python 기반 Hello world 스크립트가 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-124">For this simple example, a Python-based hello world script is created.</span></span> <span data-ttu-id="d848a-125">이 작업은 다음 명령을 사용하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-125">This can be done with the following command:</span></span>

```bash
echo 'print("Hello World!")' > hello.py
```

<span data-ttu-id="d848a-126">컨테이너에 있는 동안 스크립트를 테스트하려면 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-126">To test the script while you're still in the container, run the following command:</span></span>

```bash
python hello.py
```

<span data-ttu-id="d848a-127">그러면 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-127">This will produce the following output:</span></span>

```bash
Hello World!
```

<span data-ttu-id="d848a-128">스크립트가 예상대로 작동하여 만족스러운 경우 `exit`를 입력하여 컨테이너에서 나옵니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-128">When you're satisfied that the script functions as expected, exit out of the container by typing `exit`:</span></span>

```bash
exit
```

<span data-ttu-id="d848a-129">로컬 시스템의 터미널로 돌아가서, `docker ps` 명령을 사용하여 실행 중인 모든 컨테이너를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-129">Back in the terminal of your local system, use the `docker ps` command to list all running containers:</span></span>

```bash
docker ps
```

<span data-ttu-id="d848a-130">아무 것도 실행되고 있지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-130">Notice that nothing is running.</span></span> <span data-ttu-id="d848a-131">실행 중인 컨테이너에서 `exit`를 입력하면 Bash 프로세스가 완료되고 컨테이너가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-131">When you entered `exit` in the running container, the Bash process completed, which then stopped the container.</span></span> <span data-ttu-id="d848a-132">이것은 예상된 정상적인 동작입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-132">This is the expected behavior and is ok.</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

<span data-ttu-id="d848a-133">`docker ps`를 다시 사용하여 `-a` 인수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-133">Use `docker ps` again and include the `-a` argument.</span></span> <span data-ttu-id="d848a-134">이 명령은 실행 여부에 관계없이 모든 컨테이너 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-134">This command will return a list of all containers, regardless if they're running.</span></span>

```bash
docker ps -a
```

<span data-ttu-id="d848a-135">이름이 *python-demo*인 컨테이너의 상태는 *끝냄*입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-135">Notice that a container with the name *python-demo* has a status of *Exited*.</span></span> <span data-ttu-id="d848a-136">이 컨테이너는 방금 종료한 컨테이너의 중지된 인스턴스입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-136">This container is the stopped instance of the container that you just exited from.</span></span>

```bash
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
```

<span data-ttu-id="d848a-137">이 컨테이너에서 새 컨테이너 이미지를 만들려면 `docker commit` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-137">To create a new container image from this container, use the `docker commit` command.</span></span> <span data-ttu-id="d848a-138">다음 예제는 *python-demo* 컨테이너로 *python-custom*이라는 이미지를 만들도록 *docker commit*에 지시합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-138">The following example instructs *docker commit* to create an image named *python-custom* from the *python-demo* containers.</span></span>

```bash
docker commit python-demo python-custom
```

<span data-ttu-id="d848a-139">명령을 완료한 후 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-139">After the command completes, you should see output similar to the following:</span></span>

```bash
sha256:91a0cf9aa9857bebcd7ebec3418970f97f043e31987fd4a257c8ac8c8418dc38
```

<span data-ttu-id="d848a-140">이제 `docker images`를 실행하여 컨테이너 이미지 목록을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-140">Now run `docker images` to see a list of container images:</span></span>

```bash
docker images
```

<span data-ttu-id="d848a-141">사용자 지정 Python 이미지가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-141">You should now see the custom Python image.</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
python-custom       latest              1f231e7127a1        6 seconds ago       922MB
python              latest              638817465c7d        24 hours ago        922MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

<span data-ttu-id="d848a-142">새 이미지에서 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-142">Run a container from the new image.</span></span> <span data-ttu-id="d848a-143">컨테이너 내에서 실행할 명령 또는 프로세스도 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-143">You also need to specify what command or process to run inside of the container.</span></span> <span data-ttu-id="d848a-144">이 예제에서는 `python hello.py`를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-144">With this example, run `python hello.py`.</span></span>


```bash
docker run python-custom python hello.py
```

<span data-ttu-id="d848a-145">컨테이너가 시작되고 Hello world 메시지가 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-145">The container will start and output the hello world message.</span></span> <span data-ttu-id="d848a-146">그 후 Python 프로세스가 완료되고 컨테이너가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-146">The Python process is then complete and the container stops.</span></span>

```bash
Hello World!
```

## <a name="automated-image-creation"></a><span data-ttu-id="d848a-147">자동화된 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="d848a-147">Automated image creation</span></span>

<span data-ttu-id="d848a-148">지난 섹션에서는 수동으로 컨테이너 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-148">In the last section, a container image was manually created.</span></span> <span data-ttu-id="d848a-149">이 방법은 일회성 또는 경험을 쌓기 위한 이미지 만들기에는 적합하지만, 프로덕션 환경에서 유지 가능한 방법이 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-149">While this method works great for one-off or experiential image creation, it's not sustainable in a production environment.</span></span> <span data-ttu-id="d848a-150">*Dockerfile* 및 `docker build` 명령을 사용하여 컨테이너 이미지 만들기를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-150">Container image creation can be automated using a *Dockerfile* and the `docker build` command.</span></span> <span data-ttu-id="d848a-151">*docker build* 명령은 기본적으로 컨테이너를 시작하고, *Dockerfile*에서 찾은 지침을 실행하고, 결과를 새 컨테이너 이미지에 캡처합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-151">The *docker build* command essentially starts a container, runs the instructions found in the *Dockerfile*, and then captures the results to a new container image.</span></span>

<span data-ttu-id="d848a-152">*Dockerfile*이라는 파일을 만들고 다음 텍스트를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-152">Create a file named *Dockerfile* and enter the following text:</span></span>

```bash
FROM python

WORKDIR ./app

RUN echo 'print("Hello World!")' > hello.py

CMD python hello.py
```

<span data-ttu-id="d848a-153">*FROM* 문은 이미지 만들기에 사용할 기본 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-153">The *FROM* statement specifies the base image to be used during image creations.</span></span> <span data-ttu-id="d848a-154">*RUN* 문은 컨테이너 내에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-154">The *RUN* statement runs commands inside of the container.</span></span> <span data-ttu-id="d848a-155">*RUN*은 소프트웨어를 설치하고, 구성을 변경하고, 캡처 이벤트 전에 컨테이너를 정리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-155">*RUN* can be used to install software, make configuration changes, and cleanup the container before the capture event.</span></span> <span data-ttu-id="d848a-156">*CMD* 문은 컨테이너가 시작될 때 실행할 프로세스를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-156">The *CMD* statement specifies the process that should run when a container is started.</span></span>

<span data-ttu-id="d848a-157">`docker build` 명령을 사용하여 Dockerfile에 지정된 지침을 따르는 새 컨테이너 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-157">Use the `docker build` command to create a new container image using the instructions specified in the Dockerfile.</span></span>

```bash
docker build -t python-dockerfile .
```

<span data-ttu-id="d848a-158">다음과 유사한 결과가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-158">You should see output similar to the following.</span></span>

```bash
Sending build context to Docker daemon  2.048kB
Step 1/4 : FROM python
 ---> 638817465c7d
Step 2/4 : WORKDIR ./app
 ---> Running in 990d17e86466
Removing intermediate container 990d17e86466
 ---> 59a074a092cc
Step 3/4 : RUN echo 'print("Hello World!")' > hello.py
 ---> Running in aed707c53bc5
Removing intermediate container aed707c53bc5
 ---> d7f55a9d0e85
Step 4/4 : CMD python hello.py
 ---> Running in e87ec55a8d36
Removing intermediate container e87ec55a8d36
 ---> 98c39b91770f
Successfully built 98c39b91770f
Successfully tagged python-dockerfile:latest
```

<span data-ttu-id="d848a-159">`docker images` 명령을 사용하여 컨테이너 이미지 목록을 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-159">Use the `docker images` command to return a list of container images.</span></span>

```bash
docker images
```

<span data-ttu-id="d848a-160">사용자 지정 이미지가 보일 것입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-160">You should now see the custom image.</span></span>

```bash
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
python-dockerfile   latest              98c39b91770f        About a minute ago   922MB
python              latest              638817465c7d        26 hours ago         922MB
alpine              latest              11cd0b38bc3c        2 weeks ago          4.41MB
```

<span data-ttu-id="d848a-161">`docker run` 명령을 사용하여 사용자 지정 이미지에서 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-161">Use the `docker run` command to run a container from the custom image.</span></span>

<span data-ttu-id="d848a-162">여기서는 `docker run` 명령에 아무 인수도 제공되지 않았습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-162">Notice here that no arguments have been provided to the `docker run` command.</span></span> <span data-ttu-id="d848a-163">수동으로 컨테이너 이미지를 만들 때와는 달리, Dockerfile을 사용하면 컨테이너가 시작될 때 실행할 명령을 포함할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-163">Unlike when you manually create a container image, a Dockerfile allows you to include a command to run when the container starts.</span></span> <span data-ttu-id="d848a-164">이 예에서 지정된 명령은 컨테이너에 Python 스크립트를 실행하라고 지시하는 `python hello.py`입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-164">In this case, the specified command is `python hello.py`, which causes the container to run the Python script.</span></span>

```bash
docker run python-dockerfile
```

<span data-ttu-id="d848a-165">명령을 실행하면 컨테이너 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-165">After you run the command, you should see the container output.</span></span>

```bash
Hello World!
```

## <a name="push-the-image-to-a-public-registry"></a><span data-ttu-id="d848a-166">이미지를 공용 레지스트리에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-166">Push the image to a public registry</span></span>

<span data-ttu-id="d848a-167">Docker 허브는 공용 컨테이너 레지스트리입니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-167">Docker Hub is a public container registry.</span></span> <span data-ttu-id="d848a-168">컨테이너 이미지를 Docker 허브에 푸시하려면 Docker 계정이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-168">In order to push container images to Docker Hub, you must have a Docker account.</span></span> <span data-ttu-id="d848a-169">필요한 경우 [Docker 허브 사이트](https://hub.docker.com/)를 방문하여 계정을 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-169">If needed, visit the [Docker Hub site](https://hub.docker.com/) to register for an account.</span></span>

<span data-ttu-id="d848a-170">Docker 허브 계정을 만든 후에는 계정 이름을 컨테이너 이미지의 태그로 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-170">After you have a Docker Hub account, the container image must be tagged with the account name.</span></span> <span data-ttu-id="d848a-171">이렇게 하려면 `docker tag` 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-171">To do so, use the `docker tag` command.</span></span>

<span data-ttu-id="d848a-172">다음 예제에서는 Docker 허브 계정 이름을 *python dockerfile* 이미지의 태그로 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-172">In the following example, the *python-dockerfile* image is tagged with a Docker Hub account name.</span></span> <span data-ttu-id="d848a-173">`<account name>`을 Docker 허브 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-173">Replace `<account name>` with your Docker Hub account name.</span></span>

```bash
docker tag python-dockerfile <account name>/python-dockerfile
```

<span data-ttu-id="d848a-174">다음으로, `docker login` 명령을 사용하여 Docker 허브에 로그인되었는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-174">Next, make sure that you are logged into Docker Hub using the `docker login` command.</span></span>

```bash
docker login
```

<span data-ttu-id="d848a-175">마지막으로, `docker push` 명령을 사용하여 *python-dockerfile* 이미지를 Docker 허브에 푸시합니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-175">Finally push the *python-dockerfile* image to Docker Hub using the `docker push` command.</span></span> <span data-ttu-id="d848a-176">`<account name>`을 Docker 허브 계정 이름으로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-176">Replace `<account name>` with your Docker Hub account name.</span></span>

```bash
docker push <account name>/python-dockerfile
```

<span data-ttu-id="d848a-177">컨테이너 이미지가 Docker 허브에 업로드되는 동안 다음과 유사한 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-177">While the container image is being uploaded to Docker Hub, you will see output similar to the following:</span></span>

```bash
The push refers to repository [docker.io/account/python-dockerfile]
f39073ca4d5a: Pushed
9dfcec2738a9: Pushed
ffab8273c674: Mounted from account/python
e6f6cbe5e14e: Mounted from account/python
3eb255f8a6ac: Mounted from account/python
b860b6c48eec: Mounted from account/python
1fa8778eb779: Mounted from account/python
fa0c3f992cbd: Mounted from account/python
ce6466f43b11: Mounted from account/python
719d45669b35: Mounted from account/python
3b10514a95be: Mounted from account/python
```

<span data-ttu-id="d848a-178">컨테이너 이미지가 Docker 허브에 저장되었으며 인터넷에 연결된 모든 머신에서 `docker pull` 또는 `docker run` 명령을 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-178">The container image is now stored in Docker Hub and can be accessed from any internet-connected machine using `docker pull` or `docker run`.</span></span>

## <a name="summary"></a><span data-ttu-id="d848a-179">요약</span><span class="sxs-lookup"><span data-stu-id="d848a-179">Summary</span></span>

<span data-ttu-id="d848a-180">이 섹션에서는 두 개의 컨테이너 이미지를 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-180">In this unit, you created two container images.</span></span> <span data-ttu-id="d848a-181">첫 번째 이미지는 수동으로 만들었고 두 번째 이미지는 Dockerfile을 사용하여 자동화했습니다.</span><span class="sxs-lookup"><span data-stu-id="d848a-181">The first was created manually and the second was automated using a Dockerfile.</span></span>
