---
title: "as consultas de análises de aaaRun contra várias bases de dados SQL do Azure | Microsoft Docs"
description: "Extrair dados de bases de dados do inquilino para uma base de dados de análise para a análise offline"
keywords: tutorial de base de dados sql
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: scale out apps
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: billgib; sstein
ms.openlocfilehash: f2664e4aafd2fecc98d20d229342bca19b0b08c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="extract-data-from-tenant-databases-into-an-analytics-database-for-offline-analysis"></a><span data-ttu-id="e1bf6-104">Extrair dados de bases de dados do inquilino para uma base de dados de análise para a análise offline</span><span class="sxs-lookup"><span data-stu-id="e1bf6-104">Extract data from tenant databases into an analytics database for offline analysis</span></span>

<span data-ttu-id="e1bf6-105">Neste tutorial, utilize uma tarefa elástico toorun consultas cada base de dados do inquilino.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-105">In this tutorial, you use an elastic job toorun queries against each tenant database.</span></span> <span data-ttu-id="e1bf6-106">tarefa de Olá extrai dados de vendas de permissão e carrega-o para uma base de dados de análise (ou do armazém de dados) para análise.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-106">hello job extracts ticket sales data and loads it into an analytics database (or data warehouse) for analysis.</span></span> <span data-ttu-id="e1bf6-107">Olá base de dados de análise em seguida, é consultado tooextract conhecimentos aprofundados sobre estes dados operacionais diárias de todos os inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-107">hello analytics database is then queried tooextract insights from this day-to-day operational data of all tenants.</span></span>


<span data-ttu-id="e1bf6-108">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-108">In this tutorial you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1bf6-109">Criar base de dados de análise de inquilino de Olá</span><span class="sxs-lookup"><span data-stu-id="e1bf6-109">Create hello tenant analytics database</span></span>
> * <span data-ttu-id="e1bf6-110">Criar dados de tooretrieve uma tarefa agendada e preencher a base de dados de análise de Olá</span><span class="sxs-lookup"><span data-stu-id="e1bf6-110">Create a scheduled job tooretrieve data and populate hello analytics database</span></span>

<span data-ttu-id="e1bf6-111">toocomplete neste tutorial, Olá se disponibilizar os seguintes pré-requisitos são cumpridos:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-111">toocomplete this tutorial, make sure hello following prerequisites are met:</span></span>

* <span data-ttu-id="e1bf6-112">Olá Wingtip SaaS aplicação é implementada.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-112">hello Wingtip SaaS app is deployed.</span></span> <span data-ttu-id="e1bf6-113">toodeploy em menos de cinco minutos, consulte [implementar e explorar aplicações de Wingtip SaaS Olá](sql-database-saas-tutorial.md)</span><span class="sxs-lookup"><span data-stu-id="e1bf6-113">toodeploy in less than five minutes, see [Deploy and explore hello Wingtip SaaS application](sql-database-saas-tutorial.md)</span></span>
* <span data-ttu-id="e1bf6-114">O Azure PowerShell está instalado.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-114">Azure PowerShell is installed.</span></span> <span data-ttu-id="e1bf6-115">Para obter mais detalhes, veja [Introdução ao Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span><span class="sxs-lookup"><span data-stu-id="e1bf6-115">For details, see [Getting started with Azure PowerShell](https://docs.microsoft.com/powershell/azure/get-started-azureps)</span></span>
* <span data-ttu-id="e1bf6-116">Olá mais recente versão do SQL Server Management Studio (SSMS) está instalada.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-116">hello latest version of SQL Server Management Studio (SSMS) is installed.</span></span> [<span data-ttu-id="e1bf6-117">Transferir e instalar o SSMS</span><span class="sxs-lookup"><span data-stu-id="e1bf6-117">Download and Install SSMS</span></span>](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)

## <a name="tenant-operational-analytics-pattern"></a><span data-ttu-id="e1bf6-118">Padrão de Análise Operacional de Inquilinos</span><span class="sxs-lookup"><span data-stu-id="e1bf6-118">Tenant Operational Analytics pattern</span></span>

