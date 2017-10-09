---
title: "diagnóstico de registo de eventos de lote - Azure aaaEnable | Microsoft Docs"
description: "Registar e analisar eventos de registo de diagnóstico para recursos da conta do Azure Batch, como conjuntos e tarefas."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a><span data-ttu-id="64f4f-103">Eventos de registo para a avaliação de diagnóstico e monitorização de soluções do Batch</span><span class="sxs-lookup"><span data-stu-id="64f4f-103">Log events for diagnostic evaluation and monitoring of Batch solutions</span></span>

<span data-ttu-id="64f4f-104">Tal como acontece com vários serviços do Azure, Olá serviço Batch emite eventos de registo para determinados recursos durante Olá duração do recurso de Olá.</span><span class="sxs-lookup"><span data-stu-id="64f4f-104">As with many Azure services, hello Batch service emits log events for certain resources during hello lifetime of hello resource.</span></span> <span data-ttu-id="64f4f-105">Pode ativar a eventos de toorecord de registos de diagnóstico do Azure Batch para recursos como conjuntos e tarefas e, em seguida, utilizar registos de Olá para avaliação de diagnóstico e monitorização.</span><span class="sxs-lookup"><span data-stu-id="64f4f-105">You can enable Azure Batch diagnostic logs toorecord events for resources like pools and tasks, and then use hello logs for diagnostic evaluation and monitoring.</span></span> <span data-ttu-id="64f4f-106">Eventos como agrupamento de criar, eliminar agrupamento, início da tarefa, tarefa concluída e outros estão incluídos nos registos de diagnóstico do Batch.</span><span class="sxs-lookup"><span data-stu-id="64f4f-106">Events like pool create, pool delete, task start, task complete, and others are included in Batch diagnostic logs.</span></span>

