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
# <a name="managing-statistics-on-tables-in-sql-data-warehouse"></a><span data-ttu-id="ba43a-103">Gerir as estatísticas em tabelas no armazém de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="ba43a-103">Managing statistics on tables in SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * <span data-ttu-id="ba43a-104">[Descrição geral][Overview]</span><span class="sxs-lookup"><span data-stu-id="ba43a-104">[Overview][Overview]</span></span>
> * <span data-ttu-id="ba43a-105">[Tipos de dados][Data Types]</span><span class="sxs-lookup"><span data-stu-id="ba43a-105">[Data Types][Data Types]</span></span>
> * <span data-ttu-id="ba43a-106">[Distribuir][Distribute]</span><span class="sxs-lookup"><span data-stu-id="ba43a-106">[Distribute][Distribute]</span></span>
> * <span data-ttu-id="ba43a-107">[Índice][Index]</span><span class="sxs-lookup"><span data-stu-id="ba43a-107">[Index][Index]</span></span>
> * <span data-ttu-id="ba43a-108">[Partição][Partition]</span><span class="sxs-lookup"><span data-stu-id="ba43a-108">[Partition][Partition]</span></span>
> * <span data-ttu-id="ba43a-109">[Estatísticas][Statistics]</span><span class="sxs-lookup"><span data-stu-id="ba43a-109">[Statistics][Statistics]</span></span>
> * <span data-ttu-id="ba43a-110">[Temporário][Temporary]</span><span class="sxs-lookup"><span data-stu-id="ba43a-110">[Temporary][Temporary]</span></span>
> 
> 

<span data-ttu-id="ba43a-111">Hello mais SQL Data Warehouse conhece os dados, hello mais rapidamente do pode executar consultas nos dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-111">hello more SQL Data Warehouse knows about your data, hello faster it can execute queries against your data.</span></span>  <span data-ttu-id="ba43a-112">forma Olá que dizem ao SQL Data Warehouse sobre os dados, é através da recolha de estatísticas sobre os dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-112">hello way that you tell SQL Data Warehouse about your data, is by collecting statistics about your data.</span></span>  <span data-ttu-id="ba43a-113">Ter estatísticas nos seus dados é um dos aspetos mais importantes Olá, pode fazê-lo toooptimize as suas consultas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-113">Having statistics on your data is one of hello most important things you can do toooptimize your queries.</span></span>  <span data-ttu-id="ba43a-114">Estatísticas de ajudam a criar Olá plano ideal para consultas do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ba43a-114">Statistics help SQL Data Warehouse create hello most optimal plan for your queries.</span></span>  <span data-ttu-id="ba43a-115">Isto acontece porque a consulta de SQL Data Warehouse Olá otimizador é um custo com otimizador de base.</span><span class="sxs-lookup"><span data-stu-id="ba43a-115">This is because hello SQL Data Warehouse query optimizer is a cost based optimizer.</span></span>  <span data-ttu-id="ba43a-116">Ou seja, compara o custo de Olá de vários planos de consulta e, em seguida, escolhe Olá plano com Olá menor custo, que também deve ser o plano de Olá que irão executar Olá mais rápido.</span><span class="sxs-lookup"><span data-stu-id="ba43a-116">That is, it compares hello cost of various query plans and then chooses hello plan with hello lowest cost, which should also be hello plan that will execute hello fastest.</span></span>

<span data-ttu-id="ba43a-117">Podem ser criadas estatísticas no única coluna, várias colunas ou um índice de uma tabela.</span><span class="sxs-lookup"><span data-stu-id="ba43a-117">Statistics can be created on a single column, multiple columns or on an index of a table.</span></span>  <span data-ttu-id="ba43a-118">As estatísticas são armazenadas num histograma que captura intervalo Olá e selectivity dos valores.</span><span class="sxs-lookup"><span data-stu-id="ba43a-118">Statistics are stored in a histogram which captures hello range and selectivity of values.</span></span>  <span data-ttu-id="ba43a-119">Esta é a do especial interesse dos quando precisa de otimizador de Olá tooevaluate associações, GROUP BY, HAVING e cláusulas WHERE numa consulta.</span><span class="sxs-lookup"><span data-stu-id="ba43a-119">This is of particular interest when hello optimizer needs tooevaluate JOINs, GROUP BY, HAVING and WHERE clauses in a query.</span></span>  <span data-ttu-id="ba43a-120">Por exemplo, se o otimizador de Olá calcula que data Olá são filtragem na sua consulta devolverá 1 linha, pode escolher a muito diferentes planear que o se se estimativas que data selecionou irá devolver 1 milhões de linhas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-120">For example, if hello optimizer estimates that hello date you are filtering in your query will return 1 row, it may choose a very different plan than if it estimates that they date you have selected will return 1 million rows.</span></span>  <span data-ttu-id="ba43a-121">Enquanto é extremamente importante criar estatísticas, é igualmente importante que estatísticas *com precisão* refletir Olá estado atual da tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-121">While creating statistics is extremely important, it is equally important that statistics *accurately* reflect hello current state of hello table.</span></span>  <span data-ttu-id="ba43a-122">Ter estatísticas atualizadas garante que um bom plano está selecionado por otimizador de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-122">Having up-to-date statistics ensures that a good plan is selected by hello optimizer.</span></span>  <span data-ttu-id="ba43a-123">os planos de Olá criados por otimizador de Olá só estão como boas como estatísticas de Olá nos seus dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-123">hello plans created by hello optimizer are only as good as hello statistics on your data.</span></span>

<span data-ttu-id="ba43a-124">Olá o processo de criação e a atualizar as estatísticas é atualmente um processo manual, mas é toodo muito simple.</span><span class="sxs-lookup"><span data-stu-id="ba43a-124">hello process of creating and updating statistics is currently a manual process, but is very simple toodo.</span></span>  <span data-ttu-id="ba43a-125">Tal não acontecia no SQL Server, que cria e atualiza as estatísticas de índices e colunas único automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ba43a-125">This is unlike SQL Server which automatically creates and updates statistics on single columns and indexes.</span></span>  <span data-ttu-id="ba43a-126">Ao utilizar as informações de Olá abaixo, pode significativamente automatizar a gestão de Olá das estatísticas de Olá nos seus dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-126">By using hello information below, you can greatly automate hello management of hello statistics on your data.</span></span> 

