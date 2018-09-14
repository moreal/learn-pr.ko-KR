해커는 데이터베이스에 액세스 하려고 한다고 가정 합니다. 데이터베이스에 연결 하는 응용 프로그램 공격에 취약 한 스폿 이며 이러한 응용 프로그램 보안 메서드를 사용 하 여 데이터베이스에 연결 되지 않을 수 있습니다.

데이터베이스 자체 보안 필요는 없지만 데이터베이스를 액세스 하는 방법을 데이터 보안에서 중요 한 역할을 담당할 수 있습니다. 성공적인 데이터베이스 침해 결과인 일반적으로 SQL 삽입 공격. SQL 주입 공격은 데이터베이스에 액세스 하기 위한 기본 사례를 사용 하지 않는 응용 프로그램의 결과입니다.

응용 프로그램 계층에서 데이터베이스를 보호 하는 방법에 살펴보겠습니다.

## <a name="sql-injection-attacks"></a>SQL 삽입 공격

합니다 [OWASP foundation](https://owasp.org) 는 신뢰할 수 있도록 응용 프로그램에 대 한 표준을 작성 하도록 설계 된 비영리 not 조직입니다. 상위 10 개의 보안 취약점의 목록을 정기적으로 게시합니다.

OWASP에 따라 가장 일반적인 취약성은 일반적으로 SQL 주입 공격의 형태는 주입 공격입니다. SQL 문에 전달 되는 정보는 SQL 주입 공격에서 수정 됩니다. 이러한 수정 된 쿼리 중요 한 정보를 반환 하거나 데이터베이스의 악의적인 작업을 수행 합니다.

ADO.NET을 사용 하 여 특정 고객와의 상호 작용을 가져올 다음 ASP.NET Core 코드를 살펴보겠습니다.

```csharp
public List<CustomerInteraction> GetCustomerInteractions(string customerId)
{
    var result = new List<CustomerInteraction>();

    using (var conn = new SqlConnection(ConnectionString))
    {
        var sql = "select Id, CustomerId, InteractionDate, Details " +
            "from CustomerInteractions where CustomerId = '" + customerId + "'";

        using (var command = conn.CreateCommand())
        {
            command.CommandText = sql;
            conn.Open();

            using (var reader = command.ExecuteReader())
            {
                if (reader.HasRows)
                {
                    while (reader.Read())
                        result.Add(GetInteractionsFromReader(reader));
                }
            }
        }
        return result.OrderByDescending(i => i.InteractionDate).ToList();
    }
}
```

쿼리 자체는 customerId 매개 변수는 쿼리를 살펴보기 전에 삭제 되지 않습니다 및 수정할 수 있도록 SQL 공격에 대 한 분산이 됩니다. 쿼리를 호출 하는 웹 사이트는 customerId 매개 변수를 전달 URL 쿼리 문자열에 다음과 같이 합니다.

.../Home/ViewInteractions?customerId=8c69a607-3c09-45ac-9beb-c59ca2de2385

이 전략을 사용 하 여 문제는 customerId 매개 변수를 수정할 수 있습니다. 예를 들어 쿼리에 추가 정보를 배치 하 고 다른 테이블의 데이터를 선택 customerId 매개 변수를 수정할 수 있습니다.

```sql
select Id, CustomerId, InteractionDate, Details from CustomerInteractions where CustomerId = '8c69a607-3c09-45ac-9beb-c59ca2de2385'
```

이제 다음 쿼리를 추가 하 여 추가 정보를 추가 하는 UNION 문을 통해 추가 정보를 추가 하려면 수정할 수 있습니다.

```sql
union select Id, Id as CustomerId, getdate() as InteractionDate, CreditCardNumber + '/' + STR(CreditCardExpiryMonth, 2) + '/' + STR(CreditCardExpiryYear, 4) + ' cvv ' + STR(CreditCardCVV, 3) as Details from Customers --
```

SQL 쿼리는 URL로 인코딩된 되므로 값은 올바른 웹 URL 일부로 허용 됩니다. 웹 사이트에 전달 되는 URL 및 데이터베이스에서 추가 SQL 쿼리를 실행 합니다.

```sql
%27+union+select+Id%2C+Id+as+CustomerId%2C+getdate%28%29+as+InteractionDate%2C+CreditCardNumber+%2B+%27%2F%27+%2B+STR%28CreditCardExpiryMonth%2C+2%29+%2B+%27%2F%27+%2B+STR%28CreditCardExpiryYear%2C+4%29+%2B+%27+cvv+%27+%2B+STR%28CreditCardCVV%2C+3%29+as+Details+from+Customers+--
```

이 예제에서는 어떻게 하지 사이트에서 정보를 삭제 하는 데이터 보안 문제가 발생할 수 있습니다.

![웹 앱을 통해 SQL 주입 공격 시도의 예제를 보여 주는 막대 웹 브라우저 주소의 스크린샷.](../media-draft/4-view-web-page-after-sql-injection.png)

> [!Note]
> 삽입 공격에 대 한 자세한 내용을 알아보려면를 방문 합니다 [OWASP Foundation](https://www.owasp.org/)합니다.

## <a name="avoiding-sql-injection-attacks"></a>SQL 주입 공격 방지

SQL 삽입 공격을 방지 하려면 항상 확인 해야 사용자가 입력 한 입력 정화 됩니다. 쿼리에 대 한 매개 변수로 사용 하는 사용자 입력 문자열 연결을 통해 생성 수 있지만 실제 쿼리 매개 변수로 전달 하면 안 됩니다.

다음 예제에서는 보면 CustomerId 이제 전달 하는 방법을 사용 하 여 매개 변수는 @ 기호입니다. 매개 변수는 명시적으로 정의 하 고 값이 쿼리로 전달 합니다.

```csharp
using (var command = conn.CreateCommand())
{
    var sql = "select Id, CustomerId, InteractionDate, Details " +
        "from CustomerInteractions where CustomerId = @CustomerId order by InteractionDate";

    command.CommandText = sql;
    var prmCustomerId = command.Parameters.Add("@CustomerId", SqlDbType.UniqueIdentifier);
    prmCustomerId.Value = Guid.Parse(customerId);

    conn.Open();

    using (var reader = command.ExecuteReader())
    {
        if (reader.HasRows)
        {
            while (reader.Read())
                result.Add(GetInteractionsFromReader(reader));
        }
    }
}
```

코드의 핵심 줄을 다음과 같습니다.

```csharp
    var prmCustomerId = command.Parameters.Add("@CustomerId", SqlDbType.UniqueIdentifier);
    prmCustomerId.Value = Guid.Parse(customerId);
```

삭제 된 데이터 입력 및 매개 변수가 있는 쿼리를 사용 하 여 데이터베이스에서 SQL 주입 공격의 가능성을 줄입니다.

ASP.NET Core 개념을 설명 하는 데 사용 하는 예제입니다. 그러나 염두에 SQL Server에 대 한 액세스를 지 원하는 모든 프로그래밍 시스템 있는 쿼리에 대 한 값으로 매개 변수를 전달 하는 메커니즘입니다.

## <a name="dynamic-data-masking"></a>동적 데이터 마스킹

보셨을 데이터베이스의 정보 중 일부는 특히 중요 합니다. 아마도 신용 카드 정보입니다. 실제 시스템에서 암호화 되지 않은 신용 카드 정보는 저장 하지 마십시오. 아쉽게도 신용 카드 정보를 암호화 되지 않은 데이터를 숨기는 또 다른 방법은 찾을 해야 하며

쇼핑 웹 사이트를 빌드하는 주문 프로세스 동안 사이트에 있는 신용 카드 세부 정보를 표시할 가정해 보겠습니다. Xxxx-xxxx-1234와 같은 표시 하는 사용자 로부터 차단 처음 12 자리를 표시 하려고 합니다.

이 기술은 동적 데이터 마스킹 라고 합니다. 동적 데이터 마스킹 데이터베이스 내의 열에 대 한 마스크를 추가할 수 있습니다.

1. 에 마스크를 적용 하 고 클릭 하려는 데이터베이스를 선택 하면 포털을 사용 합니다 **동적 데이터 마스킹** 에서 옵션을 **보안** 설정 합니다.

    마스킹 규칙 화면에는 기존 동적 데이터 마스크 및 잠재적으로 적용 한 동적 데이터 마스크 해야 하는 열에 대 한 권장 사항 목록을 표시 합니다.

    ![다양 한 샘플 데이터베이스의 열을 데이터베이스에 대 한 권장 되는 마스크의 목록을 보여 주는 Azure portal의 스크린샷.](../media-draft/4-view-recommended-masked-columns.png)

1. 열에 마스크를 추가 하려면 클릭 합니다 **추가 마스크** 열에 권장 되는 마스크를 추가 하려면 단추입니다.

    ![마스크 함수를 사용 하 고 적용 하는 마스크 된 열을 권장 Auzre 포털 보여 주는 스크린샷.](../media-draft/4-recommended-masks-applied.png)

1. 각 새 마스크 마스킹 규칙 목록에 추가 됩니다. 클릭 합니다 **저장** 마스크를 적용 하는 단추입니다.

데이터베이스 관리자는 열을 쿼리할 때 원래 값이 표시는 되지만 비관리자 마스킹된 값이 표시 됩니다.

다른 사용자가 목록 마스킹에서 제외 된 SQL 사용자에 게 추가 하 여 마스크 되지 않은 버전을 확인할 수 있습니다.

관리자가 아닌 서 쿼리할 같습니다 마스킹된 데이터 여기 볼 수 있습니다.

![전자 메일, 전화 번호, SocialSecurityNumber, 및 CreditCardNumber 표시 하는 데이터베이스 쿼리 스크린샷 결과 열의 비-관리자가 볼 수는 때 마스킹됩니다.](../media-draft/4-sql-query-showing-masks.png)

디스플레이에 마스크 된 추가 권장 사항에 따라는 수동으로 추가할 수 있습니다 마스크를 너무 합니다. 선택 된 + 마스크 단추를 추가 하 고 다음 pop 초과 하면 스키마, 테이블 및 열을 사용 하 여 선택할 수 있습니다. 사용 되는 마스킹을 정의할 수 있습니다. 와 같은 사용할 수 있는 표준 마스크 가지가 있습니다.

- 대신 해당 데이터 형식에 대 한 기본값을 표시 하는 기본값
- 다른 모든 숫자를 소문자로 변환한 x; 번호의 마지막 4 자리 표시는 신용 카드 값
- 이름 및 전자 메일 계정 이름의 첫 번째 문자를 제외한 모든 도메인을 숨기는 전자 메일
- 난수 값의 범위를 지정 하는 번호입니다. 예를 들어, 신용 카드가 만료 월과 연도, 없습니다 임의 개월 1에서 12 선택한 2018 년 범위가 3000;로 또는
- 사용자 지정 문자열입니다. 이 옵션을 사용 하면 데이터의 시작 부분에서 개수 데이터의 끝에서 노출 하는 문자 및 문자 데이터의 나머지 부분에 대 한 반복를 노출 하는 문자 수를 설정할 수 있습니다.
