---
title: "o nível de compatibilidade de aaaDatabase 130 - SQL Database do Azure | Microsoft Docs"
description: "Neste artigo, vamos explorar as vantagens de Olá da SQL Database do Azure a executar ao nível de compatibilidade 130 e tirar partido dos benefícios de Olá do novo otimizador de consultas Olá e consultar as funcionalidades do processador. Podemos também endereços Olá possíveis-efeitos secundários no desempenho das consultas Olá para aplicações de SQL Olá existentes."
services: sql-database
documentationcenter: 
author: alainlissoir
manager: jhubbard
editor: 
ms.assetid: 8619f90b-7516-46dc-9885-98429add0053
ms.service: sql-database
ms.custom: monitor & tune
ms.workload: data-management
ms.devlang: NA
ms.tgt_pltfrm: NA
ms.topic: article
ms.date: 08/08/2016
ms.author: alainl
ms.openlocfilehash: 25693c5f7b01405b7073fa7d4cc2833fbe125e2f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="improved-query-performance-with-compatibility-level-130-in-azure-sql-database"></a><span data-ttu-id="9c2b0-104">Melhorada desempenho das consultas com 130 de nível de compatibilidade na SQL Database do Azure</span><span class="sxs-lookup"><span data-stu-id="9c2b0-104">Improved query performance with compatibility Level 130 in Azure SQL Database</span></span>
<span data-ttu-id="9c2b0-105">Base de dados SQL do Azure está em execução transparente centenas de milhares de bases de dados em vários níveis de compatibilidade diferentes, preservando e guaranteeing versão correspondente do toohello de compatibilidade com versões anteriores de Olá do Microsoft SQL Server para todos os seus clientes!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-105">Azure SQL Database is running transparently hundreds of thousands of databases at many different compatibility levels, preserving and guaranteeing hello backward compatibility toohello corresponding version of Microsoft SQL Server for all its customers!</span></span>

<span data-ttu-id="9c2b0-106">Neste artigo, vamos explorar as vantagens de Olá da sua Databse de SQL do Azure a executar ao nível de compatibilidade 130 e tirar partido dos benefícios de Olá do novo otimizador de consultas Olá e consultar as funcionalidades do processador.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-106">In this article, we explore hello benefits of running your Azure SQL Databse at compatibility level 130, and leveraging hello benefits of hello new query optimizer and query processor features.</span></span> <span data-ttu-id="9c2b0-107">Podemos também endereços Olá possíveis-efeitos secundários no desempenho das consultas Olá para aplicações de SQL Olá existentes.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-107">We also address hello possible side-effects on hello query performance for hello existing SQL applications.</span></span>

<span data-ttu-id="9c2b0-108">Como um lembrete do histórico, alinhamento Olá dos níveis de compatibilidade do SQL Server versões toodefault são:</span><span class="sxs-lookup"><span data-stu-id="9c2b0-108">As a reminder of history, hello alignment of SQL versions toodefault compatibility levels are as follows:</span></span>

* <span data-ttu-id="9c2b0-109">100: no SQL Server 2008 e o Azure SQL da base de dados V11.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-109">100: in SQL Server 2008 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="9c2b0-110">110: no SQL Server 2012 e SQL do Azure da base de dados V11.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-110">110: in SQL Server 2012 and Azure SQL Database V11.</span></span>
* <span data-ttu-id="9c2b0-111">120: no SQL Server 2014 e SQL do Azure da base de dados V12.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-111">120: in SQL Server 2014 and Azure SQL Database V12.</span></span>
* <span data-ttu-id="9c2b0-112">130: no SQL Server 2016 e o Azure SQL da base de dados V12.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-112">130: in SQL Server 2016 and Azure SQL Database V12.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="9c2b0-113">A partir de **mid Junho de 2016**, na base de dados SQL do Azure, o nível de compatibilidade predefinido Olá será 130 em vez de 120 para **recém-criado** bases de dados.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-113">Starting in **mid-June 2016**, in Azure SQL Database, hello default compatibility level will be 130 instead of 120 for **newly created** databases.</span></span>
> 
> <span data-ttu-id="9c2b0-114">Bases de dados criadas antes mid Junho de 2016 serão *não* afetadas e irão manter o respetivo nível de compatibilidade atual (100, 110 ou 120).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-114">Databases created before mid-June 2016 will *not* be affected, and will maintain their current compatibility level (100, 110, or 120).</span></span> <span data-ttu-id="9c2b0-115">As bases de dados migrados de SQL Database do Azure versão V11 tooV12 terão um nível de compatibilidade 110 ou 100.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-115">Databases that migrated from Azure SQL Database version V11 tooV12 will have a compatibility level of either 100 or 110.</span></span> 
> 

## <a name="about-compatibility-level-130"></a><span data-ttu-id="9c2b0-116">Sobre o nível de compatibilidade 130</span><span class="sxs-lookup"><span data-stu-id="9c2b0-116">About compatibility level 130</span></span>
<span data-ttu-id="9c2b0-117">Em primeiro lugar, se quiser tooknow Olá atual nível de compatibilidade da base de dados, execute Olá a seguinte instrução Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-117">First, if you want tooknow hello current compatibility level of your database, execute hello following Transact-SQL statement.</span></span>

```
SELECT compatibility_level
    FROM sys.databases
    WHERE name = '<YOUR DATABASE_NAME>’;
```


<span data-ttu-id="9c2b0-118">Antes desta alteração toolevel 130 acontece para **recentemente** criar bases de dados, vamos rever o que esta alteração é tudo através de alguns exemplos de consultas muito básica e ver como a qualquer pessoa pode beneficiar do mesmo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-118">Before this change toolevel 130 happens for **newly** created databases, let’s review what this change is all about through some very basic query examples, and see how anyone can benefit from it.</span></span>

<span data-ttu-id="9c2b0-119">O processamento da consulta em bases de dados relacionais pode ser muito complexo e pode levar toolots de computador ciência e mathematics toounderstand Olá inerente opções de design e comportamentos.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-119">Query processing in relational databases can be very complex and can lead toolots of computer science and mathematics toounderstand hello inherent design choices and behaviors.</span></span> <span data-ttu-id="9c2b0-120">Neste documento, o conteúdo de Olá foi intencionalmente simplificada tooensure que qualquer pessoa com algum conhecimento técnico mínimo compreender Olá impacto da alteração de nível de compatibilidade de Olá e determinar como beneficiar aplicações.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-120">In this document, hello content has been intentionally simplified tooensure that anyone with some minimum technical background can understand hello impact of hello compatibility level change and determine how it can benefit applications.</span></span>

