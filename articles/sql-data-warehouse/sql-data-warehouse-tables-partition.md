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
# <a name="partitioning-tables-in-sql-data-warehouse"></a><span data-ttu-id="c50f6-103">A criação de partições de tabelas no armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="c50f6-103">Partitioning tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="c50f6-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="c50f6-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="c50f6-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="c50f6-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="c50f6-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="c50f6-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="c50f6-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="c50f6-107">[Index][Index]</span></span>
> * <span data-ttu-id="c50f6-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="c50f6-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="c50f6-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="c50f6-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="c50f6-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="c50f6-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="c50f6-111">Criação de partições é suportada em todos os tipos de tabela do SQL Data Warehouse; incluindo columnstore em cluster, índice em cluster e área dinâmica para dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-111">Partitioning is supported on all SQL Data Warehouse table types; including clustered columnstore, clustered index, and heap.</span></span>  <span data-ttu-id="c50f6-112">Criação de partições também é suportada em todos os tipos de distribuição, incluindo hash ou o round robin distribuído.</span><span class="sxs-lookup"><span data-stu-id="c50f6-112">Partitioning is also supported on all distribution types, including both hash or round robin distributed.</span></span>  <span data-ttu-id="c50f6-113">Criação de partições permite-lhe toodivide os dados para grupos mais pequenos de dados e na maioria dos casos, a criação de partições são feitos por uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="c50f6-113">Partitioning enables you toodivide your data into smaller groups of data and in most cases, partitioning is done on a date column.</span></span>

## <a name="benefits-of-partitioning"></a><span data-ttu-id="c50f6-114">Vantagens da criação de partições</span><span class="sxs-lookup"><span data-stu-id="c50f6-114">Benefits of partitioning</span></span>
<span data-ttu-id="c50f6-115">Criação de partições pode beneficiar desempenho de consulta e de manutenção de dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-115">Partitioning can benefit data maintenance and query performance.</span></span>  <span data-ttu-id="c50f6-116">Indica se beneficia ambos ou apenas um é depende da forma como os dados são carregados e se hello mesma coluna pode ser utilizada para ambos os fins, desde que a criação de partições só pode ser efetuada numa coluna.</span><span class="sxs-lookup"><span data-stu-id="c50f6-116">Whether it benefits both or just one is dependent on how data is loaded and whether hello same column can be used for both purposes, since partitioning can only be done on one column.</span></span>

### <a name="benefits-tooloads"></a><span data-ttu-id="c50f6-117">Vantagens tooloads</span><span class="sxs-lookup"><span data-stu-id="c50f6-117">Benefits tooloads</span></span>
<span data-ttu-id="c50f6-118">Olá das principais vantagens da criação de partições no SQL Data Warehouse é melhorar a eficiência de Olá e o desempenho de carregamento de dados através de eliminação de partição, mudar e intercalação.</span><span class="sxs-lookup"><span data-stu-id="c50f6-118">hello primary benefit of partitioning in SQL Data Warehouse is improve hello efficiency and performance of loading data by use of partition deletion, switching and merging.</span></span>  <span data-ttu-id="c50f6-119">Na maioria dos casos, dados estão particionados numa data coluna está estreitamente associado sequência toohello que dados Olá são carregada toohello base de dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-119">In most cases data is partitioned on a date column that is closely tied toohello sequence which hello data is loaded toohello database.</span></span>  <span data-ttu-id="c50f6-120">Uma das vantagens de mais Olá da utilização de dados de toomaintain partições-Olá evitação de ciclos de registo de transações.</span><span class="sxs-lookup"><span data-stu-id="c50f6-120">One of hello greatest benefits of using partitions toomaintain data it hello avoidance of transaction logging.</span></span>  <span data-ttu-id="c50f6-121">Embora simplesmente a inserir, atualizar ou eliminar dados possam ser abordagem mais simples de Olá, com um pequeno profundamente e esforço, a criação de partições durante o processo de carga a utilizar pode substancialmente melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="c50f6-121">While simply inserting, updating or deleting data can be hello most straightforward approach, with a little thought and effort, using partitioning during your load process can substantially improve performance.</span></span>

