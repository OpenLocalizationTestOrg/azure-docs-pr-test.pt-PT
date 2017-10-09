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
# <a name="run-job-preparation-and-job-release-tasks-on-batch-compute-nodes"></a><span data-ttu-id="56ca8-103">Executar tarefa de preparação e tarefas de lançamento do batch nós de computação</span><span class="sxs-lookup"><span data-stu-id="56ca8-103">Run job preparation and job release tasks on Batch compute nodes</span></span>

 <span data-ttu-id="56ca8-104">Uma tarefa de lote do Azure requer, muitas vezes, algum tipo de configuração antes das respetivas tarefas são executadas e manutenção de tarefa pós-cópia quando as tarefas estão concluídas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-104">An Azure Batch job often requires some form of setup before its tasks are executed, and post-job maintenance when its tasks are completed.</span></span> <span data-ttu-id="56ca8-105">Poderá ter toodownload comuns tarefas dados de entrada tooyour nós de computação ou carregar tooAzure de dados de saída de tarefas armazenamento após a conclusão da tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-105">You might need toodownload common task input data tooyour compute nodes, or upload task output data tooAzure Storage after hello job completes.</span></span> <span data-ttu-id="56ca8-106">Pode utilizar **preparação da tarefa** e **lançamento da tarefa** tarefas tooperform estas operações.</span><span class="sxs-lookup"><span data-stu-id="56ca8-106">You can use **job preparation** and **job release** tasks tooperform these operations.</span></span>

## <a name="what-are-job-preparation-and-release-tasks"></a><span data-ttu-id="56ca8-107">O que são a tarefa de preparação e versão tarefas?</span><span class="sxs-lookup"><span data-stu-id="56ca8-107">What are job preparation and release tasks?</span></span>
<span data-ttu-id="56ca8-108">Antes de executam tarefas de um trabalho, é executada Olá tarefa de preparação da tarefa em todas as computação nós agendada toorun pelo menos uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-108">Before a job's tasks run, hello job preparation task runs on all compute nodes scheduled toorun at least one task.</span></span> <span data-ttu-id="56ca8-109">Depois de concluída a tarefa de Olá, Olá tarefa de lançamento da tarefa é executada em cada nó no conjunto de Olá que executou, pelo menos, uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-109">Once hello job is completed, hello job release task runs on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="56ca8-110">Tal como acontece com as tarefas de lote normal, pode especificar um toobe de linha de comandos invocada quando uma tarefa de preparação ou de lançamento da tarefa é executado.</span><span class="sxs-lookup"><span data-stu-id="56ca8-110">As with normal Batch tasks, you can specify a command line toobe invoked when a job preparation or release task is run.</span></span>

<span data-ttu-id="56ca8-111">Tarefas de preparação e de lançamento da tarefa oferecem funcionalidades de tarefa do Batch familiares como a transferência de ficheiro ([ficheiros de recursos][net_job_prep_resourcefiles]), elevados execução, variáveis de ambiente personalizadas, duração de execução máximo, contagem de repetições e tempo de retenção de ficheiros.</span><span class="sxs-lookup"><span data-stu-id="56ca8-111">Job preparation and release tasks offer familiar Batch task features such as file download ([resource files][net_job_prep_resourcefiles]), elevated execution, custom environment variables, maximum execution duration, retry count, and file retention time.</span></span>

<span data-ttu-id="56ca8-112">Olá secções a seguir, irá aprender como toouse Olá [JobPreparationTask] [ net_job_prep] e [JobReleaseTask] [ net_job_release] localizadas classes na Olá [.NET do batch] [ api_net] biblioteca.</span><span class="sxs-lookup"><span data-stu-id="56ca8-112">In hello following sections, you'll learn how toouse hello [JobPreparationTask][net_job_prep] and [JobReleaseTask][net_job_release] classes found in hello [Batch .NET][api_net] library.</span></span>

> [!TIP]
> <span data-ttu-id="56ca8-113">Tarefas de preparação e de lançamento da tarefa são especialmente útil em ambientes do "agrupamento partilhado", em que um conjunto de nós de computação persistir entre execuções de tarefa e é utilizado por muitas tarefas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-113">Job preparation and release tasks are especially helpful in "shared pool" environments, in which a pool of compute nodes persists between job runs and is used by many jobs.</span></span>
> 
> 

