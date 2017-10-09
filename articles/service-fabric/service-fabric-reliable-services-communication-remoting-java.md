---
title: "comunicação remota de aaaService no Service Fabric do Azure | Microsoft Docs"
description: "Comunicação remota do Service Fabric permite que os clientes e serviços toocommunicate com serviços através de uma chamada de procedimento remoto."
services: service-fabric
documentationcenter: java
author: PavanKunapareddyMSFT
manager: timlt
ms.assetid: 
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: required
ms.date: 06/30/2017
ms.author: pakunapa
ms.openlocfilehash: 1177a5ede91352dc61422f2df7424b0d5645147d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="service-remoting-with-reliable-services"></a><span data-ttu-id="98b43-103">Comunicação remota do serviço com Reliable Services</span><span class="sxs-lookup"><span data-stu-id="98b43-103">Service remoting with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="98b43-104">C# no Windows</span><span class="sxs-lookup"><span data-stu-id="98b43-104">C# on Windows</span></span>](service-fabric-reliable-services-communication-remoting.md)
> * [<span data-ttu-id="98b43-105">Java em Linux</span><span class="sxs-lookup"><span data-stu-id="98b43-105">Java on Linux</span></span>](service-fabric-reliable-services-communication-remoting-java.md)
>
>

<span data-ttu-id="98b43-106">arquitetura de Reliable Services de Olá fornece um tooquickly de mecanismo de comunicação remota e configurar facilmente a chamada de procedimento remoto para os serviços.</span><span class="sxs-lookup"><span data-stu-id="98b43-106">hello Reliable Services framework provides a remoting mechanism tooquickly and easily set up remote procedure call for services.</span></span>

## <a name="set-up-remoting-on-a-service"></a><span data-ttu-id="98b43-107">Configurar a gestão remota num serviço</span><span class="sxs-lookup"><span data-stu-id="98b43-107">Set up remoting on a service</span></span>
<span data-ttu-id="98b43-108">Configurar a gestão remota para um serviço é efetuada em dois passos simples:</span><span class="sxs-lookup"><span data-stu-id="98b43-108">Setting up remoting for a service is done in two simple steps:</span></span>

1. <span data-ttu-id="98b43-109">Crie uma interface para sua tooimplement de serviço.</span><span class="sxs-lookup"><span data-stu-id="98b43-109">Create an interface for your service tooimplement.</span></span> <span data-ttu-id="98b43-110">Esta interface define os métodos de Olá que estão disponíveis para uma chamada de procedimento remoto do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="98b43-110">This interface defines hello methods that are available for a remote procedure call on your service.</span></span> <span data-ttu-id="98b43-111">tem de ser métodos Olá tarefas métodos assíncronos.</span><span class="sxs-lookup"><span data-stu-id="98b43-111">hello methods must be task-returning asynchronous methods.</span></span> <span data-ttu-id="98b43-112">tem de implementar a interface de Olá `microsoft.serviceFabric.services.remoting.Service` toosignal Olá serviço tem uma interface de gestão remota.</span><span class="sxs-lookup"><span data-stu-id="98b43-112">hello interface must implement `microsoft.serviceFabric.services.remoting.Service` toosignal that hello service has a remoting interface.</span></span>
2. <span data-ttu-id="98b43-113">Utilize um serviço de escuta de comunicação remota no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="98b43-113">Use a remoting listener in your service.</span></span> <span data-ttu-id="98b43-114">Este é um `CommunicationListener` implementação que oferece funções de sistema de interação remota.</span><span class="sxs-lookup"><span data-stu-id="98b43-114">This is an `CommunicationListener` implementation that provides remoting capabilities.</span></span> <span data-ttu-id="98b43-115">`FabricTransportServiceRemotingListener`pode ser utilizado toocreate um serviço de escuta da gestão remota utilizando o protocolo de transporte de comunicação remota do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="98b43-115">`FabricTransportServiceRemotingListener` can be used toocreate a remoting listener using hello default remoting transport protocol.</span></span>

<span data-ttu-id="98b43-116">Por exemplo, hello seguinte serviço sem estado expõe um único método tooget "Olá mundo" através de uma chamada de procedimento remoto.</span><span class="sxs-lookup"><span data-stu-id="98b43-116">For example, hello following stateless service exposes a single method tooget "Hello World" over a remote procedure call.</span></span>

```java
import java.util.ArrayList;
import java.util.concurrent.CompletableFuture;
import java.util.List;
import microsoft.servicefabric.services.communication.runtime.ServiceInstanceListener;
import microsoft.servicefabric.services.remoting.Service;
import microsoft.servicefabric.services.runtime.StatelessService;

public interface MyService extends Service {
    CompletableFuture<String> helloWorldAsync();
}

class MyServiceImpl extends StatelessService implements MyService {
    public MyServiceImpl(StatelessServiceContext context) {
       super(context);
    }

    public CompletableFuture<String> helloWorldAsync() {
        return CompletableFuture.completedFuture("Hello!");
    }

    @Override
    protected List<ServiceInstanceListener> createServiceInstanceListeners() {
        ArrayList<ServiceInstanceListener> listeners = new ArrayList<>();
        listeners.add(new ServiceInstanceListener((context) -> {
            return new FabricTransportServiceRemotingListener(context,this);
        }));
        return listeners;
    }
}
```

