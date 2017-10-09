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
# <a name="distributing-tables-in-sql-data-warehouse"></a><span data-ttu-id="0cd3b-103">Distribuir a tabelas no armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0cd3b-103">Distributing tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="0cd3b-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="0cd3b-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="0cd3b-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="0cd3b-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-107">[Index][Index]</span></span>
> * <span data-ttu-id="0cd3b-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="0cd3b-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="0cd3b-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="0cd3b-110">[Temporary][Temporary]</span></span>
>
>

<span data-ttu-id="0cd3b-111">O SQL Data Warehouse é um sistema de base de dados distribuído de processamento paralelo em massa (MPP).</span><span class="sxs-lookup"><span data-stu-id="0cd3b-111">SQL Data Warehouse is a massively parallel processing (MPP) distributed database system.</span></span>  <span data-ttu-id="0cd3b-112">Ao dividir os dados e a capacidade de processamento entre vários nós, o SQL Data Warehouse pode oferecer uma enorme escalabilidade, muito além de qualquer sistema único.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-112">By dividing data and processing capability across multiple nodes, SQL Data Warehouse can offer huge scalability - far beyond any single system.</span></span>  <span data-ttu-id="0cd3b-113">Decidir como toodistribute os dados no seu SQL Data Warehouse são uma das mais importante de Olá fatores tooachieving um desempenho ideal.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-113">Deciding how toodistribute your data within your SQL Data Warehouse is one of hello most important factors tooachieving optimal performance.</span></span>   <span data-ttu-id="0cd3b-114">desempenho de chave toooptimal Olá é minimizar o movimento de dados e por sua vez movimento de dados de chave toominimizing Olá é selecionando a estratégia de distribuição direita Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-114">hello key toooptimal performance is minimizing data movement and in turn hello key toominimizing data movement is selecting hello right distribution strategy.</span></span>

## <a name="understanding-data-movement"></a><span data-ttu-id="0cd3b-115">Movimento de dados de conhecimento</span><span class="sxs-lookup"><span data-stu-id="0cd3b-115">Understanding data movement</span></span>
<span data-ttu-id="0cd3b-116">Num sistema MPP, os dados de Olá de cada tabela estão divididos em várias bases de dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-116">In an MPP system, hello data from each table is divided across several underlying databases.</span></span>  <span data-ttu-id="0cd3b-117">consultas de Olá mais otimizada num sistema MPP podem simplesmente ser transmitidas tooexecute no Olá individuais bases de dados distribuídas sem interação entre Olá outras bases de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-117">hello most optimized queries on an MPP system can simply be passed through tooexecute on hello individual distributed databases with no interaction between hello other databases.</span></span>  <span data-ttu-id="0cd3b-118">Por exemplo, vamos supor que tem uma base de dados com dados de vendas que contém duas tabelas, vendas e clientes.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-118">For example, let's say you have a database with sales data which contains two tables, sales and customers.</span></span>  <span data-ttu-id="0cd3b-119">Se tiver uma consulta que necessita de toojoin a vendas tooyour cliente tabela e dividir as suas vendas e tabelas de cliente cópias de segurança por número de cliente, colocando a cada cliente numa base de dados separada, todas as consultas que aderir ao cliente e de vendas possam ser resolvidas em cada base de dados com sem qualquer conhecimento do Olá outras bases de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-119">If you have a query that needs toojoin your sales table tooyour customer table and you divide both your sales and customer tables up by customer number, putting each customer in a separate database, any queries which join sales and customer can be solved within each database with no knowledge of hello other databases.</span></span>  <span data-ttu-id="0cd3b-120">Em contrapartida, se dividir os dados de vendas por número de ordem e os dados de cliente por número de cliente, em seguida, qualquer base de dados indicado não terá dados correspondentes Olá para cada cliente e, consequentemente, se pretendesse toojoin os dados de cliente de tooyour de dados de vendas, seria necessária tooget hello dados para cada cliente de Olá outras bases de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-120">In contrast, if you divided your sales data by order number and your customer data by customer number, then any given database will not have hello corresponding data for each customer and thus if you wanted toojoin your sales data tooyour customer data, you would need tooget hello data for each customer from hello other databases.</span></span>  <span data-ttu-id="0cd3b-121">Neste exemplo segundo, movimento de dados teria toooccur toomove Olá cliente dados toohello dados de vendas, para que podem ser associadas a tabelas de Olá dois.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-121">In this second example, data movement would need toooccur toomove hello customer data toohello sales data, so that hello two tables can be joined.</span></span>  

