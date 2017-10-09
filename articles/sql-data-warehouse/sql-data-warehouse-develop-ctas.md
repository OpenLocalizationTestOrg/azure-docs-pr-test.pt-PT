---
title: tabela aaaCreate como selecione (CTAS) no SQL Data Warehouse | Microsoft Docs
description: "Sugestões para programação com Olá criar tabela como selecionar instrução (CTAS) no Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 68ac9a94-09f9-424b-b536-06a125a653bd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 01/30/2017
ms.author: shigu;barbkess
ms.openlocfilehash: e381601a0a4d94e189d8f9115bf2e7593025410b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a><span data-ttu-id="f1943-103">Create Table As Select (CTAS) no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="f1943-103">Create Table As Select (CTAS) in SQL Data Warehouse</span></span>
<span data-ttu-id="f1943-104">Criar tabela como selecionar ou `CTAS` é uma das Olá funcionalidades mais importantes de T-SQL disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f1943-104">Create table as select or `CTAS` is one of hello most important T-SQL features available.</span></span> <span data-ttu-id="f1943-105">É uma operação totalmente parallelized que cria uma nova tabela com base no resultado de Olá de uma instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="f1943-105">It is a fully parallelized operation that creates a new table based on hello output of a SELECT statement.</span></span> <span data-ttu-id="f1943-106">`CTAS`é uma cópia de uma tabela de Olá toocreate de forma mais simples e mais rápida.</span><span class="sxs-lookup"><span data-stu-id="f1943-106">`CTAS` is hello simplest and fastest way toocreate a copy of a table.</span></span> <span data-ttu-id="f1943-107">Este documento fornece exemplos e melhores práticas para `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="f1943-107">This document provides both examples and best practices for `CTAS`.</span></span>

## <a name="selectinto-vs-ctas"></a><span data-ttu-id="f1943-108">SELECIONAR... NO vs. CTAS</span><span class="sxs-lookup"><span data-stu-id="f1943-108">SELECT..INTO vs. CTAS</span></span>
<span data-ttu-id="f1943-109">Pode considerar `CTAS` como uma versão Super-obrigatórios debitada do `SELECT..INTO`.</span><span class="sxs-lookup"><span data-stu-id="f1943-109">You can consider `CTAS` as a super-charged version of `SELECT..INTO`.</span></span>

<span data-ttu-id="f1943-110">Segue-se um exemplo de uma simples `SELECT..INTO` instrução:</span><span class="sxs-lookup"><span data-stu-id="f1943-110">Below is an example of a simple `SELECT..INTO` statement:</span></span>

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

<span data-ttu-id="f1943-111">No exemplo Olá acima `[dbo].[FactInternetSales_new]` seria possível criar como tabela de distribuída ROUND_ROBIN com um índice de COLUMNSTORE em cluster no mesmo como estas são as predefinições da tabela de Olá no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f1943-111">In hello example above `[dbo].[FactInternetSales_new]` would be created as ROUND_ROBIN distributed table with a CLUSTERED COLUMNSTORE INDEX on it as these are hello table defaults in Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="f1943-112">`SELECT..INTO`No entanto não permitem-lhe toochange o índice de método ou Olá da distribuição de Olá escreva como parte da operação de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-112">`SELECT..INTO` however does not allow you toochange either hello distribution method or hello index type as part of hello operation.</span></span> <span data-ttu-id="f1943-113">Este é onde `CTAS` é apresentada no.</span><span class="sxs-lookup"><span data-stu-id="f1943-113">This is where `CTAS` comes in.</span></span>

<span data-ttu-id="f1943-114">tooconvert Olá acima demasiado`CTAS` é bastante simples:</span><span class="sxs-lookup"><span data-stu-id="f1943-114">tooconvert hello above too`CTAS` is quite straight-forward:</span></span>

```sql
CREATE TABLE [dbo].[FactInternetSales_new]
WITH
(
    DISTRIBUTION = ROUND_ROBIN
,   CLUSTERED COLUMNSTORE INDEX
)
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
;
```

<span data-ttu-id="f1943-115">Com `CTAS` são toochange capaz de ambos Olá distribuição de dados da tabela Olá, bem como o tipo de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-115">With `CTAS` you are able toochange both hello distribution of hello table data as well as hello table type.</span></span> 

