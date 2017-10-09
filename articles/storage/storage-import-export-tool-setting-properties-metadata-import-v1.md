---
title: aaaSetting propriedades e os metadados utilizando para importar/exportar do Azure - v1 | Microsoft Docs
description: "Saiba como toospecify toobe de propriedades e os metadados definidos no blobs de destino Olá quando em execução Olá ferramenta de importação/exportação do Azure tooprepare suas unidades. Isto refere-se toov1 de Olá ferramenta de importação/exportação."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: e8541695-bcfb-4bf0-84d9-72c9de32a0a8
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 66e55c2076fbcda9b78302f17b5ff2cf96bb24e7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="setting-properties-and-metadata-during-hello-import-process"></a><span data-ttu-id="0c79a-104">Processo de importar metadados durante Olá e propriedades da definição</span><span class="sxs-lookup"><span data-stu-id="0c79a-104">Setting properties and metadata during hello import process</span></span>
<span data-ttu-id="0c79a-105">Quando executar Olá ferramenta de importação/exportação do Microsoft Azure tooprepare suas unidades, pode especificar propriedades e toobe metadados definido em blobs de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="0c79a-105">When you run hello Microsoft Azure Import/Export Tool tooprepare your drives, you can specify properties and metadata toobe set on hello destination blobs.</span></span> <span data-ttu-id="0c79a-106">Siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="0c79a-106">Follow these steps:</span></span>  
  
1.  <span data-ttu-id="0c79a-107">Propriedades de blob tooset, crie um ficheiro de texto no seu computador local que especifica os nomes de propriedades e valores.</span><span class="sxs-lookup"><span data-stu-id="0c79a-107">tooset blob properties, create a text file on your local computer that specifies property names and values.</span></span>  
  
2.  <span data-ttu-id="0c79a-108">tooset metadados do blob, crie um ficheiro de texto no seu computador local que especifica os valores e nomes de metadados.</span><span class="sxs-lookup"><span data-stu-id="0c79a-108">tooset blob metadata, create a text file on your local computer that specifies metadata names and values.</span></span>  
  
3.  <span data-ttu-id="0c79a-109">Passar Olá caminho completo tooone ou ambos estes toohello ficheiros ferramenta de importação/exportação do Azure como parte da Olá `PrepImport` operação.</span><span class="sxs-lookup"><span data-stu-id="0c79a-109">Pass hello full path tooone or both of these files toohello Azure Import/Export Tool as part of hello `PrepImport` operation.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="0c79a-110">Quando especificar um ficheiro de metadados ou propriedades como parte de uma sessão de cópia, essas propriedades ou metadados estão definidos para todos os BLOBs que são importados como parte da sessão cópia.</span><span class="sxs-lookup"><span data-stu-id="0c79a-110">When you specify a properties or metadata file as part of a copy session, those properties or metadata are set for every blob that is imported as part of that copy session.</span></span> <span data-ttu-id="0c79a-111">Se pretender toospecify um conjunto diferente de propriedades ou metadados para alguns dos blobs Olá a ser importados, terá de toocreate sessão com as diferentes propriedades ou ficheiros de metadados de cópia de um separado.</span><span class="sxs-lookup"><span data-stu-id="0c79a-111">If you want toospecify a different set of properties or metadata for some of hello blobs being imported, you'll need toocreate a separate copy session with different properties or metadata files.</span></span>  
  
## <a name="specify-blob-properties-in-a-text-file"></a><span data-ttu-id="0c79a-112">Especificar as propriedades de Blob num ficheiro de texto</span><span class="sxs-lookup"><span data-stu-id="0c79a-112">Specify Blob Properties in a Text File</span></span>  
<span data-ttu-id="0c79a-113">Propriedades de blob toospecify, crie um ficheiro de texto local e incluem XML que especifica os nomes das propriedades como elementos e valores de propriedade como valores.</span><span class="sxs-lookup"><span data-stu-id="0c79a-113">toospecify blob properties, create a local text file, and include XML that specifies property names as elements, and property values as values.</span></span> <span data-ttu-id="0c79a-114">Eis um exemplo que especifica alguns valores de propriedade:</span><span class="sxs-lookup"><span data-stu-id="0c79a-114">Here's an example that specifies some property values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
<span data-ttu-id="0c79a-115">Localização Olá ficheiro tooa local como `C:\WAImportExport\ImportProperties.txt`.</span><span class="sxs-lookup"><span data-stu-id="0c79a-115">Save hello file tooa local location like `C:\WAImportExport\ImportProperties.txt`.</span></span>  
  
## <a name="specify-blob-metadata-in-a-text-file"></a><span data-ttu-id="0c79a-116">Especifique os metadados do Blob num ficheiro de texto</span><span class="sxs-lookup"><span data-stu-id="0c79a-116">Specify Blob Metadata in a Text File</span></span>  
<span data-ttu-id="0c79a-117">Da mesma forma, toospecify metadados do blob, crie um ficheiro de texto local que especifica os nomes dos metadados como elementos e valores de metadados como valores.</span><span class="sxs-lookup"><span data-stu-id="0c79a-117">Similarly, toospecify blob metadata, create a local text file that specifies metadata names as elements, and metadata values as values.</span></span> <span data-ttu-id="0c79a-118">Eis um exemplo que especifica alguns valores de metadados:</span><span class="sxs-lookup"><span data-stu-id="0c79a-118">Here's an example that specifies some metadata values:</span></span>  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
<span data-ttu-id="0c79a-119">Localização Olá ficheiro tooa local como `C:\WAImportExport\ImportMetadata.txt`.</span><span class="sxs-lookup"><span data-stu-id="0c79a-119">Save hello file tooa local location like `C:\WAImportExport\ImportMetadata.txt`.</span></span>  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a><span data-ttu-id="0c79a-120">Criar um Olá cópia sessão incluindo propriedades ou ficheiros de metadados</span><span class="sxs-lookup"><span data-stu-id="0c79a-120">Create a Copy Session Including hello Properties or Metadata Files</span></span>  
<span data-ttu-id="0c79a-121">Quando executar a tarefa de importação do Olá ferramenta de importação/exportação do Azure tooprepare Olá, especifique o ficheiro de propriedades de Olá na linha de comandos Olá utilizando Olá `PropertyFile` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0c79a-121">When you run hello Azure Import/Export Tool tooprepare hello import job, specify hello properties file on hello command line using hello `PropertyFile` parameter.</span></span> <span data-ttu-id="0c79a-122">Especifique o ficheiro de metadados de Olá na linha de comandos Olá utilizando Olá `/MetadataFile` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="0c79a-122">Specify hello metadata file on hello command line using hello `/MetadataFile` parameter.</span></span> <span data-ttu-id="0c79a-123">Eis um exemplo que especifica ambos os ficheiros:</span><span class="sxs-lookup"><span data-stu-id="0c79a-123">Here's an example that specifies both files:</span></span>  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a><span data-ttu-id="0c79a-124">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0c79a-124">Next steps</span></span>

* [<span data-ttu-id="0c79a-125">Formato de ficheiro dos metadados e propriedades do serviço Importar/Exportar</span><span class="sxs-lookup"><span data-stu-id="0c79a-125">Import/Export service metadata and properties file format</span></span>](storage-import-export-file-format-metadata-and-properties.md)