> [!NOTE]
> <span data-ttu-id="98b43-117">argumentos Olá e Olá devolvem tipos na interface de serviço Olá podem ser qualquer tipos personalizados, simples ou complexos, mas tem de ser serializáveis.</span><span class="sxs-lookup"><span data-stu-id="98b43-117">hello arguments and hello return types in hello service interface can be any simple, complex, or custom types, but they must be serializable.</span></span>
>
>

## <a name="call-remote-service-methods"></a><span data-ttu-id="98b43-118">Chamar os métodos de serviço remoto</span><span class="sxs-lookup"><span data-stu-id="98b43-118">Call remote service methods</span></span>
<span data-ttu-id="98b43-119">Chamar os métodos num serviço utilizando a pilha de comunicação remota de Olá é feito utilizando um serviço de toohello local proxy através de Olá `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` classe.</span><span class="sxs-lookup"><span data-stu-id="98b43-119">Calling methods on a service by using hello remoting stack is done by using a local proxy toohello service through hello `microsoft.serviceFabric.services.remoting.client.ServiceProxyBase` class.</span></span> <span data-ttu-id="98b43-120">Olá `ServiceProxyBase` método cria um proxy local utilizando Olá a mesma interface Olá service implementa.</span><span class="sxs-lookup"><span data-stu-id="98b43-120">hello `ServiceProxyBase` method creates a local proxy by using hello same interface that hello service implements.</span></span> <span data-ttu-id="98b43-121">Com esse proxy, pode chamar simplesmente métodos na interface de Olá remotamente.</span><span class="sxs-lookup"><span data-stu-id="98b43-121">With that proxy, you can simply call methods on hello interface remotely.</span></span>

```java

MyService helloWorldClient = ServiceProxyBase.create(MyService.class, new URI("fabric:/MyApplication/MyHelloWorldService"));

CompletableFuture<String> message = helloWorldClient.helloWorldAsync();

```

<span data-ttu-id="98b43-122">arquitetura de sistema de interação remota Olá propaga exceções acionadas no cliente do serviço do Olá toohello.</span><span class="sxs-lookup"><span data-stu-id="98b43-122">hello remoting framework propagates exceptions thrown at hello service toohello client.</span></span> <span data-ttu-id="98b43-123">Lógica de processamento de exceções, por isso, cliente Olá utilizando `ServiceProxyBase` diretamente pode processar exceções Olá gera de serviço.</span><span class="sxs-lookup"><span data-stu-id="98b43-123">So exception-handling logic at hello client by using `ServiceProxyBase` can directly handle exceptions that hello service throws.</span></span>

## <a name="service-proxy-lifetime"></a><span data-ttu-id="98b43-124">Duração do Proxy de serviço</span><span class="sxs-lookup"><span data-stu-id="98b43-124">Service Proxy Lifetime</span></span>
<span data-ttu-id="98b43-125">Criação de ServiceProxy é uma operação simples, para que o utilizador pode criar tantas como precisarem.</span><span class="sxs-lookup"><span data-stu-id="98b43-125">ServiceProxy creation is a lightweight operation, so user can create as many as they need it.</span></span> <span data-ttu-id="98b43-126">Proxy de serviço pode ser reutilizado desde que o utilizador precisar dele.</span><span class="sxs-lookup"><span data-stu-id="98b43-126">Service Proxy can be re-used as long as user need it.</span></span> <span data-ttu-id="98b43-127">Utilizador pode utilizar novamente Olá proxy mesmo em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="98b43-127">User can re-use hello same proxy in case of Exception.</span></span> <span data-ttu-id="98b43-128">Cada ServiceProxy contém comunicação cliente utilizado toosend mensagens através de transmissão de Olá.</span><span class="sxs-lookup"><span data-stu-id="98b43-128">Each ServiceProxy contains communication client used toosend messages over hello wire.</span></span> <span data-ttu-id="98b43-129">Ao invocar a API, temos toosee verificação interno se o cliente de comunicação utilizada é válido.</span><span class="sxs-lookup"><span data-stu-id="98b43-129">While invoking API, we have internal check toosee if communication client used is valid.</span></span> <span data-ttu-id="98b43-130">Com base no que resultam, vamos voltar crie Olá comunicação do cliente.</span><span class="sxs-lookup"><span data-stu-id="98b43-130">Based on that result, we re-create hello communication client.</span></span> <span data-ttu-id="98b43-131">Por conseguinte, o utilizador não é necessário toorecreate serviceproxy em caso de exceção.</span><span class="sxs-lookup"><span data-stu-id="98b43-131">Hence user do not need toorecreate serviceproxy in case of Exception.</span></span>

