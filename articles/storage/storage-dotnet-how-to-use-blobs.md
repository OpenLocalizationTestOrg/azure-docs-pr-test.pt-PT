---
title: "aaaGet iniciado com o Blob storage do Azure (armazenamento de objetos) através do .NET | Microsoft Docs"
description: "Armazene dados não estruturados na nuvem de Olá Blob Storage do Azure (armazenamento de objetos)."
services: storage
documentationcenter: .net
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: d18a8fc8-97cb-4d37-a408-a6f8107ea8b3
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: hero-article
ms.date: 03/27/2017
ms.author: marsma
ms.openlocfilehash: 9b675ac073e7e901fe1afe54f7bfea12eefbf3ec
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-blob-storage-using-net"></a>Introdução ao Blob Storage do Azure através do .NET

[!INCLUDE [storage-selector-blob-include](../../includes/storage-selector-blob-include.md)]

[!INCLUDE [storage-check-out-samples-dotnet](../../includes/storage-check-out-samples-dotnet.md)]

Armazenamento de Blobs do Azure é um serviço que armazena dados não estruturados na nuvem de Olá como objetos/blobs. O Blob Storage pode armazenar qualquer tipo de texto ou de dados binários, tal como um documento, um ficheiro de multimédia ou um instalador da aplicação. O blob storage também é referido tooas armazenamento de objetos.

### <a name="about-this-tutorial"></a>Acerca deste tutorial
Este tutorial mostra como código de toowrite .NET para alguns cenários comuns utilizando o Blob storage do Azure. Os cenários abrangidos incluem carregar, listar, transferir e eliminar blobs.

**Pré-requisitos:**