> [!NOTE]
> <span data-ttu-id="f1943-116">Se apenas estiver a tentar o índice de Olá toochange na sua `CTAS` operação e Olá tabela de origem é hash distribuída, em seguida, o `CTAS` irão efetuar a operação melhor se mantém Olá mesmo tipo de coluna e os dados de distribuição.</span><span class="sxs-lookup"><span data-stu-id="f1943-116">If you are only trying toochange hello index in your `CTAS` operation and hello source table is hash distributed then your `CTAS` operation will perform best if you maintain hello same distribution column and data type.</span></span> <span data-ttu-id="f1943-117">Evitará cruzada movimento de dados de distribuição durante a operação de Olá que é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="f1943-117">This will avoid cross distribution data movement during hello operation which is more efficient.</span></span>
> 
> 

## <a name="using-ctas-toocopy-a-table"></a><span data-ttu-id="f1943-118">Utilizar CTAS toocopy uma tabela</span><span class="sxs-lookup"><span data-stu-id="f1943-118">Using CTAS toocopy a table</span></span>
<span data-ttu-id="f1943-119">Talvez utiliza um dos Olá mais comuns de `CTAS` está a criar uma cópia de uma tabela para que possa alterar Olá DDL.</span><span class="sxs-lookup"><span data-stu-id="f1943-119">Perhaps one of hello most common uses of `CTAS` is creating a copy of a table so that you can change hello DDL.</span></span> <span data-ttu-id="f1943-120">Se, por exemplo, que criou originalmente a tabela como `ROUND_ROBIN` e agora pretende alterá-la tooa tabela distribuídas numa coluna, `CTAS` é a forma como iria alterar uma coluna de distribuição Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-120">If for example you originally created your table as `ROUND_ROBIN` and now want change it tooa table distributed on a column, `CTAS` is how you would change hello distribution column.</span></span> <span data-ttu-id="f1943-121">`CTAS`Também pode ser o toochange utilizado tipos de criação de partições, indexar ou coluna.</span><span class="sxs-lookup"><span data-stu-id="f1943-121">`CTAS` can also be used toochange partitioning, indexing, or column types.</span></span>

<span data-ttu-id="f1943-122">Digamos que criou esta tabela utilizando o tipo de distribuição predefinido Olá de `ROUND_ROBIN` distribuído, uma vez que não existe nenhuma coluna de distribuição foi especificada na Olá `CREATE TABLE`.</span><span class="sxs-lookup"><span data-stu-id="f1943-122">Let's say you created this table using hello default distribution type of `ROUND_ROBIN` distributed since no distribution column was specified in hello `CREATE TABLE`.</span></span>

```sql
CREATE TABLE FactInternetSales
(
    ProductKey int NOT NULL,
    OrderDateKey int NOT NULL,
    DueDateKey int NOT NULL,
    ShipDateKey int NOT NULL,
    CustomerKey int NOT NULL,
    PromotionKey int NOT NULL,
    CurrencyKey int NOT NULL,
    SalesTerritoryKey int NOT NULL,
    SalesOrderNumber nvarchar(20) NOT NULL,
    SalesOrderLineNumber tinyint NOT NULL,
    RevisionNumber tinyint NOT NULL,
    OrderQuantity smallint NOT NULL,
    UnitPrice money NOT NULL,
    ExtendedAmount money NOT NULL,
    UnitPriceDiscountPct float NOT NULL,
    DiscountAmount float NOT NULL,
    ProductStandardCost money NOT NULL,
    TotalProductCost money NOT NULL,
    SalesAmount money NOT NULL,
    TaxAmt money NOT NULL,
    Freight money NOT NULL,
    CarrierTrackingNumber nvarchar(25),
    CustomerPONumber nvarchar(25)
);
```

<span data-ttu-id="f1943-123">Agora pretende toocreate uma nova cópia desta tabela com um índice de Columnstore em cluster, de modo a que pode tirar partido de desempenho de Olá das tabelas Columnstore em cluster.</span><span class="sxs-lookup"><span data-stu-id="f1943-123">Now you want toocreate a new copy of this table with a Clustered Columnstore Index so that you can take advantage of hello performance of Clustered Columnstore tables.</span></span> <span data-ttu-id="f1943-124">Também deve toodistribute esta tabela em ProductKey uma vez que são prevendo associações nesta coluna e pretender tooavoid movimento de dados durante as associações no ProductKey.</span><span class="sxs-lookup"><span data-stu-id="f1943-124">You also want toodistribute this table on ProductKey since you are anticipating joins on this column and want tooavoid data movement during joins on ProductKey.</span></span> <span data-ttu-id="f1943-125">Por último, também é aconselhável tooadd a criação de partições no OrderDateKey para que rapidamente pode eliminar dados antigos, arrastando partições antigas.</span><span class="sxs-lookup"><span data-stu-id="f1943-125">Lastly you also want tooadd partitioning on OrderDateKey so that you can quickly delete old data by dropping old partitions.</span></span> <span data-ttu-id="f1943-126">Segue-se a instrução de CTAS Olá que seria copie a tabela antiga para uma nova tabela.</span><span class="sxs-lookup"><span data-stu-id="f1943-126">Here is hello CTAS statement which would copy your old table into a new table.</span></span>

