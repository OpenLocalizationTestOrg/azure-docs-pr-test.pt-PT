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
# <a name="group-by-options-in-sql-data-warehouse"></a>Agrupar por opções no SQL Data Warehouse
Olá [GROUP BY] [ GROUP BY] é utilizar a cláusula set resumo do tooaggregate dados tooa de linhas. Também tem algumas opções que expandem a funcionalidade de toobe essa necessidade trabalhado em torno como não são suportados diretamente ao Azure SQL Data Warehouse.

Estas opções são

* GROUP BY com ROLLUP
* CONJUNTOS DE AGRUPAMENTO
* GROUP BY cubo

## <a name="rollup-and-grouping-sets-options"></a>Rollup e grouping define as opções
Olá aqui a opção mais simples é toouse `UNION ALL` em vez disso, tooperform Olá rollup, em vez de depender Olá sintaxe explícita. resultado de Olá é exatamente Olá mesmo

Segue-se um exemplo de um grupo pela instrução utilizando Olá `ROLLUP` opção:

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

Através da utilização de agregação, iremos pediu Olá agregações os seguintes:

* País e região
* País
* Total geral

tooreplace isto, terá de toouse `UNION ALL`; especificar agregações Olá necessárias explicitamente tooreturn Olá mesmos resultados:

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

Para GROUPING SETS precisamos apenas toodo é que adotar Olá mesmo principal, mas só criar secções UNION ALL para Olá níveis de agregação queremos toosee

## <a name="cube-options"></a>Opções do cubo
É possível toocreate um grupo por com cubo utilizando abordagem UNION ALL Olá. problema de Olá é que o código de Olá pode rapidamente tornar-se complexa e unwieldy. toomitigate isto, pode utilizar este mais avançadas abordagem.

Vamos utilizar o exemplo de Olá acima.

Step-by-Olá primeiro passo é toodefine Olá 'cube', que define todos os níveis de Olá de agregação que queremos toocreate. É importante tootake nota Olá CROSS JOIN de duas tabelas derivadas de Olá. Isto gera todos os níveis de Olá para-nos. rest Olá de código Olá existe realmente para formatação.

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

Olá os resultados da Olá CTAS podem ser vistos abaixo:

![][1]

segundo passo de Olá é toospecify que resulta de um provisório de toostore de tabela de destino:

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

terceiro passo de Olá é tooloop através do nosso cubo de colunas de executar a agregação de Olá. consulta de Olá irá executar uma vez para cada linha na tabela temporária Olá #Cube e armazenar os resultados de Olá numa tabela temporária Olá #Results

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

Por último, pode devolver resultados Olá lendo simplesmente de tabela temporária Olá #Results

```sql
SELECT *
FROM #Results
ORDER BY 1,2,3
;
```

Ao dividi código Olá em secções e de gerar um ciclo Olá de construção código torna-se mais fácil de gerir e sustentável.

## <a name="next-steps"></a>Passos seguintes
Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-group-by-options/sql-data-warehouse-develop-group-by-cube.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[GROUP BY]: https://msdn.microsoft.com/library/ms177673.aspx


<!--Other Web references-->
