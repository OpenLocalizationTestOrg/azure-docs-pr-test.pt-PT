---
title: "aaaApplication Insights API de métricas e eventos personalizados | Microsoft Docs"
description: "Insira alguns linhas de código na sua utilização de tootrack dispositivo ou aplicação de ambiente de trabalho, a página Web ou serviço e diagnosticar problemas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 80400495-c67b-4468-a92e-abf49793a54d
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/17/2017
ms.author: bwren
ms.openlocfilehash: f3d207a47bb4825efda806a19dd0c26540db7bdd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="application-insights-api-for-custom-events-and-metrics"></a>API do Application Insights para as métricas e eventos personalizados

Inserir algumas linhas de código no seu toofind aplicação out que os utilizadores estão a fazer com o mesmo ou toohelp diagnosticar problemas. Pode enviar telemetria a partir de aplicações de ambiente de trabalho e dispositivos, os clientes web e servidores web. Olá utilize [Azure Application Insights](app-insights-overview.md) principal API de telemetria toosend e eventos personalizados e métricas, as suas próprias versões de telemetria padrão. Esta API é Olá API mesmo padrão que Olá utilizam os recoletores de dados do Application Insights.

## <a name="api-summary"></a>Resumo da API
Olá API é uniforme em todas as plataformas, para além dos algumas variações pequenas.

