---
title: "aaaPowerShell exemplo monitor-escala SQL elásticas conjunto Azure base de dados SQL | Microsoft Docs"
description: "Toomonitor de script de exemplo do PowerShell do Azure e o dimensionamento um agrupamento elástico de SQL no SQL Database do Azure"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: PowerShell
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 149a45174ccb8072ea21753364196c7f98fd4101
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-sql-elastic-pool-in-azure-sql-database"></a><span data-ttu-id="4b40f-103">Utilize o PowerShell toomonitor e dimensionar um agrupamento elástico de SQL no SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="4b40f-103">Use PowerShell toomonitor and scale a SQL elastic pool in Azure SQL Database</span></span>

<span data-ttu-id="4b40f-104">Neste exemplo de script do PowerShell monitores Olá métricas de desempenho de um conjunto elástico, dimensiona este nível de desempenho superior tooa e cria uma regra de alerta num Olá métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="4b40f-104">This PowerShell script example monitors hello performance metrics of an elastic pool, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="4b40f-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4b40f-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-pool/monitor-and-scale-pool.ps1?highlight=16-17 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="4b40f-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="4b40f-106">Clean up deployment</span></span>

<span data-ttu-id="4b40f-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="4b40f-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="4b40f-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="4b40f-108">Script explanation</span></span>

<span data-ttu-id="4b40f-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="4b40f-109">This script uses hello following commands.</span></span> <span data-ttu-id="4b40f-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="4b40f-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4b40f-111">Comando</span><span class="sxs-lookup"><span data-stu-id="4b40f-111">Command</span></span> | <span data-ttu-id="4b40f-112">Notas</span><span class="sxs-lookup"><span data-stu-id="4b40f-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="4b40f-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b40f-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="4b40f-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="4b40f-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b40f-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="4b40f-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="4b40f-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="4b40f-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="4b40f-117">Novo-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="4b40f-117">New-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) | <span data-ttu-id="4b40f-118">Cria um conjunto elástico dentro de um servidor lógico.</span><span class="sxs-lookup"><span data-stu-id="4b40f-118">Creates an elastic pool within a logical server.</span></span> |
| [<span data-ttu-id="4b40f-119">New-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="4b40f-119">New-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/new-azurermsqldatabase) | <span data-ttu-id="4b40f-120">Cria uma base de dados de um servidor lógico como um único ou uma base de dados agrupado.</span><span class="sxs-lookup"><span data-stu-id="4b40f-120">Creates a database in a logical server as a single or a pooled database.</span></span> |
| [<span data-ttu-id="4b40f-121">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="4b40f-121">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="4b40f-122">Mostra informações de utilização do Olá tamanho da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="4b40f-122">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="4b40f-123">AzureRMMetricAlertRule adicionar</span><span class="sxs-lookup"><span data-stu-id="4b40f-123">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="4b40f-124">Adiciona ou atualiza uma regra de alerta baseada em métrica.</span><span class="sxs-lookup"><span data-stu-id="4b40f-124">Adds or updates a metric-based alert rule.</span></span> |
| [<span data-ttu-id="4b40f-125">Set-AzureRmSqlElasticPool</span><span class="sxs-lookup"><span data-stu-id="4b40f-125">Set-AzureRmSqlElasticPool</span></span>](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) | <span data-ttu-id="4b40f-126">Atualiza as propriedades do conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="4b40f-126">Updates elastic pool properties</span></span> |
| [<span data-ttu-id="4b40f-127">AzureRMMetricAlertRule adicionar</span><span class="sxs-lookup"><span data-stu-id="4b40f-127">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="4b40f-128">Define uma regra de alerta de monitor de tooautomatically DTUs Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="4b40f-128">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="4b40f-129">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="4b40f-129">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="4b40f-130">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="4b40f-130">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="4b40f-131">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4b40f-131">Next steps</span></span>

<span data-ttu-id="4b40f-132">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4b40f-132">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4b40f-133">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="4b40f-133">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