<span data-ttu-id="0cd3b-122">Movimento de dados não se encontra sempre uma coisa danificada, por vezes é necessário toosolve uma consulta.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-122">Data movement isn't always a bad thing, sometimes it's necessary toosolve a query.</span></span>  <span data-ttu-id="0cd3b-123">Mas, quando este passo adicional pode ser evitado, naturalmente sua consulta serão são executadas mais rápido.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-123">But when this extra step can be avoided, naturally your query will run faster.</span></span>  <span data-ttu-id="0cd3b-124">Movimento de dados for mais frequentemente quando estão associadas a tabelas ou agregações são executadas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-124">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="0cd3b-125">Muitas vezes necessitam toodo ambos, pelo que enquanto poderá toooptimize para um cenário, como uma associação, é ainda necessário toohelp de movimento de dados resolver para Olá outro cenário, como uma agregação.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-125">Often you need toodo both, so while you may be able toooptimize for one scenario, like a join, you still need data movement toohelp you solve for hello other scenario, like an aggregation.</span></span>  <span data-ttu-id="0cd3b-126">truque Olá é perceber que é menor trabalho.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-126">hello trick is figuring out which is less work.</span></span>  <span data-ttu-id="0cd3b-127">Na maioria dos casos, distribuir as tabelas de factos grande numa coluna normalmente associada é Olá método mais eficaz para reduzir Olá a maioria das movimento de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-127">In most cases, distributing large fact tables on a commonly joined column is hello most effective method for reducing hello most data movement.</span></span>  <span data-ttu-id="0cd3b-128">Distribuição de dados em colunas de associação é um movimento de dados do método tooreduce muito mais comuns a distribuição de dados em colunas envolvidos numa agregação.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-128">Distributing data on join columns is a much more common method tooreduce data movement than distributing data on columns involved in an aggregation.</span></span>

## <a name="select-distribution-method"></a><span data-ttu-id="0cd3b-129">Selecione o método de distribuição</span><span class="sxs-lookup"><span data-stu-id="0cd3b-129">Select distribution method</span></span>
<span data-ttu-id="0cd3b-130">Em segundo plano do Olá, o SQL Data Warehouse divide os dados em 60 bases de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-130">Behind hello scenes, SQL Data Warehouse divides your data into 60 databases.</span></span>  <span data-ttu-id="0cd3b-131">Cada base de dados individuais é referenciado tooas um **distribuição**.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-131">Each individual database is referred tooas a **distribution**.</span></span>  <span data-ttu-id="0cd3b-132">Quando os dados são carregados para cada tabela, o SQL Data Warehouse tem tooknow como toodivide os dados entre estes 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-132">When data is loaded into each table, SQL Data Warehouse has tooknow how toodivide your data across these 60 distributions.</span></span>  

<span data-ttu-id="0cd3b-133">o método de distribuição de Olá é definido ao nível da tabela de Olá e atualmente, existem duas opções:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-133">hello distribution method is defined at hello table level and currently there are two choices:</span></span>

1. <span data-ttu-id="0cd3b-134">**O round robin** que distribui dados uniformemente mas aleatoriamente.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-134">**Round robin** which distribute data evenly but randomly.</span></span>
2. <span data-ttu-id="0cd3b-135">**A função hash distribuídas** que distribui dados com base em hash valores de uma única coluna</span><span class="sxs-lookup"><span data-stu-id="0cd3b-135">**Hash Distributed** which distributes data based on hashing values from a single column</span></span>

<span data-ttu-id="0cd3b-136">Por predefinição, quando não definem um método de distribuição de dados, a tabela será distribuída utilizando Olá **round robin** método de distribuição.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-136">By default, when you do not define a data distribution method, your table will be distributed using hello **round robin** distribution method.</span></span>  <span data-ttu-id="0cd3b-137">No entanto, à ficam mais sofisticadas na sua implementação, é aconselhável utilizar tooconsider **hash distribuída** tabelas de movimento de dados de toominimize que por sua vez irão otimizar o desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-137">However, as you become more sophisticated in your implementation, you will want tooconsider using **hash distributed** tables toominimize data movement which will in turn optimize query performance.</span></span>

### <a name="round-robin-tables"></a><span data-ttu-id="0cd3b-138">O Round Robin tabelas</span><span class="sxs-lookup"><span data-stu-id="0cd3b-138">Round Robin Tables</span></span>
<span data-ttu-id="0cd3b-139">A utilização de Olá Round Robin de método de distribuição de dados é muito como-SOA.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-139">Using hello Round Robin method of distributing data is very much how it sounds.</span></span>  <span data-ttu-id="0cd3b-140">Como os dados são carregados, cada linha é simplesmente enviada distribuição seguinte toohello.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-140">As your data is loaded, each row is simply sent toohello next distribution.</span></span>  <span data-ttu-id="0cd3b-141">Este método de distribuição de dados de Olá será sempre aleatoriamente distribuir dados Olá muito uniformemente em todas as distribuições de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-141">This method of distributing hello data will always randomly distribute hello data very evenly across all of hello distributions.</span></span>  <span data-ttu-id="0cd3b-142">Ou seja, não há qualquer ordenação efectuada durante Olá arredondar round robin processo que coloca os dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-142">That is, there is no sorting done during hello round robin process which places your data.</span></span>  <span data-ttu-id="0cd3b-143">Uma distribuição round robin denomina-se um hash aleatório por este motivo.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-143">A round robin distribution is sometimes called a random hash for this reason.</span></span>  <span data-ttu-id="0cd3b-144">Com uma tabela distribuída round robin há não existem dados de Olá toounderstand necessário.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-144">With a round-robin distributed table there is no need toounderstand hello data.</span></span>  <span data-ttu-id="0cd3b-145">Por este motivo, tabelas Round-Robin, muitas vezes, tornar carregamento boa destinos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-145">For this reason, Round-Robin tables often make good loading targets.</span></span>

