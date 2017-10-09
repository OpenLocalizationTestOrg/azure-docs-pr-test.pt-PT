---
title: aaaManage bases de dados no Azure SQL Data Warehouse | Microsoft Docs
description: "Descrição geral da gestão de bases de dados do armazém de dados do SQL Server. Inclui ferramentas de gestão, as DWUs e o desempenho de escalamento horizontal, resolução de problemas de desempenho das consultas, estabelecer políticas boa segurança e restaurar uma base de dados de Corrupção de dados ou a partir de uma falha regional."
services: sql-data-warehouse
documentationcenter: NA
author: kevinvngo
manager: jhubbard
editor: 
ms.assetid: 8576fdb3-71fe-4b3b-a4e0-5e8a7f148acf
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: manage
ms.date: 10/31/2016
ms.author: kevin;barbkess
ms.openlocfilehash: caec6572c4ab395107c3b095adc69a53eae8bd88
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-databases-in-azure-sql-data-warehouse"></a><span data-ttu-id="7e911-104">Gerir bases de dados no Azure SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7e911-104">Manage databases in Azure SQL Data Warehouse</span></span>
<span data-ttu-id="7e911-105">O SQL Data Warehouse automatiza vários aspetos da gestão de bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7e911-105">SQL Data Warehouse automates many aspects of managing your databases.</span></span> <span data-ttu-id="7e911-106">Por exemplo, desempenho tooscale basta tooadjust e paga Olá neste nível de recursos de computação e, em seguida, permitir que o SQL Data Warehouse fazê-lo a todos os Olá trabalho de ampliar e dimensionamento back.</span><span class="sxs-lookup"><span data-stu-id="7e911-106">For example, tooscale performance you only need tooadjust and pay for hello right level of compute resources, and then let SQL Data Warehouse do all hello work of scaling out and scaling back.</span></span>

<span data-ttu-id="7e911-107">Undoubtedly convém toomonitor sua tooidentify de carga de trabalho, o desempenho tem de, bem como resolver problemas relacionados com consultas de execução longa.</span><span class="sxs-lookup"><span data-stu-id="7e911-107">You will undoubtedly want toomonitor your workload tooidentify your performance needs as well as troubleshoot long-running queries.</span></span> <span data-ttu-id="7e911-108">Também terá de tooperform algumas tarefas toomanage as permissões de segurança para utilizadores e os inícios de sessão.</span><span class="sxs-lookup"><span data-stu-id="7e911-108">You will also need tooperform a few security tasks toomanage permissions for users and logins.</span></span>

<span data-ttu-id="7e911-109">Esta descrição geral inclui estes aspetos da gestão do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e911-109">This overview covers these aspects of managing SQL Data Warehouse.</span></span>

* <span data-ttu-id="7e911-110">Ferramentas de gestão</span><span class="sxs-lookup"><span data-stu-id="7e911-110">Management tools</span></span>
* <span data-ttu-id="7e911-111">Dimensionar a computação</span><span class="sxs-lookup"><span data-stu-id="7e911-111">Scale Compute</span></span>
* <span data-ttu-id="7e911-112">Colocar em pausa e retomar</span><span class="sxs-lookup"><span data-stu-id="7e911-112">Pause and Resume</span></span>
* <span data-ttu-id="7e911-113">Melhores práticas do desempenho</span><span class="sxs-lookup"><span data-stu-id="7e911-113">Performance Best Practices</span></span>
* <span data-ttu-id="7e911-114">Monitorização de consulta</span><span class="sxs-lookup"><span data-stu-id="7e911-114">Query Monitoring</span></span>
* <span data-ttu-id="7e911-115">Segurança</span><span class="sxs-lookup"><span data-stu-id="7e911-115">Security</span></span>
* <span data-ttu-id="7e911-116">Cópia de segurança e restauro</span><span class="sxs-lookup"><span data-stu-id="7e911-116">Backup and restore</span></span>

## <a name="management-tools"></a><span data-ttu-id="7e911-117">Ferramentas de gestão</span><span class="sxs-lookup"><span data-stu-id="7e911-117">Management tools</span></span>
<span data-ttu-id="7e911-118">Pode utilizar uma variedade de bases de dados de toomanage de ferramentas no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7e911-118">You can use a variety of tools toomanage databases in SQL Data Warehouse.</span></span> <span data-ttu-id="7e911-119">Como gerir bases de dados, irá desenvolver as preferências de ferramenta para cada tipo de tarefa terá tooperform.</span><span class="sxs-lookup"><span data-stu-id="7e911-119">As you manage databases, you will develop tool preferences for each type of task you need tooperform.</span></span>

