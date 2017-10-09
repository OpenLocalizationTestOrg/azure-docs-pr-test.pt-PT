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
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Eventos de registo para a avaliação de diagnóstico e monitorização de soluções do Batch

Tal como acontece com vários serviços do Azure, Olá serviço Batch emite eventos de registo para determinados recursos durante Olá duração do recurso de Olá. Pode ativar a eventos de toorecord de registos de diagnóstico do Azure Batch para recursos como conjuntos e tarefas e, em seguida, utilizar registos de Olá para avaliação de diagnóstico e monitorização. Eventos como agrupamento de criar, eliminar agrupamento, início da tarefa, tarefa concluída e outros estão incluídos nos registos de diagnóstico do Batch.

> [!NOTE]
> Este artigo aborda os eventos de registo de recursos de conta do Batch próprios, não da tarefa e dados de saída de tarefas. Para obter detalhes sobre o armazenamento de dados de saída de Olá dos seus trabalhos e tarefas, consulte [saída de tarefas e manter o Azure Batch](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* [Conta de Batch do Azure](batch-account-create-portal.md)
* [Conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  registos de diagnóstico do toopersist Batch, tem de criar uma conta de armazenamento do Azure onde o Azure irá armazenar Olá registos. Especificar esta conta de armazenamento quando que [ativar o registo de diagnóstico](#enable-diagnostic-logging) para a sua conta do Batch. Olá, especificar quando ativar a recolha de registos de conta de armazenamento é não Olá mesmo como um Olá de tooin referidos de conta do storage ligadas [pacotes de aplicações](batch-application-packages.md) e [persistência de saída de tarefas](batch-task-output.md) artigos.
  
  > [!WARNING]
  > É **cobrados** para dados de Olá armazenados na sua conta do Storage do Azure. Isto inclui os registos de diagnóstico Olá abordados neste artigo. Manter isto em consideração quando conceber a sua [política de retenção de registo](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Ativar o registo de diagnósticos
Registo de diagnóstico não está ativado por predefinição para a sua conta do Batch. Tem de ativar explicitamente o registo de diagnóstico para cada conta do Batch que pretende toomonitor:

[Como tooenable coleção de registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

Recomendamos que leia Olá completa [descrição geral do Azure os registos de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo toogain uma compreensão dos não apenas como tooenable registo, mas Olá iniciar categorias suportado pelo Olá vários serviços do Azure. Por exemplo, do Azure Batch atualmente suporta uma categoria de registo: **registos do serviço**.

## <a name="service-logs"></a>Registos do serviço
Os registos de serviço do Azure Batch contém eventos emitidos pelo serviço do Azure Batch Olá durante a duração de Olá de um recurso de Batch, como um conjunto ou tarefas. Cada evento emitido pelo Batch é armazenado no Olá especificada conta de armazenamento no formato JSON. Por exemplo, este é o corpo de Olá de uma amostra **conjunto criar eventos**:

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

Cada corpo de evento reside num. JSON ficheiro Olá especificar conta de armazenamento do Azure. Se quiser tooaccess Olá registos diretamente, pode ser útil tooreview Olá [esquema de registos de diagnóstico na conta do storage Olá](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Eventos de registo do serviço
Olá serviço Batch atualmente emite Olá seguintes eventos de registo do serviço. Esta lista não pode ser exaustiva, uma vez que os eventos adicionais poderão ter sido adicionados uma vez que este artigo foi atualizado pela última vez.

| **Eventos de registo do serviço** |
| --- |
| [Criar conjunto][pool_create] |
| [Início de eliminação do conjunto][pool_delete_start] |
| [Eliminar conjunto concluída][pool_delete_complete] |
| [Início de redimensionamento de conjunto][pool_resize_start] |
| [Redimensionamento de agrupamento completo][pool_resize_complete] |
| [Início da tarefa][task_start] |
| [Tarefa concluída][task_complete] |
| [Falha de tarefa][task_fail] |

## <a name="next-steps"></a>Passos seguintes
Nos eventos de registo de diagnóstico do toostoring adição numa conta do Storage do Azure, também pode transmitir tooan de eventos de registo do serviço Batch [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e enviá-las demasiado[Log Analytics do Azure](../log-analytics/log-analytics-overview.md).

* [Transmitir os registos de diagnóstico do Azure tooEvent Hubs](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Transmitir o serviço de entrada de dados altamente dimensionável de toohello de eventos de diagnóstico Batch, os Event Hubs. Hubs de eventos podem ingerir milhões de eventos por segundo, que pode, em seguida, transformar e armazenar utilizando um fornecedor de análise em tempo real.
* [Analisar os registos de diagnóstico do Azure através da análise do registo](../log-analytics/log-analytics-azure-storage.md)
  
  Envie o tooLog de registos de diagnóstico análise onde pode analisá-las no portal do Operations Management Suite (OMS) de Olá ou exportá-las para análise no Power BI ou no Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
