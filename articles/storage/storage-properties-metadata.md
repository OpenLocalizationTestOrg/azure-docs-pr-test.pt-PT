---
title: aaaSet e obter objeto de propriedades e os metadados no armazenamento do Azure | Microsoft Docs
description: Armazenar metadados personalizados sobre objetos no Storage do Azure e definir e obter as propriedades do sistema.
services: storage
documentationcenter: 
author: mmacy
manager: timlt
editor: tysonn
ms.assetid: 036f9006-273e-400b-844b-3329045e9e1f
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: marsma
ms.openlocfilehash: 44f9243183014845964f337b476a6b0069dc0902
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="set-and-retrieve-properties-and-metadata"></a>Definir e obter propriedades e metadados

Objetos nas propriedades do sistema de suporte de armazenamento do Azure e os metadados definidos pelo utilizador, além disso toohello dados que contêm. Este artigo aborda as propriedades do sistema de gestão e os metadados definidos pelo utilizador com Olá [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).

* **Propriedades do sistema**: existem propriedades do sistema em cada recurso de armazenamento. Alguns deles possam ler ou definir, enquanto outras são só de leitura. Em bastidores Olá, algumas propriedades do sistema correspondem toocertain cabeçalhos de HTTP padrão. biblioteca de clientes do storage do Azure Olá mantém estas por si.

* **Os metadados definidos pelo utilizador**: os metadados definidos pelo utilizador são metadados que especifica um recurso especificado no formato Olá um par nome / valor. Pode utilizar valores adicionais do metadados toostore com um recurso de armazenamento. Estes valores de metadados adicionais são os seus próprios apenas para fins de e não afetam a forma como se comporta recursos Olá.

Ao obter valores de propriedade e metadados para um recurso de armazenamento é um processo de dois passos. Antes de ler estes valores, tem explicitamente obtê-los ao chamar Olá **FetchAttributes** método.

> [!IMPORTANT]
> Os valores de propriedade e metadados para um recurso de armazenamento não são preenchidos a menos que tem de chamar um dos Olá **FetchAttributes** métodos.
>
> Receberá um `400 Bad Request` se qualquer pares nome/valor contém carateres não ASCII. Metadados pares de nome/valor são os cabeçalhos de HTTP válidos e, pelo que tem de respeitar as restrições de tooall que rege cabeçalhos de HTTP. Por conseguinte, é recomendado que utilize a codificação do URL ou codificação Base64 para os nomes e valores que contêm carateres não ASCII.
>

## <a name="setting-and-retrieving-properties"></a>Definir e obter propriedades
os valores de propriedade tooretrieve, chamada Olá **FetchAttributes** método no seu blob ou contentor toopopulate Olá propriedades, em seguida, leia os valores de Olá.

tooset propriedades de um objeto, especifique o valor da propriedade Olá, em seguida, invoque Olá **SetProperties** método.

Olá exemplo de código seguinte cria um contentor, em seguida, escreve algumas da janela de consola de tooa de valores de propriedade.

```csharp
//Parse hello connection string for hello storage account.
const string ConnectionString = "DefaultEndpointsProtocol=https;AccountName=account-name;AccountKey=account-key";
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(ConnectionString);

//Create hello service client object for credentialed access toohello Blob service.
CloudBlobClient blobClient = storageAccount.CreateCloudBlobClient();

// Retrieve a reference tooa container.
CloudBlobContainer container = blobClient.GetContainerReference("mycontainer");

// Create hello container if it does not already exist.
container.CreateIfNotExists();

// Fetch container properties and write out their values.
container.FetchAttributes();
Console.WriteLine("Properties for container {0}", container.StorageUri.PrimaryUri.ToString());
Console.WriteLine("LastModifiedUTC: {0}", container.Properties.LastModified.ToString());
Console.WriteLine("ETag: {0}", container.Properties.ETag);
Console.WriteLine();
```

## <a name="setting-and-retrieving-metadata"></a>Definir e obter os metadados
Pode especificar metadados como um ou mais pares nome-valor num recurso blob ou contentor. metadados tooset, adicionar os pares nome-valor toohello **metadados** coleção no recurso de Olá, em seguida, chame Olá **SetMetadata** Olá do método toosave valores toohello serviço.

> [!NOTE]
> nome Olá os seus metadados estão em conformidade com tem toohello convenções de nomenclatura para os identificadores de c#.
>
>

Olá exemplo de código seguinte define metadados de um contentor. Um valor é definido através da coleção de Olá **adicionar** método. Olá outro valor é definido utilizando a sintaxe de chave/valor implícito. Ambos são válidas.

```csharp
public static void AddContainerMetadata(CloudBlobContainer container)
{
    //Add some metadata toohello container.
    container.Metadata.Add("docType", "textDocuments");
    container.Metadata["category"] = "guidance";

    //Set hello container's metadata.
    container.SetMetadata();
}
```

metadados tooretrieve, chamada Olá **FetchAttributes** método no seu Olá de toopopulate blob ou contentor **metadados** coleção, em seguida, lido valores Olá, conforme mostrado no exemplo Olá abaixo.

```csharp
public static void ListContainerMetadata(CloudBlobContainer container)
{
    //Fetch container attributes in order toopopulate hello container's properties and metadata.
    container.FetchAttributes();

    //Enumerate hello container's metadata.
    Console.WriteLine("Container metadata:");
    foreach (var metadataItem in container.Metadata)
    {
        Console.WriteLine("\tKey: {0}", metadataItem.Key);
        Console.WriteLine("\tValue: {0}", metadataItem.Value);
    }
}
```

## <a name="next-steps"></a>Passos seguintes
* [Biblioteca de clientes do Storage do Azure para referência do .NET](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [Biblioteca de clientes do Storage do Azure para o pacote NuGet do .NET](https://www.nuget.org/packages/WindowsAzure.Storage/)
