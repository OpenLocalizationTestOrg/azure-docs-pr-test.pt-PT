---
title: "aaaScheduler referência de Cmdlets do PowerShell"
description: "Referência de Cmdlets do PowerShell do agendador"
services: scheduler
documentationcenter: .NET
author: derek1ee
manager: kevinlam1
editor: 
ms.assetid: 9a26c457-d7a1-4e4a-bc79-f26592155218
ms.service: scheduler
ms.workload: infrastructure-services
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 08/18/2016
ms.author: deli
ms.openlocfilehash: a2b23bcd3e4493ffba1dbf21fbb87818be7c01e5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scheduler-powershell-cmdlets-reference"></a><span data-ttu-id="e2382-103">Referência de Cmdlets do PowerShell do agendador</span><span class="sxs-lookup"><span data-stu-id="e2382-103">Scheduler PowerShell Cmdlets Reference</span></span>
<span data-ttu-id="e2382-104">Olá, a tabela seguinte descreve e liga toohello página de referência de cada um dos cmdlets principais do Olá no agendador do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2382-104">hello following table describes and links toohello reference page of each of hello major cmdlets in Azure Scheduler.</span></span>

<span data-ttu-id="e2382-105">tooinstall Azure PowerShell e associá-lo à sua subscrição do Azure, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e2382-105">tooinstall Azure PowerShell and associate it with your Azure subscription, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span> 

