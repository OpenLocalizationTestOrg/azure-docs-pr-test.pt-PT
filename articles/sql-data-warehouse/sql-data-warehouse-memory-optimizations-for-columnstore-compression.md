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
# <a name="maximizing-rowgroup-quality-for-columnstore"></a>Maximizar a forma de qualidade de rowgroup para columnstore

Qualidade de Rowgroup é determinada pelo número de Olá de linhas num rowgroup. Reduza os requisitos de memória ou aumentar Olá memória disponível toomaximize Olá número de linhas que comprime um índice columnstore em cada rowgroup.  Utilize estas taxas de compressão tooimprove de métodos e o desempenho das consultas para índices columnstore.

## <a name="why-hello-rowgroup-size-matters"></a>Por que motivo o tamanho de rowgroup Olá é importante
Uma vez que um índice columnstore analisa uma tabela através da análise de segmentos de coluna de rowgroups individuais, maximizando a número Olá de linhas em cada rowgroup melhora o desempenho de consulta. Quando rowgroups tem um elevado número de linhas, compressão de dados melhora o que significa que há menos tooread de dados do disco.

Para mais informações sobre rowgroups, consulte [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).

## <a name="target-size-for-rowgroups"></a>Tamanho de destino para rowgroups
Para melhor desempenho das consultas, o objetivo de Olá é toomaximize Olá número de linhas por rowgroup num índice columnstore. Um rowgroup pode ter um máximo de 1.048.576 linhas. Toonot pode ter Olá número máximo de linhas por rowgroup. Os índices Columnstore alcançarem o bom desempenho quando rowgroups tem, pelo menos, 100 000 linhas.

## <a name="rowgroups-can-get-trimmed-during-compression"></a>Pode obter cortada Rowgroups durante a compressão

Durante uma em massa de carga ou columnstore índice reconstrução, por vezes, não existe não é suficiente toocompress disponíveis de memória que Olá todas as linhas designadas para cada rowgroup. Quando existe pressão de memória, os índices columnstore compactar tamanhos de rowgroup Olá para que compressão no columnstore Olá pode ter êxito. 

Quando existe linhas toocompress, pelo menos, 10 000 de memória insuficiente para cada rowgroup, o SQL Data Warehouse gera um erro.