```sql
CREATE TABLE FactInternetSales_new
WITH
(
    CLUSTERED COLUMNSTORE INDEX,
    DISTRIBUTION = HASH(ProductKey),
    PARTITION
    (
        OrderDateKey RANGE RIGHT FOR VALUES
        (
        20000101,20010101,20020101,20030101,20040101,20050101,20060101,20070101,20080101,20090101,
        20100101,20110101,20120101,20130101,20140101,20150101,20160101,20170101,20180101,20190101,
        20200101,20210101,20220101,20230101,20240101,20250101,20260101,20270101,20280101,20290101
        )
    )
)
AS SELECT * FROM FactInternetSales;
```

<span data-ttu-id="f1943-127">Por fim, pode mudar o nome do seu tooswap tabelas na sua nova tabela e, em seguida, remover a tabela antiga.</span><span class="sxs-lookup"><span data-stu-id="f1943-127">Finally you can rename your tables tooswap in your new table and then drop your old table.</span></span>

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> <span data-ttu-id="f1943-128">O Azure SQL Data Warehouse ainda não suporta a criação ou atualização automática de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="f1943-128">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="f1943-129">Na ordem tooget Olá melhor desempenho das consultas, é importante que sejam criadas estatísticas em todas as colunas de todas as tabelas após o primeiro carregamento de Olá ou ocorrerem quaisquer alterações substanciais nos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-129">In order tooget hello best performance from your queries, it's important that statistics be created on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="f1943-130">Para obter uma explicação detalhada das estatísticas, consulte Olá [estatísticas] [ Statistics] tópico, no grupo de tópicos desenvolver de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-130">For a detailed explanation of statistics, see hello [Statistics][Statistics] topic in hello Develop group of topics.</span></span>
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a><span data-ttu-id="f1943-131">Utilizar CTAS toowork em torno de funcionalidades não suportadas</span><span class="sxs-lookup"><span data-stu-id="f1943-131">Using CTAS toowork around unsupported features</span></span>
<span data-ttu-id="f1943-132">`CTAS`Também pode ser utilizado toowork em torno de um número de funcionalidades de Olá não suportado listados abaixo.</span><span class="sxs-lookup"><span data-stu-id="f1943-132">`CTAS` can also be used toowork around a number of hello unsupported features listed below.</span></span> <span data-ttu-id="f1943-133">Isto pode frequentemente provar toobe uma situação de win/win como não apenas o código estarão em conformidade, mas são, muitas vezes, executados mais rapidamente no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="f1943-133">This can often prove toobe a win/win situation as not only will your code be compliant but it will often execute faster on SQL Data Warehouse.</span></span> <span data-ttu-id="f1943-134">Trata-se como resultado da respetiva estrutura parallelized completamente.</span><span class="sxs-lookup"><span data-stu-id="f1943-134">This is as a result of its fully parallelized design.</span></span> <span data-ttu-id="f1943-135">Os cenários que podem ser trabalhados em torno com CTAS incluem:</span><span class="sxs-lookup"><span data-stu-id="f1943-135">Scenarios that can be worked around with CTAS include:</span></span>

* <span data-ttu-id="f1943-136">ASSOCIAÇÕES de ANSI nas atualizações</span><span class="sxs-lookup"><span data-stu-id="f1943-136">ANSI JOINS on UPDATEs</span></span>
* <span data-ttu-id="f1943-137">Associações de ANSI em eliminações</span><span class="sxs-lookup"><span data-stu-id="f1943-137">ANSI JOINs on DELETEs</span></span>
* <span data-ttu-id="f1943-138">Declaração de intercalação</span><span class="sxs-lookup"><span data-stu-id="f1943-138">MERGE statement</span></span>

