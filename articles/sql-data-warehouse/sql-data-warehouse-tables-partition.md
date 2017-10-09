---
title: tabelas de aaaPartitioning no SQL Data Warehouse | Microsoft Docs
description: "Introdução à criação de partições de tabela no Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: 6cef870c-114f-470c-af10-02300c58885d
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: aa63c51562f3e6f83063320860b195e135a721e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="partitioning-tables-in-sql-data-warehouse"></a>A criação de partições de tabelas no armazém de dados do SQL Server
> [!div class="op_single_selector"]
> * [Descrição geral][Overview]
> * [Tipos de dados][Data Types]
> * [Distribuir][Distribute]
> * [Índice][Index]
> * [Partição][Partition]
> * [Estatísticas][Statistics]
> * [Temporário][Temporary]
> 
> 

Criação de partições é suportada em todos os tipos de tabela do SQL Data Warehouse; incluindo columnstore em cluster, índice em cluster e área dinâmica para dados.  Criação de partições também é suportada em todos os tipos de distribuição, incluindo hash ou o round robin distribuído.  Criação de partições permite-lhe toodivide os dados para grupos mais pequenos de dados e na maioria dos casos, a criação de partições são feitos por uma coluna de data.

## <a name="benefits-of-partitioning"></a>Vantagens da criação de partições
Criação de partições pode beneficiar desempenho de consulta e de manutenção de dados.  Indica se beneficia ambos ou apenas um é depende da forma como os dados são carregados e se hello mesma coluna pode ser utilizada para ambos os fins, desde que a criação de partições só pode ser efetuada numa coluna.

### <a name="benefits-tooloads"></a>Vantagens tooloads
Olá das principais vantagens da criação de partições no SQL Data Warehouse é melhorar a eficiência de Olá e o desempenho de carregamento de dados através de eliminação de partição, mudar e intercalação.  Na maioria dos casos, dados estão particionados numa data coluna está estreitamente associado sequência toohello que dados Olá são carregada toohello base de dados.  Uma das vantagens de mais Olá da utilização de dados de toomaintain partições-Olá evitação de ciclos de registo de transações.  Embora simplesmente a inserir, atualizar ou eliminar dados possam ser abordagem mais simples de Olá, com um pequeno profundamente e esforço, a criação de partições durante o processo de carga a utilizar pode substancialmente melhorar o desempenho.

Mudar de partição pode ser utilizados tooquickly remover ou substituir uma secção de uma tabela.  Por exemplo, uma tabela de factos vendas poderá conter dados apenas para Olá últimos meses 36.  No final de Olá de cada mês, hello mais antigos mês de dados de vendas é eliminado da tabela de Olá.  Foi possível eliminar estes dados através de um instrução toodelete Olá dados para Olá mês mais antigos.  No entanto, a eliminação de uma grande quantidade de dados linha por linha com a instrução delete pode demorar muito tempo, bem como criar o risco de Olá de grande transações que pode demorar um toorollback muito tempo se algo não bate certo.  Uma abordagem mais ideal é uma partição mais antiga do toosimply largar Olá de dados.  Em que a eliminação de linhas individuais Olá pode demorar horas, eliminar uma partição completa pode demorar algum segundos.

### <a name="benefits-tooqueries"></a>Vantagens tooqueries
Criação de partições também pode ser utilizado tooimprove desempenho das consultas.  Se uma consulta aplica-se um filtro numa coluna particionada, isto pode limitar Olá tooonly análise de Olá elegíveis partições que podem ser um subconjunto mais pequeno de dados de Olá, evitando uma análise completa de tabela.  Olá, com introdução de índices columnstore em cluster benefícios de desempenho de eliminação de predicado Olá são menos úteis, mas em alguns casos pode haver um tooqueries benefício.  Por exemplo, se a tabela de factos vendas Olá está particionada em meses 36 utilizando o campo de data vendas Olá, em seguida, consultas de filtro na data de venda Olá podem ignorar procura em partições que não correspondem ao filtro de Olá.

