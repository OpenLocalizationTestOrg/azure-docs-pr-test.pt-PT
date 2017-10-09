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
# <a name="using-hello-azure-importexport-service-rest-api"></a>Utilizar a REST API do serviço de importação/exportação do Azure Olá

Olá serviço de importação/exportação do Microsoft Azure expõe um controlo programático de tooenable de REST API de tarefas de importação/exportação. Pode utilizar a REST API de Olá tooperform todas Olá importar/exportar operações que pode realizar com Olá [portal do Azure](https://portal.azure.com/). Além disso, pode utilizar Olá REST API tooperform determinadas granulares operações, como a consulta de conclusão de percentagem de Olá de uma tarefa, que não estão atualmente disponíveis no portal clássico Olá.

Consulte [utilizando Olá importação/exportação do Microsoft Azure service tooTransfer dados tooBlob armazenamento](storage-import-export-service.md) para uma descrição geral do serviço de importação/exportação Olá e um tutorial que demonstra como toouse Olá toocreate portal clássico e gerir importação exportação e tarefas.

## <a name="service-endpoints"></a>pontos finais de serviço

Olá serviço importar/exportar do Azure é um fornecedor de recursos do Azure Resource Manager e fornece um conjunto de REST APIs a Olá ponto final de HTTPS para gerir as tarefas de importação/exportação os seguintes:

```
https://management.azure.com/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.ImportExport/jobs/<job-name>
```

## <a name="versioning"></a>Controlo de versões

Pedidos de serviço de importação/exportação do toohello tem de especificar Olá `api-version` parâmetro e defina o respetivo valor demasiado`2016-11-01`.

## <a name="importexport-service-operations"></a>Operações de serviço para importar/exportar

[Criação de uma tarefa de importação](storage-import-export-creating-an-import-job.md)

[Criação de uma tarefa de exportação](storage-import-export-creating-an-export-job.md)

[Obter informações de estado para uma tarefa](storage-import-export-retrieving-state-info-for-a-job.md)

[Enumerar tarefas](storage-import-export-enumerating-jobs.md)

[Cancelar e eliminar tarefas](storage-import-export-cancelling-and-deleting-jobs.md)

[Cópia de segurança manifestos de unidade](storage-import-export-backing-up-drive-manifests.md)

[Recuperação de diagnósticos e erros para tarefas de Importação/Exportação](storage-import-export-diagnostics-and-error-recovery.md)

## <a name="next-steps"></a>Passos seguintes

* [Armazenamento para importar/exportar REST](/rest/api/storageimportexport)
