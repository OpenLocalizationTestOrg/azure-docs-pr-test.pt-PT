---
title: tabelas de aaaDistributing no SQL Data Warehouse | Microsoft Docs
description: "Introdução à distribuição de tabelas do Azure SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: 5ed4337f-7262-4ef6-8fd6-1809ce9634fc
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 10/31/2016
ms.author: shigu;barbkess
ms.openlocfilehash: 65093eeaeb00fef85aaa6070da2c976fed3f4bbe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="distributing-tables-in-sql-data-warehouse"></a>Distribuir a tabelas no armazém de dados do SQL Server
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

O SQL Data Warehouse é um sistema de base de dados distribuído de processamento paralelo em massa (MPP).  Ao dividir os dados e a capacidade de processamento entre vários nós, o SQL Data Warehouse pode oferecer uma enorme escalabilidade, muito além de qualquer sistema único.  Decidir como toodistribute os dados no seu SQL Data Warehouse são uma das mais importante de Olá fatores tooachieving um desempenho ideal.   desempenho de chave toooptimal Olá é minimizar o movimento de dados e por sua vez movimento de dados de chave toominimizing Olá é selecionando a estratégia de distribuição direita Olá.

## <a name="understanding-data-movement"></a>Movimento de dados de conhecimento
Num sistema MPP, os dados de Olá de cada tabela estão divididos em várias bases de dados subjacentes.  consultas de Olá mais otimizada num sistema MPP podem simplesmente ser transmitidas tooexecute no Olá individuais bases de dados distribuídas sem interação entre Olá outras bases de dados.  Por exemplo, vamos supor que tem uma base de dados com dados de vendas que contém duas tabelas, vendas e clientes.  Se tiver uma consulta que necessita de toojoin a vendas tooyour cliente tabela e dividir as suas vendas e tabelas de cliente cópias de segurança por número de cliente, colocando a cada cliente numa base de dados separada, todas as consultas que aderir ao cliente e de vendas possam ser resolvidas em cada base de dados com sem qualquer conhecimento do Olá outras bases de dados.  Em contrapartida, se dividir os dados de vendas por número de ordem e os dados de cliente por número de cliente, em seguida, qualquer base de dados indicado não terá dados correspondentes Olá para cada cliente e, consequentemente, se pretendesse toojoin os dados de cliente de tooyour de dados de vendas, seria necessária tooget hello dados para cada cliente de Olá outras bases de dados.  Neste exemplo segundo, movimento de dados teria toooccur toomove Olá cliente dados toohello dados de vendas, para que podem ser associadas a tabelas de Olá dois.  

Movimento de dados não se encontra sempre uma coisa danificada, por vezes é necessário toosolve uma consulta.  Mas, quando este passo adicional pode ser evitado, naturalmente sua consulta serão são executadas mais rápido.  Movimento de dados for mais frequentemente quando estão associadas a tabelas ou agregações são executadas.  Muitas vezes necessitam toodo ambos, pelo que enquanto poderá toooptimize para um cenário, como uma associação, é ainda necessário toohelp de movimento de dados resolver para Olá outro cenário, como uma agregação.  truque Olá é perceber que é menor trabalho.  Na maioria dos casos, distribuir as tabelas de factos grande numa coluna normalmente associada é Olá método mais eficaz para reduzir Olá a maioria das movimento de dados.  Distribuição de dados em colunas de associação é um movimento de dados do método tooreduce muito mais comuns a distribuição de dados em colunas envolvidos numa agregação.

## <a name="select-distribution-method"></a>Selecione o método de distribuição
Em segundo plano do Olá, o SQL Data Warehouse divide os dados em 60 bases de dados.  Cada base de dados individuais é referenciado tooas um **distribuição**.  Quando os dados são carregados para cada tabela, o SQL Data Warehouse tem tooknow como toodivide os dados entre estes 60 distribuições.  

o método de distribuição de Olá é definido ao nível da tabela de Olá e atualmente, existem duas opções:

1. **O round robin** que distribui dados uniformemente mas aleatoriamente.
2. **A função hash distribuídas** que distribui dados com base em hash valores de uma única coluna

Por predefinição, quando não definem um método de distribuição de dados, a tabela será distribuída utilizando Olá **round robin** método de distribuição.  No entanto, à ficam mais sofisticadas na sua implementação, é aconselhável utilizar tooconsider **hash distribuída** tabelas de movimento de dados de toominimize que por sua vez irão otimizar o desempenho das consultas.

