---
title: "formato de ficheiro de registo de importação/exportação aaaAzure | Microsoft Docs"
description: "Saiba mais sobre o formato de Olá Olá dos ficheiros de registo criado quando são executados os passos para uma tarefa de serviço de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 38cc16bd-ad55-4625-9a85-e1726c35fd1b
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 15a652455aa947922af0aa39ccefe68811a3db19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-importexport-service-log-file-format"></a><span data-ttu-id="7e406-103">Formato do ficheiro de registo de serviço do Azure para importar/exportar</span><span class="sxs-lookup"><span data-stu-id="7e406-103">Azure Import/Export service log file format</span></span>
<span data-ttu-id="7e406-104">Quando Olá serviço de importação/exportação do Microsoft Azure efetua uma ação num disco como parte de uma tarefa de importação ou uma tarefa de exportação, os registos são escritos tooblock blobs na conta do storage Olá associada com essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="7e406-104">When hello Microsoft Azure Import/Export service performs an action on a drive as part of an import job or an export job, logs are written tooblock blobs in hello storage account associated with that job.</span></span>  
  
<span data-ttu-id="7e406-105">Existem dois registos que podem ser escritos pelo Olá serviço importar/exportar:</span><span class="sxs-lookup"><span data-stu-id="7e406-105">There are two logs that may be written by hello Import/Export service:</span></span>  
  
-   <span data-ttu-id="7e406-106">registo de erros de Olá sempre é gerado no evento Olá de um erro.</span><span class="sxs-lookup"><span data-stu-id="7e406-106">hello error log is always generated in hello event of an error.</span></span>  
  
