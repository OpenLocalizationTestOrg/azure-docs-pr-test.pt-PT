---
title: aaaDevelop para o File storage do Azure com o Java | Microsoft Docs
description: "Saiba como aplicações de Java toodevelop e serviços que utilizam toostore de armazenamento de ficheiros do Azure de ficheiros de dados."
services: storage
documentationcenter: java
author: robinsh
manager: timlt
editor: tysonn
ms.assetid: 3bfbfa7f-d378-4fb4-8df3-e0b6fcea5b27
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: Java
ms.topic: article
ms.date: 05/27/2017
ms.author: robinsh
ms.openlocfilehash: b50703815daf2c829e7e9a9a4196c31a2b8727e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="develop-for-azure-file-storage-with-java"></a>Desenvolver para o File storage do Azure com Java
[!INCLUDE [storage-selector-file-include](../../includes/storage-selector-file-include.md)]

[!INCLUDE [storage-check-out-samples-java](../../includes/storage-check-out-samples-java.md)]

## <a name="about-this-tutorial"></a>Acerca deste tutorial
Este tutorial demonstrar Noções básicas de Olá da utilização de aplicações do Java toodevelop ou serviços que utilizam dados de ficheiros de toostore de armazenamento de ficheiros do Azure. Neste tutorial, iremos criar uma aplicação de consola simples e Mostrar como tooperform ações básicas com o storage do Java e ficheiros do Azure:

* Criar e eliminar as partilhas de ficheiros do Azure
* Criar e eliminar diretórios
* Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure
* Carregar, transferir e eliminar um ficheiro

