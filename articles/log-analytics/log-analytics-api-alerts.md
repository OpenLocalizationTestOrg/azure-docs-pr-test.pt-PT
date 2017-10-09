---
title: "aaaUsing API de REST OMS registo de análise de alerta"
description: "Olá a API de REST de alerta de análise do registo permite-lhe toocreate e gerir alertas na análise de registos que faz parte do Operations Management Suite (OMS).  Este artigo fornece detalhes de Olá API e vários exemplos para efetuar operações diferentes."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 628ad256-7181-4a0d-9e68-4ed60c0f3f04
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 05/12/2017
ms.author: bwren
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 418dc7eb71d6151c6380b8925f1f147a0e13b178
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a>Criar e gerir regras de alertas na análise de registos com a REST API
Olá a API de REST de alerta de análise do registo permite-lhe toocreate e gerir alertas no Operations Management Suite (OMS).  Este artigo fornece detalhes de Olá API e vários exemplos para efetuar operações diferentes.

Olá API de REST de pesquisa de análise de registo é RESTful e pode ser acedido através de Olá API de REST do Azure Resource Manager. Este documento irá encontrar exemplos onde Olá API é acedido a partir de uma linha de comandos do PowerShell utilizando [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comandos de código aberto que simplifica a invocar Olá API do Azure Resource Manager. utilização Olá ARMClient e do PowerShell é uma das muitas opções de Olá de tooaccess API de pesquisa de análise do registo. Com estas ferramentas que pode utilizar Olá RESTful API do Azure Resource Manager toomake chamadas tooOMS áreas de trabalho e executar comandos de pesquisa dentro delas. Olá API será saída tooyou de resultados de pesquisa no formato JSON, permitindo-lhe os resultados da pesquisa Olá toouse de várias maneiras diferentes através de programação.

## <a name="prerequisites"></a>Pré-requisitos
Atualmente, os alertas só podem ser criados com uma procura guardada na análise de registos.  Pode consultar toohello [API de REST do registo de pesquisa](log-analytics-log-search-api.md) para obter mais informações.

## <a name="schedules"></a>Agendas
Uma pesquisa guardada pode ter uma ou mais agendas. Olá agenda define frequência hello pesquisa é executada e intervalo de tempo de Olá através de critérios que Olá é identificado.
As agendas tem propriedades de Olá Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| intervalo |Frequência hello pesquisa é executada. Medido em minutos. |
| QueryTimeSpan |intervalo de tempo de Olá através do qual Olá critérios é avaliada. Tem de ser igual tooor superior ao intervalo. Medido em minutos. |
| Versão |Olá versão de API que está a ser utilizada.  Atualmente, este deve ser sempre definida too1. |

Por exemplo, considere uma consulta de eventos com um intervalo de 15 minutos e um Timespan de 30 minutos. Neste caso, consulta Olá iria ser executada a cada 15 minutos e seria possível acionar um alerta se os critérios de Olá continuaram tooresolve tootrue através de um intervalo de 30 minutos.

### <a name="retrieving-schedules"></a>A obter agendas
Olá utilize obter método tooretrieve todas as agendas de uma procura guardada.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

Olá utilize obter método com um tooretrieve de ID de agenda uma determinada agenda para uma pesquisa guardada.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

Segue-se uma resposta de amostra de uma agenda.

```json
{
    "value": [{
        "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/MyWorkspace/savedSearches/0f0f4853-17f8-4ed1-9a03-8e888b0d16ec/schedules/a17b53ef-bd70-4ca4-9ead-83b00f2024a8",
        "etag": "W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\"",
        "properties": {
            "Interval": 15,
            "QueryTimeSpan": 15
        }
    }]
}
```

### <a name="creating-a-schedule"></a>Criar uma agenda
Utilize o método de Put Olá com um toocreate de ID exclusivo agenda uma nova agenda.  Tenha em atenção que as duas agendas não é possível ter Olá mesmo ID mesmo que se encontrem associados com diferentes das procuras guardadas.  Quando criar uma agenda na consola do OMS Olá, um GUID é criado para o ID de agenda Olá.

> [!NOTE]
> nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a>Editar uma agenda
Utilize o método de Put do Olá com uma agenda existente ID para Olá mesmo guardar pesquisa toomodify agendar.  corpo de Olá de pedido de Olá tem de incluir Olá etag da agenda de Olá.

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a>Agendas de eliminação
Utilize o método de eliminação de Olá com um toodelete de ID de agenda uma agenda.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a>Ações
Uma agenda pode ter várias ações. Uma ação pode definir uma ou mais processos tooperform como enviar uma mensagem ou iniciar um runbook ou pode definir um limiar que determina quando resultados de Olá de uma procura correspondem alguns critérios.  Algumas ações vai definir ambos para que os processos de Olá são efetuados quando Olá limiar ser cumprido.

Todas as ações tem propriedades de Olá Olá a tabela seguinte.  Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.

| Propriedade | Descrição |
|:--- |:--- |
| Tipo |Tipo de ação de Olá.  Atualmente valores possíveis Olá são alerta e o Webhook. |
| Nome |Nome a apresentar para o alerta de Olá. |
| Versão |Olá versão de API que está a ser utilizada.  Atualmente, este deve ser sempre definida too1. |

### <a name="retrieving-actions"></a>A obter ações
Olá utilize obter método tooretrieve todas as ações para uma agenda.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

Olá utilize obter método com Olá ação ID tooretrieve uma ação específica para uma agenda.

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a>Criação ou edição de ações
Utilize o método de Put Olá com um ID de ação que é exclusiva toohello agenda toocreate uma ação de novo.  Quando cria uma ação na consola do OMS Olá, um GUID é Olá ação ID

> [!NOTE]
> nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.

Utilize o método de Put do Olá com uma ação existente ID para Olá mesmo guardar pesquisa toomodify agendar.  corpo de Olá de pedido de Olá tem de incluir Olá etag da agenda de Olá.

formato de pedido de Olá para criar uma nova ação varia consoante o tipo de ação para que estes exemplos são fornecidos nas secções de Olá abaixo.

### <a name="deleting-actions"></a>Eliminar ações
Utilize o método Delete de Olá com Olá ação ID toodelete uma ação.

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a>Ações de alerta
Uma agenda deve ter um e apenas uma ação de alerta.  Ações de alerta de ter uma ou mais das secções Olá Olá a tabela seguinte.  Cada um é descrita mais detalhadamente abaixo.

| Secção | Descrição |
|:--- |:--- |
| Limiar |Critérios de execução da ação de Olá. |
| EmailNotification |Envie correio toomultiple destinatários. |
| Remediação |Iniciar um runbook na automatização do Azure tooattempt toocorrect identificado o problema. |

#### <a name="thresholds"></a>Limiares
Uma ação de alerta deve ter um e apenas um limiar.  Quando os resultados de Olá de uma procura guardada corresponderem limiar Olá numa ação associada essa procura, quaisquer outros processos nessa ação são executados.  Uma ação também pode conter apenas um limiar para que possa ser utilizado com as ações de outros tipos que não contenham limiares.

Limiares tem propriedades de Olá Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| operador |Operador de comparação de limiar de Olá. <br> gt = maior que <br> lt = inferior a |
| Valor |Valor de limiar de Olá. |

Por exemplo, considere uma consulta de eventos com um intervalo de 15 minutos, Timespan de 30 minutos e um limiar de maior que 10. Neste caso, consulta Olá iria ser executada a cada 15 minutos e seria possível acionar um alerta se devolveu 10 eventos que foram criados ao longo de um intervalo de 30 minutos.

Segue-se uma resposta de amostra de uma ação com apenas um limiar.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My threshold action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Version": 1
    }

Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação de limiar para uma agenda.  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de limiar existente para uma agenda.  corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a>Notificação por e-mail
Enviam notificações por e-mail correio tooone ou mais destinatários.  Estas incluírem propriedades Olá Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| Destinatários |Lista de endereços de correio. |
| Assunto |requerente Olá do correio Olá. |
| Anexo |Anexos não são atualmente suportados, pelo que este terão sempre um valor de "None". |

