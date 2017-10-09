---
title: aaaMonitor a carga de trabalho com DMVs | Microsoft Docs
description: Saiba como toomonitor a carga de trabalho com DMVs.
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 69ecd479-0941-48df-b3d0-cf54c79e6549
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 10/31/2016
ms.author: joeyong;barbkess
ms.openlocfilehash: acccf952d165ccec3de3b4b1c633b18bbbf78077
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-your-workload-using-dmvs"></a><span data-ttu-id="2a157-103">Monitorizar a carga de trabalho com DMVs</span><span class="sxs-lookup"><span data-stu-id="2a157-103">Monitor your workload using DMVs</span></span>
<span data-ttu-id="2a157-104">Este artigo descreve como toouse vistas de gestão dinâmica (DMVs) toomonitor a carga de trabalho e investigar a execução de consultas no armazém de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="2a157-104">This article describes how toouse Dynamic Management Views (DMVs) toomonitor your workload and investigate query execution in Azure SQL Data Warehouse.</span></span>

## <a name="permissions"></a><span data-ttu-id="2a157-105">Permissões</span><span class="sxs-lookup"><span data-stu-id="2a157-105">Permissions</span></span>
<span data-ttu-id="2a157-106">Olá tooquery DMVs neste artigo, necessita de permissão de vista de estado de base de dados ou controlo.</span><span class="sxs-lookup"><span data-stu-id="2a157-106">tooquery hello DMVs in this article, you need either VIEW DATABASE STATE or CONTROL permission.</span></span> <span data-ttu-id="2a157-107">Normalmente, conceder vista base de dados de estado é permissão Olá preferido é muito mais restritiva.</span><span class="sxs-lookup"><span data-stu-id="2a157-107">Usually granting VIEW DATABASE STATE is hello preferred permission as it is much more restrictive.</span></span>

```sql
GRANT VIEW DATABASE STATE toomyuser;
```

