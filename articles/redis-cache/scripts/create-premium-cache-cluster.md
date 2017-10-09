---
title: aaaAzure CLI Script de exemplo - criar uma Cache de Redis do Azure Premium com clustering | Microsoft Docs
description: "Script CLI do Azure de exemplo - criação de um escalão Premium a Cache de Redis do Azure com o clustering"
services: redis-cache
documentationcenter: 
author: steved0x
manager: douge
editor: 
tags: azure-service-management
ms.assetid: 07bcceae-2521-4fe3-b88f-ed833104ddd2
ms.service: cache-redis
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 04/14/2017
ms.author: sdanie
ms.openlocfilehash: ca34d40059b282cb2abc7e3e2b8771226029744c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-premium-azure-redis-cache-with-clustering"></a><span data-ttu-id="e41da-103">Criar uma Cache de Redis do Azure Premium com clustering</span><span class="sxs-lookup"><span data-stu-id="e41da-103">Create a Premium Azure Redis Cache with clustering</span></span>

<span data-ttu-id="e41da-104">Neste cenário, saiba como toocreate ativado um escalão Premium da 6 GB a Cache de Redis do Azure com o clustering e duas partições horizontais.</span><span class="sxs-lookup"><span data-stu-id="e41da-104">In this scenario, you learn how toocreate a 6 GB Premium tier Azure Redis Cache with clustering enabled and two shards.</span></span>

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

## <a name="sample-script"></a><span data-ttu-id="e41da-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e41da-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/redis-cache/create-premium-cache-cluster/create-premium-cache-cluster.sh "Azure Redis Cache")]

[!INCLUDE [cli-script-clean-up](../../../includes/redis-cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="e41da-106">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="e41da-106">Script explanation</span></span>

<span data-ttu-id="e41da-107">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos e uma cache de redis do escalão Premium com clustering de ativação.</span><span class="sxs-lookup"><span data-stu-id="e41da-107">This script uses hello following commands toocreate a resource group and a Premium tier redis cache with clustering enable.</span></span> <span data-ttu-id="e41da-108">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="e41da-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e41da-109">Comando</span><span class="sxs-lookup"><span data-stu-id="e41da-109">Command</span></span> | <span data-ttu-id="e41da-110">Notas</span><span class="sxs-lookup"><span data-stu-id="e41da-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e41da-111">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="e41da-111">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="e41da-112">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e41da-112">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e41da-113">Criar AZ redis</span><span class="sxs-lookup"><span data-stu-id="e41da-113">az redis create</span></span>](https://docs.microsoft.com/cli/azure/redis#create) | <span data-ttu-id="e41da-114">Crie uma instância da Cache de Redis.</span><span class="sxs-lookup"><span data-stu-id="e41da-114">Create Redis Cache instance.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="e41da-115">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e41da-115">Next steps</span></span>

<span data-ttu-id="e41da-116">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e41da-116">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e41da-117">Exemplos de script CLI de Cache de Redis do Azure adicionais podem ser encontrados na Olá [documentação de Cache de Redis do Azure](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e41da-117">Additional Azure Redis Cache CLI script samples can be found in hello [Azure Redis Cache documentation](../cli-samples.md).</span></span>