> [!Note]  
> Porque o File storage do Azure pode ser acedido através de SMB, é possível toowrite aplicações simples que aceder à partilha de ficheiros do Azure Olá utilizar Olá padrão e/s de Java classes. Este artigo descreve como toowrite aplicações que utilizam Olá SDK de Java do Azure armazenamento, que utiliza Olá [File storage do Azure REST API](https://docs.microsoft.com/rest/api/storageservices/fileservices/file-service-rest-api) tootalk tooAzure armazenamento de ficheiros.

## <a name="create-a-java-application"></a>Criar uma aplicação Java
amostras de Olá toobuild, terá de Olá Kit de desenvolvimento Java (JDK) e Olá [SDK de armazenamento do Azure para Java] [-]. Deve também criou uma conta de armazenamento do Azure.

## <a name="setup-your-application-toouse-azure-file-storage"></a>Configurar a sua aplicação toouse File storage do Azure
Olá toouse storage do Azure APIs, adicionar Olá seguir parte superior do toohello de declaração do ficheiro de Java de olá onde pretende tooaccess Olá armazenamento serviço.

```java
// Include hello following imports toouse blob APIs.
import com.microsoft.azure.storage.*;
import com.microsoft.azure.storage.file.*;
```

## <a name="setup-an-azure-storage-connection-string"></a>Configurar uma cadeia de ligação de armazenamento do Azure
toouse File storage do Azure, terá de tooconnect tooyour conta de armazenamento Azure. Olá primeiro passo seria tooconfigure uma cadeia de ligação que iremos utilizar conta de armazenamento de tooyour tooconnect. Vamos definir um toodo variável estática que.

```java
// Configure hello connection-string with your values
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account_name;" +
    "AccountKey=your_storage_account_key";
```

> [!NOTE]
> Substitua os valores reais Olá para a sua conta de armazenamento your_storage_account_name e your_storage_account_key.
> 
> 

## <a name="connecting-tooan-azure-storage-account"></a>Ligar tooan conta de armazenamento do Azure
conta de armazenamento de tooyour tooconnect, terá de toouse Olá **CloudStorageAccount** objeto, transmitir um tooits de cadeia de ligação **analisar** método.

```java
// Use hello CloudStorageAccount object tooconnect tooyour storage account
try {
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);
} catch (InvalidKeyException invalidKey) {
    // Handle hello exception
}
```

**CloudStorageAccount.parse** gera um InvalidKeyException, pelo que terá tooput-lo dentro de um catch/tente bloquear.

## <a name="create-an-azure-file-share"></a>Criar uma partilha de ficheiros do Azure
Todos os ficheiros e diretórios no File storage do Azure residem num contentor chamado um **partilha**. A conta do storage pode ter o mesmo partilhas que permite a capacidade de conta. partilha de tooa tooobtain acesso e o respetivo conteúdo, terá de toouse um cliente de armazenamento de ficheiros do Azure.

```java
// Create hello Azure File storage client.
CloudFileClient fileClient = storageAccount.createCloudFileClient();
```

Utilizando o cliente de armazenamento de ficheiros do Azure de Olá, em seguida, pode obter uma partilha de tooa de referência.

```java
// Get a reference toohello file share
CloudFileShare share = fileClient.getShareReference("sampleshare");
```

tooactually criar partilha de Olá, utilize Olá **createIfNotExists** método de Olá CloudFileShare objeto.

```java
if (share.createIfNotExists()) {
    System.out.println("New share created");
}
```

Neste momento, **partilhar** contém uma partilha de tooa referência denominada **sampleshare**.

## <a name="delete-an-azure-file-share"></a>Eliminar uma partilha de ficheiros do Azure
Eliminar uma partilha é feito ao chamar Olá **deleteIfExists** método num objeto CloudFileShare. Eis o código de exemplo que suporta que.

```java
try
{
    // Retrieve storage account from connection-string.
    CloudStorageAccount storageAccount = CloudStorageAccount.parse(storageConnectionString);

    // Create hello file client.
   CloudFileClient fileClient = storageAccount.createCloudFileClient();

   // Get a reference toohello file share
   CloudFileShare share = fileClient.getShareReference("sampleshare");

   if (share.deleteIfExists()) {
       System.out.println("sampleshare deleted");
   }
} catch (Exception e) {
    e.printStackTrace();
}
```

## <a name="create-a-directory"></a>Criar um diretório
Também pode organizar armazenamento colocando os ficheiros secundárias diretórios em vez de ter todos eles no diretório de raiz de Olá. File storage do Azure permite-lhe toocreate como permitem muito diretórios como será a conta. código de Olá abaixo irá criar um subdiretório com o nome **sampledir** no diretório de raiz de Olá.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello sampledir directory
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

if (sampleDir.createIfNotExists()) {
    System.out.println("sampledir created");
} else {
    System.out.println("sampledir already exists");
}
```

## <a name="delete-a-directory"></a>Eliminar um diretório
Eliminar um diretório é uma tarefa bastante simple, embora deve ser salientado que não é possível eliminar um diretório que contiver ficheiros ou outros diretórios.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory you want toodelete
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

// Delete hello directory
if ( containerDir.deleteIfExists() ) {
    System.out.println("Directory deleted");
}
```

## <a name="enumerate-files-and-directories-in-an-azure-file-share"></a>Enumerar ficheiros e diretórios numa partilha de ficheiros do Azure
Obter uma lista de ficheiros e diretórios dentro de uma partilha facilmente é feito chamando **listFilesAndDirectories** numa referência CloudFileDirectory. método de Olá devolve uma lista de objetos de ListFileItem que pode iterar. Por exemplo, hello código seguinte irá listar ficheiros e diretórios dentro do diretório de raiz de Olá.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

for ( ListFileItem fileItem : rootDir.listFilesAndDirectories() ) {
    System.out.println(fileItem.getUri());
}
```

## <a name="upload-a-file"></a>Carregar um ficheiro
Um ficheiro de Azure partilha contém em Olá muito menos, um diretório de raiz, onde podem residir os ficheiros. Nesta secção, irá aprender como tooupload um ficheiro a partir do armazenamento local para Olá raiz do diretório de uma partilha.

Olá primeiro passo para carregar um ficheiro é tooobtain um diretório de toohello de referência onde deve residir. Pode fazê-lo ao chamar Olá **getRootDirectoryReference** método do objeto de partilha de Olá.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();
```

Agora que tem um diretório de raiz de toohello de referência da partilha de Olá, pode carregar um ficheiro no mesmo utilizando Olá seguinte código.

```java
        // Define hello path tooa local file.
        final String filePath = "C:\\temp\\Readme.txt";
    
        CloudFile cloudFile = rootDir.getFileReference("Readme.txt");
        cloudFile.uploadFromFile(filePath);
```

## <a name="download-a-file"></a>Transferir um ficheiro
Uma das Olá induzirem mais frequentes operações que irá executar contra File storage do Azure é ficheiros toodownload. No seguinte exemplo de Olá, código de Olá transfere SampleFile.txt e apresenta o respetivo conteúdo.

```java
//Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

//Get a reference toohello directory that contains hello file
CloudFileDirectory sampleDir = rootDir.getDirectoryReference("sampledir");

//Get a reference toohello file you want toodownload
CloudFile file = sampleDir.getFileReference("SampleFile.txt");

//Write hello contents of hello file toohello console.
System.out.println(file.downloadText());
```

## <a name="delete-a-file"></a>Eliminar um ficheiro
Há outra operação de armazenamento de ficheiros do Azure comum é a eliminação de ficheiros. Olá seguinte código elimina um ficheiro denominado SampleFile.txt armazenados dentro de um diretório com o nome **sampledir**.

```java
// Get a reference toohello root directory for hello share.
CloudFileDirectory rootDir = share.getRootDirectoryReference();

// Get a reference toohello directory where hello file toobe deleted is in
CloudFileDirectory containerDir = rootDir.getDirectoryReference("sampledir");

String filename = "SampleFile.txt"
CloudFile file;

file = containerDir.getFileReference(filename)
if ( file.deleteIfExists() ) {
    System.out.println(filename + " was deleted");
}
```

## <a name="next-steps"></a>Passos seguintes
Se quiser toolearn mais informações sobre outras APIs de armazenamento do Azure, siga estas ligações.

* [Centro de Programadores do Java](http://azure.microsoft.com/develop/java/)
* [Armazenamento do Azure SDK para Java](https://github.com/azure/azure-storage-java)
* [Armazenamento do Azure SDK para Android](https://github.com/azure/azure-storage-android)
* [Referência do SDK de cliente de armazenamento do Azure](http://dl.windowsazure.com/storage/javadoc/)
* [API REST dos Serviços do Armazenamento do Azure](https://msdn.microsoft.com/library/azure/dd179355.aspx)
* [Blogue da Equipa de Armazenamento do Azure](http://blogs.msdn.com/b/windowsazurestorage/)
* [Transferência de dados com o utilitário de linha de comandos do AzCopy Olá](storage-use-azcopy.md)
