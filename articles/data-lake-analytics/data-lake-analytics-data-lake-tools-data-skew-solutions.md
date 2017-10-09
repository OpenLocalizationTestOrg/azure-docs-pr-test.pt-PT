---
title: problemas de desfasamento de dados de aaaResolve utilizando ferramentas do Azure Data Lake para Visual Studio | Microsoft Docs
description: "Resolução de problemas possíveis soluções para problemas de desfasamento de dados utilizando ferramentas do Azure Data Lake para Visual Studio."
services: data-lake-analytics
documentationcenter: 
author: yanancai
manager: 
editor: 
ms.assetid: 
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 12/16/2016
ms.author: yanacai
ms.openlocfilehash: 3909fbd89eb40f061268cb7128f7fa84a3c33de7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="resolve-data-skew-problems-by-using-azure-data-lake-tools-for-visual-studio"></a><span data-ttu-id="ec22a-103">Resolver problemas de desfasamento de dados utilizando ferramentas do Azure Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ec22a-103">Resolve data-skew problems by using Azure Data Lake Tools for Visual Studio</span></span>

## <a name="what-is-data-skew"></a><span data-ttu-id="ec22a-104">O que é dados desfasamento?</span><span class="sxs-lookup"><span data-stu-id="ec22a-104">What is data skew?</span></span>