<span data-ttu-id="0cd3b-146">Por predefinição, não se for escolhido nenhum método de distribuição, hello round robin distribuição método irá ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-146">By default, if no distribution method is chosen, hello round robin distribution method will be used.</span></span>  <span data-ttu-id="0cd3b-147">No entanto, enquanto o round robin tabelas são fáceis toouse, porque dados aleatoriamente são distribuídos por sistema Olá significa que o sistema Olá não pode garantir qual distribuição cada linha é no.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-147">However, while round robin tables are easy toouse, because data is randomly distributed across hello system it means that hello system can't guarantee which distribution each row is on.</span></span>  <span data-ttu-id="0cd3b-148">Como resultado, sistema de Olá, por vezes, precisa de tooinvoke um toobetter de operação de movimento de dados organize os dados antes de pode resolver uma consulta.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-148">As a result, hello system sometimes needs tooinvoke a data movement operation toobetter organize your data before it can resolve a query.</span></span>  <span data-ttu-id="0cd3b-149">Este passo adicional pode atrasar as suas consultas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-149">This extra step can slow down your queries.</span></span>

<span data-ttu-id="0cd3b-150">Considere utilizar o Round Robin distribuição para a sua tabela no Olá os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-150">Consider using Round Robin distribution for your table in hello following scenarios:</span></span>

* <span data-ttu-id="0cd3b-151">Quando introdução como um ponto de partida simple</span><span class="sxs-lookup"><span data-stu-id="0cd3b-151">When getting started as a simple starting point</span></span>
* <span data-ttu-id="0cd3b-152">Se não houver nenhuma chave joining óbvios</span><span class="sxs-lookup"><span data-stu-id="0cd3b-152">If there is no obvious joining key</span></span>
* <span data-ttu-id="0cd3b-153">Se não houver coluna bom candidato para distribuir a tabela de Olá de hash</span><span class="sxs-lookup"><span data-stu-id="0cd3b-153">If there is not good candidate column for hash distributing hello table</span></span>
* <span data-ttu-id="0cd3b-154">Se hello tabela não partilha uma chave de associação comuns com outras tabelas</span><span class="sxs-lookup"><span data-stu-id="0cd3b-154">If hello table does not share a common join key with other tables</span></span>
* <span data-ttu-id="0cd3b-155">Se a associação de Olá é menos significativa que outros associações na consulta de Olá</span><span class="sxs-lookup"><span data-stu-id="0cd3b-155">If hello join is less significant than other joins in hello query</span></span>
* <span data-ttu-id="0cd3b-156">Quando a tabela de Olá é uma tabela de transição temporária</span><span class="sxs-lookup"><span data-stu-id="0cd3b-156">When hello table is a temporary staging table</span></span>

<span data-ttu-id="0cd3b-157">Ambos estes exemplos irão criar uma tabela de Round Robin:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-157">Both of these examples will create a Round Robin Table:</span></span>

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
> <span data-ttu-id="0cd3b-158">Enquanto o round robin é o tipo de tabela Olá predefinido a ser explícita na sua DDL é considerado uma melhor prática, para que intenções Olá do seu esquema de tabela são tooothers encriptado.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-158">While round robin is hello default table type being explicit in your DDL is considered a best practice so that hello intentions of your table layout are clear tooothers.</span></span>
>
>

