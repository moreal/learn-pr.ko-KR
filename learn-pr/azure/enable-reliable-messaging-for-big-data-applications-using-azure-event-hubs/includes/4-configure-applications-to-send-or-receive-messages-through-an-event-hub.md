이벤트 허브를 만들고 구성한 후에는 이벤트 데이터 스트림을 보내고 받도록 응용 프로그램을 구성해야 합니다.

예를 들어 결제 처리 솔루션은 발신자 응용 프로그램 형식을 사용하여 고객의 신용 카드 데이터를 수집하고 수신자 응용 프로그램 형식을 사용하여 신용 카드가 유효한지 확인합니다.

Java 응용 프로그램 구성 방식에는 차이가 있지만, .NET 응용 프로그램과 비교하여 응용 프로그램을 이벤트 허브에 연결하고 메시지를 성공적으로 보내거나 받을 수 있는 일반적인 원칙이 있습니다. 따라서 Java 구성 텍스트 파일을 편집하는 프로세스가 Visual Studio를 사용하여 .NET 응용 프로그램을 준비하는 것과 다르더라도 원칙은 동일합니다.

## <a name="what-are-the-minimum-event-hub-application-requirements"></a>최소 이벤트 허브 응용 프로그램 요구 사항은 무엇인가요?

이벤트 허브로 메시지를 보내도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공해야 합니다.

- 이벤트 허브 네임스페이스 이름
- 이벤트 허브 이름
- 공유 액세스 정책 이름
- 기본 공유 액세스 키

이벤트 허브에서 메시지를 받도록 응용 프로그램을 구성하려면, 응용 프로그램이 연결 자격 증명을 만들 수 있도록 다음 정보를 제공합니다.

- 이벤트 허브 네임스페이스 이름
- 이벤트 허브 이름
- 공유 액세스 정책 이름
- 기본 공유 액세스 키
- 저장소 계정 이름
- 저장소 계정 연결 문자열
- 저장소 계정 컨테이너 이름

Azure Blob Storage에 메시지를 저장하는 수신자 응용 프로그램이 있는 경우 먼저 저장소 계정을 구성해야 합니다.

## <a name="the-azure-cli-commands-for-creating-a-general-purpose-standard-storage-account"></a>범용 표준 저장소 계정을 만들기 위한 Azure CLI 명령

1. 리소스 그룹 및 리소스 그룹을 만들 때 사용한 것과 동일한 Azure 데이터 센터 위치에 저장소 계정(범용 V2)을 만듭니다.

    ```azurecli
    az storage account create --name <storage account name> --resource-group <resource group name> --location <location> --sku Standard_RAGRS --encryption blob
    ```
2. 이 저장소에 액세스하려면 저장소 계정 액세스 키가 필요합니다. 저장소 계정과 연결된 액세스 키를 봅니다.

    ```azurecli
    az storage account keys list --account-name <storage account name> --resource-group <resource group name>
    ```
3. **key1**과 연결된 값을 저장합니다.
4. 저장소 계정에 대한 연결 정보도 필요합니다. 저장소 계정에 대한 연결 문자열을 봅니다.

    ```azurecli
    az storage account show-connection-string -n <storage account name> -g <resource group name>
    ```
5. **connectionString**과 연결된 값을 저장합니다.
6. 메시지는 저장소 계정 내의 컨테이너에 저장됩니다. 이전 단계의 연결 문자열과 함께 `<connection string>`을 사용하여 저장소 계정에 컨테이너를 만듭니다.

    ```azurecli
    az storage container create -n <container> --connection-string "<connection string>"
    ```

## <a name="shell-command-for-cloning-an-application-github-repository"></a>응용 프로그램 GitHub 리포지토리를 복제하기 위한 셸 명령

Git은 배포 버전 제어 모델을 사용하는 공동 작업 도구이며 소프트웨어 및 문서 프로젝트에 대한 공동 작업을 위해 설계되었습니다. Git 클라이언트는 Windows를 비롯한 여러 플랫폼에서 사용할 수 있으며 Git 명령줄은 Azure Bash Cloud Shell에 포함되어 있습니다. GitHub는 Git 리포지토리에 대한 웹 기반 호스팅 서비스입니다. 

GitHub에서 프로젝트로 호스트되는 응용 프로그램이 있는 경우 **git clone** 명령을 사용하여 리포지토리를 복제하면 프로젝트의 로컬 복사본을 만들 수 있습니다.

1. 리포지토리를 홈 디렉터리에 복제합니다.

    ```azurecli
      git clone https://github.com/<project repository>
    ```

## <a name="shell-commands-for-preparing-an-application"></a>응용 프로그램을 준비하기 위한 셸 명령

1. 이제 **nano**와 같은 편집기를 사용하여 응용 프로그램을 편집하고 이벤트 허브 네임스페이스, 이벤트 허브 이름, 공유 액세스 정책 이름 및 기본 키를 추가할 수 있습니다. Nano는 Linux 및 기타 Unix 같은 운영 체제에 사용할 수 있는 간단한 텍스트 편집기이며, Azure Bash Cloud Shell에서도 사용할 수 있습니다. 예를 들어 이 명령을 사용하여 **nano** 편집기에서 Java 응용 프로그램 파일을 엽니다.

    ```azurecli
    nano <application>.java
    ```

1. 응용 프로그램 개발 방법에 따라 이벤트 허브 구성 정보를 추가한 후 응용 프로그램을 컴파일하거나 빌드해야 할 수 있습니다. 예를 들어 다음 단원에서 사용되는 Java 응용 프로그램은 Apache **Maven**과 같은 도구를 사용하여 빌드해야 합니다. Maven은 .java 파일을 .class 파일로 컴파일하거나 .jar 파일로 패키지합니다. Maven은 Bash Cloud Shell에서 사용할 수 있으며, Java 응용 프로그램을 빌드하려면 **mvn** 명령을 사용합니다. 이 mvn 명령을 사용하여 Java 응용 프로그램을 빌드합니다.

    ```azurecli
    mvn clean package -DskipTests
    ```

## <a name="summary"></a>요약

발신자 및 수신자 응용 프로그램은 이벤트 허브 환경에 대한 특정 정보로 구성되어야 합니다. 수신자 응용 프로그램이 메시지를 Blob Storage에 저장하는 경우 저장소 계정을 만듭니다. 응용 프로그램이 GitHub에서 호스트되는 경우 응용 프로그램을 로컬 디렉터리에 복제해야 합니다. **nano**와 같은 텍스트 편집기는 네임스페이스를 응용 프로그램에 추가하는 데 사용됩니다.