* [Microsoft Visual Studio](https://www.visualstudio.com/)
* [Biblioteca de Clientes do Armazenamento do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
* [Gestor de Configuração do Azure para .NET](https://www.nuget.org/packages/Microsoft.WindowsAzure.ConfigurationManager/)
* Uma [Conta do Storage do Azure](storage-create-storage-account.md#create-a-storage-account)

[!INCLUDE [storage-dotnet-client-library-version-include](../../includes/storage-dotnet-client-library-version-include.md)]

### <a name="more-samples"></a>Mais exemplos
Para obter exemplos adicionais que utilizam o Armazenamento de Blobs, veja [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/). Pode transferir a aplicação de exemplo de Olá e executá-la ou procurar Olá código no GitHub.

[!INCLUDE [storage-blob-concepts-include](../../includes/storage-blob-concepts-include.md)]

[!INCLUDE [storage-create-account-include](../../includes/storage-create-account-include.md)]

[!INCLUDE [storage-development-environment-include](../../includes/storage-development-environment-include.md)]

### <a name="add-using-directives"></a>Adicionar com diretivas
Adicione Olá seguinte **utilizando** diretivas toohello parte superior Olá `Program.cs` ficheiro:

```csharp
using Microsoft.WindowsAzure; // Namespace for CloudConfigurationManager
using Microsoft.WindowsAzure.Storage; // Namespace for CloudStorageAccount
using Microsoft.WindowsAzure.Storage.Blob; // Namespace for Blob storage types
```

### <a name="parse-hello-connection-string"></a>Analisar cadeia de ligação de Olá
[!INCLUDE [storage-cloud-configuration-manager-include](../../includes/storage-cloud-configuration-manager-include.md)]

### <a name="create-hello-blob-service-client"></a>Crie hello do cliente do serviço Blob
Olá **CloudBlobClient** classe permite-lhe tooretrieve contentores e blobs armazenados no Blob storage. Segue-se o cliente do serviço Olá toocreate unidirecional:

```csharp
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();
```
Agora, está pronto toowrite código que lê dados de e escreve tooBlob o armazenamento de dados.

## <a name="create-a-container"></a>Criar um contentor
[!INCLUDE [storage-container-naming-rules-include](../../includes/storage-container-naming-rules-include.md)]

Este exemplo mostra como toocreate um contentor se já existir:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it doesn't already exist.
container.CreateIfNotExists();
```

Por predefinição, o novo contentor de Olá é privado, o que significa que terá de especificar os blobs de toodownload chave de acesso de armazenamento deste contentor. Se pretender que os ficheiros de Olá toomake dentro Olá contentor disponíveis tooeveryone, pode definir Olá contentor toobe público utilizando Olá seguinte código:

```csharp
container.SetPermissions(
    new BlobContainerPermissions { PublicAccess = BlobContainerPublicAccessType.Blob });
```

Qualquer pessoa na Internet de Olá pode ver os blobs num contentor público. No entanto, pode modificar ou eliminá-los apenas se tiver a chave de acesso da conta adequada de Olá ou uma assinatura de acesso partilhado.

## <a name="upload-a-blob-into-a-container"></a>Carregar um blob para um contentor
O Blob Storage do Azure suporta blobs de blocos e blobs de páginas.  Na maioria dos casos, o blob de bloco é Olá recomendado toouse de tipo.

tooupload um blob de blocos do ficheiro tooa, obtenha uma referência de contentor e utilizá-lo tooget uma referência de blob de bloco. Depois de ter uma referência de blob, pode carregar qualquer fluxo de dados tooit ao chamar Olá **UploadFromStream** método. Esta operação cria blob Olá se anteriormente não existir ou substitui-lo se existir.

Olá seguinte exemplo mostra como tooupload um blob para um contentor e parte do princípio de que contentor Olá já foi criado.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob");

// Create or overwrite hello "myblob" blob with contents from a local file.
using (var fileStream = System.IO.File.OpenRead(@"path\myfile"))
{
    blockBlob.UploadFromStream(fileStream);
}
```

## <a name="list-hello-blobs-in-a-container"></a>Lista Olá blobs num contentor
os blobs de Olá toolist num contentor, obtenha primeiro uma referência de contentor. Em seguida, pode utilizar um contentor Olá **ListBlobs** blobs do método tooretrieve Olá e/ou os diretórios dentro do mesmo. tooaccess Olá conjunto avançado de propriedades e métodos de um **IListBlobItem**, tem de o transmitir-tooa **CloudBlockBlob**, **CloudPageBlob**, ou  **CloudBlobDirectory** objeto. Se o tipo de Olá for desconhecido, pode utilizar o toodetermine de verificação de um tipo que toocast para. Olá código seguinte demonstra como tooretrieve e de saída Olá URI de cada item no Olá _fotografias_ contentor:

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("photos");

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
```

Ao incluir informações do caminho nos nomes de blobs, pode criar uma estrutura de diretório virtual que pode organizar e percorrer tal como faria com um sistema de ficheiros tradicional. estrutura de diretórios Olá é virtual Olá apenas – apenas recursos disponíveis no Blob storage são contentores e blobs. No entanto, biblioteca de clientes do storage Olá oferece um **CloudBlobDirectory** diretório virtual do toorefer tooa de objeto e simplificar o processo de Olá de trabalhar com blobs que se encontram organizados desta forma.

Por exemplo, considere o seguinte conjunto de blobs de blocos num contentor com o nome de Olá *fotografias*:

```
photo1.jpg
2010/architecture/description.txt
2010/architecture/photo3.jpg
2010/architecture/photo4.jpg
2011/architecture/photo5.jpg
2011/architecture/photo6.jpg
2011/architecture/description.txt
2011/photo7.jpg
```

Quando chamar **ListBlobs** no Olá *fotografias* contentor (tal como no Olá precedente fragmento de código), é devolvida uma lista hierárquica. Esta contém os **CloudBlobDirectory** e **CloudBlockBlob** objetos, que representam os diretórios de Olá e os blobs no contentor de Olá, respetivamente. saída resultante Olá tem o seguinte:

```
Directory: https://<accountname>.blob.core.windows.net/photos/2010/
Directory: https://<accountname>.blob.core.windows.net/photos/2011/
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

Opcionalmente, pode definir Olá **UseFlatBlobListing** parâmetro de Olá **ListBlobs** método **verdadeiro**. Neste caso, todos os BLOBs no contentor de Olá é devolvido como uma **CloudBlockBlob** objeto. Olá chamada demasiado**ListBlobs** tooreturn uma lista não hierárquica tem o seguinte aspeto:

```csharp
// Loop over items within hello container and output hello length and URI.
foreach (IListBlobItem item in container.ListBlobs(null, true))
{
    ...
}
```

e resultados de Olá tem o seguinte aspeto:

```
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2010/architecture/description.txt
Block blob of length 314618: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo3.jpg
Block blob of length 522713: https://<accountname>.blob.core.windows.net/photos/2010/architecture/photo4.jpg
Block blob of length 4: https://<accountname>.blob.core.windows.net/photos/2011/architecture/description.txt
Block blob of length 419048: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo5.jpg
Block blob of length 506388: https://<accountname>.blob.core.windows.net/photos/2011/architecture/photo6.jpg
Block blob of length 399751: https://<accountname>.blob.core.windows.net/photos/2011/photo7.jpg
Block blob of length 505623: https://<accountname>.blob.core.windows.net/photos/photo1.jpg
```

## <a name="download-blobs"></a>Transferir blobs
toodownload blobs, obtenha primeiro uma referência de blob e, em seguida, chame Olá **DownloadToStream** método. Olá exemplo seguinte utiliza Olá **DownloadToStream** método tootransfer Olá blob conteúdo tooa objeto de fluxo, em seguida, pode manter tooa de ficheiros local.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "photo1.jpg".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("photo1.jpg");

// Save blob contents tooa file.
using (var fileStream = System.IO.File.OpenWrite(@"path\myfile"))
{
    blockBlob.DownloadToStream(fileStream);
}
```

Também pode utilizar Olá **DownloadToStream** método toodownload Olá conteúdo um blob como uma cadeia de texto.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt"
CloudBlockBlob blockBlob2 = container.GetBlockBlobReference("myblob.txt");

string text;
using (var memoryStream = new MemoryStream())
{
    blockBlob2.DownloadToStream(memoryStream);
    text = System.Text.Encoding.UTF8.GetString(memoryStream.ToArray());
}
```

## <a name="delete-blobs"></a>Eliminar blobs
toodelete um blob, obtenha primeiro uma referência de blob e, em seguida, chame o **eliminar** método.

```csharp
// Retrieve storage account from connection string.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    CloudConfigurationManager.GetSetting("StorageConnectionString"));

// Create hello blob client.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve reference tooa previously created container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Retrieve reference tooa blob named "myblob.txt".
CloudBlockBlob blockBlob = container.GetBlockBlobReference("myblob.txt");

// Delete hello blob.
blockBlob.Delete();
```

## <a name="list-blobs-in-pages-asynchronously"></a>Listar blobs em páginas de forma assíncrona
Se está a listar um grande número de blobs ou pretende que o número de Olá toocontrol de resultados devolvido numa operação de listagem, pode listar os blobs em páginas de resultados. Este exemplo mostra como tooreturn resulta nas páginas de forma assíncrona, para que a execução não fique bloqueada enquanto espera tooreturn um grande conjunto de resultados.

Este exemplo mostra uma lista de BLOBs não hierárquica, mas também pode criar uma lista hierárquica ao definir Olá _useFlatBlobListing_ parâmetro de Olá **ListBlobsSegmentedAsync** too_false_ de método.

Uma vez que o método de exemplo de Olá chama um método assíncrono, tem de ser precedido pela Olá _async_ palavra-chave e tem de devolver um **tarefas** objeto. Olá await palavra-chave especificada para Olá **ListBlobsSegmentedAsync** método suspende a execução do método de exemplo de Olá até concluir a tarefa de listagem Olá.

```csharp
async public static Task ListBlobsSegmentedInFlatListing(CloudBlobContainer container)
{
    //List blobs toohello console window, with paging.
    Console.WriteLine("List blobs in pages:");

    int i = 0;
    BlobContinuationToken continuationToken = null;
    BlobResultSegment resultSegment = null;

    //Call ListBlobsSegmentedAsync and enumerate hello result segment returned, while hello continuation token is non-null.
    //When hello continuation token is null, hello last page has been returned and execution can exit hello loop.
    do
    {
        //This overload allows control of hello page size. You can return all remaining results by passing null for hello maxResults parameter,
        //or by calling a different overload.
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
```

## <a name="writing-tooan-append-blob"></a>Blob de acréscimo tooan de escrita
Um blob de acréscimo está otimizado para operações de acréscimo, como o registo. Como um blob de blocos, um blob de acréscimo é composto por blocos, mas quando adicionar um novo blob de acréscimo tooan de bloco, é sempre toohello anexado final do blob Olá. Não é possível atualizar ou eliminar um bloco existente num blob de acréscimo. o bloco de Olá IDs para um blob de acréscimo não são expostos como acontece para um blob de blocos.

Cada bloco num blob de acréscimo pode ter um tamanho diferente, cópia de segurança tooa máximo de 4 MB, e um blob de acréscimo pode incluir um máximo de 50 000 blocos. Consequentemente, o tamanho máximo do Olá de um blob de acréscimo é ligeiramente superior a 195 GB (4 MB X 50 000 blocos).

exemplo de Olá abaixo cria um novo blob de acréscimo e acrescenta alguns dados tooit, simulando uma operação de registo simples.

```csharp
//Parse hello connection string for hello storage account.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(
    Microsoft.Azure.CloudConfigurationManager.GetSetting("StorageConnectionString"));

//Create service client for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

//Get a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("my-append-blobs");

//Create hello container if it does not already exist.
container.CreateIfNotExists();

//Get a reference tooan append blob.
CloudAppendBlob appendBlob = container.GetAppendBlobReference("append-blob.log");

//Create hello append blob. Note that if hello blob already exists, hello CreateOrReplace() method will overwrite it.
//You can check whether hello blob exists tooavoid overwriting it by using CloudAppendBlob.Exists().
appendBlob.CreateOrReplace();

int numBlocks = 10;

//Generate an array of random bytes.
Random rnd = new Random();
byte[] bytes = new byte[numBlocks];
rnd.NextBytes(bytes);

//Simulate a logging operation by writing text data and byte data toohello end of hello append blob.
for (int i = 0; i < numBlocks; i++)
{
    appendBlob.AppendText(String.Format("Timestamp: {0:u} \tLog Entry: {1}{2}",
        DateTime.UtcNow, bytes[i], Environment.NewLine));
}

//Read hello append blob toohello console window.
Console.WriteLine(appendBlob.DownloadText());
```

Consulte [compreender os Blobs de blocos, Blobs de páginas e os Blobs de acréscimo](/rest/api/storageservices/Understanding-Block-Blobs--Append-Blobs--and-Page-Blobs) para obter mais informações sobre as diferenças de Olá entre tipos de Olá três de blobs.

## <a name="managing-security-for-blobs"></a>Gerir a segurança dos blobs
Por predefinição, armazenamento do Azure mantém os seus dados seguros ao limitar acesso toohello proprietário da conta, que está na posse das chaves de acesso de conta Olá. Quando precisar de dados de BLOBs de tooshare na sua conta de armazenamento, é importante toodo Sim sem comprometer a segurança de Olá das suas chaves de acesso da conta. Além disso, pode encriptar tooensure de dados de BLOBs que estes estão seguros durante a transmissão Olá e no Storage do Azure.

[!INCLUDE [storage-account-key-note-include](../../includes/storage-account-key-note-include.md)]

### <a name="controlling-access-tooblob-data"></a>Controlar o acesso tooblob dados
Por predefinição, dados de BLOBs de Olá na sua conta do storage são o proprietário da conta toostorage apenas acessíveis. Autenticar pedidos para o Blob storage requer a chave de acesso da conta de Olá por predefinição. No entanto, pode ser útil toomake determinados utilizadores tooother disponíveis de dados de Blobs. Tem duas opções:

* **Acesso anónimo:** pode tornar um contentor ou os respetivos blobs publicamente disponíveis para acesso anónimo. Consulte [gerir o acesso de leitura anónimo toocontainers e blobs](storage-manage-access-to-resources.md) para obter mais informações.
* **Assinaturas de acesso partilhado:** pode fornecer aos clientes uma assinatura de acesso partilhado (SAS), que concede acesso delegado tooa recursos na sua conta de armazenamento, com as permissões que especificar e durante um intervalo que especificou. Veja [Utilizar Assinaturas de Acesso Partilhado (SAS)](storage-dotnet-shared-access-signature-part-1.md) para obter mais informações.

### <a name="encrypting-blob-data"></a>Encriptar dados de blobs
Armazenamento do Azure suporta a encriptação de dados de BLOBs cliente Olá e no servidor de Olá:

* **Encriptação do lado do cliente:** Olá biblioteca de clientes de armazenamento para .NET suporta a encriptação de dados dentro de aplicações de cliente antes de carregar tooAzure armazenamento e a desencriptação de dados ao transferir toohello cliente. biblioteca de Olá também suporta a integração com o Cofre de chaves do Azure para a gestão de chaves de conta de armazenamento. Consulte [Encriptação do Lado do Cliente com .NET para o Armazenamento do Microsoft Azure](storage-client-side-encryption.md) para obter mais informações. Consulte também [Tutorial: encriptar e desencriptar blobs no Armazenamento do Microsoft Azure com o Cofre de Chaves do Azure](storage-encrypt-decrypt-blobs-key-vault.md).
* **Encriptação do lado do servidor**: agora, o Storage do Azure suporta a encriptação do lado do servidor. Consulte [Encriptação do Serviço do Storage do Azure para Dados Inativos (Pré-visualização)](storage-service-encryption.md).

## <a name="next-steps"></a>Passos seguintes
Agora que aprendeu Olá Noções básicas do Blob storage, siga estas toolearn ligações mais.

### <a name="microsoft-azure-storage-explorer"></a>Explorador de Armazenamento do Microsoft Azure
* [Explorador de armazenamento do Azure (MASE) da Microsoft](../vs-azure-tools-storage-manage-with-storage-explorer.md) é uma aplicação autónoma e gratuita da Microsoft permite-lhe toowork visualmente com dados de armazenamento do Azure no Windows, macOS e Linux.

### <a name="blob-storage-samples"></a>Exemplos de Armazenamento de Blobs
* [Introdução ao Armazenamento de Blobs do Azure no .NET](https://azure.microsoft.com/documentation/samples/storage-blob-dotnet-getting-started/)

### <a name="blob-storage-reference"></a>Referência do Blob Storage
* [Referência da Biblioteca de Clientes do Storage para o .NET](https://msdn.microsoft.com/library/azure/mt347887.aspx)
* [Referência da API REST](/rest/api/storageservices/azure-storage-services-rest-api-reference)

### <a name="conceptual-guides"></a>Guias conceptuais
* [Transferência de dados com Olá utilitário de linha de comandos AzCopy](storage-use-azcopy.md)
* [Introdução ao Armazenamento de ficheiros do .NET](storage-dotnet-how-to-use-files.md)
* [Como o armazenamento com Olá SDK de WebJobs de BLOBs de toouse do Azure](../app-service-web/websites-dotnet-webjobs-sdk-storage-blobs-how-to.md)
