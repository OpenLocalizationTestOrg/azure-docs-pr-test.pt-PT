---
title: "aaaConfigure webhooks alertas métrica do Azure | Microsoft Docs"
description: "Reroute sistemas de não Azure tooother de alertas do Azure."
author: johnkemnetz
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 8b3ae540-1d19-4f3d-a635-376042f8a5bb
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/03/2017
ms.author: johnkem
ms.openlocfilehash: bc4153ccdcff41c5b9d3c081e59a1bf260d8a283
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-webhook-on-an-azure-metric-alert"></a>Configurar um webhook num alerta métrico do Azure
Webhooks permitem-lhe tooroute um Azure sistemas de notificação de tooother para ações de pós-processamento ou personalizados do alerta. Pode utilizar um webhook de um alerta tooroute-tooservices Enviar SMS, registo de erros, notificar a equipa através de serviços de chat/mensagens ou fazer qualquer número de outras ações. Este artigo descreve como tooset um webhook no alerta métrico do Azure e o payload de Olá para Olá HTTP POST tooa webhook aspeto. Para obter informações sobre a configuração de Olá e esquema de um alerta de registo de atividade do Azure (alerta em eventos), [consulte em vez disso, esta página](insights-auditlog-to-webhook-email.md).

Azure alertas HTTP POST Olá alerta do conteúdo no formato JSON, esquema definido abaixo, tooa webhook URI que fornecem ao criar o alerta de Olá. Este URI tem de ser um ponto final HTTP ou HTTPS válido. Azure mensagens uma entrada por pedido, quando um alerta é ativado.

## <a name="configuring-webhooks-via-hello-portal"></a>Como configurar webhooks através do portal Olá
Pode adicionar ou atualizar o webhook de Olá URI no ecrã de alertas de Create/Update Olá no Olá [portal](https://portal.azure.com/).

![Adicionar uma regra de alerta](./media/insights-webhooks-alerts/Alertwebhook.png)

Também pode configurar um webhook de tooa toopost alerta URI utilizando Olá [Cmdlets do PowerShell do Azure](insights-powershell-samples.md#create-metric-alerts), [CLI de várias plataformas](insights-cli-samples.md#work-with-alerts), ou [API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).

## <a name="authenticating-hello-webhook"></a>Autenticar Olá webhook
webhook de Olá pode autenticar através de autorização baseada em tokens. webhook de Olá URI é guardado com um ID de token, por exemplo. `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`

## <a name="payload-schema"></a>Esquema de payload
Olá operação POST contém Olá seguir JSON payload e o esquema para todos os métrica com base em alertas.

```JSON
{
"status": "Activated",
"context": {
            "timestamp": "2015-08-14T22:26:41.9975398Z",
            "id": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.insights/alertrules/ruleName1",
            "name": "ruleName1",
            "description": "some description",
            "conditionType": "Metric",
            "condition": {
                        "metricName": "Requests",
                        "metricUnit": "Count",
                        "metricValue": "10",
                        "threshold": "10",
                        "windowSize": "15",
                        "timeAggregation": "Average",
                        "operator": "GreaterThanOrEqual"
                },
            "subscriptionId": "s1",
            "resourceGroupName": "useast",                                
            "resourceName": "mysite1",
            "resourceType": "microsoft.foo/sites",
            "resourceId": "/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1",
            "resourceRegion": "centralus",
            "portalLink": "https://portal.azure.com/#resource/subscriptions/s1/resourceGroups/useast/providers/microsoft.foo/sites/mysite1"
},
"properties": {
              "key1": "value1",
              "key2": "value2"
              }
}
```


| Campo | Obrigatório | Fixo conjunto de valores | Notas |
|:--- |:--- |:--- |:--- |
| status |S |"Ativado", "Resolvido" |Estado de alerta de Olá baseado nos condições Olá tiver definido. |
| Contexto |S | |contexto do alerta Olá. |
| carimbo de data/hora |S | |tempo de Olá no qual Olá foi acionado o alerta. |
| ID |S | |Cada regra de alerta tem um id exclusivo. |
| nome |S | |nome do alerta Olá. |
| descrição |S | |Descrição do alerta Olá. |
| conditionType |S |"Métrica", "Evento de" |São suportados dois tipos de alertas. Um baseada numa condição de métrica e Olá outros com base num evento no registo de atividade de Olá. Utilize este valor toocheck se alerta Olá se basear numa métrica ou eventos. |
| Condição |S | |Olá toocheck campos específicos para com base no Olá conditionType. |
| metricName |existência de alertas métricas | |nome de Olá de métrica de Olá que define a regra que Olá monitoriza. |
| metricUnit |existência de alertas métricas |"Bytes", "BytesPerSecond", "Count", "CountPerSecond", "Percentagem", "Segundos" |unidade de Olá permitida no métrica Olá. [Permitido valores estão listados aqui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.unit.aspx). |
| metricValue |existência de alertas métricas | |valor de Olá real de métrica de Olá que causou o alerta de Olá. |
| Limiar |existência de alertas métricas | |valor de limiar de Olá no qual Olá alerta está ativado. |
| windowSize |existência de alertas métricas | |Olá durante período de tempo de atividade de alerta toomonitor utilizados com base num limiar Olá. Tem de estar entre 5 minutos e 1 dia. Formato de duração ISO 8601. |
| timeAggregation |existência de alertas métricas |"Médio", "Último", "Máximo", "Mínimo", "None", "Total de" |Como devem ser combinados dados Olá que são recolhidos ao longo do tempo. valor predefinido de Olá é média. [Permitido valores estão listados aqui](https://msdn.microsoft.com/library/microsoft.azure.insights.models.aggregationtype.aspx). |
| operador |existência de alertas métricas | |utilizar o operador de Olá toocompare Olá atual dados métricos toohello limiar definido. |
| subscriptionId |S | |ID da subscrição do Azure. |
| resourceGroupName |S | |Nome do grupo de recursos de Olá Olá afetado recursos. |
| resourceName |S | |Nome do recurso de Olá afetado recursos. |
| resourceType |S | |Tipo de recurso dos Olá afetado recursos. |
| resourceId |S | |ID de recurso de Olá afetado recursos. |
| resourceRegion |S | |Região ou localização de Olá afetado recursos. |
| portalLink |S | |Ligação direta toohello recursos portal página de resumo. |
| propriedades |N |Opcional |Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento de Olá. o campo de propriedades de Olá é opcional. Num personalizada da IU ou lógica baseada na aplicação fluxo de trabalho, os utilizadores podem introduzir/valores de chave que podem ser transmitidos através de payload Olá. Olá maneira alternativa toopass propriedades personalizadas back toohello webhook é uri de via Olá webhook propriamente dito (como parâmetros de consulta) |

> [!NOTE]
> campo de propriedades de Olá só pode ser definido utilizando Olá [API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx).
>
>

## <a name="next-steps"></a>Passos seguintes
* Saiba mais sobre alertas do Azure e webhooks vídeo Olá [integrar alertas do Azure com PagerDuty](http://go.microsoft.com/fwlink/?LinkId=627080)
* [Executar scripts de automatização do Azure (Runbooks) nos alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Utilizar a aplicação lógica toosend um SMS através do Twilio partir de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
* [Utilizar a aplicação lógica toosend uma mensagem Slack a partir de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
* [Utilizar a aplicação lógica toosend um tooan de mensagem filas do Azure a partir de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)