> [!NOTE]
> <span data-ttu-id="f1943-139">Tente toothink "CTAS primeiro".</span><span class="sxs-lookup"><span data-stu-id="f1943-139">Try toothink "CTAS first".</span></span> <span data-ttu-id="f1943-140">Se pensa que pode resolver um problema utilizando `CTAS` , em seguida, que é, geralmente, Olá melhor forma tooapproach-lo -, mesmo que o se estiver a escrever mais dados como resultado.</span><span class="sxs-lookup"><span data-stu-id="f1943-140">If you think you can solve a problem using `CTAS` then that is generally hello best way tooapproach it - even if you are writing more data as a result.</span></span>
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a><span data-ttu-id="f1943-141">Substituição de associação de ANSI para instruções update</span><span class="sxs-lookup"><span data-stu-id="f1943-141">ANSI join replacement for update statements</span></span>
<span data-ttu-id="f1943-142">Pode considerar que tem uma atualização complexa que associa mais de duas tabelas utilizando ANSI associar Olá de tooperform sintaxe UPDATE ou DELETE.</span><span class="sxs-lookup"><span data-stu-id="f1943-142">You may find you have a complex update that joins more than two tables together using ANSI joining syntax tooperform hello UPDATE or DELETE.</span></span>

<span data-ttu-id="f1943-143">Imagine que tinha tooupdate nesta tabela:</span><span class="sxs-lookup"><span data-stu-id="f1943-143">Imagine you had tooupdate this table:</span></span>

```sql
CREATE TABLE [dbo].[AnnualCategorySales]
(    [EnglishProductCategoryName]    NVARCHAR(50)    NOT NULL
,    [CalendarYear]                    SMALLINT        NOT NULL
,    [TotalSalesAmount]                MONEY            NOT NULL
)
WITH
(
    DISTRIBUTION = ROUND_ROBIN
)
;
```

<span data-ttu-id="f1943-144">poderá ter comparados consulta original Olá algo semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="f1943-144">hello original query might have looked something like this:</span></span>

```sql
UPDATE    acs
SET        [TotalSalesAmount] = [fis].[TotalSalesAmount]
FROM    [dbo].[AnnualCategorySales]     AS acs
JOIN    (
        SELECT    [EnglishProductCategoryName]
        ,        [CalendarYear]
        ,        SUM([SalesAmount])                AS [TotalSalesAmount]
        FROM    [dbo].[FactInternetSales]        AS s
        JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
        JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
        JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
        JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
        WHERE     [CalendarYear] = 2004
        GROUP BY
                [EnglishProductCategoryName]
        ,        [CalendarYear]
        ) AS fis
ON    [acs].[EnglishProductCategoryName]    = [fis].[EnglishProductCategoryName]
AND    [acs].[CalendarYear]                = [fis].[CalendarYear]
;
```

<span data-ttu-id="f1943-145">Uma vez que não suporta o SQL Data Warehouse ANSI associações na Olá `FROM` cláusula de um `UPDATE` declaração, não é possível copiar este código de ativação pós-falha sem ligeiramente a alteração.</span><span class="sxs-lookup"><span data-stu-id="f1943-145">Since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of an `UPDATE` statement, you cannot copy this code over without changing it slightly.</span></span>

<span data-ttu-id="f1943-146">Pode utilizar uma combinação de um `CTAS` e uma implícita associar tooreplace este código:</span><span class="sxs-lookup"><span data-stu-id="f1943-146">You can use a combination of a `CTAS` and an implicit join tooreplace this code:</span></span>

```sql
-- Create an interim table
CREATE TABLE CTAS_acs
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT    ISNULL(CAST([EnglishProductCategoryName] AS NVARCHAR(50)),0)    AS [EnglishProductCategoryName]
,        ISNULL(CAST([CalendarYear] AS SMALLINT),0)                         AS [CalendarYear]
,        ISNULL(CAST(SUM([SalesAmount]) AS MONEY),0)                        AS [TotalSalesAmount]
FROM    [dbo].[FactInternetSales]        AS s
JOIN    [dbo].[DimDate]                    AS d    ON s.[OrderDateKey]                = d.[DateKey]
JOIN    [dbo].[DimProduct]                AS p    ON s.[ProductKey]                = p.[ProductKey]
JOIN    [dbo].[DimProductSubCategory]    AS u    ON p.[ProductSubcategoryKey]    = u.[ProductSubcategoryKey]
JOIN    [dbo].[DimProductCategory]        AS c    ON u.[ProductCategoryKey]        = c.[ProductCategoryKey]
WHERE     [CalendarYear] = 2004
GROUP BY
        [EnglishProductCategoryName]
,        [CalendarYear]
;

-- Use an implicit join tooperform hello update
UPDATE  AnnualCategorySales
SET     AnnualCategorySales.TotalSalesAmount = CTAS_ACS.TotalSalesAmount
FROM    CTAS_acs
WHERE   CTAS_acs.[EnglishProductCategoryName] = AnnualCategorySales.[EnglishProductCategoryName]
AND     CTAS_acs.[CalendarYear]               = AnnualCategorySales.[CalendarYear]
;

--Drop hello interim table
DROP TABLE CTAS_acs
;
```