<span data-ttu-id="c50f6-122">Mudar de partição pode ser utilizados tooquickly remover ou substituir uma secção de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c50f6-122">Partition switching can be used tooquickly remove or replace a section of a table.</span></span>  <span data-ttu-id="c50f6-123">Por exemplo, uma tabela de factos vendas poderá conter dados apenas para Olá últimos meses 36.</span><span class="sxs-lookup"><span data-stu-id="c50f6-123">For example, a sales fact table might contain just data for hello past 36 months.</span></span>  <span data-ttu-id="c50f6-124">No final de Olá de cada mês, hello mais antigos mês de dados de vendas é eliminado da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-124">At hello end of every month, hello oldest month of sales data is deleted from hello table.</span></span>  <span data-ttu-id="c50f6-125">Foi possível eliminar estes dados através de um instrução toodelete Olá dados para Olá mês mais antigos.</span><span class="sxs-lookup"><span data-stu-id="c50f6-125">This data could be deleted by using a delete statement toodelete hello data for hello oldest month.</span></span>  <span data-ttu-id="c50f6-126">No entanto, a eliminação de uma grande quantidade de dados linha por linha com a instrução delete pode demorar muito tempo, bem como criar o risco de Olá de grande transações que pode demorar um toorollback muito tempo se algo não bate certo.</span><span class="sxs-lookup"><span data-stu-id="c50f6-126">However, deleting a large amount of data row-by-row with a delete statement can take a very long time, as well as create hello risk of large transactions which could take a long time toorollback if something goes wrong.</span></span>  <span data-ttu-id="c50f6-127">Uma abordagem mais ideal é uma partição mais antiga do toosimply largar Olá de dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-127">A more optimal approach is toosimply drop hello oldest partition of data.</span></span>  <span data-ttu-id="c50f6-128">Em que a eliminação de linhas individuais Olá pode demorar horas, eliminar uma partição completa pode demorar algum segundos.</span><span class="sxs-lookup"><span data-stu-id="c50f6-128">Where deleting hello individual rows could take hours, deleting an entire partition could take seconds.</span></span>

### <a name="benefits-tooqueries"></a><span data-ttu-id="c50f6-129">Vantagens tooqueries</span><span class="sxs-lookup"><span data-stu-id="c50f6-129">Benefits tooqueries</span></span>
<span data-ttu-id="c50f6-130">Criação de partições também pode ser utilizado tooimprove desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="c50f6-130">Partitioning can also be used tooimprove query performance.</span></span>  <span data-ttu-id="c50f6-131">Se uma consulta aplica-se um filtro numa coluna particionada, isto pode limitar Olá tooonly análise de Olá elegíveis partições que podem ser um subconjunto mais pequeno de dados de Olá, evitando uma análise completa de tabela.</span><span class="sxs-lookup"><span data-stu-id="c50f6-131">If a query applies a filter on a partitioned column, this can limit hello scan tooonly hello qualifying partitions which may be a much smaller subset of hello data, avoiding a full table scan.</span></span>  <span data-ttu-id="c50f6-132">Olá, com introdução de índices columnstore em cluster benefícios de desempenho de eliminação de predicado Olá são menos úteis, mas em alguns casos pode haver um tooqueries benefício.</span><span class="sxs-lookup"><span data-stu-id="c50f6-132">With hello introduction of clustered columnstore indexes, hello predicate elimination performance benefits are less beneficial, but in some cases there can be a benefit tooqueries.</span></span>  <span data-ttu-id="c50f6-133">Por exemplo, se a tabela de factos vendas Olá está particionada em meses 36 utilizando o campo de data vendas Olá, em seguida, consultas de filtro na data de venda Olá podem ignorar procura em partições que não correspondem ao filtro de Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-133">For example, if hello sales fact table is partitioned into 36 months using hello sales date field, then queries that filter on hello sale date can skip searching in partitions that don’t match hello filter.</span></span>

