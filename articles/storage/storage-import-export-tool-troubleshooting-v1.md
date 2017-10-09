---
title: "Olá aaaTroubleshooting ferramenta de importação/exportação do Azure | Microsoft Docs"
description: "Saiba mais sobre alguns dos problemas comuns de Olá vistos quando utilizar Olá ferramenta de importação/exportação do Azure e como a toohandle-los."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: b91ca5eb-c557-460a-9afc-0590b38471f9
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: 5445cefe2703edf4d9d285f761433b7b66d8cb6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hello-azure-importexport-tool"></a><span data-ttu-id="bc019-103">Resolução de problemas Olá ferramenta de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="bc019-103">Troubleshooting hello Azure Import/Export Tool</span></span>
<span data-ttu-id="bc019-104">Olá ferramenta de importação/exportação do Microsoft Azure devolve mensagens de erro se ficar para problemas.</span><span class="sxs-lookup"><span data-stu-id="bc019-104">hello Microsoft Azure Import/Export Tool returns error messages if it runs into issues.</span></span> <span data-ttu-id="bc019-105">Este tópico apresenta alguns problemas comuns que os utilizadores podem executar no.</span><span class="sxs-lookup"><span data-stu-id="bc019-105">This topic lists some common issues that users may run into.</span></span>  
  
## <a name="a-copy-session-fails-what-i-should-do"></a><span data-ttu-id="bc019-106">Uma sessão de cópia falha, o que devo fazer?</span><span class="sxs-lookup"><span data-stu-id="bc019-106">A copy session fails, what I should do?</span></span>  
 <span data-ttu-id="bc019-107">Quando uma sessão de cópia falha, existem duas opções:</span><span class="sxs-lookup"><span data-stu-id="bc019-107">When a copy session fails, there are two options:</span></span>  
  
 <span data-ttu-id="bc019-108">Se o erro de Olá for repetição, por exemplo, se a partilha de rede Olá estava offline para um curto período e agora está novamente online, pode retomar a sessão de cópia de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc019-108">If hello error is retryable, for example if hello network share was offline for a short period and now is back online, you can resume hello copy session.</span></span> <span data-ttu-id="bc019-109">Se o erro de Olá não for repetição, por exemplo, se especificou o diretório do ficheiro de origem errado Olá nos parâmetros de linha de comandos Olá, terá de sessão de cópia de Olá tooabort.</span><span class="sxs-lookup"><span data-stu-id="bc019-109">If hello error is not retryable, for example if you specified hello wrong source file directory in hello command line parameters, you need tooabort hello copy session.</span></span> <span data-ttu-id="bc019-110">Consulte [preparar os discos rígidos de uma tarefa de importação](storage-import-export-tool-preparing-hard-drives-import-v1.md) para obter mais informações sobre a retomar e abortar sessões de cópia.</span><span class="sxs-lookup"><span data-stu-id="bc019-110">See [Preparing Hard Drives for an Import Job](storage-import-export-tool-preparing-hard-drives-import-v1.md) for more information about resuming and aborting copy sessions.</span></span>  
  
## <a name="i-cant-resume-or-abort-a-copy-session"></a><span data-ttu-id="bc019-111">Não consigo retomar ou abortar uma sessão de cópia.</span><span class="sxs-lookup"><span data-stu-id="bc019-111">I can't resume or abort a copy session.</span></span>  
 <span data-ttu-id="bc019-112">Se sessão de cópia de Olá está Olá primeira sessão de cópia para uma unidade, em seguida, mensagem de erro de saudação deve Estado: "Olá primeira sessão de cópia não pode ser retomado ou abortada."</span><span class="sxs-lookup"><span data-stu-id="bc019-112">If hello copy session is hello first copy session for a drive, then hello error message should state: "hello first copy session cannot be resumed or aborted."</span></span> <span data-ttu-id="bc019-113">Neste caso, pode eliminar o ficheiro de diário antigo Olá e volte a executar o comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="bc019-113">In this case, you can delete hello old journal file and rerun hello command.</span></span>  
  
 <span data-ttu-id="bc019-114">Se uma sessão de cópia não é hello primeiro uma para uma unidade, pode ser retomado sempre ou abortada.</span><span class="sxs-lookup"><span data-stu-id="bc019-114">If a copy session is not hello first one for a drive, it can always be resumed or aborted.</span></span>  
  
## <a name="i-lost-hello-journal-file-can-i-still-create-hello-job"></a><span data-ttu-id="bc019-115">Perdeu a ficheiros do diário de alterações de Olá, pode ainda criar tarefa de Olá?</span><span class="sxs-lookup"><span data-stu-id="bc019-115">I lost hello journal file, can I still create hello job?</span></span>  
 <span data-ttu-id="bc019-116">ficheiros do diário de alterações de Olá para uma unidade contém Olá informações de copiar a unidade de toothis de dados e é necessário tooadd mais unidade de toohello de ficheiros e será utilizado toocreate uma tarefa de importação.</span><span class="sxs-lookup"><span data-stu-id="bc019-116">hello journal file for a drive contains hello complete information of copying data toothis drive, and it is needed tooadd more files toohello drive and will be used toocreate an import job.</span></span> <span data-ttu-id="bc019-117">Se o ficheiro do diário de alterações de Olá se tenha perdido, terá de tooredo todas as sessões de cópia de Olá para unidade Olá.</span><span class="sxs-lookup"><span data-stu-id="bc019-117">If hello journal file is lost, you will have tooredo all hello copy sessions for hello drive.</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="bc019-118">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="bc019-118">Next steps</span></span>
 
* [<span data-ttu-id="bc019-119">Configurar a ferramenta de importação/exportação do azure Olá</span><span class="sxs-lookup"><span data-stu-id="bc019-119">Setting up hello azure import/export tool</span></span>](storage-import-export-tool-setup-v1.md)   
* [<span data-ttu-id="bc019-120">Preparar as unidades de disco rígido para uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="bc019-120">Preparing hard drives for an import job</span></span>](storage-import-export-tool-preparing-hard-drives-import-v1.md)   
* [<span data-ttu-id="bc019-121">Revisão do estado da tarefa com ficheiros de registo de cópia</span><span class="sxs-lookup"><span data-stu-id="bc019-121">Reviewing job status with copy log files</span></span>](storage-import-export-tool-reviewing-job-status-v1.md)   
* [<span data-ttu-id="bc019-122">Reparação de uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="bc019-122">Repairing an import job</span></span>](storage-import-export-tool-repairing-an-import-job-v1.md)   
* [<span data-ttu-id="bc019-123">Reparação de uma tarefa de exportação</span><span class="sxs-lookup"><span data-stu-id="bc019-123">Repairing an export job</span></span>](storage-import-export-tool-repairing-an-export-job-v1.md)