## <a name="ansi-join-replacement-for-delete-statements"></a><span data-ttu-id="f1943-147">Substituição de associação de ANSI para eliminar instruções</span><span class="sxs-lookup"><span data-stu-id="f1943-147">ANSI join replacement for delete statements</span></span>
<span data-ttu-id="f1943-148">Por vezes, a abordagem das melhores Olá à eliminação de dados é toouse `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="f1943-148">Sometimes hello best approach for deleting data is toouse `CTAS`.</span></span> <span data-ttu-id="f1943-149">Em vez de eliminar dados de Olá simplesmente seleciona os dados de Olá pretende tookeep.</span><span class="sxs-lookup"><span data-stu-id="f1943-149">Rather than deleting hello data simply select hello data you want tookeep.</span></span> <span data-ttu-id="f1943-150">Este particularmente verdadeiro para `DELETE` instruções que utilizar ansi associar sintaxe, uma vez que o SQL Data Warehouse não suporta associações ANSI no Olá `FROM` cláusula de um `DELETE` instrução.</span><span class="sxs-lookup"><span data-stu-id="f1943-150">This especially true for `DELETE` statements that use ansi joining syntax since SQL Data Warehouse does not support ANSI joins in hello `FROM` clause of a `DELETE` statement.</span></span>

<span data-ttu-id="f1943-151">Um exemplo de uma instrução DELETE convertida está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="f1943-151">An example of a converted DELETE statement is available below:</span></span>

```sql
CREATE TABLE dbo.DimProduct_upsert
WITH
(   Distribution=HASH(ProductKey)
,   CLUSTERED INDEX (ProductKey)
)
AS -- Select Data you wish tookeep
SELECT     p.ProductKey
,          p.EnglishProductName
,          p.Color
FROM       dbo.DimProduct p
RIGHT JOIN dbo.stg_DimProduct s
ON         p.ProductKey = s.ProductKey
;

RENAME OBJECT dbo.DimProduct        tooDimProduct_old;
RENAME OBJECT dbo.DimProduct_upsert tooDimProduct;
```

## <a name="replace-merge-statements"></a><span data-ttu-id="f1943-152">Substitua as instruções de intercalação</span><span class="sxs-lookup"><span data-stu-id="f1943-152">Replace merge statements</span></span>
<span data-ttu-id="f1943-153">Instruções Merge podem ser substituídas, pelo menos, parte, utilizando `CTAS`.</span><span class="sxs-lookup"><span data-stu-id="f1943-153">Merge statements can be replaced, at least in part, by using `CTAS`.</span></span> <span data-ttu-id="f1943-154">Pode consolidar Olá `INSERT` e Olá `UPDATE` para uma instrução única.</span><span class="sxs-lookup"><span data-stu-id="f1943-154">You can consolidate hello `INSERT` and hello `UPDATE` into a single statement.</span></span> <span data-ttu-id="f1943-155">Quaisquer registos eliminados teria toobe fechado desativar numa instrução segundo.</span><span class="sxs-lookup"><span data-stu-id="f1943-155">Any deleted records would need toobe closed off in a second statement.</span></span>

<span data-ttu-id="f1943-156">Um exemplo de um `UPSERT` está disponível abaixo:</span><span class="sxs-lookup"><span data-stu-id="f1943-156">An example of an `UPSERT` is available below:</span></span>

```sql
CREATE TABLE dbo.[DimProduct_upsert]
WITH
(   DISTRIBUTION = HASH([ProductKey])
,   CLUSTERED INDEX ([ProductKey])
)
AS
-- New rows and new versions of rows
SELECT      s.[ProductKey]
,           s.[EnglishProductName]
,           s.[Color]
FROM      dbo.[stg_DimProduct] AS s
UNION ALL  
-- Keep rows that are not being touched
SELECT      p.[ProductKey]
,           p.[EnglishProductName]
,           p.[Color]
FROM      dbo.[DimProduct] AS p
WHERE NOT EXISTS
(   SELECT  *
    FROM    [dbo].[stg_DimProduct] s
    WHERE   s.[ProductKey] = p.[ProductKey]
)
;

