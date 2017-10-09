---
title: chaves de aaaAzure conta de Script de PowerShell-Get para cosmosdb | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - obter chaves de conta para cosmosdb
services: cosmos-db
documentationcenter: cosmosdb
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: cosmosdb
ms.workload: database
ms.date: 05/10/2017
ms.author: mimig
ms.openlocfilehash: 9ccee3085dc4fa6507d43e4a220dd5fc32889a9b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="get-account-keys-for-azure-cosmos-db-using-powershell"></a><span data-ttu-id="6b84d-103">Obter chaves de conta de base de dados do Cosmos do Azure com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6b84d-103">Get account keys for Azure Cosmos DB using PowerShell</span></span>

<span data-ttu-id="6b84d-104">Este exemplo obtém as chaves de conta para qualquer tipo de conta de base de dados do Azure Cosmos.</span><span class="sxs-lookup"><span data-stu-id="6b84d-104">This sample gets account keys for any kind of Azure Cosmos DB account.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="6b84d-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="6b84d-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/get-account-keys/get-account-keys.ps1?highlight=36-40 "Get hello keys for an Azure Cosmos DB account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="6b84d-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="6b84d-106">Clean up deployment</span></span>

<span data-ttu-id="6b84d-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="6b84d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="6b84d-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="6b84d-108">Script explanation</span></span>

<span data-ttu-id="6b84d-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="6b84d-109">This script uses hello following commands.</span></span> <span data-ttu-id="6b84d-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="6b84d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="6b84d-111">Comando</span><span class="sxs-lookup"><span data-stu-id="6b84d-111">Command</span></span> | <span data-ttu-id="6b84d-112">Notas</span><span class="sxs-lookup"><span data-stu-id="6b84d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6b84d-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6b84d-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="6b84d-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="6b84d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6b84d-115">Novo AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="6b84d-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="6b84d-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="6b84d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="6b84d-117">AzureRmResourceAction invocar</span><span class="sxs-lookup"><span data-stu-id="6b84d-117">Invoke-AzureRmResourceAction</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/invoke-azurermresourceaction?view=azurermps-3.8.0) | <span data-ttu-id="6b84d-118">Invoca uma ação no Olá conta CosmosDB do Azure.</span><span class="sxs-lookup"><span data-stu-id="6b84d-118">Invokes an action on hello Azure CosmosDB account.</span></span> |
| [<span data-ttu-id="6b84d-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="6b84d-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="6b84d-120">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="6b84d-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="6b84d-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="6b84d-121">Next steps</span></span>

<span data-ttu-id="6b84d-122">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="6b84d-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="6b84d-123">Exemplos de script do PowerShell de base de dados do Azure Cosmos adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="6b84d-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
