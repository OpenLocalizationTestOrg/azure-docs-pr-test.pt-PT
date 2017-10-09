---
title: "referência de aaaQuick para comandos de tarefa de importação de ferramenta de importação/exportação do Azure - v1 | Microsoft Docs"
description: "Referência de comandos de ferramenta de importação/exportação do Azure para comandos de tarefa de importação utilizadas frequentemente. Isto refere-se toov1 de Olá ferramenta de importação/exportação."
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
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: e36f065e5d23268758cf6b6db9428fe8a8e1056d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Referência rápida para comandos utilizados com frequência para tarefas de importação
Esta secção fornece que uma rápida referências para algumas utilizadas frequentemente comandos. Para utilização detalhada, consulte [preparar os discos rígidos de uma tarefa de importação](storage-import-export-tool-preparing-hard-drives-import-v1.md).  

## <a name="prepare-hello-disks-when-data-already-copied-toohello-disks"></a>Preparar os discos de Olá quando os dados copiados já toohello discos
 Eis um tooprepare de comando de exemplo um discos quando dados sido ainda copiado o disco de rígido toohello que ainda não foi ainda foi encriptada com BitLocker:  
  
```  
  WAImportExport.exe PrepImport /j:9WM35C2V.jrn /id:session#1 /sk:VkGbrUqBWLYJ6zg1m29VOTrxpBgdNOlp+kp0C9MEdx3GELxmBw4hK94f7KysbbeKLDksg7VoN1W/a5UuM2zNgQ== /t:d /encrypt /srcdir:d:\movies\drama /dstdir:movies/drama/ /skipwrite
```    

## <a name="copy-a-single-directory-tooa-hard-drive"></a>Copiar uma unidade de disco rígido de tooa de diretório única  
 Eis um toocopy de comando de exemplo da origem de um único diretório tooa unidade de disco rígido que ainda não foi ainda foi encriptada com BitLocker:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
## <a name="copy-wwo-directories-tooa-hard-drive"></a>Copiar a unidade de disco rígido wwo diretórios tooa  
 toocopy dois origem diretórios tooa unidade, terá dois comandos.  
  
 Olá primeiro comando Especifica o diretório de registo de Olá, a chave de conta de armazenamento, a letra de unidade de destino e `format/encrypt` requisitos, nos parâmetros comuns de toohello de adição:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:movies /logdir:c:\logs /sk:8ImTigJhIwvL9VEIQKB/zbqcXbxrIHbBjLIfOt0tyR98TxtFvUM/7T0KVNR6KRkJrh26u5I8hTxTLM2O1aDVqg== /t:x /format /encrypt /srcdir:d:\Movies /dstdir:entertainment/movies/  
```  
  
 segundo comando de Olá Especifica o ficheiro do diário de alterações de Olá, um novo ID de sessão e localizações de origem e destino Olá:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:music /srcdir:d:\Music /dstdir:entertainment/music/  
```  
  
## <a name="copy-a-large-file-tooa-hard-drive-in-a-second-copy-session"></a>Copiar uma unidade de disco rígido tooa ficheiros grandes uma segunda sessão de cópia  
 Eis um comando de exemplo que copia uma unidade de tooa único ficheiro de grandes dimensões que tenha sido preparada numa sessão de cópia anterior:  
  
```  
WAImportExport.exe PrepImport /j:FirstDrive.jrn /id:dvd /srcfile:d:\dvd\favoritemovie.vhd /dstblob:dvd/favoritemovie.vhd  
```  
  
## <a name="next-steps"></a>Passos seguintes

* [Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow-v1.md)