## <a name="when-toouse-job-preparation-and-release-tasks"></a><span data-ttu-id="56ca8-114">Quando toouse preparação da tarefa e tarefas da versão</span><span class="sxs-lookup"><span data-stu-id="56ca8-114">When toouse job preparation and release tasks</span></span>
<span data-ttu-id="56ca8-115">Preparação de trabalho e tarefas de lançamento são uma boa opção para Olá seguintes situações:</span><span class="sxs-lookup"><span data-stu-id="56ca8-115">Job preparation and job release tasks are a good fit for hello following situations:</span></span>

<span data-ttu-id="56ca8-116">**Transferência de dados de tarefas comuns**</span><span class="sxs-lookup"><span data-stu-id="56ca8-116">**Download common task data**</span></span>

<span data-ttu-id="56ca8-117">Tarefas do batch, muitas vezes, necessitam de um conjunto de dados comum como entrada para tarefas do trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-117">Batch jobs often require a common set of data as input for hello job's tasks.</span></span> <span data-ttu-id="56ca8-118">Por exemplo, nos cálculos de análise de risco diária, dados de mercado são tarefa específico, ainda comuns tooall de tarefas na tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-118">For example, in daily risk analysis calculations, market data is job-specific, yet common tooall tasks in hello job.</span></span> <span data-ttu-id="56ca8-119">Estes dados de mercado, muitas vezes, vários gigabytes de tamanho, devem ser o nó de computação tooeach transferido apenas uma vez para que qualquer tarefa que é executado no nó de Olá pode utilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="56ca8-119">This market data, often several gigabytes in size, should be downloaded tooeach compute node only once so that any task that runs on hello node can use it.</span></span> <span data-ttu-id="56ca8-120">Utilize um **tarefa de preparação** toodownload este nó de tooeach dados antes de execução de Olá da tarefa de Olá 's outras tarefas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-120">Use a **job preparation task** toodownload this data tooeach node before hello execution of hello job's other tasks.</span></span>

<span data-ttu-id="56ca8-121">**Eliminar tarefas e saída**</span><span class="sxs-lookup"><span data-stu-id="56ca8-121">**Delete job and task output**</span></span>

<span data-ttu-id="56ca8-122">Num ambiente "agrupamento partilhado", onde não são desativados entre trabalhos de nós de computação de um conjunto, poderá ter dados de tarefa toodelete entre é executado.</span><span class="sxs-lookup"><span data-stu-id="56ca8-122">In a "shared pool" environment, where a pool's compute nodes are not decommissioned between jobs, you may need toodelete job data between runs.</span></span> <span data-ttu-id="56ca8-123">Poderá ser necessário tooconserve espaço em disco em nós Olá ou satisfazer as políticas de segurança da sua organização.</span><span class="sxs-lookup"><span data-stu-id="56ca8-123">You might need tooconserve disk space on hello nodes, or satisfy your organization's security policies.</span></span> <span data-ttu-id="56ca8-124">Utilize um **tarefa de libertação** toodelete dados que foi transferidos por uma tarefa de preparação ou gerados durante a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-124">Use a **job release task** toodelete data that was downloaded by a job preparation task, or generated during task execution.</span></span>

<span data-ttu-id="56ca8-125">**Retenção do registo**</span><span class="sxs-lookup"><span data-stu-id="56ca8-125">**Log retention**</span></span>

<span data-ttu-id="56ca8-126">Pode querer tookeep uma cópia de ficheiros de registo que as suas tarefas geram ou talvez falhas ficheiros de informação que podem ser gerados pelas aplicações com falhas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-126">You might want tookeep a copy of log files that your tasks generate, or perhaps crash dump files that can be generated by failed applications.</span></span> <span data-ttu-id="56ca8-127">Utilize um **tarefa de libertação** nessas toocompress casos e carregar este tooan dados [Storage do Azure] [ azure_storage] conta.</span><span class="sxs-lookup"><span data-stu-id="56ca8-127">Use a **job release task** in such cases toocompress and upload this data tooan [Azure Storage][azure_storage] account.</span></span>

> [!TIP]
> <span data-ttu-id="56ca8-128">Outra forma toopersist registos e outras tarefas e saída de dados são toouse Olá [convenções de ficheiro do Azure Batch](batch-task-output.md) biblioteca.</span><span class="sxs-lookup"><span data-stu-id="56ca8-128">Another way toopersist logs and other job and task output data is toouse hello [Azure Batch File Conventions](batch-task-output.md) library.</span></span>
> 
> 

