지난 섹션에서는 미리 만들어진 컨테이너 이미지를 사용하여 몇 가지 기본적인 Docker 작업을 수행했습니다. 이번 섹션에서는 사용자 지정 컨테이너 이미지를 만들고, 이러한 이미지를 공용 컨테이너 레지스트리에 푸시하고, 이러한 이미지에서 컨테이너를 실행하겠습니다.

컨테이너 이미지를 직접 만들어도 되고 Dockerfile을 사용하여 프로세스를 자동화해도 됩니다. 사람들이 선호하는 방법은 Dockerfile이지만, 이번 섹션에서는 두 가지 방법을 모두 살펴보겠습니다. 수동 프로세스를 이해하면 자동화를 위해 Dockerfile을 사용할 때 발생하는 상황을 잘 이해할 수 있습니다.

## <a name="manual-image-creation"></a>수동으로 이미지 만들기

컨테이너 이미지를 수동으로 만들 때에는 다음 작업을 수행합니다.

- 컨테이너 인스턴스를 시작합니다.
- 컨테이너와 터미널 세션을 설정합니다.
- 소프트웨어를 설치하고 구성을 변경하여 컨테이너를 수정합니다.
- `docker capture` 명령을 사용하여 컨테이너를 새 이미지에 캡처합니다.

첫 번째 예제에서는 Python을 실행하는 컨테이너 인스턴스를 시작하고 'Hello World' 응용 프로그램을 만든 다음, 컨테이너를 새 이미지에 캡처합니다.

먼저 NGINX 이미지에서 컨테이너를 실행합니다. 이 명령은 이전 섹션에서 실행한 명령과 약간 다르게 보입니다. 실행 중인 컨테이너와 터미널 세션을 설정하려는 것이기 때문에 `-t` 및 `-i` 인수를 입력합니다. 두 인수는 함께 사용할 경우 실행 중 상태를 유지하는 의사 터미널을 할당하라고 Docker에 지시합니다. 즉, `-t` 및 `-i` 인수는 실행 중인 컨테이너와 대화형 세션을 만듭니다.

그런 다음, `python` 컨테이너 이미지를 사용하고 컨테이너 내부에서 `bash` 프로세스를 실행하도록 지정합니다.

```bash
docker run --name python-demo -ti python bash
```

명령을 실행하면 터미널 세션이 컨테이너 의사 터미널로 전환됩니다. 이것은 터미널 프롬프트에서 확인할 수 있으며, 다음과 비슷하게 변경되었을 것입니다.

```output
root@d8ccada9c61e:/#
```

지금은 컨테이너 내부에서 작업합니다. 컨테이너 내부에서 작업하는 것은 가상 또는 물리적 시스템 내부에서 작업하는 것과 비슷합니다. 예를 들어 파일을 나열, 생성 및 삭제하고, 소프트웨어를 설치하고, 구성을 변경할 수 있습니다. 이 간단한 예제에서는 Python 기반 'Hello World' 스크립트가 생성됩니다. 이 작업은 다음 명령을 사용하여 수행할 수 있습니다.

```bash
echo 'print("Hello World!")' > hello.py
```

컨테이너에 있는 동안 스크립트를 테스트하려면 다음 명령을 실행합니다.

```bash
python hello.py
```

그러면 다음 출력이 표시됩니다.

```output
Hello World!
```

스크립트가 예상대로 작동하여 만족스러운 경우 `exit`를 입력하여 컨테이너에서 나옵니다.

```bash
exit
```

로컬 시스템의 터미널로 돌아가서, `docker ps` 명령을 사용하여 실행 중인 모든 컨테이너를 나열합니다.

```bash
docker ps
```

아무 것도 실행되고 있지 않습니다. 실행 중인 컨테이너에서 `exit`를 입력하면 Bash 프로세스가 완료되고 컨테이너가 중지됩니다. 이것은 예상된 정상적인 동작입니다.

```output
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS              PORTS               NAMES
```

`docker ps`를 다시 사용하여 `-a` 인수를 포함합니다. 이 명령은 실행 여부에 관계없이 모든 컨테이너 목록을 반환합니다.

```bash
docker ps -a
```

이름이 *python-demo*인 컨테이너의 상태는 *끝냄*입니다. 이 컨테이너는 방금 종료한 컨테이너의 중지된 인스턴스입니다.

```output
CONTAINER ID        IMAGE               COMMAND             CREATED             STATUS                      PORTS               NAMES
cf6ac8e06fd9        python              "bash"              27 seconds ago      Exited (0) 12 seconds ago                       python-demo
```

이 컨테이너에서 새 컨테이너 이미지를 만들려면 `docker commit` 명령을 사용합니다. 다음 예제는 *python-demo* 컨테이너로 *python-custom*이라는 이미지를 만들도록 *docker commit*에 지시합니다.

```bash
docker commit python-demo python-custom
```

명령을 완료한 후 다음과 유사한 출력이 표시됩니다.

```output
sha256:91a0cf9aa9857bebcd7ebec3418970f97f043e31987fd4a257c8ac8c8418dc38
```

이제 `docker images`를 실행하여 컨테이너 이미지 목록을 봅니다.

```bash
docker images
```

