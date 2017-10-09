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
# <a name="create-and-manage-alert-rules-in-log-analytics-with-rest-api"></a><span data-ttu-id="85659-104">Criar e gerir regras de alertas na análise de registos com a REST API</span><span class="sxs-lookup"><span data-stu-id="85659-104">Create and manage alert rules in Log Analytics with REST API</span></span>
<span data-ttu-id="85659-105">Olá a API de REST de alerta de análise do registo permite-lhe toocreate e gerir alertas no Operations Management Suite (OMS).</span><span class="sxs-lookup"><span data-stu-id="85659-105">hello Log Analytics Alert REST API allows you toocreate and manage alerts in Operations Management Suite (OMS).</span></span>  <span data-ttu-id="85659-106">Este artigo fornece detalhes de Olá API e vários exemplos para efetuar operações diferentes.</span><span class="sxs-lookup"><span data-stu-id="85659-106">This article provides details of hello API and several examples for performing different operations.</span></span>

<span data-ttu-id="85659-107">Olá API de REST de pesquisa de análise de registo é RESTful e pode ser acedido através de Olá API de REST do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85659-107">hello Log Analytics Search REST API is RESTful and can be accessed via hello Azure Resource Manager REST API.</span></span> <span data-ttu-id="85659-108">Este documento irá encontrar exemplos onde Olá API é acedido a partir de uma linha de comandos do PowerShell utilizando [ARMClient](https://github.com/projectkudu/ARMClient), uma ferramenta de linha de comandos de código aberto que simplifica a invocar Olá API do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="85659-108">In this document you will find examples where hello API is accessed from a PowerShell command line using  [ARMClient](https://github.com/projectkudu/ARMClient), an open source command line tool that simplifies invoking hello Azure Resource Manager API.</span></span> <span data-ttu-id="85659-109">utilização Olá ARMClient e do PowerShell é uma das muitas opções de Olá de tooaccess API de pesquisa de análise do registo.</span><span class="sxs-lookup"><span data-stu-id="85659-109">hello use of ARMClient and PowerShell is one of many options tooaccess hello Log Analytics Search API.</span></span> <span data-ttu-id="85659-110">Com estas ferramentas que pode utilizar Olá RESTful API do Azure Resource Manager toomake chamadas tooOMS áreas de trabalho e executar comandos de pesquisa dentro delas.</span><span class="sxs-lookup"><span data-stu-id="85659-110">With these tools you can utilize hello RESTful Azure Resource Manager API toomake calls tooOMS workspaces and perform search commands within them.</span></span> <span data-ttu-id="85659-111">Olá API será saída tooyou de resultados de pesquisa no formato JSON, permitindo-lhe os resultados da pesquisa Olá toouse de várias maneiras diferentes através de programação.</span><span class="sxs-lookup"><span data-stu-id="85659-111">hello API will output search results tooyou in JSON format, allowing you toouse hello search results in many different ways programmatically.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="85659-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="85659-112">Prerequisites</span></span>
<span data-ttu-id="85659-113">Atualmente, os alertas só podem ser criados com uma procura guardada na análise de registos.</span><span class="sxs-lookup"><span data-stu-id="85659-113">Currently, alerts can only be created with a saved search in Log Analytics.</span></span>  <span data-ttu-id="85659-114">Pode consultar toohello [API de REST do registo de pesquisa](log-analytics-log-search-api.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="85659-114">You can refer toohello [Log Search REST API](log-analytics-log-search-api.md) for more information.</span></span>

## <a name="schedules"></a><span data-ttu-id="85659-115">Agendas</span><span class="sxs-lookup"><span data-stu-id="85659-115">Schedules</span></span>
<span data-ttu-id="85659-116">Uma pesquisa guardada pode ter uma ou mais agendas.</span><span class="sxs-lookup"><span data-stu-id="85659-116">A saved search can have one or more schedules.</span></span> <span data-ttu-id="85659-117">Olá agenda define frequência hello pesquisa é executada e intervalo de tempo de Olá através de critérios que Olá é identificado.</span><span class="sxs-lookup"><span data-stu-id="85659-117">hello schedule defines how often hello search is run and hello time interval over which hello criteria is identified.</span></span>
<span data-ttu-id="85659-118">As agendas tem propriedades de Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-118">Schedules have hello properties in hello following table.</span></span>

| <span data-ttu-id="85659-119">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-119">Property</span></span> | <span data-ttu-id="85659-120">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-120">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-121">intervalo</span><span class="sxs-lookup"><span data-stu-id="85659-121">Interval</span></span> |<span data-ttu-id="85659-122">Frequência hello pesquisa é executada.</span><span class="sxs-lookup"><span data-stu-id="85659-122">How often hello search is run.</span></span> <span data-ttu-id="85659-123">Medido em minutos.</span><span class="sxs-lookup"><span data-stu-id="85659-123">Measured in minutes.</span></span> |
| <span data-ttu-id="85659-124">QueryTimeSpan</span><span class="sxs-lookup"><span data-stu-id="85659-124">QueryTimeSpan</span></span> |<span data-ttu-id="85659-125">intervalo de tempo de Olá através do qual Olá critérios é avaliada.</span><span class="sxs-lookup"><span data-stu-id="85659-125">hello time interval over which hello criteria is evaluated.</span></span> <span data-ttu-id="85659-126">Tem de ser igual tooor superior ao intervalo.</span><span class="sxs-lookup"><span data-stu-id="85659-126">Must be equal tooor greater than Interval.</span></span> <span data-ttu-id="85659-127">Medido em minutos.</span><span class="sxs-lookup"><span data-stu-id="85659-127">Measured in minutes.</span></span> |
| <span data-ttu-id="85659-128">Versão</span><span class="sxs-lookup"><span data-stu-id="85659-128">Version</span></span> |<span data-ttu-id="85659-129">Olá versão de API que está a ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="85659-129">hello API version being used.</span></span>  <span data-ttu-id="85659-130">Atualmente, este deve ser sempre definida too1.</span><span class="sxs-lookup"><span data-stu-id="85659-130">Currently, this should always be set too1.</span></span> |

<span data-ttu-id="85659-131">Por exemplo, considere uma consulta de eventos com um intervalo de 15 minutos e um Timespan de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="85659-131">For example, consider an event query with an Interval of 15 minutes and a Timespan of 30 minutes.</span></span> <span data-ttu-id="85659-132">Neste caso, consulta Olá iria ser executada a cada 15 minutos e seria possível acionar um alerta se os critérios de Olá continuaram tooresolve tootrue através de um intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="85659-132">In this case, hello query would be run every 15 minutes, and an alert would be triggered if hello criteria continued tooresolve tootrue over a 30 minute span.</span></span>

### <a name="retrieving-schedules"></a><span data-ttu-id="85659-133">A obter agendas</span><span class="sxs-lookup"><span data-stu-id="85659-133">Retrieving schedules</span></span>
<span data-ttu-id="85659-134">Olá utilize obter método tooretrieve todas as agendas de uma procura guardada.</span><span class="sxs-lookup"><span data-stu-id="85659-134">Use hello Get method tooretrieve all schedules for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules?api-version=2015-03-20

<span data-ttu-id="85659-135">Olá utilize obter método com um tooretrieve de ID de agenda uma determinada agenda para uma pesquisa guardada.</span><span class="sxs-lookup"><span data-stu-id="85659-135">Use hello Get method with a schedule ID tooretrieve a particular schedule for a saved search.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20

<span data-ttu-id="85659-136">Segue-se uma resposta de amostra de uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-136">Following is a sample response for a schedule.</span></span>

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

### <a name="creating-a-schedule"></a><span data-ttu-id="85659-137">Criar uma agenda</span><span class="sxs-lookup"><span data-stu-id="85659-137">Creating a schedule</span></span>
<span data-ttu-id="85659-138">Utilize o método de Put Olá com um toocreate de ID exclusivo agenda uma nova agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-138">Use hello Put method with a unique schedule ID toocreate a new schedule.</span></span>  <span data-ttu-id="85659-139">Tenha em atenção que as duas agendas não é possível ter Olá mesmo ID mesmo que se encontrem associados com diferentes das procuras guardadas.</span><span class="sxs-lookup"><span data-stu-id="85659-139">Note that two schedules cannot have hello same ID even if they are associated with different saved searches.</span></span>  <span data-ttu-id="85659-140">Quando criar uma agenda na consola do OMS Olá, um GUID é criado para o ID de agenda Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-140">When you create a schedule in hello OMS console, a GUID is created for hello schedule ID.</span></span>

> [!NOTE]
> <span data-ttu-id="85659-141">nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="85659-141">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

    $scheduleJson = "{'properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson

### <a name="editing-a-schedule"></a><span data-ttu-id="85659-142">Editar uma agenda</span><span class="sxs-lookup"><span data-stu-id="85659-142">Editing a schedule</span></span>
<span data-ttu-id="85659-143">Utilize o método de Put do Olá com uma agenda existente ID para Olá mesmo guardar pesquisa toomodify agendar.</span><span class="sxs-lookup"><span data-stu-id="85659-143">Use hello Put method with an existing schedule ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="85659-144">corpo de Olá de pedido de Olá tem de incluir Olá etag da agenda de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-144">hello body of hello request must include hello etag of hello schedule.</span></span>

      $scheduleJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A49.8074679Z'\""','properties': { 'Interval': 15, 'QueryTimeSpan':15, 'Active':'true' } }"
      armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/mynewschedule?api-version=2015-03-20 $scheduleJson