### <a name="serviceproxyfactory-lifetime"></a><span data-ttu-id="98b43-132">Duração de ServiceProxyFactory</span><span class="sxs-lookup"><span data-stu-id="98b43-132">ServiceProxyFactory Lifetime</span></span>
<span data-ttu-id="98b43-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) é uma fábrica de que cria o proxy para interfaces de comunicação remota diferente.</span><span class="sxs-lookup"><span data-stu-id="98b43-133">[FabricServiceProxyFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._fabric_service_proxy_factory) is a factory that creates proxy for different remoting interfaces.</span></span> <span data-ttu-id="98b43-134">Se utilizar a API `ServiceProxyBase.create` para criar o proxy, em seguida, framework cria um `FabricServiceProxyFactory`.</span><span class="sxs-lookup"><span data-stu-id="98b43-134">If you use API `ServiceProxyBase.create` for creating proxy, then framework creates a `FabricServiceProxyFactory`.</span></span>
<span data-ttu-id="98b43-135">É útil toocreate um manualmente quando precisar de toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) propriedades.</span><span class="sxs-lookup"><span data-stu-id="98b43-135">It is useful toocreate one manually when you need toooverride [ServiceRemotingClientFactory](https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.remoting.client._service_remoting_client_factory) properties.</span></span>
<span data-ttu-id="98b43-136">Fábrica é uma operação dispendiosa.</span><span class="sxs-lookup"><span data-stu-id="98b43-136">Factory is an expensive operation.</span></span> <span data-ttu-id="98b43-137">`FabricServiceProxyFactory`mantém a cache de clientes de comunicação.</span><span class="sxs-lookup"><span data-stu-id="98b43-137">`FabricServiceProxyFactory` maintains cache of communication clients.</span></span>
<span data-ttu-id="98b43-138">Melhor prática é toocache `FabricServiceProxyFactory` há tempo quanto possível.</span><span class="sxs-lookup"><span data-stu-id="98b43-138">Best practice is toocache `FabricServiceProxyFactory` for as long as possible.</span></span>

## <a name="remoting-exception-handling"></a><span data-ttu-id="98b43-139">Processamento de exceções de comunicação remota</span><span class="sxs-lookup"><span data-stu-id="98b43-139">Remoting Exception Handling</span></span>
<span data-ttu-id="98b43-140">Todos os Olá remoto Ocorreu uma excepção ao serviço API, são enviadas como RuntimeException ou FabricException toohello back-cliente.</span><span class="sxs-lookup"><span data-stu-id="98b43-140">All hello remote exception thrown by service API, are sent back toohello client either as RuntimeException or FabricException.</span></span>

<span data-ttu-id="98b43-141">ServiceProxy processar todas as exceções de ativação pós-falha para a partição de serviço Olá é criado para.</span><span class="sxs-lookup"><span data-stu-id="98b43-141">ServiceProxy does handle all Failover Exception for hello service partition it  is created for.</span></span> <span data-ttu-id="98b43-142">Resolve novamente pontos finais de Olá se houver Exceptions(Non-Transient Exceptions) ativação pós-falha e repete chamada Olá com o ponto final do Olá correto.</span><span class="sxs-lookup"><span data-stu-id="98b43-142">It re-resolves hello endpoints if there is Failover Exceptions(Non-Transient Exceptions) and retries hello call with hello correct endpoint.</span></span> <span data-ttu-id="98b43-143">Número de tentativas de ativação pós-falha exceção é indefinido.</span><span class="sxs-lookup"><span data-stu-id="98b43-143">Number of retries for failover Exception is indefinite.</span></span>
<span data-ttu-id="98b43-144">Em caso de TransientExceptions, apenas de voltar a chamada de Olá.</span><span class="sxs-lookup"><span data-stu-id="98b43-144">In case of TransientExceptions, it only retries hello call.</span></span>

<span data-ttu-id="98b43-145">Os parâmetros predefinidos de repetição são fornecidos por [OperationRetrySettings].</span><span class="sxs-lookup"><span data-stu-id="98b43-145">Default retry parameters are provied by [OperationRetrySettings].</span></span> <span data-ttu-id="98b43-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) Utilizador pode configurar estes valores através da transmissão de construtor de tooServiceProxyFactory OperationRetrySettings objeto.</span><span class="sxs-lookup"><span data-stu-id="98b43-146">(https://docs.microsoft.com/en-us/java/api/microsoft.servicefabric.services.communication.client._operation_retry_settings) User can configure these values by passing OperationRetrySettings object tooServiceProxyFactory constructor.</span></span>

## <a name="next-steps"></a><span data-ttu-id="98b43-147">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="98b43-147">Next steps</span></span>
* [<span data-ttu-id="98b43-148">Proteger a comunicação para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="98b43-148">Securing communication for Reliable Services</span></span>](service-fabric-reliable-services-secure-communication.md)
