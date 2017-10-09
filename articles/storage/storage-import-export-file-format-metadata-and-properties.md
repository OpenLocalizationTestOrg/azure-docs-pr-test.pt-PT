---
title: formato de ficheiro de aaaAzure importar/exportar os metadados e propriedades | Microsoft Docs
description: "Saiba como metadados toospecify e propriedades de um ou mais blobs que fazem parte de uma importação ou exportação tarefa."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 840364c6-d9a8-4b43-a9f3-f7441c625069
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: bb13c1f1a27baea77298cb224970cd521d02d8c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a><span data-ttu-id="75036-103">Do Azure para importar/exportar serviço metadados e as propriedades de formato de ficheiro</span><span class="sxs-lookup"><span data-stu-id="75036-103">Azure Import/Export service metadata and properties file format</span></span>
<span data-ttu-id="75036-104">Pode especificar propriedades de um ou mais blobs e metadados como parte de uma tarefa de importação ou uma tarefa de exportação.</span><span class="sxs-lookup"><span data-stu-id="75036-104">You can specify metadata and properties for one or more blobs as part of an import job or an export job.</span></span> <span data-ttu-id="75036-105">metadados tooset ou propriedades de blobs a ser criadas como parte de uma tarefa de importação, forneça um ficheiro de metadados ou propriedades no disco rígido Olá contendo Olá dados toobe importado.</span><span class="sxs-lookup"><span data-stu-id="75036-105">tooset metadata or properties for blobs being created as part of an import job, you provide a metadata or properties file on hello hard drive containing hello data toobe imported.</span></span> <span data-ttu-id="75036-106">Para uma tarefa de exportação, metadados e as propriedades são escritas tooa ficheiro de metadados ou propriedades que está incluído no disco rígido Olá devolvido tooyou.</span><span class="sxs-lookup"><span data-stu-id="75036-106">For an export job, metadata and properties are written tooa metadata or properties file that is included on hello hard drive returned tooyou.</span></span>  
  
## <a name="metadata-file-format"></a><span data-ttu-id="75036-107">Formato de ficheiro de metadados</span><span class="sxs-lookup"><span data-stu-id="75036-107">Metadata file format</span></span>  
<span data-ttu-id="75036-108">formato de Olá de um ficheiro de metadados é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75036-108">hello format of a metadata file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|<span data-ttu-id="75036-109">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="75036-109">XML Element</span></span>|<span data-ttu-id="75036-110">Tipo</span><span class="sxs-lookup"><span data-stu-id="75036-110">Type</span></span>|<span data-ttu-id="75036-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="75036-111">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Metadata`|<span data-ttu-id="75036-112">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="75036-112">Root element</span></span>|<span data-ttu-id="75036-113">elemento de raiz de Olá de ficheiro de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-113">hello root element of hello metadata file.</span></span>|  
|`metadata-name`|<span data-ttu-id="75036-114">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-114">String</span></span>|<span data-ttu-id="75036-115">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-115">Optional.</span></span> <span data-ttu-id="75036-116">elemento XML de Olá Especifica o nome de Olá dos metadados de Olá para BLOBs Olá e respetivo valor Especifica o valor de Olá da definição de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-116">hello XML element specifies hello name of hello metadata for hello blob, and its value specifies hello value of hello metadata setting.</span></span>|  
  
## <a name="properties-file-format"></a><span data-ttu-id="75036-117">Formato de ficheiro de propriedades</span><span class="sxs-lookup"><span data-stu-id="75036-117">Properties file format</span></span>  
<span data-ttu-id="75036-118">formato de Olá de um ficheiro de propriedades é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="75036-118">hello format of a properties file is as follows:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
[<Last-Modified>date-time-value</Last-Modified>]  
[<Etag>etag</Etag>]  
[<Content-Length>size-in-bytes<Content-Length>]  
[<Content-Type>content-type</Content-Type>]  
[<Content-MD5>content-md5</Content-MD5>]  
[<Content-Encoding>content-encoding</Content-Encoding>]  
[<Content-Language>content-language</Content-Language>]  
[<Cache-Control>cache-control</Cache-Control>]  
</Properties>  
```
  
