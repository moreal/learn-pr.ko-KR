이 단원에서는 Azure에 호스트된 Ubuntu Linux 가상 머신에 Node.js(MEAN 머리글자어의 **N**)를 설치합니다. Node.js는 HTTP 트래픽을 처리하고 웹 응용 프로그램을 호스트하는 데 런타임으로 사용됩니다.

## <a name="connect-to-the-vm"></a>VM에 연결

Node.js를 설치하려면 **ssh**를 사용하여 VM에 연결해야 합니다. 아직 VM에 연결되지 않은 경우 다음 명령을 실행합니다. `<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공용 IP 주소로 바꿉니다.

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-nodejs"></a>Node.js 설치

> [!Important]
> Ubuntu는 **Node.js-legacy**라는 비공식 패키지를 제공합니다. 이 패키지는 Node.js에서 유지되지 않으며 만료되었습니다.

1. **apt-get**이 가상 머신에 설치할 올바른 패키지를 찾을 수 있도록 Node.js 패키지 리포지토리를 등록합니다.

    ```bash
    curl -sL https://deb.nodesource.com/setup_8.x | sudo -E bash -
    ```

1. Linux 시스템에 Node.js 패키지를 설치합니다.

    ```bash
    sudo apt-get install -y Node.js
    ```

1. 다음의 간단한 Node.js 명령을 실행하여 Node.js 설치에 성공했는지 확인합니다.

    ```bash
    node -v
    ```

    `v8.11.4`처럼 출력되어야 하며, 패키지를 설치할 때 사용 가능한 최신 Node.js 버전을 반영하는 버전을 포함합니다.

## <a name="summary"></a>요약

가상 머신에 Node.js가 설치되면 실행해야 하는 웹 응용 프로그램 빌드를 시작할 수 있습니다.