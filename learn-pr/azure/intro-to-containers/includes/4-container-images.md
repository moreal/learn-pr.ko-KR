지금까지는 다른 사용자가 만든 Docker 이미지를 다운로드하고 실행했습니다. 여기에서는 사용자 고유의 컨테이너 이미지를 빌드합니다. 이 문서에서 배울 내용은 다음과 같습니다.

* 수동 프로세스를 사용하여 이미지를 만듭니다.
* Dockerfile이라는 좀 더 자동화된 프로세스를 사용하여 동일한 이미지를 만듭니다.
* 공용 컨테이너 레지스트리인 Docker 허브에 이미지를 게시합니다.

## <a name="what-is-a-dockerfile"></a>Dockerfile이란?

Dockerfile이란 컨테이너가 실행해야 하는 모든 것이 설명된 텍스트 파일입니다.

Dockerfile의 지침에는 다음이 정의될 수 있습니다.

* 이미지가 기반을 두고 있는 부모 이미지입니다.
* 설치할 소프트웨어 패키지입니다.
* 앱이 실행해야 하는 구성 또는 다른 파일입니다.
* 사용할 수 있도록 하려는 포트 등의 네트워킹 설정입니다.
* 컨테이너가 시작될 때 실행할 명령입니다.

수동 프로세스를 사용하여 컨테이너 이미지를 만들거나 Dockerfile을 사용하여 프로세스를 자동화할 수 있습니다. Docker 이미지를 수동으로 만들면 프로세스를 이해하는 데 도움이 됩니다. Dockerfile을 사용하면 프로세스를 더 쉽고 빠르게 반복할 수 있습니다.

## <a name="what-is-docker-hub"></a>Docker 허브란?

Docker 허브란 Docker 이미지를 저장하고 다운로드할 수 있는 곳입니다. 이전에 사용한 Nginx 이미지처럼 Docker 및 Docker 커뮤니티에서 만든 Docker 이미지를 다운로드할 수 있습니다. 또한 Docker 커뮤니티 또는 자신의 팀과 자체 사용자 고유의 이미지를 공유할 수 있습니다.

## <a name="create-an-image-manually"></a>수동으로 이미지 만들기

여기에서는 기본 Python 응용 프로그램을 실행하는 Docker 이미지를 만듭니다.

