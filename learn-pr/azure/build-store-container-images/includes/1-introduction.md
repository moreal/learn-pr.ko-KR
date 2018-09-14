Azure Container Registry는 오픈 소스 Docker 레지스트리 2.0 기반의 관리되는 Docker 레지스트리 서비스입니다. Container Registry는 Azure에 호스팅된 개인 레지스트리로서 모든 유형의 컨테이너 배포에 대한 이미지를 빌드하고 저장하며 관리할 수 있습니다.

Docker CLI 또는 Azure CLI를 사용하는 Container Registry를 통해 컨테이너 이미지를 밀어넣고 끌어올 수 있습니다. Azure Portal 통합을 통해 Container Registry의 컨테이너 이미지를 시각적으로 검사할 수 있습니다. 분산 환경에서는 지역화된 배포를 위해 Container Registry 지역 복제 기능을 사용하여 컨테이너 이미지를 여러 Azure 데이터 센터에 배포할 수 있습니다.

Azure Container Registry 빌드는 컨테이너 이미지를 저장할 뿐만 아니라 Azure에서 컨테이너 이미지를 빌드할 수도 있습니다. 빌드는 로컬 Docker 도구를 사용할 필요 없이 표준 Dockerfile을 사용하여 Azure Container Registry에 컨테이너 이미지를 만들고 저장합니다. Azure Container Registry 빌드를 사용하면 DevOps 프로세스와 도구를 사용하여 컨테이너 이미지 빌드를 완전히 자동화하거나 요청 시 빌드할 수 있습니다.

## <a name="learning-objectives"></a>학습 목표

이 모듈에서는 다음을 수행합니다.

- Azure Container Registry 배포
- Azure Container Registry 빌드를 사용하여 컨테이너 이미지 빌드
- Azure 컨테이너 인스턴스에 이 컨테이너 배포
- 여러 Azure 데이터 센터에 컨테이너 이미지 복제