---
title: "Descrição geral de comunicação de serviços aaaReliable | Microsoft Docs"
description: "Descrição geral do Olá Reliable Services modelo de comunicação, incluindo os serviços de escuta de abertura nos serviços, resolver pontos finais e comunicação entre os serviços."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: BharatNarasimman
ms.assetid: 36217988-420e-409d-b0a4-e0e875b6eac8
ms.service: service-fabric
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 04/07/2017
ms.author: vturecek
ms.openlocfilehash: 93a7017b50df0822969daa5ad78302c73e8ba641
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-hello-reliable-services-communication-apis"></a>Como toouse Olá comunicação Reliable Services APIs
Azure Service Fabric, como uma plataforma é completamente agnóstico relativamente sobre a comunicação entre os serviços. Todas as pilhas e protocolos são aceitáveis, de UDP tooHTTP. Está a funcionar toohello serviço Programador toochoose como serviços devem comunicar. estrutura da aplicação Olá Reliable Services fornece comunicação incorporada às pilhas, bem como as APIs que pode utilizar toobuild os componentes de comunicação personalizado.

## <a name="set-up-service-communication"></a>Configurar a comunicação de serviço
Olá fiável de serviços de API utiliza uma interface simples para comunicação de serviço. tooopen um ponto final para o seu serviço, basta implemente esta interface:

```csharp

public interface ICommunicationListener
{
    Task<string> OpenAsync(CancellationToken cancellationToken);

    Task CloseAsync(CancellationToken cancellationToken);

    void Abort();
}

```

```java
public interface CommunicationListener {
    CompletableFuture<String> openAsync(CancellationToken cancellationToken);

    CompletableFuture<?> closeAsync(CancellationToken cancellationToken);

    void abort();
}
```

Em seguida, pode adicionar a implementação de serviço de escuta de comunicação ao devolver uma substituição de método de classe com base no serviço.

Para serviços sem monitorização de estado:

```csharp
class MyStatelessService : StatelessService
{
    protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
    {
        ...
    }
    ...
}
```
```java
public class MyStatelessService extends StatelessService {

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ...
    }
    ...
}
```

Para os serviços com monitorização de estado:

> [!NOTE]
> Serviços fiáveis com monitorização de estado não são suportados ainda em Java.
>
>

```csharp
class MyStatefulService : StatefulService
{
    protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
    {
        ...
    }
    ...
}
```

Em ambos os casos, tem de devolver uma coleção de serviços de escuta. Isto permite que o serviço toolisten no múltiplos pontos finais, potencialmente com protocolos diferentes, utilizando vários serviços de escuta. Por exemplo, pode ter um serviço de escuta HTTP e um serviço de escuta de WebSocket separado. Cada serviço de escuta obtém um nome e a coleção de resultante Olá de *name: endereço* pares são representados como um objeto JSON quando um cliente solicita endereços de escuta de Olá para uma instância de serviço ou uma partição.

Um serviço sem monitorização de estado, substituição Olá devolve uma coleção de ServiceInstanceListeners. A `ServiceInstanceListener` contém uma função toocreate um `ICommunicationListener(C#) / CommunicationListener(Java)` e concede-lhe um nome. Para os serviços com monitorização de estado, a substituição de Olá devolve uma coleção de ServiceReplicaListeners. Isto é ligeiramente diferente do respetivo homólogo sem monitorização de estado, porque um `ServiceReplicaListener` tem uma opção tooopen um `ICommunicationListener` nas réplicas secundárias. Não só pode utilizar vários serviços de escuta de comunicação num serviço, mas também pode especificar que os serviços de escuta que aceitam pedidos em réplicas secundárias e aqueles escutarem apenas em réplicas primárias.

Por exemplo, pode ter um ServiceRemotingListener que aceita chamadas RPC apenas em réplicas primárias e uma escuta segundo, personalizada que demora leitura pedidos nas réplicas secundárias através de HTTP:

```csharp
protected override IEnumerable<ServiceReplicaListener> CreateServiceReplicaListeners()
{
    return new[]
    {
        new ServiceReplicaListener(context =>
            new MyCustomHttpListener(context),
            "HTTPReadonlyEndpoint",
            true),

        new ServiceReplicaListener(context =>
            this.CreateServiceRemotingListener(context),
            "rpcPrimaryEndpoint",
            false)
    };
}
```

> [!NOTE]
> Ao criar vários serviços de escuta para um serviço, cada serviço de escuta **tem** ser fornecido um nome exclusivo.
>
>

Por fim, descrevem pontos finais de Olá que são necessários para o serviço de Olá no Olá [manifesto serviço](service-fabric-application-model.md) na secção de Olá em pontos finais.

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

o serviço de escuta do Olá comunicação pode aceder a recursos de ponto final de Olá alocados tooit dos Olá `CodePackageActivationContext` no Olá `ServiceContext`. serviço de escuta de Olá, em seguida, pode começar a escutar para pedidos quando for aberta.

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> Recursos de ponto final são o pacote de todo o serviço de toohello comuns e são atribuídos pelo Service Fabric quando o pacote de serviço Olá está ativado. Várias réplicas de serviço alojadas no Olá pode partilhar o mesmo ServiceHost Olá mesma porta. Isto significa que o serviço de escuta de comunicação que Olá deve suportar a partilha de portas. Olá recomendada a forma de fazê-lo é Olá comunicação serviço de escuta toouse Olá partição ID e o ID de réplica/instância quando é gerado o endereço de escuta de Olá.
>
>

### <a name="service-address-registration"></a>Registo de endereço do serviço
Um serviço de sistema chamado Olá *Naming Service* é executado em clusters de Service Fabric. Olá Naming Service é uma entidade de registo para serviços e os respetivos endereços que cada instância ou a réplica do serviço de Olá está a escutar. Quando Olá `OpenAsync(C#) / openAsync(Java)` método de um `ICommunicationListener(C#) / CommunicationListener(Java)` estiver concluída, o retorno valor obtém registado no Olá Naming Service. Isto devolver o valor que obtém Olá publicado no Naming Service é uma cadeia cujo valor pode ser qualquer coisa de todo. Este valor de cadeia é clientes veem quando pedem para um endereço do serviço Olá Olá Naming Service.

```csharp
public Task<string> OpenAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.CodePackageActivationContext.GetEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.Port;

    this.listeningAddress = string.Format(
                CultureInfo.InvariantCulture,
                "http://+:{0}/",
                port);

    this.publishAddress = this.listeningAddress.Replace("+", FabricRuntime.GetNodeContext().IPAddressOrFQDN);

    this.webApp = WebApp.Start(this.listeningAddress, appBuilder => this.startup.Invoke(appBuilder));

    // hello string returned here will be published in hello Naming Service.
    return Task.FromResult(this.publishAddress);
}
```
```java
public CompletableFuture<String> openAsync(CancellationToken cancellationToken)
{
    EndpointResourceDescription serviceEndpoint = serviceContext.getCodePackageActivationContext.getEndpoint("ServiceEndpoint");
    int port = serviceEndpoint.getPort();

    this.publishAddress = String.format("http://%s:%d/", FabricRuntime.getNodeContext().getIpAddressOrFQDN(), port);

    this.webApp = new WebApp(port);
    this.webApp.start();

    /* hello string returned here will be published in hello Naming Service.
     */
    return CompletableFuture.completedFuture(this.publishAddress);
}
```

O Service Fabric fornece APIs que permitem que os clientes e outro serviços toothen peça para este endereço de por nome de serviço. Isto é importante porque o endereço do serviço Olá não é estático. Os serviços são movidos em torno num cluster de Olá para fins de balanceamento e disponibilidade de recursos. Este é o mecanismo de Olá que permitem aos clientes Olá tooresolve endereço para um serviço de escuta.

