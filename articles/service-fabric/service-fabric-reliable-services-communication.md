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
# <a name="how-toouse-hello-reliable-services-communication-apis"></a><span data-ttu-id="0e224-103">Como toouse Olá comunicação Reliable Services APIs</span><span class="sxs-lookup"><span data-stu-id="0e224-103">How toouse hello Reliable Services communication APIs</span></span>
<span data-ttu-id="0e224-104">Azure Service Fabric, como uma plataforma é completamente agnóstico relativamente sobre a comunicação entre os serviços.</span><span class="sxs-lookup"><span data-stu-id="0e224-104">Azure Service Fabric as a platform is completely agnostic about communication between services.</span></span> <span data-ttu-id="0e224-105">Todas as pilhas e protocolos são aceitáveis, de UDP tooHTTP.</span><span class="sxs-lookup"><span data-stu-id="0e224-105">All protocols and stacks are acceptable, from UDP tooHTTP.</span></span> <span data-ttu-id="0e224-106">Está a funcionar toohello serviço Programador toochoose como serviços devem comunicar.</span><span class="sxs-lookup"><span data-stu-id="0e224-106">It's up toohello service developer toochoose how services should communicate.</span></span> <span data-ttu-id="0e224-107">estrutura da aplicação Olá Reliable Services fornece comunicação incorporada às pilhas, bem como as APIs que pode utilizar toobuild os componentes de comunicação personalizado.</span><span class="sxs-lookup"><span data-stu-id="0e224-107">hello Reliable Services application framework provides built-in communication stacks as well as APIs that you can use toobuild your custom communication components.</span></span>

## <a name="set-up-service-communication"></a><span data-ttu-id="0e224-108">Configurar a comunicação de serviço</span><span class="sxs-lookup"><span data-stu-id="0e224-108">Set up service communication</span></span>
<span data-ttu-id="0e224-109">Olá fiável de serviços de API utiliza uma interface simples para comunicação de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e224-109">hello Reliable Services API uses a simple interface for service communication.</span></span> <span data-ttu-id="0e224-110">tooopen um ponto final para o seu serviço, basta implemente esta interface:</span><span class="sxs-lookup"><span data-stu-id="0e224-110">tooopen an endpoint for your service, simply implement this interface:</span></span>

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

<span data-ttu-id="0e224-111">Em seguida, pode adicionar a implementação de serviço de escuta de comunicação ao devolver uma substituição de método de classe com base no serviço.</span><span class="sxs-lookup"><span data-stu-id="0e224-111">You can then add your communication listener implementation by returning it in a service-based class method override.</span></span>

<span data-ttu-id="0e224-112">Para serviços sem monitorização de estado:</span><span class="sxs-lookup"><span data-stu-id="0e224-112">For stateless services:</span></span>

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

<span data-ttu-id="0e224-113">Para os serviços com monitorização de estado:</span><span class="sxs-lookup"><span data-stu-id="0e224-113">For stateful services:</span></span>

> [!NOTE]
> <span data-ttu-id="0e224-114">Serviços fiáveis com monitorização de estado não são suportados ainda em Java.</span><span class="sxs-lookup"><span data-stu-id="0e224-114">Stateful reliable services are not supported in Java yet.</span></span>
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

<span data-ttu-id="0e224-115">Em ambos os casos, tem de devolver uma coleção de serviços de escuta.</span><span class="sxs-lookup"><span data-stu-id="0e224-115">In both cases, you return a collection of listeners.</span></span> <span data-ttu-id="0e224-116">Isto permite que o serviço toolisten no múltiplos pontos finais, potencialmente com protocolos diferentes, utilizando vários serviços de escuta.</span><span class="sxs-lookup"><span data-stu-id="0e224-116">This allows your service toolisten on multiple endpoints, potentially using different protocols, by using multiple listeners.</span></span> <span data-ttu-id="0e224-117">Por exemplo, pode ter um serviço de escuta HTTP e um serviço de escuta de WebSocket separado.</span><span class="sxs-lookup"><span data-stu-id="0e224-117">For example, you may have an HTTP listener and a separate WebSocket listener.</span></span> <span data-ttu-id="0e224-118">Cada serviço de escuta obtém um nome e a coleção de resultante Olá de *name: endereço* pares são representados como um objeto JSON quando um cliente solicita endereços de escuta de Olá para uma instância de serviço ou uma partição.</span><span class="sxs-lookup"><span data-stu-id="0e224-118">Each listener gets a name, and hello resulting collection of *name : address* pairs are represented as a JSON object when a client requests hello listening addresses for a service instance or a partition.</span></span>

