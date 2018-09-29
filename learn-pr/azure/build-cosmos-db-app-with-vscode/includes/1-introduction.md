<span data-ttu-id="58014-101">온라인 판매점의 저장소를 관리한다고 가정해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="58014-101">Imagine you're managing storage for an online retailer.</span></span> <span data-ttu-id="58014-102">사용자 및 제품 데이터를 만들고, 업데이트하고, 삭제하는 도구가 필요합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-102">You need tools to create, update, and delete your user and product data.</span></span>

<span data-ttu-id="58014-103">이 모듈에서는 Visual Studio Code에서 .NET Core 콘솔 응용 프로그램을 빌드하여 사용자 레코드를 만들고, 업데이트하고, 삭제하며, 데이터를 쿼리하고, C#을 사용하여 저장 프로시저를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-103">In this module, you will build a .NET Core console application in Visual Studio Code to create, update, and delete user records, query your data, and perform stored procedures using C#.</span></span>

<span data-ttu-id="58014-104">데이터는 Azure Cosmos DB에 저장되며, 여기에는 편리한 Visual Studio Code 확장이 있으므로 Azure Portal을 열지 않아도 쉽게 Azure Cosmos DB 계정, 데이터베이스 및 컬렉션을 만들고, 앱에 연결 문자열을 복사할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="58014-104">Your data will be stored in Azure Cosmos DB, which has a convenient Visual Studio Code extension so you can easily create an Azure Cosmos DB account, database, and collection, and copy your connection string into the app without having to open the Azure portal.</span></span>

## <a name="learning-objectives"></a><span data-ttu-id="58014-105">학습 목표</span><span class="sxs-lookup"><span data-stu-id="58014-105">Learning objectives</span></span>

<span data-ttu-id="58014-106">이 모듈에서는 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-106">In this module, you will:</span></span>  

- <span data-ttu-id="58014-107">Azure Cosmos DB 확장을 사용하여 Visual Studio Code에서 Azure Cosmos DB 계정, 데이터베이스 및 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="58014-107">Create an Azure Cosmos DB account, database, and collection in Visual Studio Code using the Azure Cosmos DB extension</span></span>
- <span data-ttu-id="58014-108">Azure Cosmos DB에 데이터를 저장하고 쿼리하는 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="58014-108">Create an application to store and query data in Azure Cosmos DB</span></span>
- <span data-ttu-id="58014-109">Visual Studio Code의 터미널을 사용하여 신속하게 콘솔 응용 프로그램 만들기</span><span class="sxs-lookup"><span data-stu-id="58014-109">Use the Terminal in Visual Studio Code to quickly create a console application</span></span>
- <span data-ttu-id="58014-110">Visual Studio Code용 Azure Cosmos DB 확장을 활용하여 Azure Cosmos DB 기능 추가</span><span class="sxs-lookup"><span data-stu-id="58014-110">Add Azure Cosmos DB functionality with the help of the Azure Cosmos DB extension for Visual Studio Code</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58014-111">필수 구성 요소</span><span class="sxs-lookup"><span data-stu-id="58014-111">Prerequisites</span></span>

- <span data-ttu-id="58014-112">[Visual Studio Code](https://code.visualstudio.com/)가 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-112">Must have [Visual Studio Code](https://code.visualstudio.com/) installed</span></span>
- <span data-ttu-id="58014-113">[.NET Core 2.1](https://www.microsoft.com/net/download)이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-113">Must have [.NET Core 2.1](https://www.microsoft.com/net/download) installed</span></span>
- <span data-ttu-id="58014-114">Visual Studio Code에 [Azure 계정](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) 확장이 설치되어 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="58014-114">Must have the [Azure Account](https://marketplace.visualstudio.com/items?itemName=ms-vscode.azure-account) extension installed in Visual Studio Code</span></span>
