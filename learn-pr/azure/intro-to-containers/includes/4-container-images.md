<span data-ttu-id="2ab5b-101">지금까지는 다른 사용자가 만든 Docker 이미지를 다운로드하고 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-101">Up until now, you downloaded and ran Docker images created by others.</span></span> <span data-ttu-id="2ab5b-102">여기에서는 사용자 고유의 컨테이너 이미지를 빌드합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-102">Here, you'll build your own container images.</span></span> <span data-ttu-id="2ab5b-103">이 문서에서 배울 내용은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-103">You'll learn how to:</span></span>

* <span data-ttu-id="2ab5b-104">수동 프로세스를 사용하여 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-104">Create an image using a manual process.</span></span>
* <span data-ttu-id="2ab5b-105">Dockerfile이라는 좀 더 자동화된 프로세스를 사용하여 동일한 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-105">Create the same image using a more automated process, called a Dockerfile.</span></span>
* <span data-ttu-id="2ab5b-106">공용 컨테이너 레지스트리인 Docker 허브에 이미지를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-106">Publish your image to Docker Hub, a public container registry.</span></span>

## <a name="what-is-a-dockerfile"></a><span data-ttu-id="2ab5b-107">Dockerfile이란?</span><span class="sxs-lookup"><span data-stu-id="2ab5b-107">What is a Dockerfile?</span></span>

<span data-ttu-id="2ab5b-108">Dockerfile이란 컨테이너가 실행해야 하는 모든 것이 설명된 텍스트 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-108">A Dockerfile is a text file that describes everything your container needs to run.</span></span>

<span data-ttu-id="2ab5b-109">Dockerfile의 지침에는 다음이 정의될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-109">An instruction in the Dockerfile can define:</span></span>

* <span data-ttu-id="2ab5b-110">이미지가 기반을 두고 있는 부모 이미지입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-110">The parent image your image is based on.</span></span>
* <span data-ttu-id="2ab5b-111">설치할 소프트웨어 패키지입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-111">A software package to install.</span></span>
* <span data-ttu-id="2ab5b-112">앱이 실행해야 하는 구성 또는 다른 파일입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-112">A configuration or other file your app needs to run.</span></span>
* <span data-ttu-id="2ab5b-113">사용할 수 있도록 하려는 포트 등의 네트워킹 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-113">Networking settings, such as a port you want to make available.</span></span>
* <span data-ttu-id="2ab5b-114">컨테이너가 시작될 때 실행할 명령입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-114">The command to run when the container starts.</span></span>

<span data-ttu-id="2ab5b-115">수동 프로세스를 사용하여 컨테이너 이미지를 만들거나 Dockerfile을 사용하여 프로세스를 자동화할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-115">You can create a container image using a manual process or use a Dockerfile to automate the process.</span></span> <span data-ttu-id="2ab5b-116">Docker 이미지를 수동으로 만들면 프로세스를 이해하는 데 도움이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-116">Creating a Docker image manually is a good way to understand the process.</span></span> <span data-ttu-id="2ab5b-117">Dockerfile을 사용하면 프로세스를 더 쉽고 빠르게 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-117">Using a Dockerfile makes the process faster and easier to repeat.</span></span>

## <a name="what-is-docker-hub"></a><span data-ttu-id="2ab5b-118">Docker 허브란?</span><span class="sxs-lookup"><span data-stu-id="2ab5b-118">What is Docker Hub?</span></span>

<span data-ttu-id="2ab5b-119">Docker 허브란 Docker 이미지를 저장하고 다운로드할 수 있는 곳입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-119">Docker Hub is a place for you to store and download Docker images.</span></span> <span data-ttu-id="2ab5b-120">이전에 사용한 Nginx 이미지처럼 Docker 및 Docker 커뮤니티에서 만든 Docker 이미지를 다운로드할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-120">You can download Docker images that have been created by Docker and the Docker community, such as the Nginx image you used previously.</span></span> <span data-ttu-id="2ab5b-121">또한 Docker 커뮤니티 또는 자신의 팀과 자체 사용자 고유의 이미지를 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-121">You can also share your own images with the Docker community or just with your team.</span></span>

## <a name="create-an-image-manually"></a><span data-ttu-id="2ab5b-122">수동으로 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="2ab5b-122">Create an image manually</span></span>

