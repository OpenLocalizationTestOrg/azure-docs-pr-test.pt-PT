---
title: aaaMonitor progresso da tarefa por contagem de tarefas por Estado - Azure Batch | Microsoft Docs
description: "Monitorizar o progresso de Olá de uma tarefa chamando a operação de obter a contagem de tarefas Olá toocount tarefas para uma tarefa. Pode obter uma contagem de tarefas do Active Directory, em execução e foi concluídas e, por tarefas que foi concluída com êxito ou falha."
services: batch
author: tamram
manager: timlt
ms.service: batch
ms.topic: article
ms.date: 08/02/2017
ms.author: tamram
ms.openlocfilehash: 03957d8a3d678bf44587f3bc7f988a76885c2af0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="count-tasks-by-state-toomonitor-a-jobs-progress-preview"></a>Contagem de tarefas por toomonitor de estado de progresso de uma tarefa (pré-visualização)

O Azure Batch fornece um forma eficiente toomonitor Olá progresso uma tarefa executa as respetivas tarefas. Pode chamar Olá [obter contagens de tarefa] [ rest_get_task_counts] operação toofind como muitas tarefas estão num Estado em execução, Active Directory ou foi concluído e tem quantos foi concluída com êxito ou falha. Por número de Olá das tarefas em cada Estado de contagem, mais facilmente pode apresentar o utilizador de tooa de progresso da tarefa de Olá ou detetar atrasos inesperados ou falhas que podem afetar a tarefa de Olá.

> [!IMPORTANT]
> Olá operação obter contagens de tarefa está atualmente em pré-visualização e ainda não está disponível no Azure Government, Azure China e Datacenters do Azure. 
>
>

## <a name="how-tasks-are-counted"></a>Como as tarefas são contadas

Olá obter contagens de tarefa operação contagens tarefas por Estado, da seguinte forma:

- Uma tarefa é contabilizada como **Active Directory** quando é toorun em fila e podem, mas não está atualmente atribuída nó de computação tooa. Uma tarefa também é contabilizada como **Active Directory** se está dependente de uma tarefa principal que ainda não foi concluído. Para obter mais informações sobre as dependências de tarefas, consulte [criar as dependências de tarefas toorun tarefas que dependem de outras tarefas](batch-task-dependencies.md). 
- Uma tarefa é contabilizada como **executar** quando este foi atribuído um nó de computação tooa, mas ainda não foi concluído. Uma tarefa é contabilizada como **executar** quando o estado é `preparing` ou `running`, conforme indicado pelo Olá [obter informações sobre uma tarefa] [ rest_get_task] operação.
- Uma tarefa é contabilizada como **concluída** quando já não está toorun elegível. Uma tarefa contabilizado como **concluída** tem normalmente concluída com êxito, ou foi concluída sem êxito e também esgotou o respetivo limite de repetição. 