<span data-ttu-id="0e224-119">Um serviço sem monitorização de estado, substituição Olá devolve uma coleção de ServiceInstanceListeners.</span><span class="sxs-lookup"><span data-stu-id="0e224-119">In a stateless service, hello override returns a collection of ServiceInstanceListeners.</span></span> <span data-ttu-id="0e224-120">A `ServiceInstanceListener` contém uma função toocreate um `ICommunicationListener(C#) / CommunicationListener(Java)` e concede-lhe um nome.</span><span class="sxs-lookup"><span data-stu-id="0e224-120">A `ServiceInstanceListener` contains a function toocreate an `ICommunicationListener(C#) / CommunicationListener(Java)` and gives it a name.</span></span> <span data-ttu-id="0e224-121">Para os serviços com monitorização de estado, a substituição de Olá devolve uma coleção de ServiceReplicaListeners.</span><span class="sxs-lookup"><span data-stu-id="0e224-121">For stateful services, hello override returns a collection of ServiceReplicaListeners.</span></span> <span data-ttu-id="0e224-122">Isto é ligeiramente diferente do respetivo homólogo sem monitorização de estado, porque um `ServiceReplicaListener` tem uma opção tooopen um `ICommunicationListener` nas réplicas secundárias.</span><span class="sxs-lookup"><span data-stu-id="0e224-122">This is slightly different from its stateless counterpart, because a `ServiceReplicaListener` has an option tooopen an `ICommunicationListener` on secondary replicas.</span></span> <span data-ttu-id="0e224-123">Não só pode utilizar vários serviços de escuta de comunicação num serviço, mas também pode especificar que os serviços de escuta que aceitam pedidos em réplicas secundárias e aqueles escutarem apenas em réplicas primárias.</span><span class="sxs-lookup"><span data-stu-id="0e224-123">Not only can you use multiple communication listeners in a service, but you can also specify which listeners accept requests on secondary replicas and which ones listen only on primary replicas.</span></span>

<span data-ttu-id="0e224-124">Por exemplo, pode ter um ServiceRemotingListener que aceita chamadas RPC apenas em réplicas primárias e uma escuta segundo, personalizada que demora leitura pedidos nas réplicas secundárias através de HTTP:</span><span class="sxs-lookup"><span data-stu-id="0e224-124">For example, you can have a ServiceRemotingListener that takes RPC calls only on primary replicas, and a second, custom listener that takes read requests on secondary replicas over HTTP:</span></span>

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
> <span data-ttu-id="0e224-125">Ao criar vários serviços de escuta para um serviço, cada serviço de escuta **tem** ser fornecido um nome exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0e224-125">When creating multiple listeners for a service, each listener **must** be given a unique name.</span></span>
>
>

<span data-ttu-id="0e224-126">Por fim, descrevem pontos finais de Olá que são necessários para o serviço de Olá no Olá [manifesto serviço](service-fabric-application-model.md) na secção de Olá em pontos finais.</span><span class="sxs-lookup"><span data-stu-id="0e224-126">Finally, describe hello endpoints that are required for hello service in hello [service manifest](service-fabric-application-model.md) under hello section on endpoints.</span></span>

```xml
<Resources>
    <Endpoints>
      <Endpoint Name="WebServiceEndpoint" Protocol="http" Port="80" />
      <Endpoint Name="OtherServiceEndpoint" Protocol="tcp" Port="8505" />
    <Endpoints>
</Resources>

```