## <a name="getting-started-with-statistics"></a><span data-ttu-id="ba43a-127">Introdução ao estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-127">Getting started with statistics</span></span>
 <span data-ttu-id="ba43a-128">Criar estatísticas amostras em cada coluna é uma forma fácil tooget iniciado com as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-128">Creating sampled statistics on every column is an easy way tooget started with statistics.</span></span>  <span data-ttu-id="ba43a-129">Uma vez que é igualmente importante tookeep estatísticas atualizadas, uma abordagem conservador poderá ser tooupdate as estatísticas diariamente ou após cada carga.</span><span class="sxs-lookup"><span data-stu-id="ba43a-129">Since it is equally important tookeep statistics up-to-date, a conservative approach may be tooupdate your statistics daily or after each load.</span></span> <span data-ttu-id="ba43a-130">São sempre compromissos entre o desempenho e Olá custo toocreate e atualizar as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-130">There are always trade-offs between performance and hello cost toocreate and update statistics.</span></span>  <span data-ttu-id="ba43a-131">Se encontrar estiver a demorar demasiado tempo toomaintain todas as estatísticas, poderá precisa de induzirem tootry toobe mais seletiva sobre as colunas que tem as estatísticas ou as colunas frequentes atualizar.</span><span class="sxs-lookup"><span data-stu-id="ba43a-131">If you find it is taking too long toomaintain all of your statistics, you may want tootry toobe more selective about which columns have statistics or which columns need frequent updating.</span></span>  <span data-ttu-id="ba43a-132">Por exemplo, é aconselhável colunas de data tooupdate diariamente, como podem ser adicionados novos valores em vez de após cada carga.</span><span class="sxs-lookup"><span data-stu-id="ba43a-132">For example, you might want tooupdate date columns daily, as new values may be added rather than after every load.</span></span> <span data-ttu-id="ba43a-133">Novamente, irá obter Olá benefício a maioria das, fazendo com que as estatísticas em colunas envolvidas em associações, GROUP BY, HAVING e cláusulas WHERE.</span><span class="sxs-lookup"><span data-stu-id="ba43a-133">Again, you will gain hello most benefit by having statistics on columns involved in JOINs, GROUP BY, HAVING and WHERE clauses.</span></span>  <span data-ttu-id="ba43a-134">Se tiver uma tabela com uma grande quantidade de colunas que apenas são utilizadas em Olá SELECIONAR cláusula, estatísticas destas colunas não podem ajudar e gastos um pequeno tooidentify esforço mais Olá as colunas onde irão ajudar a estatísticas, pode reduzir Olá tempo toomaintain as estatísticas .</span><span class="sxs-lookup"><span data-stu-id="ba43a-134">If you have a table with a lot of columns which are only used in hello SELECT clause, statistics on these columns may not help, and spending a little more effort tooidentify only hello columns where statistics will help, can reduce hello time toomaintain your statistics.</span></span>

## <a name="multi-column-statistics"></a><span data-ttu-id="ba43a-135">Estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="ba43a-135">Multi-column statistics</span></span>
<span data-ttu-id="ba43a-136">Além disso toocreating estatísticas em colunas único, pode considerar que as suas consultas irão beneficiar de estatísticas de várias colunas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-136">In addition toocreating statistics on single columns, you may find that your queries will benefit from multi-column statistics.</span></span>  <span data-ttu-id="ba43a-137">Estatísticas de várias colunas são criadas numa lista de colunas de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-137">Multi-column statistics are statistics created on a list of columns.</span></span>  <span data-ttu-id="ba43a-138">Incluem estatísticas de coluna única na primeira coluna de Olá na lista de Olá, mais algumas informações de correlação entre coluna chamado densities.</span><span class="sxs-lookup"><span data-stu-id="ba43a-138">They include single column statistics on hello first column in hello list, plus some cross-column correlation information called densities.</span></span>  <span data-ttu-id="ba43a-139">Por exemplo, se tiver uma tabela que associa tooanother duas colunas, pode considerar que o SQL Data Warehouse pode otimizar melhor plano Olá se compreende relação Olá entre duas colunas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-139">For example, if you have a table that joins tooanother on two columns, you may find that SQL Data Warehouse can better optimize hello plan if it understands hello relationship between two columns.</span></span>   <span data-ttu-id="ba43a-140">Estatísticas de várias colunas podem melhorar o desempenho de consulta para algumas operações, tais como associações compostas e agrupar por.</span><span class="sxs-lookup"><span data-stu-id="ba43a-140">Multi-column statistics can improve query performance for some operations such as composite joins and group by.</span></span>

## <a name="updating-statistics"></a><span data-ttu-id="ba43a-141">A atualizar as estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-141">Updating statistics</span></span>
<span data-ttu-id="ba43a-142">A atualizar as estatísticas é uma parte importante da sua rotina de gestão de base de dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-142">Updating statistics is an important part of your database management routine.</span></span>  <span data-ttu-id="ba43a-143">Quando altera a distribuição de Olá dos dados na base de dados de Olá, estatísticas tem toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="ba43a-143">When hello distribution of data in hello database changes, statistics need toobe updated.</span></span>  <span data-ttu-id="ba43a-144">Estatísticas Desatualizadas direciona o desempenho das consultas toosub ideal.</span><span class="sxs-lookup"><span data-stu-id="ba43a-144">Out-of-date statistics will lead toosub-optimal query performance.</span></span>

<span data-ttu-id="ba43a-145">Uma melhor prática é tooupdate estatísticas em colunas de data por dia datas novas são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-145">One best practice is tooupdate statistics on date columns each day as new dates are added.</span></span>  <span data-ttu-id="ba43a-146">Cada novas linhas de tempo são carregados para o armazém de dados de Olá, datas de carga novo ou datas de transação são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-146">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="ba43a-147">Estes alterar a distribuição de dados de Olá e certifique-estatísticas Olá desatualizados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-147">These change hello data distribution and make hello statistics out-of-date.</span></span> <span data-ttu-id="ba43a-148">Por outro lado, estatísticas de uma coluna de país numa tabela cliente nunca poderão ter toobe atualizado, como a distribuição de Olá de valores, geralmente, não irá alterar.</span><span class="sxs-lookup"><span data-stu-id="ba43a-148">Conversely, statistics on a country column in a customer table might never need toobe updated, as hello distribution of values doesn’t generally change.</span></span> <span data-ttu-id="ba43a-149">Partindo do princípio de distribuição de Olá é constante entre os clientes, adicionar nova variação de tabela de toohello linhas não vai distribuição de dados de Olá toochange.</span><span class="sxs-lookup"><span data-stu-id="ba43a-149">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="ba43a-150">No entanto, se o armazém de dados contém apenas um país e colocar dados de um novo país, resultando em dados a partir de vários países que está a ser armazenados, em seguida, sem dúvida terá tooupdate estatísticas na coluna de país Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-150">However, if your data warehouse only contains one country and you bring in data from a new country, resulting in data from multiple countries being stored, then you definitely need tooupdate statistics on hello country column.</span></span>

<span data-ttu-id="ba43a-151">Um dos Olá tooask de perguntas primeiro quando uma consulta de resolução de problemas, "estão estatísticas Olá atualizados?"</span><span class="sxs-lookup"><span data-stu-id="ba43a-151">One of hello first questions tooask when troubleshooting a query is, "Are hello statistics up-to-date?"</span></span>

