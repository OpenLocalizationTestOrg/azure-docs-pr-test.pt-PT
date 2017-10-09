---
title: "Olá aaaUsing REST API do serviço de importação/exportação do Azure | Microsoft Docs"
description: "Saiba onde toofind recursos para a utilização de Olá do Azure para importar/exportar serviço API REST, incluindo o material de referência como tooand."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 233f80e9-2e7f-48e0-9639-5c7785e7d743
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/15/2017
ms.author: muralikk
ms.openlocfilehash: a01c170b1bc9c2b2ce9086d39de78a39fafb2c8b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="using-hello-azure-importexport-service-rest-api"></a><span data-ttu-id="06627-103">Utilizar a REST API do serviço de importação/exportação do Azure Olá</span><span class="sxs-lookup"><span data-stu-id="06627-103">Using hello Azure Import/Export service REST API</span></span>

<span data-ttu-id="06627-104">Olá serviço de importação/exportação do Microsoft Azure expõe um controlo programático de tooenable de REST API de tarefas de importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="06627-104">hello Microsoft Azure Import/Export service exposes a REST API tooenable programmatic control of import/export jobs.</span></span> <span data-ttu-id="06627-105">Pode utilizar a REST API de Olá tooperform todas Olá importar/exportar operações que pode realizar com Olá [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="06627-105">You can use hello REST API tooperform all of hello import/export operations that you can perform with hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="06627-106">Além disso, pode utilizar Olá REST API tooperform determinadas granulares operações, como a consulta de conclusão de percentagem de Olá de uma tarefa, que não estão atualmente disponíveis no portal clássico Olá.</span><span class="sxs-lookup"><span data-stu-id="06627-106">Additionally, you can use hello REST API tooperform certain granular operations, such as querying hello percentage completion of a job, which are not currently available in hello classic portal.</span></span>

<span data-ttu-id="06627-107">Consulte [utilizando Olá importação/exportação do Microsoft Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá toocreate portal clássico e gerir importação exportação e tarefas.</span><span class="sxs-lookup"><span data-stu-id="06627-107">See [Using hello Microsoft Azure Import/Export service tooTransfer Data tooBlob Storage](storage-import-export-service.md) for an overview of hello Import/Export service and a tutorial that demonstrates how toouse hello classic portal toocreate and manage import and export jobs.</span></span>

## <a name="service-endpoints"></a><span data-ttu-id="06627-108">pontos finais de serviço</span><span class="sxs-lookup"><span data-stu-id="06627-108">Service endpoints</span></span>

<span data-ttu-id="06627-109">Olá serviço importar/exportar do Azure é um fornecedor de recursos do Azure Resource Manager e fornece um conjunto de REST APIs a Olá ponto final de HTTPS para gerir as tarefas de importação/exportação os seguintes:</span><span class="sxs-lookup"><span data-stu-id="06627-109">hello Azure Import/Export service is a resource provider for Azure Resource Manager and provides a set of REST APIs at hello following HTTPS endpoint for managing import/export jobs:</span></span>

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a><span data-ttu-id="06627-110">Controlo de versões</span><span class="sxs-lookup"><span data-stu-id="06627-110">Versioning</span></span>

<span data-ttu-id="06627-111">Pedidos de serviço de importação/exportação do toohello tem de especificar Olá `api-version` parâmetro e defina o respetivo valor demasiado`2016-11-01`.</span><span class="sxs-lookup"><span data-stu-id="06627-111">Requests toohello Import/Export service must specify hello `api-version` parameter and set its value too`2016-11-01`.</span></span>

## <a name="importexport-service-operations"></a><span data-ttu-id="06627-112">Operações de serviço para importar/exportar</span><span class="sxs-lookup"><span data-stu-id="06627-112">Import/Export service operations</span></span>

[<span data-ttu-id="06627-113">Criação de uma tarefa de importação</span><span class="sxs-lookup"><span data-stu-id="06627-113">Creating an import job</span></span>](storage-import-export-creating-an-import-job.md)

[<span data-ttu-id="06627-114">Criação de uma tarefa de exportação</span><span class="sxs-lookup"><span data-stu-id="06627-114">Creating an export job</span></span>](storage-import-export-creating-an-export-job.md)

[<span data-ttu-id="06627-115">Obter informações de estado para uma tarefa</span><span class="sxs-lookup"><span data-stu-id="06627-115">Retrieving state information for a job</span></span>](storage-import-export-retrieving-state-info-for-a-job.md)

[<span data-ttu-id="06627-116">Enumerar tarefas</span><span class="sxs-lookup"><span data-stu-id="06627-116">Enumerating jobs</span></span>](storage-import-export-enumerating-jobs.md)

[<span data-ttu-id="06627-117">Cancelar e eliminar tarefas</span><span class="sxs-lookup"><span data-stu-id="06627-117">Cancelling and deleting jobs</span></span>](storage-import-export-cancelling-and-deleting-jobs.md)

[<span data-ttu-id="06627-118">Cópia de segurança manifestos de unidade</span><span class="sxs-lookup"><span data-stu-id="06627-118">Backing Up drive manifests</span></span>](storage-import-export-backing-up-drive-manifests.md)

[<span data-ttu-id="06627-119">Recuperação de diagnósticos e erros para tarefas de Importação/Exportação</span><span class="sxs-lookup"><span data-stu-id="06627-119">Diagnostics and error recovery for Import/Export jobs</span></span>](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a><span data-ttu-id="06627-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="06627-120">Next steps</span></span>

* [<span data-ttu-id="06627-121">Armazenamento para importar/exportar REST</span><span class="sxs-lookup"><span data-stu-id="06627-121">Storage Import/Export REST</span></span>](/rest/api/storageimportexport)
