---
title: "aaaBacking cópias de segurança do Azure para importar/exportar unidade manifestos | Microsoft Docs"
description: "Saiba como toohave sua unidade manifestos para o serviço de importação/exportação do Microsoft Azure Olá um cópia de segurança automaticamente."
author: muralikk
manager: syadav
editor: tysonn
services: storage
documentationcenter: 
ms.assetid: 594abd80-b834-4077-a474-d8a0f4b7928a
ms.service: storage
ms.workload: storage
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: muralikk
ms.openlocfilehash: f48b97a2cce62714aace2b30a393305202c7ecd9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a>Cópia de segurança unidade manifestos para tarefas de importação/exportação do Azure

Manifestos de unidade podem ser automaticamente copiadas em segurança tooblobs por definição Olá `BackupDriveManifest` propriedade demasiado`true` no Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operações de REST API. Por predefinição, Olá manifestos de unidade não são guardados em cópia de segurança. Olá unidade manifesto as cópias de segurança são armazenadas como blobs de blocos num contentor na conta do storage Olá associado à tarefa Olá. Por predefinição, o nome do contentor Olá é `waimportexport`, mas pode especificar um nome diferente no Olá `DiagnosticsPath` propriedade ao chamar Olá `Put Job` ou `Update Job Properties` operações. Olá blob manifesto cópia de segurança são denominados no Olá seguinte formato: `waies/jobname_driveid_timestamp_manifest.xml`.

 Pode obter Olá URI da unidade de cópia de segurança de Olá manifestos de uma tarefa ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operação. blob Olá URI é devolvido em Olá `ManifestUri` propriedade para cada unidade.

## <a name="next-steps"></a>Passos seguintes

* [Utilizar a REST API do serviço de importação/exportação Olá](storage-import-export-using-the-rest-api.md)
