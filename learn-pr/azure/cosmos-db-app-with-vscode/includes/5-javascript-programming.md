<span data-ttu-id="682a4-101">데이터베이스의 여러 문서를 동시에 업데이트해야 하는 경우가 많습니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-101">Multiple documents in your database frequently need to be updated at the same time.</span></span> <span data-ttu-id="682a4-102">이 단원에서는 .NET 콘솔 응용 프로그램에서 저장 프로시저를 만들고 등록 및 실행하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-102">This unit discusses how to create, register, and run stored procedures from your .NET console application.</span></span>

## <a name="create-a-stored-procedure-in-your-app"></a><span data-ttu-id="682a4-103">앱에서 저장 프로시저 만들기</span><span class="sxs-lookup"><span data-stu-id="682a4-103">Create a stored procedure in your app</span></span>

<span data-ttu-id="682a4-104">이 저장 프로시저에서 주문의 모든 품목 목록을 포함하는 OrderId는 주문 총액을 계산하는 데 사용됩니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-104">In this stored procedure, the OrderId, which contains a list of all the items in the order, is used to calculate an order total.</span></span> <span data-ttu-id="682a4-105">주문 총액은 주문의 품목 합계에서 고객이 보유한 배당금(대변)을 뺀 금액으로 계산되며, 모든 쿠폰 코드를 고려합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-105">The order total is calculated from the sum of the items in the order, less any dividend (credit) the customer has, and takes any coupon codes into account.</span></span>

1. <span data-ttu-id="682a4-106">다음 코드를 복사하여 Program.cs 파일의 끝에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-106">Copy the following code and paste it into the end of the Program.cs file.</span></span>

    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->
    ```csharp
    private async Task UpdateOrderTotal(string databaseName, string collectionName, Order orderId)
    {
    var markAntiquesSproc = new StoredProcedure
    {
        Id = "ValidateDocumentAge",
        Body = @"
                function(docToCreate, antiqueYear) {
                    var collection = getContext().getCollection();    
                    var response = getContext().getResponse();    
    
                    if(docToCreate.Year != undefined && docToCreate.Year < antiqueYear){
                        docToCreate.antique = true;
                    }
    
                    collection.createDocument(collection.getSelfLink(), docToCreate, {}, 
                        function(err, docCreated, options) { 
                            if(err) throw new Error('Error while creating document: ' + err.message);                              
                            if(options.maxCollectionSizeInMb == 0) throw 'max collection size not found'; 
                            response.setBody(docCreated);
                    });
             }"
    };
    // register stored procedure
    StoredProcedure createdStoredProcedure = await client.CreateStoredProcedureAsync(UriFactory.CreateDocumentCollectionUri("db", "coll"), markAntiquesSproc);
    dynamic document = new Document() { Id = "Borges_112" };
    document.Title = "Aleph";
    document.Year = 1949;
    
    // execute stored procedure
    Document createdDocument = await client.ExecuteStoredProcedureAsync<Document>(UriFactory.CreateStoredProcedureUri("db", "coll", "ValidateDocumentAge"), document, 1920);
    }
    ```

2. <span data-ttu-id="682a4-107">이제 다음 코드를 복사하여 **BasicOperations** 메서드의 끝에 붙여넣습니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-107">Now copy the following code and paste it into the end of the **BasicOperations** method.</span></span>

    ```
    await this.UpdateOrderTotal("Users", "WebCustomers", "5-6235");
    ```

3. <span data-ttu-id="682a4-108">Program.cs 파일을 저장한 후에 통합 터미널에서 다음 명령을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-108">Save the Program.cs file and then, in the integrated terminal, run the following command.</span></span>

    ```
    dotnet run
    ```

    <span data-ttu-id="682a4-109">콘솔에 다음 출력이 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-109">The console displays the following output.</span></span>

    ```
    Order total is 90.85.
    Press any key to continue ...
    ```

## <a name="clean-up"></a><span data-ttu-id="682a4-110">정리</span><span class="sxs-lookup"><span data-stu-id="682a4-110">Clean up</span></span>

<span data-ttu-id="682a4-111">이 학습 경로의 모듈에서 계속 작업하려면 정리 프로세스를 건너뛰거나, 다음 단계를 사용하여 서비스 사용 요금이 발생하지 않도록 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-111">If you plan to continue working on the modules in this learning path, skip the clean-up process, or else use the following steps to delete your resources to avoid incurring charges for use of the service.</span></span>

1. <span data-ttu-id="682a4-112">Azure Portal에서 맨 왼쪽에 있는 **리소스 그룹**을 선택한 후에 만든 리소스 그룹을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-112">In the Azure portal, select **Resource groups** on the far left, and then select the resource group you created.</span></span>  

    <span data-ttu-id="682a4-113">왼쪽 메뉴가 접혀 있으면</span><span class="sxs-lookup"><span data-stu-id="682a4-113">If the left menu is collapsed, click</span></span> ![[확장] 단추를](../media/5-javascript-programming/expand.png) <span data-ttu-id="682a4-115">클릭하여 펼칩니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-115">to expand it.</span></span>

   ![Azure Portal의 메트릭](../media/5-javascript-programming/delete-resources-select.png)

2. <span data-ttu-id="682a4-117">새 창에서 리소스 그룹을 선택한 후에 **리소스 그룹 삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-117">In the new window select the resource group, and then click **Delete resource group**.</span></span>

   ![Azure Portal의 메트릭](../media/5-javascript-programming/delete-resources.png)

3. <span data-ttu-id="682a4-119">새 창에서 삭제할 리소스 그룹의 이름을 입력한 후에 **삭제**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-119">In the new window, type the name of the resource group to delete, and then click **Delete**.</span></span>

## <a name="summary"></a><span data-ttu-id="682a4-120">요약</span><span class="sxs-lookup"><span data-stu-id="682a4-120">Summary</span></span>

<span data-ttu-id="682a4-121">이 모듈에서는 사용자 레코드를 생성, 업데이트 및 삭제하고, SQL 및 LINQ를 사용하여 사용자를 쿼리하며, 저장 프로시저를 실행하여 사용자 배당금과 쿠폰을 고려하는 주문 총액을 만드는 .NET Core 콘솔 응용 프로그램을 만들었습니다.</span><span class="sxs-lookup"><span data-stu-id="682a4-121">In this module you've created a .NET Core console application that creates, updates, and deletes user records, queries the users by using SQL and LINQ, and runs a stored procedure to create an order total that takes the users dividends and coupons into account.</span></span>