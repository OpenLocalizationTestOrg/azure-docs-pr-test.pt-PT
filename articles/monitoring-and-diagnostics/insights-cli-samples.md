---
title: "Exemplos de início rápido aaaAzure Monitor CLI 1.0. | Microsoft Docs"
description: "Comandos de exemplo CLI 1.0 para funcionalidades de monitorização do Azure. Monitor do Azure é um serviço do Microsoft Azure que permite as notificações de alerta toosend, chamada web URLs com base nos valores de dados de telemetria configurado e serviços de Cloud de dimensionamento automático, as máquinas virtuais e aplicações Web."
author: kamathashwin
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 1653aa81-0ee6-4622-9c65-d4801ed9006f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: ashwink
ms.openlocfilehash: 6cd9cd62b3a1977276563f5e43f5384ccca66247
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-monitor--cross-platform-cli-10-quick-start-samples"></a><span data-ttu-id="e184c-105">Exemplos de início rápido 1.0 Monitor plataforma CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="e184c-105">Azure Monitor  Cross-platform CLI 1.0 quick start samples</span></span>
<span data-ttu-id="e184c-106">Este artigo apresenta o exemplo toohelp de comandos de interface de linha de comandos (CLI) pode aceder às funcionalidades de monitorização do Azure.</span><span class="sxs-lookup"><span data-stu-id="e184c-106">This article shows you sample command-line interface (CLI) commands toohelp you access Azure Monitor features.</span></span> <span data-ttu-id="e184c-107">Monitor do Azure permite-lhe tooAutoScale serviços em nuvem, as máquinas virtuais e aplicações Web e toosend as notificações de alerta ou chamada web URLs com base nos valores de dados de telemetria configurado.</span><span class="sxs-lookup"><span data-stu-id="e184c-107">Azure Monitor allows you tooAutoScale Cloud Services, Virtual Machines, and Web Apps and toosend alert notifications or call web URLs based on values of configured telemetry data.</span></span>

> [!NOTE]
> <span data-ttu-id="e184c-108">Monitor do Azure é o nome novo Olá que foi chamado "Informações do Azure" até 25th de Setembro de 2016.</span><span class="sxs-lookup"><span data-stu-id="e184c-108">Azure Monitor is hello new name for what was called "Azure Insights" until Sept 25th, 2016.</span></span> <span data-ttu-id="e184c-109">No entanto, Olá espaços de nomes e, consequentemente, os comandos de Olá abaixo contém ainda insights"Olá".</span><span class="sxs-lookup"><span data-stu-id="e184c-109">However, hello namespaces and thus hello commands below still contain hello "insights".</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="e184c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e184c-110">Prerequisites</span></span>
<span data-ttu-id="e184c-111">Se ainda não instalou Olá CLI do Azure, consulte [instalação Olá CLI do Azure](../cli-install-nodejs.md).</span><span class="sxs-lookup"><span data-stu-id="e184c-111">If you haven't already installed hello Azure CLI, see [Install hello Azure CLI](../cli-install-nodejs.md).</span></span> <span data-ttu-id="e184c-112">Se não estiver familiarizado com a CLI do Azure, pode ler mais sobre-lo no [Olá utilize CLI do Azure para Mac, Linux e Windows com o Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e184c-112">If you're unfamiliar with Azure CLI, you can read more about it at [Use hello Azure CLI for Mac, Linux, and Windows with Azure Resource Manager](../xplat-cli-azure-resource-manager.md).</span></span>

