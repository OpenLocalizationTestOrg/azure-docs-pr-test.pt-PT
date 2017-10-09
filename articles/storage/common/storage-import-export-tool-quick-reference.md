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
# <a name="quick-reference-for-frequently-used-commands-for-import-jobs"></a><span data-ttu-id="5428e-103">Referência rápida para comandos utilizados com frequência para tarefas de importação</span><span class="sxs-lookup"><span data-stu-id="5428e-103">Quick reference for frequently used commands for import jobs</span></span>

<span data-ttu-id="5428e-104">Este artigo fornece que uma referência rápida para algumas utilizadas frequentemente comandos.</span><span class="sxs-lookup"><span data-stu-id="5428e-104">This article provides a quick reference for some frequently used commands.</span></span> <span data-ttu-id="5428e-105">Para utilização detalhada, consulte [preparar os discos rígidos de uma tarefa de importação](../storage-import-export-tool-preparing-hard-drives-import.md).</span><span class="sxs-lookup"><span data-stu-id="5428e-105">For detailed usage, see [Preparing Hard Drives for an Import Job](../storage-import-export-tool-preparing-hard-drives-import.md).</span></span>

## <a name="first-session"></a><span data-ttu-id="5428e-106">Primeira sessão</span><span class="sxs-lookup"><span data-stu-id="5428e-106">First session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#1 /sk:************* /InitialDriveSet:driveset-1.csv /DataSet:dataset-1.csv /logdir:F:\logs
```

## <a name="second-session"></a><span data-ttu-id="5428e-107">Segunda sessão</span><span class="sxs-lookup"><span data-stu-id="5428e-107">Second session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /DataSet:dataset-2.csv
```

## <a name="abort-latest-session"></a><span data-ttu-id="5428e-108">Abortar sessão mais recente</span><span class="sxs-lookup"><span data-stu-id="5428e-108">Abort latest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#2 /AbortSession
```

## <a name="resume-latest-interrupted-session"></a><span data-ttu-id="5428e-109">Retomar a mais recente interrompida sessão</span><span class="sxs-lookup"><span data-stu-id="5428e-109">Resume latest interrupted session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /ResumeSession
```

## <a name="add-drives-toolatest-session"></a><span data-ttu-id="5428e-110">Adicione unidades toolatest sessão</span><span class="sxs-lookup"><span data-stu-id="5428e-110">Add drives toolatest session</span></span>

```
WAImportExport.exe PrepImport /j:JournalTest.jrn /id:session#3 /AdditionalDriveSet:driveset-2.csv
```

## <a name="next-steps"></a><span data-ttu-id="5428e-111">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5428e-111">Next steps</span></span>

* [<span data-ttu-id="5428e-112">Discos rígidos do tooprepare de fluxo de trabalho de exemplo para uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="5428e-112">Sample workflow tooprepare hard drives for an import job</span></span>](storage-import-export-tool-sample-preparing-hard-drives-import-job-workflow.md)
