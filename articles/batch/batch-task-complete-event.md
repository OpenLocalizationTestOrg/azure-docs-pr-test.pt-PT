---
title: "AAA \"eventos de conclusão de tarefas do Azure Batch | Microsoft Docs\""
description: "Referência para o evento de conclusão de tarefas do Batch."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: c126bf897071c008be3d24190cf77bba5878b807
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="task-complete-event"></a>Evento de tarefa concluído

 Este evento é emitido depois de uma tarefa é concluída, independentemente do código de saída Olá. Este evento pode ser utilizado toodetermine Olá duração de uma tarefa, onde o Olá tarefa foi executada e se foi repetida.


 Olá exemplo seguinte mostra corpo Olá de um evento de conclusão de tarefas.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "startTime": "2016-09-08T16:32:23.799Z",
        "endTime": "2016-09-08T16:34:00.666Z",
        "exitCode": 0,
        "retryCount": 0,
        "requeueCount": 0
    }
}
```

|Nome do elemento|Tipo|Notas|
|------------------|----------|-----------|
|JobId|Cadeia|id de Olá da tarefa de Olá que contém a tarefa de Olá.|
|ID|Cadeia|id da tarefa de Olá Olá.|
|taskType|Cadeia|tipo de Olá de tarefa de Olá. Isto pode ser 'JobManager', indicando que é uma tarefa de gestão ou 'User', que indica que não se trata de uma tarefa de gestão. Este evento não é emitido para tarefas de preparação, tarefas de lançamento ou tarefas de início.|
|systemTaskVersion|Int32|Este é o contador de repetições interno de Olá uma tarefa. Internamente o serviço de Batch de Olá pode repetir tooaccount uma tarefa para problemas transitórios. Estes problemas podem incluir interno agendamento erros ou tentativas toorecover de nós de computação num Estado incorreto.|
|[nodeInfo](#nodeInfo)|Tipo complexo|Contém informações sobre o nó de computação de Olá no qual Olá a tarefa foi executada.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complexo|Especifica a que tarefa Olá é uma tarefa de várias instâncias que necessitam de vários nós de computação.  Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para obter mais detalhes.|
|[restrições](#constraints)|Tipo complexo|restrições de execução de Olá que se aplicam toothis tarefas.|
|[executionInfo](#executionInfo)|Tipo complexo|Contém informações sobre a execução de Olá da tarefa de Olá.|

###  <a name="nodeInfo"></a>nodeInfo

|Nome do elemento|Tipo|Notas|
|------------------|----------|-----------|
|poolId|Cadeia|Olá id do conjunto de Olá no qual Olá a tarefa foi executada.|
|nodeId|Cadeia|id de Olá do nó de Olá no qual Olá a tarefa foi executada.|

###  <a name="multiInstanceSettings"></a>multiInstanceSettings

|Nome do elemento|Tipo|Notas|
|------------------|----------|-----------|
|numberOfInstances|Int32|número de Olá de nós de computação necessária para a tarefa de Olá.|

###  <a name="constraints"></a>restrições

|Nome do elemento|Tipo|Notas|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Olá número máximo de vezes que uma tarefa de Olá pode ser repetida. Olá serviço Batch repete uma tarefa se o código de saída é diferente de zero.<br /><br /> Tenha em atenção que este valor controla especificamente número Olá de tentativas. serviço de Batch de Olá tentará tarefas Olá uma vez e, em seguida, pode voltar a tentar configurar toothis limite. Por exemplo, se a contagem de repetições máxima Olá é 3, o Batch tenta uma tarefa de cópia de segurança too4 horas (um tente inicial e 3 tentativas).<br /><br /> Se Olá contagem de repetições máxima for 0, Olá serviço Batch não repete a ação tarefas.<br /><br /> Se a contagem de repetições máxima Olá for -1, o serviço de Batch de Olá repete tarefas sem limite.<br /><br /> valor predefinido de Olá é 0 (nenhum tentativas).|

###  <a name="executionInfo"></a>executionInfo

|Nome do elemento|Tipo|Notas|
|------------------|----------|-----------|
|startTime|DateTime|hora de Olá no qual tarefas Olá começou a ser executada. 'Executar' corresponde ao toohello **executar** Estado, pelo que o se a tarefa de Olá Especifica os ficheiros de recursos ou pacotes de aplicações, em seguida, a hora de início Olá reflete hora Olá que tarefas Olá iniciada transferir ou implementar estes.  Se a tarefa de Olá foi reiniciada ou repetida, este é Olá hora mais recente que tarefas Olá começou a ser executada.|
|endTime|DateTime|hora de Olá no qual tarefa Olá foi concluída.|
|exitCode|Int32|código de saída de Olá da tarefa de Olá.|
|retryCount|Int32|Olá, número de vezes que foram repetiu uma tarefa de Olá pelo serviço de Batch de Olá. tarefa de Olá é repetida se sai com um código de saída diferente de zero, cópia de segurança toohello especificado MaxTaskRetryCount.|
|requeueCount|Int32|Olá, número de vezes que a tarefa de Olá tem foi recolocado em fila pelo serviço de Batch de Olá como resultado de Olá de um pedido de utilizador.<br /><br /> Quando remove de utilizador de Olá nós a partir de um agrupamento (ao redimensionar ou reduzir o conjunto de Olá) ou quando a tarefa de Olá está a ser desativada, utilizador de Olá podem especificar que as tarefas em execução em nós de Olá ser colocadas em fila para execução. Esta contagem controla o número de vezes tarefas Olá foi recolocado em fila por estes motivos.|