## <a name="partition-sizing-guidance"></a>Orientação de dimensionamento de partição
Durante a criação de partições pode ser utilizados tooimprove desempenho alguns cenários, criar uma tabela com **demasiados** partições pacote podem prejudicar o desempenho em algumas circunstâncias.  Estas questões são particularmente verdadeiras para tabelas columnstore em cluster.  Para a criação de partições toobe úteis, é importante toounderstand quando toouse criação de partições e Olá o número de partições toocreate.  Não existe nenhuma regra rápida rígida como toohow partições muitos for demasiado elevado, depende nos seus dados e partições quantos são carregar toosimultaneously.  Mas como geral regra geral, considere adicionar 10s too100s de partições, não 1000s.

Ao criar a criação de partições no **columnstore em cluster** tabelas, é importante tooconsider quantas linhas serão encaminhado para cada partição.  Para compressão ideal e o desempenho das tabelas columnstore em cluster, é necessário um mínimo de 1 milhões de linhas por partição e de distribuição.  Antes da criação de partições, o SQL Data Warehouse divide já cada tabela em 60 bases de dados distribuídas.  Qualquer tabela tooa adicionado criação de partições é além disso distribuições toohello criadas em segundo plano de Olá.  Com este exemplo, se tabela de factos vendas Olá contidos 36 partições mensais e uma vez que o SQL Data Warehouse tem 60 distribuições, em seguida, Olá facto venda tabela deverá conter 60 milhões de linhas por mês ou 2.1 milhões de linhas quando todos os meses são povoados.  Se uma tabela contém significativamente menos linhas do Olá recomendado número mínimo de linhas por partição, considere utilizar partições menos na ordem toomake aumento Olá número de linhas por partição.  Consulte também Olá [Indexing] [ Index] artigo que inclui as consultas que podem ser executadas no SQL Data Warehouse tooassess Olá de quality of índices columnstore de cluster.

## <a name="syntax-difference-from-sql-server"></a>Diferença de sintaxe do SQL Server
O SQL Data Warehouse introduz uma definição simplificada de partições que é ligeiramente diferente do SQL Server.  As funções de criação de partições e de esquemas não são utilizados no armazém de dados do SQL dado que estão no SQL Server.  Em vez disso, tudo o que precisa toodo é identificar os pontos de limites de coluna e Olá particionados.  Enquanto a sintaxe de Olá a criação de partições poderão ser ligeiramente diferente do SQL Server, os conceitos básicos do Olá são Olá mesmo.  SQL Server e do armazém de dados do SQL Server suportam uma partição coluna por tabela, o que pode ser ranged partição.  toolearn mais informações sobre a criação de partições, consulte [índices e tabelas Particionadas][Partitioned Tables and Indexes].

Olá abaixo exemplo de um SQL Data Warehouse particionada [CREATE TABLE] [ CREATE TABLE] declaração, partições tabela FactInternetSales de Olá na coluna de OrderDateKey Olá:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101,20010101,20020101
                    ,20030101,20040101,20050101
                    )
                )
)
;
```

## <a name="migrating-partitioning-from-sql-server"></a>Migrar a criação de partições do SQL Server
toomigrate do SQL Server tooSQL de definições do armazém de dados de partição simplesmente:

* Eliminar Olá do SQL Server [esquema de partição][partition scheme].
* Adicionar Olá [função de partição] [ partition function] definição tooyour criar tabela.

Se estiver a migrar uma tabela particionada necessitar de um Olá de instância do SQL Server abaixo SQL Server pode ajudá-lo toointerrogate Olá diversas linhas que estão em cada partição.  Tenha em atenção que, se hello granularidade de criação de partições mesma é utilizada no SQL Data Warehouse, o número de Olá de linhas por partição irão diminuir por um fator de 60.  

```sql
-- Partition information for a SQL Server Database
SELECT      s.[name]                        AS      [schema_name]
,           t.[name]                        AS      [table_name]
,           i.[name]                        AS      [index_name]
,           p.[partition_number]            AS      [partition_number]
,           SUM(a.[used_pages]*8.0)         AS      [partition_size_kb]
,           SUM(a.[used_pages]*8.0)/1024    AS      [partition_size_mb]
,           SUM(a.[used_pages]*8.0)/1048576 AS      [partition_size_gb]
,           p.[rows]                        AS      [partition_row_count]
,           rv.[value]                      AS      [partition_boundary_value]
,           p.[data_compression_desc]       AS      [partition_compression_desc]
FROM        sys.schemas s
JOIN        sys.tables t                    ON      t.[schema_id]         = s.[schema_id]
JOIN        sys.partitions p                ON      p.[object_id]         = t.[object_id]
JOIN        sys.allocation_units a          ON      a.[container_id]      = p.[partition_id]
JOIN        sys.indexes i                   ON      i.[object_id]         = p.[object_id]
                                            AND     i.[index_id]          = p.[index_id]
