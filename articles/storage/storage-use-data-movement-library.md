---
title: "aaaTransfer dados com Olá biblioteca de movimento de dados do Microsoft Azure Storage | Microsoft Docs"
description: "Utilize Olá biblioteca de movimento de dados toomove ou copiar dados tooor do conteúdo de blob e o ficheiro. Copiar dados tooAzure armazenamento de ficheiros locais ou copie os dados dentro ou entre contas de armazenamento. Migre facilmente a sua tooAzure dados de armazenamento."
services: storage
documentationcenter: 
author: seguler
manager: jahogg
editor: tysonn
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 03/22/2017
ms.author: seguler
ms.openlocfilehash: 5de902d132565a8eafdc672f7a1a18e1a2db3a06
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a>Transferência de dados com Olá biblioteca de movimento de dados do Microsoft Azure Storage

## <a name="overview"></a>Descrição geral
Olá biblioteca de movimento de dados do Microsoft Azure Storage é uma biblioteca de open source para várias plataformas que foi concebida para carregamento, a transferência e a cópia de Blobs de armazenamento do Azure e os ficheiros de elevado desempenho. Esta biblioteca é framework movimento de dados de núcleos de Olá que for ligado [AzCopy](storage-use-azcopy.md). Biblioteca de movimento de dados de Olá fornece métodos convenientes que não estão disponíveis no nosso tradicional [biblioteca de clientes de armazenamento de Azure .NET](storage-dotnet-how-to-use-blobs.md). Isto inclui Olá capacidade tooset Olá diversas operações simultâneas, controlar progresso da transferência, retome facilmente uma transferência cancelada e muito mais.  

