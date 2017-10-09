---
title: "toouse aaaHow criação de batches de desempenho da aplicação tooimprove SQL Database do Azure"
description: "Olá tópico fornece uma prova que criação de batches de base de dados operações significativamente imroves Olá velocidade e escalabilidade das suas aplicações de base de dados do Azure SQL. Embora estas técnicas de lotes de trabalho para qualquer base de dados do SQL Server, o foco Olá artigo Olá é no Azure."
services: sql-database
documentationcenter: na
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 563862ca-c65a-46f6-975d-10df7ff6aa9c
ms.service: sql-database
ms.custom: develop apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/12/2016
ms.author: sstein
ms.openlocfilehash: 124b203ee69c595f0813852ff09ef9ec6841233a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-batching-tooimprove-sql-database-application-performance"></a><span data-ttu-id="36e1d-104">Como toouse tooimprove de desempenho de aplicações de base de dados SQL de criação de batches</span><span class="sxs-lookup"><span data-stu-id="36e1d-104">How toouse batching tooimprove SQL Database application performance</span></span>
<span data-ttu-id="36e1d-105">Criação de batches de operações tooAzure base de dados SQL significativamente melhora o desempenho de Olá e a escalabilidade das suas aplicações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-105">Batching operations tooAzure SQL Database significantly improves hello performance and scalability of your applications.</span></span> <span data-ttu-id="36e1d-106">Na ordem toounderstand Olá vantagens, indicadas Olá primeira parte deste artigo abrange alguns resultados do teste de exemplo que comparam os pedidos de batches e sequenciais tooa base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-106">In order toounderstand hello benefits, hello first part of this article covers some sample test results that compare sequential and batched requests tooa SQL Database.</span></span> <span data-ttu-id="36e1d-107">Olá resto Olá artigo mostra técnicas Olá, cenários e considerações toohelp toouse de criação de batches com êxito nas suas aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="36e1d-107">hello remainder of hello article shows hello techniques, scenarios, and considerations toohelp you toouse batching successfully in your Azure applications.</span></span>

## <a name="why-is-batching-important-for-sql-database"></a><span data-ttu-id="36e1d-108">Por isso é criação de batches importante para a base de dados SQL?</span><span class="sxs-lookup"><span data-stu-id="36e1d-108">Why is batching important for SQL Database?</span></span>
<span data-ttu-id="36e1d-109">Serviço remoto de tooa chamadas de criação de batches é uma estratégia para aumentar o desempenho e escalabilidade bem conhecida.</span><span class="sxs-lookup"><span data-stu-id="36e1d-109">Batching calls tooa remote service is a well-known strategy for increasing performance and scalability.</span></span> <span data-ttu-id="36e1d-110">Não existe corrigidas interações de tooany os custos com um serviço remoto, como serialização, a transferência de rede e a anulação da serialização de processamento.</span><span class="sxs-lookup"><span data-stu-id="36e1d-110">There are fixed processing costs tooany interactions with a remote service, such as serialization, network transfer, and deserialization.</span></span> <span data-ttu-id="36e1d-111">Empacotamento transações separadas muitos para um único lote minimiza estes custos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-111">Packaging many separate transactions into a single batch minimizes these costs.</span></span>

<span data-ttu-id="36e1d-112">Neste documento, queremos tooexamine várias estratégias de lotes de base de dados SQL e cenários.</span><span class="sxs-lookup"><span data-stu-id="36e1d-112">In this paper, we want tooexamine various SQL Database batching strategies and scenarios.</span></span> <span data-ttu-id="36e1d-113">Embora estas estratégias também são importantes para aplicações no local que utilizam o SQL Server, existem várias razões para Realce a utilização de Olá de criação de batches para a base de dados SQL:</span><span class="sxs-lookup"><span data-stu-id="36e1d-113">Although these strategies are also important for on-premises applications that use SQL Server, there are several reasons for highlighting hello use of batching for SQL Database:</span></span>

* <span data-ttu-id="36e1d-114">Não há potencialmente maior latência de rede no acesso à base de dados do SQL Server, especialmente se estão a aceder à base de dados SQL a partir de fora Olá mesmo centro de dados do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="36e1d-114">There is potentially greater network latency in accessing SQL Database, especially if you are accessing SQL Database from outside hello same Microsoft Azure datacenter.</span></span>
* <span data-ttu-id="36e1d-115">características de multi-inquilino de Olá de meios de base de dados SQL que Olá eficiência de dados de Olá toohello correlaciona de camada de acesso global escalabilidade da base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-115">hello multitenant characteristics of SQL Database means that hello efficiency of hello data access layer correlates toohello overall scalability of hello database.</span></span> <span data-ttu-id="36e1d-116">Base de dados do SQL Server tem a impedir que qualquer utilizador/inquilino único monopolizing detrimento toohello de recursos de base de dados de outros inquilinos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-116">SQL Database must prevent any single tenant/user from monopolizing database resources toohello detriment of other tenants.</span></span> <span data-ttu-id="36e1d-117">Em resposta toousage que excedam quotas predefinidas, base de dados SQL pode reduzir o débito ou responder com exceções de limitação.</span><span class="sxs-lookup"><span data-stu-id="36e1d-117">In response toousage in excess of predefined quotas, SQL Database can reduce throughput or respond with throttling exceptions.</span></span> <span data-ttu-id="36e1d-118">Resulta numa eficiência, tais como a criação de batches, permitem toodo trabalhar mais na base de dados do SQL Server antes de atingir estes limites.</span><span class="sxs-lookup"><span data-stu-id="36e1d-118">Efficiencies, such as batching, enable you toodo more work on SQL Database before reaching these limits.</span></span> 
* <span data-ttu-id="36e1d-119">Criação de batches também é rentável para arquiteturas que utilizem várias bases de dados (fragmentação).</span><span class="sxs-lookup"><span data-stu-id="36e1d-119">Batching is also effective for architectures that use multiple databases (sharding).</span></span> <span data-ttu-id="36e1d-120">eficiência de Olá da sua interação com cada unidade de base de dados ainda é um fator chave a escalabilidade geral.</span><span class="sxs-lookup"><span data-stu-id="36e1d-120">hello efficiency of your interaction with each database unit is still a key factor in your overall scalability.</span></span> 

<span data-ttu-id="36e1d-121">Uma das vantagens de Olá da utilização da base de dados do SQL Server é se não tiver toomanage Olá servidores desse anfitrião Olá da base de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-121">One of hello benefits of using SQL Database is that you don’t have toomanage hello servers that host hello database.</span></span> <span data-ttu-id="36e1d-122">No entanto, esta infraestrutura gerida também significa que tem toothink diferente sobre otimizações de base de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-122">However, this managed infrastructure also means that you have toothink differently about database optimizations.</span></span> <span data-ttu-id="36e1d-123">Já não pode ser tooimprove Olá da base de dados hardware ou na rede de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="36e1d-123">You can no longer look tooimprove hello database hardware or network infrastructure.</span></span> <span data-ttu-id="36e1d-124">Microsoft Azure controla os ambientes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-124">Microsoft Azure controls those environments.</span></span> <span data-ttu-id="36e1d-125">área de principais de Olá que pode controlar é como a sua aplicação interage com base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-125">hello main area that you can control is how your application interacts with SQL Database.</span></span> <span data-ttu-id="36e1d-126">Criação de batches é uma destas otimizações de.</span><span class="sxs-lookup"><span data-stu-id="36e1d-126">Batching is one of these optimizations.</span></span> 

<span data-ttu-id="36e1d-127">Olá primeira parte documento Olá examina várias técnicas de lotes para aplicações de .NET que utilizam a base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-127">hello first part of hello paper examines various batching techniques for .NET applications that use SQL Database.</span></span> <span data-ttu-id="36e1d-128">Olá últimas duas secções abrangem cenários e as diretrizes de lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-128">hello last two sections cover batching guidelines and scenarios.</span></span>

## <a name="batching-strategies"></a><span data-ttu-id="36e1d-129">Estratégias de criação de batches</span><span class="sxs-lookup"><span data-stu-id="36e1d-129">Batching strategies</span></span>
### <a name="note-about-timing-results-in-this-topic"></a><span data-ttu-id="36e1d-130">Tenha em atenção sobre os resultados de temporização neste tópico</span><span class="sxs-lookup"><span data-stu-id="36e1d-130">Note about timing results in this topic</span></span>
> [!NOTE]
> <span data-ttu-id="36e1d-131">Resultados não são benchmarks mas destinam tooshow **desempenho relativo**.</span><span class="sxs-lookup"><span data-stu-id="36e1d-131">Results are not benchmarks but are meant tooshow **relative performance**.</span></span> <span data-ttu-id="36e1d-132">As temporizações baseiam-se uma média de, pelo menos, 10 execuções do teste.</span><span class="sxs-lookup"><span data-stu-id="36e1d-132">Timings are based on an average of at least 10 test runs.</span></span> <span data-ttu-id="36e1d-133">As operações são inserções para uma tabela vazia.</span><span class="sxs-lookup"><span data-stu-id="36e1d-133">Operations are inserts into an empty table.</span></span> <span data-ttu-id="36e1d-134">Estes testes foram medidos pre-V12 e não necessariamente correspondem toothroughput que podem ocorrer numa base de dados V12 utilizando Olá novo [escalões de serviço](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="36e1d-134">These tests were measured pre-V12, and they do not necessarily correspond toothroughput that you might experience in a V12 database using hello new [service tiers](sql-database-service-tiers.md).</span></span> <span data-ttu-id="36e1d-135">benefício de relativo Olá de Olá técnica de criação de batches deve ser semelhante.</span><span class="sxs-lookup"><span data-stu-id="36e1d-135">hello relative benefit of hello batching technique should be similar.</span></span>
> 
> 

### <a name="transactions"></a><span data-ttu-id="36e1d-136">Transações</span><span class="sxs-lookup"><span data-stu-id="36e1d-136">Transactions</span></span>
<span data-ttu-id="36e1d-137">Parece um toobegin uma revisão de criação de batches por debater transações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-137">It seems strange toobegin a review of batching by discussing transactions.</span></span> <span data-ttu-id="36e1d-138">Mas utilize Olá de transações do lado do cliente tem um efeito de lotes do lado do servidor subtis que melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-138">But hello use of client-side transactions has a subtle server-side batching effect that improves performance.</span></span> <span data-ttu-id="36e1d-139">Transações podem ser adicionadas e com apenas algumas linhas de código, para que fornecem um desempenho de tooimprove de forma rápida de operações sequenciais.</span><span class="sxs-lookup"><span data-stu-id="36e1d-139">And transactions can be added with only a few lines of code, so they provide a fast way tooimprove performance of sequential operations.</span></span>

<span data-ttu-id="36e1d-140">Considere o seguinte código c# que contém uma sequência de inserção de Olá e operações numa tabela simple de atualização.</span><span class="sxs-lookup"><span data-stu-id="36e1d-140">Consider hello following C# code that contains a sequence of insert and update operations on a simple table.</span></span>

    List<string> dbOperations = new List<string>();
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 1");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 2");
    dbOperations.Add("update MyTable set mytext = 'updated text' where id = 3");
    dbOperations.Add("insert MyTable values ('new value',1)");
    dbOperations.Add("insert MyTable values ('new value',2)");
    dbOperations.Add("insert MyTable values ('new value',3)");

<span data-ttu-id="36e1d-141">Olá seguir ADO.NET código sequencialmente executa estas operações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-141">hello following ADO.NET code sequentially performs these operations.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();

        foreach(string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn);
            cmd.ExecuteNonQuery();                   
        }
    }

<span data-ttu-id="36e1d-142">Olá melhor forma toooptimize este código é tooimplement alguma forma de criação de batches de lado do cliente destas chamadas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-142">hello best way toooptimize this code is tooimplement some form of client-side batching of these calls.</span></span> <span data-ttu-id="36e1d-143">Mas há um desempenho de Olá tooincrease de forma simples deste código simplesmente envolvendo sequência Olá de chamadas de uma transação.</span><span class="sxs-lookup"><span data-stu-id="36e1d-143">But there is a simple way tooincrease hello performance of this code by simply wrapping hello sequence of calls in a transaction.</span></span> <span data-ttu-id="36e1d-144">Eis Olá código mesmo que utiliza uma transação.</span><span class="sxs-lookup"><span data-stu-id="36e1d-144">Here is hello same code that uses a transaction.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        conn.Open();
        SqlTransaction transaction = conn.BeginTransaction();

        foreach (string commandString in dbOperations)
        {
            SqlCommand cmd = new SqlCommand(commandString, conn, transaction);
            cmd.ExecuteNonQuery();
        }

        transaction.Commit();
    }