Olá operação obter contagens de tarefas relatórios também como muitas tarefas tem êxito ou falhou. Batch determina se uma tarefa teve êxito ou falha ao verificar Olá **resultado** propriedade Olá [executionInfo] [https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task#executionInfo] propriedade:

    - Uma tarefa é contabilizada como **foi concluída com êxito** se Olá resultado da execução da tarefa é `success`.
    - Uma tarefa é contabilizada como **falha** se Olá resultado da execução da tarefa é `failure`.

Para mais informações sobre os Estados de tarefas, consulte [obter informações sobre uma tarefa][rest_get_task].

Olá .NET código exemplo seguinte mostra como tarefa tooretrieve contagens por Estado: 

```csharp
var taskCounts = await batchClient.JobOperations.GetTaskCountsAsync("job-1");

Console.WriteLine("Task count in active state: {0}", taskCounts.Active);
Console.WriteLine("Task count in preparing or running state: {0}", taskCounts.Running);
Console.WriteLine("Task count in completed state: {0}", taskCounts.Completed);
Console.WriteLine("Succeeded task count: {0}", taskCounts.Succeeded);
Console.WriteLine("Failed task count: {0}", taskCounts.Failed);
Console.WriteLine("ValidationStatus: {0}", taskCounts.ValidationStatus);
```

> [!NOTE]
> Pode utilizar um padrão semelhante para REST e outras linguagens tooget tarefas contagem de uma tarefa. 
> 
> 

## <a name="consistency-checking-for-task-counts"></a>Verificação de contagens de tarefa de consistência

serviço de Batch de Olá agrega contagens de tarefa por a recolha de dados de várias partes de um sistema distribuída assíncrona. tooensure contagens de tarefas estão corretos, o Batch fornece validação adicional para contagens de estado, efetuando as verificações de consistência contra vários componentes do sistema de Olá. Batch executa estas verificações de consistência, desde que existem menos de 200 000 tarefas na tarefa de Olá. No Olá improvável eventualidade que a verificação de consistência Olá encontra erros, o Batch corrige resultado de Olá da operação de obter a contagem de tarefas de Olá com base nos resultados de Olá de verificação de consistência Olá. Olá verificação de consistência é uma tooensure medidas adicionais que os clientes que dependem de Olá operação obter contagens de tarefa obter informações corretas Olá que necessitam para a solução.

Olá **validationStatus** propriedade na resposta Olá indica se o Batch tem efetuar verificação de consistência Olá. Se o lote não foi possível toocheck Estado contagens contra Estados real Olá contidos num sistema Olá, em seguida, Olá **validationStatus** for definida demasiado`unvalidated`. Por motivos de desempenho, Batch não irá efetuar verificação de consistência Olá se Olá trabalho inclui mais de 200 000 tarefas, por isso, Olá **validationStatus** propriedade pode ser definida demasiado`unvalidated` neste caso. No entanto, contagem de tarefas Olá não é necessariamente errada neste caso, dado que, mesmo a perda de dados muito limitado é muito pouco provável. 

Quando uma tarefa muda de estado, o pipeline de agregação de Olá processa Olá alteração dentro de alguns segundos. Olá obter contagens de tarefa operação reflete contagens de tarefa Olá atualizado durante esse período. No entanto, se o pipeline de agregação de Olá pedidos sem êxito uma alteração de estado de tarefas, em seguida, que a alteração não é registado até a passagem de validação seguinte Olá. Durante este período, contagens de tarefas podem ser ligeiramente incorretas devido toohello de evento em falta, mas estes são corrigidas na passagem de validação seguinte Olá.

## <a name="best-practices-for-counting-a-jobs-tasks"></a>Melhores práticas para tarefas do trabalho de contagem

Chamar a operação de obter a contagem de tarefas Olá é Olá tooreturn da forma mais eficiente uma contagem das tarefas de uma tarefa pelo Estado básica. Se estiver a utilizar versão de serviço de Batch de 2017-06-01.5.1, recomendamos que escrever ou atualizar a sua toouse código obter contagens de tarefas.

Olá obter contagens de tarefa operação anterior ao 2017-06-01.5.1 não está disponível nas versões do serviço de Batch. Se estiver a utilizar uma versão antiga do serviço de Olá, em seguida, utilize uma lista consulta toocount tarefas numa tarefa em vez disso. Para obter mais informações, consulte [criar eficazmente os recursos do Batch toolist consultas](batch-efficient-list-queries.md).

## <a name="next-steps"></a>Passos seguintes

* Consulte Olá [descrição geral da funcionalidade do Batch](batch-api-basics.md) toolearn mais sobre as funcionalidades e conceitos do serviço Batch. Olá artigo aborda Olá recursos do Batch principais como conjuntos, nós de computação, trabalhos e tarefas e fornece uma descrição geral das funcionalidades do serviço de Olá.
* Saiba Olá Noções básicas sobre desenvolver uma aplicação preparada para Batch utilizando Olá [biblioteca de cliente .NET do Batch](batch-dotnet-get-started.md) ou [Python](batch-python-tutorial.md). Estes artigos introdutórias ajudá-lo através de uma aplicação de trabalho que utiliza tooexecute de serviço de Batch de Olá uma carga de trabalho em vários nós de computação.


[rest_get_task_counts]: https://docs.microsoft.com/rest/api/batchservice/get-the-task-counts-for-a-job
[rest_get_task]: https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task
[rest_list_tasks]: https://docs.microsoft.com/rest/api/batchservice/list-the-tasks-associated-with-a-job
