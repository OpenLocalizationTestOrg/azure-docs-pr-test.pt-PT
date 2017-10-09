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
# <a name="previewing-drive-usage-for-an-export-job"></a>Pré-visualização da utilização da unidade para uma tarefa de exportação
Antes de criar uma tarefa de exportação, terá de toochoose um conjunto de blobs toobe exportado. Olá serviço de importação/exportação do Microsoft Azure permite-lhe toouse uma lista de caminhos de blob ou blob prefixos blobs de Olá toorepresent que selecionou.  
  
Em seguida, terá de toodetermine unidades quantos terá toosend. Olá ferramenta de importação/exportação fornece Olá `PreviewExport` comando toopreview utilização da unidade de blobs de Olá que selecionou, com base no tamanho Olá de unidades de Olá vai toouse.

## <a name="command-line-parameters"></a>Parâmetros da linha de comandos

Pode utilizar Olá seguir os parâmetros ao utilizar Olá `PreviewExport` comando de Olá ferramenta de importação/exportação.

|Parâmetro da linha de comandos|Descrição|  
|--------------------------|-----------------|  
|**/LOGDIR:**< LogDirectory\>|Opcional. diretório de registo de Olá. Ficheiros de registo verboso serão escritos toothis diretório. Não se for especificado nenhum diretório de registo, diretório atual Olá será utilizado como o diretório de registo de Olá.|  
|**/SN:**< StorageAccountName\>|Necessário. nome de Olá Olá da conta de armazenamento para Olá exportar tarefa.|  
|**/SK:**< StorageAccountKey\>|Necessário se e apenas se não for especificado um contentor SAS. chave da conta para conta de armazenamento Olá Olá Olá exportar tarefa.|  
|**/csas:**< ContainerSas\>|Necessário se e apenas se não for especificada uma chave de conta do storage. o contentor de Olá SAS de listagem Olá blobs toobe exportados na tarefa de exportação de Olá.|  
|**/ ExportBlobListFile:**< ExportBlobListFile\>|Necessário. Caminho toohello XML do ficheiro que contém lista de caminhos de blob ou prefixos de caminho de Olá blobs toobe exportados do blob. formato de ficheiro de Olá utilizado no Olá `BlobListBlobPath` elemento Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) operação de Olá REST API do serviço de importação/exportação.|  
|**/ DriveSize:**< DriveSize\>|Necessário. Olá tamanho das unidades toouse para uma tarefa de exportação, *por exemplo,*, 500 GB, 1,5 TB.|  

## <a name="command-line-example"></a>Exemplo de linha de comandos

Olá exemplo seguinte demonstra Olá `PreviewExport` comando:  
  
```  
WAImportExport.exe PreviewExport /sn:bobmediaaccount /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /ExportBlobListFile:C:\WAImportExport\mybloblist.xml /DriveSize:500GB    
```  
  
Olá ficheiro de exportação de lista de blob pode conter nomes de blob e blob prefixos, conforme mostrado aqui:  
  
```xml 
<?xml version="1.0" encoding="utf-8"?>  
<BlobList>  
<BlobPath>pictures/animals/koala.jpg</BlobPath>  
<BlobPathPrefix>/vhds/</BlobPathPrefix>  
<BlobPathPrefix>/movies/</BlobPathPrefix>  
</BlobList>  
```

Olá ferramenta de importação/exportação do Azure apresenta uma lista de todos os blobs toobe exportado e calcula como toopack-los para unidades de Olá especificado tamanho, tendo em conta quaisquer necessário overhead, em seguida, calcula o número de Olá de unidades necessário blobs de Olá toohold e utilização da unidade informações.  
  
Eis um exemplo de saída de Olá, com os registos informativas omitido:  
  
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
  
## <a name="next-steps"></a>Passos seguintes

* [Referência da ferramenta de importação/exportação do Azure](../storage-import-export-tool-how-to-v1.md)
