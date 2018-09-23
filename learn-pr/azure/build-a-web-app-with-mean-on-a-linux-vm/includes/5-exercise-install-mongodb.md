<span data-ttu-id="daf9a-101">이 단원에서는 Ubuntu Linux 가상 머신에 MongoDB를 설치하여 향후 샘플 웹 응용 프로그램의 데이터 저장소로 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-101">In this unit, you will install MongoDB on your Ubuntu Linux virtual machine to act as a data store for your upcoming sample web application.</span></span>

## <a name="install-mongodb"></a><span data-ttu-id="daf9a-102">MongoDB 설치</span><span class="sxs-lookup"><span data-stu-id="daf9a-102">Install MongoDB</span></span>

1. <span data-ttu-id="daf9a-103">Cloud Shell에서 VM에 SSH합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-103">From Cloud Shell, SSH into your VM.</span></span>

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. <span data-ttu-id="daf9a-104">MongoDB 리포지토리의 암호화 키를 가져옵니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-104">Import the encryption key for the MongoDB repository.</span></span> <span data-ttu-id="daf9a-105">이렇게 하면 설치하는 mongodb 패키지가 MongoDB Inc.에서 제공하는 것인지를 패키지 관리자가 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-105">This will allow the package manager to verify that the mongodb packages you install are coming from MongoDB Inc.</span></span>

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    <span data-ttu-id="daf9a-106">**sudo** 명령은 관리자 권한으로 지정된 명령을 실행하고자 함을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-106">The **sudo** command means that we want to run the specified command with administrative privileges.</span></span>

1. <span data-ttu-id="daf9a-107">패키지 관리자가 mongodb 패키지를 찾을 수 있도록 MongoDB Ubuntu 리포지토리를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-107">Register the MongoDB Ubuntu repository so the package manager can locate the mongodb packages.</span></span>

    > [!NOTE]
    > <span data-ttu-id="daf9a-108">이 명령은 Ubuntu 버전별로 다릅니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-108">This command is different for different versions of Ubuntu.</span></span> <span data-ttu-id="daf9a-109">사용 중인 Ubuntu 버전을 찾으려면 `uname -v`를 실행하세요.</span><span class="sxs-lookup"><span data-stu-id="daf9a-109">To find out which version of Ubuntu you're using, run: `uname -v`.</span></span>
    > <span data-ttu-id="daf9a-110">이 명령은 `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`처럼 출력됩니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-110">This command will output something like this: `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`.</span></span>
    >
    > <span data-ttu-id="daf9a-111">이 출력은 Ubuntu 버전 16.04.1을 실행 중임을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-111">This output indicates that we're running Ubuntu version 16.04.1.</span></span>
    > <span data-ttu-id="daf9a-112">버전에 맞는 정확한 명령을 가져오려면 [Ubuntu에 MongoDB Community Edition 설치](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) 설명서를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="daf9a-112">Refer to the [Install MongoDB Community Edition on Ubuntu](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) documentation to get the exact command for your version.</span></span>

    <span data-ttu-id="daf9a-113">Ubuntu 16.04에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-113">On Ubuntu 16.04, we run this command:</span></span>

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. <span data-ttu-id="daf9a-114">최신 패키지 정보를 포함하도록 패키지 데이터베이스를 업데이트합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-114">Update the package database so we have the latest package information.</span></span>

    ```bash
    sudo apt-get update
    ```

1. <span data-ttu-id="daf9a-115">VM에 MongoDB 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-115">Install the MongoDB package onto our VM.</span></span>

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. <span data-ttu-id="daf9a-116">나중에 연결할 수 있도록 MongoDB 서비스를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-116">Start the MongoDB service so you can connect to it later.</span></span>

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a><span data-ttu-id="daf9a-117">요약</span><span class="sxs-lookup"><span data-stu-id="daf9a-117">Summary</span></span>

<span data-ttu-id="daf9a-118">이제 Ubuntu Linux VM에 MongoDB가 설치되었습니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-118">We now have MongoDB installed on our Ubuntu Linux VM.</span></span> <span data-ttu-id="daf9a-119">MongoDB는 웹 응용 프로그램에서 저장하고 검색하는 정보에 대한 지원 데이터 저장소로 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="daf9a-119">MongoDB will serve as your backing data store for the information you save and retrieve in your web application.</span></span>