### <a name="round-robin-tables"></a>O Round Robin tabelas
A utilização de Olá Round Robin de método de distribuição de dados é muito como-SOA.  Como os dados são carregados, cada linha é simplesmente enviada distribuição seguinte toohello.  Este método de distribuição de dados de Olá será sempre aleatoriamente distribuir dados Olá muito uniformemente em todas as distribuições de Olá.  Ou seja, não há qualquer ordenação efectuada durante Olá arredondar round robin processo que coloca os dados.  Uma distribuição round robin denomina-se um hash aleatório por este motivo.  Com uma tabela distribuída round robin há não existem dados de Olá toounderstand necessário.  Por este motivo, tabelas Round-Robin, muitas vezes, tornar carregamento boa destinos.

Por predefinição, não se for escolhido nenhum método de distribuição, hello round robin distribuição método irá ser utilizado.  No entanto, enquanto o round robin tabelas são fáceis toouse, porque dados aleatoriamente são distribuídos por sistema Olá significa que o sistema Olá não pode garantir qual distribuição cada linha é no.  Como resultado, sistema de Olá, por vezes, precisa de tooinvoke um toobetter de operação de movimento de dados organize os dados antes de pode resolver uma consulta.  Este passo adicional pode atrasar as suas consultas.

Considere utilizar o Round Robin distribuição para a sua tabela no Olá os seguintes cenários:

* Quando introdução como um ponto de partida simple
* Se não houver nenhuma chave joining óbvios
* Se não houver coluna bom candidato para distribuir a tabela de Olá de hash
* Se hello tabela não partilha uma chave de associação comuns com outras tabelas
* Se a associação de Olá é menos significativa que outros associações na consulta de Olá
* Quando a tabela de Olá é uma tabela de transição temporária

Ambos estes exemplos irão criar uma tabela de Round Robin:

```SQL
-- Round Robin created by default
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
,   [OrderDateKey]          int          NOT NULL
,   [CustomerKey]           int          NOT NULL
,   [PromotionKey]          int          NOT NULL
,   [SalesOrderNumber]      nvarchar(20) NOT NULL
,   [OrderQuantity]         smallint     NOT NULL
,   [UnitPrice]             money        NOT NULL
,   [SalesAmount]           money        NOT NULL
)
;

-- Explicitly Created Round Robin Table
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,   DISTRIBUTION = ROUND_ROBIN
)
;
```

> [!NOTE]
> Enquanto o round robin é o tipo de tabela Olá predefinido a ser explícita na sua DDL é considerado uma melhor prática, para que intenções Olá do seu esquema de tabela são tooothers encriptado.
>
>

### <a name="hash-distributed-tables"></a>Distribuída tabelas de hash
Utilizar um **Hash distribuída** algoritmo toodistribute as tabelas podem melhorar o desempenho de muitos cenários ao reduzir o movimento de dados no momento da consulta.  Hash distribuídas tabelas são tabelas que são divididas entre Olá distribuídas bases de dados utilizando um algoritmo hash numa única coluna que selecionar.  a coluna de distribuição Olá é que determina a forma como os dados de Olá são divididos entre as bases de dados distribuídas.  função de hash de Olá utiliza Olá distribuição coluna tooassign linhas toodistributions.  Olá algoritmo hash e distribuição resultante é determinística.  Ou seja Olá mesmo valor com o mesmo tipo de dados será sempre de Olá tem toohello distribuição mesma.    

Neste exemplo, irá criar uma tabela distribuída no id de:

```SQL
CREATE TABLE [dbo].[FactInternetSales]
(   [ProductKey]            int          NOT NULL
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
,  DISTRIBUTION = HASH([ProductKey])
)
;
```

## <a name="select-distribution-column"></a>Selecione a coluna de distribuição
Quando escolhe demasiado**hash distribuir** uma tabela, terá de tooselect uma coluna de distribuição único.  Quando selecionar uma coluna de distribuição, existem três principais fatores tooconsider.  

Selecione uma coluna que irá:

1. Não é possível atualizar
2. Distribuir dados uniformemente, evitando dados dissimetrias
3. Minimizar o movimento de dados