### <a name="azure-portal"></a><span data-ttu-id="7e911-120">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="7e911-120">Azure portal</span></span>
<span data-ttu-id="7e911-121">Olá [portal do Azure] [ Azure portal] é um portal baseado na web, onde pode criar, atualizar e eliminar as bases de dados-las e monitorizar os recursos de base de dados.</span><span class="sxs-lookup"><span data-stu-id="7e911-121">hello [Azure portal][Azure portal] is a web-based portal where you can create, update, and delete databases and monitor database resources.</span></span> <span data-ttu-id="7e911-122">Esta ferramenta é uma grande é se que está a começar com o Azure, gerir um pequeno número de bases de dados, ou precisar de tooquickly fazer algo.</span><span class="sxs-lookup"><span data-stu-id="7e911-122">This tool is great is if you're just getting started with Azure, managing a small number of data warehouse databases, or need tooquickly do something.</span></span>

<span data-ttu-id="7e911-123">tooget começar Olá portal do Azure, consulte [criar um SQL Data Warehouse (portal do Azure)][Create a SQL Data Warehouse (Azure portal)].</span><span class="sxs-lookup"><span data-stu-id="7e911-123">tooget started with hello Azure portal, see [Create a SQL Data Warehouse (Azure portal)][Create a SQL Data Warehouse (Azure portal)].</span></span>

### <a name="sql-server-data-tools-in-visual-studio"></a><span data-ttu-id="7e911-124">Ferramentas de dados do SQL Server no Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7e911-124">SQL Server Data Tools in Visual Studio</span></span>
<span data-ttu-id="7e911-125">[SQL Server Data Tools] [ SQL Server Data Tools] (SSDT) no Visual Studio permite-lhe tooconnect gerir e desenvolver as bases de dados.</span><span class="sxs-lookup"><span data-stu-id="7e911-125">[SQL Server Data Tools][SQL Server Data Tools] (SSDT) in Visual Studio allows you tooconnect to, manage, and develop your databases.</span></span> <span data-ttu-id="7e911-126">Se tiver um programador de aplicações familiarizado com o Visual Studio ou outros ambientes de desenvolvimento integrado (IDEs), experimente utilizar SSDT no Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="7e911-126">If you're an application developer familiar with Visual Studio or other integrated development environments (IDEs), try using SSDT in Visual Studio.</span></span>

<span data-ttu-id="7e911-127">SSDT inclui Olá SQL Server Object Explorer que lhe permite toovisualize, ligar e executar scripts em bases de dados do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e911-127">SSDT includes hello SQL Server Object Explorer which enables you toovisualize, connect, and execute scripts against SQL Data Warehouse databases.</span></span> <span data-ttu-id="7e911-128">tooquickly ligar tooSQL do armazém de dados, basta clicar em Olá **abrir no Visual Studio** botão na barra de comando Olá quando visualiza detalhes de base de dados de Olá em Olá Portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="7e911-128">tooquickly connect tooSQL Data Warehouse, you can simply click hello **Open in Visual Studio** button in hello command bar when viewing hello database details in hello Azure Classic Portal.</span></span>  

