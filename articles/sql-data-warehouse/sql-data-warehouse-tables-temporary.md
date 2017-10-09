---
title: tabelas de aaaTemporary no SQL Data Warehouse | Microsoft Docs
description: "Introdução ao tabelas temporárias no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 9b1119eb-7f54-46d0-ad74-19c85a2a555a
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 2e8b122eb6d71d5bc0a99ce8a2ecab5dbe2d1b49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="temporary-tables-in-sql-data-warehouse"></a><span data-ttu-id="7b199-103">Tabelas temporárias no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7b199-103">Temporary tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="7b199-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="7b199-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="7b199-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="7b199-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="7b199-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="7b199-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="7b199-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="7b199-107">[Index][Index]</span></span>
> * <span data-ttu-id="7b199-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="7b199-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="7b199-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="7b199-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="7b199-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="7b199-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="7b199-111">Tabelas temporárias são muito úteis durante o processamento de dados - especialmente durante a transformação onde resultados intermédios Olá são transitórios.</span><span class="sxs-lookup"><span data-stu-id="7b199-111">Temporary tables are very useful when processing data - especially during transformation where hello intermediate results are transient.</span></span> <span data-ttu-id="7b199-112">No SQL Data Warehouse tabelas temporárias existirem ao nível de sessão de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b199-112">In SQL Data Warehouse temporary tables exist at hello session level.</span></span>  <span data-ttu-id="7b199-113">São apenas visíveis toohello sessão em que foram criadas e são automaticamente removidas quando termina a sessão.</span><span class="sxs-lookup"><span data-stu-id="7b199-113">They are only visible toohello session in which they were created and are automatically dropped when that session logs off.</span></span>  <span data-ttu-id="7b199-114">Tabelas temporárias oferecem uma vantagem de desempenho, porque os respetivos resultados são escritos toolocal em vez de armazenamento remoto.</span><span class="sxs-lookup"><span data-stu-id="7b199-114">Temporary tables offer a performance benefit because their results are written toolocal rather than remote storage.</span></span>  <span data-ttu-id="7b199-115">Tabelas temporárias são ligeiramente diferentes no armazém de dados SQL do Azure SQL Database do Azure que possam ser acedidos de qualquer local dentro da sessão de Olá, incluindo dentro e fora de um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="7b199-115">Temporary tables are slightly different in Azure SQL Data Warehouse than Azure SQL Database as they can be accessed from anywhere inside hello session, including both inside and outside of a stored procedure.</span></span>

<span data-ttu-id="7b199-116">Este artigo contém documentação de orientação essencial para utilizar tabelas temporárias e realça os princípios de Olá de tabelas temporárias ao nível de sessão.</span><span class="sxs-lookup"><span data-stu-id="7b199-116">This article contains essential guidance for using temporary tables and highlights hello principles of session level temporary tables.</span></span> <span data-ttu-id="7b199-117">Utilizar informações de Olá neste artigo pode ajudá-lo modularize código, melhorando reusability e facilidade de manutenção do seu código.</span><span class="sxs-lookup"><span data-stu-id="7b199-117">Using hello information in this article can help you modularize your code, improving both reusability and ease of maintenance of your code.</span></span>

## <a name="create-a-temporary-table"></a><span data-ttu-id="7b199-118">Criar uma tabela temporária</span><span class="sxs-lookup"><span data-stu-id="7b199-118">Create a temporary table</span></span>
<span data-ttu-id="7b199-119">São criadas tabelas temporárias atribuindo simplesmente lhe o prefixo do nome de tabela com um `#`.</span><span class="sxs-lookup"><span data-stu-id="7b199-119">Temporary tables are created by simply prefixing your table name with a `#`.</span></span>  <span data-ttu-id="7b199-120">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="7b199-120">For example:</span></span>

```sql
CREATE TABLE #stats_ddl
(
    [schema_name]        NVARCHAR(128) NOT NULL
,    [table_name]            NVARCHAR(128) NOT NULL
,    [stats_name]            NVARCHAR(128) NOT NULL
,    [stats_is_filtered]     BIT           NOT NULL
,    [seq_nmbr]              BIGINT        NOT NULL
,    [two_part_name]         NVARCHAR(260) NOT NULL
,    [three_part_name]       NVARCHAR(400) NOT NULL
)
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
```

<span data-ttu-id="7b199-121">Também é possível criar tabelas temporárias com um `CTAS` exatamente utilizando Olá a mesma abordagem:</span><span class="sxs-lookup"><span data-stu-id="7b199-121">Temporary tables can also be created with a `CTAS` using exactly hello same approach:</span></span>

```sql
CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
,    HEAP
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
``` 