### <a name="select-distribution-column-which-will-not-be-updated"></a>Selecione a coluna de distribuição que não será atualizada
Colunas de distribuição não são atualizáveis, por conseguinte, selecione uma coluna com valores estáticos.  Se uma coluna terá toobe atualizada, geralmente, não é um candidato a distribuição bom.  Se existir um caso onde deve atualizar uma coluna de distribuição, isto pode ser feito pelo primeiro eliminar linha Olá e, em seguida, a inserir uma nova linha.

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a>Selecione a coluna de distribuição que será a distribuir uniformemente dados
Uma vez que um sistema distribuído efetua apenas tão rápido como a distribuição da mesma mais lenta, é importante toodivide Olá trabalho uniformemente em toda as distribuições de Olá na ordem tooachieve com balanceamento de execução em sistema Olá.  forma Olá trabalho Olá está dividido num sistema distribuído baseia onde exista dados Olá para cada distribuição.  Isto torna muito importante tooselect Olá distribuição direita coluna distribuir dados Olá, para que cada distribuição tem trabalho igual e irá tirar Olá mesmo tempo toocomplete sua parte do trabalho Olá.  Quando o trabalho também está dividido em sistema Olá, dados de Olá são equilibrados nos distribuições Olá.  Quando os dados não é uniformemente balanceamento, chamamos a isto **desfasamento de dados**.  

dados toodivide uniformemente e evitar dados dissimetrias, considere o seguinte Olá ao selecionar a coluna de distribuição:

1. Selecione uma coluna que contém um número significativo de valores distintos.
2. Evite distribuição de dados em colunas com alguns valores distintos.
3. Evite distribuição de dados em colunas com uma frequência alta de valores NULL.
4. Evite distribuição de dados em colunas de data.

Uma vez que cada valor com hash too1 de 60 distribuições, distribuição, mesmo que tooachieve convém tooselect uma coluna que é exclusiva de elevada disponibilidade e contém mais de 60 valores exclusivos.  tooillustrate, considere o caso em que uma coluna tem 40 valores exclusivos apenas.  Se esta coluna foi selecionada como Olá de distribuição de chaves, dados de Olá para essa tabela seriam encaminhado para no 40 distribuições no máximo, deixando 20 distribuições com não dados e não toodo de processamento.  Por outro lado, hello outras 40 distribuições teria mais toodo de trabalho que se hello dados foi uniformemente distribuídos mais de 60 distribuições.  Este cenário é um exemplo de dados dissimetrias.

Num sistema MPP, cada passo de consulta aguarda todas as distribuições toocomplete os respetivos partilha do trabalho Olá.  Se uma distribuição é efetuar trabalho mais do que outras pessoas Olá, em seguida, Olá recurso dos Olá outras distribuições são essencialmente desperdiçadas apenas aguardar a resposta de distribuição ocupado Olá.  Quando o trabalho não é distribuído uniformemente por todas as distribuições, chamamos a isto **processamento dissimetrias**.  O desfasamento de processamento fará toorun consultas mais lenta do que o se carga de trabalho Olá serem distribuída uniformemente por distribuições Olá.  O desfasamento de dados irá causar tooprocessing dissimetrias.

Evitar distribuição na coluna de elevada disponibilidade que pode ser nula como valores nulos Olá serão todos os apresentado no Olá igual distribuição. Distribuição de uma coluna de data pode também fazer com que processamento dissimetrias porque todos os dados para uma determinada data serão apresentado no Olá igual distribuição. Se vários utilizadores se encontram em execução filtragem todas as consultas no Olá mesmo data, em seguida, apenas 1 das distribuições de 60 Olá irá fazer todo o trabalho de Olá, uma vez que uma determinada data só estará num de distribuição. Neste cenário, consultas de Olá, provavelmente, irão executar 60 vezes mais lentas do que o se os dados de Olá igualmente foram distribuídos por todas as distribuições de Olá.

Quando não existe nenhuma coluna bom candidato, em seguida, considere utilizar o round robin como método de distribuição Olá.

### <a name="select-distribution-column-which-will-minimize-data-movement"></a>Selecione a coluna de distribuição que irá minimizar o movimento de dados
Minimizar o movimento de dados selecionando a coluna da direita da distribuição de Olá é uma das estratégias de mais importantes de Olá para otimizar o desempenho do seu SQL Data Warehouse.  Movimento de dados for mais frequentemente quando estão associadas a tabelas ou agregações são executadas.  As colunas utilizadas no `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` cláusulas todas tornam para **boa** candidatos a distribuição de hash.

