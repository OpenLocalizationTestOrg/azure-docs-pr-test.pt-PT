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
# <a name="azure-importexport-service-metadata-and-properties-file-format"></a>Do Azure para importar/exportar serviço metadados e as propriedades de formato de ficheiro
Pode especificar propriedades de um ou mais blobs e metadados como parte de uma tarefa de importação ou uma tarefa de exportação. metadados tooset ou propriedades de blobs a ser criadas como parte de uma tarefa de importação, forneça um ficheiro de metadados ou propriedades no disco rígido Olá contendo Olá dados toobe importado. Para uma tarefa de exportação, metadados e as propriedades são escritas tooa ficheiro de metadados ou propriedades que está incluído no disco rígido Olá devolvido tooyou.  
  
## <a name="metadata-file-format"></a>Formato de ficheiro de metadados  
formato de Olá de um ficheiro de metadados é o seguinte:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
[<metadata-name-1>metadata-value-1</metadata-name-1>]  
[<metadata-name-2>metadata-value-2</metadata-name-2>]  
. . .  
</Metadata>  
```
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`Metadata`|Elemento raiz|elemento de raiz de Olá de ficheiro de metadados de Olá.|  
|`metadata-name`|Cadeia|Opcional. elemento XML de Olá Especifica o nome de Olá dos metadados de Olá para BLOBs Olá e respetivo valor Especifica o valor de Olá da definição de metadados de Olá.|  
  
## <a name="properties-file-format"></a>Formato de ficheiro de propriedades  
formato de Olá de um ficheiro de propriedades é o seguinte:  
  
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
  
|Elemento XML|Tipo|Descrição|  
|-----------------|----------|-----------------|  
|`Properties`|Elemento raiz|elemento de raiz de Olá do ficheiro de propriedades de Olá.|  
|`Last-Modified`|Cadeia|Opcional. Olá last-modified tempo para o blob Olá. Para as tarefas de exportação apenas.|  
|`Etag`|Cadeia|Opcional. Olá valor ETag de blob. Para as tarefas de exportação apenas.|  
|`Content-Length`|Cadeia|Opcional. tamanho de Olá do blob Olá em bytes. Para as tarefas de exportação apenas.|  
|`Content-Type`|Cadeia|Opcional. tipo de conteúdo de Olá do blob Olá.|  
|`Content-MD5`|Cadeia|Opcional. Olá hash MD5 de blob.|  
|`Content-Encoding`|Cadeia|Opcional. Olá, conteúdo do blob codificação.|  
|`Content-Language`|Cadeia|Opcional. Olá, idioma de conteúdo do blob.|  
|`Cache-Control`|Cadeia|Opcional. cadeia de controlo de cache de Olá para BLOBs Olá.|  

## <a name="next-steps"></a>Passos seguintes

Consulte [defina as propriedades de blob](/rest/api/storageservices/set-blob-properties), [definir metadados do Blob](/rest/api/storageservices/set-blob-metadata), e [definição e ao obter propriedades e os metadados para recursos do blob](/rest/api/storageservices/setting-and-retrieving-properties-and-metadata-for-blob-resources) para regras de detalhado sobre a definição de metadados de blob e propriedades.