## <a name="job-preparation-task"></a><span data-ttu-id="56ca8-129">Tarefa de preparação</span><span class="sxs-lookup"><span data-stu-id="56ca8-129">Job preparation task</span></span>
<span data-ttu-id="56ca8-130">Antes da execução das tarefas de uma tarefa, o Batch executa Olá tarefa de preparação da tarefa em cada nó de computação que é toorun agendada uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-130">Before execution of a job's tasks, Batch executes hello job preparation task on each compute node that is scheduled toorun a task.</span></span> <span data-ttu-id="56ca8-131">Por predefinição, Olá serviço Batch aguarda Olá tarefa preparação tarefas toobe concluída antes de executar Olá tarefas agendadas tooexecute no nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-131">By default, hello Batch service waits for hello job preparation task toobe completed before running hello tasks scheduled tooexecute on hello node.</span></span> <span data-ttu-id="56ca8-132">No entanto, pode configurar o serviço de Olá toowait não.</span><span class="sxs-lookup"><span data-stu-id="56ca8-132">However, you can configure hello service not toowait.</span></span> <span data-ttu-id="56ca8-133">Se reiniciar o nó de Olá, Olá tarefa de preparação da tarefa é executada novamente, mas também pode desativar este comportamento.</span><span class="sxs-lookup"><span data-stu-id="56ca8-133">If hello node restarts, hello job preparation task runs again, but you can also disable this behavior.</span></span>

<span data-ttu-id="56ca8-134">tarefa de preparação Olá é executada apenas em nós que são toorun agendada uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-134">hello job preparation task is executed only on nodes that are scheduled toorun a task.</span></span> <span data-ttu-id="56ca8-135">Isto impede que a execução de desnecessários Olá de uma tarefa de preparação, no caso de um nó não está atribuído uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-135">This prevents hello unnecessary execution of a preparation task in case a node is not assigned a task.</span></span> <span data-ttu-id="56ca8-136">Isto pode ocorrer quando o número de Olá de tarefas para uma tarefa é inferior ao número de Olá de nós num conjunto.</span><span class="sxs-lookup"><span data-stu-id="56ca8-136">This can occur when hello number of tasks for a job is less than hello number of nodes in a pool.</span></span> <span data-ttu-id="56ca8-137">Também se aplica quando [a execução da tarefa em simultâneo](batch-parallel-node-tasks.md) estiver ativado, que deixa alguns nós inativo se a contagem de tarefas Olá é inferior ao tarefas simultâneas possíveis total Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-137">It also applies when [concurrent task execution](batch-parallel-node-tasks.md) is enabled, which leaves some nodes idle if hello task count is lower than hello total possible concurrent tasks.</span></span> <span data-ttu-id="56ca8-138">Por não executar tarefa de preparação Olá em nós inativos, pode pode menos adiantar dinheiro com taxas aplicáveis às transferências de dados.</span><span class="sxs-lookup"><span data-stu-id="56ca8-138">By not running hello job preparation task on idle nodes, you can spend less money on data transfer charges.</span></span>

> [!NOTE]
> <span data-ttu-id="56ca8-139">[JobPreparationTask] [ net_job_prep_cloudjob] difere [CloudPool.StartTask] [ pool_starttask] nessa JobPreparationTask executa no início de Olá de cada tarefa, enquanto que StartTask executa apenas quando um nó de computação primeiro associa um conjunto ou de reiniciar.</span><span class="sxs-lookup"><span data-stu-id="56ca8-139">[JobPreparationTask][net_job_prep_cloudjob] differs from [CloudPool.StartTask][pool_starttask] in that JobPreparationTask executes at hello start of each job, whereas StartTask executes only when a compute node first joins a pool or restarts.</span></span>
> 
> 

## <a name="job-release-task"></a><span data-ttu-id="56ca8-140">Tarefa de lançamento da tarefa</span><span class="sxs-lookup"><span data-stu-id="56ca8-140">Job release task</span></span>
<span data-ttu-id="56ca8-141">Depois de uma tarefa é marcada como concluído, Olá tarefa de lançamento da tarefa é executado em cada nó no conjunto de Olá que executou, pelo menos, uma tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-141">Once a job is marked as completed, hello job release task is executed on each node in hello pool that executed at least one task.</span></span> <span data-ttu-id="56ca8-142">Marcar uma tarefa como concluído ao emitir um pedido de terminar.</span><span class="sxs-lookup"><span data-stu-id="56ca8-142">You mark a job as completed by issuing a terminate request.</span></span> <span data-ttu-id="56ca8-143">Olá serviço Batch, em seguida, define Olá estado de tarefa demasiado*terminar*, termina quaisquer tarefas em execução ou Active Directory associadas à tarefa Olá e executa a tarefa de libertação Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-143">hello Batch service then sets hello job state too*terminating*, terminates any active or running tasks associated with hello job, and runs hello job release task.</span></span> <span data-ttu-id="56ca8-144">tarefa de Olá, em seguida, move toohello *concluída* estado.</span><span class="sxs-lookup"><span data-stu-id="56ca8-144">hello job then moves toohello *completed* state.</span></span>

