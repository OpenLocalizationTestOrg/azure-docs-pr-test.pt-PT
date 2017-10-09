---
title: "referência de aaaQuick para comandos de tarefa de importação de ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Referência de comandos de ferramenta de importação/exportação do Azure para comandos de tarefa de importação utilizadas frequentemente."
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
ms.openlocfilehash: 35e46f24f764a5098ca465adb51badcab2d13e9d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a>Referência rápida para comandos utilizados com frequência para tarefas de importação

Este artigo fornece que uma referência rápida para algumas utilizadas frequentemente comandos. Para utilização detalhada, consulte [preparar os discos rígidos de uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import.md).

## <a name="first-session"></a>Primeira sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a>Segunda sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a>Abortar sessão mais recente

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a>Retomar a mais recente interrompida sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a>Adicione unidades toolatest sessão

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a>Passos seguintes

* [Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