RENAME OBJECT dbo.[DimProduct]          too[DimProduct_old];
RENAME OBJECT dbo.[DimpProduct_upsert]  too[DimProduct];

```

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a><span data-ttu-id="f1943-157">Recomendação CTAS: Estado explicitamente o tipo de dados e nulidade da saída</span><span class="sxs-lookup"><span data-stu-id="f1943-157">CTAS recommendation: Explicitly state data type and nullability of output</span></span>
<span data-ttu-id="f1943-158">Quando migrar código poderá achar que sejam executadas neste tipo de codificação padrão:</span><span class="sxs-lookup"><span data-stu-id="f1943-158">When migrating code you might find you run across this type of coding pattern:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE result
(result DECIMAL(7,2) NOT NULL
)
WITH (DISTRIBUTION = ROUND_ROBIN)

INSERT INTO result
SELECT @d*@f
;
```

<span data-ttu-id="f1943-159">Instinctively se pensa deve migrar tooa este código CTAS e será correto.</span><span class="sxs-lookup"><span data-stu-id="f1943-159">Instinctively you might think you should migrate this code tooa CTAS and you would be correct.</span></span> <span data-ttu-id="f1943-160">No entanto, há um problema oculto aqui.</span><span class="sxs-lookup"><span data-stu-id="f1943-160">However, there is a hidden issue here.</span></span>

