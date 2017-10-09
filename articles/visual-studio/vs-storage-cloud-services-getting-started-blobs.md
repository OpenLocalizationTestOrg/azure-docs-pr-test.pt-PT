---
title: "aaaGet começar a utilizar o blob storage e o Visual Studio serviços ligados (Serviços de cloud) | Microsoft Docs"
description: "Como tooget iniciado utilizando o armazenamento de Blobs do Azure num projeto de serviço em nuvem no Visual Studio depois de ligar tooa conta de armazenamento com o Visual Studio ligada a serviços"
services: storage
documentationcenter: 
author: kraigb
manager: ghogen
editor: 
ms.assetid: 1144a958-f75a-4466-bb21-320b7ae8f304
ms.service: storage
ms.workload: web
ms.tgt_pltfrm: vs-getting-started
ms.devlang: na
ms.topic: article
ms.date: 12/02/2016
ms.author: kraigb
ms.openlocfilehash: 158197a9d49bc4f26841d689405529192c52f529
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-and-visual-studio-connected-services-cloud-services-projects"></a>Introdução ao Blob Storage do Azure e o Visual Studio ligado serviços (projetos de serviços de nuvem)
[!INCLUDE [storage-try-azure-tools-blobs](../../includes/storage-try-azure-tools-blobs.md)]

## <a name="overview"></a>Descrição geral
Este artigo descreve como tooget começar a utilizar armazenamento de Blobs do Azure após a criação ou referenciada uma conta de armazenamento do Azure utilizando Olá Visual Studio **adicionar serviços ligados** projeto dos serviços de caixa de diálogo numa nuvem Visual Studio. Vamos mostrar-lhe como tooaccess e criar contentores de BLOBs e que as tarefas comuns tooperform como carregar, listar e transferir os blobs. Exemplos de Olá são escritos no C\# e utilizar Olá [biblioteca do cliente de armazenamento do Microsoft Azure para .NET](https://msdn.microsoft.com/library/azure/dn261237.aspx).

Armazenamento de Blobs do Azure é um serviço para armazenar grandes quantidades de dados não estruturados, que podem ser acedidos de qualquer local no mundo Olá através de HTTP ou HTTPS. Um blob único pode ser qualquer dimensão. Os BLOBs podem ser coisas como imagens, ficheiros de áudio e vídeos, dados não processados e ficheiros do documento.

Tal como em direto de ficheiros em pastas, blobs de armazenamento em direto nos contentores. Depois de ter criado um armazenamento, crie um ou mais contentores no armazenamento de Olá. Por exemplo, um armazenamento chamado "Scrapbook", pode criar contentores no armazenamento de Olá chamado imagens de toostore "imagens" e outra denominada "áudio" toostore ficheiros áudio. Depois de criar contentores de Olá, pode carregar blob individuais toothem de ficheiros.