### <a name="deleting-schedules"></a><span data-ttu-id="85659-145">Agendas de eliminação</span><span class="sxs-lookup"><span data-stu-id="85659-145">Deleting schedules</span></span>
<span data-ttu-id="85659-146">Utilize o método de eliminação de Olá com um toodelete de ID de agenda uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-146">Use hello Delete method with a schedule ID toodelete a schedule.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}?api-version=2015-03-20


## <a name="actions"></a><span data-ttu-id="85659-147">Ações</span><span class="sxs-lookup"><span data-stu-id="85659-147">Actions</span></span>
<span data-ttu-id="85659-148">Uma agenda pode ter várias ações.</span><span class="sxs-lookup"><span data-stu-id="85659-148">A schedule can have multiple actions.</span></span> <span data-ttu-id="85659-149">Uma ação pode definir uma ou mais processos tooperform como enviar uma mensagem ou iniciar um runbook ou pode definir um limiar que determina quando resultados de Olá de uma procura correspondem alguns critérios.</span><span class="sxs-lookup"><span data-stu-id="85659-149">An action may define one or more processes tooperform such as sending a mail or starting a runbook, or it may define a threshold that determines when hello results of a search match some criteria.</span></span>  <span data-ttu-id="85659-150">Algumas ações vai definir ambos para que os processos de Olá são efetuados quando Olá limiar ser cumprido.</span><span class="sxs-lookup"><span data-stu-id="85659-150">Some actions will define both so that hello processes are performed when hello threshold is met.</span></span>

