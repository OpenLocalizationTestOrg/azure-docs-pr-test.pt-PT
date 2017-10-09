---
title: "estatísticas de aaaManaging em tabelas no armazém de dados SQL | Microsoft Docs"
description: "Introdução ao estatísticas de tabelas do Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: jhubbard
editor: 
ms.assetid: faa1034d-314c-4f9d-af81-f5a9aedf33e4
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: c9521dc47891f68d124e77a53e2e15d03275caaa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a>Gerir as estatísticas em tabelas no armazém de dados do SQL Server
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

Hello mais SQL Data Warehouse conhece os dados, hello mais rapidamente do pode executar consultas nos dados.  forma Olá que dizem ao SQL Data Warehouse sobre os dados, é através da recolha de estatísticas sobre os dados.  Ter estatísticas nos seus dados é um dos aspetos mais importantes Olá, pode fazê-lo toooptimize as suas consultas.  Estatísticas de ajudam a criar Olá plano ideal para consultas do SQL Data Warehouse.  Isto acontece porque a consulta de SQL Data Warehouse Olá otimizador é um custo com otimizador de base.  Ou seja, compara o custo de Olá de vários planos de consulta e, em seguida, escolhe Olá plano com Olá menor custo, que também deve ser o plano de Olá que irão executar Olá mais rápido.

Podem ser criadas estatísticas no única coluna, várias colunas ou um índice de uma tabela.  As estatísticas são armazenadas num histograma que captura intervalo Olá e selectivity dos valores.  Esta é a do especial interesse dos quando precisa de otimizador de Olá tooevaluate associações, GROUP BY, HAVING e cláusulas WHERE numa consulta.  Por exemplo, se o otimizador de Olá calcula que data Olá são filtragem na sua consulta devolverá 1 linha, pode escolher a muito diferentes planear que o se se estimativas que data selecionou irá devolver 1 milhões de linhas.  Enquanto é extremamente importante criar estatísticas, é igualmente importante que estatísticas *com precisão* refletir Olá estado atual da tabela de Olá.  Ter estatísticas atualizadas garante que um bom plano está selecionado por otimizador de Olá.  os planos de Olá criados por otimizador de Olá só estão como boas como estatísticas de Olá nos seus dados.

Olá o processo de criação e a atualizar as estatísticas é atualmente um processo manual, mas é toodo muito simple.  Tal não acontecia no SQL Server, que cria e atualiza as estatísticas de índices e colunas único automaticamente.  Ao utilizar as informações de Olá abaixo, pode significativamente automatizar a gestão de Olá das estatísticas de Olá nos seus dados. 

## <a name="getting-started-with-statistics"></a>Introdução ao estatísticas
 Criar estatísticas amostras em cada coluna é uma forma fácil tooget iniciado com as estatísticas.  Uma vez que é igualmente importante tookeep estatísticas atualizadas, uma abordagem conservador poderá ser tooupdate as estatísticas diariamente ou após cada carga. São sempre compromissos entre o desempenho e Olá custo toocreate e atualizar as estatísticas.  Se encontrar estiver a demorar demasiado tempo toomaintain todas as estatísticas, poderá precisa de induzirem tootry toobe mais seletiva sobre as colunas que tem as estatísticas ou as colunas frequentes atualizar.  Por exemplo, é aconselhável colunas de data tooupdate diariamente, como podem ser adicionados novos valores em vez de após cada carga. Novamente, irá obter Olá benefício a maioria das, fazendo com que as estatísticas em colunas envolvidas em associações, GROUP BY, HAVING e cláusulas WHERE.  Se tiver uma tabela com uma grande quantidade de colunas que apenas são utilizadas em Olá SELECIONAR cláusula, estatísticas destas colunas não podem ajudar e gastos um pequeno tooidentify esforço mais Olá as colunas onde irão ajudar a estatísticas, pode reduzir Olá tempo toomaintain as estatísticas .