No Olá por outro lado, as colunas na Olá `WHERE` cláusula efetue **não** efetuar para candidatos de coluna de hash boa porque estes limitam as distribuições participam na consulta de Olá, fazendo com que o processamento dissimetrias.  Um bom exemplo de uma coluna que pode ser tempting toodistribute no, mas, muitas vezes, pode causar este processamento dissimetrias é uma coluna de data.

Um modo geral, se tiver duas tabelas de factos grande frequentemente envolvidas numa associação, irá obter Olá um desempenho mais por distribuição de ambas as tabelas numa das colunas de associação de Olá.  Se tiver uma tabela que nunca esteja tabela de factos grande de tooanother associados, em seguida, procure toocolumns que estão frequentemente Olá `GROUP BY` cláusula.

Existem alguns chaves os critérios que têm de ser cumpridos tooavoid movimento de dados durante uma associação:

1. Olá tabelas envolvidos na associação Olá tem de ser hash distribuído **um** de colunas de Olá participar na União Olá.
2. tipos de dados de Olá de colunas de associação de Olá tem de corresponder entre ambas as tabelas.
3. colunas de Olá tem de ser associadas com um operador igual a.
4. Olá tipo de associação não pode ser um `CROSS JOIN`.

## <a name="troubleshooting-data-skew"></a>Dados dissimetrias de resolução de problemas
Quando os dados da tabela são distribuídos utilizando o método de distribuição de hash de Olá há a possibilidade de algumas distribuições será skewed toohave disproportionately mais dados que outras pessoas. Dados excessivos dissimetrias podem afetar o desempenho de consulta porque o resultado final do Olá de uma consulta distribuída tem de aguardar Olá mais longo em execução distribuição toofinish. Dependendo grau de Olá dos dados de Olá dissimetrias que poderá ser necessário tooaddress-lo.

### <a name="identifying-skew"></a>Identificar desfasamento
Uma forma simples de tooidentify uma tabela como skewed é toouse `DBCC PDW_SHOWSPACEUSED`.  Esta é uma forma muito rápida e simples toosee Olá número de linhas de tabela que estão armazenados em cada uma das distribuições de Olá 60 da base de dados.  Lembre-se de que para um desempenho mais com balanceamento de Olá, linhas de Olá na tabela distribuída devem ser distribuídas uniformemente por todas as distribuições de Olá.

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

No entanto, se consultar vistas de gestão dinâmica do Azure SQL Data Warehouse Olá (DMV) pode executar uma análise mais detalhada.  toostart, criar vista Olá [dbo.vTableSizes] [ dbo.vTableSizes] vistos através de Olá SQL a partir do [descrição geral da tabela] [ Overview] artigo.  Assim que for criada vista Olá, execute este tooidentify de consulta que tabelas tem mais do que o desfasamento de dados de 10%.

```sql
select *
from dbo.vTableSizes
where two_part_name in
    (
    select two_part_name
    from dbo.vTableSizes
    where row_count > 0
    group by two_part_name
    having min(row_count * 1.000)/max(row_count * 1.000) > .10
    )
order by two_part_name, row_count
;
```

### <a name="resolving-data-skew"></a>Resolver dados dissimetrias
Não todos os dissimetrias é suficiente toowarrant uma correção.  Em alguns casos, desempenho Olá de uma tabela em algumas consultas pode prevalecem sobre a possibilidade de Olá dos dados dissimetrias.  toodecide se deve resolver dados desfasamento numa tabela, deve compreender quanto possível sobre os volumes de dados de Olá e consultas na sua carga de trabalho.   Uma forma toolook no impacto Olá de desfasamento é toouse passos Olá Olá [consulta monitorização] [ Query Monitoring] artigo toomonitor Olá impacto dissimetrias no desempenho das consultas e especificamente Olá consultas de tempo de toohow de impacto colocar toocomplete distribuições individuais Olá.

Distribuição de dados é um fim de encontrar o equilíbrio certo entre Olá entre minimizando desfasamento de dados e minimizar o movimento de dados. Estes podem ser opposing objetivos e, por vezes, é aconselhável tookeep dados dissimetrias no movimento de dados de tooreduce de ordem. Por exemplo, quando a coluna de distribuição Olá é frequentemente Olá partilhado coluna associações e agregações, irá ser minimizando movimento de dados. Olá vantagem de ter o movimento de dados mínimo de Olá poderá compensar impacto Olá da eliminação de dados desfasamento.