### <a name="hash-distributed-tables"></a><span data-ttu-id="0cd3b-159">Distribuída tabelas de hash</span><span class="sxs-lookup"><span data-stu-id="0cd3b-159">Hash Distributed Tables</span></span>
<span data-ttu-id="0cd3b-160">Utilizar um **Hash distribuída** algoritmo toodistribute as tabelas podem melhorar o desempenho de muitos cenários ao reduzir o movimento de dados no momento da consulta.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-160">Using a **Hash distributed** algorithm toodistribute your tables can improve performance for many scenarios by reducing data movement at query time.</span></span>  <span data-ttu-id="0cd3b-161">Hash distribuídas tabelas são tabelas que são divididas entre Olá distribuídas bases de dados utilizando um algoritmo hash numa única coluna que selecionar.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-161">Hash distributed tables are tables which are divided between hello distributed databases using a hashing algorithm on a single column which you select.</span></span>  <span data-ttu-id="0cd3b-162">a coluna de distribuição Olá é que determina a forma como os dados de Olá são divididos entre as bases de dados distribuídas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-162">hello distribution column is what determines how hello data is divided across your distributed databases.</span></span>  <span data-ttu-id="0cd3b-163">função de hash de Olá utiliza Olá distribuição coluna tooassign linhas toodistributions.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-163">hello hash function uses hello distribution column tooassign rows toodistributions.</span></span>  <span data-ttu-id="0cd3b-164">Olá algoritmo hash e distribuição resultante é determinística.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-164">hello hashing algorithm and resulting distribution is deterministic.</span></span>  <span data-ttu-id="0cd3b-165">Ou seja Olá mesmo valor com o mesmo tipo de dados será sempre de Olá tem toohello distribuição mesma.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-165">That is hello same value with hello same data type will always has toohello same distribution.</span></span>    

<span data-ttu-id="0cd3b-166">Neste exemplo, irá criar uma tabela distribuída no id de:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-166">This example will create a table distributed on id:</span></span>

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

## <a name="select-distribution-column"></a><span data-ttu-id="0cd3b-167">Selecione a coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="0cd3b-167">Select distribution column</span></span>
<span data-ttu-id="0cd3b-168">Quando escolhe demasiado**hash distribuir** uma tabela, terá de tooselect uma coluna de distribuição único.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-168">When you choose too**hash distribute** a table, you will need tooselect a single distribution column.</span></span>  <span data-ttu-id="0cd3b-169">Quando selecionar uma coluna de distribuição, existem três principais fatores tooconsider.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-169">When selecting a distribution column, there are three major factors tooconsider.</span></span>  

<span data-ttu-id="0cd3b-170">Selecione uma coluna que irá:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-170">Select a single column which will:</span></span>

1. <span data-ttu-id="0cd3b-171">Não é possível atualizar</span><span class="sxs-lookup"><span data-stu-id="0cd3b-171">Not be updated</span></span>
2. <span data-ttu-id="0cd3b-172">Distribuir dados uniformemente, evitando dados dissimetrias</span><span class="sxs-lookup"><span data-stu-id="0cd3b-172">Distribute data evenly, avoiding data skew</span></span>
3. <span data-ttu-id="0cd3b-173">Minimizar o movimento de dados</span><span class="sxs-lookup"><span data-stu-id="0cd3b-173">Minimize data movement</span></span>

### <a name="select-distribution-column-which-will-not-be-updated"></a><span data-ttu-id="0cd3b-174">Selecione a coluna de distribuição que não será atualizada</span><span class="sxs-lookup"><span data-stu-id="0cd3b-174">Select distribution column which will not be updated</span></span>
<span data-ttu-id="0cd3b-175">Colunas de distribuição não são atualizáveis, por conseguinte, selecione uma coluna com valores estáticos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-175">Distribution columns are not updatable, therefore, select a column with static values.</span></span>  <span data-ttu-id="0cd3b-176">Se uma coluna terá toobe atualizada, geralmente, não é um candidato a distribuição bom.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-176">If a column will need toobe updated, it is generally not a good distribution candidate.</span></span>  <span data-ttu-id="0cd3b-177">Se existir um caso onde deve atualizar uma coluna de distribuição, isto pode ser feito pelo primeiro eliminar linha Olá e, em seguida, a inserir uma nova linha.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-177">If there is a case where you must update a distribution column, this can be done by first deleting hello row and then inserting a new row.</span></span>

### <a name="select-distribution-column-which-will-distribute-data-evenly"></a><span data-ttu-id="0cd3b-178">Selecione a coluna de distribuição que será a distribuir uniformemente dados</span><span class="sxs-lookup"><span data-stu-id="0cd3b-178">Select distribution column which will distribute data evenly</span></span>
<span data-ttu-id="0cd3b-179">Uma vez que um sistema distribuído efetua apenas tão rápido como a distribuição da mesma mais lenta, é importante toodivide Olá trabalho uniformemente em toda as distribuições de Olá na ordem tooachieve com balanceamento de execução em sistema Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-179">Since a distributed system performs only as fast as its slowest distribution, it is important toodivide hello work evenly across hello distributions in order tooachieve balanced execution across hello system.</span></span>  <span data-ttu-id="0cd3b-180">forma Olá trabalho Olá está dividido num sistema distribuído baseia onde exista dados Olá para cada distribuição.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-180">hello way hello work is divided on a distributed system is based on where hello data for each distribution lives.</span></span>  <span data-ttu-id="0cd3b-181">Isto torna muito importante tooselect Olá distribuição direita coluna distribuir dados Olá, para que cada distribuição tem trabalho igual e irá tirar Olá mesmo tempo toocomplete sua parte do trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-181">This makes it very important tooselect hello right distribution column for distributing hello data so that each distribution has equal work and will take hello same time toocomplete its portion of hello work.</span></span>  <span data-ttu-id="0cd3b-182">Quando o trabalho também está dividido em sistema Olá, dados de Olá são equilibrados nos distribuições Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-182">When work is well divided across hello system, hello data is balanced across hello distributions.</span></span>  <span data-ttu-id="0cd3b-183">Quando os dados não é uniformemente balanceamento, chamamos a isto **desfasamento de dados**.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-183">When data is not evenly balanced, we call this **data skew**.</span></span>  

