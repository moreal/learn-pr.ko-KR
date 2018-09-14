<span data-ttu-id="255cb-101">데이터베이스의 여러 문서를 동시에 업데이트해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="255cb-102">이 단원에서는 .NET 콘솔 응용 프로그램에서 저장 프로시저를 만들고 등록 및 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="255cb-103">앱에서 저장 프로시저 만들기</span><span class="sxs-lookup"><span data-stu-id="255cb-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="255cb-104">이 저장 프로시저에서 주문의 모든 품목 목록을 포함하는 OrderId는 주문 총액을 계산하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="255cb-105">주문 총액은 주문의 품목 합계에서 고객이 보유한 배당금(대변)을 뺀 금액으로 계산되며, 모든 쿠폰 코드를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-105">The order total is calculated from the sum of the items in the order, less any dividends (credits) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="255cb-106">Visual Studio Code에서에 **Azure: Cosmos DB** 탭에서 Azure Cosmos DB 계정 > **사용자가** > **WebCustomers** 마우스오른쪽단추로클릭하고 **저장 프로시저** 을 클릭 한 다음 **저장 프로시저 만들기**합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-106">In Visual Studio Code, in the **Azure: Cosmos DB** tab, expand your Azure Cosmos DB account > **Users** > **WebCustomers** and then right-click **Stored Procedures** and then click **Create Stored Procedure**.</span></span>

1. <span data-ttu-id="255cb-107">화면 맨 위에 있는 텍스트 상자에 *UpdateOrderTotal*을 입력하고 Enter를 눌러 저장 프로시저의 이름을 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-107">In the text box at the top of the screen, type *UpdateOrderTotal* and click Enter to give the stored procedure a name.</span></span>

1. <span data-ttu-id="255cb-108">에 **Azure: Cosmos DB** 탭에서 **저장 프로시저** 클릭 **UpdateOrderTotal**합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-108">In the **Azure: Cosmos DB** tab, expand **Stored Procedures** and click **UpdateOrderTotal**.</span></span>

    <span data-ttu-id="255cb-109">기본적으로 첫 번째 항목을 검색하는 저장 프로시저가 제공됩니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-109">By default, a stored procedure that retrieves the first item is provided.</span></span>

1. <span data-ttu-id="255cb-110">응용 프로그램에서 이 저장 프로시저를 실행하려면 Program.cs 파일에 다음 코드를 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-110">To run this stored procedure from your application, add the following code to the Program.cs file.</span></span>

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        try
        {
            await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "UpdateOrderTotal"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            Console.WriteLine("Stored procedure complete");
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }
    ```

1. <span data-ttu-id="255cb-111">이제 다음 코드를 복사한 후 붙여 합니다 `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` 줄을 **BasicOperations** 메서드.</span><span class="sxs-lookup"><span data-stu-id="255cb-111">Now copy the following code and paste it before the `await this.DeleteUserDocument("Users", "WebCustomers", yanhe);` line in the **BasicOperations** method.</span></span>

    ```
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. <span data-ttu-id="255cb-112">통합 터미널에서 다음 명령을 실행하여 저장 프로시저가 포함된 샘플을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-112">In the integrated terminal, run the following command to run the sample with the stored procedure.</span></span>

    ```
    dotnet run
    ```
    <span data-ttu-id="255cb-113">저장 프로시저가 완료되었음을 나타내는 출력이 콘솔에 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-113">The console displays output indicating that the stored procedure was completed.</span></span>

## <a name="summary"></a><span data-ttu-id="255cb-114">요약</span><span class="sxs-lookup"><span data-stu-id="255cb-114">Summary</span></span>

<span data-ttu-id="255cb-115">이 모듈에서는 사용자 레코드를 생성, 업데이트, 삭제하고, SQL 및 LINQ를 사용하여 사용자를 쿼리하고, 저장 프로시저를 실행하여 데이터베이스의 항목을 쿼리하는 .NET Core 콘솔 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="255cb-115">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to query items in the database.</span></span>

[!include[](../../../includes/azure-sandbox-cleanup.md)]