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
# <a name="setting-properties-and-metadata-during-hello-import-process"></a>Processo de importar metadados durante Olá e propriedades da definição
Quando executar Olá ferramenta de importação/exportação do Microsoft Azure tooprepare suas unidades, pode especificar propriedades e toobe metadados definido em blobs de destino Olá. Siga estes passos.  
  
1.  Propriedades de blob tooset, crie um ficheiro de texto no seu computador local que especifica os nomes de propriedades e valores.  
  
2.  tooset metadados do blob, crie um ficheiro de texto no seu computador local que especifica os valores e nomes de metadados.  
  
3.  Passar Olá caminho completo tooone ou ambos estes toohello ficheiros ferramenta de importação/exportação do Azure como parte da Olá `PrepImport` operação.  
  
> [!NOTE]
>  Quando especificar um ficheiro de metadados ou propriedades como parte de uma sessão de cópia, essas propriedades ou metadados estão definidos para todos os BLOBs que são importados como parte da sessão cópia. Se pretender toospecify um conjunto diferente de propriedades ou metadados para alguns dos blobs Olá a ser importados, terá de toocreate sessão com as diferentes propriedades ou ficheiros de metadados de cópia de um separado.  
  
## <a name="specify-blob-properties-in-a-text-file"></a>Especificar as propriedades de Blob num ficheiro de texto  
Propriedades de blob toospecify, crie um ficheiro de texto local e incluem XML que especifica os nomes das propriedades como elementos e valores de propriedade como valores. Eis um exemplo que especifica alguns valores de propriedade:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Properties>  
    <Content-Type>application/octet-stream</Content-Type>  
    <Content-MD5>Q2hlY2sgSW50ZWdyaXR5IQ==</Content-MD5>  
    <Cache-Control>no-cache</Cache-Control>  
</Properties>  
```
  
Localização Olá ficheiro tooa local como `C:\WAImportExport\ImportProperties.txt`.  
  
## <a name="specify-blob-metadata-in-a-text-file"></a>Especifique os metadados do Blob num ficheiro de texto  
Da mesma forma, toospecify metadados do blob, crie um ficheiro de texto local que especifica os nomes dos metadados como elementos e valores de metadados como valores. Eis um exemplo que especifica alguns valores de metadados:  
  
```xml
<?xml version="1.0" encoding="UTF-8"?>  
<Metadata>  
    <UploadMethod>Windows Azure Import/Export service</UploadMethod>  
    <DataSetName>SampleData</DataSetName>  
    <CreationDate>10/1/2013</CreationDate>  
</Metadata>  
```
  
Localização Olá ficheiro tooa local como `C:\WAImportExport\ImportMetadata.txt`.  
  
## <a name="create-a-copy-session-including-hello-properties-or-metadata-files"></a>Criar um Olá cópia sessão incluindo propriedades ou ficheiros de metadados  
Quando executar a tarefa de importação do Olá ferramenta de importação/exportação do Azure tooprepare Olá, especifique o ficheiro de propriedades de Olá na linha de comandos Olá utilizando Olá `PropertyFile` parâmetro. Especifique o ficheiro de metadados de Olá na linha de comandos Olá utilizando Olá `/MetadataFile` parâmetro. Eis um exemplo que especifica ambos os ficheiros:  
  
```
WAImportExport.exe PrepImport /j:SecondDrive.jrn /id:BlueRayIso /srcfile:K:\Temp\BlueRay.ISO /dstblob:favorite/BlueRay.ISO /MetadataFile:c:\WAImportExport\SampleMetadata.txt /PropertyFile:c:\WAImportExport\SampleProperties.txt  
```
  
## <a name="next-steps"></a>Passos seguintes

* [Formato de ficheiro dos metadados e propriedades do serviço Importar/Exportar](storage-import-export-file-format-metadata-and-properties.md)