<span data-ttu-id="e1bf6-119">Uma das oportunidades de excelente Olá com aplicações de SaaS é toouse Olá inquilino avançado dados que são armazenados na nuvem de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-119">One of hello great opportunities with SaaS applications is toouse hello rich tenant data that is stored in hello cloud.</span></span> <span data-ttu-id="e1bf6-120">Utilize este dados toogain aprofundadas operação Olá e a utilização da sua aplicação e inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-120">Use this data toogain insights into hello operation and usage of your application, and your tenants.</span></span> <span data-ttu-id="e1bf6-121">Estes dados podem ajudá desenvolvimento da funcionalidade, melhoramentos de Facilidade de utilização e outros investimentos na aplicação Olá e plataforma.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-121">This data can guide feature development, usability improvements, and other investments in hello app and platform.</span></span> <span data-ttu-id="e1bf6-122">O acesso a estes dados é fácil quando existir uma única base de dados multi-inquilino, mas não será tão fácil quando existir uma distribuição à escala através de potencialmente milhares de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-122">Accessing this data when it's in a single multi-tenant database is easy, but not so easy when distributed at scale across potentially thousands of databases.</span></span> <span data-ttu-id="e1bf6-123">Uma abordagem tooaccessing estes dados são toouse as tarefas elásticas, que permitem o resultado a devolver resultados da consulta da tarefa execução toobe capturada numa base de dados de saída e a tabela.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-123">One approach tooaccessing this data is toouse Elastic jobs, which enable result-returning query results from job execution toobe captured in an output database and table.</span></span>

## <a name="get-hello-wingtip-application-scripts"></a><span data-ttu-id="e1bf6-124">Obter Olá Wingtip aplicação scripts</span><span class="sxs-lookup"><span data-stu-id="e1bf6-124">Get hello Wingtip application scripts</span></span>

<span data-ttu-id="e1bf6-125">Olá Wingtip SaaS scripts e código fonte da aplicação estão disponíveis no Olá [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) repositório do github.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-125">hello Wingtip SaaS scripts and application source code are available in hello [WingtipSaaS](https://github.com/Microsoft/WingtipSaaS) github repo.</span></span> <span data-ttu-id="e1bf6-126">[Os passos scripts de Wingtip SaaS toodownload Olá](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span><span class="sxs-lookup"><span data-stu-id="e1bf6-126">[Steps toodownload hello Wingtip SaaS scripts](sql-database-wtp-overview.md#download-and-unblock-the-wingtip-saas-scripts).</span></span>

## <a name="deploy-a-database-for-tenant-analytics-results"></a><span data-ttu-id="e1bf6-127">Implementar uma base de dados dos resultados da análise de inquilinos</span><span class="sxs-lookup"><span data-stu-id="e1bf6-127">Deploy a database for tenant analytics results</span></span>

<span data-ttu-id="e1bf6-128">Este tutorial requer toohave que Olá de toocapture implementada uma base de dados resultante da execução da tarefa de scripts, que contêm a devolver resultados de consultas.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-128">This tutorial requires you toohave a database deployed toocapture hello results from job execution of scripts, which contain results-returning queries.</span></span> <span data-ttu-id="e1bf6-129">Vamos criar uma base de dados chamada tenantanalytics para esta finalidade.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-129">Let's create a database called tenantanalytics for this purpose.</span></span>

1. <span data-ttu-id="e1bf6-130">Abra... \\Learning módulos\\análise operacional\\inquilino análise\\*demonstração TenantAnalyticsDB.ps1* no Olá *ISE do PowerShell* e defina Olá seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-130">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="e1bf6-131">**$DemoScenario** = **2** *Implementar a base de dados da análise operacional*</span><span class="sxs-lookup"><span data-stu-id="e1bf6-131">**$DemoScenario** = **2** *Deploy operational analytics database*</span></span>
1. <span data-ttu-id="e1bf6-132">Prima **F5** script de demonstração de Olá toorun (que Olá chamadas *implementar TenantAnalyticsDB.ps1* script) que cria Olá inquilino análise da base de dados.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-132">Press **F5** toorun hello demo script (that calls hello *Deploy-TenantAnalyticsDB.ps1* script) which creates hello tenant analytics database.</span></span>

