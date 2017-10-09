---
title: "tarefa de importar aaaSample fluxo de trabalho tooprep unidades de disco rígido para um Azure para importar/exportar | Microsoft Docs"
description: "Consulte as instruções para o processo de conclusão de Olá da preparação unidades para uma tarefa de importação Olá serviço importar/exportar do Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/07/2017
ms.author: muralikk
ms.openlocfilehash: 560220b7dc9f87416f1fec1ff30fa5cd65812ce5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="sample-workflow-tooprepare-hard-drives-for-an-import-job"></a><span data-ttu-id="a7ee9-103">Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="a7ee9-103">Sample workflow tooprepare hard drives for an import job</span></span>

<span data-ttu-id="a7ee9-104">Este artigo orienta-o através do processo completo de Olá da preparação unidades para uma tarefa de importação.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-104">This article walks you through hello complete process of preparing drives for an import job.</span></span>

## <a name="sample-data"></a><span data-ttu-id="a7ee9-105">Dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="a7ee9-105">Sample data</span></span>

<span data-ttu-id="a7ee9-106">Neste exemplo importa os seguintes dados para uma conta do storage do Azure com o nome de Olá `mystorageaccount`:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-106">This example imports hello following data into an Azure storage account named `mystorageaccount`:</span></span>

|<span data-ttu-id="a7ee9-107">Localização</span><span class="sxs-lookup"><span data-stu-id="a7ee9-107">Location</span></span>|<span data-ttu-id="a7ee9-108">Descrição</span><span class="sxs-lookup"><span data-stu-id="a7ee9-108">Description</span></span>|<span data-ttu-id="a7ee9-109">Tamanho dos dados</span><span class="sxs-lookup"><span data-stu-id="a7ee9-109">Data size</span></span>|
|--------------|-----------------|-----|
|<span data-ttu-id="a7ee9-110">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-110">H:\Video\\</span></span> |<span data-ttu-id="a7ee9-111">Uma coleção de vídeos</span><span class="sxs-lookup"><span data-stu-id="a7ee9-111">A collection of videos</span></span>|<span data-ttu-id="a7ee9-112">12 TB</span><span class="sxs-lookup"><span data-stu-id="a7ee9-112">12 TB</span></span>|
|<span data-ttu-id="a7ee9-113">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-113">H:\Photo\\</span></span> |<span data-ttu-id="a7ee9-114">Uma coleção de fotografias</span><span class="sxs-lookup"><span data-stu-id="a7ee9-114">A collection of photos</span></span>|<span data-ttu-id="a7ee9-115">30 GB</span><span class="sxs-lookup"><span data-stu-id="a7ee9-115">30 GB</span></span>|
|<span data-ttu-id="a7ee9-116">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a7ee9-116">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a7ee9-117">Imagem de disco A Blu-ray™</span><span class="sxs-lookup"><span data-stu-id="a7ee9-117">A Blu-Ray™ disk image</span></span>|<span data-ttu-id="a7ee9-118">25 GB</span><span class="sxs-lookup"><span data-stu-id="a7ee9-118">25 GB</span></span>|
|<span data-ttu-id="a7ee9-119">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-119">\\\bigshare\john\music\\</span></span>|<span data-ttu-id="a7ee9-120">Uma coleção de ficheiros de música numa partilha de rede</span><span class="sxs-lookup"><span data-stu-id="a7ee9-120">A collection of music files on a network share</span></span>|<span data-ttu-id="a7ee9-121">10 GB</span><span class="sxs-lookup"><span data-stu-id="a7ee9-121">10 GB</span></span>|

## <a name="storage-account-destinations"></a><span data-ttu-id="a7ee9-122">Destinos de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="a7ee9-122">Storage account destinations</span></span>

<span data-ttu-id="a7ee9-123">tarefa de importação de Olá irá importar dados de Olá para Olá destinos na conta do storage Olá os seguintes:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-123">hello import job will import hello data into hello following destinations in hello storage account:</span></span>

