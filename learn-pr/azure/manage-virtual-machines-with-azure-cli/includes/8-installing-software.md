<span data-ttu-id="7fa0c-101">VM에서 시도하려는 마지막 항목은 웹 서버를 설치하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-101">The last thing we want to try on our VM is to install a web server.</span></span> <span data-ttu-id="7fa0c-102">설치할 가장 쉬운 패키지 중 하나는 `nginx`입니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-102">One of the easiest packages to install is `nginx`.</span></span>

## <a name="install-nginx-web-server"></a><span data-ttu-id="7fa0c-103">NGINX 웹 서버 설치</span><span class="sxs-lookup"><span data-stu-id="7fa0c-103">Install NGINX web server</span></span>

1. <span data-ttu-id="7fa0c-104">Linux 가상 머신의 공용 IP 주소를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-104">Locate the public IP address of your Linux virtual machine.</span></span> <span data-ttu-id="7fa0c-105">`vm list-ip-addresses` 명령을 사용하여 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-105">Remember you can use the `vm list-ip-addresses` command to look it up.</span></span>

1. <span data-ttu-id="7fa0c-106">그런 다음, 테스트할 때 수행한 것처럼 머신에 대한 `ssh` 연결을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-106">Next, open an `ssh` connection to the machine like you did when we tested it.</span></span> <span data-ttu-id="7fa0c-107">관리자 이름(“**aldis**”)을 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-107">Remember you will need to pass in the admin name ("**aldis**").</span></span>

1. <span data-ttu-id="7fa0c-108">제공된 셸에서 다음 명령을 실행하여 `nginx` 웹 서버를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-108">In the presented shell, execute the following command to install the `nginx` web server.</span></span>

```bash
sudo apt-get -y update && sudo apt-get -y install nginx
```

1. <span data-ttu-id="7fa0c-109">Secure Shell을 종료합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-109">Exit the Secure Shell.</span></span>

```bash
exit
```

## <a name="retrieve-our-default-page"></a><span data-ttu-id="7fa0c-110">기본 페이지 검색</span><span class="sxs-lookup"><span data-stu-id="7fa0c-110">Retrieve our default page</span></span>

1. <span data-ttu-id="7fa0c-111">Azure Cloud Shell에서 `curl`을 사용하여 Linux 웹 서버의 기본 페이지를 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-111">In Azure Cloud Shell, use `curl` to read the default page from your Linux web server.</span></span> <span data-ttu-id="7fa0c-112">또는 새 브라우저 탭을 열고 공용 IP 주소로 이동할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-112">Alternatively, you can open a new browser tab and browse to the public IP address.</span></span>

```azurecli
curl 40.83.165.85
```

<span data-ttu-id="7fa0c-113">Linux 가상 머신이 기본 제공 방화벽을 통해 포트 80(`http`)을 노출하지 않기 때문에 이동에 실패합니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-113">It will fail because the Linux virtual machine doesn't expose port 80 (`http`) through the built-in firewall.</span></span> <span data-ttu-id="7fa0c-114">다행히 Azure CLI에는 이를 위한 `vm open-port` 명령이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-114">Luckily, the Azure CLI has a command for that: `vm open-port`.</span></span> 

1. <span data-ttu-id="7fa0c-115">Cloud Shell에 다음을 입력하여 포트 80을 엽니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-115">Type the following into Cloud Shell to open port 80:</span></span>

```azurecli
az vm open-port --port 80 --resource-group <rgn>[Sandbox resource group name]</rgn> --name SampleVM
```

<span data-ttu-id="7fa0c-116">네트워크 규칙을 추가하고 방화벽을 통해 포트를 열기까지는 시간이 오래 걸립니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-116">It will take a moment to add the network rule and open the port through the firewall.</span></span> <span data-ttu-id="7fa0c-117">`curl`을 다시 시도하세요.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-117">Try `curl` again.</span></span> <span data-ttu-id="7fa0c-118">이번에는 데이터가 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-118">This time it should return data.</span></span> <span data-ttu-id="7fa0c-119">브라우저에서도 페이지를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7fa0c-119">You can see the page in a browser as well.</span></span>

```output
<!DOCTYPE html>
<html>
<head>
<title>Welcome to nginx on Debian!</title>
<style>
    body {
        width: 35em;
        margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
    }
</style>
</head>
<body>
<h1>Welcome to nginx on Debian!</h1>
<p>If you see this page, the nginx web server is successfully installed and
working on Debian. Further configuration is required.</p>

<p>For online documentation and support please refer to
<a href="http://nginx.org/">nginx.org</a></p>

<p>
      Please use the <tt>reportbug</tt> tool to report bugs in the
      nginx package with Debian. However, check <a
      href="http://bugs.debian.org/cgi-bin/pkgreport.cgi?ordering=normal;archive=0;src=nginx;repeatmerged=0">existing
      bug reports</a> before reporting a new bug.
</p>

<p><em>Thank you for using debian and nginx.</em></p>


</body>
</html>
```
