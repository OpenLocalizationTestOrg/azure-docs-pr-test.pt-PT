---
title: "aaaAlert solução de gestão no Operations Management Suite (OMS) | Microsoft Docs"
description: "Olá solução de gestão de alertas no Log Analytics ajuda a analisar todos os alertas de Olá no seu ambiente.  Na adição tooconsolidating os alertas gerados no OMS,-importa alertas de grupos de gestão do System Center Operations Manager ligados para análise de registos."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: fe5d534e-0418-4e2f-9073-8025e13271a8
ms.service: operations-management-suite
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/13/2017
ms.author: bwren
ms.openlocfilehash: aff9bd8d88839c5227bb9ec3a1b5209a3cd7cdf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="alert-management-solution-in-operations-management-suite-oms"></a>Solução de gestão de alerta no Operations Management Suite (OMS)

![Ícone de gestão de alertas](media/log-analytics-solution-alert-management/icon.png)

Olá solução de gestão de alertas ajuda a analisar todos os alertas de Olá no seu repositório de análise de registos.  Estes alertas podem ter provenientes de uma variedade de origens, incluindo as origens [criados pela análise de registos](log-analytics-alerts.md) ou [importados a partir da Nagios ou da Zabbix](log-analytics-linux-agents.md).  Olá solução também importa alertas a partir de qualquer [ligado grupos de gestão do System Center Operations Manager](log-analytics-om-agents.md).

## <a name="prerequisites"></a>Pré-requisitos
solução Olá funciona com qualquer registos no repositório de análise de registos de Olá com um tipo de **alerta**, por isso, tem de efetuar qualquer configuração é necessária toocollect estes registos.

- Existência de alertas de análise de registos, [criar regras de alertas](log-analytics-alerts.md) toocreate registos alerta diretamente no repositório de Olá.
- Existência de alertas da Nagios e da Zabbix, [configurar esses servidores](log-analytics-linux-agents.md) toosend alertas tooLog análise.
- Existência de alertas do System Center Operations Manager, [ligar a sua área de análise de registos do Operations Manager gestão grupo tooyour](log-analytics-om-agents.md).  Todos os alertas criados no System Center Operations Manager são importados para análise de registos.  

## <a name="configuration"></a>Configuração
Adicionar tooyour de solução de gestão de alertas de Olá área de trabalho do OMS através de Olá processo descrita no [adicionar soluções](log-analytics-add-solutions.md).  Não há nenhuma configuração adicional.

## <a name="management-packs"></a>Pacotes de gestão
Se o grupo de gestão do System Center Operations Manager é a área de trabalho do tooyour ligado OMS, Olá os seguintes pacotes de gestão está instalado no System Center Operations Manager ao adicionar esta solução.  Não há nenhuma configuração ou a manutenção Olá de pacotes de gestão necessários.  

* Gestão de alertas do Microsoft System Center Advisor (Microsoft.IntelligencePacks.AlertManagement)

Para obter mais informações sobre a forma como os pacotes de gestão de solução são atualizados, consulte [ligar o Operations Manager tooLog análise](log-analytics-om-agents.md).

## <a name="data-collection"></a>Recolha de dados
### <a name="agents"></a>Agentes
Olá, a tabela seguinte descreve as origens de Olá ligado que são suportadas por esta solução.

| Origem Ligada | Suporte | Descrição |
|:--- |:--- |:--- |
| [Agentes do Windows](log-analytics-windows-agents.md) | Não |Agentes diretos do Windows não gerar alertas.  É possível criar alertas de análise do registo de eventos e dados de desempenho recolhidos a partir do Windows, os agentes. |
| [Agentes do Linux](log-analytics-linux-agents.md) | Não |Diretos agentes Linux não gerar alertas.  Alertas de análise do registo podem ser criadas de eventos e os dados de desempenho recolhidas de agentes Linux.  Alertas da Nagios e da Zabbix são recolhidas a partir desses servidores que necessitam de agente do Linux Olá. |
| [Grupo de gestão do System Center Operations Manager](log-analytics-om-agents.md) |Sim |Alertas que são gerados agentes do Operations Manager são entregues toohello grupo de gestão e, em seguida, reencaminhados tooLog análise.<br><br>Uma ligação direta de tooLog de agentes do Operations Manager não é necessária análise. Dados de alerta são reencaminhados do repositório de análise de registos de toohello de grupo de gestão de Olá. |