1. 먼저 [python](https://hub.docker.com/_/python/?azure-portal=true) 이미지에서 컨테이너 인스턴스를 불러옵니다.

    ```bash
    docker run --name python-demo -it python bash
    ```

    Docker가 Docker Hub에서 이 이미지를 끌어오는 동안 잠시 시간이 걸립니다. 기다리는 동안 명령의 역할에 대해 살펴보겠습니다.

    * `--name` 인수는 컨테이너의 이름 "python-demo"를 지정합니다.
    * `-i` 및 `-t` 인수는 `-it`라는 하나의 인수로 결합됩니다. 이러한 인수는 실행 중인 컨테이너와의 대화형 세션을 만듭니다.
      * `-i`는 컨테이너를 사용하여 대화형 세션을 만듭니다.
      * `-t`는 실행 중 상태로 유지되는 의사 터미널을 만듭니다.
    * `python`은 기본 이미지를 지정합니다. Docker는 Docker 허브에서 이 이미지를 다운로드합니다. 이 이미지는 Python 프로그래밍용 환경으로 사전 구성되어 있습니다.
    * `bash`는 실행할 프로그램을 지정합니다.

    이 설정은 Python 앱을 작성하는 데 필요한 대화형 환경으로 보면 됩니다. 앱을 시작할 준비가 되면 환경의 이미지나 스냅숏을 캡처할 수 있습니다. 앱을 개선하면서 사용자 또는 팀을 위한 추가 이미지를 만들 수 있습니다.

    터미널 세션이 컨테이너의 의사 터미널로 전환됩니다. 다음과 유사한 프롬프트가 표시됩니다.

    ```docker
    root@d8ccada9c61e:/#
    ```

1. Docker 세션에서 이를 실행하여 `./app`이라는 디렉터리를 만들고 이 디렉터리로 이동합니다.

    ```bash
    mkdir ./app && cd ./app
    ```

    필수는 아니지만 필요할 경우 `./app` 디렉터리에 Python 코드를 추가할 수 있습니다.

1. 매우 기본적인 Python 프로그램을 만들려면 다음을 실행합니다.

    ```bash
    echo 'print("Hello World!")' > hello.py
    ```

    이 프로그램은 터미널에 "Hello World!"를 출력합니다.

    > [!TIP]
    > 실제로는 워크스테이션의 디렉터리를 컨테이너의 디렉터리에 _마운트_할 수 있습니다. 그러면 워크스테이션에서 자주 사용하는 편집기를 사용하여 코드를 작성할 수 있습니다. 파일을 저장하면 해당 파일이 컨테이너에도 나타납니다.

1. 다음을 실행하여 Python 프로그램을 사용해 봅니다.

    ```bash
    python hello.py
    ```

    다음이 표시됩니다.

    ```output
    Hello World!
    ```

1. 대화형 세션을 종료합니다.

    ```bash
    exit
    ```

1. Linux VM에서 `docker ps`를 실행하여 실행 중인 모든 컨테이너를 나열합니다.

    ```bash
    docker ps
    ```

    아무것도 실행되고 있지 않은 것을 알 수 있습니다. 

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
    ```

    컨테이너를 종료하면 Bash 세션도 종료되기 때문입니다. 컨테이너가 실행하는 응용 프로그램 또는 서비스가 종료되면 Docker가 컨테이너를 중지합니다.

1. `docker ps`를 다시 한 번 실행하고 `-a` 인수를 포함합니다. 이 명령은 실행 중이거나 중지된 모든 컨테이너를 반환합니다.

    ```bash
    docker ps -a
    ```

    다음과 같이 표시됩니다.

    ```output
    CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
    cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
    ```

   **python-demo** 컨테이너의 상태는 **종료됨**입니다.

1. `docker commit`를 실행하여 컨테이너에서 이미지를 만듭니다.

   ```bash
   docker commit python-demo python-custom
   ```

   이때 Docker는 **python-demo**라는 컨테이너에서 **python-custom**이라는 이미지를 만듭니다. 이미지 이름은 원하는 대로 지정할 수 있습니다.

1. `docker images`를 실행하여 이미지를 나열합니다.

    ```bash
    docker images
    ```

    **python-custom** 이미지가 보입니다.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-custom       latest              1f231e7127a1        6 seconds ago       922MB
    python              latest              638817465c7d        24 hours ago        922MB
    ```

1. `docker run`을 사용하여 이미지를 테스트해 봅니다.

    ```bash
    docker run python-custom python app/hello.py
    ```

    `docker run`은 실행할 명령을 최종 인수로 사용한다는 사실을 떠올려 보세요. 여기서 이 명령은 `python app/hello.py`입니다.

    다음이 표시됩니다.

    ```output
    Hello World!
    ```

    이 컨테이너를 대화형으로 실행하고 있지 않으므로 Python 프로그램이 실행되고 컨테이너가 중지됩니다.

## <a name="use-a-dockerfile-to-create-an-image-automatically"></a>Dockerfile을 사용하여 자동으로 이미지 생성

여기에서는 좀 더 자동화된 프로세스를 사용하여 Python 프로그램을 실행하는 동일한 Docker 이미지를 만듭니다.

수동으로 이미지를 빌드하는 것은 새로운 기능을 실험하고 살펴보는 데 좋은 방법입니다. 하지만 프로세스를 팀과 공유하거나 반복하려고 하는 경우를 가정해 보겠습니다. 예를 들어, 매일 저녁에 팀이 개발 중인 소프트웨어의 최신 버전을 실행하는 새 이미지를 만들려고 한다고 가정해 보겠습니다.

이때 Dockerfile이 필요합니다. Dockerfile은 수동으로 수행할 뻔한 지침을 설명하는 방법으로 생각하면 됩니다.

1. Linux VM에서 Python 프로그램을 실행하는 Dockerfile을 만들려면 이 명령을 실행합니다.

    ```bash
    cat << EOF > Dockerfile
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    EOF
    ```

    이 예는 파일을 만드는 간단한 방법일 뿐입니다. 실제로는 자주 사용하는 코드 편집기를 사용하여 파일을 만들면 됩니다.

    콘솔에 Dockerfile을 출력합니다.

    ```bash
    cat Dockerfile
    ```

    다음이 표시됩니다.

    ```output
    FROM python
    
    WORKDIR ./app
    
    RUN echo 'print("Hello World!")' > hello.py
    
    CMD python hello.py
    ```

    Dockerfile에서 수행하는 작업을 분석해 보겠습니다.

    * `FROM`은 이 이미지의 기반이 될 부모 이미지를 지정합니다. 여기서 부모 이미지는 **python**입니다.
    * `WORKDIR`은 Dockerfile의 뒷부분에 표시되는 `RUN` 및 `CMD` 문의 작업 디렉터리를 지정합니다. Docker는 이러한 디렉터리를 자동으로 생성합니다(이 경우 `./app`).
    * `RUN`은 컨테이너에서 실행할 명령을 지정합니다. `RUN`은 소프트웨어를 설치하고, 구성을 변경하고, 컨테이너를 캡처하기 전에 정리하는 데 사용할 수 있습니다. 여기에서는 기본 Python 프로그램을 `./app/hello.py`로 작성합니다.
    * `CMD`는 컨테이너가 시작될 때 실행할 명령을 지정합니다. 여기에서는 `/.app` 디렉터리에서 `python hello.py`를 실행했습니다.

    이미지를 수동으로 빌드할 때와 거의 똑같은 단계임을 눈치채신 분도 있을 것입니다. 이 단계를 코드로 표현하면 프로세스를 더 쉽게 공유하고 반복할 수 있습니다.

1. Dockerfile에 지정된 지침에 따라 `docker build`를 실행하여 이미지를 만듭니다.

    ```bash
    docker build -t python-dockerfile .
    ```

    일반적으로 Docker가 이미지를 빌드하기까지 몇 초밖에 걸리지 않습니다.

    다음과 같은 출력이 표시됩니다.

    ```output
    Sending build context to Docker daemon  2.048kB
    Step 1/4 : FROM python
     ---> 638817465c7d
    Step 2/4 : WORKDIR ./app
     ---> Running in 990d17e86466
    Removing intermediate container 990d17e86466
     ---> 59a074a092cc
    Step 3/4 : RUN echo 'print("Hello World!")' > hello.py
     ---> Running in aed707c53bc5
    Removing intermediate container aed707c53bc5
     ---> d7f55a9d0e85
    Step 4/4 : CMD python hello.py
     ---> Running in e87ec55a8d36
    Removing intermediate container e87ec55a8d36
     ---> 98c39b91770f
    Successfully built 98c39b91770f
    Successfully tagged python-dockerfile:latest
    ```

1. `docker images`를 사용하여 이미지를 나열합니다.

    ```bash
    docker images
    ```

    방금 전에 빌드한 **python-dockerfile** 이미지가 보입니다.

    ```output
    REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
    python-dockerfile   latest              8ed5f85c5e5b        24 seconds ago      923MB
    python-custom       latest              6789cbe2cceb        4 minutes ago       923MB
    python              latest              a9d071760c82        2 weeks ago         923MB
    ```

1. `docker run`을 사용하여 컨테이너를 테스트해 봅니다.

    ```bash
    docker run python-dockerfile
    ```

    다음이 표시됩니다.

    ```output
    Hello World!
    ```

    수동으로 만든 이미지를 테스트할 때와 달리 여기에서는 실행할 명령 `python app/hello.py`를 지정하지 않습니다. Dockerfile에서 이를 지정하므로 이미지에 명령이 기본 제공됩니다.

## <a name="publish-your-image-to-docker-hub"></a>Docker 허브에 Docker 이미지 게시

Docker 허브에 이미지를 게시하려면 계정이 필요합니다. 여기에서는 Docker 허브 계정을 설정하고 **python-dockerfile** 이미지를 Docker 허브에 게시합니다.

1. [Docker 허브 계정을 생성](https://hub.docker.com?azure-portal=true)합니다.

1. Docker 허브 계정 이름을 환경 변수로 내보냅니다. **account-name**을 사용자의 계정 이름으로 바꾸세요.

    ```bash
    export docker_account=account-name
    ```

    이 환경 변수를 통해 다음에 나오는 명령을 더 쉽게 실행할 수 있습니다.

1. `docker tag`를 실행하여 이미지에 Docker Hub 계정 이름을 태그합니다.

    ```bash
    docker tag python-dockerfile $docker_account/python-dockerfile
    ```

1. `docker login`을 실행하여 Docker 허브에 로그인합니다.

    ```bash
    docker login
    ```

    메시지가 표시되면 사용자 이름 및 암호를 입력합니다.

1. `docker push`를 실행하여 **python-dockerfile** 이미지를 Docker 허브에 게시하거나 업로드합니다.

    ```bash
    docker push $docker_account/python-dockerfile
    ```

    그러면 다음과 같은 출력이 표시됩니다.

    ```output
    The push refers to repository [docker.io/account/python-dockerfile]
    f39073ca4d5a: Pushed
    9dfcec2738a9: Pushed
    ffab8273c674: Mounted from account/python
    e6f6cbe5e14e: Mounted from account/python
    3eb255f8a6ac: Mounted from account/python
    b860b6c48eec: Mounted from account/python
    1fa8778eb779: Mounted from account/python
    fa0c3f992cbd: Mounted from account/python
    ce6466f43b11: Mounted from account/python
    719d45669b35: Mounted from account/python
    3b10514a95be: Mounted from account/python
    latest: digest: sha256:b816c32382d06ac74530d56f2a7b83000c86174218f430c6bb5039fdcfba38aa size: 2631
    ```

    이제 Docker 이미지가 Docker 허브에 저장됩니다. 다른 컴퓨터에서 `docker pull` 또는 `docker run`을 사용하여 Docker 허브의 이미지를 다운로드하거나 실행할 수 있습니다. 다음은 두 가지 예입니다.

    1. 이 예에서는 Docker 허브에서 최신 이미지를 끌어옵니다.

        ```bash
        docker pull $docker_account/python-dockerfile
        ```

    1. 이 예에서는 컨테이너를 실행합니다.

        ```bash
        docker run $docker_account/python-dockerfile
        ```

1. 컨테이너를 테스트해 보세요.

    [Docker 허브 계정](https://hub.docker.com?azure-portal=true)으로 이동합니다. **리포지토리** 탭에 Docker 이미지가 표시됩니다.

    ![Docker 허브의 Docker 이미지](../media/4-docker-hub-python-dockerfile.png)
