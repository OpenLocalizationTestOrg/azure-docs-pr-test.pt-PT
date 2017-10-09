---
title: "aaaMonitor e obter informações sobre a sua aplicação lógica é executado utilizando OMS - Azure Logic Apps | Microsoft Docs"
description: "Monitorizar as execuções de aplicação lógica com o Operations Management Suite (OMS) e de análise de registo insights tooget e detalhes de depuração mais rico para resolução de problemas e diagnóstico"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="e2778-103">Monitorizar e obter informações sobre a execução de aplicação lógica com o Operations Management Suite (OMS) e análise de registos</span><span class="sxs-lookup"><span data-stu-id="e2778-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="e2778-104">Para informações de depuração e Rica de monitorização, pode ativar análise de registos em Olá mesmo tempo, quando criar uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e2778-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="e2778-105">Análise de registos fornece diagnóstico de registo e monitorização para a sua aplicação lógica é executada através do portal Olá Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="e2778-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="e2778-106">Quando adiciona tooOMS de solução de gestão de aplicações de lógica de Olá, obter o estado agregado da sua execuções de aplicação de lógica e os detalhes específicos, como o estado, o tempo de execução, o estado de resubmission e o ID de correlação.</span><span class="sxs-lookup"><span data-stu-id="e2778-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="e2778-107">Este tópico mostra como tooturn na análise de registos ou instalar Olá solução de gestão de aplicações de lógica no OMS, pelo que pode ver eventos de tempo de execução e execute de dados para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e2778-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="e2778-108">toomonitor as logic apps existentes, siga estes passos demasiado [ativar o registo de diagnóstico e enviar tooOMS de dados de runtime de aplicação lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="e2778-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="e2778-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="e2778-109">Requirements</span></span>

