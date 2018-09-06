소프트웨어 개발자는 코드를 작성할 때 가능한 한 많은 시간을 절약하려고 합니다. Azure Storage와 상호 작용하기 위해 REST 엔드포인트를 사용할 수 있지만, 이 경우 상당한 양의 작업이 필요합니다. 이러한 문제로 인해 Azure Storage에 신속하게 연결하고 이를 사용하기 위한 라이브러리가 개발 중입니다. 일반적으로 이러한 라이브러리를 *클라이언트 라이브러리*라고 하며, Azure Storage와 상호 작용하는 가장 쉬운 방법입니다. 

여기서는 해당 클라이언트 라이브러리를 .NET 응용 프로그램에서 참조로 추가하는 방법을 알아봅니다.

## <a name="application-programming-interface-api"></a>API(응용 프로그래밍 인터페이스)

Azure Storage는 REST(Representational State Transfer) 프로토콜을 사용하며 인터넷을 통해 API(응용 프로그래밍 인터페이스) 집합을 사용하여 서비스를 노출합니다. 이러한 API는 [Azure Storage 서비스 REST API 참조](https://docs.microsoft.com/en-us/rest/api/storageservices/)에 완전히 문서화되어 있습니다. 이러한 API와 직접 상호 작용할 수 있지만, Azure Storage에는 일반적으로 클라이언트 라이브러리를 사용하여 액세스합니다. API는 적절한 테스트를 거쳤으므로, 클라이언트 라이브러리를 통해 응용 프로그램 개발자의 작업량을 크게 줄일 수 있습니다.

## <a name="language-support"></a>언어 지원

Azure Storage에 액세스하기 위한 클라이언트 라이브러리가 많이 있으며 이러한 라이브러리는 여러 언어를 지원합니다. 이 [SDK 도구 설명서 페이지](https://docs.microsoft.com/en-us/azure/#pivot=sdkstools)에는 현재 지원되는 모든 언어의 클라이언트 라이브러리 또는 SDK에 대한 링크가 포함되어 있습니다. 여기에는 .NET, Java, Python, Node.js 및 Go가 포함됩니다.

## <a name="summary"></a>요약

Azure Storage는 모든 서비스와 상호 작용하기 위한 REST 엔드포인트를 제공합니다. 이러한 엔드포인트를 사용할 수 있지만 클라이언트 라이브러리를 사용하는 것이 더 일반적입니다. Azure Storage는 .NET, Java, Python 및 Node.js를 비롯한 여러 언어를 지원합니다.


