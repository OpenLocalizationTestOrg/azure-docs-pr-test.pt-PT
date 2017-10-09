---
title: "aaaOverview de registos de diagnóstico do Azure | Microsoft Docs"
description: "Saiba quais são os registos de diagnóstico do Azure e como pode utilizá-los eventos toounderstand ocorrer dentro de um recurso do Azure."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: fe8887df-b0e6-46f8-b2c0-11994d28e44f
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: johnkem; magoedte
ms.openlocfilehash: e38991c540626b4bb5b5b9a995276881ee58f368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="collect-and-consume-log-data-from-your-azure-resources"></a><span data-ttu-id="5e690-103">Recolher e consumir dados de registo dos seus recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5e690-103">Collect and consume log data from your Azure resources</span></span>

## <a name="what-are-azure-resource-diagnostic-logs"></a><span data-ttu-id="5e690-104">Quais são os registos de diagnóstico de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5e690-104">What are Azure resource diagnostic logs</span></span>
<span data-ttu-id="5e690-105">**Os registos de diagnóstico ao nível de recursos do Azure** são registos emitidos por um recurso que fornecem dados avançados, frequentes sobre a operação de Olá desse recurso.</span><span class="sxs-lookup"><span data-stu-id="5e690-105">**Azure resource-level diagnostic logs** are logs emitted by a resource that provide rich, frequent data about hello operation of that resource.</span></span> <span data-ttu-id="5e690-106">conteúdo de Olá estes registos varia consoante o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="5e690-106">hello content of these logs varies by resource type.</span></span> <span data-ttu-id="5e690-107">Por exemplo, os contadores de regra de grupo de segurança de rede e de auditorias do Cofre de chaves são duas categorias de registos de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e690-107">For example, Network Security Group rule counters and Key Vault audits are two categories of resource logs.</span></span>

<span data-ttu-id="5e690-108">Os registos de diagnóstico de nível de recursos sejam diferentes das Olá [registo de atividade](monitoring-overview-activity-logs.md).</span><span class="sxs-lookup"><span data-stu-id="5e690-108">Resource-level diagnostic logs differ from hello [Activity Log](monitoring-overview-activity-logs.md).</span></span> <span data-ttu-id="5e690-109">Olá registo de atividade fornece informações sobre as operações de Olá que foram efetuadas nos recursos na sua subscrição com o Resource Manager, por exemplo, criar uma máquina virtual ou eliminar uma aplicação lógica.</span><span class="sxs-lookup"><span data-stu-id="5e690-109">hello Activity Log provides insight into hello operations that were performed on resources in your subscription using Resource Manager, for example, creating a virtual machine or deleting a logic app.</span></span> <span data-ttu-id="5e690-110">Olá registo de atividade é um registo de nível de subscrição.</span><span class="sxs-lookup"><span data-stu-id="5e690-110">hello Activity Log is a subscription-level log.</span></span> <span data-ttu-id="5e690-111">Os registos de diagnóstico de nível de recursos fornecem informações aprofundadas operações que foram efetuadas no recurso de si próprio, por exemplo, obter um segredo do Cofre de chaves.</span><span class="sxs-lookup"><span data-stu-id="5e690-111">Resource-level diagnostic logs provide insight into operations that were performed within that resource itself, for example, getting a secret from a Key Vault.</span></span>

<span data-ttu-id="5e690-112">Os registos de diagnóstico de nível de recursos também diferem dos registos de diagnóstico de nível de SO convidado.</span><span class="sxs-lookup"><span data-stu-id="5e690-112">Resource-level diagnostic logs also differ from guest OS-level diagnostic logs.</span></span> <span data-ttu-id="5e690-113">Os registos de diagnóstico de SO convidado são esses recolhidos por um agente em execução dentro de uma máquina virtual ou outros suportado o tipo de recurso.</span><span class="sxs-lookup"><span data-stu-id="5e690-113">Guest OS diagnostic logs are those collected by an agent running inside of a virtual machine or other supported resource type.</span></span> <span data-ttu-id="5e690-114">Os registos de diagnóstico de nível de recursos requerem não existem dados de recursos específicos agente e captura do Olá plataforma do Azure, enquanto os registos de diagnóstico de nível de SO convidado capturar os dados do sistema de operativo Olá e aplicações em execução numa máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5e690-114">Resource-level diagnostic logs require no agent and capture resource-specific data from hello Azure platform itself, while guest OS-level diagnostic logs capture data from hello operating system and applications running on a virtual machine.</span></span>

