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
# <a name="create-and-manage-an-elastic-pool-with-powershell"></a>Criar e gerir um conjunto elástico com o PowerShell
Este tópico mostra como toocreate e gerir dimensionável [conjuntos elásticos](sql-database-elastic-pool.md) com o PowerShell.  Também pode criar e gerir um conjunto elástico do Azure utilizando Olá [portal do Azure](https://portal.azure.com/), REST API, ou [c#](sql-database-elastic-pool-manage-csharp.md). Também pode criar e mover bases de dados para dentro e fora conjuntos elásticos utilizando [Transact-SQL](sql-database-elastic-pool-manage-tsql.md).

[!INCLUDE [Start your PowerShell session](../../includes/sql-database-powershell.md)]

## <a name="create-an-elastic-pool"></a>Criar um conjunto elástico
Olá [New-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/new-azurermsqlelasticpool) cmdlet cria um conjunto elástico. Olá os valores de eDTU por conjunto, min e max DTUs estão restritos pelo valor da camada de serviço Olá (básica, Standard, Premium ou Premium RS). Consulte [eDTU e limites de armazenamento para conjuntos elásticos e bases de dados agrupados](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools).

```PowerShell
New-AzureRmSqlElasticPool -ResourceGroupName "resourcegroup1" -ServerName "server1" -ElasticPoolName "elasticpool1" -Edition "Standard" -Dtu 400 -DatabaseDtuMin 10 -DatabaseDtuMax 100
```

## <a name="create-a-pooled-database-in-an-elastic-pool"></a>Criar uma base de dados agrupado num agrupamento elástico
Olá utilize [New-AzureRmSqlDatabase](/powershell/module/azurerm.sql/new-azurermsqldatabase) cmdlet e conjunto Olá **ElasticPoolName** agrupamento de destino do parâmetro toohello. toomove uma base de dados existente para um conjunto elástico, consulte [mover uma base de dados para um conjunto elástico](sql-database-elastic-pool-manage-powershell.md#move-a-database-into-an-elastic-pool).

```PowerShell
New-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

### <a name="complete-script"></a>Script completo
Este script cria um grupo de recursos do Azure e um servidor. Quando lhe for solicitado, forneça um nome de utilizador administrador e a palavra-passe para o novo servidor de Olá (não as credenciais do Azure).

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

## <a name="create-an-elastic-pool-and-add-multiple-pooled-databases"></a>Criar um conjunto elástico e adicionar várias bases de dados agrupados
Criação de muitas bases de dados num agrupamento elástico pode demorar concluída ao utilizar o portal de Olá ou cmdlets do PowerShell que criam apenas uma única base de dados de cada vez. criação de tooautomate para um conjunto elástico, consulte [CreateOrUpdateElasticPoolAndPopulate ](https://gist.github.com/billgib/d80c7687b17355d3c2ec8042323819ae).

## <a name="move-a-database-into-an-elastic-pool"></a>Mover uma base de dados para um conjunto elástico
Pode mover uma base de dados ou a sair de um agrupamento elástico com Olá [Set-AzureRmSqlDatabase](/powershell/module/azurerm.sql/set-azurermsqlelasticpool).

```PowerShell
Set-AzureRmSqlDatabase -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="change-performance-settings-of-an-elastic-pool"></a>Alterar as definições de desempenho de um conjunto elástico
Quando o desempenho diminuirá, pode alterar as definições de Olá de crescimento de tooaccommodate Olá agrupamento. Olá utilize [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet. Definir Olá - Dtu parâmetro toohello eDTUs por conjunto. Consulte [eDTU e limites de armazenamento](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para os valores possíveis.

```PowerShell
Set-AzureRmSqlElasticPool -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1” -Dtu 1200 -DatabaseDtuMax 100 -DatabaseDtuMin 50
```

## <a name="change-hello-storage-limit-for-an-elastic-pool"></a>Alterar o limite de armazenamento Olá de um conjunto elástico

Olá utilize [Set-AzureRmSqlElasticPool](/powershell/module/azurerm.sql/set-azurermsqlelasticpool) cmdlet tooset Olá _- StorageMB_ parâmetro. Forneça o limite de armazenamento Olá em MB (por exemplo, 2097152 conjuntos Olá armazenamento limite too2 TB). Consulte [eDTU e limites de armazenamento](sql-database-elastic-pool.md#edtu-and-storage-limits-for-elastic-pools) para os valores possíveis.

> [!IMPORTANT]
> armazenamento de dados máximo predefinido Olá por agrupamento para conjuntos de Premium com 1500 eDTUs ou mais são 750 GB. Olá tooobtain superior _máximo de tamanho de armazenamento de dados por conjunto_, limite de armazenamento Olá tem de ser explicitamente definido. Conjuntos de Premium com mais de 750 GB de armazenamento está atualmente em pré-visualização pública Olá seguintes regiões: EUA Leste 2, EUA oeste, EUA us Virginia, Europa Ocidental, Alemanha Central, Sudeste asiático, leste do Japão, leste da Austrália, Canadá Central e Canadá Leste.

```PowerShell
Set-AzureRmSqlElasticPool -ServerName "server1" -ElasticPoolName “elasticpool1” -StorageMB 2097152
```

## <a name="get-hello-status-of-pool-operations"></a>Obter o estado de Olá das operações de conjunto
Criar um conjunto elástico, pode demorar um tempo. Estado de Olá tootrack de operações do conjunto, incluindo a criação e atualizações, utilize Olá [Get-AzureRmSqlElasticPoolActivity](/powershell/module/azurerm.sql/get-azurermsqlelasticpoolactivity) cmdlet.

```PowerShell
Get-AzureRmSqlElasticPoolActivity -ResourceGroupName “resourcegroup1” -ServerName “server1” -ElasticPoolName “elasticpool1”
```

## <a name="get-hello-status-of-moving-a-database-into-and-out-of-an-elastic-pool"></a>Obter o estado de Olá de mover uma base de dados dentro e fora de um conjunto elástico
Mover uma base de dados pode demorar tempo. Monitorizar um Estado de movimentação utilizando Olá [Get-AzureRmSqlDatabaseActivity](/powershell/module/azurerm.sql/get-azurermsqldatabaseactivity) cmdlet.

```PowerShell
Get-AzureRmSqlDatabaseActivity -ResourceGroupName "resourcegroup1" -ServerName "server1" -DatabaseName "database1" -ElasticPoolName "elasticpool1"
```

## <a name="get-resource-usage-data-for-an-elastic-pool"></a>Obter dados de utilização de recursos de um conjunto elástico
Métricas que podem ser obtidas como uma percentagem do limite do conjunto de recursos de Olá:

| Nome da métrica | Descrição |
|:--- |:--- |
| CPU\_por cento |Média de utilização na percentagem de limite de Olá do conjunto de Olá computação. |
| físico\_dados\_ler\_por cento |Utilização de e/s média com base no limite de Olá do conjunto de Olá como percentagem. |
| registo\_escrever\_por cento |Média de escrita utilização de recursos como percentagem do limite de Olá do conjunto de Olá. |
| DTU\_consumo\_por cento |Utilização média da eDTU percentagem do limite de eDTU do conjunto de Olá |
| armazenamento\_por cento |Utilização do armazenamento médio percentagem do limite de armazenamento Olá do conjunto de Olá. |
| os funcionários\_por cento |Máximos simultâneas trabalhadores (pedidos) com base no limite de Olá do conjunto de Olá como percentagem. |
| sessões\_por cento |Máximo de sessões em simultâneo com base no limite de Olá do conjunto de Olá como percentagem. |
| eDTU_limit |Máximo do conjunto elástico DTU definição actual para este agrupamento elástico durante esse intervalo. |
| armazenamento\_limite |Limite de armazenamento do atual máximo do conjunto elástico definir para este conjunto elástico em megabytes durante este intervalo. |
| eDTU\_utilizado |EDTUs média utilizada pelo agrupamento de Olá neste intervalo. |
| armazenamento\_utilizado |Armazenamento média utilizado pelo agrupamento de Olá neste intervalo em bytes |

**Períodos de retenção/granularidade métricas:**

* Granularidade de 5 minutos, são devolvidos dados.  
* Retenção de dados é 35 dias.  

Esta API e o cmdlet limita o número de Olá de linhas que pode ser obtido no chamada too1000 linhas (cerca de 3 dias de dados granularidade de 5 minutos). Mas este comando pode ser chamado várias vezes com tooretrieve de intervalos de tempo de início/fim diferentes mais dados

métricas de Olá tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/elasticPools/franchisepool -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="get-resource-usage-data-for-a-database-in-an-elastic-pool"></a>Obter dados de utilização de recursos para uma base de dados num agrupamento elástico
Estas APIs são Olá igual ao hello APIs para monitorizar a utilização de recursos de Olá de uma base de dados, exceto Olá seguir diferença semântica: métricas obtidas são expresso como uma percentagem de Olá por eDTUs máximo da base de dados (ou equivalente extremidade para Olá subjacente métrica como CPU ou e/s) definido para o conjunto. Por exemplo, 50% de utilização de qualquer um destas métricas indica que o consumo de recursos específico de Olá em 50% do Olá por limite de extremidade de base de dados para esse recurso num conjunto de principais de Olá.

métricas de Olá tooretrieve:

```PowerShell
$metrics = (Get-AzureRmMetric -ResourceId /subscriptions/<subscriptionId>/resourceGroups/FabrikamData01/providers/Microsoft.Sql/servers/fabrikamsqldb02/databases/myDB -TimeGrain ([TimeSpan]::FromMinutes(5)) -StartTime "4/18/2015" -EndTime "4/21/2015")
```

## <a name="add-an-alert-tooan-elastic-pool-resource"></a>Adicione um recurso de conjunto elástico tooan alerta
Pode adicionar regras de alerta tooan conjunto elástico toosend notificações por correio eletrónico ou cadeias de alerta demasiado[pontos finais de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando o conjunto elástico Olá chega a um limiar de utilização que configurou. Utilize o cmdlet Olá AzureRmMetricAlertRule adicionar.

> [!IMPORTANT]
> Utilização de recursos de monitorização para conjuntos elásticos tem um atraso de, pelo menos, 5 minutos. Definir alertas de menos de 10 minutos para conjuntos elásticos não é atualmente suportado. Definir todos os alertas para conjuntos elásticos com um período (parâmetro denominado "-WindowSize" PowerShell API) de menos de 10 minutos não ser acionadas. Certifique-se de que todos os alertas define para conjuntos elásticos utilizam um período (WindowSize) de 10 minutos ou mais.
>
>

Este exemplo adiciona um alerta para ser notificado quando o consumo de eDTU do conjunto elástico ultrapassar determinado limiar.

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

Para obter mais informações, consulte [criam alertas de base de dados SQL no portal do Azure](sql-database-insights-alerts-portal.md).

## <a name="add-alerts-tooall-databases-in-an-elastic-pool"></a>Adicionar bases de dados de alertas tooall num agrupamento elástico
Pode adicionar regras de alerta tooall base de dados no toosend conjunto elástico notificações por correio eletrónico ou cadeias de alerta demasiado[pontos finais de URL](https://msdn.microsoft.com/library/mt718036.aspx) quando um recurso chega a um limiar de utilização configurar por alerta Olá.

> [!IMPORTANT]
> Utilização de recursos de monitorização para conjuntos elásticos tem um atraso de, pelo menos, 5 minutos. Definir alertas de menos de 10 minutos para conjuntos elásticos não é atualmente suportado. Definir todos os alertas para conjuntos elásticos com um período (parâmetro denominado "-WindowSize" PowerShell API) de menos de 10 minutos não ser acionadas. Certifique-se de que todos os alertas define para conjuntos elásticos utilizam um período (WindowSize) de 10 minutos ou mais.
>

Este exemplo adiciona um alerta tooeach das bases de dados de Olá num conjunto elástico para ser notificado quando o consumo de DTU essa base de dados for superior determinado limiar.

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

## <a name="collect-and-monitor-resource-usage-data-across-multiple-pools-in-a-subscription"></a>Recolher e monitorizar os dados de utilização de recursos entre vários conjuntos de uma subscrição
Quando tem muitas bases de dados numa subscrição, é complexa toomonitor cada elástico agrupamento em separado. Em vez disso, os cmdlets do PowerShell de base de dados SQL e consultas de T-SQL podem ser combinado toocollect dados de utilização de recursos de vários conjuntos e as respetivas bases de dados de monitorização e análise da utilização de recursos. A [implementação de exemplo](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools) do conjunto do powershell scripts podem ser encontrados no repositório de amostras Olá GitHub SQL Server juntamente com a documentação sobre o que faz e como toouse-lo.

toouse esta implementação de exemplo, siga estes passos.

1. Transferir Olá [scripts e documentação](https://github.com/Microsoft/sql-server-samples/tree/master/samples/manage/azure-sql-db-elastic-pools):
2. Modificar os scripts de Olá para o seu ambiente. Especifique um ou mais servidores em que estão alojados conjuntos elásticos.
3. Especifique uma base de dados de telemetria onde hello métricas recolhidas são toobe armazenado.
4. Personalize a duração do Olá script toospecify Olá da execução dos scripts de Olá.

Um nível elevado, scripts de Olá Olá seguintes:

* Enumera todos os servidores de uma determinada subscrição do Azure (ou uma lista especificada de servidores).
* Executa uma tarefa em segundo plano para cada servidor. tarefa de Olá é executado em ciclo em intervalos regulares e recolhe dados de telemetria para todos os conjuntos de Olá no servidor de Olá. Em seguida, carrega Olá recolhido dados na base de dados do Olá telemetria especificado.
* Apresenta uma lista de bases de dados em dados de utilização de recursos de base de dados cada agrupamento toocollect Olá. Em seguida, carrega Olá recolhido dados na base de dados de telemetria de Olá.

Olá métricas recolhidas na base de dados de telemetria de Olá podem ser analisado toomonitor Olá estado de funcionamento conjuntos elásticos e bases de dados de Olá no mesmo. script de Olá também instala uma função de valor de tabela (TVF) predefinida no Olá telemetria da base de dados toohelp Olá agregado as métricas para uma janela de tempo especificado. Por exemplo, os resultados de Olá TVF podem ser utilizados tooshow "principais N conjuntos elásticos com utilização de eDTU máxima Olá uma janela de tempo especificado." Opcionalmente, utilize ferramentas de análise, como o Excel ou do Power BI tooquery e analisar dados de Olá recolhido.

### <a name="example-retrieve-resource-consumption-metrics-for-an-elastic-pool-and-its-databases"></a>Exemplo: obter métricas do consumo de recursos para um conjunto elástico e respetivas bases de dados
Este exemplo apresenta métricas do consumo de Olá para um determinado conjunto elástico e todas as suas bases de dados. Os dados recolhidos são formatados e escritos tooa formatado. csv. ficheiro de Olá pode ser consultado com o Excel.

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

## <a name="latency-of-elastic-pool-operations"></a>Latência de operações do conjunto elástico
* Normalmente, a alteração Olá eDTUs de Mín por base de dados ou o número máximo de eDTUs por base de dados conclui em 5 minutos ou menos.
* Alterar Olá eDTUs por conjunto depende da quantidade total de Olá de espaço utilizado por todas as bases de dados no agrupamento de Olá. Alterações em média 90 minutos ou menos por 100 GB. Por exemplo, se espaço total Olá utilizado por todas as bases de dados no agrupamento de Olá é 200 GB, em seguida, Olá esperado de latência para alterar o conjunto de Olá eDTU por conjunto é 3 horas ou menos.



## <a name="next-steps"></a>Passos seguintes
* [Criar tarefas elásticas](sql-database-elastic-jobs-overview.md) as tarefas elásticas permitem executar scripts T-SQL em qualquer número de bases de dados no agrupamento de Olá.
* Consulte [aumentar horizontalmente com a SQL Database do Azure](sql-database-elastic-scale-introduction.md): Utilize ferramentas elásticas tooscale out, mover os dados, consulta ou criar transações.
