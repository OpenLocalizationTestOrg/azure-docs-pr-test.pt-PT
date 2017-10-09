---
title: "utilização da unidade aaaPreviewing de uma tarefa de exportação de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Saiba como lista de Olá toopreview de blobs que selecionou para uma tarefa de exportação no serviço de importação/exportação do Azure Olá."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 7707d744-7ec7-4de8-ac9b-93a18608dc9a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 7378c159f6d11702cda9ae7654e84d85f9b671b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="previewing-drive-usage-for-an-export-job"></a><span data-ttu-id="bd5fc-103">Pré-visualização da utilização da unidade para uma tarefa de exportação</span><span class="sxs-lookup"><span data-stu-id="bd5fc-103">Previewing drive usage for an export job</span></span>
<span data-ttu-id="bd5fc-104">Antes de criar uma tarefa de exportação, terá de toochoose um conjunto de blobs toobe exportado.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-104">Before you create an export job, you need toochoose a set of blobs toobe exported.</span></span> <span data-ttu-id="bd5fc-105">Olá serviço de importação/exportação do Microsoft Azure permite-lhe toouse uma lista de caminhos de blob ou blob prefixos blobs de Olá toorepresent que selecionou.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-105">hello Microsoft Azure Import/Export service allows you toouse a list of blob paths or blob prefixes toorepresent hello blobs you've selected.</span></span>  
  
<span data-ttu-id="bd5fc-106">Em seguida, terá de toodetermine unidades quantos terá toosend.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-106">Next, you need toodetermine how many drives you need toosend.</span></span> <span data-ttu-id="bd5fc-107">Olá ferramenta de importação/exportação fornece Olá `PreviewExport` comando toopreview utilização da unidade de blobs de Olá que selecionou, com base no tamanho Olá de unidades de Olá vai toouse.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-107">hello Import/Export Tool provides hello `PreviewExport` command toopreview drive usage for hello blobs you selected, based on hello size of hello drives you are going toouse.</span></span>

## <a name="command-line-parameters"></a><span data-ttu-id="bd5fc-108">Parâmetros da linha de comandos</span><span class="sxs-lookup"><span data-stu-id="bd5fc-108">Command-line parameters</span></span>

<span data-ttu-id="bd5fc-109">Pode utilizar Olá seguir os parâmetros ao utilizar Olá `PreviewExport` comando de Olá ferramenta de importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-109">You can use hello following parameters when using hello `PreviewExport` command of hello Import/Export Tool.</span></span>

|<span data-ttu-id="bd5fc-110">Parâmetro da linha de comandos</span><span class="sxs-lookup"><span data-stu-id="bd5fc-110">Command-line parameter</span></span>|<span data-ttu-id="bd5fc-111">Descrição</span><span class="sxs-lookup"><span data-stu-id="bd5fc-111">Description</span></span>|  
|--------------------------|-----------------|  
|<span data-ttu-id="bd5fc-112">**/LOGDIR:**< LogDirectory\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-112">**/logdir:**<LogDirectory\></span></span>|<span data-ttu-id="bd5fc-113">Opcional.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-113">Optional.</span></span> <span data-ttu-id="bd5fc-114">diretório de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-114">hello log directory.</span></span> <span data-ttu-id="bd5fc-115">Ficheiros de registo verboso serão escritos toothis diretório.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-115">Verbose log files will be written toothis directory.</span></span> <span data-ttu-id="bd5fc-116">Não se for especificado nenhum diretório de registo, diretório atual Olá será utilizado como o diretório de registo de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-116">If no log directory is specified, hello current directory will be used as hello log directory.</span></span>|  
|<span data-ttu-id="bd5fc-117">**/SN:**< StorageAccountName\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-117">**/sn:**<StorageAccountName\></span></span>|<span data-ttu-id="bd5fc-118">Necessário.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-118">Required.</span></span> <span data-ttu-id="bd5fc-119">nome de Olá Olá da conta de armazenamento para Olá exportar tarefa.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-119">hello name of hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="bd5fc-120">**/SK:**< StorageAccountKey\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-120">**/sk:**<StorageAccountKey\></span></span>|<span data-ttu-id="bd5fc-121">Necessário se e apenas se não for especificado um contentor SAS.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-121">Required if and only if a container SAS is not specified.</span></span> <span data-ttu-id="bd5fc-122">chave da conta para conta de armazenamento Olá Olá Olá exportar tarefa.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-122">hello account key for hello storage account for hello export job.</span></span>|  
|<span data-ttu-id="bd5fc-123">**/csas:**< ContainerSas\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-123">**/csas:**<ContainerSas\></span></span>|<span data-ttu-id="bd5fc-124">Necessário se e apenas se não for especificada uma chave de conta do storage.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-124">Required if and only if a storage account key is not specified.</span></span> <span data-ttu-id="bd5fc-125">o contentor de Olá SAS de listagem Olá blobs toobe exportados na tarefa de exportação de Olá.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-125">hello container SAS for listing hello blobs toobe exported in hello export job.</span></span>|  
|<span data-ttu-id="bd5fc-126">**/ ExportBlobListFile:**< ExportBlobListFile\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-126">**/ExportBlobListFile:**<ExportBlobListFile\></span></span>|<span data-ttu-id="bd5fc-127">Necessário.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-127">Required.</span></span> <span data-ttu-id="bd5fc-128">Caminho toohello XML do ficheiro que contém lista de caminhos de blob ou prefixos de caminho de Olá blobs toobe exportados do blob.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-128">Path toohello XML file containing list of blob paths or blob path prefixes for hello blobs toobe exported.</span></span> <span data-ttu-id="bd5fc-129">formato de ficheiro de Olá utilizado no Olá `BlobListBlobPath` elemento Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação de Olá REST API do serviço de importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-129">hello file format used in hello `BlobListBlobPath` element in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operation of hello Import/Export service REST API.</span></span>|  
|<span data-ttu-id="bd5fc-130">**/ DriveSize:**< DriveSize\></span><span class="sxs-lookup"><span data-stu-id="bd5fc-130">**/DriveSize:**<DriveSize\></span></span>|<span data-ttu-id="bd5fc-131">Necessário.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-131">Required.</span></span> <span data-ttu-id="bd5fc-132">Olá tamanho das unidades toouse para uma tarefa de exportação, *por exemplo,*, 500 GB, 1,5 TB.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-132">hello size of drives toouse for an export job, *e.g.*, 500GB, 1.5TB.</span></span>|  