> [!NOTE]
> <span data-ttu-id="7b199-122">`CTAS`é um comando muito poderoso e Olá adicionou partido das que está a ser muito eficientes na sua utilização do espaço de registo de transações.</span><span class="sxs-lookup"><span data-stu-id="7b199-122">`CTAS` is a very powerful command and has hello added advantage of being very efficient in its use of transaction log space.</span></span> 
> 
> 

## <a name="dropping-temporary-tables"></a><span data-ttu-id="7b199-123">Remover tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="7b199-123">Dropping temporary tables</span></span>
<span data-ttu-id="7b199-124">Quando é criada uma nova sessão, não existem tabelas temporárias devem existir.</span><span class="sxs-lookup"><span data-stu-id="7b199-124">When a new session is created, no temporary tables should exist.</span></span>  <span data-ttu-id="7b199-125">No entanto, se estiver a chamar Olá mesmo procedimento, que cria um temporário com Olá armazenado mesmo nome, tooensure que sua `CREATE TABLE` instruções são com êxito uma verificação de pré-existência simple com um `DROP` podem ser utilizados como Olá exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="7b199-125">However, if you are calling hello same stored procedure, which creates a temporary with hello same name, tooensure that your `CREATE TABLE` statements are successful a simple pre-existence check with a `DROP` can be used as in hello below example:</span></span>

```sql
IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END
```

<span data-ttu-id="7b199-126">Para consistência de codificação, é uma boa praticar toouse este padrão de tabelas e tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="7b199-126">For coding consistency, it is a good practice toouse this pattern for both tables and temporary tables.</span></span>  <span data-ttu-id="7b199-127">Também é uma boa ideia toouse `DROP TABLE` tooremove tabelas temporárias quando tiver terminado com os mesmos no seu código.</span><span class="sxs-lookup"><span data-stu-id="7b199-127">It is also a good idea toouse `DROP TABLE` tooremove temporary tables when you have finished with them in your code.</span></span>  <span data-ttu-id="7b199-128">Desenvolvimento do procedimento armazenado é bastante comum toosee Olá comandos drop agrupados no final de Olá de um procedimento tooensure que estes objetos são limpos.</span><span class="sxs-lookup"><span data-stu-id="7b199-128">In stored procedure development it is quite common toosee hello drop commands bundled together at hello end of a procedure tooensure these objects are cleaned up.</span></span>

```sql
DROP TABLE #stats_ddl
```

## <a name="modularizing-code"></a><span data-ttu-id="7b199-129">Código modularizing</span><span class="sxs-lookup"><span data-stu-id="7b199-129">Modularizing code</span></span>
<span data-ttu-id="7b199-130">Uma vez que a tabelas temporárias podem ser vistas em qualquer lugar numa sessão de utilizador, isto pode ser explorada toohelp modularize código da aplicação.</span><span class="sxs-lookup"><span data-stu-id="7b199-130">Since temporary tables can be seen anywhere in a user session, this can be exploited toohelp you modularize your application code.</span></span>  <span data-ttu-id="7b199-131">Por exemplo, hello procedimento armazenado abaixo reúne Olá recomendado práticas from above toogenerate DDL que irá atualizar todas as estatísticas da base de dados de Olá pelo nome da estatística.</span><span class="sxs-lookup"><span data-stu-id="7b199-131">For example, hello stored procedure below brings together hello recommended practices from above toogenerate DDL which will update all statistics in hello database by statistic name.</span></span>

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_update_stats]
(   @update_type    tinyint -- 1 default 2 fullscan 3 sample 4 resample
    ,@sample_pct     tinyint
)
AS

IF @update_type NOT IN (1,2,3,4)
BEGIN;
    THROW 151000,'Invalid value for @update_type parameter. Valid range 1 (default), 2 (fullscan), 3 (sample) or 4 (resample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN
    DROP TABLE #stats_ddl
END

CREATE TABLE #stats_ddl
WITH
(
    DISTRIBUTION = HASH([seq_nmbr])
)
AS
(
SELECT
        sm.[name]                                                                AS [schema_name]
,        tb.[name]                                                                AS [table_name]
,        st.[name]                                                                AS [stats_name]
,        st.[has_filter]                                                            AS [stats_is_filtered]
,       ROW_NUMBER()
        OVER(ORDER BY (SELECT NULL))                                            AS [seq_nmbr]
,                                 QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [two_part_name]
,        QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])  AS [three_part_name]
FROM    sys.objects            AS ob
JOIN    sys.stats            AS st    ON    ob.[object_id]        = st.[object_id]
JOIN    sys.stats_columns    AS sc    ON    st.[stats_id]        = sc.[stats_id]
                                    AND st.[object_id]        = sc.[object_id]
JOIN    sys.columns            AS co    ON    sc.[column_id]        = co.[column_id]
                                    AND    sc.[object_id]        = co.[object_id]