<span data-ttu-id="36e1d-145">Transações, na verdade, estão a ser utilizadas em ambos estes exemplos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-145">Transactions are actually being used in both of these examples.</span></span> <span data-ttu-id="36e1d-146">No primeiro exemplo Olá, cada chamada individuais é uma transação implícita.</span><span class="sxs-lookup"><span data-stu-id="36e1d-146">In hello first example, each individual call is an implicit transaction.</span></span> <span data-ttu-id="36e1d-147">No segundo exemplo Olá, uma transação explícita encapsula num wrapper todas as chamadas de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-147">In hello second example, an explicit transaction wraps all of hello calls.</span></span> <span data-ttu-id="36e1d-148">Por documentação Olá Olá [registo de transações de escrita antecipada](https://msdn.microsoft.com/library/ms186259.aspx), registos são libertados toohello disco quando consolida a transação de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-148">Per hello documentation for hello [write-ahead transaction log](https://msdn.microsoft.com/library/ms186259.aspx), log records are flushed toohello disk when hello transaction commits.</span></span> <span data-ttu-id="36e1d-149">Por isso, incluindo chamadas mais de uma transação, hello registo de transações de escrita toohello pode atrasar até Olá transação está consolidada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-149">So by including more calls in a transaction, hello write toohello transaction log can delay until hello transaction is committed.</span></span> <span data-ttu-id="36e1d-150">Em vigor, pretende ativar a criação de batches para registo de transações do servidor de Olá, escritas toohello.</span><span class="sxs-lookup"><span data-stu-id="36e1d-150">In effect, you are enabling batching for hello writes toohello server’s transaction log.</span></span>

<span data-ttu-id="36e1d-151">Olá, a tabela seguinte mostra alguns resultados do teste ad-hoc.</span><span class="sxs-lookup"><span data-stu-id="36e1d-151">hello following table shows some ad-hoc testing results.</span></span> <span data-ttu-id="36e1d-152">testes de Olá realizados Olá que mesmo sequenciais insere com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-152">hello tests performed hello same sequential inserts with and without transactions.</span></span> <span data-ttu-id="36e1d-153">Para obter mais perspetiva, primeiro conjunto de Olá de testes executou remotamente a partir de uma base de dados do computador portátil toohello no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="36e1d-153">For more perspective, hello first set of tests ran remotely from a laptop toohello database in Microsoft Azure.</span></span> <span data-ttu-id="36e1d-154">Olá segundo conjunto de testes executou de um serviço em nuvem e a base de dados que ambos resided dentro Olá mesmo centro de dados do Microsoft Azure (EUA oeste).</span><span class="sxs-lookup"><span data-stu-id="36e1d-154">hello second set of tests ran from a cloud service and database that both resided within hello same Microsoft Azure datacenter (West US).</span></span> <span data-ttu-id="36e1d-155">Olá tabela seguinte mostra a duração de Olá em milissegundos do inserções sequenciais com e sem transações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-155">hello following table shows hello duration in milliseconds of sequential inserts with and without transactions.</span></span>

<span data-ttu-id="36e1d-156">**No local tooAzure**:</span><span class="sxs-lookup"><span data-stu-id="36e1d-156">**On-Premises tooAzure**:</span></span>

| <span data-ttu-id="36e1d-157">Operações</span><span class="sxs-lookup"><span data-stu-id="36e1d-157">Operations</span></span> | <span data-ttu-id="36e1d-158">Nenhuma transação (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-158">No Transaction (ms)</span></span> | <span data-ttu-id="36e1d-159">Transações (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-159">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-160">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-160">1</span></span> |<span data-ttu-id="36e1d-161">130</span><span class="sxs-lookup"><span data-stu-id="36e1d-161">130</span></span> |<span data-ttu-id="36e1d-162">402</span><span class="sxs-lookup"><span data-stu-id="36e1d-162">402</span></span> |
| <span data-ttu-id="36e1d-163">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-163">10</span></span> |<span data-ttu-id="36e1d-164">1208</span><span class="sxs-lookup"><span data-stu-id="36e1d-164">1208</span></span> |<span data-ttu-id="36e1d-165">1226</span><span class="sxs-lookup"><span data-stu-id="36e1d-165">1226</span></span> |
| <span data-ttu-id="36e1d-166">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-166">100</span></span> |<span data-ttu-id="36e1d-167">12662</span><span class="sxs-lookup"><span data-stu-id="36e1d-167">12662</span></span> |<span data-ttu-id="36e1d-168">10395</span><span class="sxs-lookup"><span data-stu-id="36e1d-168">10395</span></span> |
| <span data-ttu-id="36e1d-169">1000</span><span class="sxs-lookup"><span data-stu-id="36e1d-169">1000</span></span> |<span data-ttu-id="36e1d-170">128852</span><span class="sxs-lookup"><span data-stu-id="36e1d-170">128852</span></span> |<span data-ttu-id="36e1d-171">102917</span><span class="sxs-lookup"><span data-stu-id="36e1d-171">102917</span></span> |

<span data-ttu-id="36e1d-172">**TooAzure do Azure (mesmo centro de dados)**:</span><span class="sxs-lookup"><span data-stu-id="36e1d-172">**Azure tooAzure (same datacenter)**:</span></span>

| <span data-ttu-id="36e1d-173">Operações</span><span class="sxs-lookup"><span data-stu-id="36e1d-173">Operations</span></span> | <span data-ttu-id="36e1d-174">Nenhuma transação (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-174">No Transaction (ms)</span></span> | <span data-ttu-id="36e1d-175">Transações (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-175">Transaction (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-176">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-176">1</span></span> |<span data-ttu-id="36e1d-177">21</span><span class="sxs-lookup"><span data-stu-id="36e1d-177">21</span></span> |<span data-ttu-id="36e1d-178">26</span><span class="sxs-lookup"><span data-stu-id="36e1d-178">26</span></span> |
| <span data-ttu-id="36e1d-179">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-179">10</span></span> |<span data-ttu-id="36e1d-180">220</span><span class="sxs-lookup"><span data-stu-id="36e1d-180">220</span></span> |<span data-ttu-id="36e1d-181">56</span><span class="sxs-lookup"><span data-stu-id="36e1d-181">56</span></span> |
| <span data-ttu-id="36e1d-182">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-182">100</span></span> |<span data-ttu-id="36e1d-183">2145</span><span class="sxs-lookup"><span data-stu-id="36e1d-183">2145</span></span> |<span data-ttu-id="36e1d-184">341</span><span class="sxs-lookup"><span data-stu-id="36e1d-184">341</span></span> |
| <span data-ttu-id="36e1d-185">1000</span><span class="sxs-lookup"><span data-stu-id="36e1d-185">1000</span></span> |<span data-ttu-id="36e1d-186">21479</span><span class="sxs-lookup"><span data-stu-id="36e1d-186">21479</span></span> |<span data-ttu-id="36e1d-187">2756</span><span class="sxs-lookup"><span data-stu-id="36e1d-187">2756</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-188">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-188">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-189">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-189">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-190">Com base nos resultados do teste anterior Olá, uma única operação de moldagem de uma transação diminui, na verdade, o desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-190">Based on hello previous test results, wrapping a single operation in a transaction actually decreases performance.</span></span> <span data-ttu-id="36e1d-191">Mas como aumentar o número de Olá de operações dentro de uma transação única, melhoramento de desempenho de Olá torna-se mais marcado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-191">But as you increase hello number of operations within a single transaction, hello performance improvement becomes more marked.</span></span> <span data-ttu-id="36e1d-192">diferença de desempenho de Olá também é mais evidente quando todas as operações de ocorrerem num centro de dados do Olá Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="36e1d-192">hello performance difference is also more noticeable when all operations occur within hello Microsoft Azure datacenter.</span></span> <span data-ttu-id="36e1d-193">Olá uma maior latência da utilização de base de dados SQL do datacenter do Microsoft Azure de Olá exteriores overshadows ganhos de desempenho de Olá da utilização de transações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-193">hello increased latency of using SQL Database from outside hello Microsoft Azure datacenter overshadows hello performance gain of using transactions.</span></span>

<span data-ttu-id="36e1d-194">Embora a utilização de Olá de transações pode aumentar o desempenho, continuar demasiado[observar as melhores práticas para ligações de transações e](https://msdn.microsoft.com/library/ms187484.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e1d-194">Although hello use of transactions can increase performance, continue too[observe best practices for transactions and connections](https://msdn.microsoft.com/library/ms187484.aspx).</span></span> <span data-ttu-id="36e1d-195">Manter transação Olá o mais curta como ligação de base de dados possíveis e fechar Olá após a conclusão do trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-195">Keep hello transaction as short as possible, and close hello database connection after hello work completes.</span></span> <span data-ttu-id="36e1d-196">Olá, utilizando a instrução no exemplo anterior Olá garante que Olá a ligação foi fechada quando blocos de código subsequentes Olá estiver concluída.</span><span class="sxs-lookup"><span data-stu-id="36e1d-196">hello using statement in hello previous example assures that hello connection is closed when hello subsequent code block completes.</span></span>

<span data-ttu-id="36e1d-197">exemplo anterior Olá demonstra que pode adicionar um código ADO.NET tooany transações locais com duas linhas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-197">hello previous example demonstrates that you can add a local transaction tooany ADO.NET code with two lines.</span></span> <span data-ttu-id="36e1d-198">Transações oferecem uma forma rápida de desempenho de Olá tooimprove de código que torna sequencial inserir, atualizar e eliminar operações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-198">Transactions offer a quick way tooimprove hello performance of code that makes sequential insert, update, and delete operations.</span></span> <span data-ttu-id="36e1d-199">No entanto, para um desempenho mais rápido Olá, considere alterar Olá código adicional tootake partido do lado do cliente de criação de batches, tais como parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-199">However, for hello fastest performance, consider changing hello code further tootake advantage of client-side batching, such as table-valued parameters.</span></span>

<span data-ttu-id="36e1d-200">Para obter mais informações sobre transações por ADO.NET, consulte [transações locais em ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span><span class="sxs-lookup"><span data-stu-id="36e1d-200">For more information about transactions in ADO.NET, see [Local Transactions in ADO.NET](https://docs.microsoft.com/dotnet/framework/data/adonet/local-transactions).</span></span>

### <a name="table-valued-parameters"></a><span data-ttu-id="36e1d-201">parâmetros de valor de tabela</span><span class="sxs-lookup"><span data-stu-id="36e1d-201">Table-valued parameters</span></span>
<span data-ttu-id="36e1d-202">Parâmetros de valor de tabela suportam tipos de tabela definido pelo utilizador como parâmetros instruções Transact-SQL, funções e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-202">Table-valued parameters support user-defined table types as parameters in Transact-SQL statements, stored procedures, and functions.</span></span> <span data-ttu-id="36e1d-203">Esta técnica de lotes do lado do cliente permite-lhe toosend várias linhas de dados dentro do parâmetro de valor de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-203">This client-side batching technique allows you toosend multiple rows of data within hello table-valued parameter.</span></span> <span data-ttu-id="36e1d-204">parâmetros de valor de tabela de toouse, defina primeiro um tipo de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-204">toouse table-valued parameters, first define a table type.</span></span> <span data-ttu-id="36e1d-205">Olá a seguinte instrução Transact-SQL cria um tipo de tabela com o nome **MyTableType**.</span><span class="sxs-lookup"><span data-stu-id="36e1d-205">hello following Transact-SQL statement creates a table type named **MyTableType**.</span></span>

    CREATE TYPE MyTableType AS TABLE 
    ( mytext TEXT,
      num INT );


<span data-ttu-id="36e1d-206">No código, crie um **DataTable** com Olá exacta mesmo nomes e tipos de tipo de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-206">In code, you create a **DataTable** with hello exact same names and types of hello table type.</span></span> <span data-ttu-id="36e1d-207">Passar esta **DataTable** num parâmetro de uma consulta de texto ou o procedimento armazenado chamada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-207">Pass this **DataTable** in a parameter in a text query or stored procedure call.</span></span> <span data-ttu-id="36e1d-208">Olá exemplo seguinte mostra esta técnica:</span><span class="sxs-lookup"><span data-stu-id="36e1d-208">hello following example shows this technique:</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        DataTable table = new DataTable();
        // Add columns and rows. hello following is a simple example.
        table.Columns.Add("mytext", typeof(string));
        table.Columns.Add("num", typeof(int));    
        for (var i = 0; i < 10; i++)
        {
            table.Rows.Add(DateTime.Now.ToString(), DateTime.Now.Millisecond);
        }

        SqlCommand cmd = new SqlCommand(
            "INSERT INTO MyTable(mytext, num) SELECT mytext, num FROM @TestTvp",
            connection);

        cmd.Parameters.Add(
            new SqlParameter()
            {
                ParameterName = "@TestTvp",
                SqlDbType = SqlDbType.Structured,
                TypeName = "MyTableType",
                Value = table,
            });

        cmd.ExecuteNonQuery();
    }

<span data-ttu-id="36e1d-209">No exemplo anterior Olá, Olá **SqlCommand** objeto insere linhas de um parâmetro de valor de tabela,  **@TestTvp** .</span><span class="sxs-lookup"><span data-stu-id="36e1d-209">In hello previous example, hello **SqlCommand** object inserts rows from a table-valued parameter, **@TestTvp**.</span></span> <span data-ttu-id="36e1d-210">Olá criado anteriormente **DataTable** objeto está atribuído parâmetro toothis com Olá **SqlCommand.Parameters.Add** método.</span><span class="sxs-lookup"><span data-stu-id="36e1d-210">hello previously created **DataTable** object is assigned toothis parameter with hello **SqlCommand.Parameters.Add** method.</span></span> <span data-ttu-id="36e1d-211">Inserções de Olá lotes de uma chamada significativamente aumenta desempenho Olá através de inserções sequenciais.</span><span class="sxs-lookup"><span data-stu-id="36e1d-211">Batching hello inserts in one call significantly increases hello performance over sequential inserts.</span></span>

<span data-ttu-id="36e1d-212">tooimprove Olá anterior exemplo além disso, utilize um procedimento armazenado em vez de um comando baseado em texto.</span><span class="sxs-lookup"><span data-stu-id="36e1d-212">tooimprove hello previous example further, use a stored procedure instead of a text-based command.</span></span> <span data-ttu-id="36e1d-213">Olá comando Transact-SQL a seguir cria um procedimento armazenado que aceita Olá **SimpleTestTableType** parâmetro de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-213">hello following Transact-SQL command creates a stored procedure that takes hello **SimpleTestTableType** table-valued parameter.</span></span>

    CREATE PROCEDURE [dbo].[sp_InsertRows] 
    @TestTvp as MyTableType READONLY
    AS
    BEGIN
    INSERT INTO MyTable(mytext, num) 
    SELECT mytext, num FROM @TestTvp
    END
    GO

<span data-ttu-id="36e1d-214">Em seguida, altere Olá **SqlCommand** declaração no seguinte de toohello de exemplo Olá anterior código de objeto.</span><span class="sxs-lookup"><span data-stu-id="36e1d-214">Then change hello **SqlCommand** object declaration in hello previous code example toohello following.</span></span>

    SqlCommand cmd = new SqlCommand("sp_InsertRows", connection);
    cmd.CommandType = CommandType.StoredProcedure;

<span data-ttu-id="36e1d-215">Na maioria dos casos, os parâmetros de valor de tabela ter equivalente ou um melhor desempenho do que outras técnicas de lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-215">In most cases, table-valued parameters have equivalent or better performance than other batching techniques.</span></span> <span data-ttu-id="36e1d-216">Parâmetros de valor de tabela são, muitas vezes, preferível, mais flexíveis do que outras opções.</span><span class="sxs-lookup"><span data-stu-id="36e1d-216">Table-valued parameters are often preferable, because they are more flexible than other options.</span></span> <span data-ttu-id="36e1d-217">Por exemplo, outras técnicas, tais como a cópia em massa SQL, apenas permitem a inserção de Olá de linhas novas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-217">For example, other techniques, such as SQL bulk copy, only permit hello insertion of new rows.</span></span> <span data-ttu-id="36e1d-218">Mas com parâmetros de valor de tabela, pode utilizar lógica Olá armazenado procedimento toodetermine que linhas são atualizações e que são insere.</span><span class="sxs-lookup"><span data-stu-id="36e1d-218">But with table-valued parameters, you can use logic in hello stored procedure toodetermine which rows are updates and which are inserts.</span></span> <span data-ttu-id="36e1d-219">tipo de tabela Olá também pode ser modificado toocontain uma coluna de "Operação" que indica se Olá especificadas linha deve ser inserida, atualizada ou eliminada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-219">hello table type can also be modified toocontain an “Operation” column that indicates whether hello specified row should be inserted, updated, or deleted.</span></span>

<span data-ttu-id="36e1d-220">Olá, a tabela seguinte mostra os resultados do teste de ad-hoc para utilização de Olá dos parâmetros de valor de tabela em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-220">hello following table shows ad-hoc test results for hello use of table-valued parameters in milliseconds.</span></span>

| <span data-ttu-id="36e1d-221">Operações</span><span class="sxs-lookup"><span data-stu-id="36e1d-221">Operations</span></span> | <span data-ttu-id="36e1d-222">No local tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-222">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="36e1d-223">Azure mesmo centro de dados (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-223">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-224">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-224">1</span></span> |<span data-ttu-id="36e1d-225">124</span><span class="sxs-lookup"><span data-stu-id="36e1d-225">124</span></span> |<span data-ttu-id="36e1d-226">32</span><span class="sxs-lookup"><span data-stu-id="36e1d-226">32</span></span> |
| <span data-ttu-id="36e1d-227">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-227">10</span></span> |<span data-ttu-id="36e1d-228">131</span><span class="sxs-lookup"><span data-stu-id="36e1d-228">131</span></span> |<span data-ttu-id="36e1d-229">25</span><span class="sxs-lookup"><span data-stu-id="36e1d-229">25</span></span> |
| <span data-ttu-id="36e1d-230">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-230">100</span></span> |<span data-ttu-id="36e1d-231">338</span><span class="sxs-lookup"><span data-stu-id="36e1d-231">338</span></span> |<span data-ttu-id="36e1d-232">51</span><span class="sxs-lookup"><span data-stu-id="36e1d-232">51</span></span> |
| <span data-ttu-id="36e1d-233">1000</span><span class="sxs-lookup"><span data-stu-id="36e1d-233">1000</span></span> |<span data-ttu-id="36e1d-234">2615</span><span class="sxs-lookup"><span data-stu-id="36e1d-234">2615</span></span> |<span data-ttu-id="36e1d-235">382</span><span class="sxs-lookup"><span data-stu-id="36e1d-235">382</span></span> |
| <span data-ttu-id="36e1d-236">10000</span><span class="sxs-lookup"><span data-stu-id="36e1d-236">10000</span></span> |<span data-ttu-id="36e1d-237">23830</span><span class="sxs-lookup"><span data-stu-id="36e1d-237">23830</span></span> |<span data-ttu-id="36e1d-238">3586</span><span class="sxs-lookup"><span data-stu-id="36e1d-238">3586</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-239">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-239">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-240">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-240">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-241">Olá ganhos de desempenho da criação de batches é imediatamente aparente.</span><span class="sxs-lookup"><span data-stu-id="36e1d-241">hello performance gain from batching is immediately apparent.</span></span> <span data-ttu-id="36e1d-242">No teste sequenciais anterior Olá, 1000 demorou segundos 129 Olá exteriores datacenter e segundos 21 num Olá Centro de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-242">In hello previous sequential test, 1000 operations took 129 seconds outside hello datacenter and 21 seconds from within hello datacenter.</span></span> <span data-ttu-id="36e1d-243">Mas com parâmetros de valor de tabela, 1000 operações demorar apenas segundos 2.6 fora do datacenter Olá e 0.4 segundos num Olá Centro de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-243">But with table-valued parameters, 1000 operations take only 2.6 seconds outside hello datacenter and 0.4 seconds within hello datacenter.</span></span>

<span data-ttu-id="36e1d-244">Para obter mais informações sobre os parâmetros de valor de tabela, consulte [Table-Valued parâmetros](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e1d-244">For more information on table-valued parameters, see [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

### <a name="sql-bulk-copy"></a><span data-ttu-id="36e1d-245">Cópia em massa SQL</span><span class="sxs-lookup"><span data-stu-id="36e1d-245">SQL bulk copy</span></span>
<span data-ttu-id="36e1d-246">Cópia em massa SQL é outra forma tooinsert grandes quantidades de dados para uma base de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="36e1d-246">SQL bulk copy is another way tooinsert large amounts of data into a target database.</span></span> <span data-ttu-id="36e1d-247">As aplicações de .NET podem utilizar Olá **SqlBulkCopy** operações de inserção em massa tooperform de classe.</span><span class="sxs-lookup"><span data-stu-id="36e1d-247">.NET applications can use hello **SqlBulkCopy** class tooperform bulk insert operations.</span></span> <span data-ttu-id="36e1d-248">**SqlBulkCopy** é semelhante na ferramenta de linha de comandos toohello função, **Bcp.exe**, ou Olá instrução de Transact-SQL, **inserção em massa**.</span><span class="sxs-lookup"><span data-stu-id="36e1d-248">**SqlBulkCopy** is similar in function toohello command-line tool, **Bcp.exe**, or hello Transact-SQL statement, **BULK INSERT**.</span></span> <span data-ttu-id="36e1d-249">Olá exemplo de código seguinte mostra como toobulk Olá de copiar as linhas da origem de Olá **DataTable**, tabela, a tabela de destino toohello no SQL Server, MyTable.</span><span class="sxs-lookup"><span data-stu-id="36e1d-249">hello following code example shows how toobulk copy hello rows in hello source **DataTable**, table, toohello destination table in SQL Server, MyTable.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        using (SqlBulkCopy bulkCopy = new SqlBulkCopy(connection))
        {
            bulkCopy.DestinationTableName = "MyTable";
            bulkCopy.ColumnMappings.Add("mytext", "mytext");
            bulkCopy.ColumnMappings.Add("num", "num");
            bulkCopy.WriteToServer(table);
        }
    }

<span data-ttu-id="36e1d-250">Existem alguns casos onde cópia em massa é preferencial através de parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-250">There are some cases where bulk copy is preferred over table-valued parameters.</span></span> <span data-ttu-id="36e1d-251">Consulte a tabela de comparação de Olá de Table-Valued parameters versus operações de inserção em massa tópico Olá [Table-Valued parâmetros](https://msdn.microsoft.com/library/bb510489.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e1d-251">See hello comparison table of Table-Valued parameters versus BULK INSERT operations in hello topic [Table-Valued Parameters](https://msdn.microsoft.com/library/bb510489.aspx).</span></span>

<span data-ttu-id="36e1d-252">Olá seguintes resultados de teste do ad-hoc mostram desempenho Olá de criação de batches com **SqlBulkCopy** em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-252">hello following ad-hoc test results show hello performance of batching with **SqlBulkCopy** in milliseconds.</span></span>

| <span data-ttu-id="36e1d-253">Operações</span><span class="sxs-lookup"><span data-stu-id="36e1d-253">Operations</span></span> | <span data-ttu-id="36e1d-254">No local tooAzure (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-254">On-Premises tooAzure (ms)</span></span> | <span data-ttu-id="36e1d-255">Azure mesmo centro de dados (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-255">Azure same datacenter (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-256">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-256">1</span></span> |<span data-ttu-id="36e1d-257">433</span><span class="sxs-lookup"><span data-stu-id="36e1d-257">433</span></span> |<span data-ttu-id="36e1d-258">57</span><span class="sxs-lookup"><span data-stu-id="36e1d-258">57</span></span> |
| <span data-ttu-id="36e1d-259">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-259">10</span></span> |<span data-ttu-id="36e1d-260">441</span><span class="sxs-lookup"><span data-stu-id="36e1d-260">441</span></span> |<span data-ttu-id="36e1d-261">32</span><span class="sxs-lookup"><span data-stu-id="36e1d-261">32</span></span> |
| <span data-ttu-id="36e1d-262">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-262">100</span></span> |<span data-ttu-id="36e1d-263">636</span><span class="sxs-lookup"><span data-stu-id="36e1d-263">636</span></span> |<span data-ttu-id="36e1d-264">53</span><span class="sxs-lookup"><span data-stu-id="36e1d-264">53</span></span> |
| <span data-ttu-id="36e1d-265">1000</span><span class="sxs-lookup"><span data-stu-id="36e1d-265">1000</span></span> |<span data-ttu-id="36e1d-266">2535</span><span class="sxs-lookup"><span data-stu-id="36e1d-266">2535</span></span> |<span data-ttu-id="36e1d-267">341</span><span class="sxs-lookup"><span data-stu-id="36e1d-267">341</span></span> |
| <span data-ttu-id="36e1d-268">10000</span><span class="sxs-lookup"><span data-stu-id="36e1d-268">10000</span></span> |<span data-ttu-id="36e1d-269">21605</span><span class="sxs-lookup"><span data-stu-id="36e1d-269">21605</span></span> |<span data-ttu-id="36e1d-270">2737</span><span class="sxs-lookup"><span data-stu-id="36e1d-270">2737</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-271">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-271">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-272">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-272">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-273">Em tamanhos de lote mais pequenos, parâmetros de valor de tabela de utilização de Olá outperformed Olá **SqlBulkCopy** classe.</span><span class="sxs-lookup"><span data-stu-id="36e1d-273">In smaller batch sizes, hello use table-valued parameters outperformed hello **SqlBulkCopy** class.</span></span> <span data-ttu-id="36e1d-274">No entanto, **SqlBulkCopy** efetuada 12-31% mais rapidamente do que os parâmetros de valor de tabela de testes de Olá de linhas de 1000 e 10 000.</span><span class="sxs-lookup"><span data-stu-id="36e1d-274">However, **SqlBulkCopy** performed 12-31% faster than table-valued parameters for hello tests of 1,000 and 10,000 rows.</span></span> <span data-ttu-id="36e1d-275">Como parâmetros de valor de tabela, **SqlBulkCopy** é uma boa opção para inserções em lote, especialmente quando comparado com desempenho toohello das operações não em lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-275">Like table-valued parameters, **SqlBulkCopy** is a good option for batched inserts, especially when compared toohello performance of non-batched operations.</span></span>

<span data-ttu-id="36e1d-276">Para obter mais informações sobre a cópia em massa no ADO.NET, consulte [operações de cópia em massa no SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e1d-276">For more information on bulk copy in ADO.NET, see [Bulk Copy Operations in SQL Server](https://msdn.microsoft.com/library/7ek5da1a.aspx).</span></span>

### <a name="multiple-row-parameterized-insert-statements"></a><span data-ttu-id="36e1d-277">Instruções parametrizadas inserir várias linhas</span><span class="sxs-lookup"><span data-stu-id="36e1d-277">Multiple-row Parameterized INSERT statements</span></span>
<span data-ttu-id="36e1d-278">Uma alternativa para lotes pequenos é tooconstruct uma grande parametrizadas instrução INSERT que insere várias linhas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-278">One alternative for small batches is tooconstruct a large parameterized INSERT statement that inserts multiple rows.</span></span> <span data-ttu-id="36e1d-279">Olá seguinte exemplo de código demonstra esta técnica.</span><span class="sxs-lookup"><span data-stu-id="36e1d-279">hello following code example demonstrates this technique.</span></span>

    using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
    {
        connection.Open();

        string insertCommand = "INSERT INTO [MyTable] ( mytext, num ) " +
            "VALUES (@p1, @p2), (@p3, @p4), (@p5, @p6), (@p7, @p8), (@p9, @p10)";

        SqlCommand cmd = new SqlCommand(insertCommand, connection);

        for (int i = 1; i <= 10; i += 2)
        {
            cmd.Parameters.Add(new SqlParameter("@p" + i.ToString(), "test"));
            cmd.Parameters.Add(new SqlParameter("@p" + (i+1).ToString(), i));
        }

        cmd.ExecuteNonQuery();
    }


<span data-ttu-id="36e1d-280">Neste exemplo destina o conceito básico de Olá tooshow.</span><span class="sxs-lookup"><span data-stu-id="36e1d-280">This example is meant tooshow hello basic concept.</span></span> <span data-ttu-id="36e1d-281">Um cenário mais realista seria percorrer cadeia de consulta do Olá necessário entidades tooconstruct Olá e parâmetros de comando Olá em simultâneo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-281">A more realistic scenario would loop through hello required entities tooconstruct hello query string and hello command parameters simultaneously.</span></span> <span data-ttu-id="36e1d-282">Está limitado tooa total dos parâmetros de consulta de 2100, pelo que isto limita o número total de Olá de linhas que podem ser processados desta forma.</span><span class="sxs-lookup"><span data-stu-id="36e1d-282">You are limited tooa total of 2100 query parameters, so this limits hello total number of rows that can be processed in this manner.</span></span>

<span data-ttu-id="36e1d-283">Olá seguir desempenho Olá mostrar de resultados de teste de ad-hoc deste tipo de instrução insert em milissegundos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-283">hello following ad-hoc test results show hello performance of this type of insert statement in milliseconds.</span></span>

| <span data-ttu-id="36e1d-284">Operações</span><span class="sxs-lookup"><span data-stu-id="36e1d-284">Operations</span></span> | <span data-ttu-id="36e1d-285">Parâmetros de valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-285">Table-valued parameters (ms)</span></span> | <span data-ttu-id="36e1d-286">INSERÇÃO de instrução única (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-286">Single-statement INSERT (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-287">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-287">1</span></span> |<span data-ttu-id="36e1d-288">32</span><span class="sxs-lookup"><span data-stu-id="36e1d-288">32</span></span> |<span data-ttu-id="36e1d-289">20</span><span class="sxs-lookup"><span data-stu-id="36e1d-289">20</span></span> |
| <span data-ttu-id="36e1d-290">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-290">10</span></span> |<span data-ttu-id="36e1d-291">30</span><span class="sxs-lookup"><span data-stu-id="36e1d-291">30</span></span> |<span data-ttu-id="36e1d-292">25</span><span class="sxs-lookup"><span data-stu-id="36e1d-292">25</span></span> |
| <span data-ttu-id="36e1d-293">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-293">100</span></span> |<span data-ttu-id="36e1d-294">33</span><span class="sxs-lookup"><span data-stu-id="36e1d-294">33</span></span> |<span data-ttu-id="36e1d-295">51</span><span class="sxs-lookup"><span data-stu-id="36e1d-295">51</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-296">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-296">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-297">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-297">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-298">Esta abordagem pode ser ligeiramente mais rápida para lotes são menos de 100 linhas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-298">This approach can be slightly faster for batches that are less than 100 rows.</span></span> <span data-ttu-id="36e1d-299">Embora seja pequena melhoria Olá, esta técnica é outra opção que poderá funcionar corretamente no seu cenário de aplicação específica.</span><span class="sxs-lookup"><span data-stu-id="36e1d-299">Although hello improvement is small, this technique is another option that might work well in your specific application scenario.</span></span>

### <a name="dataadapter"></a><span data-ttu-id="36e1d-300">DataAdapter</span><span class="sxs-lookup"><span data-stu-id="36e1d-300">DataAdapter</span></span>
<span data-ttu-id="36e1d-301">Olá **DataAdapter** classe permite-lhe toomodify um **DataSet** objeto e, em seguida, submeter as alterações de Olá como operações INSERT, UPDATE e DELETE.</span><span class="sxs-lookup"><span data-stu-id="36e1d-301">hello **DataAdapter** class allows you toomodify a **DataSet** object and then submit hello changes as INSERT, UPDATE, and DELETE operations.</span></span> <span data-ttu-id="36e1d-302">Se estiver a utilizar Olá **DataAdapter** desta forma, é importante toonote que separam as chamadas são efetuados para cada operação distinct.</span><span class="sxs-lookup"><span data-stu-id="36e1d-302">If you are using hello **DataAdapter** in this manner, it is important toonote that separate calls are made for each distinct operation.</span></span> <span data-ttu-id="36e1d-303">tooimprove desempenho, utilize Olá **UpdateBatchSize** propriedade toohello diversas operações que deve ser em lotes num momento.</span><span class="sxs-lookup"><span data-stu-id="36e1d-303">tooimprove performance, use hello **UpdateBatchSize** property toohello number of operations that should be batched at a time.</span></span> <span data-ttu-id="36e1d-304">Para obter mais informações, consulte [efetuar Batch operações utilizando DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span><span class="sxs-lookup"><span data-stu-id="36e1d-304">For more information, see [Performing Batch Operations Using DataAdapters](https://msdn.microsoft.com/library/aadf8fk2.aspx).</span></span>

### <a name="entity-framework"></a><span data-ttu-id="36e1d-305">Do Entity framework</span><span class="sxs-lookup"><span data-stu-id="36e1d-305">Entity framework</span></span>
<span data-ttu-id="36e1d-306">Do Entity Framework não suporta atualmente a criação de batches.</span><span class="sxs-lookup"><span data-stu-id="36e1d-306">Entity Framework does not currently support batching.</span></span> <span data-ttu-id="36e1d-307">Os programadores diferentes na Comunidade Olá foi efetuada uma tentativa soluções toodemonstrate, como ignorar Olá **SaveChanges** método.</span><span class="sxs-lookup"><span data-stu-id="36e1d-307">Different developers in hello community have attempted toodemonstrate workarounds, such as override hello **SaveChanges** method.</span></span> <span data-ttu-id="36e1d-308">Mas soluções Olá são normalmente toohello complexa e personalizadas aplicação e o modelo de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-308">But hello solutions are typically complex and customized toohello application and data model.</span></span> <span data-ttu-id="36e1d-309">projeto de codeplex Olá do Entity Framework tem atualmente uma página de debate sobre este pedido de funcionalidade.</span><span class="sxs-lookup"><span data-stu-id="36e1d-309">hello Entity Framework codeplex project currently has a discussion page on this feature request.</span></span> <span data-ttu-id="36e1d-310">tooview este debate, consulte [Design reunião notas - 2 de Agosto de 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span><span class="sxs-lookup"><span data-stu-id="36e1d-310">tooview this discussion, see [Design Meeting Notes - August 2, 2012](http://entityframework.codeplex.com/wikipage?title=Design%20Meeting%20Notes%20-%20August%202%2c%202012).</span></span>

### <a name="xml"></a><span data-ttu-id="36e1d-311">XML</span><span class="sxs-lookup"><span data-stu-id="36e1d-311">XML</span></span>
<span data-ttu-id="36e1d-312">Por questões de exaustividade, iremos sentir que é importante tootalk sobre XML como uma estratégia de lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-312">For completeness, we feel that it is important tootalk about XML as a batching strategy.</span></span> <span data-ttu-id="36e1d-313">No entanto, a utilização de Olá de XML não tem nenhum vantagens através de outros métodos e as desvantagens várias.</span><span class="sxs-lookup"><span data-stu-id="36e1d-313">However, hello use of XML has no advantages over other methods and several disadvantages.</span></span> <span data-ttu-id="36e1d-314">abordagem de Olá é parâmetros tootable valor semelhantes, mas um ficheiro XML ou cadeia é transferida um procedimento tooa armazenado em vez de uma tabela definida pelo utilizador.</span><span class="sxs-lookup"><span data-stu-id="36e1d-314">hello approach is similar tootable-valued parameters, but an XML file or string is passed tooa stored procedure instead of a user-defined table.</span></span> <span data-ttu-id="36e1d-315">procedimento armazenado de Olá analisa comandos Olá no procedimento de Olá armazenado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-315">hello stored procedure parses hello commands in hello stored procedure.</span></span>

<span data-ttu-id="36e1d-316">Existem várias desvantagens toothis abordagem:</span><span class="sxs-lookup"><span data-stu-id="36e1d-316">There are several disadvantages toothis approach:</span></span>

* <span data-ttu-id="36e1d-317">Trabalhar com XML pode ser complicada e propensas ao erro.</span><span class="sxs-lookup"><span data-stu-id="36e1d-317">Working with XML can be cumbersome and error prone.</span></span>
* <span data-ttu-id="36e1d-318">Análise Olá XML na base de dados de Olá pode ser intensivas em CPU.</span><span class="sxs-lookup"><span data-stu-id="36e1d-318">Parsing hello XML on hello database can be CPU-intensive.</span></span>
* <span data-ttu-id="36e1d-319">Na maioria dos casos, este método é mais lento do que os parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-319">In most cases, this method is slower than table-valued parameters.</span></span>

<span data-ttu-id="36e1d-320">Por esta razão, não se recomenda utilizar Olá de XML para consultas de batch.</span><span class="sxs-lookup"><span data-stu-id="36e1d-320">For these reasons, hello use of XML for batch queries is not recommended.</span></span>

## <a name="batching-considerations"></a><span data-ttu-id="36e1d-321">Considerações sobre a criação de batches</span><span class="sxs-lookup"><span data-stu-id="36e1d-321">Batching considerations</span></span>
<span data-ttu-id="36e1d-322">Olá seguintes secções fornece mais orientação para a utilização de Olá de criação de batches em aplicações de base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-322">hello following sections provide more guidance for hello use of batching in SQL Database applications.</span></span>

### <a name="tradeoffs"></a><span data-ttu-id="36e1d-323">Fala</span><span class="sxs-lookup"><span data-stu-id="36e1d-323">Tradeoffs</span></span>
<span data-ttu-id="36e1d-324">Consoante a arquitetura, a criação de batches pode envolver uma variação entre o desempenho e resiliência.</span><span class="sxs-lookup"><span data-stu-id="36e1d-324">Depending on your architecture, batching can involve a tradeoff between performance and resiliency.</span></span> <span data-ttu-id="36e1d-325">Por exemplo, considere o cenário de olá onde a função inesperadamente fica inativo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-325">For example, consider hello scenario where your role unexpectedly goes down.</span></span> <span data-ttu-id="36e1d-326">Se perder a uma linha de dados, o impacto de Olá é inferior ao impacto Olá de perda de um lote de linhas unsubmitted grande.</span><span class="sxs-lookup"><span data-stu-id="36e1d-326">If you lose one row of data, hello impact is smaller than hello impact of losing a large batch of unsubmitted rows.</span></span> <span data-ttu-id="36e1d-327">Não há um maior risco quando a memória intermédia linhas antes de lhes enviar toohello base de dados numa janela de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-327">There is a greater risk when you buffer rows before sending them toohello database in a specified time window.</span></span>

<span data-ttu-id="36e1d-328">Devido a esta compromisso, avalie o tipo de Olá de operações que o batch.</span><span class="sxs-lookup"><span data-stu-id="36e1d-328">Because of this tradeoff, evaluate hello type of operations that you batch.</span></span> <span data-ttu-id="36e1d-329">Batch de forma mais agressiva (lotes maiores e mais intervalos de tempo) com dados seja menos críticos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-329">Batch more aggressively (larger batches and longer time windows) with data that is less critical.</span></span>

### <a name="batch-size"></a><span data-ttu-id="36e1d-330">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="36e1d-330">Batch size</span></span>
<span data-ttu-id="36e1d-331">No nossos testes, normalmente, não havia não lotes de grandes dimensões de toobreaking partido para segmentos mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-331">In our tests, there was typically no advantage toobreaking large batches into smaller chunks.</span></span> <span data-ttu-id="36e1d-332">Na verdade, muitas vezes, esta subdivision resultou no desempenho mais lento ao submeter um único lote grande.</span><span class="sxs-lookup"><span data-stu-id="36e1d-332">In fact, this subdivision often resulted in slower performance than submitting a single large batch.</span></span> <span data-ttu-id="36e1d-333">Por exemplo, considere um cenário onde pretende tooinsert 1000 linhas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-333">For example, consider a scenario where you want tooinsert 1000 rows.</span></span> <span data-ttu-id="36e1d-334">Olá tabela seguinte mostra quanto tempo os parâmetros de valor de tabela toouse tooinsert 1000 linhas quando dividido em lotes mais pequenos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-334">hello following table shows how long it takes toouse table-valued parameters tooinsert 1000 rows when divided into smaller batches.</span></span>

| <span data-ttu-id="36e1d-335">Tamanho do lote</span><span class="sxs-lookup"><span data-stu-id="36e1d-335">Batch size</span></span> | <span data-ttu-id="36e1d-336">Iterações</span><span class="sxs-lookup"><span data-stu-id="36e1d-336">Iterations</span></span> | <span data-ttu-id="36e1d-337">Parâmetros de valor de tabela (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-337">Table-valued parameters (ms)</span></span> |
| --- | --- | --- |
| <span data-ttu-id="36e1d-338">1000</span><span class="sxs-lookup"><span data-stu-id="36e1d-338">1000</span></span> |<span data-ttu-id="36e1d-339">1</span><span class="sxs-lookup"><span data-stu-id="36e1d-339">1</span></span> |<span data-ttu-id="36e1d-340">347</span><span class="sxs-lookup"><span data-stu-id="36e1d-340">347</span></span> |
| <span data-ttu-id="36e1d-341">500</span><span class="sxs-lookup"><span data-stu-id="36e1d-341">500</span></span> |<span data-ttu-id="36e1d-342">2</span><span class="sxs-lookup"><span data-stu-id="36e1d-342">2</span></span> |<span data-ttu-id="36e1d-343">355</span><span class="sxs-lookup"><span data-stu-id="36e1d-343">355</span></span> |
| <span data-ttu-id="36e1d-344">100</span><span class="sxs-lookup"><span data-stu-id="36e1d-344">100</span></span> |<span data-ttu-id="36e1d-345">10</span><span class="sxs-lookup"><span data-stu-id="36e1d-345">10</span></span> |<span data-ttu-id="36e1d-346">465</span><span class="sxs-lookup"><span data-stu-id="36e1d-346">465</span></span> |
| <span data-ttu-id="36e1d-347">50</span><span class="sxs-lookup"><span data-stu-id="36e1d-347">50</span></span> |<span data-ttu-id="36e1d-348">20</span><span class="sxs-lookup"><span data-stu-id="36e1d-348">20</span></span> |<span data-ttu-id="36e1d-349">630</span><span class="sxs-lookup"><span data-stu-id="36e1d-349">630</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-350">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-350">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-351">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-351">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-352">Pode ver que Olá obter o melhor desempenho para 1000 linhas é toosubmit-los ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-352">You can see that hello best performance for 1000 rows is toosubmit them all at once.</span></span> <span data-ttu-id="36e1d-353">Outros testes (não apresentados aqui) surgiu um toobreak ganhos de desempenho pequeno um lote de 10000 linhas em dois lotes de 5000.</span><span class="sxs-lookup"><span data-stu-id="36e1d-353">In other tests (not shown here) there was a small performance gain toobreak a 10000 row batch into two batches of 5000.</span></span> <span data-ttu-id="36e1d-354">Mas o esquema da tabela Olá para estes testes é relativamente simple, pelo que deverá efetuar os testes no seu dados específicos e batch tamanhos tooverify estes findings.</span><span class="sxs-lookup"><span data-stu-id="36e1d-354">But hello table schema for these tests is relatively simple, so you should perform tests on your specific data and batch sizes tooverify these findings.</span></span>

<span data-ttu-id="36e1d-355">Outro fator tooconsider é que, se ficar demasiado grande batch total Olá, base de dados do SQL Server poderá limitar e refuse batch de Olá toocommit.</span><span class="sxs-lookup"><span data-stu-id="36e1d-355">Another factor tooconsider is that if hello total batch becomes too large, SQL Database might throttle and refuse toocommit hello batch.</span></span> <span data-ttu-id="36e1d-356">Para obter melhores resultados Olá, teste toodetermine seu cenário específico se houver um tamanho de lote ideal.</span><span class="sxs-lookup"><span data-stu-id="36e1d-356">For hello best results, test your specific scenario toodetermine if there is an ideal batch size.</span></span> <span data-ttu-id="36e1d-357">Certifique-tamanho de lote Olá configuráveis em tempo de execução tooenable ajustes rápida com base no desempenho ou erros.</span><span class="sxs-lookup"><span data-stu-id="36e1d-357">Make hello batch size configurable at runtime tooenable quick adjustments based on performance or errors.</span></span>

<span data-ttu-id="36e1d-358">Por fim, equilibrar o tamanho do lote de Olá Olá com riscos de Olá associados à criação de batches.</span><span class="sxs-lookup"><span data-stu-id="36e1d-358">Finally, balance hello size of hello batch with hello risks associated with batching.</span></span> <span data-ttu-id="36e1d-359">Se existem erros transitórios ou função Olá falha, considere consequências Olá repetir a operação de Olá ou perda de dados de Olá no lote de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-359">If there are transient errors or hello role fails, consider hello consequences of retrying hello operation or of losing hello data in hello batch.</span></span>

### <a name="parallel-processing"></a><span data-ttu-id="36e1d-360">Processamento paralelo</span><span class="sxs-lookup"><span data-stu-id="36e1d-360">Parallel processing</span></span>
<span data-ttu-id="36e1d-361">E se demorou abordagem Olá de reduzir o tamanho do lote Olá mas utilizados vários threads o tooexecute Olá trabalho?</span><span class="sxs-lookup"><span data-stu-id="36e1d-361">What if you took hello approach of reducing hello batch size but used multiple threads tooexecute hello work?</span></span> <span data-ttu-id="36e1d-362">Novamente, os nossos testes mostrou que vários lotes multithread mais pequeno normalmente a efetuadas worse um único lote maior.</span><span class="sxs-lookup"><span data-stu-id="36e1d-362">Again, our tests showed that several smaller multithreaded batches typically performed worse than a single larger batch.</span></span> <span data-ttu-id="36e1d-363">Olá teste seguinte tenta tooinsert 1000 linhas num ou mais lotes paralelas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-363">hello following test attempts tooinsert 1000 rows in one or more parallel batches.</span></span> <span data-ttu-id="36e1d-364">Este teste mostra como mais lotes em simultâneo, na verdade, diminuir o desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-364">This test shows how more simultaneous batches actually decreased performance.</span></span>

| <span data-ttu-id="36e1d-365">Tamanho do lote [iterações]</span><span class="sxs-lookup"><span data-stu-id="36e1d-365">Batch size [Iterations]</span></span> | <span data-ttu-id="36e1d-366">Dois threads (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-366">Two threads (ms)</span></span> | <span data-ttu-id="36e1d-367">Quatro threads (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-367">Four threads (ms)</span></span> | <span data-ttu-id="36e1d-368">Seis threads (ms)</span><span class="sxs-lookup"><span data-stu-id="36e1d-368">Six threads (ms)</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="36e1d-369">1000 [1]</span><span class="sxs-lookup"><span data-stu-id="36e1d-369">1000 [1]</span></span> |<span data-ttu-id="36e1d-370">277</span><span class="sxs-lookup"><span data-stu-id="36e1d-370">277</span></span> |<span data-ttu-id="36e1d-371">315</span><span class="sxs-lookup"><span data-stu-id="36e1d-371">315</span></span> |<span data-ttu-id="36e1d-372">266</span><span class="sxs-lookup"><span data-stu-id="36e1d-372">266</span></span> |
| <span data-ttu-id="36e1d-373">500 [2]</span><span class="sxs-lookup"><span data-stu-id="36e1d-373">500 [2]</span></span> |<span data-ttu-id="36e1d-374">548</span><span class="sxs-lookup"><span data-stu-id="36e1d-374">548</span></span> |<span data-ttu-id="36e1d-375">278</span><span class="sxs-lookup"><span data-stu-id="36e1d-375">278</span></span> |<span data-ttu-id="36e1d-376">256</span><span class="sxs-lookup"><span data-stu-id="36e1d-376">256</span></span> |
| <span data-ttu-id="36e1d-377">250 [4]</span><span class="sxs-lookup"><span data-stu-id="36e1d-377">250 [4]</span></span> |<span data-ttu-id="36e1d-378">405</span><span class="sxs-lookup"><span data-stu-id="36e1d-378">405</span></span> |<span data-ttu-id="36e1d-379">329</span><span class="sxs-lookup"><span data-stu-id="36e1d-379">329</span></span> |<span data-ttu-id="36e1d-380">265</span><span class="sxs-lookup"><span data-stu-id="36e1d-380">265</span></span> |
| <span data-ttu-id="36e1d-381">100 [10]</span><span class="sxs-lookup"><span data-stu-id="36e1d-381">100 [10]</span></span> |<span data-ttu-id="36e1d-382">488</span><span class="sxs-lookup"><span data-stu-id="36e1d-382">488</span></span> |<span data-ttu-id="36e1d-383">439</span><span class="sxs-lookup"><span data-stu-id="36e1d-383">439</span></span> |<span data-ttu-id="36e1d-384">391</span><span class="sxs-lookup"><span data-stu-id="36e1d-384">391</span></span> |

> [!NOTE]
> <span data-ttu-id="36e1d-385">Resultados não são testes de desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-385">Results are not benchmarks.</span></span> <span data-ttu-id="36e1d-386">Consulte Olá [nota sobre os resultados de temporização neste tópico](#note-about-timing-results-in-this-topic).</span><span class="sxs-lookup"><span data-stu-id="36e1d-386">See hello [note about timing results in this topic](#note-about-timing-results-in-this-topic).</span></span>
> 
> 

<span data-ttu-id="36e1d-387">Existem várias razões possíveis para degradação do desempenho do Olá tooparallelism devida:</span><span class="sxs-lookup"><span data-stu-id="36e1d-387">There are several potential reasons for hello degradation in performance due tooparallelism:</span></span>

* <span data-ttu-id="36e1d-388">Existem várias chamadas de rede em simultâneo em vez de um.</span><span class="sxs-lookup"><span data-stu-id="36e1d-388">There are multiple simultaneous network calls instead of one.</span></span>
* <span data-ttu-id="36e1d-389">Várias operações em relação a uma única tabela podem resultar em contenção e a bloquear.</span><span class="sxs-lookup"><span data-stu-id="36e1d-389">Multiple operations against a single table can result in contention and blocking.</span></span>
* <span data-ttu-id="36e1d-390">Existem sobrecargas associadas multithreading.</span><span class="sxs-lookup"><span data-stu-id="36e1d-390">There are overheads associated with multithreading.</span></span>
* <span data-ttu-id="36e1d-391">despesa Olá abrir várias ligações prevalece sobre o benefício de Olá de processamento paralelo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-391">hello expense of opening multiple connections outweighs hello benefit of parallel processing.</span></span>

<span data-ttu-id="36e1d-392">Se destinar a tabelas diferentes ou bases de dados, é possível toosee algumas desempenho obter com esta estratégia.</span><span class="sxs-lookup"><span data-stu-id="36e1d-392">If you target different tables or databases, it is possible toosee some performance gain with this strategy.</span></span> <span data-ttu-id="36e1d-393">Fragmentação de base de dados ou federações seria um cenário para esta abordagem.</span><span class="sxs-lookup"><span data-stu-id="36e1d-393">Database sharding or federations would be a scenario for this approach.</span></span> <span data-ttu-id="36e1d-394">Fragmentação utiliza várias bases de dados e base de dados de tooeach de dados diferente de rotas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-394">Sharding uses multiple databases and routes different data tooeach database.</span></span> <span data-ttu-id="36e1d-395">Se cada lote pequeno for tooa base de dados diferente, em seguida, efetuar operações de Olá em paralelo pode ser mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="36e1d-395">If each small batch is going tooa different database, then performing hello operations in parallel can be more efficient.</span></span> <span data-ttu-id="36e1d-396">No entanto, Olá ganhos de desempenho não é suficientemente significativa toouse como base Olá de fragmentação de base de dados de toouse uma decisão na sua solução.</span><span class="sxs-lookup"><span data-stu-id="36e1d-396">However, hello performance gain is not significant enough toouse as hello basis for a decision toouse database sharding in your solution.</span></span>

<span data-ttu-id="36e1d-397">Em algumas estruturas, execução paralela de lotes de menores pode resultar na melhor débito de pedidos num sistema com carga.</span><span class="sxs-lookup"><span data-stu-id="36e1d-397">In some designs, parallel execution of smaller batches can result in improved throughput of requests in a system under load.</span></span> <span data-ttu-id="36e1d-398">Neste caso, mesmo que se tooprocess mais rápida, um único lote maior, processamento de lotes de vários em paralelo poderá ser mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="36e1d-398">In this case, even though it is quicker tooprocess a single larger batch, processing multiple batches in parallel might be more efficient.</span></span>

<span data-ttu-id="36e1d-399">Se utilizar a execução paralela, considere controlar Olá de número máximo de threads de trabalho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-399">If you do use parallel execution, consider controlling hello maximum number of worker threads.</span></span> <span data-ttu-id="36e1d-400">Um número mais pequeno poderá resultar em menos contenção e um tempo de execução mais rápido.</span><span class="sxs-lookup"><span data-stu-id="36e1d-400">A smaller number might result in less contention and a faster execution time.</span></span> <span data-ttu-id="36e1d-401">Além disso, considere a carga adicional Olá que isto coloca na base de dados Olá destino nas ligações e transações.</span><span class="sxs-lookup"><span data-stu-id="36e1d-401">Also, consider hello additional load that this places on hello target database both in connections and transactions.</span></span>

### <a name="related-performance-factors"></a><span data-ttu-id="36e1d-402">Fatores de desempenho relacionados</span><span class="sxs-lookup"><span data-stu-id="36e1d-402">Related performance factors</span></span>
<span data-ttu-id="36e1d-403">Documentação de orientação típica no desempenho da base de dados também afeta a criação de batches.</span><span class="sxs-lookup"><span data-stu-id="36e1d-403">Typical guidance on database performance also affects batching.</span></span> <span data-ttu-id="36e1d-404">Por exemplo, inserir desempenho é reduzido para tabelas com uma chave primária grande ou vários índices não em cluster.</span><span class="sxs-lookup"><span data-stu-id="36e1d-404">For example, insert performance is reduced for tables that have a large primary key or many nonclustered indexes.</span></span>

<span data-ttu-id="36e1d-405">Se os parâmetros de valor de tabela utilizam um procedimento armazenado, pode utilizar o comando de Olá **SET NOCOUNT ON** início Olá procedimento Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-405">If table-valued parameters use a stored procedure, you can use hello command **SET NOCOUNT ON** at hello beginning of hello procedure.</span></span> <span data-ttu-id="36e1d-406">Esta declaração suprime retorno Olá de contagem de Olá de linhas de Olá afetado no procedimento de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-406">This statement suppresses hello return of hello count of hello affected rows in hello procedure.</span></span> <span data-ttu-id="36e1d-407">No entanto, nos nossos testes, Olá utilização de **SET NOCOUNT ON** tinha sem qualquer efeito ou diminuir o desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-407">However, in our tests, hello use of **SET NOCOUNT ON** either had no effect or decreased performance.</span></span> <span data-ttu-id="36e1d-408">Olá procedimento armazenado de teste foi simple com um único **inserir** comando a partir do parâmetro de valor de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-408">hello test stored procedure was simple with a single **INSERT** command from hello table-valued parameter.</span></span> <span data-ttu-id="36e1d-409">É possível que mais complexos procedimentos armazenados seriam beneficiar esta instrução.</span><span class="sxs-lookup"><span data-stu-id="36e1d-409">It is possible that more complex stored procedures would benefit from this statement.</span></span> <span data-ttu-id="36e1d-410">Mas não parta do princípio que adicionar **SET NOCOUNT ON** tooyour armazenado procedimento automaticamente melhora o desempenho.</span><span class="sxs-lookup"><span data-stu-id="36e1d-410">But don’t assume that adding **SET NOCOUNT ON** tooyour stored procedure automatically improves performance.</span></span> <span data-ttu-id="36e1d-411">toounderstand Olá efeito, testar o procedimento armazenado com e sem Olá **SET NOCOUNT ON** instrução.</span><span class="sxs-lookup"><span data-stu-id="36e1d-411">toounderstand hello effect, test your stored procedure with and without hello **SET NOCOUNT ON** statement.</span></span>

## <a name="batching-scenarios"></a><span data-ttu-id="36e1d-412">Cenários de criação de batches</span><span class="sxs-lookup"><span data-stu-id="36e1d-412">Batching scenarios</span></span>
<span data-ttu-id="36e1d-413">Olá secções seguintes descrevem como parâmetros de valor de tabela toouse em três cenários de aplicação.</span><span class="sxs-lookup"><span data-stu-id="36e1d-413">hello following sections describe how toouse table-valued parameters in three application scenarios.</span></span> <span data-ttu-id="36e1d-414">cenário primeiro Olá mostra como colocação em memória intermédia e criação de batches podem trabalhar em conjunto.</span><span class="sxs-lookup"><span data-stu-id="36e1d-414">hello first scenario shows how buffering and batching can work together.</span></span> <span data-ttu-id="36e1d-415">cenário segundo Olá melhora o desempenho efetuando o detalhe do mestre de operações numa chamada de procedimento armazenado único.</span><span class="sxs-lookup"><span data-stu-id="36e1d-415">hello second scenario improves performance by performing master-detail operations in a single stored procedure call.</span></span> <span data-ttu-id="36e1d-416">Olá final cenário mostra como toouse parâmetros de valor de tabela numa operação "UPSERT".</span><span class="sxs-lookup"><span data-stu-id="36e1d-416">hello final scenario shows how toouse table-valued parameters in an “UPSERT” operation.</span></span>

### <a name="buffering"></a><span data-ttu-id="36e1d-417">Colocação em memória intermédia</span><span class="sxs-lookup"><span data-stu-id="36e1d-417">Buffering</span></span>
<span data-ttu-id="36e1d-418">Apesar de existirem alguns cenários que são candidatos óbvios de criação de batches, há muitos cenários que podem tirar partido da criação de batches pelo processamento atrasado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-418">Although there are some scenarios that are obvious candidate for batching, there are many scenarios that could take advantage of batching by delayed processing.</span></span> <span data-ttu-id="36e1d-419">No entanto, também processar atrasada acarreta um maior risco que há perdidos de dados de Olá no evento Olá de uma falha inesperada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-419">However, delayed processing also carries a greater risk that hello data is lost in hello event of an unexpected failure.</span></span> <span data-ttu-id="36e1d-420">É importante toounderstand este risco e considere consequências Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-420">It is important toounderstand this risk and consider hello consequences.</span></span>

<span data-ttu-id="36e1d-421">Por exemplo, considere uma aplicação web que controla o histórico de navegação de Olá de cada utilizador.</span><span class="sxs-lookup"><span data-stu-id="36e1d-421">For example, consider a web application that tracks hello navigation history of each user.</span></span> <span data-ttu-id="36e1d-422">Em cada pedido de página aplicação Olá foi possível efetuar a vista de página de base de dados chamada toorecord Olá do utilizador.</span><span class="sxs-lookup"><span data-stu-id="36e1d-422">On each page request, hello application could make a database call toorecord hello user’s page view.</span></span> <span data-ttu-id="36e1d-423">Mas, mais elevado desempenho e escalabilidade podem ser conseguidos através da memória intermédia de atividades de navegação dos utilizadores Olá e, em seguida, enviar esta base de dados de toohello dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-423">But higher performance and scalability can be achieved by buffering hello users’ navigation activities and then sending this data toohello database in batches.</span></span> <span data-ttu-id="36e1d-424">Pode acionar a atualização de base de dados de Olá por tempo decorrido e/ou tamanho da memória intermédia.</span><span class="sxs-lookup"><span data-stu-id="36e1d-424">You can trigger hello database update by elapsed time and/or buffer size.</span></span> <span data-ttu-id="36e1d-425">Por exemplo, uma regra de especificar que esse batch Olá deve ser processada após 20 segundos ou quando a memória intermédia de Olá atinge 1000 itens.</span><span class="sxs-lookup"><span data-stu-id="36e1d-425">For example, a rule could specify that hello batch should be processed after 20 seconds or when hello buffer reaches 1000 items.</span></span>

<span data-ttu-id="36e1d-426">seguinte Olá código de exemplo utiliza [extensões reativa - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess colocado na memória intermédia eventos gerados por uma classe de monitorização.</span><span class="sxs-lookup"><span data-stu-id="36e1d-426">hello following code example uses [Reactive Extensions - Rx](https://msdn.microsoft.com/data/gg577609) tooprocess buffered events raised by a monitoring class.</span></span> <span data-ttu-id="36e1d-427">Olá quando a memória intermédia preenche ou um tempo limite for atingido, lote de Olá dos dados de utilizador é enviado toohello base de dados com um parâmetro de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-427">When hello buffer fills or a timeout is reached, hello batch of user data is sent toohello database with a table-valued parameter.</span></span>

<span data-ttu-id="36e1d-428">Olá os detalhes de navegação de utilizador modelos Olá NavHistoryData classe.</span><span class="sxs-lookup"><span data-stu-id="36e1d-428">hello following NavHistoryData class models hello user navigation details.</span></span> <span data-ttu-id="36e1d-429">Contém informações básicas, tais como o identificador de utilizador Olá, Olá URL acedidos e Olá tempo de acesso.</span><span class="sxs-lookup"><span data-stu-id="36e1d-429">It contains basic information such as hello user identifier, hello URL accessed, and hello access time.</span></span>

    public class NavHistoryData
    {
        public NavHistoryData(int userId, string url, DateTime accessTime)
        { UserId = userId; URL = url; AccessTime = accessTime; }
        public int UserId { get; set; }
        public string URL { get; set; }
        public DateTime AccessTime { get; set; }
    }

<span data-ttu-id="36e1d-430">Olá NavHistoryDataMonitor classe é responsável pela base de dados do Olá utilizador navegação dados toohello da memória intermédia.</span><span class="sxs-lookup"><span data-stu-id="36e1d-430">hello NavHistoryDataMonitor class is responsible for buffering hello user navigation data toohello database.</span></span> <span data-ttu-id="36e1d-431">Contém um método, RecordUserNavigationEntry, que responde ao gerar uma **OnAdded** eventos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-431">It contains a method, RecordUserNavigationEntry, which responds by raising an **OnAdded** event.</span></span> <span data-ttu-id="36e1d-432">Olá código seguinte mostra lógica de construtor de Olá que utiliza Rx toocreate uma coleção observable com base em eventos de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-432">hello following code shows hello constructor logic that uses Rx toocreate an observable collection based on hello event.</span></span> <span data-ttu-id="36e1d-433">Em seguida, subscreve coleção observable toothis com o método de memória intermédia de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-433">It then subscribes toothis observable collection with hello Buffer method.</span></span> <span data-ttu-id="36e1d-434">sobrecarga Olá Especifica que memória intermédia Olá deve ser enviada cada 20 segundos ou entradas de 1000.</span><span class="sxs-lookup"><span data-stu-id="36e1d-434">hello overload specifies that hello buffer should be sent every 20 seconds or 1000 entries.</span></span>

    public NavHistoryDataMonitor()
    {
        var observableData =
            Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

        observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
    }

<span data-ttu-id="36e1d-435">processador Olá converte todos os itens de Olá colocado na memória intermédia de um tipo de valor de tabela e, em seguida, passa este procedimento tooa armazenado do tipo que batch Olá de processos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-435">hello handler converts all of hello buffered items into a table-valued type and then passes this type tooa stored procedure that processes hello batch.</span></span> <span data-ttu-id="36e1d-436">Olá código seguinte mostra Olá concluir definição Olá NavHistoryDataEventArgs e classes de NavHistoryDataMonitor Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-436">hello following code shows hello complete definition for both hello NavHistoryDataEventArgs and hello NavHistoryDataMonitor classes.</span></span>

    public class NavHistoryDataEventArgs : System.EventArgs
    {
        public NavHistoryDataEventArgs(NavHistoryData data) { Data = data; }
        public NavHistoryData Data { get; set; }
    }

    public class NavHistoryDataMonitor
    {
        public event EventHandler<NavHistoryDataEventArgs> OnAdded;

        public NavHistoryDataMonitor()
        {
            var observableData =
                Observable.FromEventPattern<NavHistoryDataEventArgs>(this, "OnAdded");

            observableData.Buffer(TimeSpan.FromSeconds(20), 1000).Subscribe(Handler);           
        }

        public void RecordUserNavigationEntry(NavHistoryData data)
        {    
            if (OnAdded != null)
                OnAdded(this, new NavHistoryDataEventArgs(data));
        }

        protected void Handler(IList<EventPattern<NavHistoryDataEventArgs>> items)
        {
            DataTable navHistoryBatch = new DataTable("NavigationHistoryBatch");
            navHistoryBatch.Columns.Add("UserId", typeof(int));
            navHistoryBatch.Columns.Add("URL", typeof(string));
            navHistoryBatch.Columns.Add("AccessTime", typeof(DateTime));
            foreach (EventPattern<NavHistoryDataEventArgs> item in items)
            {
                NavHistoryData data = item.EventArgs.Data;
                navHistoryBatch.Rows.Add(data.UserId, data.URL, data.AccessTime);
            }

            using (SqlConnection connection = new SqlConnection(CloudConfigurationManager.GetSetting("Sql.ConnectionString")))
            {
                connection.Open();

                SqlCommand cmd = new SqlCommand("sp_RecordUserNavigation", connection);
                cmd.CommandType = CommandType.StoredProcedure;

                cmd.Parameters.Add(
                    new SqlParameter()
                    {
                        ParameterName = "@NavHistoryBatch",
                        SqlDbType = SqlDbType.Structured,
                        TypeName = "NavigationHistoryTableType",
                        Value = navHistoryBatch,
                    });

                cmd.ExecuteNonQuery();
            }
        }
    }

<span data-ttu-id="36e1d-437">toouse esta classe buffering, aplicação Olá cria um objeto de NavHistoryDataMonitor estático.</span><span class="sxs-lookup"><span data-stu-id="36e1d-437">toouse this buffering class, hello application creates a static NavHistoryDataMonitor object.</span></span> <span data-ttu-id="36e1d-438">Sempre que um utilizador acede a uma página aplicação Olá chama o método de NavHistoryDataMonitor.RecordUserNavigationEntry Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-438">Each time a user accesses a page, hello application calls hello NavHistoryDataMonitor.RecordUserNavigationEntry method.</span></span> <span data-ttu-id="36e1d-439">Olá, colocação em memória intermédia lógica prossegue tootake care of a enviar de base de dados de toohello estas entradas em lotes.</span><span class="sxs-lookup"><span data-stu-id="36e1d-439">hello buffering logic proceeds tootake care of sending these entries toohello database in batches.</span></span>

### <a name="master-detail"></a><span data-ttu-id="36e1d-440">Detalhe de principal</span><span class="sxs-lookup"><span data-stu-id="36e1d-440">Master detail</span></span>
<span data-ttu-id="36e1d-441">Parâmetros de valor de tabela são úteis para cenários de inserção simples.</span><span class="sxs-lookup"><span data-stu-id="36e1d-441">Table-valued parameters are useful for simple INSERT scenarios.</span></span> <span data-ttu-id="36e1d-442">No entanto, pode ser mais difícil inserções toobatch que envolvem mais do que uma tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-442">However, it can be more challenging toobatch inserts that involve more than one table.</span></span> <span data-ttu-id="36e1d-443">cenário de "mestre/Detalhes" Olá é um bom exemplo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-443">hello “master/detail” scenario is a good example.</span></span> <span data-ttu-id="36e1d-444">tabela principal Olá identifica entidade principal Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-444">hello master table identifies hello primary entity.</span></span> <span data-ttu-id="36e1d-445">Uma ou mais tabelas de detalhe armazenam mais dados sobre a entidade de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-445">One or more detail tables store more data about hello entity.</span></span> <span data-ttu-id="36e1d-446">Neste cenário, as relações de chave externas Impor relação Olá da entidade principal do detalhes tooa exclusivo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-446">In this scenario, foreign key relationships enforce hello relationship of details tooa unique master entity.</span></span> <span data-ttu-id="36e1d-447">Considere uma versão simplificada da tabela PurchaseOrder e a respetiva tabela de OrderDetail associada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-447">Consider a simplified version of a PurchaseOrder table and its associated OrderDetail table.</span></span> <span data-ttu-id="36e1d-448">Olá Transact-SQL a seguir cria tabela de PurchaseOrder Olá com quatro colunas: OrderID, OrderDate, CustomerID e estado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-448">hello following Transact-SQL creates hello PurchaseOrder table with four columns: OrderID, OrderDate, CustomerID, and Status.</span></span>

    CREATE TABLE [dbo].[PurchaseOrder](
    [OrderID] [int] IDENTITY(1,1) NOT NULL,
    [OrderDate] [datetime] NOT NULL,
    [CustomerID] [int] NOT NULL,
    [Status] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrder] 
    PRIMARY KEY CLUSTERED ( [OrderID] ASC ))

<span data-ttu-id="36e1d-449">Cada ordem contém um ou mais compras de produto.</span><span class="sxs-lookup"><span data-stu-id="36e1d-449">Each order contains one or more product purchases.</span></span> <span data-ttu-id="36e1d-450">Esta informação é capturada na tabela de PurchaseOrderDetail Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-450">This information is captured in hello PurchaseOrderDetail table.</span></span> <span data-ttu-id="36e1d-451">Olá seguir Transact-SQL cria tabela de PurchaseOrderDetail Olá com cinco colunas: OrderID, OrderDetailID, ProductID, UnitPrice e OrderQty.</span><span class="sxs-lookup"><span data-stu-id="36e1d-451">hello following Transact-SQL creates hello PurchaseOrderDetail table with five columns: OrderID, OrderDetailID, ProductID, UnitPrice, and OrderQty.</span></span>

    CREATE TABLE [dbo].[PurchaseOrderDetail](
    [OrderID] [int] NOT NULL,
    [OrderDetailID] [int] IDENTITY(1,1) NOT NULL,
    [ProductID] [int] NOT NULL,
    [UnitPrice] [money] NULL,
    [OrderQty] [smallint] NULL,
     CONSTRAINT [PrimaryKey_PurchaseOrderDetail] PRIMARY KEY CLUSTERED 
    ( [OrderID] ASC, [OrderDetailID] ASC ))

<span data-ttu-id="36e1d-452">coluna de OrderID Olá na tabela de PurchaseOrderDetail Olá tem de referenciar uma ordem da tabela de PurchaseOrder Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-452">hello OrderID column in hello PurchaseOrderDetail table must reference an order from hello PurchaseOrder table.</span></span> <span data-ttu-id="36e1d-453">Olá seguinte definição de uma chave externa impõe esta restrição.</span><span class="sxs-lookup"><span data-stu-id="36e1d-453">hello following definition of a foreign key enforces this constraint.</span></span>

    ALTER TABLE [dbo].[PurchaseOrderDetail]  WITH CHECK ADD 
    CONSTRAINT [FK_OrderID_PurchaseOrder] FOREIGN KEY([OrderID])
    REFERENCES [dbo].[PurchaseOrder] ([OrderID])

<span data-ttu-id="36e1d-454">Nos parâmetros de valor de tabela de toouse de ordem, tem de ter um tipo de tabela definido pelo utilizador para cada tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="36e1d-454">In order toouse table-valued parameters, you must have one user-defined table type for each target table.</span></span>

    CREATE TYPE PurchaseOrderTableType AS TABLE 
    ( OrderID INT,
      OrderDate DATETIME,
      CustomerID INT,
      Status NVARCHAR(50) );
    GO

    CREATE TYPE PurchaseOrderDetailTableType AS TABLE 
    ( OrderID INT,
      ProductID INT,
      UnitPrice MONEY,
      OrderQty SMALLINT );
    GO

<span data-ttu-id="36e1d-455">Em seguida, defina um procedimento armazenado que aceita tabelas destes tipos.</span><span class="sxs-lookup"><span data-stu-id="36e1d-455">Then define a stored procedure that accepts tables of these types.</span></span> <span data-ttu-id="36e1d-456">Este procedimento permite que um lote de toolocally aplicação um conjunto de encomendas pendentes e detalhes da encomenda numa única chamada.</span><span class="sxs-lookup"><span data-stu-id="36e1d-456">This procedure allows an application toolocally batch a set of orders and order details in a single call.</span></span> <span data-ttu-id="36e1d-457">Olá Transact-SQL seguinte fornece Olá declaração de procedimento armazenado concluído para este exemplo de ordem de compra.</span><span class="sxs-lookup"><span data-stu-id="36e1d-457">hello following Transact-SQL provides hello complete stored procedure declaration for this purchase order example.</span></span>

    CREATE PROCEDURE sp_InsertOrdersBatch (
    @orders as PurchaseOrderTableType READONLY,
    @details as PurchaseOrderDetailTableType READONLY )
    AS
    SET NOCOUNT ON;

    -- Table that connects hello order identifiers in hello @orders
    -- table with hello actual order identifiers in hello PurchaseOrder table
    DECLARE @IdentityLink AS TABLE ( 
    SubmittedKey int, 
    ActualKey int, 
    RowNumber int identity(1,1)
    );

          -- Add new orders toohello PurchaseOrder table, storing hello actual
    -- order identifiers in hello @IdentityLink table   
    INSERT INTO PurchaseOrder ([OrderDate], [CustomerID], [Status])
    OUTPUT inserted.OrderID INTO @IdentityLink (ActualKey)
    SELECT [OrderDate], [CustomerID], [Status] FROM @orders ORDER BY OrderID;

    -- Match hello passed-in order identifiers with hello actual identifiers
    -- and complete hello @IdentityLink table for use with inserting hello details
    WITH OrderedRows As (
    SELECT OrderID, ROW_NUMBER () OVER (ORDER BY OrderID) As RowNumber 
    FROM @orders
    )
    UPDATE @IdentityLink SET SubmittedKey = M.OrderID
    FROM @IdentityLink L JOIN OrderedRows M ON L.RowNumber = M.RowNumber;

    -- Insert hello order details into hello PurchaseOrderDetail table, 
          -- using hello actual order identifiers of hello master table, PurchaseOrder
    INSERT INTO PurchaseOrderDetail (
    [OrderID],
    [ProductID],
    [UnitPrice],
    [OrderQty] )
    SELECT L.ActualKey, D.ProductID, D.UnitPrice, D.OrderQty
    FROM @details D
    JOIN @IdentityLink L ON L.SubmittedKey = D.OrderID;
    GO

<span data-ttu-id="36e1d-458">Neste exemplo, Olá definida localmente @IdentityLink tabela armazena Olá OrderID os valores reais de linhas de Olá recentemente inserida.</span><span class="sxs-lookup"><span data-stu-id="36e1d-458">In this example, hello locally defined @IdentityLink table stores hello actual OrderID values from hello newly inserted rows.</span></span> <span data-ttu-id="36e1d-459">Estes identificadores de ordem são diferentes das Olá temporários OrderID valores Olá @orders e @details parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-459">These order identifiers are different from hello temporary OrderID values in hello @orders and @details table-valued parameters.</span></span> <span data-ttu-id="36e1d-460">Por este motivo, Olá @IdentityLink tabela, em seguida, liga-se os valores de OrderID Olá de Olá @orders toohello reais OrderID os valores de parâmetros para novas linhas de Olá na tabela de PurchaseOrder Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-460">For this reason, hello @IdentityLink table then connects hello OrderID values from hello @orders parameter toohello real OrderID values for hello new rows in hello PurchaseOrder table.</span></span> <span data-ttu-id="36e1d-461">Após este passo, Olá @IdentityLink tabela pode facilitar inserir detalhes da encomenda Olá com Olá OrderID real que satisfaz a restrição de chave externa Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-461">After this step, hello @IdentityLink table can facilitate inserting hello order details with hello actual OrderID that satisfies hello foreign key constraint.</span></span>

<span data-ttu-id="36e1d-462">Este procedimento armazenado pode ser utilizado a partir do código ou a partir de outras chamadas de Transact-SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-462">This stored procedure can be used from code or from other Transact-SQL calls.</span></span> <span data-ttu-id="36e1d-463">Consulte a secção de parâmetros de valor de tabela de Olá deste documento para obter um exemplo de código.</span><span class="sxs-lookup"><span data-stu-id="36e1d-463">See hello table-valued parameters section of this paper for a code example.</span></span> <span data-ttu-id="36e1d-464">Olá Transact-SQL a seguir mostra como toocall Olá sp_InsertOrdersBatch.</span><span class="sxs-lookup"><span data-stu-id="36e1d-464">hello following Transact-SQL shows how toocall hello sp_InsertOrdersBatch.</span></span>

    declare @orders as PurchaseOrderTableType
    declare @details as PurchaseOrderDetailTableType

    INSERT @orders 
    ([OrderID], [OrderDate], [CustomerID], [Status])
    VALUES(1, '1/1/2013', 1125, 'Complete'),
    (2, '1/13/2013', 348, 'Processing'),
    (3, '1/12/2013', 2504, 'Shipped')

    INSERT @details
    ([OrderID], [ProductID], [UnitPrice], [OrderQty])
    VALUES(1, 10, $11.50, 1),
    (1, 12, $1.58, 1),
    (2, 23, $2.57, 2),
    (3, 4, $10.00, 1)

    exec sp_InsertOrdersBatch @orders, @details

<span data-ttu-id="36e1d-465">Esta solução permite toouse cada lote de um conjunto de valores de OrderID que começam em 1.</span><span class="sxs-lookup"><span data-stu-id="36e1d-465">This solution allows each batch toouse a set of OrderID values that begin at 1.</span></span> <span data-ttu-id="36e1d-466">Estes valores OrderID temporários descrevem as relações de Olá no lote de Olá, mas são determinados valores de OrderID reais Olá momento Olá da operação de inserção de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-466">These temporary OrderID values describe hello relationships in hello batch, but hello actual OrderID values are determined at hello time of hello insert operation.</span></span> <span data-ttu-id="36e1d-467">Pode executar Olá instruções mesmas no exemplo anterior Olá repetidamente e gerar as ordens exclusivas na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-467">You can run hello same statements in hello previous example repeatedly and generate unique orders in hello database.</span></span> <span data-ttu-id="36e1d-468">Por este motivo, considere adicionar mais lógica código ou a base de dados, que impede as ordens duplicadas quando utilizar esta técnica de criação de batches.</span><span class="sxs-lookup"><span data-stu-id="36e1d-468">For this reason, consider adding more code or database logic that prevents duplicate orders when using this batching technique.</span></span>

<span data-ttu-id="36e1d-469">Este exemplo demonstra que podem ser em ainda mais complexas operações de base de dados, tais como de detalhe do mestre de operações, de lotes utilizando os parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-469">This example demonstrates that even more complex database operations, such as master-detail operations, can be batched using table-valued parameters.</span></span>

### <a name="upsert"></a><span data-ttu-id="36e1d-470">UPSERT</span><span class="sxs-lookup"><span data-stu-id="36e1d-470">UPSERT</span></span>
<span data-ttu-id="36e1d-471">Outro cenário lotes envolve em simultâneo atualizar linhas existentes e inserir novas linhas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-471">Another batching scenario involves simultaneously updating existing rows and inserting new rows.</span></span> <span data-ttu-id="36e1d-472">Esta operação é por vezes, referidos tooas uma operação de "UPSERT" (atualização + insert).</span><span class="sxs-lookup"><span data-stu-id="36e1d-472">This operation is sometimes referred tooas an “UPSERT” (update + insert) operation.</span></span> <span data-ttu-id="36e1d-473">Em vez de efetuar chamadas separado tooINSERT e a ATUALIZAÇÃO, a instrução de intercalação de Olá é melhor se adequam toothis tarefas.</span><span class="sxs-lookup"><span data-stu-id="36e1d-473">Rather than making separate calls tooINSERT and UPDATE, hello MERGE statement is best suited toothis task.</span></span> <span data-ttu-id="36e1d-474">Olá instrução MERGE pode executar ambos os insert e operações numa única chamada de atualização.</span><span class="sxs-lookup"><span data-stu-id="36e1d-474">hello MERGE statement can perform both insert and update operations in a single call.</span></span>

<span data-ttu-id="36e1d-475">Parâmetros de valor de tabela podem ser utilizados com Olá intercalação instrução tooperform atualiza e inserções.</span><span class="sxs-lookup"><span data-stu-id="36e1d-475">Table-valued parameters can be used with hello MERGE statement tooperform updates and inserts.</span></span> <span data-ttu-id="36e1d-476">Por exemplo, considere uma tabela de empregado simplificada que contém Olá seguintes colunas: campo IDdeEmpregado, nome próprio, apelido, SocialSecurityNumber:</span><span class="sxs-lookup"><span data-stu-id="36e1d-476">For example, consider a simplified Employee table that contains hello following columns: EmployeeID, FirstName, LastName, SocialSecurityNumber:</span></span>

    CREATE TABLE [dbo].[Employee](
    [EmployeeID] [int] IDENTITY(1,1) NOT NULL,
    [FirstName] [nvarchar](50) NOT NULL,
    [LastName] [nvarchar](50) NOT NULL,
    [SocialSecurityNumber] [nvarchar](50) NOT NULL,
     CONSTRAINT [PrimaryKey_Employee] PRIMARY KEY CLUSTERED 
    ([EmployeeID] ASC ))

<span data-ttu-id="36e1d-477">Neste exemplo, pode utilizar o facto de Olá que esse Olá SocialSecurityNumber é exclusivo tooperform uma intercalação das várias empregados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-477">In this example, you can use hello fact that hello SocialSecurityNumber is unique tooperform a MERGE of multiple employees.</span></span> <span data-ttu-id="36e1d-478">Em primeiro lugar, crie o tipo de tabela definido pelo utilizador Olá:</span><span class="sxs-lookup"><span data-stu-id="36e1d-478">First, create hello user-defined table type:</span></span>

    CREATE TYPE EmployeeTableType AS TABLE 
    ( Employee_ID INT,
      FirstName NVARCHAR(50),
      LastName NVARCHAR(50),
      SocialSecurityNumber NVARCHAR(50) );
    GO

<span data-ttu-id="36e1d-479">Em seguida, crie um procedimento armazenado ou escrever código que utiliza Olá atualização de Olá de tooperform de instrução de intercalação e insere.</span><span class="sxs-lookup"><span data-stu-id="36e1d-479">Next, create a stored procedure or write code that uses hello MERGE statement tooperform hello update and insert.</span></span> <span data-ttu-id="36e1d-480">Olá exemplo seguinte utiliza instrução MERGE de Olá num parâmetro de valor de tabela, @employees, do tipo EmployeeTableType.</span><span class="sxs-lookup"><span data-stu-id="36e1d-480">hello following example uses hello MERGE statement on a table-valued parameter, @employees, of type EmployeeTableType.</span></span> <span data-ttu-id="36e1d-481">Olá conteúdo Olá @employees tabela não são mostrados aqui.</span><span class="sxs-lookup"><span data-stu-id="36e1d-481">hello contents of hello @employees table are not shown here.</span></span>

    MERGE Employee AS target
    USING (SELECT [FirstName], [LastName], [SocialSecurityNumber] FROM @employees) 
    AS source ([FirstName], [LastName], [SocialSecurityNumber])
    ON (target.[SocialSecurityNumber] = source.[SocialSecurityNumber])
    WHEN MATCHED THEN 
    UPDATE SET
    target.FirstName = source.FirstName, 
    target.LastName = source.LastName
    WHEN NOT MATCHED THEN
       INSERT ([FirstName], [LastName], [SocialSecurityNumber])
       VALUES (source.[FirstName], source.[LastName], source.[SocialSecurityNumber]);

<span data-ttu-id="36e1d-482">Para obter mais informações, consulte a documentação de Olá e exemplos de instrução de intercalação Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-482">For more information, see hello documentation and examples for hello MERGE statement.</span></span> <span data-ttu-id="36e1d-483">Embora Olá trabalho mesmo pode ser efetuado num passo vários armazenadas chamada de procedimento com as operações INSERT e ATUALIZAÇÃO separadas, Olá instrução MERGE é mais eficiente.</span><span class="sxs-lookup"><span data-stu-id="36e1d-483">Although hello same work could be performed in a multiple-step stored procedure call with separate INSERT and UPDATE operations, hello MERGE statement is more efficient.</span></span> <span data-ttu-id="36e1d-484">Código de base de dados também pode construir chamadas de Transact-SQL que utilizem a instrução de intercalação de Olá diretamente, sem necessidade de dois chamadas de base de dados para inserir e a ATUALIZAÇÃO.</span><span class="sxs-lookup"><span data-stu-id="36e1d-484">Database code can also construct Transact-SQL calls that use hello MERGE statement directly without requiring two database calls for INSERT and UPDATE.</span></span>

## <a name="recommendation-summary"></a><span data-ttu-id="36e1d-485">Recomendação resumo</span><span class="sxs-lookup"><span data-stu-id="36e1d-485">Recommendation summary</span></span>
<span data-ttu-id="36e1d-486">Olá lista seguinte fornece um resumo das Olá criação de batches recomendações apresentadas neste tópico:</span><span class="sxs-lookup"><span data-stu-id="36e1d-486">hello following list provides a summary of hello batching recommendations discussed in this topic:</span></span>

* <span data-ttu-id="36e1d-487">Utilize a colocação em memória intermédia e criação de batches de desempenho de Olá tooincrease e a escalabilidade das aplicações de base de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="36e1d-487">Use buffering and batching tooincrease hello performance and scalability of SQL Database applications.</span></span>
* <span data-ttu-id="36e1d-488">Compreenda fala Olá entre a criação de batches/colocação em memória intermédia e resiliência.</span><span class="sxs-lookup"><span data-stu-id="36e1d-488">Understand hello tradeoffs between batching/buffering and resiliency.</span></span> <span data-ttu-id="36e1d-489">Durante uma falha de função, o risco de Olá de perda de um lote não processado de dados críticos da empresa poderá compensar vantagem de desempenho de Olá de criação de batches.</span><span class="sxs-lookup"><span data-stu-id="36e1d-489">During a role failure, hello risk of losing an unprocessed batch of business-critical data might outweigh hello performance benefit of batching.</span></span>
* <span data-ttu-id="36e1d-490">Tentativa de tookeep todas as chamadas toohello da base de dados dentro de uma latência de tooreduce único centro de dados.</span><span class="sxs-lookup"><span data-stu-id="36e1d-490">Attempt tookeep all calls toohello database within a single datacenter tooreduce latency.</span></span>
* <span data-ttu-id="36e1d-491">Se optar por uma única técnica de lotes, parâmetros de valor de tabela oferecem o melhor desempenho possível Olá e flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="36e1d-491">If you choose a single batching technique, table-valued parameters offer hello best performance and flexibility.</span></span>
* <span data-ttu-id="36e1d-492">Para mais rápido Olá inserir o desempenho, siga estas Diretrizes gerais, mas testar o cenário:</span><span class="sxs-lookup"><span data-stu-id="36e1d-492">For hello fastest insert performance, follow these general guidelines but test your scenario:</span></span>
  * <span data-ttu-id="36e1d-493">Para < 100 linhas, utilize um único comando INSERT parametrizado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-493">For < 100 rows, use a single parameterized INSERT command.</span></span>
  * <span data-ttu-id="36e1d-494">Para < 1000 linhas, utilize parâmetros de valor de tabela.</span><span class="sxs-lookup"><span data-stu-id="36e1d-494">For < 1000 rows, use table-valued parameters.</span></span>
  * <span data-ttu-id="36e1d-495">Para > = 1000 linhas, utilize SqlBulkCopy.</span><span class="sxs-lookup"><span data-stu-id="36e1d-495">For >= 1000 rows, use SqlBulkCopy.</span></span>
* <span data-ttu-id="36e1d-496">Para atualizar e eliminar operações, utilize parâmetros de valor de tabela com a lógica de procedimento armazenado que determina a operação de correto Olá em cada linha no parâmetro de tabela Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-496">For update and delete operations, use table-valued parameters with stored procedure logic that determines hello correct operation on each row in hello table parameter.</span></span>
* <span data-ttu-id="36e1d-497">Diretrizes de tamanho de lote:</span><span class="sxs-lookup"><span data-stu-id="36e1d-497">Batch size guidelines:</span></span>
  * <span data-ttu-id="36e1d-498">Utilize Olá maiores batch tamanhos que façam sentido para a sua aplicação e os requisitos comerciais.</span><span class="sxs-lookup"><span data-stu-id="36e1d-498">Use hello largest batch sizes that make sense for your application and business requirements.</span></span>
  * <span data-ttu-id="36e1d-499">Obter saldo Olá desempenho de lotes grande com riscos de Olá de falhas temporárias ou catastrófica.</span><span class="sxs-lookup"><span data-stu-id="36e1d-499">Balance hello performance gain of large batches with hello risks of temporary or catastrophic failures.</span></span> <span data-ttu-id="36e1d-500">O que é consequence Olá de novas tentativas ou perda de dados de Olá no lote de Olá?</span><span class="sxs-lookup"><span data-stu-id="36e1d-500">What is hello consequence of retries or loss of hello data in hello batch?</span></span> 
  * <span data-ttu-id="36e1d-501">Teste Olá maior batch tamanho tooverify que a base de dados do SQL Server não rejeitá-lo.</span><span class="sxs-lookup"><span data-stu-id="36e1d-501">Test hello largest batch size tooverify that SQL Database does not reject it.</span></span>
  * <span data-ttu-id="36e1d-502">Crie definições de configuração esse controlo de criação de batches, tais como o tamanho do lote Olá ou janela de tempo de colocação em memória intermédia Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-502">Create configuration settings that control batching, such as hello batch size or hello buffering time window.</span></span> <span data-ttu-id="36e1d-503">Estas definições fornecem flexibilidade.</span><span class="sxs-lookup"><span data-stu-id="36e1d-503">These settings provide flexibility.</span></span> <span data-ttu-id="36e1d-504">Pode alterar Olá criação de batches de comportamento em produção sem voltar a implementar o serviço em nuvem Olá.</span><span class="sxs-lookup"><span data-stu-id="36e1d-504">You can change hello batching behavior in production without redeploying hello cloud service.</span></span>
* <span data-ttu-id="36e1d-505">Evite a execução paralela de lotes funcionar numa tabela na base de dados de um único.</span><span class="sxs-lookup"><span data-stu-id="36e1d-505">Avoid parallel execution of batches that operate on a single table in one database.</span></span> <span data-ttu-id="36e1d-506">Se optar por toodivide um único lote em vários threads de trabalho, execute testes toodetermine Olá número ideal de threads.</span><span class="sxs-lookup"><span data-stu-id="36e1d-506">If you do choose toodivide a single batch across multiple worker threads, run tests toodetermine hello ideal number of threads.</span></span> <span data-ttu-id="36e1d-507">Depois de um limiar não especificado, mais threads irão diminuir o desempenho em vez de o aumente demasiado.</span><span class="sxs-lookup"><span data-stu-id="36e1d-507">After an unspecified threshold, more threads will decrease performance rather than increase it.</span></span>
* <span data-ttu-id="36e1d-508">Considere a memória intermédia de tamanho e a hora como uma forma de implementar a criação de batches para cenários mais.</span><span class="sxs-lookup"><span data-stu-id="36e1d-508">Consider buffering on size and time as a way of implementing batching for more scenarios.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36e1d-509">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="36e1d-509">Next steps</span></span>
<span data-ttu-id="36e1d-510">Este artigo concentra-se em como técnicas de programação e de design de base de dados relacionados toobatching pode melhorar o desempenho da aplicação e a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="36e1d-510">This article focused on how database design and coding techniques related toobatching can improve your application performance and scalability.</span></span> <span data-ttu-id="36e1d-511">Mas este é um fator na sua estratégia geral.</span><span class="sxs-lookup"><span data-stu-id="36e1d-511">But this is just one factor in your overall strategy.</span></span> <span data-ttu-id="36e1d-512">Para obter mais maneiras tooimprove desempenho e a escalabilidade, consulte [orientações de desempenho de SQL Database do Azure para bases de dados individuais](sql-database-performance-guidance.md) e [considerações sobre preço e desempenho de um conjunto elástico](sql-database-elastic-pool-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="36e1d-512">For more ways tooimprove performance and scalability, see [Azure SQL Database performance guidance for single databases](sql-database-performance-guidance.md) and [Price and performance considerations for an elastic pool](sql-database-elastic-pool-guidance.md).</span></span>