> [!NOTE]
> Para uma passagem concluída de forma toowrite um serviço de escuta de comunicação, consulte o artigo [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md) para c#, enquanto que para Java pode escrever a sua própria implementação do servidor de HTTP, consulte o artigo EchoServer aplicação exemplo ao https://github.com/Azure-Samples/service-fabric-java-getting-started.
>
>

## <a name="communicating-with-a-service"></a>Ao comunicar com um serviço
Olá fiável de serviços de API fornece Olá seguintes de clientes de toowrite de bibliotecas que comunicam com os serviços.

### <a name="service-endpoint-resolution"></a>Resolução de ponto final de serviço
primeiro passo toocommunication Olá com um serviço é tooresolve um endereço de ponto final de partição Olá ou instância de serviço Olá que pretende tootalk para. Olá `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe de utilitário é um primitivo básico que ajuda os clientes determinam Olá ponto final de um serviço em tempo de execução. Na terminologia de Service Fabric, o processo de Olá de determinar Olá ponto final de um serviço é referenciado tooas Olá *resolução de ponto final de serviço*.

tooconnect tooservices dentro de um cluster, ServicePartitionResolver pode ser criada através das predefinições. Este é Olá recomendado a utilização da maioria das situações:

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

tooconnect tooservices num cluster diferente, um ServicePartitionResolver pode ser criada com um conjunto de pontos finais de gateway do cluster. Tenha em atenção que os pontos finais de gateway são apenas diferentes pontos finais para ligar toohello mesmo cluster. Por exemplo:

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

Em alternativa, `ServicePartitionResolver` pode ser especificado uma função para a criação de um `FabricClient` toouse internamente:

```csharp
public delegate FabricClient CreateFabricClientDelegate();
```
```java
public FabricServicePartitionResolver(CreateFabricClient createFabricClient) {
...
}

public interface CreateFabricClient {
    public FabricClient getFabricClient();
}
```

`FabricClient`é um objeto de Olá que é utilizado toocommunicate com o cluster do Service Fabric Olá para várias operações de gestão no cluster de Olá. Isto é útil quando pretende mais controlo sobre como uma resolução de partição de serviço interage com o cluster. `FabricClient`efetua a colocação em cache internamente e é geralmente dispendiosa toocreate, pelo que é importante tooreuse `FabricClient` instâncias quanto possíveis.

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

Um método de resolução é utilizada tooretrieve Olá endereço de um serviço ou uma partição de serviço para os serviços particionadas.

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();

ResolvedServicePartition partition =
    await resolver.ResolveAsync(new Uri("fabric:/MyApp/MyService"), new ServicePartitionKey(), cancellationToken);
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();

CompletableFuture<ResolvedServicePartition> partition =
    resolver.resolveAsync(new URI("fabric:/MyApp/MyService"), new ServicePartitionKey());
```

Um endereço de serviço pode ser resolvido utilizando facilmente um ServicePartitionResolver, mas é necessário o mais trabalho tooensure Olá resolver o endereço pode ser utilizado corretamente. O cliente tem toodetect se a tentativa de ligação de Olá falhou devido a um erro transitório e pode ser repetida (por exemplo, serviço movido ou está temporariamente indisponível), ou um erro permanente (por exemplo, serviço foi eliminado ou hello recurso pedido já não existe). Instâncias de serviço ou de réplicas podem mover-se do nó toonode em qualquer altura para por vários motivos. endereço de serviço de Olá resolvido através de ServicePartitionResolver poderá estar obsoleto por tempo Olá que o código de cliente tenta tooconnect. Nesse caso novamente Olá cliente tem de endereço de Olá toore resolve. Fornecer Olá anterior `ResolvedServicePartition` indica que Olá resolução necessidades tootry novamente em vez de apenas obter um endereço em cache.