## <a name="create-some-data-for-hello-demo"></a><span data-ttu-id="e1bf6-133">Criar alguns dados de demonstração de Olá</span><span class="sxs-lookup"><span data-stu-id="e1bf6-133">Create some data for hello demo</span></span>

1. <span data-ttu-id="e1bf6-134">Abra... \\Learning módulos\\análise operacional\\inquilino análise\\*demonstração TenantAnalyticsDB.ps1* no Olá *ISE do PowerShell* e defina Olá seguinte valor:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-134">Open …\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*Demo-TenantAnalyticsDB.ps1* in hello *PowerShell ISE* and set hello following value:</span></span>
   * <span data-ttu-id="e1bf6-135">**$DemoScenario** = **1** *Comprar bilhetes para eventos em todos os locais*</span><span class="sxs-lookup"><span data-stu-id="e1bf6-135">**$DemoScenario** = **1** *Purchase tickets for events at all venues*</span></span>
1. <span data-ttu-id="e1bf6-136">Prima **F5** toorun Olá script e criar pedido de compra de histórico.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-136">Press **F5** toorun hello script and create ticket purchasing history.</span></span>


## <a name="create-a-scheduled-job-tooretrieve-tenant-analytics-about-ticket-purchases"></a><span data-ttu-id="e1bf6-137">Criar uma análise de inquilino de tooretrieve tarefa agendada sobre compras de permissão</span><span class="sxs-lookup"><span data-stu-id="e1bf6-137">Create a scheduled job tooretrieve tenant analytics about ticket purchases</span></span>

<span data-ttu-id="e1bf6-138">Este script cria uma tooretrieve permissão compra as informações da tarefa a partir de todos os inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-138">This script creates a job tooretrieve ticket purchase information from all tenants.</span></span> <span data-ttu-id="e1bf6-139">Depois agregado numa única tabela, pode obter métricas insightful avançadas sobre a aquisição padrões entre inquilinos Olá de pedido de suporte.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-139">Once aggregated into a single table, you can gain rich insightful metrics about ticket purchasing patterns across hello tenants.</span></span>

1. <span data-ttu-id="e1bf6-140">Abra o SSMS e ligue toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor</span><span class="sxs-lookup"><span data-stu-id="e1bf6-140">Open SSMS and connect toohello catalog-&lt;user&gt;.database.windows.net server</span></span>
1. <span data-ttu-id="e1bf6-141">Abra ...\\Módulos de Aprendizagem\\Análise Operacional\\Análise de Inquilinos\\*TicketPurchasesfromAllTenants.sql*</span><span class="sxs-lookup"><span data-stu-id="e1bf6-141">Open ...\\Learning Modules\\Operational Analytics\\Tenant Analytics\\*TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="e1bf6-142">Modificar &lt;utilizador&gt;, nome de utilizador de Olá de utilização utilizado quando implementou a aplicação de Wingtip SaaS Olá, Olá parte superior do script Olá, **sp\_adicionar\_destino\_grupo\_membro** e **sp\_adicionar\_passo de tarefa**</span><span class="sxs-lookup"><span data-stu-id="e1bf6-142">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app at hello top of hello script, **sp\_add\_target\_group\_member** and **sp\_add\_jobstep**</span></span>
1. <span data-ttu-id="e1bf6-143">Clique com o botão direito, selecione **ligação**e ligar toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor, se ainda não estiver ligado</span><span class="sxs-lookup"><span data-stu-id="e1bf6-143">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="e1bf6-144">Certifique-se de que estão ligado toohello **jobaccount** base de dados e prima **F5** para executar o script de Olá</span><span class="sxs-lookup"><span data-stu-id="e1bf6-144">Ensure you are connected toohello **jobaccount** database and press **F5** to run hello script</span></span>