<span data-ttu-id="ba43a-152">Esta questão não é um que pode ser respondida por antiguidade Olá dos dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-152">This question is not one that can be answered by hello age of hello data.</span></span> <span data-ttu-id="ba43a-153">Um objeto de estatísticas de toodate se pode ser muito antigo não se tiver ocorrido toohello nenhuma alteração materiais subjacente dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-153">An up toodate statistics object could be very old if there's been no material change toohello underlying data.</span></span> <span data-ttu-id="ba43a-154">Quando Olá número de linhas alterado substancialmente ou existe uma alteração na distribuição Olá de valores para uma determinada coluna materiais *, em seguida,* é as estatísticas de tooupdate de tempo.</span><span class="sxs-lookup"><span data-stu-id="ba43a-154">When hello number of rows has changed substantially or there is a material change in hello distribution of values for a given column *then* it's time tooupdate statistics.</span></span>  

<span data-ttu-id="ba43a-155">Para referência, **do SQL Server** (não o SQL Data Warehouse) atualiza automaticamente as estatísticas para estas situações:</span><span class="sxs-lookup"><span data-stu-id="ba43a-155">For reference, **SQL Server** (not SQL Data Warehouse) automatically updates statistics for these situations:</span></span>

* <span data-ttu-id="ba43a-156">Se tiver zero linhas na tabela de Olá, quando adiciona linhas, obterá uma atualização automática de estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-156">If you have zero rows in hello table, when you add rows, you’ll get an automatic update of statistics</span></span>
* <span data-ttu-id="ba43a-157">Ao Adicionar tabela tooa mais do que 500 linhas, começando com menos de 500 linhas (por exemplo, no início tiver 499 e, em seguida, adicionar 500 total de tooa de linhas de 999 linhas), obterá uma atualização automática</span><span class="sxs-lookup"><span data-stu-id="ba43a-157">When you add more than 500 rows tooa table starting with less than 500 rows (e.g. at start you have 499 and then add 500 rows tooa total of 999 rows), you’ll get an automatic update</span></span> 
* <span data-ttu-id="ba43a-158">Assim que tiver mais de 500 linhas terá tooadd 500 linhas de adicionais + 20% do tamanho de Olá da tabela de Olá antes, verá uma atualização automática no estatísticas Olá</span><span class="sxs-lookup"><span data-stu-id="ba43a-158">Once you’re over 500 rows you will have tooadd 500 additional rows + 20% of hello size of hello table before you’ll see an automatic update on hello stats</span></span>

<span data-ttu-id="ba43a-159">Uma vez que não existe nenhum toodetermine DMV se dados numa tabela de Olá tem sido alterado desde que foram atualizadas as estatísticas de tempo último Olá, saber idade Olá das suas estatísticas pode fornecer com parte da imagem de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-159">Since there is no DMV toodetermine if data within hello table has changed since hello last time statistics were updated, knowing hello age of your statistics can provide you with part of hello picture.</span></span>  <span data-ttu-id="ba43a-160">Pode utilizar Olá toodetermine Olá hora da última as estatísticas de consulta a seguir onde atualizadas em cada tabela.</span><span class="sxs-lookup"><span data-stu-id="ba43a-160">You can use hello following query toodetermine hello last time your statistics where updated on each table.</span></span>  

> [!NOTE]
> <span data-ttu-id="ba43a-161">Lembre-se de que o se houver uma alteração essenciais na distribuição Olá de valores para uma determinada coluna, que deve atualizar estatísticas independentemente Olá hora da última que foram atualizados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-161">Remember if there is a material change in hello distribution of values for a given column, you should update statistics regardless of hello last time they were updated.</span></span>  
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

<span data-ttu-id="ba43a-162">Colunas de data no armazém de dados, por exemplo, normalmente, tem de induzirem frequentes estatísticas atualizações.</span><span class="sxs-lookup"><span data-stu-id="ba43a-162">Date columns in a data warehouse, for example, usually need frequent statistics updates.</span></span> <span data-ttu-id="ba43a-163">Cada novas linhas de tempo são carregados para o armazém de dados de Olá, datas de carga novo ou datas de transação são adicionadas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-163">Each time new rows are loaded into hello data warehouse, new load dates or transaction dates are added.</span></span> <span data-ttu-id="ba43a-164">Estes alterar a distribuição de dados de Olá e certifique-estatísticas Olá desatualizados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-164">These change hello data distribution and make hello statistics out-of-date.</span></span>  <span data-ttu-id="ba43a-165">Por outro lado, estatísticas de uma coluna de sexo numa tabela com o cliente nunca poderão ter toobe atualizado.</span><span class="sxs-lookup"><span data-stu-id="ba43a-165">Conversely, statistics on a gender column on a customer table might never need toobe updated.</span></span> <span data-ttu-id="ba43a-166">Partindo do princípio de distribuição de Olá é constante entre os clientes, adicionar nova variação de tabela de toohello linhas não vai distribuição de dados de Olá toochange.</span><span class="sxs-lookup"><span data-stu-id="ba43a-166">Assuming hello distribution is constant between customers, adding new rows toohello table variation isn't going toochange hello data distribution.</span></span> <span data-ttu-id="ba43a-167">No entanto, se o armazém de dados contém apenas um sexo e um novo resultados de requisito em vários genders sem dúvida terá de estatísticas de tooupdate na coluna de sexo Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-167">However, if your data warehouse only contains one gender and a new requirement results in multiple genders then you definitely need tooupdate statistics on hello gender column.</span></span>

