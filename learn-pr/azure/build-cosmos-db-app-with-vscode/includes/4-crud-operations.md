<!--TODO: explain Etag in knowledge needed-->

<span data-ttu-id="1fc54-101">Azure Cosmos DB에 대한 연결이 설정되면 다음 단계는 데이터베이스에 저장된 문서를 만들고, 읽고, 바꾸고, 삭제하는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-101">Once the connection to Azure Cosmos DB has been made, the next step is to create, read, replace, and delete the documents that are stored in the database.</span></span> <span data-ttu-id="1fc54-102">이 단원에서는 WebCustomer 컬렉션에 사용자 문서를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-102">In this unit, you will create User documents in your WebCustomer collection.</span></span> <span data-ttu-id="1fc54-103">그런 다음, 해당 문서를 ID별로 검색하고, 바꾸고, 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-103">Then, you'll retrieve them by ID, replace them, and delete them.</span></span>

## <a name="working-with-documents-programmatically"></a><span data-ttu-id="1fc54-104">프로그래밍 방식으로 문서 작업</span><span class="sxs-lookup"><span data-stu-id="1fc54-104">Working with documents programmatically</span></span>

<span data-ttu-id="1fc54-105">데이터는 Azure Cosmos DB의 JSON 문서에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-105">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="1fc54-106">[문서](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents)는 이전 모듈에 나와 있는 대로 또는 이 모듈에서 설명한 대로 프로그래밍 방식으로 포털에서 만들어지거나, 검색되거나, 바뀌거나, 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-106">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="1fc54-107">Azure Cosmos DB는 .NET, .NET Core, Java, Node.js 및 Python에 사용되는 클라이언트 쪽 SDK를 제공합니다. 이러한 도구는 각각 해당 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-107">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="1fc54-108">이 모듈에서는 .NET Core SDK를 사용하여 Azure Cosmos DB에 저장된 NoSQL 데이터에 CRUD(만들기, 검색, 업데이트 및 삭제) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-108">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations on the NoSQL data stored in Azure Cosmos DB.</span></span>

