컨테이너는 클라우드 응용 프로그램을 패키지, 배포 및 관리하기 위한 기본 방법으로 도입되고 있습니다. Azure Container Instances는 어떠한 가상 머신도 관리하지 않고 또 더 높은 수준의 서비스를 채택하지 않고도 Azure에서 컨테이너를 실행하는 가장 빠르고 간단한 방법을 제공합니다.

Azure Container Instances는 간단한 응용 프로그램, 작업 자동화 및 빌드 작업 등 격리된 컨테이너에서 작동할 수 있는 모든 시나리오에 적합한 솔루션입니다. 여러 컨테이너 간 서비스 검색, 자동 크기 조정 및 조정된 응용 프로그램 업그레이드를 포함하여 전체 컨테이너 오케스트레이션이 필요한 시나리오에는 AKS(Azure Kubernetes Service)를 사용하는 것이 좋습니다.

Azure Container Instances는 다음과 같은 이점을 제공합니다.

- **빠른 시작**: Azure Container Instances는 Azure의 컨테이너를 몇 초 안에 시작할 수 있습니다.
- **초당 청구**: 컨테이너가 실행되는 동안에만 비용이 청구됩니다.
- **하이퍼바이저 수준 보안**: Azure Container Instances는 응용 프로그램이 VM에서 격리되는 것처럼 컨테이너에서도 격리되도록 보장합니다.
- **사용자 지정 크기**: Azure Container Instances는 CPU 코어 및 메모리의 정확한 사양을 허용하여 최적의 활용도를 제공합니다.
- **영구적 저장소**: Azure Container Instances를 통해 상태를 검색하고 유지할 수 있도록 직접 Azure Files 공유를 탑재시킵니다.
- **Linux 및 Windows**: Azure Container Instances는 동일한 API로 Windows 및 Linux 컨테이너를 모두 예약할 수 있습니다.

## <a name="learning-objectives"></a>학습 목표  

이 모듈에서는 다음을 수행합니다.

- Azure Container Instances에서 컨테이너를 실행합니다.
- 컨테이너 다시 시작 동작을 제어합니다.
- 컨테이너에서 환경 변수를 사용합니다.
- Azure Container Instance에 데이터 볼륨을 연결합니다.
- Azure Container Instances 문제 해결에 대해 알아봅니다.