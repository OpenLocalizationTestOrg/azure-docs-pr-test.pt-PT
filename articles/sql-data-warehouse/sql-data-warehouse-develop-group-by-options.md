---
title: "aaaGroup pelas opções no SQL Data Warehouse | Microsoft Docs"
description: "Sugestões para implementar o grupo por opções no Azure SQL Data Warehouse para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f95a1e43-768f-4b7b-8a10-8a0509d0c871
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: cc443c2af4e3ef2babd74d78aa6fb57bb3c1c7ea
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="group-by-options-in-sql-data-warehouse"></a><span data-ttu-id="92866-103">Agrupar por opções no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="92866-103">Group by options in SQL Data Warehouse</span></span>
<span data-ttu-id="92866-104">Olá [GROUP BY] [ GROUP BY] é utilizar a cláusula set resumo do tooaggregate dados tooa de linhas.</span><span class="sxs-lookup"><span data-stu-id="92866-104">hello [GROUP BY][GROUP BY] clause is used tooaggregate data tooa summary set of rows.</span></span> <span data-ttu-id="92866-105">Também tem algumas opções que expandem a funcionalidade de toobe essa necessidade trabalhado em torno como não são suportados diretamente ao Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="92866-105">It also has a few options that extend it's functionality that need toobe worked around as they are not directly supported by Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="92866-106">Estas opções são</span><span class="sxs-lookup"><span data-stu-id="92866-106">These options are</span></span>

* <span data-ttu-id="92866-107">GROUP BY com ROLLUP</span><span class="sxs-lookup"><span data-stu-id="92866-107">GROUP BY with ROLLUP</span></span>
* <span data-ttu-id="92866-108">CONJUNTOS DE AGRUPAMENTO</span><span class="sxs-lookup"><span data-stu-id="92866-108">GROUPING SETS</span></span>
* <span data-ttu-id="92866-109">GROUP BY cubo</span><span class="sxs-lookup"><span data-stu-id="92866-109">GROUP BY with CUBE</span></span>

## <a name="rollup-and-grouping-sets-options"></a><span data-ttu-id="92866-110">Rollup e grouping define as opções</span><span class="sxs-lookup"><span data-stu-id="92866-110">Rollup and grouping sets options</span></span>
<span data-ttu-id="92866-111">Olá aqui a opção mais simples é toouse `UNION ALL` em vez disso, tooperform Olá rollup, em vez de depender Olá sintaxe explícita.</span><span class="sxs-lookup"><span data-stu-id="92866-111">hello simplest option here is toouse `UNION ALL` instead tooperform hello rollup rather than relying on hello explicit syntax.</span></span> <span data-ttu-id="92866-112">resultado de Olá é exatamente Olá mesmo</span><span class="sxs-lookup"><span data-stu-id="92866-112">hello result is exactly hello same</span></span>

<span data-ttu-id="92866-113">Segue-se um exemplo de um grupo pela instrução utilizando Olá `ROLLUP` opção:</span><span class="sxs-lookup"><span data-stu-id="92866-113">Below is an example of a group by statement using hello `ROLLUP` option:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount)             AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t       ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY ROLLUP (
                        [SalesTerritoryCountry]
                ,       [SalesTerritoryRegion]
                )
