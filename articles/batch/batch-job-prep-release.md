---
title: "as tarefas aaaCreate tooprepare trabalhos e tarefas de conclua em nós de computação - Azure Batch | Microsoft Docs"
description: "Utilização ao nível da tarefa de preparação tarefas toominimize dados transferência nós de computação do Batch tooAzure e as tarefas de limpeza de nó após conclusão da tarefa de versão."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 63d9d4f1-8521-4bbb-b95a-c4cad73692d3
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 02/27/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fd5fb47ae6700281e63048c49a1241f4e935baba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a>Executar tarefa de preparação e tarefas de lançamento do batch nós de computação

 Uma tarefa de lote do Azure requer, muitas vezes, algum tipo de configuração antes das respetivas tarefas são executadas e manutenção de tarefa pós-cópia quando as tarefas estão concluídas. Poderá ter toodownload comuns tarefas dados de entrada tooyour nós de computação ou carregar tooAzure de dados de saída de tarefas armazenamento após a conclusão da tarefa de Olá. Pode utilizar **preparação da tarefa** e **lançamento da tarefa** tarefas tooperform estas operações.

## <a name="what-are-job-preparation-and-release-tasks"></a>O que são a tarefa de preparação e versão tarefas?
Antes de executam tarefas de um trabalho, é executada Olá tarefa de preparação da tarefa em todas as computação nós agendada toorun pelo menos uma tarefa. Depois de concluída a tarefa de Olá, Olá tarefa de lançamento da tarefa é executada em cada nó no conjunto de Olá que executou, pelo menos, uma tarefa. Tal como acontece com as tarefas de lote normal, pode especificar um toobe de linha de comandos invocada quando uma tarefa de preparação ou de lançamento da tarefa é executado.

Tarefas de preparação e de lançamento da tarefa oferecem funcionalidades de tarefa do Batch familiares como a transferência de ficheiro ([ficheiros de recursos][net_job_prep_resourcefiles]), elevados execução, variáveis de ambiente personalizadas, duração de execução máximo, contagem de repetições e tempo de retenção de ficheiros.

Olá secções a seguir, irá aprender como toouse Olá [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] localizadas classes na Olá [.NET do batch] [ api_net] biblioteca.

> [!TIP]
> Tarefas de preparação e de lançamento da tarefa são especialmente útil em ambientes do "agrupamento partilhado", em que um conjunto de nós de computação persistir entre execuções de tarefa e é utilizado por muitas tarefas.
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a>Quando toouse preparação da tarefa e tarefas da versão
Preparação de trabalho e tarefas de lançamento são uma boa opção para Olá seguintes situações:

**Transferência de dados de tarefas comuns**

Tarefas do batch, muitas vezes, necessitam de um conjunto de dados comum como entrada para tarefas do trabalho Olá. Por exemplo, nos cálculos de análise de risco diária, dados de mercado são tarefa específico, ainda comuns tooall de tarefas na tarefa de Olá. Estes dados de mercado, muitas vezes, vários gigabytes de tamanho, devem ser o nó de computação tooeach transferido apenas uma vez para que qualquer tarefa que é executado no nó de Olá pode utilizá-lo. Utilize um **tarefa de preparação** toodownload este nó de tooeach dados antes de execução de Olá da tarefa de Olá 's outras tarefas.

**Eliminar tarefas e saída**

Num ambiente "agrupamento partilhado", onde não são desativados entre trabalhos de nós de computação de um conjunto, poderá ter dados de tarefa toodelete entre é executado. Poderá ser necessário tooconserve espaço em disco em nós Olá ou satisfazer as políticas de segurança da sua organização. Utilize um **tarefa de libertação** toodelete dados que foi transferidos por uma tarefa de preparação ou gerados durante a execução da tarefa.

**Retenção do registo**

Pode querer tookeep uma cópia de ficheiros de registo que as suas tarefas geram ou talvez falhas ficheiros de informação que podem ser gerados pelas aplicações com falhas. Utilize um **tarefa de libertação** nessas toocompress casos e carregar este tooan dados [Storage do Azure] [ azure_storage] conta.

> [!TIP]
> Outra forma toopersist registos e outras tarefas e saída de dados são toouse Olá [convenções de ficheiro do Azure Batch](batch-task-output.md) biblioteca.
> 
> 

## <a name="job-preparation-task"></a>Tarefa de preparação
Antes da execução das tarefas de uma tarefa, o Batch executa Olá tarefa de preparação da tarefa em cada nó de computação que é toorun agendada uma tarefa. Por predefinição, Olá serviço Batch aguarda Olá tarefa preparação tarefas toobe concluída antes de executar Olá tarefas agendadas tooexecute no nó de Olá. No entanto, pode configurar o serviço de Olá toowait não. Se reiniciar o nó de Olá, Olá tarefa de preparação da tarefa é executada novamente, mas também pode desativar este comportamento.

