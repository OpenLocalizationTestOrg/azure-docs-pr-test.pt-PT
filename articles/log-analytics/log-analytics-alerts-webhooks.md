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
# <a name="create-an-alert-webhook-action-in-oms-log-analytics-toosend-message-tooslack"></a><span data-ttu-id="305c1-104">Criar uma ação do webhook alerta na análise de registos do OMS toosend mensagem tooSlack</span><span class="sxs-lookup"><span data-stu-id="305c1-104">Create an alert webhook action in OMS Log Analytics toosend message tooSlack</span></span>
<span data-ttu-id="305c1-105">Uma das ações de Olá pode executar numa resposta tooa [alerta de análise de registos](log-analytics-alerts.md) é um *webhook*, que lhe permite tooinvoke processo externo através de um único pedido HTTP.</span><span class="sxs-lookup"><span data-stu-id="305c1-105">One of hello actions you can run in response tooa [Log Analytics alert](log-analytics-alerts.md) is a *webhook*, which allows you tooinvoke an external process through a single HTTP request.</span></span>  <span data-ttu-id="305c1-106">Pode ler sobre os detalhes de alertas e webhooks no [alertas na análise de registos](log-analytics-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="305c1-106">You can read about details of alerts and webhooks in [Alerts in Log Analytics](log-analytics-alerts.md)</span></span>

<span data-ttu-id="305c1-107">Neste artigo, vamos explicar através de um exemplo de criação de uma ação de webhook num alerta de análise de registos utilizando Slack que é um serviço de mensagens.</span><span class="sxs-lookup"><span data-stu-id="305c1-107">In this article, we’ll walk through an example of creating a webhook action in a Log Analytics alert using Slack which is a messaging service.</span></span>

> [!NOTE]
> <span data-ttu-id="305c1-108">Tem de ter uma conta Slack toocomplete este exemplo.</span><span class="sxs-lookup"><span data-stu-id="305c1-108">You must have a Slack account toocomplete this sample.</span></span>  <span data-ttu-id="305c1-109">Pode inscrever-se numa conta gratuita em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="305c1-109">You can sign up for a free account at [slack.com](http://slack.com).</span></span>
> 
> 

## <a name="step-1---enable-webhooks-in-slack"></a><span data-ttu-id="305c1-110">Passo 1 – ativar webhooks no Slack</span><span class="sxs-lookup"><span data-stu-id="305c1-110">Step 1 - Enable webhooks in Slack</span></span>
1. <span data-ttu-id="305c1-111">Inicie sessão no tooSlack em [slack.com](http://slack.com).</span><span class="sxs-lookup"><span data-stu-id="305c1-111">Sign in tooSlack at [slack.com](http://slack.com).</span></span>
2. <span data-ttu-id="305c1-112">Selecione um canal Olá **canais** secção no painel esquerdo Olá.</span><span class="sxs-lookup"><span data-stu-id="305c1-112">Select a channel in hello **Channels** section in hello left pane.</span></span>  <span data-ttu-id="305c1-113">Este é o canal de Olá essa mensagem de saudação será enviada para.</span><span class="sxs-lookup"><span data-stu-id="305c1-113">This is hello channel that hello message will be sent to.</span></span>  <span data-ttu-id="305c1-114">Pode selecionar um dos canais de predefinição Olá como **geral** ou **aleatório**.</span><span class="sxs-lookup"><span data-stu-id="305c1-114">You can select one of hello default channels such as **general** or **random**.</span></span>  <span data-ttu-id="305c1-115">Num cenário de produção, provavelmente criaria um canal especial, tal como **criticalservicealerts**.</span><span class="sxs-lookup"><span data-stu-id="305c1-115">In a production scenario, you would most likely create a special channel such as **criticalservicealerts**.</span></span> <br>
   
   ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks01.png)
3. <span data-ttu-id="305c1-117">Clique em **adicionar uma aplicação ou integração personalizados** tooopen Olá diretório de aplicação.</span><span class="sxs-lookup"><span data-stu-id="305c1-117">Click **Add an app or custom integration** tooopen hello App Directory.</span></span>
4. <span data-ttu-id="305c1-118">Tipo *webhooks* na caixa de pesquisa de Olá e, em seguida, selecione **WebHooks entrada**.</span><span class="sxs-lookup"><span data-stu-id="305c1-118">Type *webhooks* into hello search box and then select **Incoming WebHooks**.</span></span> <br>
   
   ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks02.png)
5. <span data-ttu-id="305c1-120">Clique em **instalar** nome do agrupamento tooyour seguinte.</span><span class="sxs-lookup"><span data-stu-id="305c1-120">Click **Install** next tooyour team name.</span></span>
6. <span data-ttu-id="305c1-121">Clique em **Adicionar configuração**.</span><span class="sxs-lookup"><span data-stu-id="305c1-121">Click **Add Configuration**.</span></span>
7. <span data-ttu-id="305c1-122">Canal de Olá Olá selecione que vai toouse para este exemplo e, em seguida, clique em **Adicionar entrada WebHooks integração**.</span><span class="sxs-lookup"><span data-stu-id="305c1-122">Select hello hello channel that you're going toouse for this example, and then click **Add Incoming WebHooks integration**.</span></span>  
8. <span data-ttu-id="305c1-123">Olá cópia **URL do Webhook**.</span><span class="sxs-lookup"><span data-stu-id="305c1-123">Copy hello **Webhook URL**.</span></span>  <span data-ttu-id="305c1-124">Que irá ser colar isto na configuração de alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="305c1-124">You'll be pasting this into hello Alert configuration.</span></span> <br>
   
    ![Nos canais slack](media/log-analytics-alerts-webhooks/oms-webhooks05.png)

## <a name="step-2---create-alert-rule-in-log-analytics"></a><span data-ttu-id="305c1-126">Passo 2 - Criar regra de alerta na análise de registos</span><span class="sxs-lookup"><span data-stu-id="305c1-126">Step 2 - Create alert rule in Log Analytics</span></span>
1. <span data-ttu-id="305c1-127">[Criar uma regra de alerta](log-analytics-alerts.md) com Olá seguintes definições.</span><span class="sxs-lookup"><span data-stu-id="305c1-127">[Create an alert rule](log-analytics-alerts.md) with hello following settings.</span></span>
   * <span data-ttu-id="305c1-128">Consulta:```    Type=Event EventLevelName=error ```</span><span class="sxs-lookup"><span data-stu-id="305c1-128">Query: ```    Type=Event EventLevelName=error ```</span></span>
   * <span data-ttu-id="305c1-129">Verificar este alerta cada: 5 minutos</span><span class="sxs-lookup"><span data-stu-id="305c1-129">Check for this alert every: 5 minutes</span></span>
   * <span data-ttu-id="305c1-130">número de Olá de resultados é: maiores que 10</span><span class="sxs-lookup"><span data-stu-id="305c1-130">hello number of results is: greater than 10</span></span>
   * <span data-ttu-id="305c1-131">Durante este período de tempo: 60 minutos</span><span class="sxs-lookup"><span data-stu-id="305c1-131">Over this time window: 60 minutes</span></span>
   * <span data-ttu-id="305c1-132">Selecione **Sim** para **Webhook** e **não** para Olá outras ações.</span><span class="sxs-lookup"><span data-stu-id="305c1-132">Select **Yes** for **Webhook** and **No** for hello other actions.</span></span>
2. <span data-ttu-id="305c1-133">Olá de colar Slack URL para Olá **URL do Webhook** campo.</span><span class="sxs-lookup"><span data-stu-id="305c1-133">Paste hello Slack URL into hello **Webhook URL** field.</span></span>
3. <span data-ttu-id="305c1-134">Selecione a opção de Olá demasiado**incluem um payload JSON personalizado**.</span><span class="sxs-lookup"><span data-stu-id="305c1-134">Select hello option too**include a custom JSON payload**.</span></span>
4. <span data-ttu-id="305c1-135">Slack espera um payload formatado em JSON, com um parâmetro com o nome *texto*.</span><span class="sxs-lookup"><span data-stu-id="305c1-135">Slack expects a payload formatted in JSON with a parameter named *text*.</span></span>  <span data-ttu-id="305c1-136">Este é o texto de Olá que apresentará a mensagem de saudação cria.</span><span class="sxs-lookup"><span data-stu-id="305c1-136">This is hello text that it will display in hello message it creates.</span></span>  <span data-ttu-id="305c1-137">Pode utilizar um ou mais dos parâmetros de alerta Olá utilizando Olá  *#*  símbolo, tais como no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="305c1-137">You can use one or more of hello alert parameters using hello *#* symbol such as in hello following example.</span></span>
   
    ```
    {
    "text":"#alertrulename fired with #searchresultcount records which exceeds hello over threshold of #thresholdvalue ."
    }
    ```
   
    ![payload JSON de exemplo](media/log-analytics-alerts-webhooks/oms-webhooks07.png)
5. <span data-ttu-id="305c1-139">Clique em **guardar** regra de alerta de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="305c1-139">Click **Save** toosave hello alert rule.</span></span>
6. <span data-ttu-id="305c1-140">Aguarde algum tempo suficiente para um toobe alerta criado e, em seguida, procurar Slack uma mensagem que será semelhante toohello seguinte.</span><span class="sxs-lookup"><span data-stu-id="305c1-140">Wait sufficient time for an alert toobe created and then check Slack for a message which will be similar toohello following.</span></span>
   
   ![exemplo webhook no Slack](media/log-analytics-alerts-webhooks/oms-webhooks08.png)

### <a name="advanced-webhook-payload-for-slack"></a><span data-ttu-id="305c1-142">Avançadas payload de webhook para Slack</span><span class="sxs-lookup"><span data-stu-id="305c1-142">Advanced webhook payload for Slack</span></span>
<span data-ttu-id="305c1-143">Amplamente pode personalizar as mensagens de entrada com Slack.</span><span class="sxs-lookup"><span data-stu-id="305c1-143">You can extensively customize inbound messages with Slack.</span></span> <span data-ttu-id="305c1-144">Para obter mais informações, consulte [Webhooks entrada](https://api.slack.com/incoming-webhooks) no Web site do Olá Slack.</span><span class="sxs-lookup"><span data-stu-id="305c1-144">For more information, see [Incoming Webhooks](https://api.slack.com/incoming-webhooks) on hello Slack website.</span></span> <span data-ttu-id="305c1-145">Segue-se um toocreate de payload uma mensagem avançada com formatação mais complexa:</span><span class="sxs-lookup"><span data-stu-id="305c1-145">Following is a more complex payload toocreate a rich message with formatting:</span></span>

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


<span data-ttu-id="305c1-146">Isto irá gerar uma mensagem Slack seguir toohello semelhantes.</span><span class="sxs-lookup"><span data-stu-id="305c1-146">This would generate a message in Slack similar toohello following.</span></span>

![mensagem de exemplo na Slack](media/log-analytics-alerts-webhooks/oms-webhooks09.png)

## <a name="summary"></a><span data-ttu-id="305c1-148">Resumo</span><span class="sxs-lookup"><span data-stu-id="305c1-148">Summary</span></span>
<span data-ttu-id="305c1-149">Com esta regra de alerta no local, terá de uma mensagem enviada tooSlack sempre Olá critérios forem satisfeitos.</span><span class="sxs-lookup"><span data-stu-id="305c1-149">With this alert rule in place, you would have a message sent tooSlack every time hello criteria is met.</span></span>  

<span data-ttu-id="305c1-150">Este é apenas um exemplo de uma ação que pode criar no alerta de tooan de resposta.</span><span class="sxs-lookup"><span data-stu-id="305c1-150">This is only one example of an action that you can create in response tooan alert.</span></span>  <span data-ttu-id="305c1-151">Pode criar uma ação de webhook que chama outro serviço externo, um toostart de ação de runbook um runbook na automatização do Azure ou um toosend de ação de correio eletrónico um tooyourself de correio ou outros destinatários.</span><span class="sxs-lookup"><span data-stu-id="305c1-151">You could create a webhook action that calls another external service, a runbook action toostart a runbook in Azure Automation, or an email action toosend a mail tooyourself or other recipients.</span></span>   

## <a name="next-steps"></a><span data-ttu-id="305c1-152">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="305c1-152">Next Steps</span></span>
* <span data-ttu-id="305c1-153">Saiba mais sobre outros [ações na análise de registos de alerta](log-analytics-alerts-actions.md) incluindo outras ações.</span><span class="sxs-lookup"><span data-stu-id="305c1-153">Learn about other [alert actions in Log Analytics](log-analytics-alerts-actions.md) including other actions.</span></span>


