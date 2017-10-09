---
title: "aaaPersist tarefas e saída tooAzure armazenamento com a biblioteca de convenções de ficheiro Olá para .NET - Azure Batch | Microsoft Docs"
description: "Saiba como toouse biblioteca de convenções de ficheiro do Azure Batch para .NET toopersist tarefa do Batch e tooAzure de saída da tarefa armazenamento e Olá vista persistente saída no Olá portal do Azure."
services: batch
documentationcenter: .net
author: tamram
manager: timlt
editor: 
ms.assetid: 16e12d0e-958c-46c2-a6b8-7843835d830e
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cf2ac8632a13d32438c1bdcf11b4b9649de1e2b5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a><span data-ttu-id="ca549-103">Manter a tarefa e tarefas dados tooAzure armazenamento com biblioteca de convenções de ficheiro Batch Olá para toopersist de .NET</span><span class="sxs-lookup"><span data-stu-id="ca549-103">Persist job and task data tooAzure Storage with hello Batch File Conventions library for .NET toopersist</span></span> 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

<span data-ttu-id="ca549-104">Dados de tarefa toopersist unidirecional são toouse Olá [biblioteca convenções de ficheiro do Azure Batch para .NET][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="ca549-104">One way toopersist task data is toouse hello [Azure Batch File Conventions library for .NET][nuget_package].</span></span> <span data-ttu-id="ca549-105">Olá biblioteca convenções de ficheiros simplifica o processo de Olá do armazenamento de resultado da tarefa dados tooAzure armazenamento e obtê-lo.</span><span class="sxs-lookup"><span data-stu-id="ca549-105">hello File Conventions library simplifies hello process of storing task output data tooAzure Storage and retrieving it.</span></span> <span data-ttu-id="ca549-106">Pode utilizar as convenções de ficheiro de Olá biblioteca no código de tarefas e o cliente &mdash; no código de tarefas para ficheiros persistentes e no cliente code toolist e obtê-los.</span><span class="sxs-lookup"><span data-stu-id="ca549-106">You can use hello File Conventions library in both task and client code &mdash; in task code for persisting files, and in client code toolist and retrieve them.</span></span> <span data-ttu-id="ca549-107">O código de tarefas pode também utilizar a Olá biblioteca tooretrieve Olá saída das tarefas a montante, tal como num [dependências de tarefas](batch-task-dependencies.md) cenário.</span><span class="sxs-lookup"><span data-stu-id="ca549-107">Your task code can also use hello library tooretrieve hello output of upstream tasks, such as in a [task dependencies](batch-task-dependencies.md) scenario.</span></span> 

<span data-ttu-id="ca549-108">ficheiros de biblioteca do Olá convenções de ficheiro de saída tooretrieve, pode localizar ficheiros Olá para uma determinada tarefa tarefas enumerando-los por ID e o objetivo.</span><span class="sxs-lookup"><span data-stu-id="ca549-108">tooretrieve output files with hello File Conventions library, you can locate hello files for a given job or task by listing them by ID and purpose.</span></span> <span data-ttu-id="ca549-109">Não precisa de nomes de Olá tooknow ou localizações dos ficheiros de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-109">You don't need tooknow hello names or locations of hello files.</span></span> <span data-ttu-id="ca549-110">Por exemplo, pode utilizar toolist de biblioteca de convenções de ficheiro Olá todos os ficheiros intermédios de uma determinada tarefa ou obter um ficheiro de pré-visualização para uma determinada tarefa.</span><span class="sxs-lookup"><span data-stu-id="ca549-110">For example, you can use hello File Conventions library toolist all intermediate files for a given task, or get a preview file for a given job.</span></span>

> [!TIP]
> <span data-ttu-id="ca549-111">A partir da versão de 2017-05-01, Olá API do serviço Batch suporta persistentes tooAzure de dados de saída armazenamento para tarefas e tarefas de Gestor de tarefas serem executadas em conjuntos criados com a configuração da máquina virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-111">Starting with version 2017-05-01, hello Batch service API supports persisting output data tooAzure Storage for tasks and job manager tasks that run on pools created with hello virtual machine configuration.</span></span> <span data-ttu-id="ca549-112">Olá API do serviço Batch fornece um toopersist de forma simples de saída de dentro do código de Olá que cria uma tarefa e funciona como uma biblioteca de convenções de ficheiro toohello alternativo.</span><span class="sxs-lookup"><span data-stu-id="ca549-112">hello Batch service API provides a simple way toopersist output from within hello code that creates a task and serves as an alternative toohello File Conventions library.</span></span> <span data-ttu-id="ca549-113">Pode modificar a saída de toopersist de aplicações do Batch cliente sem necessitar de aplicação de Olá tooupdate que a tarefa está em execução.</span><span class="sxs-lookup"><span data-stu-id="ca549-113">You can modify your Batch client applications toopersist output without needing tooupdate hello application that your task is running.</span></span> <span data-ttu-id="ca549-114">Para obter mais informações, consulte [manter tarefas dados tooAzure armazenamento com Olá API do serviço Batch](batch-task-output-files.md).</span><span class="sxs-lookup"><span data-stu-id="ca549-114">For more information, see [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md).</span></span>
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a><span data-ttu-id="ca549-115">Quando utilizar o resultado da tarefa toopersist Olá convenções de ficheiro biblioteca?</span><span class="sxs-lookup"><span data-stu-id="ca549-115">When do I use hello File Conventions library toopersist task output?</span></span>

<span data-ttu-id="ca549-116">O Azure Batch fornece mais de uma forma toopersist o resultado da tarefa.</span><span class="sxs-lookup"><span data-stu-id="ca549-116">Azure Batch provides more than one way toopersist task output.</span></span> <span data-ttu-id="ca549-117">Olá convenções de ficheiro é melhor cenários de toothese adequada:</span><span class="sxs-lookup"><span data-stu-id="ca549-117">hello File Conventions is best suited toothese scenarios:</span></span>

- <span data-ttu-id="ca549-118">Pode facilmente modificar código Olá para aplicação Olá que a tarefa está em execução ficheiros toopersist utilizando Olá convenções de ficheiro biblioteca.</span><span class="sxs-lookup"><span data-stu-id="ca549-118">You can easily modify hello code for hello application that your task is running toopersist files using hello File Conventions library.</span></span>
- <span data-ttu-id="ca549-119">Pretende toostream dados tooAzure armazenamento enquanto a tarefa de Olá ainda está em execução.</span><span class="sxs-lookup"><span data-stu-id="ca549-119">You want toostream data tooAzure Storage while hello task is still running.</span></span>
- <span data-ttu-id="ca549-120">Pretende que os dados de toopersist em agrupamentos criados com a configuração de máquina virtual de Olá ou a configuração do serviço de nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-120">You want toopersist data from pools created with either hello cloud service configuration or hello virtual machine configuration.</span></span>
- <span data-ttu-id="ca549-121">A aplicação cliente ou outras tarefas no Olá toolocate necessidades de tarefa e transferir ficheiros de saída de tarefas por ID ou por objetivo.</span><span class="sxs-lookup"><span data-stu-id="ca549-121">Your client application or other tasks in hello job needs toolocate and download task output files by ID or by purpose.</span></span> 
- <span data-ttu-id="ca549-122">Pretende que o resultado da tarefa tooview no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca549-122">You want tooview task output in hello Azure portal.</span></span>

<span data-ttu-id="ca549-123">Se o seu cenário difere de acordo com os listado acima, poderá ser necessário tooconsider uma abordagem diferente.</span><span class="sxs-lookup"><span data-stu-id="ca549-123">If your scenario differs from those listed above, you may need tooconsider a different approach.</span></span> <span data-ttu-id="ca549-124">Para obter mais informações sobre outras opções para persistentes resultado da tarefa, consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md).</span><span class="sxs-lookup"><span data-stu-id="ca549-124">For more information on other options for persisting task output, see [Persist job and task output tooAzure Storage](batch-task-output.md).</span></span> 