-   <span data-ttu-id="7e406-107">Olá registo verboso não está ativado por predefinição, mas pode ser ativado por definição Olá `EnableVerboseLog` propriedade um [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operação.</span><span class="sxs-lookup"><span data-stu-id="7e406-107">hello verbose log is not enabled by default, but may be enabled by setting hello `EnableVerboseLog` property on a [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation.</span></span>  
  
## <a name="log-file-location"></a><span data-ttu-id="7e406-108">Localização do ficheiro de registo</span><span class="sxs-lookup"><span data-stu-id="7e406-108">Log file location</span></span>  
<span data-ttu-id="7e406-109">Olá registos são escritos tooblock blobs no contentor de Olá ou diretório virtual especificado pelo Olá `ImportExportStatesPath` definição, que podem ser definidas num `Put Job` operação.</span><span class="sxs-lookup"><span data-stu-id="7e406-109">hello logs are written tooblock blobs in hello container or virtual directory specified by hello `ImportExportStatesPath` setting, which you can set on a `Put Job` operation.</span></span> <span data-ttu-id="7e406-110">Olá localização toowhich Olá registos são escritos depende de como a autenticação é especificada para a tarefa de Olá, juntamente com o valor de Olá especificado para `ImportExportStatesPath`.</span><span class="sxs-lookup"><span data-stu-id="7e406-110">hello location toowhich hello logs are written depends on how authentication is specified for hello job, together with hello value specified for `ImportExportStatesPath`.</span></span> <span data-ttu-id="7e406-111">Autenticação para a tarefa de Olá pode ser especificada através de uma chave de conta de armazenamento ou de um contentor SAS (assinatura de acesso partilhado).</span><span class="sxs-lookup"><span data-stu-id="7e406-111">Authentication for hello job may be specified via a storage account key, or a container SAS (shared access signature).</span></span>  
  
<span data-ttu-id="7e406-112">nome de Olá do contentor de Olá ou diretório virtual poderá a ser Olá predefinido nome de `waimportexport`, ou outro contentor ou nome do diretório virtual que especificou.</span><span class="sxs-lookup"><span data-stu-id="7e406-112">hello name of hello container or virtual directory may either be hello default name of `waimportexport`, or another container or virtual directory name that you specify.</span></span>  
  
<span data-ttu-id="7e406-113">tabela de Olá abaixo mostra as opções de possíveis Olá:</span><span class="sxs-lookup"><span data-stu-id="7e406-113">hello table below shows hello possible options:</span></span>  
  
|<span data-ttu-id="7e406-114">Método de Autenticação</span><span class="sxs-lookup"><span data-stu-id="7e406-114">Authentication Method</span></span>|<span data-ttu-id="7e406-115">O valor de `ImportExportStatesPath`elemento</span><span class="sxs-lookup"><span data-stu-id="7e406-115">Value of `ImportExportStatesPath`Element</span></span>|<span data-ttu-id="7e406-116">Localização de Blobs de registo</span><span class="sxs-lookup"><span data-stu-id="7e406-116">Location of Log Blobs</span></span>|  
|---------------------------|----------------------------------------------|---------------------------|  
|<span data-ttu-id="7e406-117">Chave de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7e406-117">Storage account key</span></span>|<span data-ttu-id="7e406-118">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="7e406-118">Default value</span></span>|<span data-ttu-id="7e406-119">Um contentor com o nome `waimportexport`, que é o contentor do Olá predefinido.</span><span class="sxs-lookup"><span data-stu-id="7e406-119">A container named `waimportexport`, which is hello default container.</span></span> <span data-ttu-id="7e406-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7e406-120">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/waimportexport`|  
|<span data-ttu-id="7e406-121">Chave de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="7e406-121">Storage account key</span></span>|<span data-ttu-id="7e406-122">Valor de utilizador especificado</span><span class="sxs-lookup"><span data-stu-id="7e406-122">User-specified value</span></span>|<span data-ttu-id="7e406-123">Um contentor designado por utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-123">A container named by hello user.</span></span> <span data-ttu-id="7e406-124">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7e406-124">For example:</span></span><br /><br /> `https://myaccount.blob.core.windows.net/mylogcontainer`|  
|<span data-ttu-id="7e406-125">Contentor SAS</span><span class="sxs-lookup"><span data-stu-id="7e406-125">Container SAS</span></span>|<span data-ttu-id="7e406-126">Valor predefinido</span><span class="sxs-lookup"><span data-stu-id="7e406-126">Default value</span></span>|<span data-ttu-id="7e406-127">Um diretório virtual com o nome `waimportexport`, que é o nome predefinido de Olá, por baixo do contentor de Olá especificado na Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="7e406-127">A virtual directory named `waimportexport`, which is hello default name, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="7e406-128">Por exemplo, se Olá SAS especificado para a tarefa de Olá é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, em seguida, a localização de registo Olá seria`https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span><span class="sxs-lookup"><span data-stu-id="7e406-128">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport`</span></span>|  
|<span data-ttu-id="7e406-129">Contentor SAS</span><span class="sxs-lookup"><span data-stu-id="7e406-129">Container SAS</span></span>|<span data-ttu-id="7e406-130">Valor de utilizador especificado</span><span class="sxs-lookup"><span data-stu-id="7e406-130">User-specified value</span></span>|<span data-ttu-id="7e406-131">Um diretório virtual com o nome pelo utilizador Olá, por baixo do contentor de Olá especificado na Olá SAS.</span><span class="sxs-lookup"><span data-stu-id="7e406-131">A virtual directory named by hello user, beneath hello container specified in hello SAS.</span></span><br /><br /> <span data-ttu-id="7e406-132">Por exemplo, se Olá SAS especificado para a tarefa de Olá é `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, e Olá especificado diretório virtual é denominado `mylogblobs`, em seguida, a localização de registo Olá seria `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span><span class="sxs-lookup"><span data-stu-id="7e406-132">For example, if hello SAS specified for hello job is  `https://myaccount.blob.core.windows.net/mylogcontainer?sv=2012-02-12&se=2015-05-22T06%3A54%3A55Z&sr=c&sp=wl&sig=sigvalue`, and hello specified virtual directory is named `mylogblobs`, then hello log location would be `https://myaccount.blob.core.windows.net/mylogcontainer/waimportexport/mylogblobs`.</span></span>|  
  
<span data-ttu-id="7e406-133">Pode obter URL Olá para registos de verbosos e erro Olá ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação.</span><span class="sxs-lookup"><span data-stu-id="7e406-133">You can retrieve hello URL for hello error and verbose logs by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation.</span></span> <span data-ttu-id="7e406-134">estão disponíveis registos de Olá após a conclusão do processamento da unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-134">hello logs are available after processing of hello drive is complete.</span></span>  
  
## <a name="log-file-format"></a><span data-ttu-id="7e406-135">Formato de ficheiro de registo</span><span class="sxs-lookup"><span data-stu-id="7e406-135">Log file format</span></span>  
<span data-ttu-id="7e406-136">Olá formato para ambos os registos é Olá mesmo: um blob que contém XML as descrições dos eventos de Olá que ocorreram durante a cópia de blobs entre o disco rígido Olá e conta hello do cliente.</span><span class="sxs-lookup"><span data-stu-id="7e406-136">hello format for both logs is hello same: a blob containing XML descriptions of hello events that occurred while copying blobs between hello hard drive and hello customer's account.</span></span>  
  
<span data-ttu-id="7e406-137">registo verboso Olá contém informações sobre o estado de Olá de operação de cópia de Olá para cada blob (para uma tarefa de importação) ou o ficheiro (para uma tarefa de exportação), enquanto que o registo de erros de Olá contém apenas informações de Olá para blobs ou ficheiros que encontrou erros durante a Olá importar ou exportar a tarefa.</span><span class="sxs-lookup"><span data-stu-id="7e406-137">hello verbose log contains complete information about hello status of hello copy operation for every blob (for an import job) or file (for an export job), whereas hello error log contains only hello information for blobs or files that encountered errors during hello import or export job.</span></span>  
  
<span data-ttu-id="7e406-138">formato de registo verboso Olá é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7e406-138">hello verbose log format is shown below.</span></span> <span data-ttu-id="7e406-139">registo de erros de Olá tem Olá mesmo estrutura, mas filtra operações com êxito.</span><span class="sxs-lookup"><span data-stu-id="7e406-139">hello error log has hello same structure, but filters out successful operations.</span></span>  

```xml
<DriveLog Version="2014-11-01">  
  <DriveId>drive-id</DriveId>  
  [<Blob Status="blob-status">  
   <BlobPath>blob-path</BlobPath>  
   <FilePath>file-path</FilePath>  
   [<Snapshot>snapshot</Snapshot>]  
   <Length>length</Length>  
   [<LastModified>last-modified</LastModified>]  
   [<ImportDisposition Status="import-disposition-status">import-disposition</ImportDisposition>]  
   [page-range-list-or-block-list]  
   [metadata-status]  
   [properties-status]  
  </Blob>]  
  [<Blob>  
    . . .  
  </Blob>]  
  <Status>drive-status</Status>  
</DriveLog>  
  
page-range-list-or-block-list ::= 
  page-range-list | block-list  
  
page-range-list ::=   
<PageRangeList>  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
      [<PageRange Offset="page-range-offset" Length="page-range-length"   
       [Hash="md5-hash"] Status="page-range-status"/>]  
</PageRangeList>  
  
block-list ::=  
<BlockList>  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]  
       [Hash="md5-hash"] Status="block-status"/>]  
      [<Block Offset="block-offset" Length="block-length" [Id="block-id"]   
       [Hash="md5-hash"] Status="block-status"/>]  
</BlockList>  
  
metadata-status ::=  
<Metadata Status="metadata-status">  
   [<GlobalPath Hash="md5-hash">global-metadata-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">metadata-file-path</Path>]  
</Metadata>  
  
properties-status ::=  
<Properties Status="properties-status">  
   [<GlobalPath Hash="md5-hash">global-properties-file-path</GlobalPath>]  
   [<Path Hash="md5-hash">properties-file-path</Path>]  
</Properties>  
```

<span data-ttu-id="7e406-140">Olá seguinte tabela descreve os elementos de Olá Olá do ficheiro de registo.</span><span class="sxs-lookup"><span data-stu-id="7e406-140">hello following table describes hello elements of hello log file.</span></span>  
  
|<span data-ttu-id="7e406-141">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-141">XML Element</span></span>|<span data-ttu-id="7e406-142">Tipo</span><span class="sxs-lookup"><span data-stu-id="7e406-142">Type</span></span>|<span data-ttu-id="7e406-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-143">Description</span></span>|  
|-----------------|----------|-----------------|  
|`DriveLog`|<span data-ttu-id="7e406-144">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-144">XML Element</span></span>|<span data-ttu-id="7e406-145">Representa um registo de unidade.</span><span class="sxs-lookup"><span data-stu-id="7e406-145">Represents a drive log.</span></span>|  
|`Version`|<span data-ttu-id="7e406-146">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-146">Attribute, String</span></span>|<span data-ttu-id="7e406-147">versão de Olá do formato de registo Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-147">hello version of hello log format.</span></span>|  
|`DriveId`|<span data-ttu-id="7e406-148">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-148">String</span></span>|<span data-ttu-id="7e406-149">Olá, número de série de hardware da unidade.</span><span class="sxs-lookup"><span data-stu-id="7e406-149">hello drive's hardware serial number.</span></span>|  
|`Status`|<span data-ttu-id="7e406-150">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-150">String</span></span>|<span data-ttu-id="7e406-151">Estado de processamento de unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-151">Status of hello drive processing.</span></span> <span data-ttu-id="7e406-152">Consulte Olá `Drive Status Codes` tabela abaixo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="7e406-152">See hello `Drive Status Codes` table below for more information.</span></span>|  
|`Blob`|<span data-ttu-id="7e406-153">Aninhada elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-153">Nested XML element</span></span>|<span data-ttu-id="7e406-154">Representa um blob.</span><span class="sxs-lookup"><span data-stu-id="7e406-154">Represents a blob.</span></span>|  
|`Blob/BlobPath`|<span data-ttu-id="7e406-155">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-155">String</span></span>|<span data-ttu-id="7e406-156">URI de blob Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-156">hello URI of hello blob.</span></span>|  
|`Blob/FilePath`|<span data-ttu-id="7e406-157">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-157">String</span></span>|<span data-ttu-id="7e406-158">Olá caminho relativo toohello o ficheiro na unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-158">hello relative path toohello file on hello drive.</span></span>|  
|`Blob/Snapshot`|<span data-ttu-id="7e406-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="7e406-159">DateTime</span></span>|<span data-ttu-id="7e406-160">versão de instantâneo de Olá do blob Olá, para apenas uma tarefa de exportação.</span><span class="sxs-lookup"><span data-stu-id="7e406-160">hello snapshot version of hello blob, for an export job only.</span></span>|  
|`Blob/Length`|<span data-ttu-id="7e406-161">Número inteiro</span><span class="sxs-lookup"><span data-stu-id="7e406-161">Integer</span></span>|<span data-ttu-id="7e406-162">comprimento total Olá dos BLOBs Olá em bytes.</span><span class="sxs-lookup"><span data-stu-id="7e406-162">hello total length of hello blob in bytes.</span></span>|  
|`Blob/LastModified`|<span data-ttu-id="7e406-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="7e406-163">DateTime</span></span>|<span data-ttu-id="7e406-164">Olá data/hora esse blob Olá foi modificado pela última vez, para apenas uma tarefa de exportação.</span><span class="sxs-lookup"><span data-stu-id="7e406-164">hello date/time that hello blob was last modified, for an export job only.</span></span>|  
|`Blob/ImportDisposition`|<span data-ttu-id="7e406-165">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-165">String</span></span>|<span data-ttu-id="7e406-166">Olá importar disposição de blob Olá, apenas uma tarefa de importação.</span><span class="sxs-lookup"><span data-stu-id="7e406-166">hello import disposition of hello blob, for an import job only.</span></span>|  
|`Blob/ImportDisposition/@Status`|<span data-ttu-id="7e406-167">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-167">Attribute, String</span></span>|<span data-ttu-id="7e406-168">Estado de Olá de Olá importar disposição.</span><span class="sxs-lookup"><span data-stu-id="7e406-168">hello status of hello import disposition.</span></span>|  
|`PageRangeList`|<span data-ttu-id="7e406-169">Aninhada elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-169">Nested XML element</span></span>|<span data-ttu-id="7e406-170">Representa uma lista de intervalos de página para um blob de página.</span><span class="sxs-lookup"><span data-stu-id="7e406-170">Represents a list of page ranges for a page blob.</span></span>|  
|`PageRange`|<span data-ttu-id="7e406-171">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-171">XML element</span></span>|<span data-ttu-id="7e406-172">Representa um intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="7e406-172">Represents a page range.</span></span>|  
|`PageRange/@Offset`|<span data-ttu-id="7e406-173">Atributo de número inteiro</span><span class="sxs-lookup"><span data-stu-id="7e406-173">Attribute, Integer</span></span>|<span data-ttu-id="7e406-174">A partir de deslocamento do intervalo de páginas de Olá blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-174">Starting offset of hello page range in hello blob.</span></span>|  
|`PageRange/@Length`|<span data-ttu-id="7e406-175">Atributo de número inteiro</span><span class="sxs-lookup"><span data-stu-id="7e406-175">Attribute, Integer</span></span>|<span data-ttu-id="7e406-176">Comprimento em bytes do intervalo de páginas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-176">Length in bytes of hello page range.</span></span>|  
|`PageRange/@Hash`|<span data-ttu-id="7e406-177">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-177">Attribute, String</span></span>|<span data-ttu-id="7e406-178">Com codificação Base16 hash MD5 do intervalo de páginas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-178">Base16-encoded MD5 hash of hello page range.</span></span>|  
|`PageRange/@Status`|<span data-ttu-id="7e406-179">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-179">Attribute, String</span></span>|<span data-ttu-id="7e406-180">Estado do processamento de intervalo de páginas de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-180">Status of processing hello page range.</span></span>|  
|`BlockList`|<span data-ttu-id="7e406-181">Aninhada elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-181">Nested XML element</span></span>|<span data-ttu-id="7e406-182">Representa uma lista de blocos para um blob de blocos.</span><span class="sxs-lookup"><span data-stu-id="7e406-182">Represents a list of blocks for a block blob.</span></span>|  
|`Block`|<span data-ttu-id="7e406-183">Elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-183">XML element</span></span>|<span data-ttu-id="7e406-184">Representa um bloco.</span><span class="sxs-lookup"><span data-stu-id="7e406-184">Represents a block.</span></span>|  
|`Block/@Offset`|<span data-ttu-id="7e406-185">Atributo de número inteiro</span><span class="sxs-lookup"><span data-stu-id="7e406-185">Attribute, Integer</span></span>|<span data-ttu-id="7e406-186">Desvio inicial de Olá bloco num blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-186">Starting offset of hello block in hello blob.</span></span>|  
|`Block/@Length`|<span data-ttu-id="7e406-187">Atributo de número inteiro</span><span class="sxs-lookup"><span data-stu-id="7e406-187">Attribute, Integer</span></span>|<span data-ttu-id="7e406-188">Comprimento em bytes do bloco de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-188">Length in bytes of hello block.</span></span>|  
|`Block/@Id`|<span data-ttu-id="7e406-189">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-189">Attribute, String</span></span>|<span data-ttu-id="7e406-190">ID do bloco de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-190">hello block ID.</span></span>|  
|`Block/@Hash`|<span data-ttu-id="7e406-191">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-191">Attribute, String</span></span>|<span data-ttu-id="7e406-192">Com codificação Base16 hash MD5 do bloco de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-192">Base16-encoded MD5 hash of hello block.</span></span>|  
|`Block/@Status`|<span data-ttu-id="7e406-193">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-193">Attribute, String</span></span>|<span data-ttu-id="7e406-194">Estado do bloco de Olá de processamento.</span><span class="sxs-lookup"><span data-stu-id="7e406-194">Status of processing hello block.</span></span>|  
|`Metadata`|<span data-ttu-id="7e406-195">Aninhada elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-195">Nested XML element</span></span>|<span data-ttu-id="7e406-196">Representa os metadados do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-196">Represents hello blob's metadata.</span></span>|  
|`Metadata/@Status`|<span data-ttu-id="7e406-197">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-197">Attribute, String</span></span>|<span data-ttu-id="7e406-198">Estado de processamento de metadados do blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-198">Status of processing of hello blob metadata.</span></span>|  
|`Metadata/GlobalPath`|<span data-ttu-id="7e406-199">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-199">String</span></span>|<span data-ttu-id="7e406-200">Ficheiro de metadados globais do caminho relativo toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-200">Relative path toohello global metadata file.</span></span>|  
|`Metadata/GlobalPath/@Hash`|<span data-ttu-id="7e406-201">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-201">Attribute, String</span></span>|<span data-ttu-id="7e406-202">Com codificação Base16 hash MD5 do ficheiro de metadados globais Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-202">Base16-encoded MD5 hash of hello global metadata file.</span></span>|  
|`Metadata/Path`|<span data-ttu-id="7e406-203">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-203">String</span></span>|<span data-ttu-id="7e406-204">Ficheiro de metadados do caminho relativo toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-204">Relative path toohello metadata file.</span></span>|  
|`Metadata/Path/@Hash`|<span data-ttu-id="7e406-205">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-205">Attribute, String</span></span>|<span data-ttu-id="7e406-206">Com codificação Base16 MD5 hash de ficheiro de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-206">Base16-encoded MD5 hash of hello metadata file.</span></span>|  
|`Properties`|<span data-ttu-id="7e406-207">Aninhada elemento XML</span><span class="sxs-lookup"><span data-stu-id="7e406-207">Nested XML element</span></span>|<span data-ttu-id="7e406-208">Representa as propriedades de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-208">Represents hello blob properties.</span></span>|  
|`Properties/@Status`|<span data-ttu-id="7e406-209">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-209">Attribute, String</span></span>|<span data-ttu-id="7e406-210">Estado do processamento de propriedades de blob Olá, por exemplo, ficheiro não encontrado; foi concluída.</span><span class="sxs-lookup"><span data-stu-id="7e406-210">Status of processing hello blob properties, e.g. file not found, completed.</span></span>|  
|`Properties/GlobalPath`|<span data-ttu-id="7e406-211">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-211">String</span></span>|<span data-ttu-id="7e406-212">Ficheiros do caminho relativo toohello propriedades globais.</span><span class="sxs-lookup"><span data-stu-id="7e406-212">Relative path toohello global properties file.</span></span>|  
|`Properties/GlobalPath/@Hash`|<span data-ttu-id="7e406-213">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-213">Attribute, String</span></span>|<span data-ttu-id="7e406-214">Com codificação Base16 hash MD5 do ficheiro de propriedades globais Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-214">Base16-encoded MD5 hash of hello global properties file.</span></span>|  
|`Properties/Path`|<span data-ttu-id="7e406-215">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-215">String</span></span>|<span data-ttu-id="7e406-216">Ficheiro de propriedades do caminho relativo toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-216">Relative path toohello properties file.</span></span>|  
|`Properties/Path/@Hash`|<span data-ttu-id="7e406-217">Atributo, cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-217">Attribute, String</span></span>|<span data-ttu-id="7e406-218">Com codificação Base16 hash MD5 do ficheiro de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-218">Base16-encoded MD5 hash of hello properties file.</span></span>|  
|`Blob/Status`|<span data-ttu-id="7e406-219">Cadeia</span><span class="sxs-lookup"><span data-stu-id="7e406-219">String</span></span>|<span data-ttu-id="7e406-220">Estado do processamento de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-220">Status of processing hello blob.</span></span>|  
  
# <a name="drive-status-codes"></a><span data-ttu-id="7e406-221">Códigos de estado de unidade</span><span class="sxs-lookup"><span data-stu-id="7e406-221">Drive status codes</span></span>  
<span data-ttu-id="7e406-222">Olá tabela seguinte lista os códigos de estado de Olá para uma unidade de processamento.</span><span class="sxs-lookup"><span data-stu-id="7e406-222">hello following table lists hello status codes for processing a drive.</span></span>  
  
|<span data-ttu-id="7e406-223">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-223">Status code</span></span>|<span data-ttu-id="7e406-224">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-224">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7e406-225">unidade de Olá concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="7e406-225">hello drive has finished processing without any errors.</span></span>|  
|`CompletedWithWarnings`|<span data-ttu-id="7e406-226">unidade de Olá concluiu o processamento com avisos num ou mais blobs por dispositions de importação de Olá especificados para o blobs Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-226">hello drive has finished processing with warnings in one or more blobs per hello import dispositions specified for hello blobs.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="7e406-227">unidade de Olá foi concluída com erros de um ou mais blobs ou segmentos.</span><span class="sxs-lookup"><span data-stu-id="7e406-227">hello drive has finished with errors in one or more blobs or chunks.</span></span>|  
|`DiskNotFound`|<span data-ttu-id="7e406-228">Está localizado nenhum disco na unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-228">No disk is found on hello drive.</span></span>|  
|`VolumeNotNtfs`|<span data-ttu-id="7e406-229">Olá primeiro dados volume num disco Olá não está no formato NTFS.</span><span class="sxs-lookup"><span data-stu-id="7e406-229">hello first data volume on hello disk is not in NTFS format.</span></span>|  
|`DiskOperationFailed`|<span data-ttu-id="7e406-230">Ocorreu uma falha desconhecida ao realizar operações na unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-230">An unknown failure occurred when performing operations on hello drive.</span></span>|  
|`BitLockerVolumeNotFound`|<span data-ttu-id="7e406-231">Não foi encontrado nenhum volume encryptable do BitLocker.</span><span class="sxs-lookup"><span data-stu-id="7e406-231">No BitLocker encryptable volume is found.</span></span>|  
|`BitLockerNotActivated`|<span data-ttu-id="7e406-232">O BitLocker não estiver ativado num volume de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-232">BitLocker is not enabled on hello volume.</span></span>|  
|`BitLockerProtectorNotFound`|<span data-ttu-id="7e406-233">protetor de chave de palavra-passe numérica Olá não existe no volume de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-233">hello numerical password key protector does not exist on hello volume.</span></span>|  
|`BitLockerKeyInvalid`|<span data-ttu-id="7e406-234">Olá numérica palavra-passe fornecida não é possível desbloquear o volume de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-234">hello numerical password provided cannot unlock hello volume.</span></span>|  
|`BitLockerUnlockVolumeFailed`|<span data-ttu-id="7e406-235">Falha desconhecida tiver ocorrido durante a tentativa de volume de Olá toounlock.</span><span class="sxs-lookup"><span data-stu-id="7e406-235">Unknown failure has happened when trying toounlock hello volume.</span></span>|  
|`BitLockerFailed`|<span data-ttu-id="7e406-236">Ocorreu uma falha desconhecida ao executar operações de BitLocker.</span><span class="sxs-lookup"><span data-stu-id="7e406-236">An unknown failure occurred while performing BitLocker operations.</span></span>|  
|`ManifestNameInvalid`|<span data-ttu-id="7e406-237">nome de ficheiro de manifesto Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="7e406-237">hello manifest file name is invalid.</span></span>|  
|`ManifestNameTooLong`|<span data-ttu-id="7e406-238">nome de ficheiro de manifesto Olá é demasiado longo.</span><span class="sxs-lookup"><span data-stu-id="7e406-238">hello manifest file name is too long.</span></span>|  
|`ManifestNotFound`|<span data-ttu-id="7e406-239">o ficheiro de manifesto Olá não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="7e406-239">hello manifest file is not found.</span></span>|  
|`ManifestAccessDenied`|<span data-ttu-id="7e406-240">Ficheiro de manifesto de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="7e406-240">Access toohello manifest file is denied.</span></span>|  
|`ManifestCorrupted`|<span data-ttu-id="7e406-241">Olá ficheiro de manifesto está danificado (conteúdo Olá não corresponde ao respetivo hash).</span><span class="sxs-lookup"><span data-stu-id="7e406-241">hello manifest file is corrupted (hello content does not match its hash).</span></span>|  
|`ManifestFormatInvalid`|<span data-ttu-id="7e406-242">conteúdo de manifesto Olá não está em conformidade com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-242">hello manifest content does not conform toohello required format.</span></span>|  
|`ManifestDriveIdMismatch`|<span data-ttu-id="7e406-243">unidade de Olá não corresponde ao ID de ficheiro de manifesto Olá Olá uma leitura do disco de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-243">hello drive ID in hello manifest file does not match hello one read from hello drive.</span></span>|  
|`ReadManifestFailed`|<span data-ttu-id="7e406-244">Ocorreu um falha de e/s de disco ao ler o manifesto Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-244">A disk I/O failure occurred while reading from hello manifest.</span></span>|  
|`BlobListFormatInvalid`|<span data-ttu-id="7e406-245">blob de lista de BLOBs de exportação de Olá não está em conformidade com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-245">hello export blob list blob does not conform toohello required format.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="7e406-246">Aceder a blobs toohello na conta do storage Olá é proibido.</span><span class="sxs-lookup"><span data-stu-id="7e406-246">Access toohello blobs in hello storage account is forbidden.</span></span> <span data-ttu-id="7e406-247">Esta situação pode ser devido a chave de conta do storage tooinvalid ou contentor SAS.</span><span class="sxs-lookup"><span data-stu-id="7e406-247">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`InternalError`|<span data-ttu-id="7e406-248">E, Ocorreu um erro interno ao processar a unidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-248">And internal error occurred while processing hello drive.</span></span>|  
  
## <a name="blob-status-codes"></a><span data-ttu-id="7e406-249">Códigos de estado de blob</span><span class="sxs-lookup"><span data-stu-id="7e406-249">Blob status codes</span></span>  
<span data-ttu-id="7e406-250">Olá tabela seguinte lista os códigos de estado de Olá para o processamento de um blob.</span><span class="sxs-lookup"><span data-stu-id="7e406-250">hello following table lists hello status codes for processing a blob.</span></span>  
  
|<span data-ttu-id="7e406-251">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-251">Status code</span></span>|<span data-ttu-id="7e406-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-252">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7e406-253">blob Olá concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="7e406-253">hello blob has finished processing without errors.</span></span>|  
|`CompletedWithErrors`|<span data-ttu-id="7e406-254">blob Olá concluiu o processamento de erros em um ou mais intervalos de página ou blocos, os metadados ou propriedades.</span><span class="sxs-lookup"><span data-stu-id="7e406-254">hello blob has finished processing with errors in one or more page ranges or blocks, metadata, or properties.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7e406-255">nome de ficheiro Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="7e406-255">hello file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7e406-256">nome de ficheiro Olá é demasiado longo.</span><span class="sxs-lookup"><span data-stu-id="7e406-256">hello file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7e406-257">Olá ficheiro não encontrado.</span><span class="sxs-lookup"><span data-stu-id="7e406-257">hello file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7e406-258">Ficheiro de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="7e406-258">Access toohello file is denied.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7e406-259">Falha no pedido de serviço Blob Olá tooaccess Olá blob.</span><span class="sxs-lookup"><span data-stu-id="7e406-259">hello Blob service request tooaccess hello blob has failed.</span></span>|  
|`BlobRequestForbidden`|<span data-ttu-id="7e406-260">pedido de serviço Blob Olá tooaccess Olá blob é proibido.</span><span class="sxs-lookup"><span data-stu-id="7e406-260">hello Blob service request tooaccess hello blob is forbidden.</span></span> <span data-ttu-id="7e406-261">Esta situação pode ser devido a chave de conta do storage tooinvalid ou contentor SAS.</span><span class="sxs-lookup"><span data-stu-id="7e406-261">This might be due tooinvalid storage account key or container SAS.</span></span>|  
|`RenameFailed`|<span data-ttu-id="7e406-262">Falha ao blob do Olá toorename (para uma tarefa de importação) ou ficheiro Olá (para uma tarefa de exportação).</span><span class="sxs-lookup"><span data-stu-id="7e406-262">Failed toorename hello blob (for an import job) or hello file (for an export job).</span></span>|  
|`BlobUnexpectedChange`|<span data-ttu-id="7e406-263">Tiver ocorrido uma alteração inesperada com BLOBs Olá (para uma tarefa de exportação).</span><span class="sxs-lookup"><span data-stu-id="7e406-263">An unexpected change has occurred with hello blob (for an export job).</span></span>|  
|`LeasePresent`|<span data-ttu-id="7e406-264">Há uma concessão presente no blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-264">There is a lease present on hello blob.</span></span>|  
|`IOFailed`|<span data-ttu-id="7e406-265">Um disco ou a falha de e/s de rede ocorreu ao processar o blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-265">A disk or network I/O failure occurred while processing hello blob.</span></span>|  
|`Failed`|<span data-ttu-id="7e406-266">Ocorreu uma falha desconhecida ao processar o blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-266">An unknown failure occurred while processing hello blob.</span></span>|  
  
## <a name="import-disposition-status-codes"></a><span data-ttu-id="7e406-267">Códigos de estado de disposição de importação</span><span class="sxs-lookup"><span data-stu-id="7e406-267">Import disposition status codes</span></span>  
<span data-ttu-id="7e406-268">Olá tabela seguinte lista os códigos de estado de Olá para resolver uma disposição de importação.</span><span class="sxs-lookup"><span data-stu-id="7e406-268">hello following table lists hello status codes for resolving an import disposition.</span></span>  
  
|<span data-ttu-id="7e406-269">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-269">Status code</span></span>|<span data-ttu-id="7e406-270">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-270">Description</span></span>|  
|-----------------|-----------------|  
|`Created`|<span data-ttu-id="7e406-271">blob Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="7e406-271">hello blob has been created.</span></span>|  
|`Renamed`|<span data-ttu-id="7e406-272">blob Olá foi alterado por disposição de importação de mudança de nome.</span><span class="sxs-lookup"><span data-stu-id="7e406-272">hello blob has been renamed per rename import disposition.</span></span> <span data-ttu-id="7e406-273">Olá `Blob/BlobPath` elemento contém Olá URI de blob Olá mudado.</span><span class="sxs-lookup"><span data-stu-id="7e406-273">hello `Blob/BlobPath` element contains hello URI for hello renamed blob.</span></span>|  
|`Skipped`|<span data-ttu-id="7e406-274">blob Olá foi ignorado por `no-overwrite` importar disposição.</span><span class="sxs-lookup"><span data-stu-id="7e406-274">hello blob has been skipped per `no-overwrite` import disposition.</span></span>|  
|`Overwritten`|<span data-ttu-id="7e406-275">blob Olá substituíram um blob existente por `overwrite` importar disposição.</span><span class="sxs-lookup"><span data-stu-id="7e406-275">hello blob has overwritten an existing blob per `overwrite` import disposition.</span></span>|  
|`Cancelled`|<span data-ttu-id="7e406-276">Uma falha anterior foi parado o processamento disposição de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-276">A prior failure has stopped further processing of hello import disposition.</span></span>|  
  
## <a name="page-rangeblock-status-codes"></a><span data-ttu-id="7e406-277">Códigos de estado de intervalo/bloco de página</span><span class="sxs-lookup"><span data-stu-id="7e406-277">Page range/block status codes</span></span>  
<span data-ttu-id="7e406-278">Olá tabela seguinte lista os códigos de estado de Olá para o processamento de um intervalo de página ou um bloco.</span><span class="sxs-lookup"><span data-stu-id="7e406-278">hello following table lists hello status codes for processing a page range or a block.</span></span>  
  
|<span data-ttu-id="7e406-279">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-279">Status code</span></span>|<span data-ttu-id="7e406-280">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-280">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7e406-281">intervalo de páginas de Olá ou bloco concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="7e406-281">hello page range or block has finished processing without any errors.</span></span>|  
|`Committed`|<span data-ttu-id="7e406-282">Bloco de Olá tiver sido consolidado, mas não no Olá lista de bloqueios completa porque outros blocos tem falha ou coloque a lista de bloqueios completa próprio tem falhou.</span><span class="sxs-lookup"><span data-stu-id="7e406-282">hello block has been committed,  but not in hello full block list because other blocks have failed, or put full block list itself has failed.</span></span>|  
|`Uncommitted`|<span data-ttu-id="7e406-283">Bloco de Olá é carregado, mas não consolidado.</span><span class="sxs-lookup"><span data-stu-id="7e406-283">hello block is uploaded but not committed.</span></span>|  
|`Corrupted`|<span data-ttu-id="7e406-284">intervalo de páginas de Olá ou de bloqueios está danificado (conteúdo Olá não corresponde ao respetivo hash).</span><span class="sxs-lookup"><span data-stu-id="7e406-284">hello page range or block is corrupted (hello content does not match its hash).</span></span>|  
|`FileUnexpectedEnd`|<span data-ttu-id="7e406-285">Foi detetado um fim inesperado do ficheiro.</span><span class="sxs-lookup"><span data-stu-id="7e406-285">An unexpected end of file has been encountered.</span></span>|  
|`BlobUnexpectedEnd`|<span data-ttu-id="7e406-286">Foi detetado um fim inesperado do blob.</span><span class="sxs-lookup"><span data-stu-id="7e406-286">An unexpected end of blob has been encountered.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7e406-287">Falha ao bloco ou Olá pedido de serviço Blob tooaccess Olá intervalo de páginas.</span><span class="sxs-lookup"><span data-stu-id="7e406-287">hello Blob service request tooaccess hello page range or block has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7e406-288">Um disco ou a falha de e/s de rede ocorreu ao processar o intervalo de páginas de Olá ou de bloqueios.</span><span class="sxs-lookup"><span data-stu-id="7e406-288">A disk or network I/O failure occurred while processing hello page range or block.</span></span>|  
|`Failed`|<span data-ttu-id="7e406-289">Ocorreu uma falha desconhecida ao processar o intervalo de páginas de Olá ou de bloqueios.</span><span class="sxs-lookup"><span data-stu-id="7e406-289">An unknown failure occurred while processing hello page range or block.</span></span>|  
|`Cancelled`|<span data-ttu-id="7e406-290">Uma falha anterior foi parado o processamento adicional do intervalo de páginas de Olá ou de bloqueios.</span><span class="sxs-lookup"><span data-stu-id="7e406-290">A prior failure has stopped further processing of hello page range or block.</span></span>|  
  
## <a name="metadata-status-codes"></a><span data-ttu-id="7e406-291">Códigos de estado de metadados</span><span class="sxs-lookup"><span data-stu-id="7e406-291">Metadata status codes</span></span>  
<span data-ttu-id="7e406-292">Olá tabela seguinte lista os códigos de estado de Olá para metadados do blob de processamento.</span><span class="sxs-lookup"><span data-stu-id="7e406-292">hello following table lists hello status codes for processing blob metadata.</span></span>  
  
|<span data-ttu-id="7e406-293">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-293">Status code</span></span>|<span data-ttu-id="7e406-294">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-294">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7e406-295">metadados de Olá concluiu o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="7e406-295">hello metadata has finished processing without errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7e406-296">nome de ficheiro de metadados de Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="7e406-296">hello metadata file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7e406-297">nome de ficheiro de metadados de Olá é demasiado longo.</span><span class="sxs-lookup"><span data-stu-id="7e406-297">hello metadata file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7e406-298">ficheiro de metadados de Olá não foi encontrado.</span><span class="sxs-lookup"><span data-stu-id="7e406-298">hello metadata file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7e406-299">Ficheiro de metadados de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="7e406-299">Access toohello metadata file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="7e406-300">ficheiro de metadados de Olá está danificado (conteúdo Olá não corresponde ao respetivo hash).</span><span class="sxs-lookup"><span data-stu-id="7e406-300">hello metadata file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="7e406-301">conteúdo de metadados de Olá não está em conformidade com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-301">hello metadata content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="7e406-302">Escrever metadados Olá que XML falhou.</span><span class="sxs-lookup"><span data-stu-id="7e406-302">Writing hello metadata XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7e406-303">Falha no pedido de serviço Blob Olá tooaccess Olá metadados.</span><span class="sxs-lookup"><span data-stu-id="7e406-303">hello Blob service request tooaccess hello metadata has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7e406-304">Ocorreu uma falha de e/s de disco ou de rede durante o processamento de metadados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-304">A disk or network I/O failure occurred while processing hello metadata.</span></span>|  
|`Failed`|<span data-ttu-id="7e406-305">Ocorreu uma falha desconhecida ao processar Olá metadados.</span><span class="sxs-lookup"><span data-stu-id="7e406-305">An unknown failure occurred while processing hello metadata.</span></span>|  
|`Cancelled`|<span data-ttu-id="7e406-306">Uma falha anterior foi parado o processamento Olá metadados.</span><span class="sxs-lookup"><span data-stu-id="7e406-306">A prior failure has stopped further processing of hello metadata.</span></span>|  
  
## <a name="properties-status-codes"></a><span data-ttu-id="7e406-307">Códigos de estado de propriedades</span><span class="sxs-lookup"><span data-stu-id="7e406-307">Properties status codes</span></span>  
<span data-ttu-id="7e406-308">Olá tabela seguinte lista os códigos de estado de Olá para o processamento de propriedades de blob.</span><span class="sxs-lookup"><span data-stu-id="7e406-308">hello following table lists hello status codes for processing blob properties.</span></span>  
  
|<span data-ttu-id="7e406-309">Código de estado</span><span class="sxs-lookup"><span data-stu-id="7e406-309">Status code</span></span>|<span data-ttu-id="7e406-310">Descrição</span><span class="sxs-lookup"><span data-stu-id="7e406-310">Description</span></span>|  
|-----------------|-----------------|  
|`Completed`|<span data-ttu-id="7e406-311">Propriedades de Olá tem concluído o processamento sem erros.</span><span class="sxs-lookup"><span data-stu-id="7e406-311">hello properties have finished processing without any errors.</span></span>|  
|`FileNameInvalid`|<span data-ttu-id="7e406-312">nome de ficheiro de propriedades de Olá é inválido.</span><span class="sxs-lookup"><span data-stu-id="7e406-312">hello properties file name is invalid.</span></span>|  
|`FileNameTooLong`|<span data-ttu-id="7e406-313">nome de ficheiro de propriedades de Olá é demasiado longo.</span><span class="sxs-lookup"><span data-stu-id="7e406-313">hello properties file name is too long.</span></span>|  
|`FileNotFound`|<span data-ttu-id="7e406-314">ficheiro de propriedades de Olá não encontrado.</span><span class="sxs-lookup"><span data-stu-id="7e406-314">hello properties file is not found.</span></span>|  
|`FileAccessDenied`|<span data-ttu-id="7e406-315">Ficheiro de propriedades de toohello de acesso é negado.</span><span class="sxs-lookup"><span data-stu-id="7e406-315">Access toohello properties file is denied.</span></span>|  
|`Corrupted`|<span data-ttu-id="7e406-316">Olá propriedades ficheiro está corrompido (conteúdo Olá não corresponde ao respetivo hash).</span><span class="sxs-lookup"><span data-stu-id="7e406-316">hello properties file is corrupted (hello content does not match its hash).</span></span>|  
|`XmlReadFailed`|<span data-ttu-id="7e406-317">conteúdo de propriedades de Olá não está em conformidade com formato necessário toohello.</span><span class="sxs-lookup"><span data-stu-id="7e406-317">hello properties content does not conform toohello required format.</span></span>|  
|`XmlWriteFailed`|<span data-ttu-id="7e406-318">Escrever propriedades Olá que XML falhou.</span><span class="sxs-lookup"><span data-stu-id="7e406-318">Writing hello properties XML has failed.</span></span>|  
|`BlobRequestFailed`|<span data-ttu-id="7e406-319">Falha no pedido de serviço Blob Olá tooaccess Olá propriedades.</span><span class="sxs-lookup"><span data-stu-id="7e406-319">hello Blob service request tooaccess hello properties has failed.</span></span>|  
|`IOFailed`|<span data-ttu-id="7e406-320">Ocorreu uma falha de e/s de disco ou de rede durante o processamento de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-320">A disk or network I/O failure occurred while processing hello properties.</span></span>|  
|`Failed`|<span data-ttu-id="7e406-321">Ocorreu uma falha desconhecida ao processar propriedades Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-321">An unknown failure occurred while processing hello properties.</span></span>|  
|`Cancelled`|<span data-ttu-id="7e406-322">Uma falha anterior foi parado o processamento adicional de propriedades de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-322">A prior failure has stopped further processing of hello properties.</span></span>|  
  
## <a name="sample-logs"></a><span data-ttu-id="7e406-323">Registos de exemplo</span><span class="sxs-lookup"><span data-stu-id="7e406-323">Sample logs</span></span>  
<span data-ttu-id="7e406-324">Olá segue-se um exemplo de registo verboso.</span><span class="sxs-lookup"><span data-stu-id="7e406-324">hello following is an example of verbose log.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV123456</DriveId>  
    <Blob Status="Completed">  
       <BlobPath>pictures/bob/wild/desert.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\wild\desert.jpg</FilePath>  
       <Length>98304</Length>  
       <ImportDisposition Status="Created">overwrite</ImportDisposition>  
       <BlockList>  
          <Block Offset="0" Length="65536" Id="AAAAAA==" Hash=" 9C8AE14A55241F98533C4D80D85CDC68" Status="Completed"/>  
          <Block Offset="65536" Length="32768" Id="AQAAAA==" Hash=" DF54C531C9B3CA2570FDDDB3BCD0E27D" Status="Completed"/>  
       </BlockList>  
       <Metadata Status="Completed">  
          <GlobalPath Hash=" E34F54B7086BCF4EC1601D056F4C7E37">\Users\bob\Pictures\wild\metadata.xml</GlobalPath>  
       </Metadata>  
    </Blob>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="0" Length="65536" Hash="19701B8877418393CB3CB567F53EE225" Status="Completed"/>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
          <PageRange Offset="131072" Length="4096" Hash="9BA552E1C3EEAFFC91B42B979900A996" Status="Completed"/>  
       </PageRangeList>  
       <Properties Status="Completed">  
          <Path Hash="38D7AE80653F47F63C0222FEE90EC4E7">\Users\bob\Pictures\animals\koala.jpg.properties</Path>  
       </Properties>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```  
  
<span data-ttu-id="7e406-325">registo de erro correspondente Olá é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="7e406-325">hello corresponding error log is shown below.</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<DriveLog Version="2014-11-01">  
    <DriveId>WD-WMATV6965824</DriveId>  
    <Blob Status="CompletedWithErrors">  
       <BlobPath>pictures/bob/animals/koala.jpg</BlobPath>  
       <FilePath>\Users\bob\Pictures\animals\koala.jpg</FilePath>  
       <Length>163840</Length>  
       <ImportDisposition Status="Overwritten">overwrite</ImportDisposition>  
       <PageRangeList>  
          <PageRange Offset="65536" Length="65536" Hash="AA2585F6F6FD01C4AD4256E018240CD4" Status="Corrupted"/>  
       </PageRangeList>  
    </Blob>  
    <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

 <span data-ttu-id="7e406-326">registo de erros de siga Olá para uma tarefa de importação contém um erro sobre um ficheiro não encontrado na unidade de importação de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-326">hello follow error log for an import job contains an error about a file not found on hello import drive.</span></span> <span data-ttu-id="7e406-327">Tenha em atenção que o estado de Olá dos componentes subsequentes é `Cancelled`.</span><span class="sxs-lookup"><span data-stu-id="7e406-327">Note that hello status of subsequent components is `Cancelled`.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C2V</DriveId>  
  <Blob Status="FileNotFound">  
    <BlobPath>pictures/animals/koala.jpg</BlobPath>  
    <FilePath>\animals\koala.jpg</FilePath>  
    <Length>30310</Length>  
    <ImportDisposition Status="Cancelled">rename</ImportDisposition>  
    <BlockList>  
      <Block Offset="0" Length="6062" Id="MD5/cAzn4h7VVSWXf696qp5Uaw==" Hash="700CE7E21ED55525977FAF7AAA9E546B" Status="Cancelled" />  
      <Block Offset="6062" Length="6062" Id="MD5/PEnGwYOI8LPLNYdfKr7kAg==" Hash="3C49C6C18388F0B3CB35875F2ABEE402" Status="Cancelled" />  
      <Block Offset="12124" Length="6062" Id="MD5/FG4WxqfZKuUWZ2nGTU2qVA==" Hash="146E16C6A7D92AE5166769C64D4DAA54" Status="Cancelled" />  
      <Block Offset="18186" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
      <Block Offset="24248" Length="6062" Id="MD5/ZzibNDzr3IRBQENRyegeXQ==" Hash="67389B343CEBDC8441404351C9E81E5D" Status="Cancelled" />  
    </BlockList>  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```

<span data-ttu-id="7e406-328">Olá seguinte registo de erros para uma tarefa de exportação indica que conteúdo de blob Olá tem foi escrita com êxito na unidade de toohello, mas que ocorreu um erro ao exportar as propriedades de blob Olá.</span><span class="sxs-lookup"><span data-stu-id="7e406-328">hello following error log for an export job indicates that hello blob content has been successfully written toohello drive, but that an error occurred while exporting hello blob's properties.</span></span>  
  
```xml
<?xml version="1.0" encoding="utf-8"?>  
<DriveLog Version="2014-11-01">  
  <DriveId>9WM35C3U</DriveId>  
  <Blob Status="CompletedWithErrors">  
    <BlobPath>pictures/wild/canyon.jpg</BlobPath>  
    <FilePath>\pictures\wild\canyon.jpg</FilePath>  
    <LastModified>2012-09-18T23:47:08Z</LastModified>  
    <Length>163840</Length>  
    <BlockList />  
    <Properties Status="Failed" />  
  </Blob>  
  <Status>CompletedWithErrors</Status>  
</DriveLog>  
```
  
## <a name="next-steps"></a><span data-ttu-id="7e406-329">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e406-329">Next steps</span></span>
 
* [<span data-ttu-id="7e406-330">API de REST do Storage para importar/exportar</span><span class="sxs-lookup"><span data-stu-id="7e406-330">Storage Import/Export REST API</span></span>](/rest/api/storageimportexport/)