> [!NOTE]
> <span data-ttu-id="56ca8-145">Eliminação da tarefa também executa Olá tarefa de lançamento da tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-145">Job deletion also executes hello job release task.</span></span> <span data-ttu-id="56ca8-146">No entanto, se uma tarefa já foi terminada, Olá de lançamento da tarefa não é executado uma segunda vez se tarefa Olá for eliminada mais tarde.</span><span class="sxs-lookup"><span data-stu-id="56ca8-146">However, if a job has already been terminated, hello release task is not run a second time if hello job is later deleted.</span></span>
> 
> 

## <a name="job-prep-and-release-tasks-with-batch-net"></a><span data-ttu-id="56ca8-147">Tarefa de preparação e versão tarefas com .NET do Batch</span><span class="sxs-lookup"><span data-stu-id="56ca8-147">Job prep and release tasks with Batch .NET</span></span>
<span data-ttu-id="56ca8-148">toouse uma tarefa de preparação, atribuir um [JobPreparationTask] [ net_job_prep] da tarefa do objeto tooyour [CloudJob.JobPreparationTask] [ net_job_prep_cloudjob] propriedade .</span><span class="sxs-lookup"><span data-stu-id="56ca8-148">toouse a job preparation task, assign a [JobPreparationTask][net_job_prep] object tooyour job's [CloudJob.JobPreparationTask][net_job_prep_cloudjob] property.</span></span> <span data-ttu-id="56ca8-149">Da mesma forma, inicializar um [JobReleaseTask] [ net_job_release] e atribua-a tarefa de tooyour [CloudJob.JobReleaseTask] [ net_job_prep_cloudjob] Olá tooset de propriedade tarefa de lançamento da tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-149">Similarly, initialize a [JobReleaseTask][net_job_release] and assign it tooyour job's [CloudJob.JobReleaseTask][net_job_prep_cloudjob] property tooset hello job's release task.</span></span>

<span data-ttu-id="56ca8-150">Este fragmento de código, `myBatchClient` é uma instância de [BatchClient][net_batch_client], e `myPool` é um conjunto existente na Olá conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="56ca8-150">In this code snippet, `myBatchClient` is an instance of [BatchClient][net_batch_client], and `myPool` is an existing pool within hello Batch account.</span></span>

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

<span data-ttu-id="56ca8-151">Conforme mencionado anteriormente, Olá de lançamento da tarefa é executado quando uma tarefa é terminada ou eliminada.</span><span class="sxs-lookup"><span data-stu-id="56ca8-151">As mentioned earlier, hello release task is executed when a job is terminated or deleted.</span></span> <span data-ttu-id="56ca8-152">Terminar uma tarefa com [joboperations. Terminatejobasync][net_job_terminate].</span><span class="sxs-lookup"><span data-stu-id="56ca8-152">Terminate a job with [JobOperations.TerminateJobAsync][net_job_terminate].</span></span> <span data-ttu-id="56ca8-153">Eliminar uma tarefa com [JobOperations.DeleteJobAsync][net_job_delete].</span><span class="sxs-lookup"><span data-stu-id="56ca8-153">Delete a job with [JobOperations.DeleteJobAsync][net_job_delete].</span></span> <span data-ttu-id="56ca8-154">Normalmente, terminar ou eliminar uma tarefa quando as tarefas estão concluídas, ou quando foi atingido o limite de tempo que definiu.</span><span class="sxs-lookup"><span data-stu-id="56ca8-154">You typically terminate or delete a job when its tasks are completed, or when a timeout that you've defined has been reached.</span></span>

```csharp
// Terminate hello job toomark it as Completed; this will initiate the
// Job Release Task on any node that executed job tasks. Note that the
// Job Release Task is also executed when a job is deleted, thus you
// need not call Terminate if you typically delete jobs after task completion.
await myBatchClient.JobOperations.TerminateJobAsy("JobPrepReleaseSampleJob");
```

