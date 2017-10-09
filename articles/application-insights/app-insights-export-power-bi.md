---
title: aaaExport tooPower BI do Application Insights | Microsoft Docs
description: "As consultas de análises podem ser apresentadas no Power BI."
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="30b60-103">Feed do Power BI do Application Insights</span><span class="sxs-lookup"><span data-stu-id="30b60-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="30b60-104">[Power BI](http://www.powerbi.com/) é um conjunto de ferramentas de análise de negócio que ajudam a analisar os dados e partilhar informações.</span><span class="sxs-lookup"><span data-stu-id="30b60-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="30b60-105">Dashboards avançados estão disponíveis em todos os dispositivos.</span><span class="sxs-lookup"><span data-stu-id="30b60-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="30b60-106">Pode combinar dados de várias origens, incluindo consultas de análises de [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="30b60-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="30b60-107">Existem três métodos para exportar tooPower de dados do Application Insights BI recomendados.</span><span class="sxs-lookup"><span data-stu-id="30b60-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="30b60-108">Pode utilizá-los em separado ou em conjunto.</span><span class="sxs-lookup"><span data-stu-id="30b60-108">You can use them separately or together.</span></span>

* <span data-ttu-id="30b60-109">[**Adaptador do Power BI** ](#power-pi-adapter) -configurar um dashboard completo da telemetria da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="30b60-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="30b60-110">conjunto de Olá de gráficos está predefinido, mas pode adicionar as suas próprias consultas de quaisquer outras fontes.</span><span class="sxs-lookup"><span data-stu-id="30b60-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="30b60-111">[**Exportar as consultas de análises** ](#export-analytics-queries) -escrever qualquer consulta que pretende através da análise e exportá-lo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="30b60-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="30b60-112">Pode colocar esta consulta num dashboard juntamente com quaisquer outros dados.</span><span class="sxs-lookup"><span data-stu-id="30b60-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="30b60-113">[**A exportação contínua e Stream Analytics** ](app-insights-export-stream-analytics.md) -Isto envolve tooset de trabalho mais cópias de segurança.</span><span class="sxs-lookup"><span data-stu-id="30b60-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="30b60-114">Isto é útil se pretender tookeep os dados por períodos longos.</span><span class="sxs-lookup"><span data-stu-id="30b60-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="30b60-115">Caso contrário, hello outros métodos são recomendados.</span><span class="sxs-lookup"><span data-stu-id="30b60-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="30b60-116">Adaptador do Power BI</span><span class="sxs-lookup"><span data-stu-id="30b60-116">Power BI adapter</span></span>
<span data-ttu-id="30b60-117">Este método cria um dashboard completo de telemetria para si.</span><span class="sxs-lookup"><span data-stu-id="30b60-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="30b60-118">conjunto de dados inicial Olá está predefinido, mas pode adicionar mais dados tooit.</span><span class="sxs-lookup"><span data-stu-id="30b60-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="30b60-119">Obter adaptador Olá</span><span class="sxs-lookup"><span data-stu-id="30b60-119">Get hello adapter</span></span>
1. <span data-ttu-id="30b60-120">A iniciar sessão demasiado[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="30b60-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="30b60-121">Abra **obter dados**, **serviços**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="30b60-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Obter a partir da origem de dados do Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="30b60-123">Forneça detalhes de Olá do recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="30b60-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Obter a partir da origem de dados do Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="30b60-125">Aguarde um minuto ou dois para Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="30b60-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Adaptador do Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="30b60-127">Pode editar dashboard Olá, combinar gráficos de Application Insights Olá com as outras origens e com as consultas de análises.</span><span class="sxs-lookup"><span data-stu-id="30b60-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="30b60-128">Há uma galeria de visualização, onde pode obter mais gráficos e cada gráfico tem uma parâmetros que pode definir.</span><span class="sxs-lookup"><span data-stu-id="30b60-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="30b60-129">Após a importação inicial Olá, Olá dashboard e os relatórios de Olá continuar tooupdate diariamente.</span><span class="sxs-lookup"><span data-stu-id="30b60-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="30b60-130">Pode controlar a agenda de atualização de Olá Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="30b60-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="30b60-131">Consultas de análises de exportação</span><span class="sxs-lookup"><span data-stu-id="30b60-131">Export Analytics queries</span></span>
<span data-ttu-id="30b60-132">Esta rota permite-lhe toowrite qualquer análise consultá-lo e, em seguida, exportar esse dashboard do Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="30b60-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="30b60-133">(Pode adicionar dashboard toohello criado pelo adaptador Olá.)</span><span class="sxs-lookup"><span data-stu-id="30b60-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="30b60-134">Uma vez: instalar o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="30b60-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="30b60-135">tooimport a consulta do Application Insights, utilizar Olá versão de ambiente de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="30b60-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="30b60-136">Mas, em seguida, pode publicar este toohello web ou tooyour área de trabalho do Power BI na nuvem.</span><span class="sxs-lookup"><span data-stu-id="30b60-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="30b60-137">Instalar [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="30b60-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="30b60-138">Exportar uma consulta de análise</span><span class="sxs-lookup"><span data-stu-id="30b60-138">Export an Analytics query</span></span>
1. <span data-ttu-id="30b60-139">[Abra a análise e escrever a consulta](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="30b60-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="30b60-140">Testar e refine a consulta de Olá até estiver satisfeito com os resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="30b60-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="30b60-141">**Certifique-se de que consulta Olá é executada corretamente no Analytics antes de exportá-lo.**</span><span class="sxs-lookup"><span data-stu-id="30b60-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="30b60-142">No Olá **exportar** menu, escolha **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="30b60-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="30b60-143">Guarde o ficheiro de texto de Olá.</span><span class="sxs-lookup"><span data-stu-id="30b60-143">Save hello text file.</span></span>
   
    ![Exportar a consulta do Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="30b60-145">Em select do Power BI Desktop **obter dados, a consulta em branco** e, em seguida, no Olá consultar editor, em **vista** selecione **Editor de consultas avançada**.</span><span class="sxs-lookup"><span data-stu-id="30b60-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="30b60-146">Script de idioma M colar Olá exportado para Olá Editor de consultas avançada.</span><span class="sxs-lookup"><span data-stu-id="30b60-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Editor de consultas avançada](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="30b60-148">Poderá ter tooprovide credenciais tooallow Power BI tooaccess do Azure.</span><span class="sxs-lookup"><span data-stu-id="30b60-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="30b60-149">Utilize toosign 'conta institucional' com a sua conta Microsoft.</span><span class="sxs-lookup"><span data-stu-id="30b60-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Forneça credenciais do Azure tooenable Power BI toorun a consulta do Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="30b60-151">(Se precisar de credenciais de Olá tooverify, utilize comandos de menu de definições da origem de dados de Olá Olá Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="30b60-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="30b60-152">Tenha atenção as credenciais de Olá toospecify que utilizar para o Azure, o que pode ser diferente das suas credenciais para o Power BI.)</span><span class="sxs-lookup"><span data-stu-id="30b60-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="30b60-153">Escolha uma visualização para a sua consulta e selecionar Olá campos para o eixo x, eixo y e segmentar dimensão.</span><span class="sxs-lookup"><span data-stu-id="30b60-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Selecione a visualização](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="30b60-155">Publica a sua área de trabalho de nuvem de Power BI de tooyour do relatório.</span><span class="sxs-lookup"><span data-stu-id="30b60-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="30b60-156">A partir daí, pode incorporar uma versão sincronizada para outras páginas web.</span><span class="sxs-lookup"><span data-stu-id="30b60-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Selecione a visualização](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="30b60-158">Atualizar o relatório de Olá manualmente intervalos ou configurar uma atualização agendada na página de opções de Olá.</span><span class="sxs-lookup"><span data-stu-id="30b60-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="30b60-159">Resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="30b60-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="30b60-160">não autorizado 401 ou 403</span><span class="sxs-lookup"><span data-stu-id="30b60-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="30b60-161">Isto pode acontecer se não tiver sido atualizado o seu token refesh.</span><span class="sxs-lookup"><span data-stu-id="30b60-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="30b60-162">Tente tooensure estes passos continuam a ter acesso.</span><span class="sxs-lookup"><span data-stu-id="30b60-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="30b60-163">Se tiver acesso e as credenciais de Olá refershing não funcionar, abra um pedido de suporte.</span><span class="sxs-lookup"><span data-stu-id="30b60-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="30b60-164">Inicie sessão no Portal do Azure de Olá e certifique-se de que pode aceder a recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="30b60-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="30b60-165">Tente toorefresh Olá as credenciais Olá Dashboard</span><span class="sxs-lookup"><span data-stu-id="30b60-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="30b60-166">502 Gateway incorreto</span><span class="sxs-lookup"><span data-stu-id="30b60-166">502 Bad Gateway</span></span>
<span data-ttu-id="30b60-167">Isto é habitualmente provocado por uma consulta de análise que devolve demasiados dados.</span><span class="sxs-lookup"><span data-stu-id="30b60-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="30b60-168">Deve tentar utilizar um intervalo de tempo mais pequeno ou utilizando Olá [há](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) funciona apenas [projeto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Olá campos precisa.</span><span class="sxs-lookup"><span data-stu-id="30b60-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="30b60-169">Se reduzir o conjunto de dados de Olá provenientes da consulta de análise Olá não cumpre os requisitos da sua deve considerar a utilização Olá [API](https://dev.applicationinsights.io/documentation/overview) toopull um conjunto de dados maior.</span><span class="sxs-lookup"><span data-stu-id="30b60-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="30b60-170">Seguem-se instruções sobre como tooconvert Olá M consulta exportar toouse Olá API.</span><span class="sxs-lookup"><span data-stu-id="30b60-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="30b60-171">Criar um [chave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="30b60-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="30b60-172">Olá atualização script de Power BI M que exportou a partir da análise, substituindo Olá ARM URL com a API de AI (consulte o exemplo abaixo)</span><span class="sxs-lookup"><span data-stu-id="30b60-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="30b60-173">Substitua **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="30b60-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="30b60-174">com **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="30b60-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="30b60-175">Por fim, Atualize as credenciais toobasic e utilizar a sua chave de API</span><span class="sxs-lookup"><span data-stu-id="30b60-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="30b60-176">**Script existente**</span><span class="sxs-lookup"><span data-stu-id="30b60-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="30b60-177">**Script atualizado**</span><span class="sxs-lookup"><span data-stu-id="30b60-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="30b60-178">Sobre a amostragem</span><span class="sxs-lookup"><span data-stu-id="30b60-178">About sampling</span></span>
<span data-ttu-id="30b60-179">Se a sua aplicação enviar uma grande quantidade de dados, a funcionalidade de amostragem adaptável Olá pode operar e enviar apenas uma percentagem da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="30b60-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="30b60-180">Olá que mesmo se aplica se manualmente definiu amostragem num Olá SDK ou numa ingestão.</span><span class="sxs-lookup"><span data-stu-id="30b60-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="30b60-181">Saiba mais sobre a amostragem.</span><span class="sxs-lookup"><span data-stu-id="30b60-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="30b60-182">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="30b60-182">Next steps</span></span>
* [<span data-ttu-id="30b60-183">Power BI - Saiba mais</span><span class="sxs-lookup"><span data-stu-id="30b60-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="30b60-184">Tutorial de análise</span><span class="sxs-lookup"><span data-stu-id="30b60-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