<span data-ttu-id="0e224-127">o serviço de escuta do Olá comunicação pode aceder a recursos de ponto final de Olá alocados tooit dos Olá `CodePackageActivationContext` no Olá `ServiceContext`.</span><span class="sxs-lookup"><span data-stu-id="0e224-127">hello communication listener can access hello endpoint resources allocated tooit from hello `CodePackageActivationContext` in hello `ServiceContext`.</span></span> <span data-ttu-id="0e224-128">serviço de escuta de Olá, em seguida, pode começar a escutar para pedidos quando for aberta.</span><span class="sxs-lookup"><span data-stu-id="0e224-128">hello listener can then start listening for requests when it is opened.</span></span>

```csharp
var codePackageActivationContext = serviceContext.CodePackageActivationContext;
var port = codePackageActivationContext.GetEndpoint("ServiceEndpoint").Port;

```
```java
CodePackageActivationContext codePackageActivationContext = serviceContext.getCodePackageActivationContext();
int port = codePackageActivationContext.getEndpoint("ServiceEndpoint").getPort();

```

> [!NOTE]
> <span data-ttu-id="0e224-129">Recursos de ponto final são o pacote de todo o serviço de toohello comuns e são atribuídos pelo Service Fabric quando o pacote de serviço Olá está ativado.</span><span class="sxs-lookup"><span data-stu-id="0e224-129">Endpoint resources are common toohello entire service package, and they are allocated by Service Fabric when hello service package is activated.</span></span> <span data-ttu-id="0e224-130">Várias réplicas de serviço alojadas no Olá pode partilhar o mesmo ServiceHost Olá mesma porta.</span><span class="sxs-lookup"><span data-stu-id="0e224-130">Multiple service replicas hosted in hello same ServiceHost may share hello same port.</span></span> <span data-ttu-id="0e224-131">Isto significa que o serviço de escuta de comunicação que Olá deve suportar a partilha de portas.</span><span class="sxs-lookup"><span data-stu-id="0e224-131">This means that hello communication listener should support port sharing.</span></span> <span data-ttu-id="0e224-132">Olá recomendada a forma de fazê-lo é Olá comunicação serviço de escuta toouse Olá partição ID e o ID de réplica/instância quando é gerado o endereço de escuta de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e224-132">hello recommended way of doing this is for hello communication listener toouse hello partition ID and replica/instance ID when it generates hello listen address.</span></span>
>
>

### <a name="service-address-registration"></a><span data-ttu-id="0e224-133">Registo de endereço do serviço</span><span class="sxs-lookup"><span data-stu-id="0e224-133">Service address registration</span></span>
<span data-ttu-id="0e224-134">Um serviço de sistema chamado Olá *Naming Service* é executado em clusters de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="0e224-134">A system service called hello *Naming Service* runs on Service Fabric clusters.</span></span> <span data-ttu-id="0e224-135">Olá Naming Service é uma entidade de registo para serviços e os respetivos endereços que cada instância ou a réplica do serviço de Olá está a escutar.</span><span class="sxs-lookup"><span data-stu-id="0e224-135">hello Naming Service is a registrar for services and their addresses that each instance or replica of hello service is listening on.</span></span> <span data-ttu-id="0e224-136">Quando Olá `OpenAsync(C#) / openAsync(Java)` método de um `ICommunicationListener(C#) / CommunicationListener(Java)` estiver concluída, o retorno valor obtém registado no Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="0e224-136">When hello `OpenAsync(C#) / openAsync(Java)` method of an `ICommunicationListener(C#) / CommunicationListener(Java)` completes, its return value gets registered in hello Naming Service.</span></span> <span data-ttu-id="0e224-137">Isto devolver o valor que obtém Olá publicado no Naming Service é uma cadeia cujo valor pode ser qualquer coisa de todo.</span><span class="sxs-lookup"><span data-stu-id="0e224-137">This return value that gets published in hello Naming Service is a string whose value can be anything at all.</span></span> <span data-ttu-id="0e224-138">Este valor de cadeia é clientes veem quando pedem para um endereço do serviço Olá Olá Naming Service.</span><span class="sxs-lookup"><span data-stu-id="0e224-138">This string value is what clients see when they ask for an address for hello service from hello Naming Service.</span></span>

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