* <span data-ttu-id="e1bf6-145">**SP\_adicionar\_destino\_grupo** cria o nome do grupo de destino Olá *TenantGroup*, agora é preciso tooadd membros de destino.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-145">**sp\_add\_target\_group** creates hello target group name *TenantGroup*, now we need tooadd target members.</span></span>
* <span data-ttu-id="e1bf6-146">**SP\_adicionar\_destino\_grupo\_membro** adiciona um *servidor* tipo de membro, considere todas as bases de dados dentro do que (tenha em atenção é Olá customer1 - o servidor de destino &lt;Utilizador&gt; server com bases de dados de inquilino de Olá) no momento da tarefa de execução deve ser incluída na tarefa de Olá.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-146">**sp\_add\_target\_group\_member** adds a *server* target member type, which deems all databases within that server (note this is hello customer1-&lt;User&gt; server containing hello tenant databases) at time of job execution should be included in hello job.</span></span>
* <span data-ttu-id="e1bf6-147">**sp\_add\_job** cria uma nova tarefa semanal agendada denominada “Compras de Bilhetes de Todos os Inquilinos”</span><span class="sxs-lookup"><span data-stu-id="e1bf6-147">**sp\_add\_job** creates a new weekly scheduled job called “Ticket Purchases from all Tenants”</span></span>
* <span data-ttu-id="e1bf6-148">**SP\_adicionar\_passo** cria o passo da tarefa Olá contendo tooretrieve de texto de comando T-SQL todas as informações de compra de permissão de Olá de todos os inquilinos e Olá cópia devolver resultados para uma tabela chamada  *AllTicketsPurchasesfromAllTenants*</span><span class="sxs-lookup"><span data-stu-id="e1bf6-148">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called *AllTicketsPurchasesfromAllTenants*</span></span>
* <span data-ttu-id="e1bf6-149">vistas de restantes Olá no script de Olá apresentam existência Olá de objetos de Olá e execução da tarefa de monitorização.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-149">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="e1bf6-150">Reveja o valor de estado de Olá de Olá **ciclo de vida** estado de Olá toomonitor de coluna.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-150">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="e1bf6-151">Uma vez, foi concluída com êxito, a tarefa de Olá foi concluída com êxito em todas as bases de dados do inquilino e de Olá duas bases de dados adicionais, que contém Olá referenciam tabela.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-151">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>

<span data-ttu-id="e1bf6-152">Com êxito a executar o script de Olá deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-152">Successfully running hello script should result in similar results:</span></span>

![resultados](media/sql-database-saas-tutorial-tenant-analytics/ticket-purchases-job.png)

## <a name="create-a-job-tooretrieve-a-summary-count-of-ticket-purchases-from-all-tenants"></a><span data-ttu-id="e1bf6-154">Criar um tooretrieve tarefa adquire uma contagem de resumo de permissão de todos os inquilinos</span><span class="sxs-lookup"><span data-stu-id="e1bf6-154">Create a job tooretrieve a summary count of ticket purchases from all tenants</span></span>

<span data-ttu-id="e1bf6-155">Este script cria uma soma de tooretrieve de tarefa de todas as compras de permissão de todos os inquilinos.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-155">This script creates a job tooretrieve sum of all ticket purchases from all tenants.</span></span>

1. <span data-ttu-id="e1bf6-156">Abra o SSMS e ligue toohello *catálogo -&lt;utilizador&gt;. database.windows.net* servidor</span><span class="sxs-lookup"><span data-stu-id="e1bf6-156">Open SSMS and connect toohello *catalog-&lt;User&gt;.database.windows.net* server</span></span>
1. <span data-ttu-id="e1bf6-157">Ficheiro aberto Olá... \\Learning módulos\\aprovisionar e catálogo\\análise operacional\\inquilino análise\\*TicketPurchasesfromAllTenants.sql resultados*</span><span class="sxs-lookup"><span data-stu-id="e1bf6-157">Open hello file …\\Learning Modules\\Provision and Catalog\\Operational Analytics\\Tenant Analytics\\*Results-TicketPurchasesfromAllTenants.sql*</span></span>
1. <span data-ttu-id="e1bf6-158">Modificar &lt;utilizador&gt;, nome de utilizador de Olá de utilização utilizado quando implementou a aplicação de Wingtip SaaS Olá no script de Olá, no Olá **sp\_adicionar\_passo** procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="e1bf6-158">Modify &lt;User&gt;, use hello user name used when you deployed hello Wingtip SaaS app in hello script, in hello **sp\_add\_jobstep** stored procedure</span></span>
1. <span data-ttu-id="e1bf6-159">Clique com o botão direito, selecione **ligação**e ligar toohello catálogo -&lt;utilizador&gt;. database.windows.net servidor, se ainda não estiver ligado</span><span class="sxs-lookup"><span data-stu-id="e1bf6-159">Right click, select **Connection**, and connect toohello catalog-&lt;User&gt;.database.windows.net server, if not already connected</span></span>
1. <span data-ttu-id="e1bf6-160">Certifique-se de que estão ligado toohello **tenantanalytics** base de dados e prima **F5** para executar o script de Olá</span><span class="sxs-lookup"><span data-stu-id="e1bf6-160">Ensure you are connected toohello **tenantanalytics** database and press **F5** to run hello script</span></span>