## <a name="partition-sizing-guidance"></a><span data-ttu-id="c50f6-134">Orientação de dimensionamento de partição</span><span class="sxs-lookup"><span data-stu-id="c50f6-134">Partition sizing guidance</span></span>
<span data-ttu-id="c50f6-135">Durante a criação de partições pode ser utilizados tooimprove desempenho alguns cenários, criar uma tabela com **demasiados** partições pacote podem prejudicar o desempenho em algumas circunstâncias.</span><span class="sxs-lookup"><span data-stu-id="c50f6-135">While partitioning can be used tooimprove performance some scenarios, creating a table with **too many** partitions can hurt performance under some circumstances.</span></span>  <span data-ttu-id="c50f6-136">Estas questões são particularmente verdadeiras para tabelas columnstore em cluster.</span><span class="sxs-lookup"><span data-stu-id="c50f6-136">These concerns are especially true for clustered columnstore tables.</span></span>  <span data-ttu-id="c50f6-137">Para a criação de partições toobe úteis, é importante toounderstand quando toouse criação de partições e Olá o número de partições toocreate.</span><span class="sxs-lookup"><span data-stu-id="c50f6-137">For partitioning toobe helpful, it is important toounderstand when toouse partitioning and hello number of partitions toocreate.</span></span>  <span data-ttu-id="c50f6-138">Não existe nenhuma regra rápida rígida como toohow partições muitos for demasiado elevado, depende nos seus dados e partições quantos são carregar toosimultaneously.</span><span class="sxs-lookup"><span data-stu-id="c50f6-138">There is no hard fast rule as toohow many partitions are too many, it depends on your data and how many partitions you are loading toosimultaneously.</span></span>  <span data-ttu-id="c50f6-139">Mas como geral regra geral, considere adicionar 10s too100s de partições, não 1000s.</span><span class="sxs-lookup"><span data-stu-id="c50f6-139">But as a general rule of thumb, think of adding 10s too100s of partitions, not 1000s.</span></span>

<span data-ttu-id="c50f6-140">Ao criar a criação de partições no **columnstore em cluster** tabelas, é importante tooconsider quantas linhas serão encaminhado para cada partição.</span><span class="sxs-lookup"><span data-stu-id="c50f6-140">When creating partitioning on **clustered columnstore** tables, it is important tooconsider how many rows will land in each partition.</span></span>  <span data-ttu-id="c50f6-141">Para compressão ideal e o desempenho das tabelas columnstore em cluster, é necessário um mínimo de 1 milhões de linhas por partição e de distribuição.</span><span class="sxs-lookup"><span data-stu-id="c50f6-141">For optimal compression and performance of clustered columnstore tables, a minimum of 1 million rows per distribution and partition is needed.</span></span>  <span data-ttu-id="c50f6-142">Antes da criação de partições, o SQL Data Warehouse divide já cada tabela em 60 bases de dados distribuídas.</span><span class="sxs-lookup"><span data-stu-id="c50f6-142">Before partitions are created, SQL Data Warehouse already divides each table into 60 distributed databases.</span></span>  <span data-ttu-id="c50f6-143">Qualquer tabela tooa adicionado criação de partições é além disso distribuições toohello criadas em segundo plano de Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-143">Any partitioning added tooa table is in addition toohello distributions created behind hello scenes.</span></span>  <span data-ttu-id="c50f6-144">Com este exemplo, se tabela de factos vendas Olá contidos 36 partições mensais e uma vez que o SQL Data Warehouse tem 60 distribuições, em seguida, Olá facto venda tabela deverá conter 60 milhões de linhas por mês ou 2.1 milhões de linhas quando todos os meses são povoados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-144">Using this example, if hello sales fact table contained 36 monthly partitions, and given that SQL Data Warehouse has 60 distributions, then hello sales fact table should contain 60 million rows per month, or 2.1 billion rows when all months are populated.</span></span>  <span data-ttu-id="c50f6-145">Se uma tabela contém significativamente menos linhas do Olá recomendado número mínimo de linhas por partição, considere utilizar partições menos na ordem toomake aumento Olá número de linhas por partição.</span><span class="sxs-lookup"><span data-stu-id="c50f6-145">If a table contains significantly less rows than hello recommended minimum number of rows per partition, consider using fewer partitions in order toomake increase hello number of rows per partition.</span></span>  <span data-ttu-id="c50f6-146">Consulte também Olá [Indexing] [ Index] artigo que inclui as consultas que podem ser executadas no SQL Data Warehouse tooassess Olá de quality of índices columnstore de cluster.</span><span class="sxs-lookup"><span data-stu-id="c50f6-146">Also see hello [Indexing][Index] article which includes queries that can be run on SQL Data Warehouse tooassess hello quality of cluster columnstore indexes.</span></span>

