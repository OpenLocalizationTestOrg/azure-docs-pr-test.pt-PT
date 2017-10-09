---
title: "alertas de aaaCreate para serviços do Azure - CLI de várias plataformas | Microsoft Docs"
description: "Acionar mensagens de correio eletrónico, notificações, os URLs de Web sites chamada (webhooks) ou automatização quando forem cumpridas condições Olá que especificar."
author: rboucher
manager: carmonm
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 5c6a2d27-7dcc-4f89-8752-9bb31b05ff35
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2016
ms.author: robb
ms.openlocfilehash: e53701e5377a415038a69fbd32f1e5fc5fe99be9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-metric-alerts-in-azure-monitor-for-azure-services---cross-platform-cli"></a><span data-ttu-id="f5f35-103">Criar métricas alertas no Monitor do Azure para serviços do Azure - CLI de várias plataformas</span><span class="sxs-lookup"><span data-stu-id="f5f35-103">Create metric alerts in Azure Monitor for Azure services - Cross-platform CLI</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="f5f35-104">Portal</span><span class="sxs-lookup"><span data-stu-id="f5f35-104">Portal</span></span>](insights-alerts-portal.md)
> * [<span data-ttu-id="f5f35-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5f35-105">PowerShell</span></span>](insights-alerts-powershell.md)
> * [<span data-ttu-id="f5f35-106">CLI</span><span class="sxs-lookup"><span data-stu-id="f5f35-106">CLI</span></span>](insights-alerts-command-line-interface.md)
>
>

## <a name="overview"></a><span data-ttu-id="f5f35-107">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="f5f35-107">Overview</span></span>
<span data-ttu-id="f5f35-108">Este artigo mostra como tooset configurar alertas de métricas do Azure utilizando Olá plataforma Interface de linha de comandos (CLI).</span><span class="sxs-lookup"><span data-stu-id="f5f35-108">This article shows you how tooset up Azure metric alerts using hello cross-platform Command Line Interface (CLI).</span></span>

> [!NOTE]
> <span data-ttu-id="f5f35-109">Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="f5f35-109">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="f5f35-110">No entanto, Olá espaços de nomes e, consequentemente, os comandos de Olá abaixo contém ainda insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="f5f35-110">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
>
>

<span data-ttu-id="f5f35-111">Pode receber um alerta com base na monitorização métricas para ou eventos nos seus serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f35-111">You can receive an alert based on monitoring metrics for, or events on, your Azure services.</span></span>

* <span data-ttu-id="f5f35-112">**Valores métricos** - hello acionadores de alertas quando o valor de Olá de uma métrica especificada atravesse um limiar atribuir em qualquer direção.</span><span class="sxs-lookup"><span data-stu-id="f5f35-112">**Metric values** - hello alert triggers when hello value of a specified metric crosses a threshold you assign in either direction.</span></span> <span data-ttu-id="f5f35-113">Ou seja, aciona ambas quando Olá primeiro condição e, em seguida, posteriormente quando condição que é já não está a ser cumprido.</span><span class="sxs-lookup"><span data-stu-id="f5f35-113">That is, it triggers both when hello condition is first met and then afterwards when that condition is no longer being met.</span></span>    
* <span data-ttu-id="f5f35-114">**Eventos de registo de atividade** -pode acionar um alerta num *cada* eventos ou apenas quando ocorre um determinados eventos.</span><span class="sxs-lookup"><span data-stu-id="f5f35-114">**Activity log events** - An alert can trigger on *every* event, or, only when a certain events occurs.</span></span> <span data-ttu-id="f5f35-115">mais informações sobre alertas de registo de atividade toolearn [clique aqui](monitoring-activity-log-alerts.md)</span><span class="sxs-lookup"><span data-stu-id="f5f35-115">toolearn more about activity log alerts [click here](monitoring-activity-log-alerts.md)</span></span>

<span data-ttu-id="f5f35-116">Pode configurar uma métrica toodo alerta Olá a seguir quando aciona:</span><span class="sxs-lookup"><span data-stu-id="f5f35-116">You can configure a metric alert toodo hello following when it triggers:</span></span>

