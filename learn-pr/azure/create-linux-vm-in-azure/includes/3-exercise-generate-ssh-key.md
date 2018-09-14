<span data-ttu-id="669c4-101">Azure에서 Linux 가상 머신을 만들려면 먼저 원격 액세스에 대해 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-101">Before we can create a Linux virtual machine in Azure, we will need to think about remote access.</span></span> <span data-ttu-id="669c4-102">Linux 웹 서버에 로그인하여 소프트웨어를 구성하고 유지 관리를 수행할 수 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-102">We want to be able to sign into our Linux web server to configure the software and perform maintenance.</span></span> <span data-ttu-id="669c4-103">Azure에 호스트되는 Linux VM을 관리하는 기본적인 수단은 SSH입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-103">The default approach to administering Linux VMs hosted in Azure is SSH.</span></span>

## <a name="what-is-ssh"></a><span data-ttu-id="669c4-104">SSH란?</span><span class="sxs-lookup"><span data-stu-id="669c4-104">What is SSH?</span></span>

<span data-ttu-id="669c4-105">SSH(Secure Shell)는 암호화된 연결 프로토콜이며, 보안이 설정되지 않은 연결을 통한 보안 로그인을 허용합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-105">Secure Shell (SSH) is an encrypted connection protocol that allows secure sign-ins over unsecured connections.</span></span> <span data-ttu-id="669c4-106">SSH를 사용하면 네트워크 연결을 사용하여 원격 위치에서 터미널 셸에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-106">SSH allows you to connect to a terminal shell from a remote location using a network connection.</span></span>

<span data-ttu-id="669c4-107">SSH 연결을 인증하는 두 가지 방법은 \*\* 사용자 이름/암호\*\* 또는 **SSH 키 쌍**입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-107">There are two approaches we can use to authenticate an SSH connection: \*\* username/password\*\*, or a **SSH key pair**.</span></span> 

> [!TIP]
> <span data-ttu-id="669c4-108">SSH에서 암호화된 연결을 제공하지만 SSH 연결에 암호를 사용하면 VM이 무차별 암호 대입 공격(brute force attack)이나 암호 추측에 취약해집니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-108">Although SSH provides an encrypted connection, using passwords with SSH connections leaves the VM vulnerable to brute-force attacks or guessing of passwords.</span></span> <span data-ttu-id="669c4-109">SSH를 사용하여 Linux VM에 연결하는 보다 안전하고 널리 사용되는 방법은 공개 키-개인 키 쌍(SSH 키라고도 함)입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-109">A more secure and preferred method of connecting to a Linux VM with SSH is with a public-private key pair, also known as SSH keys.</span></span>

<span data-ttu-id="669c4-110">SSH 키 쌍을 사용하면 Linux 기반 Azure Virtual Machines에 암호 없이 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-110">With an SSH key pair, you can sign in to Linux-based Azure virtual machines without a password.</span></span> <span data-ttu-id="669c4-111">몇 대의 컴퓨터에서만 로그인할 계획이면 이것이 보다 안전한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-111">This is a more secure approach if you only plan to sign into the from a few computers.</span></span> <span data-ttu-id="669c4-112">다양한 위치에서 Linux VM에 액세스할 수 있어야 하는 경우에는 사용자 이름과 암호 조합이 더 좋은 방법일 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-112">If you need to be able to access the Linux VM from a variety of locations, a username and password combination might be a better approach.</span></span> <span data-ttu-id="669c4-113">SSH 키 쌍에는 공개 키와 개인 키라는 두 부분이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-113">There are two parts to an SSH key pair: a public key, and a private key.</span></span>

* <span data-ttu-id="669c4-114">공개 키는 public-key 암호화를 사용하려는 Linux VM 또는 다른 서비스에 배치됩니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-114">The public key is placed on your Linux VM or any other service that you wish to use with public-key cryptography.</span></span> <span data-ttu-id="669c4-115">이 키는 다른 사람과 공유할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-115">This can be shared with anyone.</span></span>

* <span data-ttu-id="669c4-116">개인 키는 사용자가 SSH 연결을 수행할 때 자신의 ID를 확인하기 위해 Linux VM에 제출하는 키입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-116">The private key is what you present to your Linux VM when you make an SSH connection, to verify your identity.</span></span> <span data-ttu-id="669c4-117">이것은 기밀 정보이며 암호나 기타 개인 데이터처럼 보호해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-117">Consider this confidential information and protect this like you would a password or any other private data.</span></span>