<span data-ttu-id="f1943-161">Olá seguinte código não produzir Olá o mesmo resultado:</span><span class="sxs-lookup"><span data-stu-id="f1943-161">hello following code does NOT yield hello same result:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455
;

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT @d*@f as result
;
```

<span data-ttu-id="f1943-162">Tenha em atenção que o resultado"Olá coluna" reencaminhar acarreta Olá tipo e nulidade valores de dados de expressão Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-162">Notice that hello column "result" carries forward hello data type and nullability values of hello expression.</span></span> <span data-ttu-id="f1943-163">Isto pode levar a variações de toosubtle como valores, se não tenha o cuidado.</span><span class="sxs-lookup"><span data-stu-id="f1943-163">This can lead toosubtle variances in values if you aren't careful.</span></span>

<span data-ttu-id="f1943-164">Tente Olá passos seguintes como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="f1943-164">Try hello following as an example:</span></span>

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

<span data-ttu-id="f1943-165">valor de Olá armazenado para o resultado é diferente.</span><span class="sxs-lookup"><span data-stu-id="f1943-165">hello value stored for result is different.</span></span> <span data-ttu-id="f1943-166">Como hello persistente valor na coluna de resultado Olá é utilizado em outro erro de Olá expressões fica ainda mais significativo.</span><span class="sxs-lookup"><span data-stu-id="f1943-166">As hello persisted value in hello result column is used in other expressions hello error becomes even more significant.</span></span>

![][1]

<span data-ttu-id="f1943-167">Isto é particularmente importante para migrações de dados.</span><span class="sxs-lookup"><span data-stu-id="f1943-167">This is particularly important for data migrations.</span></span> <span data-ttu-id="f1943-168">Apesar de consulta segundo Olá é possivelmente mais exata há um problema.</span><span class="sxs-lookup"><span data-stu-id="f1943-168">Even though hello second query is arguably more accurate there is a problem.</span></span> <span data-ttu-id="f1943-169">dados de Olá seria toohello diferentes em comparação com sistema de origem e que servem como tooquestions de integridade na migração Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-169">hello data would be different compared toohello source system and that leads tooquestions of integrity in hello migration.</span></span> <span data-ttu-id="f1943-170">Este é um dos casos raros onde resposta "errado" Olá é, efetivamente, direito de Olá um!</span><span class="sxs-lookup"><span data-stu-id="f1943-170">This is one of those rare cases where hello "wrong" answer is actually hello right one!</span></span>

<span data-ttu-id="f1943-171">Olá razão vemos este disparidade entre resultados Olá dois está inativo tooimplicit escreva conversão.</span><span class="sxs-lookup"><span data-stu-id="f1943-171">hello reason we see this disparity between hello two results is down tooimplicit type casting.</span></span> <span data-ttu-id="f1943-172">No Olá primeira tabela do exemplo Olá define a definição da coluna Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-172">In hello first example hello table defines hello column definition.</span></span> <span data-ttu-id="f1943-173">Quando é inserida linha Olá ocorre uma conversão de tipo implícito.</span><span class="sxs-lookup"><span data-stu-id="f1943-173">When hello row is inserted an implicit type conversion occurs.</span></span> <span data-ttu-id="f1943-174">No segundo exemplo de Olá não há nenhuma conversão de tipo implícito expressão Olá define o tipo de dados da coluna de Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-174">In hello second example there is no implicit type conversion as hello expression defines data type of hello column.</span></span> <span data-ttu-id="f1943-175">Repare que também essa coluna Olá no segundo exemplo de Olá foi definida como uma coluna de tipo nulo enquanto no primeiro exemplo de Olá não tem.</span><span class="sxs-lookup"><span data-stu-id="f1943-175">Notice also that hello column in hello second example has been defined as a NULLable column whereas in hello first example it has not.</span></span> <span data-ttu-id="f1943-176">Quando a tabela de Olá foi criada no nulidade de coluna de exemplo Olá primeiro explicitamente foi definida.</span><span class="sxs-lookup"><span data-stu-id="f1943-176">When hello table was created in hello first example column nullability was explicitly defined.</span></span> <span data-ttu-id="f1943-177">No segundo exemplo de Olá toohello expressão apenas foi deixada e por predefinição este resultaria numa definição de um valor nulo.</span><span class="sxs-lookup"><span data-stu-id="f1943-177">In hello second example it was just left toohello expression and by default this would result in a NULL definition.</span></span>  

<span data-ttu-id="f1943-178">tooresolve estes problemas que tem de definir explicitamente a conversão de tipo Olá e permissão de valores NULL na Olá `SELECT` parte Olá `CTAS` instrução.</span><span class="sxs-lookup"><span data-stu-id="f1943-178">tooresolve these issues you must explicitly set hello type conversion and nullability in hello `SELECT` portion of hello `CTAS` statement.</span></span> <span data-ttu-id="f1943-179">Não é possível definir estas propriedades no Olá criar parte da tabela.</span><span class="sxs-lookup"><span data-stu-id="f1943-179">You cannot set these properties in hello create table part.</span></span>

<span data-ttu-id="f1943-180">exemplo de Olá abaixo demonstra como toofix Olá código:</span><span class="sxs-lookup"><span data-stu-id="f1943-180">hello example below demonstrates how toofix hello code:</span></span>

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

<span data-ttu-id="f1943-181">Tenha em atenção o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="f1943-181">Note hello following:</span></span>

* <span data-ttu-id="f1943-182">CAST ou CONVERT foi foram utilizado</span><span class="sxs-lookup"><span data-stu-id="f1943-182">CAST or CONVERT could have been used</span></span>
* <span data-ttu-id="f1943-183">ISNULL é utilizado tooforce nulidade não COALESCE</span><span class="sxs-lookup"><span data-stu-id="f1943-183">ISNULL is used tooforce NULLability not COALESCE</span></span>
* <span data-ttu-id="f1943-184">ISNULL é função mais exterior Olá</span><span class="sxs-lookup"><span data-stu-id="f1943-184">ISNULL is hello outermost function</span></span>
* <span data-ttu-id="f1943-185">Olá segunda parte Olá ISNULL é uma constante ou seja, 0</span><span class="sxs-lookup"><span data-stu-id="f1943-185">hello second part of hello ISNULL is a constant i.e. 0</span></span>

> [!NOTE]
> <span data-ttu-id="f1943-186">Para Olá nulidade toobe definido corretamente, é vital toouse `ISNULL` e não `COALESCE`.</span><span class="sxs-lookup"><span data-stu-id="f1943-186">For hello nullability toobe correctly set it is vital toouse `ISNULL` and not `COALESCE`.</span></span> <span data-ttu-id="f1943-187">`COALESCE`Não é uma função determinista e, por isso, o resultado de Olá da expressão de Olá será sempre NULLable.</span><span class="sxs-lookup"><span data-stu-id="f1943-187">`COALESCE` is not a deterministic function and so hello result of hello expression will always be NULLable.</span></span> <span data-ttu-id="f1943-188">`ISNULL`é diferente.</span><span class="sxs-lookup"><span data-stu-id="f1943-188">`ISNULL` is different.</span></span> <span data-ttu-id="f1943-189">É determinística.</span><span class="sxs-lookup"><span data-stu-id="f1943-189">It is deterministic.</span></span> <span data-ttu-id="f1943-190">Por conseguinte Olá quando a segunda parte do Olá `ISNULL` função é uma constante ou um literal, em seguida, o valor resultante Olá irá ser não nulo.</span><span class="sxs-lookup"><span data-stu-id="f1943-190">Therefore when hello second part of hello `ISNULL` function is a constant or a literal then hello resulting value will be NOT NULL.</span></span>
> 
> 

<span data-ttu-id="f1943-191">Não é apenas útil para assegurar a integridade de Olá dos seus cálculos desta sugestão.</span><span class="sxs-lookup"><span data-stu-id="f1943-191">This tip is not just useful for ensuring hello integrity of your calculations.</span></span> <span data-ttu-id="f1943-192">Também é importante para a mudança de partições de tabela.</span><span class="sxs-lookup"><span data-stu-id="f1943-192">It is also important for table partition switching.</span></span> <span data-ttu-id="f1943-193">Imagine que tiver esta tabela definida como o facto:</span><span class="sxs-lookup"><span data-stu-id="f1943-193">Imagine you have this table defined as your fact:</span></span>

```sql
CREATE TABLE [dbo].[Sales]
(
    [date]      INT     NOT NULL
,   [product]   INT     NOT NULL
,   [store]     INT     NOT NULL
,   [quantity]  INT     NOT NULL
,   [price]     MONEY   NOT NULL
,   [amount]    MONEY   NOT NULL
)
WITH
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

