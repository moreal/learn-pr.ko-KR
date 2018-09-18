작동하는 컨테이너 개발 환경이 생겼으니, 기본적인 컨테이너 작업 몇 가지를 간략하게 살펴보겠습니다. 이 단원에서는 전체 Docker 기능 목록이 포함되지 않습니다(비슷하지도 않음). 이번 섹션에서는 컨테이너를 실행, 나열 및 삭제하기 위한 준비를 할 것입니다. 이 모듈의 나머지 부분에서는 컨테이너 작업을 추가로 공개하겠습니다.

## <a name="run-a-basic-container"></a>기본 컨테이너 실행

컨테이너 실행 및 관리에 대해 자세히 알아보기 전에, 컨테이너를 얼마나 간단하게 실행할 수 있는지 잠시 알아보겠습니다.

다음 명령을 사용하여 첫 번째 컨테이너를 만듭니다.

```bash
docker run alpine echo "Hello World"
```

다음과 비슷한 결과가 나타나야 합니다.

```output
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

`docker run` 명령은 컨테이너 인스턴스를 만듭니다. 이 예에서는 로컬 시스템에 다운로드한 `alpine`이라는 컨테이너 이미지로 컨테이너를 만들었습니다. 컨테이너가 시작된 후 컨테이너 내부에서 `echo "Hello World"` 명령을 실행했고 출력이 터미널에 반향으로 나타났습니다.

지금은 각 작업의 기술적인 세부 사항에 대해 걱정할 필요가 없습니다. 이 모듈의 전체에 걸쳐 자세히 살펴볼 것입니다.

## <a name="get-container-images"></a>컨테이너 이미지 가져오기

‘Hello World’ 예제에서 본 것처럼, 컨테이너는 컨테이너 이미지에서 실행됩니다. 이러한 이미지는 컨테이너 기본 운영 체제 및 추가 프로세스, 응용 프로그램, 구성을 포함하고 있습니다. 컨테이너 이미지는 컨테이너 레지스트리에 저장됩니다. ‘Hello World’ 예제의 *alpine* 이미지는 공용 컨테이너 레지스트리인 Docker 허브에서 끌어온 것입니다.

미리 생성된 컨테이너 이미지를 검색하고 다운로드하는 방법을 알아보겠습니다.

다음 명령을 실행하여 시스템에 다운로드한 이미지 목록을 살펴봅니다.

```bash
docker images
```

과정을 잘 따라 했다면 alpine 이미지가 보일 것입니다. 이 이미지는 ‘Hello World’ 예제를 실행할 때 다운로드되었습니다.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

컨테이너 이미지를 검색하려면 `docker search` 명령을 사용합니다. 예를 들어 다음 예제를 사용하면 이름에 `nginx`가 포함된 컨테이너 이미지를 모두 나열할 수 있습니다.

```bash
docker search nginx
```

출력은 다음과 비슷합니다.

```output
NAME                                                   DESCRIPTION                                     STARS               OFFICIAL            AUTOMATED
nginx                                                  Official build of Nginx.                        9071                [OK]
jwilder/nginx-proxy                                    Automated Nginx reverse proxy for docker con…   1365                                    [OK]
richarvey/nginx-php-fpm                                Container running Nginx + PHP-FPM capable of…   593                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion                 LetsEncrypt container to use with nginx as p…   390                                     [OK]
kong                                                   Open-source Microservice & API Management la…   207                 [OK]
webdevops/php-nginx                                    Nginx with PHP-FPM                              106                                     [OK]
kitematic/hello-world-nginx                            A light-weight nginx container that demonstr…   102
zabbix/zabbix-web-nginx-mysql                          Zabbix frontend based on Nginx web-server wi…   60                                      [OK]
bitnami/nginx                                          Bitnami nginx Docker Image                      54                                      [OK]
1and1internet/ubuntu-16-nginx-php-phpmyadmin-mysql-5   ubuntu-16-nginx-php-phpmyadmin-mysql-5          38                                      [OK]
linuxserver/nginx                                      An Nginx container, brought to you by LinuxS…   37
tobi312/rpi-nginx                                      NGINX on Raspberry Pi / armhf                   20                                      [OK]
nginxdemos/nginx-ingress                               NGINX Ingress Controller for Kubernetes . Th…   11
blacklabelops/nginx                                    Dockerized Nginx Reverse Proxy Server.          10                                      [OK]
wodby/drupal-nginx                                     Nginx for Drupal container image                9                                       [OK]
webdevops/nginx                                        Nginx container                                 8                                       [OK]
nginxdemos/hello                                       NGINX webserver that serves a simple page co…   7                                       [OK]
centos/nginx-18-centos7                                Platform for running nginx 1.8 or building n…   6
1science/nginx                                         Nginx Docker images that include Consul Temp…   4                                       [OK]
centos/nginx-112-centos7                               Platform for running nginx 1.12 or building …   3
pebbletech/nginx-proxy                                 nginx-proxy sets up a container running ngin…   2                                       [OK]
travix/nginx                                           NGinx reverse proxy                             1                                       [OK]
toccoag/openshift-nginx                                Nginx reverse proxy for Nice running on same…   1                                       [OK]
ansibleplaybookbundle/nginx-apb                        An APB to deploy NGINX                          0                                       [OK]
mailu/nginx                                            Mailu nginx frontend                            0                                       [OK]
```

이미지를 실행하기 전에 미리 다운로드하려면 `docker pull` 명령을 사용합니다. 다음 예제는 *nginx* 이미지를 시스템으로 끌어옵니다.

```bash
docker pull nginx
```

출력은 다음과 비슷합니다.

```output
Using default tag: latest
latest: Pulling from library/nginx
be8881be8156: Pull complete
f2f27ed9664f: Extracting [===============>                                   ]  6.652MB/22.14MB
54ff137eb1b2: Download complete
```

`docker images` 명령을 다시 실행하면 시스템의 모든 이미지가 나열됩니다. *nginx* 이미지가 시스템에 추가된 것을 볼 수 있습니다.

```bash
docker images
```

출력은 다음과 비슷합니다.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
nginx               latest              c82521676580        26 hours ago        109MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

## <a name="run-containers"></a>컨테이너 실행

*nginx* 이미지를 확인하고 다운로드했으니, 이미지에서 컨테이너를 실행합니다. Docker CLI를 사용하여 컨테이너 이미지를 실행할 때 `docker run` 명령을 사용합니다.

다음 예제의 `-d` 인수는 컨테이너를 분리 모드에서 실행하도록 지정합니다. 이 구성에서는 컨테이너가 지정된 프로세스를 실행합니다. 해당 프로세스가 중지되거나 크래시가 발생하면 컨테이너 자체가 중지됩니다. `-p 8080:80` 인수는 컨테이너 호스트의 포트 8080에 도착하는 네트워크 트래픽을 지정하며, 이 예의 개발 시스템은 컨테이너의 포트 80으로 전달됩니다. 마지막으로 `ngingx` 인수는 실행할 컨테이너 이미지의 이름입니다.

`docker run` 인수 전체 목록은 [docker run 참조](https://docs.docker.com/engine/reference/run/)에서 확인할 수 있습니다.

```bash
docker run -d -p 8080:80 nginx
```

이 작업은 전체 컨테이너 ID를 반환합니다.

```output
bd2424bfe7a5423d7d65efdf0b1622770d59e212db7b82862c3129fb630b5721
```

`docker ps` 명령을 사용하여 시스템에서 실행 중인 컨테이너를 나열합니다.

```bash
docker ps
```

실행 중인 단일 컨테이너가 보이는데, 마지막 단계에서 실행한 NGINX 컨테이너입니다. 컨테이너의 ID와 이름이 모두 있습니다. 두 값 중 하나를 사용하여 컨테이너를 관리할 수 있습니다. 컨테이너 ID를 기록해 둡니다. 이 값은 나중에 사용됩니다.

```output
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS              PORTS                  NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   37 minutes ago      Up 37 minutes       0.0.0.0:8080->80/tcp   gallant_engelbart
```

컨테이너를 테스트하기 위해, 브라우저를 열고 주소로 http://localhost:8080을 입력합니다. 완료되면 NGINX 기본 웹 사이트가 표시됩니다.

![NGINX 시작 화면이 표시된 Microsoft Edge](../media-draft/3-nginx.png)

## <a name="delete-containers"></a>컨테이너 삭제

컨테이너 사용을 마친 후에는 `docker rm` 명령에 컨테이너 이름 또는 ID를 입력하여 컨테이너를 삭제할 수 있습니다. NGINX를 실행하는 컨테이너의 컨테이너 ID로 이 작업을 연습해 보세요. 이 예제의 ID를 해당 환경의 ID로 바꾸면 됩니다.

```bash
docker rm bd2424bfe7a5
```

컨테이너가 실행 중 상태이므로 컨테이너를 제거할 수 없습니다.

```output
Error response from daemon: You cannot remove a running container a31c5a5f2a8d6e420435bfcadbe158fa6a26ed29c005a892171505cc0c2861b2. Stop the container before attempting removal or force remove
```

`docker stop` 명령을 사용하여 컨테이너를 중지합니다.

```bash
docker stop bd2424bfe7a5
```

이 시점에서 `docker ps` 명령을 사용하여 모든 컨테이너를 나열하면 nginx 컨테이너가 나열되지 않습니다.

```bash
docker ps
```

출력은 다음과 비슷합니다.

```output
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