<span data-ttu-id="0e224-139">O Service Fabric fornece APIs que permitem que os clientes e outro serviços toothen peça para este endereço de por nome de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e224-139">Service Fabric provides APIs that allow clients and other services toothen ask for this address by service name.</span></span> <span data-ttu-id="0e224-140">Isto é importante porque o endereço do serviço Olá não é estático.</span><span class="sxs-lookup"><span data-stu-id="0e224-140">This is important because hello service address is not static.</span></span> <span data-ttu-id="0e224-141">Os serviços são movidos em torno num cluster de Olá para fins de balanceamento e disponibilidade de recursos.</span><span class="sxs-lookup"><span data-stu-id="0e224-141">Services are moved around in hello cluster for resource balancing and availability purposes.</span></span> <span data-ttu-id="0e224-142">Este é o mecanismo de Olá que permitem aos clientes Olá tooresolve endereço para um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="0e224-142">This is hello mechanism that allow clients tooresolve hello listening address for a service.</span></span>

> [!NOTE]
> <span data-ttu-id="0e224-143">Para uma passagem concluída de forma toowrite um serviço de escuta de comunicação, consulte o artigo [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md) para c#, enquanto que para Java pode escrever a sua própria implementação do servidor de HTTP, consulte o artigo EchoServer aplicação exemplo ao https://github.com/Azure-Samples/service-fabric-java-getting-started.</span><span class="sxs-lookup"><span data-stu-id="0e224-143">For a complete walk-through of how toowrite a communication listener, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md) for C#, whereas for Java you can write your own HTTP server implementation, see EchoServer application example at https://github.com/Azure-Samples/service-fabric-java-getting-started.</span></span>
>
>

## <a name="communicating-with-a-service"></a><span data-ttu-id="0e224-144">Ao comunicar com um serviço</span><span class="sxs-lookup"><span data-stu-id="0e224-144">Communicating with a service</span></span>
<span data-ttu-id="0e224-145">Olá fiável de serviços de API fornece Olá seguintes de clientes de toowrite de bibliotecas que comunicam com os serviços.</span><span class="sxs-lookup"><span data-stu-id="0e224-145">hello Reliable Services API provides hello following libraries toowrite clients that communicate with services.</span></span>

### <a name="service-endpoint-resolution"></a><span data-ttu-id="0e224-146">Resolução de ponto final de serviço</span><span class="sxs-lookup"><span data-stu-id="0e224-146">Service endpoint resolution</span></span>
<span data-ttu-id="0e224-147">primeiro passo toocommunication Olá com um serviço é tooresolve um endereço de ponto final de partição Olá ou instância de serviço Olá que pretende tootalk para.</span><span class="sxs-lookup"><span data-stu-id="0e224-147">hello first step toocommunication with a service is tooresolve an endpoint address of hello partition or instance of hello service you want tootalk to.</span></span> <span data-ttu-id="0e224-148">Olá `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` classe de utilitário é um primitivo básico que ajuda os clientes determinam Olá ponto final de um serviço em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0e224-148">hello `ServicePartitionResolver(C#) / FabricServicePartitionResolver(Java)` utility class is a basic primitive that helps clients determine hello endpoint of a service at runtime.</span></span> <span data-ttu-id="0e224-149">Na terminologia de Service Fabric, o processo de Olá de determinar Olá ponto final de um serviço é referenciado tooas Olá *resolução de ponto final de serviço*.</span><span class="sxs-lookup"><span data-stu-id="0e224-149">In Service Fabric terminology, hello process of determining hello endpoint of a service is referred tooas hello *service endpoint resolution*.</span></span>

<span data-ttu-id="0e224-150">tooconnect tooservices dentro de um cluster, ServicePartitionResolver pode ser criada através das predefinições.</span><span class="sxs-lookup"><span data-stu-id="0e224-150">tooconnect tooservices within a cluster, ServicePartitionResolver can be created using default settings.</span></span> <span data-ttu-id="0e224-151">Este é Olá recomendado a utilização da maioria das situações:</span><span class="sxs-lookup"><span data-stu-id="0e224-151">This is hello recommended usage for most situations:</span></span>

```csharp
ServicePartitionResolver resolver = ServicePartitionResolver.GetDefault();
```
```java
FabricServicePartitionResolver resolver = FabricServicePartitionResolver.getDefault();
```

