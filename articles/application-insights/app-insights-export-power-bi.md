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
# <a name="feed-power-bi-from-application-insights"></a>Feed do Power BI do Application Insights
[Power BI](http://www.powerbi.com/) é um conjunto de ferramentas de análise de negócio que ajudam a analisar os dados e partilhar informações. Dashboards avançados estão disponíveis em todos os dispositivos. Pode combinar dados de várias origens, incluindo consultas de análises de [Azure Application Insights](app-insights-overview.md).

Existem três métodos para exportar tooPower de dados do Application Insights BI recomendados. Pode utilizá-los em separado ou em conjunto.

* [**Adaptador do Power BI** ](#power-pi-adapter) -configurar um dashboard completo da telemetria da sua aplicação. conjunto de Olá de gráficos está predefinido, mas pode adicionar as suas próprias consultas de quaisquer outras fontes.
* [**Exportar as consultas de análises** ](#export-analytics-queries) -escrever qualquer consulta que pretende através da análise e exportá-lo tooPower BI. Pode colocar esta consulta num dashboard juntamente com quaisquer outros dados.
* [**A exportação contínua e Stream Analytics** ](app-insights-export-stream-analytics.md) -Isto envolve tooset de trabalho mais cópias de segurança. Isto é útil se pretender tookeep os dados por períodos longos. Caso contrário, hello outros métodos são recomendados.

## <a name="power-bi-adapter"></a>Adaptador do Power BI
Este método cria um dashboard completo de telemetria para si. conjunto de dados inicial Olá está predefinido, mas pode adicionar mais dados tooit.

### <a name="get-hello-adapter"></a>Obter adaptador Olá
1. A iniciar sessão demasiado[Power BI](https://app.powerbi.com/).
2. Abra **obter dados**, **serviços**, **Application Insights**
   
    ![Obter a partir da origem de dados do Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. Forneça detalhes de Olá do recurso do Application Insights.
   
    ![Obter a partir da origem de dados do Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. Aguarde um minuto ou dois para Olá dados toobe importado.
   
    ![Adaptador do Power BI](./media/app-insights-export-power-bi/010.png)

Pode editar dashboard Olá, combinar gráficos de Application Insights Olá com as outras origens e com as consultas de análises. Há uma galeria de visualização, onde pode obter mais gráficos e cada gráfico tem uma parâmetros que pode definir.

Após a importação inicial Olá, Olá dashboard e os relatórios de Olá continuar tooupdate diariamente. Pode controlar a agenda de atualização de Olá Olá conjunto de dados.

## <a name="export-analytics-queries"></a>Consultas de análises de exportação
Esta rota permite-lhe toowrite qualquer análise consultá-lo e, em seguida, exportar esse dashboard do Power BI tooa. (Pode adicionar dashboard toohello criado pelo adaptador Olá.)

### <a name="one-time-install-power-bi-desktop"></a>Uma vez: instalar o Power BI Desktop
tooimport a consulta do Application Insights, utilizar Olá versão de ambiente de trabalho do Power BI. Mas, em seguida, pode publicar este toohello web ou tooyour área de trabalho do Power BI na nuvem. 

Instalar [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).

### <a name="export-an-analytics-query"></a>Exportar uma consulta de análise
1. [Abra a análise e escrever a consulta](app-insights-analytics-tour.md).
2. Testar e refine a consulta de Olá até estiver satisfeito com os resultados de Olá.

   **Certifique-se de que consulta Olá é executada corretamente no Analytics antes de exportá-lo.**
3. No Olá **exportar** menu, escolha **Power BI (M)**. Guarde o ficheiro de texto de Olá.
   
    ![Exportar a consulta do Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. Em select do Power BI Desktop **obter dados, a consulta em branco** e, em seguida, no Olá consultar editor, em **vista** selecione **Editor de consultas avançada**.

    Script de idioma M colar Olá exportado para Olá Editor de consultas avançada.

    ![Editor de consultas avançada](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. Poderá ter tooprovide credenciais tooallow Power BI tooaccess do Azure. Utilize toosign 'conta institucional' com a sua conta Microsoft.
   
    ![Forneça credenciais do Azure tooenable Power BI toorun a consulta do Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    (Se precisar de credenciais de Olá tooverify, utilize comandos de menu de definições da origem de dados de Olá Olá Editor de consultas. Tenha atenção as credenciais de Olá toospecify que utilizar para o Azure, o que pode ser diferente das suas credenciais para o Power BI.)
2. Escolha uma visualização para a sua consulta e selecionar Olá campos para o eixo x, eixo y e segmentar dimensão.
   
    ![Selecione a visualização](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. Publica a sua área de trabalho de nuvem de Power BI de tooyour do relatório. A partir daí, pode incorporar uma versão sincronizada para outras páginas web.
   
    ![Selecione a visualização](./media/app-insights-export-power-bi/publish-power-bi.png)
4. Atualizar o relatório de Olá manualmente intervalos ou configurar uma atualização agendada na página de opções de Olá.

## <a name="troubleshooting"></a>Resolução de problemas

### <a name="401-or-403-unauthorized"></a>não autorizado 401 ou 403 
Isto pode acontecer se não tiver sido atualizado o seu token refesh. Tente tooensure estes passos continuam a ter acesso. Se tiver acesso e as credenciais de Olá refershing não funcionar, abra um pedido de suporte.

1. Inicie sessão no Portal do Azure de Olá e certifique-se de que pode aceder a recursos de Olá
2. Tente toorefresh Olá as credenciais Olá Dashboard

### <a name="502-bad-gateway"></a>502 Gateway incorreto
Isto é habitualmente provocado por uma consulta de análise que devolve demasiados dados. Deve tentar utilizar um intervalo de tempo mais pequeno ou utilizando Olá [há](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) funciona apenas [projeto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Olá campos precisa.

Se reduzir o conjunto de dados de Olá provenientes da consulta de análise Olá não cumpre os requisitos da sua deve considerar a utilização Olá [API](https://dev.applicationinsights.io/documentation/overview) toopull um conjunto de dados maior. Seguem-se instruções sobre como tooconvert Olá M consulta exportar toouse Olá API.

1. Criar um [chave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)
2. Olá atualização script de Power BI M que exportou a partir da análise, substituindo Olá ARM URL com a API de AI (consulte o exemplo abaixo)
   * Substitua **https://management.azure.com/subscriptions/...**
   * com **https://api.applicationinsights.io/beta/apps/...**
3. Por fim, Atualize as credenciais toobasic e utilizar a sua chave de API
  

**Script existente**
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
**Script atualizado**
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a>Sobre a amostragem
Se a sua aplicação enviar uma grande quantidade de dados, a funcionalidade de amostragem adaptável Olá pode operar e enviar apenas uma percentagem da sua telemetria. Olá que mesmo se aplica se manualmente definiu amostragem num Olá SDK ou numa ingestão. [Saiba mais sobre a amostragem.](app-insights-sampling.md)


## <a name="next-steps"></a>Passos seguintes
* [Power BI - Saiba mais](http://www.powerbi.com/learning/)
* [Tutorial de análise](app-insights-analytics-tour.md)

