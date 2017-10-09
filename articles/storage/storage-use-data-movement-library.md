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
# <a name="transfer-data-with-hello-microsoft-azure-storage-data-movement-library"></a><span data-ttu-id="bdc69-105">Transferência de dados com Olá biblioteca de movimento de dados do Microsoft Azure Storage</span><span class="sxs-lookup"><span data-stu-id="bdc69-105">Transfer Data with hello Microsoft Azure Storage Data Movement Library</span></span>

## <a name="overview"></a><span data-ttu-id="bdc69-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="bdc69-106">Overview</span></span>
<span data-ttu-id="bdc69-107">Olá biblioteca de movimento de dados do Microsoft Azure Storage é uma biblioteca de open source para várias plataformas que foi concebida para carregamento, a transferência e a cópia de Blobs de armazenamento do Azure e os ficheiros de elevado desempenho.</span><span class="sxs-lookup"><span data-stu-id="bdc69-107">hello Microsoft Azure Storage Data Movement Library is a cross-platform open source library that is designed for high performance uploading, downloading, and copying of Azure Storage Blobs and Files.</span></span> <span data-ttu-id="bdc69-108">Esta biblioteca é framework movimento de dados de núcleos de Olá que for ligado [AzCopy](storage-use-azcopy.md).</span><span class="sxs-lookup"><span data-stu-id="bdc69-108">This library is hello core data movement framework that powers [AzCopy](storage-use-azcopy.md).</span></span> <span data-ttu-id="bdc69-109">Biblioteca de movimento de dados de Olá fornece métodos convenientes que não estão disponíveis no nosso tradicional [biblioteca de clientes de armazenamento de Azure .NET](storage-dotnet-how-to-use-blobs.md).</span><span class="sxs-lookup"><span data-stu-id="bdc69-109">hello Data Movement Library provides convenient methods that aren't available in our traditional [.NET Azure Storage Client Library](storage-dotnet-how-to-use-blobs.md).</span></span> <span data-ttu-id="bdc69-110">Isto inclui Olá capacidade tooset Olá diversas operações simultâneas, controlar progresso da transferência, retome facilmente uma transferência cancelada e muito mais.</span><span class="sxs-lookup"><span data-stu-id="bdc69-110">This includes hello ability tooset hello number of parallel operations, track transfer progress, easily resume a canceled transfer, and much more.</span></span>  