Para obter mais informações sobre o carregamento em massa, consulte [carregamento em massa para um índice columnstore em cluster](https://msdn.microsoft.com/en-us/library/dn935008.aspx#Bulk load into a clustered columnstore index).

## <a name="how-toomonitor-rowgroup-quality"></a>Como toomonitor rowgroup qualidade

Não há DMV (sys.dm_pdw_nodes_db_column_store_row_group_physical_stats) que expõe informações úteis, tais como o número de linhas na rowgroups e Olá razão para corte se foi corte não existe. Pode criar Olá vista como tooquery uma forma útil de seguir estas informações de tooget DMV em rowgroup corte.

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

Olá trim_reason_desc indica se foi cortada Olá rowgroup (trim_reason_desc = NO_TRIM implica não ocorreu nenhuma corte e grupo de linhas de qualidade ideal). Olá pelas seguintes razões compactação indicam prematuro corte de Olá rowgroup:
- BULKLOAD: Esta compactação motivo é utilizado quando o lote de entrada Olá das linhas de carga Olá tinha inferior a 1 milhões de linhas. motor de Olá irá criar grupos de linhas comprimido se existem superior a 100.000 linhas que está a ser inseridas (como oposição ao tooinserting para arquivo de diferenças Olá) mas conjuntos Olá tooBULKLOAD razão de compactação. Neste cenário, é aconselhável aumentar o tooaccumulate de janela de carga de lote mais linhas. Além disso, reevaluate a criação de partições tooensure de esquema não está demasiado granular como grupos de linhas não podem abranger limites de partição.
- MEMORY_LIMITATION: toocreate grupos de linhas com 1 milhões de linhas, uma determinada quantidade de memória de trabalho é necessário pelo motor de Olá. Quando a memória disponível de Olá carregar sessão é inferior ao hello necessário trabalhar memória, grupos de linhas prematuramente obterem recortados. Olá secções a seguir explica como tooestimate memória necessária e alocar mais memória.
- DICTIONARY_SIZE: Esta compactação razão indica que corte rowgroup ocorreu porque ocorreu pelo menos uma coluna de cadeia com cadeias de cardinalidade abrangente e/ou elevado. o tamanho de dicionário de Olá é limitado too16 MB na memória e assim que este limite for atingido o grupo de linhas de Olá é comprimido. Caso se depare com esta situação, considere isolar coluna problemáticas Olá numa tabela separada.

## <a name="how-tooestimate-memory-requirements"></a>Como os requisitos de memória tooestimate

<!--
tooview an estimate of hello memory requirements toocompress a rowgroup of maximum size into a columnstore index, download and run hello view [dbo.vCS_mon_mem_grant](). This view shows hello size of hello memory grant that a rowgroup requires for compression in toohello columnstore.
-->

Olá máximo de memória necessária toocompress um rowgroup é aproximadamente

- 72 MB +
- \#linhas \* \#colunas \* 8 bytes +
- \#linhas \* \#colunas de cadeia curta \* 32 bytes +
- \#colunas de cadeia longa \* 16 MB de dicionário de compressão

em colunas de cadeia curta utilizam tipos de dados de cadeia de < = 32 bytes e tipos de dados de cadeia de utilização de colunas de cadeia longa de > 32 bytes.

Cadeias de longas são comprimidas com um método de compressão concebido para a compressão de texto. Este método de compressão utiliza um *dicionário* toostore padrões de texto. tamanho máximo do Olá de um dicionário é 16 MB. Não há apenas um dicionário para cada coluna de cadeia longo na Olá rowgroup.

Para um debate aprofundado sobre os requisitos de memória columnstore, veja o vídeo [Azure SQL Data Warehouse dimensionamento: configuração e as orientações](https://myignite.microsoft.com/videos/14822).

## <a name="ways-tooreduce-memory-requirements"></a>Requisitos de memória de tooreduce de formas

Utilize Olá seguintes técnicas tooreduce Olá os requisitos de memória para a compressão rowgroups em índices columnstore.

### <a name="use-fewer-columns"></a>Utilizar menos colunas
Se for possível, estruture tabela Olá com menos colunas. Quando um rowgroup é comprimido para columnstore Olá, o índice columnstore Olá comprime cada segmento de coluna em separado. Olá, por conseguinte, os requisitos de memória toocompress um rowgroup aumentar como número de Olá de aumentos de colunas.


### <a name="use-fewer-string-columns"></a>Utilizar menos colunas de cadeia
Colunas de tipos de dados de cadeia requerem mais memória do que um valor numérico e tipos de dados de data. requisitos de memória tooreduce, considere remover colunas de cadeia de tabelas de factos e colocando-as nas tabelas de dimensão mais pequena.

Requisitos de memória adicional para compressão de cadeia:

- Tipos de dados de cadeia segurança too32 carateres podem exigir a 32 bytes adicionais por valor.
- Tipos de dados de cadeia com mais do que 32 carateres são comprimidos através de métodos de dicionário.  Cada coluna no Olá rowgroup pode exigir a cópia de segurança dicionário de Olá de toobuild tooan adicionais 16 MB.

### <a name="avoid-over-partitioning"></a>Evitar a criação de partições excessiva

Os índices Columnstore criar um ou mais rowgroups por partição. No SQL Data Warehouse, número de Olá de partições cresce rapidamente, porque os dados de Olá são distribuídos e cada distribuição está particionada. Se a tabela de Olá tem demasiados partições, poderão não existir suficiente rowgroups de Olá toofill linhas. falta de Olá de linhas não cria pressão de memória durante a compressão, mas servem como toorowgroups não conseguir Olá melhor columnstore desempenho das consultas.

Outro motivo tooavoid excessiva criação de partições é há uma memória sobrecarga de carregamento linhas para um índice columnstore numa tabela particionada. Durante uma carga várias partições foi receber linhas entrada Olá, que são guardadas na memória até cada partição tem suficiente toobe linhas comprimido. Ter partições demasiados cria pressão de memória adicional.

### <a name="simplify-hello-load-query"></a>Simplificar a consulta de carga Olá

Olá da base de dados partilhas Olá concessão de memória para uma consulta entre todos os operadores de Olá na consulta de Olá. Quando uma consulta de carga tem tipos complexos e associações, é reduzida memória Olá disponível para compressão.

Design Olá carga consulta toofocus apenas em carregar Olá consulta. Se precisar de transformações de toorun nos dados de Olá, executá-los separada da consulta de carga Olá. Por exemplo, fase Olá numa tabela Área dinâmica para dados, execução transformações Olá e, em seguida, carregar Olá tabela de teste para o índice columnstore Olá. Pode também carregar os dados de Olá primeiro e, em seguida, utilizar Olá MPP tootransform Olá os dados sistema.

### <a name="adjust-maxdop"></a>Ajustar MAXDOP

Cada distribuição comprime rowgroups no columnstore Olá em paralelo quando existe mais do que um núcleo de CPU disponíveis por distribuição. paralelismo Olá necessita de recursos de memória adicional, o que podem levar toomemory pressão e rowgroup corte.

tooreduce pressão de memória, pode utilizar Olá MAXDOP consulta sugestão tooforce Olá carga operação toorun no modo de série dentro de cada distribuição.

```
CREATE TABLE MyFactSalesQuota
WITH (DISTRIBUTION = ROUND_ROBIN)
AS SELECT * FROM FactSalesQUota
OPTION (MAXDOP 1);
```

## <a name="ways-tooallocate-more-memory"></a>Formas tooallocate mais memória

DWU tamanho e Olá utilizador classe de recursos em conjunto determinam a quantidade de memória está disponível para uma consulta do utilizador. memória de Olá tooincrease conceder para uma consulta de carga, pode aumentar o número de Olá de DWUs ou aumentar a classe de recursos de Olá.

- Olá tooincrease DWUs, consulte [como aumentar o desempenho?](sql-data-warehouse-manage-compute-overview.md#scale-compute)
- classe de recursos de Olá toochange para uma consulta, consulte [alterar um exemplo de classe de recursos de utilizador](sql-data-warehouse-develop-concurrency.md#changing-user-resource-class-example).

Por exemplo, no DWU 100 um utilizador na classe de recursos de smallrc Olá pode utilizar a 100 MB de memória para cada distribuição. Para detalhes de Olá, consulte [simultaneidade no SQL Data Warehouse](sql-data-warehouse-develop-concurrency.md).

Suponha que determine que tem de 700 MB de tamanhos de alta qualidade rowgroup tooget de memória. Estes exemplos mostram como pode executar a consulta de carga Olá com memória suficiente.

- DWU 1000 e mediumrc, a concessão de memória é utilizar 800 MB
- A utilização de DWU 600 e largerc, a concessão de memória é 800 MB.


## <a name="next-steps"></a>Passos seguintes

toofind mais formas tooimprove um desempenho no SQL Data Warehouse, consulte Olá [descrição geral do desempenho](sql-data-warehouse-overview-manage-user-queries.md).

<!--Image references-->

<!--Article references-->


<!--MSDN references-->

<!--Other Web references-->
