---
title: os registos de aaaView atividade do Azure com o Log Analytics | Microsoft Docs
description: "Pode utilizar Olá tooanalyze da solução de registos de atividade do Azure e o registo de atividade do Azure de Olá de pesquisa nas suas subscrições do Azure."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: dbac4c73-0058-4191-a906-e59aca8e2ee0
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/07/2017
ms.author: banders
ms.openlocfilehash: 171d0d604d03a5714a9599cc0b448fc5f6471f69
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="view-azure-activity-logs"></a>Ver registos de atividade do Azure

![Símbolo de registos de atividade do Azure](./media/log-analytics-activity/activity-log-analytics.png)

Olá solução de análise de registos de atividade ajuda a analisar e procurar Olá [registo de atividade do Azure](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md) nas suas subscrições do Azure. Olá registo de atividade do Azure é um registo que disponibiliza informações aprofundadas operações de Olá efetuadas nos recursos nas suas subscrições. Olá registo de atividade era anteriormente conhecido como *registos de auditoria* ou *registos operacionais* , uma vez que os relatórios de eventos para as suas subscrições.

Olá registo de atividade pode determinar Olá *que*, *quem*, e *quando* para quaisquer operações (PUT, POST, DELETE) efetuadas para recursos de Olá na sua subscrição de escrita. Também pode compreender o estado de Olá das operações de Olá e outras propriedades relevantes. Olá registo de atividade inclui leitura operações (GET) ou as operações para recursos que utilizam o modelo de implementação clássica Olá.

Quando se liga a tooLog de registos de atividade do Azure análise, pode:

- Analisar os registos de atividade de Olá com vistas predefinidos
- Analisar e registos de pesquisa e a atividade de várias subscrições do Azure
- Mantenha os registos de atividade para mais de 90 dias<sup>1</sup>
- Correlacionar os registos de atividade com outro Azure plataforma e dados de aplicações
- Ver as atividades operacionais agregadas pelo Estado
- Ver tendências de atividades a acontecer em cada um dos seus serviços do Azure
- Relatório sobre as alterações de autorização em todos os seus recursos do Azure
- Identificar problemas de estado de funcionamento de serviço ou falha afetar os recursos
- Utilize atividades de utilizador de toocorrelate de pesquisa de registo, as operações de dimensionamento automático, as alterações de autorização e registos de tooother de estado de funcionamento do serviço ou as métricas do seu ambiente

<sup>1</sup>por predefinição, análise de registos mantém os seus registos de atividade do Azure para 90 dias, mesmo que estejam no escalão gratuito Olá. Em alternativa, se tiver uma definição de retenção de área de trabalho de inferior a 90 dias. Se a sua área de trabalho tiver retenção é maior do que 90 dias, os registos de atividade Olá são mantidos durante o período de retenção de Olá da sua área de trabalho.

Análise de registos recolhe registos de atividade gratuitas e armazena os registos de Olá gratuitas de 90 dias. Se armazenar os registos para mais de 90 dias, será cobrado custo de retenção de dados para dados de Olá armazenados já mais do que 90 dias.

Quando estiver no Olá livres escalão de preço, registos de atividade não aplicam tooyour consumo de dados diária.

## <a name="connected-sources"></a>Origens ligadas

Ao contrário da maioria das outras soluções de análise de registos, os dados não estão recolhidos para registos de atividade por agentes. Todos os dados utilizados pela solução de Olá vem diretamente a partir do Azure.

| Origem Ligada | Suportado | Descrição |
| --- | --- | --- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não | solução Olá recolhe informações de agentes do Windows. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não | solução Olá recolhe informações de agentes Linux. |
| [Grupo de gestão do SCOM](log-analytics-om-agents.md) | Não | solução Olá recolhe informações de agentes num grupo de gestão do SCOM ligado. |
| [Conta de armazenamento do Azure](log-analytics-azure-storage.md) | Não | solução Olá recolhe informações de armazenamento do Azure. |

## <a name="prerequisites"></a>Pré-requisitos

- tooaccess informações de registo de atividade do Azure, tem de ter uma subscrição do Azure.

## <a name="configuration"></a>Configuração

Efetue Olá seguir a solução de análise do registo de atividade do passos tooconfigure Olá para as áreas de trabalho.