;
```

<span data-ttu-id="92866-114">Através da utilização de agregação, iremos pediu Olá agregações os seguintes:</span><span class="sxs-lookup"><span data-stu-id="92866-114">By using ROLLUP we have requested hello following aggregations:</span></span>

* <span data-ttu-id="92866-115">País e região</span><span class="sxs-lookup"><span data-stu-id="92866-115">Country and Region</span></span>
* <span data-ttu-id="92866-116">País</span><span class="sxs-lookup"><span data-stu-id="92866-116">Country</span></span>
* <span data-ttu-id="92866-117">Total geral</span><span class="sxs-lookup"><span data-stu-id="92866-117">Grand Total</span></span>

<span data-ttu-id="92866-118">tooreplace isto, terá de toouse `UNION ALL`; especificar agregações Olá necessárias explicitamente tooreturn Olá mesmos resultados:</span><span class="sxs-lookup"><span data-stu-id="92866-118">tooreplace this you will need toouse `UNION ALL`; specifying hello aggregations required explicitly tooreturn hello same results:</span></span>

```sql
SELECT [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
,      [SalesTerritoryRegion]
UNION ALL
SELECT [SalesTerritoryCountry]
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey
GROUP BY
       [SalesTerritoryCountry]
UNION ALL
SELECT NULL
,      NULL
,      SUM(SalesAmount) AS TotalSalesAmount
FROM  dbo.factInternetSales s
JOIN  dbo.DimSalesTerritory t     ON s.SalesTerritoryKey       = t.SalesTerritoryKey;
```

<span data-ttu-id="92866-119">Para GROUPING SETS precisamos apenas toodo é que adotar Olá mesmo principal, mas só criar secções UNION ALL para Olá níveis de agregação queremos toosee</span><span class="sxs-lookup"><span data-stu-id="92866-119">For GROUPING SETS all we need toodo is adopt hello same principal but only create UNION ALL sections for hello aggregation levels we want toosee</span></span>

## <a name="cube-options"></a><span data-ttu-id="92866-120">Opções do cubo</span><span class="sxs-lookup"><span data-stu-id="92866-120">Cube options</span></span>
<span data-ttu-id="92866-121">É possível toocreate um grupo por com cubo utilizando abordagem UNION ALL Olá.</span><span class="sxs-lookup"><span data-stu-id="92866-121">It is possible toocreate a GROUP BY WITH CUBE using hello UNION ALL approach.</span></span> <span data-ttu-id="92866-122">problema de Olá é que o código de Olá pode rapidamente tornar-se complexa e unwieldy.</span><span class="sxs-lookup"><span data-stu-id="92866-122">hello problem is that hello code can quickly become cumbersome and unwieldy.</span></span> <span data-ttu-id="92866-123">toomitigate isto, pode utilizar este mais avançadas abordagem.</span><span class="sxs-lookup"><span data-stu-id="92866-123">toomitigate this you can use this more advanced approach.</span></span>

<span data-ttu-id="92866-124">Vamos utilizar o exemplo de Olá acima.</span><span class="sxs-lookup"><span data-stu-id="92866-124">Let's use hello example above.</span></span>

<span data-ttu-id="92866-125">Step-by-Olá primeiro passo é toodefine Olá 'cube', que define todos os níveis de Olá de agregação que queremos toocreate.</span><span class="sxs-lookup"><span data-stu-id="92866-125">hello first step is toodefine hello 'cube' that defines all hello levels of aggregation that we want toocreate.</span></span> <span data-ttu-id="92866-126">É importante tootake nota Olá CROSS JOIN de duas tabelas derivadas de Olá.</span><span class="sxs-lookup"><span data-stu-id="92866-126">It is important tootake note of hello CROSS JOIN of hello two derived tables.</span></span> <span data-ttu-id="92866-127">Isto gera todos os níveis de Olá para-nos.</span><span class="sxs-lookup"><span data-stu-id="92866-127">This generates all hello levels for us.</span></span> <span data-ttu-id="92866-128">rest Olá de código Olá existe realmente para formatação.</span><span class="sxs-lookup"><span data-stu-id="92866-128">hello rest of hello code is really there for formatting.</span></span>

```sql
CREATE TABLE #Cube
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
AS
WITH GrpCube AS
(SELECT    CAST(ISNULL(Country,'NULL')+','+ISNULL(Region,'NULL') AS NVARCHAR(50)) as 'Cols'
,          CAST(ISNULL(Country+',','')+ISNULL(Region,'') AS NVARCHAR(50))  as 'GroupBy'
,          ROW_NUMBER() OVER (ORDER BY Country) as 'Seq'
FROM       ( SELECT 'SalesTerritoryCountry' as Country
             UNION ALL
             SELECT NULL
           ) c
CROSS JOIN ( SELECT 'SalesTerritoryRegion' as Region
             UNION ALL
             SELECT NULL
           ) r
)
SELECT Cols
,      CASE WHEN SUBSTRING(GroupBy,LEN(GroupBy),1) = ','
            THEN SUBSTRING(GroupBy,1,LEN(GroupBy)-1)
            ELSE GroupBy
       END AS GroupBy  --Remove Trailing Comma
,Seq
FROM GrpCube;
```

<span data-ttu-id="92866-129">Olá os resultados da Olá CTAS podem ser vistos abaixo:</span><span class="sxs-lookup"><span data-stu-id="92866-129">hello results of hello CTAS can be seen below:</span></span>

![][1]

<span data-ttu-id="92866-130">segundo passo de Olá é toospecify que resulta de um provisório de toostore de tabela de destino:</span><span class="sxs-lookup"><span data-stu-id="92866-130">hello second step is toospecify a target table toostore interim results:</span></span>

```sql
DECLARE
 @SQL NVARCHAR(4000)
,@Columns NVARCHAR(4000)
,@GroupBy NVARCHAR(4000)
,@i INT = 1
,@nbr INT = 0
;
CREATE TABLE #Results
(
 [SalesTerritoryCountry] NVARCHAR(50)
,[SalesTerritoryRegion]  NVARCHAR(50)
,[TotalSalesAmount]      MONEY
)
WITH
(   DISTRIBUTION = ROUND_ROBIN
,   LOCATION = USER_DB
)
;
```

<span data-ttu-id="92866-131">terceiro passo de Olá é tooloop através do nosso cubo de colunas de executar a agregação de Olá.</span><span class="sxs-lookup"><span data-stu-id="92866-131">hello third step is tooloop over our cube of columns performing hello aggregation.</span></span> <span data-ttu-id="92866-132">consulta de Olá irá executar uma vez para cada linha na tabela temporária Olá #Cube e armazenar os resultados de Olá numa tabela temporária Olá #Results</span><span class="sxs-lookup"><span data-stu-id="92866-132">hello query will run once for every row in hello #Cube temporary table and store hello results in hello #Results temp table</span></span>

```sql
SET @nbr =(SELECT MAX(Seq) FROM #Cube);

WHILE @i<=@nbr
BEGIN
    SET @Columns = (SELECT Cols    FROM #Cube where seq = @i);
    SET @GroupBy = (SELECT GroupBy FROM #Cube where seq = @i);

    SET @SQL ='INSERT INTO #Results
              SELECT '+@Columns+'
              ,      SUM(SalesAmount) AS TotalSalesAmount
              FROM  dbo.factInternetSales s
              JOIN  dbo.DimSalesTerritory t  
              ON s.SalesTerritoryKey = t.SalesTerritoryKey
              '+CASE WHEN @GroupBy <>''
                     THEN 'GROUP BY '+@GroupBy ELSE '' END

    EXEC sp_executesql @SQL;
    SET @i +=1;
END
```

<span data-ttu-id="92866-133">Por último, pode devolver resultados Olá lendo simplesmente de tabela temporária Olá #Results</span><span class="sxs-lookup"><span data-stu-id="92866-133">Lastly we can return hello results by simply reading from hello #Results temporary table</span></span>

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

<span data-ttu-id="92866-134">Ao dividi código Olá em secções e de gerar um ciclo Olá de construção código torna-se mais fácil de gerir e sustentável.</span><span class="sxs-lookup"><span data-stu-id="92866-134">By breaking hello code up into sections and generating a looping construct hello code becomes more manageable and maintainable.</span></span>

## <a name="next-steps"></a><span data-ttu-id="92866-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="92866-135">Next steps</span></span>
<span data-ttu-id="92866-136">Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="92866-136">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
