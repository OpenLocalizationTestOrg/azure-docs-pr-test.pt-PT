---
title: "referência de aaaApplicationInsights.config - Azure | Microsoft Docs"
description: "Ativar ou desativar os módulos de recolha de dados e adicionar os contadores de desempenho e outros parâmetros."
services: application-insights
documentationcenter: 
author: OlegAnaniev-MSFT
editor: alancameronwills
manager: carmonm
ms.assetid: 6e397752-c086-46e9-8648-a1196e8078c2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 05/3/2017
ms.author: bwren
ms.openlocfilehash: 76cb11349d87dfc508ec8b1c454259a0b079c48a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configuring-hello-application-insights-sdk-with-applicationinsightsconfig-or-xml"></a>Configurar Olá Application Insights SDK com Applicationinsights ou. XML
Olá SDK .NET do Application Insights é composta por um número de pacotes NuGet. O [pacote core](http://www.nuget.org/packages/Microsoft.ApplicationInsights) fornece Olá API para enviar telemetria ao hello do Application Insights. [Pacotes adicionais](http://www.nuget.org/packages?q=Microsoft.ApplicationInsights) fornecer telemetria *módulos* e *inicializadores* para controlo automaticamente telemetria da sua aplicação e o respetivo contexto. Ao ajustar o ficheiro de configuração de Olá, pode ativar ou desativar os módulos de telemetria e inicializadores e definir os parâmetros de algumas delas.

nome do ficheiro de configuração de Olá `ApplicationInsights.config` ou `ApplicationInsights.xml`, consoante o tipo de Olá da sua aplicação. É automaticamente adicionado tooyour projeto quando [instalar a maioria das versões do SDK de Olá][start]. Foi também adicionada a aplicação web tooa [Monitor de estado num servidor IIS][redfield], ou quando seleciona Olá Appplication Insights [extensão para um Web site Azure ou VM](app-insights-azure-web-apps.md).

Não é um Olá de toocontrol ficheiro equivalente [SDK numa página web][client].

Este documento descreve secções Olá que vê na configuração de Olá ficheiro, como controlarem estes componentes Olá de Olá SDK, e quais os pacotes NuGet carregar desses componentes.

## <a name="telemetry-modules-aspnet"></a>Módulos de telemetria (ASP.NET)
Cada módulo telemetria recolhe um tipo específico de dados e utiliza core Olá dados de Olá toosend de API. módulos de Olá estão instalados por diferentes pacotes de NuGet, que também adicionar o ficheiro do Olá linhas necessária toohello. config.

Não há um nó no ficheiro de configuração de Olá para cada módulo. toodisable um módulo, elimine o nó de Olá ou comente-lo.

### <a name="dependency-tracking"></a>Controlo de dependência
[Controlo de dependência](app-insights-asp-net-dependencies.md) recolhe telemetria sobre as chamadas a aplicação faz com que serviços externos e toodatabases e bases de dados. tooallow toowork este módulo, um servidor de IIS, terá de demasiado[instalar Monitor de estado][redfield]. toouse-lo em aplicações web do Azure ou VMs, [selecionar extensão do Application Insights Olá](app-insights-azure-web-apps.md).

Também pode escrever o seu próprio controlo código utilizando Olá de dependência [TrackDependency API](app-insights-api-custom-events-metrics.md#trackdependency).

* `Microsoft.ApplicationInsights.DependencyCollector.DependencyTrackingTelemetryModule`
* [Microsoft.ApplicationInsights.DependencyCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.DependencyCollector) pacote NuGet.

### <a name="performance-collector"></a>Recoletor de desempenho
[Recolhe os contadores de desempenho do sistema](app-insights-performance-counters.md) tais como CPU, memória e rede carregar das instalações do IIS. Pode especificar que toocollect contadores, incluindo os contadores de desempenho que configurou por si.

* `Microsoft.ApplicationInsights.Extensibility.PerfCounterCollector.PerformanceCollectorModule`
* [Microsoft.ApplicationInsights.PerfCounterCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.PerfCounterCollector) pacote NuGet.

### <a name="application-insights-diagnostics-telemetry"></a>Telemetria de diagnóstico do Application Insights
Olá `DiagnosticsTelemetryModule` relatórios de erros no Olá código de instrumentação do Application Insights em si. Por exemplo, se o código de Olá não é possível aceder contadores de desempenho ou se um `ITelemetryInitializer` emite uma exceção. Telemetria de rastreio registada por este módulo é apresentado no Olá [pesquisa de diagnóstico][diagnostic]. Envia dados de diagnóstico toodc.services.vsallin.net.

* `Microsoft.ApplicationInsights.Extensibility.Implementation.Tracing.DiagnosticsTelemetryModule`
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pacote NuGet. Se apenas a instalar este pacote, o ficheiro de Applicationinsights Olá não é criado automaticamente.

### <a name="developer-mode"></a>Modo de programador
`DeveloperModeWithDebuggerAttachedTelemetryModule`força Olá Application Insights `TelemetryChannel` toosend dados imediatamente, itens de um telemetria cada vez, quando um depurador for anexado toohello processo da aplicação. Esta reduz Olá período de tempo entre o momento de Olá quando a aplicação controla telemetria e quando é apresentado no portal do Application Insights Olá. Causa overhead significativo na largura de banda de CPU e da rede.

* `Microsoft.ApplicationInsights.WindowsServer.DeveloperModeWithDebuggerAttachedTelemetryModule`
* [Windows Server do Application Insights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pacote NuGet

### <a name="web-request-tracking"></a>Pedido de Web de controlo
Olá relatórios [código de tempo e o resultado da resposta](app-insights-asp-net.md) de pedidos HTTP.

* `Microsoft.ApplicationInsights.Web.RequestTrackingTelemetryModule`
* [Applicationinsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pacote NuGet

### <a name="exception-tracking"></a>Controlo de exceções
`ExceptionTrackingTelemetryModule`controla exceções não processadas na aplicação web. Consulte [falhas e exceções][exceptions].

* `Microsoft.ApplicationInsights.Web.ExceptionTrackingTelemetryModule`
* [Applicationinsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.Web) pacote NuGet
* `Microsoft.ApplicationInsights.WindowsServer.UnobservedExceptionTelemetryModule`-controla [não observada exceções tarefas](http://blogs.msdn.com/b/pfxteam/archive/2011/09/28/task-exception-handling-in-net-4-5.aspx).
* `Microsoft.ApplicationInsights.WindowsServer.UnhandledExceptionTelemetryModule`-controla exceções não processadas para as funções de trabalho, serviços do windows e aplicações de consola.
* [Windows Server do Application Insights](http://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer/) pacote NuGet.

### <a name="eventsource-tracking"></a>Controlo de EventSource
`EventSourceTelemetryModule`permite-lhe tooconfigure toobe de eventos de EventSource enviado tooApplication Insights como rastreios. Para obter informações sobre o registo de eventos de EventSource, consulte [através de eventos de EventSource](app-insights-asp-net-trace-logs.md#using-eventsource-events).

* `Microsoft.ApplicationInsights.EventSourceListener.EventSourceTelemetryModule`
* [Microsoft.ApplicationInsights.EventSourceListener](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EventSourceListener) 

### <a name="etw-event-tracking"></a>Registo de eventos do ETW
`EtwCollectorTelemetryModule`permite-lhe tooconfigure eventos do ETW fornecedores toobe enviado tooApplication Insights como rastreios. Para obter informações sobre o registo de eventos ETW, consulte [através de eventos do ETW](app-insights-asp-net-trace-logs.md#using-etw-events).

* `Microsoft.ApplicationInsights.EtwCollector.EtwCollectorTelemetryModule`
* [Microsoft.ApplicationInsights.EtwCollector](http://www.nuget.org/packages/Microsoft.ApplicationInsights.EtwCollector) 

### <a name="microsoftapplicationinsights"></a>Microsoft.ApplicationInsights
pacote de Microsoft.ApplicationInsights Olá fornece Olá [principal API](https://msdn.microsoft.com/library/mt420197.aspx) de Olá SDK. Olá outros módulos de telemetria utilizá-lo e também pode [utilizá-lo toodefine sua própria telemetria](app-insights-api-custom-events-metrics.md).

* Nenhuma entrada no Applicationinsights.
* [Microsoft.ApplicationInsights](http://www.nuget.org/packages/Microsoft.ApplicationInsights) pacote NuGet. Se instalar apenas esta NuGet, não é gerado nenhum ficheiro. config.

## <a name="telemetry-channel"></a>Canal de telemetria
canal de telemetria de Olá gere a colocação em memória intermédia e transmissão de telemetria toohello serviço Application Insights.

* `Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.ServerTelemetryChannel`é Olá predefinido canal para os serviços. Este serve de memória intermédia dados na memória.
* `Microsoft.ApplicationInsights.PersistenceChannel`é uma alternativa para aplicações de consola. Pode poupar qualquer armazenamento de toopersistent unflushed dados quando a aplicação fecha-se para baixo e irá enviar quando inicia a aplicação Olá novamente.

## <a name="telemetry-initializers-aspnet"></a>Inicializadores de telemetria (ASP.NET)
Os inicializadores de telemetria definir propriedades de contexto, que são enviadas juntamente com todos os itens de telemetria.

Pode [escrever os seus próprios inicializadores](app-insights-api-filtering-sampling.md#add-properties) tooset propriedades de contexto.

Os inicializadores padrão Olá estão todos definidos por pacotes de Web ou WindowsServer NuGet Olá:

* `AccountIdTelemetryInitializer`Define a propriedade de AccountId Olá.
* `AuthenticatedUserIdTelemetryInitializer`Define a propriedade de AuthenticatedUserId de Olá conforme definido por Olá JavaScript SDK.
* `AzureRoleEnvironmentTelemetryInitializer`Olá atualizações `RoleName` e `RoleInstance` propriedades de Olá `Device` contexto de todos os itens de telemetria com informações extraídas do ambiente de tempo de execução do Azure Olá.
* `BuildInfoConfigComponentVersionTelemetryInitializer`Olá atualizações `Version` propriedade Olá `Component` contexto de todos os itens de telemetria com o valor de Olá extraídos de Olá `BuildInfo.config` ficheiro produzidos por MS Build.
* `ClientIpHeaderTelemetryInitializer`atualizações `Ip` propriedade Olá `Location` contexto de todos os itens de telemetria com base no Olá `X-Forwarded-For` cabeçalho HTTP do pedido de Olá.
* `DeviceTelemetryInitializer`Olá atualizações seguintes propriedades de Olá `Device` contexto de todos os itens de telemetria.
  * `Type`está definido demasiado "PC"
  * `Id`está definido toohello o nome de domínio do computador olá onde a aplicação web de Olá está em execução.
  * `OemName`definir o valor toohello extraído de Olá `Win32_ComputerSystem.Manufacturer` campo através do WMI.
  * `Model`definir o valor toohello extraído de Olá `Win32_ComputerSystem.Model` campo através do WMI.
  * `NetworkType`definir o valor toohello extraído de Olá `NetworkInterface`.
  * `Language`está a definir o nome toohello Olá `CurrentCulture`.
* `DomainNameRoleInstanceTelemetryInitializer`Olá atualizações `RoleInstance` propriedade Olá `Device` contexto de todos os itens de telemetria com o nome de domínio Olá do computador olá onde a aplicação web de Olá está em execução.
* `OperationNameTelemetryInitializer`Olá atualizações `Name` propriedade Olá `RequestTelemetry` e Olá `Name` propriedade Olá `Operation` contexto de todos os itens de telemetria com base no método Olá HTTP, bem como os nomes de Olá de tooprocess invocado de controlador e a ação de MVC do ASP.NET pedido.
* `OperationIdTelemetryInitializer`ou `OperationCorrelationTelemetryInitializer` Olá atualizações `Operation.Id` propriedade de contexto de todos os itens de telemetria controlados durante o processamento de um pedido com Olá gerado automaticamente `RequestTelemetry.Id`.
* `SessionTelemetryInitializer`Olá atualizações `Id` propriedade Olá `Session` contexto de todos os itens de telemetria com valor extraídos de Olá `ai_session` cookie gerados pelo Olá, código de instrumentação de ApplicationInsights JavaScript em execução no browser do utilizador Olá.
* `SyntheticTelemetryInitializer`ou `SyntheticUserAgentTelemetryInitializer` Olá atualizações `User`, `Session` e `Operation` controlado de propriedades de contextos de todos os itens de telemetria ao processar um pedido de uma origem sintética, tal como um disponibilidade testar ou bot do motor de pesquisa. Por predefinição, [Explorador de métricas](app-insights-metrics-explorer.md) não apresenta a telemetria sintética.

    Olá `<Filters>` definir propriedades de pedidos de Olá a identificar.
* `UserAgentTelemetryInitializer`Olá atualizações `UserAgent` propriedade Olá `User` contexto de todos os itens de telemetria com base no Olá `User-Agent` cabeçalho HTTP do pedido de Olá.
* `UserTelemetryInitializer`Olá atualizações `Id` e `AcquisitionDate` propriedades de `User` contexto de todos os itens de telemetria com valores extraídos de Olá `ai_user` cookie gerado pelo Olá Application Insights instrumentação no código JavaScript em execução no Olá browser do utilizador.
* `WebTestTelemetryInitializer`conjuntos de Olá id de utilizador, id de sessão e propriedades da origem sintético para pedidos de HTTP que provenientes do [testes de disponibilidade](app-insights-monitor-web-app-availability.md).
  Olá `<Filters>` definir propriedades de pedidos de Olá a identificar.

Para aplicações de .NET em execução no Service Fabric, pode incluir Olá `Microsoft.ApplicationInsights.ServiceFabric` pacote NuGet. Este pacote inclui um `FabricTelemetryInitializer`, que adiciona itens de tootelemetry de propriedades de Service Fabric. Para obter mais informações, consulte Olá [página do GitHub](https://go.microsoft.com/fwlink/?linkid=848457) sobre as propriedades de Olá adicionadas por este pacote NuGet.

## <a name="telemetry-processors-aspnet"></a>Processadores de telemetria (ASP.NET)
Processadores de telemetria podem filtrar e modificar cada item de telemetria apenas antes de ser enviada partir Olá SDK toohello do portal.

Pode [escrever os seus próprios processadores de telemetria](app-insights-api-filtering-sampling.md#filtering).

#### <a name="adaptive-sampling-telemetry-processor-from-200-beta3"></a>Processador de telemetria de amostragem adaptável (a partir de 2.0.0-Beta3)
Opção ativada por predefinição. Se a aplicação envia uma grande quantidade de telemetria, este processador remove algumas do mesmo.

```xml

    <TelemetryProcessors>
      <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.AdaptiveSamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">
        <MaxTelemetryItemsPerSecond>5</MaxTelemetryItemsPerSecond>
      </Add>
    </TelemetryProcessors>

```

parâmetro de Olá fornece destino Olá que Olá algoritmo tenta tooachieve. Cada instância de Olá que SDK funciona de forma independente, pelo que o se o servidor for um cluster de vários computadores, o volume real de Olá de telemetria irá ser multiplicado em conformidade.

[Saiba mais sobre amostragem](app-insights-sampling.md).

#### <a name="fixed-rate-sampling-telemetry-processor-from-200-beta1"></a>A amostragem-taxa telemetria processador (2.0.0-beta1)
Também é uma norma [amostragem processador telemetria](app-insights-api-filtering-sampling.md) (a partir de 2.0.1):

```XML

    <TelemetryProcessors>
     <Add Type="Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel.SamplingTelemetryProcessor, Microsoft.AI.ServerTelemetryChannel">

     <!-- Set a percentage close too100/N where N is an integer. -->
     <!-- E.g. 50 (=100/2), 33.33 (=100/3), 25 (=100/4), 20, 1 (=100/100), 0.1 (=100/1000) -->
     <SamplingPercentage>10</SamplingPercentage>
     </Add>
   </TelemetryProcessors>

```



## <a name="channel-parameters-java"></a>Parâmetros do canal (Java)
Estes parâmetros afetam como Olá SDK de Java deve armazenar e esvaziar dados de telemetria de Olá que recolhe.

#### <a name="maxtelemetrybuffercapacity"></a>MaxTelemetryBufferCapacity
número de Olá de itens de telemetria que podem ser armazenados no armazenamento de dentro da memória do Olá SDK. Quando este número for atingido, a memória intermédia de telemetria de Olá for descarregada - ou seja, itens de telemetria de Olá são enviados por servidor do Application Insights toohello.

* Mínimo: 1
* Máx.: 1000
* Predefinição: 500

```

  <ApplicationInsights>
      ...
      <Channel>
       <MaxTelemetryBufferCapacity>100</MaxTelemetryBufferCapacity>
      </Channel>
      ...
  </ApplicationInsights>
```

#### <a name="flushintervalinseconds"></a>FlushIntervalInSeconds
Determina a frequência hello dados armazenados no armazenamento de dentro da memória Olá devem ser removida da cache (enviado tooApplication Insights).

* Mínimo: 1
* Máx.: 300
* Predefinição: 5

```

    <ApplicationInsights>
      ...
      <Channel>
        <FlushIntervalInSeconds>100</FlushIntervalInSeconds>
      </Channel>
      ...
    </ApplicationInsights>
```

#### <a name="maxtransmissionstoragecapacityinmb"></a>MaxTransmissionStorageCapacityInMB
Determina o tamanho máximo do Olá em MB, que é atribuído toohello armazenamento persistente num disco local Olá. Este tipo de armazenamento é utilizado para itens de telemetria persistentes que falharam toobe transmitido toohello Application Insights endpoint. Quando o tamanho de armazenamento Olá tem sido cumprido, novos itens de telemetria serão eliminados.

* Mínimo: 1
* Máxima: 100
* Predefinição: 10

```

   <ApplicationInsights>
      ...
      <Channel>
        <MaxTransmissionStorageCapacityInMB>50</MaxTransmissionStorageCapacityInMB>
      </Channel>
      ...
   </ApplicationInsights>
```



## <a name="instrumentationkey"></a>InstrumentationKey
Isto determina o recurso do Application Insights Olá na qual os dados são apresentados. Normalmente, crie um recurso de separado, com uma chave separada, para cada uma das suas aplicações.

Se pretende tooset Olá chave dinamicamente - por exemplo, se quiser toosend resultados dos seus recursos de toodifferent da aplicação - pode omitir a chave de Olá Olá ficheiro de configuração e configurá-lo no código.

chave de Olá tooset para todas as instâncias TelemetryClient, incluindo módulos de telemetria padrão, defina a chave de Olá no TelemetryConfiguration.Active. Fazê-lo um método de inicialização, tais como global.aspx.cs num serviço ASP.NET:

```C#

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      //...
```

Se pretender apenas toosend específicos de um conjunto de recursos diferente de tooa de eventos, pode definir chave Olá para um TelemetryClient específico:

```C#

    var tc = new TelemetryClient();
    tc.Context.InstrumentationKey = "----- my key ----";
    tc.TrackEvent("myEvent");
    // ...

```

tooget uma nova chave, [criar um novo recurso no portal do Application Insights Olá][new].

## <a name="next-steps"></a>Passos seguintes
[Saiba mais sobre Olá API][api].

<!--Link references-->

[api]: app-insights-api-custom-events-metrics.md
[client]: app-insights-javascript.md
[diagnostic]: app-insights-diagnostic-search.md
[exceptions]: app-insights-asp-net-exceptions.md
[netlogs]: app-insights-asp-net-trace-logs.md
[new]: app-insights-create-new-resource.md
[redfield]: app-insights-monitor-performance-live-website-now.md
[start]: app-insights-overview.md