<span data-ttu-id="0cd3b-184">dados toodivide uniformemente e evitar dados dissimetrias, considere o seguinte Olá ao selecionar a coluna de distribuição:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-184">toodivide data evenly and avoid data skew, consider hello following when selecting your distribution column:</span></span>

1. <span data-ttu-id="0cd3b-185">Selecione uma coluna que contém um número significativo de valores distintos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-185">Select a column which contains a significant number of distinct values.</span></span>
2. <span data-ttu-id="0cd3b-186">Evite distribuição de dados em colunas com alguns valores distintos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-186">Avoid distributing data on columns with a few distinct values.</span></span>
3. <span data-ttu-id="0cd3b-187">Evite distribuição de dados em colunas com uma frequência alta de valores NULL.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-187">Avoid distributing data on columns with a high frequency of nulls.</span></span>
4. <span data-ttu-id="0cd3b-188">Evite distribuição de dados em colunas de data.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-188">Avoid distributing data on date columns.</span></span>

<span data-ttu-id="0cd3b-189">Uma vez que cada valor com hash too1 de 60 distribuições, distribuição, mesmo que tooachieve convém tooselect uma coluna que é exclusiva de elevada disponibilidade e contém mais de 60 valores exclusivos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-189">Since each value is hashed too1 of 60 distributions, tooachieve even distribution you will want tooselect a column that is highly unique and contains more than 60 unique values.</span></span>  <span data-ttu-id="0cd3b-190">tooillustrate, considere o caso em que uma coluna tem 40 valores exclusivos apenas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-190">tooillustrate, consider a case where a column only has 40 unique values.</span></span>  <span data-ttu-id="0cd3b-191">Se esta coluna foi selecionada como Olá de distribuição de chaves, dados de Olá para essa tabela seriam encaminhado para no 40 distribuições no máximo, deixando 20 distribuições com não dados e não toodo de processamento.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-191">If this column was selected as hello distribution key, hello data for that table would land on 40 distributions at most, leaving 20 distributions with no data and no processing toodo.</span></span>  <span data-ttu-id="0cd3b-192">Por outro lado, hello outras 40 distribuições teria mais toodo de trabalho que se hello dados foi uniformemente distribuídos mais de 60 distribuições.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-192">Conversely, hello other 40 distributions would have more work toodo that if hello data was evenly spread over 60 distributions.</span></span>  <span data-ttu-id="0cd3b-193">Este cenário é um exemplo de dados dissimetrias.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-193">This scenario is an example of data skew.</span></span>

<span data-ttu-id="0cd3b-194">Num sistema MPP, cada passo de consulta aguarda todas as distribuições toocomplete os respetivos partilha do trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-194">In MPP system, each query step waits for all distributions toocomplete their share of hello work.</span></span>  <span data-ttu-id="0cd3b-195">Se uma distribuição é efetuar trabalho mais do que outras pessoas Olá, em seguida, Olá recurso dos Olá outras distribuições são essencialmente desperdiçadas apenas aguardar a resposta de distribuição ocupado Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-195">If one distribution is doing more work than hello others, then hello resource of hello other distributions are essentially wasted just waiting on hello busy distribution.</span></span>  <span data-ttu-id="0cd3b-196">Quando o trabalho não é distribuído uniformemente por todas as distribuições, chamamos a isto **processamento dissimetrias**.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-196">When work is not evenly spread across all distributions, we call this **processing skew**.</span></span>  <span data-ttu-id="0cd3b-197">O desfasamento de processamento fará toorun consultas mais lenta do que o se carga de trabalho Olá serem distribuída uniformemente por distribuições Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-197">Processing skew will cause queries toorun slower than if hello workload can be evenly spread across hello distributions.</span></span>  <span data-ttu-id="0cd3b-198">O desfasamento de dados irá causar tooprocessing dissimetrias.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-198">Data skew will lead tooprocessing skew.</span></span>

