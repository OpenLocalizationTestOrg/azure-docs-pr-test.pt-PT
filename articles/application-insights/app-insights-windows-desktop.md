---
title: "utilização de aaaMonitoring e desempenho para aplicações de ambiente de trabalho do Windows"
description: "Análise da utilização e desempenho da sua aplicação de ambiente de trabalho do Windows com o HockeyApp e o Application Insights."
services: application-insights
documentationcenter: windows
author: CFreemanwa
manager: carmonm
ms.assetid: 19040746-3315-47e7-8c60-4b3000d2ddc4
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/26/2016
ms.author: bwren
ms.openlocfilehash: 73806885a6f0ed3896c0e43308c90ba087007887
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a>Monitorização de utilização e desempenho de aplicações de Ambiente de Trabalho do Windows


O [Azure Application Insights](app-insights-overview.md) e o [HockeyApp](https://hockeyapp.net) permitem-lhe monitorizar a aplicação implementada para utilização e desempenho.

> [!IMPORTANT]
> Recomendamos [HockeyApp](https://hockeyapp.net) toodistribute e monitorizar aplicações de ambiente de trabalho e dispositivos. Com o HockeyApp, pode gerir a distribuição, os testes em direto e os comentários do utilizador, bem como monitorizar relatórios de utilização e falhas. Também pode [exportar e consultar a telemetria com a Análise](app-insights-hockeyapp-bridge-app.md).
> 
> Apesar de telemetria pode ser enviada informações tooApplication de uma aplicação de ambiente de trabalho, este é chiefly úteis para fins de depuração e experimental.
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a>toosend telemetria tooApplication Insights a partir de uma aplicação do Windows
1. No Olá [portal do Azure](https://portal.azure.com), [crie um recurso do Application Insights](app-insights-create-new-resource.md). Para o tipo de aplicação, escolha a aplicação ASP.NET.
2. Efetuar uma cópia da chave de instrumentação de Olá. Localize a chave de Olá na Olá pendente Essentials do novo recurso do Olá que acabou de criar. 
3. No Visual Studio, edite os pacotes de NuGet Olá do seu projeto de aplicação e adicione Microsoft.ApplicationInsights.WindowsServer. (Ou escolha Microsoft.ApplicationInsights se pretender apenas Olá versão simples da API, sem módulos de coleção de telemetria padrão Olá)
4. Chave de instrumentação Olá definido no seu código:
   
    `TelemetryConfiguration.Active.InstrumentationKey = "` *a sua chave* `";` 
   
    ou no Applicationinsights (se tiver instalado um dos pacotes de telemetria padrão Olá):
   
    `<InstrumentationKey>`*a sua chave*`</InstrumentationKey>` 
   
    Se utilizar Applicationinsights, certificar-se de que as respetivas propriedades no Explorador de soluções estão definidas demasiado**ação criar = conteúdo, cópia tooOutput Directory = cópia**.
5. [Utilize a API de Olá](app-insights-api-custom-events-metrics.md) toosend telemetria.
6. Executar a aplicação e ver a telemetria de Olá no recurso de Olá que criou no Olá Portal do Azure.

## <a name="telemetry"></a>Código de exemplo
```C#

    public partial class Form1 : Form
    {
        private TelemetryClient tc = new TelemetryClient();
        ...
        private void Form1_Load(object sender, EventArgs e)
        {
            // Alternative toosetting ikey in config file:
            tc.InstrumentationKey = "key copied from portal";

            // Set session data:
            tc.Context.User.Id = Environment.UserName;
            tc.Context.Session.Id = Guid.NewGuid().ToString();
            tc.Context.Device.OperatingSystem = Environment.OSVersion.ToString();

            // Log a page view:
            tc.TrackPageView("Form1");
            ...
        }

        protected override void OnClosing(CancelEventArgs e)
        {
            stop = true;
            if (tc != null)
            {
                tc.Flush(); // only for desktop apps

                // Allow time for flushing:
                System.Threading.Thread.Sleep(1000);
            }
            base.OnClosing(e);
        }

```

## <a name="next-steps"></a>Passos seguintes
* [Criar um dashboard](app-insights-dashboards.md)
* [Pesquisa de Diagnóstico](app-insights-diagnostic-search.md)
* [Explorar métricas](app-insights-metrics-explorer.md)
* [Escrever consultas da Análise](app-insights-analytics.md)