JOIN    sys.tables            AS tb    ON    co.[object_id]        = tb.[object_id]
JOIN    sys.schemas            AS sm    ON    tb.[schema_id]        = sm.[schema_id]
WHERE    1=1
AND        st.[user_created]   = 1
GROUP BY
        sm.[name]
,        tb.[name]
,        st.[name]
,        st.[filter_definition]
,        st.[has_filter]
)
SELECT
    CASE @update_type
    WHEN 1
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+');'
    WHEN 2
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH FULLSCAN;'
    WHEN 3
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH SAMPLE '+CAST(@sample_pct AS VARCHAR(20))+' PERCENT;'
    WHEN 4
    THEN 'UPDATE STATISTICS '+[two_part_name]+'('+[stats_name]+') WITH RESAMPLE;'
    END AS [update_stats_ddl]
,   [seq_nmbr]
FROM    t1
;
GO
```

<span data-ttu-id="7b199-132">Nesta fase, a única ação de Olá ocorrida é criação Olá de um procedimento armazenado que será gerado simplesmente uma tabela temporária, stats_ddl #, com as instruções DDL.</span><span class="sxs-lookup"><span data-stu-id="7b199-132">At this stage hello only action that has occurred is hello creation of a stored procedure which will simply generated a temporary table, #stats_ddl, with DDL statements.</span></span>  <span data-ttu-id="7b199-133">Este procedimento armazenado irá remover #stats_ddl se já existir tooensure não falha se mais do que uma vez executado dentro de uma sessão.</span><span class="sxs-lookup"><span data-stu-id="7b199-133">This stored procedure will drop #stats_ddl if it already exists tooensure it does not fail if run more than once within a session.</span></span>  <span data-ttu-id="7b199-134">No entanto, uma vez que não existe nenhum `DROP TABLE` no fim de Olá do procedimento armazenado de Olá, quando hello procedimento armazenado for concluído, que irá deixar tabela Olá criada para que possa ser lido fora do procedimento armazenado de Olá.</span><span class="sxs-lookup"><span data-stu-id="7b199-134">However, since there is no `DROP TABLE` at hello end of hello stored procedure, when hello stored procedure completes, it will leave hello created table so that it can be read outside of hello stored procedure.</span></span>  <span data-ttu-id="7b199-135">No SQL Data Warehouse, ao contrário de outras bases de dados do SQL Server, é possível toouse tabela temporária de Olá fora do procedimento de Olá que o criou.</span><span class="sxs-lookup"><span data-stu-id="7b199-135">In SQL Data Warehouse, unlike other SQL Server databases, it is possible toouse hello temporary table outside of hello procedure that created it.</span></span>  <span data-ttu-id="7b199-136">Tabelas temporárias do SQL Data Warehouse podem ser utilizadas **em qualquer lugar** dentro Olá sessão.</span><span class="sxs-lookup"><span data-stu-id="7b199-136">SQL Data Warehouse temporary tables can be used **anywhere** inside hello session.</span></span> <span data-ttu-id="7b199-137">Isto pode levar toomore modular e gerível o código que aparece Olá exemplo abaixo:</span><span class="sxs-lookup"><span data-stu-id="7b199-137">This can lead toomore modular and manageable code as in hello below example:</span></span>

```sql
EXEC [dbo].[prc_sqldw_update_stats] @update_type = 1, @sample_pct = NULL;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''

WHILE @i <= @t
BEGIN
    SET @s=(SELECT update_stats_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

## <a name="temporary-table-limitations"></a><span data-ttu-id="7b199-138">Limitações de tabela temporária</span><span class="sxs-lookup"><span data-stu-id="7b199-138">Temporary table limitations</span></span>
<span data-ttu-id="7b199-139">O SQL Data Warehouse impõe algumas limitações ao efetuar a tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="7b199-139">SQL Data Warehouse does impose a couple of limitations when implementing temporary tables.</span></span>  <span data-ttu-id="7b199-140">Atualmente, apenas a sessão de tabelas temporárias âmbito são suportadas.</span><span class="sxs-lookup"><span data-stu-id="7b199-140">Currently, only session scoped temporary tables are supported.</span></span>  <span data-ttu-id="7b199-141">As tabelas temporárias globais não são suportadas.</span><span class="sxs-lookup"><span data-stu-id="7b199-141">Global Temporary Tables are not supported.</span></span>  <span data-ttu-id="7b199-142">Além disso, não não possível criar vistas de tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="7b199-142">In addition, views cannot be created on temporary tables.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7b199-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7b199-143">Next steps</span></span>
<span data-ttu-id="7b199-144">toolearn mais, consulte os artigos de Olá no [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de indexação][Index], [uma tabela de criação de partições] [ Partition] e [ Manter as estatísticas da tabela][Statistics].</span><span class="sxs-lookup"><span data-stu-id="7b199-144">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Maintaining Table Statistics][Statistics].</span></span>  <span data-ttu-id="7b199-145">Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7b199-145">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
