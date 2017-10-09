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
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a>Monitorizar e obter informações sobre a execução de aplicação lógica com o Operations Management Suite (OMS) e análise de registos

Para informações de depuração e Rica de monitorização, pode ativar análise de registos em Olá mesmo tempo, quando criar uma aplicação lógica. Análise de registos fornece diagnóstico de registo e monitorização para a sua aplicação lógica é executada através do portal Olá Operations Management Suite (OMS). Quando adiciona tooOMS de solução de gestão de aplicações de lógica de Olá, obter o estado agregado da sua execuções de aplicação de lógica e os detalhes específicos, como o estado, o tempo de execução, o estado de resubmission e o ID de correlação.

Este tópico mostra como tooturn na análise de registos ou instalar Olá solução de gestão de aplicações de lógica no OMS, pelo que pode ver eventos de tempo de execução e execute de dados para a sua aplicação lógica.

 > [!TIP]
 > toomonitor as logic apps existentes, siga estes passos demasiado [ativar o registo de diagnóstico e enviar tooOMS de dados de runtime de aplicação lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).

## <a name="requirements"></a>Requisitos

Antes de começar, terá de toohave uma área de trabalho do OMS. Saiba [como toocreate uma área de trabalho do OMS](../log-analytics/log-analytics-get-started.md). 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a>Ativar o registo de diagnóstico ao criar as logic apps

1. No [portal do Azure](https://portal.azure.com), criar uma aplicação lógica. Escolha **novo** > **integração empresarial com** > **aplicação lógica** > **criar**.

   ![Criar uma aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. No Olá **Criar aplicação de lógica** página, efetuar estas tarefas, conforme mostrado:

   1. Forneça um nome para a sua aplicação lógica e selecione a sua subscrição do Azure. 
   2. Crie ou selecione um grupo de recursos do Azure.
   3. Definir **Log Analytics** demasiado**no**. 
   Executa a área de trabalho do OMS Olá selecione onde pretende demasiado enviar dados para a sua aplicação lógica. 
   4. Quando estiver pronto, selecione **Pin toodashboard** > **criar**.

      ![Criar aplicação lógica](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      Depois de concluir este passo, o Azure cria a aplicação lógica, que está agora associado à sua área de trabalho do OMS. 
      Além disso, este passo instala também automaticamente solução de gestão de aplicações de lógica de Olá na sua área de trabalho do OMS.

3. tooview execução na sua aplicação lógica na OMS, [continuar com estes passos](#view-logic-app-runs-oms).

## <a name="install-hello-logic-apps-management-solution-in-oms"></a>Instalar a solução de gestão de aplicações de lógica de Olá na OMS

Se já ativou análise de registos quando criou a sua aplicação lógica, ignore este passo. Já tem a solução de gestão de aplicações de lógica de Olá instalada no OMS.

1. No Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**. Procure "análise de registos" como o filtro e escolha **Log Analytics** conforme mostrado:

   ![Escolha "Análise de registos"](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. Em **Log Analytics**, localize e selecione a sua área de trabalho do OMS. 

   ![Selecione a sua área de trabalho do OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. Em **gestão**, escolha **Portal do OMS**.

   ![Escolha "Portal do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. Na sua home page do OMS, se for apresentada a faixa de atualização de Olá, escolha a faixa de Olá, para que o primeiro a atualizar a área de trabalho do OMS. Em seguida, escolha **soluções galeria**.

   ![Escolha "Soluções Galeria"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. Em **todas as soluções**, localizar e escolha o mosaico Olá para Olá **de gestão de aplicações lógicas** solução.

   ![Escolha "Lógica de gestão de aplicações"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. Escolha a solução de Olá tooinstall na sua área de trabalho do OMS, **adicionar**.

   ![Escolha "Adicionar" para "Gestão de aplicações lógicas"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a>Vista de que execução na sua aplicação lógica na sua área de trabalho do OMS

1. Contagem de Olá tooview e o estado para a sua aplicação lógica é executado, página de descrição geral de toohello vá para a sua área de trabalho do OMS. Reveja os detalhes de Olá no Olá **de gestão de aplicações lógicas** mosaico.

   ![Mosaico de descrição geral que mostra o estado e contagem de executar de aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > Se esta faixa de atualização é apresentado em vez do mosaico de gestão de aplicações de lógica de Olá, escolha faixa Olá, para que o primeiro a atualizar a área de trabalho do OMS.
  
   > ![Atualizar "Área de trabalho do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. tooview um resumo com mais detalhes sobre as execuções de aplicação lógica, escolha Olá **de gestão de aplicações lógicas** mosaico.

   Aqui, a execução de aplicação lógica é agrupadas por nome ou por Estado de execução.

   ![Executa o estado de resumo para a sua aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. tooview que todas hello é executado para uma aplicação lógica específica ou o estado, a linha de Olá Selecione para um Estado ou de uma aplicação lógica.

   Eis um exemplo que mostra todas as execuções de Olá para uma aplicação lógica específica:

   ![Vista de execução para um Estado ou de uma aplicação lógica](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > Olá **Resubmission** coluna mostra "Sim" para execuções resultam de uma execução submetido novamente.

4. toofilter estes resultados, pode realizar a filtragem do lado do cliente e do lado do servidor.

   * Filtro de lado do cliente: para cada coluna, escolha filtros de Olá que pretende. 
   Eis alguns exemplos:

     ![Filtros de coluna de exemplo](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * Filtro de lado do servidor: toochoose hora específica janela ou toolimit Olá diversas executa que são apresentadas, utilize um controlo de âmbito Olá ao hello parte superior da página Olá. 
   Por predefinição, apenas 1000 registos aparecem uma vez. 
   
     ![Janela de tempo de Olá de alteração](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. tooview todos os Olá ações e os respetivos detalhes para uma execução, específica, selecione uma linha, que abre a página de pesquisa de registo Olá. 

   * tooview estas informações numa tabela, escolha **tabela**.
   * consulta de Olá toochange, pode editar cadeia de consulta Olá na barra de procura Olá. 
   Para uma melhor experiência, escolha **análise avançadas**.

     ![Ver detalhes para uma aplicação lógica de execução e de ações](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     Aqui na página do Olá Log Analytics do Azure, pode atualizar consultas e ver Olá resulta da tabela de Olá. 
     Esta consulta utiliza [idioma de consulta Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que pode editar se quiser tooview diferentes resultados. 

     ![Análise de registos do Azure - vista de consulta](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a>Passos seguintes

* [Monitorizar mensagens B2B](../logic-apps/logic-apps-monitor-b2b-message.md)