<span data-ttu-id="7e911-129">tooget iniciado com SSDT no Visual Studio, consulte [consultar o Azure SQL Data Warehouse com o Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span><span class="sxs-lookup"><span data-stu-id="7e911-129">tooget started with SSDT in Visual Studio, see [Query Azure SQL Data Warehouse with Visual Studio][Query Azure SQL Data Warehouse with Visual Studio].</span></span>

### <a name="command-line-tools"></a><span data-ttu-id="7e911-130">Ferramentas de linha de comandos</span><span class="sxs-lookup"><span data-stu-id="7e911-130">Command-line tools</span></span>
<span data-ttu-id="7e911-131">Ferramentas de linha de comandos são ideais para automatizar as cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7e911-131">Command line tools are ideal for automating your workloads.</span></span>  <span data-ttu-id="7e911-132">PowerShell sqlcmd, sendo duas formas excelente tooautomate os processos.</span><span class="sxs-lookup"><span data-stu-id="7e911-132">PowerShell and sqlcmd are two great ways tooautomate your processes.</span></span>  <span data-ttu-id="7e911-133">Recomendamos que estas ferramentas para gerir um grande número de servidores de lógicas e implementar as alterações de recursos num ambiente de produção como tarefas de Olá necessárias podem ser convertidos em script e, em seguida, automatizadas.</span><span class="sxs-lookup"><span data-stu-id="7e911-133">We recommend these tools for managing a large number of logical servers and deploying resource changes in a production environment as hello tasks necessary can be scripted and then automated.</span></span>

### <a name="dynamic-management-views"></a><span data-ttu-id="7e911-134">Vistas de gestão dinâmica</span><span class="sxs-lookup"><span data-stu-id="7e911-134">Dynamic management views</span></span>
<span data-ttu-id="7e911-135">DMVs são Olá bread e butter da gestão do armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e911-135">DMVs are hello bread and butter of managing SQL Data Warehouse.</span></span> <span data-ttu-id="7e911-136">Quase todas as informações que analisa no portal de Olá depende DMVs.</span><span class="sxs-lookup"><span data-stu-id="7e911-136">Almost all information that surfaces in hello portal relies on DMVs.</span></span> <span data-ttu-id="7e911-137">toosee uma lista de DMVs de armazém de dados do SQL Server, consulte [vistas de sistema do SQL Data Warehouse][SQL Data Warehouse system views].</span><span class="sxs-lookup"><span data-stu-id="7e911-137">toosee a list of SQL Data Warehouse DMVs, see [SQL Data Warehouse system views][SQL Data Warehouse system views].</span></span>

<span data-ttu-id="7e911-138">tooget iniciado, consulte [ligar e consultar com sqlcmd][Connect and query with sqlcmd], e [criar uma base de dados (PowerShell)][Create a database (PowerShell)].</span><span class="sxs-lookup"><span data-stu-id="7e911-138">tooget started, see [Connect and query with sqlcmd][Connect and query with sqlcmd], and [Create a database (PowerShell)][Create a database (PowerShell)].</span></span>

## <a name="scale-compute"></a><span data-ttu-id="7e911-139">Dimensionar a computação</span><span class="sxs-lookup"><span data-stu-id="7e911-139">Scale compute</span></span>
<span data-ttu-id="7e911-140">No SQL Data Warehouse, pode dimensionar rapidamente o desempenho out ou retroceder por aumente ou diminua a recursos de computação de CPU, memória e largura de banda de e/s.</span><span class="sxs-lookup"><span data-stu-id="7e911-140">In SQL Data Warehouse, you can quickly scale performance out or back by increasing or decreasing compute resources of CPU, memory, and I/O bandwidth.</span></span> <span data-ttu-id="7e911-141">desempenho de tooscale, tudo o que precisa toodo é ajuste Olá número de unidades do data warehouse (DWUs) que o SQL Data Warehouse aloca tooyour base de dados.</span><span class="sxs-lookup"><span data-stu-id="7e911-141">tooscale performance, all you need toodo is adjust hello number of data warehouse units (DWUs) that SQL Data Warehouse allocates tooyour database.</span></span> <span data-ttu-id="7e911-142">O SQL Data Warehouse rapidamente torna Olá alterar e processa todos os Olá subjacente alterações toohardware ou software.</span><span class="sxs-lookup"><span data-stu-id="7e911-142">SQL Data Warehouse quickly makes hello change and handles all hello underlying changes toohardware or software.</span></span>

<span data-ttu-id="7e911-143">toolearn mais informações sobre dimensionamento DWUs, consulte [Dimensionar desempenho].</span><span class="sxs-lookup"><span data-stu-id="7e911-143">toolearn more about scaling DWUs, see [Scale performance].</span></span>

## <a name="pause-and-resume"></a><span data-ttu-id="7e911-144">Colocar em pausa e retomar</span><span class="sxs-lookup"><span data-stu-id="7e911-144">Pause and resume</span></span>
<span data-ttu-id="7e911-145">custos de toosave, pode colocar em pausa e retomar computação recursos a pedido.</span><span class="sxs-lookup"><span data-stu-id="7e911-145">toosave costs, you can pause and resume compute resources on-demand.</span></span> <span data-ttu-id="7e911-146">Por exemplo, se não utilizar a base de dados de Olá durante a noite Olá e no fim de semana, pode colocar em pausa-lo durante essas horas e retomá-lo durante o dia de Olá.</span><span class="sxs-lookup"><span data-stu-id="7e911-146">For example, if you won't be using hello database during hello night and on weekends, you can pause it during those times, and resume it during hello day.</span></span> <span data-ttu-id="7e911-147">Não lhe será cobrado dwus enquanto a base de dados de Olá está em pausa.</span><span class="sxs-lookup"><span data-stu-id="7e911-147">You won't be charged for DWUs while hello database is paused.</span></span>

<span data-ttu-id="7e911-148">Para obter mais informações, consulte [colocar em pausa computação][Pause compute], e [retomar a computação][Resume compute].</span><span class="sxs-lookup"><span data-stu-id="7e911-148">For more information, see [Pause compute][Pause compute], and [Resume compute][Resume compute].</span></span>

## <a name="performance-best-practices"></a><span data-ttu-id="7e911-149">Melhores práticas do desempenho</span><span class="sxs-lookup"><span data-stu-id="7e911-149">Performance Best Practices</span></span>
<span data-ttu-id="7e911-150">Quando a introdução com uma nova tecnologia, detetar truques que funcionam melhor direito de início de Olá e sugestões de Olá pode poupar muitos de tempo.</span><span class="sxs-lookup"><span data-stu-id="7e911-150">When getting started with a new technology, discovering hello tips and tricks that work best right from hello start can save you lots of time.</span></span>  <span data-ttu-id="7e911-151">Encontrará as melhores práticas ao longo de muitos dos nossos tópicos.</span><span class="sxs-lookup"><span data-stu-id="7e911-151">You will find best practices throughout many of our topics.</span></span>

<span data-ttu-id="7e911-152">toosee muitos um resumo das considerações mais importantes de Olá quando desenvolver a sua carga de trabalho, consulte [melhores práticas do SQL Data Warehouse][SQL Data Warehouse Best Practices].</span><span class="sxs-lookup"><span data-stu-id="7e911-152">toosee many a summary of hello most important considerations when developing your workload, see [SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices].</span></span>

## <a name="query-monitoring"></a><span data-ttu-id="7e911-153">Monitorização de consulta</span><span class="sxs-lookup"><span data-stu-id="7e911-153">Query Monitoring</span></span>
<span data-ttu-id="7e911-154">Por vezes, uma consulta está a ser executado demasiado tempo, mas não é Certifique-se de que é culprit Olá.</span><span class="sxs-lookup"><span data-stu-id="7e911-154">Sometimes a query is running too long, but you aren't sure of which one is hello culprit.</span></span> <span data-ttu-id="7e911-155">O SQL Data Warehouse tem vistas de gestão dinâmica (DMVs) que pode utilizar toofigure saída que consulta está a demorar demasiado tempo.</span><span class="sxs-lookup"><span data-stu-id="7e911-155">SQL Data Warehouse has dynamic management views (DMVs) that you can use toofigure out which query is taking too long.</span></span>

<span data-ttu-id="7e911-156">consultas de execução longa toofind, consulte [monitorizar a carga de trabalho com DMVs][Monitor your workload using DMVs].</span><span class="sxs-lookup"><span data-stu-id="7e911-156">toofind long-running queries, see [Monitor your workload using DMVs][Monitor your workload using DMVs].</span></span>

## <a name="security"></a><span data-ttu-id="7e911-157">Segurança</span><span class="sxs-lookup"><span data-stu-id="7e911-157">Security</span></span>
<span data-ttu-id="7e911-158">toomaintain um sistema seguro, tem de estar num alerta Olá e proteger contra qualquer tipo de acesso não autorizado.</span><span class="sxs-lookup"><span data-stu-id="7e911-158">toomaintain a secure system, you must be on hello alert and guard against any type of unauthorized access.</span></span> <span data-ttu-id="7e911-159">Um sistema de segurança tem toomake se as regras de firewall estão em vigor autorizado para apenas endereços IP podem ligar.</span><span class="sxs-lookup"><span data-stu-id="7e911-159">A security system needs toomake sure firewall rules are in place so only authorized IP addresses can connect.</span></span> <span data-ttu-id="7e911-160">Necessita de uma autenticação adequada das credenciais do utilizador.</span><span class="sxs-lookup"><span data-stu-id="7e911-160">It needs proper authentication of user credentials.</span></span> <span data-ttu-id="7e911-161">Depois de um utilizador tenha ligado toohello base de dados, Olá utilizador deve apenas tem permissões tooperform um número mínimo de ações.</span><span class="sxs-lookup"><span data-stu-id="7e911-161">After a user has connected toohello database, hello user should only have permissions tooperform a minimal number of actions.</span></span> <span data-ttu-id="7e911-162">toosecure dados, pode utilizar a encriptação.</span><span class="sxs-lookup"><span data-stu-id="7e911-162">toosecure data, you can use encryption.</span></span> <span data-ttu-id="7e911-163">Também é importante toohave auditoria e controlo para pode retrace eventos se não houver qualquer atividade suspeita.</span><span class="sxs-lookup"><span data-stu-id="7e911-163">It's also important toohave auditing and tracking so you can retrace events if there is any suspicious activity.</span></span>

<span data-ttu-id="7e911-164">toolearn sobre a gestão de segurança, head através de toohello [descrição geral de segurança][Security overview].</span><span class="sxs-lookup"><span data-stu-id="7e911-164">toolearn about managing security, head over toohello [Security overview][Security overview].</span></span>

## <a name="backup-and-restore"></a><span data-ttu-id="7e911-165">Cópia de segurança e restauro</span><span class="sxs-lookup"><span data-stu-id="7e911-165">Backup and restore</span></span>
<span data-ttu-id="7e911-166">Ter backps fiável dos seus dados é uma parte essencial dos qualquer base de dados de produção.</span><span class="sxs-lookup"><span data-stu-id="7e911-166">Having reliable backps of your data is an essential part of any production database.</span></span> <span data-ttu-id="7e911-167">Armazém de dados do SQL Server mantém os seus dados seguros por automaticamente fazer cópias de segurança das bases de dados do Active Directory em intervalos regulares.</span><span class="sxs-lookup"><span data-stu-id="7e911-167">SQL Data Warehouse keeps your data safe by automatically backing up your active databases at regular intervals.</span></span> <span data-ttu-id="7e911-168">Estas cópias de segurança permitem-lhe toorecover de cenários em que tiver danificado os dados ou acidentalmente ignorados os dados ou a base de dados.</span><span class="sxs-lookup"><span data-stu-id="7e911-168">These backups allow you toorecover from scenarios where you've corrupted your data or accidentally dropped your data or database.</span></span>  <span data-ttu-id="7e911-169">Para a agenda de cópia de segurança de dados Olá, política de retenção e como toorestore uma base de dados, consulte [restaurar a partir do instantâneo][Restore from snapshot].</span><span class="sxs-lookup"><span data-stu-id="7e911-169">For hello data backup schedule, retention policy and how toorestore a database, see [Restore from snapshot][Restore from snapshot].</span></span>

## <a name="next-steps"></a><span data-ttu-id="7e911-170">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7e911-170">Next steps</span></span>
<span data-ttu-id="7e911-171">A utilização de princípios de design da base de dados boa tornarão mais fácil toomanage as bases de dados no armazém de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="7e911-171">Using good database design principles will make it easier toomanage your databases in SQL Data Warehouse.</span></span> <span data-ttu-id="7e911-172">toolearn mais, head através de toohello [descrição geral do desenvolvimento][Development overview].</span><span class="sxs-lookup"><span data-stu-id="7e911-172">toolearn more, head over toohello [Development overview][Development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Create a SQL Data Warehouse (Azure Portal)]: sql-data-warehouse-get-started-provision.md
[Create a database (PowerShell)]: sql-data-warehouse-get-started-provision-powershell.md
[connection]: sql-data-warehouse-develop-connections.md
[Query Azure SQL Data Warehouse with Visual Studio]: sql-data-warehouse-query-visual-studio.md
[Connect and query with sqlcmd]: sql-data-warehouse-get-started-connect-sqlcmd.md
[Development overview]: sql-data-warehouse-overview-develop.md
[Monitor your workload using DMVs]: sql-data-warehouse-manage-monitor.md
[Pause compute]: sql-data-warehouse-manage-compute-overview.md#pause-compute-bk
[Restore from snapshot]: sql-data-warehouse-restore-database-overview.md
[Resume compute]: sql-data-warehouse-manage-compute-overview.md#resume-compute-bk
[Dimensionar desempenho]: sql-data-warehouse-manage-compute-overview.md#scale-compute
[Security overview]: sql-data-warehouse-overview-manage-security.md
[SQL Data Warehouse Best Practices]: sql-data-warehouse-best-practices.md
[SQL Data Warehouse system views]: sql-data-warehouse-reference-tsql-system-views.md

<!--MSDN references-->
[SQL Server Data Tools]: https://msdn.microsoft.com/library/mt204009.aspx

<!--Other web references-->
[Azure portal]: http://portal.azure.com/