## <a name="what-is-hello-batch-file-conventions-standard"></a><span data-ttu-id="ca549-125">O que é Olá convenções de ficheiro Batch padrão?</span><span class="sxs-lookup"><span data-stu-id="ca549-125">What is hello Batch File Conventions standard?</span></span>

<span data-ttu-id="ca549-126">Olá [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornece um esquema de nomenclatura para contentores de destino Olá e BLOBs caminhos toowhich os ficheiros de saída são escritos.</span><span class="sxs-lookup"><span data-stu-id="ca549-126">hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) provides a naming scheme for hello destination containers and blob paths toowhich your output files are written.</span></span> <span data-ttu-id="ca549-127">Ficheiros persistente tooAzure armazenamento respeitar toohello convenções de ficheiro padrão estão automaticamente disponíveis para visualização nos Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca549-127">Files persisted tooAzure Storage that adhere toohello File Conventions standard are automatically available for viewing in hello Azure portal.</span></span> <span data-ttu-id="ca549-128">portal de Olá tem conhecimento de convenção de nomenclatura de Olá e, por isso, pode visualizar ficheiros que cumprem tooit.</span><span class="sxs-lookup"><span data-stu-id="ca549-128">hello portal is aware of hello naming convention and so can display files that adhere tooit.</span></span>

<span data-ttu-id="ca549-129">biblioteca de convenções de ficheiro Olá para .NET nomes automaticamente os ficheiros de saída de tarefas de acordo com toohello convenções de ficheiro padrão e contentores de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-129">hello File Conventions library for .NET automatically names your storage containers and task output files according toohello File Conventions standard.</span></span> <span data-ttu-id="ca549-130">biblioteca de convenções de ficheiro Olá também fornece métodos tooquery ficheiros de saída no armazenamento do Azure de acordo com o ID de toojob, o ID de tarefa ou o objetivo.</span><span class="sxs-lookup"><span data-stu-id="ca549-130">hello File Conventions library also provides methods tooquery output files in Azure Storage according toojob ID, task ID, or purpose.</span></span>   