<span data-ttu-id="0e224-152">tooconnect tooservices num cluster diferente, um ServicePartitionResolver pode ser criada com um conjunto de pontos finais de gateway do cluster.</span><span class="sxs-lookup"><span data-stu-id="0e224-152">tooconnect tooservices in a different cluster, a ServicePartitionResolver can be created with a set of cluster gateway endpoints.</span></span> <span data-ttu-id="0e224-153">Tenha em atenção que os pontos finais de gateway são apenas diferentes pontos finais para ligar toohello mesmo cluster.</span><span class="sxs-lookup"><span data-stu-id="0e224-153">Note that gateway endpoints are just different endpoints for connecting toohello same cluster.</span></span> <span data-ttu-id="0e224-154">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0e224-154">For example:</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver("mycluster.cloudapp.azure.com:19000", "mycluster.cloudapp.azure.com:19001");
```

<span data-ttu-id="0e224-155">Em alternativa, `ServicePartitionResolver` pode ser especificado uma função para a criação de um `FabricClient` toouse internamente:</span><span class="sxs-lookup"><span data-stu-id="0e224-155">Alternatively, `ServicePartitionResolver` can be given a function for creating a `FabricClient` toouse internally:</span></span>

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

<span data-ttu-id="0e224-156">`FabricClient`é um objeto de Olá que é utilizado toocommunicate com o cluster do Service Fabric Olá para várias operações de gestão no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="0e224-156">`FabricClient` is hello object that is used toocommunicate with hello Service Fabric cluster for various management operations on hello cluster.</span></span> <span data-ttu-id="0e224-157">Isto é útil quando pretende mais controlo sobre como uma resolução de partição de serviço interage com o cluster.</span><span class="sxs-lookup"><span data-stu-id="0e224-157">This is useful when you want more control over how a service partition resolver interacts with your cluster.</span></span> <span data-ttu-id="0e224-158">`FabricClient`efetua a colocação em cache internamente e é geralmente dispendiosa toocreate, pelo que é importante tooreuse `FabricClient` instâncias quanto possíveis.</span><span class="sxs-lookup"><span data-stu-id="0e224-158">`FabricClient` performs caching internally and is generally expensive toocreate, so it is important tooreuse `FabricClient` instances as much as possible.</span></span>

```csharp
ServicePartitionResolver resolver = new  ServicePartitionResolver(() => CreateMyFabricClient());
```
```java
FabricServicePartitionResolver resolver = new  FabricServicePartitionResolver(() -> new CreateFabricClientImpl());
```

<span data-ttu-id="0e224-159">Um método de resolução é utilizada tooretrieve Olá endereço de um serviço ou uma partição de serviço para os serviços particionadas.</span><span class="sxs-lookup"><span data-stu-id="0e224-159">A resolve method is then used tooretrieve hello address of a service or a service partition for partitioned services.</span></span>

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

<span data-ttu-id="0e224-160">Um endereço de serviço pode ser resolvido utilizando facilmente um ServicePartitionResolver, mas é necessário o mais trabalho tooensure Olá resolver o endereço pode ser utilizado corretamente.</span><span class="sxs-lookup"><span data-stu-id="0e224-160">A service address can be resolved easily using a ServicePartitionResolver, but more work is required tooensure hello resolved address can be used correctly.</span></span> <span data-ttu-id="0e224-161">O cliente tem toodetect se a tentativa de ligação de Olá falhou devido a um erro transitório e pode ser repetida (por exemplo, serviço movido ou está temporariamente indisponível), ou um erro permanente (por exemplo, serviço foi eliminado ou hello recurso pedido já não existe).</span><span class="sxs-lookup"><span data-stu-id="0e224-161">Your client needs toodetect whether hello connection attempt failed because of a transient error and can be retried (e.g., service moved or is temporarily unavailable), or a permanent error (e.g., service was deleted or hello requested resource no longer exists).</span></span> <span data-ttu-id="0e224-162">Instâncias de serviço ou de réplicas podem mover-se do nó toonode em qualquer altura para por vários motivos.</span><span class="sxs-lookup"><span data-stu-id="0e224-162">Service instances or replicas can move around from node toonode at any time for multiple reasons.</span></span> <span data-ttu-id="0e224-163">endereço de serviço de Olá resolvido através de ServicePartitionResolver poderá estar obsoleto por tempo Olá que o código de cliente tenta tooconnect.</span><span class="sxs-lookup"><span data-stu-id="0e224-163">hello service address resolved through ServicePartitionResolver may be stale by hello time your client code attempts tooconnect.</span></span> <span data-ttu-id="0e224-164">Nesse caso novamente Olá cliente tem de endereço de Olá toore resolve.</span><span class="sxs-lookup"><span data-stu-id="0e224-164">In that case again hello client needs toore-resolve hello address.</span></span> <span data-ttu-id="0e224-165">Fornecer Olá anterior `ResolvedServicePartition` indica que Olá resolução necessidades tootry novamente em vez de apenas obter um endereço em cache.</span><span class="sxs-lookup"><span data-stu-id="0e224-165">Providing hello previous `ResolvedServicePartition` indicates that hello resolver needs tootry again rather than simply retrieve a cached address.</span></span>

<span data-ttu-id="0e224-166">Normalmente, o código de cliente Olá necessário não funciona com Olá ServicePartitionResolver diretamente.</span><span class="sxs-lookup"><span data-stu-id="0e224-166">Typically, hello client code need not work with hello ServicePartitionResolver directly.</span></span> <span data-ttu-id="0e224-167">É criado e transmitido toocommunication fábricas de cliente no Olá fiável de serviços de API.</span><span class="sxs-lookup"><span data-stu-id="0e224-167">It is created and passed on toocommunication client factories in hello Reliable Services API.</span></span> <span data-ttu-id="0e224-168">fábricas de Olá utilizam resolução Olá internamente toogenerate um objeto de cliente que pode ser utilizado toocommunicate com os serviços.</span><span class="sxs-lookup"><span data-stu-id="0e224-168">hello factories use hello resolver internally toogenerate a client object that can be used toocommunicate with services.</span></span>

### <a name="communication-clients-and-factories"></a><span data-ttu-id="0e224-169">Os clientes de comunicação e fábricas de</span><span class="sxs-lookup"><span data-stu-id="0e224-169">Communication clients and factories</span></span>
<span data-ttu-id="0e224-170">biblioteca de fábrica de comunicação de Olá implementa um padrão de repetição de processamento de falhas normal que facilita a repetir ligações tooresolved pontos finais de serviço.</span><span class="sxs-lookup"><span data-stu-id="0e224-170">hello communication factory library implements a typical fault-handling retry pattern that makes retrying connections tooresolved service endpoints easier.</span></span> <span data-ttu-id="0e224-171">biblioteca de fábrica Olá fornece o mecanismo de repetição de Olá enquanto fornecer processadores de erro Olá.</span><span class="sxs-lookup"><span data-stu-id="0e224-171">hello factory library provides hello retry mechanism while you provide hello error handlers.</span></span>

<span data-ttu-id="0e224-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`Define a interface base Olá implementado por uma fábrica do cliente de comunicação que produza os clientes que podem comunicar com o serviço de Service Fabric tooa.</span><span class="sxs-lookup"><span data-stu-id="0e224-172">`ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)` defines hello base interface implemented by a communication client factory that produces clients that can talk tooa Service Fabric service.</span></span> <span data-ttu-id="0e224-173">Olá, implementação de Olá que communicationclientfactory depende da pilha de comunicações de Olá utilizada pelo serviço de Service Fabric olá onde o cliente de Olá pretende toocommunicate.</span><span class="sxs-lookup"><span data-stu-id="0e224-173">hello implementation of hello CommunicationClientFactory depends on hello communication stack used by hello Service Fabric service where hello client wants toocommunicate.</span></span> <span data-ttu-id="0e224-174">Olá fiável de serviços de API fornece um `CommunicationClientFactoryBase<TCommunicationClient>`.</span><span class="sxs-lookup"><span data-stu-id="0e224-174">hello Reliable Services API provides a `CommunicationClientFactoryBase<TCommunicationClient>`.</span></span> <span data-ttu-id="0e224-175">Isto fornece uma implementação da interface de CommunicationClientFactory Olá base e executa tarefas de pilhas de comunicação de Olá tooall comuns.</span><span class="sxs-lookup"><span data-stu-id="0e224-175">This provides a base implementation of hello CommunicationClientFactory interface and performs tasks that are common tooall hello communication stacks.</span></span> <span data-ttu-id="0e224-176">(Estas tarefas incluem a utilização de um ServicePartitionResolver toodetermine Olá ponto final do serviço).</span><span class="sxs-lookup"><span data-stu-id="0e224-176">(These tasks include using a ServicePartitionResolver toodetermine hello service endpoint).</span></span> <span data-ttu-id="0e224-177">Clientes, normalmente, implementam a Olá abstrata CommunicationClientFactoryBase classe toohandle lógica que é a pilha de comunicações toohello específico.</span><span class="sxs-lookup"><span data-stu-id="0e224-177">Clients usually implement hello abstract CommunicationClientFactoryBase class toohandle logic that is specific toohello communication stack.</span></span>

