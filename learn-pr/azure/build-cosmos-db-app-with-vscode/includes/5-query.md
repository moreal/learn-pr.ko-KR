<!--TODO: Explain how to do ExecuteNext (pages closer to SDK imp) vs ToList (continuation token)--> 응용 프로그램에 문서를 만들었으므로 응용 프로그램에서 문서를 쿼리해 보겠습니다. Azure Cosmos DB는 SQL 쿼리 및 LINQ 쿼리를 사용합니다. 그러므로 이 단원에서는 SQL 쿼리 및 LINQ 쿼리를 포털이 아닌 응용 프로그램에서 실행하는 방법을 중점적으로 살펴봅니다.

온라인 판매점 응용 프로그램을 위해 만든 사용자 문서를 사용하여 이러한 쿼리를 테스트합니다.

## <a name="linq-query-basics"></a>LINQ 쿼리 기본 사항

LINQ는 개체 스트림에 대한 쿼리로 계산을 표현하는 .NET 프로그래밍 모델입니다. Azure Cosmos DB를 직접 쿼리하여 LINQ 쿼리를 Cosmos DB 쿼리로 변환하는 **IQueryable** 개체를 만들 수 있습니다. 그런 다음, JSON 형식으로 결과 집합을 검색하기 위해 쿼리가 Azure Cosmos DB 서버로 전달됩니다. 반환된 결과는 클라이언트 쪽에서 .NET 개체 스트림으로 역직렬화됩니다. 많은 개발자가 LINQ 쿼리를 선호합니다. 응용 프로그램 코드에서 개체를 사용하는 방법과 데이터베이스에서 실행되는 쿼리 논리 표현 방법에서 일관된 단일 프로그래밍 모델을 제공하기 때문입니다.

다음 표는 LINQ 쿼리가 SQL로 변환되는 방법을 보여 줍니다.

| LINQ 식 | SQL 변환 |
|---|---|
| `input.Select(family => family.parents[0].familyName);`| `SELECT VALUE f.parents[0].familyName FROM Families f` |
|`input.Select(family => family.children[0].grade + c); // c is an int variable` | `SELECT VALUE f.children[0].grade + c FROM Families f` |
|`input.Select(family => new { name = family.children[0].familyName, grade = family.children[0].grade + 3});`| `SELECT VALUE {"name":f.children[0].familyName, "grade": f.children[0].grade + 3 } FROM Families f`|
|`input.Where(family=> family.parents[0].familyName == "Smith");`|`SELECT * FROM Families f WHERE f.parents[0].familyName = "Smith"`|

## <a name="run-sql-and-linq-queries"></a>SQL 및 LINQ 쿼리 실행

1. 다음 샘플은 .NET 코드의 SQL, LINQ 또는 LINQ 람다에서 쿼리가 수행되는 방법을 보여 줍니다. 코드를 복사하여 Program.cs 파일의 끝에 추가합니다.

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

1. **BasicOperations** 메서드에 `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` 줄 앞에 다음 코드를 복사하여 붙여넣습니다.

    ```csharp
    this.ExecuteSimpleQuery("Users", "WebCustomers");
    ```

1. 통합 터미널에서 다음 명령을 실행합니다.

    ```bash
    dotnet run
    ```

    LINQ 및 SQL 쿼리의 출력이 콘솔에 표시됩니다.

이 단원에서는 LINQ 쿼리에 대해 알아보고 사용자 레코드를 검색하기 위해 LINQ 및 SQL 쿼리를 응용 프로그램에 추가했습니다.
