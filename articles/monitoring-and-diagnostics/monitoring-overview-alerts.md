---
title: aaaOverview de alertas no Microsoft Azure e o Monitor do Azure | Microsoft Docs
description: "Alertas permitem-lhe toomonitor métricas de recurso do Azure, eventos ou os registos e ser notificados quando for cumprida uma condição que especificar."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: a6dea224-57bf-43d8-a292-06523037d70b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: robb
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: d080080666fedc9eefda6b35cdea3714785d2223
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="what-are-alerts-in-microsoft-azure"></a>O que são alertas no Microsoft Azure?
Este artigo descreve Olá várias origens de alertas no Microsoft Azure, o que são Olá fins de alertas, os seus benefícios e como tooget começar a utilizá-los. -La especificamente aplica-se tooAzure Monitor, mas disponibiliza apontadores tooother serviços, bem como os alertas. Alertas oferecem um método de monitorização no Azure que permite condições tooconfigure sobre dados e ficar notificado quando as condições de Olá corresponderem Olá mais recentes dados de monitorização.

## <a name="taxonomy-of-azure-alerts"></a>Taxonomia de alertas do Azure
Termos seguintes do Azure utiliza Olá toodescribe alertas e as respetivas funções:
* **Alerta** -uma definição de critérios (um ou mais regras ou condições) que torna-se ativado quando cumpridos.
* **Active Directory** - hello de estado quando hello critérios definidos por um alerta for cumprida.
* **Resolvido** - hello de estado quando hello critérios definidos por um alerta já não for cumprida após ter anteriormente foram cumpridos.
* **Notificação** -Olá a ação tomada baseada em termina a sessão de um alerta se tornar Active Directory.
* **Ação** -um recetor de tooa específico chamada, enviada uma notificação (por exemplo, relacionada um endereço ou publicar o URL do webhook tooa). As notificações, normalmente, podem acionar várias ações.

## <a name="alerts-in-different-azure-services"></a>Alertas nas diferentes serviços do Azure
Alertas estão disponíveis no Azure vários serviços de monitorização. Para obter informações sobre como e quando toouse estes serviços, [consulte este artigo](./monitoring-overview.md). Aqui está uma divisão Olá de tipos de alertas disponível através do Azure:

| Serviço | Tipo de alerta | Serviços suportados | Descrição |
|---|---|---|---|
| Azure Monitor | [Métricas alertas](./insights-alerts-portal.md) | [Métricas suportadas do Monitor do Azure](./monitoring-supported-metrics.md) | Receber uma notificação quando qualquer métrica de nível de plataforma cumpre uma condição específica (por exemplo, numa VM de CPU % é superior a 90 para Olá últimos 5 minutos). |
| Azure Monitor | [Alertas de registo de atividade](./monitoring-activity-log-alerts.md) | Todos os tipos de recursos disponíveis no Gestor de recursos do Azure | Receber uma notificação quando um novo evento no Olá [registo de atividade do Azure](./monitoring-overview-activity-logs.md) corresponde condições específicas (por exemplo, se ocorre uma operação de "Eliminar VM" myProductionResourceGroup ou quando um novo evento de estado de funcionamento do serviço com "Ativo" como é apresentado o estado de Olá). |
| Application Insights | [Métricas alertas](../application-insights/app-insights-alerts.md) | Qualquer aplicação instrumentados toosend dados tooApplication Insights | Receber uma notificação quando qualquer métrica de nível de aplicação cumpre uma condição específica (por exemplo, tempo de resposta do servidor é maior do que 2 segundos). |
| Application Insights | [Alertas de teste Web](../application-insights/app-insights-monitor-web-app-availability.md) | Qualquer Web site instrumentados toosend dados tooApplication Insights | Receba uma notificação quando a disponibilidade ou capacidade de resposta de um Web site é inferior a expetativas. |
| Log Analytics | [Alertas de análise do registo](../log-analytics/log-analytics-alerts.md) | Qualquer serviço configurado toosend dados para análise de registos | Receba uma notificação quando uma consulta de pesquisa de análise de registos através de dados de métrica de e/ou eventos cumpra determinados critérios. |

## <a name="alerts-on-azure-monitor-data"></a>Alertas nos dados de monitorização do Azure
Existem dois tipos de alertas retire dados disponíveis a partir do Monitor do Azure – métricas alertas e alertas de registo de atividade.

