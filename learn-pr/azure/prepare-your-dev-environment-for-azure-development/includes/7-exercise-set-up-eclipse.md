<span data-ttu-id="fabfd-101">여기서는 개발 머신에 Eclipse 및 Azure 도구 키트를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-101">Here you'll install Eclipse and the Azure Toolkit on your development machine.</span></span> <span data-ttu-id="fabfd-102">연습이 끝날 때 쯤이면 Azure에 연결된 Java 응용 프로그램을 만드는 데 필요한 모든 것이 있게 됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-102">By the end of the exercise, you'll have everything you need to create a Java application connected to Azure.</span></span>

## <a name="install-eclipse-ide"></a><span data-ttu-id="fabfd-103">Eclipse IDE 설치</span><span class="sxs-lookup"><span data-stu-id="fabfd-103">Install Eclipse IDE</span></span>

1. <span data-ttu-id="fabfd-104">[운영 체제에 적합한 Eclipse IDE](https://www.eclipse.org/downloads/packages/installer)를 다운로드하세요.</span><span class="sxs-lookup"><span data-stu-id="fabfd-104">Download the appropriate [Eclipse IDE for your operating system](https://www.eclipse.org/downloads/packages/installer).</span></span>

1. <span data-ttu-id="fabfd-105">다운로드한 후 Eclipse 설치 관리자를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-105">Start the Eclipse installer once downloaded.</span></span>

    1. <span data-ttu-id="fabfd-106">Windows에서 다운로드한 파일을 두 번 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-106">On Windows, double-click the downloaded file.</span></span>

    1. <span data-ttu-id="fabfd-107">macOS 및 Linux에서, 다운로드된 파일의 설치 관리자 압축을 풀고 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-107">On macOS and Linux, unzip the installer from the downloaded file and run it.</span></span>

        > [!NOTE]
        > <span data-ttu-id="fabfd-108">Java Development Kit가 누락된 경우 설치 관리자에 설치하라는 메시지가 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-108">The installer may prompt you to install the Java Development Kit, if it is missing.</span></span>

1. <span data-ttu-id="fabfd-109">설치할 패키지를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-109">Select the packages to install.</span></span> <span data-ttu-id="fabfd-110">Java 개발자의 경우 Java 또는 Java EE Eclipse IDE 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-110">For Java developers, choose either the Java or Java EE Eclipse IDE option.</span></span>

1. <span data-ttu-id="fabfd-111">머신에서 설치 대상을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-111">Select the installation destination on your machine.</span></span>

1. <span data-ttu-id="fabfd-112">Eclipse를 시작하여 제대로 설치되었는지 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-112">Launch Eclipse to validate that it installed correctly.</span></span>

## <a name="install-azure-toolkit-for-eclipse"></a><span data-ttu-id="fabfd-113">Eclipse용 Azure 도구 키트 설치</span><span class="sxs-lookup"><span data-stu-id="fabfd-113">Install Azure Toolkit for Eclipse</span></span>

<span data-ttu-id="fabfd-114">Azure Toolkit는 Windows, macOS 및 Linux에서 동일하게 설치됩니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-114">Installing the Azure Toolkit is the same across Windows, macOS, and Linux.</span></span>

1. <span data-ttu-id="fabfd-115">Eclipse를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-115">Start Eclipse.</span></span>

1. <span data-ttu-id="fabfd-116">**도움말** > **새 소프트웨어 설치...** 로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-116">Go to **Help** > **Install New Software...**.</span></span>

    <span data-ttu-id="fabfd-117">다음 스크린샷은 **새 소프트웨어 설치...** 항목의 메뉴 위치를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-117">The following screenshot shows the menu location of the **Install New Software...** item.</span></span>

    ![Eclipse 도움말 메뉴에 새 소프트웨어 설치 옵션이 강조되어 있는 스크린샷입니다.](../media/7-eclipse-install-new-software.png)

1. <span data-ttu-id="fabfd-119">**사용 가능한 소프트웨어** 대화 상자가 열립니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-119">The **Available Software** dialog will open.</span></span> <span data-ttu-id="fabfd-120">**작업:** 텍스트 상자에 `http://dl.microsoft.com/eclipse/`를 입력하고 Enter 키를 누릅니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-120">In the **Work with:** text box, type `http://dl.microsoft.com/eclipse/` and press Enter.</span></span>

1. <span data-ttu-id="fabfd-121">결과에서 **Azure Toolkit for Java** 옵션을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-121">In the results, check the **Azure Toolkit for Java** option.</span></span> <span data-ttu-id="fabfd-122">**Contact all update sites during install to find required software**(설치 중 모든 업데이트 사이트에 문의하여 필요한 소프트웨어 찾기) 옵션이 선택 취소되어 있지 않은 경우 선택 취소해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-122">Make sure you uncheck the **Contact all update sites during install to find required software** option, if it isn't already.</span></span>

    <span data-ttu-id="fabfd-123">다음 스크린샷은 위에 설명된 **사용 가능한 소프트웨어** 설치 구성을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-123">The following screenshot shows the **Available Software** install configuration as described above.</span></span>

    ![Azure Toolkit for Java를 찾아 설치하는 데 필요한 구성이 강조되어 있는 상자가 포함된 Eclipse의 사용 가능한 소프트웨어 창 스크린샷입니다.](../media/7-eclipse-download-azure-toolkit-for-java.png)

1. <span data-ttu-id="fabfd-125">**다음**을 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-125">Click **Next**.</span></span>

1. <span data-ttu-id="fabfd-126">메시지가 표시되면 사용권 계약을 검토 및 동의하고 **완료**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-126">Review and accept the license agreements when prompted, and click **Finish**.</span></span>

1. <span data-ttu-id="fabfd-127">Eclipse는 Azure Toolkit를 다운로드하여 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-127">Eclipse will download and install the Azure Toolkit.</span></span>

1. <span data-ttu-id="fabfd-128">필요한 경우 Eclipse를 다시 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-128">Restart Eclipse if required.</span></span>

1. <span data-ttu-id="fabfd-129">Eclipse에서 **도구** > **Azure** 메뉴 옵션을 찾을 수 있는지 확인하여 Azure Toolkit 설치의 유효성을 검사합니다.</span><span class="sxs-lookup"><span data-stu-id="fabfd-129">Validate the Azure Toolkit installation by verifying that you can find a **Tools** > **Azure** menu option in Eclipse.</span></span>