## <a name="syntax-difference-from-sql-server"></a><span data-ttu-id="c50f6-147">Diferença de sintaxe do SQL Server</span><span class="sxs-lookup"><span data-stu-id="c50f6-147">Syntax difference from SQL Server</span></span>
<span data-ttu-id="c50f6-148">O SQL Data Warehouse introduz uma definição simplificada de partições que é ligeiramente diferente do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c50f6-148">SQL Data Warehouse introduces a simplified definition of partitions which is slightly different from SQL Server.</span></span>  <span data-ttu-id="c50f6-149">As funções de criação de partições e de esquemas não são utilizados no armazém de dados do SQL dado que estão no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="c50f6-149">Partitioning functions and schemes are not used in SQL Data Warehouse as they are in SQL Server.</span></span>  <span data-ttu-id="c50f6-150">Em vez disso, tudo o que precisa toodo é identificar os pontos de limites de coluna e Olá particionados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-150">Instead, all you need toodo is identify partitioned column and hello boundary points.</span></span>  <span data-ttu-id="c50f6-151">Enquanto a sintaxe de Olá a criação de partições poderão ser ligeiramente diferente do SQL Server, os conceitos básicos do Olá são Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="c50f6-151">While hello syntax of partitioning may be slightly different from SQL Server, hello basic concepts are hello same.</span></span>  <span data-ttu-id="c50f6-152">SQL Server e do armazém de dados do SQL Server suportam uma partição coluna por tabela, o que pode ser ranged partição.</span><span class="sxs-lookup"><span data-stu-id="c50f6-152">SQL Server and SQL Data Warehouse support one partition column per table, which can be ranged partition.</span></span>  <span data-ttu-id="c50f6-153">toolearn mais informações sobre a criação de partições, consulte [índices e tabelas Particionadas][Partitioned Tables and Indexes].</span><span class="sxs-lookup"><span data-stu-id="c50f6-153">toolearn more about partitioning, see [Partitioned Tables and Indexes][Partitioned Tables and Indexes].</span></span>

<span data-ttu-id="c50f6-154">Olá abaixo exemplo de um SQL Data Warehouse particionada [CREATE TABLE] [ CREATE TABLE] declaração, partições tabela FactInternetSales de Olá na coluna de OrderDateKey Olá:</span><span class="sxs-lookup"><span data-stu-id="c50f6-154">hello below example of a SQL Data Warehouse partitioned [CREATE TABLE][CREATE TABLE] statement, partitions hello FactInternetSales table on hello OrderDateKey column:</span></span>

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

## <a name="migrating-partitioning-from-sql-server"></a><span data-ttu-id="c50f6-155">Migrar a criação de partições do SQL Server</span><span class="sxs-lookup"><span data-stu-id="c50f6-155">Migrating partitioning from SQL Server</span></span>
<span data-ttu-id="c50f6-156">toomigrate do SQL Server tooSQL de definições do armazém de dados de partição simplesmente:</span><span class="sxs-lookup"><span data-stu-id="c50f6-156">toomigrate SQL Server partition definitions tooSQL Data Warehouse simply:</span></span>

* <span data-ttu-id="c50f6-157">Eliminar Olá do SQL Server [esquema de partição][partition scheme].</span><span class="sxs-lookup"><span data-stu-id="c50f6-157">Eliminate hello SQL Server [partition scheme][partition scheme].</span></span>
* <span data-ttu-id="c50f6-158">Adicionar Olá [função de partição] [ partition function] definição tooyour criar tabela.</span><span class="sxs-lookup"><span data-stu-id="c50f6-158">Add hello [partition function][partition function] definition tooyour CREATE TABLE.</span></span>

<span data-ttu-id="c50f6-159">Se estiver a migrar uma tabela particionada necessitar de um Olá de instância do SQL Server abaixo SQL Server pode ajudá-lo toointerrogate Olá diversas linhas que estão em cada partição.</span><span class="sxs-lookup"><span data-stu-id="c50f6-159">If you are migrating a partitioned table from a SQL Server instance hello below SQL can help you toointerrogate hello number of rows that are in each partition.</span></span>  <span data-ttu-id="c50f6-160">Tenha em atenção que, se hello granularidade de criação de partições mesma é utilizada no SQL Data Warehouse, o número de Olá de linhas por partição irão diminuir por um fator de 60.</span><span class="sxs-lookup"><span data-stu-id="c50f6-160">Keep in mind that if hello same partitioning granularity is used on SQL Data Warehouse, hello number of rows per partition will decrease by a factor of 60.</span></span>  

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

