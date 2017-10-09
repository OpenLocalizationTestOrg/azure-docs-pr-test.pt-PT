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
# <a name="create-table-as-select-ctas-in-sql-data-warehouse"></a>Create Table As Select (CTAS) no SQL Data Warehouse
Criar tabela como selecionar ou `CTAS` é uma das Olá funcionalidades mais importantes de T-SQL disponíveis. É uma operação totalmente parallelized que cria uma nova tabela com base no resultado de Olá de uma instrução SELECT. `CTAS`é uma cópia de uma tabela de Olá toocreate de forma mais simples e mais rápida. Este documento fornece exemplos e melhores práticas para `CTAS`.

## <a name="selectinto-vs-ctas"></a>SELECIONAR... NO vs. CTAS
Pode considerar `CTAS` como uma versão Super-obrigatórios debitada do `SELECT..INTO`.

Segue-se um exemplo de uma simples `SELECT..INTO` instrução:

```sql
SELECT *
INTO    [dbo].[FactInternetSales_new]
FROM    [dbo].[FactInternetSales]
```

No exemplo Olá acima `[dbo].[FactInternetSales_new]` seria possível criar como tabela de distribuída ROUND_ROBIN com um índice de COLUMNSTORE em cluster no mesmo como estas são as predefinições da tabela de Olá no Azure SQL Data Warehouse.

`SELECT..INTO`No entanto não permitem-lhe toochange o índice de método ou Olá da distribuição de Olá escreva como parte da operação de Olá. Este é onde `CTAS` é apresentada no.

tooconvert Olá acima demasiado`CTAS` é bastante simples:

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

Com `CTAS` são toochange capaz de ambos Olá distribuição de dados da tabela Olá, bem como o tipo de tabela Olá. 

> [!NOTE]
> Se apenas estiver a tentar o índice de Olá toochange na sua `CTAS` operação e Olá tabela de origem é hash distribuída, em seguida, o `CTAS` irão efetuar a operação melhor se mantém Olá mesmo tipo de coluna e os dados de distribuição. Evitará cruzada movimento de dados de distribuição durante a operação de Olá que é mais eficiente.
> 
> 

## <a name="using-ctas-toocopy-a-table"></a>Utilizar CTAS toocopy uma tabela
Talvez utiliza um dos Olá mais comuns de `CTAS` está a criar uma cópia de uma tabela para que possa alterar Olá DDL. Se, por exemplo, que criou originalmente a tabela como `ROUND_ROBIN` e agora pretende alterá-la tooa tabela distribuídas numa coluna, `CTAS` é a forma como iria alterar uma coluna de distribuição Olá. `CTAS`Também pode ser o toochange utilizado tipos de criação de partições, indexar ou coluna.

Digamos que criou esta tabela utilizando o tipo de distribuição predefinido Olá de `ROUND_ROBIN` distribuído, uma vez que não existe nenhuma coluna de distribuição foi especificada na Olá `CREATE TABLE`.

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

Agora pretende toocreate uma nova cópia desta tabela com um índice de Columnstore em cluster, de modo a que pode tirar partido de desempenho de Olá das tabelas Columnstore em cluster. Também deve toodistribute esta tabela em ProductKey uma vez que são prevendo associações nesta coluna e pretender tooavoid movimento de dados durante as associações no ProductKey. Por último, também é aconselhável tooadd a criação de partições no OrderDateKey para que rapidamente pode eliminar dados antigos, arrastando partições antigas. Segue-se a instrução de CTAS Olá que seria copie a tabela antiga para uma nova tabela.

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

Por fim, pode mudar o nome do seu tooswap tabelas na sua nova tabela e, em seguida, remover a tabela antiga.

```sql
RENAME OBJECT FactInternetSales tooFactInternetSales_old;
RENAME OBJECT FactInternetSales_new tooFactInternetSales;

DROP TABLE FactInternetSales_old;
```