<span data-ttu-id="0cd3b-199">Evitar distribuição na coluna de elevada disponibilidade que pode ser nula como valores nulos Olá serão todos os apresentado no Olá igual distribuição.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-199">Avoid distributing on highly nullable column as hello null values will all land on hello same distribution.</span></span> <span data-ttu-id="0cd3b-200">Distribuição de uma coluna de data pode também fazer com que processamento dissimetrias porque todos os dados para uma determinada data serão apresentado no Olá igual distribuição.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-200">Distributing on a date column can also cause processing skew because all data for a given date will land on hello same distribution.</span></span> <span data-ttu-id="0cd3b-201">Se vários utilizadores se encontram em execução filtragem todas as consultas no Olá mesmo data, em seguida, apenas 1 das distribuições de 60 Olá irá fazer todo o trabalho de Olá, uma vez que uma determinada data só estará num de distribuição.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-201">If several users are executing queries all filtering on hello same date, then only 1 of hello 60 distributions will be doing all of hello work since a given date will only be on one distribution.</span></span> <span data-ttu-id="0cd3b-202">Neste cenário, consultas de Olá, provavelmente, irão executar 60 vezes mais lentas do que o se os dados de Olá igualmente foram distribuídos por todas as distribuições de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-202">In this scenario, hello queries will likely run 60 times slower than if hello data were equally spread over all of hello distributions.</span></span>

<span data-ttu-id="0cd3b-203">Quando não existe nenhuma coluna bom candidato, em seguida, considere utilizar o round robin como método de distribuição Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-203">When no good candidate columns exist, then consider using round robin as hello distribution method.</span></span>

### <a name="select-distribution-column-which-will-minimize-data-movement"></a><span data-ttu-id="0cd3b-204">Selecione a coluna de distribuição que irá minimizar o movimento de dados</span><span class="sxs-lookup"><span data-stu-id="0cd3b-204">Select distribution column which will minimize data movement</span></span>
<span data-ttu-id="0cd3b-205">Minimizar o movimento de dados selecionando a coluna da direita da distribuição de Olá é uma das estratégias de mais importantes de Olá para otimizar o desempenho do seu SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-205">Minimizing data movement by selecting hello right distribution column is one of hello most important strategies for optimizing performance of your SQL Data Warehouse.</span></span>  <span data-ttu-id="0cd3b-206">Movimento de dados for mais frequentemente quando estão associadas a tabelas ou agregações são executadas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-206">Data Movement most commonly arises when tables are joined or aggregations are performed.</span></span>  <span data-ttu-id="0cd3b-207">As colunas utilizadas no `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` e `HAVING` cláusulas todas tornam para **boa** candidatos a distribuição de hash.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-207">Columns used in `JOIN`, `GROUP BY`, `DISTINCT`, `OVER` and `HAVING` clauses all make for **good** hash distribution candidates.</span></span>

<span data-ttu-id="0cd3b-208">No Olá por outro lado, as colunas na Olá `WHERE` cláusula efetue **não** efetuar para candidatos de coluna de hash boa porque estes limitam as distribuições participam na consulta de Olá, fazendo com que o processamento dissimetrias.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-208">On hello other hand, columns in hello `WHERE` clause do **not** make for good hash column candidates because they limit which distributions participate in hello query, causing processing skew.</span></span>  <span data-ttu-id="0cd3b-209">Um bom exemplo de uma coluna que pode ser tempting toodistribute no, mas, muitas vezes, pode causar este processamento dissimetrias é uma coluna de data.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-209">A good example of a column which might be tempting toodistribute on, but often can cause this processing skew is a date column.</span></span>

<span data-ttu-id="0cd3b-210">Um modo geral, se tiver duas tabelas de factos grande frequentemente envolvidas numa associação, irá obter Olá um desempenho mais por distribuição de ambas as tabelas numa das colunas de associação de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-210">Generally speaking, if you have two large fact tables frequently involved in a join, you will gain hello most performance by distributing both tables on one of hello join columns.</span></span>  <span data-ttu-id="0cd3b-211">Se tiver uma tabela que nunca esteja tabela de factos grande de tooanother associados, em seguida, procure toocolumns que estão frequentemente Olá `GROUP BY` cláusula.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-211">If you have a table that is never joined tooanother large fact table, then look toocolumns that are frequently in hello `GROUP BY` clause.</span></span>

<span data-ttu-id="0cd3b-212">Existem alguns chaves os critérios que têm de ser cumpridos tooavoid movimento de dados durante uma associação:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-212">There are a few key criteria which must be met tooavoid data movement during a join:</span></span>

1. <span data-ttu-id="0cd3b-213">Olá tabelas envolvidos na associação Olá tem de ser hash distribuído **um** de colunas de Olá participar na União Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-213">hello tables involved in hello join must be hash distributed on **one** of hello columns participating in hello join.</span></span>
2. <span data-ttu-id="0cd3b-214">tipos de dados de Olá de colunas de associação de Olá tem de corresponder entre ambas as tabelas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-214">hello data types of hello join columns must match between both tables.</span></span>
3. <span data-ttu-id="0cd3b-215">colunas de Olá tem de ser associadas com um operador igual a.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-215">hello columns must be joined with an equals operator.</span></span>
4. <span data-ttu-id="0cd3b-216">Olá tipo de associação não pode ser um `CROSS JOIN`.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-216">hello join type may not be a `CROSS JOIN`.</span></span>

