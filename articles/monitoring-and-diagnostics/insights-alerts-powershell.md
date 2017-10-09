---
title: "alertas de aaaCreate para serviços do Azure - PowerShell | Microsoft Docs"
description: "Acionar mensagens de correio eletrónico, notificações, os URLs de Web sites chamada (webhooks) ou automatização quando forem cumpridas condições Olá que especificar."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: d26ab15b-7b7e-42a9-81c8-3ce9ead5d252
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/20/2016
ms.author: robb
ms.openlocfilehash: 80d3a3f194fc6a5a09a81d04206ea7a1640bddb0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---powershell"></a><span data-ttu-id="01322-103">Criar métricas alertas no Monitor do Azure para serviços do Azure - PowerShell</span><span class="sxs-lookup"><span data-stu-id="01322-103">Create metric alerts in Azure Monitor for Azure services - PowerShell</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="01322-104">Portal</span><span class="sxs-lookup"><span data-stu-id="01322-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="01322-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01322-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="01322-106">CLI</span><span class="sxs-lookup"><span data-stu-id="01322-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="01322-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="01322-107">Overview</span></span>
<span data-ttu-id="01322-108">Este artigo mostra como tooset cópias de segurança do Azure métrica alertas utilizando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01322-108">This article shows you how tooset up Azure metric alerts using PowerShell.</span></span>  

