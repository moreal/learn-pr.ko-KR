올바른 저장소 솔루션을 선택하면 성능이 향상될 수 있습니다. 여기에서는 데이터에 대해 배운 내용을 온라인 판매점 시나리오에 적용하고 각 데이터 집합에 가장 적합한 Azure 서비스를 찾아봅니다. 

## <a name="product-catalog-data"></a>제품 카탈로그 데이터

데이터 분류: 반구조적

작업:

* 고객은 데이터베이스 내 많은 필드에 대해 쿼리할 수 있는 기능과 함께 많은 읽기 작업이 필요합니다.
* 비즈니스에서 지속적으로 변하는 재고를 추적하려면 많은 쓰기 작업이 필요합니다.

대기 시간 및 처리량: 높은 처리량 및 낮은 대기 시간

트랜잭션 지원: 필수

### <a name="recommended-service-azure-cosmos-db"></a>권장 서비스: Azure Cosmos DB

Azure Cosmos DB는 디자인별로 반구조적 데이터 또는 NoSQL 데이터를 지원합니다. 따라서 Bluetooth 사용 필드와 같은 새로운 필드나 이후에 필요한 모든 새 필드 지원이 Azure Cosmos DB를 통해 제공됩니다.

작업의 경우 Azure Cosmos DB는 쿼리를 위한 SQL을 지원하고 모든 속성은 기본적으로 인덱싱되므로 거의 모든 항목에서 필터링하여 고객의 요구 사항을 충족하는 쿼리를 만드는 작업이 지원됩니다.

대기 시간과 처리량의 경우 Azure Cosmos DB를 통해 처리량을 구성할 수 있으므로 쇼핑 최대 이용 시간 중 높은 고객 수요를 처리하도록 규모를 확대하거나 이용이 적은 시간 중 규모를 축소하여 비용을 절약할 수 있습니다. 또한 Azure Cosmos DB는 기본적으로 모든 속성을 인덱싱하므로 고객이 모든 필드에 대해 쿼리 가능하게 할 수 있습니다.

Azure Cosmos DB는 ACID도 준수하므로 해당하는 엄격한 요구 사항에 따라 트랜잭션이 완료되었는지 확인할 수 있습니다.

더하기를 추가하면 Azure Cosmos DB를 통해 전 세계 어디에서든 단추 하나만 클릭하여 데이터를 복제할 수도 있습니다. 따라서 전자상거래 사이트가 미국, 프랑스 및 영국의 사용자에 집중되어 있는 경우 해당 데이터 센터로 데이터를 복제하면 사용자에 더 가깝게 물리적으로 데이터를 이동했으므로 대기 시간을 줄일 수 있습니다. 또한 전 세계에서 복제된 데이터로도 다섯 개의 일관성 수준 중 하나를 선택할 수 있으므로 일관성, 가용성, 대기 시간 및 처리량 간에 설정할 절충점을 결정할 수 있습니다.

### <a name="why-not-other-azure-services"></a>다른 Azure 서비스도 사용해 보세요.

Azure Table Storage, HDInsight의 일부인 Azure HBase, Azure Redis Cache 등의 다른 Azure 서비스도 NoSQL 데이터를 저장할 수 있습니다. 이 시나리오에서는 사용자가 여러 필드에 대해 쿼리하려고 하므로 Azure Table Storage, Azure Redis Cache, HDInsight의 일부인 Azure HBase보다 Azure Cosmos DB가 더 적합합니다. Azure Cosmos DB는 기본적으로 모든 필드를 인덱싱하는 데 비해 다른 서비스는 인덱싱하는 데이터에 제한이 있어 데이터베이스의 모든 필드에 대해 쿼리하는 기능이 제한되기 때문입니다.

## <a name="photos-and-videos"></a>사진 및 비디오

데이터 분류: 비구조적

작업:

* 사진 및 비디오는 ID로만 검색해야 합니다.
* 만들기 및 업데이트는 다소 자주 발생하지 않으므로 읽기 작업보다 대기 시간이 더 높을 수 있습니다.

대기 시간 및 처리량: ID별 검색에서는 낮은 대기 시간과 높은 처리량을 지원해야 합니다. 만들기 및 업데이트가 읽기 작업보다 대기 시간이 더 높을 수 있습니다.