<span data-ttu-id="ba43a-168">Para uma explicação mais, consulte [estatísticas] [ Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba43a-168">For further explanation, see [Statistics][Statistics] on MSDN.</span></span>

## <a name="implementing-statistics-management"></a><span data-ttu-id="ba43a-169">Implementar a gestão de estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-169">Implementing statistics management</span></span>
<span data-ttu-id="ba43a-170">Muitas vezes, é uma boa ideia tooextend Olá, os dados ao carregar o processo tooensure que as estatísticas são atualizadas ao fim de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-170">It is often a good idea tooextend your data loading process tooensure that statistics are updated at hello end of hello load.</span></span> <span data-ttu-id="ba43a-171">carregamento de dados de Olá é quando tabelas com mais frequência a alterar o tamanho e/ou a respetiva distribuição dos valores.</span><span class="sxs-lookup"><span data-stu-id="ba43a-171">hello data load is when tables most frequently change their size and/or their distribution of values.</span></span> <span data-ttu-id="ba43a-172">Por conseguinte, esta é uma tooimplement local lógico alguns processos de gestão.</span><span class="sxs-lookup"><span data-stu-id="ba43a-172">Therefore, this is a logical place tooimplement some management processes.</span></span>

<span data-ttu-id="ba43a-173">Alguns princípios de orientação para são fornecidos abaixo para atualizar as estatísticas durante o processo de carregamento de Olá:</span><span class="sxs-lookup"><span data-stu-id="ba43a-173">Some guiding principles are provided below for updating your statistics during hello load process:</span></span>

* <span data-ttu-id="ba43a-174">Certifique-se de que cada tabela carregada tem, pelo menos, um objeto de estatísticas atualizado.</span><span class="sxs-lookup"><span data-stu-id="ba43a-174">Ensure that each loaded table has at least one statistics object updated.</span></span> <span data-ttu-id="ba43a-175">Este Olá atualizações tabelas informações de tamanho (contagem de linhas e contagem de páginas) como parte da atualização de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-175">This updates hello tables size (row count and page count) information as part of hello stats update.</span></span>
* <span data-ttu-id="ba43a-176">Concentre-se em colunas que participam na associação, GROUP BY, ORDER BY e DISTINCT cláusulas</span><span class="sxs-lookup"><span data-stu-id="ba43a-176">Focus on columns participating in JOIN, GROUP BY, ORDER BY and DISTINCT clauses</span></span>
* <span data-ttu-id="ba43a-177">Considere atualizar "chave ascendente" colunas como transação mais frequentemente estes valores não serão incluídos em histograma de estatísticas de Olá datas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-177">Consider updating "ascending key" columns such as transaction dates more frequently as these values will not be included in hello statistics histogram.</span></span>
* <span data-ttu-id="ba43a-178">Considere atualizar colunas de distribuição estático menos frequência.</span><span class="sxs-lookup"><span data-stu-id="ba43a-178">Consider updating static distribution columns less frequently.</span></span>
* <span data-ttu-id="ba43a-179">Lembre-se de que cada objeto de estatística é atualizado na série.</span><span class="sxs-lookup"><span data-stu-id="ba43a-179">Remember each statistic object is updated in series.</span></span> <span data-ttu-id="ba43a-180">Basta implementar `UPDATE STATISTICS <TABLE_NAME>` não pode ser o ideal - especialmente para tabelas wide com muitos objetos de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-180">Simply implementing `UPDATE STATISTICS <TABLE_NAME>` may not be ideal - especially for wide tables with lots of statistics objects.</span></span>

> [!NOTE]
> <span data-ttu-id="ba43a-181">Para obter mais detalhes sobre [chave ascendente], consulte o documento técnico do modelo de estimativa de cardinalidade do toohello SQL Server 2014.</span><span class="sxs-lookup"><span data-stu-id="ba43a-181">For more details on [ascending key] please refer toohello SQL Server 2014 cardinality estimation model whitepaper.</span></span>
> 
> 

<span data-ttu-id="ba43a-182">Para uma explicação mais, consulte [estimativa de cardinalidade] [ Cardinality Estimation] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba43a-182">For further explanation, see  [Cardinality Estimation][Cardinality Estimation] on MSDN.</span></span>

## <a name="examples-create-statistics"></a><span data-ttu-id="ba43a-183">Exemplos: Criar estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-183">Examples: Create statistics</span></span>
<span data-ttu-id="ba43a-184">Estes exemplos mostram como toouse várias opções para criar estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-184">These examples show how toouse various options for creating statistics.</span></span> <span data-ttu-id="ba43a-185">Opções de Olá que utilizar para cada coluna dependem características de Olá dos seus dados e como coluna de Olá será utilizada nas consultas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-185">hello options that you use for each column depend on hello characteristics of your data and how hello column will be used in queries.</span></span>

### <a name="a-create-single-column-statistics-with-default-options"></a><span data-ttu-id="ba43a-186">A.</span><span class="sxs-lookup"><span data-stu-id="ba43a-186">A.</span></span> <span data-ttu-id="ba43a-187">Criar estatísticas de coluna única com opções predefinidas</span><span class="sxs-lookup"><span data-stu-id="ba43a-187">Create single-column statistics with default options</span></span>
<span data-ttu-id="ba43a-188">estatísticas de toocreate numa coluna, só tem de fornecer um nome para o objeto de estatísticas de Olá e um nome de Olá da coluna de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-188">toocreate statistics on a column, simply provide a name for hello statistics object and hello name of hello column.</span></span>

<span data-ttu-id="ba43a-189">Esta sintaxe utiliza todas as opções predefinidas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-189">This syntax uses all of hello default options.</span></span> <span data-ttu-id="ba43a-190">Por predefinição, o SQL Data Warehouse amostras 20 por cento da tabela de Olá quando cria estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-190">By default, SQL Data Warehouse samples 20 percent of hello table when it creates statistics.</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]);
```

<span data-ttu-id="ba43a-191">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-191">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1);
```

### <a name="b-create-single-column-statistics-by-examining-every-row"></a><span data-ttu-id="ba43a-192">B.</span><span class="sxs-lookup"><span data-stu-id="ba43a-192">B.</span></span> <span data-ttu-id="ba43a-193">Criar estatísticas de coluna única, examinando cada linha</span><span class="sxs-lookup"><span data-stu-id="ba43a-193">Create single-column statistics by examining every row</span></span>
<span data-ttu-id="ba43a-194">frequência de amostragem Olá predefinição de 20 por cento é suficiente para a maioria das situações.</span><span class="sxs-lookup"><span data-stu-id="ba43a-194">hello default sampling rate of 20 percent is sufficient for most situations.</span></span> <span data-ttu-id="ba43a-195">No entanto, pode ajustar a frequência de amostragem Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-195">However, you can adjust hello sampling rate.</span></span>

<span data-ttu-id="ba43a-196">Olá toosample completo de tabela, utilizam esta sintaxe:</span><span class="sxs-lookup"><span data-stu-id="ba43a-196">toosample hello full table, use this syntax:</span></span>

```sql
CREATE STATISTICS [statistics_name] ON [schema_name].[table_name]([column_name]) WITH FULLSCAN;
```

<span data-ttu-id="ba43a-197">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-197">For example:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH FULLSCAN;
```

### <a name="c-create-single-column-statistics-by-specifying-hello-sample-size"></a><span data-ttu-id="ba43a-198">C.</span><span class="sxs-lookup"><span data-stu-id="ba43a-198">C.</span></span> <span data-ttu-id="ba43a-199">Criar estatísticas de coluna única, especificando o tamanho da amostra Olá</span><span class="sxs-lookup"><span data-stu-id="ba43a-199">Create single-column statistics by specifying hello sample size</span></span>
<span data-ttu-id="ba43a-200">Em alternativa, pode especificar o tamanho da amostra Olá como uma percentagem:</span><span class="sxs-lookup"><span data-stu-id="ba43a-200">Alternatively, you can specify hello sample size as a percent:</span></span>

```sql
CREATE STATISTICS col1_stats ON dbo.table1 (col1) WITH SAMPLE = 50 PERCENT;
```

### <a name="d-create-single-column-statistics-on-only-some-of-hello-rows"></a><span data-ttu-id="ba43a-201">D.</span><span class="sxs-lookup"><span data-stu-id="ba43a-201">D.</span></span> <span data-ttu-id="ba43a-202">Criar estatísticas de coluna única na apenas algumas das linhas de Olá</span><span class="sxs-lookup"><span data-stu-id="ba43a-202">Create single-column statistics on only some of hello rows</span></span>
<span data-ttu-id="ba43a-203">Outra opção, pode criar estatísticas numa parte de linhas de Olá na tabela.</span><span class="sxs-lookup"><span data-stu-id="ba43a-203">Another option, you can create statistics on a portion of hello rows in your table.</span></span> <span data-ttu-id="ba43a-204">Esta opção é denominada uma estatística filtrada.</span><span class="sxs-lookup"><span data-stu-id="ba43a-204">This is called a filtered statistic.</span></span>

<span data-ttu-id="ba43a-205">Por exemplo, pode utilizar as estatísticas filtradas quando planeia tooquery uma partição específica de uma tabela particionada grande.</span><span class="sxs-lookup"><span data-stu-id="ba43a-205">For example, you could use filtered statistics when you plan tooquery a specific partition of a large partitioned table.</span></span> <span data-ttu-id="ba43a-206">Ao criar estatísticas em Olá apenas valores de partição, exatidão Olá das estatísticas de Olá melhorar e, por conseguinte, melhorar o desempenho das consultas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-206">By creating statistics on only hello partition values, hello accuracy of hello statistics will improve, and therefore improve query performance.</span></span>

<span data-ttu-id="ba43a-207">Este exemplo cria estatísticas num intervalo de valores.</span><span class="sxs-lookup"><span data-stu-id="ba43a-207">This example creates statistics on a range of values.</span></span> <span data-ttu-id="ba43a-208">valores de Olá facilmente pode ser definido o intervalo de Olá toomatch de valores numa partição.</span><span class="sxs-lookup"><span data-stu-id="ba43a-208">hello values could easily be defined toomatch hello range of values in a partition.</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1(col1) WHERE col1 > '2000101' AND col1 < '20001231';
```