<span data-ttu-id="85659-151">Todas as ações tem propriedades de Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-151">All actions have hello properties in hello following table.</span></span>  <span data-ttu-id="85659-152">Diferentes tipos de alertas têm diferentes propriedades adicionais que são descritas abaixo.</span><span class="sxs-lookup"><span data-stu-id="85659-152">Different types of alerts have different additional properties which are described below.</span></span>

| <span data-ttu-id="85659-153">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-153">Property</span></span> | <span data-ttu-id="85659-154">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-154">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-155">Tipo</span><span class="sxs-lookup"><span data-stu-id="85659-155">Type</span></span> |<span data-ttu-id="85659-156">Tipo de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-156">Type of hello action.</span></span>  <span data-ttu-id="85659-157">Atualmente valores possíveis Olá são alerta e o Webhook.</span><span class="sxs-lookup"><span data-stu-id="85659-157">Currently hello possible values are Alert and Webhook.</span></span> |
| <span data-ttu-id="85659-158">Nome</span><span class="sxs-lookup"><span data-stu-id="85659-158">Name</span></span> |<span data-ttu-id="85659-159">Nome a apresentar para o alerta de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-159">Display name for hello alert.</span></span> |
| <span data-ttu-id="85659-160">Versão</span><span class="sxs-lookup"><span data-stu-id="85659-160">Version</span></span> |<span data-ttu-id="85659-161">Olá versão de API que está a ser utilizada.</span><span class="sxs-lookup"><span data-stu-id="85659-161">hello API version being used.</span></span>  <span data-ttu-id="85659-162">Atualmente, este deve ser sempre definida too1.</span><span class="sxs-lookup"><span data-stu-id="85659-162">Currently, this should always be set too1.</span></span> |

### <a name="retrieving-actions"></a><span data-ttu-id="85659-163">A obter ações</span><span class="sxs-lookup"><span data-stu-id="85659-163">Retrieving actions</span></span>
<span data-ttu-id="85659-164">Olá utilize obter método tooretrieve todas as ações para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-164">Use hello Get method tooretrieve all actions for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search  ID}/schedules/{Schedule ID}/actions?api-version=2015-03-20

<span data-ttu-id="85659-165">Olá utilize obter método com Olá ação ID tooretrieve uma ação específica para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-165">Use hello Get method with hello action ID tooretrieve a particular action for a schedule.</span></span>

    armclient get /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/actions/{Action ID}?api-version=2015-03-20

