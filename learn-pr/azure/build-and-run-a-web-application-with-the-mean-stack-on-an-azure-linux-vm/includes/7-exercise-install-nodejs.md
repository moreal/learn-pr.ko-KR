<span data-ttu-id="dac59-101">이 연습에서는 Azure에 호스트된 Ubuntu Linux 가상 머신에 Node.js(MEAN 약어의 **N**)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-101">In this exercise, you will install Node.js - the **N** in the MEAN acronym - on an Azure-hosted Ubuntu Linux virtual machine.</span></span> <span data-ttu-id="dac59-102">Node.js는 HTTP 트래픽을 처리하고 웹 응용 프로그램을 호스트하는 데 런타임으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-102">Node.js will serve as our runtime for handling our HTTP traffic and hosting our web application.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="dac59-103">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="dac59-103">Connect to the VM</span></span>

<span data-ttu-id="dac59-104">Node.js를 설치하려면 **ssh**를 사용하여 VM에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-104">In order to install Node.js, you have to connect to the VM using **ssh**.</span></span> <span data-ttu-id="dac59-105">아직 VM에 연결되지 않은 경우 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-105">If you aren't still connected to your VM, run the following command.</span></span> <span data-ttu-id="dac59-106">`<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-106">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-nodejs"></a><span data-ttu-id="dac59-107">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="dac59-107">Install Node.js</span></span>

> [!Important]
> <span data-ttu-id="dac59-108">Ubuntu는 **Node.js-legacy**라는 비공식 패키지를 제공하지만 이 패키지는 Node.js에서 유지 관리하지 않고 더 이상 사용되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-108">Ubuntu provides an unofficial package called **Node.js-legacy**, but this package is not maintained by Node.js and is outdated.</span></span>

1. <span data-ttu-id="dac59-109">**apt-get**이 가상 머신에 설치할 올바른 패키지를 찾을 수 있도록 Node.js 패키지 리포지토리를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-109">Register the Node.js package repository so **apt-get** can find the right package to install on your virtual machine.</span></span>

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. <span data-ttu-id="dac59-110">Linux 시스템에 Node.js 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-110">Install the Node.js package on your Linux system.</span></span>

    ```bash
    sudo apt-get install -y Node.js
    ```

1. <span data-ttu-id="dac59-111">간단한 다음 Node.js 명령을 실행하여 Node.js 설치에 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-111">Verify the Node.js installation succeeded by running the following simple Node.js command.</span></span>

    ```bash
    node -v
    ```

    <span data-ttu-id="dac59-112">`v8.11.4`처럼 출력되어야 하며, 패키지를 설치할 때 사용 가능한 최신 Node.js 버전을 반영하는 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-112">The output should be something like `v8.11.4`, with the version reflecting the latest Node.js version available when you install the package.</span></span>

## <a name="summary"></a><span data-ttu-id="dac59-113">요약</span><span class="sxs-lookup"><span data-stu-id="dac59-113">Summary</span></span>

<span data-ttu-id="dac59-114">가상 머신에 Node.js가 설치되면 실행해야 하는 웹 응용 프로그램 빌드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="dac59-114">With Node.js installed on your virtual machine, we can start building a web application that it will be responsible for running.</span></span>