<span data-ttu-id="1fc54-109">Azure Cosmos DB 문서에 대한 기본 작업은 [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 클래스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-109">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="1fc54-110">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="1fc54-110">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="1fc54-111">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="1fc54-111">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="1fc54-112">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="1fc54-112">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="1fc54-113">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="1fc54-113">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="1fc54-114">Upsert는 문서가 이미 존재하는지 여부에 따라 만들기 또는 바꾸기 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-114">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="1fc54-115">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="1fc54-115">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="1fc54-116">이러한 작업을 수행하려면 데이터베이스에 저장된 개체를 나타내는 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-116">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="1fc54-117">사용자 데이터베이스로 작업하기 때문에 이름, 성 및 사용자 ID(수평적 확장을 사용하도록 설정할 파티션 키이므로 필수임)와 배송 기본 설정 및 주문 기록에 대한 서브클래스 같은 기본 데이터를 저장할 **User** 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-117">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their first name, last name, and user id (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="1fc54-118">사용자를 나타내는 해당 클래스가 만들어져 있으면 각 인스턴스에 대한 새 사용자 문서를 만든 후에 문서에서 몇 가지 간단한 CRUD 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-118">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="1fc54-119">문서 만들기</span><span class="sxs-lookup"><span data-stu-id="1fc54-119">Create documents</span></span>

1. <span data-ttu-id="1fc54-120">먼저 Azure Cosmos DB에 저장할 개체를 나타내는 **User** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-120">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="1fc54-121">**User** 내에서 사용되는 **OrderHistory** 및 **ShippingPreference** 서브클래스도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-121">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="1fc54-122">문서에는 JSON에서 **id**로 직렬화된 **Id** 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-122">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span>

    <span data-ttu-id="1fc54-123">이러한 클래스를 만들려면 **BasicOperations** 메서드 아래에 있는 **User**, **OrderHistory**, **ShippingPreference** 클래스를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-123">To create these classes, copy and paste the following **User**, **OrderHistory**, and **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    ```csharp
    public class User
    {
        [JsonProperty("id")]
        public string Id { get; set; }
        [JsonProperty("userId")]
        public string UserId { get; set; }
        [JsonProperty("lastName")]
        public string LastName { get; set; }
        [JsonProperty("firstName")]
        public string FirstName { get; set; }
        [JsonProperty("email")]
        public string Email { get; set; }
        [JsonProperty("dividend")]
        public string Dividend { get; set; }
        [JsonProperty("OrderHistory")]
        public OrderHistory[] OrderHistory { get; set; }
        [JsonProperty("ShippingPreference")]
        public ShippingPreference[] ShippingPreference { get; set; }
        [JsonProperty("CouponsUsed")]
        public CouponsUsed[] Coupons { get; set; }
        public override string ToString()
        {
            return JsonConvert.SerializeObject(this);
        }
    }

    public class OrderHistory
    {
        public string OrderId { get; set; }
        public string DateShipped { get; set; }
        public string Total { get; set; }
    }

    public class ShippingPreference
    {
        public int Priority { get; set; }
        public string AddressLine1 { get; set; }
        public string AddressLine2 { get; set; }
        public string City { get; set; }
        public string State { get; set; }
        public string ZipCode { get; set; }
        public string Country { get; set; }
    }

    public class CouponsUsed
    {
        public string CouponCode { get; set; }

    }

    private void WriteToConsoleAndPromptToContinue(string format, params object[] args)
    {
        Console.WriteLine(format, args);
        Console.WriteLine("Press any key to continue ...");
        Console.ReadKey();
    }
    ```

1. <span data-ttu-id="1fc54-124">통합 터미널에서 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-124">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

1. <span data-ttu-id="1fc54-125">이제 Program.cs 파일의 끝에 있는 **WriteToConsoleAndPromptToContinue** 함수에서 **CreateUserDocumentIfNotExists** 작업을 복사하고 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-125">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **WriteToConsoleAndPromptToContinue** function at the end of the Program.cs file.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("User {0} already exists in the database", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                await this.client.CreateDocumentAsync(UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), user);
                this.WriteToConsoleAndPromptToContinue("Created User {0}", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="1fc54-126">그런 다음, **BasicOperations** 메서드에 반환하고 해당 메서드의 끝에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-126">Then, return to the **BasicOperations** method and add the following to the end of that method.</span></span>

    ```csharp
    User yanhe = new User
    {
        Id = "1",
        UserId = "yanhe",
        LastName = "He",
        FirstName = "Yan",
        Email = "yanhe@contoso.com",
        OrderHistory = new OrderHistory[]
            {
                new OrderHistory {
                    OrderId = "1000",
                    DateShipped = "08/17/2018",
                    Total = "52.49"
                }
            },
            ShippingPreference = new ShippingPreference[]
            {
                    new ShippingPreference {
                            Priority = 1,
                            AddressLine1 = "90 W 8th St",
                            City = "New York",
                            State = "NY",
                            ZipCode = "10001",
                            Country = "USA"
                    }
            },
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", yanhe);

    User nelapin = new User
    {
        Id = "2",
        UserId = "nelapin",
        LastName = "Pindakova",
        FirstName = "Nela",
        Email = "nelapin@contoso.com",
        Dividend = "8.50",
        OrderHistory = new OrderHistory[]
        {
            new OrderHistory {
                OrderId = "1001",
                DateShipped = "08/17/2018",
                Total = "105.89"
            }
        },
         ShippingPreference = new ShippingPreference[]
        {
            new ShippingPreference {
                    Priority = 1,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            },
            new ShippingPreference {
                    Priority = 2,
                    AddressLine1 = "505 NW 5th St",
                    City = "New York",
                    State = "NY",
                    ZipCode = "10001",
                    Country = "USA"
            }
        },
        Coupons = new CouponsUsed[]
        {
            new CouponsUsed{
                CouponCode = "Fall2018"
            }
        }
    };

    await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);
    ```

1. <span data-ttu-id="1fc54-127">통합 터미널에서 다시 다음 명령을 입력하여 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-127">In the integrated terminal, again, type the following command to run the program.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="1fc54-128">응용 프로그램이 새 사용자 문서를 만들 때마다 터미널에 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-128">The terminal will display output as the application creates each new user document.</span></span> <span data-ttu-id="1fc54-129">아무 키나 눌러 프로그램을 완료합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-129">Press any key to complete the program.</span></span>

    ```output
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="1fc54-130">문서 읽기</span><span class="sxs-lookup"><span data-stu-id="1fc54-130">Read documents</span></span>

1. <span data-ttu-id="1fc54-131">데이터베이스에서 문서를 읽으려면 다음 코드를 복사하여 Program.cs 파일의 WriteToConsoleAndPromptToContinue 메서드 뒤에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-131">To read documents from the database, copy in the following code and place after the WriteToConsoleAndPromptToContinue method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
        try
        {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            this.WriteToConsoleAndPromptToContinue("Read user {0}", user.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not read", user.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="1fc54-132">다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-132">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="1fc54-133">통합 터미널에서 다음 명령을 입력하여 프로그램을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-133">In the integrated terminal, type the following command to run the program.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="1fc54-134">터미널은 다음 출력을 표시합니다. 여기서 “사용자 1 읽음” 출력은 문서가 검색되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-134">The terminal displays the following output, where the output "Read user 1" indicates the document was retrieved.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="1fc54-135">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="1fc54-135">Replace documents</span></span>

<span data-ttu-id="1fc54-136">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-136">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="1fc54-137">이 경우 사용자 레코드를 업데이트하여 사용자의 성 변경을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-137">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="1fc54-138">**ReplaceFamilyDocument** 메서드를 복사하여 Program.cs 파일의 ReadUserDocument 메서드 뒤에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-138">Copy and paste the **ReplaceFamilyDocument** method after the ReadUserDocument method in the Program.cs file.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, User updatedUser)
    {
        try
        {
            await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, updatedUser.Id), updatedUser, new RequestOptions { PartitionKey = new PartitionKey(updatedUser.UserId) });
            this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", updatedUser.LastName);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for replacement", updatedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="1fc54-139">다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-139">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="1fc54-140">통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-140">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```
    <span data-ttu-id="1fc54-141">터미널은 다음 출력을 표시합니다. 여기서, “Suh의 성을 바꿈” 출력은 문서가 바뀌었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-141">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="1fc54-142">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="1fc54-142">Delete documents</span></span>

1. <span data-ttu-id="1fc54-143">**DeleteUserDocument** 메서드를 복사하여 **ReplaceUserDocument** 메서드 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-143">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>

    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, User deletedUser)
    {
        try
        {
            await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, deletedUser.Id), new RequestOptions { PartitionKey = new PartitionKey(deletedUser.UserId) });
            Console.WriteLine("Deleted user {0}", deletedUser.Id);
        }
        catch (DocumentClientException de)
        {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found for deletion", deletedUser.Id);
            }
            else
            {
                throw;
            }
        }
    }
    ```

1. <span data-ttu-id="1fc54-144">다음 코드를 복사하여 **BasicOperations** 메서드 끝에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-144">Copy and paste the following code in the end of the **BasicOperations** method.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="1fc54-145">통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-145">In the integrated terminal, run the following command.</span></span>

    ```bash
    dotnet run
    ```

    <span data-ttu-id="1fc54-146">터미널은 다음 출력을 표시합니다. 여기서 "사용자 1 삭제됨" 출력은 문서가 삭제되었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-146">The terminal displays the following output, where the output "Deleted user 1" indicates the document was deleted.</span></span>

    ```output
    Database and collection validation complete
    User 1 already exists in the database
    Press any key to continue ...
    Replaced last name for Suh
    Press any key to continue ...
    User 2 already exists in the database
    Press any key to continue ...
    Read user 1
    Press any key to continue ...
    Deleted user 1
    End of demo, press any key to exit.
    ```

<span data-ttu-id="1fc54-147">이 단원에서는 Azure Cosmos DB 데이터베이스에서 문서를 만들고, 바꾸고, 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="1fc54-147">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>