JOIN        sys.data_spaces ds              ON      ds.[data_space_id]    = i.[data_space_id]
LEFT JOIN   sys.partition_schemes ps        ON      ps.[data_space_id]    = ds.[data_space_id]
LEFT JOIN   sys.partition_functions pf      ON      pf.[function_id]      = ps.[function_id]
LEFT JOIN   sys.partition_range_values rv   ON      rv.[function_id]      = pf.[function_id]
                                            AND     rv.[boundary_id]      = p.[partition_number]
WHERE       p.[index_id] <=1
GROUP BY    s.[name]
,           t.[name]
,           i.[name]
,           p.[partition_number]
,           p.[rows]
,           rv.[value]
,           p.[data_compression_desc]
;
```

## <a name="workload-management"></a>Gestão de cargas de trabalhos
É um toofactor de consideração de peça final na decisão de partição de tabela toohello [gestão da carga de trabalho][workload management].  Gestão de carga de trabalho do armazém de dados do SQL Server é principalmente Olá a gestão de memória e concorrência.  Olá SQL Data Warehouse máximo de memória alocado tooeach distribuição durante a execução de consulta é regida recursos classes.  Idealmente, as partições serão dimensionadas in consideration of outros fatores, como Olá necessidades de memória de criação de índices columnstore em cluster.  Colocar em cluster benefício de índices columnstore significativamente quando estiverem alocados mais memória.  Por conseguinte, deverá tooensure reconstruir um índice de partição não é starved de memória. Aumentar Olá quantidade de memória disponível tooyour consulta pode ser alcançada ao mudar de função de predefinida Olá, smallrc, tooone de Olá outras funções, como largerc.

Informações sobre a atribuição de Olá de memória por distribuição estão disponíveis consultando vistas de gestão dinâmica de Governador de recursos de Olá. Na realidade a concessão de memória será inferior figuras Olá abaixo. No entanto, esta opção fornece um nível de orientação que pode utilizar ao dimensionar a sua partições para operações de gestão de dados.  Tente tooavoid as partições para além de concessão de memória de Olá fornecida pela classe de recursos muito grande de Olá de dimensionamento. Se as partições de crescimento para além desta figura executar risco Olá da pressão de memória que por sua vez servem como compressão ideal tooless.

```sql
SELECT  rp.[name]                                AS [pool_name]
,       rp.[max_memory_kb]                        AS [max_memory_kb]
,       rp.[max_memory_kb]/1024                    AS [max_memory_mb]
,       rp.[max_memory_kb]/1048576                AS [mex_memory_gb]
,       rp.[max_memory_percent]                    AS [max_memory_percent]
,       wg.[name]                                AS [group_name]
,       wg.[importance]                            AS [group_importance]
,       wg.[request_max_memory_grant_percent]    AS [request_max_memory_grant_percent]
FROM    sys.dm_pdw_nodes_resource_governor_workload_groups    wg
JOIN    sys.dm_pdw_nodes_resource_governor_resource_pools    rp ON wg.[pool_id] = rp.[pool_id]
WHERE   wg.[name] like 'SloDWGroup%'
AND     rp.[name]    = 'SloDWPool'
;
```

## <a name="partition-switching"></a>Mudar de partição
Armazém de dados SQL suporta partição dividir, intercalar e mudança. Cada uma destas funções é excuted utilizando Olá [ALTER TABLE] [ ALTER TABLE] instrução.

as partições de tooswitch entre duas tabelas, deve garantir que as partições de Olá alinhar os respetivos limites e que correspondem às definições de tabela Olá. Dado que não estão disponíveis restrições check intervalo de Olá tooenforce de valores na tabela de origem de Olá tem de conter Olá mesmo limites de partição como tabela de destino Olá. Se não for este caso de Olá, mudança de partições de Olá irá falhar como metadados da partição Olá não serão sincronizados.

### <a name="how-toosplit-a-partition-that-contains-data"></a>Como toosplit uma partição que contém os dados
Hello mais eficiente método toosplit uma partição que contém os dados já está toouse um `CTAS` instrução. Esteja tabela particionada Olá um columnstore em cluster, em seguida, partição da tabela de Olá deve estar vazia para que pode ser dividido.

Segue-se uma tabela particionada columnstore de exemplo que contém uma linha em cada partição:

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
        [ProductKey]            int          NOT NULL
    ,   [OrderDateKey]          int          NOT NULL
    ,   [CustomerKey]           int          NOT NULL
    ,   [PromotionKey]          int          NOT NULL
    ,   [SalesOrderNumber]      nvarchar(20) NOT NULL
    ,   [OrderQuantity]         smallint     NOT NULL
    ,   [UnitPrice]             money        NOT NULL
    ,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    (20000101
                    )
                )
)
;

INSERT INTO dbo.FactInternetSales
VALUES (1,19990101,1,1,1,1,1,1);
INSERT INTO dbo.FactInternetSales
VALUES (1,20000101,1,1,1,1,1,1);


CREATE STATISTICS Stat_dbo_FactInternetSales_OrderDateKey ON dbo.FactInternetSales(OrderDateKey);
```

