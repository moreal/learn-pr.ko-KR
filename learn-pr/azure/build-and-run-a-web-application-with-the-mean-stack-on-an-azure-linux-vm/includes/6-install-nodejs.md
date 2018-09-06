<span data-ttu-id="ffcb9-101">웹 응용 프로그램의 MongoDB 데이터 저장소에 대해 알아보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-101">We will be talking to our MongoDB data store from a web application.</span></span> <span data-ttu-id="ffcb9-102">MEAN 스택의 경우 이는 Node.js 오픈 소스 JavaScript 런타임을 설치하는 것을 의미합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-102">For the MEAN stack, this means installing the Node.js open-source JavaScript runtime.</span></span> <span data-ttu-id="ffcb9-103">Node.js는 웹 응용 프로그램 및 해당 콘텐츠에 대한 서버 쪽 호스트 역할을 합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-103">Node.js will act as our server-side host for our web application and its content.</span></span>

## <a name="what-must-be-installed"></a><span data-ttu-id="ffcb9-104">무엇을 설치해야 하나요?</span><span class="sxs-lookup"><span data-stu-id="ffcb9-104">What must be Installed?</span></span>

<span data-ttu-id="ffcb9-105">사용할 수 있는 Node.js의 두 가지 권장 버전은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-105">There are two recommended versions of Node.js available:</span></span>

- <span data-ttu-id="ffcb9-106">**LTS(장기 지원)** - 대부분의 사용자 및 프로덕션 환경에 권장되는 버전입니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-106">**Long Term Support (LTS)** - a version recommended for most users, and for production environments</span></span>
- <span data-ttu-id="ffcb9-107">**최신** - 최신 기능을 포함하는 버전이지만 릴리스 주기 간에 호환성이 손상되는 변경이 도입될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-107">**Current** - a version that contains the latest features, but can introduce breaking changes between release cycles.</span></span>

<span data-ttu-id="ffcb9-108">이 모듈에서는 이 문서 작성 시의 Node.js LTS, 버전 8.11.4를 사용하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-108">In this module we are going to use Node.js LTS, version 8.11.4 as of this writing.</span></span>

## <a name="how-to-install-nodejs"></a><span data-ttu-id="ffcb9-109">Node.js 설치 방법</span><span class="sxs-lookup"><span data-stu-id="ffcb9-109">How to install Node.js</span></span>

<span data-ttu-id="ffcb9-110">Node.js를 대부분의 플랫폼에 설치할 수 있지만, MEAN 스택 구성 요소는 Ubuntu Linux에 계속 설치하겠습니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-110">Node.js can be installed on most platforms, but we will continue to install MEAN stack components on Ubuntu Linux.</span></span> <span data-ttu-id="ffcb9-111">다른 운영 체제에 Node.js를 설치하는 방법에 대한 자세한 내용은 [Node.js instructions for installing it via various package managers](https://Node.js.org/en/download/package-manager/)(패키지 관리자를 통해 설치하기 위한 Node.js 지침)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-111">For information on installing Node.js on other operating systems, check out the [Node.js instructions for installing it via various package managers](https://Node.js.org/en/download/package-manager/).</span></span>

<span data-ttu-id="ffcb9-112">Ubuntu Linux에서 **apt-get** 패키지 관리자를 사용하여 Node.js를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="ffcb9-112">On Ubuntu Linux, you use the **apt-get** package manager to install Node.js.</span></span>