<span data-ttu-id="f1943-194">No entanto, o campo de valor de Olá é uma expressão calculada não faz parte de dados de origem Olá.</span><span class="sxs-lookup"><span data-stu-id="f1943-194">However, hello value field is a calculated expression it is not part of hello source data.</span></span>

<span data-ttu-id="f1943-195">toocreate o conjunto de dados particionado poderá toodo isto:</span><span class="sxs-lookup"><span data-stu-id="f1943-195">toocreate your partitioned dataset you might want toodo this:</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   [quantity]*[price]  AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create')
;
```

<span data-ttu-id="f1943-196">consulta de Olá executaria perfeitamente adequada.</span><span class="sxs-lookup"><span data-stu-id="f1943-196">hello query would run perfectly fine.</span></span> <span data-ttu-id="f1943-197">problema de Olá vem quando tenta mudança de partições de Olá tooperform.</span><span class="sxs-lookup"><span data-stu-id="f1943-197">hello problem comes when you try tooperform hello partition switch.</span></span> <span data-ttu-id="f1943-198">definições de tabela Olá não correspondem.</span><span class="sxs-lookup"><span data-stu-id="f1943-198">hello table definitions do not match.</span></span> <span data-ttu-id="f1943-199">definições de tabela de Olá toomake correspondem Olá que CTAS tem toobe modificado.</span><span class="sxs-lookup"><span data-stu-id="f1943-199">toomake hello table definitions match hello CTAS needs toobe modified.</span></span>

```sql
CREATE TABLE [dbo].[Sales_in]
WITH    
(   DISTRIBUTION = HASH([product])
,   PARTITION   (   [date] RANGE RIGHT FOR VALUES
                    (20000101,20010101
                    )
                )
)
AS
SELECT
    [date]    
,   [product]
,   [store]
,   [quantity]
,   [price]   
,   ISNULL(CAST([quantity]*[price] AS MONEY),0) AS [amount]
FROM [stg].[source]
OPTION (LABEL = 'CTAS : Partition IN table : Create');
```

<span data-ttu-id="f1943-200">Pode ver, por conseguinte, que tipo de consistência e a manutenção nulidade as propriedades de um CTAS é uma boa prática engenharia.</span><span class="sxs-lookup"><span data-stu-id="f1943-200">You can see therefore that type consistency and maintaining nullability properties on a CTAS is a good engineering best practice.</span></span> <span data-ttu-id="f1943-201">-Ajuda a integridade toomaintain nos seus cálculos e também garante que é possível comutar a partição.</span><span class="sxs-lookup"><span data-stu-id="f1943-201">It helps toomaintain integrity in your calculations and also ensures that partition switching is possible.</span></span>

<span data-ttu-id="f1943-202">Consulte tooMSDN para obter mais informações sobre como utilizar [CTAS][CTAS].</span><span class="sxs-lookup"><span data-stu-id="f1943-202">Please refer tooMSDN for more information on using [CTAS][CTAS].</span></span> <span data-ttu-id="f1943-203">É uma das instruções mais importantes de Olá no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f1943-203">It is one of hello most important statements in Azure SQL Data Warehouse.</span></span> <span data-ttu-id="f1943-204">Certifique-se que compreender exaustivamente.</span><span class="sxs-lookup"><span data-stu-id="f1943-204">Make sure you thoroughly understand it.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f1943-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f1943-205">Next steps</span></span>
<span data-ttu-id="f1943-206">Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="f1943-206">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