## <a name="troubleshooting-data-skew"></a><span data-ttu-id="0cd3b-217">Dados dissimetrias de resolução de problemas</span><span class="sxs-lookup"><span data-stu-id="0cd3b-217">Troubleshooting data skew</span></span>
<span data-ttu-id="0cd3b-218">Quando os dados da tabela são distribuídos utilizando o método de distribuição de hash de Olá há a possibilidade de algumas distribuições será skewed toohave disproportionately mais dados que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-218">When table data is distributed using hello hash distribution method there is a chance that some distributions will be skewed toohave disproportionately more data than others.</span></span> <span data-ttu-id="0cd3b-219">Dados excessivos dissimetrias podem afetar o desempenho de consulta porque o resultado final do Olá de uma consulta distribuída tem de aguardar Olá mais longo em execução distribuição toofinish.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-219">Excessive data skew can impact query performance because hello final result of a distributed query must wait for hello longest running distribution toofinish.</span></span> <span data-ttu-id="0cd3b-220">Dependendo grau de Olá dos dados de Olá dissimetrias que poderá ser necessário tooaddress-lo.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-220">Depending on hello degree of hello data skew you might need tooaddress it.</span></span>

### <a name="identifying-skew"></a><span data-ttu-id="0cd3b-221">Identificar desfasamento</span><span class="sxs-lookup"><span data-stu-id="0cd3b-221">Identifying skew</span></span>
<span data-ttu-id="0cd3b-222">Uma forma simples de tooidentify uma tabela como skewed é toouse `DBCC PDW_SHOWSPACEUSED`.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-222">A simple way tooidentify a table as skewed is toouse `DBCC PDW_SHOWSPACEUSED`.</span></span>  <span data-ttu-id="0cd3b-223">Esta é uma forma muito rápida e simples toosee Olá número de linhas de tabela que estão armazenados em cada uma das distribuições de Olá 60 da base de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-223">This is a very quick and simple way toosee hello number of table rows that are stored in each of hello 60 distributions of your database.</span></span>  <span data-ttu-id="0cd3b-224">Lembre-se de que para um desempenho mais com balanceamento de Olá, linhas de Olá na tabela distribuída devem ser distribuídas uniformemente por todas as distribuições de Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-224">Remember that for hello most balanced performance, hello rows in your distributed table should be spread evenly across all hello distributions.</span></span>

```sql
-- Find data skew for a distributed table
DBCC PDW_SHOWSPACEUSED('dbo.FactInternetSales');
```

<span data-ttu-id="0cd3b-225">No entanto, se consultar vistas de gestão dinâmica do Azure SQL Data Warehouse Olá (DMV) pode executar uma análise mais detalhada.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-225">However, if you query hello Azure SQL Data Warehouse dynamic management views (DMV) you can perform a more detailed analysis.</span></span>  <span data-ttu-id="0cd3b-226">toostart, criar vista Olá [dbo.vTableSizes] [ dbo.vTableSizes] vistos através de Olá SQL a partir do [descrição geral da tabela] [ Overview] artigo.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-226">toostart, create hello view [dbo.vTableSizes][dbo.vTableSizes] view using hello SQL from [Table Overview][Overview] article.</span></span>  <span data-ttu-id="0cd3b-227">Assim que for criada vista Olá, execute este tooidentify de consulta que tabelas tem mais do que o desfasamento de dados de 10%.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-227">Once hello view is created, run this query tooidentify which tables have more than 10% data skew.</span></span>

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

### <a name="resolving-data-skew"></a><span data-ttu-id="0cd3b-228">Resolver dados dissimetrias</span><span class="sxs-lookup"><span data-stu-id="0cd3b-228">Resolving data skew</span></span>
<span data-ttu-id="0cd3b-229">Não todos os dissimetrias é suficiente toowarrant uma correção.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-229">Not all skew is enough toowarrant a fix.</span></span>  <span data-ttu-id="0cd3b-230">Em alguns casos, desempenho Olá de uma tabela em algumas consultas pode prevalecem sobre a possibilidade de Olá dos dados dissimetrias.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-230">In some cases, hello performance of a table in some queries can outweigh hello harm of data skew.</span></span>  <span data-ttu-id="0cd3b-231">toodecide se deve resolver dados desfasamento numa tabela, deve compreender quanto possível sobre os volumes de dados de Olá e consultas na sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-231">toodecide if you should resolve data skew in a table, you should understand as much as possible about hello data volumes and queries in your workload.</span></span>   <span data-ttu-id="0cd3b-232">Uma forma toolook no impacto Olá de desfasamento é toouse passos Olá Olá [consulta monitorização] [ Query Monitoring] artigo toomonitor Olá impacto dissimetrias no desempenho das consultas e especificamente Olá consultas de tempo de toohow de impacto colocar toocomplete distribuições individuais Olá.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-232">One way toolook at hello impact of skew is toouse hello steps in hello [Query Monitoring][Query Monitoring] article toomonitor hello impact of skew on query performance and specifically hello impact toohow long queries take toocomplete on hello individual distributions.</span></span>

