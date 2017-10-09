---
title: "aaaAzure monitorização nível de aplicação de recursos de infraestrutura do serviço | Microsoft Docs"
description: "Saiba mais sobre a aplicação e os registos e eventos de nível de serviço utilizada toomonitor e diagnosticar os clusters de Service Fabric do Azure."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 05/26/2017
ms.author: dekapur
ms.openlocfilehash: 4f4da1eaad4b88428eaa3a2100ac25c8a285a727
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-and-service-level-event-and-log-generation"></a><span data-ttu-id="0412c-103">Aplicação e nível de serviço geração de eventos e de registo</span><span class="sxs-lookup"><span data-stu-id="0412c-103">Application and service level event and log generation</span></span>

## <a name="instrumenting-hello-code-with-custom-events"></a><span data-ttu-id="0412c-104">Instrumentação Olá código com eventos personalizados</span><span class="sxs-lookup"><span data-stu-id="0412c-104">Instrumenting hello code with custom events</span></span>

<span data-ttu-id="0412c-105">Instrumentação código Olá é a base de Olá para a maioria dos outros aspetos de monitorizar os seus serviços.</span><span class="sxs-lookup"><span data-stu-id="0412c-105">Instrumenting hello code is hello basis for most other aspects of monitoring your services.</span></span> <span data-ttu-id="0412c-106">Instrumentação é a única forma de Olá que pode saber que algo está errado e toodiagnose que precisa de toobe fixo.</span><span class="sxs-lookup"><span data-stu-id="0412c-106">Instrumentation is hello only way you can know that something is wrong, and toodiagnose what needs toobe fixed.</span></span> <span data-ttu-id="0412c-107">Embora seja tecnicamente possível tooconnect um serviço de produção do depurador tooa, não é uma prática comum.</span><span class="sxs-lookup"><span data-stu-id="0412c-107">Although technically it's possible tooconnect a debugger tooa production service, it's not a common practice.</span></span> <span data-ttu-id="0412c-108">Por isso, ter detalhadas dados de instrumentação é importante.</span><span class="sxs-lookup"><span data-stu-id="0412c-108">So, having detailed instrumentation data is important.</span></span>

<span data-ttu-id="0412c-109">Alguns produtos instrumentem automaticamente o seu código.</span><span class="sxs-lookup"><span data-stu-id="0412c-109">Some products automatically instrument your code.</span></span> <span data-ttu-id="0412c-110">Apesar destas soluções podem funcionar bem, instrumentação manual é quase sempre necessária.</span><span class="sxs-lookup"><span data-stu-id="0412c-110">Although these solutions can work well, manual instrumentation is almost always required.</span></span> <span data-ttu-id="0412c-111">No final de Olá, tem de ter suficiente tooforensically informações aplicação Olá de depuração.</span><span class="sxs-lookup"><span data-stu-id="0412c-111">In hello end, you must have enough information tooforensically debug hello application.</span></span> <span data-ttu-id="0412c-112">Este documento descreve diferentes abordagens tooinstrumenting código, e quando toochoose uma abordagem em vez de outro.</span><span class="sxs-lookup"><span data-stu-id="0412c-112">This document describes different approaches tooinstrumenting your code, and when toochoose one approach over another.</span></span>