* Para obter mais informações sobre manipular programaticamente os blobs, consulte [introdução ao Blob storage do Azure através do .NET](../storage/blobs/storage-dotnet-how-to-use-blobs.md).
* Para obter informações gerais sobre o Storage do Azure, consulte [documentação do Storage](https://azure.microsoft.com/documentation/services/storage/).
* Para obter informações gerais sobre os Cloud Services do Azure, consulte [documentação dos serviços de nuvem](https://azure.microsoft.com/documentation/services/cloud-services/).
* Para obter mais informações sobre a programação de aplicações ASP.NET, consulte [ASP.NET](http://www.asp.net).

## <a name="access-blob-containers-in-code"></a>Contentores de BLOBs de acesso no código
tooprogrammatically aceder aos blobs em projetos de serviço em nuvem, terá de Olá tooadd seguintes itens, se não estiverem já presentes.

1. Adicione Olá seguir superior toohello de declarações de espaço de nomes do código de qualquer ficheiro c# no qual pretende tooprogrammatically acesso Storage do Azure.
   
        using Microsoft.Framework.Configuration;
        using Microsoft.WindowsAzure.Storage;
        using Microsoft.WindowsAzure.Storage.Blob;
        using System.Threading.Tasks;
        using LogLevel = Microsoft.Framework.Logging.LogLevel;
2. Obter um **CloudStorageAccount** objeto que representa as informações da conta de armazenamento. Olá de utilização seguintes código tooget Olá a cadeia de ligação de armazenamento e as informações da configuração de serviço do Azure Olá conta de armazenamento.
   
        CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
        CloudConfigurationManager.GetSetting("<storage account name>_AzureStorageConnectionString"));
3. Obter um **CloudBlobClient** tooreference um contentor existente na sua conta de armazenamento de objeto.
   
        // Create a blob client.
        CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
4. Obter um **CloudBlobContainer** objeto tooreference um contentor de blob específico.
   
        // Get a reference tooa container named "mycontainer."
        CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

> [!NOTE]
> Utilize todas código Olá mostrado no procedimento anterior do Olá à frente do código Olá mostrado Olá secções a seguir.
> 
> 

## <a name="create-a-container-in-code"></a>Criar um contentor no código
> [!NOTE]
> Algumas APIs que efetuar chamadas de saída tooAzure armazenamento no ASP.NET são assíncronas. Consulte [programação assíncrona com Async-Await](http://msdn.microsoft.com/library/hh191443.aspx) para obter mais informações. código de Olá no seguinte exemplo de Olá parte do princípio de que está a utilizar métodos assíncronos de programação.
> 
> 

toocreate um contentor na sua conta de armazenamento, tudo o que precisa toodo é adicionar uma chamada demasiado**CreateIfNotExistsAsync** como Olá seguinte código:

    // If "mycontainer" doesn't exist, create it.
    await container.CreateIfNotExistsAsync();


toomake Olá ficheiros Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código.

    await container.SetPermissionsAsync(new BlobContainerPermissions
    {
        PublicAccess = BlobContainerPublicAccessType.Blob
    });


Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público, mas pode modificar ou eliminá-los apenas se tiver a chave de acesso adequadas Olá.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
Storage do Azure suporta blobs de blocos e blobs de páginas. Na maioria dos casos de Olá, o blob de bloco é Olá recomendado toouse de tipo.

tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco. Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStream** método. Esta operação cria blob Olá se anteriormente não existir ou substitui-lo se existir. Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.

    // Retrieve a reference tooa blob named "myblob".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

    // Create or overwrite hello "myblob" blob with contents from a local file.
    using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
    {
        blockBlob.UploadFromStream(fileStream);
    }

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor. Em seguida, pode utilizar um contentor Olá **ListBlobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo. tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se o tipo de Olá for desconhecido, pode utilizar o toodetermine de verificação de um tipo que toocast para. Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá **fotografias** contentor:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, false))
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

Conforme mostrado no exemplo de código anterior Olá, serviço de blob Olá tem o conceito de Olá de diretórios contentores, bem. Isto é, de modo a que pode organizar os blobs numa estrutura mais semelhantes a pasta. Por exemplo, considere o seguinte conjunto de blobs de blocos num contentor com o nome de Olá **fotografias**:

    photo1.jpg
    2010/architecture/description.txt
    2010/architecture/photo3.jpg
    2010/architecture/photo4.jpg
    2011/architecture/photo5.jpg
    2011/architecture/photo6.jpg
    2011/architecture/description.txt
    2011/photo7.jpg

Quando chamar **ListBlobs** no contentor de Olá (tal como no exemplo anterior Olá), contém a coleção de Olá devolvida **CloudBlobDirectory** e **CloudBlockBlob** objetos que representam os diretórios de Olá e os blobs contidos no nível superior Olá. Olá o resultado resultante é:

    Directory: https://<accountname>.blob.core.windows.net/photos/2010/
    Directory: https://<accountname>.blob.core.windows.net/photos/2011/
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg


Opcionalmente, pode definir Olá **UseFlatBlobListing** parâmetro de Olá **ListBlobs** método **verdadeiro**. Isto resulta em todos os BLOBs que está a ser devolvido como uma **CloudBlockBlob**, independentemente do diretório. Segue-se a chamada de Olá demasiado**ListBlobs**:

    // Loop over items within hello container and output hello length and URI.
    foreach (IListBlobItem item in container.ListBlobs(null, true))
    {
       ...
    }

e Eis resultados Olá:

    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
    Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
    Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
    Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
    Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
    Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
    Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
    Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg

Para obter mais informações, consulte [CloudBlobContainer.ListBlobs](https://msdn.microsoft.com/library/azure/dd135734.aspx).

## <a name="download-blobs"></a>Transferir blobs
toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **DownloadToStream** método. Olá exemplo seguinte utiliza Olá **DownloadToStream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.

    // Get a reference tooa blob named "photo1.jpg".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

    // Save blob contents tooa file.
    using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
    {
        blockBlob.DownloadToStream(fileStream);
    }

Também pode utilizar Olá **DownloadToStream** método toodownload Olá conteúdo um blob como uma cadeia de texto.

    // Get a reference tooa blob named "myblob.txt"
    CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

    string text;
    using (var memoryStream = new MemoryStream())
    {
        blockBlob2.DownloadToStream(memoryStream);
        text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
    }

## <a name="delete-blobs"></a>Eliminar blobs
toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o **eliminar** método.

    // Get a reference tooa blob named "myblob.txt".
    CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

    // Delete hello blob.
    blockBlob.Delete();


## <a name="list-blobs-in-pages-asynchronously"></a>Listar blobs em páginas de forma assíncrona
Se está a listar um grande número de blobs ou pretende que o número de Olá toocontrol de resultados devolvido numa operação de listagem, pode listar os blobs em páginas de resultados. Este exemplo mostra como tooreturn resulta nas páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera tooreturn um grande conjunto de resultados.

Este exemplo mostra uma lista de BLOBs não hierárquica, mas também pode criar uma lista hierárquica ao definir Olá **useFlatBlobListing** parâmetro de Olá **ListBlobsSegmentedAsync** método demasiado **FALSO**.

Uma vez que o método de exemplo de Olá chama um método assíncrono, tem de ser precedido pela Olá **async** palavra-chave e tem de devolver um **tarefas** objeto. Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo de Olá até concluir a tarefa de listagem Olá.

    async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
    {
        // List blobs toohello console window, with paging.
        Console.WriteLine("List blobs in pages:");

        int i = 0;
        BlobContinuationToken continuationToken = null;
        BlobResultSegment resultSegment = null;

        // Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
        // When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
        do
        {
            // This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
            // or by calling a different overload.
            resultSegment = await container.ListBlobsSegmentedAsync("", true, BlobListingDetails.All, 10, continuationToken, null, null);
            if (resultSegment.Results.Count<IListBlobItem>() > 0) { Console.WriteLine("Page {0}:", ++i); }
            foreach (var blobItem in resultSegment.Results)
            {
                Console.WriteLine("\t{0}", blobItem.StorageUri.PrimaryUri);
            }
            Console.WriteLine();

            //Get hello continuation token.
            continuationToken = resultSegment.ContinuationToken;
        }
        while (continuationToken != null);
    }

## <a name="next-steps"></a>Passos seguintes
[!INCLUDE [vs-storage-dotnet-blobs-next-steps](../../includes/vs-storage-dotnet-blobs-next-steps.md)]