<span data-ttu-id="0cd3b-233">Distribuição de dados é um fim de encontrar o equilíbrio certo entre Olá entre minimizando desfasamento de dados e minimizar o movimento de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-233">Distributing data is a matter of finding hello right balance between minimizing data skew and minimizing data movement.</span></span> <span data-ttu-id="0cd3b-234">Estes podem ser opposing objetivos e, por vezes, é aconselhável tookeep dados dissimetrias no movimento de dados de tooreduce de ordem.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-234">These can be opposing goals, and sometimes you will want tookeep data skew in order tooreduce data movement.</span></span> <span data-ttu-id="0cd3b-235">Por exemplo, quando a coluna de distribuição Olá é frequentemente Olá partilhado coluna associações e agregações, irá ser minimizando movimento de dados.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-235">For example, when hello distribution column is frequently hello shared column in joins and aggregations, you will be minimizing data movement.</span></span> <span data-ttu-id="0cd3b-236">Olá vantagem de ter o movimento de dados mínimo de Olá poderá compensar impacto Olá da eliminação de dados desfasamento.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-236">hello benefit of having hello minimal data movement might outweigh hello impact of having data skew.</span></span>

<span data-ttu-id="0cd3b-237">forma típico Olá tooresolve desfasamento de dados é toore-criar a tabela de Olá com uma coluna de distribuição diferente.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-237">hello typical way tooresolve data skew is toore-create hello table with a different distribution column.</span></span> <span data-ttu-id="0cd3b-238">Porque não existe nenhuma forma de tabela de coluna de distribuição de Olá toochange no existente, Olá forma toochange Olá distribuição uma tabela-toorecreate-o com um [[CTAS]].</span><span class="sxs-lookup"><span data-stu-id="0cd3b-238">Since there is no way toochange hello distribution column on an existing table, hello way toochange hello distribution of a table it toorecreate it with a [CTAS][].</span></span>  <span data-ttu-id="0cd3b-239">Seguem-se dois exemplos de como resolver dados dissimetrias:</span><span class="sxs-lookup"><span data-stu-id="0cd3b-239">Here are two examples of how resolve data skew:</span></span>

### <a name="example-1-re-create-hello-table-with-a-new-distribution-column"></a><span data-ttu-id="0cd3b-240">Exemplo 1: Voltar a criar tabela Olá com uma nova coluna de distribuição</span><span class="sxs-lookup"><span data-stu-id="0cd3b-240">Example 1: Re-create hello table with a new distribution column</span></span>
<span data-ttu-id="0cd3b-241">Este exemplo utiliza [CTAS] [] toore-criar uma tabela com uma coluna de distribuição hash diferentes.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-241">This example uses [CTAS][] toore-create a table with a different hash distribution column.</span></span>

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

### <a name="example-2-re-create-hello-table-using-round-robin-distribution"></a><span data-ttu-id="0cd3b-242">Exemplo 2: Voltar a criar tabela Olá utilizando o round robin distribuição</span><span class="sxs-lookup"><span data-stu-id="0cd3b-242">Example 2: Re-create hello table using round robin distribution</span></span>
<span data-ttu-id="0cd3b-243">Este exemplo utiliza [CTAS] [] toore-crie uma tabela com o round robin, em vez de uma distribuição hash.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-243">This example uses [CTAS][] toore-create a table with round robin instead of a hash distribution.</span></span> <span data-ttu-id="0cd3b-244">Esta alteração produzirá distribuição de dados, mesmo que custo Olá de movimento de dados maior.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-244">This change will produce even data distribution at hello cost of increased data movement.</span></span>

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

## <a name="next-steps"></a><span data-ttu-id="0cd3b-245">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="0cd3b-245">Next steps</span></span>
<span data-ttu-id="0cd3b-246">toolearn mais informações sobre a estrutura da tabela, consulte Olá [distribuir][Distribute], [índice][Index], [partição] [ Partition], [Tipos de dados][Data Types], [estatísticas] [ Statistics] e [tabelas temporárias] [ Temporary] artigos.</span><span class="sxs-lookup"><span data-stu-id="0cd3b-246">toolearn more about table design, see hello [Distribute][Distribute], [Index][Index], [Partition][Partition], [Data Types][Data Types], [Statistics][Statistics] and [Temporary Tables][Temporary] articles.</span></span>

<span data-ttu-id="0cd3b-247">Para obter uma descrição geral de melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="0cd3b-247">For an overview of best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

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
