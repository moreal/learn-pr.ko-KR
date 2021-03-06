비즈니스는 실행하는 시스템 및 데이터에 대한 액세스 권한에 따라 다릅니다. 고객 또는 내부 팀에게 필요한 작업에 대한 액세스 권한이 없는 경우 수익 손실이 발생할 수 있습니다. 이러한 결과가 발생하지 않도록 해야 합니다.

가용성이 높고 지역화된 광범위한 문제에서 복구하는 기능이 있도록 클라우드 솔루션을 설계하는 방법에 대한 알아보았으므로 가상의 Azure 고객이 이러한 원칙을 적용하는 방법을 살펴보겠습니다.

Lamna Healthcare는 국립 의료 서비스 공급자입니다. Lamna Healthcare의 IT 조직은 최근에 대부분의 IT 시스템을 Azure로 이동했습니다. Lamna Healthcare는 다양한 아키텍처와 기술 플랫폼에서 사용자 지정 앱, 오픈 소스 앱, 맞춤형 응용 프로그램을 혼합해서 사용합니다. Lamna Healthcare가 시스템과 데이터 보안을 유지하면서 클라우드로 마이그레이션하려면 무엇이 필요한지 알아보겠습니다.

> [!NOTE]
> 이 모듈에서 설명하는 개념은 모두를 포괄하지는 않지만 클라우드에서 솔루션을 빌드할 때 고려할 몇 가지 중요한 사항을 제시합니다. Microsoft는 Azure에서 응용 프로그램을 설계하는 방법에 대한 광범위한 패턴, 지침 및 예제를 게시합니다. 아키텍처를 계획하고 설계하기 시작할 때 [Azure 아키텍처 센터](https://docs.microsoft.com/azure/architecture/)의 내용을 살펴보는 것이 좋습니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Azure 서비스를 활용하여 고가용성 응용 프로그램 설계
- Azure 재해 복구 기능을 아키텍처에 통합
- 응용 프로그램이 데이터를 손실하거나 손상되지 않도록 Azure에 백업 및 복원