### <a name="collection-frequency"></a>Frequência da recolha
- Registos de alertas são a solução de toohello disponíveis assim que são armazenados no repositório de Olá.
- Alerta são enviados dados de Olá do Operations Manager gestão grupo tooLog análise a cada três minutos.  

## <a name="using-hello-solution"></a>Utilizar a solução de Olá
Ao adicionar a área de trabalho do Olá gestão de alertas solução tooyour OMS, Olá **gestão de alertas** mosaico é adicionado o dashboard do tooyour OMS.  Este mosaico mostra uma contagem e a representação gráfica do número de Olá de alertas atualmente ativos que foram geradas dentro de Olá últimas 24 horas.  Não é possível alterar este intervalo de tempo.

![Mosaico de gestão de alertas](media/log-analytics-solution-alert-management/tile.png)

Clique em Olá **gestão de alertas** mosaico tooopen Olá **gestão de alertas** dashboard.  dashboard de Olá inclui colunas Olá Olá a tabela seguinte.  Apresenta uma lista Olá superior 10 alertas por contagem correspondente que critérios da coluna para Olá especificado intervalo de tempo e o âmbito de cada coluna.  Pode executar uma pesquisa de registo que fornece a lista completa de Olá clicando **ver todos os** na parte inferior de Olá da coluna de Olá ou ao clicar no cabeçalho da coluna Olá.

| Coluna | Descrição |
|:--- |:--- |
| Alertas críticos |Todos os alertas com uma gravidade de crítico agrupado por nome do alerta.  Clique em toorun um nome do alerta uma pesquisa de registo devolver todos os registos para esse alerta. |
| Alertas de aviso |Todos os alertas com uma gravidade de aviso agrupado por nome do alerta.  Clique em toorun um nome do alerta uma pesquisa de registo devolver todos os registos para esse alerta. |
| Alertas ativos do SCOM |Todos os alertas recolhidos a partir do Operations Manager com qualquer Estado diferente de *fechado* agrupados por origem esse alerta Olá gerado. |
| Todos os alertas ativos |Todos os alertas com qualquer gravidade agrupados por nome do alerta. Incluir apenas alertas do Operations Manager com qualquer Estado diferente de *fechado*. |

Se se deslocar para a direita toohello, dashboard Olá apresenta uma lista de várias consultas comuns que pode clicar em tooperform um [pesquisa registo](log-analytics-log-searches.md) para dados de alertas.

![Dashboard de gestão de alertas](media/log-analytics-solution-alert-management/dashboard.png)


## <a name="log-analytics-records"></a>Registos do Log Analytics
Olá solução de gestão de alertas analisa qualquer registo com um tipo de **alerta**.  Alertas criados pela análise de registos ou recolhidos a partir da Nagios ou da Zabbix não são recolhidas diretamente pela solução de Olá.

solução Olá importar alertas do System Center Operations Manager e cria um registo correspondente para cada um com um tipo de **alerta** e um SourceSystem de **OpsManager**.  Estes registos tem propriedades de Olá no Olá a tabela seguinte:  

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |*Alerta* |
| SourceSystem |*OpsManager* |
| AlertContext |Detalhes Olá do item de dados que causou Olá toobe de alertas gerado no formato XML. |
| AlertDescription |Descrição detalhada do alerta Olá. |
| AlertId |GUID de alerta de Olá. |
| AlertName |Nome do alerta Olá. |
| AlertPriority |Nível de prioridade de alerta de Olá. |
| AlertSeverity |Nível de gravidade do alerta Olá. |
| AlertState |Mais recente estado de resolução de alerta de Olá. |
| LastModifiedBy |Nome de utilizador Olá alerta Olá da última modificação. |
| ManagementGroupName |Nome do grupo de gestão de Olá em que foi gerado o alerta de Olá. |
| RepeatCount |Número de vezes Olá mesmo alerta foi gerada para Olá que mesmo monitorizado objeto desde que está a ser resolvido. |
| ResolvedBy |Nome de utilizador Olá Olá alerta resolvido. Vazio se o alerta de Olá ainda não foi resolvida. |
| SourceDisplayName |Nome a apresentar da Olá do objeto que gerou o alerta de Olá de monitorização. |
| SourceFullName |Nome completo do Olá do objeto que gerou o alerta de Olá de monitorização. |
| TicketId |ID de permissão para alerta de Olá se o ambiente do System Center Operations Manager de Olá está integrado com um processo para atribuir permissões para alertas.  ID vazio de nenhuma permissão está atribuído. |
| TimeGenerated |Data e hora que Olá alerta foi criado. |
| TimeLastModified |Data e hora que Olá alerta foi alterado pela última vez. |
| TimeRaised |Data e hora que Olá alerta foi gerado. |
| TimeResolved |Data e hora que Olá alerta foi resolvido. Vazio se o alerta de Olá ainda não foi resolvida. |

