대부분의 응용 프로그램에는 데이터 저장소가 필요합니다. MongoDB(MEAN 스택의 “M”)는 가장 인기 있는 NoSQL 데이터 저장소 솔루션의 하나이며 무료 오픈 소스입니다. NoSQL 데이터 저장소는 SQL Server 또는 MySQL 같은 관계형 데이터베이스처럼 미리 정의된 방식으로 데이터를 구조화할 필요가 없습니다.

MongoDB는 엄격한 데이터 구조가 필요 없는 JSON 같은 문서에 데이터를 저장합니다. 그런 다음, JSON(JavaScript Object Notation)으로 전송된 쿼리 및 명령을 사용하여 MongoDB와 상호 작용합니다.

## <a name="mongodb-versions"></a>MongoDB 버전

사용할 수 있는 두 가지 버전의 MongoDB는 다음과 같습니다.

- MongoDB Community Server
- MongoDB Enterprise Server

이 모듈에서는 웹 응용 프로그램의 데이터 저장소에 대해 이 문서 작성 당시의 MongoDB Community Server 버전 3.6을 사용하겠습니다.

## <a name="how-to-install-mongodb"></a>MongoDB 설치 방법

MongoDB는 Linux, macOS 및 Windows에 설치할 수 있습니다. 이 모듈의 경우 Ubuntu Linux VM에 설치하지만, 권장되는 패키지 관리자는 OS 및 배포에 따라 다릅니다. 모든 운영 체제의 설치 프로세스는 [MongoDB 설치 설명서](https://docs.mongodb.com/manual/administration/install-community/)에 잘 설명되어 있습니다.

Ubuntu VM에 설치하려면 **apt-get** 패키지 관리자를 사용합니다.