## <a name="multi-column-statistics"></a>Estatísticas de várias colunas
Além disso toocreating estatísticas em colunas único, pode considerar que as suas consultas irão beneficiar de estatísticas de várias colunas.  Estatísticas de várias colunas são criadas numa lista de colunas de estatísticas.  Incluem estatísticas de coluna única na primeira coluna de Olá na lista de Olá, mais algumas informações de correlação entre coluna chamado densities.  Por exemplo, se tiver uma tabela que associa tooanother duas colunas, pode considerar que o SQL Data Warehouse pode otimizar melhor plano Olá se compreende relação Olá entre duas colunas.   Estatísticas de várias colunas podem melhorar o desempenho de consulta para algumas operações, tais como associações compostas e agrupar por.

## <a name="updating-statistics"></a>A atualizar as estatísticas
A atualizar as estatísticas é uma parte importante da sua rotina de gestão de base de dados.  Quando altera a distribuição de Olá dos dados na base de dados de Olá, estatísticas tem toobe atualizado.  Estatísticas Desatualizadas direciona o desempenho das consultas toosub ideal.

Uma melhor prática é tooupdate estatísticas em colunas de data por dia datas novas são adicionadas.  Cada novas linhas de tempo são carregados para o armazém de dados de Olá, datas de carga novo ou datas de transação são adicionadas. Estes alterar a distribuição de dados de Olá e certifique-estatísticas Olá desatualizados. Por outro lado, estatísticas de uma coluna de país numa tabela cliente nunca poderão ter toobe atualizado, como a distribuição de Olá de valores, geralmente, não irá alterar. Partindo do princípio de distribuição de Olá é constante entre os clientes, adicionar nova variação de tabela de toohello linhas não vai distribuição de dados de Olá toochange. No entanto, se o armazém de dados contém apenas um país e colocar dados de um novo país, resultando em dados a partir de vários países que está a ser armazenados, em seguida, sem dúvida terá tooupdate estatísticas na coluna de país Olá.

Um dos Olá tooask de perguntas primeiro quando uma consulta de resolução de problemas, "estão estatísticas Olá atualizados?"

Esta questão não é um que pode ser respondida por antiguidade Olá dos dados de Olá. Um objeto de estatísticas de toodate se pode ser muito antigo não se tiver ocorrido toohello nenhuma alteração materiais subjacente dados. Quando Olá número de linhas alterado substancialmente ou existe uma alteração na distribuição Olá de valores para uma determinada coluna materiais *, em seguida,* é as estatísticas de tooupdate de tempo.  

Para referência, **do SQL Server** (não o SQL Data Warehouse) atualiza automaticamente as estatísticas para estas situações:

* Se tiver zero linhas na tabela de Olá, quando adiciona linhas, obterá uma atualização automática de estatísticas
* Ao Adicionar tabela tooa mais do que 500 linhas, começando com menos de 500 linhas (por exemplo, no início tiver 499 e, em seguida, adicionar 500 total de tooa de linhas de 999 linhas), obterá uma atualização automática 
* Assim que tiver mais de 500 linhas terá tooadd 500 linhas de adicionais + 20% do tamanho de Olá da tabela de Olá antes, verá uma atualização automática no estatísticas Olá

Uma vez que não existe nenhum toodetermine DMV se dados numa tabela de Olá tem sido alterado desde que foram atualizadas as estatísticas de tempo último Olá, saber idade Olá das suas estatísticas pode fornecer com parte da imagem de Olá.  Pode utilizar Olá toodetermine Olá hora da última as estatísticas de consulta a seguir onde atualizadas em cada tabela.  

> [!NOTE]
> Lembre-se de que o se houver uma alteração essenciais na distribuição Olá de valores para uma determinada coluna, que deve atualizar estatísticas independentemente Olá hora da última que foram atualizados.  
> 
> 