## <a name="workload-management"></a><span data-ttu-id="c50f6-161">Gestão de cargas de trabalhos</span><span class="sxs-lookup"><span data-stu-id="c50f6-161">Workload management</span></span>
<span data-ttu-id="c50f6-162">É um toofactor de consideração de peça final na decisão de partição de tabela toohello [gestão da carga de trabalho][workload management].</span><span class="sxs-lookup"><span data-stu-id="c50f6-162">One final piece consideration toofactor in toohello table partition decision is [workload management][workload management].</span></span>  <span data-ttu-id="c50f6-163">Gestão de carga de trabalho do armazém de dados do SQL Server é principalmente Olá a gestão de memória e concorrência.</span><span class="sxs-lookup"><span data-stu-id="c50f6-163">Workload management in SQL Data Warehouse is primarily hello management of memory and concurrency.</span></span>  <span data-ttu-id="c50f6-164">Olá SQL Data Warehouse máximo de memória alocado tooeach distribuição durante a execução de consulta é regida recursos classes.</span><span class="sxs-lookup"><span data-stu-id="c50f6-164">In SQL Data Warehouse hello maximum memory allocated tooeach distribution during query execution is governed resource classes.</span></span>  <span data-ttu-id="c50f6-165">Idealmente, as partições serão dimensionadas in consideration of outros fatores, como Olá necessidades de memória de criação de índices columnstore em cluster.</span><span class="sxs-lookup"><span data-stu-id="c50f6-165">Ideally your partitions will be sized in consideration of other factors like hello memory needs of building clustered columnstore indexes.</span></span>  <span data-ttu-id="c50f6-166">Colocar em cluster benefício de índices columnstore significativamente quando estiverem alocados mais memória.</span><span class="sxs-lookup"><span data-stu-id="c50f6-166">Clustered columnstore indexes benefit greatly when they are allocated more memory.</span></span>  <span data-ttu-id="c50f6-167">Por conseguinte, deverá tooensure reconstruir um índice de partição não é starved de memória.</span><span class="sxs-lookup"><span data-stu-id="c50f6-167">Therefore, you will want tooensure that a partition index rebuild is not starved of memory.</span></span> <span data-ttu-id="c50f6-168">Aumentar Olá quantidade de memória disponível tooyour consulta pode ser alcançada ao mudar de função de predefinida Olá, smallrc, tooone de Olá outras funções, como largerc.</span><span class="sxs-lookup"><span data-stu-id="c50f6-168">Increasing hello amount of memory available tooyour query can be achieved by switching from hello default role, smallrc, tooone of hello other roles such as largerc.</span></span>

<span data-ttu-id="c50f6-169">Informações sobre a atribuição de Olá de memória por distribuição estão disponíveis consultando vistas de gestão dinâmica de Governador de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-169">Information on hello allocation of memory per distribution is available by querying hello resource governor dynamic management views.</span></span> <span data-ttu-id="c50f6-170">Na realidade a concessão de memória será inferior figuras Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="c50f6-170">In reality your memory grant will be less than hello figures below.</span></span> <span data-ttu-id="c50f6-171">No entanto, esta opção fornece um nível de orientação que pode utilizar ao dimensionar a sua partições para operações de gestão de dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-171">However, this provides a level of guidance that you can use when sizing your partitions for data management operations.</span></span>  <span data-ttu-id="c50f6-172">Tente tooavoid as partições para além de concessão de memória de Olá fornecida pela classe de recursos muito grande de Olá de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="c50f6-172">Try tooavoid sizing your partitions beyond hello memory grant provided by hello extra large resource class.</span></span> <span data-ttu-id="c50f6-173">Se as partições de crescimento para além desta figura executar risco Olá da pressão de memória que por sua vez servem como compressão ideal tooless.</span><span class="sxs-lookup"><span data-stu-id="c50f6-173">If your partitions grow beyond this figure you run hello risk of memory pressure which in turn leads tooless optimal compression.</span></span>

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

## <a name="partition-switching"></a><span data-ttu-id="c50f6-174">Mudar de partição</span><span class="sxs-lookup"><span data-stu-id="c50f6-174">Partition switching</span></span>
<span data-ttu-id="c50f6-175">Armazém de dados SQL suporta partição dividir, intercalar e mudança.</span><span class="sxs-lookup"><span data-stu-id="c50f6-175">SQL Data Warehouse supports partition splitting, merging, and switching.</span></span> <span data-ttu-id="c50f6-176">Cada uma destas funções é excuted utilizando Olá [ALTER TABLE] [ ALTER TABLE] instrução.</span><span class="sxs-lookup"><span data-stu-id="c50f6-176">Each of these functions is excuted using hello [ALTER TABLE][ALTER TABLE] statement.</span></span>

