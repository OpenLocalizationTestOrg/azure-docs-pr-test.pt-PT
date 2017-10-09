---
title: "replicação de CLI Script-Multiregion aaaAzure para a base de dados do Azure Cosmos | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - Multiregion replicação para a base de dados do Azure Cosmos"
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 06/02/2017
ms.author: mimig
ms.openlocfilehash: e3590303ed3bda9eca1046bf62fff6b61333156c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-hello-azure-cli"></a><span data-ttu-id="2dbaf-103">Replicar uma conta de base de dados de base de dados do Azure Cosmos em várias regiões e configurar as prioridades de ativação pós-falha utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2dbaf-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using hello Azure CLI</span></span>

<span data-ttu-id="2dbaf-104">Este exemplo replica qualquer tipo de conta de base de dados de base de dados do Azure Cosmos em várias regiões e configura as prioridades de ativação pós-falha utilizando Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using hello Azure CLI.</span></span>

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="2dbaf-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="2dbaf-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="2dbaf-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2dbaf-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="2dbaf-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="2dbaf-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-replicate-multiple-regions/scale-cosmosdb-replicate-multiple-regions.sh?highlight=21-31 "Scale Azure Cosmos DB into multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="2dbaf-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="2dbaf-109">Clean up deployment</span></span>

<span data-ttu-id="2dbaf-110">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="2dbaf-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="2dbaf-111">Script explanation</span></span>

<span data-ttu-id="2dbaf-112">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-112">This script uses hello following commands.</span></span> <span data-ttu-id="2dbaf-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="2dbaf-114">Comando</span><span class="sxs-lookup"><span data-stu-id="2dbaf-114">Command</span></span> | <span data-ttu-id="2dbaf-115">Notas</span><span class="sxs-lookup"><span data-stu-id="2dbaf-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2dbaf-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="2dbaf-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="2dbaf-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2dbaf-118">atualização de cosmosdb AZ</span><span class="sxs-lookup"><span data-stu-id="2dbaf-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="2dbaf-119">Atualiza uma conta de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="2dbaf-120">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="2dbaf-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="2dbaf-121">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="2dbaf-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2dbaf-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2dbaf-122">Next steps</span></span>

<span data-ttu-id="2dbaf-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2dbaf-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="2dbaf-124">Exemplos de script da CLI do Azure Cosmos DB adicionais podem ser encontrados na Olá [documentação da CLI do Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="2dbaf-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