> [!NOTE]
> Ao criar objeto de estatística de Olá, podemos assegurar que os metadados da tabela são mais exato. Se omitir iremos criar estatísticas, o SQL Data Warehouse utilizará os valores predefinidos. Para obter detalhes sobre as estatísticas reveja [estatísticas][statistics].
> 
> 

Vamos, em seguida, pode consultar contagem de linhas de Olá utilizando Olá `sys.partitions` vista de catálogo:

```sql
SELECT  QUOTENAME(s.[name])+'.'+QUOTENAME(t.[name]) as Table_name
,       i.[name] as Index_name
,       p.partition_number as Partition_nmbr
,       p.[rows] as Row_count
,       p.[data_compression_desc] as Data_Compression_desc
FROM    sys.partitions p
JOIN    sys.tables     t    ON    p.[object_id]   = t.[object_id]
JOIN    sys.schemas    s    ON    t.[schema_id]   = s.[schema_id]
JOIN    sys.indexes    i    ON    p.[object_id]   = i.[object_Id]
                            AND   p.[index_Id]    = i.[index_Id]
WHERE t.[name] = 'FactInternetSales'
;
```

Se vamos tentar toosplit nesta tabela, iremos irá obter um erro:

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

Tarifas de mensagens 35346, 15 nível, 1 de estado, linha 44 DIVIDIR cláusula da instrução ALTER PARTITION falhou porque a partição de Olá não está vazia.  Apenas as partições vazia podem ser divididas quando existe um índice columnstore na tabela de Olá. Considere desativar o índice columnstore Olá antes de emitir a instrução ALTER PARTITION de Olá, em seguida, reconstrua o índice columnstore Olá depois de ALTER PARTITION ter sido concluída.

No entanto, podemos utilizar `CTAS` toocreate um novo toohold de tabela nossos dados.

```sql
CREATE TABLE dbo.FactInternetSales_20000101
    WITH    (   DISTRIBUTION = HASH(ProductKey)
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101
                                )
                            )
            )
AS
SELECT *
FROM    FactInternetSales
WHERE   1=2
;
```

Como os limites de partição de Olá estão alinhados é permitido um comutador. Isto irá deixar a tabela de origem Olá com uma partição vazia que iremos subsequentemente pode dividir.

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

É tudo o que for deixado toodo tooalign toohello nossos dados novos limites através de partição `CTAS` e mude os nossos dados na tabela principal toohello