> [!NOTE]
> O Azure SQL Data Warehouse ainda não suporta a criação ou atualização automática de estatísticas.  Na ordem tooget Olá melhor desempenho das consultas, é importante que sejam criadas estatísticas em todas as colunas de todas as tabelas após o primeiro carregamento de Olá ou ocorrerem quaisquer alterações substanciais nos dados de Olá.  Para obter uma explicação detalhada das estatísticas, consulte Olá [estatísticas] [ Statistics] tópico, no grupo de tópicos desenvolver de Olá.
> 
> 

## <a name="using-ctas-toowork-around-unsupported-features"></a>Utilizar CTAS toowork em torno de funcionalidades não suportadas
`CTAS`Também pode ser utilizado toowork em torno de um número de funcionalidades de Olá não suportado listados abaixo. Isto pode frequentemente provar toobe uma situação de win/win como não apenas o código estarão em conformidade, mas são, muitas vezes, executados mais rapidamente no armazém de dados do SQL Server. Trata-se como resultado da respetiva estrutura parallelized completamente. Os cenários que podem ser trabalhados em torno com CTAS incluem:

* ASSOCIAÇÕES de ANSI nas atualizações
* Associações de ANSI em eliminações
* Declaração de intercalação

> [!NOTE]
> Tente toothink "CTAS primeiro". Se pensa que pode resolver um problema utilizando `CTAS` , em seguida, que é, geralmente, Olá melhor forma tooapproach-lo -, mesmo que o se estiver a escrever mais dados como resultado.
> 
> 

## <a name="ansi-join-replacement-for-update-statements"></a>Substituição de associação de ANSI para instruções update
Pode considerar que tem uma atualização complexa que associa mais de duas tabelas utilizando ANSI associar Olá de tooperform sintaxe UPDATE ou DELETE.

Imagine que tinha tooupdate nesta tabela:

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

poderá ter comparados consulta original Olá algo semelhante ao seguinte:

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

Uma vez que não suporta o SQL Data Warehouse ANSI associações na Olá `FROM` cláusula de um `UPDATE` declaração, não é possível copiar este código de ativação pós-falha sem ligeiramente a alteração.

Pode utilizar uma combinação de um `CTAS` e uma implícita associar tooreplace este código:

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

## <a name="ansi-join-replacement-for-delete-statements"></a>Substituição de associação de ANSI para eliminar instruções
Por vezes, a abordagem das melhores Olá à eliminação de dados é toouse `CTAS`. Em vez de eliminar dados de Olá simplesmente seleciona os dados de Olá pretende tookeep. Este particularmente verdadeiro para `DELETE` instruções que utilizar ansi associar sintaxe, uma vez que o SQL Data Warehouse não suporta associações ANSI no Olá `FROM` cláusula de um `DELETE` instrução.

Um exemplo de uma instrução DELETE convertida está disponível abaixo:

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

## <a name="replace-merge-statements"></a>Substitua as instruções de intercalação
Instruções Merge podem ser substituídas, pelo menos, parte, utilizando `CTAS`. Pode consolidar Olá `INSERT` e Olá `UPDATE` para uma instrução única. Quaisquer registos eliminados teria toobe fechado desativar numa instrução segundo.

Um exemplo de um `UPSERT` está disponível abaixo:

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

## <a name="ctas-recommendation-explicitly-state-data-type-and-nullability-of-output"></a>Recomendação CTAS: Estado explicitamente o tipo de dados e nulidade da saída
Quando migrar código poderá achar que sejam executadas neste tipo de codificação padrão:

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

Instinctively se pensa deve migrar tooa este código CTAS e será correto. No entanto, há um problema oculto aqui.

Olá seguinte código não produzir Olá o mesmo resultado:

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

Tenha em atenção que o resultado"Olá coluna" reencaminhar acarreta Olá tipo e nulidade valores de dados de expressão Olá. Isto pode levar a variações de toosubtle como valores, se não tenha o cuidado.

Tente Olá passos seguintes como um exemplo:

```sql
SELECT result,result*@d
from result
;

SELECT result,result*@d
from ctas_r
;
```