중지된 상태의 컨테이너를 포함하여 모든 컨테이너 목록을 반환하려면 `docker ps` 명령에 `-a` 인수를 추가합니다.

```bash
docker ps -a
```

출력은 다음과 비슷합니다.

```output
CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                     PORTS               NAMES
bd2424bfe7a5        nginx               "nginx -g 'daemon of…"   13 seconds ago      Exited (0) 3 seconds ago                       focused_spence
```

삭제 작업을 다시 연습해 봅니다. 이 예제의 ID를 해당 환경의 ID로 바꾸면 됩니다.

```bash
docker rm bd2424bfe7a5
```

이 작업은 컨테이너 ID를 반환합니다.

```output
bd2424bfe7a5
```

## <a name="delete-a-container-image"></a>컨테이너 이미지 삭제

컨테이너 이미지 사용을 마쳤으면 `docker rmi` 명령을 사용하여 제거할 수 있습니다. 컨테이너 이미지에서 컨테이너(실행 또는 중지된)가 시작되면 이미지를 삭제할 수 없습니다. 컨테이너를 먼저 제거해야 합니다. `docker rmi` 명령에 `-f` 인수를 추가하면 연결된 모든 컨테이너가 강제로 제거되고, 그 후 컨테이너 이미지가 제거됩니다.

다음 명령을 사용하여 NGINX 컨테이너 이미지를 제거합니다.

```bash
docker rmi nginx
```

출력은 다음과 비슷합니다.

```output
Untagged: nginx:latest
Untagged: nginx@sha256:4a5573037f358b6cdfa2f3e8a9c33a5cf11bcd1675ca72ca76fbe5bd77d0d682
Deleted: sha256:8b89e48b5f157d9455c963b57c85d21e2337c58b8c983bc06f88476610adc129
Deleted: sha256:119ded3eca5e85ef43ee966e74564c604ccda064d955a8c5ed762e1d5e87f428
Deleted: sha256:6ece91c2763d826487e707f7b8ec063742ad0ee56cc9e605465cce95550c9a7f
Deleted: sha256:cdb3f9544e4c61d45da1ea44f7d92386639a052c620d1550376f22f5b46981af
```

## <a name="summary"></a>요약

이 섹션에서는 몇 가지 기본적인 Docker 작업을 알아보았습니다. 다음 섹션에서는 사용자 지정 컨테이너 이미지를 만들겠습니다.