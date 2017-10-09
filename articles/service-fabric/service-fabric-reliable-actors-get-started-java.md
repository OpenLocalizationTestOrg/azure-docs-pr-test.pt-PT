---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em Java | Microsoft Docs"
description: "Este tutorial orienta-o pelos passos de Olá da criação, depurar e implementar um serviço baseado em ator simple utilizando o serviço de recursos de infraestrutura Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d31dc8ab-9760-4619-a641-facb8324c759
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 01/04/2017
ms.author: vturecek
ms.openlocfilehash: 24718a8d7034360c53597f139169580f1a6ce732
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="7b444-103">Introdução a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="7b444-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="7b444-104">C# no Windows</span><span class="sxs-lookup"><span data-stu-id="7b444-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="7b444-105">Java em Linux</span><span class="sxs-lookup"><span data-stu-id="7b444-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="7b444-106">Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Actors e explica-lhe como criar e implementar uma aplicação simples de Ator fiável em Java.</span><span class="sxs-lookup"><span data-stu-id="7b444-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating and deploying a simple Reliable Actor application in Java.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="7b444-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="7b444-107">Installation and setup</span></span>
<span data-ttu-id="7b444-108">Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="7b444-108">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="7b444-109">Se precisar de tooset-lo, aceda demasiado[introdução no Mac](service-fabric-get-started-mac.md) ou [introdução no Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7b444-109">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="7b444-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="7b444-110">Basic concepts</span></span>
<span data-ttu-id="7b444-111">tooget começar Reliable Actors, apenas é necessário toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="7b444-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="7b444-112">**Serviço de atores**.</span><span class="sxs-lookup"><span data-stu-id="7b444-112">**Actor service**.</span></span> <span data-ttu-id="7b444-113">Reliable Actors são reunidas em Reliable Services que podem ser implementados numa infraestrutura de Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="7b444-114">Instâncias de ator são ativadas numa instância de serviço com nome.</span><span class="sxs-lookup"><span data-stu-id="7b444-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="7b444-115">**Registo de ator**.</span><span class="sxs-lookup"><span data-stu-id="7b444-115">**Actor registration**.</span></span> <span data-ttu-id="7b444-116">Como com Reliable Services, um serviço de Atores fiável tem toobe registado com o tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b444-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="7b444-117">Além disso, o tipo de ator Olá deve toobe registado com o tempo de execução do Olá Ator.</span><span class="sxs-lookup"><span data-stu-id="7b444-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="7b444-118">**Interface de ator**.</span><span class="sxs-lookup"><span data-stu-id="7b444-118">**Actor interface**.</span></span> <span data-ttu-id="7b444-119">interface de ator Olá é utilizado toodefine uma interface pública com tipo seguro de um ator.</span><span class="sxs-lookup"><span data-stu-id="7b444-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="7b444-120">Na terminologia de modelo de Ator fiável Olá, a interface de ator Olá define Olá tipos de mensagens hello ator podem compreender e processar.</span><span class="sxs-lookup"><span data-stu-id="7b444-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="7b444-121">interface de ator Olá é utilizado por outros atores e aplicações cliente demasiado "de envio" (no modo assíncrono) ator toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="7b444-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="7b444-122">Reliable Actors podem implementar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="7b444-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="7b444-123">**Classe de ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="7b444-123">**ActorProxy class**.</span></span> <span data-ttu-id="7b444-124">Olá ActorProxy classe é utilizada pelo cliente aplicações tooinvoke Olá métodos expostos através da interface de ator Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="7b444-125">Olá ActorProxy classe fornece duas funcionalidades importantes:</span><span class="sxs-lookup"><span data-stu-id="7b444-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="7b444-126">Resolução de nomes: é capaz de toolocate actor de Olá num cluster de Olá (localizar Olá nó de cluster olá onde está alojado).</span><span class="sxs-lookup"><span data-stu-id="7b444-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="7b444-127">Processamento de falhas: pode repetir invocações de método e novamente resolver a localização de atores de Olá depois, por exemplo, uma falha de que necessita de Olá ator toobe relocalizada tooanother de nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="7b444-128">Olá seguintes regras que dizem respeito tooactor interfaces é mencionar:</span><span class="sxs-lookup"><span data-stu-id="7b444-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="7b444-129">Métodos de interface de ator não podem estar sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="7b444-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="7b444-130">Interface de ator métodos não pode ter out, ref ou parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="7b444-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="7b444-131">Interfaces genéricas não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="7b444-131">Generic interfaces are not supported.</span></span>

## <a name="create-an-actor-service"></a><span data-ttu-id="7b444-132">Criar um serviço de atores</span><span class="sxs-lookup"><span data-stu-id="7b444-132">Create an actor service</span></span>
<span data-ttu-id="7b444-133">Comece por criar uma nova aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b444-133">Start by creating a new Service Fabric application.</span></span> <span data-ttu-id="7b444-134">Olá para Linux SDK de Service Fabric inclui um Yeoman andaime de Olá tooprovide gerador para uma aplicação de Service Fabric com um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="7b444-134">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="7b444-135">Comece por executar Olá Yeoman os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="7b444-135">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="7b444-136">Siga Olá instruções toocreate um **fiável serviço de Atores**.</span><span class="sxs-lookup"><span data-stu-id="7b444-136">Follow hello instructions toocreate a **Reliable Actor Service**.</span></span> <span data-ttu-id="7b444-137">Para este tutorial, nome Olá aplicação "HelloWorldActorApplication" e Olá ator "HelloWorldActor."</span><span class="sxs-lookup"><span data-stu-id="7b444-137">For this tutorial, name hello application "HelloWorldActorApplication" and hello actor "HelloWorldActor."</span></span> <span data-ttu-id="7b444-138">será criado Olá andaime os seguintes:</span><span class="sxs-lookup"><span data-stu-id="7b444-138">hello following scaffolding will be created:</span></span>

```bash
HelloWorldActorApplication/
├── build.gradle
├── HelloWorldActor
│   ├── build.gradle
│   ├── settings.gradle
│   └── src
│       └── reliableactor
│           ├── HelloWorldActorHost.java
│           └── HelloWorldActorImpl.java
├── HelloWorldActorApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldActorPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   ├── _readme.txt
│       │   └── Settings.xml
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── HelloWorldActorInterface
│   ├── build.gradle
│   └── src
│       └── reliableactor
│           └── HelloWorldActor.java
├── HelloWorldActorTestClient
│   ├── build.gradle
│   ├── settings.gradle
│   ├── src
│   │   └── reliableactor
│   │       └── test
│   │           └── HelloWorldActorTestClient.java
│   └── testclient.sh
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="7b444-139">Fiáveis blocos modulares básicos Actors</span><span class="sxs-lookup"><span data-stu-id="7b444-139">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="7b444-140">conceitos básicos Olá descritos anteriormente implica Olá blocos modulares básicos de um serviço de Atores fiável.</span><span class="sxs-lookup"><span data-stu-id="7b444-140">hello basic concepts described earlier translate into hello basic building blocks of a Reliable Actor service.</span></span>

### <a name="actor-interface"></a><span data-ttu-id="7b444-141">Interface de ator</span><span class="sxs-lookup"><span data-stu-id="7b444-141">Actor interface</span></span>
<span data-ttu-id="7b444-142">Esta contém uma definição de interface de Olá para ator Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-142">This contains hello interface definition for hello actor.</span></span> <span data-ttu-id="7b444-143">Esta interface define o contrato de ator Olá que é partilhado por clientes de Olá chamar ator Olá, pelo que, normalmente, faz sentido toodefine-lo num local que está separada da implementação de ator Olá e podem ser partilhados por vários outros e de implementação de ator Olá os serviços ou aplicações de cliente.</span><span class="sxs-lookup"><span data-stu-id="7b444-143">This interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in a place that is separate from hello actor implementation and can be shared by multiple other services or client applications.</span></span>

<span data-ttu-id="7b444-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span><span class="sxs-lookup"><span data-stu-id="7b444-144">`HelloWorldActorInterface/src/reliableactor/HelloWorldActor.java`:</span></span>

```java
public interface HelloWorldActor extends Actor {
    @Readonly   
    CompletableFuture<Integer> getCountAsync();

    CompletableFuture<?> setCountAsync(int count);
}
```

### <a name="actor-service"></a><span data-ttu-id="7b444-145">Serviço de atores</span><span class="sxs-lookup"><span data-stu-id="7b444-145">Actor service</span></span>
<span data-ttu-id="7b444-146">Contém a implementação de ator e o código de registo de atores.</span><span class="sxs-lookup"><span data-stu-id="7b444-146">This contains your actor implementation and actor registration code.</span></span> <span data-ttu-id="7b444-147">a classe de ator Olá implementa a interface de ator Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-147">hello actor class implements hello actor interface.</span></span> <span data-ttu-id="7b444-148">Isto tem onde o seu ator não respetivo trabalho.</span><span class="sxs-lookup"><span data-stu-id="7b444-148">This is where your actor does its work.</span></span>

<span data-ttu-id="7b444-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span><span class="sxs-lookup"><span data-stu-id="7b444-149">`HelloWorldActor/src/reliableactor/HelloWorldActorImpl`:</span></span>

```java
@ActorServiceAttribute(name = "HelloWorldActor.HelloWorldActorService")
@StatePersistenceAttribute(statePersistence = StatePersistence.Persisted)
public class HelloWorldActorImpl extends ReliableActor implements HelloWorldActor {
    Logger logger = Logger.getLogger(this.getClass().getName());

    protected CompletableFuture<?> onActivateAsync() {
        logger.log(Level.INFO, "onActivateAsync");

        return this.stateManager().tryAddStateAsync("count", 0);
    }

    @Override
    public CompletableFuture<Integer> getCountAsync() {
        logger.log(Level.INFO, "Getting current count value");
        return this.stateManager().getStateAsync("count");
    }

    @Override
    public CompletableFuture<?> setCountAsync(int count) {
        logger.log(Level.INFO, "Setting current count value {0}", count);
        return this.stateManager().addOrUpdateStateAsync("count", count, (key, value) -> count > value ? count : value);
    }
}
```

### <a name="actor-registration"></a><span data-ttu-id="7b444-150">Registo de ator</span><span class="sxs-lookup"><span data-stu-id="7b444-150">Actor registration</span></span>
<span data-ttu-id="7b444-151">serviço de atores Olá tem de ser registado com um tipo de serviço no tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7b444-151">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="7b444-152">Na ordem de Olá toorun do serviço de Atores as instâncias de ator, o tipo de ator também tem de ser registado com Olá serviço de Atores.</span><span class="sxs-lookup"><span data-stu-id="7b444-152">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="7b444-153">Olá `ActorRuntime` método de registo efetua este trabalho de atores.</span><span class="sxs-lookup"><span data-stu-id="7b444-153">hello `ActorRuntime` registration method performs this work for actors.</span></span>

<span data-ttu-id="7b444-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span><span class="sxs-lookup"><span data-stu-id="7b444-154">`HelloWorldActor/src/reliableactor/HelloWorldActorHost`:</span></span>

```java
public class HelloWorldActorHost {

    public static void main(String[] args) throws Exception {

        try {
            ActorRuntime.registerActorAsync(HelloWorldActorImpl.class, (context, actorType) -> new ActorServiceImpl(context, actorType, ()-> new HelloWorldActorImpl()), Duration.ofSeconds(10));

            Thread.sleep(Long.MAX_VALUE);

        } catch (Exception e) {
            e.printStackTrace();
            throw e;
        }
    }
}
```

### <a name="test-client"></a><span data-ttu-id="7b444-155">Cliente de teste</span><span class="sxs-lookup"><span data-stu-id="7b444-155">Test client</span></span>
<span data-ttu-id="7b444-156">Esta é uma aplicação de cliente de teste simples pode executar separadamente a partir tootest de aplicação de Service Fabric Olá o serviço de atores.</span><span class="sxs-lookup"><span data-stu-id="7b444-156">This is a simple test client application you can run separately from hello Service Fabric application tootest your actor service.</span></span> <span data-ttu-id="7b444-157">Este é um exemplo de onde Olá ActorProxy pode ser utilizado tooactivate e comunicar com instâncias de atores.</span><span class="sxs-lookup"><span data-stu-id="7b444-157">This is an example of where hello ActorProxy can be used tooactivate and communicate with actor instances.</span></span> <span data-ttu-id="7b444-158">É implementado com o serviço.</span><span class="sxs-lookup"><span data-stu-id="7b444-158">It does not get deployed with your service.</span></span>

### <a name="hello-application"></a><span data-ttu-id="7b444-159">aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="7b444-159">hello application</span></span>
<span data-ttu-id="7b444-160">Por fim, os pacotes de aplicações de Olá Olá serviço de atores e quaisquer outros serviços, que poderá adicionar no Olá futura em conjunto para implementação.</span><span class="sxs-lookup"><span data-stu-id="7b444-160">Finally, hello application packages hello actor service and any other services you might add in hello future together for deployment.</span></span> <span data-ttu-id="7b444-161">Contém Olá *ApplicationManifest.xml* e proprietários de local para o pacote de serviço de atores Olá.</span><span class="sxs-lookup"><span data-stu-id="7b444-161">It contains hello *ApplicationManifest.xml* and place holders for hello actor service package.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="7b444-162">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="7b444-162">Run hello application</span></span>

<span data-ttu-id="7b444-163">Olá Yeoman andaime inclui um gradle script toobuild Olá bash de aplicações e scripts toodeploy e remover a aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b444-163">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="7b444-164">aplicação de Olá toodeploy, primeira aplicação de Olá de compilação com o gradle:</span><span class="sxs-lookup"><span data-stu-id="7b444-164">toodeploy hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="7b444-165">Isto produzirá um pacote de aplicação de Service Fabric que pode ser implementado através de ferramentas da CLI de recursos de infraestrutura de serviço.</span><span class="sxs-lookup"><span data-stu-id="7b444-165">This will produce a Service Fabric application package that can be deployed using Service Fabric CLI tools.</span></span>

### <a name="deploy-service-fabric-cli"></a><span data-ttu-id="7b444-166">Implementar o Service Fabric CLI</span><span class="sxs-lookup"><span data-stu-id="7b444-166">Deploy Service Fabric CLI</span></span>

<span data-ttu-id="7b444-167">script de install.sh Olá contém Olá necessário CLI de recursos de infraestrutura de serviço (sfctl) comandos toodeploy Olá pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b444-167">hello install.sh script contains hello necessary Service Fabric CLI (sfctl) commands toodeploy hello application package.</span></span>
<span data-ttu-id="7b444-168">Execute Olá install.sh script toodeploy Olá aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b444-168">Run hello install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="7b444-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b444-169">Next steps</span></span>

* [<span data-ttu-id="7b444-170">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="7b444-170">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