forma típico Olá tooresolve desfasamento de dados é toore-criar a tabela de Olá com uma coluna de distribuição diferente. Porque não existe nenhuma forma de tabela de coluna de distribuição de Olá toochange no existente, Olá forma toochange Olá distribuição uma tabela-toorecreate-o com um [[CTAS]].  Seguem-se dois exemplos de como resolver dados dissimetrias:

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a>Exemplo 1: Voltar a criar tabela Olá com uma nova coluna de distribuição
Este exemplo utiliza [CTAS] [] toore-criar uma tabela com uma coluna de distribuição hash diferentes.

```sql
CREATE TABLE [dbo].[FactInternetSales_CustomerKey]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  HASH([CustomerKey])
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_CustomerKey')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_CustomerKey] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_CustomerKey] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_CustomerKey] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_CustomerKey] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_CustomerKey] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_CustomerKey] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_CustomerKey] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_CustomerKey] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_ProductKey];
RENAME OBJECT [dbo].[FactInternetSales_CustomerKey] too[FactInternetSales];
```

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a>Exemplo 2: Voltar a criar tabela Olá utilizando o round robin distribuição
Este exemplo utiliza [CTAS] [] toore-crie uma tabela com o round robin, em vez de uma distribuição hash. Esta alteração produzirá distribuição de dados, mesmo que custo Olá de movimento de dados maior.

```sql
CREATE TABLE [dbo].[FactInternetSales_ROUND_ROBIN]
WITH (  CLUSTERED COLUMNSTORE INDEX
     ,  DISTRIBUTION =  ROUND_ROBIN
     ,  PARTITION       ( [OrderDateKey] RANGE RIGHT FOR VALUES (   20000101, 20010101, 20020101, 20030101
                                                                ,   20040101, 20050101, 20060101, 20070101
                                                                ,   20080101, 20090101, 20100101, 20110101
                                                                ,   20120101, 20130101, 20140101, 20150101
                                                                ,   20160101, 20170101, 20180101, 20190101
                                                                ,   20200101, 20210101, 20220101, 20230101
                                                                ,   20240101, 20250101, 20260101, 20270101
                                                                ,   20280101, 20290101
                                                                )
                        )
    )
AS
SELECT  *
FROM    [dbo].[FactInternetSales]
OPTION  (LABEL  = 'CTAS : FactInternetSales_ROUND_ROBIN')
;

--Create statistics on new table
CREATE STATISTICS [ProductKey] ON [FactInternetSales_ROUND_ROBIN] ([ProductKey]);
CREATE STATISTICS [OrderDateKey] ON [FactInternetSales_ROUND_ROBIN] ([OrderDateKey]);
CREATE STATISTICS [CustomerKey] ON [FactInternetSales_ROUND_ROBIN] ([CustomerKey]);
CREATE STATISTICS [PromotionKey] ON [FactInternetSales_ROUND_ROBIN] ([PromotionKey]);
CREATE STATISTICS [SalesOrderNumber] ON [FactInternetSales_ROUND_ROBIN] ([SalesOrderNumber]);
CREATE STATISTICS [OrderQuantity] ON [FactInternetSales_ROUND_ROBIN] ([OrderQuantity]);
CREATE STATISTICS [UnitPrice] ON [FactInternetSales_ROUND_ROBIN] ([UnitPrice]);
CREATE STATISTICS [SalesAmount] ON [FactInternetSales_ROUND_ROBIN] ([SalesAmount]);

--Rename hello tables
RENAME OBJECT [dbo].[FactInternetSales] too[FactInternetSales_HASH];
RENAME OBJECT [dbo].[FactInternetSales_ROUND_ROBIN] too[FactInternetSales];
```

## <a name="next-steps"></a>Passos seguintes
toolearn mais informações sobre a estrutura da tabela, consulte Olá [distribuir][Distribute], [índice][Index], [partição] [ Partition], [Tipos de dados][Data Types], [estatísticas] [ Statistics] e [tabelas temporárias] [ Temporary] artigos.

Para obter uma descrição geral de melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].

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
[Query Monitoring]: ./sql-data-warehouse-manage-monitor.md
[dbo.vTableSizes]: ./sql-data-warehouse-tables-overview.md#table-size-queries

<!--MSDN references-->
[DBCC PDW_SHOWSPACEUSED()]: https://msdn.microsoft.com/library/mt204028.aspx

<!--Other Web references-->