Segue-se uma resposta de amostra de uma ação de notificação de correio eletrónico com um limiar.  

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My email action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "EmailNotification": {
            "Recipients": [
                "recipient1@contoso.com",
                "recipient2@contoso.com"
            ],
            "Subject": "This is hello subject",
            "Attachment": "None"
        },
        "Version": 1
    }

Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma ação de correio eletrónico novo para uma agenda.  Olá exemplo seguinte cria uma notificação por e-mail com um limiar pelo Olá o correio eletrónico é enviado quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de correio eletrónico existente para uma agenda.  corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a>Ações de remediação
Remediações iniciar um runbook na automatização do Azure que tenta problema de Olá toocorrect identificado pelo alerta Olá.  Tem de criar um webhook do runbook Olá utilizado na ação de remediação e, em seguida, especifique Olá URI no Olá WebhookUri propriedade.  Ao criar esta ação utilizando a consola do OMS Olá, é criado automaticamente um novo webhook do runbook Olá.

Remediações incluem propriedades Olá Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| RunbookName |Nome do runbook Olá. Isto deve corresponder ao runbook publicado na conta de automatização de Olá configurado no Olá solução de automatização na sua área de trabalho do OMS. |
| WebhookUri |URI de Olá webhook. |
| Expiração |data de expiração de Olá e a hora de Olá webhook.  Se Olá webhook não tiver uma expiração, em seguida, isto pode ser qualquer data futura válida. |

