---
title: "desempenho de índice columnstore aaaImprove no SQL do Azure | Microsoft Docs"
description: "Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas que comprime um índice columnstore em cada rowgroup."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: ef170f39-ae24-4b04-af76-53bb4c4d16d3
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: performance
ms.date: 6/2/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 2c5a68435aa200236a2dc8538aa4638b52a59093
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="maximizing-rowgroup-quality-for-columnstore"></a><span data-ttu-id="1371a-103">Maximizar a forma de qualidade de rowgroup para columnstore</span><span class="sxs-lookup"><span data-stu-id="1371a-103">Maximizing rowgroup quality for columnstore</span></span>

<span data-ttu-id="1371a-104">Qualidade de Rowgroup é determinada pelo número de Olá de linhas num rowgroup.</span><span class="sxs-lookup"><span data-stu-id="1371a-104">Rowgroup quality is determined by hello number of rows in a rowgroup.</span></span> <span data-ttu-id="1371a-105">Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas que comprime um índice columnstore em cada rowgroup.</span><span class="sxs-lookup"><span data-stu-id="1371a-105">Reduce memory requirements or increase hello available memory toomaximize hello number of rows a columnstore index compresses into each rowgroup.</span></span>  <span data-ttu-id="1371a-106">Utilize estas taxas de compressão tooimprove de métodos e o desempenho das consultas para índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="1371a-106">Use these methods tooimprove compression rates and query performance for columnstore indexes.</span></span>

## <a name="why-hello-rowgroup-size-matters"></a><span data-ttu-id="1371a-107">Por que motivo o tamanho de rowgroup Olá é importante</span><span class="sxs-lookup"><span data-stu-id="1371a-107">Why hello rowgroup size matters</span></span>
<span data-ttu-id="1371a-108">Uma vez que um índice columnstore analisa uma tabela através da análise de segmentos de coluna de rowgroups individuais, maximizando a número Olá de linhas em cada rowgroup melhora o desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="1371a-108">Since a columnstore index scans a table by scanning column segments of individual rowgroups, maximizing hello number of rows in each rowgroup enhances query performance.</span></span> <span data-ttu-id="1371a-109">Quando rowgroups tem um elevado número de linhas, compressão de dados melhora o que significa que há menos tooread de dados do disco.</span><span class="sxs-lookup"><span data-stu-id="1371a-109">When rowgroups have a high number of rows, data compression improves which means there is less data tooread from disk.</span></span>