<span data-ttu-id="0e224-178">apenas o cliente de comunicação de Olá recebe um endereço e utiliza-tooconnect tooa serviço.</span><span class="sxs-lookup"><span data-stu-id="0e224-178">hello communication client just receives an address and uses it tooconnect tooa service.</span></span> <span data-ttu-id="0e224-179">cliente de Olá pode utilizar qualquer protocolo que pretende.</span><span class="sxs-lookup"><span data-stu-id="0e224-179">hello client can use whatever protocol it wants.</span></span>

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

<span data-ttu-id="0e224-180">fábrica do cliente Olá é principalmente responsável pela criação de clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="0e224-180">hello client factory is primarily responsible for creating communication clients.</span></span> <span data-ttu-id="0e224-181">Para clientes que não mantêm uma ligação persistente, por exemplo, um cliente HTTP, fábrica Olá só precisa de toocreate e cliente Olá de retorno.</span><span class="sxs-lookup"><span data-stu-id="0e224-181">For clients that don't maintain a persistent connection, such as an HTTP client, hello factory only needs toocreate and return hello client.</span></span> <span data-ttu-id="0e224-182">Outros protocolos que mantêm uma ligação persistente, por exemplo, alguns protocolos binários, também devem ser validados por Olá fábrica toodetermine se precisa de ligação de Olá toobe recriado.</span><span class="sxs-lookup"><span data-stu-id="0e224-182">Other protocols that maintain a persistent connection, such as some binary protocols, should also be validated by hello factory toodetermine whether hello connection needs toobe re-created.</span></span>  

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

