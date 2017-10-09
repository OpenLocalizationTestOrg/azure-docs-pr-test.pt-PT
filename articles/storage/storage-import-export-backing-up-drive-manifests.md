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
# <a name="backing-up-drive-manifests-for-azure-importexport-jobs"></a><span data-ttu-id="408a0-103">Cópia de segurança unidade manifestos para tarefas de importação/exportação do Azure</span><span class="sxs-lookup"><span data-stu-id="408a0-103">Backing up drive manifests for Azure Import/Export jobs</span></span>

<span data-ttu-id="408a0-104">Manifestos de unidade podem ser automaticamente copiadas em segurança tooblobs por definição Olá `BackupDriveManifest` propriedade demasiado`true` no Olá [colocar tarefa](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) ou [propriedades da tarefa de atualização](/rest/api/storageimportexport/jobs#Jobs_Update) operações de REST API.</span><span class="sxs-lookup"><span data-stu-id="408a0-104">Drive manifests can be automatically backed up tooblobs by setting hello `BackupDriveManifest` property too`true` in hello [Put Job](/rest/api/storageimportexport/jobs#Jobs_CreateOrUpdate) or [Update Job Properties](/rest/api/storageimportexport/jobs#Jobs_Update) REST API operations.</span></span> <span data-ttu-id="408a0-105">Por predefinição, Olá manifestos de unidade não são guardados em cópia de segurança.</span><span class="sxs-lookup"><span data-stu-id="408a0-105">By default, hello drive manifests are not backed up.</span></span> <span data-ttu-id="408a0-106">Olá unidade manifesto as cópias de segurança são armazenadas como blobs de blocos num contentor na conta do storage Olá associado à tarefa Olá.</span><span class="sxs-lookup"><span data-stu-id="408a0-106">hello drive manifest backups are stored as block blobs in a container within hello storage account associated with hello job.</span></span> <span data-ttu-id="408a0-107">Por predefinição, o nome do contentor Olá é `waimportexport`, mas pode especificar um nome diferente no Olá `DiagnosticsPath` propriedade ao chamar Olá `Put Job` ou `Update Job Properties` operações.</span><span class="sxs-lookup"><span data-stu-id="408a0-107">By default, hello container name is `waimportexport`, but you can specify a different name in hello `DiagnosticsPath` property when calling hello `Put Job` or `Update Job Properties` operations.</span></span> <span data-ttu-id="408a0-108">Olá blob manifesto cópia de segurança são denominados no Olá seguinte formato: `waies/jobname_driveid_timestamp_manifest.xml`.</span><span class="sxs-lookup"><span data-stu-id="408a0-108">hello backup manifest blob are named in hello following format: `waies/jobname_driveid_timestamp_manifest.xml`.</span></span>

 <span data-ttu-id="408a0-109">Pode obter Olá URI da unidade de cópia de segurança de Olá manifestos de uma tarefa ao chamar Olá [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operação.</span><span class="sxs-lookup"><span data-stu-id="408a0-109">You can retrieve hello URI of hello backup drive manifests for a job by calling hello [Get Job](/rest/api/storageimportexport/jobs#Jobs_Get) operation.</span></span> <span data-ttu-id="408a0-110">blob Olá URI é devolvido em Olá `ManifestUri` propriedade para cada unidade.</span><span class="sxs-lookup"><span data-stu-id="408a0-110">hello blob URI is returned in hello `ManifestUri` property for each drive.</span></span>

## <a name="next-steps"></a><span data-ttu-id="408a0-111">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="408a0-111">Next steps</span></span>

* [<span data-ttu-id="408a0-112">Utilizar a REST API do serviço de importação/exportação Olá</span><span class="sxs-lookup"><span data-stu-id="408a0-112">Using hello Import/Export service REST API</span></span>](storage-import-export-using-the-rest-api.md)