valor de Olá armazenado para o resultado é diferente. Como hello persistente valor na coluna de resultado Olá é utilizado em outro erro de Olá expressões fica ainda mais significativo.

![][1]

Isto é particularmente importante para migrações de dados. Apesar de consulta segundo Olá é possivelmente mais exata há um problema. dados de Olá seria toohello diferentes em comparação com sistema de origem e que servem como tooquestions de integridade na migração Olá. Este é um dos casos raros onde resposta "errado" Olá é, efetivamente, direito de Olá um!

Olá razão vemos este disparidade entre resultados Olá dois está inativo tooimplicit escreva conversão. No Olá primeira tabela do exemplo Olá define a definição da coluna Olá. Quando é inserida linha Olá ocorre uma conversão de tipo implícito. No segundo exemplo de Olá não há nenhuma conversão de tipo implícito expressão Olá define o tipo de dados da coluna de Olá. Repare que também essa coluna Olá no segundo exemplo de Olá foi definida como uma coluna de tipo nulo enquanto no primeiro exemplo de Olá não tem. Quando a tabela de Olá foi criada no nulidade de coluna de exemplo Olá primeiro explicitamente foi definida. No segundo exemplo de Olá toohello expressão apenas foi deixada e por predefinição este resultaria numa definição de um valor nulo.  

tooresolve estes problemas que tem de definir explicitamente a conversão de tipo Olá e permissão de valores NULL na Olá `SELECT` parte Olá `CTAS` instrução. Não é possível definir estas propriedades no Olá criar parte da tabela.

exemplo de Olá abaixo demonstra como toofix Olá código:

```sql
DECLARE @d decimal(7,2) = 85.455
,       @f float(24)    = 85.455

CREATE TABLE ctas_r
WITH (DISTRIBUTION = ROUND_ROBIN)
AS
SELECT ISNULL(CAST(@d*@f AS DECIMAL(7,2)),0) as result
```

Tenha em atenção o seguinte Olá:

* CAST ou CONVERT foi foram utilizado
* ISNULL é utilizado tooforce nulidade não COALESCE
* ISNULL é função mais exterior Olá
* Olá segunda parte Olá ISNULL é uma constante ou seja, 0

> [!NOTE]
> Para Olá nulidade toobe definido corretamente, é vital toouse `ISNULL` e não `COALESCE`. `COALESCE`Não é uma função determinista e, por isso, o resultado de Olá da expressão de Olá será sempre NULLable. `ISNULL`é diferente. É determinística. Por conseguinte Olá quando a segunda parte do Olá `ISNULL` função é uma constante ou um literal, em seguida, o valor resultante Olá irá ser não nulo.
> 
> 

Não é apenas útil para assegurar a integridade de Olá dos seus cálculos desta sugestão. Também é importante para a mudança de partições de tabela. Imagine que tiver esta tabela definida como o facto:

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

No entanto, o campo de valor de Olá é uma expressão calculada não faz parte de dados de origem Olá.

toocreate o conjunto de dados particionado poderá toodo isto:

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

consulta de Olá executaria perfeitamente adequada. problema de Olá vem quando tenta mudança de partições de Olá tooperform. definições de tabela Olá não correspondem. definições de tabela de Olá toomake correspondem Olá que CTAS tem toobe modificado.

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

Pode ver, por conseguinte, que tipo de consistência e a manutenção nulidade as propriedades de um CTAS é uma boa prática engenharia. -Ajuda a integridade toomaintain nos seus cálculos e também garante que é possível comutar a partição.

Consulte tooMSDN para obter mais informações sobre como utilizar [CTAS][CTAS]. É uma das instruções mais importantes de Olá no Azure SQL Data Warehouse. Certifique-se que compreender exaustivamente.

## <a name="next-steps"></a>Passos seguintes
Para mais sugestões de desenvolvimento, consulte [descrição geral do desenvolvimento][development overview].

<!--Image references-->
[1]: media/sql-data-warehouse-develop-ctas/ctas-results.png

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->
[CTAS]: https://msdn.microsoft.com/library/mt204041.aspx

<!--Other Web references-->
