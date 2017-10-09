---
title: "agrupamento elástico de SQL da base de dados SQL do Azure de exemplo mover aaaCLI | Microsoft Docs"
description: "Azure CLI exemplo script toomove uma base de dados SQL num agrupamento elástico de SQL"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/05/2017
ms.author: janeng
ms.openlocfilehash: 841eb57d2d49612c3fadd3a6424a2b0309c69719
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toomove-an-azure-sql-database-in-a-sql-elastic-pool"></a><span data-ttu-id="dd350-103">Utilize o CLI toomove uma base de dados SQL do Azure num agrupamento elástico de SQL</span><span class="sxs-lookup"><span data-stu-id="dd350-103">Use CLI toomove an Azure SQL database in a SQL elastic pool</span></span>

<span data-ttu-id="dd350-104">Neste exemplo de script da CLI do Azure cria dois conjuntos elásticos e move de uma base de dados SQL do Azure de um agrupamento elástico de SQL para outro conjunto elástico de SQL e, em seguida, avança base de dados de Olá fora do nível de desempenho do conjunto elástico tooa única base de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="dd350-104">This Azure CLI script example creates two elastic pools and moves an Azure SQL database from one SQL elastic pool into another SQL elastic pool, and then moves hello database out of elastic pool tooa single Azure database performance level.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="dd350-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="dd350-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="dd350-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="dd350-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="dd350-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="dd350-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="dd350-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="dd350-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/move-database-between-pools/move-database-between-pools.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="dd350-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="dd350-109">Clean up deployment</span></span>

<span data-ttu-id="dd350-110">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="dd350-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="dd350-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="dd350-111">Script explanation</span></span>

<span data-ttu-id="dd350-112">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="dd350-112">This script uses hello following commands.</span></span> <span data-ttu-id="dd350-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="dd350-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="dd350-114">Comando</span><span class="sxs-lookup"><span data-stu-id="dd350-114">Command</span></span> | <span data-ttu-id="dd350-115">Notas</span><span class="sxs-lookup"><span data-stu-id="dd350-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="dd350-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="dd350-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="dd350-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="dd350-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="dd350-118">servidor de sql AZ criar</span><span class="sxs-lookup"><span data-stu-id="dd350-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="dd350-119">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="dd350-119">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="dd350-120">criar conjuntos de elástico do sql AZ</span><span class="sxs-lookup"><span data-stu-id="dd350-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="dd350-121">Cria um conjunto elástico no servidor lógico de Olá.</span><span class="sxs-lookup"><span data-stu-id="dd350-121">Creates an elastic pool within hello logical server.</span></span> |
| [<span data-ttu-id="dd350-122">Criar BD do sql AZ</span><span class="sxs-lookup"><span data-stu-id="dd350-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="dd350-123">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="dd350-123">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="dd350-124">atualização de base de dados do sql AZ</span><span class="sxs-lookup"><span data-stu-id="dd350-124">az sql db update</span></span>](https://docs.microsoft.com/cli/azure/sql/db#update) | <span data-ttu-id="dd350-125">Atualiza as propriedades de base de dados ou move de uma base de dados para fora do ou entre conjuntos elásticos.</span><span class="sxs-lookup"><span data-stu-id="dd350-125">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="dd350-126">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="dd350-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="dd350-127">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="dd350-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="dd350-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="dd350-128">Next steps</span></span>

<span data-ttu-id="dd350-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="dd350-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="dd350-130">Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="dd350-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>


