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
# <a name="monitoring-usage-and-performance-in-windows-desktop-apps"></a><span data-ttu-id="1dea2-103">Monitorização de utilização e desempenho de aplicações de Ambiente de Trabalho do Windows</span><span class="sxs-lookup"><span data-stu-id="1dea2-103">Monitoring usage and performance in Windows Desktop apps</span></span>


<span data-ttu-id="1dea2-104">O [Azure Application Insights](app-insights-overview.md) e o [HockeyApp](https://hockeyapp.net) permitem-lhe monitorizar a aplicação implementada para utilização e desempenho.</span><span class="sxs-lookup"><span data-stu-id="1dea2-104">[Azure Application Insights](app-insights-overview.md) and [HockeyApp](https://hockeyapp.net) let you monitor your deployed application for usage and performance.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1dea2-105">Recomendamos [HockeyApp](https://hockeyapp.net) toodistribute e monitorizar aplicações de ambiente de trabalho e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="1dea2-105">We recommend [HockeyApp](https://hockeyapp.net) toodistribute and monitor desktop and device apps.</span></span> <span data-ttu-id="1dea2-106">Com o HockeyApp, pode gerir a distribuição, os testes em direto e os comentários do utilizador, bem como monitorizar relatórios de utilização e falhas.</span><span class="sxs-lookup"><span data-stu-id="1dea2-106">With HockeyApp, you can manage distribution, live testing, and user feedback, as well as monitor usage and crash reports.</span></span> <span data-ttu-id="1dea2-107">Também pode [exportar e consultar a telemetria com a Análise](app-insights-hockeyapp-bridge-app.md).</span><span class="sxs-lookup"><span data-stu-id="1dea2-107">You can also [export and query your telemetry with Analytics](app-insights-hockeyapp-bridge-app.md).</span></span>
> 
> <span data-ttu-id="1dea2-108">Apesar de telemetria pode ser enviada informações tooApplication de uma aplicação de ambiente de trabalho, este é chiefly úteis para fins de depuração e experimental.</span><span class="sxs-lookup"><span data-stu-id="1dea2-108">Although telemetry can be sent tooApplication Insights from a desktop application, this is chiefly useful for debugging and experimental purposes.</span></span>
> 
> 

## <a name="toosend-telemetry-tooapplication-insights-from-a-windows-application"></a><span data-ttu-id="1dea2-109">toosend telemetria tooApplication Insights a partir de uma aplicação do Windows</span><span class="sxs-lookup"><span data-stu-id="1dea2-109">toosend telemetry tooApplication Insights from a Windows application</span></span>
1. <span data-ttu-id="1dea2-110">No Olá [portal do Azure](https://portal.azure.com), [crie um recurso do Application Insights](app-insights-create-new-resource.md).</span><span class="sxs-lookup"><span data-stu-id="1dea2-110">In hello [Azure portal](https://portal.azure.com), [create an Application Insights resource](app-insights-create-new-resource.md).</span></span> <span data-ttu-id="1dea2-111">Para o tipo de aplicação, escolha a aplicação ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="1dea2-111">For application type, choose ASP.NET app.</span></span>
2. <span data-ttu-id="1dea2-112">Efetuar uma cópia da chave de instrumentação de Olá.</span><span class="sxs-lookup"><span data-stu-id="1dea2-112">Take a copy of hello Instrumentation Key.</span></span> <span data-ttu-id="1dea2-113">Localize a chave de Olá na Olá pendente Essentials do novo recurso do Olá que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="1dea2-113">Find hello key in hello Essentials drop-down of hello new resource you just created.</span></span> 
3. <span data-ttu-id="1dea2-114">No Visual Studio, edite os pacotes de NuGet Olá do seu projeto de aplicação e adicione Microsoft.ApplicationInsights.WindowsServer.</span><span class="sxs-lookup"><span data-stu-id="1dea2-114">In Visual Studio, edit hello NuGet packages of your app project, and add Microsoft.ApplicationInsights.WindowsServer.</span></span> <span data-ttu-id="1dea2-115">(Ou escolha Microsoft.ApplicationInsights se pretender apenas Olá versão simples da API, sem módulos de coleção de telemetria padrão Olá)</span><span class="sxs-lookup"><span data-stu-id="1dea2-115">(Or choose Microsoft.ApplicationInsights if you just want hello bare API, without hello standard telemetry collection modules.)</span></span>
4. <span data-ttu-id="1dea2-116">Chave de instrumentação Olá definido no seu código:</span><span class="sxs-lookup"><span data-stu-id="1dea2-116">Set hello instrumentation key either in your code:</span></span>
   
    <span data-ttu-id="1dea2-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *a sua chave* `";`</span><span class="sxs-lookup"><span data-stu-id="1dea2-117">`TelemetryConfiguration.Active.InstrumentationKey = "` *your key* `";`</span></span> 
   
    <span data-ttu-id="1dea2-118">ou no Applicationinsights (se tiver instalado um dos pacotes de telemetria padrão Olá):</span><span class="sxs-lookup"><span data-stu-id="1dea2-118">or in ApplicationInsights.config (if you installed one of hello standard telemetry packages):</span></span>
   
    <span data-ttu-id="1dea2-119">`<InstrumentationKey>`*a sua chave*`</InstrumentationKey>`</span><span class="sxs-lookup"><span data-stu-id="1dea2-119">`<InstrumentationKey>`*your key*`</InstrumentationKey>`</span></span> 
   
    <span data-ttu-id="1dea2-120">Se utilizar Applicationinsights, certificar-se de que as respetivas propriedades no Explorador de soluções estão definidas demasiado**ação criar = conteúdo, cópia tooOutput Directory = cópia**.</span><span class="sxs-lookup"><span data-stu-id="1dea2-120">If you use ApplicationInsights.config, make sure its properties in Solution Explorer are set too**Build Action = Content, Copy tooOutput Directory = Copy**.</span></span>
5. <span data-ttu-id="1dea2-121">[Utilize a API de Olá](app-insights-api-custom-events-metrics.md) toosend telemetria.</span><span class="sxs-lookup"><span data-stu-id="1dea2-121">[Use hello API](app-insights-api-custom-events-metrics.md) toosend telemetry.</span></span>
6. <span data-ttu-id="1dea2-122">Executar a aplicação e ver a telemetria de Olá no recurso de Olá que criou no Olá Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="1dea2-122">Run your app, and see hello telemetry in hello resource you created in hello Azure Portal.</span></span>

## <span data-ttu-id="1dea2-123"><a name="telemetry"></a>Código de exemplo</span><span class="sxs-lookup"><span data-stu-id="1dea2-123"><a name="telemetry"></a>Example code</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="1dea2-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1dea2-124">Next steps</span></span>
* [<span data-ttu-id="1dea2-125">Criar um dashboard</span><span class="sxs-lookup"><span data-stu-id="1dea2-125">Create a dashboard</span></span>](app-insights-dashboards.md)
* [<span data-ttu-id="1dea2-126">Pesquisa de Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="1dea2-126">Diagnostic Search</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="1dea2-127">Explorar métricas</span><span class="sxs-lookup"><span data-stu-id="1dea2-127">Explore metrics</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="1dea2-128">Escrever consultas da Análise</span><span class="sxs-lookup"><span data-stu-id="1dea2-128">Write Analytics queries</span></span>](app-insights-analytics.md)