* **Alertas métricas** -este alerta é acionado quando o valor de Olá de uma métrica especificada atravesse um limiar que atribuir. alerta de Olá gera uma notificação quando o alerta de Olá é "ativado" (quando é ultrapassou o limiar de Olá e Olá alerta condição), bem como quando for "resolvida" (quando o limiar de Olá é cruzado novamente e já não for cumprida a condição de Olá). Para obter uma lista crescente de métricas disponíveis suportadas pelo monitor do Azure, consulte [lista das métricas suportadas no Monitor de Azure](monitoring-supported-metrics.md).
* **Alertas de registo de atividade** -um alerta de registo de transmissão em fluxo que é acionado quando é gerado um evento de registo de atividade que corresponde ao filtrar os critérios que foram atribuídos. Estes alertas tem apenas um Estado "Ativado," uma vez que o motor de alerta de Olá simplesmente aplica Olá filtro critérios tooany novo evento. Estes alertas podem ser utilizado toobecome notificado quando ocorre um novo incidente de estado de funcionamento do serviço ou quando um utilizador ou aplicação efetua uma operação na sua subscrição, por exemplo, "Eliminar a máquina virtual."

Para dados de registo de diagnóstico disponíveis através do Monitor do Azure, sugerimos que dados de encaminhamento Olá para análise de registos e a utilização de um alerta de análise de registos. Olá diagrama a seguir resume as origens de dados no Monitor do Azure e, concecionais, como podem alertá retire dados.

![Alertas explicadas](./media/monitoring-overview-alerts/Alerts_Overview_Resource_v4.png)

## <a name="how-do-i-receive-a-notification-on-an-azure-monitor-alert"></a>Como posso receber uma notificação num alerta de Monitor do Azure?
Historicamente, os alertas do Azure a partir de diferentes serviços utilizado os seus próprios métodos de notificação incorporada. Doravante, o Monitor de Azure oferece um agrupamento de notificação reutilizáveis denominado grupos de ação. Grupos de ação especifiquem um conjunto de recetores para uma notificação – qualquer número de endereços de correio eletrónico, números de telefone (para o SMS) ou URLs de webhook - e sempre que um alerta é ativado que referências Olá grupo ação, todos os recetores recebem essa notificação. Isto permite-lhe tooreuse um agrupamento de recetores (por exemplo, a lista de engenheiro chamada no) em muitos objetos de alerta. Atualmente, apenas os alertas de registo de atividade tornar a utilização de grupos de ação, mas estão a funcionar utilizando a ação grupos, bem como vários outros tipos de alerta do Azure.

Grupos de ação suportam a notificação ao publicar o URL do webhook tooa endereços tooemail de adição e números SMS. Isto permite a automatização e remediação, por exemplo, utilizando:
    - Runbook da Automatização do Azure
    - Função do Azure
    - Aplicação lógica do Azure
    - um serviço de terceiros

Alertas de métricas não ainda a utilizar grupos de ação. Num alerta métrico individual pode configurar notificações para:
* Envie correio eletrónico notificações toohello serviço administrador, os administradores de tooco ou tooadditional endereços de e-mail que especificar.
* Chame um webhook, o que lhe permite toolaunch ações de automatização adicionais.

## <a name="next-steps"></a>Passos seguintes
Obter informações sobre regras de alertas e configurá-los utilizando:

* Saiba mais sobre [métricas](monitoring-overview-metrics.md)
* Configurar [métrica alertas através do portal do Azure](insights-alerts-portal.md)
* Configurar [métrica alertas do PowerShell](insights-alerts-powershell.md)
* Configurar [interface de linha de comandos de alertas de métrica (CLI)](insights-alerts-command-line-interface.md)
* Configurar [métrica alertas de monitorização do Azure REST API](https://msdn.microsoft.com/library/azure/dn931945.aspx)
* Saiba mais sobre [registo de atividade](monitoring-overview-activity-logs.md)
* Configurar [alertas de registo de atividade através do portal do Azure](monitoring-activity-log-alerts.md)
* Configurar [alertas de registo de atividade através do Gestor de recursos](monitoring-create-activity-log-alerts-with-resource-manager-template.md)
* Olá revisão [esquema de webhook alerta de registo de atividade](monitoring-activity-log-alerts-webhook.md)
* Saiba mais sobre [notificações de serviço](monitoring-service-notifications.md)
* Saiba mais sobre [grupos de ação](monitoring-action-groups.md)
