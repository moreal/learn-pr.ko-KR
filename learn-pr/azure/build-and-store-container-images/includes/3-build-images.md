귀하의 회사에서는 컨테이너 이미지를 사용하여 계산 워크로드를 관리한다고 가정합니다. 로컬 Docker 도구를 사용하여 컨테이너 이미지를 빌드합니다.

이제 Azure Container Registry 작업을 사용하여 이러한 컨테이너를 빌드할 수 있습니다. Container Registry 작업을 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와도 통합할 수 있습니다.

Azure Container Registry 작업을 사용하여 컨테이너 이미지 만들기를 자동화하겠습니다.

## <a name="create-a-container-image-with-azure-container-registry-tasks"></a>Azure Container Registry 작업을 사용하여 컨테이너 이미지 만들기

빌드 지침을 제공하는 표준 Dockerfile입니다. Azure Container Registry 작업을 사용하면 다단계 빌드를 포함하여 현재 환경에서 모든 Dockerfile을 다시 사용할 수 있습니다.

이 예제에서는 새 Dockerfile을 사용하겠습니다.

<!-- Activate the sandbox -->
[!include[](../../../includes/azure-sandbox-activate.md)]

첫 번째 단계는 이름이 `Dockerfile`인 새 파일을 만드는 것입니다. 모든 텍스트 편집기를 사용하여 파일을 편집할 수 있습니다. 이 예제에는 Cloud Shell 편집기를 사용합니다. 다음 명령을 Cloud Shell 창에 입력하여 편집기를 엽니다.

```bash
code
```

새 Dockerfile에 다음 내용을 복사합니다. 파일을 저장합니다.

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

키 조합 <kbd>Ctrl+S</kbd>를 사용하여 저장합니다. 메시지가 표시되면 `Dockerfile` 파일의 이름을 지정합니다.

이 구성은 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가합니다. 그런 다음, *EXPOSE* 명령을 통해 포트 80에서 응용 프로그램을 제공하도록 컨테이너를 구성합니다.

이제 Azure CLI 명령 `az acr build`를 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.

```azurecli
az acr build --registry <acrName> --image helloacrtasks:v1 .
```

명령을 실행할 때 빌드되어 Container Registry로 푸시되는 이미지가 표시됩니다.

## <a name="verify-the-image"></a>이미지 확인

다음 명령을 실행하여 이미지가 만들어지고 레지스트리에 저장되었는지 확인합니다.

```azurecli
az acr repository list --name <acrName> --output table
```

출력은 다음과 비슷해야 합니다.

```console
Result
-------------
helloacrtasks
```

이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.