* <span data-ttu-id="f5f35-117">enviar o administrador de serviços de toohello de notificações de e-mail e coadministradores</span><span class="sxs-lookup"><span data-stu-id="f5f35-117">send email notifications toohello service administrator and co-administrators</span></span>
* <span data-ttu-id="f5f35-118">envie correio eletrónico tooadditional e-mails que especificar.</span><span class="sxs-lookup"><span data-stu-id="f5f35-118">send email tooadditional emails that you specify.</span></span>
* <span data-ttu-id="f5f35-119">Chamar um webhook</span><span class="sxs-lookup"><span data-stu-id="f5f35-119">call a webhook</span></span>
* <span data-ttu-id="f5f35-120">iniciar a execução de um runbook do Azure (apenas a partir do portal do Azure neste momento Olá)</span><span class="sxs-lookup"><span data-stu-id="f5f35-120">start execution of an Azure runbook (only from hello Azure portal at this time)</span></span>

<span data-ttu-id="f5f35-121">Pode configurar e obter informações sobre regras de alerta métricas utilizando</span><span class="sxs-lookup"><span data-stu-id="f5f35-121">You can configure and get information about metric alert rules using</span></span>

* [<span data-ttu-id="f5f35-122">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="f5f35-122">Azure portal</span></span>](insights-alerts-portal.md)
* [<span data-ttu-id="f5f35-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f5f35-123">PowerShell</span></span>](insights-alerts-powershell.md)
* [<span data-ttu-id="f5f35-124">interface de linha de comandos (CLI)</span><span class="sxs-lookup"><span data-stu-id="f5f35-124">command-line interface (CLI)</span></span>](insights-alerts-command-line-interface.md)
* [<span data-ttu-id="f5f35-125">API de REST de Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="f5f35-125">Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931945.aspx)

<span data-ttu-id="f5f35-126">Pode receber sempre a ajuda para comandos escrevendo um comando e colocando - ajudar no fim de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5f35-126">You can always receive help for commands by typing a command and putting -help at hello end.</span></span> <span data-ttu-id="f5f35-127">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="f5f35-127">For example:</span></span>

    ```console
    azure insights alerts -help
    azure insights alerts actions email create -help
    ```

