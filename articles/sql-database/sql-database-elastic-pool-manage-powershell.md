---
title: "PowerShell: Criar e gerir um conjunto elástico de SQL do Azure | Microsoft Docs"
description: "Saiba como toouse PowerShell toomanage um conjunto elástico."
services: sql-database
documentationcenter: 
author: srinia
manager: jhubbard
editor: 
ms.assetid: 61289770-69b9-4ae3-9252-d0e94d709331
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: powershell
ms.workload: data-management
ms.date: 06/06/2017
ms.author: srinia
ms.openlocfilehash: 92de2a4b243dcc74502064e9d2c31682691753d5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a><span data-ttu-id="e2a87-103">Criar e gerir um conjunto elástico com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2a87-103">Create and manage an elastic pool with PowerShell</span></span>
<span data-ttu-id="e2a87-104">Este tópico mostra como toocreate e gerir dimensionável [conjuntos elásticos](sql-database-elastic-pool.md) com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="e2a87-104">This topic shows you how toocreate and manage scalable [elastic pools](sql-database-elastic-pool.md) with PowerShell.</span></span>  <span data-ttu-id="e2a87-105">Também pode criar e gerir um conjunto elástico do Azure utilizando Olá [portal do Azure](https://portal.azure.com/), REST API, ou [c#](sql-database-elastic-pool-manage-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="e2a87-105">You can also create and manage an Azure elastic pool using hello [Azure portal](https://portal.azure.com/), REST API, or [C#](sql-database-elastic-pool-manage-csharp.md).</span></span> <span data-ttu-id="e2a87-106">Também pode criar e mover bases de dados para dentro e fora conjuntos elásticos utilizando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span><span class="sxs-lookup"><span data-stu-id="e2a87-106">You can also create and move databases into and out of elastic pools using [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).</span></span>

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a><span data-ttu-id="e2a87-107">Criar um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-107">Create an elastic pool</span></span>
<span data-ttu-id="e2a87-108">Olá [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet cria um conjunto elástico.</span><span class="sxs-lookup"><span data-stu-id="e2a87-108">hello [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet creates an elastic pool.</span></span> <span data-ttu-id="e2a87-109">Olá os valores de eDTU por conjunto, min e max DTUs estão restritos pelo valor da camada de serviço Olá (básica, Standard, Premium ou Premium RS).</span><span class="sxs-lookup"><span data-stu-id="e2a87-109">hello values for eDTU per pool, min, and max DTUs are constrained by hello service tier value (Basic, Standard, Premium, or Premium RS).</span></span> <span data-ttu-id="e2a87-110">Consulte [eDTU e limites de armazenamento para conjuntos elásticos e bases de dados agrupados](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span><span class="sxs-lookup"><span data-stu-id="e2a87-110">See [eDTU and storage limits for elastic pools and pooled databases](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).</span></span>

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a><span data-ttu-id="e2a87-111">Criar uma base de dados agrupado num agrupamento elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-111">Create a pooled database in an elastic pool</span></span>
<span data-ttu-id="e2a87-112">Olá utilize [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e conjunto Olá **ElasticPoolName** agrupamento de destino do parâmetro toohello.</span><span class="sxs-lookup"><span data-stu-id="e2a87-112">Use hello [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet and set hello **ElasticPoolName** parameter toohello target pool.</span></span> <span data-ttu-id="e2a87-113">toomove uma base de dados existente para um conjunto elástico, consulte [mover uma base de dados para um conjunto elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span><span class="sxs-lookup"><span data-stu-id="e2a87-113">toomove an existing database into an elastic pool, see [Move a database into an elastic pool](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).</span></span>

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a><span data-ttu-id="e2a87-114">Script completo</span><span class="sxs-lookup"><span data-stu-id="e2a87-114">Complete script</span></span>
<span data-ttu-id="e2a87-115">Este script cria um grupo de recursos do Azure e um servidor.</span><span class="sxs-lookup"><span data-stu-id="e2a87-115">This script creates an Azure resource group and a server.</span></span> <span data-ttu-id="e2a87-116">Quando lhe for solicitado, forneça um nome de utilizador administrador e a palavra-passe para o novo servidor de Olá (não as credenciais do Azure).</span><span class="sxs-lookup"><span data-stu-id="e2a87-116">When prompted, supply an administrator username and password for hello new server (not your Azure credentials).</span></span>

```PowerShell
$subscriptionId = '<your Azure subscription id>'
$resourceGroupName = '<resource group name>'
$location = '<datacenter location>'
$serverName = '<server name>'
$poolName = '<pool name>'
$databaseName = '<database name>'

Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
New-AzureRmSqlServer -ResourceGroupName $resourceGroupName -ServerName $serverName -Location $location -ServerVersion "12.0"
New-AzureRmSqlServerFirewallRule -ResourceGroupName $resourceGroupName -ServerName $serverName -FirewallRuleName "rule1" -StartIpAddress "192.168.0.198" -EndIpAddress "192.168.0.199"

New-AzureRmSqlElasticPool -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100

New-AzureRmSqlDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -DatabaseName $databaseName -ElasticPoolName $poolName -MaxSizeBytes 10GB
```

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a><span data-ttu-id="e2a87-117">Criar um conjunto elástico e adicionar várias bases de dados agrupados</span><span class="sxs-lookup"><span data-stu-id="e2a87-117">Create an elastic pool and add multiple pooled databases</span></span>
<span data-ttu-id="e2a87-118">Criação de muitas bases de dados num agrupamento elástico pode demorar concluída ao utilizar o portal de Olá ou cmdlets do PowerShell que criam apenas uma única base de dados de cada vez.</span><span class="sxs-lookup"><span data-stu-id="e2a87-118">Creation of many databases in an elastic pool can take time when done using hello portal or PowerShell cmdlets that create only a single database at a time.</span></span> <span data-ttu-id="e2a87-119">criação de tooautomate para um conjunto elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span><span class="sxs-lookup"><span data-stu-id="e2a87-119">tooautomate creation into an elastic pool, see [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).</span></span>

## <a name="move-a-database-into-an-elastic-pool"></a><span data-ttu-id="e2a87-120">Mover uma base de dados para um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-120">Move a database into an elastic pool</span></span>
<span data-ttu-id="e2a87-121">Pode mover uma base de dados ou a sair de um agrupamento elástico com Olá [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span><span class="sxs-lookup"><span data-stu-id="e2a87-121">You can move a database into or out of an elastic pool with hello [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).</span></span>

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a><span data-ttu-id="e2a87-122">Alterar as definições de desempenho de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-122">Change performance settings of an elastic pool</span></span>
<span data-ttu-id="e2a87-123">Quando o desempenho diminuirá, pode alterar as definições de Olá de crescimento de tooaccommodate Olá agrupamento.</span><span class="sxs-lookup"><span data-stu-id="e2a87-123">When performance suffers, you can change hello settings of hello pool tooaccommodate growth.</span></span> <span data-ttu-id="e2a87-124">Olá utilize [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2a87-124">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet.</span></span> <span data-ttu-id="e2a87-125">Definir Olá - Dtu parâmetro toohello eDTUs por conjunto.</span><span class="sxs-lookup"><span data-stu-id="e2a87-125">Set hello -Dtu parameter toohello eDTUs per pool.</span></span> <span data-ttu-id="e2a87-126">Consulte [eDTU e limites de armazenamento](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para os valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="e2a87-126">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a><span data-ttu-id="e2a87-127">Alterar o limite de armazenamento Olá de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-127">Change hello storage limit for an elastic pool</span></span>

<span data-ttu-id="e2a87-128">Olá utilize [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset Olá _- StorageMB_ parâmetro.</span><span class="sxs-lookup"><span data-stu-id="e2a87-128">Use hello [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset hello _-StorageMB_ parameter.</span></span> <span data-ttu-id="e2a87-129">Forneça o limite de armazenamento Olá em MB (por exemplo, 2097152 conjuntos Olá armazenamento limite too2 TB).</span><span class="sxs-lookup"><span data-stu-id="e2a87-129">Provide hello storage limit in MB (for example, 2097152 sets hello storage limit too2 TB).</span></span> <span data-ttu-id="e2a87-130">Consulte [eDTU e limites de armazenamento](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para os valores possíveis.</span><span class="sxs-lookup"><span data-stu-id="e2a87-130">See [eDTU and storage limits](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) for possible values.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2a87-131">armazenamento de dados máximo predefinido Olá por agrupamento para conjuntos de Premium com 1500 eDTUs ou mais são 750 GB.</span><span class="sxs-lookup"><span data-stu-id="e2a87-131">hello default max data storage per pool for Premium pools with 1500 eDTUs or more is 750 GB.</span></span> <span data-ttu-id="e2a87-132">Olá tooobtain superior _máximo de tamanho de armazenamento de dados por conjunto_, limite de armazenamento Olá tem de ser explicitamente definido.</span><span class="sxs-lookup"><span data-stu-id="e2a87-132">tooobtain hello higher _max data storage size per pool_, hello storage limit must be explicitly set.</span></span> <span data-ttu-id="e2a87-133">Conjuntos de Premium com mais de 750 GB de armazenamento está atualmente em pré-visualização pública Olá seguintes regiões: EUA Leste 2, EUA oeste, EUA us Virginia, Europa Ocidental, Alemanha Central, Sudeste asiático, leste do Japão, leste da Austrália, Canadá Central e Canadá Leste.</span><span class="sxs-lookup"><span data-stu-id="e2a87-133">Premium pools with more than 750 GB of storage is currently in public preview in hello following regions: East US 2, West US, US Gov Virginia, West Europe, Germany Central, Southeast Asia, Japan East, Australia East, Canada Central, and Canada East.</span></span>

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a><span data-ttu-id="e2a87-134">Obter o estado de Olá das operações de conjunto</span><span class="sxs-lookup"><span data-stu-id="e2a87-134">Get hello status of pool operations</span></span>
<span data-ttu-id="e2a87-135">Criar um conjunto elástico, pode demorar um tempo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-135">Creating an elastic pool can take time.</span></span> <span data-ttu-id="e2a87-136">Estado de Olá tootrack de operações do conjunto, incluindo a criação e atualizações, utilize Olá [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2a87-136">tootrack hello status of pool operations including creation and updates, use hello [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a><span data-ttu-id="e2a87-137">Obter o estado de Olá de mover uma base de dados dentro e fora de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-137">Get hello status of moving a database into and out of an elastic pool</span></span>
<span data-ttu-id="e2a87-138">Mover uma base de dados pode demorar tempo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-138">Moving a database can take time.</span></span> <span data-ttu-id="e2a87-139">Monitorizar um Estado de movimentação utilizando Olá [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="e2a87-139">Track a move status using hello [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.</span></span>

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a><span data-ttu-id="e2a87-140">Obter dados de utilização de recursos de um conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-140">Get resource usage data for an elastic pool</span></span>
<span data-ttu-id="e2a87-141">Métricas que podem ser obtidas como uma percentagem do limite do conjunto de recursos de Olá:</span><span class="sxs-lookup"><span data-stu-id="e2a87-141">Metrics that can be retrieved as a percentage of hello resource pool limit:</span></span>

| <span data-ttu-id="e2a87-142">Nome da métrica</span><span class="sxs-lookup"><span data-stu-id="e2a87-142">Metric name</span></span> | <span data-ttu-id="e2a87-143">Descrição</span><span class="sxs-lookup"><span data-stu-id="e2a87-143">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="e2a87-144">CPU\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-144">cpu\_percent</span></span> |<span data-ttu-id="e2a87-145">Média de utilização na percentagem de limite de Olá do conjunto de Olá computação.</span><span class="sxs-lookup"><span data-stu-id="e2a87-145">Average compute utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-146">físico\_dados\_ler\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-146">physical\_data\_read\_percent</span></span> |<span data-ttu-id="e2a87-147">Utilização de e/s média com base no limite de Olá do conjunto de Olá como percentagem.</span><span class="sxs-lookup"><span data-stu-id="e2a87-147">Average I/O utilization in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-148">registo\_escrever\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-148">log\_write\_percent</span></span> |<span data-ttu-id="e2a87-149">Média de escrita utilização de recursos como percentagem do limite de Olá do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-149">Average write resource utilization in percentage of hello limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-150">DTU\_consumo\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-150">DTU\_consumption\_percent</span></span> |<span data-ttu-id="e2a87-151">Utilização média da eDTU percentagem do limite de eDTU do conjunto de Olá</span><span class="sxs-lookup"><span data-stu-id="e2a87-151">Average eDTU utilization in percentage of eDTU limit for hello pool</span></span> |
| <span data-ttu-id="e2a87-152">armazenamento\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-152">storage\_percent</span></span> |<span data-ttu-id="e2a87-153">Utilização do armazenamento médio percentagem do limite de armazenamento Olá do conjunto de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-153">Average storage utilization in percentage of hello storage limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-154">os funcionários\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-154">workers\_percent</span></span> |<span data-ttu-id="e2a87-155">Máximos simultâneas trabalhadores (pedidos) com base no limite de Olá do conjunto de Olá como percentagem.</span><span class="sxs-lookup"><span data-stu-id="e2a87-155">Maximum concurrent workers (requests) in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-156">sessões\_por cento</span><span class="sxs-lookup"><span data-stu-id="e2a87-156">sessions\_percent</span></span> |<span data-ttu-id="e2a87-157">Máximo de sessões em simultâneo com base no limite de Olá do conjunto de Olá como percentagem.</span><span class="sxs-lookup"><span data-stu-id="e2a87-157">Maximum concurrent sessions in percentage based on hello limit of hello pool.</span></span> |
| <span data-ttu-id="e2a87-158">eDTU_limit</span><span class="sxs-lookup"><span data-stu-id="e2a87-158">eDTU_limit</span></span> |<span data-ttu-id="e2a87-159">Máximo do conjunto elástico DTU definição actual para este agrupamento elástico durante esse intervalo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-159">Current max elastic pool DTU setting for this elastic pool during this interval.</span></span> |
| <span data-ttu-id="e2a87-160">armazenamento\_limite</span><span class="sxs-lookup"><span data-stu-id="e2a87-160">storage\_limit</span></span> |<span data-ttu-id="e2a87-161">Limite de armazenamento do atual máximo do conjunto elástico definir para este conjunto elástico em megabytes durante este intervalo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-161">Current max elastic pool storage limit setting for this elastic pool in megabytes during this interval.</span></span> |
| <span data-ttu-id="e2a87-162">eDTU\_utilizado</span><span class="sxs-lookup"><span data-stu-id="e2a87-162">eDTU\_used</span></span> |<span data-ttu-id="e2a87-163">EDTUs média utilizada pelo agrupamento de Olá neste intervalo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-163">Average eDTUs used by hello pool in this interval.</span></span> |
| <span data-ttu-id="e2a87-164">armazenamento\_utilizado</span><span class="sxs-lookup"><span data-stu-id="e2a87-164">storage\_used</span></span> |<span data-ttu-id="e2a87-165">Armazenamento média utilizado pelo agrupamento de Olá neste intervalo em bytes</span><span class="sxs-lookup"><span data-stu-id="e2a87-165">Average storage used by hello pool in this interval in bytes</span></span> |

<span data-ttu-id="e2a87-166">**Períodos de retenção/granularidade métricas:**</span><span class="sxs-lookup"><span data-stu-id="e2a87-166">**Metrics granularity/retention periods:**</span></span>

* <span data-ttu-id="e2a87-167">Granularidade de 5 minutos, são devolvidos dados.</span><span class="sxs-lookup"><span data-stu-id="e2a87-167">Data is returned at 5-minute granularity.</span></span>  
* <span data-ttu-id="e2a87-168">Retenção de dados é 35 dias.</span><span class="sxs-lookup"><span data-stu-id="e2a87-168">Data retention is 35 days.</span></span>  

<span data-ttu-id="e2a87-169">Esta API e o cmdlet limita o número de Olá de linhas que pode ser obtido no chamada too1000 linhas (cerca de 3 dias de dados granularidade de 5 minutos).</span><span class="sxs-lookup"><span data-stu-id="e2a87-169">This cmdlet and API limits hello number of rows that can be retrieved in one call too1000 rows (about 3 days of data at 5-minute granularity).</span></span> <span data-ttu-id="e2a87-170">Mas este comando pode ser chamado várias vezes com tooretrieve de intervalos de tempo de início/fim diferentes mais dados</span><span class="sxs-lookup"><span data-stu-id="e2a87-170">But this command can be called multiple times with different start/end time intervals tooretrieve more data</span></span>

<span data-ttu-id="e2a87-171">métricas de Olá tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="e2a87-171">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a><span data-ttu-id="e2a87-172">Obter dados de utilização de recursos para uma base de dados num agrupamento elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-172">Get resource usage data for a database in an elastic pool</span></span>
<span data-ttu-id="e2a87-173">Estas APIs são Olá igual ao hello APIs para monitorizar a utilização de recursos de Olá de uma base de dados, exceto Olá seguir diferença semântica: métricas obtidas são expresso como uma percentagem de Olá por eDTUs máximo da base de dados (ou equivalente extremidade para Olá subjacente métrica como CPU ou e/s) definido para o conjunto.</span><span class="sxs-lookup"><span data-stu-id="e2a87-173">These APIs are hello same as hello APIs used for monitoring hello resource utilization of a single database, except for hello following semantic difference: metrics retrieved are expressed as a percentage of hello per database max eDTUs (or equivalent cap for hello underlying metric like CPU or IO) set for that pool.</span></span> <span data-ttu-id="e2a87-174">Por exemplo, 50% de utilização de qualquer um destas métricas indica que o consumo de recursos específico de Olá em 50% do Olá por limite de extremidade de base de dados para esse recurso num conjunto de principais de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-174">For example, 50% utilization of any of these metrics indicates that hello specific resource consumption is at 50% of hello per database cap limit for that resource in hello parent pool.</span></span>

<span data-ttu-id="e2a87-175">métricas de Olá tooretrieve:</span><span class="sxs-lookup"><span data-stu-id="e2a87-175">tooretrieve hello metrics:</span></span>

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a><span data-ttu-id="e2a87-176">Adicione um recurso de conjunto elástico tooan alerta</span><span class="sxs-lookup"><span data-stu-id="e2a87-176">Add an alert tooan elastic pool resource</span></span>
<span data-ttu-id="e2a87-177">Pode adicionar regras de alerta tooan conjunto elástico toosend notificações por correio eletrónico ou cadeias de alerta demasiado[pontos finais de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando o conjunto elástico Olá chega a um limiar de utilização que configurou.</span><span class="sxs-lookup"><span data-stu-id="e2a87-177">You can add alert rules tooan elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when hello elastic pool hits a utilization threshold that you set up.</span></span> <span data-ttu-id="e2a87-178">Utilize o cmdlet Olá AzureRmMetricAlertRule adicionar.</span><span class="sxs-lookup"><span data-stu-id="e2a87-178">Use hello Add-AzureRmMetricAlertRule cmdlet.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2a87-179">Utilização de recursos de monitorização para conjuntos elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-179">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="e2a87-180">Definir alertas de menos de 10 minutos para conjuntos elásticos não é atualmente suportado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-180">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="e2a87-181">Definir todos os alertas para conjuntos elásticos com um período (parâmetro denominado "-WindowSize" PowerShell API) de menos de 10 minutos não ser acionadas.</span><span class="sxs-lookup"><span data-stu-id="e2a87-181">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="e2a87-182">Certifique-se de que todos os alertas define para conjuntos elásticos utilizam um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="e2a87-182">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>
>

<span data-ttu-id="e2a87-183">Este exemplo adiciona um alerta para ser notificado quando o consumo de eDTU do conjunto elástico ultrapassar determinado limiar.</span><span class="sxs-lookup"><span data-stu-id="e2a87-183">This example adds an alert for getting notified when an elastic pool’s eDTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location =  '<location'                         # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

#$Target Resource ID
$ResourceID = '/subscriptions/' + $subscriptionId + '/resourceGroups/' +$resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticpools/' + $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# create a unique rule name
$alertName = $poolName + "- DTU consumption rule"

# Create an alert rule for DTU_consumption_percent
Add-AzureRMMetricAlertRule -Name $alertName -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $ResourceID -MetricName "DTU_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail
```

<span data-ttu-id="e2a87-184">Para obter mais informações, consulte [criam alertas de base de dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).</span><span class="sxs-lookup"><span data-stu-id="e2a87-184">For more information, see [create SQL Database alerts in Azure portal](sql-database-insights-alerts-portal.md).</span></span>

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a><span data-ttu-id="e2a87-185">Adicionar bases de dados de alertas tooall num agrupamento elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-185">Add alerts tooall databases in an elastic pool</span></span>
<span data-ttu-id="e2a87-186">Pode adicionar regras de alerta tooall base de dados no toosend conjunto elástico notificações por correio eletrónico ou cadeias de alerta demasiado[pontos finais de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando um recurso chega a um limiar de utilização configurar por alerta Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-186">You can add alert rules tooall database in an elastic pool toosend email notifications or alert strings too[URL endpoints](https://msdn.microsoft.com/library/mt718036.aspx) when a resource hits a utilization threshold set up by hello alert.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="e2a87-187">Utilização de recursos de monitorização para conjuntos elásticos tem um atraso de, pelo menos, 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-187">Resource utilization monitoring for elastic pools has a lag of at least 5 minutes.</span></span> <span data-ttu-id="e2a87-188">Definir alertas de menos de 10 minutos para conjuntos elásticos não é atualmente suportado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-188">Setting alerts of less than 10 minutes for elastic pools is not currently supported.</span></span> <span data-ttu-id="e2a87-189">Definir todos os alertas para conjuntos elásticos com um período (parâmetro denominado "-WindowSize" PowerShell API) de menos de 10 minutos não ser acionadas.</span><span class="sxs-lookup"><span data-stu-id="e2a87-189">Any alerts set for elastic pools with a period (parameter called “-WindowSize” in PowerShell API) of less than 10 minutes may not be triggered.</span></span> <span data-ttu-id="e2a87-190">Certifique-se de que todos os alertas define para conjuntos elásticos utilizam um período (WindowSize) de 10 minutos ou mais.</span><span class="sxs-lookup"><span data-stu-id="e2a87-190">Make sure that any alerts you define for elastic pools use a period (WindowSize) of 10 minutes or more.</span></span>
>

<span data-ttu-id="e2a87-191">Este exemplo adiciona um alerta tooeach das bases de dados de Olá num conjunto elástico para ser notificado quando o consumo de DTU essa base de dados for superior determinado limiar.</span><span class="sxs-lookup"><span data-stu-id="e2a87-191">This example adds an alert tooeach of hello databases in an elastic pool for getting notified when that database’s DTU consumption goes above certain threshold.</span></span>

```PowerShell
# Set up your resource ID configurations
$subscriptionId = '<Azure subscription id>'      # Azure subscription ID
$location = '<location'                          # Azure region
$resourceGroupName = '<resource group name>'     # Resource Group
$serverName = '<server name>'                    # server name
$poolName = '<elastic pool name>'                # pool name

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Create an email action
$actionEmail = New-AzureRmAlertRuleEmail -SendToServiceOwners -CustomEmail JohnDoe@contoso.com

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
foreach ($db in $dbList)
{
    $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName

    # create a unique rule name
    $alertName = $db.DatabaseName + "- DTU consumption rule"

    # Create an alert rule for DTU_consumption_percent
    Add-AzureRMMetricAlertRule -Name $alertName  -Location $location -ResourceGroup $resourceGroupName -TargetResourceId $dbResourceId -MetricName "dtu_consumption_percent"  -Operator GreaterThan -Threshold 80 -TimeAggregationOperator Average -WindowSize 00:60:00 -Actions $actionEmail

    # drop hello alert rule
    #Remove-AzureRmAlertRule -ResourceGroup $resourceGroupName -Name $alertName
}
```

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a><span data-ttu-id="e2a87-192">Recolher e monitorizar os dados de utilização de recursos entre vários conjuntos de uma subscrição</span><span class="sxs-lookup"><span data-stu-id="e2a87-192">Collect and monitor resource usage data across multiple pools in a subscription</span></span>
<span data-ttu-id="e2a87-193">Quando tem muitas bases de dados numa subscrição, é complexa toomonitor cada elástico agrupamento em separado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-193">When you have many databases in a subscription, it is cumbersome toomonitor each elastic pool separately.</span></span> <span data-ttu-id="e2a87-194">Em vez disso, os cmdlets do PowerShell de base de dados SQL e consultas de T-SQL podem ser combinado toocollect dados de utilização de recursos de vários conjuntos e as respetivas bases de dados de monitorização e análise da utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-194">Instead, SQL database PowerShell cmdlets and T-SQL queries can be combined toocollect resource usage data from multiple pools and their databases for monitoring and analysis of resource usage.</span></span> <span data-ttu-id="e2a87-195">A [implementação de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) do conjunto do powershell scripts podem ser encontrados no repositório de amostras Olá GitHub SQL Server juntamente com a documentação sobre o que faz e como toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-195">A [sample implementation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) of such a set of powershell scripts can be found in hello GitHub SQL Server samples repository along with documentation on what it does and how toouse it.</span></span>

<span data-ttu-id="e2a87-196">toouse esta implementação de exemplo, siga estes passos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-196">toouse this sample implementation, follow these steps.</span></span>

1. <span data-ttu-id="e2a87-197">Transferir Olá [scripts e documentação](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span><span class="sxs-lookup"><span data-stu-id="e2a87-197">Download hello [scripts and documentation](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):</span></span>
2. <span data-ttu-id="e2a87-198">Modificar os scripts de Olá para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="e2a87-198">Modify hello scripts for your environment.</span></span> <span data-ttu-id="e2a87-199">Especifique um ou mais servidores em que estão alojados conjuntos elásticos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-199">Specify one or more servers on which elastic pools are hosted.</span></span>
3. <span data-ttu-id="e2a87-200">Especifique uma base de dados de telemetria onde hello métricas recolhidas são toobe armazenado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-200">Specify a telemetry database where hello collected metrics are toobe stored.</span></span>
4. <span data-ttu-id="e2a87-201">Personalize a duração do Olá script toospecify Olá da execução dos scripts de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-201">Customize hello script toospecify hello duration of hello scripts' execution.</span></span>

<span data-ttu-id="e2a87-202">Um nível elevado, scripts de Olá Olá seguintes:</span><span class="sxs-lookup"><span data-stu-id="e2a87-202">At a high level, hello scripts do hello following:</span></span>

* <span data-ttu-id="e2a87-203">Enumera todos os servidores de uma determinada subscrição do Azure (ou uma lista especificada de servidores).</span><span class="sxs-lookup"><span data-stu-id="e2a87-203">Enumerates all servers in a given Azure subscription (or a specified list of servers).</span></span>
* <span data-ttu-id="e2a87-204">Executa uma tarefa em segundo plano para cada servidor.</span><span class="sxs-lookup"><span data-stu-id="e2a87-204">Runs a background job for each server.</span></span> <span data-ttu-id="e2a87-205">tarefa de Olá é executado em ciclo em intervalos regulares e recolhe dados de telemetria para todos os conjuntos de Olá no servidor de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-205">hello job runs in a loop at regular intervals and collects telemetry data for all hello pools in hello server.</span></span> <span data-ttu-id="e2a87-206">Em seguida, carrega Olá recolhido dados na base de dados do Olá telemetria especificado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-206">It then loads hello collected data into hello specified telemetry database.</span></span>
* <span data-ttu-id="e2a87-207">Apresenta uma lista de bases de dados em dados de utilização de recursos de base de dados cada agrupamento toocollect Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-207">Enumerates a list of databases in each pool toocollect hello database resource usage data.</span></span> <span data-ttu-id="e2a87-208">Em seguida, carrega Olá recolhido dados na base de dados de telemetria de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-208">It then loads hello collected data into hello telemetry database.</span></span>

<span data-ttu-id="e2a87-209">Olá métricas recolhidas na base de dados de telemetria de Olá podem ser analisado toomonitor Olá estado de funcionamento conjuntos elásticos e bases de dados de Olá no mesmo.</span><span class="sxs-lookup"><span data-stu-id="e2a87-209">hello collected metrics in hello telemetry database can be analyzed toomonitor hello health of elastic pools and hello databases in it.</span></span> <span data-ttu-id="e2a87-210">script de Olá também instala uma função de valor de tabela (TVF) predefinida no Olá telemetria da base de dados toohelp Olá agregado as métricas para uma janela de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="e2a87-210">hello script also installs a pre-defined Table-Value function (TVF) in hello telemetry database toohelp aggregate hello metrics for a specified time window.</span></span> <span data-ttu-id="e2a87-211">Por exemplo, os resultados de Olá TVF podem ser utilizados tooshow "principais N conjuntos elásticos com utilização de eDTU máxima Olá uma janela de tempo especificado."</span><span class="sxs-lookup"><span data-stu-id="e2a87-211">For example, results of hello TVF can be used tooshow “top N elastic pools with hello maximum eDTU utilization in a given time window.”</span></span> <span data-ttu-id="e2a87-212">Opcionalmente, utilize ferramentas de análise, como o Excel ou do Power BI tooquery e analisar dados de Olá recolhido.</span><span class="sxs-lookup"><span data-stu-id="e2a87-212">Optionally, use analytic tools like Excel or Power BI tooquery and analyze hello collected data.</span></span>

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a><span data-ttu-id="e2a87-213">Exemplo: obter métricas do consumo de recursos para um conjunto elástico e respetivas bases de dados</span><span class="sxs-lookup"><span data-stu-id="e2a87-213">Example: retrieve resource consumption metrics for an elastic pool and its databases</span></span>
<span data-ttu-id="e2a87-214">Este exemplo apresenta métricas do consumo de Olá para um determinado conjunto elástico e todas as suas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="e2a87-214">This example retrieves hello consumption metrics for a given elastic pool and all its databases.</span></span> <span data-ttu-id="e2a87-215">Os dados recolhidos são formatados e escritos tooa formatado. csv.</span><span class="sxs-lookup"><span data-stu-id="e2a87-215">Collected data is formatted and written tooa .csv formatted file.</span></span> <span data-ttu-id="e2a87-216">ficheiro de Olá pode ser consultado com o Excel.</span><span class="sxs-lookup"><span data-stu-id="e2a87-216">hello file can be browsed with Excel.</span></span>

```PowerShell
$subscriptionId = '<Azure subscription id>'          # Azure subscription ID
$resourceGroupName = '<resource group name>'             # Resource Group
$serverName = <server name>                              # server name
$poolName = <elastic pool name>                          # pool name

# Login tooAzure account and select hello subscription.
Login-AzureRmAccount
Set-AzureRmContext -SubscriptionId $subscriptionId

# Get resource usage metrics for an elastic pool for hello specified time interval.
$startTime = '4/27/2016 00:00:00'  # start time in UTC
$endTime = '4/27/2016 01:00:00'    # end time in UTC

# Construct hello pool resource ID and retrive pool metrics at 5-minute granularity.
$poolResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/elasticPools/' + $poolName
$poolMetrics = (Get-AzureRmMetric -ResourceId $poolResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)

# Get hello list of databases in this pool.
$dbList = Get-AzureRmSqlElasticPoolDatabase -ResourceGroupName $resourceGroupName -ServerName $serverName -ElasticPoolName $poolName

# Get resource usage metrics for a database in an elastic pool for hello specified time interval.
$dbMetrics = @()
foreach ($db in $dbList)
{
     $dbResourceId = '/subscriptions/' + $subscriptionId + '/resourceGroups/' + $resourceGroupName + '/providers/Microsoft.Sql/servers/' + $serverName + '/databases/' + $db.DatabaseName
     $dbMetrics = $dbMetrics + (Get-AzureRmMetric -ResourceId $dbResourceId -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime $startTime -EndTime $endTime)
}

#Optionally you can format hello metrics and output as .csv file using hello following script block.
$command = {
param($metricList, $outputFile)

# Format metrics into a table.
$table = @()
foreach($metric in $metricList) {
   foreach($metricValue in $metric.MetricValues) {
      $sx = New-Object PSObject -Property @{
      Timestamp = $metricValue.Timestamp.ToString()
      MetricName = $metric.Name;
      Average = $metricValue.Average;
      ResourceID = $metric.ResourceId
   }$table = $table += $sx
   }
}

# Output hello metrics into a .csv file.
write-output $table | Export-csv -Path $outputFile -Append -NoTypeInformation
}

# Format and output pool metrics
Invoke-Command -ScriptBlock $command -ArgumentList $poolMetrics,c:\temp\poolmetrics.csv

# Format and output database metrics
Invoke-Command -ScriptBlock $command -ArgumentList $dbMetrics,c:\temp\dbmetrics.csv
```

## <a name="latency-of-elastic-pool-operations"></a><span data-ttu-id="e2a87-217">Latência de operações do conjunto elástico</span><span class="sxs-lookup"><span data-stu-id="e2a87-217">Latency of elastic pool operations</span></span>
* <span data-ttu-id="e2a87-218">Normalmente, a alteração Olá eDTUs de Mín por base de dados ou o número máximo de eDTUs por base de dados conclui em 5 minutos ou menos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-218">Changing hello min eDTUs per database or max eDTUs per database typically completes in 5 minutes or less.</span></span>
* <span data-ttu-id="e2a87-219">Alterar Olá eDTUs por conjunto depende da quantidade total de Olá de espaço utilizado por todas as bases de dados no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-219">Changing hello eDTUs per pool depends on hello total amount of space used by all databases in hello pool.</span></span> <span data-ttu-id="e2a87-220">Alterações em média 90 minutos ou menos por 100 GB.</span><span class="sxs-lookup"><span data-stu-id="e2a87-220">Changes average 90 minutes or less per 100 GB.</span></span> <span data-ttu-id="e2a87-221">Por exemplo, se espaço total Olá utilizado por todas as bases de dados no agrupamento de Olá é 200 GB, em seguida, Olá esperado de latência para alterar o conjunto de Olá eDTU por conjunto é 3 horas ou menos.</span><span class="sxs-lookup"><span data-stu-id="e2a87-221">For example, if hello total space used by all databases in hello pool is 200 GB, then hello expected latency for changing hello pool eDTU per pool is 3 hours or less.</span></span>



## <a name="next-steps"></a><span data-ttu-id="e2a87-222">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e2a87-222">Next steps</span></span>
* <span data-ttu-id="e2a87-223">[Criar tarefas elásticas](sql-database-elastic-jobs-overview.md) as tarefas elásticas permitem executar scripts T-SQL em qualquer número de bases de dados no agrupamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="e2a87-223">[Create elastic jobs](sql-database-elastic-jobs-overview.md) Elastic jobs let you run T-SQL scripts against any number of databases in hello pool.</span></span>
* <span data-ttu-id="e2a87-224">Consulte [aumentar horizontalmente com a SQL Database do Azure](sql-database-elastic-scale-introduction.md): Utilize ferramentas elásticas tooscale out, mover os dados, consulta ou criar transações.</span><span class="sxs-lookup"><span data-stu-id="e2a87-224">See [Scaling out with Azure SQL Database](sql-database-elastic-scale-introduction.md): use elastic tools tooscale out, move data, query, or create transactions.</span></span>