### <a name="creating-or-editing-actions"></a><span data-ttu-id="85659-166">Criação ou edição de ações</span><span class="sxs-lookup"><span data-stu-id="85659-166">Creating or editing actions</span></span>
<span data-ttu-id="85659-167">Utilize o método de Put Olá com um ID de ação que é exclusiva toohello agenda toocreate uma ação de novo.</span><span class="sxs-lookup"><span data-stu-id="85659-167">Use hello Put method with an action ID that is unique toohello schedule toocreate a new action.</span></span>  <span data-ttu-id="85659-168">Quando cria uma ação na consola do OMS Olá, um GUID é Olá ação ID</span><span class="sxs-lookup"><span data-stu-id="85659-168">When you create an action in hello OMS console, a GUID is for hello action ID.</span></span>

> [!NOTE]
> <span data-ttu-id="85659-169">nome de Olá para pesquisas guardadas todos os, agendas e criadas com Olá API de análise do registo de ações, tem de ser em minúsculas.</span><span class="sxs-lookup"><span data-stu-id="85659-169">hello name for all saved searches, schedules, and actions created with hello Log Analytics API must be in lowercase.</span></span>

<span data-ttu-id="85659-170">Utilize o método de Put do Olá com uma ação existente ID para Olá mesmo guardar pesquisa toomodify agendar.</span><span class="sxs-lookup"><span data-stu-id="85659-170">Use hello Put method with an existing action ID for hello same saved search toomodify that schedule.</span></span>  <span data-ttu-id="85659-171">corpo de Olá de pedido de Olá tem de incluir Olá etag da agenda de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-171">hello body of hello request must include hello etag of hello schedule.</span></span>

<span data-ttu-id="85659-172">formato de pedido de Olá para criar uma nova ação varia consoante o tipo de ação para que estes exemplos são fornecidos nas secções de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="85659-172">hello request format for creating a new action varies by action type so these examples are provided in hello sections below.</span></span>

### <a name="deleting-actions"></a><span data-ttu-id="85659-173">Eliminar ações</span><span class="sxs-lookup"><span data-stu-id="85659-173">Deleting actions</span></span>
<span data-ttu-id="85659-174">Utilize o método Delete de Olá com Olá ação ID toodelete uma ação.</span><span class="sxs-lookup"><span data-stu-id="85659-174">Use hello Delete method with hello action ID toodelete an action.</span></span>

    armclient delete /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Subscription ID}/schedules/{Schedule ID}/Actions/{Action ID}?api-version=2015-03-20

### <a name="alert-actions"></a><span data-ttu-id="85659-175">Ações de alerta</span><span class="sxs-lookup"><span data-stu-id="85659-175">Alert Actions</span></span>
<span data-ttu-id="85659-176">Uma agenda deve ter um e apenas uma ação de alerta.</span><span class="sxs-lookup"><span data-stu-id="85659-176">A Schedule should have one and only one Alert action.</span></span>  <span data-ttu-id="85659-177">Ações de alerta de ter uma ou mais das secções Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-177">Alert actions have one or more of hello sections in hello following table.</span></span>  <span data-ttu-id="85659-178">Cada um é descrita mais detalhadamente abaixo.</span><span class="sxs-lookup"><span data-stu-id="85659-178">Each is described in further detail below.</span></span>

| <span data-ttu-id="85659-179">Secção</span><span class="sxs-lookup"><span data-stu-id="85659-179">Section</span></span> | <span data-ttu-id="85659-180">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-180">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-181">Limiar</span><span class="sxs-lookup"><span data-stu-id="85659-181">Threshold</span></span> |<span data-ttu-id="85659-182">Critérios de execução da ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-182">Criteria for when hello action is run.</span></span> |
| <span data-ttu-id="85659-183">EmailNotification</span><span class="sxs-lookup"><span data-stu-id="85659-183">EmailNotification</span></span> |<span data-ttu-id="85659-184">Envie correio toomultiple destinatários.</span><span class="sxs-lookup"><span data-stu-id="85659-184">Send mail toomultiple recipients.</span></span> |
| <span data-ttu-id="85659-185">Remediação</span><span class="sxs-lookup"><span data-stu-id="85659-185">Remediation</span></span> |<span data-ttu-id="85659-186">Iniciar um runbook na automatização do Azure tooattempt toocorrect identificado o problema.</span><span class="sxs-lookup"><span data-stu-id="85659-186">Start a runbook in Azure Automation tooattempt toocorrect identified issue.</span></span> |

