---
title: "exemplo de aaaCLI dimensiona uma SQL elástica conjunto-SQL Database do Azure | Microsoft Docs"
description: "Azure CLI exemplo script tooscale um agrupamento elástico de SQL no SQL Database do Azure"
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
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 436128b8183213f78b9abc2ec46efe2a3ed3c37c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-tooscale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="17e8f-103">Utilize o CLI tooscale um agrupamento elástico de SQL no SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="17e8f-103">Use CLI tooscale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="17e8f-104">Neste exemplo de script da CLI do Azure cria conjuntos elásticos SQL, move agrupados bases de dados e níveis de desempenho do conjunto elástico é alterado.</span><span class="sxs-lookup"><span data-stu-id="17e8f-104">This Azure CLI script example creates SQL elastic pools, moves pooled databases, and changes elastic pool performance levels.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="17e8f-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="17e8f-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="17e8f-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="17e8f-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="17e8f-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="17e8f-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="17e8f-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="17e8f-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/scale-pool/scale-pool.sh "Move database between pools")]

## <a name="clean-up-deployment"></a><span data-ttu-id="17e8f-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="17e8f-109">Clean up deployment</span></span>

<span data-ttu-id="17e8f-110">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="17e8f-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="17e8f-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="17e8f-111">Script explanation</span></span>

<span data-ttu-id="17e8f-112">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, servidor lógico, base de dados SQL e as regras de firewall.</span><span class="sxs-lookup"><span data-stu-id="17e8f-112">This script uses hello following commands toocreate a resource group, logical server, SQL Database, and firewall rules.</span></span> <span data-ttu-id="17e8f-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="17e8f-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="17e8f-114">Comando</span><span class="sxs-lookup"><span data-stu-id="17e8f-114">Command</span></span> | <span data-ttu-id="17e8f-115">Notas</span><span class="sxs-lookup"><span data-stu-id="17e8f-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17e8f-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="17e8f-116">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="17e8f-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="17e8f-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="17e8f-118">servidor de sql AZ criar</span><span class="sxs-lookup"><span data-stu-id="17e8f-118">az sql server create</span></span>](https://docs.microsoft.com/cli/azure/sql/server#create) | <span data-ttu-id="17e8f-119">Cria um servidor lógico que anfitriões Olá base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="17e8f-119">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="17e8f-120">criar conjuntos de elástico do sql AZ</span><span class="sxs-lookup"><span data-stu-id="17e8f-120">az sql elastic-pools create</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#create) | <span data-ttu-id="17e8f-121">Cria um conjunto de bases de dados elásticas no servidor lógico de Olá.</span><span class="sxs-lookup"><span data-stu-id="17e8f-121">Creates an elastic database pool within hello logical server.</span></span> |
| [<span data-ttu-id="17e8f-122">Criar BD do sql AZ</span><span class="sxs-lookup"><span data-stu-id="17e8f-122">az sql db create</span></span>](https://docs.microsoft.com/cli/azure/sql/db#create) | <span data-ttu-id="17e8f-123">Cria Olá base de dados SQL no servidor lógico de Olá.</span><span class="sxs-lookup"><span data-stu-id="17e8f-123">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="17e8f-124">atualização de conjuntos elásticos sql AZ</span><span class="sxs-lookup"><span data-stu-id="17e8f-124">az sql elastic-pools update</span></span>](https://docs.microsoft.com/cli/azure/sql/elastic-pool#update) | <span data-ttu-id="17e8f-125">As atualizações de um conjunto de bases de dados elásticas, neste Olá de alterações de exemplo atribuída eDTU.</span><span class="sxs-lookup"><span data-stu-id="17e8f-125">Updates an elastic database pool, in this example changes hello assigned eDTU.</span></span> |
| [<span data-ttu-id="17e8f-126">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="17e8f-126">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="17e8f-127">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="17e8f-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17e8f-128">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="17e8f-128">Next steps</span></span>

<span data-ttu-id="17e8f-129">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="17e8f-129">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="17e8f-130">Exemplos de script CLI de base de dados do SQL adicionais podem ser encontrados na Olá [documentação da SQL Database do Azure](../sql-database-cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="17e8f-130">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>
