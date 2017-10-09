---
title: "informações acerca do desempenho de aaaQuery para a SQL Database do Azure | Microsoft Docs"
description: "Monitorização do desempenho de consulta identifica Olá mais CPU consome consultas para uma base de dados do SQL do Azure."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: c2f580b2-3835-453f-89f5-140e02dd2ea7
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 01cca26f85193c679365585cd676449c9db00e1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="azure-sql-database-query-performance-insight"></a><span data-ttu-id="e382c-103">SQL do Azure da base de dados desempenho das consultas</span><span class="sxs-lookup"><span data-stu-id="e382c-103">Azure SQL Database Query Performance Insight</span></span>
<span data-ttu-id="e382c-104">Gerir e otimização de desempenho de Olá das bases de dados relacionais são uma tarefa um desafio que requer conhecimentos significativos e o investimento de tempo.</span><span class="sxs-lookup"><span data-stu-id="e382c-104">Managing and tuning hello performance of relational databases is a challenging task that requires significant expertise and time investment.</span></span> <span data-ttu-id="e382c-105">Desempenho das consultas permite-lhe toospend menos tempo de resolução de problemas de desempenho de base de dados, fornecendo seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="e382c-105">Query Performance Insight allows you toospend less time troubleshooting database performance by providing hello following:</span></span>

* <span data-ttu-id="e382c-106">Mais aprofundadas sobre o seu consumo de recursos (DTU) de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-106">Deeper insight into your databases resource (DTU) consumption.</span></span> 
* <span data-ttu-id="e382c-107">consultas de Olá superiores por contagem de CPU/duração/execução que potencialmente podem ser otimizados para um melhor desempenho.</span><span class="sxs-lookup"><span data-stu-id="e382c-107">hello top queries by CPU/Duration/Execution count, which can potentially be tuned for improved performance.</span></span>
* <span data-ttu-id="e382c-108">Olá toodrill de capacidade para baixo para detalhes de Olá de uma consulta, ver o texto e o histórico de utilização de recursos.</span><span class="sxs-lookup"><span data-stu-id="e382c-108">hello ability toodrill down into hello details of a query, view its text and history of resource utilization.</span></span> 
* <span data-ttu-id="e382c-109">As anotações que mostram as ações executadas de otimização do desempenho [Advisor de base de dados SQL do Azure](sql-database-advisor.md)</span><span class="sxs-lookup"><span data-stu-id="e382c-109">Performance tuning annotations that show actions performed by [SQL Azure Database Advisor](sql-database-advisor.md)</span></span>  



