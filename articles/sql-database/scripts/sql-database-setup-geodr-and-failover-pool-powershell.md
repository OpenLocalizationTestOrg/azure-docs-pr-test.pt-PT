---
title: "aaaPowerShell exemplo-ativo georreplicação replicação agrupados SQL database do Azure | Microsoft Docs"
description: "Azure tooset de script de exemplo do PowerShell segurança georreplicação ativa para uma base de dados SQL do Azure agrupado"
services: sql-database
documentationcenter: sql-database
author: CarlRabeler
manager: jhubbard
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: business continuity
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 07/25/2017
ms.author: carlrab
ms.openlocfilehash: 9d183f08dcc07ba864e42fe70a562fef8bd572f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooconfigure-active-geo-replication-for-a-pooled-azure-sql-database"></a><span data-ttu-id="7533d-103">Utilizar o PowerShell tooconfigure georreplicação ativa para uma base de dados SQL do Azure agrupado</span><span class="sxs-lookup"><span data-stu-id="7533d-103">Use PowerShell tooconfigure active geo-replication for a pooled Azure SQL database</span></span>

<span data-ttu-id="7533d-104">Neste exemplo de script do PowerShell configura a georreplicação ativa para uma base de dados SQL do Azure num conjunto elástico e a ativação pós-falha toohello réplica secundária de Olá SQL database do Azure.</span><span class="sxs-lookup"><span data-stu-id="7533d-104">This PowerShell script example configures active geo-replication for an Azure SQL database in an elastic pool and fails it over toohello secondary replica of hello Azure SQL database.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-scripts"></a><span data-ttu-id="7533d-105">Scripts de exemplo</span><span class="sxs-lookup"><span data-stu-id="7533d-105">Sample scripts</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/setup-geodr-and-failover-pool/setup-geodr-and-failover-pool.ps1?highlight=16-19 "Set up active geo-replication for elastic pool")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7533d-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="7533d-106">Clean up deployment</span></span>

<span data-ttu-id="7533d-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="7533d-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myPrimaryResourceGroup"
Remove-AzureRmResourceGroup -ResourceGroupName "mySecondaryResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7533d-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="7533d-108">Script explanation</span></span>

<span data-ttu-id="7533d-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="7533d-109">This script uses hello following commands.</span></span> <span data-ttu-id="7533d-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="7533d-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7533d-111">Comando</span><span class="sxs-lookup"><span data-stu-id="7533d-111">Command</span></span> | <span data-ttu-id="7533d-112">Notas</span><span class="sxs-lookup"><span data-stu-id="7533d-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7533d-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7533d-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7533d-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7533d-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7533d-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7533d-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7533d-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="7533d-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="7533d-117">Novo-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="7533d-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="7533d-118">Cria um conjunto elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="7533d-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="7533d-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7533d-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="7533d-120">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="7533d-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="7533d-121">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7533d-121">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="7533d-122">Atualiza as propriedades de base de dados ou move de uma base de dados para fora do ou entre conjuntos elásticos.</span><span class="sxs-lookup"><span data-stu-id="7533d-122">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="7533d-123">Novo AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="7533d-123">New-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary)| <span data-ttu-id="7533d-124">Cria uma base de dados secundária para uma base de dados existente e começa a replicação de dados.</span><span class="sxs-lookup"><span data-stu-id="7533d-124">Creates a secondary database for an existing database and starts data replication.</span></span> |
| [<span data-ttu-id="7533d-125">Get-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7533d-125">Get-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabase)| <span data-ttu-id="7533d-126">Obtém um ou mais bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7533d-126">Gets one or more databases.</span></span> |
| [<span data-ttu-id="7533d-127">Conjunto AzureRmSqlDatabaseSecondary</span><span class="sxs-lookup"><span data-stu-id="7533d-127">Set-AzureRmSqlDatabaseSecondary</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary)| <span data-ttu-id="7533d-128">Muda um site primário toobe base de dados secundária na ativação pós-falha tooinitiate de ordem.</span><span class="sxs-lookup"><span data-stu-id="7533d-128">Switches a secondary database toobe primary in order tooinitiate failover.</span></span>|
| [<span data-ttu-id="7533d-129">Get-AzureRmSqlDatabaseReplicationLink</span><span class="sxs-lookup"><span data-stu-id="7533d-129">Get-AzureRmSqlDatabaseReplicationLink</span></span>](/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) | <span data-ttu-id="7533d-130">Obtém as ligações de georreplicação Olá entre uma base de dados do SQL do Azure e um grupo de recursos ou do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7533d-130">Gets hello geo-replication links between an Azure SQL Database and a resource group or SQL Server.</span></span> |
| [<span data-ttu-id="7533d-131">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7533d-131">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7533d-132">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7533d-132">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7533d-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7533d-133">Next steps</span></span>

<span data-ttu-id="7533d-134">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7533d-134">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7533d-135">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7533d-135">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
