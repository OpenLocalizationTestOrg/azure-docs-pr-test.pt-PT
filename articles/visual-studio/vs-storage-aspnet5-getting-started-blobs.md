---
title: "aaaGet começar a utilizar o blob storage e o Visual Studio serviços ligados (ASP.NET Core) | Microsoft Docs"
description: "Como tooget iniciado utilizando o Blob storage do Azure num projeto Visual Studio ASP.NET Core depois de criar uma conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 094b596a-c92c-40c4-a0f5-86407ae79672
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 8eedf331896b21658c7b30a68a4391d8d60cd729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-aspnet-core"></a>Introdução ao Blob do Azure Visual Studio e de armazenamento ligado serviços (ASP.NET Core)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Este artigo descreve como tooget iniciado utilizando o Blob storage do Azure no Visual Studio depois de ter criado ou referenciada uma conta de armazenamento do Azure num projeto ASP.NET Core, utilizando a caixa de diálogo do Olá Visual Studio adicionar ligado serviços.

Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS. Um blob único pode ser qualquer dimensão. Os BLOBs podem ser coisas como imagens, ficheiros de áudio e vídeos, dados não processados e ficheiros do documento. Este artigo descreve como tooget ao blob storage depois de criar uma conta de armazenamento do Azure utilizando Olá Visual Studio **adicionar serviços ligados** diálogo num projeto ASP.NET Core.

Tal como em direto de ficheiros em pastas, blobs de armazenamento em direto nos contentores. Depois de ter criado um armazenamento, crie um ou mais contentores no armazenamento de Olá. Por exemplo, um armazenamento chamado "Scrapbook", pode criar contentores no armazenamento de Olá chamado imagens de toostore "imagens" e outra denominada "áudio" toostore ficheiros áudio. Depois de criar contentores de Olá, pode carregar blob individuais toothem de ficheiros. Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md) para obter mais informações sobre manipular programaticamente os blobs.

## <a name="access-blob-containers-in-code"></a>Contentores de BLOBs de acesso no código
tooprogrammatically aceder aos blobs em projetos de ASP.NET Core, terá de Olá tooadd seguintes itens, se não estiverem já presentes.

1. Adicione Olá seguir superior toohello de declarações de espaço de nomes do código de qualquer ficheiro c# em que pretende acesso tooprogrammatically storage do Azure.
   
        using Microsoft.Extensions.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Extensions.Logging.LogLevel;
2. Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Utilize Olá tooget de código a seguir a cadeia de ligação de armazenamento e as informações da configuração de serviço do Azure Olá conta de armazenamento.
   
         CloudStorageAccount storageAccount = new CloudStorageAccount(
            new Microsoft.WindowsAzure.Storage.Auth.StorageCredentials(
            "<storage-account-name>",
            "<access-key>"), true);
   
    **Nota:** utilize todas Olá acima código à frente do código Olá Olá secções a seguir.
3. Utilize um **CloudBlobClient** objeto tooget um **CloudBlobContainer** referência tooan existente num contentor na sua conta do storage.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

## <a name="create-a-container-in-code"></a>Criar um contentor no código
Também pode utilizar Olá **CloudBlobClient** toocreate um contentor na sua conta de armazenamento. Tudo o que precisa toodo é demasiado tooadd uma chamada**CreateIfNotExistsAsync** como Olá seguinte código:

    // Create a blob client.
    CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

    // Get a reference tooa container named "my-new-container."
    CloudBlobContainer container = blobClient.GetContainerReference("my-new-container");

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


**Nota:** Olá APIs que efetuar chamadas tooAzure armazenamento em ASP.NET Core são assíncronas. Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações. código de Olá abaixo parte do princípio de métodos de programação assíncrona estão a ser utilizados.

toomake Olá ficheiros Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
tooupload um ficheiro de BLOBs num contentor, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob. Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStreamAsync** método. Esta operação cria blob Olá se não estiver lá, ou substitui-lo se existir. Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.

    // Get a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with hello contents of a local file
    // named "myfile".
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        await blockBlob.UploadFromStreamAsync(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor. Em seguida, pode chamar do contentor de Olá **ListBlobsSegmentedAsync** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo. tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se não souber blob Olá escreva, pode utilizar um toodetermine de verificação do tipo que toocast para. Olá seguinte código demonstra como tooretrieve e de saída Olá URI de cada item no contentor.

    BlobContinuationToken token = null;
    do
    {
        BlobResultSegment resultSegment = await container.ListBlobsSegmentedAsync(token);
        token = resultSegment.ContinuationToken;

        foreach (IListBlobItem item in resultSegment.Results)
        {
            if (item.GetType() == typeof(CloudBlockBlob))
            {
                CloudBlockBlob blob = (CloudBlockBlob)item;
                Console.WriteLine("Block blob of length {0}: {1}", blob.Properties.Length, blob.Uri);
            }

            else if (item.GetType() == typeof(CloudPageBlob))
            {
                CloudPageBlob pageBlob = (CloudPageBlob)item;

                Console.WriteLine("Page blob of length {0}: {1}", pageBlob.Properties.Length, pageBlob.Uri);
            }

            else if (item.GetType() == typeof(CloudBlobDirectory))
            {
                CloudBlobDirectory directory = (CloudBlobDirectory)item;

                Console.WriteLine("Directory: {0}", directory.Uri);
            }
        }
    } while (token != null);

Existem outras formas toolist Olá conteúdo um contentor do blob. Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#list-the-blobs-in-a-container) para obter mais informações.

## <a name="download-a-blob"></a>Transferir um blob
toodownload um blob, obtenha primeiro um blob de toohello de referência e, em seguida, chame Olá **DownloadToStreamAsync** método. Olá exemplo seguinte utiliza Olá **DownloadToStreamAsync** método tootransfer Olá blob conteúdo tooa objeto de fluxo que, em seguida, pode guardar como um ficheiro local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save hello blob contents tooa file named "myfile".
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        await blockBlob.DownloadToStreamAsync(fileStream);
    }

Existem outras formas toosave blobs como ficheiros. Consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md#download-blobs) para obter mais informações.

## <a name="delete-a-blob"></a>Eliminar um blob
toodelete um blob, obtenha primeiro um blob de toohello de referência e, em seguida, chame Olá **DeleteAsync** método.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    await blockBlob.DeleteAsync();

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

