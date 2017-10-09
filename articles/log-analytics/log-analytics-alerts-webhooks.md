---
title: "exemplo de ação alerta aaaWebhook na análise de registos do OMS | Microsoft Docs"
description: "Uma das ações de Olá pode executar no tooa resposta alerta de análise de registos é uma * webhook *, que lhe permite tooinvoke processo externo através de um único pedido HTTP. Este artigo explica-se um exemplo de criação de uma ação de webhook num alerta de análise de registos utilizando Slack."
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: tysonn
ms.assetid: 13c39f0f-fd3c-472d-8324-ddf7538be45e
ms.service: log-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 02/27/2017
ms.author: bwren
ms.openlocfilehash: e60bdc4922347073d572c2e4719461b13e8e7d1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a>Criar uma ação do webhook alerta na análise de registos do OMS toosend mensagem tooSlack
Uma das ações de Olá pode executar numa resposta tooa [alerta de análise de registos](log-analytics-alerts.md) é um *webhook*, que lhe permite tooinvoke processo externo através de um único pedido HTTP.  Pode ler sobre os detalhes de alertas e webhooks no [alertas na análise de registos](log-analytics-alerts.md)

Neste artigo, vamos explicar através de um exemplo de criação de uma ação de webhook num alerta de análise de registos utilizando Slack que é um serviço de mensagens.

> [!NOTE]
> Tem de ter uma conta Slack toocomplete este exemplo.  Pode inscrever-se numa conta gratuita em [slack.com](http://slack.com).
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a>Passo 1 – ativar webhooks no Slack
1. Inicie sessão no tooSlack em [slack.com](http://slack.com).
2. Selecione um canal Olá **canais** secção no painel esquerdo Olá.  Este é o canal de Olá essa mensagem de saudação será enviada para.  Pode selecionar um dos canais de predefinição Olá como **geral** ou **aleatório**.  Num cenário de produção, provavelmente criaria um canal especial, tal como **criticalservicealerts**. <br>
   
   ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. Clique em **adicionar uma aplicação ou integração personalizados** tooopen Olá diretório de aplicação.
4. Tipo *webhooks* na caixa de pesquisa de Olá e, em seguida, selecione **WebHooks entrada**. <br>
   
   ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. Clique em **instalar** nome do agrupamento tooyour seguinte.
6. Clique em **Adicionar configuração**.
7. Canal de Olá Olá selecione que vai toouse para este exemplo e, em seguida, clique em **Adicionar entrada WebHooks integração**.  
8. Olá cópia **URL do Webhook**.  Que irá ser colar isto na configuração de alerta de Olá. <br>
   
    ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a>Passo 2 - Criar regra de alerta na análise de registos
1. [Criar uma regra de alerta](log-analytics-alerts.md) com Olá seguintes definições.
   * Consulta:```    Type=Event EventLevelName=error ```
   * Verificar este alerta cada: 5 minutos
   * número de Olá de resultados é: maiores que 10
   * Durante este período de tempo: 60 minutos
   * Selecione **Sim** para **Webhook** e **não** para Olá outras ações.
2. Olá de colar Slack URL para Olá **URL do Webhook** campo.
3. Selecione a opção de Olá demasiado**incluem um payload JSON personalizado**.
4. Slack espera um payload formatado em JSON, com um parâmetro com o nome *texto*.  Este é o texto de Olá que apresentará a mensagem de saudação cria.  Pode utilizar um ou mais dos parâmetros de alerta Olá utilizando Olá  *#*  símbolo, tais como no seguinte exemplo de Olá.
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![payload JSON de exemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. Clique em **guardar** regra de alerta de Olá toosave.
6. Aguarde algum tempo suficiente para um toobe alerta criado e, em seguida, procurar Slack uma mensagem que será semelhante toohello seguinte.
   
   ![exemplo webhook no Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a>Avançadas payload de webhook para Slack
Amplamente pode personalizar as mensagens de entrada com Slack. Para obter mais informações, consulte [Webhooks entrada](https://api.slack.com/incoming-webhooks) no Web site do Olá Slack. Segue-se um toocreate de payload uma mensagem avançada com formatação mais complexa:

    {
        "attachments": [
            {
                "title":"OMS Alerts Custom Payload",
                "fields": [
                    {
                        "title": "Alert Rule Name",
                        "value": "#alertrulename"},
                    {
                        "title": "Link tooSearchResults",
                        "value": "<#linktosearchresults|OMS Search Results>"},
                    {
                        "title": "Search Interval",
                        "value": "#searchinterval"},
                    {
                        "title": "Threshold Operator",
                        "value": "#thresholdoperator"},
                    {
                        "title": "Threshold Value",
                        "value": "#thresholdvalue"}
                ],
                "color": "#F35A00"
            }
        ]
    }


Isto irá gerar uma mensagem Slack seguir toohello semelhantes.

![mensagem de exemplo na Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a>Resumo
Com esta regra de alerta no local, terá de uma mensagem enviada tooSlack sempre Olá critérios forem satisfeitos.  

Este é apenas um exemplo de uma ação que pode criar no alerta de tooan de resposta.  Pode criar uma ação de webhook que chama outro serviço externo, um toostart de ação de runbook um runbook na automatização do Azure ou um toosend de ação de correio eletrónico um tooyourself de correio ou outros destinatários.   

## <a name="next-steps"></a>Passos Seguintes
* Saiba mais sobre outros [ações na análise de registos de alerta](log-analytics-alerts-actions.md) incluindo outras ações.