> [!NOTE]
> <span data-ttu-id="ba43a-209">Para Olá tooconsider otimizador consulta com as estatísticas filtradas quando escolhe o plano de consulta distribuída Olá, consulta Olá deve caber Olá definição do objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-209">For hello query optimizer tooconsider using filtered statistics when it chooses hello distributed query plan, hello query must fit inside hello definition of hello statistics object.</span></span> <span data-ttu-id="ba43a-210">Exemplo de Olá anterior, Olá da consulta em que a cláusula tem toospecify col1 valores entre 2000101 e 20001231 a utilizar.</span><span class="sxs-lookup"><span data-stu-id="ba43a-210">Using hello previous example, hello query's where clause needs toospecify col1 values between 2000101 and 20001231.</span></span>
> 
> 

### <a name="e-create-single-column-statistics-with-all-hello-options"></a><span data-ttu-id="ba43a-211">E.</span><span class="sxs-lookup"><span data-stu-id="ba43a-211">E.</span></span> <span data-ttu-id="ba43a-212">Criar estatísticas de coluna única com todas as opções de Olá</span><span class="sxs-lookup"><span data-stu-id="ba43a-212">Create single-column statistics with all hello options</span></span>
<span data-ttu-id="ba43a-213">Obviamente, pode combinar as opções de Olá em conjunto.</span><span class="sxs-lookup"><span data-stu-id="ba43a-213">You can, of course, combine hello options together.</span></span> <span data-ttu-id="ba43a-214">exemplo de Olá abaixo cria um objeto de estatísticas filtradas com um tamanho de amostra personalizado:</span><span class="sxs-lookup"><span data-stu-id="ba43a-214">hello example below creates a filtered statistics object with a custom sample size:</span></span>

```sql
CREATE STATISTICS stats_col1 ON table1 (col1) WHERE col1 > '2000101' AND col1 < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="ba43a-215">Para referência completa Olá, consulte [CREATE STATISTICS] [ CREATE STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba43a-215">For hello full reference, see [CREATE STATISTICS][CREATE STATISTICS] on MSDN.</span></span>

### <a name="f-create-multi-column-statistics"></a><span data-ttu-id="ba43a-216">F.</span><span class="sxs-lookup"><span data-stu-id="ba43a-216">F.</span></span> <span data-ttu-id="ba43a-217">Criar estatísticas de várias colunas</span><span class="sxs-lookup"><span data-stu-id="ba43a-217">Create multi-column statistics</span></span>
<span data-ttu-id="ba43a-218">toocreate estatísticas de várias colunas, basta utilizar exemplos anteriores Olá, mas especificar mais colunas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-218">toocreate a multi-column statistics, simply use hello previous examples, but specify more columns.</span></span>

> [!NOTE]
> <span data-ttu-id="ba43a-219">histograma Olá, que é utilizada tooestimate número de linhas no resultado da consulta Olá, só está disponível para a primeira coluna de Olá listada na definição de objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-219">hello histogram, which is used tooestimate number of rows in hello query result, is only available for hello first column listed in hello statistics object definition.</span></span>
> 
> 

<span data-ttu-id="ba43a-220">Neste exemplo, histograma Olá é no *produto\_categoria*.</span><span class="sxs-lookup"><span data-stu-id="ba43a-220">In this example, hello histogram is on *product\_category*.</span></span> <span data-ttu-id="ba43a-221">Estatísticas de coluna em vários locais são calculadas *produto\_categoria* e *produto\_sub_c\ategory*:</span><span class="sxs-lookup"><span data-stu-id="ba43a-221">Cross-column statistics are calculated on *product\_category* and *product\_sub_c\ategory*:</span></span>

```sql
CREATE STATISTICS stats_2cols ON table1 (product_category, product_sub_category) WHERE product_category > '2000101' AND product_category < '20001231' WITH SAMPLE = 50 PERCENT;
```

<span data-ttu-id="ba43a-222">Uma vez que existe uma correlação entre *produto\_categoria* e *produto\_sub\_categoria*, estado várias coluna pode ser úteis se estas colunas são acedidas em Olá mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="ba43a-222">Since there is a correlation between *product\_category* and *product\_sub\_category*, a multi-column stat can be useful if these columns are accessed at hello same time.</span></span>

### <a name="g-create-statistics-on-all-hello-columns-in-a-table"></a><span data-ttu-id="ba43a-223">G.</span><span class="sxs-lookup"><span data-stu-id="ba43a-223">G.</span></span> <span data-ttu-id="ba43a-224">Criar estatísticas em todas as colunas de Olá numa tabela</span><span class="sxs-lookup"><span data-stu-id="ba43a-224">Create statistics on all hello columns in a table</span></span>
<span data-ttu-id="ba43a-225">Estatísticas de toocreate unidirecional é tooissues comandos CREATE STATISTICS depois de criar a tabela de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-225">One way toocreate statistics is tooissues CREATE STATISTICS commands after creating hello table.</span></span>

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

### <a name="h-use-a-stored-procedure-toocreate-statistics-on-all-columns-in-a-database"></a><span data-ttu-id="ba43a-226">H.</span><span class="sxs-lookup"><span data-stu-id="ba43a-226">H.</span></span> <span data-ttu-id="ba43a-227">Utilize as estatísticas de toocreate um procedimento armazenado em todas as colunas numa base de dados</span><span class="sxs-lookup"><span data-stu-id="ba43a-227">Use a stored procedure toocreate statistics on all columns in a database</span></span>
<span data-ttu-id="ba43a-228">Armazém de dados do SQL Server não tem um equivalente do procedimento armazenado de sistema demasiado [sp_create_stats] [-] no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="ba43a-228">SQL Data Warehouse does not have a system stored procedure equivalent too[sp_create_stats][] in SQL Server.</span></span> <span data-ttu-id="ba43a-229">Este procedimento armazenado cria um objeto de estatísticas de coluna única em cada coluna de base de dados de Olá que já não tem as estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-229">This stored procedure creates a single column statistics object on every column of hello database that doesn't already have statistics.</span></span>

<span data-ttu-id="ba43a-230">Isto irá ajudar a começar com o design da sua base de dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-230">This will help you get started with your database design.</span></span> <span data-ttu-id="ba43a-231">Sentir tooadapt livre-tooyour precisa.</span><span class="sxs-lookup"><span data-stu-id="ba43a-231">Feel free tooadapt it tooyour needs.</span></span>

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

<span data-ttu-id="ba43a-232">toocreate estatísticas em todas as colunas na tabela de Olá com este procedimento, basta chamar o procedimento de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-232">toocreate statistics on all columns in hello table with this procedure, simply call hello procedure.</span></span>

```sql
prc_sqldw_create_stats;
```

## <a name="examples-update-statistics"></a><span data-ttu-id="ba43a-233">Exemplos: estatísticas de atualização</span><span class="sxs-lookup"><span data-stu-id="ba43a-233">Examples: update statistics</span></span>
<span data-ttu-id="ba43a-234">estatísticas de tooupdate, pode:</span><span class="sxs-lookup"><span data-stu-id="ba43a-234">tooupdate statistics, you can:</span></span>

1. <span data-ttu-id="ba43a-235">Atualize um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-235">Update one statistics object.</span></span> <span data-ttu-id="ba43a-236">Especifique o nome Olá Olá estatísticas pretende tooupdate de objeto.</span><span class="sxs-lookup"><span data-stu-id="ba43a-236">Specify hello name of hello statistics object you wish tooupdate.</span></span>
2. <span data-ttu-id="ba43a-237">Atualize todos os objetos de estatísticas numa tabela.</span><span class="sxs-lookup"><span data-stu-id="ba43a-237">Update all statistics objects on a table.</span></span> <span data-ttu-id="ba43a-238">Especifique o nome de Olá da tabela de Olá em vez de um objeto de estatísticas específico.</span><span class="sxs-lookup"><span data-stu-id="ba43a-238">Specify hello name of hello table instead of one specific statistics object.</span></span>

### <a name="a-update-one-specific-statistics-object"></a><span data-ttu-id="ba43a-239">A.</span><span class="sxs-lookup"><span data-stu-id="ba43a-239">A.</span></span> <span data-ttu-id="ba43a-240">Atualizar um objeto de estatísticas específico</span><span class="sxs-lookup"><span data-stu-id="ba43a-240">Update one specific statistics object</span></span>
<span data-ttu-id="ba43a-241">Utilize Olá seguindo a sintaxe tooupdate um objeto de estatísticas específico:</span><span class="sxs-lookup"><span data-stu-id="ba43a-241">Use hello following syntax tooupdate a specific statistics object:</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name]([stat_name]);
```