<span data-ttu-id="ca549-131">Se estiver a desenvolver com um idioma diferente do .NET, pode implementar a norma de convenções de ficheiro Olá por si na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="ca549-131">If you are developing with a language other than .NET, you can implement hello File Conventions standard yourself in your application.</span></span> <span data-ttu-id="ca549-132">Para obter mais informações, consulte [sobre padrão de convenções de ficheiro Batch Olá](batch-task-output.md#about-the-batch-file-conventions-standard).</span><span class="sxs-lookup"><span data-stu-id="ca549-132">For more information, see [About hello Batch File Conventions standard](batch-task-output.md#about-the-batch-file-conventions-standard).</span></span>

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a><span data-ttu-id="ca549-133">Associar um tooyour de conta do Storage do Azure conta do Batch</span><span class="sxs-lookup"><span data-stu-id="ca549-133">Link an Azure Storage account tooyour Batch account</span></span>

<span data-ttu-id="ca549-134">toopersist tooAzure de dados de saída armazenamento utilizando a biblioteca de convenções de ficheiro Olá, primeiro tem de associar uma tooyour de conta do Storage do Azure conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="ca549-134">toopersist output data tooAzure Storage using hello File Conventions library, you must first link an Azure Storage account tooyour Batch account.</span></span> <span data-ttu-id="ca549-135">Se não tiver o feito, associar um tooyour de conta de armazenamento conta do Batch, utilizando Olá [portal do Azure](https://portal.azure.com):</span><span class="sxs-lookup"><span data-stu-id="ca549-135">If you haven't done so already, link a Storage account tooyour Batch account by using hello [Azure portal](https://portal.azure.com):</span></span>

1. <span data-ttu-id="ca549-136">Navegue tooyour conta do Batch no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca549-136">Navigate tooyour Batch account in hello Azure portal.</span></span> 
2. <span data-ttu-id="ca549-137">Em **definições**, selecione **conta de armazenamento**.</span><span class="sxs-lookup"><span data-stu-id="ca549-137">Under **Settings**, select **Storage Account**.</span></span>
3. <span data-ttu-id="ca549-138">Se ainda não tiver uma conta de armazenamento associada à sua conta do Batch, clique em **conta de armazenamento (nenhum)**.</span><span class="sxs-lookup"><span data-stu-id="ca549-138">If you do not already have a Storage account associated with your Batch account, click **Storage Account (None)**.</span></span>
4. <span data-ttu-id="ca549-139">Selecione uma conta de armazenamento na lista de Olá para a sua subscrição.</span><span class="sxs-lookup"><span data-stu-id="ca549-139">Select a Storage account from hello list for your subscription.</span></span> <span data-ttu-id="ca549-140">Para melhor desempenho, utilize uma conta de armazenamento do Azure que está a ser Olá mesma região que Olá conta do Batch em que as tarefas estão em execução.</span><span class="sxs-lookup"><span data-stu-id="ca549-140">For best performance, use an Azure Storage account that is in hello same region as hello Batch account where your tasks are running.</span></span>

## <a name="persist-output-data"></a><span data-ttu-id="ca549-141">Manter os dados de saída</span><span class="sxs-lookup"><span data-stu-id="ca549-141">Persist output data</span></span>

<span data-ttu-id="ca549-142">toopersist tarefas e saída de dados com a biblioteca de convenções de ficheiro Olá, criar um contentor de armazenamento do Azure, em seguida, guardar o contentor de toohello Olá saída.</span><span class="sxs-lookup"><span data-stu-id="ca549-142">toopersist job and task output data with hello File Conventions library, create a container in Azure Storage, then save hello output toohello container.</span></span> <span data-ttu-id="ca549-143">Olá utilize [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) no tarefas código tooupload Olá tarefas saída toohello contentor de.</span><span class="sxs-lookup"><span data-stu-id="ca549-143">Use hello [Azure Storage client library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage) in your task code tooupload hello task output toohello container.</span></span> 

<span data-ttu-id="ca549-144">Para obter mais informações sobre como trabalhar com contentores e blobs no armazenamento do Azure, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="ca549-144">For more information about working with containers and blobs in Azure Storage, see [Get started with Azure Blob storage using .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).</span></span>

> [!WARNING]
> <span data-ttu-id="ca549-145">Todas as saídas de tarefas e persistente com Olá convenções de ficheiros armazenados na biblioteca Olá mesmo contentor.</span><span class="sxs-lookup"><span data-stu-id="ca549-145">All job and task outputs persisted with hello File Conventions library are stored in hello same container.</span></span> <span data-ttu-id="ca549-146">Se um grande número de tarefas tente toopersist ficheiros em Olá mesmo tempo, [os limites de armazenamento](../storage/common/storage-performance-checklist.md#blobs) poderá ser forçado.</span><span class="sxs-lookup"><span data-stu-id="ca549-146">If a large number of tasks try toopersist files at hello same time, [storage throttling limits](../storage/common/storage-performance-checklist.md#blobs) may be enforced.</span></span>
> 
> 

### <a name="create-storage-container"></a><span data-ttu-id="ca549-147">Criar contentor de armazenamento</span><span class="sxs-lookup"><span data-stu-id="ca549-147">Create storage container</span></span>

<span data-ttu-id="ca549-148">toopersist tarefas saída tooAzure armazenamento, primeiro crie um contentor chamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync].</span><span class="sxs-lookup"><span data-stu-id="ca549-148">toopersist task output tooAzure Storage, first create a container by calling [CloudJob][net_cloudjob].[PrepareOutputStorageAsync][net_prepareoutputasync].</span></span> <span data-ttu-id="ca549-149">Este método de extensão aceita um [CloudStorageAccount] [ net_cloudstorageaccount] objeto como parâmetro.</span><span class="sxs-lookup"><span data-stu-id="ca549-149">This extension method takes a [CloudStorageAccount][net_cloudstorageaccount] object as a parameter.</span></span> <span data-ttu-id="ca549-150">Cria um contentor com o nome de acordo com toohello ficheiro convenções padrão, para que o respetivo conteúdo é detetável pelo Olá Azure métodos de obtenção portal e Olá abordados posteriormente artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-150">It creates a container named according toohello File Conventions standard,so that its contents are discoverable by hello Azure portal and hello retrieval methods discussed later in hello article.</span></span>

<span data-ttu-id="ca549-151">Normalmente, coloque o Olá código toocreate um contentor na sua aplicação de cliente &mdash; Olá aplicação que cria os agrupamentos, tarefas e tarefas.</span><span class="sxs-lookup"><span data-stu-id="ca549-151">You typically place hello code toocreate a container in your client application &mdash; hello application that creates your pools, jobs, and tasks.</span></span>

```csharp
CloudJob job = batchClient.JobOperations.CreateJob(
    "myJob",
    new PoolInformation { PoolId = "myPool" });

// Create reference toohello linked Azure Storage account
CloudStorageAccount linkedStorageAccount =
    new CloudStorageAccount(myCredentials, true);

// Create hello blob storage container for hello outputs
await job.PrepareOutputStorageAsync(linkedStorageAccount);
```

### <a name="store-task-outputs"></a><span data-ttu-id="ca549-152">Resultados de tarefas de arquivo</span><span class="sxs-lookup"><span data-stu-id="ca549-152">Store task outputs</span></span>

<span data-ttu-id="ca549-153">Agora que já preparou um contentor de armazenamento do Azure, as tarefas podem guardar contentor toohello de saída utilizando Olá [TaskOutputStorage] [ net_taskoutputstorage] encontrar a classe na biblioteca do Olá convenções de ficheiro.</span><span class="sxs-lookup"><span data-stu-id="ca549-153">Now that you've prepared a container in Azure Storage, tasks can save output toohello container by using hello [TaskOutputStorage][net_taskoutputstorage] class found in hello File Conventions library.</span></span>

<span data-ttu-id="ca549-154">No seu código de tarefas, primeiro crie um [TaskOutputStorage] [ net_taskoutputstorage] objeto, em seguida, quando a tarefa de Olá concluiu o respetivo trabalho, invoque Olá [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave tooAzure respetiva saída armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-154">In your task code, first create a [TaskOutputStorage][net_taskoutputstorage] object, then when hello task has completed its work, call hello [TaskOutputStorage][net_taskoutputstorage].[SaveAsync][net_saveasync] method toosave its output tooAzure Storage.</span></span>

```csharp
CloudStorageAccount linkedStorageAccount = new CloudStorageAccount(myCredentials);
string jobId = Environment.GetEnvironmentVariable("AZ_BATCH_JOB_ID");
string taskId = Environment.GetEnvironmentVariable("AZ_BATCH_TASK_ID");

TaskOutputStorage taskOutputStorage = new TaskOutputStorage(
    linkedStorageAccount, jobId, taskId);

/* Code tooprocess data and produce output file(s) */

await taskOutputStorage.SaveAsync(TaskOutputKind.TaskOutput, "frame_full_res.jpg");
await taskOutputStorage.SaveAsync(TaskOutputKind.TaskPreview, "frame_low_res.jpg");
```

<span data-ttu-id="ca549-155">Olá `kind` parâmetro de Olá [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método categoriza Olá persistente a ficheiros.</span><span class="sxs-lookup"><span data-stu-id="ca549-155">hello `kind` parameter of hello [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) method categorizes hello persisted files.</span></span> <span data-ttu-id="ca549-156">Existem quatro predefinidas [TaskOutputKind] [ net_taskoutputkind] tipos: `TaskOutput`, `TaskPreview`, `TaskLog`, e `TaskIntermediate.` também pode definir categorias personalizadas de saída.</span><span class="sxs-lookup"><span data-stu-id="ca549-156">There are four predefined [TaskOutputKind][net_taskoutputkind] types: `TaskOutput`, `TaskPreview`, `TaskLog`, and `TaskIntermediate.` You can also define custom categories of output.</span></span>

<span data-ttu-id="ca549-157">Estes tipos de saída permitem-lhe toospecify que tipo de saídas toolist quando consultar mais tarde o Batch para Olá persistente saídas de uma determinada tarefa.</span><span class="sxs-lookup"><span data-stu-id="ca549-157">These output types allow you toospecify which type of outputs toolist when you later query Batch for hello persisted outputs of a given task.</span></span> <span data-ttu-id="ca549-158">Por outras palavras, quando listar Olá saídas para uma tarefa, pode filtrar a lista Olá dos tipos de saída Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-158">In other words, when you list hello outputs for a task, you can filter hello list on one of hello output types.</span></span> <span data-ttu-id="ca549-159">Por exemplo, "fornecer-me Olá *pré-visualização* de saída para a tarefa *109*."</span><span class="sxs-lookup"><span data-stu-id="ca549-159">For example, "Give me hello *preview* output for task *109*."</span></span> <span data-ttu-id="ca549-160">Obter mais informações sobre a listagem e obter as saídas aparece no [obter o resultado](#retrieve-output) mais à frente artigo Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-160">More on listing and retrieving outputs appears in [Retrieve output](#retrieve-output) later in hello article.</span></span>

> [!TIP]
> <span data-ttu-id="ca549-161">Olá tipo de saída também determina onde no Olá Azure portal um determinado ficheiro aparece: *TaskOutput*-categorizados ficheiros são apresentados em **ficheiros de saída de tarefas**, e *TaskLog*ficheiros são apresentados em **registos de tarefas**.</span><span class="sxs-lookup"><span data-stu-id="ca549-161">hello output kind also determines where in hello Azure portal a particular file appears: *TaskOutput*-categorized files appear under **Task output files**, and *TaskLog* files appear under **Task logs**.</span></span>
> 
> 

### <a name="store-job-outputs"></a><span data-ttu-id="ca549-162">Saídas da tarefa de arquivo</span><span class="sxs-lookup"><span data-stu-id="ca549-162">Store job outputs</span></span>

<span data-ttu-id="ca549-163">Além disso produz toostoring tarefas, pode armazenar saídas Olá associadas uma tarefa de toda.</span><span class="sxs-lookup"><span data-stu-id="ca549-163">In addition toostoring task outputs, you can store hello outputs associated with an entire job.</span></span> <span data-ttu-id="ca549-164">Por exemplo, na tarefa de intercalação Olá de uma tarefa de composição de filmes, manter filmes Olá totalmente composto como uma saída da tarefa.</span><span class="sxs-lookup"><span data-stu-id="ca549-164">For example, in hello merge task of a movie rendering job, you could persist hello fully rendered movie as a job output.</span></span> <span data-ttu-id="ca549-165">Quando a tarefa estiver concluída, a aplicação cliente pode listar e obter Olá saídas da tarefa de Olá, e não precisa de tooquery Olá tarefas individuais.</span><span class="sxs-lookup"><span data-stu-id="ca549-165">When your job is completed, your client application can list and retrieve hello outputs for hello job, and does not need tooquery hello individual tasks.</span></span>

<span data-ttu-id="ca549-166">Armazenar o resultado da tarefa ao chamar Olá [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método e especifique Olá [JobOutputKind] [ net_joboutputkind] e nome de ficheiro:</span><span class="sxs-lookup"><span data-stu-id="ca549-166">Store job output by calling hello [JobOutputStorage][net_joboutputstorage].[SaveAsync][net_joboutputstorage_saveasync] method, and specify hello [JobOutputKind][net_joboutputkind] and filename:</span></span>

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

<span data-ttu-id="ca549-167">Tal como com Olá **TaskOutputKind** tipo para saídas de tarefas, utilize Olá [JobOutputKind] [ net_joboutputkind] tipo toocategorize uma tarefa do persistente a ficheiros.</span><span class="sxs-lookup"><span data-stu-id="ca549-167">As with hello **TaskOutputKind** type for task outputs, you use hello [JobOutputKind][net_joboutputkind] type toocategorize a job's persisted files.</span></span> <span data-ttu-id="ca549-168">Este parâmetro permite-lhe toolater consulta para um tipo específico de saída (lista).</span><span class="sxs-lookup"><span data-stu-id="ca549-168">This parameter allows you toolater query for (list) a specific type of output.</span></span> <span data-ttu-id="ca549-169">Olá **JobOutputKind** tipo inclui categorias de saída e de pré-visualização e suporta a criação de categorias personalizadas.</span><span class="sxs-lookup"><span data-stu-id="ca549-169">hello **JobOutputKind** type includes both output and preview categories, and supports creating custom categories.</span></span>

### <a name="store-task-logs"></a><span data-ttu-id="ca549-170">Registos da tarefa de arquivo</span><span class="sxs-lookup"><span data-stu-id="ca549-170">Store task logs</span></span>

<span data-ttu-id="ca549-171">Além disso toopersisting um ficheiro toodurable de armazenamento quando uma tarefa ou a tarefa estiver concluída, poderá ser necessário toopersist ficheiros que são atualizados durante a execução de Olá de uma tarefa &mdash; ficheiros de registo ou `stdout.txt` e `stderr.txt`, por exemplo.</span><span class="sxs-lookup"><span data-stu-id="ca549-171">In addition toopersisting a file toodurable storage when a task or job completes, you may need toopersist files that are updated during hello execution of a task &mdash; log files or `stdout.txt` and `stderr.txt`, for example.</span></span> <span data-ttu-id="ca549-172">Para esta finalidade, bibliotecas de convenções de ficheiro do Azure Batch Olá fornece Olá [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método.</span><span class="sxs-lookup"><span data-stu-id="ca549-172">For this purpose, hello Azure Batch File Conventions library provides hello [TaskOutputStorage][net_taskoutputstorage].[SaveTrackedAsync][net_savetrackedasync] method.</span></span> <span data-ttu-id="ca549-173">Com [SaveTrackedAsync][net_savetrackedasync], pode controlar o ficheiro de tooa atualizações no nó de Olá (com o intervalo que especificou) e manter tooAzure essas atualizações armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-173">With [SaveTrackedAsync][net_savetrackedasync], you can track updates tooa file on hello node (at an interval that you specify) and persist those updates tooAzure Storage.</span></span>

<span data-ttu-id="ca549-174">Olá seguinte fragmento de código, utilizamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` no armazenamento do Azure cada 15 segundos durante a execução de Olá da tarefa de Olá:</span><span class="sxs-lookup"><span data-stu-id="ca549-174">In hello following code snippet, we use [SaveTrackedAsync][net_savetrackedasync] tooupdate `stdout.txt` in Azure Storage every 15 seconds during hello execution of hello task:</span></span>

```csharp
TimeSpan stdoutFlushDelay = TimeSpan.FromSeconds(3);
string logFilePath = Path.Combine(
    Environment.GetEnvironmentVariable("AZ_BATCH_TASK_DIR"), "stdout.txt");

// hello primary task logic is wrapped in a using statement that sends updates to
// hello stdout.txt blob in Storage every 15 seconds while hello task code runs.
using (ITrackedSaveOperation stdout =
        await taskStorage.SaveTrackedAsync(
        TaskOutputKind.TaskLog,
        logFilePath,
        "stdout.txt",
        TimeSpan.FromSeconds(15)))
{
    /* Code tooprocess data and produce output file(s) */

    // We are tracking hello disk file toosave our standard output, but the
    // node agent may take up too3 seconds tooflush hello stdout stream to
    // disk. So give hello file a moment toocatch up.
     await Task.Delay(stdoutFlushDelay);
}
```

<span data-ttu-id="ca549-175">Olá comentado secção `Code tooprocess data and produce output file(s)` é um marcador de posição para o código de Olá que a tarefa que normalmente iria efetuar.</span><span class="sxs-lookup"><span data-stu-id="ca549-175">hello commented section `Code tooprocess data and produce output file(s)` is a placeholder for hello code that your task would normally perform.</span></span> <span data-ttu-id="ca549-176">Por exemplo, pode ter o código que transfere dados do Storage do Azure e efetua a transformação ou de cálculo no mesmo.</span><span class="sxs-lookup"><span data-stu-id="ca549-176">For example, you might have code that downloads data from Azure Storage and performs transformation or calculation on it.</span></span> <span data-ttu-id="ca549-177">Olá importante parte este fragmento é que demonstra como pode encapsular desse código, num `using` bloco tooperiodically atualizar um ficheiro com [SaveTrackedAsync][net_savetrackedasync].</span><span class="sxs-lookup"><span data-stu-id="ca549-177">hello important part of this snippet is demonstrating how you can wrap such code in a `using` block tooperiodically update a file with [SaveTrackedAsync][net_savetrackedasync].</span></span>

<span data-ttu-id="ca549-178">agente de nó Olá é um programa que é executada em cada nó no conjunto de Olá e fornece a interface de comando e controlo de Olá entre o nó de Olá e o serviço de Batch de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-178">hello node agent is a program that runs on each node in hello pool and provides hello command-and-control interface between hello node and hello Batch service.</span></span> <span data-ttu-id="ca549-179">Olá `Task.Delay` chamada é necessária no fim de Olá deste `using` tooensure de bloco que hello do agente de nó tem tempo tooflush Olá conteúdo standard out toohello stdout.txt ficheiros num nó de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-179">hello `Task.Delay` call is required at hello end of this `using` block tooensure that hello node agent has time tooflush hello contents of standard out toohello stdout.txt file on hello node.</span></span> <span data-ttu-id="ca549-180">Sem este atraso, é possível toomiss Olá último alguns segundos, de saída.</span><span class="sxs-lookup"><span data-stu-id="ca549-180">Without this delay, it is possible toomiss hello last few seconds of output.</span></span> <span data-ttu-id="ca549-181">Este atraso pode não ser necessário para todos os ficheiros.</span><span class="sxs-lookup"><span data-stu-id="ca549-181">This delay may not be required for all files.</span></span>

> [!NOTE]
> <span data-ttu-id="ca549-182">Quando ativa o ficheiro de controlo com **SaveTrackedAsync**, apenas *acrescenta* ficheiro controlado toohello são tooAzure persistente armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-182">When you enable file tracking with **SaveTrackedAsync**, only *appends* toohello tracked file are persisted tooAzure Storage.</span></span> <span data-ttu-id="ca549-183">Utilize este método apenas para o controlo não rotação dos ficheiros de registo ou outros ficheiros que são escritos toowith acrescentar a fim de toohello de operações do ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-183">Use this method only for tracking non-rotating log files or other files that are written toowith append operations toohello end of hello file.</span></span>
> 
> 

## <a name="retrieve-output-data"></a><span data-ttu-id="ca549-184">Obter dados de saída</span><span class="sxs-lookup"><span data-stu-id="ca549-184">Retrieve output data</span></span>

<span data-ttu-id="ca549-185">Ao obter o resultado persistente utilizando a biblioteca de convenções de ficheiro do Azure Batch Olá, fazê-lo de forma tarefas e tarefa-centrada.</span><span class="sxs-lookup"><span data-stu-id="ca549-185">When you retrieve your persisted output using hello Azure Batch File Conventions library, you do so in a task- and job-centric manner.</span></span> <span data-ttu-id="ca549-186">Pode pedir Olá de saída para fornecido tarefa ou sem ser necessário tooknow o caminho no Storage do Azure ou o mesmo nome do respetivo ficheiro.</span><span class="sxs-lookup"><span data-stu-id="ca549-186">You can request hello output for given task or job without needing tooknow its path in Azure Storage, or even its file name.</span></span> <span data-ttu-id="ca549-187">Em vez disso, pode pedir ficheiros de saída por tarefas ou ID de tarefa</span><span class="sxs-lookup"><span data-stu-id="ca549-187">Instead, you can request output files by task or job ID.</span></span>

<span data-ttu-id="ca549-188">Olá seguinte fragmento de código itera através de tarefas de uma tarefa, imprime algumas informações sobre os ficheiros de saída de Olá para tarefas de Olá e, em seguida, transfere os ficheiros de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-188">hello following code snippet iterates through a job's tasks, prints some information about hello output files for hello task, and then downloads its files from Storage.</span></span>

```csharp
foreach (CloudTask task in myJob.ListTasks())
{
    foreach (OutputFileReference output in
        task.OutputStorage(storageAccount).ListOutputs(
            TaskOutputKind.TaskOutput))
    {
        Console.WriteLine($"output file: {output.FilePath}");

        output.DownloadToFileAsync(
            $"{jobId}-{output.FilePath}",
            System.IO.FileMode.Create).Wait();
    }
}
```

## <a name="view-output-files-in-hello-azure-portal"></a><span data-ttu-id="ca549-189">Ver ficheiros de saída no Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ca549-189">View output files in hello Azure portal</span></span>

<span data-ttu-id="ca549-190">Olá portal do Azure apresenta os ficheiros de saída de tarefas e os registos que são tooa persistente associado conta de armazenamento do Azure utilizando Olá [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span><span class="sxs-lookup"><span data-stu-id="ca549-190">hello Azure portal displays task output files and logs that are persisted tooa linked Azure Storage account using hello [Batch File Conventions standard](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions).</span></span> <span data-ttu-id="ca549-191">Pode implementar estas convenções no Olá um idioma à escolha ou pode utilizar a biblioteca de convenções de ficheiro Olá nas suas aplicações de .NET.</span><span class="sxs-lookup"><span data-stu-id="ca549-191">You can implement these conventions yourself in hello a language of your choice, or you can use hello File Conventions library in your .NET applications.</span></span>

<span data-ttu-id="ca549-192">ecrã de Olá tooenable dos seus ficheiros de saída no portal de Olá, deve satisfazer os requisitos de Olá:</span><span class="sxs-lookup"><span data-stu-id="ca549-192">tooenable hello display of your output files in hello portal, you must satisfy hello following requirements:</span></span>

1. <span data-ttu-id="ca549-193">[Associar uma conta de armazenamento do Azure](#requirement-linked-storage-account) tooyour conta do Batch.</span><span class="sxs-lookup"><span data-stu-id="ca549-193">[Link an Azure Storage account](#requirement-linked-storage-account) tooyour Batch account.</span></span>
2. <span data-ttu-id="ca549-194">Quando a persistência de saídas de respeitar as convenções de nomenclatura toohello predefinido para ficheiros e de contentores de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-194">Adhere toohello predefined naming conventions for Storage containers and files when persisting outputs.</span></span> <span data-ttu-id="ca549-195">Pode encontrar a definição de Olá destas convenções na biblioteca de convenções de ficheiro Olá [Leia-me][github_file_conventions_readme].</span><span class="sxs-lookup"><span data-stu-id="ca549-195">You can find hello definition of these conventions in hello File Conventions library [README][github_file_conventions_readme].</span></span> <span data-ttu-id="ca549-196">Se utilizar Olá [convenções de ficheiro do Azure Batch] [ nuget_package] biblioteca toopersist o resultado, os ficheiros são mantidos toohello convenções de ficheiro padrão de acordo com.</span><span class="sxs-lookup"><span data-stu-id="ca549-196">If you use hello [Azure Batch File Conventions][nuget_package] library toopersist your output, your files are persisted according toohello File Conventions standard.</span></span>

<span data-ttu-id="ca549-197">o resultado da tarefa tooview ficheiros e inicia sessão Olá portal do Azure, navegue tarefas toohello cuja saída que está interessado, em seguida, clique em **guardados ficheiros de saída** ou **guardar registos**.</span><span class="sxs-lookup"><span data-stu-id="ca549-197">tooview task output files and logs in hello Azure portal, navigate toohello task whose output you are interested in, then click either **Saved output files** or **Saved logs**.</span></span> <span data-ttu-id="ca549-198">Esta imagem mostra Olá **guardados ficheiros de saída** para tarefas de Olá com o ID "007":</span><span class="sxs-lookup"><span data-stu-id="ca549-198">This image shows hello **Saved output files** for hello task with ID "007":</span></span>

<span data-ttu-id="ca549-199">![Painel no portal do Azure de Olá de resultados de tarefas][2]</span><span class="sxs-lookup"><span data-stu-id="ca549-199">![Task outputs blade in hello Azure portal][2]</span></span>

## <a name="code-sample"></a><span data-ttu-id="ca549-200">Exemplo de código</span><span class="sxs-lookup"><span data-stu-id="ca549-200">Code sample</span></span>

<span data-ttu-id="ca549-201">Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma das Olá [exemplos de código do Azure Batch] [ github_samples] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ca549-201">hello [PersistOutputs][github_persistoutputs] sample project is one of hello [Azure Batch code samples][github_samples] on GitHub.</span></span> <span data-ttu-id="ca549-202">Esta solução do Visual Studio demonstra como a tarefa de toopersist toouse Olá convenções de ficheiro do Azure Batch biblioteca saída toodurable armazenamento.</span><span class="sxs-lookup"><span data-stu-id="ca549-202">This Visual Studio solution demonstrates how toouse hello Azure Batch File Conventions library toopersist task output toodurable storage.</span></span> <span data-ttu-id="ca549-203">Olá toorun de exemplo, siga estes passos:</span><span class="sxs-lookup"><span data-stu-id="ca549-203">toorun hello sample, follow these steps:</span></span>

1. <span data-ttu-id="ca549-204">Projeto de Olá aberta no **Visual Studio versão 2015 ou mais recente**.</span><span class="sxs-lookup"><span data-stu-id="ca549-204">Open hello project in **Visual Studio 2015 or newer**.</span></span>
2. <span data-ttu-id="ca549-205">Adicionar o Batch e armazenamento **credenciais de contas** demasiado**AccountSettings.settings** no projeto do Olá Microsoft.</span><span class="sxs-lookup"><span data-stu-id="ca549-205">Add your Batch and Storage **account credentials** too**AccountSettings.settings** in hello Microsoft.Azure.Batch.Samples.Common project.</span></span>
3. <span data-ttu-id="ca549-206">**Criar** (mas não executam) Olá solução.</span><span class="sxs-lookup"><span data-stu-id="ca549-206">**Build** (but do not run) hello solution.</span></span> <span data-ttu-id="ca549-207">Restaure quaisquer pacotes NuGet, se lhe for pedido.</span><span class="sxs-lookup"><span data-stu-id="ca549-207">Restore any NuGet packages if prompted.</span></span>
4. <span data-ttu-id="ca549-208">Olá utilize tooupload portal do Azure um [pacote de aplicação](batch-application-packages.md) para **PersistOutputsTask**.</span><span class="sxs-lookup"><span data-stu-id="ca549-208">Use hello Azure portal tooupload an [application package](batch-application-packages.md) for **PersistOutputsTask**.</span></span> <span data-ttu-id="ca549-209">Incluir Olá `PersistOutputsTask.exe` e respetivas assemblagens dependentes no pacote. zip de Olá, ID da aplicação Olá conjunto demasiado "PersistOutputsTask" e aplicação Olá versão de pacote demasiado "1.0".</span><span class="sxs-lookup"><span data-stu-id="ca549-209">Include hello `PersistOutputsTask.exe` and its dependent assemblies in hello .zip package, set hello application ID too"PersistOutputsTask", and hello application package version too"1.0".</span></span>
5. <span data-ttu-id="ca549-210">**Iniciar** Olá (executar) **PersistOutputs** projeto.</span><span class="sxs-lookup"><span data-stu-id="ca549-210">**Start** (run) hello **PersistOutputs** project.</span></span>
6. <span data-ttu-id="ca549-211">Quando o pedido toochoose Olá persistência tecnologia toouse para em execução exemplo de Olá, introduza **1** exemplo de Olá toorun utilizando Olá convenções de ficheiro biblioteca toopersist o resultado da tarefa.</span><span class="sxs-lookup"><span data-stu-id="ca549-211">When prompted toochoose hello persistence technology toouse for running hello sample, enter **1** toorun hello sample using hello File Conventions library toopersist task output.</span></span> 

## <a name="next-steps"></a><span data-ttu-id="ca549-212">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ca549-212">Next steps</span></span>

### <a name="get-hello-batch-file-conventions-library-for-net"></a><span data-ttu-id="ca549-213">Obter a biblioteca de convenções de ficheiro Batch Olá para .NET</span><span class="sxs-lookup"><span data-stu-id="ca549-213">Get hello Batch File Conventions library for .NET</span></span>

<span data-ttu-id="ca549-214">não está disponível na biblioteca de convenções de ficheiro de Batch de Olá para .NET [NuGet][nuget_package].</span><span class="sxs-lookup"><span data-stu-id="ca549-214">hello Batch File Conventions library for .NET is available on [NuGet][nuget_package].</span></span> <span data-ttu-id="ca549-215">biblioteca de Olá expande Olá [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classes com métodos de novo.</span><span class="sxs-lookup"><span data-stu-id="ca549-215">hello library extends hello [CloudJob][net_cloudjob] and [CloudTask][net_cloudtask] classes with new methods.</span></span> <span data-ttu-id="ca549-216">Consulte também Olá [documentação de referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) da biblioteca de convenções de ficheiro Olá.</span><span class="sxs-lookup"><span data-stu-id="ca549-216">Also see hello [reference documentation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) for hello File Conventions library.</span></span>

<span data-ttu-id="ca549-217">Olá [código fonte] [ github_file_conventions] para Olá convenções de ficheiro de biblioteca está disponível no GitHub em Olá SDK do Microsoft Azure para o repositório de .NET.</span><span class="sxs-lookup"><span data-stu-id="ca549-217">hello [source code][github_file_conventions] for hello File Conventions library is available on GitHub in hello Microsoft Azure SDK for .NET repository.</span></span> 

### <a name="explore-other-approaches-for-persisting-output-data"></a><span data-ttu-id="ca549-218">Explorar outras abordagens para dados de saída persistentes</span><span class="sxs-lookup"><span data-stu-id="ca549-218">Explore other approaches for persisting output data</span></span>

- <span data-ttu-id="ca549-219">Consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md) para uma descrição geral dos dados persistentes de tarefa e tarefas.</span><span class="sxs-lookup"><span data-stu-id="ca549-219">See [Persist job and task output tooAzure Storage](batch-task-output.md) for an overview of persisting task and job data.</span></span>
- <span data-ttu-id="ca549-220">Consulte [manter tarefas dados tooAzure armazenamento com Olá API do serviço Batch](batch-task-output-files.md) toolearn como dados de saída toouse Olá API do serviço Batch toopersist.</span><span class="sxs-lookup"><span data-stu-id="ca549-220">See [Persist task data tooAzure Storage with hello Batch service API](batch-task-output-files.md) toolearn how toouse hello Batch service API toopersist output data.</span></span>

[forum_post]: https://social.msdn.microsoft.com/Forums/en-US/87b19671-1bdf-427a-972c-2af7e5ba82d9/installing-applications-and-staging-data-on-batch-compute-nodes?forum=azurebatch
[github_file_conventions]: https://github.com/Azure/azure-sdk-for-net/tree/AutoRest/src/Batch/FileConventions
[github_file_conventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
[net_batchclient]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.batchclient.aspx
[net_cloudjob]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudjob.aspx
[net_cloudstorageaccount]: https://msdn.microsoft.com/library/azure/microsoft.windowsazure.storage.cloudstorageaccount.aspx
[net_cloudtask]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.cloudtask.aspx
[net_fileconventions_readme]: https://github.com/Azure/azure-sdk-for-net/blob/AutoRest/src/Batch/FileConventions/README.md
[net_joboutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputkind.aspx
[net_joboutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.aspx
[net_joboutputstorage_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.joboutputstorage.saveasync.aspx
[net_msdn]: https://msdn.microsoft.com/library/azure/mt348682.aspx
[net_prepareoutputasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.cloudjobextensions.prepareoutputstorageasync.aspx
[net_saveasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx
[net_savetrackedasync]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.savetrackedasync.aspx
[net_taskoutputkind]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputkind.aspx
[net_taskoutputstorage]: https://msdn.microsoft.com/library/azure/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx
[nuget_manager]: https://docs.nuget.org/consume/installing-nuget
[nuget_package]: https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files
[portal]: https://portal.azure.com
[storage_explorer]: http://storageexplorer.com/

[1]: ./media/batch-task-output/task-output-01.png "Ficheiros de saída guardado e guardado seletores de registos no portal"
[2]: ./media/batch-task-output/task-output-02.png "Painel no portal do Azure de Olá de resultados de tarefas"