<span data-ttu-id="5e690-115">Nem todos os recursos suportam novo tipo de Olá de registos de diagnóstico de recurso descrito aqui.</span><span class="sxs-lookup"><span data-stu-id="5e690-115">Not all resources support hello new type of resource diagnostic logs described here.</span></span> <span data-ttu-id="5e690-116">Este artigo contém uma lista de secção que tipos de recursos suportam Olá novo nível de recursos registos de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5e690-116">This article contains a section listing which resource types support hello new resource-level diagnostic logs.</span></span>

![<span data-ttu-id="5e690-117">Registos de diagnóstico de recurso vs outros tipos de registos</span><span class="sxs-lookup"><span data-stu-id="5e690-117">Resource diagnostics logs vs other types of logs</span></span> ](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_vs_other_logs_v5.png)

## <a name="what-you-can-do-with-resource-level-diagnostic-logs"></a><span data-ttu-id="5e690-118">O que pode fazer com os registos de diagnóstico de nível de recursos</span><span class="sxs-lookup"><span data-stu-id="5e690-118">What you can do with resource-level diagnostic logs</span></span>
<span data-ttu-id="5e690-119">Seguem-se algumas das ações de Olá que pode fazer com os registos de diagnóstico de recursos:</span><span class="sxs-lookup"><span data-stu-id="5e690-119">Here are some of hello things you can do with resource diagnostic logs:</span></span>

![Posicionamento de lógico de registos de diagnóstico de recursos](./media/monitoring-overview-of-diagnostic-logs/Diagnostics_Logs_Actions.png)


* <span data-ttu-id="5e690-121">Guardá-las tooa [ **conta de armazenamento** ](monitoring-archive-diagnostic-logs.md) de inspeção de auditoria ou manual.</span><span class="sxs-lookup"><span data-stu-id="5e690-121">Save them tooa [**Storage Account**](monitoring-archive-diagnostic-logs.md) for auditing or manual inspection.</span></span> <span data-ttu-id="5e690-122">Pode especificar Olá retenção tempo (em dias) utilizando **definições de diagnóstico de recurso**.</span><span class="sxs-lookup"><span data-stu-id="5e690-122">You can specify hello retention time (in days) using **resource diagnostic settings**.</span></span>
* <span data-ttu-id="5e690-123">[Transmiti-los demasiado**Event Hubs** ](monitoring-stream-diagnostic-logs-to-event-hubs.md) para ingestão por um serviço independente ou uma solução de análise personalizada, tais como o Power BI.</span><span class="sxs-lookup"><span data-stu-id="5e690-123">[Stream them too**Event Hubs**](monitoring-stream-diagnostic-logs-to-event-hubs.md) for ingestion by a third-party service or custom analytics solution such as PowerBI.</span></span>
* <span data-ttu-id="5e690-124">Analisá-los com [análise de registos do OMS](../log-analytics/log-analytics-azure-storage.md)</span><span class="sxs-lookup"><span data-stu-id="5e690-124">Analyze them with [OMS Log Analytics](../log-analytics/log-analytics-azure-storage.md)</span></span>

<span data-ttu-id="5e690-125">Pode utilizar uma conta de armazenamento ou espaço de nomes de Event Hubs que não se encontra em Olá mesma subscrição, conforme Olá um emitir os registos.</span><span class="sxs-lookup"><span data-stu-id="5e690-125">You can use a storage account or Event Hubs namespace that is not in hello same subscription as hello one emitting logs.</span></span> <span data-ttu-id="5e690-126">Olá utilizador configura a definição de Olá tem de ter Olá adequadas RBAC acesso tooboth as subscrições.</span><span class="sxs-lookup"><span data-stu-id="5e690-126">hello user who configures hello setting must have hello appropriate RBAC access tooboth subscriptions.</span></span>