|<span data-ttu-id="75036-119">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="75036-119">XML Element</span></span>|<span data-ttu-id="75036-120">Tipo</span><span class="sxs-lookup"><span data-stu-id="75036-120">Type</span></span>|<span data-ttu-id="75036-121">Descrição</span><span class="sxs-lookup"><span data-stu-id="75036-121">Description</span></span>|  
|-----------------|----------|-----------------|  
|`Properties`|<span data-ttu-id="75036-122">Elemento raiz</span><span class="sxs-lookup"><span data-stu-id="75036-122">Root element</span></span>|<span data-ttu-id="75036-123">elemento de raiz de Olá do ficheiro de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-123">hello root element of hello properties file.</span></span>|  
|`Last-Modified`|<span data-ttu-id="75036-124">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-124">String</span></span>|<span data-ttu-id="75036-125">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-125">Optional.</span></span> <span data-ttu-id="75036-126">Olá last-modified tempo para o blob Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-126">hello last-modified time for hello blob.</span></span> <span data-ttu-id="75036-127">Para as tarefas de exportação apenas.</span><span class="sxs-lookup"><span data-stu-id="75036-127">For export jobs only.</span></span>|  
|`Etag`|<span data-ttu-id="75036-128">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-128">String</span></span>|<span data-ttu-id="75036-129">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-129">Optional.</span></span> <span data-ttu-id="75036-130">Olá valor ETag de blob.</span><span class="sxs-lookup"><span data-stu-id="75036-130">hello blob's ETag value.</span></span> <span data-ttu-id="75036-131">Para as tarefas de exportação apenas.</span><span class="sxs-lookup"><span data-stu-id="75036-131">For export jobs only.</span></span>|  
|`Content-Length`|<span data-ttu-id="75036-132">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-132">String</span></span>|<span data-ttu-id="75036-133">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-133">Optional.</span></span> <span data-ttu-id="75036-134">tamanho de Olá do blob Olá em bytes.</span><span class="sxs-lookup"><span data-stu-id="75036-134">hello size of hello blob in bytes.</span></span> <span data-ttu-id="75036-135">Para as tarefas de exportação apenas.</span><span class="sxs-lookup"><span data-stu-id="75036-135">For export jobs only.</span></span>|  
|`Content-Type`|<span data-ttu-id="75036-136">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-136">String</span></span>|<span data-ttu-id="75036-137">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-137">Optional.</span></span> <span data-ttu-id="75036-138">tipo de conteúdo de Olá do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-138">hello content type of hello blob.</span></span>|  
|`Content-MD5`|<span data-ttu-id="75036-139">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-139">String</span></span>|<span data-ttu-id="75036-140">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-140">Optional.</span></span> <span data-ttu-id="75036-141">Olá hash MD5 de blob.</span><span class="sxs-lookup"><span data-stu-id="75036-141">hello blob's MD5 hash.</span></span>|  
|`Content-Encoding`|<span data-ttu-id="75036-142">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-142">String</span></span>|<span data-ttu-id="75036-143">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-143">Optional.</span></span> <span data-ttu-id="75036-144">Olá, conteúdo do blob codificação.</span><span class="sxs-lookup"><span data-stu-id="75036-144">hello blob's content encoding.</span></span>|  
|`Content-Language`|<span data-ttu-id="75036-145">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-145">String</span></span>|<span data-ttu-id="75036-146">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-146">Optional.</span></span> <span data-ttu-id="75036-147">Olá, idioma de conteúdo do blob.</span><span class="sxs-lookup"><span data-stu-id="75036-147">hello blob's content language.</span></span>|  
|`Cache-Control`|<span data-ttu-id="75036-148">Cadeia</span><span class="sxs-lookup"><span data-stu-id="75036-148">String</span></span>|<span data-ttu-id="75036-149">Opcional.</span><span class="sxs-lookup"><span data-stu-id="75036-149">Optional.</span></span> <span data-ttu-id="75036-150">cadeia de controlo de cache de Olá para BLOBs Olá.</span><span class="sxs-lookup"><span data-stu-id="75036-150">hello cache control string for hello blob.</span></span>|  

## <a name="next-steps"></a><span data-ttu-id="75036-151">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="75036-151">Next steps</span></span>

<span data-ttu-id="75036-152">Consulte [defina as propriedades de blob](/rest/api/storageservices/set-blob-properties), [definir metadados do Blob](/rest/api/storageservices/set-blob-metadata), e [definição e ao obter propriedades e os metadados para recursos do blob](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) para regras de detalhado sobre a definição de metadados de blob e propriedades.</span><span class="sxs-lookup"><span data-stu-id="75036-152">See [Set blob properties](/rest/api/storageservices/set-blob-properties), [Set Blob Metadata](/rest/api/storageservices/set-blob-metadata), and [Setting and retrieving properties and metadata for blob resources](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) for detailed rules about setting blob metadata and properties.</span></span>