|<span data-ttu-id="a7ee9-124">Origem</span><span class="sxs-lookup"><span data-stu-id="a7ee9-124">Source</span></span>|<span data-ttu-id="a7ee9-125">Diretório virtual de destino ou blob</span><span class="sxs-lookup"><span data-stu-id="a7ee9-125">Destination virtual directory or blob</span></span>|
|------------|-------------------------------------------|
|<span data-ttu-id="a7ee9-126">H:\Video\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-126">H:\Video\\</span></span> |<span data-ttu-id="a7ee9-127">vídeo /</span><span class="sxs-lookup"><span data-stu-id="a7ee9-127">video/</span></span>|
|<span data-ttu-id="a7ee9-128">H:\Photo\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-128">H:\Photo\\</span></span> |<span data-ttu-id="a7ee9-129">fotografia /</span><span class="sxs-lookup"><span data-stu-id="a7ee9-129">photo/</span></span>|
|<span data-ttu-id="a7ee9-130">K:\Temp\FavoriteMovie.ISO</span><span class="sxs-lookup"><span data-stu-id="a7ee9-130">K:\Temp\FavoriteMovie.ISO</span></span>|<span data-ttu-id="a7ee9-131">favorite/FavoriteMovies.ISO</span><span class="sxs-lookup"><span data-stu-id="a7ee9-131">favorite/FavoriteMovies.ISO</span></span>|
|<span data-ttu-id="a7ee9-132">\\\bigshare\john\music\\</span><span class="sxs-lookup"><span data-stu-id="a7ee9-132">\\\bigshare\john\music\\</span></span> |<span data-ttu-id="a7ee9-133">música</span><span class="sxs-lookup"><span data-stu-id="a7ee9-133">music</span></span>|

<span data-ttu-id="a7ee9-134">Com este mapeamento Olá ficheiro `H:\Video\Drama\GreatMovie.mov` serão importados toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-134">With this mapping, hello file `H:\Video\Drama\GreatMovie.mov` will be imported toohello blob `https://mystorageaccount.blob.core.windows.net/video/Drama/GreatMovie.mov`.</span></span>

## <a name="determine-hard-drive-requirements"></a><span data-ttu-id="a7ee9-135">Determinar os requisitos de disco rígido</span><span class="sxs-lookup"><span data-stu-id="a7ee9-135">Determine hard drive requirements</span></span>

<span data-ttu-id="a7ee9-136">Toodetermine seguinte, o número de unidades de disco rígido forem necessárias, computação Olá tamanho dos dados de Olá:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-136">Next, toodetermine how many hard drives are needed, compute hello size of hello data:</span></span>

`12TB + 30GB + 25GB + 10GB = 12TB + 65GB`

<span data-ttu-id="a7ee9-137">Neste exemplo, dois discos rígidos de 8TB devem ser suficientes.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-137">For this example, two 8TB hard drives should be sufficient.</span></span> <span data-ttu-id="a7ee9-138">No entanto, dado que o diretório de origem Olá `H:\Video` tem 12TB de dados e a capacidade do disco rígido único é apenas de 8TB, será capaz de toospecify isto em Olá seguintes forma no Olá **driveset.csv** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-138">However, since hello source directory `H:\Video` has 12TB of data and your single hard drive's capacity is only 8TB, you will be able toospecify this in hello following way in hello **driveset.csv** file:</span></span>

```
DriveLetter,FormatOption,SilentOrPromptOnFormat,Encryption,ExistingBitLockerKey
X,Format,SilentMode,Encrypt,
Y,Format,SilentMode,Encrypt,
```
<span data-ttu-id="a7ee9-139">ferramenta de Olá será distribuem dados em duas unidades de disco rígidas uma forma otimizada.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-139">hello tool will distribute data across two hard drives in an optimized way.</span></span>

## <a name="attach-drives-and-configure-hello-job"></a><span data-ttu-id="a7ee9-140">Anexar unidades e configurar a tarefa de Olá</span><span class="sxs-lookup"><span data-stu-id="a7ee9-140">Attach drives and configure hello job</span></span>
<span data-ttu-id="a7ee9-141">Irá ligar a máquina de toohello ambos os discos e crie volumes.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-141">You will attach both disks toohello machine and create volumes.</span></span> <span data-ttu-id="a7ee9-142">Em seguida, criar **dataset.csv** ficheiro:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-142">Then author **dataset.csv** file:</span></span>
```
BasePath,DstBlobPathOrPrefix,BlobType,Disposition,MetadataFile,PropertiesFile
H:\Video\,video/,BlockBlob,rename,None,H:\mydirectory\properties.xml
H:\Photo\,photo/,BlockBlob,rename,None,H:\mydirectory\properties.xml
K:\Temp\FavoriteVideo.ISO,favorite/FavoriteVideo.ISO,BlockBlob,rename,None,H:\mydirectory\properties.xml
\\myshare\john\music\,music/,BlockBlob,rename,None,H:\mydirectory\properties.xml
```

<span data-ttu-id="a7ee9-143">Além disso, pode definir Olá metadados para todos os ficheiros a seguir:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-143">In addition, you can set hello following metadata for all files:</span></span>

* <span data-ttu-id="a7ee9-144">**UploadMethod:** serviço de importação/exportação do Windows Azure</span><span class="sxs-lookup"><span data-stu-id="a7ee9-144">**UploadMethod:** Windows Azure Import/Export service</span></span>
* <span data-ttu-id="a7ee9-145">**DataSetName:** SampleData</span><span class="sxs-lookup"><span data-stu-id="a7ee9-145">**DataSetName:** SampleData</span></span>
* <span data-ttu-id="a7ee9-146">**CreationDate:** 1/10/2013</span><span class="sxs-lookup"><span data-stu-id="a7ee9-146">**CreationDate:** 10/1/2013</span></span>

