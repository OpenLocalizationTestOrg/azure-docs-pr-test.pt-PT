---
title: "aaaCreate sua primeira baseado em ator Azure microsserviço em c# | Microsoft Docs"
description: "Este tutorial orienta-o pelos passos de Olá da criação, depurar e implementar um serviço baseado em ator simple utilizando o serviço de recursos de infraestrutura Reliable Actors."
services: service-fabric
documentationcenter: .net
author: vturecek
manager: timlt
editor: 
ms.assetid: d4aebe72-1551-4062-b1eb-54d83297f139
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/29/2017
ms.author: vturecek
ms.openlocfilehash: ab4f75bef0adb6e70f0ead587475b3fb51e6e6a5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-reliable-actors"></a><span data-ttu-id="6e33b-103">Introdução a Reliable Actors</span><span class="sxs-lookup"><span data-stu-id="6e33b-103">Getting started with Reliable Actors</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6e33b-104">C# no Windows</span><span class="sxs-lookup"><span data-stu-id="6e33b-104">C# on Windows</span></span>](service-fabric-reliable-actors-get-started.md)
> * [<span data-ttu-id="6e33b-105">Java em Linux</span><span class="sxs-lookup"><span data-stu-id="6e33b-105">Java on Linux</span></span>](service-fabric-reliable-actors-get-started-java.md)
> 
> 

<span data-ttu-id="6e33b-106">Este artigo explica Olá Noções básicas do Azure Service Fabric Reliable Actors e explica-lhe como criar, depurar e implementar uma aplicação simples de Ator fiável no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e33b-106">This article explains hello basics of Azure Service Fabric Reliable Actors and walks you through creating, debugging, and deploying a simple Reliable Actor application in Visual Studio.</span></span>

