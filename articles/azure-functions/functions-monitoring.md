---
title: "aaaMonitoring das funções do Azure | Microsoft Docs"
description: "Saiba como toomonitor as suas funções do Azure."
services: functions
documentationcenter: na
author: wesmc7777
manager: erikre
editor: 
tags: 
keywords: "funções do azure, funções, processamento de eventos, webhooks, computação dinâmica, arquitetura sem servidor"
ms.assetid: 501722c3-f2f7-4224-a220-6d59da08a320
ms.service: functions
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: na
ms.date: 11/03/2016
ms.author: wesmc
ms.openlocfilehash: 254348d1cefce925654bd9532715b6def571e0ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitoring-azure-functions"></a><span data-ttu-id="882c1-104">Monitorizar as Funções do Azure</span><span class="sxs-lookup"><span data-stu-id="882c1-104">Monitoring Azure Functions</span></span>

## <a name="overview"></a><span data-ttu-id="882c1-105">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="882c1-105">Overview</span></span> 


<span data-ttu-id="882c1-106">Olá **Monitor** separador para cada função permite-lhe tooreview cada execução de uma função.</span><span class="sxs-lookup"><span data-stu-id="882c1-106">hello **Monitor** tab for each function allows you tooreview each execution of a function.</span></span>

![Separador de monitor de funções do Azure](./media/functions-monitoring/monitor-tab.png) 

<span data-ttu-id="882c1-108">Clicar uma execução permite-lhe tooreview Olá duração, dados de entrada, erros e ficheiros de registo associados.</span><span class="sxs-lookup"><span data-stu-id="882c1-108">Clicking an execution allows you tooreview hello duration, input data, errors, and associated log files.</span></span> <span data-ttu-id="882c1-109">Isto é útil de depuração e as suas funções de otimização do desempenho.</span><span class="sxs-lookup"><span data-stu-id="882c1-109">This is useful debugging and performance tuning your functions.</span></span>