<span data-ttu-id="e1bf6-161">Com êxito a executar o script de Olá deve resultar em resultados semelhantes:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-161">Successfully running hello script should result in similar results:</span></span>

![resultados](media/sql-database-saas-tutorial-tenant-analytics/total-sales.png)



* <span data-ttu-id="e1bf6-163">**sp\_add\_job** cria uma nova tarefa agendada semanal denominada “ResultsTicketsOrders”</span><span class="sxs-lookup"><span data-stu-id="e1bf6-163">**sp\_add\_job** creates a new weekly scheduled job called “ResultsTicketsOrders”</span></span>

* <span data-ttu-id="e1bf6-164">**SP\_adicionar\_passo** cria o passo da tarefa Olá contendo tooretrieve de texto de comando T-SQL todas as informações de compra de permissão de Olá de todos os inquilinos e Olá cópia devolver resultados para uma tabela chamada CountofTicketOrders</span><span class="sxs-lookup"><span data-stu-id="e1bf6-164">**sp\_add\_jobstep** creates hello job step containing T-SQL command text tooretrieve all hello ticket purchase information from all tenants and copy hello returning result set into a table called CountofTicketOrders</span></span>

* <span data-ttu-id="e1bf6-165">vistas de restantes Olá no script de Olá apresentam existência Olá de objetos de Olá e execução da tarefa de monitorização.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-165">hello remaining views in hello script display hello existence of hello objects and monitor job execution.</span></span> <span data-ttu-id="e1bf6-166">Reveja o valor de estado de Olá de Olá **ciclo de vida** estado de Olá toomonitor de coluna.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-166">Review hello status value from hello **lifecycle** column toomonitor hello status.</span></span> <span data-ttu-id="e1bf6-167">Uma vez, foi concluída com êxito, a tarefa de Olá foi concluída com êxito em todas as bases de dados do inquilino e de Olá duas bases de dados adicionais, que contém Olá referenciam tabela.</span><span class="sxs-lookup"><span data-stu-id="e1bf6-167">Once, Succeeded, hello job has successfully finished on all tenant databases and hello two additional databases containing hello reference table.</span></span>


## <a name="next-steps"></a><span data-ttu-id="e1bf6-168">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e1bf6-168">Next steps</span></span>

<span data-ttu-id="e1bf6-169">Neste tutorial, ficou a saber como:</span><span class="sxs-lookup"><span data-stu-id="e1bf6-169">In this tutorial you learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="e1bf6-170">Implementar a base de dados de análise de inquilinos</span><span class="sxs-lookup"><span data-stu-id="e1bf6-170">Deploy a tenant analytics database</span></span>
> * <span data-ttu-id="e1bf6-171">Criar uma tarefa agendada tooretrieve analítico de dados entre inquilinos</span><span class="sxs-lookup"><span data-stu-id="e1bf6-171">Create a scheduled job tooretrieve analytical data across tenants</span></span>

<span data-ttu-id="e1bf6-172">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="e1bf6-172">Congratulations!</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e1bf6-173">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="e1bf6-173">Additional resources</span></span>

* <span data-ttu-id="e1bf6-174">Adicionais [tutoriais baseiam Olá aplicação Wingtip SaaS](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span><span class="sxs-lookup"><span data-stu-id="e1bf6-174">Additional [tutorials that build upon hello Wingtip SaaS application](sql-database-wtp-overview.md#sql-database-wingtip-saas-tutorials)</span></span>
* [<span data-ttu-id="e1bf6-175">Tarefas elásticas</span><span class="sxs-lookup"><span data-stu-id="e1bf6-175">Elastic Jobs</span></span>](sql-database-elastic-jobs-overview.md)