## <a name="code-sample-on-github"></a><span data-ttu-id="56ca8-155">Exemplo de código no GitHub</span><span class="sxs-lookup"><span data-stu-id="56ca8-155">Code sample on GitHub</span></span>
<span data-ttu-id="56ca8-156">toosee preparação e de lançamento tarefas em ação, consulte Olá [JobPrepRelease] [ job_prep_release_sample] projeto de exemplo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="56ca8-156">toosee job preparation and release tasks in action, check out hello [JobPrepRelease][job_prep_release_sample] sample project on GitHub.</span></span> <span data-ttu-id="56ca8-157">Esta aplicação de consola Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="56ca8-157">This console application does hello following:</span></span>

1. <span data-ttu-id="56ca8-158">Cria um conjunto com dois nós "pequenos".</span><span class="sxs-lookup"><span data-stu-id="56ca8-158">Creates a pool with two "small" nodes.</span></span>
2. <span data-ttu-id="56ca8-159">Cria uma tarefa com a tarefa de preparação, versão e tarefas padrão.</span><span class="sxs-lookup"><span data-stu-id="56ca8-159">Creates a job with job preparation, release, and standard tasks.</span></span>
3. <span data-ttu-id="56ca8-160">Executa Olá tarefa de preparação, que escreve primeiro o ficheiro de texto de tooa de ID de nó de Olá no diretório de "partilhado" de um nó.</span><span class="sxs-lookup"><span data-stu-id="56ca8-160">Runs hello job preparation task, which first writes hello node ID tooa text file in a node's "shared" directory.</span></span>
4. <span data-ttu-id="56ca8-161">Executa uma tarefa em cada nó que escreve o respetivo toohello de ID de tarefa mesmo ficheiro de texto.</span><span class="sxs-lookup"><span data-stu-id="56ca8-161">Runs a task on each node that writes its task ID toohello same text file.</span></span>
5. <span data-ttu-id="56ca8-162">Depois de todas as tarefas são concluídas (ou for atingido o tempo limite de Olá), imprima conteúdo Olá da consola de toohello de ficheiro de texto de cada nó.</span><span class="sxs-lookup"><span data-stu-id="56ca8-162">Once all tasks are completed (or hello timeout is reached), prints hello contents of each node's text file toohello console.</span></span>
6. <span data-ttu-id="56ca8-163">Quando a tarefa de Olá estiver concluída, é executado Olá tarefa versão tarefas toodelete Olá ficheiro a partir do nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-163">When hello job is completed, runs hello job release task toodelete hello file from hello node.</span></span>
7. <span data-ttu-id="56ca8-164">Olá impressões sair códigos de tarefa de preparação de Olá e versão tarefas para cada nó no qual são executados.</span><span class="sxs-lookup"><span data-stu-id="56ca8-164">Prints hello exit codes of hello job preparation and release tasks for each node on which they executed.</span></span>
8. <span data-ttu-id="56ca8-165">Confirmação de tooallow de execução de coloca em pausa da tarefa e/ou conjunto de eliminação.</span><span class="sxs-lookup"><span data-stu-id="56ca8-165">Pauses execution tooallow confirmation of job and/or pool deletion.</span></span>

<span data-ttu-id="56ca8-166">Resultado da aplicação de exemplo de Olá é semelhante toohello seguinte:</span><span class="sxs-lookup"><span data-stu-id="56ca8-166">Output from hello sample application is similar toohello following:</span></span>

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
> <span data-ttu-id="56ca8-167">Devido a toohello variável criação e começar a hora de nós de um novo conjunto (alguns nós, estará pronto para tarefas antes de outras), poderá ver um resultado diferente.</span><span class="sxs-lookup"><span data-stu-id="56ca8-167">Due toohello variable creation and start time of nodes in a new pool (some nodes are ready for tasks before others), you may see different output.</span></span> <span data-ttu-id="56ca8-168">Especificamente, porque as tarefas de Olá concluírem rapidamente, um de nós do conjunto de Olá poderão ser executados todos os Olá tarefas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-168">Specifically, because hello tasks complete quickly, one of hello pool's nodes may execute all of hello job's tasks.</span></span> <span data-ttu-id="56ca8-169">Se isto ocorrer, irá reparar que Olá preparação da tarefa e tarefas de versão não existe para o nó de Olá que não existem tarefas executadas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-169">If this occurs, you will notice that hello job prep and release tasks do not exist for hello node that executed no tasks.</span></span>
> 
> 