## <a name="create-alert-rules-using-hello-cli"></a><span data-ttu-id="f5f35-128">Criar regras de alertas utilizando Olá CLI</span><span class="sxs-lookup"><span data-stu-id="f5f35-128">Create alert rules using hello CLI</span></span>
1. <span data-ttu-id="f5f35-129">Efetue Olá pré-requisitos e tooAzure de início de sessão.</span><span class="sxs-lookup"><span data-stu-id="f5f35-129">Perform hello Prerequisites and login tooAzure.</span></span> <span data-ttu-id="f5f35-130">Consulte [amostras da CLI do Azure Monitor](insights-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="f5f35-130">See [Azure Monitor CLI samples](insights-cli-samples.md).</span></span> <span data-ttu-id="f5f35-131">Em suma, instale Olá CLI e executar estes comandos.</span><span class="sxs-lookup"><span data-stu-id="f5f35-131">In short, install hello CLI and run these commands.</span></span> <span data-ttu-id="f5f35-132">Podem ajudá-lo a sessão iniciada, mostram que subscrição que está a utilizar e prepará-lo toorun comandos de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f35-132">They get you logged in, show what subscription you are using, and prepare you toorun Azure Monitor commands.</span></span>

    ```console
    azure login
    azure account show
    azure config mode arm

    ```

2. <span data-ttu-id="f5f35-133">as regras existentes toolist num grupo de recursos, utilize Olá seguir formulário **informações do azure a lista de regras de alertas** *[opções] &lt;resourceGroup&gt;*</span><span class="sxs-lookup"><span data-stu-id="f5f35-133">toolist existing rules on a resource group, use hello following form **azure insights alerts rule list** *[options] &lt;resourceGroup&gt;*</span></span>

   ```console
   azure insights alerts rule list myresourcegroupname

   ```
3. <span data-ttu-id="f5f35-134">toocreate uma regra, terá de toohave várias partes importantes de informações pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="f5f35-134">toocreate a rule, you need toohave several important pieces of information first.</span></span>
  * <span data-ttu-id="f5f35-135">Olá **ID de recurso** para o recurso de Olá pretende tooset um alerta para</span><span class="sxs-lookup"><span data-stu-id="f5f35-135">hello **Resource ID** for hello resource you want tooset an alert for</span></span>
  * <span data-ttu-id="f5f35-136">Olá **as definições de métrica** disponíveis para esse recurso</span><span class="sxs-lookup"><span data-stu-id="f5f35-136">hello **metric definitions** available for that resource</span></span>

     <span data-ttu-id="f5f35-137">Olá tooget unidirecional ID de recurso é toouse Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f5f35-137">One way tooget hello Resource ID is toouse hello Azure portal.</span></span> <span data-ttu-id="f5f35-138">Pressupondo que já foi criado o recurso de Olá, selecione-o no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="f5f35-138">Assuming hello resource is already created, select it in hello portal.</span></span> <span data-ttu-id="f5f35-139">Em seguida, no painel seguinte da Olá, selecione *propriedades* em Olá *definições* secção.</span><span class="sxs-lookup"><span data-stu-id="f5f35-139">Then in hello next blade, select *Properties* under hello *Settings* section.</span></span> <span data-ttu-id="f5f35-140">Olá *ID de recurso* é um campo no painel seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="f5f35-140">hello *RESOURCE ID* is a field in hello next blade.</span></span> <span data-ttu-id="f5f35-141">Outra forma é toouse Olá [Explorador de recursos do Azure](https://resources.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="f5f35-141">Another way is toouse hello [Azure Resource Explorer](https://resources.azure.com/).</span></span>

     <span data-ttu-id="f5f35-142">É um id de recurso de exemplo para uma aplicação web</span><span class="sxs-lookup"><span data-stu-id="f5f35-142">An example resource id for a web app is</span></span>

     ```console
     /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename
     ```

     <span data-ttu-id="f5f35-143">uma lista de unidades para as métricas de exemplo de recursos anterior Olá, Olá utilize os seguintes comandos da CLI e as métricas disponíveis de Olá tooget:</span><span class="sxs-lookup"><span data-stu-id="f5f35-143">tooget a list of hello available metrics and units for those metrics for hello previous resource example, use hello following CLI command:</span></span>  

     ```console
     azure insights metrics list /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename PT1M
     ```

     <span data-ttu-id="f5f35-144">*PT1M* é granularidade Olá de medição de Olá disponíveis (intervalos de 1 minuto).</span><span class="sxs-lookup"><span data-stu-id="f5f35-144">*PT1M* is hello granularity of hello available measurement (1-minute intervals).</span></span> <span data-ttu-id="f5f35-145">Utilizar diferentes granularidades dá-lhe opções de métricas diferentes.</span><span class="sxs-lookup"><span data-stu-id="f5f35-145">Using different granularities gives you different metric options.</span></span>
4. <span data-ttu-id="f5f35-146">toocreate uma métrica com base na regra de alerta, utilize um comando de Olá seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="f5f35-146">toocreate a metric-based alert rule, use a command of hello following form:</span></span>

    <span data-ttu-id="f5f35-147">**as informações do Azure métrico conjunto de regras de alertas** *[opções] &lt;ruleName&gt; &lt;localização&gt; &lt;resourceGroup&gt; &lt;windowSize &gt; &lt;operador&gt; &lt;limiar&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt; timeAggregationOperator&gt;*</span><span class="sxs-lookup"><span data-stu-id="f5f35-147">**azure insights alerts rule metric set** *[options] &lt;ruleName&gt; &lt;location&gt; &lt;resourceGroup&gt; &lt;windowSize&gt; &lt;operator&gt; &lt;threshold&gt; &lt;targetResourceId&gt; &lt;metricName&gt; &lt;timeAggregationOperator&gt;*</span></span>

    <span data-ttu-id="f5f35-148">Olá os seguintes conjuntos de exemplo, um alerta no recurso web site.</span><span class="sxs-lookup"><span data-stu-id="f5f35-148">hello following example sets up an alert on a web site resource.</span></span> <span data-ttu-id="f5f35-149">Olá alerta acionadores sempre que recebe consistentemente qualquer tráfego de 5 minutos e novamente quando não recebe nenhum tráfego de 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="f5f35-149">hello alert triggers whenever it consistently receives any traffic for 5 minutes and again when it receives no traffic for 5 minutes.</span></span>

    ```console
    azure insights alerts rule metric set myrule eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total

    ```
5. <span data-ttu-id="f5f35-150">toocreate webhook ou enviar correio eletrónico quando um métrico alerta é acionado, primeiro crie e-mail Olá e/ou webhooks.</span><span class="sxs-lookup"><span data-stu-id="f5f35-150">toocreate webhook or send email when a metric alert fires, first create hello email and/or webhooks.</span></span> <span data-ttu-id="f5f35-151">Em seguida, criar regra de Olá imediatamente posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f5f35-151">Then create hello rule immediately afterwards.</span></span> <span data-ttu-id="f5f35-152">Não é possível associar webhook ou e-mails com já criou regras utilizando Olá CLI.</span><span class="sxs-lookup"><span data-stu-id="f5f35-152">You cannot associate webhook or emails with already created rules using hello CLI.</span></span>

    ```console
    azure insights alerts actions email create --customEmails myemail@contoso.com

    azure insights alerts actions webhook create https://www.contoso.com

    azure insights alerts rule metric set myrulewithwebhookandemail eastus myreasourcegroup PT5M GreaterThan 2 /subscriptions/dededede-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/myresourcegroupname/providers/Microsoft.Web/sites/mywebsitename BytesReceived Total
    ```

6. <span data-ttu-id="f5f35-153">Pode verificar que os alertas não foi criados corretamente ao observar uma regra de individuais.</span><span class="sxs-lookup"><span data-stu-id="f5f35-153">You can verify that your alerts have been created properly by looking at an individual rule.</span></span>

    ```console
    azure insights alerts rule list myresourcegroup --ruleName myrule
    ```
7. <span data-ttu-id="f5f35-154">regras de toodelete, utilize um comando de formulário Olá:</span><span class="sxs-lookup"><span data-stu-id="f5f35-154">toodelete rules, use a command of hello form:</span></span>

    <span data-ttu-id="f5f35-155">**informações de eliminação de regras de alertas** [opções] &lt;resourceGroup&gt; &lt;ruleName&gt;</span><span class="sxs-lookup"><span data-stu-id="f5f35-155">**insights alerts rule delete** [options] &lt;resourceGroup&gt; &lt;ruleName&gt;</span></span>

    <span data-ttu-id="f5f35-156">Estes comandos, elimine as regras de Olá que criou anteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="f5f35-156">These commands delete hello rules previously created in this article.</span></span>

    ```console
    azure insights alerts rule delete myresourcegroup myrule
    azure insights alerts rule delete myresourcegroup myrulewithwebhookandemail
    azure insights alerts rule delete myresourcegroup myActivityLogRule
    ```

## <a name="next-steps"></a><span data-ttu-id="f5f35-157">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f5f35-157">Next steps</span></span>
* <span data-ttu-id="f5f35-158">[Obter uma descrição geral da monitorização do Azure](monitoring-overview.md) , incluindo os tipos de Olá de informações que pode recolher e monitorizar.</span><span class="sxs-lookup"><span data-stu-id="f5f35-158">[Get an overview of Azure monitoring](monitoring-overview.md) including hello types of information you can collect and monitor.</span></span>
* <span data-ttu-id="f5f35-159">Saiba mais sobre [configurar webhooks alertas](insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f5f35-159">Learn more about [configuring webhooks in alerts](insights-webhooks-alerts.md).</span></span>
* <span data-ttu-id="f5f35-160">Saiba mais sobre [configurar alertas de eventos de registo de atividade](monitoring-activity-log-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="f5f35-160">Learn more about [configuring alerts on Activity log events](monitoring-activity-log-alerts.md).</span></span>
* <span data-ttu-id="f5f35-161">Saiba mais sobre [Runbooks de automatização do Azure](../automation/automation-starting-a-runbook.md).</span><span class="sxs-lookup"><span data-stu-id="f5f35-161">Learn more about [Azure Automation Runbooks](../automation/automation-starting-a-runbook.md).</span></span>
* <span data-ttu-id="f5f35-162">Obter um [descrição geral de recolha de registos de diagnóstico](monitoring-overview-of-diagnostic-logs.md) toocollect detalhadas métricas de alta frequência do seu serviço.</span><span class="sxs-lookup"><span data-stu-id="f5f35-162">Get an [overview of collecting diagnostic logs](monitoring-overview-of-diagnostic-logs.md) toocollect detailed high-frequency metrics on your service.</span></span>
* <span data-ttu-id="f5f35-163">Obter um [descrição geral da coleção de métricas](insights-how-to-customize-monitoring.md) toomake se o serviço está disponível e reativa.</span><span class="sxs-lookup"><span data-stu-id="f5f35-163">Get an [overview of metrics collection](insights-how-to-customize-monitoring.md) toomake sure your service is available and responsive.</span></span>