사용자 지정 Python 이미지가 보일 것입니다.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED             SIZE
python-custom       latest              1f231e7127a1        6 seconds ago       922MB
python              latest              638817465c7d        24 hours ago        922MB
alpine              latest              11cd0b38bc3c        2 weeks ago         4.41MB
```

새 이미지에서 컨테이너를 실행합니다. 컨테이너 내에서 실행할 명령 또는 프로세스도 지정해야 합니다. 이 예제에서는 `python hello.py`를 실행합니다.


```bash
docker run python-custom python hello.py
```

컨테이너가 시작되고 'Hello World' 메시지가 출력됩니다. 그런 다음, Python 프로세스가 완료되고 컨테이너가 중지됩니다.

```output
Hello World!
```

## <a name="automated-image-creation"></a>자동화된 이미지 만들기

지난 섹션에서는 수동으로 컨테이너 이미지를 만들었습니다. 이 방법은 일회성 또는 경험을 쌓기 위한 이미지 만들기에는 적합하지만, 프로덕션 환경에서 유지 가능한 방법이 아닙니다. *Dockerfile* 및 `docker build` 명령을 사용하여 컨테이너 이미지 만들기를 자동화할 수 있습니다. *docker build* 명령은 기본적으로 컨테이너를 시작하고, *Dockerfile*에서 찾은 지침을 실행하고, 결과를 새 컨테이너 이미지에 캡처합니다.

*Dockerfile*이라는 파일을 만들고 다음 텍스트를 입력합니다.

```bash
FROM python

WORKDIR ./app

RUN echo 'print("Hello World!")' > hello.py

CMD python hello.py
```

*FROM* 문은 이미지 만들기에 사용할 기본 이미지를 지정합니다. *RUN* 문은 컨테이너 내에서 명령을 실행합니다. *RUN*은 소프트웨어를 설치하고, 구성을 변경하고, 캡처 이벤트 전에 컨테이너를 정리하는 데 사용할 수 있습니다. *CMD* 문은 컨테이너가 시작될 때 실행할 프로세스를 지정합니다.

`docker build` 명령을 사용하여 Dockerfile에 지정된 지침을 따르는 새 컨테이너 이미지를 만듭니다.

```bash
docker build -t python-dockerfile .
```

다음과 유사한 결과가 표시됩니다.

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

`docker images` 명령을 사용하여 컨테이너 이미지 목록을 반환합니다.

```bash
docker images
```

사용자 지정 이미지가 보일 것입니다.

```output
REPOSITORY          TAG                 IMAGE ID            CREATED              SIZE
python-dockerfile   latest              98c39b91770f        About a minute ago   922MB
python              latest              638817465c7d        26 hours ago         922MB
alpine              latest              11cd0b38bc3c        2 weeks ago          4.41MB
```

`docker run` 명령을 사용하여 사용자 지정 이미지에서 컨테이너를 실행합니다.

여기서는 `docker run` 명령에 아무 인수도 제공되지 않았습니다. 수동으로 컨테이너 이미지를 만들 때와는 달리, Dockerfile을 사용하면 컨테이너가 시작될 때 실행할 명령을 포함할 수 있습니다. 이 예에서 지정된 명령은 컨테이너에 Python 스크립트를 실행하라고 지시하는 `python hello.py`입니다.

```bash
docker run python-dockerfile
```

명령을 실행하면 컨테이너 출력이 표시됩니다.

```output
Hello World!
```

## <a name="push-the-image-to-a-public-registry"></a>이미지를 공용 레지스트리에 푸시합니다.

Docker 허브는 공용 컨테이너 레지스트리입니다. 컨테이너 이미지를 Docker 허브에 푸시하려면 Docker 계정이 있어야 합니다. 필요한 경우 [Docker 허브 사이트](https://hub.docker.com/)를 방문하여 계정을 등록합니다.

Docker 허브 계정을 만든 후에는 계정 이름을 컨테이너 이미지의 태그로 지정해야 합니다. 이렇게 하려면 `docker tag` 명령을 사용합니다.

다음 예제에서는 Docker 허브 계정 이름을 *python dockerfile* 이미지의 태그로 지정합니다. `<account name>`을 Docker 허브 계정 이름으로 바꿉니다.

```bash
docker tag python-dockerfile <account name>/python-dockerfile
```

다음으로, `docker login` 명령을 사용하여 Docker 허브에 로그인되었는지 확인합니다.

```bash
docker login
```

마지막으로, `docker push` 명령을 사용하여 *python-dockerfile* 이미지를 Docker 허브에 푸시합니다. `<account name>`을 Docker 허브 계정 이름으로 바꿉니다.

```bash
docker push <account name>/python-dockerfile
```

컨테이너 이미지가 Docker 허브에 업로드되는 동안 다음과 유사한 출력이 표시됩니다.

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
```

컨테이너 이미지가 Docker 허브에 저장되었으며 인터넷에 연결된 모든 머신에서 `docker pull` 또는 `docker run` 명령을 사용하여 액세스할 수 있습니다.

## <a name="summary"></a>요약

이 섹션에서는 두 개의 컨테이너 이미지를 만들었습니다. 첫 번째 이미지는 수동으로 만들었고 두 번째 이미지는 Dockerfile을 사용하여 자동화했습니다.