트랜잭션 지원: 필요하지 않음

## <a name="recommended-service-azure-blob-storage"></a>권장 서비스: Azure Blob Storage

Azure Blob Storage는 사진 및 비디오 같은 파일의 저장을 지원합니다. Azure CDN(Content Delivery Network)에서도 가장 많이 사용된 콘텐츠를 캐싱하고 에지 서버에 저장하여 작업하므로 사용자에게 해당 이미지를 제공하는 데 걸리는 대기 시간이 줄어듭니다.

또한 Azure Blob Storage를 사용하여 핫 저장소 계층에서 쿨 또는 보관 저장소 계층으로 이미지를 이동함으로써 비용을 절감하고 가장 많이 표시되는 이미지 및 비디오에 대한 처리량에 집중할 수 있습니다.

### <a name="why-not-other-azure-services"></a>다른 Azure 서비스도 사용해 보세요.

Azure App Services에 이미지를 업로드할 수 있으므로 앱을 실행 중인 서버와 동일한 서버가 이미지를 제공합니다. 이미지가 별로 없는 경우에는 효과적이지만 파일 및 글로벌 대상 고객이 많은 경우에는 Azure Blob Storage를 Azure Content Delivery Network와 함께 사용하여 더 뛰어난 성능 결과를 얻을 수 있습니다.

## <a name="business-data"></a>비즈니스 데이터

데이터 분류: 구조적

작업: 여러 데이터베이스 사이의 읽기 전용 복합 분석 쿼리

대기 시간 및 처리량: 결과의 일부 대기 시간은 쿼리의 복잡한 특성에 따라 예상됩니다.

트랜잭션 지원: 필수

### <a name="recommended-service-azure-sql-database"></a>권장 서비스: Azure SQL Database

비즈니스 데이터는 비즈니스 분석가가 쿼리할 가능성이 크고, 비즈니스 분석가는 다른 어떤 쿼리 언어보다도 SQL을 잘 알고 있을 가능성이 큽니다. Azure SQL Database는 그 자체로 솔루션으로 사용될 수 있으나 Azure SQL Database와 Azure Analysis Services를 함께 사용하면 데이터 분석가가 Azure SQL Database의 데이터를 통해 의미 체계 모델을 만들고 비즈니스 사용자와 모델을 공유할 수 있으므로 BI 도구의 모델에 연결하고 곧바로 데이터를 탐색하여 인사이트를 얻을 수 있습니다. 

### <a name="why-not-other-azure-services"></a>다른 Azure 서비스도 사용해 보세요.

Azure SQL Data Warehouse는 OLAP 솔루션과 SQL 쿼리를 지원하지만 비즈니스 분석가는 Azure SQL Data Warehouse에서 지원하지 않는 데이터베이스 간 쿼리를 수행해야 합니다.

Azure SQL Database 외에 Azure Analysis Services를 사용할 수 있으나 비즈니스 분석가는 Power BI로 작업하는 것보다 SQL에 더 정통하므로 Azure Analysis Services에서는 지원하지 않으나 SQL 쿼리를 지원하는 데이터베이스를 사용하는 것이 좋습니다. 또한 비즈니스 데이터 집합에 저장하는 재무 데이터는 관계형이며 다차원적이라는 특징이 있고, Azure Analysis Services는 서비스 자체에서 표 형식 데이터 저장을 지원하지만 다차원 데이터에서는 지원하지 않습니다. Azure Analysis Services를 사용하여 다차원 데이터를 분석하려면 Azure SQL Database에 대해 직접 쿼리를 사용할 수 있습니다.

Azure Stream Analytics는 데이터를 분석하고 실행 가능한 인사이트로 변환하는 좋은 수단이지만, 스트리밍하고 있는 실시간 데이터에 초점을 두므로 이 경우 비즈니스 분석가가 기록 데이터만 확인하게 됩니다.

## <a name="summary"></a>요약

데이터 범주마다 저장소 요구 사항이 서로 다르므로 최상의 솔루션을 알아내야 합니다. 항상 데이터 범주, 필수 작업, 대기 시간 및 트랜잭션 지원 요구 사항을 고려해야 합니다.