#### <a name="thresholds"></a><span data-ttu-id="85659-187">Limiares</span><span class="sxs-lookup"><span data-stu-id="85659-187">Thresholds</span></span>
<span data-ttu-id="85659-188">Uma ação de alerta deve ter um e apenas um limiar.</span><span class="sxs-lookup"><span data-stu-id="85659-188">An Alert action should have one and only one threshold.</span></span>  <span data-ttu-id="85659-189">Quando os resultados de Olá de uma procura guardada corresponderem limiar Olá numa ação associada essa procura, quaisquer outros processos nessa ação são executados.</span><span class="sxs-lookup"><span data-stu-id="85659-189">When hello results of a saved search match hello threshold in an action associated with that search, then any other processes in that action are run.</span></span>  <span data-ttu-id="85659-190">Uma ação também pode conter apenas um limiar para que possa ser utilizado com as ações de outros tipos que não contenham limiares.</span><span class="sxs-lookup"><span data-stu-id="85659-190">An action can also contain only a threshold so that it can be used with actions of other types that don’t contain thresholds.</span></span>

<span data-ttu-id="85659-191">Limiares tem propriedades de Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-191">Thresholds have hello properties in hello following table.</span></span>

| <span data-ttu-id="85659-192">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-192">Property</span></span> | <span data-ttu-id="85659-193">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-193">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-194">operador</span><span class="sxs-lookup"><span data-stu-id="85659-194">Operator</span></span> |<span data-ttu-id="85659-195">Operador de comparação de limiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-195">Operator for hello threshold comparison.</span></span> <br> <span data-ttu-id="85659-196">gt = maior que</span><span class="sxs-lookup"><span data-stu-id="85659-196">gt = Greater Than</span></span> <br> <span data-ttu-id="85659-197">lt = inferior a</span><span class="sxs-lookup"><span data-stu-id="85659-197">lt = Less Than</span></span> |
| <span data-ttu-id="85659-198">Valor</span><span class="sxs-lookup"><span data-stu-id="85659-198">Value</span></span> |<span data-ttu-id="85659-199">Valor de limiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-199">Value for hello threshold.</span></span> |

<span data-ttu-id="85659-200">Por exemplo, considere uma consulta de eventos com um intervalo de 15 minutos, Timespan de 30 minutos e um limiar de maior que 10.</span><span class="sxs-lookup"><span data-stu-id="85659-200">For example, consider an event query with an Interval of 15 minutes, a Timespan of 30 minutes, and a Threshold of greater than 10.</span></span> <span data-ttu-id="85659-201">Neste caso, consulta Olá iria ser executada a cada 15 minutos e seria possível acionar um alerta se devolveu 10 eventos que foram criados ao longo de um intervalo de 30 minutos.</span><span class="sxs-lookup"><span data-stu-id="85659-201">In this case, hello query would be run every 15 minutes, and an alert would be triggered if it returned 10 events that were created over a 30 minute span.</span></span>

<span data-ttu-id="85659-202">Segue-se uma resposta de amostra de uma ação com apenas um limiar.</span><span class="sxs-lookup"><span data-stu-id="85659-202">Following is a sample response for an action with only a threshold.</span></span>  

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

<span data-ttu-id="85659-203">Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação de limiar para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-203">Use hello Put method with a unique action ID toocreate a new threshold action for a schedule.</span></span>  

    $thresholdJson = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

<span data-ttu-id="85659-204">Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de limiar existente para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-204">Use hello Put method with an existing action ID toomodify a threshold action for a schedule.</span></span>  <span data-ttu-id="85659-205">corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-205">hello body of hello request must include hello etag of hello action.</span></span>

    $thresholdJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdJson

#### <a name="email-notification"></a><span data-ttu-id="85659-206">Notificação por e-mail</span><span class="sxs-lookup"><span data-stu-id="85659-206">Email Notification</span></span>
<span data-ttu-id="85659-207">Enviam notificações por e-mail correio tooone ou mais destinatários.</span><span class="sxs-lookup"><span data-stu-id="85659-207">Email Notifications send mail tooone or more recipients.</span></span>  <span data-ttu-id="85659-208">Estas incluírem propriedades Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-208">They include hello properties in hello following table.</span></span>