<span data-ttu-id="0e224-183">Por fim, um processador de excepções é responsável por determinar que tootake ação quando ocorre uma exceção.</span><span class="sxs-lookup"><span data-stu-id="0e224-183">Finally, an exception handler is responsible for determining what action tootake when an exception occurs.</span></span> <span data-ttu-id="0e224-184">Exceções são categorizadas em **repetição** e **sem repetição**.</span><span class="sxs-lookup"><span data-stu-id="0e224-184">Exceptions are categorized into **retryable** and **non retryable**.</span></span>

* <span data-ttu-id="0e224-185">**Sem repetição** exceções simplesmente obterem novamente iniciadas back toohello autor da chamada.</span><span class="sxs-lookup"><span data-stu-id="0e224-185">**Non retryable** exceptions simply get rethrown back toohello caller.</span></span>
* <span data-ttu-id="0e224-186">**repetição** exceções mais são categorizadas em **transitório** e **não transitório**.</span><span class="sxs-lookup"><span data-stu-id="0e224-186">**retryable** exceptions are further categorized into **transient** and **non-transient**.</span></span>
  * <span data-ttu-id="0e224-187">**Transitório** exceções são aqueles que pode ser repetida simplesmente sem voltar a resolver o endereço de ponto final do serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="0e224-187">**Transient** exceptions are those that can simply be retried without re-resolving hello service endpoint address.</span></span> <span data-ttu-id="0e224-188">Estes irão incluir problemas de rede transitórios ou respostas de erro do serviço além das que indicam o endereço de ponto final de serviço Olá não existe.</span><span class="sxs-lookup"><span data-stu-id="0e224-188">These will include transient network problems or service error responses other than those that indicate hello service endpoint address does not exist.</span></span>
  * <span data-ttu-id="0e224-189">**Não transitório** exceções são aqueles que necessitam de Olá serviço endpoint endereço toobe novamente resolvido.</span><span class="sxs-lookup"><span data-stu-id="0e224-189">**Non-transient** exceptions are those that require hello service endpoint address toobe re-resolved.</span></span> <span data-ttu-id="0e224-190">Estas incluem as exceções que indicam o ponto final de serviço Olá não está acessível, que indica que o serviço de Olá moveu tooa outro nó.</span><span class="sxs-lookup"><span data-stu-id="0e224-190">These include exceptions that indicate hello service endpoint could not be reached, indicating hello service has moved tooa different node.</span></span>