## <a name="eventsource"></a><span data-ttu-id="0412c-113">EventSource</span><span class="sxs-lookup"><span data-stu-id="0412c-113">EventSource</span></span>
<span data-ttu-id="0412c-114">Quando cria uma solução de Service Fabric a partir de um modelo no Visual Studio, uma **EventSource**-classe derivada (**ServiceEventSource** ou **ActorEventSource**) é gerado .</span><span class="sxs-lookup"><span data-stu-id="0412c-114">When you create a Service Fabric solution from a template in Visual Studio, an **EventSource**-derived class (**ServiceEventSource** or **ActorEventSource**) is generated.</span></span> <span data-ttu-id="0412c-115">Um modelo é criado, na qual pode adicionar eventos para a aplicação ou serviço.</span><span class="sxs-lookup"><span data-stu-id="0412c-115">A template is created, in which you can add events for your application or service.</span></span> <span data-ttu-id="0412c-116">Olá **EventSource** nome **tem** de ser exclusivo e deve ser alterado de cadeia do modelo de Olá predefinida aminhaempresa -&lt;solução&gt; - &lt; projeto&gt;.</span><span class="sxs-lookup"><span data-stu-id="0412c-116">hello **EventSource** name **must** be unique, and should be renamed from hello default template string MyCompany-&lt;solution&gt;-&lt;project&gt;.</span></span> <span data-ttu-id="0412c-117">Ter vários **EventSource** Olá, as definições que utilizam o mesmo nome faz com que um problema no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0412c-117">Having multiple **EventSource** definitions that use hello same name causes an issue at run time.</span></span> <span data-ttu-id="0412c-118">Cada evento definido tem de ter um identificador exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0412c-118">Each defined event must have a unique identifier.</span></span> <span data-ttu-id="0412c-119">Se um identificador não for exclusivo, ocorre uma falha de tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="0412c-119">If an identifier is not unique, a runtime failure occurs.</span></span> <span data-ttu-id="0412c-120">Algumas organizações preassign intervalos de valores identificadores tooavoid em relação a conflitos entre as equipas de desenvolvimento separados.</span><span class="sxs-lookup"><span data-stu-id="0412c-120">Some organizations preassign ranges of values for identifiers tooavoid conflicts between separate development teams.</span></span> <span data-ttu-id="0412c-121">Para obter mais informações, consulte [blogue de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou Olá [documentação MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span><span class="sxs-lookup"><span data-stu-id="0412c-121">For more information, see [Vance's blog](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) or hello [MSDN documentation](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).</span></span>

### <a name="using-structured-eventsource-events"></a><span data-ttu-id="0412c-122">A utilização de eventos de EventSource estruturados</span><span class="sxs-lookup"><span data-stu-id="0412c-122">Using structured EventSource events</span></span>

<span data-ttu-id="0412c-123">Cada um dos eventos de Olá nos exemplos de código Olá nesta secção são definidos para um cenário específico, por exemplo, quando é registado um tipo de serviço.</span><span class="sxs-lookup"><span data-stu-id="0412c-123">Each of hello events in hello code examples in this section are defined for a specific case, for example, when a service type is registered.</span></span> <span data-ttu-id="0412c-124">Quando definir mensagens por caso de utilização, dados podem ser compactados com texto de Olá erro Olá e pode mais facilmente pesquisar e filtrar com base nos nomes de Olá ou valores de Olá especificado propriedades.</span><span class="sxs-lookup"><span data-stu-id="0412c-124">When you define messages by use case, data can be packaged with hello text of hello error, and you can more easily search and filter based on hello names or values of hello specified properties.</span></span> <span data-ttu-id="0412c-125">Structuring saída de instrumentação Olá torna mais fácil tooconsume, mas requer mais profundamente e hora toodefine um novo evento para cada caso de utilização.</span><span class="sxs-lookup"><span data-stu-id="0412c-125">Structuring hello instrumentation output makes it easier tooconsume, but requires more thought and time toodefine a new event for each use case.</span></span> <span data-ttu-id="0412c-126">Algumas definições de eventos podem ser partilhadas entre aplicações todo Olá.</span><span class="sxs-lookup"><span data-stu-id="0412c-126">Some event definitions can be shared across hello entire application.</span></span> <span data-ttu-id="0412c-127">Por exemplo, um início de método ou parar eventos deverá ser reutilizados em vários serviços dentro de uma aplicação.</span><span class="sxs-lookup"><span data-stu-id="0412c-127">For example, a method start or stop event would be reused across many services within an application.</span></span> <span data-ttu-id="0412c-128">Um serviço de domínio específico, como um sistema de ordem, pode ter um **CreateOrder** evento, o que tem o seu próprio evento exclusivo.</span><span class="sxs-lookup"><span data-stu-id="0412c-128">A domain-specific service, like an order system, might have a **CreateOrder** event, which has its own unique event.</span></span> <span data-ttu-id="0412c-129">Esta abordagem poderá gerar muitos eventos e potencialmente requerem a coordenação de identificadores entre equipas de projeto.</span><span class="sxs-lookup"><span data-stu-id="0412c-129">This approach might generate many events, and potentially require coordination of identifiers across project teams.</span></span> 

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello instance constructor is private tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        // hello ServiceTypeRegistered event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceTypeRegisteredEventId = 3;
        [Event(ServiceTypeRegisteredEventId, Level = EventLevel.Informational, Message = "Service host process {0} registered service type {1}", Keywords = Keywords.ServiceInitialization)]
        public void ServiceTypeRegistered(int hostProcessId, string serviceType)
        {
            WriteEvent(ServiceTypeRegisteredEventId, hostProcessId, serviceType);
        }

        // hello ServiceHostInitializationFailed event contains a unique identifier, an event attribute that defined hello event, and hello code implementation of hello event.
        private const int ServiceHostInitializationFailedEventId = 4;
        [Event(ServiceHostInitializationFailedEventId, Level = EventLevel.Error, Message = "Service host initialization failed", Keywords = Keywords.ServiceInitialization)]
        public void ServiceHostInitializationFailed(string exception)
        {
            WriteEvent(ServiceHostInitializationFailedEventId, exception);
        }
```

### <a name="using-eventsource-generically"></a><span data-ttu-id="0412c-130">Utilizar EventSource genericamente</span><span class="sxs-lookup"><span data-stu-id="0412c-130">Using EventSource generically</span></span>

<span data-ttu-id="0412c-131">Como definir eventos específicos pode ser difícil, muitas pessoas definem alguns eventos com um conjunto comum de parâmetros que geralmente as respetivas informações como uma cadeia de saída.</span><span class="sxs-lookup"><span data-stu-id="0412c-131">Because defining specific events can be difficult, many people define a few events with a common set of parameters that generally output their information as a string.</span></span> <span data-ttu-id="0412c-132">Muito do aspeto Olá estruturado perde-se, e é mais difícil toosearch e filtro Olá os resultados.</span><span class="sxs-lookup"><span data-stu-id="0412c-132">Much of hello structured aspect is lost, and it's more difficult toosearch and filter hello results.</span></span> <span data-ttu-id="0412c-133">Esta abordagem, alguns eventos que normalmente correspondem níveis de registo toohello são definidos.</span><span class="sxs-lookup"><span data-stu-id="0412c-133">In this approach, a few events that usually correspond toohello logging levels are defined.</span></span> <span data-ttu-id="0412c-134">Olá seguinte fragmento define uma mensagem de erro e de depuração:</span><span class="sxs-lookup"><span data-stu-id="0412c-134">hello following snippet defines a debug and error message:</span></span>

```csharp
    [EventSource(Name = "MyCompany-VotingState-VotingStateService")]
    internal sealed class ServiceEventSource : EventSource
    {
        public static readonly ServiceEventSource Current = new ServiceEventSource();

        // hello Instance constructor is private, tooenforce singleton semantics.
        private ServiceEventSource() : base() { }

        ...

        private const int DebugEventId = 10;
        [Event(DebugEventId, Level = EventLevel.Verbose, Message = "{0}")]
        public void Debug(string msg)
        {
            WriteEvent(DebugEventId, msg);
        }

        private const int ErrorEventId = 11;
        [Event(ErrorEventId, Level = EventLevel.Error, Message = "Error: {0} - {1}")]
        public void Error(string error, string msg)
        {
            WriteEvent(ErrorEventId, error, msg);
        }
```

<span data-ttu-id="0412c-135">Utilizar uma versão híbrida do estruturados e genérica instrumentação também pode funcionar bem.</span><span class="sxs-lookup"><span data-stu-id="0412c-135">Using a hybrid of structured and generic instrumentation also can work well.</span></span> <span data-ttu-id="0412c-136">Instrumentação Structured é utilizada para relatórios de erros e de métricas.</span><span class="sxs-lookup"><span data-stu-id="0412c-136">Structured instrumentation is used for reporting errors and metrics.</span></span> <span data-ttu-id="0412c-137">Eventos genéricos podem ser utilizados para Olá detalhada que é o registo consumida pelos engenheiros de resolução de problemas.</span><span class="sxs-lookup"><span data-stu-id="0412c-137">Generic events can be used for hello detailed logging that is consumed by engineers for troubleshooting.</span></span>

## <a name="aspnet-core-logging"></a><span data-ttu-id="0412c-138">O registo do ASP.NET Core</span><span class="sxs-lookup"><span data-stu-id="0412c-138">ASP.NET Core logging</span></span>

<span data-ttu-id="0412c-139">Toocarefully importante planeie como irá instrumentar o seu código.</span><span class="sxs-lookup"><span data-stu-id="0412c-139">It's important toocarefully plan how you will instrument your code.</span></span> <span data-ttu-id="0412c-140">plano de instrumentação direita Olá pode ajudar a evitar potencialmente destabilizing código base e, em seguida, necessitar de código de Olá tooreinstrument.</span><span class="sxs-lookup"><span data-stu-id="0412c-140">hello right instrumentation plan can help you avoid potentially destabilizing your code base, and then needing tooreinstrument hello code.</span></span> <span data-ttu-id="0412c-141">risco tooreduce, pode escolher uma biblioteca de instrumentação como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que faz parte do Microsoft ASP.NET Core.</span><span class="sxs-lookup"><span data-stu-id="0412c-141">tooreduce risk, you can choose an instrumentation library like [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), which is part of Microsoft ASP.NET Core.</span></span> <span data-ttu-id="0412c-142">ASP.NET Core tem um [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que pode utilizar com o fornecedor de Olá à sua escolha, para minimizar o efeito de Olá no código existente.</span><span class="sxs-lookup"><span data-stu-id="0412c-142">ASP.NET Core has an [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface that you can use with hello provider of your choice, while minimizing hello effect on existing code.</span></span> <span data-ttu-id="0412c-143">Pode utilizar o código de Olá em ASP.NET Core no Windows e Linux e, em Olá completa .NET Framework, pelo que o seu código de instrumentação está padronizado.</span><span class="sxs-lookup"><span data-stu-id="0412c-143">You can use hello code in ASP.NET Core on Windows and Linux, and in hello full .NET Framework, so your instrumentation code is standardized.</span></span> <span data-ttu-id="0412c-144">Isto é mais explorou abaixo:</span><span class="sxs-lookup"><span data-stu-id="0412c-144">This is further explored below:</span></span>

### <a name="using-microsoftextensionslogging-in-service-fabric"></a><span data-ttu-id="0412c-145">Utilizar Microsoft.Extensions.Logging no Service Fabric</span><span class="sxs-lookup"><span data-stu-id="0412c-145">Using Microsoft.Extensions.Logging in Service Fabric</span></span>

1. <span data-ttu-id="0412c-146">Adicione Olá projeto de toohello de pacote Microsoft.Extensions.Logging NuGet pretende tooinstrument.</span><span class="sxs-lookup"><span data-stu-id="0412c-146">Add hello Microsoft.Extensions.Logging NuGet package toohello project you want tooinstrument.</span></span> <span data-ttu-id="0412c-147">Além disso, adicione quaisquer pacotes de fornecedor (para um pacote de terceiros, consulte o seguinte exemplo de Olá).</span><span class="sxs-lookup"><span data-stu-id="0412c-147">Also, add any provider packages (for a third-party package, see hello following example).</span></span> <span data-ttu-id="0412c-148">Para obter mais informações, consulte [iniciar sessão ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span><span class="sxs-lookup"><span data-stu-id="0412c-148">For more information, see [Logging in ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).</span></span>
2. <span data-ttu-id="0412c-149">Adicionar um **utilizando** diretiva do ficheiro de serviço Microsoft.Extensions.Logging tooyour.</span><span class="sxs-lookup"><span data-stu-id="0412c-149">Add a **using** directive for Microsoft.Extensions.Logging tooyour service file.</span></span>
3. <span data-ttu-id="0412c-150">Defina uma variável privada dentro da sua classe de serviço.</span><span class="sxs-lookup"><span data-stu-id="0412c-150">Define a private variable within your service class.</span></span>

  ```csharp
  private ILogger _logger = null;

  ```
4. <span data-ttu-id="0412c-151">No construtor de Olá da sua classe de serviço, adicione este código:</span><span class="sxs-lookup"><span data-stu-id="0412c-151">In hello constructor of your service class, add this code:</span></span>

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. <span data-ttu-id="0412c-152">Inicie a instrumentação o código no seu métodos.</span><span class="sxs-lookup"><span data-stu-id="0412c-152">Start instrumenting your code in your methods.</span></span> <span data-ttu-id="0412c-153">Seguem-se alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="0412c-153">Here are a few samples:</span></span>

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a><span data-ttu-id="0412c-154">Utilizar outros fornecedores de registo</span><span class="sxs-lookup"><span data-stu-id="0412c-154">Using other logging providers</span></span>

<span data-ttu-id="0412c-155">Alguns fornecedores de terceiros utilizam a abordagem de Olá descrita Olá anterior a secção, incluindo [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span><span class="sxs-lookup"><span data-stu-id="0412c-155">Some third-party providers use hello approach described in hello preceding section, including [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), and [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging).</span></span> <span data-ttu-id="0412c-156">Pode ligue cada um no registo do ASP.NET Core ou, pode utilizá-las separadamente.</span><span class="sxs-lookup"><span data-stu-id="0412c-156">You can plug each of these into ASP.NET Core logging, or you can use them separately.</span></span> <span data-ttu-id="0412c-157">Serilog tem uma funcionalidade que otimiza todas as mensagens enviadas a partir de um registo.</span><span class="sxs-lookup"><span data-stu-id="0412c-157">Serilog has a feature that enriches all messages sent from a logger.</span></span> <span data-ttu-id="0412c-158">Esta funcionalidade pode ser útil toooutput nome do serviço de Olá, tipo e informações da partição.</span><span class="sxs-lookup"><span data-stu-id="0412c-158">This feature can be useful toooutput hello service name, type, and partition information.</span></span> <span data-ttu-id="0412c-159">toouse desta capacidade no Olá infraestrutura do ASP.NET Core, execute estes passos:</span><span class="sxs-lookup"><span data-stu-id="0412c-159">toouse this capability in hello ASP.NET Core infrastructure, do these steps:</span></span>

1. <span data-ttu-id="0412c-160">Adicione Olá Serilog, Serilog.Extensions.Logging, e pacotes de Serilog.Sinks.Observable NuGet toohello projeto.</span><span class="sxs-lookup"><span data-stu-id="0412c-160">Add hello Serilog, Serilog.Extensions.Logging, and Serilog.Sinks.Observable NuGet packages toohello project.</span></span> <span data-ttu-id="0412c-161">Para o exemplo seguinte Olá, adicione também Serilog.Sinks.Literate.</span><span class="sxs-lookup"><span data-stu-id="0412c-161">For hello next example, also add Serilog.Sinks.Literate.</span></span> <span data-ttu-id="0412c-162">Uma abordagem de melhor é mostrada posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="0412c-162">A better approach is shown later in this article.</span></span>
2. <span data-ttu-id="0412c-163">Serilog, crie uma instância de registo LoggerConfiguration e Olá.</span><span class="sxs-lookup"><span data-stu-id="0412c-163">In Serilog, create a LoggerConfiguration and hello logger instance.</span></span>

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. <span data-ttu-id="0412c-164">Adicione um construtor de serviço do Serilog.ILogger argumento toohello e passar Olá recém-criado logger.</span><span class="sxs-lookup"><span data-stu-id="0412c-164">Add a Serilog.ILogger argument toohello service constructor, and pass hello newly created logger.</span></span>

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. <span data-ttu-id="0412c-165">No construtor do serviço de Olá, adicionar Olá seguinte código, que cria Olá enrichers de propriedade para Olá **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** propriedades do serviço de Olá.</span><span class="sxs-lookup"><span data-stu-id="0412c-165">In hello service constructor, add hello following code, which creates hello property enrichers for hello **ServiceTypeName**, **ServiceName**, **PartitionId**, and **InstanceId** properties of hello service.</span></span> <span data-ttu-id="0412c-166">Também adiciona um toohello enricher de propriedade fábrica de registo do ASP.NET Core, pelo que pode utilizar Microsoft.Extensions.Logging.ILogger no seu código.</span><span class="sxs-lookup"><span data-stu-id="0412c-166">It also adds a property enricher toohello ASP.NET Core logging factory, so you can use Microsoft.Extensions.Logging.ILogger in your code.</span></span>

  ```csharp
  public Stateless(StatelessServiceContext context, Serilog.ILogger serilog)
      : base(context)
  {
      PropertyEnricher[] properties = new PropertyEnricher[]
      {
          new PropertyEnricher("ServiceTypeName", context.ServiceTypeName),
          new PropertyEnricher("ServiceName", context.ServiceName),
          new PropertyEnricher("PartitionId", context.PartitionId),
          new PropertyEnricher("InstanceId", context.ReplicaOrInstanceId),
      };

      serilog.ForContext(properties);

      _logger = new LoggerFactory().AddSerilog(serilog.ForContext(properties)).CreateLogger<Stateless>();
  }
  ```

5. <span data-ttu-id="0412c-167">Código de Olá instrumento Olá mesmo como se estava a utilizar o ASP.NET Core sem Serilog.</span><span class="sxs-lookup"><span data-stu-id="0412c-167">Instrument hello code hello same as if you were using ASP.NET Core without Serilog.</span></span>

  >[!NOTE]
  ><span data-ttu-id="0412c-168">Recomendamos que não utilize Olá estática Log.Logger com Olá anterior exemplo.</span><span class="sxs-lookup"><span data-stu-id="0412c-168">We recommend that you don't use hello static Log.Logger with hello preceding example.</span></span> <span data-ttu-id="0412c-169">Service Fabric pode alojar várias instâncias Olá mesmo do serviço de tipo dentro de um único processo.</span><span class="sxs-lookup"><span data-stu-id="0412c-169">Service Fabric can host multiple instances of hello same service type within a single process.</span></span> <span data-ttu-id="0412c-170">Se utilizar Olá Log.Logger estático, o último escritor de Olá de enrichers de propriedade Olá mostrará valores para todas as instâncias que estão em execução.</span><span class="sxs-lookup"><span data-stu-id="0412c-170">If you use hello static Log.Logger, hello last writer of hello property enrichers will show values for all instances that are running.</span></span> <span data-ttu-id="0412c-171">Este é um motivo por que razão a variável de _logger Olá é uma variável de membro privado de classe de serviço Olá.</span><span class="sxs-lookup"><span data-stu-id="0412c-171">This is one reason why hello _logger variable is a private member variable of hello service class.</span></span> <span data-ttu-id="0412c-172">Além disso, tem de se Olá _logger toocommon disponíveis código, o qual pode ser utilizado em serviços.</span><span class="sxs-lookup"><span data-stu-id="0412c-172">Also, you must make hello _logger available toocommon code, which might be used across services.</span></span>

## <a name="choosing-a-logging-provider"></a><span data-ttu-id="0412c-173">Escolher um fornecedor de registo</span><span class="sxs-lookup"><span data-stu-id="0412c-173">Choosing a logging provider</span></span>

<span data-ttu-id="0412c-174">Se a aplicação depende de elevado desempenho, **EventSource** é normalmente uma boa abordagem.</span><span class="sxs-lookup"><span data-stu-id="0412c-174">If your application relies on high performance, **EventSource** is usually a good approach.</span></span> <span data-ttu-id="0412c-175">**EventSource** *geralmente* utiliza menos recursos e efetua melhor do que o registo do ASP.NET Core ou qualquer uma das soluções de terceiros disponíveis Olá.</span><span class="sxs-lookup"><span data-stu-id="0412c-175">**EventSource** *generally* uses fewer resources and performs better than ASP.NET Core logging or any of hello available third-party solutions.</span></span>  <span data-ttu-id="0412c-176">Esta operação não é um problema para vários serviços, mas se o seu serviço é desempenho orientados, utilizando **EventSource** poderá ser uma melhor opção.</span><span class="sxs-lookup"><span data-stu-id="0412c-176">This isn't an issue for many services, but if your service is performance-oriented, using **EventSource** might be a better choice.</span></span> <span data-ttu-id="0412c-177">No entanto, tooget destas vantagens do estruturados de registo, **EventSource** requer um investimento superior da sua equipa de engenharia.</span><span class="sxs-lookup"><span data-stu-id="0412c-177">However, tooget these benefits of structured logging, **EventSource** requires a larger investment from your engineering team.</span></span> <span data-ttu-id="0412c-178">Se possível, efetue um protótipo rápido de algumas opções de registo e, em seguida, escolha Olá que melhor se adeque às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="0412c-178">If possible, do a quick prototype of a few logging options, and then choose hello one that best meets your needs.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0412c-179">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0412c-179">Next steps</span></span>

<span data-ttu-id="0412c-180">Assim que tiver escolhido o tooinstrument do fornecedor de registo as suas aplicações e serviços, os registos e eventos necessário toobe agregado antes que podem ser enviadas tooany plataforma de análise.</span><span class="sxs-lookup"><span data-stu-id="0412c-180">Once you have chosen your logging provider tooinstrument your applications and services, your logs and events need toobe aggregated before they can be sent tooany analysis platform.</span></span> <span data-ttu-id="0412c-181">Leia sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter compreender alguns dos Olá recomendado opções.</span><span class="sxs-lookup"><span data-stu-id="0412c-181">Read about [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) and [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter understand some of hello recommended options.</span></span>
