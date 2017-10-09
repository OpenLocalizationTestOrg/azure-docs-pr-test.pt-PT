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
# <a name="persist-job-and-task-data-tooazure-storage-with-hello-batch-file-conventions-library-for-net-toopersist"></a>Manter a tarefa e tarefas dados tooAzure armazenamento com biblioteca de convenções de ficheiro Batch Olá para toopersist de .NET 

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

Dados de tarefa toopersist unidirecional são toouse Olá [biblioteca convenções de ficheiro do Azure Batch para .NET][nuget_package]. Olá biblioteca convenções de ficheiros simplifica o processo de Olá do armazenamento de resultado da tarefa dados tooAzure armazenamento e obtê-lo. Pode utilizar as convenções de ficheiro de Olá biblioteca no código de tarefas e o cliente &mdash; no código de tarefas para ficheiros persistentes e no cliente code toolist e obtê-los. O código de tarefas pode também utilizar a Olá biblioteca tooretrieve Olá saída das tarefas a montante, tal como num [dependências de tarefas](batch-task-dependencies.md) cenário. 

ficheiros de biblioteca do Olá convenções de ficheiro de saída tooretrieve, pode localizar ficheiros Olá para uma determinada tarefa tarefas enumerando-los por ID e o objetivo. Não precisa de nomes de Olá tooknow ou localizações dos ficheiros de Olá. Por exemplo, pode utilizar toolist de biblioteca de convenções de ficheiro Olá todos os ficheiros intermédios de uma determinada tarefa ou obter um ficheiro de pré-visualização para uma determinada tarefa.

> [!TIP]
> A partir da versão de 2017-05-01, Olá API do serviço Batch suporta persistentes tooAzure de dados de saída armazenamento para tarefas e tarefas de Gestor de tarefas serem executadas em conjuntos criados com a configuração da máquina virtual Olá. Olá API do serviço Batch fornece um toopersist de forma simples de saída de dentro do código de Olá que cria uma tarefa e funciona como uma biblioteca de convenções de ficheiro toohello alternativo. Pode modificar a saída de toopersist de aplicações do Batch cliente sem necessitar de aplicação de Olá tooupdate que a tarefa está em execução. Para obter mais informações, consulte [manter tarefas dados tooAzure armazenamento com Olá API do serviço Batch](batch-task-output-files.md).
> 
> 

## <a name="when-do-i-use-hello-file-conventions-library-toopersist-task-output"></a>Quando utilizar o resultado da tarefa toopersist Olá convenções de ficheiro biblioteca?

O Azure Batch fornece mais de uma forma toopersist o resultado da tarefa. Olá convenções de ficheiro é melhor cenários de toothese adequada:

- Pode facilmente modificar código Olá para aplicação Olá que a tarefa está em execução ficheiros toopersist utilizando Olá convenções de ficheiro biblioteca.
- Pretende toostream dados tooAzure armazenamento enquanto a tarefa de Olá ainda está em execução.
- Pretende que os dados de toopersist em agrupamentos criados com a configuração de máquina virtual de Olá ou a configuração do serviço de nuvem de Olá.
- A aplicação cliente ou outras tarefas no Olá toolocate necessidades de tarefa e transferir ficheiros de saída de tarefas por ID ou por objetivo. 
- Pretende que o resultado da tarefa tooview no Olá portal do Azure.

Se o seu cenário difere de acordo com os listado acima, poderá ser necessário tooconsider uma abordagem diferente. Para obter mais informações sobre outras opções para persistentes resultado da tarefa, consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md). 

## <a name="what-is-hello-batch-file-conventions-standard"></a>O que é Olá convenções de ficheiro Batch padrão?

Olá [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions) fornece um esquema de nomenclatura para contentores de destino Olá e BLOBs caminhos toowhich os ficheiros de saída são escritos. Ficheiros persistente tooAzure armazenamento respeitar toohello convenções de ficheiro padrão estão automaticamente disponíveis para visualização nos Olá portal do Azure. portal de Olá tem conhecimento de convenção de nomenclatura de Olá e, por isso, pode visualizar ficheiros que cumprem tooit.

biblioteca de convenções de ficheiro Olá para .NET nomes automaticamente os ficheiros de saída de tarefas de acordo com toohello convenções de ficheiro padrão e contentores de armazenamento. biblioteca de convenções de ficheiro Olá também fornece métodos tooquery ficheiros de saída no armazenamento do Azure de acordo com o ID de toojob, o ID de tarefa ou o objetivo.   

