---
title: "a base de dados SQL de exemplo restauro-cópia de segurança Azure aaaPowerShell | Microsoft Docs"
description: "Azure PowerShell exemplo script toorestore uma base de dados SQL do Azure de cópias de segurança georredundante"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 68becb89e8a8680aa2efc3de8ad947e674c5fc35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toorestore-an-azure-sql-database-from-backups"></a><span data-ttu-id="7eff0-103">Utilizar o PowerShell toorestore uma base de dados SQL do Azure de cópias de segurança</span><span class="sxs-lookup"><span data-stu-id="7eff0-103">Use PowerShell toorestore an Azure SQL database from backups</span></span>

<span data-ttu-id="7eff0-104">Neste exemplo de script do PowerShell restaura uma base de dados SQL do Azure a partir de uma cópia de segurança georredundante, restaura um eliminada do Azure SQL da base de dados tooits mais recente cópia de segurança e restaura um ponto de específico de tooa de base de dados SQL do Azure no tempo.</span><span class="sxs-lookup"><span data-stu-id="7eff0-104">This PowerShell script example restores an Azure SQL database from a geo-redundant backup, restores a deleted Azure SQL database tooits latest backup, and restores an Azure SQL database tooa specific point in time.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="7eff0-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7eff0-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/restore-database/restore-database.ps1?highlight=17-18 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7eff0-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="7eff0-106">Clean up deployment</span></span>

<span data-ttu-id="7eff0-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="7eff0-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7eff0-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="7eff0-108">Script explanation</span></span>

<span data-ttu-id="7eff0-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="7eff0-109">This script uses hello following commands.</span></span> <span data-ttu-id="7eff0-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="7eff0-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7eff0-111">Comando</span><span class="sxs-lookup"><span data-stu-id="7eff0-111">Command</span></span> | <span data-ttu-id="7eff0-112">Notas</span><span class="sxs-lookup"><span data-stu-id="7eff0-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7eff0-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7eff0-113">New-AzureRmResourceGroup</span></span>](https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.5.0/new-azurermresourcegroup) | <span data-ttu-id="7eff0-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7eff0-114">Creates a resource group in which all resources are stored.</span></span> | [<span data-ttu-id="7eff0-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7eff0-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7eff0-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="7eff0-116">Creates a logical server that hosts a database or elastic pool.</span></span> | 
| [<span data-ttu-id="7eff0-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7eff0-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="7eff0-118">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="7eff0-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
[<span data-ttu-id="7eff0-119">Get-AzureRmSqlDatabaseGeoBackup</span><span class="sxs-lookup"><span data-stu-id="7eff0-119">Get-AzureRmSqlDatabaseGeoBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasegeobackup) | <span data-ttu-id="7eff0-120">Obtém uma cópia de segurança georredundante uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="7eff0-120">Gets a geo-redundant backup of a database.</span></span> |
| [<span data-ttu-id="7eff0-121">Restauro-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7eff0-121">Restore-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/restore-azurermsqldatabase) | <span data-ttu-id="7eff0-122">Restaura uma base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7eff0-122">Restores a SQL database.</span></span> |
|[<span data-ttu-id="7eff0-123">Remove-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7eff0-123">Remove-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/remove-azurermsqldatabase) | <span data-ttu-id="7eff0-124">Remove uma base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="7eff0-124">Removes an Azure SQL database.</span></span> |
| [<span data-ttu-id="7eff0-125">Get-AzureRmSqlDeletedDatabaseBackup</span><span class="sxs-lookup"><span data-stu-id="7eff0-125">Get-AzureRmSqlDeletedDatabaseBackup</span></span>](/powershell/module/azurerm.sql/get-azurermsqldeleteddatabasebackup) | <span data-ttu-id="7eff0-126">Obtém uma base de dados eliminada pode restaurar.</span><span class="sxs-lookup"><span data-stu-id="7eff0-126">Gets a deleted database that you can restore.</span></span> |
| [<span data-ttu-id="7eff0-127">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7eff0-127">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7eff0-128">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7eff0-128">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7eff0-129">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7eff0-129">Next steps</span></span>

<span data-ttu-id="7eff0-130">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7eff0-130">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7eff0-131">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7eff0-131">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