> [!IMPORTANT]
> <span data-ttu-id="882c1-110">Quando utilizar Olá [consumo plano de alojamento](functions-overview.md#pricing) para as funções do Azure, Olá **monitorização** mosaico no painel de descrição geral de aplicação de função Olá não apresentará quaisquer dados.</span><span class="sxs-lookup"><span data-stu-id="882c1-110">When using hello [Consumption hosting plan](functions-overview.md#pricing) for Azure Functions, hello **Monitoring** tile in hello Function App overview blade will not show any data.</span></span> <span data-ttu-id="882c1-111">Isto acontece porque a plataforma de Olá dinamicamente dimensiona e gere instâncias de computação por si, pelo que estas métricas não são significativas um plano de consumo.</span><span class="sxs-lookup"><span data-stu-id="882c1-111">This is because hello platform dynamically scales and manages compute instances for you, so these metrics are not meaningful on a Consumption plan.</span></span> <span data-ttu-id="882c1-112">utilização de Olá toomonitor das suas aplicações de função, em vez disso, deve utilizar orientações Olá neste artigo.</span><span class="sxs-lookup"><span data-stu-id="882c1-112">toomonitor hello usage of your Function Apps, you should instead use hello guidance in this article.</span></span>
> 
> <span data-ttu-id="882c1-113">Olá seguinte captura de ecrã mostra um exemplo:</span><span class="sxs-lookup"><span data-stu-id="882c1-113">hello following screen-shot shows an example:</span></span>
> 
> ![No painel de recursos principais do Olá de monitorização](./media/functions-monitoring/app-service-overview-monitoring.png)



## <a name="real-time-monitoring"></a><span data-ttu-id="882c1-115">A monitorização em tempo real</span><span class="sxs-lookup"><span data-stu-id="882c1-115">Real-time monitoring</span></span>

<span data-ttu-id="882c1-116">A monitorização em tempo real está disponível clicando **fluxo de eventos em direto** conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="882c1-116">Real-time monitoring is available by clicking **live event stream** as shown below.</span></span> 

![Em direto a opção de fluxo de eventos para o separador de monitor de Olá](./media/functions-monitoring/monitor-tab-live-event-stream.png)

<span data-ttu-id="882c1-118">fluxo de eventos em direto de Olá irá ser graphed num novo separador do browser, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="882c1-118">hello live event stream will be graphed in a new browser tab as shown below.</span></span> 

![Exemplo de fluxo do evento em direto](./media/functions-monitoring/live-event-stream.png)


> [!NOTE]
> <span data-ttu-id="882c1-120">Não há um problema conhecido que pode fazer com que a sua toobe de toofail dados preenchido.</span><span class="sxs-lookup"><span data-stu-id="882c1-120">There is a known issue that may cause your data toofail toobe populated.</span></span> <span data-ttu-id="882c1-121">Se isto ocorrer, poderá ser necessário tooclose Olá browser separador contentora Olá evento em direto fluxo e, em seguida, clique em **fluxo de eventos em direto** novamente tooallow-tooproperly preencher os dados de fluxo de eventos.</span><span class="sxs-lookup"><span data-stu-id="882c1-121">If you experience this, you may need tooclose hello browser tab containing hello live event stream and then click **live event stream** again tooallow it tooproperly populate your event stream data.</span></span> 

<span data-ttu-id="882c1-122">fluxo de eventos em direto de Olá será graph Olá estatísticas para a sua função os seguintes:</span><span class="sxs-lookup"><span data-stu-id="882c1-122">hello live event stream will graph hello following statistics for your function:</span></span>

* <span data-ttu-id="882c1-123">Execuções iniciadas por segundo</span><span class="sxs-lookup"><span data-stu-id="882c1-123">Executions started per second</span></span>
* <span data-ttu-id="882c1-124">Execuções concluídas por segundo</span><span class="sxs-lookup"><span data-stu-id="882c1-124">Executions completed per second</span></span>
* <span data-ttu-id="882c1-125">Execuções falhadas por segundo</span><span class="sxs-lookup"><span data-stu-id="882c1-125">Executions failed per second</span></span>
* <span data-ttu-id="882c1-126">Tempo de execução média em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="882c1-126">Average execution time in milliseconds.</span></span>

<span data-ttu-id="882c1-127">Estas estatísticas são em tempo real, mas Olá real graphing de dados de execução de Olá pode ter cerca de 10 segundos de latência.</span><span class="sxs-lookup"><span data-stu-id="882c1-127">These statistics are real-time but hello actual graphing of hello execution data may have around 10 seconds of latency.</span></span>






## <a name="monitoring-log-files-from-a-command-line"></a><span data-ttu-id="882c1-128">Monitorização de ficheiros de registo de uma linha de comandos</span><span class="sxs-lookup"><span data-stu-id="882c1-128">Monitoring log files from a command line</span></span>


<span data-ttu-id="882c1-129">Pode transmitir ficheiros de registo tooa sessão de linha de comandos numa estação de trabalho local utilizando Olá Interface de linha de comandos do Azure (CLI) ou o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="882c1-129">You can stream log files tooa command line session on a local workstation using hello Azure Command Line Interface (CLI) or PowerShell.</span></span>

### <a name="monitoring-function-app-log-files-with-hello-azure-cli"></a><span data-ttu-id="882c1-130">Monitorização de ficheiros de registo de aplicação de função com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="882c1-130">Monitoring function app log files with hello Azure CLI</span></span>

<span data-ttu-id="882c1-131">tooget iniciado, [instalar Olá CLI do Azure](../cli-install-nodejs.md)</span><span class="sxs-lookup"><span data-stu-id="882c1-131">tooget started, [install hello Azure CLI](../cli-install-nodejs.md)</span></span>

<span data-ttu-id="882c1-132">Registo na sua conta do Azure utilizando Olá seguintes comandos, ou qualquer uma das Olá outras opções abrangidas, [tooAzure de Olá CLI do Azure de início de sessão](../xplat-cli-connect.md).</span><span class="sxs-lookup"><span data-stu-id="882c1-132">Log into your Azure account using hello following command, or any of hello other options covered in, [Log in tooAzure from hello Azure CLI](../xplat-cli-connect.md).</span></span>

    azure login

<span data-ttu-id="882c1-133">Modo de gestão de serviço de CLI do Azure (ASM) do tooenable de comando seguinte Olá de utilização:.</span><span class="sxs-lookup"><span data-stu-id="882c1-133">Use hello following command tooenable Azure CLI Service Management (ASM) mode:.</span></span>

    azure config mode asm

<span data-ttu-id="882c1-134">Se tiver várias subscrições, utilize Olá seguir toolist comandos suas subscrições e conjunto Olá atual subscrição toohello subscrição que contém a aplicação de função.</span><span class="sxs-lookup"><span data-stu-id="882c1-134">If you have multiple subscriptions, use hello following commands toolist your subscriptions and set hello current subscription toohello subscription that contains your function app.</span></span>

    azure account list
    azure account set <subscriptionNameOrId>

<span data-ttu-id="882c1-135">Olá comando seguinte irá transmitir ficheiros de registo de Olá da sua linha de comandos de toohello de aplicação de função:</span><span class="sxs-lookup"><span data-stu-id="882c1-135">hello following command will stream hello log files of your function app toohello command line:</span></span>

    azure site log tail -v <function app name>

### <a name="monitoring-function-app-log-files-with-powershell"></a><span data-ttu-id="882c1-136">Monitorização de ficheiros de registo de aplicação de função com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="882c1-136">Monitoring function app log files with PowerShell</span></span>

<span data-ttu-id="882c1-137">tooget iniciado, [instalar e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="882c1-137">tooget started, [install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

<span data-ttu-id="882c1-138">Adicione a sua conta do Azure executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="882c1-138">Add your Azure account by running hello following command:</span></span>

    PS C:\> Add-AzureAccount

<span data-ttu-id="882c1-139">Se tiver várias subscrições, pode listá-los por nome com Olá os seguintes comandos toosee se Olá correto de subscrição é Olá atualmente selecionado com base no `IsCurrent` propriedade:</span><span class="sxs-lookup"><span data-stu-id="882c1-139">If you have multiple subscriptions, you can list them by name with hello following command toosee if hello correct subscription is hello currently selected based on `IsCurrent` property:</span></span>

    PS C:\> Get-AzureSubscription

<span data-ttu-id="882c1-140">Se precisar de tooset Olá subscrição ativa toohello um que contém a aplicação de função, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="882c1-140">If you need tooset hello active subscription toohello one containing your function app, use hello following command:</span></span>

    PS C:\> Get-AzureSubscription -SubscriptionName "MyFunctionAppSubscription" | Select-AzureSubscription

<span data-ttu-id="882c1-141">Fluxo Olá registos tooyour sessão do PowerShell com Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="882c1-141">Stream hello logs tooyour PowerShell session with hello following command:</span></span>

    PS C:\> Get-AzureWebSiteLog -Name MyFunctionApp -Tail

<span data-ttu-id="882c1-142">Para obter mais informações consulte demasiado[como: transmitir os registos para aplicações web](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span><span class="sxs-lookup"><span data-stu-id="882c1-142">For more information refer too[How to: Stream logs for web apps](../app-service-web/web-sites-enable-diagnostic-log.md#streamlogs).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="882c1-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="882c1-143">Next steps</span></span>
<span data-ttu-id="882c1-144">Para obter mais informações, consulte Olá os seguintes recursos:</span><span class="sxs-lookup"><span data-stu-id="882c1-144">For more information, see hello following resources:</span></span>

* [<span data-ttu-id="882c1-145">Uma função de teste</span><span class="sxs-lookup"><span data-stu-id="882c1-145">Testing a function</span></span>](functions-test-a-function.md)
* [<span data-ttu-id="882c1-146">Uma função de escala</span><span class="sxs-lookup"><span data-stu-id="882c1-146">Scale a function</span></span>](functions-scale.md)

