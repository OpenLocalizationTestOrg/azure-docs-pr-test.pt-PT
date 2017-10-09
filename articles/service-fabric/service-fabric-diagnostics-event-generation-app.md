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
# <a name="application-and-service-level-event-and-log-generation"></a>Aplicação e nível de serviço geração de eventos e de registo

## <a name="instrumenting-hello-code-with-custom-events"></a>Instrumentação Olá código com eventos personalizados

Instrumentação código Olá é a base de Olá para a maioria dos outros aspetos de monitorizar os seus serviços. Instrumentação é a única forma de Olá que pode saber que algo está errado e toodiagnose que precisa de toobe fixo. Embora seja tecnicamente possível tooconnect um serviço de produção do depurador tooa, não é uma prática comum. Por isso, ter detalhadas dados de instrumentação é importante.

Alguns produtos instrumentem automaticamente o seu código. Apesar destas soluções podem funcionar bem, instrumentação manual é quase sempre necessária. No final de Olá, tem de ter suficiente tooforensically informações aplicação Olá de depuração. Este documento descreve diferentes abordagens tooinstrumenting código, e quando toochoose uma abordagem em vez de outro.

## <a name="eventsource"></a>EventSource
Quando cria uma solução de Service Fabric a partir de um modelo no Visual Studio, uma **EventSource**-classe derivada (**ServiceEventSource** ou **ActorEventSource**) é gerado . Um modelo é criado, na qual pode adicionar eventos para a aplicação ou serviço. Olá **EventSource** nome **tem** de ser exclusivo e deve ser alterado de cadeia do modelo de Olá predefinida aminhaempresa -&lt;solução&gt; - &lt; projeto&gt;. Ter vários **EventSource** Olá, as definições que utilizam o mesmo nome faz com que um problema no tempo de execução. Cada evento definido tem de ter um identificador exclusivo. Se um identificador não for exclusivo, ocorre uma falha de tempo de execução. Algumas organizações preassign intervalos de valores identificadores tooavoid em relação a conflitos entre as equipas de desenvolvimento separados. Para obter mais informações, consulte [blogue de Vance](https://blogs.msdn.microsoft.com/vancem/2012/07/09/introduction-tutorial-logging-etw-events-in-c-system-diagnostics-tracing-eventsource/) ou Olá [documentação MSDN](https://msdn.microsoft.com/library/dn774985(v=pandp.20).aspx).

### <a name="using-structured-eventsource-events"></a>A utilização de eventos de EventSource estruturados

Cada um dos eventos de Olá nos exemplos de código Olá nesta secção são definidos para um cenário específico, por exemplo, quando é registado um tipo de serviço. Quando definir mensagens por caso de utilização, dados podem ser compactados com texto de Olá erro Olá e pode mais facilmente pesquisar e filtrar com base nos nomes de Olá ou valores de Olá especificado propriedades. Structuring saída de instrumentação Olá torna mais fácil tooconsume, mas requer mais profundamente e hora toodefine um novo evento para cada caso de utilização. Algumas definições de eventos podem ser partilhadas entre aplicações todo Olá. Por exemplo, um início de método ou parar eventos deverá ser reutilizados em vários serviços dentro de uma aplicação. Um serviço de domínio específico, como um sistema de ordem, pode ter um **CreateOrder** evento, o que tem o seu próprio evento exclusivo. Esta abordagem poderá gerar muitos eventos e potencialmente requerem a coordenação de identificadores entre equipas de projeto. 

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

### <a name="using-eventsource-generically"></a>Utilizar EventSource genericamente

Como definir eventos específicos pode ser difícil, muitas pessoas definem alguns eventos com um conjunto comum de parâmetros que geralmente as respetivas informações como uma cadeia de saída. Muito do aspeto Olá estruturado perde-se, e é mais difícil toosearch e filtro Olá os resultados. Esta abordagem, alguns eventos que normalmente correspondem níveis de registo toohello são definidos. Olá seguinte fragmento define uma mensagem de erro e de depuração:

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

Utilizar uma versão híbrida do estruturados e genérica instrumentação também pode funcionar bem. Instrumentação Structured é utilizada para relatórios de erros e de métricas. Eventos genéricos podem ser utilizados para Olá detalhada que é o registo consumida pelos engenheiros de resolução de problemas.

## <a name="aspnet-core-logging"></a>O registo do ASP.NET Core

Toocarefully importante planeie como irá instrumentar o seu código. plano de instrumentação direita Olá pode ajudar a evitar potencialmente destabilizing código base e, em seguida, necessitar de código de Olá tooreinstrument. risco tooreduce, pode escolher uma biblioteca de instrumentação como [Microsoft.Extensions.Logging](https://www.nuget.org/packages/Microsoft.Extensions.Logging/), que faz parte do Microsoft ASP.NET Core. ASP.NET Core tem um [ILogger](https://docs.microsoft.com/aspnet/core/api/microsoft.extensions.logging.ilogger) interface que pode utilizar com o fornecedor de Olá à sua escolha, para minimizar o efeito de Olá no código existente. Pode utilizar o código de Olá em ASP.NET Core no Windows e Linux e, em Olá completa .NET Framework, pelo que o seu código de instrumentação está padronizado. Isto é mais explorou abaixo:

### <a name="using-microsoftextensionslogging-in-service-fabric"></a>Utilizar Microsoft.Extensions.Logging no Service Fabric

1. Adicione Olá projeto de toohello de pacote Microsoft.Extensions.Logging NuGet pretende tooinstrument. Além disso, adicione quaisquer pacotes de fornecedor (para um pacote de terceiros, consulte o seguinte exemplo de Olá). Para obter mais informações, consulte [iniciar sessão ASP.NET Core](https://docs.microsoft.com/aspnet/core/fundamentals/logging).
2. Adicionar um **utilizando** diretiva do ficheiro de serviço Microsoft.Extensions.Logging tooyour.
3. Defina uma variável privada dentro da sua classe de serviço.

  ```csharp
  private ILogger _logger = null;

  ```
4. No construtor de Olá da sua classe de serviço, adicione este código:

  ```csharp
  _logger = new LoggerFactory().CreateLogger<Stateless>();

  ```
5. Inicie a instrumentação o código no seu métodos. Seguem-se alguns exemplos:

  ```csharp
  _logger.LogDebug("Debug-level event from Microsoft.Logging");
  _logger.LogInformation("Informational-level event from Microsoft.Logging");

  // In this variant, we're adding structured properties RequestName and Duration, which have values MyRequest and hello duration of hello request.
  // Later in hello article, we discuss why this step is useful.
  _logger.LogInformation("{RequestName} {Duration}", "MyRequest", requestDuration);

  ```

## <a name="using-other-logging-providers"></a>Utilizar outros fornecedores de registo

Alguns fornecedores de terceiros utilizam a abordagem de Olá descrita Olá anterior a secção, incluindo [Serilog](https://serilog.net/), [NLog](http://nlog-project.org/), e [Loggr](https://github.com/imobile3/Loggr.Extensions.Logging). Pode ligue cada um no registo do ASP.NET Core ou, pode utilizá-las separadamente. Serilog tem uma funcionalidade que otimiza todas as mensagens enviadas a partir de um registo. Esta funcionalidade pode ser útil toooutput nome do serviço de Olá, tipo e informações da partição. toouse desta capacidade no Olá infraestrutura do ASP.NET Core, execute estes passos:

1. Adicione Olá Serilog, Serilog.Extensions.Logging, e pacotes de Serilog.Sinks.Observable NuGet toohello projeto. Para o exemplo seguinte Olá, adicione também Serilog.Sinks.Literate. Uma abordagem de melhor é mostrada posteriormente neste artigo.
2. Serilog, crie uma instância de registo LoggerConfiguration e Olá.

  ```csharp
  Log.Logger = new LoggerConfiguration().WriteTo.LiterateConsole().CreateLogger();
  ```

3. Adicione um construtor de serviço do Serilog.ILogger argumento toohello e passar Olá recém-criado logger.

  ```csharp
  ServiceRuntime.RegisterServiceAsync("StatelessType", context => new Stateless(context, Log.Logger)).GetAwaiter().GetResult();
  ```

4. No construtor do serviço de Olá, adicionar Olá seguinte código, que cria Olá enrichers de propriedade para Olá **ServiceTypeName**, **ServiceName**, **PartitionId**e  **InstanceId** propriedades do serviço de Olá. Também adiciona um toohello enricher de propriedade fábrica de registo do ASP.NET Core, pelo que pode utilizar Microsoft.Extensions.Logging.ILogger no seu código.

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

5. Código de Olá instrumento Olá mesmo como se estava a utilizar o ASP.NET Core sem Serilog.

  >[!NOTE]
  >Recomendamos que não utilize Olá estática Log.Logger com Olá anterior exemplo. Service Fabric pode alojar várias instâncias Olá mesmo do serviço de tipo dentro de um único processo. Se utilizar Olá Log.Logger estático, o último escritor de Olá de enrichers de propriedade Olá mostrará valores para todas as instâncias que estão em execução. Este é um motivo por que razão a variável de _logger Olá é uma variável de membro privado de classe de serviço Olá. Além disso, tem de se Olá _logger toocommon disponíveis código, o qual pode ser utilizado em serviços.

## <a name="choosing-a-logging-provider"></a>Escolher um fornecedor de registo

Se a aplicação depende de elevado desempenho, **EventSource** é normalmente uma boa abordagem. **EventSource** *geralmente* utiliza menos recursos e efetua melhor do que o registo do ASP.NET Core ou qualquer uma das soluções de terceiros disponíveis Olá.  Esta operação não é um problema para vários serviços, mas se o seu serviço é desempenho orientados, utilizando **EventSource** poderá ser uma melhor opção. No entanto, tooget destas vantagens do estruturados de registo, **EventSource** requer um investimento superior da sua equipa de engenharia. Se possível, efetue um protótipo rápido de algumas opções de registo e, em seguida, escolha Olá que melhor se adeque às suas necessidades.

## <a name="next-steps"></a>Passos seguintes

Assim que tiver escolhido o tooinstrument do fornecedor de registo as suas aplicações e serviços, os registos e eventos necessário toobe agregado antes que podem ser enviadas tooany plataforma de análise. Leia sobre [EventFlow](service-fabric-diagnostics-event-aggregation-eventflow.md) e [WAD](service-fabric-diagnostics-event-aggregation-wad.md) toobetter compreender alguns dos Olá recomendado opções.