### <a name="inspect-job-preparation-and-release-tasks-in-hello-azure-portal"></a><span data-ttu-id="56ca8-170">Inspecione a preparação de trabalho e tarefas de lançamento no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="56ca8-170">Inspect job preparation and release tasks in hello Azure portal</span></span>
<span data-ttu-id="56ca8-171">Quando executar a aplicação de exemplo de Olá, pode utilizar Olá [portal do Azure] [ portal] tooview Olá as propriedades da tarefa de Olá e as respetivas tarefas ou mesmo transferir o ficheiro de texto partilhado Olá que é modificado pelo Olá tarefas.</span><span class="sxs-lookup"><span data-stu-id="56ca8-171">When you run hello sample application, you can use hello [Azure portal][portal] tooview hello properties of hello job and its tasks, or even download hello shared text file that is modified by hello job's tasks.</span></span>

<span data-ttu-id="56ca8-172">Olá captura de ecrã abaixo mostra Olá **painel de tarefas de preparação** no Olá portal do Azure após a execução da aplicação de exemplo de Olá.</span><span class="sxs-lookup"><span data-stu-id="56ca8-172">hello screenshot below shows hello **Preparation tasks blade** in hello Azure portal after a run of hello sample application.</span></span> <span data-ttu-id="56ca8-173">Navegue toohello *JobPrepReleaseSampleJob* propriedades depois de concluíram as suas tarefas (mas antes de eliminar o seu trabalho e o conjunto) e clique em **tarefas de preparação** ou **tarefasdaversão** tooview as respetivas propriedades.</span><span class="sxs-lookup"><span data-stu-id="56ca8-173">Navigate toohello *JobPrepReleaseSampleJob* properties after your tasks have completed (but before deleting your job and pool) and click **Preparation tasks** or **Release tasks** tooview their properties.</span></span>

![Propriedades de preparação da tarefa no portal do Azure][1]

## <a name="next-steps"></a><span data-ttu-id="56ca8-175">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="56ca8-175">Next steps</span></span>
### <a name="application-packages"></a><span data-ttu-id="56ca8-176">Pacotes de aplicações</span><span class="sxs-lookup"><span data-stu-id="56ca8-176">Application packages</span></span>
<span data-ttu-id="56ca8-177">Tarefa de preparação da tarefa do toohello adição, também pode utilizar Olá [pacotes de aplicações](batch-application-packages.md) funcionalidade do Batch tooprepare nós de computação para a execução da tarefa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-177">In addition toohello job preparation task, you can also use hello [application packages](batch-application-packages.md) feature of Batch tooprepare compute nodes for task execution.</span></span> <span data-ttu-id="56ca8-178">Esta funcionalidade é especialmente útil para a implementação de aplicações que não necessitam de executar um programa de instalação, as aplicações que contêm muitos ficheiros de (100 +) ou aplicações que requerem controlo de versão rigorosa.</span><span class="sxs-lookup"><span data-stu-id="56ca8-178">This feature is especially useful for deploying applications that do not require running an installer, applications that contain many (100+) files, or applications that require strict version control.</span></span>

### <a name="installing-applications-and-staging-data"></a><span data-ttu-id="56ca8-179">Instalar aplicações e dados de teste</span><span class="sxs-lookup"><span data-stu-id="56ca8-179">Installing applications and staging data</span></span>
<span data-ttu-id="56ca8-180">Esta mensagem num fórum MSDN fornece uma descrição geral dos vários métodos de preparar os nós para as tarefas em execução:</span><span class="sxs-lookup"><span data-stu-id="56ca8-180">This MSDN forum post provides an overview of several methods of preparing your nodes for running tasks:</span></span>

<span data-ttu-id="56ca8-181">[Instalar aplicações e dados em lote de teste de nós de computação][forum_post]</span><span class="sxs-lookup"><span data-stu-id="56ca8-181">[Installing applications and staging data on Batch compute nodes][forum_post]</span></span>

<span data-ttu-id="56ca8-182">Escrito por um dos membros da equipa do Azure Batch Olá, descreve várias técnicas que pode utilizar toodeploy aplicações e dados toocompute nós.</span><span class="sxs-lookup"><span data-stu-id="56ca8-182">Written by one of hello Azure Batch team members, it discusses several techniques that you can use toodeploy applications and data toocompute nodes.</span></span>

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
