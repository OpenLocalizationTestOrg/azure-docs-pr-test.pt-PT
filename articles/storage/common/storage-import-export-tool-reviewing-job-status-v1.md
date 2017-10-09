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
# <a name="reviewing-azure-importexport-job-status-with-copy-log-files"></a><span data-ttu-id="ed297-103">Rever o estado da tarefa de importação/exportação do Azure com os ficheiros de registo de cópia</span><span class="sxs-lookup"><span data-stu-id="ed297-103">Reviewing Azure Import/Export job status with copy log files</span></span>
<span data-ttu-id="ed297-104">Quando Olá serviço de importação/exportação do Microsoft Azure processa unidades associadas uma tarefa de importação ou exportação, escreve cópia registo ficheiros toohello armazenamento conta tooor partir do qual está a importar ou exportar blobs.</span><span class="sxs-lookup"><span data-stu-id="ed297-104">When hello Microsoft Azure Import/Export service processes drives associated with an import or export job, it writes copy log files toohello storage account tooor from which you are importing or exporting blobs.</span></span> <span data-ttu-id="ed297-105">ficheiro de registo Olá contém estado detalhadas sobre cada ficheiro que foi importado ou exportado.</span><span class="sxs-lookup"><span data-stu-id="ed297-105">hello log file contains detailed status about each file that was imported or exported.</span></span> <span data-ttu-id="ed297-106">ficheiro de registo de cópia de tooeach URL Olá é devolvido quando consultar o estado de Olá de uma tarefa concluída; consulte [Get Job](/rest/api/storageservices/Get-Job3) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ed297-106">hello URL tooeach copy log file is returned when you query hello status of a completed job; see [Get Job](/rest/api/storageservices/Get-Job3) for more information.</span></span>  

## <a name="example-urls"></a><span data-ttu-id="ed297-107">URLs de exemplo</span><span class="sxs-lookup"><span data-stu-id="ed297-107">Example URLs</span></span>

<span data-ttu-id="ed297-108">Olá, são URLs de exemplo para ficheiros de registo de cópia de uma tarefa de importação com duas unidades:</span><span class="sxs-lookup"><span data-stu-id="ed297-108">hello following are example URLs for copy log files for an import job with two drives:</span></span>  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM35C2V_20130921-034307-902_error.xml`  
  
 `http://myaccount.blob.core.windows.net/ImportExportStatesPath/waies/myjob_9WM45A6Q_20130921-042122-021_error.xml`  
  
 <span data-ttu-id="ed297-109">Consulte [serviço importar/exportar formato de ficheiro de registo](../storage-import-export-file-format-log.md) formato Olá dos registos de cópia e a lista completa de Olá de códigos de estado.</span><span class="sxs-lookup"><span data-stu-id="ed297-109">See [Import/Export service Log File Format](../storage-import-export-file-format-log.md) for hello format of copy logs and hello full list of status codes.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="ed297-110">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ed297-110">Next steps</span></span>
 
 * [<span data-ttu-id="ed297-111">Configurar a definição Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="ed297-111">Setting Up hello Azure Import/Export Tool</span></span>](storage-import-export-tool-setup-v1.md)   
 * [<span data-ttu-id="ed297-112">Preparar as unidades de disco rígido para uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="ed297-112">Preparing hard drives for an import job</span></span>](../storage-import-export-tool-preparing-hard-drives-import-v1.md)   
 * [<span data-ttu-id="ed297-113">Reparação de uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="ed297-113">Repairing an import job</span></span>](../storage-import-export-tool-repairing-an-import-job-v1.md)   
 * [<span data-ttu-id="ed297-114">Reparação de uma tarefa de exportação</span><span class="sxs-lookup"><span data-stu-id="ed297-114">Repairing an export job</span></span>](../storage-import-export-tool-repairing-an-export-job-v1.md)   
 * [<span data-ttu-id="ed297-115">Resolução de problemas Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="ed297-115">Troubleshooting hello Azure Import/Export Tool</span></span>](storage-import-export-tool-troubleshooting-v1.md)