| <span data-ttu-id="85659-209">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-209">Property</span></span> | <span data-ttu-id="85659-210">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-210">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-211">Destinatários</span><span class="sxs-lookup"><span data-stu-id="85659-211">Recipients</span></span> |<span data-ttu-id="85659-212">Lista de endereços de correio.</span><span class="sxs-lookup"><span data-stu-id="85659-212">List of mail addresses.</span></span> |
| <span data-ttu-id="85659-213">Assunto</span><span class="sxs-lookup"><span data-stu-id="85659-213">Subject</span></span> |<span data-ttu-id="85659-214">requerente Olá do correio Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-214">hello subject of hello mail.</span></span> |
| <span data-ttu-id="85659-215">Anexo</span><span class="sxs-lookup"><span data-stu-id="85659-215">Attachment</span></span> |<span data-ttu-id="85659-216">Anexos não são atualmente suportados, pelo que este terão sempre um valor de "None".</span><span class="sxs-lookup"><span data-stu-id="85659-216">Attachments are not currently supported, so this will always have a value of “None”.</span></span> |

<span data-ttu-id="85659-217">Segue-se uma resposta de amostra de uma ação de notificação de correio eletrónico com um limiar.</span><span class="sxs-lookup"><span data-stu-id="85659-217">Following is a sample response for an email notification action with a threshold.</span></span>  

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

<span data-ttu-id="85659-218">Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma ação de correio eletrónico novo para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-218">Use hello Put method with a unique action ID toocreate a new e-mail action for a schedule.</span></span>  <span data-ttu-id="85659-219">Olá exemplo seguinte cria uma notificação por e-mail com um limiar pelo Olá o correio eletrónico é enviado quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-219">hello following example creates an email notification with a threshold so hello mail is sent when hello results of hello saved search exceed hello threshold.</span></span>

    $emailJson = "{'properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

<span data-ttu-id="85659-220">Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de correio eletrónico existente para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-220">Use hello Put method with an existing action ID toomodify an e-mail action for a schedule.</span></span>  <span data-ttu-id="85659-221">corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-221">hello body of hello request must include hello etag of hello action.</span></span>

    $emailJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Name': 'MyEmailAction', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'EmailNotification': {'Recipients': ['recipient1@contoso.com', 'recipient2@contoso.com'], 'Subject':'This is hello subject', 'Attachment':'None'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myemailaction?api-version=2015-03-20 $emailJson

#### <a name="remediation-actions"></a><span data-ttu-id="85659-222">Ações de remediação</span><span class="sxs-lookup"><span data-stu-id="85659-222">Remediation actions</span></span>
<span data-ttu-id="85659-223">Remediações iniciar um runbook na automatização do Azure que tenta problema de Olá toocorrect identificado pelo alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-223">Remediations start a runbook in Azure Automation that attempts toocorrect hello problem identified by hello alert.</span></span>  <span data-ttu-id="85659-224">Tem de criar um webhook do runbook Olá utilizado na ação de remediação e, em seguida, especifique Olá URI no Olá WebhookUri propriedade.</span><span class="sxs-lookup"><span data-stu-id="85659-224">You must create a webhook for hello runbook used in a remediation action and then specify hello URI in hello WebhookUri property.</span></span>  <span data-ttu-id="85659-225">Ao criar esta ação utilizando a consola do OMS Olá, é criado automaticamente um novo webhook do runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-225">When you create this action using hello OMS console, a new webhook is automatically created for hello runbook.</span></span>

<span data-ttu-id="85659-226">Remediações incluem propriedades Olá Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-226">Remediations include hello properties in hello following table.</span></span>

| <span data-ttu-id="85659-227">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-227">Property</span></span> | <span data-ttu-id="85659-228">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-228">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-229">RunbookName</span><span class="sxs-lookup"><span data-stu-id="85659-229">RunbookName</span></span> |<span data-ttu-id="85659-230">Nome do runbook Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-230">Name of hello runbook.</span></span> <span data-ttu-id="85659-231">Isto deve corresponder ao runbook publicado na conta de automatização de Olá configurado no Olá solução de automatização na sua área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="85659-231">This must match a published runbook in hello automation account configured in hello Automation Solution in your OMS workspace.</span></span> |
| <span data-ttu-id="85659-232">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="85659-232">WebhookUri</span></span> |<span data-ttu-id="85659-233">URI de Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="85659-233">URI of hello webhook.</span></span> |
| <span data-ttu-id="85659-234">Expiração</span><span class="sxs-lookup"><span data-stu-id="85659-234">Expiry</span></span> |<span data-ttu-id="85659-235">data de expiração de Olá e a hora de Olá webhook.</span><span class="sxs-lookup"><span data-stu-id="85659-235">hello expiration date and time of hello webhook.</span></span>  <span data-ttu-id="85659-236">Se Olá webhook não tiver uma expiração, em seguida, isto pode ser qualquer data futura válida.</span><span class="sxs-lookup"><span data-stu-id="85659-236">If hello webhook doesn’t have an expiration, then this can be any valid future date.</span></span> |