<span data-ttu-id="669c4-118">동일한 단일 공개-개인 키 쌍을 사용하여 여러 Azure VM 및 서비스에 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-118">You can use the same single public-private key pair to access multiple Azure VMs and services.</span></span>

## <a name="create-the-ssh-key-pair"></a><span data-ttu-id="669c4-119">SSH 키 쌍 만들기</span><span class="sxs-lookup"><span data-stu-id="669c4-119">Create the SSH key pair</span></span>

<span data-ttu-id="669c4-120">Linux, Windows 10 및 MacOS에서는 기본 제공되는 `ssh-keygen` 명령을 사용하여 공개 키 및 개인 키 파일을 생성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-120">On Linux, Windows 10, and MacOS, you can use the built-in `ssh-keygen` command to generate the SSH public and private key files.</span></span> 

> [!TIP]
> <span data-ttu-id="669c4-121">Windows 10의 경우 **Fall Creators Update**에 SSH 클라이언트가 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-121">Windows 10 includes an SSH client with the **Fall Creators Update**.</span></span> <span data-ttu-id="669c4-122">이전 버전의 Windows에서 SSH를 사용하려면 추가 소프트웨어가 필요합니다. [자세한 내용은 설명서를 참조하세요.](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows) 또는 Windows용 Linux 하위 시스템을 설치하고 동일한 기능을 확보할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-122">Earlier versions of Windows require additional software to use SSH; [check the documentation for full details](https://docs.microsoft.com/azure/virtual-machines/linux/ssh-from-windows) Alternatively, you can install the Linux subsystem for Windows and get the same functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="669c4-123">여기서는 Azure에서 생성된 키를 개인 저장소 계정에 저장하는 Azure Cloud Shell을 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-123">We will use the Azure Cloud Shell which will store the generated keys in Azure in your private storage account.</span></span> <span data-ttu-id="669c4-124">원하는 경우 다음 명령을 로컬 셸에 직접 입력할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-124">You can also type these commands directly into your local shell if you prefer.</span></span> <span data-ttu-id="669c4-125">이 방법을 사용하는 경우에는 로컬 세션을 반영하기 위해 이 모듈 전체에서 지침을 조정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-125">You will need to adjust the instructions throughout this module to reflect a local session if you take this approach.</span></span>

<span data-ttu-id="669c4-126">Azure VM에 대한 키 쌍을 생성하는 데 필요한 최소 명령은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-126">Here is the minimum command necessary to generate the key pair for an Azure VM.</span></span> <span data-ttu-id="669c4-127">이를 통해 2048비트 길이(최소 길이)의 SSH-2(SSH 프로토콜 2) RSA 공개-개인 키 쌍이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-127">This will create an SSH protocol 2 (SSH-2) RSA public-private key pair with a 2048 bit length (the minimum length).</span></span> 

<span data-ttu-id="669c4-128">다음 명령을 Cloud Shell에 입력하세요.</span><span class="sxs-lookup"><span data-stu-id="669c4-128">Type this command into the Cloud Shell.</span></span>

```bash
ssh-keygen -t rsa -b 2048
```

<span data-ttu-id="669c4-129">도구에 파일 이름 및 선택적 암호를 입력하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-129">The tool will prompt for filenames and an optional passphrase.</span></span> <span data-ttu-id="669c4-130">기본값을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-130">Just take the defaults.</span></span> <span data-ttu-id="669c4-131">`~/.ssh` 디렉터리에 `id_rsa` 및 `id_rsa.pub`라는 두 개의 파일이 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-131">It will create two files: `id_rsa` and `id_rsa.pub` in the `~/.ssh` directory.</span></span> <span data-ttu-id="669c4-132">파일이 있으면 덮어씁니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-132">The files are overwritten if they exist.</span></span> <span data-ttu-id="669c4-133">프롬프트를 방지하기 위해 파일 이름이나 암호를 제공하는 데 사용할 수 있는 다양한 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-133">There are various options you can use to provide the filename or a passphrase to avoid the prompt.</span></span>

### <a name="private-key-passphrase"></a><span data-ttu-id="669c4-134">개인 키 암호</span><span class="sxs-lookup"><span data-stu-id="669c4-134">Private key passphrase</span></span>

<span data-ttu-id="669c4-135">개인 키를 생성하는 동안 선택적으로 암호를 입력할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-135">You can optionally provide a passphrase while generating your private key.</span></span> <span data-ttu-id="669c4-136">키를 사용할 때 입력해야 하는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-136">This is a password you must enter when you use the key.</span></span> <span data-ttu-id="669c4-137">이 암호는 개인 SSH 키 파일에 액세스하는 데 사용되며 사용자 계정 암호가 아닙니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-137">This passphrase is used to access the private SSH key file and is not the user account password.</span></span> 

<span data-ttu-id="669c4-138">SSH 키에 암호를 추가하면 128비트 AES를 사용하여 개인 키가 암호화되기 때문에 암호화를 해독할 암호가 없으면 개인 키는 쓸모가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-138">When you add a passphrase to your SSH key, it encrypts the private key using 128-bit AES, so that the private key is useless without the passphrase to decrypt it.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="669c4-139">암호를 추가하는 것이 **가장** 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-139">It is **strongly** recommended that you add a passphrase.</span></span> <span data-ttu-id="669c4-140">공격자가 개인 키를 훔치고 해당 키에 암호가 없는 경우 해당 개인 키를 사용하여 해당하는 공개 키가 있는 서버에 로그인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-140">If an attacker stole your private key and that key did not have a passphrase, they would be able to use that private key to log in to any servers that have the corresponding public key.</span></span> <span data-ttu-id="669c4-141">개인 키를 암호로 보호하면 공격자가 개인 키를 사용할 수 없기 때문에 Azure의 인프라에 대해 보안 계층이 추가로 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-141">If a passphrase protects a private key, it cannot be used by that attacker, providing an additional layer of security for your infrastructure on Azure.</span></span>

<span data-ttu-id="669c4-142">다음은 암호를 설정하는 방법을 보여주는 예제입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-142">Here is an example showing how to set the passphrase.</span></span> <span data-ttu-id="669c4-143">이 명령은(원하면 실행해도 되지만) 실행할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-143">You don't need to execute this command (although you can if you want).</span></span>

```bash
ssh-keygen -t rsa -b 4096 \
    -C "azureuser@myserver" \
    -f ~/.ssh/mykeys/myprivatekey \
    -N someReallySecurePhraseYouWillRemember
```

| <span data-ttu-id="669c4-144">매개 변수</span><span class="sxs-lookup"><span data-stu-id="669c4-144">Parameter</span></span> | <span data-ttu-id="669c4-145">기능</span><span class="sxs-lookup"><span data-stu-id="669c4-145">What it does</span></span> |
|-----------|--------------|
| `-t` | <span data-ttu-id="669c4-146">생성하는 키의 유형입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-146">Type of key to create.</span></span> <span data-ttu-id="669c4-147">**rsa**여야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-147">Must be **rsa**.</span></span> |
| `-b` | <span data-ttu-id="669c4-148">키의 비트 수입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-148">Number of bits in the key.</span></span> <span data-ttu-id="669c4-149">최소 길이는 2048, 최대 길이는 4096입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-149">Minimum length is 2048; maximum is 4096.</span></span> |
| `-C` | <span data-ttu-id="669c4-150">공개 키를 식별하는 데 사용할 수 있는 공개 키에 추가할 선택적인 주석입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-150">An optional comment to append to the public key that can be used to identify it.</span></span> <span data-ttu-id="669c4-151">일반적으로 이메일 주소이지만 간단한 텍스트로 원하는 식별 방법을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-151">Normally this is an email address, but it's simple text, and you can use whatever identification method you prefer.</span></span> |
| `-f` | <span data-ttu-id="669c4-152">개인 키 파일의 위치 및 이름입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-152">The location and filename of the private key file.</span></span> <span data-ttu-id="669c4-153">**.pub**가 추가된 해당 공개 키 파일이 동일한 디렉터리에 생성됩니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-153">A corresponding public key file appended with **.pub** is generated in the same directory.</span></span> <span data-ttu-id="669c4-154">디렉터리가 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-154">The directory must exist.</span></span> |
| `-N` | <span data-ttu-id="669c4-155">개인 키를 암호화하는 데 사용되는 암호입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-155">The passphrase used to encrypt the private key.</span></span> |

## <a name="use-the-ssh-key-pair-with-an-azure-linux-vm"></a><span data-ttu-id="669c4-156">Azure Linux VM에서 SSH 키 쌍 사용</span><span class="sxs-lookup"><span data-stu-id="669c4-156">Use the SSH key pair with an Azure Linux VM</span></span>

<span data-ttu-id="669c4-157">키 쌍이 생성되면 Azure의 Linux VM에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-157">Once you have the key pair generated, you can use it with a Linux VM in Azure.</span></span> <span data-ttu-id="669c4-158">VM을 생성하는 동안 공개 키를 제공하거나 VM을 만든 후에 공개 키를 추가할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-158">You can supply the public key during the VM creation, or add it after the VM has been created.</span></span> 

<span data-ttu-id="669c4-159">다음 명령을 사용하여 Azure Cloud Shell에서 파일의 콘텐츠를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-159">You can view the contents of the file in the Azure Cloud Shell with the following command.</span></span>

```bash
cat ~/.ssh/id_rsa.pub
```

<span data-ttu-id="669c4-160">한 줄이며 다음과 같은 모양입니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-160">It will be a single line and look something like:</span></span>

```output
ssh-rsa XXXXXXXXXXc2EAAAADAXABAAABAXC5Am7+fGZ+5zXBGgXS6GUvmsXCLGc7tX7/rViXk3+eShZzaXnt75gUmT1I2f75zFn2hlAIDGKWf4g12KWcZxy81TniUOTjUsVlwPymXUXxESL/UfJKfbdstBhTOdy5EG9rYWA0K43SJmwPhH28BpoLfXXXXXGX/ilsXXXXXKgRLiJ2W19MzXHp8z3Lxw7r9wx3HaVlP4XiFv9U4hGcp8RMI1MP1nNesFlOBpG4pV2bJRBTXNXeY4l6F8WZ3C4kuf8XxOo08mXaTpvZ3T1841altmNTZCcPkXuMrBjYSJbA8npoXAXNwiivyoe3X2KMXXXXXdXXXXXXXXXXCXXXXX/ azureuser@myserver
```

<span data-ttu-id="669c4-161">다음 연습에서 사용할 수 있도록 이 값을 복사하세요.</span><span class="sxs-lookup"><span data-stu-id="669c4-161">Copy this value off so you can use it in the next exercise.</span></span>

### <a name="use-the-ssh-key-when-creating-a-linux-vm"></a><span data-ttu-id="669c4-162">Linux VM을 만들 때 SSH 키 사용</span><span class="sxs-lookup"><span data-stu-id="669c4-162">Use the SSH key when creating a Linux VM</span></span>

<span data-ttu-id="669c4-163">새 Linux VM을 만드는 동안 SSH 키를 적용하려면 공개 키의 콘텐츠를 복사하여 Azure Portal에 제공_하거나_ 공개 키 파일을 Azure CLI 또는 Azure PowerShell 명령에 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-163">To apply the SSH key while creating a new Linux VM, you will need to copy the contents of the public key and supply it to the Azure portal, _or_ supply the public key file to the Azure CLI or Azure PowerShell command.</span></span> <span data-ttu-id="669c4-164">이 방법은 Linux VM을 만들 때 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-164">We'll use this approach when we create our Linux VM.</span></span>

### <a name="add-the-ssh-key-to-an-existing-linux-vm"></a><span data-ttu-id="669c4-165">기존 Linux VM에 SSH 키 추가</span><span class="sxs-lookup"><span data-stu-id="669c4-165">Add the SSH key to an existing Linux VM</span></span>

<span data-ttu-id="669c4-166">VM을 이미 만든 경우 `ssh-copy-id` 명령으로 Linux VM에 공개 키를 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-166">If you have already created a VM, you can install the public key onto your Linux VM with the `ssh-copy-id` command.</span></span> <span data-ttu-id="669c4-167">SSH에 대한 권한이 키에 부여되면 암호 없이 서버에 대한 액세스 권한이 부여됩니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-167">Once the key has been authorized for SSH, it grants access to the server without a password.</span></span>

<span data-ttu-id="669c4-168">이것을 키와 연결할 사용자 이름 및 공개 키 파일에 전달합니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-168">Pass it the public key file and the username to associate with the key.</span></span>

```bash
ssh-copy-id -i ~/.ssh/id_rsa.pub azureuser@myserver
```
<span data-ttu-id="669c4-169">공개 키가 확보되었으면 Azure Portal로 전환하여 Linux VM을 만들겠습니다.</span><span class="sxs-lookup"><span data-stu-id="669c4-169">Now that we have our public key let's switch to the Azure portal and create a Linux VM.</span></span>

