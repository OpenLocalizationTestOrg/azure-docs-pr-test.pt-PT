---
title: "Deteção de ameaças exemplo auditoria aaaPowerShell-Azure base de dados SQL | Microsoft Docs"
description: "Azure PowerShell exemplo script tooconfigure auditoria de deteção de ameaças e numa base de dados SQL do Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: mvc,security
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 97e057ac6efe5e730404ae796bc01e7e5c70df35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-sql-database-auditing-and-threat-detection"></a><span data-ttu-id="e9697-103">Utilizar o PowerShell tooconfigure base de dados SQL auditoria e deteção de ameaças</span><span class="sxs-lookup"><span data-stu-id="e9697-103">Use PowerShell tooconfigure SQL Database auditing and threat detection</span></span>

<span data-ttu-id="e9697-104">Neste exemplo de script do PowerShell configura a base de dados SQL auditoria e deteção de ameaças.</span><span class="sxs-lookup"><span data-stu-id="e9697-104">This PowerShell script example configures SQL Database auditing and threat detection.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="e9697-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e9697-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/database-auditing-and-threat-detection/database-auditing-and-threat-detection.ps1?highlight=13-14 "Configure auditing and threat detection")]

## <a name="clean-up-deployment"></a><span data-ttu-id="e9697-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="e9697-106">Clean up deployment</span></span>

<span data-ttu-id="e9697-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="e9697-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="e9697-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="e9697-108">Script explanation</span></span>

<span data-ttu-id="e9697-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="e9697-109">This script uses hello following commands.</span></span> <span data-ttu-id="e9697-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="e9697-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e9697-111">Comando</span><span class="sxs-lookup"><span data-stu-id="e9697-111">Command</span></span> | <span data-ttu-id="e9697-112">Notas</span><span class="sxs-lookup"><span data-stu-id="e9697-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e9697-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e9697-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e9697-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e9697-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e9697-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="e9697-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="e9697-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="e9697-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="e9697-117">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="e9697-117">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="e9697-118">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="e9697-118">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="e9697-119">Novo-AzureRmStorageAccount</span><span class="sxs-lookup"><span data-stu-id="e9697-119">New-AzureRmStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="e9697-120">Cria uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="e9697-120">Creates a Storage account.</span></span> |
| [<span data-ttu-id="e9697-121">Conjunto AzureRmSqlDatabaseAuditingPolicy</span><span class="sxs-lookup"><span data-stu-id="e9697-121">Set-AzureRmSqlDatabaseAuditingPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabaseauditingpolicy) | <span data-ttu-id="e9697-122">Define a política de auditoria Olá para uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="e9697-122">Sets hello auditing policy for a database.</span></span> |
| [<span data-ttu-id="e9697-123">Conjunto AzureRmSqlDatabaseThreatDetectionPolicy</span><span class="sxs-lookup"><span data-stu-id="e9697-123">Set-AzureRmSqlDatabaseThreatDetectionPolicy</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasethreatdetectionpolicy) | <span data-ttu-id="e9697-124">Define uma política de deteção de ameaças de uma base de dados.</span><span class="sxs-lookup"><span data-stu-id="e9697-124">Sets a threat detection policy on a database.</span></span> |
| [<span data-ttu-id="e9697-125">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e9697-125">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e9697-126">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="e9697-126">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="e9697-127">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e9697-127">Next steps</span></span>

<span data-ttu-id="e9697-128">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e9697-128">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="e9697-129">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="e9697-129">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