```sql
SELECT
    sm.[name] AS [schema_name],
    tb.[name] AS [table_name],
    co.[name] AS [stats_column_name],
    st.[name] AS [stats_name],
    STATS_DATE(st.[object_id],st.[stats_id]) AS [stats_last_updated_date]
FROM
    sys.objects ob
    JOIN sys.stats st
        ON  ob.[object_id] = st.[object_id]
    JOIN sys.stats_columns sc    
        ON  st.[stats_id] = sc.[stats_id]
        AND st.[object_id] = sc.[object_id]
    JOIN sys.columns co    
        ON  sc.[column_id] = co.[column_id]
        AND sc.[object_id] = co.[object_id]
    JOIN sys.types  ty    
        ON  co.[user_type_id] = ty.[user_type_id]
    JOIN sys.tables tb    
        ON  co.[object_id] = tb.[object_id]
    JOIN sys.schemas sm    
        ON  tb.[schema_id] = sm.[schema_id]
WHERE
    st.[user_created] = 1;
```

Colunas de data no armazém de dados, por exemplo, normalmente, tem de induzirem frequentes estatísticas atualizações. Cada novas linhas de tempo são carregados para o armazém de dados de Olá, datas de carga novo ou datas de transação são adicionadas. Estes alterar a distribuição de dados de Olá e certifique-estatísticas Olá desatualizados.  Por outro lado, estatísticas de uma coluna de sexo numa tabela com o cliente nunca poderão ter toobe atualizado. Partindo do princípio de distribuição de Olá é constante entre os clientes, adicionar nova variação de tabela de toohello linhas não vai distribuição de dados de Olá toochange. No entanto, se o armazém de dados contém apenas um sexo e um novo resultados de requisito em vários genders sem dúvida terá de estatísticas de tooupdate na coluna de sexo Olá.

Para uma explicação mais, consulte [estatísticas] [ Statistics] no MSDN.

## <a name="implementing-statistics-management"></a>Implementar a gestão de estatísticas
Muitas vezes, é uma boa ideia tooextend Olá, os dados ao carregar o processo tooensure que as estatísticas são atualizadas ao fim de carga Olá. carregamento de dados de Olá é quando tabelas com mais frequência a alterar o tamanho e/ou a respetiva distribuição dos valores. Por conseguinte, esta é uma tooimplement local lógico alguns processos de gestão.

Alguns princípios de orientação para são fornecidos abaixo para atualizar as estatísticas durante o processo de carregamento de Olá:

* Certifique-se de que cada tabela carregada tem, pelo menos, um objeto de estatísticas atualizado. Este Olá atualizações tabelas informações de tamanho (contagem de linhas e contagem de páginas) como parte da atualização de estatísticas de Olá.
* Concentre-se em colunas que participam na associação, GROUP BY, ORDER BY e DISTINCT cláusulas
* Considere atualizar "chave ascendente" colunas como transação mais frequentemente estes valores não serão incluídos em histograma de estatísticas de Olá datas.
* Considere atualizar colunas de distribuição estático menos frequência.
* Lembre-se de que cada objeto de estatística é atualizado na série. Basta implementar `UPDATE STATISTICS <TABLE_NAME>` não pode ser o ideal - especialmente para tabelas wide com muitos objetos de estatísticas.

> [!NOTE]
> Para obter mais detalhes sobre [chave ascendente], consulte o documento técnico do modelo de estimativa de cardinalidade do toohello SQL Server 2014.
> 
> 

Para uma explicação mais, consulte [estimativa de cardinalidade] [ Cardinality Estimation] no MSDN.

## <a name="examples-create-statistics"></a>Exemplos: Criar estatísticas
Estes exemplos mostram como toouse várias opções para criar estatísticas. Opções de Olá que utilizar para cada coluna dependem características de Olá dos seus dados e como coluna de Olá será utilizada nas consultas.

### <a name="a-create-single-column-statistics-with-default-options"></a>A. Criar estatísticas de coluna única com opções predefinidas
estatísticas de toocreate numa coluna, só tem de fornecer um nome para o objeto de estatísticas de Olá e um nome de Olá da coluna de Olá.

Esta sintaxe utiliza todas as opções predefinidas de Olá. Por predefinição, o SQL Data Warehouse amostras 20 por cento da tabela de Olá quando cria estatísticas.

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

