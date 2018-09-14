이 단원에서는 Azure에 호스트된 Ubuntu Linux 가상 머신에 Node.js(MEAN 약어의 **N**)를 설치합니다. Node.js는 HTTP 트래픽을 처리하고 웹 응용 프로그램을 호스트하기 위해 런타임으로 사용됩니다.

## <a name="install-nodejs"></a>Node.js 설치

1. **하지 않은 경우 여전히 SSHed 이전 연습에서 VM으로**에 SSH 합니다.

    ```bash
    ssh <vm-admin-username>@<vm-public-ip>
    ```

1. **apt-get**이 가상 머신에 설치할 올바른 패키지를 찾을 수 있도록 Node.js 패키지 리포지토리를 등록합니다.

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. Linux 시스템에 Node.js 패키지를 설치합니다.

    ```bash
    sudo apt-get install -y Node.js
    ```

1. 간단한 다음 Node.js 명령을 실행하여 Node.js 설치에 성공했는지 확인합니다.

    ```bash
    node -v
    ```

    `v8.11.4`처럼 출력되어야 하며, 패키지를 설치할 때 사용 가능한 최신 Node.js 버전을 반영하는 버전을 포함합니다.

## <a name="summary"></a>요약

가상 머신에 Node.js가 설치되면 실행해야 하는 웹 응용 프로그램 빌드를 시작할 수 있습니다.