tarefa de preparação Olá é executada apenas em nós que são toorun agendada uma tarefa. Isto impede que a execução de desnecessários Olá de uma tarefa de preparação, no caso de um nó não está atribuído uma tarefa. Isto pode ocorrer quando o número de Olá de tarefas para uma tarefa é inferior ao número de Olá de nós num conjunto. Também se aplica quando [a execução da tarefa em simultâneo](batch-parallel-node-tasks.md) estiver ativado, que deixa alguns nós inativo se a contagem de tarefas Olá é inferior ao tarefas simultâneas possíveis total Olá. Por não executar tarefa de preparação Olá em nós inativos, pode pode menos adiantar dinheiro com taxas aplicáveis às transferências de dados.

> [!NOTE]
> [JobPreparationTask] [ net_job_prep_cloudjob] difere [CloudPool.StartTask] [ pool_starttask] nessa JobPreparationTask executa no início de Olá de cada tarefa, enquanto que StartTask executa apenas quando um nó de computação primeiro associa um conjunto ou de reiniciar.
> 
> 

## <a name="job-release-task"></a>Tarefa de lançamento da tarefa
Depois de uma tarefa é marcada como concluído, Olá tarefa de lançamento da tarefa é executado em cada nó no conjunto de Olá que executou, pelo menos, uma tarefa. Marcar uma tarefa como concluído ao emitir um pedido de terminar. Olá serviço Batch, em seguida, define Olá estado de tarefa demasiado*terminar*, termina quaisquer tarefas em execução ou Active Directory associadas à tarefa Olá e executa a tarefa de libertação Olá. tarefa de Olá, em seguida, move toohello *concluída* estado.

> [!NOTE]
> Eliminação da tarefa também executa Olá tarefa de lançamento da tarefa. No entanto, se uma tarefa já foi terminada, Olá de lançamento da tarefa não é executado uma segunda vez se tarefa Olá for eliminada mais tarde.
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a>Tarefa de preparação e versão tarefas com .NET do Batch
toouse uma tarefa de preparação, atribuir um [JobPreparationTask] [ net_job_prep] da tarefa do objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriedade . Da mesma forma, inicializar um [JobReleaseTask] [ net_job_release] e atribua-a tarefa de tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] Olá tooset de propriedade tarefa de lançamento da tarefa.

Este fragmento de código, `myBatchClient` é uma instância de [BatchClient][net_batch_client], e `myPool` é um conjunto existente na Olá conta do Batch.

```csharp
// Create hello CloudJob for CloudPool "myPool"
CloudJob myJob =
    myBatchClient.JobOperations.CreateJob(
        "JobPrepReleaseSampleJob",
        new PoolInformation() { PoolId = "myPool" });

// Specify hello command lines for hello job preparation and release tasks
string jobPrepCmdLine =
    "cmd /c echo %AZ_BATCH_NODE_ID% > %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";
string jobReleaseCmdLine =
    "cmd /c del %AZ_BATCH_NODE_SHARED_DIR%\\shared_file.txt";

// Assign hello job preparation task toohello job
myJob.JobPreparationTask =
    new JobPreparationTask { CommandLine = jobPrepCmdLine };

// Assign hello job release task toohello job
myJob.JobReleaseTask =
    new JobPreparationTask { CommandLine = jobReleaseCmdLine };

await myJob.CommitAsync();
```

Conforme mencionado anteriormente, Olá de lançamento da tarefa é executado quando uma tarefa é terminada ou eliminada. Terminar uma tarefa com [joboperations. Terminatejobasync][net_job_terminate]. Eliminar uma tarefa com [JobOperations.DeleteJobAsync][net_job_delete]. Normalmente, terminar ou eliminar uma tarefa quando as tarefas estão concluídas, ou quando foi atingido o limite de tempo que definiu.

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a>Exemplo de código no GitHub
toosee preparação e de lançamento tarefas em ação, consulte Olá [JobPrepRelease] [ job_prep_release_sample] projeto de exemplo no GitHub. Esta aplicação de consola Olá seguintes:

1. Cria um conjunto com dois nós "pequenos".
2. Cria uma tarefa com a tarefa de preparação, versão e tarefas padrão.
3. Executa Olá tarefa de preparação, que escreve primeiro o ficheiro de texto de tooa de ID de nó de Olá no diretório de "partilhado" de um nó.
4. Executa uma tarefa em cada nó que escreve o respetivo toohello de ID de tarefa mesmo ficheiro de texto.
5. Depois de todas as tarefas são concluídas (ou for atingido o tempo limite de Olá), imprima conteúdo Olá da consola de toohello de ficheiro de texto de cada nó.
6. Quando a tarefa de Olá estiver concluída, é executado Olá tarefa versão tarefas toodelete Olá ficheiro a partir do nó de Olá.
7. Olá impressões sair códigos de tarefa de preparação de Olá e versão tarefas para cada nó no qual são executados.
8. Confirmação de tooallow de execução de coloca em pausa da tarefa e/ou conjunto de eliminação.

Resultado da aplicação de exemplo de Olá é semelhante toohello seguinte:

