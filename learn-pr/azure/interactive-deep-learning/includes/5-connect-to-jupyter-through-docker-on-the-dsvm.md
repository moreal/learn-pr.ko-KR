<span data-ttu-id="9de6f-101">Data Science Virtual Machine을 실행했으므로 첫 번째 딥 러닝 모델을 학습하기로 합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-101">Now that you have your Data Science Virtual Machine up and running, you decide to train your first deep learning model.</span></span> <span data-ttu-id="9de6f-102">서버의 다른 모든 항목과 격리된 상태에서 실험을 실행하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-102">You want to run your experiments in isolation from everything else on your server.</span></span> <span data-ttu-id="9de6f-103">그렇게 하려면 Docker 컨테이너 내에서 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-103">To do that, you run them within a Docker container.</span></span>

## <a name="connect-to-the-vm-with-ssh"></a><span data-ttu-id="9de6f-104">ssh로 VM에 연결하기</span><span class="sxs-lookup"><span data-stu-id="9de6f-104">Connect to the VM with ssh</span></span>

<span data-ttu-id="9de6f-105">ssh를 통해 VM에 계속 연결되어 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-105">Make sure you're still connected to your VM through ssh.</span></span> <span data-ttu-id="9de6f-106">그렇지 않다면 이 명령을 다시 실행하여 가상 머신에 원격으로 되돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-106">If not, just run this command again to remote back into the virtual machine.</span></span>

1. <span data-ttu-id="9de6f-107">Azure Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-107">Execute the following command in Azure Cloud Shell to sign into the VM.</span></span>

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    <span data-ttu-id="9de6f-108">VM을 만들 때 정의한 관리자 계정 이름으로 `<USERNAME>`을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-108">Replace  `<USERNAME>` with the admin account name you defined when creating the VM.</span></span> <span data-ttu-id="9de6f-109">이전 연습에서 저장한 VM의 IP 주소로 `<IP>`을 대체합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-109">Replace `<IP>` with the IP address of the VM you saved in the preceding exercise.</span></span>  

1. <span data-ttu-id="9de6f-110">메시지가 표시되면 관리자 계정의 암호를 입력하여 로그인 프로세스를 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-110">When prompted, enter your password for the admin account to complete the sign-in process.</span></span>

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a><span data-ttu-id="9de6f-111">VM의 Docker 컨테이너에서 Jupyter Notebook 서버 실행하기</span><span class="sxs-lookup"><span data-stu-id="9de6f-111">Run a Jupyter Notebook server in a Docker container in the VM</span></span>

> [!NOTE]
> <span data-ttu-id="9de6f-112">VM에 하나의 관리자 계정, 즉 루트 계정만 가지고 있기 때문에 `sudo`을 사용하여 모든 Docker 명령을 루트로서 실행해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-112">Since we only have an admin, or root, account on our VM, we have to run all Docker commands as root using `sudo`</span></span>

1. <span data-ttu-id="9de6f-113">VM에 어떤 Docker 컨테이너가 있는지 확인하려면 명령 프롬프트에서 다음의 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-113">To see what Docker containers exist on the VM, run the following command at the command prompt.</span></span>

    ```azurecli 
    sudo docker ps
    ```