<span data-ttu-id="a7ee9-147">tooset metadados para ficheiros de Olá importado, crie um ficheiro de texto, `c:\WAImportExport\SampleMetadata.txt`, com Olá seguinte conteúdo:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-147">tooset metadata for hello imported files, create a text file, `c:\WAImportExport\SampleMetadata.txt`, with hello following content:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Metadata>
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>
    <DataSetName>SampleData</DataSetName>
    <CreationDate>10/1/2013</CreationDate>
</Metadata>
```

<span data-ttu-id="a7ee9-148">Também pode definir algumas propriedades para Olá `FavoriteMovie.ISO` blob:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-148">You can also set some properties for hello `FavoriteMovie.ISO` blob:</span></span>

* <span data-ttu-id="a7ee9-149">**Tipo de conteúdo:** application/octet-stream.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-149">**Content-Type:** application/octet-stream</span></span>
* <span data-ttu-id="a7ee9-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ = =</span><span class="sxs-lookup"><span data-stu-id="a7ee9-150">**Content-MD5:** Q2hlY2sgSW50ZWdyaXR5IQ==</span></span>
* <span data-ttu-id="a7ee9-151">**Cache-Control:** não cache</span><span class="sxs-lookup"><span data-stu-id="a7ee9-151">**Cache-Control:** no-cache</span></span>

<span data-ttu-id="a7ee9-152">tooset estas propriedades, crie um ficheiro de texto, `c:\WAImportExport\SampleProperties.txt`:</span><span class="sxs-lookup"><span data-stu-id="a7ee9-152">tooset these properties, create a text file, `c:\WAImportExport\SampleProperties.txt`:</span></span>

```xml
<?xml version="1.0" encoding="UTF-8"?>
<Properties>
    <Content-Type>application/octet-stream</Content-Type>
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>
    <Cache-Control>no-cache</Cache-Control>
</Properties>
```

## <a name="run-hello-azure-importexport-tool-waimportexportexe"></a><span data-ttu-id="a7ee9-153">Execute Olá ferramenta de importação/exportação do Azure (WAImportExport.exe)</span><span class="sxs-lookup"><span data-stu-id="a7ee9-153">Run hello Azure Import/Export Tool (WAImportExport.exe)</span></span>

<span data-ttu-id="a7ee9-154">Agora, está pronto toorun Olá ferramenta de importação/exportação do Azure tooprepare Olá duas unidades de disco rígido.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-154">Now you are ready toorun hello Azure Import/Export Tool tooprepare hello two hard drives.</span></span>

<span data-ttu-id="a7ee9-155">**Para Olá primeira sessão:**</span><span class="sxs-lookup"><span data-stu-id="a7ee9-155">**For hello first session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1  /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

<span data-ttu-id="a7ee9-156">Se precisar de mais dados toobe adicionado, crie outro ficheiro de conjunto de dados (mesmo formato que Initialdataset).</span><span class="sxs-lookup"><span data-stu-id="a7ee9-156">If any more data needs toobe added, create another dataset file (same format as Initialdataset).</span></span>

<span data-ttu-id="a7ee9-157">**Para Olá segunda sessão:**</span><span class="sxs-lookup"><span data-stu-id="a7ee9-157">**For hello second session:**</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2  /DataSet:dataset-2.csv
```

<span data-ttu-id="a7ee9-158">Depois de concluíram as sessões de cópia de Olá, pode desligar duas unidades de Olá do computador de cópia de Olá e envie-los toohello adequado Datacenter do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-158">Once hello copy sessions have completed, you can disconnect hello two drives from hello copy computer and ship them toohello appropriate Azure data center.</span></span> <span data-ttu-id="a7ee9-159">Deverá carregar os ficheiros do diário de alterações de Olá dois, `<FirstDriveSerialNumber>.xml` e `<SecondDriveSerialNumber>.xml`, quando criar tarefa de importação de Olá no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="a7ee9-159">You'll upload hello two journal files, `<FirstDriveSerialNumber>.xml` and `<SecondDriveSerialNumber>.xml`, when you create hello import job in hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a7ee9-160">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a7ee9-160">Next steps</span></span>

* [<span data-ttu-id="a7ee9-161">Preparar as unidades de disco rígido para uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="a7ee9-161">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import.md)
* [<span data-ttu-id="a7ee9-162">Referência rápida para comandos utilizados com frequência</span><span class="sxs-lookup"><span data-stu-id="a7ee9-162">Quick reference for frequently used commands</span></span>](storage-import-export-tool-quick-reference.md)