Esta biblioteca também utiliza o .NET Core, o que significa que pode utilizá-lo ao criar aplicações de .NET para Windows, Linux e macOS. toolearn mais informações sobre .NET Core, consulte toohello [documentação do .NET Core](https://dotnet.github.io/). Esta biblioteca também funciona para tradicionais aplicações de .NET Framework para o Windows. 

Este documento demonstra como toocreate um .NET Core consola de aplicação que é executado no Windows, Linux e macOS e efetua Olá os seguintes cenários:

- Carregar ficheiros e diretórios tooBlob armazenamento.
- Defina o número de Olá de operações simultâneas ao transferir dados.
- Progresso de transferência de dados de controlar.
- Transferência de dados retomar cancelada. 
- Copie o ficheiro do URL tooBlob armazenamento. 
- Copiar do Blob Storage tooBlob armazenamento.

**O que precisa de:**

* [Visual Studio Code](https://code.visualstudio.com/)
* Uma [Conta do Storage do Azure](storage-create-storage-account.md#create-a-storage-account)

> [!NOTE]
> Este guia pressupõe que já estiver familiarizado com [Storage do Azure](https://azure.microsoft.com/services/storage/). Se não, ler Olá [introdução tooAzure armazenamento](storage-introduction.md) documentação é útil. Mais importante ainda, terá de demasiado[criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) toostart utilizando Olá a biblioteca de movimento de dados.
> 
> 

## <a name="setup"></a>Configurar  

1. Visite Olá [guia de instalação do .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core. Quando selecionar o seu ambiente, escolha a opção de linha de comandos Olá. 
2. A partir da linha de comandos Olá, crie um diretório para o seu projeto. Navegue para este diretório, em seguida, escreva `dotnet new` projeto de consola toocreate um c#.
3. Abra este diretório no Visual Studio Code. Este passo pode ser feito rapidamente através de linha de comandos Olá escrevendo `code .`.  
4. Instalar Olá [c# extensão](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de Olá Marketplace de código do Visual Studio. Reinicie o Visual Studio Code. 
5. Neste momento, deverá ver dois pedidos. Um é adicionar "toobuild necessários recursos e depuração". Clique em "Sim". Outro pedido refere-se para restaurar dependências não resolvidas. Clique em "restaurar".
6. A aplicação agora deve conter um `launch.json` ficheiro em Olá `.vscode` diretório. Neste ficheiro, alterar Olá `externalConsole` valor demasiado`true`.
7. Visual Studio Code permite-lhe toodebug aplicações de .NET Core. Atingiu o `F5` toorun a aplicação e certifique-se de que a configuração está a funcionar. Deverá ver "Olá mundo!" consola toohello impressos. 

## <a name="add-data-movement-library-tooyour-project"></a>Adicione o projeto de tooyour da biblioteca de movimento de dados

1. Adicionar a versão mais recente do Olá do Olá biblioteca de movimento de dados toohello `dependencies` secção do seu `project.json` ficheiro. No momento de Olá de escrita, seria desta versão`"Microsoft.Azure.Storage.DataMovement": "0.5.0"` 
2. Adicionar `"portable-net45+win8"` toohello `imports` secção. 
3. Numa linha deve apresentar toorestore seu projeto. Clique no botão "restaurar" de Olá. Também pode restaurar o projeto Olá linha de comandos, escrevendo o comando de Olá `dotnet restore` na raiz de Olá do seu diretório do projeto.

Modificar `project.json`:

    {
      "version": "1.0.0-*",
      "buildOptions": {
        "debugType": "portable",
        "emitEntryPoint": true
      },
      "dependencies": {
        "Microsoft.Azure.Storage.DataMovement": "0.5.0"
      },
      "frameworks": {
        "netcoreapp1.1": {
          "dependencies": {
            "Microsoft.NETCore.App": {
              "type": "platform",
              "version": "1.1.0"
            }
          },
          "imports": [
            "dnxcore50",
            "portable-net45+win8"
          ]
        }
      }
    }

## <a name="set-up-hello-skeleton-of-your-application"></a>Configurar a estrutura de Olá da sua aplicação
Olá primeira coisa a que fazer é configurar código de "estrutura" Olá da nossa aplicação. Este código solicita-numa chave de conta e o nome da conta de armazenamento e utiliza essas credenciais toocreate um `CloudStorageAccount` objeto. Este objeto é utilizado toointeract com a nossa conta de armazenamento em todos os cenários de transferência. código de Olá também pede-lhe-na tipo de Olá toochoose da operação de transferência Gostaríamos tooexecute. 

Modificar `Program.cs`:

```csharp
using System;
using System.Threading;
using System.Diagnostics;
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Blob;
using Microsoft.WindowsAzure.Storage.DataMovement;

namespace DMLibSample
{
    public class Program
    {
        public static void Main()
        {
            Console.WriteLine("Enter Storage account name:");           
            string accountName = Console.ReadLine();

            Console.WriteLine("\nEnter Storage account key:");           
            string accountKey = Console.ReadLine();

            string storageConnectionString = "DefaultEndpointsProtocol=https;AccountName=" + accountName + ";AccountKey=" + accountKey;
            CloudStorageAccount account = CloudStorageAccount.Parse(storageConnectionString);

            ExecuteChoice(account);
        }

        public static void ExecuteChoice(CloudStorageAccount account)
        {
            Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
            int choice = int.Parse(Console.ReadLine());

            if(choice == 1)
            {
                TransferLocalFileToAzureBlob(account).Wait();
            }
            else if(choice == 2)
            {
                TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
            }
            else if(choice == 3)
            {
                TransferUrlToAzureBlob(account).Wait();
            }
            else if(choice == 4)
            {
                TransferAzureBlobToAzureBlob(account).Wait();
            }
        }

        public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
        { 
            
        }

        public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
        {

        }

        public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
        {

        }
    }
}
```

## <a name="transfer-local-file-tooazure-blob"></a>Transferência de ficheiros local tooAzure Blob
Adicionar métodos de Olá `GetSourcePath` e `GetBlob` demasiado`Program.cs`:

```csharp
public static string GetSourcePath()
{
    Console.WriteLine("\nProvide path for source:");
    string sourcePath = Console.ReadLine();

    return sourcePath;
}

public static CloudBlockBlob GetBlob(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    Console.WriteLine("\nProvide name of new Blob:");
    string blobName = Console.ReadLine();
    CloudBlockBlob blob = container.GetBlockBlobReference(blobName);

    return blob;
}
```

Modificar Olá `TransferLocalFileToAzureBlob` método:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    await TransferManager.UploadAsync(localFilePath, blob);
    Console.WriteLine("\nTransfer operation complete.");
    ExecuteChoice(account);
}
```

Este código pede-lhe-nos ficheiros locais do Olá caminho tooa, Olá nome de um contentor de novo ou existente e Olá nome de um blob de novo. Olá `TransferManager.UploadAsync` método efetua carregamento Olá utilizando estas informações. 

Atingiu o `F5` toorun a aplicação. Pode verificar que carregamento Olá Ocorreu visualizando a sua conta de armazenamento com Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/).

## <a name="set-number-of-parallel-operations"></a>Número de conjunto de operações simultâneas
Uma funcionalidade excelente oferecidas pelo Olá que biblioteca de movimento de dados é Olá capacidade tooset Olá diversas débito de transferência de dados de Olá tooincrease operações simultâneas. Por predefinição, Olá biblioteca de movimento de dados define o número de Olá de operações simultâneas too8 * Olá número de núcleos no seu computador. 

Tenha em atenção que muitas operações simultâneas num ambiente de largura de banda baixa podem sobrecarregar a ligação de rede Olá e, na verdade, impedir operações totalmente conclusão. Irá precisar tooexperiment com esta definição toodetermine o que funciona melhor com base na sua largura de banda de rede disponível. 

Vamos adicionar algum código que nos permite tooset Olá diversas operações simultâneas. Vamos adicionar código vezes quanto tempo demora para Olá transferência toocomplete também.

Adicionar um `SetNumberOfParallelOperations` método demasiado`Program.cs`:

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

Modificar Olá `ExecuteChoice` método toouse `SetNumberOfParallelOperations`:

```csharp
public static void ExecuteChoice(CloudStorageAccount account)
{
    Console.WriteLine("\nWhat type of transfer would you like tooexecute?\n1. Local file --> Azure Blob\n2. Local directory --> Azure Blob directory\n3. URL (e.g. Amazon S3 file) --> Azure Blob\n4. Azure Blob --> Azure Blob");
    int choice = int.Parse(Console.ReadLine());

    SetNumberOfParallelOperations();

    if(choice == 1)
    {
        TransferLocalFileToAzureBlob(account).Wait();
    }
    else if(choice == 2)
    {
        TransferLocalDirectoryToAzureBlobDirectory(account).Wait();
    }
    else if(choice == 3)
    {
        TransferUrlToAzureBlob(account).Wait();
    }
    else if(choice == 4)
    {
        TransferAzureBlobToAzureBlob(account).Wait();
    }
}
```

Modificar Olá `TransferLocalFileToAzureBlob` método toouse um temporizador:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    Console.WriteLine("\nTransfer started...");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="track-transfer-progress"></a>Progresso da transferência de controlar
É ótimo saber quanto tempo demorou para o nosso tootransfer de dados. No entanto, a ser toosee capaz de progresso de Olá do nosso transferência *durante* operação de transferência de Olá seria ainda mais. tooachieve neste cenário, é necessário toocreate um `TransferContext` objeto. Olá `TransferContext` objeto é fornecido em dois formatos: `SingleTransferContext` e `DirectoryTransferContext`. Olá anteriores é para transferir um único ficheiro (que é que podemos estiver a fazer agora) e Olá esta última opção é para transferir um diretório de ficheiros (que iremos adicionar mais tarde).

Adicionar métodos de Olá `GetSingleTransferContext` e `GetDirectoryTransferContext` demasiado`Program.cs`: 

```csharp
public static SingleTransferContext GetSingleTransferContext(TransferCheckpoint checkpoint)
{
    SingleTransferContext context = new SingleTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}

public static DirectoryTransferContext GetDirectoryTransferContext(TransferCheckpoint checkpoint)
{
    DirectoryTransferContext context = new DirectoryTransferContext(checkpoint);

    context.ProgressHandler = new Progress<TransferStatus>((progress) =>
    {
        Console.Write("\rBytes transferred: {0}", progress.BytesTransferred );
    });
    
    return context;
}
```

Modificar Olá `TransferLocalFileToAzureBlob` método toouse `GetSingleTransferContext`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account);
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint);
    Console.WriteLine("\nTransfer started...\n");
    Stopwatch stopWatch = Stopwatch.StartNew();
    await TransferManager.UploadAsync(localFilePath, blob, null, context);
    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

## <a name="resume-a-canceled-transfer"></a>Retomar uma transferência cancelada
Outra funcionalidade conveniente oferecida pelo Olá biblioteca de movimento de dados é Olá capacidade tooresume uma transferência cancelada. Vamos adicionar algum código que nos permite tootemporarily Cancelar Olá transferência escrevendo `c`e, em seguida, retome a transferência de Olá 3 segundos mais tarde.

Modificar `TransferLocalFileToAzureBlob`:

```csharp
public static async Task TransferLocalFileToAzureBlob(CloudStorageAccount account)
{ 
    string localFilePath = GetSourcePath();
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.UploadAsync(localFilePath, blob, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadAsync(localFilePath, blob, null, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Até agora, nosso `checkpoint` sempre o valor tiver sido definido demasiado`null`. Agora, se é cancelado transferência Olá, vamos obter Olá último ponto de verificação do nosso de transferência, em seguida, utilizar este novo ponto de verificação no nosso contexto de transferência. 

## <a name="transfer-local-directory-tooazure-blob-directory"></a>Transferência de diretórios do diretório local tooAzure Blob
Seria disappointing se Olá biblioteca de movimento de dados só foi possível transferir um ficheiro de cada vez. Luckily, não for este caso de Olá. Biblioteca de movimento de dados de Olá fornece Olá capacidade tootransfer um diretório de ficheiros e todos os seus subdiretórios. Vamos adicionar algum código que nos permite toodo mesmo.

Em primeiro lugar, adicione o método de Olá `GetBlobDirectory` demasiado`Program.cs`:

```csharp
public static CloudBlobDirectory GetBlobDirectory(CloudStorageAccount account)
{
    CloudBlobClient blobClient = account.CreateCloudBlobClient();

    Console.WriteLine("\nProvide name of Blob container. This can be a new or existing Blob container:");
    string containerName = Console.ReadLine();
    CloudBlobContainer container = blobClient.GetContainerReference(containerName);
    container.CreateIfNotExistsAsync().Wait();

    CloudBlobDirectory blobDirectory = container.GetDirectoryReference("");

    return blobDirectory;
}
```

Em seguida, modificar `TransferLocalDirectoryToAzureBlobDirectory`:

```csharp
public static async Task TransferLocalDirectoryToAzureBlobDirectory(CloudStorageAccount account)
{ 
    string localDirectoryPath = GetSourcePath();
    CloudBlobDirectory blobDirectory = GetBlobDirectory(account); 
    TransferCheckpoint checkpoint = null;
    DirectoryTransferContext context = GetDirectoryTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    UploadDirectoryOptions options = new UploadDirectoryOptions()
    {
        Recursive = true
    };

    try
    {
        task = TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetDirectoryTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.UploadDirectoryAsync(localDirectoryPath, blobDirectory, options, context);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Existem algumas diferenças entre este método e o método de Olá para carregar um único ficheiro. Estamos a utilizar agora `TransferManager.UploadDirectoryAsync` e Olá `getDirectoryTransferContext` método criámos anteriormente. Além disso, atualmente, fornecemos uma `options` valor operação de carregamento de tooour, que nos permite tooindicate que queremos tooinclude subdiretórios no nosso carregamento. 

## <a name="copy-file-from-url-tooazure-blob"></a>Copie o ficheiro do URL tooAzure Blob
Agora, vamos adicionar código que nos permite toocopy um ficheiro a partir de um URL de tooan Blob do Azure. 

Modificar `TransferUrlToAzureBlob`:

```csharp
public static async Task TransferUrlToAzureBlob(CloudStorageAccount account)
{
    Uri uri = new Uri(GetSourcePath());
    CloudBlockBlob blob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(uri, blob, true, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Um caso de utilização importantes para esta funcionalidade é quando precisar de toomove dados a partir de outro tooAzure de serviço (por exemplo, AWS) na nuvem. Desde que tenha um URL que permite aceder a recursos de toohello, podem mover facilmente o recurso de em Blobs do Azure utilizando Olá `TransferManager.CopyAsync` método. Este método também introduz um novo parâmetro booleano. Definir este parâmetro demasiado`true` indica que queremos cópia toodo um assíncrono lado do servidor. Definir este parâmetro demasiado`false` indica uma cópia síncrona - o que significa que o recurso de Olá é máquina local tooour transferidos em primeiro lugar, em seguida, carregado tooAzure Blob. No entanto, copiar síncrona atualmente só está disponível para copiar a partir de um tooanother de recursos de armazenamento do Azure. 

## <a name="transfer-azure-blob-tooazure-blob"></a>Transferência de Blob do Azure tooAzure Blob
Outra funcionalidade exclusivamente fornecida pelo Olá biblioteca de movimento de dados é Olá toocopy de capacidade de um tooanother de recursos de armazenamento do Azure. 

Modificar `TransferAzureBlobToAzureBlob`:

```csharp
public static async Task TransferAzureBlobToAzureBlob(CloudStorageAccount account)
{
    CloudBlockBlob sourceBlob = GetBlob(account);
    CloudBlockBlob destinationBlob = GetBlob(account); 
    TransferCheckpoint checkpoint = null;
    SingleTransferContext context = GetSingleTransferContext(checkpoint); 
    CancellationTokenSource cancellationSource = new CancellationTokenSource();
    Console.WriteLine("\nTransfer started...\nPress 'c' tootemporarily cancel your transfer...\n");

    Stopwatch stopWatch = Stopwatch.StartNew();
    Task task;
    ConsoleKeyInfo keyinfo;
    try
    {
        task = TransferManager.CopyAsync(sourceBlob, destinationBlob, true, null, context, cancellationSource.Token);
        while(!task.IsCompleted)
        {
            if(Console.KeyAvailable)
            {
                keyinfo = Console.ReadKey(true);
                if(keyinfo.Key == ConsoleKey.C)
                {
                    cancellationSource.Cancel();
                }
            }
        }
        await task;
    }
    catch(Exception e)
    {
        Console.WriteLine("\nThe transfer is canceled: {0}", e.Message);  
    }

    if(cancellationSource.IsCancellationRequested)
    {
        Console.WriteLine("\nTransfer will resume in 3 seconds...");
        Thread.Sleep(3000);
        checkpoint = context.LastCheckpoint;
        context = GetSingleTransferContext(checkpoint);
        Console.WriteLine("\nResuming transfer...\n");
        await TransferManager.CopyAsync(sourceBlob, destinationBlob, false, null, context, cancellationSource.Token);
    }

    stopWatch.Stop();
    Console.WriteLine("\nTransfer operation completed in " + stopWatch.Elapsed.TotalSeconds + " seconds.");
    ExecuteChoice(account);
}
```

Neste exemplo, iremos definir o parâmetro booleano Olá `TransferManager.CopyAsync` demasiado`false` tooindicate que queremos toodo uma cópia síncrona. Isto significa que recursos Olá é primeiro transferida tooour computador local, em seguida, carregado tooAzure Blob. opção de cópia síncrona Olá é tooensure uma excelente forma que a operação de cópia tem uma velocidade de consistente. Em contrapartida, velocidade de Olá de uma cópia assíncrona do lado do servidor está dependente de Olá largura de banda disponível no servidor de Olá, que pode variam. No entanto, síncrona cópia poderá gerar a saída adicionais custos comparadas tooasynchronous cópia. Olá recomendado abordagem é toouse cópia síncrona numa VM do Azure que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.

## <a name="conclusion"></a>Conclusão
A nossa aplicação de movimento de dados está agora concluída. [exemplo de código completo de Olá está disponível no GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app). 

## <a name="next-steps"></a>Passos seguintes
Nesta Introdução, criámos uma aplicação que interage com o Storage do Azure e é executado no Windows, Linux e macOS. Esta introdução focado no armazenamento de Blobs. No entanto, este mesmo conhecimento pode ser aplicado tooFile armazenamento. toolearn mais, veja [documentação de referência da biblioteca de movimento de dados de armazenamento do Azure](https://azure.github.io/azure-storage-net-data-movement).

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