## <a name="resource-diagnostic-settings"></a><span data-ttu-id="5e690-127">Definições de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="5e690-127">Resource diagnostic settings</span></span>
<span data-ttu-id="5e690-128">Registos de diagnóstico de recursos de não-computação recursos estão configurados com as definições de diagnóstico de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e690-128">Resource diagnostic logs for non-Compute resources are configured using resource diagnostic settings.</span></span> <span data-ttu-id="5e690-129">**Definições de diagnóstico de recurso** para um controlo de recursos:</span><span class="sxs-lookup"><span data-stu-id="5e690-129">**Resource diagnostic settings** for a resource control:</span></span>

* <span data-ttu-id="5e690-130">Onde os registos de diagnóstico de recursos e as métricas são enviadas (conta de armazenamento, os Event Hubs, e/ou análise de registos do OMS).</span><span class="sxs-lookup"><span data-stu-id="5e690-130">Where resource diagnostic logs and metrics are sent (Storage Account, Event Hubs, and/or OMS Log Analytics).</span></span>
* <span data-ttu-id="5e690-131">As categorias de registo são enviadas e se os dados métricos também são enviados.</span><span class="sxs-lookup"><span data-stu-id="5e690-131">Which log categories are sent and whether metric data is also sent.</span></span>
* <span data-ttu-id="5e690-132">Quanto cada categoria de registo deve ser mantida na conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="5e690-132">How long each log category should be retained in a storage account</span></span>
    - <span data-ttu-id="5e690-133">Uma retenção de zero dias significa que os registos são mantidos indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="5e690-133">A retention of zero days means logs are kept forever.</span></span> <span data-ttu-id="5e690-134">Caso contrário, o valor de Olá pode ser qualquer número de dias entre 1 e 2147483647.</span><span class="sxs-lookup"><span data-stu-id="5e690-134">Otherwise, hello value can be any number of days between 1 and 2147483647.</span></span>
    - <span data-ttu-id="5e690-135">Se as políticas de retenção estão definidas, mas armazenar os registos numa conta do Storage está desativada (por exemplo, se apenas as opções de Event Hubs ou OMS estão selecionadas), as políticas de retenção de Olá não tem qualquer efeito.</span><span class="sxs-lookup"><span data-stu-id="5e690-135">If retention policies are set but storing logs in a Storage Account is disabled (for example, if only Event Hubs or OMS options are selected), hello retention policies have no effect.</span></span>
    - <span data-ttu-id="5e690-136">As políticas de retenção são aplicado por dia, pelo que a Olá regista o fim do dia (UTC), do dia de Olá que se encontra agora para além da política de retenção de Olá são eliminados.</span><span class="sxs-lookup"><span data-stu-id="5e690-136">Retention policies are applied per-day, so at hello end of a day (UTC), logs from hello day that is now beyond hello retention policy are deleted.</span></span> <span data-ttu-id="5e690-137">Por exemplo, se tiver uma política de retenção de um dia, no início de Olá de hoje em dia a dia Olá hello registos de ontem de antes do dia de Olá seriam eliminados.</span><span class="sxs-lookup"><span data-stu-id="5e690-137">For example, if you had a retention policy of one day, at hello beginning of hello day today hello logs from hello day before yesterday would be deleted.</span></span>

