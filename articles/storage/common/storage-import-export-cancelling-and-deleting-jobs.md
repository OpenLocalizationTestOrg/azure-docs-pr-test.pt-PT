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
# <a name="canceling-and-deleting-azure-importexport-jobs"></a>Cancelar e eliminar tarefas de importação/exportação do Azure

 toorequest que uma tarefa ser cancelada antes de está a ser Olá `Packaging` Estado, chamada Olá [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operação e conjunto Olá `CancelRequested` elemento demasiado`true`. tarefa de Olá é cancelada numa base de melhor esforço. Se unidades estão no processo de Olá de transferência de dados, os dados podem continuar toobe transferido, mesmo depois foi solicitado o cancelamento.

 Uma tarefa cancelada é movido toohello `Completed` estado e são mantidos durante 90 dias, altura em que é eliminado.

 toodelete uma tarefa, chamada Olá [tarefa eliminar](/rest/api/storageimportexport/jobs#Jobs_Delete) operação antes de tarefa Olá tem fornecidos (ou seja, enquanto a tarefa de Olá está em Olá `Creating` Estado). Também pode eliminar uma tarefa quando estiver a ser Olá `Completed` estado. Depois de eliminar uma tarefa, o estado e informações deixam de estar acessíveis através de Olá REST API ou Olá portal do Azure.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar a REST API do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