<span data-ttu-id="ec22a-105">Brevemente indicado, o desfasamento de dados é um valor excessiva representado.</span><span class="sxs-lookup"><span data-stu-id="ec22a-105">Briefly stated, data skew is an over-represented value.</span></span> <span data-ttu-id="ec22a-106">Imagine que atribuiu 50 examiners de dedução dos impostos tooaudit dedução dos impostos devolve, um examiner para cada Estado de E.U.A..</span><span class="sxs-lookup"><span data-stu-id="ec22a-106">Imagine that you have assigned 50 tax examiners tooaudit tax returns, one examiner for each US state.</span></span> <span data-ttu-id="ec22a-107">examiner de Wyoming Olá, porque não existe a população Olá é pequena, tem pouco toodo.</span><span class="sxs-lookup"><span data-stu-id="ec22a-107">hello Wyoming examiner, because hello population there is small, has little toodo.</span></span> <span data-ttu-id="ec22a-108">Na Califórnia, no entanto, examiner Olá é mantida muito ocupado devido a população do Estado de Olá de grandes dimensões.</span><span class="sxs-lookup"><span data-stu-id="ec22a-108">In California, however, hello examiner is kept very busy because of hello state's large population.</span></span>
    <span data-ttu-id="ec22a-109">![Exemplo de problema de desfasamento de dados](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span><span class="sxs-lookup"><span data-stu-id="ec22a-109">![Data-skew problem example](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/data-skew-problem.png)</span></span>

<span data-ttu-id="ec22a-110">No nosso cenário, dados de Olá é unevenly distribuídos por todos os examiners de dedução dos impostos, que significa que alguns examiners tem de trabalhar mais do que outras pessoas.</span><span class="sxs-lookup"><span data-stu-id="ec22a-110">In our scenario, hello data is unevenly distributed across all tax examiners, which means that some examiners must work more than others.</span></span> <span data-ttu-id="ec22a-111">No seu próprio trabalho frequentemente experiência situações como Olá exemplo de dedução dos impostos examiner aqui.</span><span class="sxs-lookup"><span data-stu-id="ec22a-111">In your own job, you frequently experience situations like hello tax-examiner example here.</span></span> <span data-ttu-id="ec22a-112">Em termos mais técnicos, um vértice obtém muito mais dados de elementos da rede, uma situação que faz com que o vértice Olá mais do que Olá outras pessoas e que eventualmente atrasar uma tarefa de toda a funcionar.</span><span class="sxs-lookup"><span data-stu-id="ec22a-112">In more technical terms, one vertex gets much more data than its peers, a situation that makes hello vertex work more than hello others and that eventually slows down an entire job.</span></span> <span data-ttu-id="ec22a-113">O que é um, a tarefa de Olá poderá falhar, porque poderão ter vértices, por exemplo, uma limitação de tempo de execução de 5 horas e uma limitação de 6 GB de memória.</span><span class="sxs-lookup"><span data-stu-id="ec22a-113">What's worse, hello job might fail, because vertices might have, for example, a 5-hour runtime limitation and a 6-GB memory limitation.</span></span>

## <a name="resolving-data-skew-problems"></a><span data-ttu-id="ec22a-114">Resolver problemas de desfasamento de dados</span><span class="sxs-lookup"><span data-stu-id="ec22a-114">Resolving data-skew problems</span></span>

<span data-ttu-id="ec22a-115">Ferramentas do Azure Data Lake para Visual Studio podem ajudá-lo a detetar se a tarefa tem um problema de desfasamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ec22a-115">Azure Data Lake Tools for Visual Studio can help detect whether your job has a data-skew problem.</span></span> <span data-ttu-id="ec22a-116">Se existir um problema, pode resolver-tentando soluções Olá nesta secção.</span><span class="sxs-lookup"><span data-stu-id="ec22a-116">If a problem exists, you can resolve it by trying hello solutions in this section.</span></span>

## <a name="solution-1-improve-table-partitioning"></a><span data-ttu-id="ec22a-117">Solução 1: Melhorar a criação de partições de tabela</span><span class="sxs-lookup"><span data-stu-id="ec22a-117">Solution 1: Improve table partitioning</span></span>

### <a name="option-1-filter-hello-skewed-key-value-in-advance"></a><span data-ttu-id="ec22a-118">Opção 1: Olá filtro skewed valor da chave antecipadamente</span><span class="sxs-lookup"><span data-stu-id="ec22a-118">Option 1: Filter hello skewed key value in advance</span></span>

<span data-ttu-id="ec22a-119">Se não afeta a lógica de negócio, pode filtrar valores de frequência superior Olá antecipadamente.</span><span class="sxs-lookup"><span data-stu-id="ec22a-119">If it does not affect your business logic, you can filter hello higher-frequency values in advance.</span></span> <span data-ttu-id="ec22a-120">Por exemplo, se existirem muitos 000 000 000 na coluna GUID, não poderá tooaggregate esse valor.</span><span class="sxs-lookup"><span data-stu-id="ec22a-120">For example, if there are a lot of 000-000-000 in column GUID, you might not want tooaggregate that value.</span></span> <span data-ttu-id="ec22a-121">Antes de agregação, pode escrever "WHERE GUID! ="000-000 000"" valor de alta frequência toofilter Olá.</span><span class="sxs-lookup"><span data-stu-id="ec22a-121">Before you aggregate, you can write “WHERE GUID != “000-000-000”” toofilter hello high-frequency value.</span></span>

### <a name="option-2-pick-a-different-partition-or-distribution-key"></a><span data-ttu-id="ec22a-122">Opção 2: Escolher uma chave de partição ou de distribuição diferente</span><span class="sxs-lookup"><span data-stu-id="ec22a-122">Option 2: Pick a different partition or distribution key</span></span>

<span data-ttu-id="ec22a-123">Olá anterior exemplo, se pretender que a carga de trabalho do toocheck apenas Olá dedução dos impostos auditoria Olá todas através de país, pode melhorar a distribuição de dados de Olá selecionando o número de ID de Olá como a chave.</span><span class="sxs-lookup"><span data-stu-id="ec22a-123">In hello preceding example, if you want only toocheck hello tax-audit workload all over hello country, you can improve hello data distribution by selecting hello ID number as your key.</span></span> <span data-ttu-id="ec22a-124">Escolha uma partição diferente ou chave de distribuição pode, por vezes, distribuir dados Olá mais uniformemente, mas tem de certificar-se de que esta opção não afeta a lógica de negócio toomake.</span><span class="sxs-lookup"><span data-stu-id="ec22a-124">Picking a different partition or distribution key can sometimes distribute hello data more evenly, but you need toomake sure that this choice doesn’t affect your business logic.</span></span> <span data-ttu-id="ec22a-125">Por exemplo, toocalculate soma de dedução dos impostos de Olá para cada Estado, poderá pretender toodesignate _estado_ como chave de partição Olá.</span><span class="sxs-lookup"><span data-stu-id="ec22a-125">For instance, toocalculate hello tax sum for each state, you might want toodesignate _State_ as hello partition key.</span></span> <span data-ttu-id="ec22a-126">Se continuar tooexperience este problema, tente utilizar a opção 3.</span><span class="sxs-lookup"><span data-stu-id="ec22a-126">If you continue tooexperience this problem, try using Option 3.</span></span>

### <a name="option-3-add-more-partition-or-distribution-keys"></a><span data-ttu-id="ec22a-127">Opção 3: Adicionar mais chaves de partição ou de distribuição</span><span class="sxs-lookup"><span data-stu-id="ec22a-127">Option 3: Add more partition or distribution keys</span></span>

<span data-ttu-id="ec22a-128">Em vez de utilizar apenas _estado_ como uma chave de partição, pode utilizar mais do que uma chave para criação de partições.</span><span class="sxs-lookup"><span data-stu-id="ec22a-128">Instead of using only _State_ as a partition key, you can use more than one key for partitioning.</span></span> <span data-ttu-id="ec22a-129">Por exemplo, considere adicionar _código postal_ como uma partição adicional tooreduce chave dados partição tamanhos e distribuir uniformemente mais dados Olá.</span><span class="sxs-lookup"><span data-stu-id="ec22a-129">For example, consider adding _ZIP Code_ as an additional partition key tooreduce data-partition sizes and distribute hello data more evenly.</span></span>

### <a name="option-4-use-round-robin-distribution"></a><span data-ttu-id="ec22a-130">Opção 4: Utilizar a distribuição de round robin</span><span class="sxs-lookup"><span data-stu-id="ec22a-130">Option 4: Use round-robin distribution</span></span>

<span data-ttu-id="ec22a-131">Se não é possível localizar uma chave adequada para a partição e a distribuição, pode experimentar toouse distribuição de round robin.</span><span class="sxs-lookup"><span data-stu-id="ec22a-131">If you cannot find an appropriate key for partition and distribution, you can try toouse round-robin distribution.</span></span> <span data-ttu-id="ec22a-132">Distribuição de round robin processa todas as linhas igualmente e aleatoriamente coloca-os no registos correspondentes.</span><span class="sxs-lookup"><span data-stu-id="ec22a-132">Round-robin distribution treats all rows equally and randomly puts them into corresponding buckets.</span></span> <span data-ttu-id="ec22a-133">dados de Olá obtém distribuídos uniformemente, mas perder informações localidade, uma desvantagem que também pode reduzir o desempenho de tarefa para algumas operações.</span><span class="sxs-lookup"><span data-stu-id="ec22a-133">hello data gets evenly distributed, but it loses locality information, a drawback that can also reduce job performance for some operations.</span></span> <span data-ttu-id="ec22a-134">Além disso, se estão a fazer a agregação para a chave distorcidos Olá mesmo assim, o problema de desfasamento de dados de Olá serão mantidas.</span><span class="sxs-lookup"><span data-stu-id="ec22a-134">Additionally, if you are doing aggregation for hello skewed key anyway, hello data-skew problem will persist.</span></span> <span data-ttu-id="ec22a-135">toolearn mais informações sobre distribuição de round robin, consulte as distribuições de tabela do U-SQL Olá secção [CREATE TABLE (U-SQL): criar uma tabela com o esquema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span><span class="sxs-lookup"><span data-stu-id="ec22a-135">toolearn more about round-robin distribution, see hello U-SQL Table Distributions section in [CREATE TABLE (U-SQL): Creating a Table with Schema](https://msdn.microsoft.com/en-us/library/mt706196.aspx#dis_sch).</span></span>

## <a name="solution-2-improve-hello-query-plan"></a><span data-ttu-id="ec22a-136">Solução 2: Melhorar o plano de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="ec22a-136">Solution 2: Improve hello query plan</span></span>

### <a name="option-1-use-hello-create-statistics-statement"></a><span data-ttu-id="ec22a-137">Opção 1: Utilizar a instrução CREATE STATISTICS de Olá</span><span class="sxs-lookup"><span data-stu-id="ec22a-137">Option 1: Use hello CREATE STATISTICS statement</span></span>

<span data-ttu-id="ec22a-138">U-SQL fornece da instrução CREATE STATISTICS Olá em tabelas.</span><span class="sxs-lookup"><span data-stu-id="ec22a-138">U-SQL provides hello CREATE STATISTICS statement on tables.</span></span> <span data-ttu-id="ec22a-139">Esta declaração fornece mais informações toohello o otimizador de consultas sobre Olá características dos dados, como a distribuição de valor, que estão armazenados numa tabela.</span><span class="sxs-lookup"><span data-stu-id="ec22a-139">This statement gives more information toohello query optimizer about hello data characteristics, such as value distribution, that are stored in a table.</span></span> <span data-ttu-id="ec22a-140">Para a maior parte das consultas, otimizador de consultas Olá já gera as estatísticas de necessário Olá para um plano de consulta de alta qualidade.</span><span class="sxs-lookup"><span data-stu-id="ec22a-140">For most queries, hello query optimizer already generates hello necessary statistics for a high-quality query plan.</span></span> <span data-ttu-id="ec22a-141">Ocasionalmente, poderá ser necessário tooimprove desempenho das consultas, criar estatísticas adicionais com CREATE STATISTICS ou ao modificar a estrutura da consulta Olá.</span><span class="sxs-lookup"><span data-stu-id="ec22a-141">Occasionally, you might need tooimprove query performance by creating additional statistics with CREATE STATISTICS or by modifying hello query design.</span></span> <span data-ttu-id="ec22a-142">Para obter mais informações, consulte Olá [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) página.</span><span class="sxs-lookup"><span data-stu-id="ec22a-142">For more information, see hello [CREATE STATISTICS (U-SQL)](https://msdn.microsoft.com/en-us/library/azure/mt771898.aspx) page.</span></span>

<span data-ttu-id="ec22a-143">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="ec22a-143">Code example:</span></span>

    CREATE STATISTICS IF NOT EXISTS stats_SampleTable_date ON SampleDB.dbo.SampleTable(date) WITH FULLSCAN;

>[!NOTE]
><span data-ttu-id="ec22a-144">Informações de estatísticas não são atualizadas automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ec22a-144">Statistics information is not updated automatically.</span></span> <span data-ttu-id="ec22a-145">Se atualizar dados Olá numa tabela sem voltar a criar estatísticas Olá, o desempenho das consultas Olá poderá diminui.</span><span class="sxs-lookup"><span data-stu-id="ec22a-145">If you update hello data in a table without re-creating hello statistics, hello query performance might decline.</span></span>

### <a name="option-2-use-skewfactor"></a><span data-ttu-id="ec22a-146">Opção 2: Utilizar SKEWFACTOR</span><span class="sxs-lookup"><span data-stu-id="ec22a-146">Option 2: Use SKEWFACTOR</span></span>

<span data-ttu-id="ec22a-147">Se quiser dedução dos impostos Olá de toosum para cada Estado, tem de utilizar o grupo por Estado, uma abordagem que não a evitar o problema do Olá desfasamento de dados.</span><span class="sxs-lookup"><span data-stu-id="ec22a-147">If you want toosum hello tax for each state, you must use GROUP BY state, an approach that doesn't avoid hello data-skew problem.</span></span> <span data-ttu-id="ec22a-148">No entanto, pode fornecer uma sugestão de dados no seu tooidentify consulta dados desfasamento nas chaves de modo a que o otimizador de Olá pode preparar um plano de execução.</span><span class="sxs-lookup"><span data-stu-id="ec22a-148">However, you can provide a data hint in your query tooidentify data skew in keys so that hello optimizer can prepare an execution plan for you.</span></span>

<span data-ttu-id="ec22a-149">Normalmente, pode definir o parâmetro Olá como 0,5 e 1, com 0,5 que significa que não desfasamento de pesada significado dissimetrias e 1.</span><span class="sxs-lookup"><span data-stu-id="ec22a-149">Usually, you can set hello parameter as 0.5 and 1, with 0.5 meaning not much skew and 1 meaning heavy skew.</span></span> <span data-ttu-id="ec22a-150">Porque a sugestão Olá afeta a otimização de plano de execução para a instrução atual Olá e todas as instruções a jusante, ser sugestão de Olá tooadd se antes de Olá potencial skewed key-wise agregação.</span><span class="sxs-lookup"><span data-stu-id="ec22a-150">Because hello hint affects execution-plan optimization for hello current statement and all downstream statements, be sure tooadd hello hint before hello potential skewed key-wise aggregation.</span></span>

    SKEWFACTOR (columns) = x

    Provides a hint that hello given columns have a skew factor x from 0 (no skew) through 1 (very heavy skew).

<span data-ttu-id="ec22a-151">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="ec22a-151">Code example:</span></span>

    //Add a SKEWFACTOR hint.
    @Impressions =
        SELECT * FROM
        searchDM.SML.PageView(@start, @end) AS PageView
        OPTION(SKEWFACTOR(Query)=0.5)
        ;

    //Query 1 for key: Query, ClientId
    @Sessions =
        SELECT
            ClientId,
            Query,
            SUM(PageClicks) AS Clicks
        FROM
            @Impressions
        GROUP BY
            Query, ClientId
        ;

    //Query 2 for Key: Query
    @Display =
        SELECT * FROM @Sessions
            INNER JOIN @Campaigns
                ON @Sessions.Query == @Campaigns.Query
        ;   

### <a name="option-3-use-rowcount"></a><span data-ttu-id="ec22a-152">Opção 3: Utilizar contagem de linhas</span><span class="sxs-lookup"><span data-stu-id="ec22a-152">Option 3: Use ROWCOUNT</span></span>  
<span data-ttu-id="ec22a-153">Além disso tooSKEWFACTOR, para skewed-chave específica associar casos, se souber que Olá outro conjunto de linhas do associado é pequeno, pode dizer otimizador de Olá adicionando uma sugestão de contagem de linhas na instrução U-SQL de Olá antes de associação.</span><span class="sxs-lookup"><span data-stu-id="ec22a-153">In addition tooSKEWFACTOR, for specific skewed-key join cases, if you know that hello other joined row set is small, you can tell hello optimizer by adding a ROWCOUNT hint in hello U-SQL statement before JOIN.</span></span> <span data-ttu-id="ec22a-154">Desta forma, otimizador pode escolher um toohelp de estratégia de associação de difusão melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="ec22a-154">This way, optimizer can choose a broadcast join strategy toohelp improve performance.</span></span> <span data-ttu-id="ec22a-155">Lembre-se de que a contagem de linhas não resolver o problema de desfasamento de dados de Olá, mas pode oferecer ajuda adicional.</span><span class="sxs-lookup"><span data-stu-id="ec22a-155">Be aware that ROWCOUNT does not resolve hello data-skew problem, but it can offer some additional help.</span></span>

    OPTION(ROWCOUNT = n)

    Identify a small row set before JOIN by providing an estimated integer row count.

<span data-ttu-id="ec22a-156">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="ec22a-156">Code example:</span></span>

    //Unstructured (24-hour daily log impressions)
    @Huge   = EXTRACT ClientId int, ...
                FROM @"wasb://ads@wcentralus/2015/10/30/{*}.nif"
                ;

    //Small subset (that is, ForgetMe opt out)
    @Small  = SELECT * FROM @Huge
                WHERE Bing.ForgetMe(x,y,z)
                OPTION(ROWCOUNT=500)
                ;

    //Result (not enough information toodetermine simple broadcast JOIN)
    @Remove = SELECT * FROM Bing.Sessions
                INNER JOIN @Small ON Sessions.Client == @Small.Client
                ;

## <a name="solution-3-improve-hello-user-defined-reducer-and-combiner"></a><span data-ttu-id="ec22a-157">Solução 3: Melhorar reducer definido pelo utilizador de Olá e combinação</span><span class="sxs-lookup"><span data-stu-id="ec22a-157">Solution 3: Improve hello user-defined reducer and combiner</span></span>

<span data-ttu-id="ec22a-158">Por vezes, pode escrever um toodeal de operador definido pelo utilizador com lógica mais complicada processo e um reducer bem escrito e a combinação podem mitigar um problema de desfasamento de dados em alguns casos.</span><span class="sxs-lookup"><span data-stu-id="ec22a-158">You can sometimes write a user-defined operator toodeal with complicated process logic, and a well-written reducer and combiner might mitigate a data-skew problem in some cases.</span></span>

### <a name="option-1-use-a-recursive-reducer-if-possible"></a><span data-ttu-id="ec22a-159">Opção 1: Utilizar um reducer recursiva, se possível</span><span class="sxs-lookup"><span data-stu-id="ec22a-159">Option 1: Use a recursive reducer, if possible</span></span>

<span data-ttu-id="ec22a-160">Por predefinição, um reducer definido pelo utilizador é executado no modo não recursivo, que significa que reduzem o trabalho para uma chave é distribuída para um único vértice.</span><span class="sxs-lookup"><span data-stu-id="ec22a-160">By default, a user-defined reducer runs in non-recursive mode, which means that reduce work for a key is distributed into a single vertex.</span></span> <span data-ttu-id="ec22a-161">Mas, se os seus dados é skewed, conjuntos de dados enormes Olá possam ser processados no vértice único e execute durante muito tempo.</span><span class="sxs-lookup"><span data-stu-id="ec22a-161">But if your data is skewed, hello huge data sets might be processed in a single vertex and run for a long time.</span></span>

<span data-ttu-id="ec22a-162">desempenho tooimprove, pode adicionar um atributo no seu toorun de reducer toodefine código no modo recursivo.</span><span class="sxs-lookup"><span data-stu-id="ec22a-162">tooimprove performance, you can add an attribute in your code toodefine reducer toorun in recursive mode.</span></span> <span data-ttu-id="ec22a-163">Em seguida, Olá grandes conjuntos de dados podem ser distribuídas toomultiple vértices e executadas em paralelo, que acelera a tarefa.</span><span class="sxs-lookup"><span data-stu-id="ec22a-163">Then, hello huge data sets can be distributed toomultiple vertices and run in parallel, which speeds up your job.</span></span>

<span data-ttu-id="ec22a-164">toochange um toorecursive de reducer não recursiva, terá de se de que o algoritmo associative toomake.</span><span class="sxs-lookup"><span data-stu-id="ec22a-164">toochange a non-recursive reducer toorecursive, you need toomake sure that your algorithm is associative.</span></span> <span data-ttu-id="ec22a-165">Por exemplo, soma Olá é associative e mediana Olá não é.</span><span class="sxs-lookup"><span data-stu-id="ec22a-165">For example, hello sum is associative, and hello median is not.</span></span> <span data-ttu-id="ec22a-166">Terá também de certificar-se de que Olá de entrada e saída para reducer manter Olá toomake mesmo esquema.</span><span class="sxs-lookup"><span data-stu-id="ec22a-166">You also need toomake sure that hello input and output for reducer keep hello same schema.</span></span>

<span data-ttu-id="ec22a-167">Atributo de recursiva reducer:</span><span class="sxs-lookup"><span data-stu-id="ec22a-167">Attribute of recursive reducer:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]

<span data-ttu-id="ec22a-168">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="ec22a-168">Code example:</span></span>

    [SqlUserDefinedReducer(IsRecursive = true)]
    public class TopNReducer : IReducer
    {
        public override IEnumerable<IRow>
            Reduce(IRowset input, IUpdatableRow output)
        {
            //Your reducer code goes here.
        }
    }

### <a name="option-2-use-row-level-combiner-mode-if-possible"></a><span data-ttu-id="ec22a-169">Opção 2: Utilizar o modo de combinação ao nível da linha, se possível</span><span class="sxs-lookup"><span data-stu-id="ec22a-169">Option 2: Use row-level combiner mode, if possible</span></span>

<span data-ttu-id="ec22a-170">Sugestão de contagem de linhas de toohello semelhante para casos de associação de chave skewed específico, o modo de combinação tenta toodistribute grande valor de chave skewed conjuntos toomultiple vértices para que o trabalho Olá pode ser executado em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="ec22a-170">Similar toohello ROWCOUNT hint for specific skewed-key join cases, combiner mode tries toodistribute huge skewed-key value sets toomultiple vertices so that hello work can be executed concurrently.</span></span> <span data-ttu-id="ec22a-171">Modo de combinação não é possível resolver problemas de desfasamento de dados, mas pode oferecer ajuda adicional para conjuntos de valores de chave skewed grande.</span><span class="sxs-lookup"><span data-stu-id="ec22a-171">Combiner mode can’t resolve data-skew issues, but it can offer some additional help for huge skewed-key value sets.</span></span>

<span data-ttu-id="ec22a-172">Por predefinição, o modo de combinação Olá é completo, o que significa que Olá deixado conjunto de linhas e conjunto de linhas à direita não pode ser separado.</span><span class="sxs-lookup"><span data-stu-id="ec22a-172">By default, hello combiner mode is Full, which means that hello left row set and right row set cannot be separated.</span></span> <span data-ttu-id="ec22a-173">Definição de modo de Olá como direito/esquerda/interna permite que a associação ao nível da linha.</span><span class="sxs-lookup"><span data-stu-id="ec22a-173">Setting hello mode as Left/Right/Inner enables row-level join.</span></span> <span data-ttu-id="ec22a-174">sistema de Olá separa conjuntos de linha correspondente Olá e distribui-las em vários vértices que são executadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="ec22a-174">hello system separates hello corresponding row sets and distributes them into multiple vertices that run in parallel.</span></span> <span data-ttu-id="ec22a-175">No entanto, antes de configurar o modo de combinação de Olá, tenha cuidado tooensure Olá conjuntos de linhas correspondentes pode ser separado.</span><span class="sxs-lookup"><span data-stu-id="ec22a-175">However, before you configure hello combiner mode, be careful tooensure that hello corresponding row sets can be separated.</span></span>

<span data-ttu-id="ec22a-176">exemplo de Olá que se segue mostra um conjunto de linhas esquerdo separados.</span><span class="sxs-lookup"><span data-stu-id="ec22a-176">hello example that follows shows a separated left row set.</span></span> <span data-ttu-id="ec22a-177">Cada linha de saída depende de uma única linha de entrada da esquerda Olá e potencialmente depende todas as linhas da Olá à direita com Olá mesmo valor da chave.</span><span class="sxs-lookup"><span data-stu-id="ec22a-177">Each output row depends on a single input row from hello left, and it potentially depends on all rows from hello right with hello same key value.</span></span> <span data-ttu-id="ec22a-178">Se definir o modo de combinação Olá como à esquerda, o sistema Olá separa Olá grande esquerda linha definida para as pequenas e atribui-las toomultiple vértices.</span><span class="sxs-lookup"><span data-stu-id="ec22a-178">If you set hello combiner mode as left, hello system separates hello huge left-row set into small ones and assigns them toomultiple vertices.</span></span>

![Ilustração do modo de combinação](./media/data-lake-analytics-data-lake-tools-data-skew-solutions/combiner-mode-illustration.png)

>[!NOTE]
><span data-ttu-id="ec22a-180">Se definir o modo de combinação errado Olá, combinação Olá é menos eficiente e resultados de Olá poderão estar incorreto.</span><span class="sxs-lookup"><span data-stu-id="ec22a-180">If you set hello wrong combiner mode, hello combination is less efficient, and hello results might be wrong.</span></span>

<span data-ttu-id="ec22a-181">Atributos do modo de combinação de:</span><span class="sxs-lookup"><span data-stu-id="ec22a-181">Attributes of combiner mode:</span></span>

- [SqlUserDefinedCombiner(Mode=CombinerMode.Full)]: Every output row potentially depends on all hello input rows from left and right with hello same key value.

- <span data-ttu-id="ec22a-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Cada linha de saída depende de uma única linha de entrada da esquerda Olá (e, potencialmente, todas as linhas da Olá à direita com Olá mesmo valor da chave).</span><span class="sxs-lookup"><span data-stu-id="ec22a-182">SqlUserDefinedCombiner(Mode=CombinerMode.Left): Every output row depends on a single input row from hello left (and potentially all rows from hello right with hello same key value).</span></span>

- <span data-ttu-id="ec22a-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): cada linha de saída depende de uma única linha de entrada de Olá direito (e, potencialmente, todas as linhas da esquerda Olá com Olá mesmo valor da chave).</span><span class="sxs-lookup"><span data-stu-id="ec22a-183">qlUserDefinedCombiner(Mode=CombinerMode.Right): Every output row depends on a single input row from hello right (and potentially all rows from hello left with hello same key value).</span></span>

- <span data-ttu-id="ec22a-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Cada linha de saída depende de uma única linha de entrada de Olá à esquerda e Olá à direita com Olá mesmo valor.</span><span class="sxs-lookup"><span data-stu-id="ec22a-184">SqlUserDefinedCombiner(Mode=CombinerMode.Inner): Every output row depends on a single input row from hello left and hello right with hello same value.</span></span>

<span data-ttu-id="ec22a-185">Exemplo de código:</span><span class="sxs-lookup"><span data-stu-id="ec22a-185">Code example:</span></span>

    [SqlUserDefinedCombiner(Mode = CombinerMode.Right)]
    public class WatsonDedupCombiner : ICombiner
    {
        public override IEnumerable<IRow>
            Combine(IRowset left, IRowset right, IUpdatableRow output)
        {
        //Your combiner code goes here.
        }
    }