## <a name="monitor-connections"></a><span data-ttu-id="2a157-108">Ligações de monitor</span><span class="sxs-lookup"><span data-stu-id="2a157-108">Monitor connections</span></span>
<span data-ttu-id="2a157-109">Todos os inícios de sessão tooSQL do armazém de dados são registados demasiado[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span><span class="sxs-lookup"><span data-stu-id="2a157-109">All logins tooSQL Data Warehouse are logged too[sys.dm_pdw_exec_sessions][sys.dm_pdw_exec_sessions].</span></span>  <span data-ttu-id="2a157-110">Este DMV contém Olá últimos 10 000 inícios de sessão.</span><span class="sxs-lookup"><span data-stu-id="2a157-110">This DMV contains hello last 10,000 logins.</span></span>  <span data-ttu-id="2a157-111">Olá session_id é a chave primária Olá e tem atribuído sequencialmente para cada início de sessão de novo.</span><span class="sxs-lookup"><span data-stu-id="2a157-111">hello session_id is hello primary key and is assigned sequentially for each new logon.</span></span>

```sql
-- Other Active Connections
SELECT * FROM sys.dm_pdw_exec_sessions where status <> 'Closed' and session_id <> session_id();
```

## <a name="monitor-query-execution"></a><span data-ttu-id="2a157-112">Execução de consulta do monitor</span><span class="sxs-lookup"><span data-stu-id="2a157-112">Monitor query execution</span></span>
<span data-ttu-id="2a157-113">Todas as consultas executadas no armazém de dados do SQL Server são registadas demasiado[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span><span class="sxs-lookup"><span data-stu-id="2a157-113">All queries executed on SQL Data Warehouse are logged too[sys.dm_pdw_exec_requests][sys.dm_pdw_exec_requests].</span></span>  <span data-ttu-id="2a157-114">Este DMV contém Olá últimos 10 000 consultas executadas.</span><span class="sxs-lookup"><span data-stu-id="2a157-114">This DMV contains hello last 10,000 queries executed.</span></span>  <span data-ttu-id="2a157-115">Olá request_id exclusivamente identifica cada consulta e é Olá chave principal para este DMV.</span><span class="sxs-lookup"><span data-stu-id="2a157-115">hello request_id uniquely identifies each query and is hello primary key for this DMV.</span></span>  <span data-ttu-id="2a157-116">Olá request_id é atribuído sequencialmente para cada nova consulta e é o prefixo QID, que representa o ID de consulta.</span><span class="sxs-lookup"><span data-stu-id="2a157-116">hello request_id is assigned sequentially for each new query and is prefixed with QID, which stands for query ID.</span></span>  <span data-ttu-id="2a157-117">Consultar este DMV para um determinado session_id mostra todas as consultas para um início de sessão especificado.</span><span class="sxs-lookup"><span data-stu-id="2a157-117">Querying this DMV for a given session_id shows all queries for a given logon.</span></span>

> [!NOTE]
> <span data-ttu-id="2a157-118">Os procedimentos armazenados utilizam vários IDs de pedido.</span><span class="sxs-lookup"><span data-stu-id="2a157-118">Stored procedures use multiple Request IDs.</span></span>  <span data-ttu-id="2a157-119">Os IDs de pedido são atribuídos por ordem sequencial.</span><span class="sxs-lookup"><span data-stu-id="2a157-119">Request IDs are assigned in sequential order.</span></span> 
> 
> 

<span data-ttu-id="2a157-120">Seguem-se os planos de execução de consulta de tooinvestigate toofollow passos e as horas para uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="2a157-120">Here are steps toofollow tooinvestigate query execution plans and times for a particular query.</span></span>

### <a name="step-1-identify-hello-query-you-wish-tooinvestigate"></a><span data-ttu-id="2a157-121">PASSO 1: Identificar consulta Olá que desejar tooinvestigate</span><span class="sxs-lookup"><span data-stu-id="2a157-121">STEP 1: Identify hello query you wish tooinvestigate</span></span>
```sql
-- Monitor active queries
SELECT * 
FROM sys.dm_pdw_exec_requests 
WHERE status not in ('Completed','Failed','Cancelled')
  AND session_id <> session_id()
ORDER BY submit_time DESC;

-- Find top 10 queries longest running queries
SELECT TOP 10 * 
FROM sys.dm_pdw_exec_requests 
ORDER BY total_elapsed_time DESC;

-- Find a query with hello Label 'My Query'
-- Use brackets when querying hello label column, as it it a key word
SELECT  *
FROM    sys.dm_pdw_exec_requests
WHERE   [label] = 'My Query';
```

<span data-ttu-id="2a157-122">De Olá precedente os resultados da consulta, **Olá nota ID do pedido** da consulta Olá que gostaria de tooinvestigate.</span><span class="sxs-lookup"><span data-stu-id="2a157-122">From hello preceding query results, **note hello Request ID** of hello query that you would like tooinvestigate.</span></span>

<span data-ttu-id="2a157-123">Consultas Olá **suspenso** Estado estão a ser colocados em fila devido a limites de tooconcurrency.</span><span class="sxs-lookup"><span data-stu-id="2a157-123">Queries in hello **Suspended** state are being queued due tooconcurrency limits.</span></span> <span data-ttu-id="2a157-124">Estas consultas também aparecem na Olá sys.dm_pdw_waits aguarda consulta com um tipo de UserConcurrencyResourceType.</span><span class="sxs-lookup"><span data-stu-id="2a157-124">These queries also appear in hello sys.dm_pdw_waits waits query with a type of UserConcurrencyResourceType.</span></span> <span data-ttu-id="2a157-125">Consulte [simultaneidade e carga de trabalho de gestão] [ Concurrency and workload management] para obter mais detalhes sobre os limites de concorrência.</span><span class="sxs-lookup"><span data-stu-id="2a157-125">See [Concurrency and workload management][Concurrency and workload management] for more details on concurrency limits.</span></span> <span data-ttu-id="2a157-126">As consultas também podem aguardar por outros motivos, tais como de bloqueios de objeto.</span><span class="sxs-lookup"><span data-stu-id="2a157-126">Queries can also wait for other reasons such as for object locks.</span></span>  <span data-ttu-id="2a157-127">Se a consulta está à espera de um recurso, consulte o artigo [investigar consultas aguardar recursos] [ Investigating queries waiting for resources] mais abaixo neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2a157-127">If your query is waiting for a resource, see [Investigating queries waiting for resources][Investigating queries waiting for resources] further down in this article.</span></span>

<span data-ttu-id="2a157-128">pesquisa de Olá toosimplify de uma consulta na tabela de sys.dm_pdw_exec_requests Olá, utilize [etiqueta] [ LABEL] tooassign uma consulta de tooyour comentário que pode ser pesquisada na vista de sys.dm_pdw_exec_requests Olá.</span><span class="sxs-lookup"><span data-stu-id="2a157-128">toosimplify hello lookup of a query in hello sys.dm_pdw_exec_requests table, use [LABEL][LABEL] tooassign a comment tooyour query that can be looked up in hello sys.dm_pdw_exec_requests view.</span></span>

```sql
-- Query with Label
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query')
;
```

### <a name="step-2-investigate-hello-query-plan"></a><span data-ttu-id="2a157-129">PASSO 2: Investigar o plano de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="2a157-129">STEP 2: Investigate hello query plan</span></span>
<span data-ttu-id="2a157-130">Utilizar plano SQL (DSQL) distribuído Olá ID do pedido tooretrieve Olá da consulta de [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span><span class="sxs-lookup"><span data-stu-id="2a157-130">Use hello Request ID tooretrieve hello query's distributed SQL (DSQL) plan from [sys.dm_pdw_request_steps][sys.dm_pdw_request_steps].</span></span>

```sql
-- Find hello distributed query plan steps for a specific query.
-- Replace request_id with value from Step 1.

SELECT * FROM sys.dm_pdw_request_steps
WHERE request_id = 'QID####'
ORDER BY step_index;
```

<span data-ttu-id="2a157-131">Quando um plano DSQL está a demorar mais que o esperado, causa Olá pode ser um plano complexo com vários passos DSQL ou apenas um passo demorar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="2a157-131">When a DSQL plan is taking longer than expected, hello cause can be a complex plan with many DSQL steps or just one step taking a long time.</span></span>  <span data-ttu-id="2a157-132">Se o plano de Olá muitos passos com várias operações de movimentação, é aconselhável o movimento de dados de tooreduce de distribuições de tabela.</span><span class="sxs-lookup"><span data-stu-id="2a157-132">If hello plan is many steps with several move operations, consider optimizing your table distributions tooreduce data movement.</span></span> <span data-ttu-id="2a157-133">Olá [tabela distribuição] [ Table distribution] artigo explica por que motivo dados tem de ser movido toosolve uma consulta e explica algumas movimento de dados de toominimize de estratégias de distribuição.</span><span class="sxs-lookup"><span data-stu-id="2a157-133">hello [Table distribution][Table distribution] article explains why data must be moved toosolve a query and explains some distribution strategies toominimize data movement.</span></span>

<span data-ttu-id="2a157-134">tooinvestigate obter mais detalhes sobre um único passo hello *operation_type* coluna Olá de passo e nota da consulta de execução longa Olá **passo índice**:</span><span class="sxs-lookup"><span data-stu-id="2a157-134">tooinvestigate further details about a single step, hello *operation_type* column of hello long-running query step and note hello **Step Index**:</span></span>

* <span data-ttu-id="2a157-135">Continuar com o passo 3a para **operações SQL**: OnOperation, RemoteOperation, ReturnOperation.</span><span class="sxs-lookup"><span data-stu-id="2a157-135">Proceed with Step 3a for **SQL operations**: OnOperation, RemoteOperation, ReturnOperation.</span></span>
* <span data-ttu-id="2a157-136">Continuar com o passo 3b para **operações de movimento de dados**: ShuffleMoveOperation BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span><span class="sxs-lookup"><span data-stu-id="2a157-136">Proceed with Step 3b for **Data Movement operations**: ShuffleMoveOperation, BroadcastMoveOperation, TrimMoveOperation, PartitionMoveOperation, MoveOperation, CopyOperation.</span></span>

### <a name="step-3a-investigate-sql-on-hello-distributed-databases"></a><span data-ttu-id="2a157-137">PASSO 3a: investigar SQL em bases de dados de Olá distribuído</span><span class="sxs-lookup"><span data-stu-id="2a157-137">STEP 3a: Investigate SQL on hello distributed databases</span></span>
<span data-ttu-id="2a157-138">Utilizar Olá ID do pedido e detalhes de tooretrieve Olá passo índice da [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], que contém informações de execução do passo de consulta Olá em todos os Olá distribuídas bases de dados.</span><span class="sxs-lookup"><span data-stu-id="2a157-138">Use hello Request ID and hello Step Index tooretrieve details from [sys.dm_pdw_sql_requests][sys.dm_pdw_sql_requests], which contains execution information of hello query step on all of hello distributed databases.</span></span>

```sql
-- Find hello distribution run times for a SQL step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_sql_requests
WHERE request_id = 'QID####' AND step_index = 2;
```

<span data-ttu-id="2a157-139">Quando executa o passo de consulta Olá, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] pode ser plano estimado do tooretrieve utilizados Olá do SQL Server de Olá cache do plano de SQL Server para o passo de Olá em execução numa determinada distribuição.</span><span class="sxs-lookup"><span data-stu-id="2a157-139">When hello query step is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello step running on a particular distribution.</span></span>

```sql
-- Find hello SQL Server execution plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(1, 78);
```

### <a name="step-3b-investigate-data-movement-on-hello-distributed-databases"></a><span data-ttu-id="2a157-140">Passo 3b: investigar o movimento de dados nas bases de dados de Olá distribuído</span><span class="sxs-lookup"><span data-stu-id="2a157-140">STEP 3b: Investigate data movement on hello distributed databases</span></span>
<span data-ttu-id="2a157-141">Utilizar Olá ID do pedido e Olá passo índice tooretrieve sobre um passo de movimento de dados em execução em cada distribuição de [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span><span class="sxs-lookup"><span data-stu-id="2a157-141">Use hello Request ID and hello Step Index tooretrieve information about a data movement step running on each distribution from [sys.dm_pdw_dms_workers][sys.dm_pdw_dms_workers].</span></span>

```sql
-- Find hello information about all hello workers completing a Data Movement Step.
-- Replace request_id and step_index with values from Step 1 and 3.

SELECT * FROM sys.dm_pdw_dms_workers
WHERE request_id = 'QID####' AND step_index = 2;
```

* <span data-ttu-id="2a157-142">Verifique Olá *total_elapsed_time* toosee coluna se um determinado distribuição está a demorar significativamente maior do que outras pessoas para movimento de dados.</span><span class="sxs-lookup"><span data-stu-id="2a157-142">Check hello *total_elapsed_time* column toosee if a particular distribution is taking significantly longer than others for data movement.</span></span>
* <span data-ttu-id="2a157-143">Para distribuição de execução longa Olá, verifique Olá *rows_processed* toosee coluna se Olá o número de linhas a ser movidos dessa distribuição é significativamente maior do que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="2a157-143">For hello long-running distribution, check hello *rows_processed* column toosee if hello number of rows being moved from that distribution is significantly larger than others.</span></span> <span data-ttu-id="2a157-144">Se Sim, isto pode indicar dissimetrias dos seus dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="2a157-144">If so, this may indicate skew of your underlying data.</span></span>

<span data-ttu-id="2a157-145">Se estiver a executar a consulta de Olá, [DBCC PDW_SHOWEXECUTIONPLAN] [ DBCC PDW_SHOWEXECUTIONPLAN] pode ser plano estimado do tooretrieve utilizados Olá do SQL Server de Olá cache do plano de SQL Server para Olá atualmente em execução passo do SQL Server dentro de um determinado distribuição.</span><span class="sxs-lookup"><span data-stu-id="2a157-145">If hello query is running, [DBCC PDW_SHOWEXECUTIONPLAN][DBCC PDW_SHOWEXECUTIONPLAN] can be used tooretrieve hello SQL Server estimated plan from hello SQL Server plan cache for hello currently running SQL Step within a particular distribution.</span></span>

```sql
-- Find hello SQL Server estimated plan for a query running on a specific SQL Data Warehouse Compute or Control node.
-- Replace distribution_id and spid with values from previous query.

DBCC PDW_SHOWEXECUTIONPLAN(55, 238);
```

<a name="waiting"></a>

## <a name="monitor-waiting-queries"></a><span data-ttu-id="2a157-146">Consultas de espera de monitor</span><span class="sxs-lookup"><span data-stu-id="2a157-146">Monitor waiting queries</span></span>
<span data-ttu-id="2a157-147">Se descobrir que progresso não é efetuar a consulta porque está a aguardar para um recurso, segue-se uma consulta que mostra todos os recursos de Olá que está a aguardar uma consulta.</span><span class="sxs-lookup"><span data-stu-id="2a157-147">If you discover that your query is not making progress because it is waiting for a resource, here is a query that shows all hello resources a query is waiting for.</span></span>

```sql
-- Find queries 
-- Replace request_id with value from Step 1.

SELECT waits.session_id,
      waits.request_id,  
      requests.command,
      requests.status,
      requests.start_time,  
      waits.type,
      waits.state,
      waits.object_type,
      waits.object_name
FROM   sys.dm_pdw_waits waits
   JOIN  sys.dm_pdw_exec_requests requests
   ON waits.request_id=requests.request_id
WHERE waits.request_id = 'QID####'
ORDER BY waits.object_name, waits.object_type, waits.state;
```

<span data-ttu-id="2a157-148">Se a consulta de Olá ativamente está a aguardar no recursos a partir de outra consulta, em seguida, estado de Olá será **AcquireResources**.</span><span class="sxs-lookup"><span data-stu-id="2a157-148">If hello query is actively waiting on resources from another query, then hello state will be **AcquireResources**.</span></span>  <span data-ttu-id="2a157-149">Se a consulta de Olá tem todos os recursos de Olá necessário, então Olá estado será **Granted**.</span><span class="sxs-lookup"><span data-stu-id="2a157-149">If hello query has all hello required resources, then hello state will be **Granted**.</span></span>

## <a name="monitor-tempdb"></a><span data-ttu-id="2a157-150">Monitor tempdb</span><span class="sxs-lookup"><span data-stu-id="2a157-150">Monitor tempdb</span></span>
<span data-ttu-id="2a157-151">A utilização de tempdb elevado pode ser Olá causa de raiz para um desempenho lento e fora de problemas de memória.</span><span class="sxs-lookup"><span data-stu-id="2a157-151">High tempdb utilization can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="2a157-152">Verifique primeiro se tiver dados qualidade dissimetrias ou fraco rowgroups e tome as ações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="2a157-152">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="2a157-153">Considere a dimensionar o seu armazém de dados se encontrar tempdb atingir os limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="2a157-153">Consider scaling your data warehouse if you find tempdb reaching its limits during query execution.</span></span> <span data-ttu-id="2a157-154">Olá seguinte descreve como tooidentify tempdb utilização por consulta em cada nó.</span><span class="sxs-lookup"><span data-stu-id="2a157-154">hello following describes how tooidentify tempdb usage per query on each node.</span></span> 

<span data-ttu-id="2a157-155">Crie Olá vista tooassociate Olá id de nó adequado para sys.dm_pdw_sql_requests seguinte.</span><span class="sxs-lookup"><span data-stu-id="2a157-155">Create hello following view tooassociate hello appropriate node id for sys.dm_pdw_sql_requests.</span></span> <span data-ttu-id="2a157-156">Este procedimento irá ativar tooleverage outros DMVs pass-through e associar as tabelas com sys.dm_pdw_sql_requests.</span><span class="sxs-lookup"><span data-stu-id="2a157-156">This will enable you tooleverage other pass-through DMVs and join those tables with sys.dm_pdw_sql_requests.</span></span>

```sql
-- sys.dm_pdw_sql_requests with hello correct node id
CREATE VIEW sql_requests AS
(SELECT
       sr.request_id,
       sr.step_index,
       (CASE 
              WHEN (sr.distribution_id = -1 ) THEN 
              (SELECT pdw_node_id FROM sys.dm_pdw_nodes WHERE type = 'CONTROL') 
              ELSE d.pdw_node_id END) AS pdw_node_id,
       sr.distribution_id,
       sr.status,
       sr.error_id,
       sr.start_time,
       sr.end_time,
       sr.total_elapsed_time,
       sr.row_count,
       sr.spid,
       sr.command
FROM sys.pdw_distributions AS d
RIGHT JOIN sys.dm_pdw_sql_requests AS sr ON d.distribution_id = sr.distribution_id)
```
<span data-ttu-id="2a157-157">Execute Olá consulta toomonitor tempdb os seguintes:</span><span class="sxs-lookup"><span data-stu-id="2a157-157">Run hello following query toomonitor tempdb:</span></span>

```sql
-- Monitor tempdb
SELECT
    sr.request_id,
    ssu.session_id,
    ssu.pdw_node_id,
    sr.command,
    sr.total_elapsed_time,
    es.login_name AS 'LoginName',
    DB_NAME(ssu.database_id) AS 'DatabaseName',
    (es.memory_usage * 8) AS 'MemoryUsage (in KB)',
    (ssu.user_objects_alloc_page_count * 8) AS 'Space Allocated For User Objects (in KB)',
    (ssu.user_objects_dealloc_page_count * 8) AS 'Space Deallocated For User Objects (in KB)',
    (ssu.internal_objects_alloc_page_count * 8) AS 'Space Allocated For Internal Objects (in KB)',
    (ssu.internal_objects_dealloc_page_count * 8) AS 'Space Deallocated For Internal Objects (in KB)',
    CASE es.is_user_process
    WHEN 1 THEN 'User Session'
    WHEN 0 THEN 'System Session'
    END AS 'SessionType',
    es.row_count AS 'RowCount'
FROM sys.dm_pdw_nodes_db_session_space_usage AS ssu
    INNER JOIN sys.dm_pdw_nodes_exec_sessions AS es ON ssu.session_id = es.session_id AND ssu.pdw_node_id = es.pdw_node_id
    INNER JOIN sys.dm_pdw_nodes_exec_connections AS er ON ssu.session_id = er.session_id AND ssu.pdw_node_id = er.pdw_node_id
    INNER JOIN sql_requests AS sr ON ssu.session_id = sr.spid AND ssu.pdw_node_id = sr.pdw_node_id
WHERE DB_NAME(ssu.database_id) = 'tempdb'
    AND es.session_id <> @@SPID
    AND es.login_name <> 'sa' 
ORDER BY sr.request_id;
```
## <a name="monitor-memory"></a><span data-ttu-id="2a157-158">Monitor de memória</span><span class="sxs-lookup"><span data-stu-id="2a157-158">Monitor memory</span></span>

<span data-ttu-id="2a157-159">Memória pode ser Olá causa de raiz para um desempenho lento e fora de problemas de memória.</span><span class="sxs-lookup"><span data-stu-id="2a157-159">Memory can be hello root cause for slow performance and out of memory issues.</span></span> <span data-ttu-id="2a157-160">Verifique primeiro se tiver dados qualidade dissimetrias ou fraco rowgroups e tome as ações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="2a157-160">Please first check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="2a157-161">Considere a dimensionar o seu armazém de dados se encontrar utilização de memória do SQL Server atingir os limites durante a execução de consulta.</span><span class="sxs-lookup"><span data-stu-id="2a157-161">Consider scaling your data warehouse if you find SQL Server memory usage reaching its limits during query execution.</span></span>

<span data-ttu-id="2a157-162">Olá seguinte consulta devolve o SQL Server memória e utilização pressão de memória por nó:</span><span class="sxs-lookup"><span data-stu-id="2a157-162">hello following query returns SQL Server memory usage and memory pressure per node:</span></span> 
```sql
-- Memory consumption
SELECT
  pc1.cntr_value as Curr_Mem_KB, 
  pc1.cntr_value/1024.0 as Curr_Mem_MB,
  (pc1.cntr_value/1048576.0) as Curr_Mem_GB,
  pc2.cntr_value as Max_Mem_KB,
  pc2.cntr_value/1024.0 as Max_Mem_MB,
  (pc2.cntr_value/1048576.0) as Max_Mem_GB,
  pc1.cntr_value * 100.0/pc2.cntr_value AS Memory_Utilization_Percentage,
  pc1.pdw_node_id
FROM
-- pc1: current memory
sys.dm_pdw_nodes_os_performance_counters AS pc1
-- pc2: total memory allowed for this SQL instance
JOIN sys.dm_pdw_nodes_os_performance_counters AS pc2 
ON pc1.object_name = pc2.object_name AND pc1.pdw_node_id = pc2.pdw_node_id
WHERE
pc1.counter_name = 'Total Server Memory (KB)'
AND pc2.counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-size"></a><span data-ttu-id="2a157-163">Tamanho do registo de transação de monitor</span><span class="sxs-lookup"><span data-stu-id="2a157-163">Monitor transaction log size</span></span>
<span data-ttu-id="2a157-164">Olá seguinte consulta devolve o tamanho de registo de transação de Olá cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="2a157-164">hello following query returns hello transaction log size on each distribution.</span></span> <span data-ttu-id="2a157-165">Verifique se tem dados qualidade dissimetrias ou fraco rowgroups e tome as ações adequadas Olá.</span><span class="sxs-lookup"><span data-stu-id="2a157-165">Please check if you have data skew or poor quality rowgroups and take hello appropriate actions.</span></span> <span data-ttu-id="2a157-166">Se um dos ficheiros de registo Olá está a atingir 160GB, deve considerar como aumentar verticalmente a sua instância ou limitar o tamanho da transação.</span><span class="sxs-lookup"><span data-stu-id="2a157-166">If one of hello log files is reaching 160GB, you should consider scaling up your instance or limiting your transaction size.</span></span> 
```sql
-- Transaction log size
SELECT
  instance_name as distribution_db,
  cntr_value*1.0/1048576 as log_file_size_used_GB,
  pdw_node_id 
FROM sys.dm_pdw_nodes_os_performance_counters 
WHERE 
instance_name like 'Distribution_%' 
AND counter_name = 'Log File(s) Used Size (KB)'
AND counter_name = 'Target Server Memory (KB)'
```
## <a name="monitor-transaction-log-rollback"></a><span data-ttu-id="2a157-167">Monitorizar a reversão da transacção de registo</span><span class="sxs-lookup"><span data-stu-id="2a157-167">Monitor transaction log rollback</span></span>
<span data-ttu-id="2a157-168">Se as suas consultas estão a falhar ou colocar um tooproceed muito tempo, pode verificar e monitorizar se tiver quaisquer transações reverter.</span><span class="sxs-lookup"><span data-stu-id="2a157-168">If your queries are failing or taking a long time tooproceed, you can check and monitor if you have any transactions rolling back.</span></span>
```sql
-- Monitor rollback
SELECT 
    SUM(CASE WHEN t.database_transaction_next_undo_lsn IS NOT NULL THEN 1 ELSE 0 END),
    t.pdw_node_id,
    nod.[type]
FROM sys.dm_pdw_nodes_tran_database_transactions t
JOIN sys.dm_pdw_nodes nod ON t.pdw_node_id = nod.pdw_node_id
GROUP BY t.pdw_node_id, nod.[type]
```

## <a name="next-steps"></a><span data-ttu-id="2a157-169">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2a157-169">Next steps</span></span>
<span data-ttu-id="2a157-170">Consulte [vistas de sistema] [ System views] para obter mais informações sobre DMVs.</span><span class="sxs-lookup"><span data-stu-id="2a157-170">See [System views][System views] for more information on DMVs.</span></span>
<span data-ttu-id="2a157-171">Consulte [melhores práticas do SQL Data Warehouse] [ SQL Data Warehouse best practices] para obter mais informações sobre as melhores práticas</span><span class="sxs-lookup"><span data-stu-id="2a157-171">See [SQL Data Warehouse best practices][SQL Data Warehouse best practices] for more information about best practices</span></span>

<!--Image references-->

<!--Article references-->
[Manage overview]: ./sql-data-warehouse-overview-manage.md
[SQL Data Warehouse best practices]: ./sql-data-warehouse-best-practices.md
[System views]: ./sql-data-warehouse-reference-tsql-system-views.md
[Table distribution]: ./sql-data-warehouse-tables-distribute.md
[Concurrency and workload management]: ./sql-data-warehouse-develop-concurrency.md
[Investigating queries waiting for resources]: ./sql-data-warehouse-manage-monitor.md#waiting

<!--MSDN references-->
[sys.dm_pdw_dms_workers]: http://msdn.microsoft.com/library/mt203878.aspx
[sys.dm_pdw_exec_requests]: http://msdn.microsoft.com/library/mt203887.aspx
[sys.dm_pdw_exec_sessions]: http://msdn.microsoft.com/library/mt203883.aspx
[sys.dm_pdw_request_steps]: http://msdn.microsoft.com/library/mt203913.aspx
[sys.dm_pdw_sql_requests]: http://msdn.microsoft.com/library/mt203889.aspx
[DBCC PDW_SHOWEXECUTIONPLAN]: http://msdn.microsoft.com/library/mt204017.aspx
[DBCC PDW_SHOWSPACEUSED]: http://msdn.microsoft.com/library/mt204028.aspx
[LABEL]: https://msdn.microsoft.com/library/ms190322.aspx