<span data-ttu-id="01322-109">Pode receber um alerta com base na monitorização métricas para ou eventos nos seus serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="01322-109">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="01322-110">**Valores métricos** - hello acionadores de alertas quando o valor de Olá de uma métrica especificada atravesse um limiar atribuir em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="01322-110">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="01322-111">Ou seja, aciona ambas quando Olá primeiro condição e, em seguida, posteriormente quando condição que é já não está a ser cumprido.</span><span class="sxs-lookup"><span data-stu-id="01322-111">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="01322-112">**Eventos de registo de atividade** -pode acionar um alerta num *cada* eventos ou apenas quando ocorre um determinados eventos.</span><span class="sxs-lookup"><span data-stu-id="01322-112">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="01322-113">mais informações sobre alertas de registo de atividade toolearn [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="01322-113">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="01322-114">Pode configurar uma métrica toodo alerta Olá a seguir quando aciona:</span><span class="sxs-lookup"><span data-stu-id="01322-114">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="01322-115">enviar o administrador de serviços de toohello de notificações de e-mail e coadministradores</span><span class="sxs-lookup"><span data-stu-id="01322-115">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="01322-116">envie correio eletrónico tooadditional e-mails que especificar.</span><span class="sxs-lookup"><span data-stu-id="01322-116">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="01322-117">Chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="01322-117">call a webhook</span></span>
* <span data-ttu-id="01322-118">iniciar a execução de um runbook do Azure (apenas a partir do portal do Azure Olá)</span><span class="sxs-lookup"><span data-stu-id="01322-118">start execution of an Azure runbook (only from hello Azure portal)</span></span>

<span data-ttu-id="01322-119">Pode configurar e obter informações sobre regras de alerta utilizando</span><span class="sxs-lookup"><span data-stu-id="01322-119">You can configure and get information about alert rules using</span></span>

* [<span data-ttu-id="01322-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="01322-120">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="01322-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="01322-121">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="01322-122">interface de linha de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="01322-122">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="01322-123">API de REST de Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="01322-123">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="01322-124">Para obter informações adicionais, pode sempre escrever ```Get-Help``` e, em seguida, Olá pretende obter ajuda no comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01322-124">For additional information, you can always type ```Get-Help``` and then hello PowerShell command you want help on.</span></span>

## <a name="create-alert-rules-in-powershell"></a><span data-ttu-id="01322-125">Criar regras de alertas no PowerShell</span><span class="sxs-lookup"><span data-stu-id="01322-125">Create alert rules in PowerShell</span></span>
1. <span data-ttu-id="01322-126">Inicie sessão no tooAzure.</span><span class="sxs-lookup"><span data-stu-id="01322-126">Log in tooAzure.</span></span>   

    ```PowerShell
    Login-AzureRmAccount

    ```
2. <span data-ttu-id="01322-127">Obter uma lista de subscrições Olá que tem disponíveis.</span><span class="sxs-lookup"><span data-stu-id="01322-127">Get a list of hello subscriptions you have available.</span></span> <span data-ttu-id="01322-128">Certifique-se de que estão a funcionar com a subscrição correta Olá.</span><span class="sxs-lookup"><span data-stu-id="01322-128">Verify that you are working with hello right subscription.</span></span> <span data-ttu-id="01322-129">Se não estiver, defina-o direito de toohello um utilizando um resultado de Olá `Get-AzureRmSubscription`.</span><span class="sxs-lookup"><span data-stu-id="01322-129">If not, set it toohello right one using hello output from `Get-AzureRmSubscription`.</span></span>

    ```PowerShell
    Get-AzureRmSubscription
    Get-AzureRmContext
    Set-AzureRmContext -SubscriptionId <subscriptionid>
    ```
3. <span data-ttu-id="01322-130">as regras existentes toolist num grupo de recursos, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="01322-130">toolist existing rules on a resource group, use hello following command:</span></span>

   ```PowerShell
   Get-AzureRmAlertRule -ResourceGroup <myresourcegroup> -DetailedOutput
   ```
4. <span data-ttu-id="01322-131">toocreate uma regra, terá de toohave várias partes importantes de informações pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="01322-131">toocreate a rule, you need toohave several important pieces of information first.</span></span>

  * <span data-ttu-id="01322-132">Olá **ID de recurso** para o recurso de Olá pretende tooset um alerta para</span><span class="sxs-lookup"><span data-stu-id="01322-132">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="01322-133">Olá **as definições de métrica** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="01322-133">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="01322-134">Olá tooget unidirecional ID de recurso é toouse Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="01322-134">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="01322-135">Pressupondo que já foi criado o recurso de Olá, selecione-o no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="01322-135">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="01322-136">Em seguida, no painel seguinte da Olá, selecione *propriedades* em Olá *definições* secção.</span><span class="sxs-lookup"><span data-stu-id="01322-136">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="01322-137">**ID de recurso** é um campo no painel seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="01322-137">**RESOURCE ID** is a field in hello next blade.</span></span> <span data-ttu-id="01322-138">Outra forma é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="01322-138">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="01322-139">É um ID de recurso de exemplo para uma aplicação web</span><span class="sxs-lookup"><span data-stu-id="01322-139">An example Resource ID for a web app is</span></span>

     ```
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="01322-140">Pode utilizar `Get-AzureRmMetricDefinition` lista de Olá tooview de todas as definições de métricas para um recurso específico.</span><span class="sxs-lookup"><span data-stu-id="01322-140">You can use `Get-AzureRmMetricDefinition` tooview hello list of all metric definitions for a specific resource.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id>
     ```

     <span data-ttu-id="01322-141">Olá exemplo seguinte gera uma tabela com o nome de métrica de Olá e Olá unidade para esse métrica.</span><span class="sxs-lookup"><span data-stu-id="01322-141">hello following example generates a table with hello metric Name and hello Unit for that metric.</span></span>

     ```PowerShell
     Get-AzureRmMetricDefinition -ResourceId <resource_id> | Format-Table -Property Name,Unit

     ```
     <span data-ttu-id="01322-142">Está disponível uma lista completa das opções disponíveis para o Get-AzureRmMetricDefinition executando Get-MetricDefinitions.</span><span class="sxs-lookup"><span data-stu-id="01322-142">A full list of available options for Get-AzureRmMetricDefinition is available by running Get-MetricDefinitions.</span></span>
5. <span data-ttu-id="01322-143">Olá os seguintes conjuntos de exemplo, um alerta no recurso web site.</span><span class="sxs-lookup"><span data-stu-id="01322-143">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="01322-144">Olá alerta acionadores sempre que recebe consistentemente qualquer tráfego de 5 minutos e novamente quando não recebe nenhum tráfego de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="01322-144">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```PowerShell
    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Description "alert on any website activity"

    ```
6. <span data-ttu-id="01322-145">toocreate webhook ou enviar correio eletrónico quando um alerta é acionado, primeiro crie e-mail Olá e/ou webhooks.</span><span class="sxs-lookup"><span data-stu-id="01322-145">toocreate webhook or send email when an alert triggers, first create hello email and/or webhooks.</span></span> <span data-ttu-id="01322-146">Em seguida, criar de imediato regra Olá posteriormente com Olá - tag de ações e conforme mostrado no seguinte exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="01322-146">Then immediately create hello rule afterwards with hello -Actions tag and as shown in hello following example.</span></span> <span data-ttu-id="01322-147">Não é possível associar webhook ou e-mails com já criou regras através do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="01322-147">You cannot associate webhook or emails with already created rules via PowerShell.</span></span>

    ```PowerShell
    $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail myname@company.com
    $actionWebhook = New-AzureRmAlertRuleWebhook -ServiceUri https://www.contoso.com?token=mytoken

    Add-AzureRmMetricAlertRule -Name myMetricRuleWithWebhookAndEmail -Location "East US" -ResourceGroup myresourcegroup -TargetResourceId /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename -MetricName "BytesReceived" -Operator GreaterThan -Threshold 2 -WindowSize 00:05:00 -TimeAggregationOperator Total -Actions $actionEmail, $actionWebhook -Description "alert on any website activity"
    ```

7. <span data-ttu-id="01322-148">tooverify que os alertas não foi criados corretamente ao observar a regras individuais Olá.</span><span class="sxs-lookup"><span data-stu-id="01322-148">tooverify that your alerts have been created properly by looking at hello individual rules.</span></span>

    ```PowerShell
    Get-AzureRmAlertRule -Name myMetricRuleWithWebhookAndEmail -ResourceGroup myresourcegroup -DetailedOutput

    Get-AzureRmAlertRule -Name myLogAlertRule -ResourceGroup myresourcegroup -DetailedOutput
    ```
8. <span data-ttu-id="01322-149">Elimine os alertas.</span><span class="sxs-lookup"><span data-stu-id="01322-149">Delete your alerts.</span></span> <span data-ttu-id="01322-150">Estes comandos, elimine as regras de Olá criadas anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="01322-150">These commands delete hello rules created previously in this article.</span></span>

    ```PowerShell
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myrule
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myMetricRuleWithWebhookAndEmail
    Remove-AzureRmAlertRule -ResourceGroup myresourcegroup -Name myLogAlertRule
    ```

## <a name="next-steps"></a><span data-ttu-id="01322-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="01322-151">Next steps</span></span>
* <span data-ttu-id="01322-152">[Obter uma descrição geral da monitorização do Azure](monitoring-overview.md) , incluindo os tipos de Olá de informações que pode recolher e monitorizar.</span><span class="sxs-lookup"><span data-stu-id="01322-152">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="01322-153">Saiba mais sobre [configurar webhooks alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="01322-153">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="01322-154">Saiba mais sobre [configurar alertas de eventos de registo de atividade](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="01322-154">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="01322-155">Saiba mais sobre [Runbooks de automatização do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="01322-155">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="01322-156">Obter um [descrição geral de recolha de registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="01322-156">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="01322-157">Obter um [descrição geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake se o serviço está disponível e reativa.</span><span class="sxs-lookup"><span data-stu-id="01322-157">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
