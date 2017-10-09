---
title: "aaaCancel e eliminar uma tarefa de importação/exportação do Azure | Microsoft Docs"
description: "Saiba como toocancel e eliminar tarefas de Olá serviço de importação/exportação do Microsoft Azure."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: fd3d66f0-1dbb-4c75-9223-307d5abaeefc
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: 13456a8e7652850baacb53730cc7bb1520b0a4c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="canceling-and-deleting-azure-importexport-jobs"></a><span data-ttu-id="c1468-103">Cancelar e eliminar tarefas de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="c1468-103">Canceling and deleting Azure Import/Export jobs</span></span>

 <span data-ttu-id="c1468-104">toorequest que uma tarefa ser cancelada antes de está a ser Olá `Packaging` Estado, chamada Olá [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operação e conjunto Olá `CancelRequested` elemento demasiado`true`.</span><span class="sxs-lookup"><span data-stu-id="c1468-104">toorequest that a job be canceled before it is in hello `Packaging` state, call hello [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) operation and set hello `CancelRequested` element too`true`.</span></span> <span data-ttu-id="c1468-105">tarefa de Olá é cancelada numa base de melhor esforço.</span><span class="sxs-lookup"><span data-stu-id="c1468-105">hello job is canceled on a best-effort basis.</span></span> <span data-ttu-id="c1468-106">Se unidades estão no processo de Olá de transferência de dados, os dados podem continuar toobe transferido, mesmo depois foi solicitado o cancelamento.</span><span class="sxs-lookup"><span data-stu-id="c1468-106">If drives are in hello process of transferring data, data may continue toobe transferred even after cancellation has been requested.</span></span>

 <span data-ttu-id="c1468-107">Uma tarefa cancelada é movido toohello `Completed` estado e são mantidos durante 90 dias, altura em que é eliminado.</span><span class="sxs-lookup"><span data-stu-id="c1468-107">A canceled job is moved toohello `Completed` state and is kept for 90 days, at which point it is deleted.</span></span>

 <span data-ttu-id="c1468-108">toodelete uma tarefa, chamada Olá [tarefa eliminar](/rest/api/storageimportexport/jobs#Jobs_Delete) operação antes de tarefa Olá tem fornecidos (ou seja, enquanto a tarefa de Olá está em Olá `Creating` Estado).</span><span class="sxs-lookup"><span data-stu-id="c1468-108">toodelete a job, call hello [Delete Job](/rest/api/storageimportexport/jobs#Jobs_Delete) operation before hello job has shipped (that is, while hello job is in hello `Creating` state).</span></span> <span data-ttu-id="c1468-109">Também pode eliminar uma tarefa quando estiver a ser Olá `Completed` estado.</span><span class="sxs-lookup"><span data-stu-id="c1468-109">You can also delete a job when it is in hello `Completed` state.</span></span> <span data-ttu-id="c1468-110">Depois de eliminar uma tarefa, o estado e informações deixam de estar acessíveis através de Olá REST API ou Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="c1468-110">After a job is deleted, its information and status are no longer accessible via hello REST API or hello Azure portal.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c1468-111">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c1468-111">Next steps</span></span>

* [<span data-ttu-id="c1468-112">Utilizar a REST API do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="c1468-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
