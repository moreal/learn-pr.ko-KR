<span data-ttu-id="fbdee-101">이 단원에서는 Azure에 호스트된 Ubuntu Linux 가상 머신에 Node.js(MEAN 머리글자어의 **N**)를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-101">In this unit, you will install Node.js - the **N** in the MEAN acronym - on an Azure-hosted Ubuntu Linux virtual machine.</span></span> <span data-ttu-id="fbdee-102">Node.js는 HTTP 트래픽을 처리하고 웹 응용 프로그램을 호스트하는 데 런타임으로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-102">Node.js will serve as our runtime for handling our HTTP traffic and hosting our web application.</span></span>

## <a name="install-nodejs"></a><span data-ttu-id="fbdee-103">Node.js 설치</span><span class="sxs-lookup"><span data-stu-id="fbdee-103">Install Node.js</span></span>

1. <span data-ttu-id="fbdee-104">**이전 연습에서 SSH를 사용하여 VM에 접근하지 않은 경우에는** SSH를 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="fbdee-104">**If you aren't still SSHed into your VM from the previous exercise**, SSH in.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. <span data-ttu-id="fbdee-105">**apt-get**이 가상 머신에 설치할 올바른 패키지를 찾을 수 있도록 Node.js 패키지 리포지토리를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-105">Register the Node.js package repository so **apt-get** can find the right package to install on your virtual machine.</span></span>

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. <span data-ttu-id="fbdee-106">Linux 시스템에 Node.js 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-106">Install the Node.js package on your Linux system.</span></span>

    ```bash
    sudo apt-get install -y Node.js
    ```

1. <span data-ttu-id="fbdee-107">다음의 간단한 Node.js 명령을 실행하여 Node.js 설치에 성공했는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-107">Verify the Node.js installation succeeded by running the following simple Node.js command.</span></span>

    ```bash
    node -v
    ```

    <span data-ttu-id="fbdee-108">`v8.11.4`처럼 출력되어야 하며, 패키지를 설치할 때 사용 가능한 최신 Node.js 버전을 반영하는 버전을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-108">The output should be something like `v8.11.4`, with the version reflecting the latest Node.js version that's available when you install the package.</span></span>

## <a name="summary"></a><span data-ttu-id="fbdee-109">요약</span><span class="sxs-lookup"><span data-stu-id="fbdee-109">Summary</span></span>

<span data-ttu-id="fbdee-110">가상 머신에 Node.js가 설치되면 실행해야 하는 웹 응용 프로그램 빌드를 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbdee-110">With Node.js installed on your virtual machine, we can start building a web application that it will be responsible for running.</span></span>