---
title: aaaReviewing estado da tarefa importar/exportar do Azure - v1 | Microsoft Docs
description: "Saiba como ficheiros de registo toouse Olá criados quando Olá importar ou exportar tarefa foi executada estado de Olá toosee da tarefa de importação/exportação Olá."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: c69d1d69-6403-4eee-9949-0185faeecfa1
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/26/2017
ms.author: muralikk
ms.openlocfilehash: 363731ede4751124a714b4ce96852e0b8c4dbca4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a>Rever o estado da tarefa de importação/exportação do Azure com os ficheiros de registo de cópia
Quando Olá serviço de importação/exportação do Microsoft Azure processa unidades associadas uma tarefa de importação ou exportação, escreve cópia registo ficheiros toohello armazenamento conta tooor partir do qual está a importar ou exportar blobs. ficheiro de registo Olá contém estado detalhadas sobre cada ficheiro que foi importado ou exportado. ficheiro de registo de cópia de tooeach URL Olá é devolvido quando consultar o estado de Olá de uma tarefa concluída; consulte [Get Job](/rest/api/storageservices/Get-Job3) para obter mais informações.  

## <a name="example-urls"></a>URLs de exemplo

Olá, são URLs de exemplo para ficheiros de registo de cópia de uma tarefa de importação com duas unidades:  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 Consulte [serviço importar/exportar formato de ficheiro de registo](../storage-import-export-file-format-log.md) formato Olá dos registos de cópia e a lista completa de Olá de códigos de estado.  
  
## <a name="next-steps"></a>Passos seguintes
 
 * [Configurar a definição Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-setup-v1.md)   
 * [Preparar as unidades de disco rígido para uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [Reparação de uma tarefa de importação](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [Reparação de uma tarefa de exportação](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [Resolução de problemas Olá ferramenta de importação/exportação do Azure](storage-import-export-tool-troubleshooting-v1.md)