| Método | Utilizado para |
| --- | --- |
| [`TrackPageView`](#page-views) |Páginas, ecrãs, painéis ou formulários. |
| [`TrackEvent`](#trackevent) |Ações de utilizador e outros eventos. Utilizado tootrack de desempenho de comportamento ou toomonitor de utilizador. |
| [`TrackMetric`](#trackmetric) |Medidas de desempenho, tais como os comprimentos fila não relacionada com eventos toospecific. |
| [`TrackException`](#trackexception) |Exceções de registo para diagnósticos adicionais. Rastreio onde ocorrer nos eventos de tooother de relação e examine rastreios de pilha. |
| [`TrackRequest`](#trackrequest) |Registo de frequência de Olá e duração de pedidos de servidor para análise de desempenho. |
| [`TrackTrace`](#tracktrace) |Mensagens de registo de diagnóstico. Também pode capturar os registos de terceiros. |
| [`TrackDependency`](#trackdependency) |Duração de Olá de registo e a frequência dos componentes de tooexternal de chamadas que depende da sua aplicação. |

Pode [anexar propriedades e métricas](#properties) toomost destas chamadas à telemetria.

## <a name="prep"></a>Antes de começar
Se ainda não tem uma referência no Application Insights SDK:

* Adicione o projeto de tooyour Olá Application Insights SDK:

  * [Projeto ASP.NET](app-insights-asp-net.md)
  * [Projeto de Java](app-insights-java-get-started.md)
  * [JavaScript em cada página Web](app-insights-javascript.md) 
* No seu código de servidor web ou de dispositivo, incluem:

    *C#:*`using Microsoft.ApplicationInsights;`

    *Visual Basic:*`Imports Microsoft.ApplicationInsights`

    *Java:*`import com.microsoft.applicationinsights.TelemetryClient;`

## <a name="constructing-a-telemetryclient-instance"></a>Construir uma instância de TelemetryClient
Construir uma instância de `TelemetryClient` (exceto em JavaScript em páginas Web):

*C#*

    private TelemetryClient telemetry = new TelemetryClient();

*Visual Basic*

    Private Dim telemetry As New TelemetryClient

*Java*

    private TelemetryClient telemetry = new TelemetryClient();

TelemetryClient é seguro para thread.

Recomendamos que utilize uma instância de TelemetryClient para cada módulo da sua aplicação. Por exemplo, pode ter uma instância de TelemetryClient no seu pedidos HTTP recebidos do web service tooreport e outro em eventos de lógica de negócio um middleware classe tooreport. Pode definir as propriedades, tais como `TelemetryClient.Context.User.Id` tootrack utilizadores e sessões, ou `TelemetryClient.Context.Device.Id` máquina de Olá tooidentify. Estas informações são eventos tooall anexado Olá envia de instância.

## <a name="trackevent"></a>TrackEvent
No Application Insights, um *evento personalizado* é um ponto de dados que pode apresentar em [Explorador de métricas](app-insights-metrics-explorer.md) como uma conta a contagem agregada e na [pesquisa de diagnóstico](app-insights-diagnostic-search.md) como ocorrências individuais. (Não se encontra tooMVC relacionado ou outros framework "eventos.")

Inserir `TrackEvent` chama no seu código toocount vários eventos. Como muitas vezes, os utilizadores devem escolher uma funcionalidade específica, frequência alcançarem estes objetivos específicos ou talvez frequência que efetuam a tipos específicos de prende.

Por exemplo, uma aplicação de jogo, envie um evento sempre que um utilizador wins jogo Olá:

*JavaScript*

    appInsights.trackEvent("WinGame");

*C#*

    telemetry.TrackEvent("WinGame");

*Visual Basic*

    telemetry.TrackEvent("WinGame")

*Java*

    telemetry.trackEvent("WinGame");

### <a name="view-your-events-in-hello-microsoft-azure-portal"></a>Ver os eventos no portal do Microsoft Azure Olá
toosee uma contagem dos seus eventos, abra uma [Explorador de métricas](app-insights-metrics-explorer.md) painel, adicione um novo gráfico e selecione **eventos**.  

![Consulte uma contagem dos eventos personalizados](./media/app-insights-api-custom-events-metrics/01-custom.png)

contagens de Olá toocompare eventos diferente, defina o tipo de gráfico de Olá demasiado**grelha**e grupo por nome de evento:

![Definir o tipo de gráfico de Olá e agrupamento](./media/app-insights-api-custom-events-metrics/07-grid.png)

Na grelha de Olá, clique em através de um evento nome toosee individuais as ocorrências esse evento. toosee mais pormenorizadamente - clique em qualquer ocorrência na lista de Olá.

![Exploração de eventos de Olá](./media/app-insights-api-custom-events-metrics/03-instances.png)

toofocus nos eventos específicos na pesquisa ou no Explorador de métricas, filtro toohello eventos os nomes do painel do conjunto Olá que está interessado em:

![Abra os filtros, expanda o nome do evento e selecione um ou mais valores](./media/app-insights-api-custom-events-metrics/06-filter.png)

### <a name="custom-events-in-analytics"></a>Eventos personalizados no Analytics

telemetria de Olá está disponível no Olá `customEvents` tabela no [Application Insights Analytics](app-insights-analytics.md). Cada linha representa uma chamada demasiado`trackEvent(..)` na sua aplicação. 

Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1. Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackEvent(), processo de amostragem Olá apenas transmitidos um deles. tooget um número correto de eventos personalizados, deve utilizar, por conseguinte, código de utilização, tais como `customEvent | summarize sum(itemCount)`.


## <a name="trackmetric"></a>TrackMetric

Application Insights podem gráfico métricas que não estão anexados tooparticular eventos. Por exemplo, pode monitorizar um comprimento de fila em intervalos regulares. Com a métrica, medidas individuais Olá são de menos interesse que variações Olá e as tendências e estatísticos, por isso, gráficos são úteis.

Na ordem toosend métricas tooApplication Insights, pode utilizar Olá `TrackMetric(..)` API. Existem duas formas toosend uma métrica de: 

* Valor único. Sempre que efetuar uma medida na sua aplicação, enviar valor correspondente Olá tooApplication Insights. Por exemplo, suponha que tem uma métrica de descrever o número de Olá de itens num contentor. Durante um período de tempo específico, primeiro coloque o três itens num contentor de Olá e, em seguida, remover dois itens. Em conformidade, iria chamar `TrackMetric` duas vezes: primeiro transmitir o valor de Olá `3` e, em seguida, Olá valor `-2`. Application Insights armazena ambos os valores em seu nome. 

* Agregação. Ao trabalhar com as métricas, cada medida único é raramente de interesse. Em vez disso, um resumo do que aconteceu durante um período de tempo específico é importante. Denomina-se um resumo essa _agregação_. Olá acima exemplo, soma métrica agregado Olá para esse período de tempo é `1` e Olá contagem de valores de métrica de Olá é `2`. Quando utilizar a abordagem de agregação de Olá, apenas invocar `TrackMetric` uma vez por período e enviar Olá agregados valores de hora. Este é Olá abordagem recomendada, uma vez que este pode reduzir significativamente o custo de Olá e desempenho dos custos gerais ao enviarem dados menos pontos tooApplication Insights, ao ainda recolher todas as informações relevantes.

### <a name="examples"></a>Exemplos:

#### <a name="single-values"></a>Valores único

um valor métrico único toosend:

*JavaScript*

 ```Javascript
     appInsights.trackMetric("queueLength", 42.0);
 ```

*C#, Java*

```C#
    var sample = new MetricTelemetry();
    sample.Name = "metric name";
    sample.Value = 42.3;
    telemetryClient.TrackMetric(sample);
```

#### <a name="aggregating-metrics"></a>Agregar as métricas

É recomendado tooaggregate métricas antes de lhes enviar da sua aplicação, tooreduce largura de banda e de desempenho de custos e tooimprove.
Eis um exemplo de código agregar:

*C#*

```C#
using System;
using System.Threading;
using System.Threading.Tasks;

using Microsoft.ApplicationInsights;
using Microsoft.ApplicationInsights.DataContracts;

namespace MetricAggregationExample
{
    /// <summary>
    /// Aggregates metric values for a single time period.
    /// </summary>
    internal class MetricAggregator
    {
        private SpinLock _trackLock = new SpinLock();

        public DateTimeOffset StartTimestamp    { get; }
        public int Count                        { get; private set; }
        public double Sum                       { get; private set; }
        public double SumOfSquares              { get; private set; }
        public double Min                       { get; private set; }
        public double Max                       { get; private set; }
        public double Average                   { get { return (Count == 0) ? 0 : (Sum / Count); } }
        public double Variance                  { get { return (Count == 0) ? 0 : (SumOfSquares / Count)
                                                                                  - (Average * Average); } }
        public double StandardDeviation         { get { return Math.Sqrt(Variance); } }

        public MetricAggregator(DateTimeOffset startTimestamp)
        {
            this.StartTimestamp = startTimestamp;
        }

        public void TrackValue(double value)
        {
            bool lockAcquired = false;

            try
            {
                _trackLock.Enter(ref lockAcquired);

                if ((Count == 0) || (value < Min))  { Min = value; }
                if ((Count == 0) || (value > Max))  { Max = value; }
                Count++;
                Sum += value;
                SumOfSquares += value * value;
            }
            finally
            {
                if (lockAcquired)
                {
                    _trackLock.Exit();
                }
            }
        }
    }   // internal class MetricAggregator

    /// <summary>
    /// Accepts metric values and sends hello aggregated values at 1-minute intervals.
    /// </summary>
    public sealed class Metric : IDisposable
    {
        private static readonly TimeSpan AggregationPeriod = TimeSpan.FromSeconds(60);

        private bool _isDisposed = false;
        private MetricAggregator _aggregator = null;
        private readonly TelemetryClient _telemetryClient;

        public string Name { get; }

        public Metric(string name, TelemetryClient telemetryClient)
        {
            this.Name = name ?? "null";
            this._aggregator = new MetricAggregator(DateTimeOffset.UtcNow);
            this._telemetryClient = telemetryClient ?? throw new ArgumentNullException(nameof(telemetryClient));

            Task.Run(this.AggregatorLoopAsync);
        }

        public void TrackValue(double value)
        {
            MetricAggregator currAggregator = _aggregator;
            if (currAggregator != null)
            {
                currAggregator.TrackValue(value);
            }
        }

        private async Task AggregatorLoopAsync()
        {
            while (_isDisposed == false)
            {
                try
                {
                    // Wait for end end of hello aggregation period:
                    await Task.Delay(AggregationPeriod).ConfigureAwait(continueOnCapturedContext: false);

                    // Atomically snap hello current aggregation:
                    MetricAggregator nextAggregator = new MetricAggregator(DateTimeOffset.UtcNow);
                    MetricAggregator prevAggregator = Interlocked.Exchange(ref _aggregator, nextAggregator);

                    // Only send anything is at least one value was measured:
                    if (prevAggregator != null && prevAggregator.Count > 0)
                    {
                        // Compute hello actual aggregation period length:
                        TimeSpan aggPeriod = nextAggregator.StartTimestamp - prevAggregator.StartTimestamp;
                        if (aggPeriod.TotalMilliseconds < 1)
                        {
                            aggPeriod = TimeSpan.FromMilliseconds(1);
                        }

                        // Construct hello metric telemetry item and send:
                        var aggregatedMetricTelemetry = new MetricTelemetry(
                                Name,
                                prevAggregator.Count,
                                prevAggregator.Sum,
                                prevAggregator.Min,
                                prevAggregator.Max,
                                prevAggregator.StandardDeviation);
                        aggregatedMetricTelemetry.Properties["AggregationPeriod"] = aggPeriod.ToString("c");

                        _telemetryClient.Track(aggregatedMetricTelemetry);
                    }
                }
                catch(Exception ex)
                {
                    // log ex as appropriate for your application
                }
            }
        }

        void IDisposable.Dispose()
        {
            _isDisposed = true;
            _aggregator = null;
        }
    }   // public sealed class Metric
}
```

### <a name="custom-metrics-in-metrics-explorer"></a>Métricas personalizadas no Explorador de métricas

resultados de Olá toosee, abra o Explorador de métricas e adicionar um novo gráfico. Edite Olá gráfico tooshow a métrica.

> [!NOTE]
> A métrica personalizada poderá demorar vários minutos tooappear na lista de Olá de métricas disponíveis.
>

![Adicione um novo gráfico ou selecione um gráfico e, em personalizado, selecione a métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

### <a name="custom-metrics-in-analytics"></a>Métricas personalizadas no Analytics

telemetria de Olá está disponível no Olá `customMetrics` tabela no [Application Insights Analytics](app-insights-analytics.md). Cada linha representa uma chamada demasiado`trackMetric(..)` na sua aplicação.
* `valueSum`-Esta é a soma de Olá uma medidas Olá. valor médio tooget Olá, dividir por `valueCount`.
* `valueCount`-Olá número de valores que foram agregados neste `trackMetric(..)` chamada.

## <a name="page-views"></a>Vistas de página
Numa aplicação ou página Web de dispositivo, a telemetria de visualizações de página é enviada por predefinição quando cada ecrã ou a página é carregada. Mas pode alterar as vistas de página que tootrack em alturas diferentes ou adicionais. Por exemplo, numa aplicação que apresenta os separadores ou em painéis, é aconselhável tootrack uma página sempre que o utilizador Olá abre um novo painel.

![Lente de utilização no painel de descrição geral](./media/app-insights-api-custom-events-metrics/appinsights-47usage-2.png)

Dados de utilizador e de sessão são enviados como propriedades, juntamente com as vistas de página Olá, por isso, gráficos de utilizador e a sessão fique ativo quando não existe telemetria de visualizações de página.

### <a name="custom-page-views"></a>Vistas de página personalizada
*JavaScript*

    appInsights.trackPageView("tab1");

*C#*

    telemetry.TrackPageView("GameReviewPage");

*Visual Basic*

    telemetry.TrackPageView("GameReviewPage")


Se tiver vários separadores dentro páginas HTML diferentes, pode especificar o URL de Olá demasiado:

    appInsights.trackPageView("tab1", "http://fabrikam.com/page1.htm");

### <a name="timing-page-views"></a>Vistas de página de temporização
Por predefinição, os tempos de Olá reportados como **tempo de carregamento da vista de página** são avaliadas da quando browser Olá envia o pedido de Olá, até que o evento de carregamento de página do browser Olá é chamado.

Em vez disso, pode:

* Defina uma duração de explícita no Olá [trackPageView](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md#trackpageview) chamar: `appInsights.trackPageView("tab1", null, null, null, durationInMilliseconds);`.
* Utilize chamadas de temporização de vista de página Olá `startTrackPage` e `stopTrackPage`.

*JavaScript*

    // toostart timing a page:
    appInsights.startTrackPage("Page1");

...

    // toostop timing and log hello page:
    appInsights.stopTrackPage("Page1", url, properties, measurements);

Olá nome que utilizar como primeiro parâmetro de Olá associa início Olá e pare chamadas. Assume toohello nome da página atual.

Olá resultante o carregamento da página apresentadas no Explorador de métricas de durações são derivadas de intervalo de Olá entre Olá iniciar e parar chamadas. Está a funcionar tooyou que intervalo, na verdade, de hora.

### <a name="page-telemetry-in-analytics"></a>Telemetria de página no Analytics

No [análise](app-insights-analytics.md) duas tabelas mostram dados de operações do browser:

* Olá `pageViews` tabela contém dados sobre o título de URL e página Olá
* Olá `browserTimings` tabela contém dados sobre o desempenho do cliente, tais como Olá tempo decorrido tooprocess Olá dados de entrada

toofind quanto browser Olá demora tooprocess páginas diferentes:

```
browserTimings | summarize avg(networkDuration), avg(processingDuration), avg(totalDuration) by name 
```

toodiscover popularities de Olá dos browsers diferentes:

```
pageViews | summarize count() by client_Browser
```

chamadas de tooAJAX de vistas de página tooassociate, associar dependências:

```
pageViews | join (dependencies) on operation_Id 
```

## <a name="trackrequest"></a>TrackRequest
o servidor de Olá SDK utiliza TrackRequest toolog os pedidos de HTTP.

Pode também chamá-la se pretender que os pedidos de toosimulate num contexto onde não tiver Olá web serviço módulo executado.

No entanto, Olá recomendado é de telemetria de pedido de toosend de forma onde pedido Olá age como um <a href="#operation-context">contexto das operações</a>.

## <a name="operation-context"></a>Contexto de operação
Pode associar os itens de telemetria em conjunto ligando toothem um ID de operação comuns. módulo de rastreio de pedido padrão Olá efetua este procedimento para exceções e outros eventos que são enviados enquanto está a ser processado um pedido de HTTP. No [pesquisa](app-insights-diagnostic-search.md) e [análise](app-insights-analytics.md), pode utilizar qualquer eventos associados ao pedido de Olá Olá ID tooeasily localizar.

Olá mais fácil forma tooset Olá ID é tooset um contexto de operação ao utilizar este padrão:

*C#*

```C#
// Establish an operation context and associated telemetry item:
using (var operation = telemetry.StartOperation<RequestTelemetry>("operationName"))
{
    // Telemetry sent in here will use hello same operation ID.
    ...
    telemetry.TrackTrace(...); // or other Track* calls
    ...
    // Set properties of containing telemetry item--for example:
    operation.Telemetry.ResponseCode = "200";

    // Optional: explicitly send telemetry item:
    telemetry.StopOperation(operation);

} // When operation is disposed, telemetry item is sent.
```

Juntamente com a definição de um contexto de operação `StartOperation` cria um item de telemetria do tipo de Olá que especificar. Envia a telemetria Olá item quando eliminar operação hello, ou se chamar explicitamente `StopOperation`. Se utilizar `RequestTelemetry` como tipo de telemetria de Olá, a duração está definida toohello excedeu o tempo limite de intervalo entre o início e fim.

Não não possível aninhar contextos de operação. Se já houver um contexto de operação, então o respetivo ID está associado a todos os itens de Olá contida, incluindo o item de Olá criado com `StartOperation`.

Pesquisa, contexto das operações Olá é utilizado toocreate Olá **itens relacionados** lista:

![Itens relacionados](./media/app-insights-api-custom-events-metrics/21.png)

Consulte [aplicação-insights-personalizada-operations-tracking.md] para obter mais informações sobre operações personalizadas de controlo.

### <a name="requests-in-analytics"></a>Pedidos de análise 

No [Application Insights Analytics](app-insights-analytics.md), os pedidos Mostrar segurança Olá `requests` tabela.

Se [amostragem](app-insights-sampling.md) está numa operação, propriedade de itemCount Olá apresentará um valor superior a 1. Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackRequest(), processo de amostragem Olá apenas transmitidos um deles. tooget uma contagem de pedidos e a duração média correta segmentada por nomes de pedido, utilize, como o código:

```AIQL
requests | summarize count = sum(itemCount), avgduration = avg(duration) by name
```


## <a name="trackexception"></a>TrackException
Envie exceções tooApplication Insights:

* demasiado[contagem-los](app-insights-metrics-explorer.md), como uma indicação de frequência de Olá de um problema.
* demasiado[examinar ocorrências individuais](app-insights-diagnostic-search.md).

os relatórios de Olá incluem os rastreios de pilha Olá.

*C#*

    try
    {
        ...
    }
    catch (Exception ex)
    {
       telemetry.TrackException(ex);
    }

*JavaScript*

    try
    {
       ...
    }
    catch (ex)
    {
       appInsights.trackException(ex);
    }

Olá SDKs catch muitas exceções automaticamente, pelo que não tem sempre toocall TrackException explicitamente.

* ASP.NET: [escrever código toocatch exceções](app-insights-asp-net-exceptions.md).
* J2EE: [as excepções são detectadas automaticamente](app-insights-java-get-started.md#exceptions-and-request-failures).
* JavaScript: Exceções são detectadas automaticamente. Se pretender que uma coleção automática toodisable, adicione um fragmento de código de toohello linha a inserir na suas páginas Web:

    ```
    ({
      instrumentationKey: "your key"
      , disableExceptionTracking: true
    })
    ```

### <a name="exceptions-in-analytics"></a>Exceções de análise

No [Application Insights Analytics](app-insights-analytics.md), exceções apresentada na Olá `exceptions` tabela.

Se [amostragem](app-insights-sampling.md) estiver a ser utilizada, hello `itemCount` propriedade mostra um valor superior a 1. Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackException(), processo de amostragem Olá apenas transmitidos um deles. um número correto de exceções de tooget segmentado pelo tipo de exceção, utilize, como o código:

```
exceptions | summarize sum(itemCount) by type
```

Maioria dos Olá importante informações de pilha já são extraídas para variáveis separadas, mas pode solicitar Olá, à excepção `details` estrutura tooget mais. Uma vez que esta estrutura dinâmica, deve de converter o tipo de toohello de resultado de Olá esperado. Por exemplo:

```AIQL
exceptions
| extend method2 = tostring(details[0].parsedStack[1].method)
```

exceções de tooassociate com os pedidos relacionados, utilize uma associação:

```
exceptions
| join (requests) on operation_Id 
```

## <a name="tracktrace"></a>TrackTrace
Utilize TrackTrace toohelp diagnosticar problemas com o envio de um "registo trilho" tooApplication Insights. Pode enviar os segmentos de dados de diagnóstico e Inspecione os mesmos em [pesquisa de diagnóstico](app-insights-diagnostic-search.md).

[Iniciar sessão adaptadores](app-insights-asp-net-trace-logs.md) utilizar esta API toosend registos de terceiros toohello portal.

*C#*

    telemetry.TrackTrace(message, SeverityLevel.Warning, properties);


Pode pesquisar o conteúdo da mensagem, mas (ao contrário dos valores de propriedade) não é possível filtrar no mesmo.

limite de tamanho de Olá em `message` é muito superior ao limite de Olá nas propriedades.
Uma vantagem TrackTrace é que pode colocar dados relativamente longos na mensagem de saudação. Por exemplo, pode codificar POST data do não existe.  

Além disso, pode adicionar uma mensagem de tooyour nível de gravidade. E, como outra telemetria, pode adicionar toohelp de valores de propriedade que filtrar ou de pesquisa para diferentes conjuntos de rastreios. Por exemplo:

    var telemetry = new Microsoft.ApplicationInsights.TelemetryClient();
    telemetry.TrackTrace("Slow database response",
                   SeverityLevel.Warning,
                   new Dictionary<string,string> { {"database", db.ID} });

No [pesquisa](app-insights-diagnostic-search.md), em seguida, pode facilmente filtrar terminar todas as mensagens de Olá de um nível de gravidade específico que se relacionam com a base de dados específica tooa.


### <a name="traces-in-analytics"></a>Rastreios no Analytics

No [Application Insights Analytics](app-insights-analytics.md), chama tooTrackTrace Mostrar cópias de segurança no Olá `traces` tabela.

Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1. Para o exemplo itemCount = = 10 significa que de 10 chamadas demasiado`trackTrace()`, processo de amostragem Olá transmitidos apenas uma delas. tooget uma contagem de chamadas de rastreio correta, deve utilizar, por conseguinte, código como `traces | summarize sum(itemCount)`.

## <a name="trackdependency"></a>TrackDependency
Olá utilize TrackDependency chamar tempos de resposta de Olá tootrack e taxas de êxito da peça de externo tooan chamadas de código. resultados de Olá são apresentados nos gráficos de dependência de Olá no portal de Olá.

```C#
var success = false;
var startTime = DateTime.UtcNow;
var timer = System.Diagnostics.Stopwatch.StartNew();
try
{
    success = dependency.Call();
}
finally
{
    timer.Stop();
    telemetry.TrackDependency("myDependency", "myCall", startTime, timer.Elapsed, success);
}
```

Lembre-se de que o servidor Olá SDKs incluem um [módulo dependência](app-insights-asp-net-dependencies.md) que Deteta e monitoriza determinadas chamadas de dependência automaticamente – por exemplo, toodatabases e REST APIs. Ter tooinstall um agente no seu módulo Olá do servidor toomake funcione. Utilize esta chamada se pretender que as chamadas de tootrack Olá controlo automatizado não catch ou se não quiser que o agente de Olá tooinstall.

Editar tooturn desativar o módulo de registo de dependência padrão Olá, [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md) e eliminar a referência de Olá demasiado`DependencyCollector.DependencyTrackingTelemetryModule`.

### <a name="dependencies-in-analytics"></a>Dependências de análise

No [Application Insights Analytics](app-insights-analytics.md), chamadas de trackDependency apresentada na Olá `dependencies` tabela.

Se [amostragem](app-insights-sampling.md) está numa operação, a propriedade de itemCount Olá mostra um valor superior a 1. Para o exemplo itemCount = = 10 significa que de 10 chamadas tootrackDependency(), processo de amostragem Olá apenas transmitidos um deles. um número correto de dependências de tooget segmentado pelo componente de destino, utilize, como o código:

```
dependencies | summarize sum(itemCount) by target
```

dependências de tooassociate com os pedidos relacionados, utilize uma associação:

```
dependencies
| join (requests) on operation_Id 
```

## <a name="flushing-data"></a>Dados Flushing
Normalmente, Olá SDK envia dados escolhidos por vezes o impacto de Olá toominimize utilizador Olá. No entanto, em alguns casos, pode querer memória intermédia de Olá tooflush – por exemplo, se estiver a utilizar o SDK de Olá numa aplicação que será encerrado.

*C#*

    telemetry.Flush();

    // Allow some time for flushing before shutdown.
    System.Threading.Thread.Sleep(1000);

Tenha em atenção que a função de Olá é assíncrona para Olá [canal do servidor de telemetria](https://www.nuget.org/packages/Microsoft.ApplicationInsights.WindowsServer.TelemetryChannel/).

## <a name="authenticated-users"></a>Utilizadores autenticados
Numa aplicação web, os utilizadores são (por predefinição) identificados por cookies. Um utilizador pode contar mais do que uma vez se acederem a aplicação a partir de outro computador ou browser ou se poderem eliminar cookies.

Se os utilizadores iniciam sessão na aplicação tooyour, pode obter uma contagem mais exata, definindo o ID de utilizador Olá autenticado no código de browser Olá:

*JavaScript*

```JS
// Called when my app has identified hello user.
function Authenticated(signInId) {
    var validatedId = signInId.replace(/[,;=| ]+/g, "_");
    appInsights.setAuthenticatedUserContext(validatedId);
    ...
}
```

Na web do ASP.NET aplicação MVC, por exemplo:

*Razor*

        @if (Request.IsAuthenticated)
        {
            <script>
                appInsights.setAuthenticatedUserContext("@User.Identity.Name
                   .Replace("\\", "\\\\")"
                   .replace(/[,;=| ]+/g, "_"));
            </script>
        }

Não se encontra toouse necessário Olá nome do utilizador real início de sessão. Tem apenas toobe um ID que é o utilizador toothat exclusivo. Não pode incluir espaços ou nenhum dos carateres Olá `,;=|`.

ID de utilizador Olá também definir um cookie de sessão e enviado toohello servidor. Se o servidor de Olá SDK está instalado, Olá autenticados utilizador que ID é enviado como parte das propriedades de contexto de Olá de telemetria de cliente e servidor. Em seguida, pode filtrar e procurar na mesma.

Se a sua aplicação grupos de utilizadores em contas, também pode transmitir um identificador de conta Olá (com Olá mesmo caráter restrições).

      appInsights.setAuthenticatedUserContext(validatedId, accountId);

No [Explorador de métricas](app-insights-metrics-explorer.md), pode criar um gráfico que contagens **utilizadores, autenticado**, e **contas de utilizador**.

Também pode [pesquisa](app-insights-diagnostic-search.md) para pontos de dados de cliente com contas e os nomes de utilizador específica.

## <a name="properties"></a>Filtragem, pesquisa e segmentar os seus dados através da utilização de propriedades
Pode anexar propriedades e medidas tooyour eventos (e também toometrics, vistas de página, exceções e outros dados de telemetria).

*Propriedades* são valores de cadeia que pode utilizar toofilter sua telemetria nos relatórios de utilização de Olá. Por exemplo, se a aplicação fornece várias jogos, poderá anexar nome Olá do evento de jogos tooeach Olá para que possa ver quais jogos são mais populares.

Não há um limite de 8192 no comprimento da cadeia Olá. (Se quiser toosend grandes segmentos de dados, utilize o parâmetro Mensagem Olá [TrackTrace](#track-trace).)

*Métricas* são valores numéricos que podem ser apresentados graficamente. Por exemplo, é aconselhável toosee se houver um aumento gradual na pontuações Olá que sua gamers alcançarem. gráficos de Olá podem ser segmentados por Olá propriedades que são enviadas com evento Olá, para que pode obter separam ou empilhadas gráficos para jogos diferentes.

Para valores métrica toobe apresentado corretamente, devem ser too0 igual ou superior.

Existem algumas [limites no número de Olá de propriedades, valores de propriedade e métricas](#limits) que pode utilizar.

*JavaScript*

    appInsights.trackEvent
      ("WinGame",
         // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );

    appInsights.trackPageView
        ("page name", "http://fabrikam.com/pageurl.html",
          // String properties:
         {Game: currentGame.name, Difficulty: currentGame.difficulty},
         // Numeric metrics:
         {Score: currentGame.score, Opponents: currentGame.opponentCount}
         );


*C#*

    // Set up some properties and metrics:
    var properties = new Dictionary <string, string>
       {{"game", currentGame.Name}, {"difficulty", currentGame.Difficulty}};
    var metrics = new Dictionary <string, double>
       {{"Score", currentGame.Score}, {"Opponents", currentGame.OpponentCount}};

    // Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics);


*Visual Basic*

    ' Set up some properties:
    Dim properties = New Dictionary (Of String, String)
    properties.Add("game", currentGame.Name)
    properties.Add("difficulty", currentGame.Difficulty)

    Dim metrics = New Dictionary (Of String, Double)
    metrics.Add("Score", currentGame.Score)
    metrics.Add("Opponents", currentGame.OpponentCount)

    ' Send hello event:
    telemetry.TrackEvent("WinGame", properties, metrics)


*Java*

    Map<String, String> properties = new HashMap<String, String>();
    properties.put("game", currentGame.getName());
    properties.put("difficulty", currentGame.getDifficulty());

    Map<String, Double> metrics = new HashMap<String, Double>();
    metrics.put("Score", currentGame.getScore());
    metrics.put("Opponents", currentGame.getOpponentCount());

    telemetry.trackEvent("WinGame", properties, metrics);


> [!NOTE]
> Asseguramos não toolog informações de identificação pessoal nas propriedades.
>
>

*Se utilizou as métricas*, abra o Explorador de métricas e selecione a métrica de Olá da Olá **personalizada** grupo:

![Abra o Explorador de métricas, gráfico de selecione Olá e selecione Olá métrica](./media/app-insights-api-custom-events-metrics/03-track-custom.png)

> [!NOTE]
> Se a métrica não aparecer, ou se hello **personalizada** cabeçalho não existe, é de painel de seleção de Olá fechar e tente novamente mais tarde. Métricas, por vezes, podem demorar uma hora toobe agregado através do pipeline de Olá.

*Se utilizou as propriedades e métricas*, segmentar métrica Olá pela propriedade Olá:

![Definir o agrupamento e, em seguida, selecione a propriedade de Olá Agrupar por](./media/app-insights-api-custom-events-metrics/04-segment-metric-event.png)

*Na pesquisa de diagnóstico*, pode ver as propriedades de Olá e métricas de ocorrências individuais de um evento.

![Selecione uma instância e, em seguida, selecione "..."](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-4.png)

Olá utilize **pesquisa** campo toosee ocorrências de eventos que tenham um valor de propriedade em particular.

![Escreva um termo na pesquisa](./media/app-insights-api-custom-events-metrics/appinsights-23-customevents-5.png)

[Saiba mais sobre as expressões de pesquisa](app-insights-diagnostic-search.md).

### <a name="alternative-way-tooset-properties-and-metrics"></a>Propriedades de tooset de maneira e métricas
Se for mais prático, é possível recolher Olá os parâmetros de um evento num objeto separado:

    var event = new EventTelemetry();

    event.Name = "WinGame";
    event.Metrics["processingTime"] = stopwatch.Elapsed.TotalMilliseconds;
    event.Properties["game"] = currentGame.Name;
    event.Properties["difficulty"] = currentGame.Difficulty;
    event.Metrics["Score"] = currentGame.Score;
    event.Metrics["Opponents"] = currentGame.Opponents.Length;

    telemetry.TrackEvent(event);

> [!WARNING]
> Não reutilize Olá mesma instância de item de telemetria (`event` neste exemplo) toocall Track*() várias vezes. Isto pode provocar toobe de telemetria enviado com configuração incorreta.
>
>

### <a name="custom-measurements-and-properties-in-analytics"></a>Medidas personalizadas e propriedades na análise

No [análise](app-insights-analytics.md), métricas personalizadas e propriedades mostram em Olá `customMeasurements` e `customDimensions` atributos de cada registo de telemetria.

Por exemplo, se tiver adicionado uma propriedade com o nome "jogos" tooyour telemetria de pedido, esta consulta contagem de ocorrências de Olá de valores diferentes de "jogo" e mostrar a média de Olá de Olá métrica personalizada "pontuação":

```
requests
| summarize sum(itemCount), avg(todouble(customMeasurements.score)) by tostring(customDimensions.game) 
```

Tenha em atenção que:

* Quando um valor a extrair Olá customDimensions ou customMeasurements JSON, tem o tipo de dinâmico e, por isso, tem de o transmitir- `tostring` ou `todouble`.
* conta de tootake da possibilidade de Olá de [amostragem](app-insights-sampling.md), deve utilizar `sum(itemCount)`, não `count()`.



## <a name="timed"></a>Eventos de temporização
Por vezes, pretende toochart quanto tempo demora tooperform uma ação. Por exemplo, poderá pretender tooknow quanto utilizadores levar a cabo tooconsider opções num jogo. Pode utilizar o parâmetro de medição de Olá para este.

*C#*

    var stopwatch = System.Diagnostics.Stopwatch.StartNew();

    // ... perform hello timed action ...

    stopwatch.Stop();

    var metrics = new Dictionary <string, double>
       {{"processingTime", stopwatch.Elapsed.TotalMilliseconds}};

    // Set up some properties:
    var properties = new Dictionary <string, string>
       {{"signalSource", currentSignalSource.Name}};

    // Send hello event:
    telemetry.TrackEvent("SignalProcessed", properties, metrics);



## <a name="defaults"></a>Propriedades predefinidas para telemetria personalizada
Se pretender que os valores de propriedade do tooset predefinido para alguns dos eventos personalizados Olá se escrever, pode defini-los numa instância TelemetryClient. São tooevery ligado ao item de telemetria que é enviado a partir de que o cliente.

*C#*

    using Microsoft.ApplicationInsights.DataContracts;

    var gameTelemetry = new TelemetryClient();
    gameTelemetry.Context.Properties["Game"] = currentGame.Name;
    // Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame");

*Visual Basic*

    Dim gameTelemetry = New TelemetryClient()
    gameTelemetry.Context.Properties("Game") = currentGame.Name
    ' Now all telemetry will automatically be sent with hello context property:
    gameTelemetry.TrackEvent("WinGame")

*Java*

    import com.microsoft.applicationinsights.TelemetryClient;
    import com.microsoft.applicationinsights.TelemetryContext;
    ...


    TelemetryClient gameTelemetry = new TelemetryClient();
    TelemetryContext context = gameTelemetry.getContext();
    context.getProperties().put("Game", currentGame.Name);

    gameTelemetry.TrackEvent("WinGame");



Chamadas de telemetria individuais podem substituir os valores predefinidos de Olá no respetivos dicionários de propriedade.

*Para JavaScript web clientes*, [utilizar inicializadores de telemetria de JavaScript](#js-initializer).

*telemetria de tooall tooadd propriedades*, incluindo dados Olá de módulos de recolha padrão, [implementar `ITelemetryInitializer` ](app-insights-api-filtering-sampling.md#add-properties).

## <a name="sampling-filtering-and-processing-telemetry"></a>Amostragem, a filtragem e o processamento de telemetria
Pode escrever o código tooprocess sua telemetria antes do envio de Olá SDK. processamento de Olá inclui dados enviados a partir de módulos de telemetria padrão de Olá, tais como recolha de pedido HTTP e a recolha de dependência.

[Adicionar propriedades](app-insights-api-filtering-sampling.md#add-properties) tootelemetry implementando `ITelemetryInitializer`. Por exemplo, pode adicionar valores que são calculados ou números de versão de outras propriedades.

[Filtragem](app-insights-api-filtering-sampling.md#filtering) pode modificar ou eliminar telemetria antes do envio de Olá SDK implementando `ITelemetryProcesor`. Controlar o que é enviado ou eliminado, mas tiver tooaccount para o efeito de Olá nas métricas. Dependendo de como eliminar itens, poderá perder Olá capacidade toonavigate entre itens relacionados.

[Amostragem](app-insights-api-filtering-sampling.md) é um volume de Olá tooreduce de solução em pacote de dados que são enviados a partir do portal de toohello de aplicação. Isto é feito sem afetar as métricas de Olá apresentado. E copia-sem afetar os problemas de toodiagnose capacidade ao navegar entre itens relacionados, tais como exceções, dos pedidos e vistas de página.

[Saiba mais](app-insights-api-filtering-sampling.md).

## <a name="disabling-telemetry"></a>Desativar a telemetria
demasiado*dinamicamente parar e iniciar* Olá transmissão de telemetria e de coleção:

*C#*

```C#

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```

demasiado*desativar os recoletores padrão selecionados*– por exemplo, os contadores de desempenho, os pedidos de HTTP ou dependências - eliminar ou comente Olá relevantes linhas [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md). Para fazer isto, por exemplo, se quiser toosend os seus próprios dados TrackRequest.

## <a name="debug"></a>Modo de programador
Durante a depuração, é útil toohave a telemetria é emitida através do pipeline de Olá para que possa ver resultados imediatamente. Pode também obter mensagens adicionais que o ajudam a quaisquer problemas com a telemetria de Olá de rastreio. Desactivá-lo na produção, porque pode atrasar da aplicação.

*C#*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = true;

*Visual Basic*

    TelemetryConfiguration.Active.TelemetryChannel.DeveloperMode = True


## <a name="ikey"></a>A definição de chave de instrumentação Olá para telemetria personalizada selecionada
*C#*

    var telemetry = new TelemetryClient();
    telemetry.InstrumentationKey = "---my key---";
    // ...


## <a name="dynamic-ikey"></a>Chave de instrumentação dinâmica
tooavoid a combinação de telemetria de desenvolvimento, teste e ambientes de produção, pode [criar recursos do Application Insights separados](app-insights-create-new-resource.md) e alterar as respetivas chaves, dependendo do ambiente de Olá.

Em vez de obter a chave de instrumentação Olá do ficheiro de configuração de Olá, pode defini-lo no seu código. Defina a chave de Olá um método de inicialização, tais como global.aspx.cs num serviço ASP.NET:

*C#*

    protected void Application_Start()
    {
      Microsoft.ApplicationInsights.Extensibility.
        TelemetryConfiguration.Active.InstrumentationKey =
          // - for example -
          WebConfigurationManager.Settings["ikey"];
      ...

*JavaScript*

    appInsights.config.instrumentationKey = myKey;



Páginas Web, é aconselhável tooset-à partir do servidor web Olá Estado, em vez de codificação-literalmente no script de Olá. Por exemplo, numa página Web gerada por uma aplicação ASP.NET:

*JavaScript em Razor*

    <script type="text/javascript">
    // Standard Application Insights webpage script:
    var appInsights = window.appInsights || function(config){ ...
    // Modify this part:
    }({instrumentationKey:  
      // Generate from server property:
      @Microsoft.ApplicationInsights.Extensibility.
         TelemetryConfiguration.Active.InstrumentationKey"
    }) // ...


## <a name="telemetrycontext"></a>TelemetryContext
TelemetryClient tem uma propriedade de contexto, que contém valores que são enviados juntamente com todos os dados de telemetria. Normalmente definidos por módulos de telemetria padrão Olá, mas também pode defini-los por si. Por exemplo:

    telemetry.Context.Operation.Name = "MyOperationName";

Se qualquer um destes valores por si, considere remover a linha relevante do Olá de [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), para que os valores e valores padrão Olá não obter confundidos.

* **Componente**: Olá aplicação e a respetiva versão.
* **Dispositivo**: dados sobre dispositivos olá onde a aplicação Olá está em execução. (Nas web apps, este é o servidor de Olá ou um dispositivo cliente telemetria Olá enviados a partir.)
* **InstrumentationKey**: Olá recurso do Application Insights no Azure onde a telemetria Olá aparecer. Este é normalmente captado Applicationinsights.
* **Localização**: Olá localização geográfica do dispositivo Olá.
* **Operação**: nas web apps, Olá atual pedido HTTP. Em outros tipos de aplicação, pode definir esta eventos toogroup em conjunto.
  * **ID**: itens relacionados com um valor gerado que está correlacionada com diferentes eventos, para que quando inspecionar qualquer evento na pesquisa de diagnóstico, possam localizar.
  * **Nome**: um identificador, normalmente, Olá URL do pedido de Olá HTTP.
  * **SyntheticSource**: Se não nulo ou está vazio, uma cadeia que indica que origem Olá de pedido de Olá foi identificada como um teste robot ou web. Por predefinição, esta é excluída da cálculos no Explorador de métricas.
* **Propriedades**: propriedades que são enviadas com todos os dados de telemetria. Pode ser substituído nas chamadas controlar * individuais.
* **Sessão**: Olá da sessão de utilizador. ID de Olá definido valor tooa gerado, o que é alterado quando o utilizador Olá não tiver sido Active Directory para o tempo.
* **Utilizador**: informações do utilizador.

## <a name="limits"></a>Limites
[!INCLUDE [application-insights-limits](../../includes/application-insights-limits.md)]

tooavoid atingir o limite de velocidade de dados Olá, utilize [amostragem](app-insights-sampling.md).

toodetermine como são mantidos dados longos, consulte [retenção de dados e privacidade](app-insights-data-retention-privacy.md).

## <a name="reference-docs"></a>Documentos de referência
* [Referência ASP.NET](https://msdn.microsoft.com/library/dn817570.aspx)
* [Referência de Java](http://dl.windowsazure.com/applicationinsights/javadoc/)
* [Referência de JavaScript](https://github.com/Microsoft/ApplicationInsights-JS/blob/master/API-reference.md)
* [SDK do Android](https://github.com/Microsoft/ApplicationInsights-Android)
* [SDK do iOS](https://github.com/Microsoft/ApplicationInsights-iOS)

## <a name="sdk-code"></a>Código do SDK
* [ASP.NET Core SDK](https://github.com/Microsoft/ApplicationInsights-dotnet)
* [ASP.NET 5](https://github.com/Microsoft/ApplicationInsights-aspnet5)
* [Pacotes do Windows Server](https://github.com/Microsoft/applicationInsights-dotnet-server)
* [SDK Java](https://github.com/Microsoft/ApplicationInsights-Java)
* [SDK JavaScript](https://github.com/Microsoft/ApplicationInsights-JS)
* [Todas as plataformas](https://github.com/Microsoft?utf8=%E2%9C%93&query=applicationInsights)

## <a name="questions"></a>Dúvidas
* *As exceções podem emitir chamadas Track_()*

    nenhum. Não precisa de toowrap-las em cláusulas try-catch. Se Olá SDK detetar problemas, irá registar mensagens na saída de consola de depuração Olá e – se hello mensagens chegar - na pesquisa de diagnóstico.
* *Existe um dados tooget de REST API do portal de Olá?*

    Sim, Olá [API de acesso a dados](https://dev.applicationinsights.io/). Incluem outros dados de tooextract formas [exportar de análise tooPower BI](app-insights-export-power-bi.md) e [a exportação contínua](app-insights-export-telemetry.md).

## <a name="next"></a>Passos seguintes
* [Eventos de pesquisa e registos](app-insights-diagnostic-search.md)

* [Resolução de problemas](app-insights-troubleshoot-faq.md)


