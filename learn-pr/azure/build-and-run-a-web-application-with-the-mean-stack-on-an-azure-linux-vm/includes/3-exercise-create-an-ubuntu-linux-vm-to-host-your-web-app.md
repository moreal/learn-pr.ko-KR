<span data-ttu-id="26ec9-101">구성 요소의 MEAN 스택에는 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="26ec9-102">사용자 고유의 서버실에서 실행 중인 가상 머신 또는 Linux 머신일 수 있으며 클라우드 기반 가상 머신에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="26ec9-103">이 모듈에서는 Azure에서 실행 중인 Ubuntu Linux 가상 머신에서 실행할 스택을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-103">In this module, we will set up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="26ec9-104">이 연습에서는 Azure에 호스트되는 새로운 Ubuntu Linux 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-104">In this exercise, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="26ec9-105">또한 기존 가상 머신 또는 물리적 호스트 머신에서 MEAN 스택 구성 요소를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="26ec9-106">이 연습으로 새 항목을 작성하면 모든 구성 요소를 Azure 리소스 그룹에 연결하여 연습을 완료한 후 관리 및 정리를 쉽게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

<span data-ttu-id="26ec9-107">Azure Portal에 통합된 Cloud Shell 명령줄을 사용하여 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-107">We will use the Cloud Shell command line that's integrated into the Azure portal to create the Linux VM.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="26ec9-108">Ubuntu Linux VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="26ec9-108">Provision an Ubuntu Linux VM</span></span>

1. <span data-ttu-id="26ec9-109">[Azure Portal](https://portal.azure.com?azure-portal=true)로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-109">Go to the [Azure portal](https://portal.azure.com?azure-portal=true).</span></span>
1. <span data-ttu-id="26ec9-110">Azure Portal 도구 모음의 꺾쇠괄호(>_) 아이콘에서 Cloud Shell을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-110">Open Cloud Shell from the angle bracket (>_) icon in the Azure portal toolbar.</span></span>
1. <span data-ttu-id="26ec9-111">Cloud Shell에서 해당 명령을 실행하여 VM을 포함할 Azure 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-111">In Cloud Shell, execute the command to create an Azure resource group, which will include our VM.</span></span> <span data-ttu-id="26ec9-112">`<resource-group-name>`을 사용자 고유의 리소스 그룹 이름으로, `<resource-group-location>`을 원하는 Azure 위치(예: `westus`)로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-112">Substitute your own resource group name for `<resource-group-name>` and your desired Azure location for `<resource-group-location>` (`westus`, for example).</span></span>


    ```bash
    az group create --name <resource-group-name> --location <resource-group-location>
    ```

    <span data-ttu-id="26ec9-113">다른 명령에서 사용할 수 있으므로 리소스 그룹 이름을 기억하세요.</span><span class="sxs-lookup"><span data-stu-id="26ec9-113">Remember your resource group name as we will use it in other commands.</span></span>

1. <span data-ttu-id="26ec9-114">Cloud Shell에서 다음 명령을 실행하여 새로운 Ubuntu Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-114">In Cloud Shell, run the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="26ec9-115">`<resource-group-name>`을 사용자 고유의 리소스 그룹 이름으로, `<vm-admin-username>` 및 `<vm-admin-password>`를 기본 설정된 관리자 사용자 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-115">Substitute your own resource group name for `<resource-group-name>` and your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```bash
    az vm create \
        --resource-group <resource-group-name> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="26ec9-116">나중에 이 VM에 연결할 수 있도록 관리자 사용자 이름과 암호를 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="26ec9-116">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="26ec9-117">이 명령은 완료되는 데 약 2분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-117">This command takes about two minutes to complete.</span></span> <span data-ttu-id="26ec9-118">명령이 완료되면 결과 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-118">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<location you chose for the resource group>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<name you chose for thr resource group>",
        "zones": ""
    }
    ```

    <span data-ttu-id="26ec9-119">또한 VM에 연결하기 위해 새로 생성된 VM의 공용 IP 주소도 저장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-119">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="26ec9-120">새 VM에 연결을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="26ec9-120">Try connecting to your new VM.</span></span>

    <span data-ttu-id="26ec9-121">명령 프롬프트/터미널 창을 열고 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-121">Open a command prompt/terminal window and run the following command.</span></span> <span data-ttu-id="26ec9-122">`<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공개 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-122">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="26ec9-123">처음 머신에 연결할 때 원격 머신을 신뢰하는지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-123">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="26ec9-124">`yes`로 응답하면 머신의 ECDSA 키 지문이 로컬에 저장되어 후속 연결을 신뢰하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-124">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally, so subsequent connections will be trusted.</span></span>

    <span data-ttu-id="26ec9-125">문제 없이 모든 항목이 진행되면 `exit`를 입력하여 SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="26ec9-126">새로 만들 웹 응용 프로그램에 들어오는 HTTP 트래픽을 허용하도록 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-126">Open port 80 to allow incoming HTTP traffic to your new web application that you will create.</span></span>

    <span data-ttu-id="26ec9-127">Azure Portal에서 Cloud Shell로 돌아갑니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-127">Go back to Cloud Shell on the Azure portal.</span></span> <span data-ttu-id="26ec9-128">`<resource-group-name>`의 원래 리소스 그룹 이름을 사용하여 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-128">Issue the following command using your original resource group name for `<resource-group-name>`.</span></span>

    ``` bash
    az vm open-port --port 80 --resource-group <resource-group-name> --name MeanDemo
    ```

    <span data-ttu-id="26ec9-129">이 명령은 생성될 때 "MeanDemo"라는 이름이 지정된 VM에서 HTTP 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-129">This command will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="26ec9-130">요약</span><span class="sxs-lookup"><span data-stu-id="26ec9-130">Summary</span></span>

<span data-ttu-id="26ec9-131">새로운 Ubuntu Linux VM을 사용할 준비가 되었으므로 이제 이를 연결하여 MEAN 스택의 다양한 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="26ec9-131">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>