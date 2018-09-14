Azure에서 컨테이너 또는 컨테이너 통합 응용 프로그램을 실행하기 전에는 대부분 노트북 같은 로컬 개발 환경에서 작업합니다. 여기에서 Docker 사용 하 여 컨테이너 개발을 위한 시스템을 준비 합니다.

## <a name="why-use-containers"></a>컨테이너를 사용하는 이유

컨테이너와 컨테이너 이미지는 디스크 공간, 메모리 및 CPU 같은 호스트 리소스를 효율적으로 사용 합니다. 이러한 효율성 덕분에 컨테이너가 신속하게 시작됩니다. 컨테이너의 새 인스턴스가 거의 즉시 시작되는 경우도 있습니다. 이 응용 프로그램의 신속한 프로 비전을 통해 주문형으로 처리 및 크기 조정 작업의 새 모델을 사용할 수 있습니다.

가끔 수요가 급증하는 일괄 처리 서비스를 실행하는 시나리오를 가정해 봅시다. 컨테이너 수 신속 하 게 새 인스턴스를 프로 비전 하 여 증가 되는 수요에 반응 하는 시스템을 구축할 수 있습니다. 이 시스템은 강력하며 기존의 가상 머신으로는 구현하기가 쉽지 않습니다.

컨테이너를 사용 하면 "하이퍼 밀도"를 달성 하기 위해 수도 있습니다. 즉, 적은 가상 또는 물리적 리소스를 사용 하 여 더 많은 응용 프로그램 및 프로세스를 실행할 수 있습니다.

컨테이너는 웹 서버 같은 기존 워크로드를 실행하기에 적합한 플랫폼이지만, 확장 가능한 일괄 처리, 최신 분산 아키텍처를 사용하여 빌드한 응용 프로그램, 주문형 크기 조정이 필요한 기타 시스템 등과 같은 기회를 제공합니다.

## <a name="docker-for-windows-and-mac"></a>Windows 및 Mac용 Docker

Docker, Inc. 설치 로컬 컨테이너 개발 환경을 구성 하는 두 개의 응용 프로그램을 게시 했습니다. 응용 프로그램 준비 도구, CLI 및 자동화에 필요한 도구와 같은 Docker를 사용 하 여 시스템입니다. Docker 플랫폼을 호스팅하는 가상 머신도 만듭니다. Docker 명령이 가상 머신으로 전달되도록 환경이 구성됩니다. 각 응용 프로그램은 서로 기능이 비슷하며 다음과 같은 특징을 갖고 있습니다.

- **Docker 플랫폼:** 만들고 컨테이너를 실행 하는 데 필요한 핵심 구성 요소입니다.
- **Docker CLI:** Docker 컨테이너를 사용 하 여 상호 작용 하기 위한 명령줄 인터페이스입니다.
- **Docker Compose:** 자동화 도구를 정의 하 고 다중 컨테이너 응용 프로그램을 실행 합니다.

운영 체제에서 Docker를 설치 하는 새 탭에서 아래에 있는 적절 한 링크를 엽니다. 

- [Windows용 Docker](https://www.docker.com/docker-windows)
- [Mac 용 docker](https://www.docker.com/docker-mac)

## <a name="docker-for-windows-environments"></a>Windows 환경용 Docker

Windows용 Docker를 사용하는 경우 Linux 및 Windows 두 가지 환경을 사용할 수 있습니다. Linux 환경을 사용하면 Windows 시스템에서 Linux 컨테이너를 실행할 수 있습니다. Docker 작업 표시줄 아이콘을 마우스 오른쪽 단추로 클릭하고, **Linux 컨테이너로 전환**을 선택하고, 화면의 지시에 따라 환경을 선택할 수 있습니다.

> [!NOTE]
> 이 자습서의 단계에서는 시스템이 Linux 컨테이너를 사용하도록 구성되었다고 가정합니다.

## <a name="docker-on-linux"></a>Linux의 Docker

Linux에 대 한 설치 응용 프로그램이 현재입니다. Linux 기반 시스템에서 작업할 경우 Docker 서버 구성 요소 및 CLI 도구를 수동으로 설치 되어야 합니다. 지침을 따릅니다 [Docker CE에 대 한](https://docs.docker.com/install/#server) 특정 Linux 배포에 대 한 합니다.

## <a name="validate-configuration"></a>구성의 유효성 검사

Docker가 성공적으로 설치 및 구성되었는지 확인하려면 터미널을 열고 다음 명령을 실행합니다.

```bash
docker search nginx
```

다음과 같은 출력이 표시 되 면 환경은 다음 단위에 대해 준비 합니다.

```output
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9034                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1362                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   589                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   390                                     [OK]
kong                                                   Open-source Microservice & API Management la…   204                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              106                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   102
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   59                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      54                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   37
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          36                                      [OK]
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
wodby/drupal-nginx                                     Nginx for Drupal container image                9                                       [OK]
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          9                                       [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   7                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   6
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   3
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```