<span data-ttu-id="9c2b0-121">Vamos ter ver rapidamente o nível de compatibilidade de Olá 130 coloca na tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-121">Let’s have a quick look at what hello compatibility level 130 brings at hello table.</span></span>  <span data-ttu-id="9c2b0-122">Pode encontrar mais detalhes em [ALTER a nível de compatibilidade da base de dados (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), mas Eis um breve resumo:</span><span class="sxs-lookup"><span data-stu-id="9c2b0-122">You can find more details at [ALTER DATABASE Compatibility Level (Transact-SQL)](https://msdn.microsoft.com/library/bb510680.aspx), but here is a short summary:</span></span>

* <span data-ttu-id="9c2b0-123">Olá a operação de inserção de uma instrução Insert select pode ser multi-thread ou pode ter um plano paralelo, enquanto que antes desta operação foi single-threaded.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-123">hello Insert operation of an Insert-select statement can be multi-threaded or can have a parallel plan, while before this operation was single-threaded.</span></span>
* <span data-ttu-id="9c2b0-124">Memória Optimized tabela e consultas de variáveis de tabela podem agora tem planos paralelos, enquanto que antes desta operação foi também single-threaded.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-124">Memory Optimized table and table variables queries can now have parallel plans, while before this operation was also single-threaded .</span></span>
* <span data-ttu-id="9c2b0-125">Estatísticas para a tabela com otimização de memória agora podem ser convertidas e são atualizados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-125">Statistics for Memory Optimized table can now be sampled and are auto-updated.</span></span> <span data-ttu-id="9c2b0-126">Consulte [Novidades no motor de base de dados: OLTP na memória](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-126">See [What's New in Database Engine: In-Memory OLTP](https://msdn.microsoft.com/library/bb510411.aspx#InMemory) for more details.</span></span>
* <span data-ttu-id="9c2b0-127">Modo de batch v/s modo linha alterações com os índices de arquivo de colunas</span><span class="sxs-lookup"><span data-stu-id="9c2b0-127">Batch mode v/s Row Mode changes with Column Store indexes</span></span>
  * <span data-ttu-id="9c2b0-128">Ordena numa tabela com um índice de arquivo de coluna está agora em modo batch.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-128">Sorts on a table with a Column Store index are now in batch mode.</span></span>
  * <span data-ttu-id="9c2b0-129">Os agregados de modos de janela agora operam em modo de lote, tais como as declarações de desfasamento de TSQL/oportunidades potenciais.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-129">Windowing aggregates now operate in batch mode such as TSQL LAG/LEAD statements.</span></span>
  * <span data-ttu-id="9c2b0-130">As consultas em tabelas de arquivo de colunas com múltiplas cláusulas distintas operam em modo de Batch.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-130">Queries on Column Store tables with Multiple distinct clauses operate in Batch mode.</span></span>
  * <span data-ttu-id="9c2b0-131">As consultas em execução em DOP = 1 ou com um plano de série também de ser executado no modo de Batch.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-131">Queries running under DOP=1 or with a serial plan also execute in Batch Mode.</span></span>
* <span data-ttu-id="9c2b0-132">Melhoramentos de estimativa de cardinalidade realmente vêm com o nível de compatibilidade 120, mas os de que a ser executado numa compatibilidade inferior ao nível (ou seja, 100, ou 110), hello mover toocompatibility nível 130 será também apresentada estas melhorias e estes também podem pela última vez, beneficiar desempenho das consultas Olá das suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-132">Last, Cardinality Estimation improvements are actually coming with compatibility level 120, but for those of you running at a lower Compatibility level (i.e. 100, or 110), hello move toocompatibility level 130 will also bring these improvements, and these can also benefit hello query performance of your applications.</span></span>

## <a name="practicing-compatibility-level-130"></a><span data-ttu-id="9c2b0-133">Nível de compatibilidade practicing 130</span><span class="sxs-lookup"><span data-stu-id="9c2b0-133">Practicing compatibility level 130</span></span>
<span data-ttu-id="9c2b0-134">Primeiro vamos obter algumas tabelas, índices e dados aleatórios criados toopractice algumas destas novas capacidades.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-134">First let’s get some tables, indexes and random data created toopractice some of these new capabilities.</span></span> <span data-ttu-id="9c2b0-135">Exemplos de script TSQL Olá podem ser executados com o SQL Server 2016 ou na SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-135">hello TSQL script examples can be executed under SQL Server 2016, or under Azure SQL Database.</span></span> <span data-ttu-id="9c2b0-136">No entanto, quando criar uma base de dados SQL do Azure, certifique-se que escolha no Olá mínimo um P2 da base de dados porque necessita de, pelo menos, duas núcleos tooallow vários segmentos e beneficiar, por conseguinte, estas funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-136">However, when creating an Azure SQL database, make sure you choose at hello minimum a P2 database because you need at least a couple of cores tooallow multi-threading and therefore benefit from these features.</span></span>

```
-- Create a Premium P2 Database in Azure SQL Database

CREATE DATABASE MyTestDB
    (EDITION=’Premium’, SERVICE_OBJECTIVE=’P2′);
GO

-- Create 2 tables with a column store index on
-- hello second one (only available on Premium databases)

CREATE TABLE T_source
    (Color varchar(10), c1 bigint, c2 bigint);

CREATE TABLE T_target
    (c1 bigint, c2 bigint);

CREATE CLUSTERED COLUMNSTORE INDEX CCI ON T_target;
GO

-- Insert few rows.

INSERT T_source VALUES
    (‘Blue’, RAND() * 100000, RAND() * 100000),
    (‘Yellow’, RAND() * 100000, RAND() * 100000),
    (‘Red’, RAND() * 100000, RAND() * 100000),
    (‘Green’, RAND() * 100000, RAND() * 100000),
    (‘Black’, RAND() * 100000, RAND() * 100000);

GO 200

INSERT T_source SELECT * FROM T_source;

GO 10
```


<span data-ttu-id="9c2b0-137">Agora, vamos tem um toosome aspeto das funcionalidades de consulta de processamento de Olá vem com um nível de compatibilidade 130.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-137">Now, let’s have a look toosome of hello Query Processing features coming with compatibility level 130.</span></span>

## <a name="parallel-insert"></a><span data-ttu-id="9c2b0-138">INSERT paralela</span><span class="sxs-lookup"><span data-stu-id="9c2b0-138">Parallel INSERT</span></span>
<span data-ttu-id="9c2b0-139">Executar Olá TSQL as instruções abaixo executa Olá a operação de inserção em nível de compatibilidade 120 e 130, que executa respetivamente Olá a operação de inserção de um modelo de threading único (120) e de um modelo com vários threads (130).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-139">Executing hello TSQL statements below executes hello INSERT operation under compatibility level 120 and 130, which respectively executes hello INSERT operation in a single threaded model (120), and in a multi-threaded model (130).</span></span>

```
-- Parallel INSERT … SELECT … in heap or CCI
-- is available under 130 only

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO 

-- hello INSERT part is in serial

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130
GO

-- hello INSERT part is in parallel

INSERT t_target WITH (tablock)
    SELECT C1, COUNT(C2) * 10 * RAND()
        FROM T_source
        GROUP BY C1
    OPTION (RECOMPILE);

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-140">Ao solicitar o plano de consulta de Olá real Olá, observar a representação gráfica ou o respetivo conteúdo XML, pode determinar que estimativa de cardinalidade função é na play.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-140">By requesting hello actual hello query plan, looking at its graphical representation or its XML content, you can determine which Cardinality Estimation function is at play.</span></span> <span data-ttu-id="9c2b0-141">Observar Olá planos do lado do lado a lado na figura 1, pode claramente, Vemos que Olá inserir do arquivo de colunas execução fica da série em 120 tooparallel no 130.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-141">Looking at hello plans side-by-side on figure 1, we can clearly see that hello Column Store INSERT execution goes from serial in 120 tooparallel in 130.</span></span> <span data-ttu-id="9c2b0-142">Além disso, tenha em atenção que alteração Olá do ícone de iterator Olá no plano 130 Olá dois setas paralelas, que mostra que ilustra o facto de Olá agora Olá execução iterator é realmente paralela.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-142">Also, note that hello change of hello iterator icon in hello 130 plan showing two parallel arrows, illustrating hello fact that now hello iterator execution is indeed parallel.</span></span> <span data-ttu-id="9c2b0-143">Se tiver um grande toocomplete de operações de inserção, execução paralela de Olá, toohello ligado número de núcleos que tem na sua disposal da base de dados de Olá, terão um desempenho superior; cópia de segurança tooa 100 vezes mais rápida consoante a sua situação!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-143">If you have large INSERT operations toocomplete, hello parallel execution, linked toohello number of core you have at your disposal for hello database, will perform better; up tooa 100 times faster depending your situation!</span></span>

<span data-ttu-id="9c2b0-144">*Figura 1: Inserir alterações de operação de série tooparallel com um nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-144">*Figure 1: INSERT operation changes from serial tooparallel with compatibility level 130.*</span></span>

![Figura 1](./media/sql-database-compatibility-level-query-performance-130/figure-1.jpg)

## <a name="serial-batch-mode"></a><span data-ttu-id="9c2b0-146">Modo de Batch de série</span><span class="sxs-lookup"><span data-stu-id="9c2b0-146">SERIAL Batch Mode</span></span>
<span data-ttu-id="9c2b0-147">Da mesma forma, mover toocompatibility nível 130 durante o processamento de linhas de dados permite o processamento de modo de batch.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-147">Similarly, moving toocompatibility level 130 when processing rows of data enables batch mode processing.</span></span> <span data-ttu-id="9c2b0-148">Em primeiro lugar, as operações de modo de lote só estão disponíveis quando tem um índice de arquivo de colunas no local.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-148">First, batch mode operations  are only available when you have a column store index in place.</span></span> <span data-ttu-id="9c2b0-149">Segundo, um lote normalmente representa ~ 900 linhas e utiliza uma lógica de código otimizada para a CPU especializada, débito de memória superior e diretamente tira partido Olá dados comprimidos de Olá coluna arquivo sempre que possível.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-149">Second, a batch typically represents ~900 rows, and uses a code logic optimized for multicore CPU, higher memory throughput and directly leverages hello compressed data of hello Column Store whenever possible.</span></span> <span data-ttu-id="9c2b0-150">Nas seguintes condições, SQL Server 2016 pode processar ~ 900 linhas de uma só vez, em vez de 1 linha momento Olá, e como consequence, hello custo global gerais da operação de Olá é agora partilhado por lote inteiro Olá, reduzindo Olá geral custo por linha.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-150">Under these conditions, SQL Server 2016 can process ~900 rows at once, instead of 1 row at hello time, and as a consequence, hello overall overhead cost of hello operation is now shared by hello entire batch, reducing hello overall cost by row.</span></span> <span data-ttu-id="9c2b0-151">Esta quantidade partilhada operações combinado com compressão de arquivo de colunas de Olá basicamente reduz a latência de Olá envolvida numa operação batch SELECIONE modo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-151">This shared amount of operations combined with hello column store compression basically reduces hello latency involved in a SELECT batch mode operation.</span></span> <span data-ttu-id="9c2b0-152">Pode encontrar mais detalhes acerca do arquivo de colunas de Olá e lote modo em [guia de índices Columnstore](https://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-152">You can find more details about hello column store and batch mode at [Columnstore Indexes Guide](https://msdn.microsoft.com/library/gg492088.aspx).</span></span>

```
-- Serial batch mode execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT (C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO 

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-153">Como visível abaixo, ao observar Olá consulta planos do lado do lado a lado na figura 2, é possível ver que o modo de processamento de Olá foi alterada com um nível de compatibilidade de Olá, e como consequence, quando executar consultas Olá completamente em ambos os nível de compatibilidade, é possível ver que a maioria do tempo de processamento de Olá é despendido no modo de (86%) em comparação com toohello batch modo linha (14%), onde 2 lotes foram processados.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-153">As visible below, by observing hello query plans side-by-side on figure 2, we can see that hello processing mode has changed with hello compatibility level, and as a consequence, when executing hello queries in both compatibility level altogether, we can see that most of hello processing time is spent in row mode (86%) compared toohello batch mode (14%), where 2 batches have been processed.</span></span> <span data-ttu-id="9c2b0-154">Aumentar o conjunto de dados de Olá, hello benefício irá aumentar.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-154">Increase hello dataset, hello benefit will increase.</span></span>

<span data-ttu-id="9c2b0-155">*Figura 2: SELECIONE as alterações de operação do modo de toobatch série com o nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-155">*Figure 2: SELECT operation changes from serial toobatch mode with compatibility level 130.*</span></span>

![Figura 2](./media/sql-database-compatibility-level-query-performance-130/figure-2.jpg)

## <a name="batch-mode-on-sort-execution"></a><span data-ttu-id="9c2b0-157">Modo de batch na execução de ordenação</span><span class="sxs-lookup"><span data-stu-id="9c2b0-157">Batch mode on Sort Execution</span></span>
<span data-ttu-id="9c2b0-158">Transição de Olá toohello semelhante acima, mas a operação de ordenação tooa aplicados, do modo de toobatch linha modo (nível de compatibilidade 120) (nível de compatibilidade 130) melhora o desempenho de Olá de Olá operação de ordenação para Olá as mesmas razões.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-158">Similar toohello above, but applied tooa sort operation, hello transition from row mode (compatibility level 120) toobatch mode (compatibility level 130) improves hello performance of hello SORT operation for hello same reasons.</span></span>

```
-- Batch mode on sort execution

SET STATISTICS XML ON;

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 120;
GO

-- hello scan and aggregate are in row mode

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

-- hello scan and aggregate are in batch mode,
-- and force MAXDOP too1 tooshow that batch mode
-- also now works in serial mode.

SELECT C1, COUNT(C2)
    FROM T_target
    GROUP BY C1
    ORDER BY C1
    OPTION (MAXDOP 1, RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-159">Visível do lado do lado a lado na figura 3, é possível ver que a operação de ordenação Olá no modo linha representa 81% de Olá custo, enquanto o modo de batch de Olá representa apenas % 19 de custo de Olá (respetivamente 81% e % de 56 na ordenação Olá próprio).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-159">Visible side-by-side on figure 3, we can see that hello sort operation in row mode represents 81% of hello cost, while hello batch mode only represents 19% of hello cost (respectively 81% and 56% on hello sort itself).</span></span>

<span data-ttu-id="9c2b0-160">*Figura 3: A operação de ordenação alterações do modo de toobatch linha com o nível de compatibilidade 130.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-160">*Figure 3: SORT operation changes from row toobatch mode with compatibility level 130.*</span></span>

![Figura 3](./media/sql-database-compatibility-level-query-performance-130/figure-3.png)

<span data-ttu-id="9c2b0-162">Obviamente, estes exemplos só contenham dezenas de milhares de linhas, que é nothing quando observar os dados de Olá disponíveis na maioria dos SQL Servers estes dias.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-162">Obviously, these samples only contain tens of thousands of rows, which is nothing when looking at hello data available in most SQL Servers these days.</span></span> <span data-ttu-id="9c2b0-163">Apenas projeto estes contra milhões de linhas em vez disso, e isto pode traduzir em vários minutos de execução spared diariamente pendentes natureza Olá a carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-163">Just project these against millions of rows instead, and this can translate in several minutes of execution spared every day pending hello nature of your workload.</span></span>

## <a name="cardinality-estimation-ce-improvements"></a><span data-ttu-id="9c2b0-164">Melhoramentos de estimativa (CE) de cardinalidade</span><span class="sxs-lookup"><span data-stu-id="9c2b0-164">Cardinality Estimation (CE) improvements</span></span>
<span data-ttu-id="9c2b0-165">Introduzida com o SQL Server 2014, qualquer base de dados com um nível de compatibilidade 120 ou acima fará com que utilize das novas funcionalidades de estimativa de cardinalidade Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-165">Introduced with SQL Server 2014, any database running at a compatibility level 120 or above will make use of hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="9c2b0-166">Essencialmente, estimativa de cardinalidade é lógica Olá utilizado toodetermine como o SQL server irá executar uma consulta com base na respetivo custo estimado.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-166">Essentially, cardinality estimation is hello logic used toodetermine how SQL server will execute a query based on its estimated cost.</span></span> <span data-ttu-id="9c2b0-167">estimativa de Olá é calculada utilizando a entrada de estatísticas associadas a objetos envolvidos nessa consulta.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-167">hello estimation is calculated using input from statistics associated with objects involved in that query.</span></span> <span data-ttu-id="9c2b0-168">Praticamente, um nível elevado, as funções de estimativa de cardinalidade são estimativas de contagem de linha, juntamente com informações sobre a distribuição de Olá dos valores de Olá, contagens de valor distintos, e contagens duplicadas contidas no Olá tabelas e os objetos referenciados na consulta de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-168">Practically, at a high-level, Cardinality Estimation functions are row count estimates along with information about hello distribution of hello values, distinct value counts, and duplicate counts contained in hello tables and objects referenced in hello query.</span></span> <span data-ttu-id="9c2b0-169">Obter estas estimativas incorreto, pode levar a e/s de disco de toounnecessary devido tooinsufficient concede de memória (ou seja, TempDB spills) ou tooa seleção de uma execução de série de plano através de um paralelo planear execução, tooname algumas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-169">Getting these estimates wrong, can lead toounnecessary disk I/O due tooinsufficient memory grants (i.e. TempDB spills), or tooa selection of a serial plan execution over a parallel plan execution, tooname a few.</span></span> <span data-ttu-id="9c2b0-170">Conclusão, estimativas incorretas podem levar tooan degradação do desempenho global de execução da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-170">Conclusion, incorrect estimates can lead tooan overall performance degradation of hello query execution.</span></span> <span data-ttu-id="9c2b0-171">No Olá outro lado, melhor calcula, estimativas mais exatas, execuções de consulta de toobetter de clientes potenciais clientes potenciais!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-171">On hello other side, better estimates, more accurate estimates, leads toobetter query executions!</span></span>

<span data-ttu-id="9c2b0-172">Tal como mencionado anteriormente, otimizações de consulta e calcula é um fim complexa, mas se pretender toolearn mais sobre os planos de consulta e o avaliador de cardinalidade herdado, pode consultar toohello documento no [otimizar o seu planos de consulta com Olá SQL Server 2014 Avaliador de cardinalidade herdado](https://msdn.microsoft.com/library/dn673537.aspx) para uma descrição mais aprofundada.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-172">As mentioned before, query optimizations and estimates are a complex matter, but if you want toolearn more about query plans and cardinality estimator, you can refer toohello document at [Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator](https://msdn.microsoft.com/library/dn673537.aspx) for a deeper dive.</span></span>

## <a name="which-cardinality-estimation-do-you-currently-use"></a><span data-ttu-id="9c2b0-173">Que estimativa de cardinalidade atualmente utiliza?</span><span class="sxs-lookup"><span data-stu-id="9c2b0-173">Which Cardinality Estimation do you currently use?</span></span>
<span data-ttu-id="9c2b0-174">toodetermine em que estimativa de cardinalidade as suas consultas estão em execução, vamos apenas utilizar consulta de Olá exemplos abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-174">toodetermine under which Cardinality Estimation your queries are running, let’s just use hello query samples below.</span></span> <span data-ttu-id="9c2b0-175">Tenha em atenção que este primeiro exemplo serão executados com nível de compatibilidade 110, implying utilize Olá de funções de estimativa de cardinalidade antigas Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-175">Note that this first example will run under compatibility level 110, implying hello use of hello old Cardinality Estimation functions.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 110;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-176">Após a conclusão da execução, clique na ligação XML Olá e observe Olá as propriedades da iterator primeiro Olá, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-176">Once execution is complete, click on hello XML link, and look at hello properties of hello first iterator as shown below.</span></span> <span data-ttu-id="9c2b0-177">Tenha em atenção o nome da propriedade Olá chamado CardinalityEstimationModelVersion atualmente definido na 70.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-177">Note hello property name called CardinalityEstimationModelVersion currently set on 70.</span></span> <span data-ttu-id="9c2b0-178">Não significa que o nível de compatibilidade de base de dados de Olá está definido a versão do SQL Server 7.0 toohello (está definido no 110 como visíveis nas instruções de TSQL Olá acima), mas o valor de Olá 70 simplesmente representa Olá legada estimativa de cardinalidade funcionalidade disponível desde o SQL Server Servidor 7.0, que não tinha nenhum revisões principais até que o SQL Server 2014 (vem com um nível de compatibilidade de 120).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-178">It does not mean that hello database compatibility level is set toohello SQL Server 7.0 version (it is set on 110 as visible in hello TSQL statements above), but hello value 70 simply represents hello legacy Cardinality Estimation functionality available since SQL Server 7.0, which had no major revisions until SQL Server 2014 (which comes with a compatibility level of 120).</span></span>

<span data-ttu-id="9c2b0-179">*Figura 4: Olá CardinalityEstimationModelVersion é definir too70 quando um nível de compatibilidade 110 ou abaixo.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-179">*Figure 4: hello CardinalityEstimationModelVersion is set too70 when using a compatibility level of 110 or below.*</span></span>

![Figura 4](./media/sql-database-compatibility-level-query-performance-130/figure-4.png)

<span data-ttu-id="9c2b0-181">Em alternativa, pode alterar too130 de nível de compatibilidade de Olá e desativar a utilização de Olá da nova função de estimativa de cardinalidade Olá utilizando Olá LEGACY_CARDINALITY_ESTIMATION definir tooON com [ALTER configuração base de dados no âmbito](https://msdn.microsoft.com/library/mt629158.aspx).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-181">Alternatively, you can change hello compatibility level too130, and disable hello use of hello new Cardinality Estimation function by using hello LEGACY_CARDINALITY_ESTIMATION set tooON with [ALTER DATABASE SCOPED CONFIGURATION](https://msdn.microsoft.com/library/mt629158.aspx).</span></span> <span data-ttu-id="9c2b0-182">Isto irá ser exatamente Olá igual ao utilizar 110 uma estimativa de cardinalidade função ponto de vista de durante a utilização de consulta mais recente Olá processar o nível de compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-182">This will be exactly hello same as using 110 from a Cardinality Estimation function point of view, while using hello latest query processing compatibility level.</span></span> <span data-ttu-id="9c2b0-183">Ao fazê-lo, pode beneficiar da nova consulta de Olá processamento funcionalidades futuras com um nível de compatibilidade mais recente do hello (ou seja, modo de lote), mas ainda dependem da funcionalidade de estimativa de cardinalidade antiga Olá se necessário.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-183">Doing so, you can benefit from hello new query processing features coming with hello latest compatibility level (i.e. batch mode), but still rely on hello old Cardinality Estimation functionality if necessary.</span></span>

```
-- Old CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-184">Mover apenas o nível de compatibilidade de toohello 120 ou 130 ativa a funcionalidade de estimativa de cardinalidade novo Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-184">Simply moving toohello compatibility level 120 or 130 enables hello new Cardinality Estimation functionality.</span></span> <span data-ttu-id="9c2b0-185">Nesse caso, a predefinição de Olá CardinalityEstimationModelVersion será definida em conformidade too120 ou 130 visível como abaixo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-185">In such a case, hello default CardinalityEstimationModelVersion will be set accordingly too120 or 130 as visible below.</span></span>

```
-- New CE

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT [c1]
    FROM [dbo].[T_target]
    WHERE [c1] > 20000;
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-186">*Figura 5: Olá CardinalityEstimationModelVersion é definir too130 quando um nível de compatibilidade de 130.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-186">*Figure 5: hello CardinalityEstimationModelVersion is set too130 when using a compatibility level of 130.*</span></span>

![figura 5](./media/sql-database-compatibility-level-query-performance-130/figure-5.jpg)

## <a name="witnessing-hello-cardinality-estimation-differences"></a><span data-ttu-id="9c2b0-188">Diferenças de estimativa de cardinalidade Olá witnessing</span><span class="sxs-lookup"><span data-stu-id="9c2b0-188">Witnessing hello Cardinality Estimation differences</span></span>
<span data-ttu-id="9c2b0-189">Agora, vamos executar ligeiramente mais complexo que envolvem um INNER JOIN com uma cláusula WHERE com algumas predicados de consulta e vamos ver estimativa de contagem de linhas Olá da função de estimativa de cardinalidade antiga Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-189">Now, let’s run a slightly more complex query involving an INNER JOIN with a WHERE clause with some predicates, and let’s look at hello row count estimate from hello old Cardinality Estimation function first.</span></span>

```
-- Old CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = ON;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-190">Executar esta consulta eficazmente devolve 200,704 linhas, enquanto Olá estimativa de linha com a funcionalidade de estimativa de cardinalidade antiga Olá afirmações 194,284 linhas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-190">Executing this query effectively returns 200,704 rows, while hello row estimate with hello old Cardinality Estimation functionality claims 194,284 rows.</span></span> <span data-ttu-id="9c2b0-191">Obviamente, como consiga aceder tal antes, esses resultados de contagem de linhas também dependerá frequência executou Olá exemplos anteriores, que preenche as tabelas de exemplo de Olá repetidas em cada execução.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-191">Obviously, as said before, these row count results will also depend how often you ran hello previous samples, which populates hello sample tables over and over again at each run.</span></span> <span data-ttu-id="9c2b0-192">Obviamente, predicados Olá na sua consulta também irão ter uma influência no estimativa real de Olá além de forma de tabela Olá, conteúdo de dados e como estes dados, na verdade, correlacionar entre si.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-192">Obviously, hello predicates in your query will also have an influence on hello actual estimation aside from hello table shape, data content, and how this data actually correlate with each other.</span></span>

<span data-ttu-id="9c2b0-193">*Figura 6: estimativa de contagem de linhas Olá está 194,284 ou 6.000 linhas desativada de Olá 200,704 as linhas esperadas.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-193">*Figure 6: hello row count estimate is 194,284 or 6,000 rows off from hello 200,704 rows expected.*</span></span>

![figura 6](./media/sql-database-compatibility-level-query-performance-130/figure-6.jpg)

<span data-ttu-id="9c2b0-195">No Olá mesma forma, vamos executar agora Olá mesmo consultar com a nova funcionalidade de estimativa de cardinalidade Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-195">In hello same way, let’s now execute hello same query with hello new Cardinality Estimation functionality.</span></span>

```
-- New CE row estimate with INNER JOIN and WHERE clause

ALTER DATABASE MyTestDB
    SET COMPATIBILITY_LEVEL = 130;
GO

ALTER DATABASE
    SCOPED CONFIGURATION
    SET LEGACY_CARDINALITY_ESTIMATION = OFF;
GO

SET STATISTICS XML ON;

SELECT T.[c2]
    FROM
                   [dbo].[T_source] S
        INNER JOIN [dbo].[T_target] T  ON T.c1=S.c1
    WHERE
        S.[Color] = ‘Red’  AND
        S.[c2] > 2000  AND
        T.[c2] > 2000
    OPTION (RECOMPILE);
GO

SET STATISTICS XML OFF;
```


<span data-ttu-id="9c2b0-196">Observar Olá abaixo, agora, Vemos que estimativa de linha de Olá é 202,877, ou muito próximo e superior ao hello estimativa de cardinalidade antigo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-196">Looking at hello below, we now see that hello row estimate is 202,877, or much closer and higher than hello old Cardinality Estimation.</span></span>

<span data-ttu-id="9c2b0-197">*A figura 7: estimativa de contagem de linhas Olá está agora 202,877, em vez de 194,284.*</span><span class="sxs-lookup"><span data-stu-id="9c2b0-197">*Figure 7: hello row count estimate is now 202,877, instead of 194,284.*</span></span>

![figura 7](./media/sql-database-compatibility-level-query-performance-130/figure-7.jpg)

<span data-ttu-id="9c2b0-199">Na realidade, o conjunto de resultados de Olá é 200,704 linhas (mas todos depende da frequência executou consultas Olá de Olá exemplos anteriores, mas mais importante ainda, porque Olá TSQL utiliza a instrução de RAND() Olá, Olá real os valores devolvidos podem diferir dos de um toohello execução seguinte).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-199">In reality, hello result set is 200,704 rows (but all of it depends how often you did run hello queries of hello previous samples, but more importantly, because hello TSQL uses hello RAND() statement, hello actual values returned can vary from one run toohello next).</span></span> <span data-ttu-id="9c2b0-200">Por conseguinte, neste exemplo específico, hello nova estimativa de cardinalidade efetua uma melhor tarefa ao fazer uma estimativa do número de Olá de linhas porque 202,877 é muito próximo too200, 704, que 194,284!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-200">Therefore, in this particular example, hello new Cardinality Estimation does a better job at estimating hello number of rows because 202,877 is much closer too200,704, than 194,284!</span></span> <span data-ttu-id="9c2b0-201">Último, se alterar Olá cláusula WHERE predicados tooequality (vez ">" para a instância), isto foi possível efetuar a Olá calcula entre Olá antiga e nova função de cardinalidade ainda mais diferentes, consoante o número de correspondências pode obter.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-201">Last, if you change hello WHERE clause predicates tooequality (rather than “>” for instance), this could make hello estimates between hello old and new Cardinality function even more different, depending on how many matches you can get.</span></span>

<span data-ttu-id="9c2b0-202">Obviamente, neste caso, que está a ser ~ 6000 linhas fora da contagem real não representa uma grande quantidade de dados em algumas situações.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-202">Obviously, in this case, being ~6000 rows off from actual count does not represent a lot of data in some situations.</span></span> <span data-ttu-id="9c2b0-203">Agora, transpor esta toomillions de linhas em várias tabelas e consultas mais complexas, e a estimativa de Olá por vezes pode estar desligada por milhões de linhas, Olá por conseguinte, o risco de segurança diretriz Olá errado plano de execução, ou quando solicitar memória insuficiente concede à esquerda tooTempDB spills e e/s mais por isso, são muito superior.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-203">Now, transpose this toomillions of rows across several tables and more complex queries, and at times hello estimate can be off by millions of rows , and therefore, hello risk of picking-up hello wrong execution plan, or requesting insufficient memory grants leading tooTempDB spills, and so more I/O, are much higher.</span></span>

<span data-ttu-id="9c2b0-204">Se tiver oportunidade de Olá, restaure esta comparação com as suas consultas mais comuns e conjuntos de dados e ver para si por quanto alguns estimativas de Olá antiga e nova são afetados, embora alguns pode ficar mais off na realidade Olá ou alguns outros apenas apenas simplesmente Quanto mais próximo linha real de toohello conta, na verdade, é devolvido em conjuntos de resultados de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-204">If you have hello opportunity, practice this comparison with your most typical queries and datasets, and see for yourself by how much some of hello old and new estimates are affected, while some could just become more off from hello reality, or some others just simply closer toohello actual row counts actually returned in hello result sets.</span></span> <span data-ttu-id="9c2b0-205">Todos dependerá da forma de Olá da sua consultas, características de base de dados SQL do Azure de Olá, natureza Olá e tamanho de Olá dos seus conjuntos de dados e estatísticas de Olá disponíveis sobre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-205">All of it will depend of hello shape of your queries, hello Azure SQL database characteristics, hello nature and hello size of your datasets, and hello statistics available about them.</span></span> <span data-ttu-id="9c2b0-206">Se acabou de criar a instância de SQL Database do Azure, Olá consulta otimizador será toobuild o conhecimento do zero em vez de estatísticas de reutilizar compostas consulta anterior Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-206">If you just created your Azure SQL Database instance, hello query optimizer will have toobuild its knowledge from scratch instead of reusing statistics made of hello previous query runs.</span></span> <span data-ttu-id="9c2b0-207">Por isso, Olá estimativas são situação de servidor e aplicação tooevery muito contextuais e quase específico.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-207">So, hello estimates are very contextual and almost specific tooevery server and application situation.</span></span> <span data-ttu-id="9c2b0-208">É tookeep um aspeto importante lembrar!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-208">It is an important aspect tookeep in mind!</span></span>

## <a name="some-considerations-tootake-into-account"></a><span data-ttu-id="9c2b0-209">Tootake algumas considerações para a conta</span><span class="sxs-lookup"><span data-stu-id="9c2b0-209">Some considerations tootake into account</span></span>
<span data-ttu-id="9c2b0-210">Embora a maioria das cargas de trabalho seriam beneficiar do nível de compatibilidade de Olá 130, antes de adotar o nível de compatibilidade de Olá para o seu ambiente de produção, basicamente tem 3 opções:</span><span class="sxs-lookup"><span data-stu-id="9c2b0-210">Although most workloads would benefit from hello compatibility level 130, before you adopting hello compatibility level for your production environment, you basically have 3 options:</span></span>

1. <span data-ttu-id="9c2b0-211">Mover o nível de toocompatibility 130 e ver como efetuar ações.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-211">You move toocompatibility level 130, and see how things perform.</span></span> <span data-ttu-id="9c2b0-212">Caso tenha em atenção algumas regressões ', apenas simplesmente definir Olá compatibilidade nível tooits back-nível original, ou manter 130 e apenas inverso modo Legado do Olá estimativa de cardinalidade back toohello (tal como explicado anteriormente, isto sozinho foi resolver Olá problema).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-212">In case you notice some regressions, you just simply set hello compatibility level back tooits original level, or keep 130, and only reverse hello Cardinality Estimation back toohello legacy mode (As explained above, this alone could address hello issue).</span></span>
2. <span data-ttu-id="9c2b0-213">Testar cuidadosamente as suas aplicações existentes em carga semelhante de produção, ajustar e validar desempenho Olá antes tooproduction contínuo.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-213">You thoroughly test your existing applications under similar production load, fine tune, and validate hello performance before going tooproduction.</span></span> <span data-ttu-id="9c2b0-214">Em caso de problemas, mesmo que acima, pode sempre voltar atrás toohello original nível de compatibilidade, ou simplesmente inverso modo Legado do Olá estimativa de cardinalidade toohello back.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-214">In case of issues, same as above, you can always go back toohello original compatibility level, or simply reverse hello Cardinality Estimation back toohello legacy mode.</span></span>
3. <span data-ttu-id="9c2b0-215">Como uma opção final e Olá tooaddress de forma mais recente estas questões, é o arquivo de consultas de Olá tooleverage.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-215">As a final option, and hello most recent way tooaddress these questions, is tooleverage hello Query Store.</span></span> <span data-ttu-id="9c2b0-216">Que é a opção recomendada de hoje!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-216">That’s today’s recommended option!</span></span> <span data-ttu-id="9c2b0-217">análise de Olá tooassist das suas consultas em compatibilidade nível 120 ou abaixo versus 130, não é possível Aconselhamo-lo suficiente toouse arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-217">tooassist hello analysis of your queries under compatibility level 120 or below versus 130, we cannot encourage you enough toouse Query Store.</span></span> <span data-ttu-id="9c2b0-218">O arquivo de consultas está disponível com a versão mais recente do Olá do Azure SQL Database V12 e foi concebido toohelp, com a resolução de problemas de desempenho de consulta.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-218">Query Store is available with hello latest version of Azure SQL Database V12, and it’s designed toohelp you with query performance troubleshooting.</span></span> <span data-ttu-id="9c2b0-219">Considere Olá arquivo de consultas como um gravador de dados para a base de dados a recolher e apresentar informações detalhadas de históricos sobre todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-219">Think of hello Query Store as a flight data recorder for your database collecting and presenting detailed historic information about all queries.</span></span> <span data-ttu-id="9c2b0-220">Isto significativamente simplifica forenses de desempenho ao reduzir Olá tempo toodiagnose e resolver problemas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-220">This greatly simplifies performance forensics by reducing hello time toodiagnose and resolve issues.</span></span> <span data-ttu-id="9c2b0-221">Pode encontrar mais informações em [arquivo de consultas: um gravador de dados para a base de dados](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-221">You can find more information at [Query Store: A flight data recorder for your database](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/).</span></span>

<span data-ttu-id="9c2b0-222">Num alto nível, se já tiver um conjunto de bases de dados com o nível de compatibilidade 120 ou abaixo e planear toomove Olá algumas delas too130, ou porque a carga de trabalho aprovisionar automaticamente novas bases de dados que serão em breve definido por predefinição too130, considere. seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="9c2b0-222">At hello high-level, if you already have a set of databases running at compatibility level 120 or below, and plan toomove some of them too130, or because your workload automatically provision new databases that will be soon be set by default too130, please consider hello followings:</span></span>

* <span data-ttu-id="9c2b0-223">Antes de alterar toohello novo nível de compatibilidade de produção, ative o arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-223">Before changing toohello new compatibility level in production, enable Query Store.</span></span> <span data-ttu-id="9c2b0-224">Pode consultar demasiado[alterar Olá modo de compatibilidade de base de dados e a utilização Olá arquivo de consultas](https://msdn.microsoft.com/library/bb895281.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-224">You can refer too[Change hello Database Compatibility Mode and Use hello Query Store](https://msdn.microsoft.com/library/bb895281.aspx) for more information.</span></span>
* <span data-ttu-id="9c2b0-225">Em seguida, teste críticas todas as cargas de trabalho com dados representativos e consultas de um ambiente de produção como e o desempenho de Olá comparar teve e conforme comunicado pelo arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-225">Next, test all critical workloads using representative data and queries of a production-like environment, and compare hello performance experienced and as reported by Query Store.</span></span> <span data-ttu-id="9c2b0-226">Se ocorrer algum regressões, pode identificar Olá regressed consultas com Olá arquivo de consultas e utilizar o plano de Olá forçar do arquivo de consultas opção (também conhecido como planear a afixação).</span><span class="sxs-lookup"><span data-stu-id="9c2b0-226">If you experience some regressions, you can identify hello regressed queries with hello Query Store and use hello plan forcing option from Query Store (aka plan pinning).</span></span> <span data-ttu-id="9c2b0-227">Nesse caso, pode definitively permaneça com um nível de compatibilidade de Olá 130 e utiliza o plano de consulta anteriores Olá como sugerido pelo Olá arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-227">In such a case, you definitively stay with hello compatibility level 130, and use hello former query plan as suggested by hello Query Store.</span></span>
* <span data-ttu-id="9c2b0-228">Se pretender tooleverage novas funcionalidades e capacidades da base de dados do SQL do Azure (que está a executar o SQL Server 2016), mas são sensíveis toochanges pelo nível de compatibilidade de Olá 130, como último recurso, pode considerar forçar o nível de compatibilidade de Olá novamente nível de toohello que se adapta às sua carga de trabalho, utilizando uma instrução ALTER DATABASE.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-228">If you want tooleverage new features and capabilities of Azure SQL Database (which is running SQL Server 2016), but are sensitive toochanges brought by hello compatibility level 130, as a last resort, you could consider forcing hello compatibility level back toohello level that suits your workload by using an ALTER DATABASE statement.</span></span> <span data-ttu-id="9c2b0-229">Mas, em primeiro lugar, tenha em atenção que plano do arquivo de consultas de Olá afixação opção é a melhor opção porque não utilizar 130 é basicamente permanecendo no nível de funcionalidade Olá de uma versão mais antiga do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-229">But first, be aware that hello Query Store plan pinning option is your best option because not using 130 is basically staying at hello functionality level of an older SQL Server version.</span></span>
* <span data-ttu-id="9c2b0-230">Se tiver aplicações multi-inquilino expansão várias bases de dados, poderá ser Olá tooupdate necessário aprovisionar lógica do seu tooensure bases de dados de um nível de compatibilidade consistente em todas as bases de dados; aqueles antigos e recentemente aprovisionadas.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-230">If you have multitenant applications spanning multiple databases, it may be necessary tooupdate hello provisioning logic of your databases tooensure a consistent compatibility level across all databases; old and newly provisioned ones.</span></span> <span data-ttu-id="9c2b0-231">O desempenho da carga de trabalho de aplicação pode ser facto toohello confidenciais que algumas bases de dados estão em execução em níveis de compatibilidade diferentes e, por conseguinte, a consistência de nível de compatibilidade em qualquer base de dados pode ser necessária na ordem tooprovide Olá mesmo experiência tooyour clientes tudo em quadro Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-231">Your application workload performance could be sensitive toohello fact that some databases are running at different compatibility levels, and therefore, compatibility level consistency across any database could be required in order tooprovide hello same experience tooyour customers all across hello board.</span></span> <span data-ttu-id="9c2b0-232">Tenha em atenção que não é um mandato, realmente depende de como a aplicação é afetada por nível de compatibilidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-232">Note that it is not a mandate, it really depends on how your application is affected by hello compatibility level.</span></span>
* <span data-ttu-id="9c2b0-233">Última, sobre Olá estimativa de cardinalidade e tal como alterar o nível de compatibilidade de Olá, antes de continuar na produção, é recomendado tootest a carga de trabalho de produção em Olá novo condições toodetermine se a aplicação é vantajosa do melhoramentos de estimativa de cardinalidade Olá.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-233">Last, regarding hello Cardinality Estimation, and just like changing hello compatibility level, before proceeding in production, it is recommended tootest your production workload under hello new conditions toodetermine if your application benefits from hello Cardinality Estimation improvements.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9c2b0-234">Conclusão</span><span class="sxs-lookup"><span data-stu-id="9c2b0-234">Conclusion</span></span>
<span data-ttu-id="9c2b0-235">Utilizar a SQL Database do Azure toobenefit de todos os melhoramentos do SQL Server 2016 claramente melhorar as execuções de consulta.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-235">Using Azure SQL Database toobenefit from all SQL Server 2016 enhancements can clearly improve your query executions.</span></span> <span data-ttu-id="9c2b0-236">Tal como-é!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-236">Just as-is!</span></span> <span data-ttu-id="9c2b0-237">Obviamente, tal como qualquer nova funcionalidade, uma avaliação adequada tem de ser efetuada toodetermine Olá exato as condições sob as quais a carga de trabalho de base de dados funciona Olá melhor.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-237">Of course, like any new feature, a proper evaluation must be done toodetermine hello exact conditions under which your database workload operates hello best.</span></span> <span data-ttu-id="9c2b0-238">Experiência mostra que a maioria das cargas de trabalho são tooat esperado pelo menos, executado transparente com nível de compatibilidade 130, tirando partido de nova consulta de processamento funções e nova estimativa de cardinalidade.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-238">Experience shows that most workload are expected tooat least run transparently under compatibility level 130, while leveraging new query processing functions, and new Cardinality Estimation.</span></span> <span data-ttu-id="9c2b0-239">Que consiga aceder tal, verdade, existem sempre algumas exceções e fazer atraso adequado diligence toodetermine uma avaliação importante quanto pode beneficiar estes melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-239">That said, realistically, there are always some exceptions and doing proper due diligence is an important assessment toodetermine how much you can benefit from these enhancements.</span></span> <span data-ttu-id="9c2b0-240">E novamente, o arquivo de consultas Olá pode ser uma ajuda excelente fazer este trabalho!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-240">And again, hello Query Store can be of a great help in doing this work!</span></span>

<span data-ttu-id="9c2b0-241">À medida que o SQL Azure evolui, que pode esperar um nível de compatibilidade 140 no Olá futuras.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-241">As SQL Azure evolves, you can expect a compatibility level 140 in hello future.</span></span> <span data-ttu-id="9c2b0-242">Quando a hora é adequada, iremos será iniciado se fala sobre o que será apresentada neste nível de compatibilidade futuros 140, tal como brevemente discutimos aqui o nível de compatibilidade 130 é colocar hoje.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-242">When time is appropriate, we will start talking about what this future compatibility level 140 will bring, just as we briefly discussed here what compatibility level 130 is bringing today.</span></span>

<span data-ttu-id="9c2b0-243">Por agora, vamos não se esqueça, a partir de Junho de 2016, SQL Database do Azure deixará nível de compatibilidade do Olá predefinição de 120 too130 para bases de dados recentemente criados.</span><span class="sxs-lookup"><span data-stu-id="9c2b0-243">For now, let’s not forget, starting June 2016, Azure SQL Database will change hello default compatibility level from 120 too130 for newly created databases.</span></span> <span data-ttu-id="9c2b0-244">Tenha em atenção!</span><span class="sxs-lookup"><span data-stu-id="9c2b0-244">Be aware!</span></span>

## <a name="references"></a><span data-ttu-id="9c2b0-245">Referências</span><span class="sxs-lookup"><span data-stu-id="9c2b0-245">References</span></span>
* [<span data-ttu-id="9c2b0-246">Novidades no motor de base de dados</span><span class="sxs-lookup"><span data-stu-id="9c2b0-246">What’s New in Database Engine</span></span>](https://msdn.microsoft.com/library/bb510411.aspx#InMemory)
* [<span data-ttu-id="9c2b0-247">Blogue: O arquivo de consultas: um gravador de dados para a base de dados, por Borko Novakovic, 8 de Junho de 2016</span><span class="sxs-lookup"><span data-stu-id="9c2b0-247">Blog: Query Store: A flight data recorder for your database, by Borko Novakovic, June 8 2016</span></span>](https://azure.microsoft.com/blog/query-store-a-flight-data-recorder-for-your-database/)
* [<span data-ttu-id="9c2b0-248">Nível de compatibilidade de base de dados ALTER (Transact-SQL)</span><span class="sxs-lookup"><span data-stu-id="9c2b0-248">ALTER DATABASE Compatibility Level (Transact-SQL)</span></span>](https://msdn.microsoft.com/library/bb510680.aspx)
* [<span data-ttu-id="9c2b0-249">ALTERAR A CONFIGURAÇÃO DE ÂMBITO DE BASE DE DADOS</span><span class="sxs-lookup"><span data-stu-id="9c2b0-249">ALTER DATABASE SCOPED CONFIGURATION</span></span>](https://msdn.microsoft.com/library/mt629158.aspx)
* [<span data-ttu-id="9c2b0-250">Nível de compatibilidade 130 para V12 de base de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="9c2b0-250">Compatibility Level 130 for Azure SQL Database V12</span></span>](https://azure.microsoft.com/updates/compatibility-level-130-for-azure-sql-database-v12/)
* [<span data-ttu-id="9c2b0-251">Otimizar o seu planos de consulta com Olá avaliador de SQL Server 2014 cardinalidade herdado</span><span class="sxs-lookup"><span data-stu-id="9c2b0-251">Optimizing Your Query Plans with hello SQL Server 2014 Cardinality Estimator</span></span>](https://msdn.microsoft.com/library/dn673537.aspx)
* [<span data-ttu-id="9c2b0-252">Guia de índices Columnstore</span><span class="sxs-lookup"><span data-stu-id="9c2b0-252">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
* [<span data-ttu-id="9c2b0-253">Blogue: Melhor desempenho das consultas com um nível de compatibilidade 130 na base de dados SQL do Azure, por Alain Lissoir, 6 de Maio de 2016</span><span class="sxs-lookup"><span data-stu-id="9c2b0-253">Blog: Improved Query Performance with Compatibility Level 130 in Azure SQL Database, by Alain Lissoir, May 6 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/)

<!--
Improved Query Performance with Compatibility Level 130 in Azure SQL Database

May 6, 2016 by Alain Lissoir (AlainL), on GitHub 'alainlissoir'.

https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/05/06/improved-query-performance-with-compatibility-level-130-in-azure-sql-database/

..... Now, above.
....................
..... Soon, below?

CAPS / MSDN ideally, but instead on ACom:
.. # Assess effects of latest compatibility level on query performance, how to

sql-database-compatibility-level-query-performance-130.md

genemi = MightyPen , 2016-05-20  Friday  17:00pm
-->