## <a name="installation-and-setup"></a><span data-ttu-id="6e33b-107">Instalação e configuração</span><span class="sxs-lookup"><span data-stu-id="6e33b-107">Installation and setup</span></span>
<span data-ttu-id="6e33b-108">Antes de começar, certifique-se de que tem o ambiente de desenvolvimento do Service Fabric Olá que configurar no seu computador.</span><span class="sxs-lookup"><span data-stu-id="6e33b-108">Before you start, ensure that you have hello Service Fabric development environment set up on your machine.</span></span>
<span data-ttu-id="6e33b-109">Se precisar de tooset-lo, consulte instruções detalhadas sobre [como tooset configurar o ambiente de desenvolvimento de Olá](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6e33b-109">If you need tooset it up, see detailed instructions on [how tooset up hello development environment](service-fabric-get-started.md).</span></span>

## <a name="basic-concepts"></a><span data-ttu-id="6e33b-110">Conceitos básicos</span><span class="sxs-lookup"><span data-stu-id="6e33b-110">Basic concepts</span></span>
<span data-ttu-id="6e33b-111">tooget começar Reliable Actors, apenas é necessário toounderstand alguns conceitos básicos:</span><span class="sxs-lookup"><span data-stu-id="6e33b-111">tooget started with Reliable Actors, you only need toounderstand a few basic concepts:</span></span>

* <span data-ttu-id="6e33b-112">**Serviço de atores**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-112">**Actor service**.</span></span> <span data-ttu-id="6e33b-113">Reliable Actors são reunidas em Reliable Services que podem ser implementados numa infraestrutura de Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-113">Reliable Actors are packaged in Reliable Services that can be deployed in hello Service Fabric infrastructure.</span></span> <span data-ttu-id="6e33b-114">Instâncias de ator são ativadas numa instância de serviço com nome.</span><span class="sxs-lookup"><span data-stu-id="6e33b-114">Actor instances are activated in a named service instance.</span></span>
* <span data-ttu-id="6e33b-115">**Registo de ator**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-115">**Actor registration**.</span></span> <span data-ttu-id="6e33b-116">Como com Reliable Services, um serviço de Atores fiável tem toobe registado com o tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e33b-116">As with Reliable Services, a Reliable Actor service needs toobe registered with hello Service Fabric runtime.</span></span> <span data-ttu-id="6e33b-117">Além disso, o tipo de ator Olá deve toobe registado com o tempo de execução do Olá Ator.</span><span class="sxs-lookup"><span data-stu-id="6e33b-117">In addition, hello actor type needs toobe registered with hello Actor runtime.</span></span>
* <span data-ttu-id="6e33b-118">**Interface de ator**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-118">**Actor interface**.</span></span> <span data-ttu-id="6e33b-119">interface de ator Olá é utilizado toodefine uma interface pública com tipo seguro de um ator.</span><span class="sxs-lookup"><span data-stu-id="6e33b-119">hello actor interface is used toodefine a strongly typed public interface of an actor.</span></span> <span data-ttu-id="6e33b-120">Na terminologia de modelo de Ator fiável Olá, a interface de ator Olá define Olá tipos de mensagens hello ator podem compreender e processar.</span><span class="sxs-lookup"><span data-stu-id="6e33b-120">In hello Reliable Actor model terminology, hello actor interface defines hello types of messages that hello actor can understand and process.</span></span> <span data-ttu-id="6e33b-121">interface de ator Olá é utilizado por outros atores e aplicações cliente demasiado "de envio" (no modo assíncrono) ator toohello de mensagens.</span><span class="sxs-lookup"><span data-stu-id="6e33b-121">hello actor interface is used by other actors and client applications too"send" (asynchronously) messages toohello actor.</span></span> <span data-ttu-id="6e33b-122">Reliable Actors podem implementar várias interfaces.</span><span class="sxs-lookup"><span data-stu-id="6e33b-122">Reliable Actors can implement multiple interfaces.</span></span>
* <span data-ttu-id="6e33b-123">**Classe de ActorProxy**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-123">**ActorProxy class**.</span></span> <span data-ttu-id="6e33b-124">Olá ActorProxy classe é utilizada pelo cliente aplicações tooinvoke Olá métodos expostos através da interface de ator Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-124">hello ActorProxy class is used by client applications tooinvoke hello methods exposed through hello actor interface.</span></span> <span data-ttu-id="6e33b-125">Olá ActorProxy classe fornece duas funcionalidades importantes:</span><span class="sxs-lookup"><span data-stu-id="6e33b-125">hello ActorProxy class provides two important functionalities:</span></span>
  
  * <span data-ttu-id="6e33b-126">Resolução de nomes: é capaz de toolocate actor de Olá num cluster de Olá (localizar Olá nó de cluster olá onde está alojado).</span><span class="sxs-lookup"><span data-stu-id="6e33b-126">Name resolution: It is able toolocate hello actor in hello cluster (find hello node of hello cluster where it is hosted).</span></span>
  * <span data-ttu-id="6e33b-127">Processamento de falhas: pode repetir invocações de método e novamente resolver a localização de atores de Olá depois, por exemplo, uma falha de que necessita de Olá ator toobe relocalizada tooanother de nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-127">Failure handling: It can retry method invocations and re-resolve hello actor location after, for example, a failure that requires hello actor toobe relocated tooanother node in hello cluster.</span></span>

<span data-ttu-id="6e33b-128">Olá seguintes regras que dizem respeito tooactor interfaces é mencionar:</span><span class="sxs-lookup"><span data-stu-id="6e33b-128">hello following rules that pertain tooactor interfaces are worth mentioning:</span></span>

* <span data-ttu-id="6e33b-129">Métodos de interface de ator não podem estar sobrecarregados.</span><span class="sxs-lookup"><span data-stu-id="6e33b-129">Actor interface methods cannot be overloaded.</span></span>
* <span data-ttu-id="6e33b-130">Interface de ator métodos não pode ter out, ref ou parâmetros opcionais.</span><span class="sxs-lookup"><span data-stu-id="6e33b-130">Actor interface methods must not have out, ref, or optional parameters.</span></span>
* <span data-ttu-id="6e33b-131">Interfaces genéricas não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="6e33b-131">Generic interfaces are not supported.</span></span>

## <a name="create-a-new-project-in-visual-studio"></a><span data-ttu-id="6e33b-132">Criar um novo projeto no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6e33b-132">Create a new project in Visual Studio</span></span>
<span data-ttu-id="6e33b-133">Inicie o Visual Studio 2015 ou Visual Studio 2017 como administrador e criar um novo projeto de aplicação de Service Fabric:</span><span class="sxs-lookup"><span data-stu-id="6e33b-133">Launch Visual Studio 2015 or Visual Studio 2017 as an administrator, and create a new Service Fabric application project:</span></span>

![Ferramentas do Service Fabric para Visual Studio – novo projeto][1]

<span data-ttu-id="6e33b-135">Na caixa de diálogo seguinte Olá, pode escolher tipo de Olá do projeto que pretende que o toocreate.</span><span class="sxs-lookup"><span data-stu-id="6e33b-135">In hello next dialog box, you can choose hello type of project that you want toocreate.</span></span>

![Modelos de projeto de Service Fabric][5]

<span data-ttu-id="6e33b-137">Para o projeto de Olámundo Olá, vamos a utilizar o serviço de Service Fabric Reliable Actors Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-137">For hello HelloWorld project, let's use hello Service Fabric Reliable Actors service.</span></span>

<span data-ttu-id="6e33b-138">Depois de ter criado solução Olá, deverá ver Olá seguir a estrutura:</span><span class="sxs-lookup"><span data-stu-id="6e33b-138">After you have created hello solution, you should see hello following structure:</span></span>

![Estrutura do projeto de Service Fabric][2]

## <a name="reliable-actors-basic-building-blocks"></a><span data-ttu-id="6e33b-140">Fiáveis blocos modulares básicos Actors</span><span class="sxs-lookup"><span data-stu-id="6e33b-140">Reliable Actors basic building blocks</span></span>
<span data-ttu-id="6e33b-141">Uma solução de Reliable Actors típica é composta por três projetos:</span><span class="sxs-lookup"><span data-stu-id="6e33b-141">A typical Reliable Actors solution is composed of three projects:</span></span>

* <span data-ttu-id="6e33b-142">**projeto de aplicação Olá (MyActorApplication)**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-142">**hello application project (MyActorApplication)**.</span></span> <span data-ttu-id="6e33b-143">Este é o projeto de Olá que todos os serviços de Olá em conjunto para a implementação de pacotes.</span><span class="sxs-lookup"><span data-stu-id="6e33b-143">This is hello project that packages all of hello services together for deployment.</span></span> <span data-ttu-id="6e33b-144">Contém Olá *ApplicationManifest.xml* e scripts do PowerShell para gerir a aplicação Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-144">It contains hello *ApplicationManifest.xml* and PowerShell scripts for managing hello application.</span></span>
* <span data-ttu-id="6e33b-145">**o projeto de interface de Olá (MyActor.Interfaces)**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-145">**hello interface project (MyActor.Interfaces)**.</span></span> <span data-ttu-id="6e33b-146">Este é o projeto de Olá que contém uma definição de interface de Olá para ator Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-146">This is hello project that contains hello interface definition for hello actor.</span></span> <span data-ttu-id="6e33b-147">No projeto de MyActor.Interfaces Olá, pode definir interfaces de Olá que serão utilizadas pelo atores Olá na solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-147">In hello MyActor.Interfaces project, you can define hello interfaces that will be used by hello actors in hello solution.</span></span> <span data-ttu-id="6e33b-148">As interfaces de ator podem ser definidas em qualquer projeto com qualquer nome, no entanto, a interface Olá define o contrato de ator Olá que é partilhado por clientes de Olá chamar ator Olá, pelo que, normalmente, faz sentido toodefine e de implementação de ator Olá-la numa assemblagem que é separar da implementação de ator Olá e pode ser partilhado por vários outros projetos.</span><span class="sxs-lookup"><span data-stu-id="6e33b-148">Your actor interfaces can be defined in any project with any name, however hello interface defines hello actor contract that is shared by hello actor implementation and hello clients calling hello actor, so it typically makes sense toodefine it in an assembly that is separate from hello actor implementation and can be shared by multiple other projects.</span></span>

```csharp
public interface IMyActor : IActor
{
    Task<string> HelloWorld();
}
```

* <span data-ttu-id="6e33b-149">**projeto de serviço de atores Olá (MyActor)**.</span><span class="sxs-lookup"><span data-stu-id="6e33b-149">**hello actor service project (MyActor)**.</span></span> <span data-ttu-id="6e33b-150">Isto é Olá projeto utilizado toodefine Olá Service Fabric serviço actor de Olá de toohost contínuo.</span><span class="sxs-lookup"><span data-stu-id="6e33b-150">This is hello project used toodefine hello Service Fabric service that is going toohost hello actor.</span></span> <span data-ttu-id="6e33b-151">Implementação de Olá de ator Olá nele contidos.</span><span class="sxs-lookup"><span data-stu-id="6e33b-151">It contains hello implementation of hello actor.</span></span> <span data-ttu-id="6e33b-152">Uma implementação de atores é uma classe que deriva de um tipo base Olá `Actor` e implementa Olá interfaces que estão definidas no projeto de MyActor.Interfaces Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-152">An actor implementation is a class that derives from hello base type `Actor` and implements hello interface(s) that are defined in hello MyActor.Interfaces project.</span></span> <span data-ttu-id="6e33b-153">Uma classe de ator também tem de implementar um construtor que aceite um `ActorService` instância e um `ActorId` e transmite-os toohello base `Actor` classe.</span><span class="sxs-lookup"><span data-stu-id="6e33b-153">An actor class must also implement a constructor that accepts an `ActorService` instance and an `ActorId` and passes them toohello base `Actor` class.</span></span> <span data-ttu-id="6e33b-154">Isto permite a inserção de dependências de construtor de dependências de plataforma.</span><span class="sxs-lookup"><span data-stu-id="6e33b-154">This allows for constructor dependency injection of platform dependencies.</span></span>

```csharp
[StatePersistence(StatePersistence.Persisted)]
class MyActor : Actor, IMyActor
{
    public MyActor(ActorService actorService, ActorId actorId)
        : base(actorService, actorId)
    {
    }

    public Task<string> HelloWorld()
    {
        return Task.FromResult("Hello world!");
    }
}
```

<span data-ttu-id="6e33b-155">serviço de atores Olá tem de ser registado com um tipo de serviço no tempo de execução do Olá Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="6e33b-155">hello actor service must be registered with a service type in hello Service Fabric runtime.</span></span> <span data-ttu-id="6e33b-156">Na ordem de Olá toorun do serviço de Atores as instâncias de ator, o tipo de ator também tem de ser registado com Olá serviço de Atores.</span><span class="sxs-lookup"><span data-stu-id="6e33b-156">In order for hello Actor Service toorun your actor instances, your actor type must also be registered with hello Actor Service.</span></span> <span data-ttu-id="6e33b-157">Olá `ActorRuntime` método de registo efetua este trabalho de atores.</span><span class="sxs-lookup"><span data-stu-id="6e33b-157">hello `ActorRuntime` registration method performs this work for actors.</span></span>

```csharp
internal static class Program
{
    private static void Main()
    {
        try
        {
            ActorRuntime.RegisterActorAsync<MyActor>(
                (context, actorType) => new ActorService(context, actorType, () => new MyActor())).GetAwaiter().GetResult();

            Thread.Sleep(Timeout.Infinite);
        }
        catch (Exception e)
        {
            ActorEventSource.Current.ActorHostInitializationFailed(e.ToString());
            throw;
        }
    }
}

```

<span data-ttu-id="6e33b-158">Se iniciar a partir de um novo projeto no Visual Studio e tiver apenas uma definição de ator, registo Olá é incluído por predefinição no código Olá que gera o Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6e33b-158">If you start from a new project in Visual Studio and you have only one actor definition, hello registration is included by default in hello code that Visual Studio generates.</span></span> <span data-ttu-id="6e33b-159">Se definir outros atores no serviço de Olá, terá de registo de ator tooadd Olá utilizando:</span><span class="sxs-lookup"><span data-stu-id="6e33b-159">If you define other actors in hello service, you need tooadd hello actor registration by using:</span></span>

```csharp
 ActorRuntime.RegisterActorAsync<MyOtherActor>();

```

> [!TIP]
> <span data-ttu-id="6e33b-160">Olá Atores do Service Fabric runtime emite algumas [eventos e contadores de desempenho relacionados com métodos tooactor](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span><span class="sxs-lookup"><span data-stu-id="6e33b-160">hello Service Fabric Actors runtime emits some [events and performance counters related tooactor methods](service-fabric-reliable-actors-diagnostics.md#actor-method-events-and-performance-counters).</span></span> <span data-ttu-id="6e33b-161">Estes são úteis em diagnóstico e monitorização do desempenho.</span><span class="sxs-lookup"><span data-stu-id="6e33b-161">They are useful in diagnostics and performance monitoring.</span></span>
> 
> 

## <a name="debugging"></a><span data-ttu-id="6e33b-162">Depuração</span><span class="sxs-lookup"><span data-stu-id="6e33b-162">Debugging</span></span>
<span data-ttu-id="6e33b-163">ferramentas do Service Fabric Olá para Visual Studio suportam a depuração no seu computador local.</span><span class="sxs-lookup"><span data-stu-id="6e33b-163">hello Service Fabric tools for Visual Studio support debugging on your local machine.</span></span> <span data-ttu-id="6e33b-164">Pode iniciar uma sessão de depuração, atingir Olá tecla F5.</span><span class="sxs-lookup"><span data-stu-id="6e33b-164">You can start a debugging session by hitting hello F5 key.</span></span> <span data-ttu-id="6e33b-165">Visual Studio cria (se necessário) pacotes.</span><span class="sxs-lookup"><span data-stu-id="6e33b-165">Visual Studio builds (if necessary) packages.</span></span> <span data-ttu-id="6e33b-166">Também implementa a aplicação Olá no cluster de Service Fabric local Olá e anexa depurador Olá.</span><span class="sxs-lookup"><span data-stu-id="6e33b-166">It also deploys hello application on hello local Service Fabric cluster and attaches hello debugger.</span></span>

<span data-ttu-id="6e33b-167">Durante o processo de implementação de Olá, pode ver o progresso de Olá na Olá **saída** janela.</span><span class="sxs-lookup"><span data-stu-id="6e33b-167">During hello deployment process, you can see hello progress in hello **Output** window.</span></span>

![Janela de saída de depuração Service Fabric][3]

## <a name="next-steps"></a><span data-ttu-id="6e33b-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6e33b-169">Next steps</span></span>
<span data-ttu-id="6e33b-170">Saiba mais sobre [como Reliable Actors utilizar plataforma de Service Fabric Olá](service-fabric-reliable-actors-platform.md).</span><span class="sxs-lookup"><span data-stu-id="6e33b-170">Learn more about [how Reliable Actors use hello Service Fabric platform](service-fabric-reliable-actors-platform.md).</span></span>

<!--Image references-->
[1]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject.PNG
[2]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-projectstructure.PNG
[3]: ./media/service-fabric-reliable-actors-get-started/debugging-output.PNG
[4]: ./media/service-fabric-reliable-actors-get-started/vs-context-menu.png
[5]: ./media/service-fabric-reliable-actors-get-started/reliable-actors-newproject1.PNG
