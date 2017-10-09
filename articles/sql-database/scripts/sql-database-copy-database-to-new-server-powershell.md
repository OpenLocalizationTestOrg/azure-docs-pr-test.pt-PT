---
title: "do novo para a base de dados do SQL Server de exemplo-cópia-Azure aaaPowerShell | Microsoft Docs"
description: Azure PowerShell exemplo script toocopy um SQL Server da base de dados tooa novo servidor
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: load & move data
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: c08f993bd75913481b1d534857ac057263e1d02b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toocopy-a-sql-database-tooa-new-server"></a><span data-ttu-id="7cb49-103">Utilizar o PowerShell toocopy um SQL Server da base de dados tooa novo servidor</span><span class="sxs-lookup"><span data-stu-id="7cb49-103">Use PowerShell toocopy a SQL database tooa new server</span></span>

<span data-ttu-id="7cb49-104">Neste exemplo de script do PowerShell cria uma cópia da base de dados existente num servidor novo.</span><span class="sxs-lookup"><span data-stu-id="7cb49-104">This PowerShell script example creates a copy of an existing database in a new server.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="copy-a-database-tooa-new-server"></a><span data-ttu-id="7cb49-105">Copiar um base de dados tooa novo servidor</span><span class="sxs-lookup"><span data-stu-id="7cb49-105">Copy a database tooa new server</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/copy-database-to-new-server/copy-database-to-new-server.ps1?highlight=18-21 "Copy database toonew server")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7cb49-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="7cb49-106">Clean up deployment</span></span>

<span data-ttu-id="7cb49-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="7cb49-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7cb49-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="7cb49-108">Script explanation</span></span>

<span data-ttu-id="7cb49-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="7cb49-109">This script uses hello following commands.</span></span> <span data-ttu-id="7cb49-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="7cb49-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7cb49-111">Comando</span><span class="sxs-lookup"><span data-stu-id="7cb49-111">Command</span></span> | <span data-ttu-id="7cb49-112">Notas</span><span class="sxs-lookup"><span data-stu-id="7cb49-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7cb49-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7cb49-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7cb49-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7cb49-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7cb49-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7cb49-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7cb49-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="7cb49-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="7cb49-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7cb49-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="7cb49-118">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="7cb49-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="7cb49-119">Novo AzureRmSqlDatabaseCopy</span><span class="sxs-lookup"><span data-stu-id="7cb49-119">New-AzureRmSqlDatabaseCopy</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasecopy) | <span data-ttu-id="7cb49-120">Cria uma cópia da base de dados que utiliza o instantâneo de Olá em Olá hora atual.</span><span class="sxs-lookup"><span data-stu-id="7cb49-120">Creates a copy of a database that uses hello snapshot at hello current time.</span></span> |
| [<span data-ttu-id="7cb49-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7cb49-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7cb49-122">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7cb49-122">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7cb49-123">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7cb49-123">Next steps</span></span>

<span data-ttu-id="7cb49-124">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7cb49-124">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7cb49-125">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7cb49-125">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
