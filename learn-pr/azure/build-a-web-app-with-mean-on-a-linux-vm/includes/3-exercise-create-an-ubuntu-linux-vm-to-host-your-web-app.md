<span data-ttu-id="becce-101">구성 요소의 MEAN 스택에는 서버가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-101">The MEAN stack of components requires a server.</span></span> <span data-ttu-id="becce-102">사용자 고유의 서버실에서 실행 중인 가상 머신 또는 Linux 머신일 수 있으며 클라우드 기반 가상 머신에서 구성될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-102">It could be a Linux machine or virtual machine running in your own server room, or it can be configured on a cloud-based virtual machine.</span></span> <span data-ttu-id="becce-103">이 모듈에서는 Azure에서 실행 중인 Ubuntu Linux 가상 머신에서 실행할 스택을 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-103">In this module, we will set up the stack to run on an Ubuntu Linux virtual machine running on Azure.</span></span>

<span data-ttu-id="becce-104">이 단원에서는 Azure에 호스트되는 새로운 Ubuntu Linux 가상 머신을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="becce-104">In this unit, you will be creating a new Ubuntu Linux virtual machine hosted on Azure.</span></span> <span data-ttu-id="becce-105">또한 기존 가상 머신 또는 물리적 호스트 머신에서 MEAN 스택 구성 요소를 설치할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-105">You could also install your MEAN stack components on an existing virtual machine or physical host machine.</span></span> <span data-ttu-id="becce-106">이 연습으로 새 항목을 작성하면 모든 구성 요소를 Azure 리소스 그룹에 연결하여 연습을 완료한 후 관리 및 정리를 쉽게 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-106">By creating a new one with this exercise, you can tie together all the components into an Azure resource group for easier management and clean-up after you complete the exercises.</span></span>

## <a name="provision-an-ubuntu-linux-vm"></a><span data-ttu-id="becce-107">Ubuntu Linux VM 프로비전</span><span class="sxs-lookup"><span data-stu-id="becce-107">Provision an Ubuntu Linux VM</span></span>

[!include[](../../../includes/azure-sandbox-activate.md)]

### <a name="creating-a-resource-group"></a><span data-ttu-id="becce-108">리소스 그룹을 만들기</span><span class="sxs-lookup"><span data-stu-id="becce-108">Creating a resource group</span></span>

<span data-ttu-id="becce-109">일반적으로 새 리소스 집합을 만들 때 가장 먼저 할일은 _리소스 그룹_을 만들어 모든 리소스를 소유하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="becce-109">Normally, the first thing you'll do when creating a new set of resources is create a _resource group_ to own them all.</span></span> <span data-ttu-id="becce-110">이 작업은 Azure 샌드박스에서 불필요한 단계일 수 있지만 사용자 고유의 구독에서 작업할 경우에는 다음 명령을 사용하여 사용자에게 가까운 위치에 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="becce-110">This is an unnecessary step in the Azure sandbox, but when you are working in your own subscription use the following command to create a resource group in a location near you.</span></span>

```azurecli
az group create --name <resource-group-name> --location <resource-group-location>
```

> [!IMPORTANT]
> <span data-ttu-id="becce-111">Azure 샌드박스를 사용하여 리소스 그룹을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-111">You do not need to create a resource group with the Azure sandbox.</span></span> <span data-ttu-id="becce-112">대신, **<rgn>[샌드박스 리소스 그룹]</rgn>** 이라는 미리 생성된 리소스 그룹을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-112">Instead use the pre-created resource group named **<rgn>[sandbox Resource Group]</rgn>**.</span></span>