Por exemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a>B. Criar estatísticas de coluna única, examinando cada linha
frequência de amostragem Olá predefinição de 20 por cento é suficiente para a maioria das situações. No entanto, pode ajustar a frequência de amostragem Olá.

Olá toosample completo de tabela, utilizam esta sintaxe:

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

Por exemplo:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a>C. Criar estatísticas de coluna única, especificando o tamanho da amostra Olá
Em alternativa, pode especificar o tamanho da amostra Olá como uma percentagem:

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a>D. Criar estatísticas de coluna única na apenas algumas das linhas de Olá
Outra opção, pode criar estatísticas numa parte de linhas de Olá na tabela. Esta opção é denominada uma estatística filtrada.

Por exemplo, pode utilizar as estatísticas filtradas quando planeia tooquery uma partição específica de uma tabela particionada grande. Ao criar estatísticas em Olá apenas valores de partição, exatidão Olá das estatísticas de Olá melhorar e, por conseguinte, melhorar o desempenho das consultas.

Este exemplo cria estatísticas num intervalo de valores. valores de Olá facilmente pode ser definido o intervalo de Olá toomatch de valores numa partição.

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> Para Olá tooconsider otimizador consulta com as estatísticas filtradas quando escolhe o plano de consulta distribuída Olá, consulta Olá deve caber Olá definição do objeto de estatísticas de Olá. Exemplo de Olá anterior, Olá da consulta em que a cláusula tem toospecify col1 valores entre 2000101 e 20001231 a utilizar.
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a>E. Criar estatísticas de coluna única com todas as opções de Olá
Obviamente, pode combinar as opções de Olá em conjunto. exemplo de Olá abaixo cria um objeto de estatísticas filtradas com um tamanho de amostra personalizado:

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

Para referência completa Olá, consulte [CREATE STATISTICS] [ CREATE STATISTICS] no MSDN.

### <a name="f-create-multi-column-statistics"></a>F. Criar estatísticas de várias colunas
toocreate estatísticas de várias colunas, basta utilizar exemplos anteriores Olá, mas especificar mais colunas.

> [!NOTE]
> histograma Olá, que é utilizada tooestimate número de linhas no resultado da consulta Olá, só está disponível para a primeira coluna de Olá listada na definição de objeto de estatísticas de Olá.
> 
> 

Neste exemplo, histograma Olá é no *produto\_categoria*. Estatísticas de coluna em vários locais são calculadas *produto\_categoria* e *produto\_sub_c\ategory*:

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

Uma vez que existe uma correlação entre *produto\_categoria* e *produto\_sub\_categoria*, estado várias coluna pode ser úteis se estas colunas são acedidas em Olá mesmo tempo.

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a>G. Criar estatísticas em todas as colunas de Olá numa tabela
Estatísticas de toocreate unidirecional é tooissues comandos CREATE STATISTICS depois de criar a tabela de Olá.

```sql
CREATE TABLE dbo.table1
(
   col1 int
,  col2 int
,  col3 int
)
WITH
  (
    CLUSTERED COLUMNSTORE INDEX
  )
;

CREATE STATISTICS stats_col1 on dbo.table1 (col1);
CREATE STATISTICS stats_col2 on dbo.table2 (col2);
CREATE STATISTICS stats_col3 on dbo.table3 (col3);
```

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a>H. Utilize as estatísticas de toocreate um procedimento armazenado em todas as colunas numa base de dados
Armazém de dados do SQL Server não tem um equivalente do procedimento armazenado de sistema demasiado [sp_create_stats] [-] no SQL Server. Este procedimento armazenado cria um objeto de estatísticas de coluna única em cada coluna de base de dados de Olá que já não tem as estatísticas.

Isto irá ajudar a começar com o design da sua base de dados. Sentir tooadapt livre-tooyour precisa.