```sql
CREATE TABLE [dbo].[FactInternetSales_20000101_20010101]
    WITH    (   DISTRIBUTION = HASH([ProductKey])
            ,   CLUSTERED COLUMNSTORE INDEX
            ,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                                (20000101,20010101
                                )
                            )
            )
AS
SELECT  *
FROM    [dbo].[FactInternetSales_20000101]
WHERE   [OrderDateKey] >= 20000101
AND     [OrderDateKey] <  20010101
;

ALTER TABLE dbo.FactInternetSales_20000101_20010101 SWITCH PARTITION 2 toodbo.FactInternetSales PARTITION 2;
```

Depois de concluir o movimento de dados de Olá Olá é estatísticas de Olá uma boa ideia toorefresh no tooensure de tabela de destino Olá refletem com precisão o distribuição novo Olá dados Olá as respetivas partições respetivas:

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a>Tabela de criação de partições de controlo de código fonte
tooavoid a definição da tabela de **rusting** no seu sistema de controlo de origem poderá ser útil Olá tooconsider abordagem os seguintes:

1. Criar tabela Olá como uma tabela particionada mas não existem valores de partição

```sql
CREATE TABLE [dbo].[FactInternetSales]
(
    [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
WITH
(   CLUSTERED COLUMNSTORE INDEX
,   DISTRIBUTION = HASH([ProductKey])
,   PARTITION   (   [OrderDateKey] RANGE RIGHT FOR VALUES
                    ()
                )
)
;
```

1. `SPLIT`tabela de Olá como parte do processo de implementação de Olá:

```sql
-- Create a table containing hello partition boundaries

CREATE TABLE #partitions
WITH
(
    LOCATION = USER_DB
,   DISTRIBUTION = HASH(ptn_no)
)
AS
SELECT  ptn_no
,       ROW_NUMBER() OVER (ORDER BY (ptn_no)) as seq_no
FROM    (
        SELECT CAST(20000101 AS INT) ptn_no
        UNION ALL
        SELECT CAST(20010101 AS INT)
        UNION ALL
        SELECT CAST(20020101 AS INT)
        UNION ALL
        SELECT CAST(20030101 AS INT)
        UNION ALL
        SELECT CAST(20040101 AS INT)
        ) a
;

-- Iterate over hello partition boundaries and split hello table

DECLARE @c INT = (SELECT COUNT(*) FROM #partitions)
,       @i INT = 1                                 --iterator for while loop
,       @q NVARCHAR(4000)                          --query
,       @p NVARCHAR(20)     = N''                  --partition_number
,       @s NVARCHAR(128)    = N'dbo'               --schema
,       @t NVARCHAR(128)    = N'FactInternetSales' --table
;

WHILE @i <= @c
BEGIN
    SET @p = (SELECT ptn_no FROM #partitions WHERE seq_no = @i);
    SET @q = (SELECT N'ALTER TABLE '+@s+N'.'+@t+N' SPLIT RANGE ('+@p+N');');

    -- PRINT @q;
    EXECUTE sp_executesql @q;

    SET @i+=1;
END

-- Code clean-up

DROP TABLE #partitions;
```

Com esta Olá abordagem código no controlo de origem permanece estático e valores de limite de criação de partições Olá são permitidos toobe dinâmico; com o armazém de Olá a evolução ao longo do tempo.

## <a name="next-steps"></a>Passos seguintes
toolearn mais, consulte os artigos de Olá no [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de indexação][Index], [manter as estatísticas da tabela] [ Statistics] e [ Tabelas temporárias][Temporary].  Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[workload management]: ./sql-data-warehouse-develop-concurrency.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!-- MSDN Articles -->
[Partitioned Tables and Indexes]: https://msdn.microsoft.com/library/ms190787.aspx
[ALTER TABLE]: https://msdn.microsoft.com/en-us/library/ms190273.aspx
[CREATE TABLE]: https://msdn.microsoft.com/library/mt203953.aspx
[partition function]: https://msdn.microsoft.com/library/ms187802.aspx
[partition scheme]: https://msdn.microsoft.com/library/ms179854.aspx


<!-- Other web references -->
