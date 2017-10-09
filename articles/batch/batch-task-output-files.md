---
title: "aaaPersist tarefas e saída tooAzure armazenamento com Olá API do serviço Azure Batch | Microsoft Docs"
description: "Saiba como tarefas de lote de toopersist toouse API do serviço Batch e tarefa tooAzure armazenamento de saída."
services: batch
author: tamram
manager: timlt
editor: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 06/16/2017
ms.author: tamram
ms.openlocfilehash: 71b3f7c0dda2d2a9d8eb3eef83229873c70ca22c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="persist-task-data-tooazure-storage-with-hello-batch-service-api"></a>Manter tarefas dados tooAzure armazenamento com Olá API do serviço de Batch

[!INCLUDE [batch-task-output-include](../../includes/batch-task-output-include.md)]

A partir da versão de 2017-05-01, Olá API do serviço Batch suporta persistentes tooAzure de dados de saída armazenamento para tarefas e tarefas de Gestor de tarefas que são executadas em conjuntos com a configuração da máquina virtual Olá. Quando adiciona uma tarefa, pode especificar um contentor no armazenamento do Azure como destino de Olá para o resultado da tarefa de Olá. serviço de Batch de Olá, em seguida, qualquer contentor de toothat de dados de saída quando escreve Olá tarefa estar concluída.

Um Olá de toousing partido Batch resultado da tarefa do serviço API toopersist é que não precisa de aplicação Olá toomodify Olá tarefas está em execução. Em vez disso, com a aplicação de cliente de tooyour de algumas alterações simples, pode manter uma saída da tarefa de Olá da dentro do código de Olá que cria a tarefa de Olá.   

## <a name="when-do-i-use-hello-batch-service-api-toopersist-task-output"></a>Quando utilizar o resultado da tarefa toopersist Olá API do serviço de Batch?

O Azure Batch fornece mais de uma forma toopersist o resultado da tarefa. A utilização de Olá API do serviço de Batch é uma abordagem conveniente que é melhor se adequam toothese cenários:

- Pretende toowrite código toopersist o resultado da tarefa de dentro da sua aplicação de cliente, sem modificar aplicação Olá que está a executar a tarefa.
- Pretende toopersist saída de tarefas de lote e o Gestor de tarefas em conjuntos criados com a configuração da máquina virtual Olá.
- Pretende que o contentor de armazenamento do Azure do toopersist saída tooan com um nome arbitrário.
- Pretende toopersist saída tooan Storage do Azure contentor com o nome de acordo com toohello [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). 

Se o seu cenário difere de acordo com os listado acima, poderá ser necessário tooconsider uma abordagem diferente. Por exemplo, API do serviço de Batch de Olá não suporta atualmente transmissão em fluxo de saída de tooAzure armazenamento durante a execução Olá tarefa. toostream de saída, considere utilizar a biblioteca de convenções de ficheiro Batch Olá, disponível para o .NET. Para outros idiomas, terá de tooimplement sua própria solução. Para obter mais informações sobre outras opções para persistentes resultado da tarefa, consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md). 

## <a name="create-a-container-in-azure-storage"></a>Criar um contentor de armazenamento do Azure