<span data-ttu-id="bdc69-111">Esta biblioteca também utiliza o .NET Core, o que significa que pode utilizá-lo ao criar aplicações de .NET para Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="bdc69-111">This library also uses .NET Core, which means you can use it when building .NET apps for Windows, Linux and macOS.</span></span> <span data-ttu-id="bdc69-112">toolearn mais informações sobre .NET Core, consulte toohello [documentação do .NET Core](https://dotnet.github.io/).</span><span class="sxs-lookup"><span data-stu-id="bdc69-112">toolearn more about .NET Core, refer toohello [.NET Core documentation](https://dotnet.github.io/).</span></span> <span data-ttu-id="bdc69-113">Esta biblioteca também funciona para tradicionais aplicações de .NET Framework para o Windows.</span><span class="sxs-lookup"><span data-stu-id="bdc69-113">This library also works for traditional .NET Framework apps for Windows.</span></span> 

<span data-ttu-id="bdc69-114">Este documento demonstra como toocreate um .NET Core consola de aplicação que é executado no Windows, Linux e macOS e efetua Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="bdc69-114">This document demonstrates how toocreate a .NET Core console application that that runs on Windows, Linux, and macOS and performs hello following scenarios:</span></span>

- <span data-ttu-id="bdc69-115">Carregar ficheiros e diretórios tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bdc69-115">Upload files and directories tooBlob Storage.</span></span>
- <span data-ttu-id="bdc69-116">Defina o número de Olá de operações simultâneas ao transferir dados.</span><span class="sxs-lookup"><span data-stu-id="bdc69-116">Define hello number of parallel operations when transferring data.</span></span>
- <span data-ttu-id="bdc69-117">Progresso de transferência de dados de controlar.</span><span class="sxs-lookup"><span data-stu-id="bdc69-117">Track data transfer progress.</span></span>
- <span data-ttu-id="bdc69-118">Transferência de dados retomar cancelada.</span><span class="sxs-lookup"><span data-stu-id="bdc69-118">Resume canceled data transfer.</span></span> 
- <span data-ttu-id="bdc69-119">Copie o ficheiro do URL tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bdc69-119">Copy file from URL tooBlob Storage.</span></span> 
- <span data-ttu-id="bdc69-120">Copiar do Blob Storage tooBlob armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bdc69-120">Copy from Blob Storage tooBlob Storage.</span></span>

<span data-ttu-id="bdc69-121">**O que precisa de:**</span><span class="sxs-lookup"><span data-stu-id="bdc69-121">**What you need:**</span></span>

* [<span data-ttu-id="bdc69-122">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="bdc69-122">Visual Studio Code</span></span>](https://code.visualstudio.com/)
* <span data-ttu-id="bdc69-123">Uma [Conta do Storage do Azure](storage-create-storage-account.md#create-a-storage-account)</span><span class="sxs-lookup"><span data-stu-id="bdc69-123">An [Azure storage account](storage-create-storage-account.md#create-a-storage-account)</span></span>

> [!NOTE]
> <span data-ttu-id="bdc69-124">Este guia pressupõe que já estiver familiarizado com [Storage do Azure](https://azure.microsoft.com/services/storage/).</span><span class="sxs-lookup"><span data-stu-id="bdc69-124">This guide assumes that you are already familiar with [Azure Storage](https://azure.microsoft.com/services/storage/).</span></span> <span data-ttu-id="bdc69-125">Se não, ler Olá [introdução tooAzure armazenamento](storage-introduction.md) documentação é útil.</span><span class="sxs-lookup"><span data-stu-id="bdc69-125">If not, reading hello [Introduction tooAzure Storage](storage-introduction.md) documentation is helpful.</span></span> <span data-ttu-id="bdc69-126">Mais importante ainda, terá de demasiado[criar uma conta de armazenamento](storage-create-storage-account.md#create-a-storage-account) toostart utilizando Olá a biblioteca de movimento de dados.</span><span class="sxs-lookup"><span data-stu-id="bdc69-126">Most importantly, you need too[create a Storage account](storage-create-storage-account.md#create-a-storage-account) toostart using hello Data Movement Library.</span></span>
> 
> 

## <a name="setup"></a><span data-ttu-id="bdc69-127">Configurar</span><span class="sxs-lookup"><span data-stu-id="bdc69-127">Setup</span></span>  

1. <span data-ttu-id="bdc69-128">Visite Olá [guia de instalação do .NET Core](https://www.microsoft.com/net/core) tooinstall .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bdc69-128">Visit hello [.NET Core Installation Guide](https://www.microsoft.com/net/core) tooinstall .NET Core.</span></span> <span data-ttu-id="bdc69-129">Quando selecionar o seu ambiente, escolha a opção de linha de comandos Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc69-129">When selecting your environment, choose hello command-line option.</span></span> 
2. <span data-ttu-id="bdc69-130">A partir da linha de comandos Olá, crie um diretório para o seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bdc69-130">From hello command line, create a directory for your project.</span></span> <span data-ttu-id="bdc69-131">Navegue para este diretório, em seguida, escreva `dotnet new` projeto de consola toocreate um c#.</span><span class="sxs-lookup"><span data-stu-id="bdc69-131">Navigate into this directory, then type `dotnet new` toocreate a C# console project.</span></span>
3. <span data-ttu-id="bdc69-132">Abra este diretório no Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bdc69-132">Open this directory in Visual Studio Code.</span></span> <span data-ttu-id="bdc69-133">Este passo pode ser feito rapidamente através de linha de comandos Olá escrevendo `code .`.</span><span class="sxs-lookup"><span data-stu-id="bdc69-133">This step can be quickly done via hello command line by typing `code .`.</span></span>  
4. <span data-ttu-id="bdc69-134">Instalar Olá [c# extensão](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) de Olá Marketplace de código do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="bdc69-134">Install hello [C# extension](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp) from hello Visual Studio Code Marketplace.</span></span> <span data-ttu-id="bdc69-135">Reinicie o Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="bdc69-135">Restart Visual Studio Code.</span></span> 
5. <span data-ttu-id="bdc69-136">Neste momento, deverá ver dois pedidos.</span><span class="sxs-lookup"><span data-stu-id="bdc69-136">At this point, you should see two prompts.</span></span> <span data-ttu-id="bdc69-137">Um é adicionar "toobuild necessários recursos e depuração".</span><span class="sxs-lookup"><span data-stu-id="bdc69-137">One is for adding "required assets toobuild and debug."</span></span> <span data-ttu-id="bdc69-138">Clique em "Sim".</span><span class="sxs-lookup"><span data-stu-id="bdc69-138">Click "yes."</span></span> <span data-ttu-id="bdc69-139">Outro pedido refere-se para restaurar dependências não resolvidas.</span><span class="sxs-lookup"><span data-stu-id="bdc69-139">Another prompt is for restoring unresolved dependencies.</span></span> <span data-ttu-id="bdc69-140">Clique em "restaurar".</span><span class="sxs-lookup"><span data-stu-id="bdc69-140">Click "restore."</span></span>
6. <span data-ttu-id="bdc69-141">A aplicação agora deve conter um `launch.json` ficheiro em Olá `.vscode` diretório.</span><span class="sxs-lookup"><span data-stu-id="bdc69-141">Your application should now contain a `launch.json` file under hello `.vscode` directory.</span></span> <span data-ttu-id="bdc69-142">Neste ficheiro, alterar Olá `externalConsole` valor demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="bdc69-142">In this file, change hello `externalConsole` value too`true`.</span></span>
7. <span data-ttu-id="bdc69-143">Visual Studio Code permite-lhe toodebug aplicações de .NET Core.</span><span class="sxs-lookup"><span data-stu-id="bdc69-143">Visual Studio Code allows you toodebug .NET Core applications.</span></span> <span data-ttu-id="bdc69-144">Atingiu o `F5` toorun a aplicação e certifique-se de que a configuração está a funcionar.</span><span class="sxs-lookup"><span data-stu-id="bdc69-144">Hit `F5` toorun your application and verify that your setup is working.</span></span> <span data-ttu-id="bdc69-145">Deverá ver "Olá mundo!"</span><span class="sxs-lookup"><span data-stu-id="bdc69-145">You should see "Hello World!"</span></span> <span data-ttu-id="bdc69-146">consola toohello impressos.</span><span class="sxs-lookup"><span data-stu-id="bdc69-146">printed toohello console.</span></span> 

## <a name="add-data-movement-library-tooyour-project"></a><span data-ttu-id="bdc69-147">Adicione o projeto de tooyour da biblioteca de movimento de dados</span><span class="sxs-lookup"><span data-stu-id="bdc69-147">Add Data Movement Library tooyour project</span></span>

1. <span data-ttu-id="bdc69-148">Adicionar a versão mais recente do Olá do Olá biblioteca de movimento de dados toohello `dependencies` secção do seu `project.json` ficheiro.</span><span class="sxs-lookup"><span data-stu-id="bdc69-148">Add hello latest version of hello Data Movement Library toohello `dependencies` section of your `project.json` file.</span></span> <span data-ttu-id="bdc69-149">No momento de Olá de escrita, seria desta versão`"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span><span class="sxs-lookup"><span data-stu-id="bdc69-149">At hello time of writing, this version would be `"Microsoft.Azure.Storage.DataMovement": "0.5.0"`</span></span> 
2. <span data-ttu-id="bdc69-150">Adicionar `"portable-net45+win8"` toohello `imports` secção.</span><span class="sxs-lookup"><span data-stu-id="bdc69-150">Add `"portable-net45+win8"` toohello `imports` section.</span></span> 
3. <span data-ttu-id="bdc69-151">Numa linha deve apresentar toorestore seu projeto.</span><span class="sxs-lookup"><span data-stu-id="bdc69-151">A prompt should display toorestore your project.</span></span> <span data-ttu-id="bdc69-152">Clique no botão "restaurar" de Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc69-152">Click hello "restore" button.</span></span> <span data-ttu-id="bdc69-153">Também pode restaurar o projeto Olá linha de comandos, escrevendo o comando de Olá `dotnet restore` na raiz de Olá do seu diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="bdc69-153">You can also restore your project from hello command line by typing hello command `dotnet restore` in hello root of your project directory.</span></span>

<span data-ttu-id="bdc69-154">Modificar `project.json`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-154">Modify `project.json`:</span></span>

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

## <a name="set-up-hello-skeleton-of-your-application"></a><span data-ttu-id="bdc69-155">Configurar a estrutura de Olá da sua aplicação</span><span class="sxs-lookup"><span data-stu-id="bdc69-155">Set up hello skeleton of your application</span></span>
<span data-ttu-id="bdc69-156">Olá primeira coisa a que fazer é configurar código de "estrutura" Olá da nossa aplicação.</span><span class="sxs-lookup"><span data-stu-id="bdc69-156">hello first thing we do is set up hello "skeleton" code of our application.</span></span> <span data-ttu-id="bdc69-157">Este código solicita-numa chave de conta e o nome da conta de armazenamento e utiliza essas credenciais toocreate um `CloudStorageAccount` objeto.</span><span class="sxs-lookup"><span data-stu-id="bdc69-157">This code prompts us for a Storage account name and account key and uses those credentials toocreate a `CloudStorageAccount` object.</span></span> <span data-ttu-id="bdc69-158">Este objeto é utilizado toointeract com a nossa conta de armazenamento em todos os cenários de transferência.</span><span class="sxs-lookup"><span data-stu-id="bdc69-158">This object is used toointeract with our Storage account in all transfer scenarios.</span></span> <span data-ttu-id="bdc69-159">código de Olá também pede-lhe-na tipo de Olá toochoose da operação de transferência Gostaríamos tooexecute.</span><span class="sxs-lookup"><span data-stu-id="bdc69-159">hello code also prompts us toochoose hello type of transfer operation we would like tooexecute.</span></span> 

<span data-ttu-id="bdc69-160">Modificar `Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-160">Modify `Program.cs`:</span></span>

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

## <a name="transfer-local-file-tooazure-blob"></a><span data-ttu-id="bdc69-161">Transferência de ficheiros local tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="bdc69-161">Transfer local file tooAzure Blob</span></span>
<span data-ttu-id="bdc69-162">Adicionar métodos de Olá `GetSourcePath` e `GetBlob` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-162">Add hello methods `GetSourcePath` and `GetBlob` too`Program.cs`:</span></span>

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

<span data-ttu-id="bdc69-163">Modificar Olá `TransferLocalFileToAzureBlob` método:</span><span class="sxs-lookup"><span data-stu-id="bdc69-163">Modify hello `TransferLocalFileToAzureBlob` method:</span></span>

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

<span data-ttu-id="bdc69-164">Este código pede-lhe-nos ficheiros locais do Olá caminho tooa, Olá nome de um contentor de novo ou existente e Olá nome de um blob de novo.</span><span class="sxs-lookup"><span data-stu-id="bdc69-164">This code prompts us for hello path tooa local file, hello name of a new or existing container, and hello name of a new blob.</span></span> <span data-ttu-id="bdc69-165">Olá `TransferManager.UploadAsync` método efetua carregamento Olá utilizando estas informações.</span><span class="sxs-lookup"><span data-stu-id="bdc69-165">hello `TransferManager.UploadAsync` method performs hello upload using this information.</span></span> 

<span data-ttu-id="bdc69-166">Atingiu o `F5` toorun a aplicação.</span><span class="sxs-lookup"><span data-stu-id="bdc69-166">Hit `F5` toorun your application.</span></span> <span data-ttu-id="bdc69-167">Pode verificar que carregamento Olá Ocorreu visualizando a sua conta de armazenamento com Olá [Explorador de armazenamento do Microsoft Azure](http://storageexplorer.com/).</span><span class="sxs-lookup"><span data-stu-id="bdc69-167">You can verify that hello upload occurred by viewing your Storage account with hello [Microsoft Azure Storage Explorer](http://storageexplorer.com/).</span></span>

## <a name="set-number-of-parallel-operations"></a><span data-ttu-id="bdc69-168">Número de conjunto de operações simultâneas</span><span class="sxs-lookup"><span data-stu-id="bdc69-168">Set number of parallel operations</span></span>
<span data-ttu-id="bdc69-169">Uma funcionalidade excelente oferecidas pelo Olá que biblioteca de movimento de dados é Olá capacidade tooset Olá diversas débito de transferência de dados de Olá tooincrease operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="bdc69-169">A great feature offered by hello Data Movement Library is hello ability tooset hello number of parallel operations tooincrease hello data transfer throughput.</span></span> <span data-ttu-id="bdc69-170">Por predefinição, Olá biblioteca de movimento de dados define o número de Olá de operações simultâneas too8 * Olá número de núcleos no seu computador.</span><span class="sxs-lookup"><span data-stu-id="bdc69-170">By default, hello Data Movement Library sets hello number of parallel operations too8 * hello number of cores on your machine.</span></span> 

<span data-ttu-id="bdc69-171">Tenha em atenção que muitas operações simultâneas num ambiente de largura de banda baixa podem sobrecarregar a ligação de rede Olá e, na verdade, impedir operações totalmente conclusão.</span><span class="sxs-lookup"><span data-stu-id="bdc69-171">Keep in mind that many parallel operations in a low-bandwidth environment may overwhelm hello network connection and actually prevent operations from fully completing.</span></span> <span data-ttu-id="bdc69-172">Irá precisar tooexperiment com esta definição toodetermine o que funciona melhor com base na sua largura de banda de rede disponível.</span><span class="sxs-lookup"><span data-stu-id="bdc69-172">You'll need tooexperiment with this setting toodetermine what works best based on your available network bandwidth.</span></span> 

<span data-ttu-id="bdc69-173">Vamos adicionar algum código que nos permite tooset Olá diversas operações simultâneas.</span><span class="sxs-lookup"><span data-stu-id="bdc69-173">Let's add some code that allows us tooset hello number of parallel operations.</span></span> <span data-ttu-id="bdc69-174">Vamos adicionar código vezes quanto tempo demora para Olá transferência toocomplete também.</span><span class="sxs-lookup"><span data-stu-id="bdc69-174">Let's also add code that times how long it takes for hello transfer toocomplete.</span></span>

<span data-ttu-id="bdc69-175">Adicionar um `SetNumberOfParallelOperations` método demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-175">Add a `SetNumberOfParallelOperations` method too`Program.cs`:</span></span>

```csharp
public static void SetNumberOfParallelOperations()
{
    Console.WriteLine("\nHow many parallel operations would you like toouse?");
    string parallelOperations = Console.ReadLine();
    TransferManager.Configurations.ParallelOperations = int.Parse(parallelOperations);
}
```

<span data-ttu-id="bdc69-176">Modificar Olá `ExecuteChoice` método toouse `SetNumberOfParallelOperations`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-176">Modify hello `ExecuteChoice` method toouse `SetNumberOfParallelOperations`:</span></span>

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

<span data-ttu-id="bdc69-177">Modificar Olá `TransferLocalFileToAzureBlob` método toouse um temporizador:</span><span class="sxs-lookup"><span data-stu-id="bdc69-177">Modify hello `TransferLocalFileToAzureBlob` method toouse a timer:</span></span>

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

## <a name="track-transfer-progress"></a><span data-ttu-id="bdc69-178">Progresso da transferência de controlar</span><span class="sxs-lookup"><span data-stu-id="bdc69-178">Track transfer progress</span></span>
<span data-ttu-id="bdc69-179">É ótimo saber quanto tempo demorou para o nosso tootransfer de dados.</span><span class="sxs-lookup"><span data-stu-id="bdc69-179">Knowing how long it took for our data tootransfer is great.</span></span> <span data-ttu-id="bdc69-180">No entanto, a ser toosee capaz de progresso de Olá do nosso transferência *durante* operação de transferência de Olá seria ainda mais.</span><span class="sxs-lookup"><span data-stu-id="bdc69-180">However, being able toosee hello progress of our transfer *during* hello transfer operation would be even better.</span></span> <span data-ttu-id="bdc69-181">tooachieve neste cenário, é necessário toocreate um `TransferContext` objeto.</span><span class="sxs-lookup"><span data-stu-id="bdc69-181">tooachieve this scenario, we need toocreate a `TransferContext` object.</span></span> <span data-ttu-id="bdc69-182">Olá `TransferContext` objeto é fornecido em dois formatos: `SingleTransferContext` e `DirectoryTransferContext`.</span><span class="sxs-lookup"><span data-stu-id="bdc69-182">hello `TransferContext` object comes in two forms: `SingleTransferContext` and `DirectoryTransferContext`.</span></span> <span data-ttu-id="bdc69-183">Olá anteriores é para transferir um único ficheiro (que é que podemos estiver a fazer agora) e Olá esta última opção é para transferir um diretório de ficheiros (que iremos adicionar mais tarde).</span><span class="sxs-lookup"><span data-stu-id="bdc69-183">hello former is for transferring a single file (which is what we're doing now) and hello latter is for transferring a directory of files (which we are adding later).</span></span>

<span data-ttu-id="bdc69-184">Adicionar métodos de Olá `GetSingleTransferContext` e `GetDirectoryTransferContext` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-184">Add hello methods `GetSingleTransferContext` and `GetDirectoryTransferContext` too`Program.cs`:</span></span> 

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

<span data-ttu-id="bdc69-185">Modificar Olá `TransferLocalFileToAzureBlob` método toouse `GetSingleTransferContext`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-185">Modify hello `TransferLocalFileToAzureBlob` method toouse `GetSingleTransferContext`:</span></span>

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

## <a name="resume-a-canceled-transfer"></a><span data-ttu-id="bdc69-186">Retomar uma transferência cancelada</span><span class="sxs-lookup"><span data-stu-id="bdc69-186">Resume a canceled transfer</span></span>
<span data-ttu-id="bdc69-187">Outra funcionalidade conveniente oferecida pelo Olá biblioteca de movimento de dados é Olá capacidade tooresume uma transferência cancelada.</span><span class="sxs-lookup"><span data-stu-id="bdc69-187">Another convenient feature offered by hello Data Movement Library is hello ability tooresume a canceled transfer.</span></span> <span data-ttu-id="bdc69-188">Vamos adicionar algum código que nos permite tootemporarily Cancelar Olá transferência escrevendo `c`e, em seguida, retome a transferência de Olá 3 segundos mais tarde.</span><span class="sxs-lookup"><span data-stu-id="bdc69-188">Let's add some code that allows us tootemporarily cancel hello transfer by typing `c`, and then resume hello transfer 3 seconds later.</span></span>

<span data-ttu-id="bdc69-189">Modificar `TransferLocalFileToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-189">Modify `TransferLocalFileToAzureBlob`:</span></span>

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

<span data-ttu-id="bdc69-190">Até agora, nosso `checkpoint` sempre o valor tiver sido definido demasiado`null`.</span><span class="sxs-lookup"><span data-stu-id="bdc69-190">Up until now, our `checkpoint` value has always been set too`null`.</span></span> <span data-ttu-id="bdc69-191">Agora, se é cancelado transferência Olá, vamos obter Olá último ponto de verificação do nosso de transferência, em seguida, utilizar este novo ponto de verificação no nosso contexto de transferência.</span><span class="sxs-lookup"><span data-stu-id="bdc69-191">Now, if we cancel hello transfer, we retrieve hello last checkpoint of our transfer, then use this new checkpoint in our transfer context.</span></span> 

## <a name="transfer-local-directory-tooazure-blob-directory"></a><span data-ttu-id="bdc69-192">Transferência de diretórios do diretório local tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="bdc69-192">Transfer local directory tooAzure Blob directory</span></span>
<span data-ttu-id="bdc69-193">Seria disappointing se Olá biblioteca de movimento de dados só foi possível transferir um ficheiro de cada vez.</span><span class="sxs-lookup"><span data-stu-id="bdc69-193">It would be disappointing if hello Data Movement Library could only transfer one file at a time.</span></span> <span data-ttu-id="bdc69-194">Luckily, não for este caso de Olá.</span><span class="sxs-lookup"><span data-stu-id="bdc69-194">Luckily, this is not hello case.</span></span> <span data-ttu-id="bdc69-195">Biblioteca de movimento de dados de Olá fornece Olá capacidade tootransfer um diretório de ficheiros e todos os seus subdiretórios.</span><span class="sxs-lookup"><span data-stu-id="bdc69-195">hello Data Movement Library provides hello ability tootransfer a directory of files and all of its subdirectories.</span></span> <span data-ttu-id="bdc69-196">Vamos adicionar algum código que nos permite toodo mesmo.</span><span class="sxs-lookup"><span data-stu-id="bdc69-196">Let's add some code that allows us toodo just that.</span></span>

<span data-ttu-id="bdc69-197">Em primeiro lugar, adicione o método de Olá `GetBlobDirectory` demasiado`Program.cs`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-197">First, add hello method `GetBlobDirectory` too`Program.cs`:</span></span>

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

<span data-ttu-id="bdc69-198">Em seguida, modificar `TransferLocalDirectoryToAzureBlobDirectory`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-198">Then, modify `TransferLocalDirectoryToAzureBlobDirectory`:</span></span>

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

<span data-ttu-id="bdc69-199">Existem algumas diferenças entre este método e o método de Olá para carregar um único ficheiro.</span><span class="sxs-lookup"><span data-stu-id="bdc69-199">There are a few differences between this method and hello method for uploading a single file.</span></span> <span data-ttu-id="bdc69-200">Estamos a utilizar agora `TransferManager.UploadDirectoryAsync` e Olá `getDirectoryTransferContext` método criámos anteriormente.</span><span class="sxs-lookup"><span data-stu-id="bdc69-200">We're now using `TransferManager.UploadDirectoryAsync` and hello `getDirectoryTransferContext` method we created earlier.</span></span> <span data-ttu-id="bdc69-201">Além disso, atualmente, fornecemos uma `options` valor operação de carregamento de tooour, que nos permite tooindicate que queremos tooinclude subdiretórios no nosso carregamento.</span><span class="sxs-lookup"><span data-stu-id="bdc69-201">In addition, we now provide an `options` value tooour upload operation, which allows us tooindicate that we want tooinclude subdirectories in our upload.</span></span> 

## <a name="copy-file-from-url-tooazure-blob"></a><span data-ttu-id="bdc69-202">Copie o ficheiro do URL tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="bdc69-202">Copy file from URL tooAzure Blob</span></span>
<span data-ttu-id="bdc69-203">Agora, vamos adicionar código que nos permite toocopy um ficheiro a partir de um URL de tooan Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc69-203">Now, let's add code that allows us toocopy a file from a URL tooan Azure Blob.</span></span> 

<span data-ttu-id="bdc69-204">Modificar `TransferUrlToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-204">Modify `TransferUrlToAzureBlob`:</span></span>

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

<span data-ttu-id="bdc69-205">Um caso de utilização importantes para esta funcionalidade é quando precisar de toomove dados a partir de outro tooAzure de serviço (por exemplo, AWS) na nuvem.</span><span class="sxs-lookup"><span data-stu-id="bdc69-205">One important use case for this feature is when you need toomove data from another cloud service (e.g. AWS) tooAzure.</span></span> <span data-ttu-id="bdc69-206">Desde que tenha um URL que permite aceder a recursos de toohello, podem mover facilmente o recurso de em Blobs do Azure utilizando Olá `TransferManager.CopyAsync` método.</span><span class="sxs-lookup"><span data-stu-id="bdc69-206">As long as you have a URL that gives you access toohello resource, you can easily move that resource into Azure Blobs by using hello `TransferManager.CopyAsync` method.</span></span> <span data-ttu-id="bdc69-207">Este método também introduz um novo parâmetro booleano.</span><span class="sxs-lookup"><span data-stu-id="bdc69-207">This method also introduces a new boolean parameter.</span></span> <span data-ttu-id="bdc69-208">Definir este parâmetro demasiado`true` indica que queremos cópia toodo um assíncrono lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="bdc69-208">Setting this parameter too`true` indicates that we want toodo an asynchronous server-side copy.</span></span> <span data-ttu-id="bdc69-209">Definir este parâmetro demasiado`false` indica uma cópia síncrona - o que significa que o recurso de Olá é máquina local tooour transferidos em primeiro lugar, em seguida, carregado tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="bdc69-209">Setting this parameter too`false` indicates a synchronous copy - meaning hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="bdc69-210">No entanto, copiar síncrona atualmente só está disponível para copiar a partir de um tooanother de recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc69-210">However, synchronous copy is currently only available for copying from one Azure Storage resource tooanother.</span></span> 

## <a name="transfer-azure-blob-tooazure-blob"></a><span data-ttu-id="bdc69-211">Transferência de Blob do Azure tooAzure Blob</span><span class="sxs-lookup"><span data-stu-id="bdc69-211">Transfer Azure Blob tooAzure Blob</span></span>
<span data-ttu-id="bdc69-212">Outra funcionalidade exclusivamente fornecida pelo Olá biblioteca de movimento de dados é Olá toocopy de capacidade de um tooanother de recursos de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="bdc69-212">Another feature that's uniquely provided by hello Data Movement Library is hello ability toocopy from one Azure Storage resource tooanother.</span></span> 

<span data-ttu-id="bdc69-213">Modificar `TransferAzureBlobToAzureBlob`:</span><span class="sxs-lookup"><span data-stu-id="bdc69-213">Modify `TransferAzureBlobToAzureBlob`:</span></span>

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

<span data-ttu-id="bdc69-214">Neste exemplo, iremos definir o parâmetro booleano Olá `TransferManager.CopyAsync` demasiado`false` tooindicate que queremos toodo uma cópia síncrona.</span><span class="sxs-lookup"><span data-stu-id="bdc69-214">In this example, we set hello boolean parameter in `TransferManager.CopyAsync` too`false` tooindicate that we want toodo a synchronous copy.</span></span> <span data-ttu-id="bdc69-215">Isto significa que recursos Olá é primeiro transferida tooour computador local, em seguida, carregado tooAzure Blob.</span><span class="sxs-lookup"><span data-stu-id="bdc69-215">This means that hello resource is downloaded tooour local machine first, then uploaded tooAzure Blob.</span></span> <span data-ttu-id="bdc69-216">opção de cópia síncrona Olá é tooensure uma excelente forma que a operação de cópia tem uma velocidade de consistente.</span><span class="sxs-lookup"><span data-stu-id="bdc69-216">hello synchronous copy option is a great way tooensure that your copy operation has a consistent speed.</span></span> <span data-ttu-id="bdc69-217">Em contrapartida, velocidade de Olá de uma cópia assíncrona do lado do servidor está dependente de Olá largura de banda disponível no servidor de Olá, que pode variam.</span><span class="sxs-lookup"><span data-stu-id="bdc69-217">In contrast, hello speed of an asynchronous server-side copy is dependent on hello available network bandwidth on hello server, which can fluctuate.</span></span> <span data-ttu-id="bdc69-218">No entanto, síncrona cópia poderá gerar a saída adicionais custos comparadas tooasynchronous cópia.</span><span class="sxs-lookup"><span data-stu-id="bdc69-218">However, synchronous copy may generate additional egress cost compared tooasynchronous copy.</span></span> <span data-ttu-id="bdc69-219">Olá recomendado abordagem é toouse cópia síncrona numa VM do Azure que está a ser Olá mesma região que o custo de saída tooavoid de conta de armazenamento de origem.</span><span class="sxs-lookup"><span data-stu-id="bdc69-219">hello recommended approach is toouse synchronous copy in an Azure VM that is in hello same region as your source storage account tooavoid egress cost.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bdc69-220">Conclusão</span><span class="sxs-lookup"><span data-stu-id="bdc69-220">Conclusion</span></span>
<span data-ttu-id="bdc69-221">A nossa aplicação de movimento de dados está agora concluída.</span><span class="sxs-lookup"><span data-stu-id="bdc69-221">Our data movement application is now complete.</span></span> <span data-ttu-id="bdc69-222">[exemplo de código completo de Olá está disponível no GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span><span class="sxs-lookup"><span data-stu-id="bdc69-222">[hello full code sample is available on GitHub](https://github.com/azure-samples/storage-dotnet-data-movement-library-app).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="bdc69-223">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bdc69-223">Next steps</span></span>
<span data-ttu-id="bdc69-224">Nesta Introdução, criámos uma aplicação que interage com o Storage do Azure e é executado no Windows, Linux e macOS.</span><span class="sxs-lookup"><span data-stu-id="bdc69-224">In this getting started, we created an application that interacts with Azure Storage and runs on Windows, Linux, and macOS.</span></span> <span data-ttu-id="bdc69-225">Esta introdução focado no armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="bdc69-225">This getting started focused on Blob Storage.</span></span> <span data-ttu-id="bdc69-226">No entanto, este mesmo conhecimento pode ser aplicado tooFile armazenamento.</span><span class="sxs-lookup"><span data-stu-id="bdc69-226">However, this same knowledge can be applied tooFile Storage.</span></span> <span data-ttu-id="bdc69-227">toolearn mais, veja [documentação de referência da biblioteca de movimento de dados de armazenamento do Azure](https://azure.github.io/azure-storage-net-data-movement).</span><span class="sxs-lookup"><span data-stu-id="bdc69-227">toolearn more, check out [Azure Storage Data Movement Library reference documentation](https://azure.github.io/azure-storage-net-data-movement).</span></span>

[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]