<span data-ttu-id="ba43a-242">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-242">For example:</span></span>

```sql
UPDATE STATISTICS [dbo].[table1] ([stats_col1]);
```

<span data-ttu-id="ba43a-243">Ao atualizar objetos de estatísticas específico, pode minimizar Olá recursos e tempo necessários toomanage estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-243">By updating specific statistics objects, you can minimize hello time and resources required toomanage statistics.</span></span> <span data-ttu-id="ba43a-244">Isto requer que alguns considerar-se, no entanto, toochoose Olá melhor estatísticas objetos tooupdate.</span><span class="sxs-lookup"><span data-stu-id="ba43a-244">This requires some thought, though, toochoose hello best statistics objects tooupdate.</span></span>

### <a name="b-update-all-statistics-on-a-table"></a><span data-ttu-id="ba43a-245">B.</span><span class="sxs-lookup"><span data-stu-id="ba43a-245">B.</span></span> <span data-ttu-id="ba43a-246">Atualizar todas as estatísticas numa tabela</span><span class="sxs-lookup"><span data-stu-id="ba43a-246">Update all statistics on a table</span></span>
<span data-ttu-id="ba43a-247">Mostra um método simples para atualizar todos os objetos de estatísticas de Olá numa tabela.</span><span class="sxs-lookup"><span data-stu-id="ba43a-247">This shows a simple method for updating all hello statistics objects on a table.</span></span>

```sql
UPDATE STATISTICS [schema_name].[table_name];
```

<span data-ttu-id="ba43a-248">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-248">For example:</span></span>

```sql
UPDATE STATISTICS dbo.table1;
```

<span data-ttu-id="ba43a-249">Esta instrução é fácil toouse.</span><span class="sxs-lookup"><span data-stu-id="ba43a-249">This statement is easy toouse.</span></span> <span data-ttu-id="ba43a-250">Lembre-se apenas isto atualiza todas as estatísticas na tabela de Olá e, assim, poderá efetuar trabalho mais do que é necessário.</span><span class="sxs-lookup"><span data-stu-id="ba43a-250">Just remember this updates all statistics on hello table, and therefore might perform more work than is necessary.</span></span> <span data-ttu-id="ba43a-251">Se o desempenho de Olá não for um problema, esta é sem dúvida forma de mais fácil e mais completa de Olá tooguarantee estatísticas são atualizadas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-251">If hello performance is not an issue, this is definitely hello easiest and most complete way tooguarantee statistics are up-to-date.</span></span>

> [!NOTE]
> <span data-ttu-id="ba43a-252">Ao atualizar todas as estatísticas numa tabela, o SQL Data Warehouse efetua uma tabela de Olá toosample de análise para cada estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-252">When updating all statistics on a table, SQL Data Warehouse does a scan toosample hello table for each statistics.</span></span> <span data-ttu-id="ba43a-253">Se a tabela de Olá for grande, tem demasiadas colunas e estatísticas de muitas, poderá ser mais eficientes tooupdate individuais as estatísticas com base na necessidade.</span><span class="sxs-lookup"><span data-stu-id="ba43a-253">If hello table is large, has many columns, and many statistics, it might be more efficient tooupdate individual statistics based on need.</span></span>
> 
> 

<span data-ttu-id="ba43a-254">Para uma implementação de um `UPDATE STATISTICS` procedimento Consulte Olá [tabelas temporárias] [ Temporary] artigo.</span><span class="sxs-lookup"><span data-stu-id="ba43a-254">For an implementation of an `UPDATE STATISTICS` procedure please see hello [Temporary Tables][Temporary] article.</span></span> <span data-ttu-id="ba43a-255">o método de implementação de Olá é ligeiramente diferente toohello `CREATE STATISTICS` procedimento acima, mas o resultado final de Olá é Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="ba43a-255">hello implementation method is slightly different toohello `CREATE STATISTICS` procedure above but hello end result is hello same.</span></span>