<span data-ttu-id="2ab5b-123">여기에서는 기본 Python 응용 프로그램을 실행하는 Docker 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-123">Here you'll create a Docker image that runs a basic Python application.</span></span>

1. <span data-ttu-id="2ab5b-124">먼저 [python](https://hub.docker.com/_/python/?azure-portal=true) 이미지에서 컨테이너 인스턴스를 불러옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-124">Start by bringing up a container instance from the [python](https://hub.docker.com/_/python/?azure-portal=true) image.</span></span>

    ```bash
    docker run --name python-demo -it python bash
    ```

    <span data-ttu-id="2ab5b-125">Docker가 Docker Hub에서 이 이미지를 끌어오는 동안 잠시 시간이 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-125">It'll take a few moments for Docker to pull down this image from Docker Hub.</span></span> <span data-ttu-id="2ab5b-126">기다리는 동안 명령의 역할에 대해 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-126">While you wait, let's look at what the command does.</span></span>

    * <span data-ttu-id="2ab5b-127">`--name` 인수는 컨테이너의 이름 "python-demo"를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-127">The `--name` argument specifies your container's name, "python-demo".</span></span>
    * <span data-ttu-id="2ab5b-128">`-i` 및 `-t` 인수는 `-it`라는 하나의 인수로 결합됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-128">The `-i` and `-t` arguments are combined into one argument, `-it`.</span></span> <span data-ttu-id="2ab5b-129">이러한 인수는 실행 중인 컨테이너와의 대화형 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-129">These arguments create an interactive session with the running container.</span></span>
      * <span data-ttu-id="2ab5b-130">`-i`는 컨테이너를 사용하여 대화형 세션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-130">`-i` creates an interactive session with the container.</span></span>
      * <span data-ttu-id="2ab5b-131">`-t`는 실행 중 상태로 유지되는 의사 터미널을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-131">`-t` creates a pseudo terminal that remains in a running state.</span></span>
    * <span data-ttu-id="2ab5b-132">`python`은 기본 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-132">`python` specifies the base image.</span></span> <span data-ttu-id="2ab5b-133">Docker는 Docker 허브에서 이 이미지를 다운로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-133">Docker downloads this image from Docker Hub.</span></span> <span data-ttu-id="2ab5b-134">이 이미지는 Python 프로그래밍용 환경으로 사전 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-134">This image is preconfigued with an environment for Python programming.</span></span>
    * <span data-ttu-id="2ab5b-135">`bash`는 실행할 프로그램을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-135">`bash` specifies the program to run.</span></span>

    <span data-ttu-id="2ab5b-136">이 설정은 Python 앱을 작성하는 데 필요한 대화형 환경으로 보면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-136">Think of this setup as an interactive environment for you to write Python apps.</span></span> <span data-ttu-id="2ab5b-137">앱을 시작할 준비가 되면 환경의 이미지나 스냅숏을 캡처할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-137">Once you have your app up and running, you can capture an image, or snapshot, of your environment.</span></span> <span data-ttu-id="2ab5b-138">앱을 개선하면서 사용자 또는 팀을 위한 추가 이미지를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-138">As you improve your app, you can create additional images for you or your team.</span></span>

    <span data-ttu-id="2ab5b-139">터미널 세션이 컨테이너의 의사 터미널로 전환됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-139">Your terminal session switches to the container's pseudo terminal.</span></span> <span data-ttu-id="2ab5b-140">다음과 유사한 프롬프트가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-140">Your prompt resembles this:</span></span>

    ```docker
    root@d8ccada9c61e:/#
    ```

1. <span data-ttu-id="2ab5b-141">Docker 세션에서 이를 실행하여 `./app`이라는 디렉터리를 만들고 이 디렉터리로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-141">From your Docker session, run this to create a directory named `./app` and move to it.</span></span>

    ```bash
    mkdir ./app && cd ./app
    ```

    <span data-ttu-id="2ab5b-142">필수는 아니지만 필요할 경우 `./app` 디렉터리에 Python 코드를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-142">Although not required, the `./app` directory gives you a place to add your Python code.</span></span>

1. <span data-ttu-id="2ab5b-143">매우 기본적인 Python 프로그램을 만들려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-143">Run this to create a very basic Python program.</span></span>

    ```bash
    echo 'print("Hello World!")' > hello.py
    ```

    <span data-ttu-id="2ab5b-144">이 프로그램은 터미널에 "Hello World!"를</span><span class="sxs-lookup"><span data-stu-id="2ab5b-144">This program prints "Hello World!"</span></span> <span data-ttu-id="2ab5b-145">출력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-145">to the terminal.</span></span>

    > [!TIP]
    > <span data-ttu-id="2ab5b-146">실제로는 워크스테이션의 디렉터리를 컨테이너의 디렉터리에 _마운트_할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-146">In practice, you can _mount_ a directory on your workstation to a directory on your container.</span></span> <span data-ttu-id="2ab5b-147">그러면 워크스테이션에서 자주 사용하는 편집기를 사용하여 코드를 작성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-147">This enables you to use your favorite editor on your workstation to write code.</span></span> <span data-ttu-id="2ab5b-148">파일을 저장하면 해당 파일이 컨테이너에도 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-148">When you save your file, that file also appears on your container.</span></span>

1. <span data-ttu-id="2ab5b-149">다음을 실행하여 Python 프로그램을 사용해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-149">Run the following to try out your Python program.</span></span>

    ```bash
    python hello.py
    ```

    <span data-ttu-id="2ab5b-150">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-150">You see this.</span></span>

    ```output
    Hello World!
    ```

1. <span data-ttu-id="2ab5b-151">대화형 세션을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-151">Exit your interactive session.</span></span>

    ```bash
    exit
    ```

1. <span data-ttu-id="2ab5b-152">Linux VM에서 `docker ps`를 실행하여 실행 중인 모든 컨테이너를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-152">From your Linux VM, run `docker ps` to list all running containers:</span></span>

    ```bash
    docker ps
    ```

    <span data-ttu-id="2ab5b-153">아무것도 실행되고 있지 않은 것을 알 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-153">You see that nothing is running.</span></span> 

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    ```

    <span data-ttu-id="2ab5b-154">컨테이너를 종료하면 Bash 세션도 종료되기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-154">That's because exiting the container ends your Bash session.</span></span> <span data-ttu-id="2ab5b-155">컨테이너가 실행하는 응용 프로그램 또는 서비스가 종료되면 Docker가 컨테이너를 중지합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-155">When the application or service your container runs exits, Docker stops the container.</span></span>

1. <span data-ttu-id="2ab5b-156">`docker ps`를 다시 한 번 실행하고 `-a` 인수를 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-156">Run `docker ps` a second time and include the `-a` argument.</span></span> <span data-ttu-id="2ab5b-157">이 명령은 실행 중이거나 중지된 모든 컨테이너를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-157">This command returns all containers, running or stopped.</span></span>

    ```bash
    docker ps -a
    ```

    <span data-ttu-id="2ab5b-158">다음과 같이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-158">You see something like this:</span></span>

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
    ```

   <span data-ttu-id="2ab5b-159">**python-demo** 컨테이너의 상태는 **종료됨**입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-159">Your container, **python-demo**, has a status of **Exited**.</span></span>

1. <span data-ttu-id="2ab5b-160">`docker commit`를 실행하여 컨테이너에서 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-160">Run `docker commit` to create an image from your container.</span></span>

   ```bash
   docker commit python-demo python-custom
   ```

   <span data-ttu-id="2ab5b-161">이때 Docker는 **python-demo**라는 컨테이너에서 **python-custom**이라는 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-161">Here, Docker creates an image named **python-custom** from your container named **python-demo**.</span></span> <span data-ttu-id="2ab5b-162">이미지 이름은 원하는 대로 지정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-162">The image name can be whatever you want.</span></span>

1. <span data-ttu-id="2ab5b-163">`docker images`를 실행하여 이미지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-163">Run `docker images` to list your images.</span></span>

    ```bash
    docker images
    ```

    <span data-ttu-id="2ab5b-164">**python-custom** 이미지가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-164">You see the **python-custom** image.</span></span>

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-custom       latest              1f231e7127a1        6 seconds ago       922MB
    python              latest              638817465c7d        24 hours ago        922MB
    ```

1. <span data-ttu-id="2ab5b-165">`docker run`을 사용하여 이미지를 테스트해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-165">Use `docker run` to test out your image.</span></span>

    ```bash
    docker run python-custom python app/hello.py
    ```

    <span data-ttu-id="2ab5b-166">`docker run`은 실행할 명령을 최종 인수로 사용한다는 사실을 떠올려 보세요.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-166">Recall that `docker run` takes the command to run as its final argument.</span></span> <span data-ttu-id="2ab5b-167">여기서 이 명령은 `python app/hello.py`입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-167">Here, the command is `python app/hello.py`.</span></span>

    <span data-ttu-id="2ab5b-168">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-168">You see this.</span></span>

    ```output
    Hello World!
    ```

    <span data-ttu-id="2ab5b-169">이 컨테이너를 대화형으로 실행하고 있지 않으므로 Python 프로그램이 실행되고 컨테이너가 중지됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-169">Because you're not running this container interactively, the Python program runs and the container stops.</span></span>

## <a name="use-a-dockerfile-to-create-an-image-automatically"></a><span data-ttu-id="2ab5b-170">Dockerfile을 사용하여 자동으로 이미지 생성</span><span class="sxs-lookup"><span data-stu-id="2ab5b-170">Use a Dockerfile to create an image automatically</span></span>

<span data-ttu-id="2ab5b-171">여기에서는 좀 더 자동화된 프로세스를 사용하여 Python 프로그램을 실행하는 동일한 Docker 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-171">Here you'll use a more automated process to create the same Docker image that runs your Python program.</span></span>

<span data-ttu-id="2ab5b-172">수동으로 이미지를 빌드하는 것은 새로운 기능을 실험하고 살펴보는 데 좋은 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-172">Building an image manually is a great way to experiment and explore new features.</span></span> <span data-ttu-id="2ab5b-173">하지만 프로세스를 팀과 공유하거나 반복하려고 하는 경우를 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-173">But say you want to share the process with your team or make it repeatable.</span></span> <span data-ttu-id="2ab5b-174">예를 들어, 매일 저녁에 팀이 개발 중인 소프트웨어의 최신 버전을 실행하는 새 이미지를 만들려고 한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-174">For example, say you want to create a new image each evening that runs the latest version of the software your team is building.</span></span>

<span data-ttu-id="2ab5b-175">이때 Dockerfile이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-175">That's where the Dockerfile comes in.</span></span> <span data-ttu-id="2ab5b-176">Dockerfile은 수동으로 수행할 뻔한 지침을 설명하는 방법으로 생각하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-176">Think of a Dockerfile as a way to describe instructions you would otherwise do manually.</span></span>

1. <span data-ttu-id="2ab5b-177">Linux VM에서 Python 프로그램을 실행하는 Dockerfile을 만들려면 이 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-177">From your Linux VM, run this command to create a Dockerfile that runs your Python program.</span></span>

    ```bash
    cat << EOF > Dockerfile
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    EOF
    ```

    <span data-ttu-id="2ab5b-178">이 예는 파일을 만드는 간단한 방법일 뿐입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-178">This example is just an easy way for you to create the file.</span></span> <span data-ttu-id="2ab5b-179">실제로는 자주 사용하는 코드 편집기를 사용하여 파일을 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-179">In practice, you would use your favorite code editor to create it.</span></span>

    <span data-ttu-id="2ab5b-180">콘솔에 Dockerfile을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-180">Print your Dockerfile to the console.</span></span>

    ```bash
    cat Dockerfile
    ```

    <span data-ttu-id="2ab5b-181">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-181">You see this.</span></span>

    ```output
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    ```

    <span data-ttu-id="2ab5b-182">Dockerfile에서 수행하는 작업을 분석해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-182">Let's break down what the Dockerfile does.</span></span>

    * <span data-ttu-id="2ab5b-183">`FROM`은 이 이미지의 기반이 될 부모 이미지를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-183">`FROM` specifies the parent image to base this image on.</span></span> <span data-ttu-id="2ab5b-184">여기서 부모 이미지는 **python**입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-184">Here, the parent image is **python**.</span></span>
    * <span data-ttu-id="2ab5b-185">`WORKDIR`은 Dockerfile의 뒷부분에 표시되는 `RUN` 및 `CMD` 문의 작업 디렉터리를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-185">`WORKDIR` specifies the working directory for any `RUN` and `CMD` statements that appear later in the Dockerfile.</span></span> <span data-ttu-id="2ab5b-186">Docker는 이러한 디렉터리를 자동으로 생성합니다(이 경우 `./app`).</span><span class="sxs-lookup"><span data-stu-id="2ab5b-186">Docker creates this directory for you, in this case, `./app`.</span></span>
    * <span data-ttu-id="2ab5b-187">`RUN`은 컨테이너에서 실행할 명령을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-187">`RUN` specifies a command to run in the container.</span></span> <span data-ttu-id="2ab5b-188">`RUN`은 소프트웨어를 설치하고, 구성을 변경하고, 컨테이너를 캡처하기 전에 정리하는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-188">You can use `RUN` to install software, make configuration changes, and cleanup the container before it's captured.</span></span> <span data-ttu-id="2ab5b-189">여기에서는 기본 Python 프로그램을 `./app/hello.py`로 작성합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-189">Here, we write a basic Python program to `./app/hello.py`.</span></span>
    * <span data-ttu-id="2ab5b-190">`CMD`는 컨테이너가 시작될 때 실행할 명령을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-190">`CMD` specifies the process to run when the container starts.</span></span> <span data-ttu-id="2ab5b-191">여기에서는 `/.app` 디렉터리에서 `python hello.py`를 실행했습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-191">Here, we run `python hello.py` from the `/.app` directory.</span></span>

    <span data-ttu-id="2ab5b-192">이미지를 수동으로 빌드할 때와 거의 똑같은 단계임을 눈치채신 분도 있을 것입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-192">You've probably noticed that these are nearly the exact same steps you took to build the image manually.</span></span> <span data-ttu-id="2ab5b-193">이 단계를 코드로 표현하면 프로세스를 더 쉽게 공유하고 반복할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-193">Expressing these steps as code makes the process easier to share and repeat.</span></span>

1. <span data-ttu-id="2ab5b-194">Dockerfile에 지정된 지침에 따라 `docker build`를 실행하여 이미지를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-194">Run `docker build` to create the image, using the instructions specified in the Dockerfile.</span></span>

    ```bash
    docker build -t python-dockerfile .
    ```

    <span data-ttu-id="2ab5b-195">일반적으로 Docker가 이미지를 빌드하기까지 몇 초밖에 걸리지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-195">It will typically take only a few seconds for Docker to build your image.</span></span>

    <span data-ttu-id="2ab5b-196">다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-196">You see output like the following.</span></span>

    ```output
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

1. <span data-ttu-id="2ab5b-197">`docker images`를 사용하여 이미지를 나열합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-197">Use the `docker images` to list your images.</span></span>

    ```bash
    docker images
    ```

    <span data-ttu-id="2ab5b-198">방금 전에 빌드한 **python-dockerfile** 이미지가 보입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-198">You see the **python-dockerfile** image you just built.</span></span>

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-dockerfile   latest              8ed5f85c5e5b        24 seconds ago      923MB
    python-custom       latest              6789cbe2cceb        4 minutes ago       923MB
    python              latest              a9d071760c82        2 weeks ago         923MB
    ```

1. <span data-ttu-id="2ab5b-199">`docker run`을 사용하여 컨테이너를 테스트해 봅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-199">Use `docker run` to test out your container.</span></span>

    ```bash
    docker run python-dockerfile
    ```

    <span data-ttu-id="2ab5b-200">다음이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-200">You see this.</span></span>

    ```output
    Hello World!
    ```

    <span data-ttu-id="2ab5b-201">수동으로 만든 이미지를 테스트할 때와 달리 여기에서는 실행할 명령 `python app/hello.py`를 지정하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-201">Unlike when you tested the image you created manually, here you don't specify the command to run, `python app/hello.py`.</span></span> <span data-ttu-id="2ab5b-202">Dockerfile에서 이를 지정하므로 이미지에 명령이 기본 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-202">Your Dockerfile specifies that, so the command is built into the image.</span></span>

## <a name="publish-your-image-to-docker-hub"></a><span data-ttu-id="2ab5b-203">Docker 허브에 Docker 이미지 게시</span><span class="sxs-lookup"><span data-stu-id="2ab5b-203">Publish your image to Docker Hub</span></span>

<span data-ttu-id="2ab5b-204">Docker 허브에 이미지를 게시하려면 계정이 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-204">To publish an image to Docker Hub, you need an account.</span></span> <span data-ttu-id="2ab5b-205">여기에서는 Docker 허브 계정을 설정하고 **python-dockerfile** 이미지를 Docker 허브에 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-205">Here you'll set up your Docker Hub account and publish your **python-dockerfile** image to Docker Hub.</span></span>

1. <span data-ttu-id="2ab5b-206">[Docker 허브 계정을 생성](https://hub.docker.com?azure-portal=true)합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-206">[Create your Docker Hub account](https://hub.docker.com?azure-portal=true).</span></span>

1. <span data-ttu-id="2ab5b-207">Docker 허브 계정 이름을 환경 변수로 내보냅니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-207">Export your Docker Hub account name as an environment variable.</span></span> <span data-ttu-id="2ab5b-208">**account-name**을 사용자의 계정 이름으로 바꾸세요.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-208">Replace **account-name** with your account name.</span></span>

    ```bash
    export docker_account=account-name
    ```

    <span data-ttu-id="2ab5b-209">이 환경 변수를 통해 다음에 나오는 명령을 더 쉽게 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-209">This environment variable will make it easier for you to run the commands that follow.</span></span>

1. <span data-ttu-id="2ab5b-210">`docker tag`를 실행하여 이미지에 Docker Hub 계정 이름을 태그합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-210">Run `docker tag` to tag your image with your Docker Hub account name.</span></span>

    ```bash
    docker tag python-dockerfile $docker_account/python-dockerfile
    ```

1. <span data-ttu-id="2ab5b-211">`docker login`을 실행하여 Docker 허브에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-211">Run `docker login` to log in to Docker Hub.</span></span>

    ```bash
    docker login
    ```

    <span data-ttu-id="2ab5b-212">메시지가 표시되면 사용자 이름 및 암호를 입력합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-212">When prompted, enter your username and password.</span></span>

1. <span data-ttu-id="2ab5b-213">`docker push`를 실행하여 **python-dockerfile** 이미지를 Docker 허브에 게시하거나 업로드합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-213">Run `docker push` to push, or upload, your **python-dockerfile** image to Docker Hub.</span></span>

    ```bash
    docker push $docker_account/python-dockerfile
    ```

    <span data-ttu-id="2ab5b-214">그러면 다음과 같은 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-214">You see output similar to the following:</span></span>

    ```output
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
    latest: digest: sha256:b816c32382d06ac74530d56f2a7b83000c86174218f430c6bb5039fdcfba38aa size: 2631
    ```

    <span data-ttu-id="2ab5b-215">이제 Docker 이미지가 Docker 허브에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-215">Your Docker image is now stored in Docker Hub.</span></span> <span data-ttu-id="2ab5b-216">다른 컴퓨터에서 `docker pull` 또는 `docker run`을 사용하여 Docker 허브의 이미지를 다운로드하거나 실행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-216">You can use `docker pull` or `docker run` from another computer to download or run your image from Docker Hub.</span></span> <span data-ttu-id="2ab5b-217">다음은 두 가지 예입니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-217">Here are two examples:</span></span>

    1. <span data-ttu-id="2ab5b-218">이 예에서는 Docker 허브에서 최신 이미지를 끌어옵니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-218">This example pulls the latest image from Docker Hub.</span></span>

        ```bash
        docker pull $docker_account/python-dockerfile
        ```

    1. <span data-ttu-id="2ab5b-219">이 예에서는 컨테이너를 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-219">This example runs the container.</span></span>

        ```bash
        docker run $docker_account/python-dockerfile
        ```

1. <span data-ttu-id="2ab5b-220">컨테이너를 테스트해 보세요.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-220">Test out your container.</span></span>

    <span data-ttu-id="2ab5b-221">[Docker 허브 계정](https://hub.docker.com?azure-portal=true)으로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-221">Navigate to [your Docker Hub account](https://hub.docker.com?azure-portal=true).</span></span> <span data-ttu-id="2ab5b-222">**리포지토리** 탭에 Docker 이미지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="2ab5b-222">From the **Repositories** tab, you see your Docker image.</span></span>

    ![Docker 허브의 Docker 이미지](../media/4-docker-hub-python-dockerfile.png)