<span data-ttu-id="85659-237">Segue-se uma resposta de amostra de uma ação de remediação com um limiar.</span><span class="sxs-lookup"><span data-stu-id="85659-237">Following is a sample response for a remediation action with a threshold.</span></span>

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

<span data-ttu-id="85659-238">Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação de remediação para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-238">Use hello Put method with a unique action ID toocreate a new remediation action for a schedule.</span></span>  <span data-ttu-id="85659-239">Olá exemplo seguinte cria uma remediação com um limiar para que Olá runbook é iniciado quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-239">hello following example creates a remediation with a threshold so hello runbook is started when hello results of hello saved search exceed hello threshold.</span></span>

    $remediateJson = "{'properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

<span data-ttu-id="85659-240">Utilize o método de Put do Olá com um toomodify de ID de ação uma ação de remediação existente para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-240">Use hello Put method with an existing action ID toomodify a remediation action for a schedule.</span></span>  <span data-ttu-id="85659-241">corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-241">hello body of hello request must include hello etag of hello action.</span></span>

    $remediateJson = "{'etag': 'W/\"datetime'2016-02-25T20%3A54%3A20.1302566Z'\"','properties': { 'Type':'Alert', 'Name': 'My Remediation Action', 'Version':'1', 'Threshold': { 'Operator': 'gt', 'Value': 10 }, 'Remediation': {'RunbookName': 'My-Runbook', 'WebhookUri':'https://s1events.azure-automation.net/webhooks?token=4jCibOjO3w4W2Cfg%2b2NkjLYdafnusaG6i8tnP8h%2fNNg%3d', 'Expiry':'2018-02-25T18:27:20Z'} }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/myremediationaction?api-version=2015-03-20 $remediateJson

#### <a name="example"></a><span data-ttu-id="85659-242">Exemplo</span><span class="sxs-lookup"><span data-stu-id="85659-242">Example</span></span>
<span data-ttu-id="85659-243">Segue-se um exemplo completo de toocreate um novo alerta de e-mail.</span><span class="sxs-lookup"><span data-stu-id="85659-243">Following is a complete example toocreate a new email alert.</span></span>  <span data-ttu-id="85659-244">Esta ação cria uma nova agenda juntamente com uma ação que contém um limiar e e-mail.</span><span class="sxs-lookup"><span data-stu-id="85659-244">This creates a new schedule along with an action containing a threshold and email.</span></span>

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

### <a name="webhook-actions"></a><span data-ttu-id="85659-245">Ações de Webhook</span><span class="sxs-lookup"><span data-stu-id="85659-245">Webhook actions</span></span>
<span data-ttu-id="85659-246">As ações de Webhook iniciar um processo ao chamar um URL e, opcionalmente, fornecer um toobe payload enviada.</span><span class="sxs-lookup"><span data-stu-id="85659-246">Webhook actions start a process by calling a URL and optionally providing a payload toobe sent.</span></span>  <span data-ttu-id="85659-247">Estes são semelhantes tooRemediation ações exceto no que se destinam para webhooks que pode invocar processos que não sejam runbooks de automatização do Azure.</span><span class="sxs-lookup"><span data-stu-id="85659-247">They are similar tooRemediation actions except they are meant for webhooks that may invoke processes other than Azure Automation runbooks.</span></span>  <span data-ttu-id="85659-248">Também fornecem opção adicional de Olá de fornecer um payload toobe entregar toohello um processo remoto.</span><span class="sxs-lookup"><span data-stu-id="85659-248">They also provide hello additional option of providing a payload toobe delivered toohello remote process.</span></span>

<span data-ttu-id="85659-249">As ações de Webhook não dispõe de um limiar, mas em vez disso, devem ser adicionadas tooa agenda que tem uma ação com um limiar de alerta.</span><span class="sxs-lookup"><span data-stu-id="85659-249">Webhook actions do not have a threshold but instead should be added tooa schedule that has an Alert action with a threshold.</span></span>  <span data-ttu-id="85659-250">Pode adicionar várias ações de Webhook todas serem executadas quando Olá limiar ser cumprido.</span><span class="sxs-lookup"><span data-stu-id="85659-250">You can add multiple Webhook actions that will all be run when hello threshold is met.</span></span>