<span data-ttu-id="ba43a-256">Para a sintaxe completa Olá, consulte [Update Statistics] [ Update Statistics] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba43a-256">For hello full syntax, see [Update Statistics][Update Statistics] on MSDN.</span></span>

## <a name="statistics-metadata"></a><span data-ttu-id="ba43a-257">Metadados de estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-257">Statistics metadata</span></span>
<span data-ttu-id="ba43a-258">Existem várias funções que pode utilizar toofind informações sobre as estatísticas e vista de sistema.</span><span class="sxs-lookup"><span data-stu-id="ba43a-258">There are several system view and functions that you can use toofind information about statistics.</span></span> <span data-ttu-id="ba43a-259">Por exemplo, pode ver se um objeto de estatísticas pode estar desatualizado utilizando Olá estatísticas data função toosee quando estatísticas foram criadas ou atualizadas pela última vez.</span><span class="sxs-lookup"><span data-stu-id="ba43a-259">For example, you can see if a statistics object might be out-of-date by using hello stats-date function toosee when statistics were last created or updated.</span></span>

### <a name="catalog-views-for-statistics"></a><span data-ttu-id="ba43a-260">Vistas de catálogo para estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-260">Catalog views for statistics</span></span>
<span data-ttu-id="ba43a-261">Estas vistas de sistema fornecem informações sobre as estatísticas:</span><span class="sxs-lookup"><span data-stu-id="ba43a-261">These system views provide information about statistics:</span></span>

| <span data-ttu-id="ba43a-262">Vista de catálogo</span><span class="sxs-lookup"><span data-stu-id="ba43a-262">Catalog View</span></span> | <span data-ttu-id="ba43a-263">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba43a-263">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba43a-264">[sys.Columns][sys.columns]</span><span class="sxs-lookup"><span data-stu-id="ba43a-264">[sys.columns][sys.columns]</span></span> |<span data-ttu-id="ba43a-265">Uma linha para cada coluna.</span><span class="sxs-lookup"><span data-stu-id="ba43a-265">One row for each column.</span></span> |
| <span data-ttu-id="ba43a-266">[sys.Objects][sys.objects]</span><span class="sxs-lookup"><span data-stu-id="ba43a-266">[sys.objects][sys.objects]</span></span> |<span data-ttu-id="ba43a-267">Uma linha para cada objeto na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-267">One row for each object in hello database.</span></span> |
| <span data-ttu-id="ba43a-268">[sys.schemas][sys.schemas]</span><span class="sxs-lookup"><span data-stu-id="ba43a-268">[sys.schemas][sys.schemas]</span></span> |<span data-ttu-id="ba43a-269">Uma linha para cada esquema na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-269">One row for each schema in hello database.</span></span> |
| <span data-ttu-id="ba43a-270">[sys.Stats][sys.stats]</span><span class="sxs-lookup"><span data-stu-id="ba43a-270">[sys.stats][sys.stats]</span></span> |<span data-ttu-id="ba43a-271">Uma linha para cada objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-271">One row for each statistics object.</span></span> |
| <span data-ttu-id="ba43a-272">[sys.stats_columns][sys.stats_columns]</span><span class="sxs-lookup"><span data-stu-id="ba43a-272">[sys.stats_columns][sys.stats_columns]</span></span> |<span data-ttu-id="ba43a-273">Uma linha para cada coluna no objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-273">One row for each column in hello statistics object.</span></span> <span data-ttu-id="ba43a-274">Ligações de fazer uma cópia toosys.columns.</span><span class="sxs-lookup"><span data-stu-id="ba43a-274">Links back toosys.columns.</span></span> |
| <span data-ttu-id="ba43a-275">[sys. Tables][sys.tables]</span><span class="sxs-lookup"><span data-stu-id="ba43a-275">[sys.tables][sys.tables]</span></span> |<span data-ttu-id="ba43a-276">Uma linha para cada tabela (inclui as tabelas externas).</span><span class="sxs-lookup"><span data-stu-id="ba43a-276">One row for each table (includes external tables).</span></span> |
| <span data-ttu-id="ba43a-277">[sys.table_types][sys.table_types]</span><span class="sxs-lookup"><span data-stu-id="ba43a-277">[sys.table_types][sys.table_types]</span></span> |<span data-ttu-id="ba43a-278">Uma linha para cada tipo de dados.</span><span class="sxs-lookup"><span data-stu-id="ba43a-278">One row for each data type.</span></span> |

### <a name="system-functions-for-statistics"></a><span data-ttu-id="ba43a-279">Funções de sistema para estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-279">System functions for statistics</span></span>
<span data-ttu-id="ba43a-280">Estas funções de sistema são úteis para trabalhar com as estatísticas:</span><span class="sxs-lookup"><span data-stu-id="ba43a-280">These system functions are useful for working with statistics:</span></span>

| <span data-ttu-id="ba43a-281">Função de sistema</span><span class="sxs-lookup"><span data-stu-id="ba43a-281">System Function</span></span> | <span data-ttu-id="ba43a-282">Descrição</span><span class="sxs-lookup"><span data-stu-id="ba43a-282">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="ba43a-283">[STATS_DATE][STATS_DATE]</span><span class="sxs-lookup"><span data-stu-id="ba43a-283">[STATS_DATE][STATS_DATE]</span></span> |<span data-ttu-id="ba43a-284">Objeto de estatísticas de Olá data foi atualizado pela última vez.</span><span class="sxs-lookup"><span data-stu-id="ba43a-284">Date hello statistics object was last updated.</span></span> |
| <span data-ttu-id="ba43a-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span><span class="sxs-lookup"><span data-stu-id="ba43a-285">[DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS]</span></span> |<span data-ttu-id="ba43a-286">Fornece resumidas nível e informações detalhadas sobre a distribuição de Olá de valores como compreendida por objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-286">Provides summary level and detailed information about hello distribution of values as understood by hello statistics object.</span></span> |

### <a name="combine-statistics-columns-and-functions-into-one-view"></a><span data-ttu-id="ba43a-287">Combinar as colunas de estatísticas e as funções para uma vista</span><span class="sxs-lookup"><span data-stu-id="ba43a-287">Combine statistics columns and functions into one view</span></span>
<span data-ttu-id="ba43a-288">Esta vista apresenta as colunas que se relacionam com toostatistics e os resultados da função de [] Olá [STATS_DATE()] em conjunto.</span><span class="sxs-lookup"><span data-stu-id="ba43a-288">This view brings columns that relate toostatistics, and results from hello [STATS_DATE()][]function together.</span></span>

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

## <a name="dbcc-showstatistics-examples"></a><span data-ttu-id="ba43a-289">Exemplos de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="ba43a-289">DBCC SHOW_STATISTICS() examples</span></span>
<span data-ttu-id="ba43a-290">DBCC SHOW_STATISTICS() mostra os dados de Olá contidos dentro de um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-290">DBCC SHOW_STATISTICS() shows hello data held within a statistics object.</span></span> <span data-ttu-id="ba43a-291">Estes dados é apresentada no três partes.</span><span class="sxs-lookup"><span data-stu-id="ba43a-291">This data comes in three parts.</span></span>