1. <span data-ttu-id="becce-113">오른쪽에 있는 Cloud Shell에 다음 명령을 입력하여 새 Ubuntu Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="becce-113">In the Cloud Shell on the right, type the following command to create a new Ubuntu Linux VM.</span></span> <span data-ttu-id="becce-114">`<vm-admin-username>` 및 `<vm-admin-password>`를 기본 설정된 관리자 사용자 이름 및 암호로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="becce-114">Substitute your preferred admin username and password for `<vm-admin-username>` and `<vm-admin-password>`.</span></span>

    ```azurecli
    az vm create \
        --resource-group <rgn>[sandbox resource group name]</rgn> \
        --name MeanDemo \
        --image UbuntuLTS \
        --admin-username <vm-admin-username> \
        --admin-password <vm-admin-password> \
        --generate-ssh-keys
    ```

    <span data-ttu-id="becce-115">나중에 이 VM에 연결할 수 있도록 관리자 사용자 이름과 암호를 기록해 두세요.</span><span class="sxs-lookup"><span data-stu-id="becce-115">Take note of your admin username and password to allow you to connect to this VM later.</span></span>

    <span data-ttu-id="becce-116">이 명령은 완료되는 데 약 2분 정도 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="becce-116">This command takes about two minutes to complete.</span></span> <span data-ttu-id="becce-117">명령이 완료되면 결과 출력은 다음과 유사합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-117">When the command finishes, the resulting output will look similar to this.</span></span>

    ```json
    {
        "fqdns": "",
        "id": "...",
        "location": "<resource group location>",
        "macAddress": "00-0D-3A-3A-54-EC",
        "powerState": "VM running",
        "privateIpAddress": "10.0.0.4",
        "publicIpAddress": "<the public IP address of the newly created machine>",
        "resourceGroup": "<rgn>[sandbox resource group name]</rgn>",
        "zones": ""
    }
    ```

    <span data-ttu-id="becce-118">또한 VM에 연결하기 위해 새로 생성된 VM의 공용 IP 주소도 저장하려고 합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-118">You will also want to save the public IP address of the newly created VM in order to connect to the VM.</span></span>

1. <span data-ttu-id="becce-119">새 VM에 연결을 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="becce-119">Try connecting to your new VM.</span></span>

    <span data-ttu-id="becce-120">Cloud Shell에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="becce-120">From the Cloud Shell, run the following command.</span></span> <span data-ttu-id="becce-121">`<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공개 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="becce-121">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

    <span data-ttu-id="becce-122">처음 머신에 연결할 때 원격 머신을 신뢰하는지 묻는 메시지가 나타납니다.</span><span class="sxs-lookup"><span data-stu-id="becce-122">The first time you connect to the machine, you'll be asked if you trust the remote machine.</span></span> <span data-ttu-id="becce-123">`yes`로 응답하면 머신의 ECDSA 키 지문이 로컬에 저장되어 후속 연결을 신뢰하게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="becce-123">By answering `yes`, the machine's ECDSA key fingerprint will be saved locally, so subsequent connections will be trusted.</span></span> <span data-ttu-id="becce-124">그러면 연결할 때마다 암호를 확인하는 메시지가 표시되는 것을 보게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="becce-124">You'll then be prompted for your password, which you'll see every time you connect.</span></span>

    <span data-ttu-id="becce-125">모든 항목이 문제없으면 `exit`를 입력하여 SSH 세션을 닫습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-125">If everything looks fine, type `exit` to close the SSH session.</span></span>

1. <span data-ttu-id="becce-126">새로 만들 웹 응용 프로그램에 들어오는 HTTP 트래픽을 허용하도록 VM에서 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="becce-126">Open port 80 on the VM to allow incoming HTTP traffic to the new web application that you will create.</span></span>

    ```azurecli
    az vm open-port --port 80 --resource-group <rgn>[sandbox resource group name]</rgn> --name MeanDemo
    ```

    <span data-ttu-id="becce-127">이 명령은 생성될 때 "MeanDemo"라는 이름이 지정된 VM에서 HTTP 포트를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="becce-127">This command will open up the HTTP port on your VM that was named "MeanDemo" when it was created.</span></span>

## <a name="summary"></a><span data-ttu-id="becce-128">요약</span><span class="sxs-lookup"><span data-stu-id="becce-128">Summary</span></span>

<span data-ttu-id="becce-129">새로운 Ubuntu Linux VM을 사용할 준비가 되었으므로 이제 이를 연결하여 MEAN 스택의 다양한 구성 요소를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="becce-129">With your new Ubuntu Linux VM ready to go, we can now connect to it to start installing the various components of the MEAN stack.</span></span>