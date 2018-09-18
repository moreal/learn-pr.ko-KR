귀하의 회사에서는 컨테이너 이미지를 사용하여 회사의 계산 워크로드를 관리합니다. 로컬 Docker 도구를 사용하여 컨테이너 이미지를 빌드합니다. Azure Container Registry를 사용하기로 결정하면 이제 클라우드에서 컨테이너 이미지를 빌드할 수 있습니다. 

이제 Azure Container Registry Build를 사용하여 이러한 컨테이너를 빌드할 수 있습니다. Container Registry 빌드를 사용하면 소스 코드 커밋에서 DevOps 프로세스를 자동화된 빌드와도 통합할 수 있습니다.

Azure Container Registry Build를 사용하여 컨테이너 이미지 만들기를 자동화하겠습니다.

## <a name="create-a-container-image-with-azure-container-registry-build"></a>Azure Container Registry Build를 사용하여 컨테이너 이미지 만들기

표준 Dockerfile을 사용하여 빌드 지침을 제공합니다. Azure Container Registry Build를 사용하면 다단계 빌드를 포함하여 현재 환경에서 모든 Dockerfile을 다시 사용할 수 있습니다.

예제로 새 Dockerfile을 사용하겠습니다. 

첫 번째 단계는 `Dockerfile`이라는 새 파일을 만드는 것입니다. 모든 텍스트 편집기를 사용하여 파일을 편집할 수 있습니다. 이 예제로 Visual Studio Code를 사용하겠습니다.

```bash
code Dockerfile
```

새 Dockerfile에 다음 내용을 복사합니다. 파일이 안전한지 확인합니다. 

```bash
FROM    node:9-alpine
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/package.json /
ADD     https://raw.githubusercontent.com/Azure-Samples/acr-build-helloworld-node/master/server.js /
RUN     npm install
EXPOSE  80
CMD     ["node", "server.js"]
```

이 구성에서는 `node:9-alpine` 이미지에 Node.js 응용 프로그램을 추가합니다. 그런 다음, *EXPOSE* 명령을 통해 포트 80에서 응용 프로그램을 제공하도록 컨테이너를 구성합니다.

이제 Azure CLI 명령 `az acr build`를 실행하여 Dockerfile에서 컨테이너 이미지를 빌드합니다.

```azurecli
az acr build --registry <acrName> --image helloacrbuild:v1 .
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
helloacrbuild
```

이제 `helloacrbuild` 이미지를 사용할 준비가 되었습니다.