1. <span data-ttu-id="ba43a-292">Cabeçalho</span><span class="sxs-lookup"><span data-stu-id="ba43a-292">Header</span></span>
2. <span data-ttu-id="ba43a-293">Vetor de densidade</span><span class="sxs-lookup"><span data-stu-id="ba43a-293">Density Vector</span></span>
3. <span data-ttu-id="ba43a-294">Histograma</span><span class="sxs-lookup"><span data-stu-id="ba43a-294">Histogram</span></span>

<span data-ttu-id="ba43a-295">metadados de cabeçalho de Olá sobre estatísticas Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-295">hello header metadata about hello statistics.</span></span> <span data-ttu-id="ba43a-296">histograma Olá mostra a distribuição Olá de valores na primeira coluna chave Olá do objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-296">hello histogram displays hello distribution of values in hello first key column of hello statistics object.</span></span> <span data-ttu-id="ba43a-297">Olá densidade vetor medidas entre coluna correlação.</span><span class="sxs-lookup"><span data-stu-id="ba43a-297">hello density vector measures cross-column correlation.</span></span> <span data-ttu-id="ba43a-298">SQLDW calcula estimativas de cardinalidade com qualquer um dos dados de Olá no objeto de estatísticas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ba43a-298">SQLDW computes cardinality estimates with any of hello data in hello statistics object.</span></span>

### <a name="show-header-density-and-histogram"></a><span data-ttu-id="ba43a-299">Mostrar o cabeçalho, densidade e histograma</span><span class="sxs-lookup"><span data-stu-id="ba43a-299">Show header, density, and histogram</span></span>
<span data-ttu-id="ba43a-300">Neste exemplo simples mostra todos os três partes de um objeto de estatísticas.</span><span class="sxs-lookup"><span data-stu-id="ba43a-300">This simple example shows all three parts of a statistics object.</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>)
```

<span data-ttu-id="ba43a-301">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-301">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1);
```

### <a name="show-one-or-more-parts-of-dbcc-showstatistics"></a><span data-ttu-id="ba43a-302">Mostrar uma ou mais partes de DBCC SHOW_STATISTICS();</span><span class="sxs-lookup"><span data-stu-id="ba43a-302">Show one or more parts of DBCC SHOW_STATISTICS();</span></span>
<span data-ttu-id="ba43a-303">Se apenas estiver interessado em partes específicas de visualização, utilize Olá `WITH` cláusula e especifique que partes pretende toosee:</span><span class="sxs-lookup"><span data-stu-id="ba43a-303">If you are only interested in viewing specific parts, use hello `WITH` clause and specify which parts you want toosee:</span></span>

```sql
DBCC SHOW_STATISTICS([<schema_name>.<table_name>],<stats_name>) WITH stat_header, histogram, density_vector
```

<span data-ttu-id="ba43a-304">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="ba43a-304">For example:</span></span>

```sql
DBCC SHOW_STATISTICS (dbo.table1, stats_col1) WITH histogram, density_vector
```

## <a name="dbcc-showstatistics-differences"></a><span data-ttu-id="ba43a-305">Diferenças de DBCC SHOW_STATISTICS()</span><span class="sxs-lookup"><span data-stu-id="ba43a-305">DBCC SHOW_STATISTICS() differences</span></span>
<span data-ttu-id="ba43a-306">DBCC SHOW_STATISTICS() mais estritamente está implementada no servidor do armazém de dados do SQL Server em comparação com tooSQL.</span><span class="sxs-lookup"><span data-stu-id="ba43a-306">DBCC SHOW_STATISTICS() is more strictly implemented in SQL Data Warehouse compared tooSQL Server.</span></span>

1. <span data-ttu-id="ba43a-307">Não são suportadas as funcionalidades não documentadas</span><span class="sxs-lookup"><span data-stu-id="ba43a-307">Undocumented features are not supported</span></span>
2. <span data-ttu-id="ba43a-308">Não é possível utilizar Stats_stream</span><span class="sxs-lookup"><span data-stu-id="ba43a-308">Cannot use Stats_stream</span></span>
3. <span data-ttu-id="ba43a-309">Não é possível associar resultados para subconjuntos específicos de dados de estatísticas por exemplo, (STAT_HEADER associação DENSITY_VECTOR)</span><span class="sxs-lookup"><span data-stu-id="ba43a-309">Cannot join results for specific subsets of statistics data e.g. (STAT_HEADER JOIN DENSITY_VECTOR)</span></span>
4. <span data-ttu-id="ba43a-310">Não é possível definir NO_INFOMSGS para supressão de mensagem</span><span class="sxs-lookup"><span data-stu-id="ba43a-310">NO_INFOMSGS cannot be set for message suppression</span></span>
5. <span data-ttu-id="ba43a-311">Não é possível utilizar parênteses Retos à volta de nomes de estatísticas</span><span class="sxs-lookup"><span data-stu-id="ba43a-311">Square brackets around statistics names cannot be used</span></span>
6. <span data-ttu-id="ba43a-312">Não é possível utilizar objetos de estatísticas de tooidentify de nomes de coluna</span><span class="sxs-lookup"><span data-stu-id="ba43a-312">Cannot use column names tooidentify statistics objects</span></span>
7. <span data-ttu-id="ba43a-313">Erro personalizado 2767 não é suportado</span><span class="sxs-lookup"><span data-stu-id="ba43a-313">Custom error 2767 is not supported</span></span>

## <a name="next-steps"></a><span data-ttu-id="ba43a-314">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ba43a-314">Next steps</span></span>
<span data-ttu-id="ba43a-315">Para obter mais detalhes, consulte [DBCC SHOW_STATISTICS] [ DBCC SHOW_STATISTICS] no MSDN.</span><span class="sxs-lookup"><span data-stu-id="ba43a-315">For more details, see [DBCC SHOW_STATISTICS][DBCC SHOW_STATISTICS] on MSDN.</span></span>  <span data-ttu-id="ba43a-316">toolearn mais, consulte os artigos de Olá no [descrição geral da tabela][Overview], [tipos de dados de tabela][Data Types], [distribuir uma tabela] [ Distribute], [Uma tabela de indexação][Index], [uma tabela de criação de partições] [ Partition] e [ Tabelas temporárias][Temporary].</span><span class="sxs-lookup"><span data-stu-id="ba43a-316">toolearn more, see hello articles on [Table Overview][Overview], [Table Data Types][Data Types], [Distributing a Table][Distribute], [Indexing a Table][Index],  [Partitioning a Table][Partition] and [Temporary Tables][Temporary].</span></span>  <span data-ttu-id="ba43a-317">Para obter mais informações sobre as melhores práticas, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="ba43a-317">For more about best practices, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>  

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
