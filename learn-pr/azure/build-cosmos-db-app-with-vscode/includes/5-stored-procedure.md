데이터베이스의 여러 문서를 동시에 업데이트해야 하는 경우가 많습니다. 이 단원에서는 .NET 콘솔 응용 프로그램에서 저장 프로시저를 만들고 등록 및 실행하는 방법을 설명합니다.

## <a name="create-a-stored-procedure-in-your-app"></a>앱에서 저장 프로시저 만들기

이 저장 프로시저에서 주문의 모든 품목 목록을 포함하는 OrderId는 주문 총액을 계산하는 데 사용됩니다. 주문 총액은 주문의 품목 합계에서 고객이 보유한 배당금(대변)을 뺀 금액으로 계산되며, 모든 쿠폰 코드를 고려합니다.

1. Visual Studio Code의 Azure 탭에서 **학습 모듈(SQL)** > **사용자** > **WebCustomers**를 확장한 다음, **저장 프로시저**를 마우스 오른쪽 단추로 클릭하고 **저장 프로시저 만들기**를 클릭합니다.

1. 화면 맨 위에 있는 텍스트 상자에 *UpdateOrderTotal*을 입력하고 Enter를 눌러 저장 프로시저의 이름을 지정합니다.

1. **저장 프로시저**를 확장하고 **UpdateOrderTotal**을 클릭합니다.

1. 기본적으로 첫 번째 항목을 검색하는 저장 프로시저가 제공됩니다.

1. 응용 프로그램에서 이 저장 프로시저를 실행하려면 Program.cs 파일에 다음 코드를 추가합니다.

    ```csharp
    public async Task RunStoredProcedure(string databaseName, string collectionName, User user)
    {
        try
        {
            await client.ExecuteStoredProcedureAsync<string>(UriFactory.CreateStoredProcedureUri(databaseName, collectionName, "sample"), new RequestOptions { PartitionKey = new PartitionKey(user.UserId) });
            Console.WriteLine("Stored procedure complete");
        }
        catch (DocumentClientException de)
        {
            throw;
        }
    }
    ```
    <!--TODO: Update sproc to take order total and check for available dividend, and use of summer coupon code, and provide updated total-->

1. 이제 다음 코드를 복사하여 **BasicOperations** 메서드의 끝에 붙여넣습니다.

    ```
    await this.RunStoredProcedure("Users", "WebCustomers", yanhe);
    ```

1. 통합 터미널에서 다음 명령을 실행하여 저장 프로시저가 포함된 샘플을 실행합니다.

    ```
    dotnet run
    ```
    저장 프로시저가 완료되었음을 나타내는 출력이 콘솔에 표시됩니다.

## <a name="clean-up"></a>정리
<!---TODO: Update for sandbox?--->

이 학습 경로의 모듈에서 계속 작업하려면 정리 프로세스를 건너뛰거나, 다음 단계를 사용하여 서비스 사용 요금이 발생하지 않도록 리소스를 삭제합니다.

1. Azure Portal에서 맨 왼쪽에 있는 **리소스 그룹**을 선택한 후에 만든 리소스 그룹을 선택합니다.  

    왼쪽 메뉴가 접혀 있으면 ![[확장] 단추를](../media/5-javascript-programming/expand.png) 클릭하여 펼칩니다.

   ![Azure Portal의 메트릭](../media/5-javascript-programming/delete-resources-select.png)

1. 새 창에서 리소스 그룹을 선택한 후에 **리소스 그룹 삭제**를 클릭합니다.

   ![Azure Portal의 메트릭](../media/5-javascript-programming/delete-resources.png)

1. 새 창에서 삭제할 리소스 그룹의 이름을 입력한 후에 **삭제**를 클릭합니다.

## <a name="summary"></a>요약

이 모듈에서는 사용자 레코드를 생성, 업데이트, 삭제하고, SQL 및 LINQ를 사용하여 사용자를 쿼리하고, 저장 프로시저를 실행하여 데이터베이스의 항목을 쿼리하는 .NET Core 콘솔 응용 프로그램을 만들었습니다.