Se estiver a desenvolver com um idioma diferente do .NET, pode implementar a norma de convenções de ficheiro Olá por si na sua aplicação. Para obter mais informações, consulte [sobre padrão de convenções de ficheiro Batch Olá](batch-task-output.md#about-the-batch-file-conventions-standard).

## <a name="link-an-azure-storage-account-tooyour-batch-account"></a>Associar um tooyour de conta do Storage do Azure conta do Batch

toopersist tooAzure de dados de saída armazenamento utilizando a biblioteca de convenções de ficheiro Olá, primeiro tem de associar uma tooyour de conta do Storage do Azure conta do Batch. Se não tiver o feito, associar um tooyour de conta de armazenamento conta do Batch, utilizando Olá [portal do Azure](https://portal.azure.com):

1. Navegue tooyour conta do Batch no Olá portal do Azure. 
2. Em **definições**, selecione **conta de armazenamento**.
3. Se ainda não tiver uma conta de armazenamento associada à sua conta do Batch, clique em **conta de armazenamento (nenhum)**.
4. Selecione uma conta de armazenamento na lista de Olá para a sua subscrição. Para melhor desempenho, utilize uma conta de armazenamento do Azure que está a ser Olá mesma região que Olá conta do Batch em que as tarefas estão em execução.

## <a name="persist-output-data"></a>Manter os dados de saída

toopersist tarefas e saída de dados com a biblioteca de convenções de ficheiro Olá, criar um contentor de armazenamento do Azure, em seguida, guardar o contentor de toohello Olá saída. Olá utilize [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage) no tarefas código tooupload Olá tarefas saída toohello contentor de. 

Para obter mais informações sobre como trabalhar com contentores e blobs no armazenamento do Azure, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).

> [!WARNING]
> Todas as saídas de tarefas e persistente com Olá convenções de ficheiros armazenados na biblioteca Olá mesmo contentor. Se um grande número de tarefas tente toopersist ficheiros em Olá mesmo tempo, [os limites de armazenamento](../storage/common/storage-performance-checklist.md#blobs) poderá ser forçado.
> 
> 

### <a name="create-storage-container"></a>Criar contentor de armazenamento

toopersist tarefas saída tooAzure armazenamento, primeiro crie um contentor chamando [CloudJob][net_cloudjob].[ PrepareOutputStorageAsync][net_prepareoutputasync]. Este método de extensão aceita um [CloudStorageAccount] [ net_cloudstorageaccount] objeto como parâmetro. Cria um contentor com o nome de acordo com toohello ficheiro convenções padrão, para que o respetivo conteúdo é detetável pelo Olá Azure métodos de obtenção portal e Olá abordados posteriormente artigo Olá.

Normalmente, coloque o Olá código toocreate um contentor na sua aplicação de cliente &mdash; Olá aplicação que cria os agrupamentos, tarefas e tarefas.

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

### <a name="store-task-outputs"></a>Resultados de tarefas de arquivo

Agora que já preparou um contentor de armazenamento do Azure, as tarefas podem guardar contentor toohello de saída utilizando Olá [TaskOutputStorage] [ net_taskoutputstorage] encontrar a classe na biblioteca do Olá convenções de ficheiro.

No seu código de tarefas, primeiro crie um [TaskOutputStorage] [ net_taskoutputstorage] objeto, em seguida, quando a tarefa de Olá concluiu o respetivo trabalho, invoque Olá [TaskOutputStorage] [ net_taskoutputstorage]. [SaveAsync] [ net_saveasync] método toosave tooAzure respetiva saída armazenamento.

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

Olá `kind` parâmetro de Olá [TaskOutputStorage](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.aspx).[ SaveAsync](https://msdn.microsoft.com/library/microsoft.azure.batch.conventions.files.taskoutputstorage.saveasync.aspx) método categoriza Olá persistente a ficheiros. Existem quatro predefinidas [TaskOutputKind] [ net_taskoutputkind] tipos: `TaskOutput`, `TaskPreview`, `TaskLog`, e `TaskIntermediate.` também pode definir categorias personalizadas de saída.

Estes tipos de saída permitem-lhe toospecify que tipo de saídas toolist quando consultar mais tarde o Batch para Olá persistente saídas de uma determinada tarefa. Por outras palavras, quando listar Olá saídas para uma tarefa, pode filtrar a lista Olá dos tipos de saída Olá. Por exemplo, "fornecer-me Olá *pré-visualização* de saída para a tarefa *109*." Obter mais informações sobre a listagem e obter as saídas aparece no [obter o resultado](#retrieve-output) mais à frente artigo Olá.

> [!TIP]
> Olá tipo de saída também determina onde no Olá Azure portal um determinado ficheiro aparece: *TaskOutput*-categorizados ficheiros são apresentados em **ficheiros de saída de tarefas**, e *TaskLog*ficheiros são apresentados em **registos de tarefas**.
> 
> 

### <a name="store-job-outputs"></a>Saídas da tarefa de arquivo

Além disso produz toostoring tarefas, pode armazenar saídas Olá associadas uma tarefa de toda. Por exemplo, na tarefa de intercalação Olá de uma tarefa de composição de filmes, manter filmes Olá totalmente composto como uma saída da tarefa. Quando a tarefa estiver concluída, a aplicação cliente pode listar e obter Olá saídas da tarefa de Olá, e não precisa de tooquery Olá tarefas individuais.

Armazenar o resultado da tarefa ao chamar Olá [JobOutputStorage][net_joboutputstorage].[ SaveAsync] [ net_joboutputstorage_saveasync] método e especifique Olá [JobOutputKind] [ net_joboutputkind] e nome de ficheiro:

```csharp
CloudJob job = new JobOutputStorage(acct, jobId);
JobOutputStorage jobOutputStorage = job.OutputStorage(linkedStorageAccount);

await jobOutputStorage.SaveAsync(JobOutputKind.JobOutput, "mymovie.mp4");
await jobOutputStorage.SaveAsync(JobOutputKind.JobPreview, "mymovie_preview.mp4");
```

Tal como com Olá **TaskOutputKind** tipo para saídas de tarefas, utilize Olá [JobOutputKind] [ net_joboutputkind] tipo toocategorize uma tarefa do persistente a ficheiros. Este parâmetro permite-lhe toolater consulta para um tipo específico de saída (lista). Olá **JobOutputKind** tipo inclui categorias de saída e de pré-visualização e suporta a criação de categorias personalizadas.

### <a name="store-task-logs"></a>Registos da tarefa de arquivo

Além disso toopersisting um ficheiro toodurable de armazenamento quando uma tarefa ou a tarefa estiver concluída, poderá ser necessário toopersist ficheiros que são atualizados durante a execução de Olá de uma tarefa &mdash; ficheiros de registo ou `stdout.txt` e `stderr.txt`, por exemplo. Para esta finalidade, bibliotecas de convenções de ficheiro do Azure Batch Olá fornece Olá [TaskOutputStorage][net_taskoutputstorage].[ SaveTrackedAsync] [ net_savetrackedasync] método. Com [SaveTrackedAsync][net_savetrackedasync], pode controlar o ficheiro de tooa atualizações no nó de Olá (com o intervalo que especificou) e manter tooAzure essas atualizações armazenamento.

Olá seguinte fragmento de código, utilizamos [SaveTrackedAsync] [ net_savetrackedasync] tooupdate `stdout.txt` no armazenamento do Azure cada 15 segundos durante a execução de Olá da tarefa de Olá:

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

Olá comentado secção `Code tooprocess data and produce output file(s)` é um marcador de posição para o código de Olá que a tarefa que normalmente iria efetuar. Por exemplo, pode ter o código que transfere dados do Storage do Azure e efetua a transformação ou de cálculo no mesmo. Olá importante parte este fragmento é que demonstra como pode encapsular desse código, num `using` bloco tooperiodically atualizar um ficheiro com [SaveTrackedAsync][net_savetrackedasync].

agente de nó Olá é um programa que é executada em cada nó no conjunto de Olá e fornece a interface de comando e controlo de Olá entre o nó de Olá e o serviço de Batch de Olá. Olá `Task.Delay` chamada é necessária no fim de Olá deste `using` tooensure de bloco que hello do agente de nó tem tempo tooflush Olá conteúdo standard out toohello stdout.txt ficheiros num nó de Olá. Sem este atraso, é possível toomiss Olá último alguns segundos, de saída. Este atraso pode não ser necessário para todos os ficheiros.

> [!NOTE]
> Quando ativa o ficheiro de controlo com **SaveTrackedAsync**, apenas *acrescenta* ficheiro controlado toohello são tooAzure persistente armazenamento. Utilize este método apenas para o controlo não rotação dos ficheiros de registo ou outros ficheiros que são escritos toowith acrescentar a fim de toohello de operações do ficheiro de Olá.
> 
> 

## <a name="retrieve-output-data"></a>Obter dados de saída

Ao obter o resultado persistente utilizando a biblioteca de convenções de ficheiro do Azure Batch Olá, fazê-lo de forma tarefas e tarefa-centrada. Pode pedir Olá de saída para fornecido tarefa ou sem ser necessário tooknow o caminho no Storage do Azure ou o mesmo nome do respetivo ficheiro. Em vez disso, pode pedir ficheiros de saída por tarefas ou ID de tarefa

Olá seguinte fragmento de código itera através de tarefas de uma tarefa, imprime algumas informações sobre os ficheiros de saída de Olá para tarefas de Olá e, em seguida, transfere os ficheiros de armazenamento.

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

## <a name="view-output-files-in-hello-azure-portal"></a>Ver ficheiros de saída no Olá portal do Azure

Olá portal do Azure apresenta os ficheiros de saída de tarefas e os registos que são tooa persistente associado conta de armazenamento do Azure utilizando Olá [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). Pode implementar estas convenções no Olá um idioma à escolha ou pode utilizar a biblioteca de convenções de ficheiro Olá nas suas aplicações de .NET.

ecrã de Olá tooenable dos seus ficheiros de saída no portal de Olá, deve satisfazer os requisitos de Olá:

1. [Associar uma conta de armazenamento do Azure](#requirement-linked-storage-account) tooyour conta do Batch.
2. Quando a persistência de saídas de respeitar as convenções de nomenclatura toohello predefinido para ficheiros e de contentores de armazenamento. Pode encontrar a definição de Olá destas convenções na biblioteca de convenções de ficheiro Olá [Leia-me][github_file_conventions_readme]. Se utilizar Olá [convenções de ficheiro do Azure Batch] [ nuget_package] biblioteca toopersist o resultado, os ficheiros são mantidos toohello convenções de ficheiro padrão de acordo com.

o resultado da tarefa tooview ficheiros e inicia sessão Olá portal do Azure, navegue tarefas toohello cuja saída que está interessado, em seguida, clique em **guardados ficheiros de saída** ou **guardar registos**. Esta imagem mostra Olá **guardados ficheiros de saída** para tarefas de Olá com o ID "007":

![Painel no portal do Azure de Olá de resultados de tarefas][2]

## <a name="code-sample"></a>Exemplo de código

Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma das Olá [exemplos de código do Azure Batch] [ github_samples] no GitHub. Esta solução do Visual Studio demonstra como a tarefa de toopersist toouse Olá convenções de ficheiro do Azure Batch biblioteca saída toodurable armazenamento. Olá toorun de exemplo, siga estes passos:

1. Projeto de Olá aberta no **Visual Studio versão 2015 ou mais recente**.
2. Adicionar o Batch e armazenamento **credenciais de contas** demasiado**AccountSettings.settings** no projeto do Olá Microsoft.
3. **Criar** (mas não executam) Olá solução. Restaure quaisquer pacotes NuGet, se lhe for pedido.
4. Olá utilize tooupload portal do Azure um [pacote de aplicação](batch-application-packages.md) para **PersistOutputsTask**. Incluir Olá `PersistOutputsTask.exe` e respetivas assemblagens dependentes no pacote. zip de Olá, ID da aplicação Olá conjunto demasiado "PersistOutputsTask" e aplicação Olá versão de pacote demasiado "1.0".
5. **Iniciar** Olá (executar) **PersistOutputs** projeto.
6. Quando o pedido toochoose Olá persistência tecnologia toouse para em execução exemplo de Olá, introduza **1** exemplo de Olá toorun utilizando Olá convenções de ficheiro biblioteca toopersist o resultado da tarefa. 

## <a name="next-steps"></a>Passos seguintes

### <a name="get-hello-batch-file-conventions-library-for-net"></a>Obter a biblioteca de convenções de ficheiro Batch Olá para .NET

não está disponível na biblioteca de convenções de ficheiro de Batch de Olá para .NET [NuGet][nuget_package]. biblioteca de Olá expande Olá [CloudJob] [ net_cloudjob] e [CloudTask] [ net_cloudtask] classes com métodos de novo. Consulte também Olá [documentação de referência](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files) da biblioteca de convenções de ficheiro Olá.

Olá [código fonte] [ github_file_conventions] para Olá convenções de ficheiro de biblioteca está disponível no GitHub em Olá SDK do Microsoft Azure para o repositório de .NET. 

### <a name="explore-other-approaches-for-persisting-output-data"></a>Explorar outras abordagens para dados de saída persistentes

- Consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md) para uma descrição geral dos dados persistentes de tarefa e tarefas.
- Consulte [manter tarefas dados tooAzure armazenamento com Olá API do serviço Batch](batch-task-output-files.md) toolearn como dados de saída toouse Olá API do serviço Batch toopersist.

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
