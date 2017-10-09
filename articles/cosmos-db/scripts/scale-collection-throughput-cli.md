---
title: "débito de contentor do CLI escala de Script do Azure Cosmos DB aaaAzure | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - escala Azure Cosmos DB contianer débito"
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
ms.openlocfilehash: b1a60feaf43f555a9f6ba20e5e0617f73521c0a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-cosmos-db-container-throughput-using-hello-azure-cli"></a><span data-ttu-id="056da-103">Débito de contentor Azure Cosmos BD do dimensionamento utilizando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="056da-103">Scale Azure Cosmos DB container throughput using hello Azure CLI</span></span>

<span data-ttu-id="056da-104">Este exemplo ajusta o débito de contentor para qualquer tipo de contentor do Azure Cosmos DB.</span><span class="sxs-lookup"><span data-stu-id="056da-104">This sample scales container throughput for any kind of Azure Cosmos DB container.</span></span>  

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="056da-105">Se escolher tooinstall e utilizar Olá CLI localmente, este tópico requer que estiver a executar Olá CLI do Azure versão 2.0 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="056da-105">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="056da-106">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="056da-106">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="056da-107">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="056da-107">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="056da-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="056da-108">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/cosmosdb/scale-cosmosdb-throughput/scale-cosmosdb-throughput.sh?highlight=40-46 "Scale Azure Cosmos DB throughput")]

## <a name="clean-up-deployment"></a><span data-ttu-id="056da-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="056da-109">Clean up deployment</span></span>

<span data-ttu-id="056da-110">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="056da-110">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="056da-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="056da-111">Script explanation</span></span>

<span data-ttu-id="056da-112">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="056da-112">This script uses hello following commands.</span></span> <span data-ttu-id="056da-113">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="056da-113">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="056da-114">Comando</span><span class="sxs-lookup"><span data-stu-id="056da-114">Command</span></span> | <span data-ttu-id="056da-115">Notas</span><span class="sxs-lookup"><span data-stu-id="056da-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="056da-116">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="056da-116">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="056da-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="056da-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="056da-118">atualização de cosmosdb AZ</span><span class="sxs-lookup"><span data-stu-id="056da-118">az cosmosdb update</span></span>](https://docs.microsoft.com/cli/azure/cosmosdb#update) | <span data-ttu-id="056da-119">Atualiza uma conta de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="056da-119">Updates an Azure Cosmos DB account.</span></span> |
| [<span data-ttu-id="056da-120">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="056da-120">az group delete</span></span>](https://docs.microsoft.com/cli/azure/group#delete) | <span data-ttu-id="056da-121">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="056da-121">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="056da-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="056da-122">Next steps</span></span>

<span data-ttu-id="056da-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="056da-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="056da-124">Exemplos de script da CLI do Azure Cosmos DB adicionais podem ser encontrados na Olá [documentação da CLI do Azure Cosmos DB](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="056da-124">Additional Azure Cosmos DB CLI script samples can be found in hello [Azure Cosmos DB CLI documentation](../cli-samples.md).</span></span>
