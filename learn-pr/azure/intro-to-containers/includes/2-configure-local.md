Azure에서 컨테이너 또는 컨테이너 통합 응용 프로그램을 실행하기 전에는 대부분 노트북 같은 로컬 개발 환경에서 작업합니다. 이 단원에서는 Docker를 사용하여 컨테이너 개발을 위한 시스템 준비 작업을 도와줍니다.

## <a name="docker-for-windows-and-mac"></a>Windows 및 Mac용 Docker

Docker, Inc.는 로컬 컨테이너 개발 환경을 설치하고 구성할 수 있는 두 가지 응용 프로그램을 게시했습니다. 기본적으로 각 응용 프로그램은 필수 CLI 및 자동화 도구 같은 Docker 도구를 사용하여 시스템을 준비합니다. Docker 플랫폼을 호스팅하는 가상 머신도 만듭니다. Docker 명령이 가상 머신으로 전달되도록 환경이 구성됩니다. 각 응용 프로그램은 서로 기능이 비슷하며 다음과 같은 특징을 갖고 있습니다.

- **Docker 플랫폼:** 컨테이너를 만들고 실행하는 데 필요한 핵심 구성 요소입니다.
- **Docker CLI:** Docker 컨테이너와 상호 작용하기 위한 명령줄 인터페이스입니다.
- **Docker Compose:** 다중 컨테이너 응용 프로그램을 정의하고 실행하는 자동화 도구입니다.

아래 해당 링크를 새 탭에서 열고 Docker를 운영 체제에 설치합니다. 

- [Windows용 Docker](https://www.docker.com/docker-windows)
- [Mac용 Docker](https://www.docker.com/docker-mac)

## <a name="docker-for-windows-environments"></a>Windows용 Docker 환경

Windows용 Docker를 사용하는 경우 Linux 및 Windows 두 가지 환경을 사용할 수 있습니다. Linux 환경을 사용하면 Windows 시스템에서 Linux 컨테이너를 실행할 수 있습니다. Docker 작업 표시줄 아이콘을 마우스 오른쪽 단추로 클릭하고, **Linux 컨테이너로 전환**을 선택하고, 화면의 지시에 따라 환경을 선택할 수 있습니다.

![Windows용 Docker, Linux 컨테이너로 전환](../media-draft/2-docker-linux.png)

> [!NOTE]
> 이 자습서의 단계에서는 시스템이 Linux 컨테이너를 사용하도록 구성되었다고 가정합니다.

## <a name="docker-on-linux"></a>Linux의 Docker

Linux 기반 시스템에서 작업하는 경우 Docker 서버 구성 요소 및 CLI 도구를 수동으로 설치할 수 있습니다. [Docker CE 정보](https://docs.docker.com/install/#server)에서 해당 Linux 배포판에 대한 지침을 따르세요.

## <a name="validate-configuration"></a>구성의 유효성 검사

Docker가 성공적으로 설치 및 구성되었는지 확인하려면 터미널을 열고 다음 명령을 실행합니다.

```bash
docker search nginx
```

다음과 비슷한 출력이 표시되면 다음 단원을 진행하기 위한 환경 준비가 완료된 것입니다.

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

## <a name="summary"></a>요약

이 섹션에서는 로컬 컨테이너 개발 환경을 준비했습니다. 다음 섹션에서는 몇 가지 기본적인 Docker 작업에 대해 알아보겠습니다.