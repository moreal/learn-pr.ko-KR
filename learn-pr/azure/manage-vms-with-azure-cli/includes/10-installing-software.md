<span data-ttu-id="cde53-101">VM에서 시도하려는 마지막 항목은 웹 서버를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="cde53-102">설치할 가장 쉬운 패키지 중 하나는 `nginx` 입니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-102">One of the easiest packages to install is `nginx`.</span></span>

1. <span data-ttu-id="cde53-103">Linux 가상 머신의 공용 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-103">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="cde53-104">`vm list-ip-addresses` 명령을 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-104">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

2. <span data-ttu-id="cde53-105">그런 다음, 테스트할 때 수행한 것처럼 머신에 대한 `ssh` 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-105">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="cde53-106">관리자 이름(“**aldis**”)을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-106">Remember you will need to pass in the admin name ("**aldis**").</span></span>

3. <span data-ttu-id="cde53-107">제공된 셸에서 다음 명령을 실행하여 `nginx` 웹 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-107">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```azurecli
sudo apt-get -y update && sudo apt-get -y install nginx
```

4. <span data-ttu-id="cde53-108">Azure Cloud Shell에서 `curl`을 사용하여 Linux 웹 서버의 기본 페이지를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="cde53-108">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="cde53-109">또는 새 브라우저 탭을 열고 공용 IP 주소로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-109">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 168.61.54.62
```

<span data-ttu-id="cde53-110">Linux 가상 머신이 기본 제공 방화벽을 통해 포트 80(`http`)을 노출하지 않기 때문에 이동에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-110">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="cde53-111">다행히 Azure CLI에는 이를 위한 `vm open-port` 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-111">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

5. <span data-ttu-id="cde53-112">Cloud Shell에 다음을 입력하여 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-112">Type the following into Cloud Shell to open port 80:</span></span>

```
az vm open-port --port 80 --resource-group ExerciseResources --name SampleVM
```

<span data-ttu-id="cde53-113">마지막으로 `curl`을 다시 시도합니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-113">Finally, try `curl` again.</span></span> <span data-ttu-id="cde53-114">이번에는 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-114">This time it should return data.</span></span> <span data-ttu-id="cde53-115">브라우저에서도 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="cde53-115">You can see the page in a browser as well.</span></span>



