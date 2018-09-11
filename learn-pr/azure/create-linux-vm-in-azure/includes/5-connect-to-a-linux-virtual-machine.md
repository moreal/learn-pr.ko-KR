<span data-ttu-id="48fc2-101">Azure에 Linux VM이 준비되었으면, 다음으로 진행할 작업은 Azure로 옮기려는 작업 맞게 VM을 구성하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-101">Now that we have a Linux VM in Azure, the next thing you’ll want to do is configure it for the tasks we want to move to Azure.</span></span>

<span data-ttu-id="48fc2-102">사이트 간 VPN을 Azure로 설정하지 않았다면 로컬 네트워크에서 Azure VM에 액세스할 수 없습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-102">Unless you’ve set up a site-to-site VPN to Azure, your Azure VMs won’t be accessible from your local network.</span></span> <span data-ttu-id="48fc2-103">Azure 사용을 처음 시작하는 경우에는 작동 중인 사이트 간 VPN이 없을 가능성이 높습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-103">If you’re just getting started with Azure, it’s unlikely that you have a working site-to-site VPN.</span></span> <span data-ttu-id="48fc2-104">그러면 가상 머신에 어떻게 연결할 수 있을까요?</span><span class="sxs-lookup"><span data-stu-id="48fc2-104">So how can you connect to the virtual machine?</span></span>

## <a name="azure-vm-ip-addresses"></a><span data-ttu-id="48fc2-105">Azure VM IP 주소</span><span class="sxs-lookup"><span data-stu-id="48fc2-105">Azure VM IP addresses</span></span>

<span data-ttu-id="48fc2-106">조금 전에 봤듯이 Azure VM은 가상 네트워크에서 통신합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-106">As we saw a moment ago, Azure VMs communicate on a virtual network.</span></span> <span data-ttu-id="48fc2-107">또한 선택적인 공용 IP 주소가 할당되어 있을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-107">They can also have an optional public IP address assigned to them.</span></span> <span data-ttu-id="48fc2-108">공용 IP가 있으면 인터넷을 통해 VM과 상호 작용이 가능합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-108">With a public IP, we can interact with the VM over the Internet.</span></span> <span data-ttu-id="48fc2-109">온-프레미스 네트워크를 Azure에 연결하는 VPN(가상 사설망)을 설정할 수도 있습니다. 그러면 공용 IP를 노출시키지 않고 VM에 안전하게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-109">Alternatively, we can set up a virtual private network (VPN) that connects our on-premises network to Azure - letting us securely connect to the VM without exposing a public IP.</span></span> <span data-ttu-id="48fc2-110">이 방식은 다른 모듈에 설명되어 있으며, 해당 옵션에 관심이 있는 사용자를 위해 전체 설명이 문서로 작성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-110">This approach is covered in another module and is fully documented if you are interested in exploring that option.</span></span>

<span data-ttu-id="48fc2-111">Azure의 공용 IP 주소에 대해 알고 있어야하는 사항은, 동적으로 할당되는 경우가 많다는 점입니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-111">One thing to be aware of with public IP addresses in Azure is they are often dynamically allocated.</span></span> <span data-ttu-id="48fc2-112">즉, 시간이 지나면 IP 주소가 변경될 수 있습니다. VM의 경우에는 VM을 다시 시작하면 IP 주소가 변경됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-112">That means the IP address can change over time - for VMs this happens when the VM is restarted.</span></span> <span data-ttu-id="48fc2-113">이름 대신 IP 주소에 직접 연결하고 IP 주소가 변경되지 않도록 해야 하는 경우에는 요금을 더 지불하고 고정 주소가 할당되도록 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-113">You can pay more to assign static addresses if you want to connect directly to an IP address instead of a name and need to ensure that the IP address will not change.</span></span>

## <a name="connect-to-an-azure-linux-vm-with-ssh"></a><span data-ttu-id="48fc2-114">SSH로 Azure Linux VM에 연결</span><span class="sxs-lookup"><span data-stu-id="48fc2-114">Connect to an Azure Linux VM with SSH</span></span>

<span data-ttu-id="48fc2-115">SSH를 사용하여 Azure에서 VM에 연결하는 것은 간단합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-115">Connecting to a VM in Azure using SSH is straight forward.</span></span> <span data-ttu-id="48fc2-116">Azure Portal에서 VM 속성을 열고 위쪽의 **연결**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-116">In the Azure portal, open the properties of your VM and at the top, click **Connect**.</span></span> <span data-ttu-id="48fc2-117">그러면 VM에 할당된 IP 주소와 SSH의 모든 로그인 세부 정보가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-117">This will show you the IP addresses assigned to the VM along with all the login details for SSH.</span></span> 