1. Ativar a solução de análise de registos de atividade Olá de Olá [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.AzureActivityOMS?tab=Overview) ou utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).
2. Configure a área de trabalho do atividade registos toogo tooyour análise de registos.
    1. No Olá portal do Azure, selecione a área de trabalho e, em seguida, clique em **registo de atividade do Azure**.
    2. Para cada subscrição, clique em nome da subscrição Olá.  
        ![Adicionar subscrição](./media/log-analytics-activity/add-subscription.png)
    3. No Olá *SubscriptionName* painel, clique em **Connect**.  
        ![ligar a subscrição](./media/log-analytics-activity/subscription-connect.png)

Se adicionar solução Olá utilizando o portal do OMS Olá, verá a seguinte Olá mosaico. Inicie sessão no toohello tooconnect portal do Azure uma área de trabalho de tooyour de subscrição do Azure.  
![efetuar a avaliação](./media/log-analytics-activity/tile-performing-assessment.png)

## <a name="using-hello-solution"></a>Utilizar a solução de Olá

Ao adicionar a área de trabalho do Olá análise de registos de atividade solução tooyour, Olá **registos de atividade do Azure** mosaico é adicionado o dashboard de descrição geral de tooyour. Este mosaico mostra uma contagem do número de Olá de registos de actividades do Azure para hello subscrições do Azure que solução de Olá tem acesso.

![Mosaico de registos de atividade do Azure](./media/log-analytics-activity/azure-activity-logs-tile.png)

### <a name="view-azure-activity-logs"></a>Regista a atividade do Azure de vista

Clique em Olá **registos de atividade do Azure** mosaico tooopen Olá **registos de atividade do Azure** dashboard. dashboard de Olá inclui painéis de Olá Olá a tabela seguinte. Apresenta uma lista dos itens de too10 correspondente que critérios do painel para Olá especificado intervalo de tempo e o âmbito de cada painel. Pode executar uma pesquisa de registo que devolve todos os registos clicando **ver todos os** na parte inferior de Olá do painel de Olá ou clicando cabeçalho do painel de Olá.

Dados de registo de atividade só é apresentada *depois* que tiver configurado a sua solução toohello toogo registos de atividade, pelo que não é possível ver os dados antes.

| Painel | Descrição |
| --- | --- |
| Entradas de registo de atividade do Azure | Mostra um gráfico de barras de principais de Olá entrada de registo de atividade do Azure totais registos Olá período de tempo selecionado e mostra uma lista de Olá os chamadores de atividade 10 principais. Clique em Olá gráfico de barras toorun uma pesquisa de registo para <code>Type=AzureActivity</code>. Clique num toorun de item de autor da chamada uma pesquisa de registo devolver todas as entradas de registo de atividade para esse item. |
| Registos de atividade por Estado | Mostra um gráfico de anel para o estado de registo de atividade do Azure Olá período de tempo que selecionou. Também mostra uma lista uma lista de registos de estado dez principais Olá. Clique em Olá gráfico toorun uma pesquisa de registo para <code>Type=AzureActivity &#124; measure count() by ActivityStatus</code>. Clique num toorun de item de estado uma pesquisa de registo devolver todas as entradas de registo de atividade para esse registo de estado. |
| Registos de atividade por recurso | Mostra o número total de Olá de recursos com registos de atividade e apresenta uma lista de principais de Olá contagens de dez recursos com o registo de cada recurso. Clique em Olá área total toorun uma pesquisa de registo para <code>Type=AzureActivity &#124; measure count() by Resource</code>, que mostra todos os recursos do Azure disponíveis toohello solução. Clique em toorun um recurso uma pesquisa de registo devolver todos os registos de atividade para esse recurso. |
| Registos de atividade pelo fornecedor de recursos | Mostra Olá número total de fornecedores de recursos que produzem atividade regista e apresenta uma lista de principais de Olá dez. Clique em Olá área total toorun uma pesquisa de registo para <code>Type=AzureActivity &#124; measure count() by ResourceProvider</code>, que mostra todos os fornecedores de recursos do Azure. Clique num toorun de fornecedor de recursos uma pesquisa de registo todos os registos de atividade para o fornecedor de Olá a devolver. |

![Dashboard de registos de atividade do Azure](./media/log-analytics-activity/activity-log-dash.png)

## <a name="next-steps"></a>Passos seguintes

- Criar um [alerta](log-analytics-alerts-creating.md) quando ocorre uma atividade específica.
- Utilize [pesquisa registo](log-analytics-log-searches.md) tooview detalhadas informações dos seus registos de atividade.
