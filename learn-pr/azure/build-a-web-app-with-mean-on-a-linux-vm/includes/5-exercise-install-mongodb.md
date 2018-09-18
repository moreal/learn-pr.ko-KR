<span data-ttu-id="547a1-101">여기에서는 Ubuntu Linux 가상 머신에 향후 샘플 웹 응용 프로그램의 데이터 저장소 역할을 할 MongoDB를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-101">In this unit, you will install MongoDB on your Ubuntu Linux virtual machine to act as a data store for your upcoming sample web application.</span></span>

## <a name="connect-to-the-vm"></a><span data-ttu-id="547a1-102">VM에 연결</span><span class="sxs-lookup"><span data-stu-id="547a1-102">Connect to the VM</span></span>

<span data-ttu-id="547a1-103">MongoDB를 설치하려면 **ssh**를 사용하여 VM에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-103">In order to install MongoDB, you have to connect to the VM using **ssh**.</span></span> <span data-ttu-id="547a1-104">`<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공용 IP 주소로 바꿉니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-104">Substitute your admin username and your VM's public IP address from above for the `<vm-admin-username>` and `<vm-public-ip>` placeholders.</span></span>

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-mongodb"></a><span data-ttu-id="547a1-105">MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="547a1-105">Install MongoDB</span></span>

> [!Important]
> <span data-ttu-id="547a1-106">Ubuntu는 **mongodb**라는 비공식 패키지를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-106">Ubuntu provides an unofficial package called **mongodb**.</span></span> <span data-ttu-id="547a1-107">이 패키지는 MongoDB inc가 유지 관리하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-107">This package is not maintained by MongoDB Inc.</span></span>

1. <span data-ttu-id="547a1-108">MongoDB 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-108">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="547a1-109">이렇게 하면 설치하는 mongodb 패키지가 MongoDB Inc.에서 제공하는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-109">This will allow the package manager to verify that the mongodb packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    <span data-ttu-id="547a1-110">**sudo** 명령은 관리자 권한으로 지정된 명령을 실행하고자 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-110">The **sudo** command means that we want to run the specified command with administrative privileges.</span></span>

1. <span data-ttu-id="547a1-111">패키지 관리자가 mongodb 패키지를 찾을 수 있도록 MongoDB Ubuntu 리포지토리를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-111">Register the MongoDB Ubuntu repository so the package manager can locate the mongodb packages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="547a1-112">이 명령은 Ubuntu 버전별로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-112">This command is different for different versions of Ubuntu.</span></span> <span data-ttu-id="547a1-113">사용 중인 Ubuntu 버전을 찾으려면 `uname -v`를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="547a1-113">To find out which version of Ubuntu you're using, run: `uname -v`.</span></span>
    > <span data-ttu-id="547a1-114">이 명령은 `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`처럼 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-114">This command will output something like this: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span></span>
    >
    > <span data-ttu-id="547a1-115">이 출력은 Ubuntu 버전 16.04.1을 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-115">This output indicates that we're running Ubuntu version 16.04.1.</span></span>
    > <span data-ttu-id="547a1-116">버전에 맞는 정확한 명령을 가져오려면 [Ubuntu에 MongoDB Community Edition 설치](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="547a1-116">Refer to the [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) documentation to get the exact command for your version.</span></span>

    <span data-ttu-id="547a1-117">Ubuntu 16.04에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-117">On Ubuntu 16.04, we run this command:</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="547a1-118">최신 패키지 정보를 포함하도록 패키지 데이터베이스를 다시 로드합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-118">Reload the package database so we have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="547a1-119">VM에 MongoDB 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-119">Install the MongoDB package onto our VM.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="547a1-120">나중에 연결할 수 있도록 MongoDB 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-120">Start the MongoDB service so you can connect to it later.</span></span>

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a><span data-ttu-id="547a1-121">요약</span><span class="sxs-lookup"><span data-stu-id="547a1-121">Summary</span></span>

<span data-ttu-id="547a1-122">이제 Ubuntu Linux VM에 MongoDB가 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-122">We now have MongoDB installed on our Ubuntu Linux VM.</span></span> <span data-ttu-id="547a1-123">MongoDB는 웹 응용 프로그램에서 저장하고 검색하는 정보에 대한 지원 데이터 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="547a1-123">MongoDB will serve as your backing data store for the information you save and retrieve in your web application.</span></span>