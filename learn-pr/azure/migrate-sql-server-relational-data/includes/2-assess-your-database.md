Azure의 확장성 및 가용성을 활용하기 위해 SQL Server 데이터베이스를 Azure SQL Database로 이동하기로 결정했습니다. 단, 현재 온-프레미스 SQL Server에서 사용하는 모든 기능이 Azure SQL Server에서도 제공되는지 유효성을 검사하고자 합니다.

Data Migration Assistant 도구를 사용하여 기존 데이터베이스와 Azure SQL Server의 호환성을 평가할 것입니다.

## <a name="what-is-the-data-migration-assistant-dma"></a>DMA(Data Migration Assistant)란?

Data Migration Assistant는 온-프레미스 SQL Server 인스턴스 분석 전용 도구입니다. 이 도구는 SQL 데이터베이스를 Azure SQL Server로 마이그레이션하는 과정을 지연시킬 수 있는 일반적인 문제를 검색하여 보고합니다.

그리고 마이그레이션을 차단할 수 있는 호환성 문제를 검색할 뿐 아니라, 온-프레미스 서버에서 사용되는 기능 중 부분적으로만 지원되거나 지원되지 않는 기능도 인식합니다.

또한 마이그레이션 전에 온-프레미스 서버에서 수행해야 하는 권장 작업도 포괄적으로 제공합니다.

### <a name="why-do-you-need-data-migration-assistant"></a>Data Migration Assistant가 필요한 이유

Azure SQL Database는 계속 개발 중인 상태이며 현재 SQL Server의 일부 기능을 지원하지 않습니다.

최신 기능 목록은 [Azure SQL Database 기능 목록](https://docs.microsoft.com/azure/sql-database/sql-database-features)에서 확인할 수 있습니다.

## <a name="how-to-assess-your-database-using-data-migration-assistant"></a>Data Migration Assistant를 사용하여 데이터베이스를 평가하는 방법

Data Migration Assistant를 사용하여 데이터베이스를 평가할 때는 대개 다음 단계를 수행합니다.

- **Data Migration Assistant 설치** – https://www.microsoft.com/download/details.aspx?id=53595에서 Data Migration Assistant를 다운로드하여 설치합니다. Azure SQL Database는 정기적으로 업데이트되며 Data Migration Assistant도 새로운 기능을 반영하도록 업데이트됩니다. 따라서 설치 관리자를 실행해 최신 버전이 설치되어 있는지를 확인하는 것이 좋습니다.
- **평가 만들기** – 온-프레미스 데이터베이스와 대상 데이터베이스를 정의하는 새 평가를 만듭니다. Azure Virtual Machines에서 SQL Server의 다른 대상을 평가하여 대체 마이그레이션을 비교할 수도 있습니다.
- **평가 및 데이터베이스 원본에 대한 옵션 선택** – 두 데이터베이스 간의 호환성이나 기능 패리티를 확인할지 여부 등의 옵션을 선택합니다. 그런 다음 원본 데이터베이스를 선택합니다. 여러 원본을 선택할 수 있습니다.
- **결과 검토** - 상세 결과에서 오류를 검토하고 정정 작업을 수행할 수 있습니다. 결과에는 지원되지 않는 기능과 함께 데이터베이스 간 참조 및 SQL Server 에이전트가 표시됩니다. 그리고 부분적으로 지원되는 기능 목록과 전체 텍스트 검색 및 감사 기능도 제공됩니다. 결과에서는 발생 가능한 오류 및 해당 오류를 수정하는 방법을 제공합니다. Data Migration Assistant 결과는 .json 파일로 내보낼 수 있습니다.
