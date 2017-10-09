---
title: "a base de dados SQL do Azure de exemplo-monitor escala único aaaPowerShell | Microsoft Docs"
description: Toomonitor de script de exemplo do PowerShell do Azure e dimensionar uma base de dados SQL do Azure
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
ms.openlocfilehash: bd8f880fb47b1360ae4962d2b039faa742de258e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-toomonitor-and-scale-a-single-sql-database"></a><span data-ttu-id="7adc6-103">Utilize o PowerShell toomonitor e dimensionar uma base de dados SQL</span><span class="sxs-lookup"><span data-stu-id="7adc6-103">Use PowerShell toomonitor and scale a single SQL database</span></span>

<span data-ttu-id="7adc6-104">Neste exemplo de script do PowerShell monitores Olá métricas de desempenho da base de dados, dimensiona este nível de desempenho superior tooa e cria uma regra de alerta num Olá métricas de desempenho.</span><span class="sxs-lookup"><span data-stu-id="7adc6-104">This PowerShell script example monitors hello performance metrics of a database, scales it tooa higher performance level, and creates an alert rule on one of hello performance metrics.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

## <a name="sample-script"></a><span data-ttu-id="7adc6-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7adc6-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/sql-database/monitor-and-scale-database/monitor-and-scale-database.ps1?highlight=13-14 "Monitor and scale single SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7adc6-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="7adc6-106">Clean up deployment</span></span>

<span data-ttu-id="7adc6-107">Depois de executar o script de exemplo Olá, Olá seguir o comando pode ser grupo de recursos de Olá tooremove utilizado e todos os recursos associados à mesma.</span><span class="sxs-lookup"><span data-stu-id="7adc6-107">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```powershell
Remove-AzureRmResourceGroup -ResourceGroupName "myResourceGroup"
```

## <a name="script-explanation"></a><span data-ttu-id="7adc6-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="7adc6-108">Script explanation</span></span>

<span data-ttu-id="7adc6-109">Este script utiliza Olá os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="7adc6-109">This script uses hello following commands.</span></span> <span data-ttu-id="7adc6-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="7adc6-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7adc6-111">Comando</span><span class="sxs-lookup"><span data-stu-id="7adc6-111">Command</span></span> | <span data-ttu-id="7adc6-112">Notas</span><span class="sxs-lookup"><span data-stu-id="7adc6-112">Notes</span></span> |
|---|---|
 [<span data-ttu-id="7adc6-113">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7adc6-113">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="7adc6-114">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="7adc6-114">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="7adc6-115">Novo AzureRmSqlServer</span><span class="sxs-lookup"><span data-stu-id="7adc6-115">New-AzureRmSqlServer</span></span>](/powershell/module/azurerm.sql/new-azurermsqlserver) | <span data-ttu-id="7adc6-116">Cria um servidor lógico que aloja um agrupamento de base de dados ou elástico.</span><span class="sxs-lookup"><span data-stu-id="7adc6-116">Creates a logical server that hosts a database or elastic pool.</span></span> |
| [<span data-ttu-id="7adc6-117">Get-AzureRmMetric</span><span class="sxs-lookup"><span data-stu-id="7adc6-117">Get-AzureRmMetric</span></span>](/powershell/module/azurerm.insights/get-azurermmetric) | <span data-ttu-id="7adc6-118">Mostra informações de utilização do Olá tamanho da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="7adc6-118">Shows hello size usage information for hello database.</span></span>|
| [<span data-ttu-id="7adc6-119">Set-AzureRmSqlDatabase</span><span class="sxs-lookup"><span data-stu-id="7adc6-119">Set-AzureRmSqlDatabase</span></span>](/powershell/module/azurerm.sql/set-azurermsqldatabase) | <span data-ttu-id="7adc6-120">Atualiza as propriedades de base de dados ou move de uma base de dados para fora do ou entre conjuntos elásticos.</span><span class="sxs-lookup"><span data-stu-id="7adc6-120">Updates database properties or moves a database into, out of, or between elastic pools.</span></span> |
| [<span data-ttu-id="7adc6-121">AzureRMMetricAlertRule adicionar</span><span class="sxs-lookup"><span data-stu-id="7adc6-121">Add-AzureRMMetricAlertRule</span></span>](/powershell/module/azurerm.insights/add-azurermmetricalertrule) | <span data-ttu-id="7adc6-122">Define uma regra de alerta de monitor de tooautomatically DTUs Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="7adc6-122">Sets an alert rule tooautomatically monitor DTUs in hello future.</span></span> |
| [<span data-ttu-id="7adc6-123">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7adc6-123">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7adc6-124">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="7adc6-124">Deletes a resource group including all nested resources.</span></span> |
|||

## <a name="next-steps"></a><span data-ttu-id="7adc6-125">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7adc6-125">Next steps</span></span>

<span data-ttu-id="7adc6-126">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7adc6-126">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7adc6-127">Exemplos de script do PowerShell de base de dados do SQL adicionais podem ser encontrados na Olá [scripts do PowerShell de base de dados do SQL Azure](../sql-database-powershell-samples.md).</span><span class="sxs-lookup"><span data-stu-id="7adc6-127">Additional SQL Database PowerShell script samples can be found in hello [Azure SQL Database PowerShell scripts](../sql-database-powershell-samples.md).</span></span>