> [!NOTE]
> <span data-ttu-id="64f4f-107">Este artigo aborda os eventos de registo de recursos de conta do Batch próprios, não da tarefa e dados de saída de tarefas.</span><span class="sxs-lookup"><span data-stu-id="64f4f-107">This article discusses logging events for Batch account resources themselves, not job and task output data.</span></span> <span data-ttu-id="64f4f-108">Para obter detalhes sobre o armazenamento de dados de saída de Olá dos seus trabalhos e tarefas, consulte [saída de tarefas e manter o Azure Batch](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="64f4f-108">For details on storing hello output data of your jobs and tasks, see [Persist Azure Batch job and task output](batch-task-output.md).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="64f4f-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="64f4f-109">Prerequisites</span></span>
* [<span data-ttu-id="64f4f-110">Conta de Batch do Azure</span><span class="sxs-lookup"><span data-stu-id="64f4f-110">Azure Batch account</span></span>](batch-account-create-portal.md)
* [<span data-ttu-id="64f4f-111">Conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="64f4f-111">Azure Storage account</span></span>](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  <span data-ttu-id="64f4f-112">registos de diagnóstico do toopersist Batch, tem de criar uma conta de armazenamento do Azure onde o Azure irá armazenar Olá registos.</span><span class="sxs-lookup"><span data-stu-id="64f4f-112">toopersist Batch diagnostic logs, you must create an Azure Storage account where Azure will store hello logs.</span></span> <span data-ttu-id="64f4f-113">Especificar esta conta de armazenamento quando que [ativar o registo de diagnóstico](#enable-diagnostic-logging) para a sua conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="64f4f-113">You specify this Storage account when you [enable diagnostic logging](#enable-diagnostic-logging) for your Batch account.</span></span> <span data-ttu-id="64f4f-114">Olá, especificar quando ativar a recolha de registos de conta de armazenamento é não Olá mesmo como um Olá de tooin referidos de conta do storage ligadas [pacotes de aplicações](batch-application-packages.md) e [persistência de saída de tarefas](batch-task-output.md) artigos.</span><span class="sxs-lookup"><span data-stu-id="64f4f-114">hello Storage account you specify when you enable log collection is not hello same as a linked storage account referred tooin hello [application packages](batch-application-packages.md) and [task output persistence](batch-task-output.md) articles.</span></span>
  
  > [!WARNING]
  > <span data-ttu-id="64f4f-115">É **cobrados** para dados de Olá armazenados na sua conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="64f4f-115">You are **charged** for hello data stored in your Azure Storage account.</span></span> <span data-ttu-id="64f4f-116">Isto inclui os registos de diagnóstico Olá abordados neste artigo.</span><span class="sxs-lookup"><span data-stu-id="64f4f-116">This includes hello diagnostic logs discussed in this article.</span></span> <span data-ttu-id="64f4f-117">Manter isto em consideração quando conceber a sua [política de retenção de registo](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span><span class="sxs-lookup"><span data-stu-id="64f4f-117">Keep this in mind when designing your [log retention policy](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).</span></span>
  > 
  > 

## <a name="enable-diagnostic-logging"></a><span data-ttu-id="64f4f-118">Ativar o registo de diagnósticos</span><span class="sxs-lookup"><span data-stu-id="64f4f-118">Enable diagnostic logging</span></span>
<span data-ttu-id="64f4f-119">Registo de diagnóstico não está ativado por predefinição para a sua conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="64f4f-119">Diagnostic logging is not enabled by default for your Batch account.</span></span> <span data-ttu-id="64f4f-120">Tem de ativar explicitamente o registo de diagnóstico para cada conta do Batch que pretende toomonitor:</span><span class="sxs-lookup"><span data-stu-id="64f4f-120">You must explicitly enable diagnostic logging for each Batch account you want toomonitor:</span></span>

[<span data-ttu-id="64f4f-121">Como tooenable coleção de registos de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="64f4f-121">How tooenable collection of Diagnostic Logs</span></span>](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

<span data-ttu-id="64f4f-122">Recomendamos que leia Olá completa [descrição geral do Azure os registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo toogain uma compreensão dos não apenas como tooenable registo, mas Olá iniciar categorias suportado pelo Olá vários serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="64f4f-122">We recommend that you read hello full [Overview of Azure Diagnostic Logs](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) article toogain an understanding of not only how tooenable logging, but hello log categories supported by hello various Azure services.</span></span> <span data-ttu-id="64f4f-123">Por exemplo, do Azure Batch atualmente suporta uma categoria de registo: **registos do serviço**.</span><span class="sxs-lookup"><span data-stu-id="64f4f-123">For example, Azure Batch currently supports one log category: **Service Logs**.</span></span>

## <a name="service-logs"></a><span data-ttu-id="64f4f-124">Registos do serviço</span><span class="sxs-lookup"><span data-stu-id="64f4f-124">Service Logs</span></span>
<span data-ttu-id="64f4f-125">Os registos de serviço do Azure Batch contém eventos emitidos pelo serviço do Azure Batch Olá durante a duração de Olá de um recurso de Batch, como um conjunto ou tarefas.</span><span class="sxs-lookup"><span data-stu-id="64f4f-125">Azure Batch Service Logs contain events emitted by hello Azure Batch service during hello lifetime of a Batch resource like a pool or task.</span></span> <span data-ttu-id="64f4f-126">Cada evento emitido pelo Batch é armazenado no Olá especificada conta de armazenamento no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="64f4f-126">Each event emitted by Batch is stored in hello specified Storage account in JSON format.</span></span> <span data-ttu-id="64f4f-127">Por exemplo, este é o corpo de Olá de uma amostra **conjunto criar eventos**:</span><span class="sxs-lookup"><span data-stu-id="64f4f-127">For example, this is hello body of a sample **pool create event**:</span></span>

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

<span data-ttu-id="64f4f-128">Cada corpo de evento reside num. JSON ficheiro Olá especificar conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="64f4f-128">Each event body resides in a .json file in hello specified Azure Storage account.</span></span> <span data-ttu-id="64f4f-129">Se quiser tooaccess Olá registos diretamente, pode ser útil tooreview Olá [esquema de registos de diagnóstico na conta do storage Olá](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span><span class="sxs-lookup"><span data-stu-id="64f4f-129">If you want tooaccess hello logs directly, you may wish tooreview hello [schema of Diagnostic Logs in hello storage account](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).</span></span>

## <a name="service-log-events"></a><span data-ttu-id="64f4f-130">Eventos de registo do serviço</span><span class="sxs-lookup"><span data-stu-id="64f4f-130">Service Log events</span></span>
<span data-ttu-id="64f4f-131">Olá serviço Batch atualmente emite Olá seguintes eventos de registo do serviço.</span><span class="sxs-lookup"><span data-stu-id="64f4f-131">hello Batch service currently emits hello following Service Log events.</span></span> <span data-ttu-id="64f4f-132">Esta lista não pode ser exaustiva, uma vez que os eventos adicionais poderão ter sido adicionados uma vez que este artigo foi atualizado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="64f4f-132">This list may not be exhaustive, since additional events may have been added since this article was last updated.</span></span>

| <span data-ttu-id="64f4f-133">**Eventos de registo do serviço**</span><span class="sxs-lookup"><span data-stu-id="64f4f-133">**Service Log events**</span></span> |
| --- |
| <span data-ttu-id="64f4f-134">[Criar conjunto][pool_create]</span><span class="sxs-lookup"><span data-stu-id="64f4f-134">[Pool create][pool_create]</span></span> |
| <span data-ttu-id="64f4f-135">[Início de eliminação do conjunto][pool_delete_start]</span><span class="sxs-lookup"><span data-stu-id="64f4f-135">[Pool delete start][pool_delete_start]</span></span> |
| <span data-ttu-id="64f4f-136">[Eliminar conjunto concluída][pool_delete_complete]</span><span class="sxs-lookup"><span data-stu-id="64f4f-136">[Pool delete complete][pool_delete_complete]</span></span> |
| <span data-ttu-id="64f4f-137">[Início de redimensionamento de conjunto][pool_resize_start]</span><span class="sxs-lookup"><span data-stu-id="64f4f-137">[Pool resize start][pool_resize_start]</span></span> |
| <span data-ttu-id="64f4f-138">[Redimensionamento de agrupamento completo][pool_resize_complete]</span><span class="sxs-lookup"><span data-stu-id="64f4f-138">[Pool resize complete][pool_resize_complete]</span></span> |
| <span data-ttu-id="64f4f-139">[Início da tarefa][task_start]</span><span class="sxs-lookup"><span data-stu-id="64f4f-139">[Task start][task_start]</span></span> |
| <span data-ttu-id="64f4f-140">[Tarefa concluída][task_complete]</span><span class="sxs-lookup"><span data-stu-id="64f4f-140">[Task complete][task_complete]</span></span> |
| <span data-ttu-id="64f4f-141">[Falha de tarefa][task_fail]</span><span class="sxs-lookup"><span data-stu-id="64f4f-141">[Task fail][task_fail]</span></span> |

## <a name="next-steps"></a><span data-ttu-id="64f4f-142">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="64f4f-142">Next steps</span></span>
<span data-ttu-id="64f4f-143">Nos eventos de registo de diagnóstico do toostoring adição numa conta do Storage do Azure, também pode transmitir tooan de eventos de registo do serviço Batch [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e enviá-las demasiado[Log Analytics do Azure](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="64f4f-143">In addition toostoring diagnostic log events in an Azure Storage account, you can also stream Batch Service Log events tooan [Azure Event Hub](../event-hubs/event-hubs-what-is-event-hubs.md), and send them too[Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span>

* [<span data-ttu-id="64f4f-144">Transmitir os registos de diagnóstico do Azure tooEvent Hubs</span><span class="sxs-lookup"><span data-stu-id="64f4f-144">Stream Azure Diagnostic Logs tooEvent Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  <span data-ttu-id="64f4f-145">Transmitir o serviço de entrada de dados altamente dimensionável de toohello de eventos de diagnóstico Batch, os Event Hubs.</span><span class="sxs-lookup"><span data-stu-id="64f4f-145">Stream Batch diagnostic events toohello highly scalable data ingress service, Event Hubs.</span></span> <span data-ttu-id="64f4f-146">Hubs de eventos podem ingerir milhões de eventos por segundo, que pode, em seguida, transformar e armazenar utilizando um fornecedor de análise em tempo real.</span><span class="sxs-lookup"><span data-stu-id="64f4f-146">Event Hubs can ingest millions of events per second, which you can then transform and store using any real-time analytics provider.</span></span>
* [<span data-ttu-id="64f4f-147">Analisar os registos de diagnóstico do Azure através da análise do registo</span><span class="sxs-lookup"><span data-stu-id="64f4f-147">Analyze Azure diagnostic logs using Log Analytics</span></span>](../log-analytics/log-analytics-azure-storage.md)
  
  <span data-ttu-id="64f4f-148">Envie o tooLog de registos de diagnóstico análise onde pode analisá-las no portal do Operations Management Suite (OMS) de Olá ou exportá-las para análise no Power BI ou no Excel.</span><span class="sxs-lookup"><span data-stu-id="64f4f-148">Send your diagnostic logs tooLog Analytics where you can analyze them in hello Operations Management Suite (OMS) portal, or export them for analysis in Power BI or Excel.</span></span>

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