Normalmente, o código de cliente Olá necessário não funciona com Olá ServicePartitionResolver diretamente. É criado e transmitido toocommunication fábricas de cliente no Olá fiável de serviços de API. fábricas de Olá utilizam resolução Olá internamente toogenerate um objeto de cliente que pode ser utilizado toocommunicate com os serviços.

### <a name="communication-clients-and-factories"></a>Os clientes de comunicação e fábricas de
biblioteca de fábrica de comunicação de Olá implementa um padrão de repetição de processamento de falhas normal que facilita a repetir ligações tooresolved pontos finais de serviço. biblioteca de fábrica Olá fornece o mecanismo de repetição de Olá enquanto fornecer processadores de erro Olá.

`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Define a interface base Olá implementado por uma fábrica do cliente de comunicação que produza os clientes que podem comunicar com o serviço de Service Fabric tooa. Olá, implementação de Olá que communicationclientfactory depende da pilha de comunicações de Olá utilizada pelo serviço de Service Fabric olá onde o cliente de Olá pretende toocommunicate. Olá fiável de serviços de API fornece um `CommunicationClientFactoryBase<TCommunicationClient>`. Isto fornece uma implementação da interface de CommunicationClientFactory Olá base e executa tarefas de pilhas de comunicação de Olá tooall comuns. (Estas tarefas incluem a utilização de um ServicePartitionResolver toodetermine Olá ponto final do serviço). Clientes, normalmente, implementam a Olá abstrata CommunicationClientFactoryBase classe toohandle lógica que é a pilha de comunicações toohello específico.

apenas o cliente de comunicação de Olá recebe um endereço e utiliza-tooconnect tooa serviço. cliente de Olá pode utilizar qualquer protocolo que pretende.

```csharp
class MyCommunicationClient : ICommunicationClient
{
    public ResolvedServiceEndpoint Endpoint { get; set; }

    public string ListenerName { get; set; }

    public ResolvedServicePartition ResolvedServicePartition { get; set; }
}
```
```java
public class MyCommunicationClient implements CommunicationClient {

    private ResolvedServicePartition resolvedServicePartition;
    private String listenerName;
    private ResolvedServiceEndpoint endPoint;

    /*
     * Getters and Setters
     */
}
```

fábrica do cliente Olá é principalmente responsável pela criação de clientes de comunicação. Para clientes que não mantêm uma ligação persistente, por exemplo, um cliente HTTP, fábrica Olá só precisa de toocreate e cliente Olá de retorno. Outros protocolos que mantêm uma ligação persistente, por exemplo, alguns protocolos binários, também devem ser validados por Olá fábrica toodetermine se precisa de ligação de Olá toobe recriado.  

```csharp
public class MyCommunicationClientFactory : CommunicationClientFactoryBase<MyCommunicationClient>
{
    protected override void AbortClient(MyCommunicationClient client)
    {
    }

    protected override Task<MyCommunicationClient> CreateClientAsync(string endpoint, CancellationToken cancellationToken)
    {
    }

    protected override bool ValidateClient(MyCommunicationClient clientChannel)
    {
    }

    protected override bool ValidateClient(string endpoint, MyCommunicationClient client)
    {
    }
}
```
```java
public class MyCommunicationClientFactory extends CommunicationClientFactoryBase<MyCommunicationClient> {

    @Override
    protected boolean validateClient(MyCommunicationClient clientChannel) {
    }

    @Override
    protected boolean validateClient(String endpoint, MyCommunicationClient client) {
    }

    @Override
    protected CompletableFuture<MyCommunicationClient> createClientAsync(String endpoint) {
    }

