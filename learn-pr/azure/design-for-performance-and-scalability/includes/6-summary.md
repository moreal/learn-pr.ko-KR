축하합니다. 성능 및 확장성에 대한 모듈을 완료했습니다. 진행한 내용을 요약하면 다음과 같습니다.

## <a name="scaling-up-and-scaling-out"></a>확장 및 스케일 아웃

- 확장/축소(인스턴스에 프로비전된 리소스 수준) 및 스케일 인/스케일 아웃(사용 가능한 인스턴스 수 늘리기 또는 줄이기) 간 차이점. 또한 Azure의 각 예제도 살펴보았습니다.
- 상태 관리 및 응용 프로그램 시작 시간과 관련해서 스케일 인/스케일 아웃을 수행할 때 고려할 사항.
- 자동 크기 조정 및 이 기능이 응용 프로그램의 일정 또는 수요에 따라 인스턴스 수를 조정하는 데 도움을 주는 방식.
- 서버리스 및 컨테이너를 비롯하여 확장성에 도움이 되는 대체 기술을 살펴보았습니다.

## <a name="optimize-network-performance"></a>네트워크 성능 최적화

- 네트워크 대기 시간은 발신자에서 수신자로 전송되는 데이터의 지연 시간을 측정한 것입니다.
- 온-프레미스에 비해 클라우드 환경에서는 리소스가 더 이상 즉시 공동 배치되지 않으므로 통신량이 많은 응용 프로그램의 성능이 더 많은 영향을 받을 수 있습니다.
- 데이터베이스 쓰기 엔드포인트 근처에 API를 공동 배치하면 두 리소스 간에 네트워크 대기 시간이 줄어들어 성능상의 이점을 제공할 수 있습니다.
- Azure Traffic Manager를 사용하여 네트워크 대기 시간이 가장 적게 배포된 인스턴스로 사용자를 라우팅할 수 있습니다.
- Azure CDN(Content Delivery Network)을 사용하면 사용자에게 가까운 CDN 에지 노드에 콘텐츠를 캐시하여 기본 응용 프로그램에서 계산을 오프로드하고 응용 프로그램 로드 시간을 단축할 수 있습니다.

## <a name="optimize-storage-performance"></a>저장소 성능 최적화

- IaaS(Infrastructure as a Service) 배포에는 세 가지 기본 디스크 유형을 사용할 수 있습니다. 바로, 표준 HDD 디스크(대기 시간이 일관되지 않고 처리량 수준이 낮음), 표준 SSD 디스크(대기 시간이 일관되고 처리량 수준이 낮음) 및 프리미엄 SSD 디스크(대기 시간이 일관되고 처리량 수준이 높음)입니다.
- 응용 프로그램 계층에서 캐싱을 사용하여 응용 프로그램의 로드 시간을 향상시킬 수 있습니다. 자주 요청되는 정보는 데이터베이스 앞의 캐시에 저장될 수 있으므로 가장 자주 요청되는 정보의 데이터 로드 시간에 맞게 최적화할 수 있습니다.
- 솔루션을 빌드할 때 작업에 대해 적절한 백 엔드 데이터 저장소를 사용하는 방식을 고려하는 것이 좋습니다(다중저장소 지속성).

## <a name="identify-performance-bottlenecks"></a>성능 병목 상태 식별

- 작업을 설계하거나 구축하기 전에 응용 프로그램의 예상 성능 파악의 중요성.
- 효과적인 DevOps 전략이 보다 강력하고 성능이 뛰어난 응용 프로그램을 빌드하는 데 어떻게 도움을 줄 수 있는지에 대한 이해.
- Azure Monitor(Azure에서 모니터링하기 위한 창), Azure Log Analytics(로그 수집 및 IaaS 모니터링) 및 Application Insights(가용성, 성능 및 예외 정보를 포함하는 응용 프로그램 성능 모니터링)를 포함하여 Azure에서 사용 가능한 모니터링 옵션을 요약하였습니다.