<span data-ttu-id="c50f6-177">as partições de tooswitch entre duas tabelas, deve garantir que as partições de Olá alinhar os respetivos limites e que correspondem às definições de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-177">tooswitch partitions between two tables you must ensure that hello partitions align on their respective boundaries and that hello table definitions match.</span></span> <span data-ttu-id="c50f6-178">Dado que não estão disponíveis restrições check intervalo de Olá tooenforce de valores na tabela de origem de Olá tem de conter Olá mesmo limites de partição como tabela de destino Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-178">As check constraints are not available tooenforce hello range of values in a table hello source table must contain hello same partition boundaries as hello target table.</span></span> <span data-ttu-id="c50f6-179">Se não for este caso de Olá, mudança de partições de Olá irá falhar como metadados da partição Olá não serão sincronizados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-179">If this is not hello case, then hello partition switch will fail as hello partition metadata will not be synchronized.</span></span>

### <a name="how-toosplit-a-partition-that-contains-data"></a><span data-ttu-id="c50f6-180">Como toosplit uma partição que contém os dados</span><span class="sxs-lookup"><span data-stu-id="c50f6-180">How toosplit a partition that contains data</span></span>
<span data-ttu-id="c50f6-181">Hello mais eficiente método toosplit uma partição que contém os dados já está toouse um `CTAS` instrução.</span><span class="sxs-lookup"><span data-stu-id="c50f6-181">hello most efficient method toosplit a partition that already contains data is toouse a `CTAS` statement.</span></span> <span data-ttu-id="c50f6-182">Esteja tabela particionada Olá um columnstore em cluster, em seguida, partição da tabela de Olá deve estar vazia para que pode ser dividido.</span><span class="sxs-lookup"><span data-stu-id="c50f6-182">If hello partitioned table is a clustered columnstore then hello table partition must be empty before it can be split.</span></span>

<span data-ttu-id="c50f6-183">Segue-se uma tabela particionada columnstore de exemplo que contém uma linha em cada partição:</span><span class="sxs-lookup"><span data-stu-id="c50f6-183">Below is a sample partitioned columnstore table containing one row in each partition:</span></span>

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
> <span data-ttu-id="c50f6-184">Ao criar objeto de estatística de Olá, podemos assegurar que os metadados da tabela são mais exato.</span><span class="sxs-lookup"><span data-stu-id="c50f6-184">By Creating hello statistic object, we ensure that table metadata is more accurate.</span></span> <span data-ttu-id="c50f6-185">Se omitir iremos criar estatísticas, o SQL Data Warehouse utilizará os valores predefinidos.</span><span class="sxs-lookup"><span data-stu-id="c50f6-185">If we omit creating statistics, then SQL Data Warehouse will use default values.</span></span> <span data-ttu-id="c50f6-186">Para obter detalhes sobre as estatísticas reveja [estatísticas][statistics].</span><span class="sxs-lookup"><span data-stu-id="c50f6-186">For details on statistics please review [statistics][statistics].</span></span>
> 
> 

<span data-ttu-id="c50f6-187">Vamos, em seguida, pode consultar contagem de linhas de Olá utilizando Olá `sys.partitions` vista de catálogo:</span><span class="sxs-lookup"><span data-stu-id="c50f6-187">We can then query for hello row count using hello `sys.partitions` catalog view:</span></span>

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

<span data-ttu-id="c50f6-188">Se vamos tentar toosplit nesta tabela, iremos irá obter um erro:</span><span class="sxs-lookup"><span data-stu-id="c50f6-188">If we try toosplit this table, we will get an error:</span></span>