```sql
CREATE PROCEDURE    [dbo].[prc_sqldw_create_stats]
(   @create_type    tinyint -- 1 default 2 Fullscan 3 Sample
,   @sample_pct     tinyint
)
AS

IF @create_type NOT IN (1,2,3)
BEGIN
    THROW 151000,'Invalid value for @stats_type parameter. Valid range 1 (default), 2 (fullscan) or 3 (sample).',1;
END;

IF @sample_pct IS NULL
BEGIN;
    SET @sample_pct = 20;
END;

IF OBJECT_ID('tempdb..#stats_ddl') IS NOT NULL
BEGIN;
    DROP TABLE #stats_ddl;
END;

CREATE TABLE #stats_ddl
WITH    (   DISTRIBUTION    = HASH([seq_nmbr])
        ,   LOCATION        = USER_DB
        )
AS
WITH T
AS
(
SELECT      t.[name]                        AS [table_name]
,           s.[name]                        AS [table_schema_name]
,           c.[name]                        AS [column_name]
,           c.[column_id]                   AS [column_id]
,           t.[object_id]                   AS [object_id]
,           ROW_NUMBER()
            OVER(ORDER BY (SELECT NULL))    AS [seq_nmbr]
FROM        sys.[tables] t
JOIN        sys.[schemas] s         ON  t.[schema_id]       = s.[schema_id]
JOIN        sys.[columns] c         ON  t.[object_id]       = c.[object_id]
LEFT JOIN   sys.[stats_columns] l   ON  l.[object_id]       = c.[object_id]
                                    AND l.[column_id]       = c.[column_id]
                                    AND l.[stats_column_id] = 1
LEFT JOIN    sys.[external_tables] e    ON    e.[object_id]        = t.[object_id]
WHERE       l.[object_id] IS NULL
AND            e.[object_id] IS NULL -- not an external table
)
SELECT  [table_schema_name]
,       [table_name]
,       [column_name]
,       [column_id]
,       [object_id]
,       [seq_nmbr]
,       CASE @create_type
        WHEN 1
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+')' AS VARCHAR(8000))
        WHEN 2
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH FULLSCAN' AS VARCHAR(8000))
        WHEN 3
        THEN    CAST('CREATE STATISTICS '+QUOTENAME('stat_'+table_schema_name+ '_' + table_name + '_'+column_name)+' ON '+QUOTENAME(table_schema_name)+'.'+QUOTENAME(table_name)+'('+QUOTENAME(column_name)+') WITH SAMPLE '+@sample_pct+'PERCENT' AS VARCHAR(8000))
        END AS create_stat_ddl
FROM T
;

DECLARE @i INT              = 1
,       @t INT              = (SELECT COUNT(*) FROM #stats_ddl)
,       @s NVARCHAR(4000)   = N''
;

WHILE @i <= @t
BEGIN
    SET @s=(SELECT create_stat_ddl FROM #stats_ddl WHERE seq_nmbr = @i);

    PRINT @s
    EXEC sp_executesql @s
    SET @i+=1;
END

DROP TABLE #stats_ddl;
```

toocreate estatísticas em todas as colunas na tabela de Olá com este procedimento, basta chamar o procedimento de Olá.

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a>Exemplos: estatísticas de atualização
estatísticas de tooupdate, pode:

1. Atualize um objeto de estatísticas. Especifique o nome Olá Olá estatísticas pretende tooupdate de objeto.
2. Atualize todos os objetos de estatísticas numa tabela. Especifique o nome de Olá da tabela de Olá em vez de um objeto de estatísticas específico.

### <a name="a-update-one-specific-statistics-object"></a>A. Atualizar um objeto de estatísticas específico
Utilize Olá seguindo a sintaxe tooupdate um objeto de estatísticas específico:

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

Por exemplo:

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

Ao atualizar objetos de estatísticas específico, pode minimizar Olá recursos e tempo necessários toomanage estatísticas. Isto requer que alguns considerar-se, no entanto, toochoose Olá melhor estatísticas objetos tooupdate.

### <a name="b-update-all-statistics-on-a-table"></a>B. Atualizar todas as estatísticas numa tabela
Mostra um método simples para atualizar todos os objetos de estatísticas de Olá numa tabela.

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

Por exemplo:

```sql
UPDATE STATISTICS dbo.table1;
```