Segue-se uma resposta de amostra de uma ação de remediação com um limiar.

    "etag": "W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"",
    "properties": {
        "Type": "Alert",
        "Name": "My remediation action",
        "Threshold": {
            "Operator": "gt",
            "Value": 10
        },
        "Remediation": {
            "RunbookName": "My-Runbook",
            "WebhookUri": "https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d",
            "Expiry": "2018-02-25T18:27:20"
            },
        "Version": 1
    }

Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação de remediação para uma agenda.  Olá exemplo seguinte cria uma remediação com um limiar para que Olá runbook é iniciado quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de remediação existente para uma agenda.  corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a>Exemplo
Segue-se um exemplo completo de toocreate um novo alerta de e-mail.  Esta ação cria uma nova agenda juntamente com uma ação que contém um limiar e e-mail.

    $subscriptionId = "3d56705e-5b26-5bcc-9368-dbc8d2fafbfc"
    $resourceGroup  = "MyResourceGroup"    
    $workspaceName    = "MyWorkspace"
    $searchId       = "MySearch"
    $scheduleId     = "MySchedule"
    $thresholdId    = "MyThreshold"
    $actionId       = "MyEmailAction"

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/?api-version=2015-03-20 $scheduleJson

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Severity':'Warning', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/$subscriptionId/resourceGroups/$resourceGroup/providers/Microsoft.OperationalInsights/workspaces/$workspaceName/savedSearches/$searchId/schedules/$scheduleId/actions/$actionId/?api-version=2015-03-20 $emailJson

### <a name="webhook-actions"></a>Ações de Webhook
As ações de Webhook iniciar um processo ao chamar um URL e, opcionalmente, fornecer um toobe payload enviada.  Estes são semelhantes tooRemediation ações exceto no que se destinam para webhooks que pode invocar processos que não sejam runbooks de automatização do Azure.  Também fornecem opção adicional de Olá de fornecer um payload toobe entregar toohello um processo remoto.

As ações de Webhook não dispõe de um limiar, mas em vez disso, devem ser adicionadas tooa agenda que tem uma ação com um limiar de alerta.  Pode adicionar várias ações de Webhook todas serem executadas quando Olá limiar ser cumprido.

As ações de Webhook incluem propriedades Olá no Olá a tabela seguinte.

| Propriedade | Descrição |
|:--- |:--- |
| WebhookUri |requerente Olá do correio Olá. |
| CustomPayload |Payload personalizado toobe enviado toohello webhook.  formato de Olá dependerá que webhook Olá está à espera. |

Segue-se uma resposta de exemplo para a ação de webhook e uma ação de alerta associada com um limiar.

    {
        "__metadata": {},
        "value": [
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/72884702-acf9-4653-bb67-f42436b342b4",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"",
                "properties": {
                    "Type": "Webhook",
                    "Name": "My Webhook Action",
                    "WebhookUri": "https://oaaswebhookdf.cloudapp.net/webhooks?token=VfkYTIlpk%2fc%2bJBP",
                    "CustomPayload": "{\"fielld1\":\"value1\",\"field2\":\"value2\"}",
                    "Version": 1
                }
            },
            {
                "id": "subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/bwren/savedSearches/2d1b30fb-7f48-4de5-9614-79ee244b52de/schedules/b80f5621-7217-4007-b32d-165d14377093/Actions/90a27cf8-71b7-4df2-b04f-54ed01f1e4b6",
                "etag": "W/\"datetime'2016-02-26T20%3A25%3A00.565204Z'\"",
                "properties": {
                    "Type": "Alert",
                    "Name": "Threshold for my webhook action",
                    "Threshold": {
                        "Operator": "gt",
                        "Value": 10
                    },
                    "Version": 1
                }
            }
        ]
    }

#### <a name="create-or-edit-a-webhook-action"></a>Criar ou editar uma ação do webhook
Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação do webhook para uma agenda.  Olá exemplo seguinte cria uma ação de Webhook e uma ação de alerta com um limiar para que Olá webhook será acionada quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

Utilize o método de Put do Olá com um toomodify de ID de ação uma ação do webhook existente para uma agenda.  corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a>Passos seguintes
* Olá utilize [REST API tooperform registo pesquisas](log-analytics-log-search-api.md) na análise de registos.

