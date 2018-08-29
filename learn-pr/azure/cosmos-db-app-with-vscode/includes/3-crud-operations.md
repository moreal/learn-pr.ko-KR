<!--TODO: explain Etag in knowledge needed-->
<!--TODO: Update to weave in the online retailer story-->


<span data-ttu-id="d5620-101">데이터는 Azure Cosmos DB의 JSON 문서에 저장됩니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-101">Data is stored in JSON documents in Azure Cosmos DB.</span></span> <span data-ttu-id="d5620-102">[문서](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents)는 이전 모듈에 나와 있는 대로 또는 이 모듈에서 설명한 대로 프로그래밍 방식으로 포털에서 만들어지거나, 검색되거나, 바뀌거나, 삭제될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-102">[Documents](https://docs.microsoft.com/azure/cosmos-db/sql-api-resources#documents) can be created, retrieved, replaced, or deleted in the portal, as shown in the previous module, or programmatically, as described in this module.</span></span> <span data-ttu-id="d5620-103">Azure Cosmos DB는 .NET, .NET Core, Java, Node.js 및 Python에 사용되는 클라이언트 쪽 SDK를 제공합니다. 이러한 도구는 각각 해당 작업을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-103">Azure Cosmos DB provides client-side SDKs for .NET, .NET Core, Java, Node.js, and Python, each of which supports these operations.</span></span> <span data-ttu-id="d5620-104">이 모듈에서는 .NET Core SDK를 사용하여 CRUD(만들기, 검색, 업데이트 및 삭제) 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-104">In this module we'll be using the .NET Core SDK to perform CRUD (create, retrieve, update, and delete) operations.</span></span> 

<span data-ttu-id="d5620-105">Azure Cosmos DB 문서에 대한 기본 작업은 [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) 클래스의 일부입니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-105">The main operations for Azure Cosmos DB documents are part of the [DocumentClient](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient?view=azure-dotnet) class:</span></span>
* [<span data-ttu-id="d5620-106">CreateDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="d5620-106">CreateDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.createdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="d5620-107">ReadDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="d5620-107">ReadDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.readdocumentasync?view=azure-dotnet)
* [<span data-ttu-id="d5620-108">ReplaceDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="d5620-108">ReplaceDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.replacedocumentasync?view=azure-dotnet)
* <span data-ttu-id="d5620-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span><span class="sxs-lookup"><span data-stu-id="d5620-109">[UpsertDocumentAsync](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.upsertdocumentasync?view=azure-dotnet).</span></span> <span data-ttu-id="d5620-110">Upsert는 문서가 이미 존재하는지 여부에 따라 만들기 또는 바꾸기 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-110">Upsert performs a create or replace operation depending on whether the document already exists.</span></span>
* [<span data-ttu-id="d5620-111">DeleteDocumentAsync</span><span class="sxs-lookup"><span data-stu-id="d5620-111">DeleteDocumentAsync</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.azure.documents.client.documentclient.deletedocumentasync?view=azure-dotnet)

<span data-ttu-id="d5620-112">이러한 작업을 수행하려면 데이터베이스에 저장된 개체를 나타내는 클래스를 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-112">To perform any of these operations, you need to create a class that represents the object stored in the database.</span></span> <span data-ttu-id="d5620-113">사용자 데이터베이스로 작업하기 때문에 이름 및 사용자 ID(수평적 확장을 사용하도록 설정할 파티션 키이므로 필수임)와 배송 기본 설정 및 주문 기록에 대한 서브클래스 같은 기본 데이터를 저장할 **User** 클래스를 작성해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-113">Because we're working with a database of users, you'll want to create a **User** class to store primary data such as their name and UserId (which is required, as that's the partition key to enable horizontal scaling) and subclasses for shipping preferences and order history.</span></span>

<span data-ttu-id="d5620-114">사용자를 나타내는 해당 클래스가 만들어져 있으면 각 인스턴스에 대한 새 사용자 문서를 만든 후에 문서에서 몇 가지 간단한 CRUD 작업을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-114">Once you have those classes created to represent your users, you'll create new user documents for each instance, and then we'll perform some simple CRUD operations on the documents.</span></span>

## <a name="create-documents"></a><span data-ttu-id="d5620-115">문서 만들기</span><span class="sxs-lookup"><span data-stu-id="d5620-115">Create documents</span></span>

1. <span data-ttu-id="d5620-116">먼저 Azure Cosmos DB에 저장할 개체를 나타내는 **User** 클래스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-116">First, create a **User** class that represents the objects to store in Azure Cosmos DB.</span></span> <span data-ttu-id="d5620-117">**User** 내에서 사용되는 **OrderHistory** 및 **ShippingPreference** 서브클래스도 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-117">We will also create **OrderHistory** and **ShippingPreference** subclasses that are used within **User**.</span></span> <span data-ttu-id="d5620-118">문서에는 JSON에서 **ID**로 직렬화된 **ID** 속성이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-118">Note that documents must have an **Id** property serialized as **id** in JSON.</span></span> 

    <span data-ttu-id="d5620-119">이러한 클래스를 만들려면 **BasicOperations** 메서드 아래에 있는 **User**, **OrderHistory**, **ShippingPreference** 클래스를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-119">To create these classes, copy and paste the following **User**, **OrderHistory**, **ShippingPreference** classes underneath the **BasicOperations** method.</span></span>

    <!--TODO: specify JSON for all of these? -->
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
            public OrderHistory[] OrderHistory { get; set; }
            public ShippingPreference[] ShippingPreference { get; set; }
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

2. <span data-ttu-id="d5620-120">통합 터미널에서 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-120">In the integrated terminal, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

3. <span data-ttu-id="d5620-121">이제 **ShippingPreference** 클래스 아래의 **CreateUserDocumentIfNotExists** 작업을 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-121">Now copy and paste the **CreateUserDocumentIfNotExists** task under the **ShippingPreference** class.</span></span>

    ```csharp
    private async Task CreateUserDocumentIfNotExists(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found {0}", user.Id);
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

4. <span data-ttu-id="d5620-122">그런 다음, **BasicOperations** 메서드에 다음을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-122">Then add the following to the **BasicOperations** method.</span></span>

    ```csharp
     User yanhe = new User
                {
                    Id = "1",
                    UserId = "yanhe",
                    LastName = "He",
                    FirstName = "Yan",
                    Email = "yanhe@todo.com",
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
                    Email = "nelapin@todo.com",
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

5. <span data-ttu-id="d5620-123">통합 터미널에서 다시 다음 명령을 입력하고 프로그램을 실행하여 프로그램이 실행되는 것을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-123">In the integrated terminal, again, type the following command to run the program to ensure it runs.</span></span>

    ```csharp
    dotnet run
    ```

    <span data-ttu-id="d5620-124">터미널은 사용자 레코드가 둘 다 성공적으로 만들어졌음을 나타내는 다음 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-124">The terminal displays the following output, indicating that both user records were successfully created.</span></span> 

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="read-documents"></a><span data-ttu-id="d5620-125">문서 읽기</span><span class="sxs-lookup"><span data-stu-id="d5620-125">Read documents</span></span>

1. <span data-ttu-id="d5620-126">데이터베이스에서 문서를 읽으려면 다음 코드에서 복사하여 Program.cs 파일 끝에 놓습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-126">To read documents from the database, copy in the following code and place it at the end of the Program.cs file.</span></span>

    ```csharp
    private async Task ReadUserDocument(string databaseName, string collectionName, User user)
    {
            try
            {
            await this.client.ReadDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, user.Id), new RequestOptions { PartitionKey = new PartitionKey("user.userId") });
            this.WriteToConsoleAndPromptToContinue("Found user {0}", user.Id);
            }
            catch (DocumentClientException de)
            {
            if (de.StatusCode == HttpStatusCode.NotFound)
            {
                this.WriteToConsoleAndPromptToContinue("User {0} not found", user.Id);
            }
            else
            {
                throw;
            }
            }
    }
    ```

2.  <span data-ttu-id="d5620-127">다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-127">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    await this.ReadUserDocument("Users", "WebCustomers", yanhe);
    ```

4. <span data-ttu-id="d5620-128">Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-128">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="d5620-129">터미널은 “사용자 1 찾음” 출력이 문서를 찾았음을 나타내는 다음 출력을 표시합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-129">The terminal displays the following output, where the output "Found user 1" indicates the document was found.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    End of demo, press any key to exit.
    ```

## <a name="replace-documents"></a><span data-ttu-id="d5620-130">문서 바꾸기</span><span class="sxs-lookup"><span data-stu-id="d5620-130">Replace documents</span></span>
<span data-ttu-id="d5620-131">Azure Cosmos DB는 JSON 문서 바꾸기를 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-131">Azure Cosmos DB supports replacing JSON documents.</span></span> <span data-ttu-id="d5620-132">이 경우 사용자 레코드를 업데이트하여 사용자의 성 변경을 처리합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-132">In this case, we'll update a user record to account for a change to their last name.</span></span>

1. <span data-ttu-id="d5620-133">**ReplaceFamilyDocument** 메서드를 복사하여 **CreateUserDocumentIfNotExists** 메서드 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-133">Copy and paste the **ReplaceFamilyDocument** method underneath your **CreateUserDocumentIfNotExists** method.</span></span>

    ```csharp
    private async Task ReplaceUserDocument(string databaseName, string collectionName, string LastName, User updatedUser)
    {
        await this.client.ReplaceDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, LastName), updatedUser);
        this.WriteToConsoleAndPromptToContinue("Replaced last name for {0}", LastName);
    }
    ```

2. <span data-ttu-id="d5620-134">다음 코드를 복사하여 **BasicOperations** 메서드 끝의 `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` 줄 뒤에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-134">Copy and paste the following code to the end of the **BasicOperations** method, after the `await this.CreateUserDocumentIfNotExists("Users", "WebCustomers", nelapin);` line.</span></span>

    ```csharp
    yanhe.LastName = "Suh";
    await this.ReplaceUserDocument("Users", "WebCustomers", yanhe.LastName, yanhe);
    ```
    <!--TODO: need to fix this as it's giving an error-->

4. <span data-ttu-id="d5620-135">Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-135">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="d5620-136">터미널은 다음 출력을 표시합니다. 여기서, “Suh의 성을 바꿈” 출력은 문서가 바뀌었음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-136">The terminal displays the following output, where the output "Replaced last name for Suh" indicates the document was replaced.</span></span>

    ```
    Database and collection validation complete
    Created User 1
    Press any key to continue ...
    Created User 2
    Press any key to continue ...
    Found user 1
    Press any key to continue ...
    Replaced last name for Suh 
    End of demo, press any key to exit.
    ```

## <a name="delete-documents"></a><span data-ttu-id="d5620-137">문서 삭제</span><span class="sxs-lookup"><span data-stu-id="d5620-137">Delete documents</span></span>

1. <span data-ttu-id="d5620-138">**DeleteUserDocument** 메서드를 복사하여 **ReplaceUserDocument** 메서드 아래에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-138">Copy and paste the **DeleteUserDocument** method underneath your **ReplaceUserDocument** method.</span></span>
    
    ```csharp
    private async Task DeleteUserDocument(string databaseName, string collectionName, string documentName)
    {
        await this.client.DeleteDocumentAsync(UriFactory.CreateDocumentUri(databaseName, collectionName, documentName), new RequestOptions { PartitionKey = new PartitionKey("User.UserId") });
        Console.WriteLine("Deleted User {0}", documentName);
    }
    ```

2. <span data-ttu-id="d5620-139">두 번째 쿼리 실행의 **BasicOperations** 메서드에 다음 코드를 복사하여 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-139">Copy and paste the following code to your **BasicOperations** method underneath the second query execution.</span></span>

    ```csharp
    await this.DeleteUserDocument("Users", "WebCustomers", "1");
    ```

3. <span data-ttu-id="d5620-140">Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-140">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="d5620-141">축하합니다!</span><span class="sxs-lookup"><span data-stu-id="d5620-141">Congratulations!</span></span> <span data-ttu-id="d5620-142">Azure Cosmos DB 문서를 성공적으로 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-142">You have successfully deleted an Azure Cosmos DB document.</span></span>

## <a name="summary"></a><span data-ttu-id="d5620-143">요약</span><span class="sxs-lookup"><span data-stu-id="d5620-143">Summary</span></span>

<span data-ttu-id="d5620-144">이 단원에서는 Azure Cosmos DB 데이터베이스에서 문서를 만들고, 바꾸고, 삭제했습니다.</span><span class="sxs-lookup"><span data-stu-id="d5620-144">In this unit you created, replaced, and deleted documents in your Azure Cosmos DB database.</span></span>