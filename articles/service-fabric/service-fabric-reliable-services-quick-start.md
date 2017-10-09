---
title: "aaaCreate sua primeira aplicação de Service Fabric em c# | Microsoft Docs"
description: "Introdução toocreating uma aplicação do Microsoft Azure Service Fabric com serviços sem monitorização de estado e com monitorização de estado."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d9b44d75-e905-468e-b867-2190ce97379a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/06/2017
ms.author: vturecek
ms.openlocfilehash: e95e67cc84be1b83c936b250cae9112ddc77b963
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-reliable-services"></a><span data-ttu-id="c3124-103">Introdução ao Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c3124-103">Get started with Reliable Services</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c3124-104">C# no Windows</span><span class="sxs-lookup"><span data-stu-id="c3124-104">C# on Windows</span></span>](service-fabric-reliable-services-quick-start.md)
> * [<span data-ttu-id="c3124-105">Java em Linux</span><span class="sxs-lookup"><span data-stu-id="c3124-105">Java on Linux</span></span>](service-fabric-reliable-services-quick-start-java.md)
> 
> 

<span data-ttu-id="c3124-106">Uma aplicação do Azure Service Fabric contém um ou mais serviços com o seu código.</span><span class="sxs-lookup"><span data-stu-id="c3124-106">An Azure Service Fabric application contains one or more services that run your code.</span></span> <span data-ttu-id="c3124-107">Este guia mostra como toocreate sem monitorização de estado e com monitorização de estado aplicações de Service Fabric com [Reliable Services](service-fabric-reliable-services-introduction.md).</span><span class="sxs-lookup"><span data-stu-id="c3124-107">This guide shows you how toocreate both stateless and stateful Service Fabric applications with [Reliable Services](service-fabric-reliable-services-introduction.md).</span></span>  <span data-ttu-id="c3124-108">Este vídeo Microsoft Virtual Academy mostra também como toocreate um serviço fiável sem monitorização de estado:<center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span><span class="sxs-lookup"><span data-stu-id="c3124-108">This Microsoft Virtual Academy video also shows you how toocreate a stateless Reliable service: <center><a target="_blank" href="https://mva.microsoft.com/en-US/training-courses/building-microservices-applications-on-azure-service-fabric-16747?l=s39AO76yC_7206218965"></span></span>  
<img src="./media/service-fabric-reliable-services-quick-start/ReliableServicesVid.png" WIDTH="360" HEIGHT="244">  
</a></center>

## <a name="basic-concepts"></a><span data-ttu-id="c3124-109">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="c3124-109">Basic concepts</span></span>
<span data-ttu-id="c3124-110">tooget começar Reliable Services, apenas é necessário toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="c3124-110">tooget started with Reliable Services, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="c3124-111">**Tipo de serviço**: Esta é a implementação de serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-111">**Service type**: This is your service implementation.</span></span> <span data-ttu-id="c3124-112">Está definido por classe de Olá escreve que expande `StatelessService` e quaisquer outras código ou dependências utilizadas nas mesmas, juntamente com um nome e um número de versão.</span><span class="sxs-lookup"><span data-stu-id="c3124-112">It is defined by hello class you write that extends `StatelessService` and any other code or dependencies used therein, along with a name and a version number.</span></span>
* <span data-ttu-id="c3124-113">**Com o nome de instância de serviço**: toorun seu serviço, criar instâncias nomeadas do seu tipo de serviço, muito como criar instâncias do objecto de um tipo de classe.</span><span class="sxs-lookup"><span data-stu-id="c3124-113">**Named service instance**: toorun your service, you create named instances of your service type, much like you create object instances of a class type.</span></span> <span data-ttu-id="c3124-114">Uma instância de serviço tem um nome de formato Olá de um URI utilizando Olá "fabric: /" esquema, tal como "fabric: / MyApp/MyService".</span><span class="sxs-lookup"><span data-stu-id="c3124-114">A service instance has a name in hello form of a URI using hello "fabric:/" scheme, such as "fabric:/MyApp/MyService".</span></span>
* <span data-ttu-id="c3124-115">**Anfitrião do serviço**: Olá com o nome de instâncias de serviço criar necessidade toorun dentro de um processo de anfitrião.</span><span class="sxs-lookup"><span data-stu-id="c3124-115">**Service host**: hello named service instances you create need toorun inside a host process.</span></span> <span data-ttu-id="c3124-116">anfitrião do serviço Olá é apenas um processo em que podem executar instâncias do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-116">hello service host is just a process where instances of your service can run.</span></span>
* <span data-ttu-id="c3124-117">**Serviço de registo**: registo reúne tudo.</span><span class="sxs-lookup"><span data-stu-id="c3124-117">**Service registration**: Registration brings everything together.</span></span> <span data-ttu-id="c3124-118">Olá o tipo de serviço tem de ser registado com Olá Service Fabric runtime num serviço alojem tooallow Service Fabric toocreate instâncias do mesmo toorun.</span><span class="sxs-lookup"><span data-stu-id="c3124-118">hello service type must be registered with hello Service Fabric runtime in a service host tooallow Service Fabric toocreate instances of it toorun.</span></span>  