<span data-ttu-id="1371a-110">Para mais informações sobre rowgroups, consulte [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="1371a-110">For more information about rowgroups, see [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

## <a name="target-size-for-rowgroups"></a><span data-ttu-id="1371a-111">Tamanho de destino para rowgroups</span><span class="sxs-lookup"><span data-stu-id="1371a-111">Target size for rowgroups</span></span>
<span data-ttu-id="1371a-112">Para melhor desempenho das consultas, o objetivo de Olá é toomaximize Olá número de linhas por rowgroup num índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="1371a-112">For best query performance, hello goal is toomaximize hello number of rows per rowgroup in a columnstore index.</span></span> <span data-ttu-id="1371a-113">Um rowgroup pode ter um máximo de 1.048.576 linhas.</span><span class="sxs-lookup"><span data-stu-id="1371a-113">A rowgroup can have a maximum of 1,048,576 rows.</span></span> <span data-ttu-id="1371a-114">Toonot pode ter Olá número máximo de linhas por rowgroup.</span><span class="sxs-lookup"><span data-stu-id="1371a-114">It's okay toonot have hello maximum number of rows per rowgroup.</span></span> <span data-ttu-id="1371a-115">Os índices Columnstore alcançarem o bom desempenho quando rowgroups tem, pelo menos, 100 000 linhas.</span><span class="sxs-lookup"><span data-stu-id="1371a-115">Columnstore indexes achieve good performance when rowgroups have at least 100,000 rows.</span></span>

## <a name="rowgroups-can-get-trimmed-during-compression"></a><span data-ttu-id="1371a-116">Pode obter cortada Rowgroups durante a compressão</span><span class="sxs-lookup"><span data-stu-id="1371a-116">Rowgroups can get trimmed during compression</span></span>

<span data-ttu-id="1371a-117">Durante uma em massa de carga ou columnstore índice reconstrução, por vezes, não existe não é suficiente toocompress disponíveis de memória que Olá todas as linhas designadas para cada rowgroup.</span><span class="sxs-lookup"><span data-stu-id="1371a-117">During a bulk load or columnstore index rebuild, sometimes there isn't enough memory available toocompress all hello rows designated for each rowgroup.</span></span> <span data-ttu-id="1371a-118">Quando existe pressão de memória, os índices columnstore compactar tamanhos de rowgroup Olá para que compressão no columnstore Olá pode ter êxito.</span><span class="sxs-lookup"><span data-stu-id="1371a-118">When there is memory pressure, columnstore indexes trim hello rowgroup sizes so compression into hello columnstore can succeed.</span></span> 

<span data-ttu-id="1371a-119">Quando existe linhas toocompress, pelo menos, 10 000 de memória insuficiente para cada rowgroup, o SQL Data Warehouse gera um erro.</span><span class="sxs-lookup"><span data-stu-id="1371a-119">When there is insufficient memory toocompress at least 10,000 rows into each rowgroup, SQL Data Warehouse generates an error.</span></span>

<span data-ttu-id="1371a-120">Para obter mais informações sobre o carregamento em massa, consulte [carregamento em massa para um índice columnstore em cluster](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span><span class="sxs-lookup"><span data-stu-id="1371a-120">For more information on bulk loading, see [Bulk load into a clustered columnstore index](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).</span></span>

## <a name="how-toomonitor-rowgroup-quality"></a><span data-ttu-id="1371a-121">Como toomonitor rowgroup qualidade</span><span class="sxs-lookup"><span data-stu-id="1371a-121">How toomonitor rowgroup quality</span></span>

<span data-ttu-id="1371a-122">Não há DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expõe informações úteis, tais como o número de linhas na rowgroups e Olá razão para corte se foi corte não existe.</span><span class="sxs-lookup"><span data-stu-id="1371a-122">There is a DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) that exposes useful information such as number of rows in rowgroups and hello reason for trimming if there was trimming.</span></span> <span data-ttu-id="1371a-123">Pode criar Olá vista como tooquery uma forma útil de seguir estas informações de tooget DMV em rowgroup corte.</span><span class="sxs-lookup"><span data-stu-id="1371a-123">You can create hello following view as a handy way tooquery this DMV tooget information on rowgroup trimming.</span></span>

```sql
create view dbo.vCS_rg_physical_stats
as 
with cte
as
(
select   tb.[name]                    AS [logical_table_name]
,        rg.[row_group_id]            AS [row_group_id]
,        rg.[state]                   AS [state]
,        rg.[state_desc]              AS [state_desc]
,        rg.[total_rows]              AS [total_rows]
,        rg.[trim_reason_desc]        AS trim_reason_desc
,        mp.[physical_name]           AS physical_name
FROM    sys.[schemas] sm
JOIN    sys.[tables] tb               ON  sm.[schema_id]          = tb.[schema_id]                             
JOIN    sys.[pdw_table_mappings] mp   ON  tb.[object_id]          = mp.[object_id]
JOIN    sys.[pdw_nodes_tables] nt     ON  nt.[name]               = mp.[physical_name]
JOIN    sys.[dm_pdw_nodes_db_column_store_row_group_physical_stats] rg      ON  rg.[object_id]     = nt.[object_id]
                                                                            AND rg.[pdw_node_id]   = nt.[pdw_node_id]
                                        AND rg.[distribution_id]    = nt.[distribution_id]                                          
)
select *
from cte;
```

<span data-ttu-id="1371a-124">Olá trim_reason_desc indica se foi cortada Olá rowgroup (trim_reason_desc = NO_TRIM implica não ocorreu nenhuma corte e grupo de linhas de qualidade ideal).</span><span class="sxs-lookup"><span data-stu-id="1371a-124">hello trim_reason_desc tells whether hello rowgroup was trimmed(trim_reason_desc = NO_TRIM implies there was no trimming and row group is of optimal quality).</span></span> <span data-ttu-id="1371a-125">Olá pelas seguintes razões compactação indicam prematuro corte de Olá rowgroup:</span><span class="sxs-lookup"><span data-stu-id="1371a-125">hello following trim reasons indicate premature trimming of hello rowgroup:</span></span>
- <span data-ttu-id="1371a-126">BULKLOAD: Esta compactação motivo é utilizado quando o lote de entrada Olá das linhas de carga Olá tinha inferior a 1 milhões de linhas.</span><span class="sxs-lookup"><span data-stu-id="1371a-126">BULKLOAD: This trim reason is used when hello incoming batch of rows for hello load had less than 1 million rows.</span></span> <span data-ttu-id="1371a-127">motor de Olá irá criar grupos de linhas comprimido se existem superior a 100.000 linhas que está a ser inseridas (como oposição ao tooinserting para arquivo de diferenças Olá) mas conjuntos Olá tooBULKLOAD razão de compactação.</span><span class="sxs-lookup"><span data-stu-id="1371a-127">hello engine will create compressed row groups if there are greater than 100,000 rows being inserted (as opposed tooinserting into hello delta store) but sets hello trim reason tooBULKLOAD.</span></span> <span data-ttu-id="1371a-128">Neste cenário, é aconselhável aumentar o tooaccumulate de janela de carga de lote mais linhas.</span><span class="sxs-lookup"><span data-stu-id="1371a-128">In this scenario, consider increasing your batch load window tooaccumulate more rows.</span></span> <span data-ttu-id="1371a-129">Além disso, reevaluate a criação de partições tooensure de esquema não está demasiado granular como grupos de linhas não podem abranger limites de partição.</span><span class="sxs-lookup"><span data-stu-id="1371a-129">Also, reevaluate your partitioning scheme tooensure it is not too granular as row groups cannot span partition boundaries.</span></span>
- <span data-ttu-id="1371a-130">MEMORY_LIMITATION: toocreate grupos de linhas com 1 milhões de linhas, uma determinada quantidade de memória de trabalho é necessário pelo motor de Olá.</span><span class="sxs-lookup"><span data-stu-id="1371a-130">MEMORY_LIMITATION: toocreate row groups with 1 million rows, a certain amount of working memory is required by hello engine.</span></span> <span data-ttu-id="1371a-131">Quando a memória disponível de Olá carregar sessão é inferior ao hello necessário trabalhar memória, grupos de linhas prematuramente obterem recortados.</span><span class="sxs-lookup"><span data-stu-id="1371a-131">When available memory of hello loading session is less than hello required working memory, row groups get prematurely trimmed.</span></span> <span data-ttu-id="1371a-132">Olá secções a seguir explica como tooestimate memória necessária e alocar mais memória.</span><span class="sxs-lookup"><span data-stu-id="1371a-132">hello following sections explain how tooestimate memory required and allocate more memory.</span></span>
- <span data-ttu-id="1371a-133">DICTIONARY_SIZE: Esta compactação razão indica que corte rowgroup ocorreu porque ocorreu pelo menos uma coluna de cadeia com cadeias de cardinalidade abrangente e/ou elevado.</span><span class="sxs-lookup"><span data-stu-id="1371a-133">DICTIONARY_SIZE: This trim reason indicates that rowgroup trimming occurred because there was at least one string column with wide and/or high cardinality strings.</span></span> <span data-ttu-id="1371a-134">o tamanho de dicionário de Olá é limitado too16 MB na memória e assim que este limite for atingido o grupo de linhas de Olá é comprimido.</span><span class="sxs-lookup"><span data-stu-id="1371a-134">hello dictionary size is limited too16 MB in memory and once this limit is reached hello row group is compressed.</span></span> <span data-ttu-id="1371a-135">Caso se depare com esta situação, considere isolar coluna problemáticas Olá numa tabela separada.</span><span class="sxs-lookup"><span data-stu-id="1371a-135">If you do run into this situation, consider isolating hello problematic column into a separate table.</span></span>

## <a name="how-tooestimate-memory-requirements"></a><span data-ttu-id="1371a-136">Como os requisitos de memória tooestimate</span><span class="sxs-lookup"><span data-stu-id="1371a-136">How tooestimate memory requirements</span></span>

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

<span data-ttu-id="1371a-137">Olá máximo de memória necessária toocompress um rowgroup é aproximadamente</span><span class="sxs-lookup"><span data-stu-id="1371a-137">hello maximum required memory toocompress one rowgroup is approximately</span></span>

- <span data-ttu-id="1371a-138">72 MB +</span><span class="sxs-lookup"><span data-stu-id="1371a-138">72 MB +</span></span>
- <span data-ttu-id="1371a-139">\#linhas \* \#colunas \* 8 bytes +</span><span class="sxs-lookup"><span data-stu-id="1371a-139">\#rows \* \#columns \* 8 bytes +</span></span>
- <span data-ttu-id="1371a-140">\#linhas \* \#colunas de cadeia curta \* 32 bytes +</span><span class="sxs-lookup"><span data-stu-id="1371a-140">\#rows \* \#short-string-columns \* 32 bytes +</span></span>
- <span data-ttu-id="1371a-141">\#colunas de cadeia longa \* 16 MB de dicionário de compressão</span><span class="sxs-lookup"><span data-stu-id="1371a-141">\#long-string-columns \* 16 MB for compression dictionary</span></span>

<span data-ttu-id="1371a-142">em colunas de cadeia curta utilizam tipos de dados de cadeia de < = 32 bytes e tipos de dados de cadeia de utilização de colunas de cadeia longa de > 32 bytes.</span><span class="sxs-lookup"><span data-stu-id="1371a-142">where short-string-columns use string data types of <= 32 bytes and long-string-columns use string data types of > 32 bytes.</span></span>

<span data-ttu-id="1371a-143">Cadeias de longas são comprimidas com um método de compressão concebido para a compressão de texto.</span><span class="sxs-lookup"><span data-stu-id="1371a-143">Long strings are compressed with a compression method designed for compressing text.</span></span> <span data-ttu-id="1371a-144">Este método de compressão utiliza um *dicionário* toostore padrões de texto.</span><span class="sxs-lookup"><span data-stu-id="1371a-144">This compression method uses a *dictionary* toostore text patterns.</span></span> <span data-ttu-id="1371a-145">tamanho máximo do Olá de um dicionário é 16 MB.</span><span class="sxs-lookup"><span data-stu-id="1371a-145">hello maximum size of a dictionary is 16 MB.</span></span> <span data-ttu-id="1371a-146">Não há apenas um dicionário para cada coluna de cadeia longo na Olá rowgroup.</span><span class="sxs-lookup"><span data-stu-id="1371a-146">There is only one dictionary for each long string column in hello rowgroup.</span></span>

<span data-ttu-id="1371a-147">Para um debate aprofundado sobre os requisitos de memória columnstore, veja o vídeo [Azure SQL Data Warehouse dimensionamento: configuração e as orientações](https://myignite.microsoft.com/videos/14822).</span><span class="sxs-lookup"><span data-stu-id="1371a-147">For an in-depth discussion of columnstore memory requirements, see the video [Azure SQL Data Warehouse scaling: configuration and guidance](https://myignite.microsoft.com/videos/14822).</span></span>

## <a name="ways-tooreduce-memory-requirements"></a><span data-ttu-id="1371a-148">Requisitos de memória de tooreduce de formas</span><span class="sxs-lookup"><span data-stu-id="1371a-148">Ways tooreduce memory requirements</span></span>

<span data-ttu-id="1371a-149">Utilize Olá seguintes técnicas tooreduce Olá os requisitos de memória para a compressão rowgroups em índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="1371a-149">Use hello following techniques tooreduce hello memory requirements for compressing rowgroups into columnstore indexes.</span></span>

### <a name="use-fewer-columns"></a><span data-ttu-id="1371a-150">Utilizar menos colunas</span><span class="sxs-lookup"><span data-stu-id="1371a-150">Use fewer columns</span></span>
<span data-ttu-id="1371a-151">Se for possível, estruture tabela Olá com menos colunas.</span><span class="sxs-lookup"><span data-stu-id="1371a-151">If possible, design hello table with fewer columns.</span></span> <span data-ttu-id="1371a-152">Quando um rowgroup é comprimido para columnstore Olá, o índice columnstore Olá comprime cada segmento de coluna em separado.</span><span class="sxs-lookup"><span data-stu-id="1371a-152">When a rowgroup is compressed into hello columnstore, hello columnstore index compresses each column segment separately.</span></span> <span data-ttu-id="1371a-153">Olá, por conseguinte, os requisitos de memória toocompress um rowgroup aumentar como número de Olá de aumentos de colunas.</span><span class="sxs-lookup"><span data-stu-id="1371a-153">Therefore hello memory requirements toocompress a rowgroup increase as hello number of columns increases.</span></span>


### <a name="use-fewer-string-columns"></a><span data-ttu-id="1371a-154">Utilizar menos colunas de cadeia</span><span class="sxs-lookup"><span data-stu-id="1371a-154">Use fewer string columns</span></span>
<span data-ttu-id="1371a-155">Colunas de tipos de dados de cadeia requerem mais memória do que um valor numérico e tipos de dados de data.</span><span class="sxs-lookup"><span data-stu-id="1371a-155">Columns of string data types require more memory than numeric and date data types.</span></span> <span data-ttu-id="1371a-156">requisitos de memória tooreduce, considere remover colunas de cadeia de tabelas de factos e colocando-as nas tabelas de dimensão mais pequena.</span><span class="sxs-lookup"><span data-stu-id="1371a-156">tooreduce memory requirements, consider removing string columns from fact tables and putting them in smaller dimension tables.</span></span>

<span data-ttu-id="1371a-157">Requisitos de memória adicional para compressão de cadeia:</span><span class="sxs-lookup"><span data-stu-id="1371a-157">Additional memory requirements for string compression:</span></span>

- <span data-ttu-id="1371a-158">Tipos de dados de cadeia segurança too32 carateres podem exigir a 32 bytes adicionais por valor.</span><span class="sxs-lookup"><span data-stu-id="1371a-158">String data types up too32 characters can require 32 additional bytes per value.</span></span>
- <span data-ttu-id="1371a-159">Tipos de dados de cadeia com mais do que 32 carateres são comprimidos através de métodos de dicionário.</span><span class="sxs-lookup"><span data-stu-id="1371a-159">String data types with more than 32 characters are compressed using dictionary methods.</span></span>  <span data-ttu-id="1371a-160">Cada coluna no Olá rowgroup pode exigir a cópia de segurança dicionário de Olá de toobuild tooan adicionais 16 MB.</span><span class="sxs-lookup"><span data-stu-id="1371a-160">Each column in hello rowgroup can require up tooan additional 16 MB toobuild hello dictionary.</span></span>

### <a name="avoid-over-partitioning"></a><span data-ttu-id="1371a-161">Evitar a criação de partições excessiva</span><span class="sxs-lookup"><span data-stu-id="1371a-161">Avoid over-partitioning</span></span>

<span data-ttu-id="1371a-162">Os índices Columnstore criar um ou mais rowgroups por partição.</span><span class="sxs-lookup"><span data-stu-id="1371a-162">Columnstore indexes create one or more rowgroups per partition.</span></span> <span data-ttu-id="1371a-163">No SQL Data Warehouse, número de Olá de partições cresce rapidamente, porque os dados de Olá são distribuídos e cada distribuição está particionada.</span><span class="sxs-lookup"><span data-stu-id="1371a-163">In SQL Data Warehouse, hello number of partitions grows quickly because hello data is distributed and each distribution is partitioned.</span></span> <span data-ttu-id="1371a-164">Se a tabela de Olá tem demasiados partições, poderão não existir suficiente rowgroups de Olá toofill linhas.</span><span class="sxs-lookup"><span data-stu-id="1371a-164">If hello table has too many partitions, there might not be enough rows toofill hello rowgroups.</span></span> <span data-ttu-id="1371a-165">falta de Olá de linhas não cria pressão de memória durante a compressão, mas servem como toorowgroups não conseguir Olá melhor columnstore desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="1371a-165">hello lack of rows does not create memory pressure during compression, but it leads toorowgroups that do not achieve hello best columnstore query performance.</span></span>

<span data-ttu-id="1371a-166">Outro motivo tooavoid excessiva criação de partições é há uma memória sobrecarga de carregamento linhas para um índice columnstore numa tabela particionada.</span><span class="sxs-lookup"><span data-stu-id="1371a-166">Another reason tooavoid over-partitioning is there is a memory overhead for loading rows into a columnstore index on a partitioned table.</span></span> <span data-ttu-id="1371a-167">Durante uma carga várias partições foi receber linhas entrada Olá, que são guardadas na memória até cada partição tem suficiente toobe linhas comprimido.</span><span class="sxs-lookup"><span data-stu-id="1371a-167">During a load, many partitions could receive hello incoming rows, which are held in memory until each partition has enough rows toobe compressed.</span></span> <span data-ttu-id="1371a-168">Ter partições demasiados cria pressão de memória adicional.</span><span class="sxs-lookup"><span data-stu-id="1371a-168">Having too many partitions creates additional memory pressure.</span></span>

### <a name="simplify-hello-load-query"></a><span data-ttu-id="1371a-169">Simplificar a consulta de carga Olá</span><span class="sxs-lookup"><span data-stu-id="1371a-169">Simplify hello load query</span></span>

<span data-ttu-id="1371a-170">Olá da base de dados partilhas Olá concessão de memória para uma consulta entre todos os operadores de Olá na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="1371a-170">hello database shares hello memory grant for a query among all hello operators in hello query.</span></span> <span data-ttu-id="1371a-171">Quando uma consulta de carga tem tipos complexos e associações, é reduzida memória Olá disponível para compressão.</span><span class="sxs-lookup"><span data-stu-id="1371a-171">When a load query has complex sorts and joins, hello memory available for compression is reduced.</span></span>

<span data-ttu-id="1371a-172">Design Olá carga consulta toofocus apenas em carregar Olá consulta.</span><span class="sxs-lookup"><span data-stu-id="1371a-172">Design hello load query toofocus only on loading hello query.</span></span> <span data-ttu-id="1371a-173">Se precisar de transformações de toorun nos dados de Olá, executá-los separada da consulta de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="1371a-173">If you need toorun transformations on hello data, run them separate from hello load query.</span></span> <span data-ttu-id="1371a-174">Por exemplo, fase Olá numa tabela Área dinâmica para dados, execução transformações Olá e, em seguida, carregar Olá tabela de teste para o índice columnstore Olá.</span><span class="sxs-lookup"><span data-stu-id="1371a-174">For example, stage hello data in a heap table, run hello transformations, and then load hello staging table into hello columnstore index.</span></span> <span data-ttu-id="1371a-175">Pode também carregar os dados de Olá primeiro e, em seguida, utilizar Olá MPP tootransform Olá os dados sistema.</span><span class="sxs-lookup"><span data-stu-id="1371a-175">You can also load hello data first and then use hello MPP system tootransform hello data.</span></span>

### <a name="adjust-maxdop"></a><span data-ttu-id="1371a-176">Ajustar MAXDOP</span><span class="sxs-lookup"><span data-stu-id="1371a-176">Adjust MAXDOP</span></span>

<span data-ttu-id="1371a-177">Cada distribuição comprime rowgroups no columnstore Olá em paralelo quando existe mais do que um núcleo de CPU disponíveis por distribuição.</span><span class="sxs-lookup"><span data-stu-id="1371a-177">Each distribution compresses rowgroups into hello columnstore in parallel when there is more than one CPU core available per distribution.</span></span> <span data-ttu-id="1371a-178">paralelismo Olá necessita de recursos de memória adicional, o que podem levar toomemory pressão e rowgroup corte.</span><span class="sxs-lookup"><span data-stu-id="1371a-178">hello parallelism requires additional memory resources, which can lead toomemory pressure and rowgroup trimming.</span></span>

<span data-ttu-id="1371a-179">tooreduce pressão de memória, pode utilizar Olá MAXDOP consulta sugestão tooforce Olá carga operação toorun no modo de série dentro de cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="1371a-179">tooreduce memory pressure, you can use hello MAXDOP query hint tooforce hello load operation toorun in serial mode within each distribution.</span></span>

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a><span data-ttu-id="1371a-180">Formas tooallocate mais memória</span><span class="sxs-lookup"><span data-stu-id="1371a-180">Ways tooallocate more memory</span></span>

<span data-ttu-id="1371a-181">DWU tamanho e Olá utilizador classe de recursos em conjunto determinam a quantidade de memória está disponível para uma consulta do utilizador.</span><span class="sxs-lookup"><span data-stu-id="1371a-181">DWU size and hello user resource class together determine how much memory is available for a user query.</span></span> <span data-ttu-id="1371a-182">memória de Olá tooincrease conceder para uma consulta de carga, pode aumentar o número de Olá de DWUs ou aumentar a classe de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="1371a-182">tooincrease hello memory grant for a load query, you can either increase hello number of DWUs or increase hello resource class.</span></span>

- <span data-ttu-id="1371a-183">Olá tooincrease DWUs, consulte [como aumentar o desempenho?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span><span class="sxs-lookup"><span data-stu-id="1371a-183">tooincrease hello DWUs, see [How do I scale performance?](sql-data-warehouse-manage-compute-overview.md#scale-compute)</span></span>
- <span data-ttu-id="1371a-184">classe de recursos de Olá toochange para uma consulta, consulte [alterar um exemplo de classe de recursos de utilizador](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span><span class="sxs-lookup"><span data-stu-id="1371a-184">toochange hello resource class for a query, see [Change a user resource class example](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).</span></span>

<span data-ttu-id="1371a-185">Por exemplo, no DWU 100 um utilizador na classe de recursos de smallrc Olá pode utilizar a 100 MB de memória para cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="1371a-185">For example, on DWU 100 a user in hello smallrc resource class can use 100 MB of memory for each distribution.</span></span> <span data-ttu-id="1371a-186">Para detalhes de Olá, consulte [simultaneidade no SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span><span class="sxs-lookup"><span data-stu-id="1371a-186">For hello details, see [Concurrency in SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).</span></span>

<span data-ttu-id="1371a-187">Suponha que determine que tem de 700 MB de tamanhos de alta qualidade rowgroup tooget de memória.</span><span class="sxs-lookup"><span data-stu-id="1371a-187">Suppose you determine that you need 700 MB of memory tooget high-quality rowgroup sizes.</span></span> <span data-ttu-id="1371a-188">Estes exemplos mostram como pode executar a consulta de carga Olá com memória suficiente.</span><span class="sxs-lookup"><span data-stu-id="1371a-188">These examples show how you can run hello load query with enough memory.</span></span>

- <span data-ttu-id="1371a-189">DWU 1000 e mediumrc, a concessão de memória é utilizar 800 MB</span><span class="sxs-lookup"><span data-stu-id="1371a-189">Using DWU 1000 and mediumrc, your memory grant is 800 MB</span></span>
- <span data-ttu-id="1371a-190">A utilização de DWU 600 e largerc, a concessão de memória é 800 MB.</span><span class="sxs-lookup"><span data-stu-id="1371a-190">Using DWU 600 and largerc, your memory grant is 800 MB.</span></span>


## <a name="next-steps"></a><span data-ttu-id="1371a-191">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="1371a-191">Next steps</span></span>

<span data-ttu-id="1371a-192">toofind mais formas tooimprove um desempenho no SQL Data Warehouse, consulte Olá [descrição geral do desempenho](sql-data-warehouse-overview-manage-user-queries.md).</span><span class="sxs-lookup"><span data-stu-id="1371a-192">toofind more ways tooimprove performance in SQL Data Warehouse, see hello [Performance overview](sql-data-warehouse-overview-manage-user-queries.md).</span></span>

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
