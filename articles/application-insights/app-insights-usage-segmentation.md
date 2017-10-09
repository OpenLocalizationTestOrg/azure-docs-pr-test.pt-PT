---
title: "análise de aaaUser, sessão e eventos no Azure Application Insights | Documentos da Microsoft"
description: "Análise demográficas dos utilizadores da sua aplicação web."
services: application-insights
documentationcenter: 
author: botatoes
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: multiple
ms.topic: article
ms.date: 05/03/2017
ms.author: bwren
ms.openlocfilehash: 152ab90e9a25c03087d3ebbde1263ec72acb227e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="users-sessions-and-events-analysis-in-application-insights"></a>Análise de utilizadores, sessões e os eventos no Application Insights

Determinar quando pessoas utilizam a sua aplicação web, as páginas que está a mais interessados, onde estão localizados os seus utilizadores, que sistemas operativos e browsers utilizam. Analisar o negócio e telemetria de utilização através da utilização de [Azure Application Insights](app-insights-overview.md).

## <a name="get-started"></a>Introdução

Se não vir ainda dados Olá utilizadores, sessões ou painéis de eventos no portal do Application Insights Olá, [Saiba como utilizar a tooget com ferramentas de utilização de Olá](app-insights-usage-overview.md).

## <a name="hello-users-sessions-and-events-segmentation-tool"></a>ferramenta de segmentação de utilizadores, sessões e os eventos de Olá

Três utilizam painéis de utilização de Olá Olá mesma ferramenta tooslice e organizam telemetria da sua aplicação web de três perspetivas. Ao filtrar e dividir dados Olá, pode descobrir informações sobre a utilização de relativo Olá das páginas diferentes e funcionalidades.

* **Ferramenta de utilizadores**: como muitas pessoas utilizado a aplicação e as respetivas funcionalidades.  Os utilizadores são contados utilizando IDs anónimos armazenados em cookies do browser. Uma única pessoa através de browsers diferentes ou máquinas será contada como mais do que um utilizador.
* **Ferramenta de sessões**: O número de sessões de atividade do utilizador tem incluído determinadas páginas e funcionalidades da sua aplicação. Uma sessão é contabilizada após a meia hora de inatividade do utilizador, ou após contínua 24 horas de utilização.
* **Ferramenta de eventos**: com que frequência são utilizadas determinadas páginas e funcionalidades da sua aplicação. Uma vista de página é contabilizada quando um browser carrega uma página da sua aplicação fornecida tem [instrumentadas-](app-insights-javascript.md). 

    Um evento personalizado representa uma ocorrência de algo acontecer na sua aplicação, muitas vezes, uma interação do utilizador como um botão clique ou Olá concluir algumas tarefas. Inserir código na sua aplicação demasiado[gerar eventos personalizados](app-insights-api-custom-events-metrics.md#trackevent).

![Ferramenta de utilização](./media/app-insights-usage-segmentation/users.png)

## <a name="querying-for-certain-users"></a>Consultar determinados utilizadores 

Explore a diferentes grupos de utilizadores ao ajustar as opções de consulta de Olá na parte superior de Olá da ferramenta de utilizadores Olá: 

* Quem utilizada: escolha eventos personalizados e vistas de página. 
* Durante a: Escolha um intervalo de tempo. 
* Por: Escolha como toobucket Olá dados, por um período de tempo ou por outra propriedade como browser ou uma localidade. 
* Dividir por: Escolha uma propriedade ao que dados de Olá toosplit ou segmento. 
* Adicionar filtros: Limitar os utilizadores toocertain da consulta Olá, sessões ou eventos com base nas respetivas propriedades, tais como o browser ou uma localidade. 
 
## <a name="saving-and-sharing-reports"></a>Guardar e partilhar relatórios 
Pode guardar relatórios de utilizadores, ou privada tooyou apenas na secção dos meus relatórios hello, ou partilhado com todas as pessoas pessoa com acesso toothis recurso do Application Insights no Olá secção relatórios partilhado.  
 
Ao guardar um relatório ou editar as respetivas propriedades, escolha toosave "Relativo intervalo de tempo atual", que um relatório será continuamente atualizada de dados, retroceder alguma quantidade de tempo fixa.  
 
Escolha o "Intervalo atual de tempo absoluto" toosave um relatório com um conjunto de dados fixo. Tenha em atenção que os dados no Application Insights apenas são armazenados durante 90 dias, pelo que o se passem mais do que 90 dias desde um relatório com um intervalo de tempo absoluto foi guardada, relatório de Olá aparecerá em branco. 
 
## <a name="example-instances"></a>Instâncias de exemplo

secção de instâncias de exemplo de Olá mostra informações sobre alguns a utilizadores individuais, sessões ou eventos que são correspondidos por consulta atual Olá. Considerar e explorar os comportamentos Olá indivíduos, em adição tooaggregates, podem fornecer informações sobre como as pessoas utilizam, na verdade, a sua aplicação. 
 
## <a name="insights"></a>Informações 

barra lateral Insights de Olá mostra grandes clusters de utilizadores que partilham propriedades comuns. Esses clusters podem descobrir tendências surprising na forma como as pessoas utilizam a sua aplicação. Por exemplo, se 40% de utilização de Olá da sua aplicação todo provenientes de pessoas através de uma funcionalidade único.  


## <a name="next-steps"></a>Passos seguintes
- utilização de tooenable experiências, começar a enviar [eventos personalizados](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-api-custom-events-metrics#trackevent) ou [vistas de página](https://docs.microsoft.com/azure/application-insights/app-insights-api-custom-events-metrics#page-views).
- Se já enviar eventos personalizados ou vistas de página, explore Olá utilização ferramentas toolearn como os utilizadores utilizam o serviço.
    - [Funis](usage-funnels.md)
    - [Retenção](app-insights-usage-retention.md)
    - [Fluxos do Utilizador](app-insights-usage-flows.md)
    - [Livros](app-insights-usage-workbooks.md)
    - [Adicionar o contexto de utilizador](app-insights-usage-send-user-context.md)