Esta instrução é fácil toouse. Lembre-se apenas isto atualiza todas as estatísticas na tabela de Olá e, assim, poderá efetuar trabalho mais do que é necessário. Se o desempenho de Olá não for um problema, esta é sem dúvida forma de mais fácil e mais completa de Olá tooguarantee estatísticas são atualizadas.

> [!NOTE]
> Ao atualizar todas as estatísticas numa tabela, o SQL Data Warehouse efetua uma tabela de Olá toosample de análise para cada estatísticas. Se a tabela de Olá for grande, tem demasiadas colunas e estatísticas de muitas, poderá ser mais eficientes tooupdate individuais as estatísticas com base na necessidade.
> 
> 

Para uma implementação de um `UPDATE STATISTICS` procedimento Consulte Olá [tabelas temporárias] [ Temporary] artigo. o método de implementação de Olá é ligeiramente diferente toohello `CREATE STATISTICS` procedimento acima, mas o resultado final de Olá é Olá mesmo.

Para a sintaxe completa Olá, consulte [Update Statistics] [ Update Statistics] no MSDN.

## <a name="statistics-metadata"></a>Metadados de estatísticas
Existem várias funções que pode utilizar toofind informações sobre as estatísticas e vista de sistema. Por exemplo, pode ver se um objeto de estatísticas pode estar desatualizado utilizando Olá estatísticas data função toosee quando estatísticas foram criadas ou atualizadas pela última vez.

### <a name="catalog-views-for-statistics"></a>Vistas de catálogo para estatísticas
Estas vistas de sistema fornecem informações sobre as estatísticas:

| Vista de catálogo | Descrição |
|:--- |:--- |
| [sys.Columns][sys.columns] |Uma linha para cada coluna. |
| [sys.Objects][sys.objects] |Uma linha para cada objeto na base de dados de Olá. |
| [sys.schemas][sys.schemas] |Uma linha para cada esquema na base de dados de Olá. |
| [sys.Stats][sys.stats] |Uma linha para cada objeto de estatísticas. |
| [sys.stats_columns][sys.stats_columns] |Uma linha para cada coluna no objeto de estatísticas de Olá. Ligações de fazer uma cópia toosys.columns. |
| [sys. Tables][sys.tables] |Uma linha para cada tabela (inclui as tabelas externas). |
| [sys.table_types][sys.table_types] |Uma linha para cada tipo de dados. |

### <a name="system-functions-for-statistics"></a>Funções de sistema para estatísticas
Estas funções de sistema são úteis para trabalhar com as estatísticas:

| Função de sistema | Descrição |
|:--- |:--- |
| [STATS_DATE][STATS_DATE] |Objeto de estatísticas de Olá data foi atualizado pela última vez. |
| [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] |Fornece resumidas nível e informações detalhadas sobre a distribuição de Olá de valores como compreendida por objeto de estatísticas de Olá. |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a>Combinar as colunas de estatísticas e as funções para uma vista
Esta vista apresenta as colunas que se relacionam com toostatistics e os resultados da função de [] Olá [STATS_DATE()] em conjunto.

```sql
CREATE VIEW dbo.vstats_columns
AS
SELECT
        sm.[name]                           AS [schema_name]
,       tb.[name]                           AS [table_name]
,       st.[name]                           AS [stats_name]
,       st.[filter_definition]              AS [stats_filter_defiinition]
,       st.[has_filter]                     AS [stats_is_filtered]
,       STATS_DATE(st.[object_id],st.[stats_id])
                                            AS [stats_last_updated_date]
,       co.[name]                           AS [stats_column_name]
,       ty.[name]                           AS [column_type]
,       co.[max_length]                     AS [column_max_length]
,       co.[precision]                      AS [column_precision]
,       co.[scale]                          AS [column_scale]
,       co.[is_nullable]                    AS [column_is_nullable]
,       co.[collation_name]                 AS [column_collation_name]
,       QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS two_part_name
,       QUOTENAME(DB_NAME())+'.'+QUOTENAME(sm.[name])+'.'+QUOTENAME(tb.[name])
                                            AS three_part_name
FROM    sys.objects                         AS ob
JOIN    sys.stats           AS st ON    ob.[object_id]      = st.[object_id]
JOIN    sys.stats_columns   AS sc ON    st.[stats_id]       = sc.[stats_id]
                            AND         st.[object_id]      = sc.[object_id]
JOIN    sys.columns         AS co ON    sc.[column_id]      = co.[column_id]
                            AND         sc.[object_id]      = co.[object_id]
JOIN    sys.types           AS ty ON    co.[user_type_id]   = ty.[user_type_id]
JOIN    sys.tables          AS tb ON  co.[object_id]        = tb.[object_id]
JOIN    sys.schemas         AS sm ON  tb.[schema_id]        = sm.[schema_id]
WHERE   1=1
AND     st.[user_created] = 1
;
```