<span data-ttu-id="e2778-110">Antes de começar, terá de toohave uma área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="e2778-111">Saiba [como toocreate uma área de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="e2778-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="e2778-112">Ativar o registo de diagnóstico ao criar as logic apps</span><span class="sxs-lookup"><span data-stu-id="e2778-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="e2778-113">No [portal do Azure](https://portal.azure.com), criar uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e2778-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="e2778-114">Escolha **novo** > **integração empresarial com** > **aplicação lógica** > **criar**.</span><span class="sxs-lookup"><span data-stu-id="e2778-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Criar uma aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="e2778-116">No Olá **Criar aplicação de lógica** página, efetuar estas tarefas, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e2778-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="e2778-117">Forneça um nome para a sua aplicação lógica e selecione a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2778-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="e2778-118">Crie ou selecione um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2778-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="e2778-119">Definir **Log Analytics** demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="e2778-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="e2778-120">Executa a área de trabalho do OMS Olá selecione onde pretende demasiado enviar dados para a sua aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e2778-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="e2778-121">Quando estiver pronto, selecione **Pin toodashboard** > **criar**.</span><span class="sxs-lookup"><span data-stu-id="e2778-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Criar aplicação lógica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="e2778-123">Depois de concluir este passo, o Azure cria a aplicação lógica, que está agora associado à sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="e2778-124">Além disso, este passo instala também automaticamente solução de gestão de aplicações de lógica de Olá na sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="e2778-125">tooview execução na sua aplicação lógica na OMS, [continuar com estes passos](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="e2778-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="e2778-126">Instalar a solução de gestão de aplicações de lógica de Olá na OMS</span><span class="sxs-lookup"><span data-stu-id="e2778-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="e2778-127">Se já ativou análise de registos quando criou a sua aplicação lógica, ignore este passo.</span><span class="sxs-lookup"><span data-stu-id="e2778-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="e2778-128">Já tem a solução de gestão de aplicações de lógica de Olá instalada no OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="e2778-129">No Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="e2778-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="e2778-130">Procure "análise de registos" como o filtro e escolha **Log Analytics** conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="e2778-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Escolha "Análise de registos"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="e2778-132">Em **Log Analytics**, localize e selecione a sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecione a sua área de trabalho do OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="e2778-134">Em **gestão**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="e2778-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolha "Portal do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="e2778-136">Na sua home page do OMS, se for apresentada a faixa de atualização de Olá, escolha a faixa de Olá, para que o primeiro a atualizar a área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="e2778-137">Em seguida, escolha **soluções galeria**.</span><span class="sxs-lookup"><span data-stu-id="e2778-137">Then choose **Solutions Gallery**.</span></span>

   ![Escolha "Soluções Galeria"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="e2778-139">Em **todas as soluções**, localizar e escolha o mosaico Olá para Olá **de gestão de aplicações lógicas** solução.</span><span class="sxs-lookup"><span data-stu-id="e2778-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Escolha "Lógica de gestão de aplicações"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="e2778-141">Escolha a solução de Olá tooinstall na sua área de trabalho do OMS, **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="e2778-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Escolha "Adicionar" para "Gestão de aplicações lógicas"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="e2778-143">Vista de que execução na sua aplicação lógica na sua área de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="e2778-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="e2778-144">Contagem de Olá tooview e o estado para a sua aplicação lógica é executado, página de descrição geral de toohello vá para a sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="e2778-145">Reveja os detalhes de Olá no Olá **de gestão de aplicações lógicas** mosaico.</span><span class="sxs-lookup"><span data-stu-id="e2778-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Mosaico de descrição geral que mostra o estado e contagem de executar de aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="e2778-147">Se esta faixa de atualização é apresentado em vez do mosaico de gestão de aplicações de lógica de Olá, escolha faixa Olá, para que o primeiro a atualizar a área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="e2778-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Atualizar "Área de trabalho do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="e2778-149">tooview um resumo com mais detalhes sobre as execuções de aplicação lógica, escolha Olá **de gestão de aplicações lógicas** mosaico.</span><span class="sxs-lookup"><span data-stu-id="e2778-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="e2778-150">Aqui, a execução de aplicação lógica é agrupadas por nome ou por Estado de execução.</span><span class="sxs-lookup"><span data-stu-id="e2778-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Executa o estado de resumo para a sua aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="e2778-152">tooview que todas hello é executado para uma aplicação lógica específica ou o estado, a linha de Olá Selecione para um Estado ou de uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="e2778-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="e2778-153">Eis um exemplo que mostra todas as execuções de Olá para uma aplicação lógica específica:</span><span class="sxs-lookup"><span data-stu-id="e2778-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Vista de execução para um Estado ou de uma aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="e2778-155">Olá **Resubmission** coluna mostra "Sim" para execuções resultam de uma execução submetido novamente.</span><span class="sxs-lookup"><span data-stu-id="e2778-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="e2778-156">toofilter estes resultados, pode realizar a filtragem do lado do cliente e do lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="e2778-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="e2778-157">Filtro de lado do cliente: para cada coluna, escolha filtros de Olá que pretende.</span><span class="sxs-lookup"><span data-stu-id="e2778-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="e2778-158">Eis alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="e2778-158">Here are some examples:</span></span>

     ![Filtros de coluna de exemplo](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="e2778-160">Filtro de lado do servidor: toochoose hora específica janela ou toolimit Olá diversas executa que são apresentadas, utilize um controlo de âmbito Olá ao hello parte superior da página Olá.</span><span class="sxs-lookup"><span data-stu-id="e2778-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="e2778-161">Por predefinição, apenas 1000 registos aparecem uma vez.</span><span class="sxs-lookup"><span data-stu-id="e2778-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Janela de tempo de Olá de alteração](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="e2778-163">tooview todos os Olá ações e os respetivos detalhes para uma execução, específica, selecione uma linha, que abre a página de pesquisa de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="e2778-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="e2778-164">tooview estas informações numa tabela, escolha **tabela**.</span><span class="sxs-lookup"><span data-stu-id="e2778-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="e2778-165">consulta de Olá toochange, pode editar cadeia de consulta Olá na barra de procura Olá.</span><span class="sxs-lookup"><span data-stu-id="e2778-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="e2778-166">Para uma melhor experiência, escolha **análise avançadas**.</span><span class="sxs-lookup"><span data-stu-id="e2778-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Ver detalhes para uma aplicação lógica de execução e de ações](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="e2778-168">Aqui na página do Olá Log Analytics do Azure, pode atualizar consultas e ver Olá resulta da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2778-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="e2778-169">Esta consulta utiliza [idioma de consulta Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que pode editar se quiser tooview diferentes resultados.</span><span class="sxs-lookup"><span data-stu-id="e2778-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Análise de registos do Azure - vista de consulta](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="e2778-171">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e2778-171">Next steps</span></span>

* [<span data-ttu-id="e2778-172">Monitorizar mensagens B2B</span><span class="sxs-lookup"><span data-stu-id="e2778-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