![Linux VM에 대한 SSH 연결 세부 정보](../media-drafts/5-connect-ssh.png)

<span data-ttu-id="48fc2-119">세부 정보가 표시되면 다음 명령을 사용하여 Linux VM에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-119">With these details, we can use the following command to get into our Linux VM:</span></span>

```bash
ssh jim@137.117.101.249
```

<span data-ttu-id="48fc2-120">처음으로 연결하면 SSH는 알려지지 않은 호스트에 대한 인증을 요청합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-120">The first time we connect, SSH will ask us about authenticating against an unknown host.</span></span> <span data-ttu-id="48fc2-121">이 서버에 연결한 적이 없다는 알림도 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-121">SSH is telling you that you've never connected to this server before.</span></span> <span data-ttu-id="48fc2-122">이것이 사실이라면, 지극히 정상적입니다. "예"라고 응답하면 알려진 호스트 파일에 서버의 지문을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-122">If that's true, then it's perfectly normal, and you can respond with "yes" to save the fingerprint of the server off in the known host file.</span></span>

```output
The authenticity of host '137.117.101.249 (137.117.101.249)' can't be established.
ECDSA key fingerprint is SHA256:w1h08h4ie1iMq7ibIVSQM/PhcXFV7O7EEhjEqhPYMWY.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added '137.117.101.249' (ECDSA) to the list of known hosts.
```

## <a name="transferring-files-to-the-vm"></a><span data-ttu-id="48fc2-123">VM으로 파일 전송</span><span class="sxs-lookup"><span data-stu-id="48fc2-123">Transferring files to the VM</span></span>

<span data-ttu-id="48fc2-124">일반적으로 수행하는 또 다른 작업은 로컬 파일 또는 데이터를 서버 간에 복사하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-124">Another common task is to copy local files or data from one server to another.</span></span> <span data-ttu-id="48fc2-125">여기서는 웹 사이트 데이터를 Azure VM에 복사할 것입니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-125">In our case, we'll eventually want to copy our website data up to our Azure VM.</span></span> <span data-ttu-id="48fc2-126">Linux VM과 SSH를 사용하는 경우 `scp` 명령을 사용하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-126">With Linux VMs and SSH, we can use the `scp` command.</span></span> <span data-ttu-id="48fc2-127">이 명령은 `cp`를 사용하여 로컬 파일을 복사하는 방식과 비슷합니다. 단, 명령에 원격 사용자와 호스트를 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-127">The command is similar to copying local files with `cp`, except you'll have to specify the remote user and host in your command.</span></span> 

<span data-ttu-id="48fc2-128">예를 들어 현재 디렉터리의 `somefile.txt`를 IP 주소가 `192.168.1.25`인 Linux 머신의 `~/folder`에 복사하려는 경우 다음 명령을 입력하면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-128">For example, to copy `somefile.txt` from our current directory to `~/folder` on a Linux machine with the IP address `192.168.1.25`, you can type:</span></span>

```bash
scp somefile.txt someuser@192.168.1.25:~/folder/
```

<span data-ttu-id="48fc2-129">그러면 원격 시스템에서 `someuser`로 인증이 진행되어 암호를 입력하라는 메시지가 표시되거나 SSH 개인 키가 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-129">This will authenticate as `someuser` on the remote system, prompting for a password, or using your SSH private key.</span></span> <span data-ttu-id="48fc2-130">해당 사용자는 대상 서버의 `~/folder/`에 대한 쓰기 권한이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-130">That user will need to have write permissions to `~/folder/` on the destination server.</span></span>

> [!WARNING]
> <span data-ttu-id="48fc2-131">명령줄을 올바르게 입력하지 않으면 `scp`는 로컬 파일 복사를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-131">`scp` will do local file copies if you don't get the command line quite right.</span></span> <span data-ttu-id="48fc2-132">가장 자주 빠뜨리는 부분은 대상 폴더입니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-132">The most common missing piece is the destination folder.</span></span>

<span data-ttu-id="48fc2-133">SSH를 사용하여 실행 중인 Linux VM에 연결해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="48fc2-133">Let's try using SSH to connect to our running Linux VM.</span></span>