<span data-ttu-id="5e690-138">Estas definições são facilmente configuradas através de definições de diagnóstico de Olá para um recurso no portal do Azure de Olá, através de comandos do Azure PowerShell e CLI ou através de Olá [API REST da Azure Monitor](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e690-138">These settings are easily configured via hello diagnostic settings for a resource in hello Azure portal, via Azure PowerShell and CLI commands, or via hello [Azure Monitor REST API](https://msdn.microsoft.com/library/azure/dn931943.aspx).</span></span>

> [!WARNING]
> <span data-ttu-id="5e690-139">Os registos de diagnóstico e métricas de camada de SO convidado Olá de utilização de recursos (por exemplo, VMs ou Service Fabric) de computação de [um mecanismo separado para a configuração e seleção de saídas](../azure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="5e690-139">Diagnostic logs and metrics for from hello guest OS layer of Compute resources (for example, VMs or Service Fabric) use [a separate mechanism for configuration and selection of outputs](../azure-diagnostics.md).</span></span>
>
>

## <a name="how-tooenable-collection-of-resource-diagnostic-logs"></a><span data-ttu-id="5e690-140">Como tooenable coleção de registos de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="5e690-140">How tooenable collection of resource diagnostic logs</span></span>
<span data-ttu-id="5e690-141">Coleção de registos de diagnóstico de recurso pode ser ativada [como parte da criação de um recurso num modelo do Resource Manager](./monitoring-enable-diagnostic-logs-using-template.md) ou depois de criar um recurso da página desse recurso no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="5e690-141">Collection of resource diagnostic logs can be enabled [as part of creating a resource in a Resource Manager template](./monitoring-enable-diagnostic-logs-using-template.md) or after a resource is created from that resource's page in hello portal.</span></span> <span data-ttu-id="5e690-142">Também pode ativar a coleção em qualquer momento utilizando os comandos do Azure PowerShell ou o CLI, ou Olá API de REST de Monitor do Azure.</span><span class="sxs-lookup"><span data-stu-id="5e690-142">You can also enable collection at any point using Azure PowerShell or CLI commands, or using hello Azure Monitor REST API.</span></span>

> [!TIP]
> <span data-ttu-id="5e690-143">Estas instruções não aplicadas diretamente tooevery recursos.</span><span class="sxs-lookup"><span data-stu-id="5e690-143">These instructions may not apply directly tooevery resource.</span></span> <span data-ttu-id="5e690-144">Consulte as hiperligações de esquema de Olá no Olá parte inferior desta página toounderstand especial os passos que podem ser aplicadas toocertain tipos de recursos.</span><span class="sxs-lookup"><span data-stu-id="5e690-144">See hello schema links at hello bottom of this page toounderstand special steps that may apply toocertain resource types.</span></span>
>
>

### <a name="enable-collection-of-resource-diagnostic-logs-in-hello-portal"></a><span data-ttu-id="5e690-145">Ativar a recolha de registos de diagnóstico de recurso no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="5e690-145">Enable collection of resource diagnostic logs in hello portal</span></span>
<span data-ttu-id="5e690-146">Pode ativar a coleção de registos de diagnóstico de recurso no Olá Azure portal depois de um recurso foi criado pelo recurso específico de tooa vai ou navegando tooAzure Monitor.</span><span class="sxs-lookup"><span data-stu-id="5e690-146">You can enable collection of resource diagnostic logs in hello Azure portal after a resource has been created either by going tooa specific resource or by navigating tooAzure Monitor.</span></span> <span data-ttu-id="5e690-147">tooenable isto através do Azure Monitor:</span><span class="sxs-lookup"><span data-stu-id="5e690-147">tooenable this via Azure Monitor:</span></span>

1. <span data-ttu-id="5e690-148">No Olá [portal do Azure](http://portal.azure.com), navegue até tooAzure Monitor e clique em **definições de diagnóstico**</span><span class="sxs-lookup"><span data-stu-id="5e690-148">In hello [Azure portal](http://portal.azure.com), navigate tooAzure Monitor and click on **Diagnostic Settings**</span></span>

    ![Secção de monitorização do Monitor do Azure](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

2. <span data-ttu-id="5e690-150">Opcionalmente filtrar a lista de Olá por tipo de recurso ou grupo de recursos, em seguida, clique no recurso de Olá para o qual gostaria de tooset uma definição de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5e690-150">Optionally filter hello list by resource group or resource type, then click on hello resource for which you would like tooset a diagnostic setting.</span></span>

3. <span data-ttu-id="5e690-151">Se não existem definições de existirem no recurso de Olá que selecionou, são toocreate que lhes é pedida uma definição.</span><span class="sxs-lookup"><span data-stu-id="5e690-151">If no settings exist on hello resource you have selected, you are prompted toocreate a setting.</span></span> <span data-ttu-id="5e690-152">Clique em "Ativar o diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="5e690-152">Click "Turn on diagnostics."</span></span>

   ![Adicionar definição de diagnóstico - sem definições existentes](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-none.png)

   <span data-ttu-id="5e690-154">Se existirem definições existentes no recurso de Olá, verá uma lista das definições já configurada neste recurso.</span><span class="sxs-lookup"><span data-stu-id="5e690-154">If there are existing settings on hello resource, you will see a list of settings already configured on this resource.</span></span> <span data-ttu-id="5e690-155">Clique em "Adicionar definição de diagnóstico".</span><span class="sxs-lookup"><span data-stu-id="5e690-155">Click "Add diagnostic setting."</span></span>

   ![Adicionar definição de diagnóstico - existente definições](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-multiple.png)

3. <span data-ttu-id="5e690-157">Atribua a um nome da definição, verifique as caixas de Olá para cada toowhich destino teria como toosend dados e configurar o recurso é utilizado para cada destino.</span><span class="sxs-lookup"><span data-stu-id="5e690-157">Give your setting a name, check hello boxes for each destination toowhich you would like toosend data, and configure which resource is used for each destination.</span></span> <span data-ttu-id="5e690-158">Opcionalmente, defina um número de dias tooretain estes registos utilizando Olá **retenção (dias)** controlos de deslize (apenas aplicável toohello conta destino de armazenamento).</span><span class="sxs-lookup"><span data-stu-id="5e690-158">Optionally, set a number of days tooretain these logs by using hello **Retention (days)** sliders (only applicable toohello storage account destination).</span></span> <span data-ttu-id="5e690-159">Uma retenção de zero dias armazena os registos de Olá indefinidamente.</span><span class="sxs-lookup"><span data-stu-id="5e690-159">A retention of zero days stores hello logs indefinitely.</span></span>
   
   ![Adicionar definição de diagnóstico - existente definições](media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-configure.png)
    
4. <span data-ttu-id="5e690-161">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="5e690-161">Click **Save**.</span></span>

<span data-ttu-id="5e690-162">Após alguns instantes, a nova definição é apresentada na lista de definições para este recurso e os registos de diagnóstico são enviados toohello Olá especificado destinos assim que os novos dados de evento são gerados.</span><span class="sxs-lookup"><span data-stu-id="5e690-162">After a few moments, hello new setting appears in your list of settings for this resource, and diagnostic logs are sent toohello specified destinations as soon as new event data is generated.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-powershell"></a><span data-ttu-id="5e690-163">Ativar a recolha de registos de diagnóstico de recursos através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="5e690-163">Enable collection of resource diagnostic logs via PowerShell</span></span>
<span data-ttu-id="5e690-164">coleção de tooenable de registos de diagnóstico de recursos através do Azure PowerShell, Olá utilize os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5e690-164">tooenable collection of resource diagnostic logs via Azure PowerShell, use hello following commands:</span></span>

<span data-ttu-id="5e690-165">armazenamento de tooenable dos registos de diagnóstico numa conta do storage, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-165">tooenable storage of diagnostic logs in a storage account, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -StorageAccountId [your storage account id] -Enabled $true
```

<span data-ttu-id="5e690-166">ID de conta de armazenamento de Olá Olá ID de recurso para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.</span><span class="sxs-lookup"><span data-stu-id="5e690-166">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="5e690-167">tooenable de transmissão em fluxo os registos de diagnóstico tooan do hub de eventos, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-167">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -ServiceBusRuleId [your Service Bus rule id] -Enabled $true
```

<span data-ttu-id="5e690-168">ID de regra de barramento de serviço Olá é uma cadeia com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="5e690-168">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="5e690-169">Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-169">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```powershell
Set-AzureRmDiagnosticSetting -ResourceId [your resource id] -WorkspaceId [resource id of hello log analytics workspace] -Enabled $true
```

<span data-ttu-id="5e690-170">Pode obter o ID de recurso Olá da sua área de trabalho de análise de registos utilizando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5e690-170">You can obtain hello resource ID of your Log Analytics workspace using hello following command:</span></span>

```powershell
(Get-AzureRmOperationalInsightsWorkspace).ResourceId
```

<span data-ttu-id="5e690-171">Pode combinar estas tooenable parâmetros várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="5e690-171">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-cli"></a><span data-ttu-id="5e690-172">Ativar a recolha de registos de diagnóstico de recursos através da CLI</span><span class="sxs-lookup"><span data-stu-id="5e690-172">Enable collection of resource diagnostic logs via CLI</span></span>
<span data-ttu-id="5e690-173">coleção de tooenable de registos de diagnóstico de recursos através de Olá CLI do Azure, utilize Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="5e690-173">tooenable collection of resource diagnostic logs via hello Azure CLI, use hello following commands:</span></span>

<span data-ttu-id="5e690-174">armazenamento de tooenable dos registos de diagnóstico numa conta do Storage, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-174">tooenable storage of diagnostic logs in a Storage Account, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --storageId <storageAccountId> --enabled true
```

<span data-ttu-id="5e690-175">ID de conta de armazenamento de Olá Olá ID de recurso para toowhich de conta de armazenamento de Olá pretende toosend Olá registos.</span><span class="sxs-lookup"><span data-stu-id="5e690-175">hello storage account ID is hello resource ID for hello storage account toowhich you want toosend hello logs.</span></span>

<span data-ttu-id="5e690-176">tooenable de transmissão em fluxo os registos de diagnóstico tooan do hub de eventos, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-176">tooenable streaming of diagnostic logs tooan event hub, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --serviceBusRuleId <serviceBusRuleId> --enabled true
```

<span data-ttu-id="5e690-177">ID de regra de barramento de serviço Olá é uma cadeia com este formato: `{Service Bus resource ID}/authorizationrules/{key name}`.</span><span class="sxs-lookup"><span data-stu-id="5e690-177">hello service bus rule ID is a string with this format: `{Service Bus resource ID}/authorizationrules/{key name}`.</span></span>

<span data-ttu-id="5e690-178">Enviar tooenable da área de trabalho do Log Analytics do tooa de registos de diagnóstico, utilize este comando:</span><span class="sxs-lookup"><span data-stu-id="5e690-178">tooenable sending of diagnostic logs tooa Log Analytics workspace, use this command:</span></span>

```azurecli
azure insights diagnostic set --resourceId <resourceId> --workspaceId <resource id of hello log analytics workspace> --enabled true
```

<span data-ttu-id="5e690-179">Pode combinar estas tooenable parâmetros várias opções de saída.</span><span class="sxs-lookup"><span data-stu-id="5e690-179">You can combine these parameters tooenable multiple output options.</span></span>

### <a name="enable-collection-of-resource-diagnostic-logs-via-rest-api"></a><span data-ttu-id="5e690-180">Ativar a recolha de registos de diagnóstico de recursos através de REST API</span><span class="sxs-lookup"><span data-stu-id="5e690-180">Enable collection of resource diagnostic logs via REST API</span></span>
<span data-ttu-id="5e690-181">definições de diagnóstico toochange utilizando Olá API de REST de Monitor do Azure, consulte [neste documento](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span><span class="sxs-lookup"><span data-stu-id="5e690-181">toochange diagnostic settings using hello Azure Monitor REST API, see [this document](https://msdn.microsoft.com/library/azure/dn931931.aspx).</span></span>

## <a name="manage-resource-diagnostic-settings-in-hello-portal"></a><span data-ttu-id="5e690-182">Gerir definições de diagnóstico de recursos no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="5e690-182">Manage resource diagnostic settings in hello portal</span></span>
<span data-ttu-id="5e690-183">Certifique-se de que todos os seus recursos estão configurados com definições de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5e690-183">Ensure that all of your resources are set up with diagnostic settings.</span></span> <span data-ttu-id="5e690-184">Navegue demasiado**Monitor** no Olá portal e abra **definições de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="5e690-184">Navigate too**Monitor** in hello portal and open **Diagnostic settings**.</span></span>

![Diagnóstico registos painel no portal de Olá](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-nav.png)

<span data-ttu-id="5e690-186">Poderá ter tooclick mais secção "serviços" toofind Olá Monitor.</span><span class="sxs-lookup"><span data-stu-id="5e690-186">You may have tooclick "More services" toofind hello Monitor section.</span></span>

<span data-ttu-id="5e690-187">Aqui pode ver e filtrar todos os recursos que suportam toosee de definições de diagnóstico, se tiver ativado o diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="5e690-187">Here you can view and filter all resources that support diagnostic settings toosee if they have diagnostics enabled.</span></span> <span data-ttu-id="5e690-188">Também pode desagregar toosee se várias definições estão definidas num recurso e verifique que a conta de armazenamento, o espaço de nomes de Event Hubs e/ou as área de trabalho de análise de registos que são enviados dados para.</span><span class="sxs-lookup"><span data-stu-id="5e690-188">You can also drill down toosee if multiple settings are set on a resource and check which storage account, Event Hubs namespace, and/or Log Analytics workspace that data are flowing to.</span></span>

![Resultados de registos de diagnóstico no portal](./media/monitoring-overview-of-diagnostic-logs/diagnostic-settings-blade.png)

<span data-ttu-id="5e690-190">Adicionar que uma definição de diagnóstico aparece Olá vista de definições de diagnóstico, onde pode ativar, desativar ou modificar as definições de diagnóstico para Olá selecionado recursos.</span><span class="sxs-lookup"><span data-stu-id="5e690-190">Adding a diagnostic setting brings up hello Diagnostic Settings view, where you can enable, disable, or modify your diagnostic settings for hello selected resource.</span></span>

## <a name="supported-services-categories-and-schemas-for-resource-diagnostic-logs"></a><span data-ttu-id="5e690-191">Serviços suportados, categorias e esquemas de registos de diagnóstico de recursos</span><span class="sxs-lookup"><span data-stu-id="5e690-191">Supported services, categories, and schemas for resource diagnostic logs</span></span>
<span data-ttu-id="5e690-192">[Consulte este artigo](monitoring-diagnostic-logs-schema.md) para uma lista completa dos serviços suportados e categorias de registo Olá e esquemas utilizadas por esses serviços.</span><span class="sxs-lookup"><span data-stu-id="5e690-192">[See this article](monitoring-diagnostic-logs-schema.md) for a complete list of supported services and hello log categories and schemas used by those services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5e690-193">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5e690-193">Next steps</span></span>

* [<span data-ttu-id="5e690-194">Os registos de diagnóstico de recursos de sequência demasiado**Event Hubs**</span><span class="sxs-lookup"><span data-stu-id="5e690-194">Stream resource diagnostic logs too**Event Hubs**</span></span>](monitoring-stream-diagnostic-logs-to-event-hubs.md)
* [<span data-ttu-id="5e690-195">Alterar definições de diagnóstico do recurso utilizando Olá API de REST de Monitor do Azure</span><span class="sxs-lookup"><span data-stu-id="5e690-195">Change resource diagnostic settings using hello Azure Monitor REST API</span></span>](https://msdn.microsoft.com/library/azure/dn931931.aspx)
* [<span data-ttu-id="5e690-196">Analisar os registos do armazenamento do Azure com a análise de registos</span><span class="sxs-lookup"><span data-stu-id="5e690-196">Analyze logs from Azure storage with Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