<span data-ttu-id="e184c-113">No Windows, instale npm a partir de Olá [Web site do Node.js](https://nodejs.org/).</span><span class="sxs-lookup"><span data-stu-id="e184c-113">In Windows, install npm from hello [Node.js website](https://nodejs.org/).</span></span> <span data-ttu-id="e184c-114">Depois de concluir a instalação de Olá, com CMD.exe com privilégios de executar como administrador, execute o seguinte Olá a partir da pasta de olá onde npm está instalado:</span><span class="sxs-lookup"><span data-stu-id="e184c-114">After you complete hello installation, using CMD.exe with Run As Administrator privileges, execute hello following from hello folder where npm is installed:</span></span>

```console
npm install azure-cli --global
```

<span data-ttu-id="e184c-115">Em seguida, navegue até tooany/localização da pasta que pretende e escreva Olá da linha de comandos:</span><span class="sxs-lookup"><span data-stu-id="e184c-115">Next, navigate tooany folder/location you want and type at hello command-line:</span></span>

```console
azure help
```

## <a name="log-in-tooazure"></a><span data-ttu-id="e184c-116">Inicie sessão no tooAzure</span><span class="sxs-lookup"><span data-stu-id="e184c-116">Log in tooAzure</span></span>
<span data-ttu-id="e184c-117">Step-by-Olá primeiro passo é toologin tooyour conta do Azure.</span><span class="sxs-lookup"><span data-stu-id="e184c-117">hello first step is toologin tooyour Azure account.</span></span>

```console
azure login
```

<span data-ttu-id="e184c-118">Depois de executar este comando, tem toosign em através de instruções de Olá no ecrã de Olá.</span><span class="sxs-lookup"><span data-stu-id="e184c-118">After running this command, you have toosign in via hello instructions on hello screen.</span></span> <span data-ttu-id="e184c-119">Posteriormente, para ver a conta, TenantId e predefinido ID da subscrição. Todos os comandos funcionam no contexto de Olá da sua subscrição predefinida.</span><span class="sxs-lookup"><span data-stu-id="e184c-119">Afterward, you see your Account, TenantId, and default Subscription Id. All commands work in hello context of your default subscription.</span></span>

<span data-ttu-id="e184c-120">detalhes de Olá toolist da sua subscrição atual, utilize Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e184c-120">toolist hello details of your current subscription, use hello following command.</span></span>

```console
azure account show
```

<span data-ttu-id="e184c-121">toochange trabalho contexto tooa subscrição diferente, Olá utilize os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e184c-121">toochange working context tooa different subscription, use hello following command.</span></span>

```console
azure account set "subscription ID or subscription name"
```

<span data-ttu-id="e184c-122">toouse o Azure Resource Manager e o Monitor de Azure os comandos, terá de toobe no modo Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="e184c-122">toouse Azure Resource Manager and Azure Monitor commands, you need toobe in Azure Resource Manager mode.</span></span>

```console
azure config mode arm
```

<span data-ttu-id="e184c-123">tooview uma lista de todos os comandos suportados do Monitor do Azure, execute o seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="e184c-123">tooview a list of all supported Azure Monitor commands, perform hello following.</span></span>

```console
azure insights
```

## <a name="view-activity-log-for-a-subscription"></a><span data-ttu-id="e184c-124">Ver o registo de atividade para uma subscrição</span><span class="sxs-lookup"><span data-stu-id="e184c-124">View activity log for a subscription</span></span>
<span data-ttu-id="e184c-125">tooview uma lista de eventos de registo de atividade, efetue o seguinte de Olá.</span><span class="sxs-lookup"><span data-stu-id="e184c-125">tooview a list of activity log events, perform hello following.</span></span>

```console
azure insights logs list [options]
```

<span data-ttu-id="e184c-126">Tente Olá seguir tooview todas as opções disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e184c-126">Try hello following tooview all available options.</span></span>

```console
azure insights logs list -help
```

<span data-ttu-id="e184c-127">Eis um exemplo registos toolist por um resourceGroup</span><span class="sxs-lookup"><span data-stu-id="e184c-127">Here is an example toolist logs by a resourceGroup</span></span>

```console
azure insights logs list --resourceGroup "myrg1"
```

<span data-ttu-id="e184c-128">Registos de toolist de exemplo pelo autor da chamada</span><span class="sxs-lookup"><span data-stu-id="e184c-128">Example toolist logs by caller</span></span>

```console
azure insights logs list --caller "myname@company.com"
```

<span data-ttu-id="e184c-129">Registos de toolist de exemplo pelo autor da chamada num tipo de recurso, dentro de uma data de início e de fim</span><span class="sxs-lookup"><span data-stu-id="e184c-129">Example toolist logs by caller on a resource type, within a start and end date</span></span>

```console
azure insights logs list --resourceProvider "Microsoft.Web" --caller "myname@company.com" --startTime 2016-03-08T00:00:00Z --endTime 2016-03-16T00:00:00Z
```

## <a name="work-with-alerts"></a><span data-ttu-id="e184c-130">Trabalhar com alertas</span><span class="sxs-lookup"><span data-stu-id="e184c-130">Work with alerts</span></span>
<span data-ttu-id="e184c-131">Pode utilizar informações de Olá Olá secção toowork com alertas.</span><span class="sxs-lookup"><span data-stu-id="e184c-131">You can use hello information in hello section toowork with alerts.</span></span>

### <a name="get-alert-rules-in-a-resource-group"></a><span data-ttu-id="e184c-132">Obter as regras de alerta num grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e184c-132">Get alert rules in a resource group</span></span>
```console
azure insights alerts rule list abhingrgtest123
azure insights alerts rule list abhingrgtest123 --ruleName andy0323
```

### <a name="create-a-metric-alert-rule"></a><span data-ttu-id="e184c-133">Criar uma regra de alerta métrica</span><span class="sxs-lookup"><span data-stu-id="e184c-133">Create a metric alert rule</span></span>
```console
azure insights alerts actions email create --customEmails foo@microsoft.com
azure insights alerts actions webhook create https://someuri.com
azure insights alerts rule metric set andy0323 eastus abhingrgtest123 PT5M GreaterThan 2 /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Web-EastUS/providers/Microsoft.Web/serverfarms/Default1 BytesReceived Total
```

### <a name="create-webtest-alert-rule"></a><span data-ttu-id="e184c-134">Criar regra de alerta do teste Web</span><span class="sxs-lookup"><span data-stu-id="e184c-134">Create webtest alert rule</span></span>
```console
azure insights alerts rule webtest set leowebtestr1-webtestr1 eastus Default-Web-WestUS PT5M 1 GSMT_AvRaw /subscriptions/b67f7fec-69fc-4974-9099-a26bd6ffeda3/resourcegroups/Default-Web-WestUS/providers/microsoft.insights/webtests/leowebtestr1-webtestr1
```

### <a name="delete-an-alert-rule"></a><span data-ttu-id="e184c-135">Eliminar uma regra de alerta</span><span class="sxs-lookup"><span data-stu-id="e184c-135">Delete an alert rule</span></span>
```console
azure insights alerts rule delete abhingrgtest123 andy0323
```

## <a name="log-profiles"></a><span data-ttu-id="e184c-136">Perfis de registo</span><span class="sxs-lookup"><span data-stu-id="e184c-136">Log profiles</span></span>
<span data-ttu-id="e184c-137">Utilize as informações de Olá toowork esta secção com perfis de registo.</span><span class="sxs-lookup"><span data-stu-id="e184c-137">Use hello information in this section toowork with log profiles.</span></span>

### <a name="get-a-log-profile"></a><span data-ttu-id="e184c-138">Obter um perfil de registo</span><span class="sxs-lookup"><span data-stu-id="e184c-138">Get a log profile</span></span>
```console
azure insights logprofile list
azure insights logprofile get -n default
```


### <a name="add-a-log-profile-without-retention"></a><span data-ttu-id="e184c-139">Adicionar um perfil de registo sem retenção</span><span class="sxs-lookup"><span data-stu-id="e184c-139">Add a log profile without retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia
```

### <a name="remove-a-log-profile"></a><span data-ttu-id="e184c-140">Remover um perfil de registo</span><span class="sxs-lookup"><span data-stu-id="e184c-140">Remove a log profile</span></span>
```console
azure insights logprofile delete --name default
```

### <a name="add-a-log-profile-with-retention"></a><span data-ttu-id="e184c-141">Adicionar um perfil de registo com retenção</span><span class="sxs-lookup"><span data-stu-id="e184c-141">Add a log profile with retention</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```

### <a name="add-a-log-profile-with-retention-and-eventhub"></a><span data-ttu-id="e184c-142">Adicionar um perfil de registo com retenção e EventHub</span><span class="sxs-lookup"><span data-stu-id="e184c-142">Add a log profile with retention and EventHub</span></span>
```console
azure insights logprofile add --name default --storageId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/insights-integration/providers/Microsoft.Storage/storageAccounts/insightsintegration7777 --serviceBusRuleId /subscriptions/1a66ce04-b633-4a0b-b2bc-a912ec8986a6/resourceGroups/Default-ServiceBus-EastUS/providers/Microsoft.ServiceBus/namespaces/testshoeboxeastus/authorizationrules/RootManageSharedAccessKey --locations global,westus,eastus,northeurope,westeurope,eastasia,southeastasia,japaneast,japanwest,northcentralus,southcentralus,eastus2,centralus,australiaeast,australiasoutheast,brazilsouth,centralindia,southindia,westindia --retentionInDays 90
```


## <a name="diagnostics"></a><span data-ttu-id="e184c-143">Diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e184c-143">Diagnostics</span></span>
<span data-ttu-id="e184c-144">Utilize as informações de Olá toowork nesta secção, com definições de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="e184c-144">Use hello information in this section toowork with diagnostic settings.</span></span>

### <a name="get-a-diagnostic-setting"></a><span data-ttu-id="e184c-145">Obter uma definição de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e184c-145">Get a diagnostic setting</span></span>
```console
azure insights diagnostic get --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp
```

### <a name="disable-a-diagnostic-setting"></a><span data-ttu-id="e184c-146">Desativar a definição de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="e184c-146">Disable a diagnostic setting</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled false
```

### <a name="enable-a-diagnostic-setting-without-retention"></a><span data-ttu-id="e184c-147">Ativar uma definição de diagnóstico sem retenção</span><span class="sxs-lookup"><span data-stu-id="e184c-147">Enable a diagnostic setting without retention</span></span>
```console
azure insights diagnostic set --resourceId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/andyrg/providers/Microsoft.Logic/workflows/andy0315logicapp --storageId /subscriptions/df602c9c-7aa0-407d-a6fb-eb20c8bd1192/resourceGroups/Default-Storage-WestUS/providers/Microsoft.Storage/storageAccounts/shibanitesting --enabled true
```


## <a name="autoscale"></a><span data-ttu-id="e184c-148">Dimensionamento Automático</span><span class="sxs-lookup"><span data-stu-id="e184c-148">Autoscale</span></span>
<span data-ttu-id="e184c-149">Utilize as informações de Olá toowork nesta secção, com definições de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="e184c-149">Use hello information in this section toowork with autoscale settings.</span></span> <span data-ttu-id="e184c-150">É necessário toomodify estes exemplos.</span><span class="sxs-lookup"><span data-stu-id="e184c-150">You need toomodify these examples.</span></span>

### <a name="get-autoscale-settings-for-a-resource-group"></a><span data-ttu-id="e184c-151">Obter definições de dimensionamento automático para um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e184c-151">Get autoscale settings for a resource group</span></span>
```console
azure insights autoscale setting list montest2
```

### <a name="get-autoscale-settings-by-name-in-a-resource-group"></a><span data-ttu-id="e184c-152">Obter definições de dimensionamento automático por nome de um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="e184c-152">Get autoscale settings by name in a resource group</span></span>
```console
azure insights autoscale setting list montest2 -n setting2
```


### <a name="set-auotoscale-settings"></a><span data-ttu-id="e184c-153">Configurar as definições de auotoscale</span><span class="sxs-lookup"><span data-stu-id="e184c-153">Set auotoscale settings</span></span>
```console
azure insights autoscale setting set montest2 -n setting2 --settingSpec
```
