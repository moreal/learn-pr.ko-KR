이 단원에서는 Ubuntu Linux 가상 머신에 MongoDB를 설치하여 향후 샘플 웹 응용 프로그램의 데이터 저장소로 사용합니다.

## <a name="connect-to-the-vm"></a>VM에 연결

MongoDB를 설치하려면 **ssh**를 사용하여 VM에 연결해야 합니다. `<vm-admin-username>` 및 `<vm-public-ip>` 자리 표시자를 위의 관리자 사용자 이름과 VM의 공용 IP 주소로 바꿉니다.

```bash
ssh <vm-admin-username>@<vm-public-ip>
```

## <a name="install-mongodb"></a>MongoDB 설치

> [!Important]
> Ubuntu는 **mongodb**라는 비공식 패키지를 제공합니다. 이 패키지는 MongoDB inc에서 유지 관리되지 않습니다.

1. MongoDB 리포지토리의 암호화 키를 가져옵니다. 이렇게 하면 설치하는 mongodb 패키지가 MongoDB Inc.에서 제공하는 것인지를 패키지 관리자가 확인할 수 있습니다.

    ```bash
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 9DA31620334BD75D9DCB49F368818C72E52529D4
    ```

    **sudo** 명령은 관리자 권한으로 지정된 명령을 실행하고자 함을 의미합니다.

1. 패키지 관리자가 mongodb 패키지를 찾을 수 있도록 MongoDB Ubuntu 리포지토리를 등록합니다.

    > [!NOTE]
    > 이 명령은 Ubuntu 버전별로 다릅니다. 사용 중인 Ubuntu 버전을 찾으려면 `uname -v`를 실행하세요.
    > 이 명령은 `#21~16.04.1-Ubuntu SMP Fri Aug 10 12:36:09 UTC 2018`과 같이 출력합니다.
    >
    > 이 출력은 Ubuntu 버전 16.04.1을 실행 중임을 나타냅니다.
    > 버전의 정확한 명령을 가져오려면 [Ubuntu에 MongoDB Community Edition 설치](https://docs.mongodb.com/manual/tutorial/install-mongodb-on-ubuntu/) 설명서를 참조하세요.

    Ubuntu 16.04에서 다음 명령을 실행합니다.

    ```bash
    echo "deb [ arch=amd64,arm64 ] https://repo.mongodb.org/apt/ubuntu xenial/mongodb-org/4.0 multiverse" | sudo tee /etc/apt/sources.list.d/mongodb-org-4.0.list
    ```

1. 최신 패키지 정보를 포함하도록 패키지 데이터베이스를 다시 로드합니다.

    ```bash
    sudo apt-get update
    ```

1. VM에 MongoDB 패키지를 설치합니다.

    ```bash
    sudo apt-get install -y mongodb-org
    ```

1. 나중에 연결할 수 있도록 MongoDB 서비스를 시작합니다.

    ```bash
    sudo service mongod start
    ```

## <a name="summary"></a>요약

이제 Ubuntu Linux VM에 MongoDB가 설치되었습니다. MongoDB는 웹 응용 프로그램에서 저장하고 검색하는 정보에 대한 지원 데이터 저장소로 사용됩니다.