```
Attempting toocreate pool: JobPrepReleaseSamplePool
Created pool JobPrepReleaseSamplePool with 2 small nodes
Checking for existing job JobPrepReleaseSampleJob...
Job JobPrepReleaseSampleJob not found, creating...
Submitting tasks and awaiting completion...
All tasks completed.

Contents of shared\job_prep_and_release.txt on tvm-2434664350_1-20160623t173951z:
-------------------------------------------
tvm-2434664350_1-20160623t173951z tasks:
  task001
  task004
  task005
  task006

Contents of shared\job_prep_and_release.txt on tvm-2434664350_2-20160623t173951z:
-------------------------------------------
tvm-2434664350_2-20160623t173951z tasks:
  task008
  task002
  task003
  task007

Waiting for job JobPrepReleaseSampleJob tooreach state Completed
...

tvm-2434664350_1-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

tvm-2434664350_2-20160623t173951z:
  Prep task exit code:    0
  Release task exit code: 0

Delete job? [yes] no
yes
Delete pool? [yes] no
yes

Sample complete, hit ENTER tooexit...
```

> [!NOTE]
> Devido a toohello variável criação e começar a hora de nós de um novo conjunto (alguns nós, estará pronto para tarefas antes de outras), poderá ver um resultado diferente. Especificamente, porque as tarefas de Olá concluírem rapidamente, um de nós do conjunto de Olá poderão ser executados todos os Olá tarefas. Se isto ocorrer, irá reparar que Olá preparação da tarefa e tarefas de versão não existe para o nó de Olá que não existem tarefas executadas.
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a>Inspecione a preparação de trabalho e tarefas de lançamento no Olá portal do Azure
Quando executar a aplicação de exemplo de Olá, pode utilizar Olá [portal do Azure] [ portal] tooview Olá as propriedades da tarefa de Olá e as respetivas tarefas ou mesmo transferir o ficheiro de texto partilhado Olá que é modificado pelo Olá tarefas.

Olá captura de ecrã abaixo mostra Olá **painel de tarefas de preparação** no Olá portal do Azure após a execução da aplicação de exemplo de Olá. Navegue toohello *JobPrepReleaseSampleJob* propriedades depois de concluíram as suas tarefas (mas antes de eliminar o seu trabalho e o conjunto) e clique em **tarefas de preparação** ou **tarefasdaversão** tooview as respetivas propriedades.

![Propriedades de preparação da tarefa no portal do Azure][1]

## <a name="next-steps"></a>Passos seguintes
### <a name="application-packages"></a>Pacotes de aplicações
Tarefa de preparação da tarefa do toohello adição, também pode utilizar Olá [pacotes de aplicações](batch-application-packages.md) funcionalidade do Batch tooprepare nós de computação para a execução da tarefa. Esta funcionalidade é especialmente útil para a implementação de aplicações que não necessitam de executar um programa de instalação, as aplicações que contêm muitos ficheiros de (100 +) ou aplicações que requerem controlo de versão rigorosa.

### <a name="installing-applications-and-staging-data"></a>Instalar aplicações e dados de teste
Esta mensagem num fórum MSDN fornece uma descrição geral dos vários métodos de preparar os nós para as tarefas em execução:

[Instalar aplicações e dados em lote de teste de nós de computação][forum_post]

Escrito por um dos membros da equipa do Azure Batch Olá, descreve várias técnicas que pode utilizar toodeploy aplicações e dados toocompute nós.

[api_net]: http://msdn.microsoft.com/library/azure/mt348682.aspx
[api_net_listjobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[api_rest]: http://msdn.microsoft.com/library/azure/dn820158.aspx
[azure_storage]: https://azure.microsoft.com/services/storage/
[portal]: https://portal.azure.com
[job_prep_release_sample]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/JobPrepRelease
[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[net_batch_client]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]:https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_job_prep]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.aspx
[net_job_prep_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobpreparationtask.aspx
[net_job_prep_resourcefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobpreparationtask.resourcefiles.aspx
[net_job_delete]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.deletejobasync.aspx
[net_job_terminate]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.terminatejobasync.aspx
[net_job_release]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobreleasetask.aspx
[net_job_release_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.jobreleasetask.aspx
[pool_starttask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudpool.starttask.aspx

[net_list_certs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.certificateoperations.listcertificates.aspx
[net_list_compute_nodes]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listcomputenodes.aspx
[net_list_job_schedules]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobschedules.aspx
[net_list_jobprep_status]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobpreparationandreleasetaskstatus.aspx
[net_list_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listjobs.aspx
[net_list_nodefiles]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listnodefiles.aspx
[net_list_pools]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.pooloperations.listpools.aspx
[net_list_schedule_jobs]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.jobscheduleoperations.listjobs.aspx
[net_list_task_files]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.listnodefiles.aspx
[net_list_tasks]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.joboperations.listtasks.aspx

[1]: ./media/batch-job-prep-release/portal-jobprep-01.png