<span data-ttu-id="85659-251">As ações de Webhook incluem propriedades Olá no Olá a tabela seguinte.</span><span class="sxs-lookup"><span data-stu-id="85659-251">Webhook actions include hello properties in hello following table.</span></span>

| <span data-ttu-id="85659-252">Propriedade</span><span class="sxs-lookup"><span data-stu-id="85659-252">Property</span></span> | <span data-ttu-id="85659-253">Descrição</span><span class="sxs-lookup"><span data-stu-id="85659-253">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="85659-254">WebhookUri</span><span class="sxs-lookup"><span data-stu-id="85659-254">WebhookUri</span></span> |<span data-ttu-id="85659-255">requerente Olá do correio Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-255">hello subject of hello mail.</span></span> |
| <span data-ttu-id="85659-256">CustomPayload</span><span class="sxs-lookup"><span data-stu-id="85659-256">CustomPayload</span></span> |<span data-ttu-id="85659-257">Payload personalizado toobe enviado toohello webhook.</span><span class="sxs-lookup"><span data-stu-id="85659-257">Custom payload toobe sent toohello webhook.</span></span>  <span data-ttu-id="85659-258">formato de Olá dependerá que webhook Olá está à espera.</span><span class="sxs-lookup"><span data-stu-id="85659-258">hello format will depend on what hello webhook is expecting.</span></span> |

<span data-ttu-id="85659-259">Segue-se uma resposta de exemplo para a ação de webhook e uma ação de alerta associada com um limiar.</span><span class="sxs-lookup"><span data-stu-id="85659-259">Following is a sample response for webhook action and an associated alert action with a threshold.</span></span>

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

#### <a name="create-or-edit-a-webhook-action"></a><span data-ttu-id="85659-260">Criar ou editar uma ação do webhook</span><span class="sxs-lookup"><span data-stu-id="85659-260">Create or edit a webhook action</span></span>
<span data-ttu-id="85659-261">Utilize o método de Put do Olá com um toocreate de ID de ação exclusivo uma nova ação do webhook para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-261">Use hello Put method with a unique action ID toocreate a new webhook action for a schedule.</span></span>  <span data-ttu-id="85659-262">Olá exemplo seguinte cria uma ação de Webhook e uma ação de alerta com um limiar para que Olá webhook será acionada quando Olá os resultados da Olá guardada pesquisa excedem o limiar de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-262">hello following example creates a Webhook action and an Alert action with a threshold so that hello webhook will be triggered when hello results of hello saved search exceed hello threshold.</span></span>

    $thresholdAction = "{'properties': { 'Name': 'My Threshold', 'Version':'1', 'Type':'Alert', 'Threshold': { 'Operator': 'gt', 'Value': 10 } }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mythreshold?api-version=2015-03-20 $thresholdAction

    $webhookAction = "{'properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

<span data-ttu-id="85659-263">Utilize o método de Put do Olá com um toomodify de ID de ação uma ação do webhook existente para uma agenda.</span><span class="sxs-lookup"><span data-stu-id="85659-263">Use hello Put method with an existing action ID toomodify a webhook action for a schedule.</span></span>  <span data-ttu-id="85659-264">corpo de Olá de pedido de Olá tem de incluir Olá etag de ação de Olá.</span><span class="sxs-lookup"><span data-stu-id="85659-264">hello body of hello request must include hello etag of hello action.</span></span>

    $webhookAction = "{'etag': 'W/\"datetime'2016-02-26T20%3A25%3A00.6862124Z'\"','properties': {'Type': 'Webhook', 'Name': 'My Webhook", 'WebhookUri': 'https://oaaswebhookdf.cloudapp.net/webhooks?token=VrkYTKlhk%2fc%2bKBP', 'CustomPayload': '{\"field1\":\"value1\",\"field2\":\"value2\"}', 'Version': 1 }"
    armclient put /subscriptions/{Subscription ID}/resourceGroups/OI-Default-East-US/providers/Microsoft.OperationalInsights/workspaces/{Workspace Name}/savedSearches/{Search ID}/schedules/{Schedule ID}/actions/mywebhookaction?api-version=2015-03-20 $webhookAction

## <a name="next-steps"></a><span data-ttu-id="85659-265">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="85659-265">Next steps</span></span>
* <span data-ttu-id="85659-266">Olá utilize [REST API tooperform registo pesquisas](log-analytics-log-search-api.md) na análise de registos.</span><span class="sxs-lookup"><span data-stu-id="85659-266">Use hello [REST API tooperform log searches](log-analytics-log-search-api.md) in Log Analytics.</span></span>

