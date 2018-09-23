Data Science Virtual Machine을 실행했으므로 첫 번째 딥 러닝 모델을 학습하기로 합니다. 서버의 다른 모든 항목과 격리된 상태에서 실험을 실행하려고 합니다. 그렇게 하려면 Docker 컨테이너 내에서 실행합니다.

## <a name="connect-to-the-vm-with-ssh"></a>ssh로 VM에 연결하기

ssh를 통해 VM에 계속 연결되어 있는지 확인합니다. 그렇지 않다면 이 명령을 다시 실행하여 가상 머신에 원격으로 되돌아갑니다.

1. Azure Cloud Shell에서 다음 명령을 실행하여 VM에 로그인합니다.

    ```azurecli 
    ssh <USERNAME>@<IP>
    ``` 
    
    VM을 만들 때 정의한 관리자 계정 이름으로 `<USERNAME>`을 대체합니다. 이전 연습에서 저장한 VM의 IP 주소로 `<IP>`을 대체합니다.  

1. 메시지가 표시되면 관리자 계정의 암호를 입력하여 로그인 프로세스를 완료합니다.

## <a name="run-a-jupyter-notebook-server-in-a-docker-container-in-the-vm"></a>VM의 Docker 컨테이너에서 Jupyter Notebook 서버 실행하기

> [!NOTE]
> VM에 하나의 관리자 계정, 즉 루트 계정만 가지고 있기 때문에 `sudo`을 사용하여 모든 Docker 명령을 루트로서 실행해야 합니다.

1. VM에 어떤 Docker 컨테이너가 있는지 확인하려면 명령 프롬프트에서 다음의 명령을 실행합니다.

    ```azurecli 
    sudo docker ps
    ```

1. 명령 프롬프트에서 다음의 명령을 실행하여 실험을 위한 새 컨테이너를 만듭니다.

    ```azurecli 
    sudo docker run --rm -it --entrypoint '/bin/sh' -p 8888:8888 pytorch/pytorch -c \
    'conda install jupyter matplotlib -y &&\
    curl https://pytorch.org/tutorials/_downloads/cifar10_tutorial.ipynb > first_pytorch_classifier.ipynb &&\
    jupyter notebook --ip=0.0.0.0 --no-browser --allow-root'
    ``` 

    이 명령은 꽤 오래 실행됩니다. 따라서 명령이 무엇을 하는지 잠시 살펴보겠습니다. 
    - `docker run`은 새 컨테이너에서 명령을 실행합니다. 사용되는 Docker 이미지는 pytorch/pytorch입니다. 이것은 먼저 지정된 이미지 위에 쓰기가 가능한 컨테이너 계층을 만든 다음, 지정된 명령을 사용하여 그것을 시작합니다.
    - `--rm`이 종료되면 컨테이너가 제거됩니다. 관련 컨테이너를 유지하려면 이 인수를 드롭합니다. 
    - `--entrypoint 'bin/sh'`은 이미지의 기본 진입점을 덮어써서 Bash shell이 됩니다.
    - `-c`은 컨테이너를 시작할 때 실행하는 명령을 정의합니다. 이 경우, 세 가지 명령을 실행합니다.
        - Jupyter 및 matplotlib 설치하기
        - pytorch.org에서 `first_pytorch_classifier.ipynb`로 호출된 컨테이너의 파일로 노트북(cifar10_tutorial.ipynb) 복사하기
        - 이전의 연습과 동일한 방식으로 컨테이너에서 노트북 서버를 시작합니다.  브라우저가 시작되는 것이 아니라, 노트북이 루트에 의해 액세스되고 모든 포트에 수신 대기합니다. 
    
    노트북 서버는 그 컨테이너의 모든 포트에 수신 대기합니다. 하지만 어떻게 트래픽이 컨테이너 외부에서 들어올까요? 호스트 머신에서 TCP 포트 8888로 컨테이너의 `-p 8888:8888` 포트를 인수가 바인딩합니다 `8888`. 따라서 포트 8888을 통해 VM에 들어오는 트래픽은 컨테이너에 의해 선택됩니다. 

## <a name="connect-to-the-jupyter-notebook-server-from-a-remote-browser"></a>원격 브라우저에서 Jupyter Notebook 서버에 연결하기 

컨테이너에서 Jupyter Notebook이 실행되면 다음의 메시지와 유사한 메시지가 표시됩니다. 

> *처음으로 연결할 때 토큰을 사용하여 로그인하려면 http://(5b8783e7911d or 127.0.0.1):8888/?token={sometoken} URL을 복사하여 브라우저에 붙여넣습니다.*

1. URL의 **http://(5b8783e7911d or 127.0.0.1)** 부분을 `<HOSTNAME>.<REGION>.cloudapp.azure.com`이나 VM의 IP로 바꾸고 브라우저의 새 탭에서 그 주소로 이동합니다.

    ![Jupyter Notebook 대시보드를 보여주는 스크린샷입니다. ](../media/notebook-in-docker.png)
    
    이번에는 단일 노트북만 보입니다. 사용자가 컨테이너 안에 있으며 이 노트북만 복사했기 때문입니다. 다음 연습에서는 이 노트북을 사용하여 실험합니다. 
    
    > [!TIP]
    > 아직 노트북 서버를 종료하지 마십시오. 다음 연습에서 `first_pytorch_classifier.ipynb` 노트북을 살펴보겠습니다.