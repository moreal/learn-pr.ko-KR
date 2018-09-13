<span data-ttu-id="424f6-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> 응용 프로그램에 문서를 만들었으므로 응용 프로그램에서 문서를 쿼리해 보겠습니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-101"><!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> Now that you've created documents in your application, let's query them from your application.</span></span> <span data-ttu-id="424f6-102">Azure Cosmos DB는 SQL 쿼리 및 LINQ 쿼리를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-102">Azure Cosmos DB uses SQL queries and LINQ queries.</span></span> <span data-ttu-id="424f6-103">Azure Cosmos DB에서 지원하는 SQL 쿼리에 대한 일반 정보는 **데이터베이스의 데이터 추가 및 데이터 쿼리** 모듈에 있습니다. 이 단원에서는 포털과 대조적으로 응용 프로그램에서 SQL 쿼리 및 LINQ 쿼리를 실행하는 데 중점을 둡니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-103">General information about the SQL queries Azure Cosmos DB supports is in **Add data and query data in your database** module; this unit focuses on running SQL queries and LINQ queries from your application, as opposed to the portal.</span></span>

<span data-ttu-id="424f6-104">온라인 판매점 응용 프로그램을 위해 만든 사용자 문서를 사용하여 이러한 쿼리를 테스트합니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-104">We'll use the user documents you've created for your online retailer application to test these queries.</span></span>

## <a name="linq-query-basics"></a><span data-ttu-id="424f6-105">LINQ 쿼리 기본 사항</span><span class="sxs-lookup"><span data-stu-id="424f6-105">LINQ query basics</span></span>

<span data-ttu-id="424f6-106">LINQ는 개체 스트림에 대한 쿼리로 계산을 표현하는 .NET 프로그래밍 모델입니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-106">LINQ is a .NET programming model that expresses computations as queries on streams of objects.</span></span> <span data-ttu-id="424f6-107">Azure Cosmos DB를 직접 쿼리하여 LINQ 쿼리를 Cosmos DB 쿼리로 변환하는 **IQueryable** 개체를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-107">You can create an **IQueryable** object that directly queries Azure Cosmos DB, which translates the LINQ query into a Cosmos DB query.</span></span> <span data-ttu-id="424f6-108">그런 다음, JSON 형식으로 결과 집합을 검색하기 위해 쿼리가 Azure Cosmos DB 서버로 전달됩니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-108">The query is then passed to the Azure Cosmos DB server to retrieve a set of results in JSON format.</span></span> <span data-ttu-id="424f6-109">반환된 결과는 클라이언트 쪽에서 .NET 개체 스트림으로 역직렬화됩니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-109">The returned results are deserialized into a stream of .NET objects on the client side.</span></span> <span data-ttu-id="424f6-110">많은 개발자가 LINQ 쿼리를 선호합니다. 응용 프로그램 코드에서 개체를 사용하는 방법과 데이터베이스에서 실행되는 쿼리 논리 표현 방법에서 일관된 단일 프로그래밍 모델을 제공하기 때문입니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-110">Many developers prefer LINQ queries, as they provide a single consistent programming model across how they work with objects in application code and how they express query logic running in the database.</span></span>

<span data-ttu-id="424f6-111">다음 표는 LINQ 쿼리가 SQL로 변환되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-111">The following table shows how LINQ queries are translated into SQL.</span></span>

| <span data-ttu-id="424f6-112">LINQ 식</span><span class="sxs-lookup"><span data-stu-id="424f6-112">LINQ expression</span></span> | <span data-ttu-id="424f6-113">SQL 변환</span><span class="sxs-lookup"><span data-stu-id="424f6-113">SQL translation</span></span> |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a><span data-ttu-id="424f6-114">SQL 및 LINQ 쿼리 실행</span><span class="sxs-lookup"><span data-stu-id="424f6-114">Run SQL and LINQ queries</span></span>

1. <span data-ttu-id="424f6-115">다음 샘플은 .NET 코드의 SQL, LINQ 또는 LINQ 람다에서 쿼리가 수행되는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-115">The following sample shows how a query could be performed in SQL, LINQ, or LINQ lambda from your .NET code.</span></span> <span data-ttu-id="424f6-116">코드를 복사하여 Program.cs 파일의 끝에 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-116">Copy the code and add it to the end of the Program.cs file.</span></span>

    ```csharp
    private void ExecuteSimpleQuery(string databaseName, string collectionName)
    {
        // Set some common query options
        FeedOptions queryOptions = new FeedOptions { MaxItemCount = -1, EnableCrossPartitionQuery = true };
    
            // Here we find nelapin via their LastName
            IQueryable<User> userQuery = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), queryOptions)
                    .Where(u => u.LastName == "Pindakova");
    
            // The query is executed synchronously here, but can also be executed asynchronously via the IDocumentQuery<T> interface
            Console.WriteLine("Running LINQ query...");
            foreach (User user in userQuery)
            {
                Console.WriteLine("\tRead {0}", user);
            }
    
            // Now execute the same query via direct SQL
            IQueryable<User> userQueryInSql = this.client.CreateDocumentQuery<User>(
                    UriFactory.CreateDocumentCollectionUri(databaseName, collectionName), 
                    "SELECT * FROM User WHERE User.lastName = 'Pindakova'", queryOptions );
    
            Console.WriteLine("Running direct SQL query...");
            foreach (User user in userQueryInSql)
            {
                    Console.WriteLine("\tRead {0}", user);
            }
    
            Console.WriteLine("Press any key to continue ...");
            Console.ReadKey();
    }
    ```

1. <span data-ttu-id="424f6-117">다음 코드를 복사하여 **BasicOperations** 메서드, `await this.DeleteUserDocument("Users", "WebCustomers", "1");` 줄 앞에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-117">Copy and paste the following code to your **BasicOperations** method, before the `await this.DeleteUserDocument("Users", "WebCustomers", "1");` line.</span></span>

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. <span data-ttu-id="424f6-118">Program.cs 파일을 저장한 다음, 통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-118">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>
    
    ```
    dotnet run
    ```

    <span data-ttu-id="424f6-119">LINQ 및 SQL 쿼리의 출력이 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-119">The console displays the output of the LINQ and SQL queries.</span></span>

## <a name="summary"></a><span data-ttu-id="424f6-120">요약</span><span class="sxs-lookup"><span data-stu-id="424f6-120">Summary</span></span>

<span data-ttu-id="424f6-121">이 단원에서는 LINQ 쿼리에 대해 알아보고 사용자 레코드를 검색하기 위해 LINQ 및 SQL 쿼리를 응용 프로그램에 추가했습니다.</span><span class="sxs-lookup"><span data-stu-id="424f6-121">In this unit you learned about LINQ queries, and then added a LINQ and SQL query to your application to retrieve user records.</span></span>