## <a name="prerequisites"></a><span data-ttu-id="e382c-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="e382c-110">Prerequisites</span></span>
* <span data-ttu-id="e382c-111">Consulta Performance Insight requer que [arquivo de consultas](https://msdn.microsoft.com/library/dn817826.aspx) está ativo na base de dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-111">Query Performance Insight requires that [Query Store](https://msdn.microsoft.com/library/dn817826.aspx) is active on your database.</span></span> <span data-ttu-id="e382c-112">Se o arquivo de consultas não está em execução, o portal de Olá pede-lhe tooturn-lo na.</span><span class="sxs-lookup"><span data-stu-id="e382c-112">If Query Store is not running, hello portal prompts you tooturn it on.</span></span>

## <a name="permissions"></a><span data-ttu-id="e382c-113">Permissões</span><span class="sxs-lookup"><span data-stu-id="e382c-113">Permissions</span></span>
<span data-ttu-id="e382c-114">seguinte Olá [controlo de acesso baseado em funções](../active-directory/role-based-access-control-what-is.md) permissões são necessária toouse Query Performance Insight:</span><span class="sxs-lookup"><span data-stu-id="e382c-114">hello following [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions are required toouse Query Performance Insight:</span></span> 

* <span data-ttu-id="e382c-115">**Leitor**, **proprietário**, **contribuinte**, **contribuinte da BD SQL**, ou **contribuinte de servidor de SQL** são permissões necessário tooview Olá principais recursos consumir consultas e gráficos.</span><span class="sxs-lookup"><span data-stu-id="e382c-115">**Reader**, **Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview hello top resource consuming queries and charts.</span></span> 
* <span data-ttu-id="e382c-116">**Proprietário**, **contribuinte**, **contribuinte da BD SQL**, ou **contribuinte de servidor de SQL** permissões são necessárias tooview texto da consulta.</span><span class="sxs-lookup"><span data-stu-id="e382c-116">**Owner**, **Contributor**, **SQL DB Contributor**, or **SQL Server Contributor** permissions are required tooview query text.</span></span>

## <a name="using-query-performance-insight"></a><span data-ttu-id="e382c-117">Utilizar o desempenho das consultas</span><span class="sxs-lookup"><span data-stu-id="e382c-117">Using Query Performance Insight</span></span>
<span data-ttu-id="e382c-118">Desempenho das consultas é fácil toouse:</span><span class="sxs-lookup"><span data-stu-id="e382c-118">Query Performance Insight is easy toouse:</span></span>

* <span data-ttu-id="e382c-119">Abra [portal do Azure](https://portal.azure.com/) e localizar base de dados que pretende que o tooexamine.</span><span class="sxs-lookup"><span data-stu-id="e382c-119">Open [Azure portal](https://portal.azure.com/) and find database that you want tooexamine.</span></span> 
  * <span data-ttu-id="e382c-120">No menu do lado esquerdo, em suporte e resolução de problemas, selecione "Query Performance Insight".</span><span class="sxs-lookup"><span data-stu-id="e382c-120">From left-hand side menu, under support and troubleshooting, select “Query Performance Insight”.</span></span>
* <span data-ttu-id="e382c-121">No separador de primeiro Olá, reveja a lista de Olá de consultas de consumo de recursos principais.</span><span class="sxs-lookup"><span data-stu-id="e382c-121">On hello first tab, review hello list of top resource-consuming queries.</span></span>
* <span data-ttu-id="e382c-122">Selecione uma consulta individual tooview os respetivos detalhes.</span><span class="sxs-lookup"><span data-stu-id="e382c-122">Select an individual query tooview its details.</span></span>
* <span data-ttu-id="e382c-123">Abra [Advisor de base de dados do SQL Azure](sql-database-advisor.md) e verifique se as recomendações estarão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="e382c-123">Open [SQL Azure Database Advisor](sql-database-advisor.md) and check if any recommendations are available.</span></span>
* <span data-ttu-id="e382c-124">Utilizar controlos de deslize ou toochange ícones observado o intervalo de zoom.</span><span class="sxs-lookup"><span data-stu-id="e382c-124">Use sliders or zoom icons toochange observed interval.</span></span>
  
    ![dashboard de desempenho](./media/sql-database-query-performance/performance.png)

> [!NOTE]
> <span data-ttu-id="e382c-126">Horas de alguns dos dados tem toobe capturado pelo arquivo de consultas para o query performance Insight para base de dados SQL tooprovide.</span><span class="sxs-lookup"><span data-stu-id="e382c-126">A couple hours of data needs toobe captured by Query Store for SQL Database tooprovide query performance insights.</span></span> <span data-ttu-id="e382c-127">Se a base de dados de Olá não tem nenhuma atividade ou o arquivo de consultas não esteve ativo durante um determinado período de tempo, os gráficos de Olá estará vazios quando se apresenta esse período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e382c-127">If hello database has no activity or Query Store was not active during a certain time period, hello charts will be empty when displaying that time period.</span></span> <span data-ttu-id="e382c-128">Se não está em execução, pode ativar o arquivo de consultas em qualquer altura.</span><span class="sxs-lookup"><span data-stu-id="e382c-128">You may enable Query Store at any time if it is not running.</span></span>   
> 
> 

## <a name="review-top-cpu-consuming-queries"></a><span data-ttu-id="e382c-129">Reveja principal da CPU de consultas de consumo</span><span class="sxs-lookup"><span data-stu-id="e382c-129">Review top CPU consuming queries</span></span>
<span data-ttu-id="e382c-130">No Olá [portal](http://portal.azure.com) Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="e382c-130">In hello [portal](http://portal.azure.com) do hello following:</span></span>

1. <span data-ttu-id="e382c-131">Procurar tooa SQL da base de dados e clique em **todas as definições** > **suporte + resolução de problemas** > **nas informações de desempenho de consulta**.</span><span class="sxs-lookup"><span data-stu-id="e382c-131">Browse tooa SQL database and click **All settings** > **Support + Troubleshooting** > **Query performance insight**.</span></span> 
   
    ![Query Performance Insight][1]
   
    <span data-ttu-id="e382c-133">Abre a vista de consultas superiores Olá e as principais consultas consumo de CPU de Olá estão listadas.</span><span class="sxs-lookup"><span data-stu-id="e382c-133">hello top queries view opens and hello top CPU consuming queries are listed.</span></span>
2. <span data-ttu-id="e382c-134">Clique em torno do gráfico de Olá para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e382c-134">Click around hello chart for details.</span></span><br><span data-ttu-id="e382c-135">Olá linha superior mostra % geral de DTU para base de dados de Olá, enquanto as barras de Olá mostram % de CPU consumido por consultas Olá selecionado durante o intervalo selecionado Olá (por exemplo, se **passado semana** está selecionado cada barra representa um dia).</span><span class="sxs-lookup"><span data-stu-id="e382c-135">hello top line shows overall DTU% for hello database, while hello bars show CPU% consumed by hello selected queries during hello selected interval (for example, if **Past week** is selected each bar represents one day).</span></span>
   
    ![consultas superiores][2]
   
    <span data-ttu-id="e382c-137">grelha de inferior Olá representa a informação agregada para consultas visível Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-137">hello bottom grid represents aggregated information for hello visible queries.</span></span>
   
   * <span data-ttu-id="e382c-138">ID de consulta - o identificador exclusivo da consulta no interior da base de dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-138">Query ID - unique identifier of query inside database.</span></span>
   * <span data-ttu-id="e382c-139">CPU por consulta durante o intervalo de observable (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="e382c-139">CPU per query during observable interval (depends on aggregation function).</span></span>
   * <span data-ttu-id="e382c-140">Duração por consulta (depende da função de agregação).</span><span class="sxs-lookup"><span data-stu-id="e382c-140">Duration per query (depends on aggregation function).</span></span>
   * <span data-ttu-id="e382c-141">Número total de execuções de uma consulta específica.</span><span class="sxs-lookup"><span data-stu-id="e382c-141">Total number of executions for a particular query.</span></span>
     
     <span data-ttu-id="e382c-142">Selecione ou desmarque tooinclude consultas individuais ou excluir da gráfico Olá com caixas de verificação.</span><span class="sxs-lookup"><span data-stu-id="e382c-142">Select or clear individual queries tooinclude or exclude them from hello chart using checkboxes.</span></span>
3. <span data-ttu-id="e382c-143">Se os dados torna-se obsoleta, clique em Olá **atualizar** botão.</span><span class="sxs-lookup"><span data-stu-id="e382c-143">If your data becomes stale, click hello **Refresh** button.</span></span>
4. <span data-ttu-id="e382c-144">Pode utilizar controlos de deslize e o intervalo de observação de toochange de botões de zoom e investigar picos: ![definições](./media/sql-database-query-performance/zoom.png)</span><span class="sxs-lookup"><span data-stu-id="e382c-144">You can use sliders and zoom buttons toochange observation interval and investigate spikes:  ![settings](./media/sql-database-query-performance/zoom.png)</span></span>
5. <span data-ttu-id="e382c-145">Opcionalmente, se pretender uma vista diferente, pode selecionar **personalizada** separador e definir:</span><span class="sxs-lookup"><span data-stu-id="e382c-145">Optionally, if you want a different view, you can select **Custom** tab and set:</span></span>
   
   * <span data-ttu-id="e382c-146">Métrica (CPU, duração, a contagem de execução)</span><span class="sxs-lookup"><span data-stu-id="e382c-146">Metric (CPU, duration, execution count)</span></span>
   * <span data-ttu-id="e382c-147">Intervalo de tempo (últimas 24 horas, após uma semana, passado mês).</span><span class="sxs-lookup"><span data-stu-id="e382c-147">Time interval (Last 24 hours, Past week, Past month).</span></span> 
   * <span data-ttu-id="e382c-148">Número de consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-148">Number of queries.</span></span>
   * <span data-ttu-id="e382c-149">Função de agregação.</span><span class="sxs-lookup"><span data-stu-id="e382c-149">Aggregation function.</span></span>
     
     ![settings](./media/sql-database-query-performance/custom-tab.png)

## <a name="viewing-individual-query-details"></a><span data-ttu-id="e382c-151">Detalhes de consulta individuais de visualização</span><span class="sxs-lookup"><span data-stu-id="e382c-151">Viewing individual query details</span></span>
<span data-ttu-id="e382c-152">detalhes de consulta tooview:</span><span class="sxs-lookup"><span data-stu-id="e382c-152">tooview query details:</span></span>

1. <span data-ttu-id="e382c-153">Clique em qualquer consulta na lista de Olá de consultas superiores.</span><span class="sxs-lookup"><span data-stu-id="e382c-153">Click any query in hello list of top queries.</span></span>
   
    ![Detalhes](./media/sql-database-query-performance/details.png)
2. <span data-ttu-id="e382c-155">Abre a vista de detalhes de Olá e contagem de consumo/duração/execução Olá consultas CPU é reduzida ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="e382c-155">hello details view opens and hello queries CPU consumption/Duration/Execution count is broken down over time.</span></span>
3. <span data-ttu-id="e382c-156">Clique em torno do gráfico de Olá para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="e382c-156">Click around hello chart for details.</span></span>
   
   * <span data-ttu-id="e382c-157">Principal gráfico mostra a linha de base de dados DTU % geral e as barras de Olá são consumida pela consulta selecionada Olá de CPU de %.</span><span class="sxs-lookup"><span data-stu-id="e382c-157">Top chart shows line with overall database DTU%, and hello bars are CPU% consumed by hello selected query.</span></span>
   * <span data-ttu-id="e382c-158">Segundo gráfico mostra a duração total pela consulta selecionada Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-158">Second chart shows total duration by hello selected query.</span></span>
   * <span data-ttu-id="e382c-159">Gráfico de inferior mostra o número total de execuções pela consulta selecionada Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-159">Bottom chart shows total number of executions by hello selected query.</span></span>
     
     ![detalhes de consulta][3]
4. <span data-ttu-id="e382c-161">Opcionalmente, utilize os controlos de deslize, zoom botões ou clique em **definições** toocustomize como consultar dados são apresentados ou toopick um período de hora diferente.</span><span class="sxs-lookup"><span data-stu-id="e382c-161">Optionally, use sliders, zoom buttons or click **Settings** toocustomize how query data is displayed, or toopick a different time period.</span></span>

## <a name="review-top-queries-per-duration"></a><span data-ttu-id="e382c-162">Reveja as consultas superiores por duração</span><span class="sxs-lookup"><span data-stu-id="e382c-162">Review top queries per duration</span></span>
<span data-ttu-id="e382c-163">A atualização recente Olá de desempenho das consultas, introduzimos duas métricas novo que podem ajudar a identificar potenciais congestionamentos: contagem de duração e a execução.</span><span class="sxs-lookup"><span data-stu-id="e382c-163">In hello recent update of Query Performance Insight, we introduced two new metrics that can help you identify potential bottlenecks: duration and execution count.</span></span><br>

<span data-ttu-id="e382c-164">As consultas de execução longa ter possibilidade de maior Olá de bloqueio mais recursos, bloquear a outros utilizadores e limitar a escalabilidade.</span><span class="sxs-lookup"><span data-stu-id="e382c-164">Long-running queries have hello greatest potential for locking resources longer, blocking other users, and limiting scalability.</span></span> <span data-ttu-id="e382c-165">Também são candidatos a melhor Olá para otimização.</span><span class="sxs-lookup"><span data-stu-id="e382c-165">They are also hello best candidates for optimization.</span></span><br>

<span data-ttu-id="e382c-166">tooidentify execução longa consultas:</span><span class="sxs-lookup"><span data-stu-id="e382c-166">tooidentify long running queries:</span></span>

1. <span data-ttu-id="e382c-167">Abra **personalizada** separador no desempenho das consultas de base de dados selecionada</span><span class="sxs-lookup"><span data-stu-id="e382c-167">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="e382c-168">Alterar as métricas toobe **duração**</span><span class="sxs-lookup"><span data-stu-id="e382c-168">Change metrics toobe **duration**</span></span>
3. <span data-ttu-id="e382c-169">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="e382c-169">Select number of queries and observation interval</span></span>
4. <span data-ttu-id="e382c-170">Selecione a função de agregação</span><span class="sxs-lookup"><span data-stu-id="e382c-170">Select aggregation function</span></span>
   
   * <span data-ttu-id="e382c-171">**Soma** adiciona todos os tempo de execução da consulta durante o intervalo de observação todo.</span><span class="sxs-lookup"><span data-stu-id="e382c-171">**Sum** adds up all query execution time during whole observation interval.</span></span>
   * <span data-ttu-id="e382c-172">**Máx.** localiza consultas que tempo de execução estava máximo no intervalo de observação todo.</span><span class="sxs-lookup"><span data-stu-id="e382c-172">**Max** finds queries which execution time was maximum at whole observation interval.</span></span>
   * <span data-ttu-id="e382c-173">**Média** encontra tempo médio de execução de todas as execuções de consulta e mostrar-lhe Olá superior fora destes médias.</span><span class="sxs-lookup"><span data-stu-id="e382c-173">**Avg** finds average execution time of all query executions and show you hello top out of these averages.</span></span> 
     
     ![duração de consulta][4]

## <a name="review-top-queries-per-execution-count"></a><span data-ttu-id="e382c-175">Reveja as consultas superiores por contagem de execução</span><span class="sxs-lookup"><span data-stu-id="e382c-175">Review top queries per execution count</span></span>
<span data-ttu-id="e382c-176">Número elevado de execuções poderá não ser que afetam a própria base de dados e a utilização de recursos pode ser reduzida, mas global da aplicação poderá obter lenta.</span><span class="sxs-lookup"><span data-stu-id="e382c-176">High number of executions might not be affecting database itself and resources usage can be low, but overall application might get slow.</span></span>

<span data-ttu-id="e382c-177">Em alguns casos, contagem de execução muito elevado pode levar tooincrease da rede de ida e volta.</span><span class="sxs-lookup"><span data-stu-id="e382c-177">In some cases, very high execution count may lead tooincrease of network round trips.</span></span> <span data-ttu-id="e382c-178">Ida e volta afetar significativamente o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e382c-178">Round trips significantly affect performance.</span></span> <span data-ttu-id="e382c-179">São latência de toonetwork do requerente e toodownstream latência de servidor.</span><span class="sxs-lookup"><span data-stu-id="e382c-179">They are subject toonetwork latency and toodownstream server latency.</span></span> 

<span data-ttu-id="e382c-180">Por exemplo, muitos sites Web condicionada por dados fortemente aceder Olá base de dados para cada pedido de utilizador.</span><span class="sxs-lookup"><span data-stu-id="e382c-180">For example, many data-driven Web sites heavily access hello database for every user request.</span></span> <span data-ttu-id="e382c-181">Enquanto a ligação agrupamento ajuda-o, hello maior tráfego de rede e a carga de processamento no servidor de base de dados de Olá negativamente pode afeta o desempenho.</span><span class="sxs-lookup"><span data-stu-id="e382c-181">While connection pooling helps, hello increased network traffic and processing load on hello database server can adversely affect performance.</span></span>  <span data-ttu-id="e382c-182">Conselhos geral é tookeep arredondar viagens tooan mínimo.</span><span class="sxs-lookup"><span data-stu-id="e382c-182">General advice is tookeep round trips tooan absolute minimum.</span></span>

<span data-ttu-id="e382c-183">tooidentify executada com frequência consultas de ("chatty") de consultas:</span><span class="sxs-lookup"><span data-stu-id="e382c-183">tooidentify frequently executed queries (“chatty”) queries:</span></span>

1. <span data-ttu-id="e382c-184">Abra **personalizada** separador no desempenho das consultas de base de dados selecionada</span><span class="sxs-lookup"><span data-stu-id="e382c-184">Open **Custom** tab in Query Performance Insight for selected database</span></span>
2. <span data-ttu-id="e382c-185">Alterar as métricas toobe **contagem de execução**</span><span class="sxs-lookup"><span data-stu-id="e382c-185">Change metrics toobe **execution count**</span></span>
3. <span data-ttu-id="e382c-186">Selecione o número de consultas e o intervalo de observação</span><span class="sxs-lookup"><span data-stu-id="e382c-186">Select number of queries and observation interval</span></span>
   
    ![Contagem de execução da consulta][5]

## <a name="understanding-performance-tuning-annotations"></a><span data-ttu-id="e382c-188">Noções sobre anotações de otimização de desempenho</span><span class="sxs-lookup"><span data-stu-id="e382c-188">Understanding performance tuning annotations</span></span>
<span data-ttu-id="e382c-189">Enquanto a explorar a carga de trabalho no desempenho das consultas, é possível que repare ícones com linha vertical por cima do gráfico Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-189">While exploring your workload in Query Performance Insight, you might notice icons with vertical line on top of hello chart.</span></span><br>

<span data-ttu-id="e382c-190">Estes ícones são anotações; representam o desempenho que afetam a ações realizadas por [Advisor de base de dados do SQL Azure](sql-database-advisor.md).</span><span class="sxs-lookup"><span data-stu-id="e382c-190">These icons are annotations; they represent performance affecting actions performed by [SQL Azure Database Advisor](sql-database-advisor.md).</span></span> <span data-ttu-id="e382c-191">Por hovering anotação, obter informações básicas sobre a ação de Olá:</span><span class="sxs-lookup"><span data-stu-id="e382c-191">By hovering annotation, you get basic information about hello action:</span></span>

![anotação de consulta][6]

<span data-ttu-id="e382c-193">Se pretender mais tooknow ou aplicar a recomendação do advisor, clique no ícone Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-193">If you want tooknow more or apply advisor recommendation, click hello icon.</span></span> <span data-ttu-id="e382c-194">Detalhes de ação é aberto.</span><span class="sxs-lookup"><span data-stu-id="e382c-194">It will open details of action.</span></span> <span data-ttu-id="e382c-195">Se for uma recomendação de Active Directory, pode aplicá-la diretamente ausente utilizando o comando.</span><span class="sxs-lookup"><span data-stu-id="e382c-195">If it’s an active recommendation you can apply it straight away using command.</span></span>

![detalhes de anotação de consulta][7]

### <a name="multiple-annotations"></a><span data-ttu-id="e382c-197">Vários anotações.</span><span class="sxs-lookup"><span data-stu-id="e382c-197">Multiple annotations.</span></span>
<span data-ttu-id="e382c-198">É possível que, devido ao nível de zoom, irão obter fechadas anotações são tooeach fechar outros numa só.</span><span class="sxs-lookup"><span data-stu-id="e382c-198">It’s possible, that because of zoom level, annotations that are close tooeach other will get collapsed into one.</span></span> <span data-ttu-id="e382c-199">Isto será representado por ícone especial, clicar nela irá abrir novo painel onde a lista de agrupadas anotações será apresentado.</span><span class="sxs-lookup"><span data-stu-id="e382c-199">This will be represented by special icon, clicking it will open new blade where list of grouped annotations will be shown.</span></span>
<span data-ttu-id="e382c-200">Correlacionar consultas e ações de otimização do desempenho pode ajudar toobetter compreender a sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="e382c-200">Correlating queries and performance tuning actions can help toobetter understand your workload.</span></span> 

## <a name="optimizing-hello-query-store-configuration-for-query-performance-insight"></a><span data-ttu-id="e382c-201">Otimizar a configuração do arquivo de consultas de Olá para o Query Performance Insight</span><span class="sxs-lookup"><span data-stu-id="e382c-201">Optimizing hello Query Store configuration for Query Performance Insight</span></span>
<span data-ttu-id="e382c-202">Durante a utilização do desempenho das consultas, que poderá encontrar Olá seguintes mensagens de arquivo de consultas:</span><span class="sxs-lookup"><span data-stu-id="e382c-202">During your use of Query Performance Insight, you might encounter hello following Query Store messages:</span></span>

* <span data-ttu-id="e382c-203">"Arquivo de consultas não está devidamente configurado nesta base de dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-203">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="e382c-204">Clique aqui toolearn mais."</span><span class="sxs-lookup"><span data-stu-id="e382c-204">Click here toolearn more."</span></span>
* <span data-ttu-id="e382c-205">"Arquivo de consultas não está devidamente configurado nesta base de dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-205">"Query Store is not properly configured on this database.</span></span> <span data-ttu-id="e382c-206">Clique aqui definições toochange."</span><span class="sxs-lookup"><span data-stu-id="e382c-206">Click here toochange settings."</span></span> 

<span data-ttu-id="e382c-207">Estas mensagens são apresentados normalmente quando o arquivo de consultas não consegue toocollect novos dados.</span><span class="sxs-lookup"><span data-stu-id="e382c-207">These messages usually appear when Query Store is not able toocollect new data.</span></span> 

<span data-ttu-id="e382c-208">Primeiro caso acontece quando o arquivo de consultas está no estado só de leitura e os parâmetros estão definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="e382c-208">First case happens when Query Store is in Read-Only state and parameters are set optimally.</span></span> <span data-ttu-id="e382c-209">Para corrigir este problema, aumente o tamanho do arquivo de consultas ou limpar o arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-209">You can fix this by increasing size of Query Store or clearing Query Store.</span></span>

![botão de qds][8]

<span data-ttu-id="e382c-211">Segundo caso acontece quando o arquivo de consultas está desligado ou com parâmetros não se encontram definidos de forma ideal.</span><span class="sxs-lookup"><span data-stu-id="e382c-211">Second case happens when Query Store is Off or parameters aren’t set optimally.</span></span> <br><span data-ttu-id="e382c-212">Pode alterar Olá retenção e a captura de política e ativar o arquivo de consultas ao executar comandos abaixo ou diretamente a partir do portal:</span><span class="sxs-lookup"><span data-stu-id="e382c-212">You can change hello Retention and Capture policy and enable Query Store by executing commands below or directly from portal:</span></span>

![botão de qds][9]

### <a name="recommended-retention-and-capture-policy"></a><span data-ttu-id="e382c-214">Política de retenção e a captura recomendada</span><span class="sxs-lookup"><span data-stu-id="e382c-214">Recommended retention and capture policy</span></span>
<span data-ttu-id="e382c-215">Existem dois tipos de políticas de retenção:</span><span class="sxs-lookup"><span data-stu-id="e382c-215">There are two types of retention policies:</span></span>

* <span data-ttu-id="e382c-216">Tamanho baseia - se for atingida a tooAUTO conjunto irá limpar dados automaticamente quando perto de tamanho máximo.</span><span class="sxs-lookup"><span data-stu-id="e382c-216">Size based - if set tooAUTO it will clean data automatically when near max size is reached.</span></span>
* <span data-ttu-id="e382c-217">Hora com base - por predefinição será o definimos too30 dias, que significa que, se o arquivo de consultas irá ficar sem espaço, serão eliminadas consultar informações com mais de 30 dias</span><span class="sxs-lookup"><span data-stu-id="e382c-217">Time based - by default we will set it too30 days, which means, if Query Store will run out of space, it will delete query information older than 30 days</span></span>

<span data-ttu-id="e382c-218">Captura de política pode ser definida como:</span><span class="sxs-lookup"><span data-stu-id="e382c-218">Capture policy could be set to:</span></span>

* <span data-ttu-id="e382c-219">**Todos os** -captura todas as consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-219">**All** - Captures all queries.</span></span>
* <span data-ttu-id="e382c-220">**Auto** -influxo consultas e consultas com a duração de compilação e execução insignificant são ignoradas.</span><span class="sxs-lookup"><span data-stu-id="e382c-220">**Auto** - Infrequent queries and queries with insignificant compile and execution duration are ignored.</span></span> <span data-ttu-id="e382c-221">Limiares de duração de execução contagem, compilação e tempo de execução são determinados internamente.</span><span class="sxs-lookup"><span data-stu-id="e382c-221">Thresholds for execution count, compile and runtime duration are internally determined.</span></span> <span data-ttu-id="e382c-222">Esta é a opção predefinida de Olá.</span><span class="sxs-lookup"><span data-stu-id="e382c-222">This is hello default option.</span></span>
* <span data-ttu-id="e382c-223">**Nenhum** -arquivo de consultas deixa de captura nova consultas, no entanto, as estatísticas de tempo de execução de consultas já capturadas são ainda recolhidas.</span><span class="sxs-lookup"><span data-stu-id="e382c-223">**None** - Query Store stops capturing new queries, however runtime stats for already captured queries are still collected.</span></span>

<span data-ttu-id="e382c-224">Recomendamos que defina todas as políticas tooAUTO e limpar política too30 dias:</span><span class="sxs-lookup"><span data-stu-id="e382c-224">We recommend setting all policies tooAUTO and clean policy too30 days:</span></span>

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (SIZE_BASED_CLEANUP_MODE = AUTO);

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (CLEANUP_POLICY = (STALE_QUERY_THRESHOLD_DAYS = 30));

    ALTER DATABASE [YourDB] 
    SET QUERY_STORE (QUERY_CAPTURE_MODE = AUTO);

<span data-ttu-id="e382c-225">Aumente o tamanho do arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-225">Increase size of Query Store.</span></span> <span data-ttu-id="e382c-226">Isto pode ser efetuada pela base de dados de tooa ligação e a emitir a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="e382c-226">This could be performed by connecting tooa database and issuing following query:</span></span>

    ALTER DATABASE [YourDB]
    SET QUERY_STORE (MAX_STORAGE_SIZE_MB = 1024);

<span data-ttu-id="e382c-227">Aplicar estas definições, eventualmente, faz com que o arquivo de consultas recolher novas consultas, no entanto, se não quiser toowait pode limpar o arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-227">Applying these settings will eventually make Query Store collecting new queries, however if you don’t want toowait you can clear Query Store.</span></span> 

> [!NOTE]
> <span data-ttu-id="e382c-228">Executar consulta seguinte irá eliminar todas as informações atuais Olá arquivo de consultas.</span><span class="sxs-lookup"><span data-stu-id="e382c-228">Executing following query will delete all current information in hello Query Store.</span></span> 
> 
> 

    ALTER DATABASE [YourDB] SET QUERY_STORE CLEAR;


## <a name="summary"></a><span data-ttu-id="e382c-229">Resumo</span><span class="sxs-lookup"><span data-stu-id="e382c-229">Summary</span></span>
<span data-ttu-id="e382c-230">Desempenho das consultas ajuda-o a compreender o impacto de Olá da sua carga de trabalho de consulta e como se relaciona com toodatabase consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="e382c-230">Query Performance Insight helps you understand hello impact of your query workload and how it relates toodatabase resource consumption.</span></span> <span data-ttu-id="e382c-231">Com esta funcionalidade, irá saber mais sobre melhores Olá consultas de consumo e identificar facilmente Olá aqueles toofix antes de ficarem um problema.</span><span class="sxs-lookup"><span data-stu-id="e382c-231">With this feature, you will learn about hello top consuming queries, and easily identify hello ones toofix before they become a problem.</span></span>

## <a name="next-steps"></a><span data-ttu-id="e382c-232">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e382c-232">Next steps</span></span>
<span data-ttu-id="e382c-233">Para obter recomendações adicionais sobre como melhorar o desempenho de Olá da sua base de dados do SQL Server, clique em [recomendações](sql-database-advisor.md) no Olá **Query Performance Insight** painel.</span><span class="sxs-lookup"><span data-stu-id="e382c-233">For additional recommendations about improving hello performance of your SQL database, click [Recommendations](sql-database-advisor.md) on hello **Query Performance Insight** blade.</span></span>

![Advisor de desempenho](./media/sql-database-query-performance/ia.png)

<!--Image references-->
[1]: ./media/sql-database-query-performance/tile.png
[2]: ./media/sql-database-query-performance/top-queries.png
[3]: ./media/sql-database-query-performance/query-details.png
[4]: ./media/sql-database-query-performance/top-duration.png
[5]: ./media/sql-database-query-performance/top-execution.png
[6]: ./media/sql-database-query-performance/annotation.png
[7]: ./media/sql-database-query-performance/annotation-details.png
[8]: ./media/sql-database-query-performance/qds-off.png
[9]: ./media/sql-database-query-performance/qds-button.png