## <a name="create-a-stateless-service"></a><span data-ttu-id="c3124-119">Criar um serviço sem monitorização de estado</span><span class="sxs-lookup"><span data-stu-id="c3124-119">Create a stateless service</span></span>
<span data-ttu-id="c3124-120">Um serviço sem monitorização de estado é um tipo de serviço que está atualmente a norma de Olá em aplicações na nuvem.</span><span class="sxs-lookup"><span data-stu-id="c3124-120">A stateless service is a type of service that is currently hello norm in cloud applications.</span></span> <span data-ttu-id="c3124-121">Considera-se sem monitorização de estado porque o serviço de Olá propriamente dito não contém dados que precisam de toobe armazenados de forma fiável ou tornado de elevada.</span><span class="sxs-lookup"><span data-stu-id="c3124-121">It is considered stateless because hello service itself does not contain data that needs toobe stored reliably or made highly available.</span></span> <span data-ttu-id="c3124-122">Se uma instância de um serviço sem monitorização de estado foi encerrado, todos os respetivo estado interno é perdido.</span><span class="sxs-lookup"><span data-stu-id="c3124-122">If an instance of a stateless service shuts down, all of its internal state is lost.</span></span> <span data-ttu-id="c3124-123">Este tipo de serviço, estado tem de ser tooan persistente arquivo externo, como tabelas do Azure ou uma base de dados do SQL Server para o mesmo toobe efetuada e de elevada disponibilidade fiável.</span><span class="sxs-lookup"><span data-stu-id="c3124-123">In this type of service, state must be persisted tooan external store, such as Azure Tables or a SQL database, for it toobe made highly available and reliable.</span></span>

<span data-ttu-id="c3124-124">Inicie o Visual Studio 2015 ou Visual Studio 2017 como administrador e criar um novo projeto de aplicação de Service Fabric com o nome *Olámundo*:</span><span class="sxs-lookup"><span data-stu-id="c3124-124">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project named *HelloWorld*:</span></span>

![Utilizar toocreate de caixa de diálogo Olá novo projeto uma nova aplicação de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject.png)

<span data-ttu-id="c3124-126">Em seguida, criar um projeto de serviço sem monitorização de estado com o nome *HelloWorldStateless*:</span><span class="sxs-lookup"><span data-stu-id="c3124-126">Then create a stateless service project named *HelloWorldStateless*:</span></span>

![Na caixa de diálogo segundo Olá, crie um projeto de serviço sem monitorização de estado](media/service-fabric-reliable-services-quick-start/hello-stateless-NewProject2.png)

<span data-ttu-id="c3124-128">Agora, a sua solução contém dois projetos:</span><span class="sxs-lookup"><span data-stu-id="c3124-128">Your solution now contains two projects:</span></span>

* <span data-ttu-id="c3124-129">*Olámundo*.</span><span class="sxs-lookup"><span data-stu-id="c3124-129">*HelloWorld*.</span></span> <span data-ttu-id="c3124-130">Este é Olá *aplicação* projeto que contém o *serviços*.</span><span class="sxs-lookup"><span data-stu-id="c3124-130">This is hello *application* project that contains your *services*.</span></span> <span data-ttu-id="c3124-131">Também contém o manifesto da aplicação Olá que descreve a aplicação Olá, bem como um número de scripts do PowerShell que o ajudam a toodeploy a aplicação.</span><span class="sxs-lookup"><span data-stu-id="c3124-131">It also contains hello application manifest that describes hello application, as well as a number of PowerShell scripts that help you toodeploy your application.</span></span>
* <span data-ttu-id="c3124-132">*HelloWorldStateless*.</span><span class="sxs-lookup"><span data-stu-id="c3124-132">*HelloWorldStateless*.</span></span> <span data-ttu-id="c3124-133">Este é o projeto de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-133">This is hello service project.</span></span> <span data-ttu-id="c3124-134">Implementação de serviço sem monitorização de estado de Olá nele contidos.</span><span class="sxs-lookup"><span data-stu-id="c3124-134">It contains hello stateless service implementation.</span></span>

## <a name="implement-hello-service"></a><span data-ttu-id="c3124-135">Implementar o serviço de Olá</span><span class="sxs-lookup"><span data-stu-id="c3124-135">Implement hello service</span></span>
<span data-ttu-id="c3124-136">Abra Olá **HelloWorldStateless.cs** ficheiros no projeto de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-136">Open hello **HelloWorldStateless.cs** file in hello service project.</span></span> <span data-ttu-id="c3124-137">No Service Fabric, um serviço pode ser executado qualquer lógica empresarial.</span><span class="sxs-lookup"><span data-stu-id="c3124-137">In Service Fabric, a service can run any business logic.</span></span> <span data-ttu-id="c3124-138">API do serviço Olá fornece dois pontos de entrada para o seu código:</span><span class="sxs-lookup"><span data-stu-id="c3124-138">hello service API provides two entry points for your code:</span></span>

