<span data-ttu-id="83010-101">emulador do storage Olá suporta uma única conta fixa e uma chave de autenticação conhecidos para a autenticação de chave partilhada.</span><span class="sxs-lookup"><span data-stu-id="83010-101">hello storage emulator supports a single fixed account and a well-known authentication key for Shared Key authentication.</span></span> <span data-ttu-id="83010-102">Esta conta e chave são Olá credenciais de chave partilhada apenas permitidas para utilização com o emulador do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="83010-102">This account and key are hello only Shared Key credentials permitted for use with hello storage emulator.</span></span> <span data-ttu-id="83010-103">São:</span><span class="sxs-lookup"><span data-stu-id="83010-103">They are:</span></span>

```
Account name: devstoreaccount1
Account key: Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==
```

> [!NOTE]
> <span data-ttu-id="83010-104">chave de autenticação de Olá suportado pelo emulador do storage Olá destina-se apenas para testes Olá funcionalidades do seu código de autenticação de cliente.</span><span class="sxs-lookup"><span data-stu-id="83010-104">hello authentication key supported by hello storage emulator is intended only for testing hello functionality of your client authentication code.</span></span> <span data-ttu-id="83010-105">Servem qualquer objetivo de segurança.</span><span class="sxs-lookup"><span data-stu-id="83010-105">It does not serve any security purpose.</span></span> <span data-ttu-id="83010-106">Não é possível utilizar a conta de armazenamento de produção e a chave com o emulador do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="83010-106">You cannot use your production storage account and key with hello storage emulator.</span></span> <span data-ttu-id="83010-107">Não deve utilizar a conta de desenvolvimento de Olá com dados de produção.</span><span class="sxs-lookup"><span data-stu-id="83010-107">You should not use hello development account with production data.</span></span>
> 
> <span data-ttu-id="83010-108">emulador do storage Olá suporta a ligação através de HTTP apenas.</span><span class="sxs-lookup"><span data-stu-id="83010-108">hello storage emulator supports connection via HTTP only.</span></span> <span data-ttu-id="83010-109">No entanto, o HTTPS é Olá recomendado protocolo para aceder a recursos na conta do storage do Azure de produção.</span><span class="sxs-lookup"><span data-stu-id="83010-109">However, HTTPS is hello recommended protocol for accessing resources in a production Azure storage account.</span></span>
> 

#### <a name="connect-toohello-emulator-account-using-a-shortcut"></a><span data-ttu-id="83010-110">Ligar a conta de emulador de toohello utilizando um atalho</span><span class="sxs-lookup"><span data-stu-id="83010-110">Connect toohello emulator account using a shortcut</span></span>
<span data-ttu-id="83010-111">Olá mais fácil forma tooconnect toohello emulador de armazenamento da sua aplicação é tooconfigure uma cadeia de ligação no ficheiro de configuração da aplicação que referencia o atalho Olá `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="83010-111">hello easiest way tooconnect toohello storage emulator from your application is tooconfigure a connection string in your application's configuration file that references hello shortcut `UseDevelopmentStorage=true`.</span></span> <span data-ttu-id="83010-112">Eis um exemplo de um emulador do storage de toohello cadeia ligação num *App. config* ficheiro:</span><span class="sxs-lookup"><span data-stu-id="83010-112">Here's an example of a connection string toohello storage emulator in an *app.config* file:</span></span> 

```xml
<appSettings>
  <add key="StorageConnectionString" value="UseDevelopmentStorage=true" />
</appSettings>
```

#### <a name="connect-toohello-emulator-account-using-hello-well-known-account-name-and-key"></a><span data-ttu-id="83010-113">Ligar a conta de emulador de toohello utilizando o nome de conta conhecidos Olá e chave</span><span class="sxs-lookup"><span data-stu-id="83010-113">Connect toohello emulator account using hello well-known account name and key</span></span>
<span data-ttu-id="83010-114">toocreate uma cadeia de ligação que referências Olá nome da conta do emulador e chave, terá de especificar pontos finais de Olá para cada um dos Olá serviços pretendem toouse do emulador de Olá na cadeia de ligação de Olá.</span><span class="sxs-lookup"><span data-stu-id="83010-114">toocreate a connection string that references hello emulator account name and key, you must specify hello endpoints for each of hello services you wish toouse from hello emulator in hello connection string.</span></span> <span data-ttu-id="83010-115">Isto é necessário para que a cadeia de ligação de Olá fará referência Olá emulador pontos finais, que são diferentes dos para uma conta de armazenamento de produção.</span><span class="sxs-lookup"><span data-stu-id="83010-115">This is necessary so that hello connection string will reference hello emulator endpoints, which are different than those for a production storage account.</span></span> <span data-ttu-id="83010-116">Por exemplo, valor Olá a cadeia de ligação terá este aspeto:</span><span class="sxs-lookup"><span data-stu-id="83010-116">For example, hello value of your connection string will look like this:</span></span>

```
DefaultEndpointsProtocol=http;AccountName=devstoreaccount1;
AccountKey=Eby8vdM02xNOcqFlqUwJPLlmEtlCDXJ1OUzFT50uSRZ6IFsuFq2UVErCz4I6tq/K1SZFPTOtr/KBHBeksoGMGw==;
BlobEndpoint=http://127.0.0.1:10000/devstoreaccount1;
TableEndpoint=http://127.0.0.1:10002/devstoreaccount1;
QueueEndpoint=http://127.0.0.1:10001/devstoreaccount1;
```

<span data-ttu-id="83010-117">Este valor é atalho toohello idênticos mostrado acima, `UseDevelopmentStorage=true`.</span><span class="sxs-lookup"><span data-stu-id="83010-117">This value is identical toohello shortcut shown above, `UseDevelopmentStorage=true`.</span></span>

#### <a name="specify-an-http-proxy"></a><span data-ttu-id="83010-118">Especifique um proxy HTTP</span><span class="sxs-lookup"><span data-stu-id="83010-118">Specify an HTTP proxy</span></span>
<span data-ttu-id="83010-119">Também pode especificar um toouse de proxy HTTP quando estiver a testar o seu serviço de emulador do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="83010-119">You can also specify an HTTP proxy toouse when you're testing your service against hello storage emulator.</span></span> <span data-ttu-id="83010-120">Isto pode ser útil para observar os pedidos e respostas HTTP enquanto estiver a depuração operações nos serviços de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="83010-120">This can be useful for observing HTTP requests and responses while you're debugging operations against hello storage services.</span></span> <span data-ttu-id="83010-121">toospecify um proxy, adicionar Olá `DevelopmentStorageProxyUri` opção toohello cadeia de ligação e defina o URI de proxy toohello de valor.</span><span class="sxs-lookup"><span data-stu-id="83010-121">toospecify a proxy, add hello `DevelopmentStorageProxyUri` option toohello connection string, and set its value toohello proxy URI.</span></span> <span data-ttu-id="83010-122">Por exemplo, aqui é uma cadeia de ligação que aponta toohello emulador de armazenamento e configura um proxy HTTP:</span><span class="sxs-lookup"><span data-stu-id="83010-122">For example, here is a connection string that points toohello storage emulator and configures an HTTP proxy:</span></span>

```
UseDevelopmentStorage=true;DevelopmentStorageProxyUri=http://myProxyUri
```

