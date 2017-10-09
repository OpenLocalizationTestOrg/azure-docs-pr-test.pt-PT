---
title: "aaaAzure Script de PowerShell-Multiregion replicação de base de dados do Azure Cosmos | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - Multiregion replicação para a base de dados do Azure Cosmos"
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
ms.openlocfilehash: 8e3e79f086f46fc037d52589eb8bcf4557214566
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-an-azure-cosmos-db-database-account-in-multiple-regions-and-configure-failover-priorities-using-powershell"></a><span data-ttu-id="151a3-103">Replicar uma conta de base de dados de base de dados do Azure Cosmos em várias regiões e configurar as prioridades de ativação pós-falha com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="151a3-103">Replicate an Azure Cosmos DB database account in multiple regions and configure failover priorities using PowerShell</span></span>

<span data-ttu-id="151a3-104">Este exemplo replica qualquer tipo de conta de base de dados de base de dados do Azure Cosmos em várias regiões e configura as prioridades de ativação pós-falha com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="151a3-104">This sample replicates any kind of Azure Cosmos DB database account in multiple regions and configures failover priorities using PowerShell.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="151a3-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="151a3-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/cosmosdb/replicate-database-multiple-regions/replicate-database-multiple-regions.ps1?highlight=37-44,47-48,51-55 "Replicate an Azure Cosmos DB account across multiple regions")]

## <a name="clean-up-deployment"></a><span data-ttu-id="151a3-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="151a3-106">Clean up deployment</span></span>

<span data-ttu-id="151a3-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="151a3-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="151a3-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="151a3-108">Script explanation</span></span>

<span data-ttu-id="151a3-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="151a3-109">This script uses hello following commands.</span></span> <span data-ttu-id="151a3-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="151a3-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="151a3-111">Comando</span><span class="sxs-lookup"><span data-stu-id="151a3-111">Command</span></span> | <span data-ttu-id="151a3-112">Notas</span><span class="sxs-lookup"><span data-stu-id="151a3-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="151a3-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="151a3-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="151a3-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="151a3-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="151a3-115">Novo AzureRmResource</span><span class="sxs-lookup"><span data-stu-id="151a3-115">New-AzureRmResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/new-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="151a3-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="151a3-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="151a3-117">Conjunto AzureRMResource</span><span class="sxs-lookup"><span data-stu-id="151a3-117">Set-AzureRMResource</span></span>](https://docs.microsoft.com/powershell/module/azurerm.resources/set-azurermresource?view=azurermps-3.8.0) | <span data-ttu-id="151a3-118">Modifica a conta de base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="151a3-118">Modifies hello database account.</span></span> |
| [<span data-ttu-id="151a3-119">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="151a3-119">Remove-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/remove-azurermresourcegroup) | <span data-ttu-id="151a3-120">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="151a3-120">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="151a3-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="151a3-121">Next steps</span></span>

<span data-ttu-id="151a3-122">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/).</span><span class="sxs-lookup"><span data-stu-id="151a3-122">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/).</span></span>

<span data-ttu-id="151a3-123">Exemplos de script do PowerShell de base de dados do Azure Cosmos adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do Azure Cosmos](../powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="151a3-123">Additional Azure Cosmos DB PowerShell script samples can be found in hello [Azure Cosmos DB PowerShell scripts](../powershell-samples.md).</span></span>