tarefa toopersist saída tooAzure armazenamento, terá de toocreate um contentor que funciona como destino de Olá para os ficheiros de saída. Crie contentor de Olá antes de executar a tarefa, preferencialmente, antes de submeter a tarefa. contentor de Olá toocreate, a biblioteca de clientes de armazenamento do Azure adequada do utilize Olá ou o SDK. Para obter mais informações sobre as APIs de armazenamento do Azure, consulte Olá [documentação do Storage do Azure](https://docs.microsoft.com/azure/storage/).

Por exemplo, se estiver a escrever a aplicação em c#, utilizar Olá [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/). Olá seguinte exemplo mostra como toocreate um contentor:

```csharp
CloudBlobContainer container = storageAccount.CreateCloudBlobClient().GetContainerReference(containerName);
await conainer.CreateIfNotExists();
```

## <a name="get-a-shared-access-signature-for-hello-container"></a>Obter uma assinatura de acesso partilhado do contentor de Olá

Depois de criar o contentor de Olá, obtenha uma assinatura de acesso partilhado (SAS) com acesso de escrita toohello contentor. Uma SAS fornece o contentor de toohello acesso delegado. Olá SAS concede acesso com um conjunto especificado de permissões e ao longo de um intervalo de tempo especificado. Olá serviço Batch tem um SAS com o contentor de toohello de saída de tarefas toowrite permissões escrita. Para obter mais informações sobre SAS, consulte [utilizar assinaturas de acesso partilhado \(SAS\) no armazenamento do Azure](../storage/common/storage-dotnet-shared-access-signature-part-1.md).

Quando obtiver um SAS com Olá APIs de armazenamento do Azure, Olá API devolve uma cadeia de token SAS. Esta cadeia token inclui todos os parâmetros de Olá SAS, incluindo permissões Olá e o intervalo de Olá ao longo do que Olá SAS é válido. toouse Olá SAS tooaccess um contentor de armazenamento do Azure, terá de tooappend Olá SAS a cadeia do token toohello URI do recurso. Olá URI do recurso, juntamente com Olá anexado SAS token, que fornece acesso autenticado tooAzure armazenamento.

Olá exemplo seguinte mostra como tooget uma SAS só de escrita a cadeia do token para o contentor de Olá, em seguida, acrescenta contentor de toohello Olá SAS URI:

```csharp
string containerSasToken = container.GetSharedAccessSignature(new SharedAccessBlobPolicy()
{
    SharedAccessExpiryTime = DateTimeOffset.UtcNow.AddDays(1),
    Permissions = SharedAccessBlobPermissions.Write
});

string containerSasUrl = container.Uri.AbsoluteUri + containerSasToken; 
```

## <a name="specify-output-files-for-task-output"></a>Especificar os ficheiros de saída de resultado da tarefa

ficheiros de saída toospecify para uma tarefa, criar uma coleção de [OutputFile](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile) objetos e atribua-lhe toohello [CloudTask.OutputFiles](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.cloudtask.outputfiles#Microsoft_Azure_Batch_CloudTask_OutputFiles) propriedade quando criar tarefas de Olá. 

Olá seguinte exemplo de código .NET cria uma tarefa que escreve o ficheiro de tooa de números aleatórios denominado `output.txt`. exemplo de Olá cria um ficheiro de saída para `output.txt` toobe escrito toohello contentor. exemplo de Olá também cria ficheiros de saída para todos os ficheiros de registo que correspondam ao padrão de ficheiro Olá `std*.txt` (_por exemplo,_, `stdout.txt` e `stderr.txt`). URL do contentor Olá requer Olá SAS que foi criada anteriormente para o contentor de Olá. Olá serviço Batch utiliza o contentor de toohello Olá SAS tooauthenticate acesso: 

```csharp
new CloudTask(taskId, "cmd /v:ON /c \"echo off && set && (FOR /L %i IN (1,1,100000) DO (ECHO !RANDOM!)) > output.txt\"")
{
    OutputFiles = new List<OutputFile>
    {
        new OutputFile(
            filePattern: @"..\std*.txt",
            destination: new OutputFileDestination(
         new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId)),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
        new OutputFile(
            filePattern: @"output.txt",
            destination: 
         new OutputFileDestination(new OutputFileBlobContainerDestination(
                    containerUrl: containerSasUrl,
                    path: taskId + @"\output.txt")),
            uploadOptions: new OutputFileUploadOptions(
            uploadCondition: OutputFileUploadCondition.TaskCompletion)),
}
```

### <a name="specify-a-file-pattern-for-matching"></a>Especificar um padrão de ficheiro para a correspondência

Quando especificar um ficheiro de saída, pode utilizar Olá [OutputFile.FilePattern](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfile.filepattern#Microsoft_Azure_Batch_OutputFile_FilePattern) propriedade toospecify um padrão de ficheiro para a correspondência. padrão de ficheiro Olá pode corresponder zero ficheiros, um único ficheiro ou um conjunto de ficheiros que são criados pela tarefa de Olá.

Olá **FilePattern** propriedade suporta carateres universais de sistema de ficheiros padrão, tais como `*` (para recursiva não corresponde a) e `**` (para recursiva corresponde). Por exemplo, o exemplo de código Olá acima Especifica Olá ficheiro padrão toomatch `std*.txt` modo não recursivo: 

`filePattern: @"..\std*.txt"`

tooupload um único ficheiro e especificar um padrão de ficheiro com carateres não universais. Por exemplo, o exemplo de código Olá acima Especifica Olá ficheiro padrão toomatch `output.txt`:

`filePattern: @"output.txt"`

### <a name="specify-an-upload-condition"></a>Especifique uma condição de carregamento

Olá [OutputFileUploadOptions.UploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileuploadoptions.uploadcondition#Microsoft_Azure_Batch_OutputFileUploadOptions_UploadCondition) propriedade permite condicional o carregamento de ficheiros de saída. Um cenário comum é um conjunto de tooupload de ficheiros se tarefas de Olá for bem sucedida e um conjunto diferente de ficheiros se falhar. Por exemplo, poderá pretender que os ficheiros de registo verboso tooupload apenas quando a tarefa de Olá falha e sai com um código de saída diferente de zero. Da mesma forma, poderá pretender que os ficheiros de resultado tooupload apenas se a tarefa de Olá for bem sucedida, como esses ficheiros poderão estar em falta ou incompletas se Olá tarefa falhar.

Olá exemplo de código acima define Olá **UploadCondition** propriedade demasiado**TaskCompletion**. Esta definição especifica que se o ficheiro de Olá é toobe carregado após a conclusão de tarefas Olá, independentemente do valor de Olá do código de saída Olá. 

`uploadCondition: OutputFileUploadCondition.TaskCompletion`

Para outras definições, consulte Olá [OutputFileUploadCondition](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.common.outputfileuploadcondition) enum.

### <a name="disambiguate-files-with-hello-same-name"></a>Ambiguidade ficheiros com Olá mesmo nome

tarefas de Olá numa tarefa podem produzir ficheiros que tenham Olá mesmo nome. Por exemplo, `stdout.txt` e `stderr.txt` são criadas para cada tarefa que é executada uma tarefa. Uma vez cada tarefa é executada no seu próprio contexto, estes ficheiros não estão em conflito no sistema de ficheiros do nó de Olá. No entanto, quando carregar ficheiros a partir do contentor partilhados de várias tarefas tooa, terá de ficheiros de toodisambiguate com Olá mesmo nome.

Olá [OutputFileBlobContainerDestination.Path](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination.path#Microsoft_Azure_Batch_OutputFileBlobContainerDestination_Path) propriedade especifica o blob de destino Olá ou diretório virtual para ficheiros de saída. Pode utilizar Olá **caminho** blob de Olá tooname de propriedade ou o diretório virtual de forma a que os ficheiros de saída com Olá mesmo nome exclusivamente são denominados no armazenamento do Azure. Com o ID de tarefa Olá no caminho de Olá é uma boa forma tooensure os nomes exclusivos de e identificar facilmente os ficheiros.

Se hello **FilePattern** propriedade está definida a expressão com carateres universais de tooa, em seguida, todos os ficheiros que correspondam ao padrão Olá são carregados toohello diretório virtual especificado pelo Olá **caminho** propriedade. Por exemplo, se hello contentor é `mycontainer`, tarefas Olá ID é `mytask`, e Olá padrão de ficheiro é `..\std*.txt`, em seguida, Olá absoluto URIs toohello ficheiros de saída no armazenamento do Azure será semelhantes a:

```
https://myaccount.blob.core.windows.net/mycontainer/mytask/stderr.txt
https://myaccount.blob.core.windows.net/mycontainer/mytask/stdout.txt
```

Se hello **FilePattern** propriedade é o conjunto toomatch um nome de ficheiro único, que significa que não contém quaisquer carateres universais, Olá, em seguida, o valor de Olá **caminho** propriedade especifica o nome do blob completamente qualificado de Olá . Se prevê a atribuição de nome entra em conflito com um único ficheiro de várias tarefas, em seguida, inclua Olá nome do diretório virtual Olá como parte da toodisambiguate de nome de ficheiro Olá esses ficheiros. Por exemplo, o conjunto Olá **caminho** propriedade tooinclude Olá ID de tarefa, o caráter delimitador de Olá (normalmente, uma barra) e o nome de ficheiro Olá:

`path: taskId + @"/output.txt"`

Olá absolutos URIs toohello ficheiros de saída para um conjunto de tarefas será semelhantes a:

```
https://myaccount.blob.core.windows.net/mycontainer/task1/output.txt
https://myaccount.blob.core.windows.net/mycontainer/task2/output.txt
```

Para obter mais informações sobre os diretórios virtuais no armazenamento do Azure, consulte [listar Olá blobs num contentor](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container).


## <a name="diagnose-file-upload-errors"></a>Diagnosticar erros de carregamento de ficheiros

Se a saída de carregar ficheiros tooAzure armazenamento falhar, então tarefas Olá move toohello **concluído** estado e Olá [TaskExecutionInformation.FailureInformation](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.taskexecutioninformation.failureinformation#Microsoft_Azure_Batch_TaskExecutionInformation_FailureInformation) propriedade está definida. Examine Olá **FailureInformation** toodetermine propriedade Ocorreu o erro. Por exemplo, é um erro que ocorre no carregamento do ficheiro se não é possível localizar o contentor de Olá aqui: 

```
Category: UserError
Code: FileUploadContainerNotFound
Message: One of hello specified Azure container(s) was not found while attempting tooupload an output file
```

Em cada carregamento de ficheiros, o Batch escreve dois nós de computação toohello de ficheiros, de registo `fileuploadout.txt` e `fileuploaderr.txt`. Pode examinar estes toolearn de ficheiros de registo mais informações sobre uma falha específica. Nos casos em que carregamento do ficheiro Olá nunca tentou, por exemplo porque não foi possível executar a tarefa de Olá próprio, em seguida, estes ficheiros de registo não existirá.

## <a name="diagnose-file-upload-performance"></a>Diagnosticar o desempenho de carregamento de ficheiros

Olá `fileuploadout.txt` progresso do carregamento de registos de ficheiros. Pode examinar toolearn este ficheiro mais informações sobre quanto carrega o ficheiro estão a demorar. Tenha em atenção que existem muitos fatores coadjuvantes desempenho tooupload, incluindo o tamanho de Olá do nó de Olá, outra atividade no nó de Olá momento Olá de carregamento de Olá, se é um contentor de destino Olá no Olá mesma região que o conjunto do Batch Olá, o número de nós são a carregar a conta de armazenamento toohello em Olá mesmo tempo e assim sucessivamente.

## <a name="use-hello-batch-service-api-with-hello-batch-file-conventions-standard"></a>Utilizar a API do serviço de Batch de Olá com Olá convenções de ficheiros de lote standard

Quando a manter o resultado da tarefa com Olá API do serviço Batch, pode atribuir o nome do contentor de destino e no entanto, como de blobs. Também pode escolher tooname-las de acordo com toohello [padrão de convenções de ficheiro Batch](https://github.com/Azure/azure-sdk-for-net/tree/vs17Dev/src/SDKs/Batch/Support/FileConventions#conventions). padrão de ficheiro convenções de Olá determina Olá os nomes de contentor de destino Olá e blob no Storage do Azure para um ficheiro de saída determinado com base nos nomes de Olá de tarefas e projetos Olá. Se utilizar Olá convenções de ficheiro padrão de nomenclatura de ficheiros de saída, em seguida, os ficheiros de saída estão disponíveis para visualização nos Olá [portal do Azure](https://portal.azure.com).

Se estiver a desenvolver em c#, pode utilizar métodos de Olá construídos Olá [biblioteca convenções de ficheiro Batch para .NET](https://www.nuget.org/packages/Microsoft.Azure.Batch.Conventions.Files). Esta biblioteca cria Olá corretamente com o nome contentores e BLOBs caminhos para si. Por exemplo, pode chamar Olá API tooget Olá o nome de corretos para o contentor de Olá, com base no nome da tarefa Olá:

```csharp
string containerName = job.OutputStorageContainerName();
```

Pode utilizar Olá [CloudJobExtensions.GetOutputStorageContainerUrl](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.conventions.files.cloudjobextensions.getoutputstoragecontainerurl) método tooreturn um URL de assinatura (SAS) de acesso partilhado que é utilizado toowrite toohello contentor. Em seguida, pode passar esta toohello SAS [OutputFileBlobContainerDestination](https://docs.microsoft.com/dotnet/api/microsoft.azure.batch.outputfileblobcontainerdestination) construtor.

Se estiver a desenvolver um idioma diferente do c#, será necessário padrão do tooimplement Olá convenções de ficheiro.

## <a name="code-sample"></a>Exemplo de código

Olá [PersistOutputs] [ github_persistoutputs] projeto de exemplo é uma das Olá [exemplos de código do Azure Batch] [ github_samples] no GitHub. Esta solução do Visual Studio demonstra como a biblioteca de clientes do toouse Olá Batch para tarefas de toopersist .NET saída toodurable armazenamento. Olá toorun de exemplo, siga estes passos:

1. Projeto de Olá aberta no **Visual Studio versão 2015 ou mais recente**.
2. Adicionar o Batch e armazenamento **credenciais de contas** demasiado**AccountSettings.settings** no projeto do Olá Microsoft.
3. **Criar** (mas não executam) Olá solução. Restaure quaisquer pacotes NuGet, se lhe for pedido.
4. Olá utilize tooupload portal do Azure um [pacote de aplicação](batch-application-packages.md) para **PersistOutputsTask**. Incluir Olá `PersistOutputsTask.exe` e respetivas assemblagens dependentes no pacote. zip de Olá, ID da aplicação Olá conjunto demasiado "PersistOutputsTask" e aplicação Olá versão de pacote demasiado "1.0".
5. **Iniciar** Olá (executar) **PersistOutputs** projeto.
6. Quando o pedido toochoose Olá persistência tecnologia toouse para em execução exemplo de Olá, introduza **2** exemplo de Olá toorun utilizando o resultado da tarefa toopersist Olá API do serviço Batch.
7. Se assim o desejar, execute o exemplo de Olá novamente, introduzir **3** toopersist resultado com a API do serviço de Batch de Olá bem como tooname Olá contentor e BLOBs de caminho de destino toohello convenções de ficheiro padrão de acordo com.

## <a name="next-steps"></a>Passos seguintes

- Para obter mais informações sobre o resultado da tarefa persistentes com biblioteca de convenções de ficheiro Olá para .NET, consulte [manter tarefas e tooAzure de dados armazenamento com biblioteca de convenções de ficheiro Batch Olá para .NET toopersist ](batch-task-output-file-conventions.md).
- Para obter informações sobre outras abordagens para dados de saída persistentes no Azure Batch, consulte [manter tarefas e saída tooAzure armazenamento](batch-task-output.md).

[github_persistoutputs]: https://github.com/Azure/azure-batch-samples/tree/master/CSharp/ArticleProjects/PersistOutputs
[github_samples]: https://github.com/Azure/azure-batch-samples
