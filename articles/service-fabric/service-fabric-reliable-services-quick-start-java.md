---
title: "aaaCreate o primeiro e fiável microsserviço do Azure em Java | Microsoft Docs"
description: "Introdução toocreating uma aplicação do Microsoft Azure Service Fabric com serviços sem monitorização de estado e com monitorização de estado."
services: service-fabric
documentationcenter: java
author: vturecek
manager: timlt
editor: 
ms.assetid: 7831886f-7ec4-4aef-95c5-b2469a5b7b5d
ms.service: service-fabric
ms.devlang: java
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: 577d96591797bbfe6be5c1094426b5f1435cca0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="c76c7-103">Introdução ao Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c76c7-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c76c7-104">C# no Windows</span><span class="sxs-lookup"><span data-stu-id="c76c7-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="c76c7-105">Java em Linux</span><span class="sxs-lookup"><span data-stu-id="c76c7-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
>
>

<span data-ttu-id="c76c7-106">Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Services e explica-lhe como criar e implementar uma aplicação de serviço fiável simple escrita em Java.</span><span class="sxs-lookup"><span data-stu-id="c76c7-106">This article explains hello basics of Azure Service Fabric Reliable Services and walks you through creating and deploying a simple Reliable Service application written in Java.</span></span> <span data-ttu-id="c76c7-107">Este vídeo Microsoft Virtual Academy mostra também como toocreate um serviço fiável sem monitorização de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span><span class="sxs-lookup"><span data-stu-id="c76c7-107">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=DOX8K86yC_206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start-java/ReliableServicesJavaVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="installation-and-setup"></a><span data-ttu-id="c76c7-108">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="c76c7-108">Installation and setup</span></span>
<span data-ttu-id="c76c7-109">Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="c76c7-109">Before you start, make sure you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="c76c7-110">Se precisar de tooset-lo, aceda demasiado[introdução no Mac](service-fabric-get-started-mac.md) ou [introdução no Linux](service-fabric-get-started-linux.md).</span><span class="sxs-lookup"><span data-stu-id="c76c7-110">If you need tooset it up, go too[getting started on Mac](service-fabric-get-started-mac.md) or [getting started on Linux](service-fabric-get-started-linux.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="c76c7-111">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="c76c7-111">Basic concepts</span></span>
<span data-ttu-id="c76c7-112">tooget começar Reliable Services, apenas é necessário toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="c76c7-112">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="c76c7-113">**Tipo de serviço**: Esta é a implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="c76c7-113">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="c76c7-114">Está definido por classe de Olá escreve que expande `StatelessService` e quaisquer outras código ou dependências utilizadas nas mesmas, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="c76c7-114">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="c76c7-115">**Com o nome de instância de serviço**: toorun seu serviço, criar instâncias nomeadas do seu tipo de serviço, muito como criar instâncias do objecto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="c76c7-115">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="c76c7-116">Instâncias de serviço são de facto instâncias de objeto da sua classe de serviço escreve.</span><span class="sxs-lookup"><span data-stu-id="c76c7-116">Service instances are in fact object instantiations of your service class that you write.</span></span>
* <span data-ttu-id="c76c7-117">**Anfitrião do serviço**: Olá instâncias de serviço criar necessidade toorun dentro de um anfitrião com o nome.</span><span class="sxs-lookup"><span data-stu-id="c76c7-117">**Service host**: hello named service instances you create need toorun inside a host.</span></span> <span data-ttu-id="c76c7-118">anfitrião do serviço Olá é apenas um processo em que podem executar instâncias do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="c76c7-118">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="c76c7-119">**Serviço de registo**: registo reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="c76c7-119">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="c76c7-120">Olá o tipo de serviço tem de ser registado com Olá Service Fabric runtime num serviço alojem tooallow Service Fabric toocreate instâncias do mesmo toorun.</span><span class="sxs-lookup"><span data-stu-id="c76c7-120">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="c76c7-121">Criar um serviço sem monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="c76c7-121">Create a stateless service</span></span>
<span data-ttu-id="c76c7-122">Comece por criar uma aplicação de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c76c7-122">Start by creating a Service Fabric application.</span></span> <span data-ttu-id="c76c7-123">Olá para Linux SDK de Service Fabric inclui um Yeoman andaime de Olá tooprovide gerador para uma aplicação de Service Fabric com um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="c76c7-123">hello Service Fabric SDK for Linux includes a Yeoman generator tooprovide hello scaffolding for a Service Fabric application with a stateless service.</span></span> <span data-ttu-id="c76c7-124">Comece por executar Olá Yeoman os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c76c7-124">Start by running hello following Yeoman command:</span></span>

```bash
$ yo azuresfjava
```

<span data-ttu-id="c76c7-125">Siga Olá instruções toocreate um **sem monitorização de estado de serviço fiável**.</span><span class="sxs-lookup"><span data-stu-id="c76c7-125">Follow hello instructions toocreate a **Reliable Stateless Service**.</span></span> <span data-ttu-id="c76c7-126">Para este tutorial, a aplicação de Olá nome "HelloWorldApplication" e a Olá do serviço "Olámundo".</span><span class="sxs-lookup"><span data-stu-id="c76c7-126">For this tutorial, name hello application "HelloWorldApplication" and hello service "HelloWorld".</span></span> <span data-ttu-id="c76c7-127">resultado de Olá inclui diretórios para Olá `HelloWorldApplication` e `HelloWorld`.</span><span class="sxs-lookup"><span data-stu-id="c76c7-127">hello result includes directories for hello `HelloWorldApplication` and `HelloWorld`.</span></span>

```bash
HelloWorldApplication/
├── build.gradle
├── HelloWorld
│   ├── build.gradle
│   └── src
│       └── statelessservice
│           ├── HelloWorldServiceHost.java
│           └── HelloWorldService.java
├── HelloWorldApplication
│   ├── ApplicationManifest.xml
│   └── HelloWorldPkg
│       ├── Code
│       │   ├── entryPoint.sh
│       │   └── _readme.txt
│       ├── Config
│       │   └── _readme.txt
│       ├── Data
│       │   └── _readme.txt
│       └── ServiceManifest.xml
├── install.sh
├── settings.gradle
└── uninstall.sh
```

## <a name="implement-hello-service"></a><span data-ttu-id="c76c7-128">Implementar o serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="c76c7-128">Implement hello service</span></span>
<span data-ttu-id="c76c7-129">Abra **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span><span class="sxs-lookup"><span data-stu-id="c76c7-129">Open **HelloWorldApplication/HelloWorld/src/statelessservice/HelloWorldService.java**.</span></span> <span data-ttu-id="c76c7-130">Esta classe define o tipo de serviço Olá e pode executar qualquer código.</span><span class="sxs-lookup"><span data-stu-id="c76c7-130">This class defines hello service type, and can run any code.</span></span> <span data-ttu-id="c76c7-131">API do serviço Olá fornece dois pontos de entrada para o seu código:</span><span class="sxs-lookup"><span data-stu-id="c76c7-131">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="c76c7-132">Um método de ponto de entrada open-ended, denominado `runAsync()`, onde pode começar a executar quaisquer cargas de trabalho, incluindo as cargas de trabalho de computação de execução longa.</span><span class="sxs-lookup"><span data-stu-id="c76c7-132">An open-ended entry point method, called `runAsync()`, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```java
@Override
protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {
    ...
}
```

* <span data-ttu-id="c76c7-133">Um ponto de entrada de comunicação em que pode plug-in a pilha de comunicação de eleição.</span><span class="sxs-lookup"><span data-stu-id="c76c7-133">A communication entry point where you can plug in your communication stack of choice.</span></span> <span data-ttu-id="c76c7-134">Este é onde pode começar a receber pedidos de utilizadores e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="c76c7-134">This is where you can start receiving requests from users and other services.</span></span>

```java
@Override
protected List<ServiceInstanceListener> createServiceInstanceListeners() {
    ...
}
```

<span data-ttu-id="c76c7-135">Neste tutorial, iremos focar-se no Olá `runAsync()` o método de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="c76c7-135">In this tutorial, we focus on hello `runAsync()` entry point method.</span></span> <span data-ttu-id="c76c7-136">Este é onde imediatamente pode começar a executar o seu código.</span><span class="sxs-lookup"><span data-stu-id="c76c7-136">This is where you can immediately start running your code.</span></span>

### <a name="runasync"></a><span data-ttu-id="c76c7-137">Runasync com</span><span class="sxs-lookup"><span data-stu-id="c76c7-137">RunAsync</span></span>
<span data-ttu-id="c76c7-138">plataforma de Olá chama este método quando uma instância de um serviço é tooexecute pronto e colocá-la.</span><span class="sxs-lookup"><span data-stu-id="c76c7-138">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="c76c7-139">Para um serviço sem monitorização de estado, basta que significa quando a instância de serviço Olá é aberta.</span><span class="sxs-lookup"><span data-stu-id="c76c7-139">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="c76c7-140">Um token de cancelamento é fornecido toocoordinate quando a instância de serviço tem toobe fechado.</span><span class="sxs-lookup"><span data-stu-id="c76c7-140">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="c76c7-141">No Service Fabric, este ciclo de abertura/fecho de uma instância de serviço pode ocorrer demasiadas vezes ao longo da duração Olá de serviço Olá como um todo.</span><span class="sxs-lookup"><span data-stu-id="c76c7-141">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="c76c7-142">Esta situação pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c76c7-142">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="c76c7-143">sistema de Olá move as instâncias de serviço para balanceamento de recurso.</span><span class="sxs-lookup"><span data-stu-id="c76c7-143">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="c76c7-144">Falhas ocorrerem no seu código.</span><span class="sxs-lookup"><span data-stu-id="c76c7-144">Faults occur in your code.</span></span>
* <span data-ttu-id="c76c7-145">aplicação Olá ou do sistema está atualizado.</span><span class="sxs-lookup"><span data-stu-id="c76c7-145">hello application or system is upgraded.</span></span>
* <span data-ttu-id="c76c7-146">hardware subjacente Olá sofre uma falha.</span><span class="sxs-lookup"><span data-stu-id="c76c7-146">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="c76c7-147">Esta orquestração é gerida pelo Service Fabric tookeep seu serviço altamente disponível e corretamente equilibrado.</span><span class="sxs-lookup"><span data-stu-id="c76c7-147">This orchestration is managed by Service Fabric tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="c76c7-148">`runAsync()`não deverá bloquear forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="c76c7-148">`runAsync()` should not block synchronously.</span></span> <span data-ttu-id="c76c7-149">A implementação de runasync com deverá devolver um CompletableFuture tooallow Olá runtime toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c76c7-149">Your implementation of runAsync should return a CompletableFuture tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="c76c7-150">Se a carga de trabalho tem uma tarefa de execução longa que deve ser efetuada dentro de tooimplement Olá CompletableFuture.</span><span class="sxs-lookup"><span data-stu-id="c76c7-150">If your workload needs tooimplement a long running task that should be done inside hello CompletableFuture.</span></span>

#### <a name="cancellation"></a><span data-ttu-id="c76c7-151">Cancelamento</span><span class="sxs-lookup"><span data-stu-id="c76c7-151">Cancellation</span></span>
<span data-ttu-id="c76c7-152">O cancelamento da sua carga de trabalho é um esforço cooperative orquestrado por Olá fornecido o token de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="c76c7-152">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="c76c7-153">sistema de Olá aguarda tooend sua tarefa (por conclusão com êxito, cancelamento ou falhas) antes de se move.</span><span class="sxs-lookup"><span data-stu-id="c76c7-153">hello system waits for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="c76c7-154">É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `runAsync()` mais rapidamente possível ao sistema de Olá pedidos de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="c76c7-154">It is important toohonor hello cancellation token, finish any work, and exit `runAsync()` as quickly as possible when hello system requests cancellation.</span></span> <span data-ttu-id="c76c7-155">Olá exemplo seguinte demonstra como toohandle um evento de cancelamento:</span><span class="sxs-lookup"><span data-stu-id="c76c7-155">hello following example demonstrates how toohandle a cancellation event:</span></span>

```java
    @Override
    protected CompletableFuture<?> runAsync(CancellationToken cancellationToken) {

        // TODO: Replace hello following sample code with your own logic
        // or remove this runAsync override if it's not needed in your service.

        CompletableFuture.runAsync(() -> {
          long iterations = 0;
          while(true)
          {
            cancellationToken.throwIfCancellationRequested();
            logger.log(Level.INFO, "Working-{0}", ++iterations);

            try
            {
              Thread.sleep(1000);
            }
            catch (IOException ex) {}
          }
        });
    }
```

### <a name="service-registration"></a><span data-ttu-id="c76c7-156">Registo do serviço</span><span class="sxs-lookup"><span data-stu-id="c76c7-156">Service registration</span></span>
<span data-ttu-id="c76c7-157">Tipos de serviço tem de ser registados com o tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="c76c7-157">Service types must be registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="c76c7-158">tipo de serviço de Olá está definido no Olá `ServiceManifest.xml` e a classe de serviço que implementa `StatelessService`.</span><span class="sxs-lookup"><span data-stu-id="c76c7-158">hello service type is defined in hello `ServiceManifest.xml` and your service class that implements `StatelessService`.</span></span> <span data-ttu-id="c76c7-159">Registo do serviço é executado no ponto de entrada principal do processo de Olá.</span><span class="sxs-lookup"><span data-stu-id="c76c7-159">Service registration is performed in hello process main entry point.</span></span> <span data-ttu-id="c76c7-160">Neste exemplo, Olá o processo de ponto de entrada principal é `HelloWorldServiceHost.java`:</span><span class="sxs-lookup"><span data-stu-id="c76c7-160">In this example, hello process main entry point is `HelloWorldServiceHost.java`:</span></span>

```java
public static void main(String[] args) throws Exception {
    try {
        ServiceRuntime.registerStatelessServiceAsync("HelloWorldType", (context) -> new HelloWorldService(), Duration.ofSeconds(10));
        logger.log(Level.INFO, "Registered stateless service type HelloWorldType.");
        Thread.sleep(Long.MAX_VALUE);
    }
    catch (Exception ex) {
        logger.log(Level.SEVERE, "Exception in registration:", ex);
        throw ex;
    }
}
```

## <a name="run-hello-application"></a><span data-ttu-id="c76c7-161">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c76c7-161">Run hello application</span></span>

<span data-ttu-id="c76c7-162">Olá Yeoman andaime inclui um gradle script toobuild Olá bash de aplicações e scripts toodeploy e remover a aplicação.</span><span class="sxs-lookup"><span data-stu-id="c76c7-162">hello Yeoman scaffolding includes a gradle script toobuild hello application and bash scripts toodeploy and remove the application.</span></span> <span data-ttu-id="c76c7-163">aplicação de Olá toorun, primeira aplicação de Olá de compilação com o gradle:</span><span class="sxs-lookup"><span data-stu-id="c76c7-163">toorun hello application, first build hello application with gradle:</span></span>

```bash
$ gradle
```

<span data-ttu-id="c76c7-164">Isto produz um pacote de aplicação de Service Fabric pode ser implementado utilizando a CLI de recursos de infraestrutura de serviço.</span><span class="sxs-lookup"><span data-stu-id="c76c7-164">This produces a Service Fabric application package that can be deployed using Service Fabric CLI.</span></span>

### <a name="deploy-with-service-fabric-cli"></a><span data-ttu-id="c76c7-165">Implementar com a CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c76c7-165">Deploy with Service Fabric CLI</span></span>

<span data-ttu-id="c76c7-166">script de install.sh Olá contém Olá necessário CLI de recursos de infraestrutura de serviço comandos toodeploy Olá pacote de aplicação.</span><span class="sxs-lookup"><span data-stu-id="c76c7-166">hello install.sh script contains hello necessary Service Fabric CLI commands toodeploy hello application package.</span></span> <span data-ttu-id="c76c7-167">Execute a aplicação de Olá install.sh script toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c76c7-167">Run the install.sh script toodeploy hello application.</span></span>

```bash
$ ./install.sh
```

## <a name="next-steps"></a><span data-ttu-id="c76c7-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c76c7-168">Next steps</span></span>

* [<span data-ttu-id="c76c7-169">Introdução à CLI do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="c76c7-169">Getting started with Service Fabric CLI</span></span>](service-fabric-cli.md)