## <a name="command-line-example"></a><span data-ttu-id="bd5fc-133">Exemplo de linha de comandos</span><span class="sxs-lookup"><span data-stu-id="bd5fc-133">Command-line example</span></span>

<span data-ttu-id="bd5fc-134">Olá exemplo seguinte demonstra Olá `PreviewExport` comando:</span><span class="sxs-lookup"><span data-stu-id="bd5fc-134">hello following example demonstrates hello `PreviewExport` command:</span></span>  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
<span data-ttu-id="bd5fc-135">Olá ficheiro de exportação de lista de blob pode conter nomes de blob e blob prefixos, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="bd5fc-135">hello export blob list file may contain blob names and blob prefixes, as shown here:</span></span>  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

<span data-ttu-id="bd5fc-136">Olá ferramenta de importação/exportação do Azure apresenta uma lista de todos os blobs toobe exportado e calcula como toopack-los para unidades de Olá especificado tamanho, tendo em conta quaisquer necessário overhead, em seguida, calcula o número de Olá de unidades necessário blobs de Olá toohold e utilização da unidade informações.</span><span class="sxs-lookup"><span data-stu-id="bd5fc-136">hello Azure Import/Export Tool lists all blobs toobe exported and calculates how toopack them into drives of hello specified size, taking into account any necessary overhead, then estimates hello number of drives needed toohold hello blobs and drive usage information.</span></span>  
  
<span data-ttu-id="bd5fc-137">Eis um exemplo de saída de Olá, com os registos informativas omitido:</span><span class="sxs-lookup"><span data-stu-id="bd5fc-137">Here is an example of hello output, with informational logs omitted:</span></span>  
  
```  
Number of unique blob paths/prefixes:   3  
Number of duplicate blob paths/prefixes:        0  
Number of nonexistent blob paths/prefixes:      1  
  
Drive size:     500.00 GB  
Number of blobs that can be exported:   6  
Number of blobs that cannot be exported:        2  
Number of drives needed:        3  
        Drive #1:       blobs = 1, occupied space = 454.74 GB  
        Drive #2:       blobs = 3, occupied space = 441.37 GB  
        Drive #3:       blobs = 2, occupied space = 131.28 GB    
```  
  
## <a name="next-steps"></a><span data-ttu-id="bd5fc-138">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bd5fc-138">Next steps</span></span>

* [<span data-ttu-id="bd5fc-139">Referência da ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="bd5fc-139">Azure Import/Export Tool reference</span></span>](../storage-import-export-tool-how-to-v1.md)