<span data-ttu-id="0e224-191">Olá `TryHandleException` faz uma decisão sobre uma determinado exceção.</span><span class="sxs-lookup"><span data-stu-id="0e224-191">hello `TryHandleException` makes a decision about a given exception.</span></span> <span data-ttu-id="0e224-192">Se este **não souber** toomake as decisões sobre uma exceção, deverá devolver **falso**.</span><span class="sxs-lookup"><span data-stu-id="0e224-192">If it **does not know** what decisions toomake about an exception, it should return **false**.</span></span> <span data-ttu-id="0e224-193">Se este **saber** toomake que decisão, deve definir o resultado de Olá em conformidade e devolver **verdadeiro**.</span><span class="sxs-lookup"><span data-stu-id="0e224-193">If it **does know** what decision toomake, it should set hello result accordingly and return **true**.</span></span>

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
### <a name="putting-it-all-together"></a><span data-ttu-id="0e224-194">Passar todos os em conjunto</span><span class="sxs-lookup"><span data-stu-id="0e224-194">Putting it all together</span></span>
<span data-ttu-id="0e224-195">Com um `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, e `IExceptionHandler(C#) / ExceptionHandler(Java)` construído em torno de um protocolo de comunicação, um `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` encapsula-lo num wrapper tudo em conjunto e fornece processamento de falhas Olá e ciclo resolução de endereço de partição do serviço em torno estes componentes.</span><span class="sxs-lookup"><span data-stu-id="0e224-195">With an `ICommunicationClient(C#) / CommunicationClient(Java)`, `ICommunicationClientFactory(C#) / CommunicationClientFactory(Java)`, and `IExceptionHandler(C#) / ExceptionHandler(Java)` built around a communication protocol, a `ServicePartitionClient(C#) / FabricServicePartitionClient(Java)` wraps it all together and provides hello fault-handling and service partition address resolution loop around these components.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0e224-196">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0e224-196">Next steps</span></span>
* <span data-ttu-id="0e224-197">Ver um exemplo de comunicação HTTP entre serviços num [c# projeto de exemplo no GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) ou [projeto de exemplo de Java no GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span><span class="sxs-lookup"><span data-stu-id="0e224-197">See an example of HTTP communication between services in a [C# sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-dotnet-getting-started/tree/classic/Services/WordCount) or [Java sample project on GitHUb](https://github.com/Azure-Samples/service-fabric-java-getting-started/tree/master/Services/WatchDog).</span></span>
* [<span data-ttu-id="0e224-198">Chamadas de procedimento remoto com o sistema de interação remota Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0e224-198">Remote procedure calls with Reliable Services remoting</span></span>](service-fabric-reliable-services-communication-remoting.md)
* [<span data-ttu-id="0e224-199">API Web que utiliza OWIN no Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0e224-199">Web API that uses OWIN in Reliable Services</span></span>](service-fabric-reliable-services-communication-webapi.md)
* [<span data-ttu-id="0e224-200">Comunicação de WCF utilizando Reliable Services</span><span class="sxs-lookup"><span data-stu-id="0e224-200">WCF communication by using Reliable Services</span></span>](service-fabric-reliable-services-communication-wcf.md)
