이제 컨테이너 개발 환경이 작동하게 되었으니 컨테이너를 실행하고, 나열하고, 삭제하는 일반적인 방법을 살펴보겠습니다.

여기에서 배울 내용은 다음과 같습니다.

* 기본 컨테이너를 실행합니다.
* 컨테이너 이미지를 다운로드합니다.
* 컨테이너와 연결된 해당 이미지를 삭제합니다.

## <a name="whats-a-container-image"></a>컨테이너 이미지란?

컨테이너 _이미지_는 기본 운영 체제 및 추가 프로세스, 응용 프로그램, 구성을 포함하고 있습니다. _컨테이너_는 가상 머신과 마찬가지로 실행 중인 이미지 인스턴스입니다.

## <a name="connect-to-your-linux-vm"></a>Linux VM에 연결

마지막 부분에서 만든 SSH 세션에서 연결이 끊어진 경우 로그인해야 합니다. 배운 내용을 떠올려 보겠습니다.

1. IP 주소를 가져옵니다.

    ```azurecli
    az vm show \
      --resource-group <rgn>[sandbox resource group name]</rgn> \
      --name DockerVM \
      --show-details \
      --query [publicIps] \
      --o tsv
    ```

1. VM에 SSH로 연결합니다. **ip-address**를 자신의 IP 주소로 바꿉니다.

    ```bash
    ssh azureuser@ip-address
    ```

## <a name="create-and-run-a-basic-container"></a>기본 컨테이너 생성 및 실행

여기에서는 Alpine Linux에 기반을 둔 컨테이너를 실행합니다. Alpine Linux는 컨테이너 이미지가 단 5MB로 매우 작아서 인기가 많습니다.

이 `docker run` 명령을 실행하여 Alpine Linux에 기반을 둔 컨테이너를 만듭니다.

```bash
docker run alpine echo "Hello World"
```

다음과 유사한 출력이 표시됩니다.

```output
Unable to find image 'alpine:latest' locally
latest: Pulling from library/alpine
8e3ba11ec2a2: Pull complete
Digest: sha256:7043076348bf5040220df6ad703798fd8593a0918d06d3ce30c6c93be117e430
Status: Downloaded newer image for alpine:latest
Hello World
```

`docker run` 명령은 컨테이너를 만들고, 제공된 된 명령을 실행한 다음, 컨테이너를 destroy합니다.