* <span data-ttu-id="c3124-139">Um método de ponto de entrada open-ended, denominado *runasync com*, onde pode começar a executar quaisquer cargas de trabalho, incluindo as cargas de trabalho de computação de execução longa.</span><span class="sxs-lookup"><span data-stu-id="c3124-139">An open-ended entry point method, called *RunAsync*, where you can begin executing any workloads, including long-running compute workloads.</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    ...
}
```

* <span data-ttu-id="c3124-140">Um ponto de entrada de comunicação em que pode plug-in a pilha de comunicação de escolha, tal como ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="c3124-140">A communication entry point where you can plug in your communication stack of choice, such as ASP.NET Core.</span></span> <span data-ttu-id="c3124-141">Este é onde pode começar a receber pedidos de utilizadores e outros serviços.</span><span class="sxs-lookup"><span data-stu-id="c3124-141">This is where you can start receiving requests from users and other services.</span></span>

```csharp
protected override IEnumerable<ServiceInstanceListener> CreateServiceInstanceListeners()
{
    ...
}
```

<span data-ttu-id="c3124-142">Neste tutorial, iremos irá focar-se no Olá `RunAsync()` o método de ponto de entrada.</span><span class="sxs-lookup"><span data-stu-id="c3124-142">In this tutorial, we will focus on hello `RunAsync()` entry point method.</span></span> <span data-ttu-id="c3124-143">Este é onde imediatamente pode começar a executar o seu código.</span><span class="sxs-lookup"><span data-stu-id="c3124-143">This is where you can immediately start running your code.</span></span>
<span data-ttu-id="c3124-144">modelo de projeto Olá inclui uma implementação de exemplo de `RunAsync()` que incrementa uma contagem graduais.</span><span class="sxs-lookup"><span data-stu-id="c3124-144">hello project template includes a sample implementation of `RunAsync()` that increments a rolling count.</span></span>

> [!NOTE]
> <span data-ttu-id="c3124-145">Para obter mais informações sobre como pilha toowork com uma comunicação, consulte [serviços de API Web do Service Fabric com OWIN automática de alojamento](service-fabric-reliable-services-communication-webapi.md)</span><span class="sxs-lookup"><span data-stu-id="c3124-145">For details about how toowork with a communication stack, see [Service Fabric Web API services with OWIN self-hosting](service-fabric-reliable-services-communication-webapi.md)</span></span>
> 
> 

### <a name="runasync"></a><span data-ttu-id="c3124-146">Runasync com</span><span class="sxs-lookup"><span data-stu-id="c3124-146">RunAsync</span></span>
```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    long iterations = 0;

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        ServiceEventSource.Current.ServiceMessage(this, "Working-{0}", ++iterations);

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
}
```

<span data-ttu-id="c3124-147">plataforma de Olá chama este método quando uma instância de um serviço é tooexecute pronto e colocá-la.</span><span class="sxs-lookup"><span data-stu-id="c3124-147">hello platform calls this method when an instance of a service is placed and ready tooexecute.</span></span> <span data-ttu-id="c3124-148">Para um serviço sem monitorização de estado, basta que significa quando a instância de serviço Olá é aberta.</span><span class="sxs-lookup"><span data-stu-id="c3124-148">For a stateless service, that simply means when hello service instance is opened.</span></span> <span data-ttu-id="c3124-149">Um token de cancelamento é fornecido toocoordinate quando a instância de serviço tem toobe fechado.</span><span class="sxs-lookup"><span data-stu-id="c3124-149">A cancellation token is provided toocoordinate when your service instance needs toobe closed.</span></span> <span data-ttu-id="c3124-150">No Service Fabric, este ciclo de abertura/fecho de uma instância de serviço pode ocorrer demasiadas vezes ao longo da duração Olá de serviço Olá como um todo.</span><span class="sxs-lookup"><span data-stu-id="c3124-150">In Service Fabric, this open/close cycle of a service instance can occur many times over hello lifetime of hello service as a whole.</span></span> <span data-ttu-id="c3124-151">Esta situação pode ocorrer por vários motivos, incluindo:</span><span class="sxs-lookup"><span data-stu-id="c3124-151">This can happen for various reasons, including:</span></span>

* <span data-ttu-id="c3124-152">sistema de Olá move as instâncias de serviço para balanceamento de recurso.</span><span class="sxs-lookup"><span data-stu-id="c3124-152">hello system moves your service instances for resource balancing.</span></span>
* <span data-ttu-id="c3124-153">Falhas ocorrerem no seu código.</span><span class="sxs-lookup"><span data-stu-id="c3124-153">Faults occur in your code.</span></span>
* <span data-ttu-id="c3124-154">aplicação Olá ou do sistema está atualizado.</span><span class="sxs-lookup"><span data-stu-id="c3124-154">hello application or system is upgraded.</span></span>
* <span data-ttu-id="c3124-155">hardware subjacente Olá sofre uma falha.</span><span class="sxs-lookup"><span data-stu-id="c3124-155">hello underlying hardware experiences an outage.</span></span>

<span data-ttu-id="c3124-156">Esta orquestração é gerida pelo Olá sistema tookeep seu serviço altamente disponível e corretamente equilibrado.</span><span class="sxs-lookup"><span data-stu-id="c3124-156">This orchestration is managed by hello system tookeep your service highly available and properly balanced.</span></span>

<span data-ttu-id="c3124-157">`RunAsync()`não deverá bloquear forma síncrona.</span><span class="sxs-lookup"><span data-stu-id="c3124-157">`RunAsync()` should not block synchronously.</span></span> <span data-ttu-id="c3124-158">A implementação de runasync com deve devolver uma tarefa ou await em quaisquer operações demoradas ou bloqueio tooallow Olá runtime toocontinue.</span><span class="sxs-lookup"><span data-stu-id="c3124-158">Your implementation of RunAsync should return a Task or await on any long-running or blocking operations tooallow hello runtime toocontinue.</span></span> <span data-ttu-id="c3124-159">Tome nota na Olá `while(true)` ciclo no exemplo anterior Olá, uma tarefa-returning `await Task.Delay()` é utilizado.</span><span class="sxs-lookup"><span data-stu-id="c3124-159">Note in hello `while(true)` loop in hello previous example, a Task-returning `await Task.Delay()` is used.</span></span> <span data-ttu-id="c3124-160">Se a carga de trabalho tem bloquear de forma síncrona, deve agendar uma nova tarefa com `Task.Run()` no seu `RunAsync` implementação.</span><span class="sxs-lookup"><span data-stu-id="c3124-160">If your workload must block synchronously, you should schedule a new Task with `Task.Run()` in your `RunAsync` implementation.</span></span>

<span data-ttu-id="c3124-161">O cancelamento da sua carga de trabalho é um esforço cooperative orquestrado por Olá fornecido o token de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="c3124-161">Cancellation of your workload is a cooperative effort orchestrated by hello provided cancellation token.</span></span> <span data-ttu-id="c3124-162">sistema Olá espera que o tooend de tarefas (por conclusão com êxito, cancelamento ou falhas) antes de se move.</span><span class="sxs-lookup"><span data-stu-id="c3124-162">hello system will wait for your task tooend (by successful completion, cancellation, or fault) before it moves on.</span></span> <span data-ttu-id="c3124-163">É importante toohonor Olá cancelamento token, concluir qualquer trabalho e sair `RunAsync()` mais rapidamente possível ao sistema de Olá pedidos de cancelamento.</span><span class="sxs-lookup"><span data-stu-id="c3124-163">It is important toohonor hello cancellation token, finish any work, and exit `RunAsync()` as quickly as possible when hello system requests cancellation.</span></span>

<span data-ttu-id="c3124-164">Neste exemplo de serviço sem monitorização de estado, contagem de Olá é armazenada numa variável local.</span><span class="sxs-lookup"><span data-stu-id="c3124-164">In this stateless service example, hello count is stored in a local variable.</span></span> <span data-ttu-id="c3124-165">Mas porque se trata de um serviço sem monitorização de estado, o valor de Olá armazenados existe apenas para Olá atual do ciclo de vida da respetiva instância de serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-165">But because this is a stateless service, hello value that's stored exists only for hello current lifecycle of its service instance.</span></span> <span data-ttu-id="c3124-166">Quando move ou reinicia o serviço de Olá, o valor de Olá é perdido.</span><span class="sxs-lookup"><span data-stu-id="c3124-166">When hello service moves or restarts, hello value is lost.</span></span>

## <a name="create-a-stateful-service"></a><span data-ttu-id="c3124-167">Criar um serviço com estado</span><span class="sxs-lookup"><span data-stu-id="c3124-167">Create a stateful service</span></span>
<span data-ttu-id="c3124-168">Serviço de recursos de infraestrutura apresenta um novo tipo de serviço que tem o estado monitorizado.</span><span class="sxs-lookup"><span data-stu-id="c3124-168">Service Fabric introduces a new kind of service that is stateful.</span></span> <span data-ttu-id="c3124-169">Um serviço com estado pode manter o estado Olá próprio serviço, localizado conjuntamente com o código de Olá que está a ser utilizado de forma fiável.</span><span class="sxs-lookup"><span data-stu-id="c3124-169">A stateful service can maintain state reliably within hello service itself, co-located with hello code that's using it.</span></span> <span data-ttu-id="c3124-170">Estado é efetuado elevado pelo Service Fabric sem Olá necessidade toopersist tooan externo armazenamento de Estados.</span><span class="sxs-lookup"><span data-stu-id="c3124-170">State is made highly available by Service Fabric without hello need toopersist state tooan external store.</span></span>

<span data-ttu-id="c3124-171">tooconvert um valor de contador de toohighly sem monitorização de estado disponível e persistente, mesmo quando o serviço de Olá move ou reinicia, precisa de um serviço com monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="c3124-171">tooconvert a counter value from stateless toohighly available and persistent, even when hello service moves or restarts, you need a stateful service.</span></span>

<span data-ttu-id="c3124-172">No Olá mesmo *Olámundo* aplicação, pode adicionar um novo serviço clicando em referências de serviços de Olá no projeto de aplicação Olá e selecionando **adicionar -> novo serviço de recursos de infraestrutura de serviço**.</span><span class="sxs-lookup"><span data-stu-id="c3124-172">In hello same *HelloWorld* application, you can add a new service by right-clicking on hello Services references in hello application project and selecting **Add ->  New Service Fabric Service**.</span></span>

![Adicionar uma aplicação de Service Fabric de tooyour de serviço](media/service-fabric-reliable-services-quick-start/hello-stateful-NewService.png)

<span data-ttu-id="c3124-174">Selecione **serviço de monitorização de estado** e dê-lhe nome *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="c3124-174">Select **Stateful Service** and name it *HelloWorldStateful*.</span></span> <span data-ttu-id="c3124-175">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="c3124-175">Click **OK**.</span></span>

![Utilizar toocreate de caixa de diálogo Olá novo projeto um novo serviço de monitorização de estado de Service Fabric](media/service-fabric-reliable-services-quick-start/hello-stateful-NewProject.png)

<span data-ttu-id="c3124-177">A aplicação deve agora ter dois serviços: Olá sem estado *HelloWorldStateless* e o serviço com estado Olá *HelloWorldStateful*.</span><span class="sxs-lookup"><span data-stu-id="c3124-177">Your application should now have two services: hello stateless service *HelloWorldStateless* and hello stateful service *HelloWorldStateful*.</span></span>

<span data-ttu-id="c3124-178">Um serviço com estado tem Olá mesmo pontos de entrada como um serviço sem estado.</span><span class="sxs-lookup"><span data-stu-id="c3124-178">A stateful service has hello same entry points as a stateless service.</span></span> <span data-ttu-id="c3124-179">Olá principal diferença é a disponibilidade de Olá de um *fornecedor de estado* que pode armazenar o estado de forma fiável.</span><span class="sxs-lookup"><span data-stu-id="c3124-179">hello main difference is hello availability of a *state provider* that can store state reliably.</span></span> <span data-ttu-id="c3124-180">Service Fabric inclui uma implementação do fornecedor de estado chamada [coleções fiável](service-fabric-reliable-services-reliable-collections.md), que lhe permite criar estruturas de dados replicados através de Olá fiável Gestor de estado.</span><span class="sxs-lookup"><span data-stu-id="c3124-180">Service Fabric comes with a state provider implementation called [Reliable Collections](service-fabric-reliable-services-reliable-collections.md), which lets you create replicated data structures through hello Reliable State Manager.</span></span> <span data-ttu-id="c3124-181">Um serviço fiável com monitorização de estado utiliza este fornecedor de estado por predefinição.</span><span class="sxs-lookup"><span data-stu-id="c3124-181">A stateful Reliable Service uses this state provider by default.</span></span>

<span data-ttu-id="c3124-182">Abra **HelloWorldStateful.cs** no *HelloWorldStateful*, que contém Olá método runasync com os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c3124-182">Open **HelloWorldStateful.cs** in *HelloWorldStateful*, which contains hello following RunAsync method:</span></span>

```csharp
protected override async Task RunAsync(CancellationToken cancellationToken)
{
    // TODO: Replace hello following sample code with your own logic
    //       or remove this RunAsync override if it's not needed in your service.

    var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");

    while (true)
    {
        cancellationToken.ThrowIfCancellationRequested();

        using (var tx = this.StateManager.CreateTransaction())
        {
            var result = await myDictionary.TryGetValueAsync(tx, "Counter");

            ServiceEventSource.Current.ServiceMessage(this, "Current Counter Value: {0}",
                result.HasValue ? result.Value.ToString() : "Value does not exist.");

            await myDictionary.AddOrUpdateAsync(tx, "Counter", 0, (key, value) => ++value);

            // If an exception is thrown before calling CommitAsync, hello transaction aborts, all changes are
            // discarded, and nothing is saved toohello secondary replicas.
            await tx.CommitAsync();
        }

        await Task.Delay(TimeSpan.FromSeconds(1), cancellationToken);
    }
```

### <a name="runasync"></a><span data-ttu-id="c3124-183">Runasync com</span><span class="sxs-lookup"><span data-stu-id="c3124-183">RunAsync</span></span>
<span data-ttu-id="c3124-184">`RunAsync()`funciona da mesma forma nos serviços de monitorização de estado e sem monitorização de estado.</span><span class="sxs-lookup"><span data-stu-id="c3124-184">`RunAsync()` operates similarly in stateful and stateless services.</span></span> <span data-ttu-id="c3124-185">No entanto, num serviço com monitorização de estado, plataforma Olá executa tarefas adicionais em seu nome antes de ser executada `RunAsync()`.</span><span class="sxs-lookup"><span data-stu-id="c3124-185">However, in a stateful service, hello platform performs additional work on your behalf before it executes `RunAsync()`.</span></span> <span data-ttu-id="c3124-186">Este trabalho pode incluir a garantir que esse Olá fiável Gestor de estado e fiável coleções são toouse pronto.</span><span class="sxs-lookup"><span data-stu-id="c3124-186">This work can include ensuring that hello Reliable State Manager and Reliable Collections are ready toouse.</span></span>

### <a name="reliable-collections-and-hello-reliable-state-manager"></a><span data-ttu-id="c3124-187">Fiável coleções e Olá fiável Gestor de estado</span><span class="sxs-lookup"><span data-stu-id="c3124-187">Reliable Collections and hello Reliable State Manager</span></span>
```csharp
var myDictionary = await this.StateManager.GetOrAddAsync<IReliableDictionary<string, long>>("myDictionary");
```

<span data-ttu-id="c3124-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) é uma implementação de dicionário que pode utilizar o estado de arquivo de tooreliably no serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-188">[IReliableDictionary](https://msdn.microsoft.com/library/dn971511.aspx) is a dictionary implementation that you can use tooreliably store state in hello service.</span></span> <span data-ttu-id="c3124-189">Com o Service Fabric e fiável de coleções, pode armazenar dados diretamente no seu serviço sem necessidade de Olá para um arquivo persistente externo.</span><span class="sxs-lookup"><span data-stu-id="c3124-189">With Service Fabric and Reliable Collections, you can store data directly in your service without hello need for an external persistent store.</span></span> <span data-ttu-id="c3124-190">Coleções fiáveis tornar os dados de elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="c3124-190">Reliable Collections make your data highly available.</span></span> <span data-ttu-id="c3124-191">Service Fabric executa esta operação através da criação e gestão de vários *réplicas* do seu serviço para si.</span><span class="sxs-lookup"><span data-stu-id="c3124-191">Service Fabric accomplishes this by creating and managing multiple *replicas* of your service for you.</span></span> <span data-ttu-id="c3124-192">Também fornece uma API que deduz complexidades Olá away de gerir as réplicas e os respetivos transições de estado.</span><span class="sxs-lookup"><span data-stu-id="c3124-192">It also provides an API that abstracts away hello complexities of managing those replicas and their state transitions.</span></span>

<span data-ttu-id="c3124-193">Coleções fiáveis podem armazenar qualquer tipo de .NET, incluindo os tipos personalizados, com algumas limitações:</span><span class="sxs-lookup"><span data-stu-id="c3124-193">Reliable Collections can store any .NET type, including your custom types, with a couple of caveats:</span></span>

* <span data-ttu-id="c3124-194">Recursos de infraestrutura de serviço faz com que o seu estado altamente disponível *replicar* Estado em nós e coleções fiável armazenar o disco de toolocal dados em cada réplica.</span><span class="sxs-lookup"><span data-stu-id="c3124-194">Service Fabric makes your state highly available by *replicating* state across nodes, and Reliable Collections store your data toolocal disk on each replica.</span></span> <span data-ttu-id="c3124-195">Isto significa que tudo o que é armazenado em coleções fiável tem de ser *serializável*.</span><span class="sxs-lookup"><span data-stu-id="c3124-195">This means that everything that is stored in Reliable Collections must be *serializable*.</span></span> <span data-ttu-id="c3124-196">Por predefinição, utilize coleções fiável [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) para serialização, por isso, é importante toomake se de que os tipos de [suportado pelo serializador de contrato de dados de Olá](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) quando utilizar a predefinição de Olá serializador.</span><span class="sxs-lookup"><span data-stu-id="c3124-196">By default, Reliable Collections use [DataContract](https://msdn.microsoft.com/library/system.runtime.serialization.datacontractattribute%28v=vs.110%29.aspx) for serialization, so it's important toomake sure that your types are [supported by hello Data Contract Serializer](https://msdn.microsoft.com/library/ms731923%28v=vs.110%29.aspx) when you use hello default serializer.</span></span>
* <span data-ttu-id="c3124-197">Objetos são replicados para elevada disponibilidade ao consolidar transações em coleções fiável.</span><span class="sxs-lookup"><span data-stu-id="c3124-197">Objects are replicated for high availability when you commit transactions on Reliable Collections.</span></span> <span data-ttu-id="c3124-198">Objetos armazenados em coleções fiável são mantidos na memória local no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-198">Objects stored in Reliable Collections are kept in local memory in your service.</span></span> <span data-ttu-id="c3124-199">Isto significa que tem um objeto de toohello de referência local.</span><span class="sxs-lookup"><span data-stu-id="c3124-199">This means that you have a local reference toohello object.</span></span>
  
   <span data-ttu-id="c3124-200">É importante que não mutate locais instâncias desses objetos sem efetuar uma operação de atualização na coleção fiável Olá numa transação.</span><span class="sxs-lookup"><span data-stu-id="c3124-200">It is important that you do not mutate local instances of those objects without performing an update operation on hello reliable collection in a transaction.</span></span> <span data-ttu-id="c3124-201">Isto acontece porque as alterações toolocal instâncias de objetos não serão replicadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="c3124-201">This is because changes toolocal instances of objects will not be replicated automatically.</span></span> <span data-ttu-id="c3124-202">Tem de inserir novamente objeto Olá no dicionário de Olá ou utilize um dos Olá *atualizar* os métodos no dicionário de Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-202">You must re-insert hello object back into hello dictionary or use one of hello *update* methods on hello dictionary.</span></span>

<span data-ttu-id="c3124-203">Olá fiável Gestor de estado gere coleções fiável para si.</span><span class="sxs-lookup"><span data-stu-id="c3124-203">hello Reliable State Manager manages Reliable Collections for you.</span></span> <span data-ttu-id="c3124-204">Pode simplesmente colocar Olá fiável Gestor de estado para uma coleção fiável pelo nome em qualquer altura e em qualquer lugar no seu serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-204">You can simply ask hello Reliable State Manager for a reliable collection by name at any time and at any place in your service.</span></span> <span data-ttu-id="c3124-205">Olá fiável Gestor de estado garante que obtém uma referência de volta.</span><span class="sxs-lookup"><span data-stu-id="c3124-205">hello Reliable State Manager ensures that you get a reference back.</span></span> <span data-ttu-id="c3124-206">Não recomendamos que guarde referências tooreliable instâncias de coleção de variáveis de membros de classe ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="c3124-206">We don't recommended that you save references tooreliable collection instances in class member variables or properties.</span></span> <span data-ttu-id="c3124-207">Especial deve ter cuidado tooensure Olá referência está definida tooan instância sempre no ciclo de vida do Olá serviço.</span><span class="sxs-lookup"><span data-stu-id="c3124-207">Special care must be taken tooensure that hello reference is set tooan instance at all times in hello service lifecycle.</span></span> <span data-ttu-id="c3124-208">Olá fiável Gestor de estado processa este trabalho por si e está otimizado para visitas de repetições.</span><span class="sxs-lookup"><span data-stu-id="c3124-208">hello Reliable State Manager handles this work for you, and it's optimized for repeat visits.</span></span>

### <a name="transactional-and-asynchronous-operations"></a><span data-ttu-id="c3124-209">Operações transacionais e assíncronas</span><span class="sxs-lookup"><span data-stu-id="c3124-209">Transactional and asynchronous operations</span></span>
```C#
using (ITransaction tx = this.StateManager.CreateTransaction())
{
    var result = await myDictionary.TryGetValueAsync(tx, "Counter-1");

    await myDictionary.AddOrUpdateAsync(tx, "Counter-1", 0, (k, v) => ++v);

    await tx.CommitAsync();
}
```

<span data-ttu-id="c3124-210">Coleções fiáveis tem muitas das Olá mesmas operações que os respetivos `System.Collections.Generic` e `System.Collections.Concurrent` homólogos, exceto LINQ.</span><span class="sxs-lookup"><span data-stu-id="c3124-210">Reliable Collections have many of hello same operations that their `System.Collections.Generic` and `System.Collections.Concurrent` counterparts do, except LINQ.</span></span> <span data-ttu-id="c3124-211">As operações em coleções fiável são assíncronas.</span><span class="sxs-lookup"><span data-stu-id="c3124-211">Operations on Reliable Collections are asynchronous.</span></span> <span data-ttu-id="c3124-212">Isto acontece porque as operações de escrita de coleções fiável efetuar tooreplicate de operações de e/s e manter toodisk de dados.</span><span class="sxs-lookup"><span data-stu-id="c3124-212">This is because write operations with Reliable Collections perform I/O operations tooreplicate and persist data toodisk.</span></span>

<span data-ttu-id="c3124-213">As operações de coleção fiável *transacional*, para que pode manter estado consistente em vários coleções fiável e operações.</span><span class="sxs-lookup"><span data-stu-id="c3124-213">Reliable Collection operations are *transactional*, so that you can keep state consistent across multiple Reliable Collections and operations.</span></span> <span data-ttu-id="c3124-214">Por exemplo, pode anular um item de trabalho a partir de uma fila fiável, efetuar uma operação no mesmo e guardar o resultado de Olá num Dictionary fiável, tudo dentro de uma única transação.</span><span class="sxs-lookup"><span data-stu-id="c3124-214">For example, you may dequeue a work item from a Reliable Queue, perform an operation on it, and save hello result in a Reliable Dictionary, all within a single transaction.</span></span> <span data-ttu-id="c3124-215">Esta é tratada como uma operação Atómica e garante que a operação todo Olá terá êxito ou irá reverter operação todo Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-215">This is treated as an atomic operation, and it guarantees that either hello entire operation will succeed or hello entire operation will roll back.</span></span> <span data-ttu-id="c3124-216">Se ocorrer um erro depois de anular o item de Olá, mas antes de guardar o resultado de Olá, transação todo Olá é revertida e item Olá permanece na fila de Olá para processamento.</span><span class="sxs-lookup"><span data-stu-id="c3124-216">If an error occurs after you dequeue hello item but before you save hello result, hello entire transaction is rolled back and hello item remains in hello queue for processing.</span></span>

## <a name="run-hello-application"></a><span data-ttu-id="c3124-217">Executar a aplicação Olá</span><span class="sxs-lookup"><span data-stu-id="c3124-217">Run hello application</span></span>
<span data-ttu-id="c3124-218">Vamos voltar agora toohello *Olámundo* aplicação.</span><span class="sxs-lookup"><span data-stu-id="c3124-218">We now return toohello *HelloWorld* application.</span></span> <span data-ttu-id="c3124-219">Agora pode compilar e implementar os seus serviços.</span><span class="sxs-lookup"><span data-stu-id="c3124-219">You can now build and deploy your services.</span></span> <span data-ttu-id="c3124-220">Quando prime **F5**, a aplicação será cluster local tooyour criados e implementados.</span><span class="sxs-lookup"><span data-stu-id="c3124-220">When you press **F5**, your application will be built and deployed tooyour local cluster.</span></span>

<span data-ttu-id="c3124-221">Após Olá do início em execução, pode ver eventos de rastreio de eventos para o Windows (ETW) Olá gerado por um **eventos de diagnóstico** janela.</span><span class="sxs-lookup"><span data-stu-id="c3124-221">After hello services start running, you can view hello generated Event Tracing for Windows (ETW) events in a **Diagnostic Events** window.</span></span> <span data-ttu-id="c3124-222">Tenha em atenção que os eventos de Olá apresentados são de serviço sem estado Olá e o serviço com estado de Olá na aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="c3124-222">Note that hello events displayed are from both hello stateless service and hello stateful service in hello application.</span></span> <span data-ttu-id="c3124-223">Pode colocar em pausa o fluxo de Olá clicando Olá **colocar em pausa** botão.</span><span class="sxs-lookup"><span data-stu-id="c3124-223">You can pause hello stream by clicking hello **Pause** button.</span></span> <span data-ttu-id="c3124-224">Em seguida, pode examinar os detalhes de Olá de uma mensagem expandindo essa mensagem.</span><span class="sxs-lookup"><span data-stu-id="c3124-224">You can then examine hello details of a message by expanding that message.</span></span>

> [!NOTE]
> <span data-ttu-id="c3124-225">Antes de executar a aplicação Olá, certifique-se de que tem um cluster de desenvolvimento local em execução.</span><span class="sxs-lookup"><span data-stu-id="c3124-225">Before you run hello application, make sure that you have a local development cluster running.</span></span> <span data-ttu-id="c3124-226">Veja Olá [guia de introdução](service-fabric-get-started.md) para obter informações sobre como configurar o ambiente local.</span><span class="sxs-lookup"><span data-stu-id="c3124-226">Check out hello [getting started guide](service-fabric-get-started.md) for information on setting up your local environment.</span></span>
> 
> 

![Ver eventos de diagnóstico no Visual Studio](media/service-fabric-reliable-services-quick-start/hello-stateful-Output.png)

## <a name="next-steps"></a><span data-ttu-id="c3124-228">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c3124-228">Next steps</span></span>
[<span data-ttu-id="c3124-229">Depurar a aplicação de Service Fabric no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="c3124-229">Debug your Service Fabric application in Visual Studio</span></span>](service-fabric-debugging-your-application.md)

[<span data-ttu-id="c3124-230">Começar a: serviços de API Web do Service Fabric com OWIN automática de alojamento</span><span class="sxs-lookup"><span data-stu-id="c3124-230">Get started: Service Fabric Web API services with OWIN self-hosting</span></span>](service-fabric-reliable-services-communication-webapi.md)

[<span data-ttu-id="c3124-231">Saiba mais sobre coleções fiável</span><span class="sxs-lookup"><span data-stu-id="c3124-231">Learn more about Reliable Collections</span></span>](service-fabric-reliable-services-reliable-collections.md)

[<span data-ttu-id="c3124-232">Implementar uma aplicação</span><span class="sxs-lookup"><span data-stu-id="c3124-232">Deploy an application</span></span>](service-fabric-deploy-remove-applications.md)

[<span data-ttu-id="c3124-233">Atualização da aplicação</span><span class="sxs-lookup"><span data-stu-id="c3124-233">Application upgrade</span></span>](service-fabric-application-upgrade.md)

[<span data-ttu-id="c3124-234">Referência para programadores para Reliable Services</span><span class="sxs-lookup"><span data-stu-id="c3124-234">Developer reference for Reliable Services</span></span>](https://msdn.microsoft.com/library/azure/dn706529.aspx)