## <a name="sample-log-searches"></a>Pesquisas de registo de exemplo
Olá tabela seguinte fornece pesquisas de registo de exemplo para registos alertas recolhidos por esta solução: 

| Consulta | Descrição |
|:--- |:--- |
| Tipo = SourceSystem alerta = OpsManager AlertSeverity = erro TimeRaised > agora 24 horas |Alertas críticos gerados nas Olá das últimas 24 horas |
| Tipo = AlertSeverity alerta = aviso TimeRaised > agora 24 horas |Alertas de aviso gerados nas Olá das últimas 24 horas |
| Tipo = SourceSystem alerta = OpsManager AlertState! = TimeRaised fechado > agora 24 horas &#124; medida existente como contagem por SourceDisplayName |Origens com alertas ativos gerados nas Olá das últimas 24 horas |
| Tipo = SourceSystem alerta = OpsManager AlertSeverity = erro TimeRaised > agora 24 horas AlertState! = fechado |Alertas críticos gerados nas Olá das últimas 24 horas que continuam ativos |
| Tipo = SourceSystem alerta = OpsManager TimeRaised > agora 24 horas AlertState = fechado |Alertas gerados durante Olá das últimas 24 horas que agora estão fechadas |
| Tipo = SourceSystem alerta = OpsManager TimeRaised > agora - 1 dia &#124; medida existente como contagem por AlertSeverity |Alertas gerados durante Olá último dia, agrupados pelo respetivo grau de gravidade |
| Tipo = SourceSystem alerta = OpsManager TimeRaised > agora - 1 dia &#124; Ordenar RepeatCount desc |Alertas gerados durante o último dia, ordenados pelo respetivo valor de contagem de repetições de Olá |


>[!NOTE]
> Se a sua área de trabalho tiver sido atualizado toohello [idioma de consulta de análise de registos nova](log-analytics-log-search-upgrade.md), em seguida, Olá precedente consultas alteraria toohello seguinte:
>
>| Consulta | Descrição |
|:---|:---|
| Alertar &#124; onde SourceSystem = = "OpsManager" e AlertSeverity = = "error" e TimeRaised > ago(24h) |Alertas críticos gerados nas Olá das últimas 24 horas |
| Alertar &#124; onde AlertSeverity = = "aviso" e TimeRaised > ago(24h) |Alertas de aviso gerados nas Olá das últimas 24 horas |
| Alertar &#124; onde SourceSystem = = "OpsManager" e AlertState! = "Fechado" e TimeRaised > ago(24h) &#124; resumir contagem = existente pelo SourceDisplayName |Origens com alertas ativos gerados nas Olá das últimas 24 horas |
| Alertar &#124; onde SourceSystem = = "OpsManager" e AlertSeverity = = "error" e TimeRaised > ago(24h) e AlertState! = "Fechado" |Alertas críticos gerados nas Olá das últimas 24 horas que continuam ativos |
| Alertar &#124; onde SourceSystem = = "OpsManager" e TimeRaised > ago(24h) e AlertState = = "Fechado" |Alertas gerados durante Olá das últimas 24 horas que agora estão fechadas |
| Alertar &#124; onde SourceSystem = = "OpsManager" e TimeRaised > ago(1d) &#124; resumir contagem = existente pelo AlertSeverity |Alertas gerados durante Olá último dia, agrupados pelo respetivo grau de gravidade |
| Alertar &#124; onde SourceSystem = = "OpsManager" e TimeRaised > ago(1d) &#124; Ordenar por RepeatCount desc |Alertas gerados durante o último dia, ordenados pelo respetivo valor de contagem de repetições de Olá |


## <a name="next-steps"></a>Passos seguintes
* Veja o artigo [Alerts in Log Analytics](log-analytics-alerts.md) (Alertas no Log Analytics) para obter detalhes sobre a geração de alertas do Log Analytics.