1. <span data-ttu-id="9de6f-114">명령 프롬프트에서 다음의 명령을 실행하여 실험을 위한 새 컨테이너를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-114">Run the following command at the command prompt to create a new container for our experiments.</span></span>

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    <span data-ttu-id="9de6f-115">이 명령은 꽤 오래 실행됩니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-115">This command will run for quite a while.</span></span> <span data-ttu-id="9de6f-116">따라서 명령이 무엇을 하는지 잠시 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-116">So, while we have some time, let's discuss what the command does.</span></span> 
    - <span data-ttu-id="9de6f-117">`docker run`은 새 컨테이너에서 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-117">`docker run` runs a command in a new container.</span></span> <span data-ttu-id="9de6f-118">사용되는 Docker 이미지는 pytorch/pytorch입니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-118">The Docker image being used is pytorch/pytorch.</span></span> <span data-ttu-id="9de6f-119">이것은 먼저 지정된 이미지 위에 쓰기가 가능한 컨테이너 계층을 만든 다음, 지정된 명령을 사용하여 그것을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-119">It first creates a writeable container layer over the specified image, and then starts it using the specified command.</span></span>
    - <span data-ttu-id="9de6f-120">`--rm`이 종료되면 컨테이너가 제거됩니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-120">`--rm` will remove the container once it exits.</span></span> <span data-ttu-id="9de6f-121">관련 컨테이너를 유지하려면 이 인수를 드롭합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-121">If you want to keep the container around, drop this argument.</span></span> 
    - <span data-ttu-id="9de6f-122">`--entrypoint 'bin/sh'`은 이미지의 기본 진입점을 덮어써서 Bash shell이 됩니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-122">`--entrypoint 'bin/sh'` overwrites the default entry point of the image to be the Bash shell</span></span>
    - <span data-ttu-id="9de6f-123">`-c`은 컨테이너를 시작할 때 실행하는 명령을 정의합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-123">`-c` defines what command to run when the container starts.</span></span> <span data-ttu-id="9de6f-124">이 경우, 세 가지 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-124">In this case, it's running three commands:</span></span>
        - <span data-ttu-id="9de6f-125">Jupyter 및 matplotlib 설치하기</span><span class="sxs-lookup"><span data-stu-id="9de6f-125">Installs Jupyter and matplotlib</span></span>
        - <span data-ttu-id="9de6f-126">pytorch.org에서 `first_pytorch_classifier.ipynb`로 호출된 컨테이너의 파일로 노트북(cifar10_tutorial.ipynb) 복사하기</span><span class="sxs-lookup"><span data-stu-id="9de6f-126">Copies a notebook (cifar10_tutorial.ipynb) from pytorch.org to a file in the container called `first_pytorch_classifier.ipynb`</span></span>
        - <span data-ttu-id="9de6f-127">이전의 연습과 동일한 방식으로 컨테이너에서 노트북 서버를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-127">Starts the notebook server in the container in the same way as the preceding exercise.</span></span>  <span data-ttu-id="9de6f-128">브라우저가 시작되는 것이 아니라, 노트북이 루트에 의해 액세스되고 모든 포트에 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-128">No browser is started, allow the notebook to be accessed by root and listen on all ports.</span></span> 
    
    <span data-ttu-id="9de6f-129">노트북 서버는 그 컨테이너의 모든 포트에 수신 대기합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-129">The notebook server listens on all ports for that container.</span></span> <span data-ttu-id="9de6f-130">하지만 어떻게 트래픽이 컨테이너 외부에서 들어올까요?</span><span class="sxs-lookup"><span data-stu-id="9de6f-130">But, how will traffic come from outside the container?</span></span> <span data-ttu-id="9de6f-131">호스트 머신에서 TCP 포트 8888로 컨테이너의 `-p 8888:8888` 포트를 인수가 바인딩합니다 `8888`.</span><span class="sxs-lookup"><span data-stu-id="9de6f-131">The `-p 8888:8888` argument binds port `8888` of the container to TCP port 8888 on the host machine.</span></span> <span data-ttu-id="9de6f-132">따라서 포트 8888을 통해 VM에 들어오는 트래픽은 컨테이너에 의해 선택됩니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-132">So, traffic coming to the VM over port 8888 will be picked up by the container.</span></span> 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a><span data-ttu-id="9de6f-133">원격 브라우저에서 Jupyter Notebook 서버에 연결하기</span><span class="sxs-lookup"><span data-stu-id="9de6f-133">Connect to the Jupyter Notebook server from a remote browser</span></span> 

<span data-ttu-id="9de6f-134">컨테이너에서 Jupyter Notebook이 실행되면 다음의 메시지와 유사한 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-134">Once the Jupyter notebook is running in the container, you'll  see a message similar to the following message.</span></span> 

> <span data-ttu-id="9de6f-135">*처음으로 연결할 때 토큰을 사용하여 로그인하려면 http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken} URL을 복사하여 브라우저에 붙여넣습니다.*</span><span class="sxs-lookup"><span data-stu-id="9de6f-135">*Copy/paste this URL into your browser when you connect for the first time, to login with a token: http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken}*</span></span>

1. <span data-ttu-id="9de6f-136">URL의 **http://(5b8783e7911d or 127.0.0.1)** 부분을 `<HOSTNAME>.<REGION>.cloudapp.azure.com`이나 VM의 IP로 바꾸고 브라우저의 새 탭에서 그 주소로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-136">Replace the **http://(5b8783e7911d or 127.0.0.1)** part of the URL with `<HOSTNAME>.<REGION>.cloudapp.azure.com` or the IP address of the VM and navigate to the address  in a new a tab of your browser.</span></span>

    ![<span data-ttu-id="9de6f-137">Jupyter Notebook 대시보드를 보여주는 스크린샷입니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-137">Screenshot showing Jupyter Notebooks dashboard.</span></span> ](../media/notebook-in-docker.png)
    
    <span data-ttu-id="9de6f-138">이번에는 단일 노트북만 보입니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-138">This time we only see a single notebook.</span></span> <span data-ttu-id="9de6f-139">사용자가 컨테이너 안에 있으며 이 노트북만 복사했기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-139">That's because we're in a container and only copied down this notebook.</span></span> <span data-ttu-id="9de6f-140">다음 연습에서는 이 노트북을 사용하여 실험합니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-140">In the next exercise, we'll experiment with this notebook.</span></span> 
    
    > [!TIP]
    > <span data-ttu-id="9de6f-141">아직 노트북 서버를 종료하지 마십시오.</span><span class="sxs-lookup"><span data-stu-id="9de6f-141">Don't shut down the notebook server just yet.</span></span> <span data-ttu-id="9de6f-142">다음 연습에서 `first_pytorch_classifier.ipynb` 노트북을 살펴보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="9de6f-142">We'll look at the `first_pytorch_classifier.ipynb` notebook in the next exercise.</span></span>