```sql
ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="c50f6-189">Tarifas de mensagens 35346, 15 nível, 1 de estado, linha 44 DIVIDIR cláusula da instrução ALTER PARTITION falhou porque a partição de Olá não está vazia.</span><span class="sxs-lookup"><span data-stu-id="c50f6-189">Msg 35346, Level 15, State 1, Line 44 SPLIT clause of ALTER PARTITION statement failed because hello partition is not empty.</span></span>  <span data-ttu-id="c50f6-190">Apenas as partições vazia podem ser divididas quando existe um índice columnstore na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="c50f6-190">Only empty partitions can be split in when a columnstore index exists on hello table.</span></span> <span data-ttu-id="c50f6-191">Considere desativar o índice columnstore Olá antes de emitir a instrução ALTER PARTITION de Olá, em seguida, reconstrua o índice columnstore Olá depois de ALTER PARTITION ter sido concluída.</span><span class="sxs-lookup"><span data-stu-id="c50f6-191">Consider disabling hello columnstore index before issuing hello ALTER PARTITION statement, then rebuilding hello columnstore index after ALTER PARTITION is complete.</span></span>

<span data-ttu-id="c50f6-192">No entanto, podemos utilizar `CTAS` toocreate um novo toohold de tabela nossos dados.</span><span class="sxs-lookup"><span data-stu-id="c50f6-192">However, we can use `CTAS` toocreate a new table toohold our data.</span></span>

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

<span data-ttu-id="c50f6-193">Como os limites de partição de Olá estão alinhados é permitido um comutador.</span><span class="sxs-lookup"><span data-stu-id="c50f6-193">As hello partition boundaries are aligned a switch is permitted.</span></span> <span data-ttu-id="c50f6-194">Isto irá deixar a tabela de origem Olá com uma partição vazia que iremos subsequentemente pode dividir.</span><span class="sxs-lookup"><span data-stu-id="c50f6-194">This will leave hello source table with an empty partition that we can subsequently split.</span></span>

```sql
ALTER TABLE FactInternetSales SWITCH PARTITION 2 too FactInternetSales_20000101 PARTITION 2;

ALTER TABLE FactInternetSales SPLIT RANGE (20010101);
```

<span data-ttu-id="c50f6-195">É tudo o que for deixado toodo tooalign toohello nossos dados novos limites através de partição `CTAS` e mude os nossos dados na tabela principal toohello</span><span class="sxs-lookup"><span data-stu-id="c50f6-195">All that is left toodo is tooalign our data toohello new partition boundaries using `CTAS` and switch our data back in toohello main table</span></span>

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

<span data-ttu-id="c50f6-196">Depois de concluir o movimento de dados de Olá Olá é estatísticas de Olá uma boa ideia toorefresh no tooensure de tabela de destino Olá refletem com precisão o distribuição novo Olá dados Olá as respetivas partições respetivas:</span><span class="sxs-lookup"><span data-stu-id="c50f6-196">Once you have completed hello movement of hello data it is a good idea toorefresh hello statistics on hello target table tooensure they accurately reflect hello new distribution of hello data in their respective partitions:</span></span>

```sql
UPDATE STATISTICS [dbo].[FactInternetSales];
```

### <a name="table-partitioning-source-control"></a><span data-ttu-id="c50f6-197">Tabela de criação de partições de controlo de código fonte</span><span class="sxs-lookup"><span data-stu-id="c50f6-197">Table partitioning source control</span></span>
<span data-ttu-id="c50f6-198">tooavoid a definição da tabela de **rusting** no seu sistema de controlo de origem poderá ser útil Olá tooconsider abordagem os seguintes:</span><span class="sxs-lookup"><span data-stu-id="c50f6-198">tooavoid your table definition from **rusting** in your source control system you may want tooconsider hello following approach:</span></span>

1. <span data-ttu-id="c50f6-199">Criar tabela Olá como uma tabela particionada mas não existem valores de partição</span><span class="sxs-lookup"><span data-stu-id="c50f6-199">Create hello table as a partitioned table but with no partition values</span></span>

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

1. <span data-ttu-id="c50f6-200">`SPLIT`tabela de Olá como parte do processo de implementação de Olá:</span><span class="sxs-lookup"><span data-stu-id="c50f6-200">`SPLIT` hello table as part of hello deployment process:</span></span>

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

<span data-ttu-id="c50f6-201">Com esta Olá abordagem código no controlo de origem permanece estático e valores de limite de criação de partições Olá são permitidos toobe dinâmico; com o armazém de Olá a evolução ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="c50f6-201">With this approach hello code in source control remains static and hello partitioning boundary values are allowed toobe dynamic; evolving with hello warehouse over time.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c50f6-202">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="c50f6-202">Next steps</span></span>
<span data-ttu-id="c50f6-203">toolearn mais, consulte os artigos de Olá no [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de indexação][Index], [manter as estatísticas da tabela] [ Statistics] e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="c50f6-203">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index], [Maintaining Table Statistics][Statistics] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="c50f6-204">Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="c50f6-204">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
