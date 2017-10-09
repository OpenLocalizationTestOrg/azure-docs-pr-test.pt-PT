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
# <a name="set-and-retrieve-properties-and-metadata"></a><span data-ttu-id="9f100-103">Definir e obter propriedades e metadados</span><span class="sxs-lookup"><span data-stu-id="9f100-103">Set and retrieve properties and metadata</span></span>

<span data-ttu-id="9f100-104">Objetos nas propriedades do sistema de suporte de armazenamento do Azure e os metadados definidos pelo utilizador, além disso toohello dados que contêm.</span><span class="sxs-lookup"><span data-stu-id="9f100-104">Objects in Azure Storage support system properties and user-defined metadata, in addition toohello data they contain.</span></span> <span data-ttu-id="9f100-105">Este artigo aborda as propriedades do sistema de gestão e os metadados definidos pelo utilizador com Olá [biblioteca de clientes do Storage do Azure para .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span><span class="sxs-lookup"><span data-stu-id="9f100-105">This article discusses managing system properties and user-defined metadata with hello [Azure Storage Client Library for .NET](https://www.nuget.org/packages/WindowsAzure.Storage/).</span></span>

* <span data-ttu-id="9f100-106">**Propriedades do sistema**: existem propriedades do sistema em cada recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9f100-106">**System properties**: System properties exist on each storage resource.</span></span> <span data-ttu-id="9f100-107">Alguns deles possam ler ou definir, enquanto outras são só de leitura.</span><span class="sxs-lookup"><span data-stu-id="9f100-107">Some of them can be read or set, while others are read-only.</span></span> <span data-ttu-id="9f100-108">Em bastidores Olá, algumas propriedades do sistema correspondem toocertain cabeçalhos de HTTP padrão.</span><span class="sxs-lookup"><span data-stu-id="9f100-108">Under hello covers, some system properties correspond toocertain standard HTTP headers.</span></span> <span data-ttu-id="9f100-109">biblioteca de clientes do storage do Azure Olá mantém estas por si.</span><span class="sxs-lookup"><span data-stu-id="9f100-109">hello Azure storage client library maintains these for you.</span></span>

* <span data-ttu-id="9f100-110">**Os metadados definidos pelo utilizador**: os metadados definidos pelo utilizador são metadados que especifica um recurso especificado no formato Olá um par nome / valor.</span><span class="sxs-lookup"><span data-stu-id="9f100-110">**User-defined metadata**: User-defined metadata is metadata that you specify on a given resource in hello form of a name-value pair.</span></span> <span data-ttu-id="9f100-111">Pode utilizar valores adicionais do metadados toostore com um recurso de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9f100-111">You can use metadata toostore additional values with a storage resource.</span></span> <span data-ttu-id="9f100-112">Estes valores de metadados adicionais são os seus próprios apenas para fins de e não afetam a forma como se comporta recursos Olá.</span><span class="sxs-lookup"><span data-stu-id="9f100-112">These additional metadata values are for your own purposes only, and do not affect how hello resource behaves.</span></span>

<span data-ttu-id="9f100-113">Ao obter valores de propriedade e metadados para um recurso de armazenamento é um processo de dois passos.</span><span class="sxs-lookup"><span data-stu-id="9f100-113">Retrieving property and metadata values for a storage resource is a two-step process.</span></span> <span data-ttu-id="9f100-114">Antes de ler estes valores, tem explicitamente obtê-los ao chamar Olá **FetchAttributes** método.</span><span class="sxs-lookup"><span data-stu-id="9f100-114">Before you can read these values, you must explicitly fetch them by calling hello **FetchAttributes** method.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9f100-115">Os valores de propriedade e metadados para um recurso de armazenamento não são preenchidos a menos que tem de chamar um dos Olá **FetchAttributes** métodos.</span><span class="sxs-lookup"><span data-stu-id="9f100-115">Property and metadata values for a storage resource are not populated unless you call one of hello **FetchAttributes** methods.</span></span>
>
> <span data-ttu-id="9f100-116">Receberá um `400 Bad Request` se qualquer pares nome/valor contém carateres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="9f100-116">You will receive a `400 Bad Request` if any name/value pairs contain non-ASCII characters.</span></span> <span data-ttu-id="9f100-117">Metadados pares de nome/valor são os cabeçalhos de HTTP válidos e, pelo que tem de respeitar as restrições de tooall que rege cabeçalhos de HTTP.</span><span class="sxs-lookup"><span data-stu-id="9f100-117">Metadata name/value pairs are valid HTTP headers, and so must adhere tooall restrictions governing HTTP headers.</span></span> <span data-ttu-id="9f100-118">Por conseguinte, é recomendado que utilize a codificação do URL ou codificação Base64 para os nomes e valores que contêm carateres não ASCII.</span><span class="sxs-lookup"><span data-stu-id="9f100-118">It is therefore recommended that you use URL encoding or Base64 encoding for names and values containing non-ASCII characters.</span></span>
>

## <a name="setting-and-retrieving-properties"></a><span data-ttu-id="9f100-119">Definir e obter propriedades</span><span class="sxs-lookup"><span data-stu-id="9f100-119">Setting and retrieving properties</span></span>
<span data-ttu-id="9f100-120">os valores de propriedade tooretrieve, chamada Olá **FetchAttributes** método no seu blob ou contentor toopopulate Olá propriedades, em seguida, leia os valores de Olá.</span><span class="sxs-lookup"><span data-stu-id="9f100-120">tooretrieve property values, call hello **FetchAttributes** method on your blob or container toopopulate hello properties, then read hello values.</span></span>

<span data-ttu-id="9f100-121">tooset propriedades de um objeto, especifique o valor da propriedade Olá, em seguida, invoque Olá **SetProperties** método.</span><span class="sxs-lookup"><span data-stu-id="9f100-121">tooset properties on an object, specify hello property value, then call hello **SetProperties** method.</span></span>

<span data-ttu-id="9f100-122">Olá exemplo de código seguinte cria um contentor, em seguida, escreve algumas da janela de consola de tooa de valores de propriedade.</span><span class="sxs-lookup"><span data-stu-id="9f100-122">hello following code example creates a container, then writes some of its property values tooa console window.</span></span>

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

## <a name="setting-and-retrieving-metadata"></a><span data-ttu-id="9f100-123">Definir e obter os metadados</span><span class="sxs-lookup"><span data-stu-id="9f100-123">Setting and retrieving metadata</span></span>
<span data-ttu-id="9f100-124">Pode especificar metadados como um ou mais pares nome-valor num recurso blob ou contentor.</span><span class="sxs-lookup"><span data-stu-id="9f100-124">You can specify metadata as one or more name-value pairs on a blob or container resource.</span></span> <span data-ttu-id="9f100-125">metadados tooset, adicionar os pares nome-valor toohello **metadados** coleção no recurso de Olá, em seguida, chame Olá **SetMetadata** Olá do método toosave valores toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="9f100-125">tooset metadata, add name-value pairs toohello **Metadata** collection on hello resource, then call hello **SetMetadata** method toosave hello values toohello service.</span></span>

> [!NOTE]
> <span data-ttu-id="9f100-126">nome Olá os seus metadados estão em conformidade com tem toohello convenções de nomenclatura para os identificadores de c#.</span><span class="sxs-lookup"><span data-stu-id="9f100-126">hello name of your metadata must conform toohello naming conventions for C# identifiers.</span></span>
>
>

<span data-ttu-id="9f100-127">Olá exemplo de código seguinte define metadados de um contentor.</span><span class="sxs-lookup"><span data-stu-id="9f100-127">hello following code example sets metadata on a container.</span></span> <span data-ttu-id="9f100-128">Um valor é definido através da coleção de Olá **adicionar** método.</span><span class="sxs-lookup"><span data-stu-id="9f100-128">One value is set using hello collection's **Add** method.</span></span> <span data-ttu-id="9f100-129">Olá outro valor é definido utilizando a sintaxe de chave/valor implícito.</span><span class="sxs-lookup"><span data-stu-id="9f100-129">hello other value is set using implicit key/value syntax.</span></span> <span data-ttu-id="9f100-130">Ambos são válidas.</span><span class="sxs-lookup"><span data-stu-id="9f100-130">Both are valid.</span></span>

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

<span data-ttu-id="9f100-131">metadados tooretrieve, chamada Olá **FetchAttributes** método no seu Olá de toopopulate blob ou contentor **metadados** coleção, em seguida, lido valores Olá, conforme mostrado no exemplo Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="9f100-131">tooretrieve metadata, call hello **FetchAttributes** method on your blob or container toopopulate hello **Metadata** collection, then read hello values, as shown in hello example below.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="9f100-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9f100-132">Next steps</span></span>
* [<span data-ttu-id="9f100-133">Biblioteca de clientes do Storage do Azure para referência do .NET</span><span class="sxs-lookup"><span data-stu-id="9f100-133">Azure Storage Client Library for .NET reference</span></span>](/dotnet/api/?term=Microsoft.WindowsAzure.Storage)
* [<span data-ttu-id="9f100-134">Biblioteca de clientes do Storage do Azure para o pacote NuGet do .NET</span><span class="sxs-lookup"><span data-stu-id="9f100-134">Azure Storage Client Library for .NET NuGet package</span></span>](https://www.nuget.org/packages/WindowsAzure.Storage/)