## <a name="dbcc-showstatistics-examples"></a>Exemplos de DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() mostra os dados de Olá contidos dentro de um objeto de estatísticas. Estes dados é apresentada no três partes.

1. Cabeçalho
2. Vetor de densidade
3. Histograma

metadados de cabeçalho de Olá sobre estatísticas Olá. histograma Olá mostra a distribuição Olá de valores na primeira coluna chave Olá do objeto de estatísticas de Olá. Olá densidade vetor medidas entre coluna correlação. SQLDW calcula estimativas de cardinalidade com qualquer um dos dados de Olá no objeto de estatísticas de Olá.

### <a name="show-header-density-and-histogram"></a>Mostrar o cabeçalho, densidade e histograma
Neste exemplo simples mostra todos os três partes de um objeto de estatísticas.

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

Por exemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a>Mostrar uma ou mais partes de DBCC SHOW_STATISTICS();
Se apenas estiver interessado em partes específicas de visualização, utilize Olá `WITH` cláusula e especifique que partes pretende toosee:

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

Por exemplo:

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a>Diferenças de DBCC SHOW_STATISTICS()
DBCC SHOW_STATISTICS() mais estritamente está implementada no servidor do armazém de dados do SQL Server em comparação com tooSQL.

1. Não são suportadas as funcionalidades não documentadas
2. Não é possível utilizar Stats_stream
3. Não é possível associar resultados para subconjuntos específicos de dados de estatísticas por exemplo, (STAT_HEADER associação DENSITY_VECTOR)
4. Não é possível definir NO_INFOMSGS para supressão de mensagem
5. Não é possível utilizar parênteses Retos à volta de nomes de estatísticas
6. Não é possível utilizar objetos de estatísticas de tooidentify de nomes de coluna
7. Erro personalizado 2767 não é suportado

## <a name="next-steps"></a>Passos seguintes
Para obter mais detalhes, consulte [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] no MSDN.  toolearn mais, consulte os artigos de Olá no [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de indexação][Index], [uma tabela de criação de partições] [ Partition] e [ Tabelas temporárias][Temporary].  Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].  

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
[Cardinality Estimation]: https://msdn.microsoft.com/library/dn600374.aspx
[CREATE STATISTICS]: https://msdn.microsoft.com/library/ms188038.aspx
[DBCC SHOW_STATISTICS]:https://msdn.microsoft.com/library/ms174384.aspx
[Statistics]: https://msdn.microsoft.com/library/ms190397.aspx
[STATS_DATE]: https://msdn.microsoft.com/library/ms190330.aspx
[sys.columns]: https://msdn.microsoft.com/library/ms176106.aspx
[sys.objects]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.schemas]: https://msdn.microsoft.com/library/ms190324.aspx
[sys.stats]: https://msdn.microsoft.com/library/ms177623.aspx
[sys.stats_columns]: https://msdn.microsoft.com/library/ms187340.aspx
[sys.tables]: https://msdn.microsoft.com/library/ms187406.aspx
[sys.table_types]: https://msdn.microsoft.com/library/bb510623.aspx
[UPDATE STATISTICS]: https://msdn.microsoft.com/library/ms187348.aspx

<!--Other Web references-->  