여기에서 Docker는 Docker 허브의 [alpine](https://hub.docker.com/_/alpine?azure-portal=true) 이미지를 다운로드하고, 컨테이너를 시작한 다음, 콘솔에 "Hello World"를 출력합니다.

이 경우 `echo` 명령이 짧게 실행된 후 종료됩니다. 이전 부분에서는 Nginx가 포그라운드에서 실행되므로 컨테이너를 중지하거나 Nginx 서비스를 중지할 때까지 컨테이너를 활성 상태로 유지하세요.

## <a name="get-container-images"></a>컨테이너 이미지 가져오기

컨테이너 이미지는 컨테이너 레지스트리에 저장됩니다. 이전 예제에서 Docker는 Docker의 공개 컨테이너 레지스트리인 Docker 허브에서 **alpine** 이미지를 끌어옵니다.

`docker images`를 실행하여 시스템에 다운로드한 이미지 목록을 살펴봅니다.

```bash
docker images
```

&mdash; **alpine** 및 **nginx**라는 두 이미지가 보입니다.

```output
REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
alpine              latest              196d12cf6ab1        8 days ago4.41MB
nginx               latest              06144b287844        2 weeks ago109MB
```

컨테이너 이미지를 검색하려면 `docker search` 명령을 사용합니다. 예를 들어 다음을 실행하면 이름에 `nginx`가 포함된 컨테이너 이미지가 모두 나열됩니다.

```bash
docker search nginx --limit 5
```

이 예제의 `--limit` 인수는 검색 작업을 처음 5개 결과로 제한합니다.

다음과 비슷한 결과가 표시됩니다.

```output
NAME                                     DESCRIPTION         STARS               OFFICIAL            AUTOMATED
nginx                                    Official build of Nginx.         9672                [OK]
jwilder/nginx-proxy                      Automated Nginx reverse proxy for docker con…   1415                                    [OK]
richarvey/nginx-php-fpm                  Container running Nginx + PHP-FPM capable of…   615                                     [OK]
jrcs/letsencrypt-nginx-proxy-companion   LetsEncrypt container to use with nginx as p…   411                                     [OK]
bitnami/nginx                            Bitnami nginx Docker Image         58                                      [OK]
```

`docker run` 같은 명령은 이미지가 로컬에 없을 경우 자동으로 이미지를 끌어옵니다. 하지만 이미지를 다운로드한 후 사용하는 것이 일반적입니다. 그러면 최신 버전을 확보할 수 있습니다.

그러기 위해서는 `docker pull` 명령을 사용하세요. 다음을 실행하여 Docker 허브에서 최신 **nginx** 이미지를 끌어옵니다.

```bash
docker pull nginx
```

이 예제에서는 최신 버전의 **nginx** 이미지가 있음을 보여줍니다.

```output
Using default tag: latest
latest: Pulling from library/nginx
Digest: sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
Status: Image is up to date for nginx:latest
```

## <a name="run-and-list-a-container"></a>컨테이너 실행 및 나열

이전 부분에서는 `docker run` 명령을 사용하여 Nginx를 불러왔습니다. 이 명령을 다시 한 벌 실행하여 어떤 일이 일어나는지 더 자세히 살펴보겠습니다.

1. SSH 연결에서 이 명령을 실행하여 Nginx를 실행하는 컨테이너를 불러옵니다.

    ```bash
    docker run -d -p 8080:80 nginx
    ```

    * `-d` 인수는 컨테이너를 분리 모드에서 실행하도록 지정합니다. 즉, 컨테이너가 백그라운드에서 실행됩니다. Nginx 프로세스가 중지되거나 크래시가 발생하면 컨테이너 자체도 중지됩니다.
    * `-p` 인수는 컨테이너 호스트의 포트 8080에 도착하는 네트워크 트래픽을 지정하며, 이 예의 Linux VM은 컨테이너의 포트 80으로 전달됩니다. 이전 부분에서 이 인수를 사용하여 브라우저에서 웹 서버에 액세스했습니다.
    * `nginx` 인수는 실행할 컨테이너 이미지의 이름입니다.

    나중에 [docker run 참고 자료](https://docs.docker.com/engine/reference/run?azure-portal=true)에서 `docker run` 옵션의 전체 목록을 살펴볼 수 있습니다.

    `docker run` 명령은 컨테이너의 고유 식별자를 표시합니다. 예:

    ```output
    9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466
    ```

1. `docker ps`를 실행하여 시스템에서 실행 중인 컨테이너를 나열합니다.

    ```bash
    docker ps
    ```

    방금 시작한 Nginx 컨테이너가 표시됩니다. 컨테이너의 ID와 이름이 모두 있습니다. 이러한 값 중 하나를 사용하여 컨테이너를 관리할 수 있습니다. 컨테이너 ID를 메모해 두세요. 나중에 필요합니다.

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS              PORTS                  NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   4 minutes ago     Up 4 minutes        0.0.0.0:8080->80/tcp   compassionate_allen
    ```

1. 이전에 수행한 것처럼, 브라우저에서 VM의 IP 주소로 이동하여 실행 중인 웹 서버를 볼 수 있습니다. URL의 일부로 포트 8080을 지정하는 것을 잊지 마세요.

    ![브라우저에서 실행 중인 웹 사이트](../media/2-nginx-browser.png)

## <a name="delete-containers"></a>컨테이너 삭제

컨테이너를 삭제하려면 `docker rm` 명령을 사용합니다. 이름 또는 ID로 컨테이너를 지정할 수 있습니다.

1. `docker rm`을 실행하여 Nginx를 실행 중인 컨테이너를 삭제해 보세요. ID를 찾아야 하는 경우 `docker ps`를 실행하세요. 예를 들면 다음과 같습니다.

    ```bash
    docker rm 9d7327e31212
    ```

    컨테이너가 실행 중 상태이므로 컨테이너를 제거할 수 없습니다.

    ```output
    Error response from daemon: You cannot remove a running container 9d7327e3121200cfe2dccb627544db1442a4e02ed3151f30681db4e538ef9466. Stop the container before attempting removal or force remove
    ```

1. 컨테이너를 중지하려면 `docker stop`을 실행합니다. 예를 들면 다음과 같습니다.

    ```bash
    docker stop 9d7327e31212
    ```
    
1. `docker ps`를 실행하여 컨테이너가 더 이상 실행되고 있지 않은지 확인합니다.

    ```bash
    docker ps
    ```

    다음이 표시됩니다.

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATEDSTATUS              PORTS               NAMES
    ```

1. `docker ps`를 다시 한 번 실행하되, 이번에는 `-a` 플래그를 지정합니다. 그러면 중지된 컨테이너까지 포함하여 모든 컨테이너가 나열됩니다.

    ```bash
    docker ps -a
    ```

    다음과 유사한 출력이 표시됩니다.

    ```output
    CONTAINER ID        IMAGE               COMMAND                  CREATED     STATUS                          PORTS               NAMES
    9d7327e31212        nginx               "nginx -g 'daemon of…"   11 minutes ago     Exited (0) About a minute ago                       compassionate_allen
    df8aeea0320f        alpine              "echo 'Hello World'"     About an hour ago   Exited (0) About an hour ago                        objective_payne
    3a7efb75c288        nginx               "nginx -g 'daemon of…"   About an hour ago   Exited (0) About an hour ago                        nginx
    ```

    이 출력에는 방금 전에 중지한 Nginx 컨테이너와 이전에 실행한 다른 컨테이너가 포함됩니다.

1. `docker rm`을 다시 한 번 실행합니다. 표시된 ID를 자신의 ID 중 하나로 바꿉니다.

    ```bash
    docker rm 9d7327e31212
    ```

1. 다음 `docker rm` 명령을 실행하여 _모든_ 활성 컨테이너를 삭제합니다.

    ```bash
    docker rm $(docker ps -aq)
    ```

1. `docker ps -a`를 다시 실행하여 실행 중이거나 중지된 활성 컨테이너가 없는지 확인합니다.

    ```bash
    docker ps -a
    ```

## <a name="delete-a-container-image"></a>컨테이너 이미지 삭제

컨테이너 이미지를 삭제하려면 `docker rmi` 명령을 사용합니다.

시작되거나, 실행 중이거나 중지되거나, 활성 상태인 컨테이너가 없는 이미지만 삭제할 수 있습니다. 하지만 `-f` 인수를 추가하면 연결된 모든 컨테이너가 강제로 제거되고, 그 후 컨테이너 이미지가 제거됩니다.

1. `docker rmi nginx`를 실행하여 Linux VM에서 Nginx 이미지를 제거합니다.

    ```bash
    docker rmi nginx
    ```

    다음과 유사한 출력이 표시됩니다.

    ```output
    Untagged: nginx:latest
    Untagged: nginx@sha256:24a0c4b4a4c0eb97a1aabb8e29f18e917d05abfe1b7a7c07857230879ce7d3d3
    Deleted: sha256:06144b2878448774e55577ae7d66b5f43a87c2e44322b3884e4e6c70d070b262
    Deleted: sha256:824a442ee3c96744d75be3737a22cc6a47aebad1b30be67f3c2f8f29cb0aa879
    Deleted: sha256:8e3d1e9e4945f930c93c30617512998437f6edafd86676770d29b1581f2520bb
    Deleted: sha256:8b15606a9e3e430cb7ba739fde2fbb3734a19f8a59a825ffa877f9be49059817
    ```

1. `docker images`를 실행하여 VM의 이미지를 나열합니다. 

    ```bash
    docker images
    ```

    **alpine** 이미지가 보입니다.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATEDSIZE
    alpine              latest              196d12cf6ab1        8 days ago4.41MB
    ```

1. 다음 `docker rmi` 명령을 실행하여 VM에서 _모든_ 이미지를 삭제합니다.

    ```bash
    docker rmi $(docker images -q)
    ```

1. `docker images`를 다시 실행하여 VM에 이미지가 없는지 확인합니다.

    ```bash
    docker images
    ```