    @Override
    protected void abortClient(MyCommunicationClient client) {
    }
}
```

Por fim, um processador de excepções é responsável por determinar que tootake ação quando ocorre uma exceção. Exceções são categorizadas em **repetição** e **sem repetição**.

* **Sem repetição** exceções simplesmente obterem novamente iniciadas back toohello autor da chamada.
* **repetição** exceções mais são categorizadas em **transitório** e **não transitório**.
  * **Transitório** exceções são aqueles que pode ser repetida simplesmente sem voltar a resolver o endereço de ponto final do serviço Olá. Estes irão incluir problemas de rede transitórios ou respostas de erro do serviço além das que indicam o endereço de ponto final de serviço Olá não existe.
  * **Não transitório** exceções são aqueles que necessitam de Olá serviço endpoint endereço toobe novamente resolvido. Estas incluem as exceções que indicam o ponto final de serviço Olá não está acessível, que indica que o serviço de Olá moveu tooa outro nó.

Olá `TryHandleException` faz uma decisão sobre uma determinado exceção. Se este **não souber** toomake as decisões sobre uma exceção, deverá devolver **falso**. Se este **saber** toomake que decisão, deve definir o resultado de Olá em conformidade e devolver **verdadeiro**.

```csharp
class MyExceptionHandler : IExceptionHandler
{
    public bool TryHandleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings, out ExceptionHandlingResult result)
    {
        // if exceptionInformation.Exception is known and is transient (can be retried without re-resolving)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, true, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;


        // if exceptionInformation.Exception is known and is not transient (indicates a new service endpoint address must be resolved)
        result = new ExceptionHandlingRetryResult(exceptionInformation.Exception, false, retrySettings, retrySettings.DefaultMaxRetryCount);
        return true;

        // if exceptionInformation.Exception is unknown (let hello next IExceptionHandler attempt toohandle it)
        result = null;
        return false;
    }
}
```
```java
public class MyExceptionHandler implements ExceptionHandler {

    @Override
    public ExceptionHandlingResult handleException(ExceptionInformation exceptionInformation, OperationRetrySettings retrySettings) {        

        /* if exceptionInformation.getException() is known and is transient (can be retried without re-resolving)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), true, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;


        /* if exceptionInformation.getException() is known and is not transient (indicates a new service endpoint address must be resolved)
         */
        result = new ExceptionHandlingRetryResult(exceptionInformation.getException(), false, retrySettings, retrySettings.getDefaultMaxRetryCount());
        return true;

        /* if exceptionInformation.getException() is unknown (let hello next ExceptionHandler attempt toohandle it)
         */
        result = null;
        return false;

    }
}
```
### <a name="putting-it-all-together"></a>Passar todos os em conjunto
Com um `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` construído em torno de um protocolo de comunicação, um `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsula-lo num wrapper tudo em conjunto e fornece processamento de falhas Olá e ciclo resolução de endereço de partição do serviço em torno estes componentes.

```csharp
private MyCommunicationClientFactory myCommunicationClientFactory;
private Uri myServiceUri;

var myServicePartitionClient = new ServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

var result = await myServicePartitionClient.InvokeWithRetryAsync(async (client) =>
   {
      // Communicate with hello service using hello client.
   },
   CancellationToken.None);

```
```java
private MyCommunicationClientFactory myCommunicationClientFactory;
private URI myServiceUri;

FabricServicePartitionClient myServicePartitionClient = new FabricServicePartitionClient<MyCommunicationClient>(
    this.myCommunicationClientFactory,
    this.myServiceUri,
    myPartitionKey);

CompletableFuture<?> result = myServicePartitionClient.invokeWithRetryAsync(client -> {
      /* Communicate with hello service using hello client.
       */
   });

```

## <a name="next-steps"></a>Passos seguintes
* Ver um exemplo de comunicação HTTP entre serviços num [c# projeto de exemplo no GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou [projeto de exemplo de Java no GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).
* [Chamadas de procedimento remoto com o sistema de interação remota Reliable Services](service-fabric-reliable-services-communication-remoting.md)
* [API Web que utiliza OWIN no Reliable Services](service-fabric-reliable-services-communication-webapi.md)
* [Comunicação de WCF utilizando Reliable Services](service-fabric-reliable-services-communication-wcf.md)