<span data-ttu-id="e2382-106">Para obter mais informações sobre [cmdlets do Azure Resource Manager](/powershell/azure/overview), consulte [utilizar o Azure PowerShell com o Azure Resource Manager](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="e2382-106">For more information about [Azure Resource Manager cmdlets](/powershell/azure/overview), see [Using Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>

| <span data-ttu-id="e2382-107">Cmdlet</span><span class="sxs-lookup"><span data-stu-id="e2382-107">Cmdlet</span></span> | <span data-ttu-id="e2382-108">Descrição do cmdlet</span><span class="sxs-lookup"><span data-stu-id="e2382-108">Cmdlet Description</span></span> |
| --- | --- |
| [<span data-ttu-id="e2382-109">Desativar AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-109">Disable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/disable-azurermschedulerjobcollection) |<span data-ttu-id="e2382-110">Desativa uma coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2382-110">Disables a job collection.</span></span> |
| [<span data-ttu-id="e2382-111">Ativar AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-111">Enable-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/enable-azurermschedulerjobcollection) |<span data-ttu-id="e2382-112">Permite a uma coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2382-112">Enables a job collection.</span></span> |
| [<span data-ttu-id="e2382-113">Get-AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="e2382-113">Get-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjob) |<span data-ttu-id="e2382-114">Obtém as tarefas do programador.</span><span class="sxs-lookup"><span data-stu-id="e2382-114">Gets Scheduler jobs.</span></span> |
| [<span data-ttu-id="e2382-115">Get-AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-115">Get-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobcollection) |<span data-ttu-id="e2382-116">Obtém as coleções de tarefa.</span><span class="sxs-lookup"><span data-stu-id="e2382-116">Gets job collections.</span></span> |
| [<span data-ttu-id="e2382-117">Get-AzureRmSchedulerJobHistory</span><span class="sxs-lookup"><span data-stu-id="e2382-117">Get-AzureRmSchedulerJobHistory</span></span>](/powershell/module/azurerm.scheduler/get-azurermschedulerjobhistory) |<span data-ttu-id="e2382-118">Obtém o histórico de tarefa.</span><span class="sxs-lookup"><span data-stu-id="e2382-118">Gets job history.</span></span> |
| [<span data-ttu-id="e2382-119">Novo AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="e2382-119">New-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerhttpjob) |<span data-ttu-id="e2382-120">Cria uma tarefa HTTP.</span><span class="sxs-lookup"><span data-stu-id="e2382-120">Creates an HTTP job.</span></span> |
| [<span data-ttu-id="e2382-121">Novo AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-121">New-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerjobcollection) |<span data-ttu-id="e2382-122">Cria uma coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2382-122">Creates a job collection.</span></span> |
| [<span data-ttu-id="e2382-123">Novo AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="e2382-123">New-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebusqueuejob) |<span data-ttu-id="e2382-124">Cria uma tarefa de fila de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2382-124">Creates a service bus queue job.</span></span> |
| [<span data-ttu-id="e2382-125">Novo AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="e2382-125">New-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerservicebustopicjob) |<span data-ttu-id="e2382-126">Cria uma tarefa de tópico de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2382-126">Creates a service bus topic job.</span></span> |
| [<span data-ttu-id="e2382-127">Novo AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="e2382-127">New-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/new-azurermschedulerstoragequeuejob) |<span data-ttu-id="e2382-128">Cria uma tarefa de fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2382-128">Creates a storage queue job.</span></span> |
| [<span data-ttu-id="e2382-129">Remover AzureRmSchedulerJob</span><span class="sxs-lookup"><span data-stu-id="e2382-129">Remove-AzureRmSchedulerJob</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjob) |<span data-ttu-id="e2382-130">Remove uma tarefa do agendador.</span><span class="sxs-lookup"><span data-stu-id="e2382-130">Removes a Scheduler job.</span></span> |
| [<span data-ttu-id="e2382-131">Remover AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-131">Remove-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/remove-azurermschedulerjobcollection) |<span data-ttu-id="e2382-132">Remove uma coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2382-132">Removes a job collection.</span></span> |
| [<span data-ttu-id="e2382-133">Conjunto AzureRmSchedulerHttpJob</span><span class="sxs-lookup"><span data-stu-id="e2382-133">Set-AzureRmSchedulerHttpJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerhttpjob) |<span data-ttu-id="e2382-134">Modifica uma tarefa do agendador HTTP.</span><span class="sxs-lookup"><span data-stu-id="e2382-134">Modifies a Scheduler HTTP job.</span></span> |
| [<span data-ttu-id="e2382-135">Conjunto AzureRmSchedulerJobCollection</span><span class="sxs-lookup"><span data-stu-id="e2382-135">Set-AzureRmSchedulerJobCollection</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerjobcollection) |<span data-ttu-id="e2382-136">Modifica uma coleção de tarefas.</span><span class="sxs-lookup"><span data-stu-id="e2382-136">Modifies a job collection.</span></span> |
| [<span data-ttu-id="e2382-137">Conjunto AzureRmSchedulerServiceBusQueueJob</span><span class="sxs-lookup"><span data-stu-id="e2382-137">Set-AzureRmSchedulerServiceBusQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebusqueuejob) |<span data-ttu-id="e2382-138">Modifica uma tarefa de fila de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2382-138">Modifies a service bus queue job.</span></span> |
| [<span data-ttu-id="e2382-139">Conjunto AzureRmSchedulerServiceBusTopicJob</span><span class="sxs-lookup"><span data-stu-id="e2382-139">Set-AzureRmSchedulerServiceBusTopicJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerservicebustopicjob) |<span data-ttu-id="e2382-140">Modifica uma tarefa de tópico de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="e2382-140">Modifies a service bus topic job.</span></span> |
| [<span data-ttu-id="e2382-141">Conjunto AzureRmSchedulerStorageQueueJob</span><span class="sxs-lookup"><span data-stu-id="e2382-141">Set-AzureRmSchedulerStorageQueueJob</span></span>](/powershell/module/azurerm.scheduler/set-azurermschedulerstoragequeuejob) |<span data-ttu-id="e2382-142">Modifica uma tarefa de fila de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e2382-142">Modifies a storage queue job.</span></span> |

<span data-ttu-id="e2382-143">Para obter informações mais detalhadas, pode executar qualquer uma das Olá os seguintes cmdlets:</span><span class="sxs-lookup"><span data-stu-id="e2382-143">For more detailed information, you can run any of hello following cmdlets:</span></span> 

```
Get-Help <cmdlet name> -Detailed
```
```
Get-Help <cmdlet name> -Examples
```
```
Get-Help <cmdlet name> -Full
```

## <a name="see-also"></a><span data-ttu-id="e2382-144">Veja Também</span><span class="sxs-lookup"><span data-stu-id="e2382-144">See Also</span></span>
 [<span data-ttu-id="e2382-145">O que é o Scheduler?</span><span class="sxs-lookup"><span data-stu-id="e2382-145">What is Scheduler?</span></span>](scheduler-intro.md)

 [<span data-ttu-id="e2382-146">Conceitos, terminologia e hierarquia de entidades do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-146">Azure Scheduler concepts, terminology, and entity hierarchy</span></span>](scheduler-concepts-terms.md)

 [<span data-ttu-id="e2382-147">Começar a utilizar o agendador no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="e2382-147">Get started using Scheduler in hello Azure portal</span></span>](scheduler-get-started-portal.md)

 [<span data-ttu-id="e2382-148">Planos e faturação no Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-148">Plans and billing in Azure Scheduler</span></span>](scheduler-plans-billing.md)

 [<span data-ttu-id="e2382-149">Referência da API REST do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-149">Azure Scheduler REST API reference</span></span>](https://msdn.microsoft.com/library/mt629143)

 [<span data-ttu-id="e2382-150">Elevada disponibilidade e fiabilidade do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-150">Azure Scheduler high-availability and reliability</span></span>](scheduler-high-availability-reliability.md)

 [<span data-ttu-id="e2382-151">Limites, predefinições e códigos de erro do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-151">Azure Scheduler limits, defaults, and error codes</span></span>](scheduler-limits-defaults-errors.md)

 [<span data-ttu-id="e2382-152">Autenticação de saída do Azure Scheduler</span><span class="sxs-lookup"><span data-stu-id="e2382-152">Azure Scheduler outbound authentication</span></span>](scheduler-outbound-authentication.md)

