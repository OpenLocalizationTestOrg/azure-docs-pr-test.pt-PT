---
title: aaaAuditing no Azure SQL Data Warehouse | Microsoft Docs
description: "Introdução ao Azure SQL Data Warehouse de auditoria"
services: sql-data-warehouse
documentationcenter: 
author: ronortloff
manager: jhubbard
editor: 
ms.assetid: 0e6af148-b218-4b43-bb5f-907917d20330
ms.service: sql-data-warehouse
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: security
ms.date: 08/21/2017
ms.author: rortloff;barbkess
ms.openlocfilehash: 948de74fa052ef206cf1aa65c0d81f084b18cb00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="auditing-in-azure-sql-data-warehouse"></a><span data-ttu-id="cb5d4-103">Auditoria no armazém de dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5d4-103">Auditing in Azure SQL Data Warehouse</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="cb5d4-104">Auditoria</span><span class="sxs-lookup"><span data-stu-id="cb5d4-104">Auditing</span></span>](sql-data-warehouse-auditing-overview.md)
> * [<span data-ttu-id="cb5d4-105">Deteção de ameaças</span><span class="sxs-lookup"><span data-stu-id="cb5d4-105">Threat detection</span></span>](sql-data-warehouse-security-threat-detection.md)
> 
> 

<span data-ttu-id="cb5d4-106">Auditoria de SQL Data Warehouse permite-lhe toorecord eventos no registo de auditoria de tooan a base de dados na sua conta do Storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-106">SQL Data Warehouse auditing allows you toorecord events in your database tooan audit log in your Azure Storage account.</span></span> <span data-ttu-id="cb5d4-107">Auditoria pode ajudar a manter a conformidade de regulamentação, compreender a atividade de base de dados e obter informações sobre discrepâncias e anomalias que poderão indicar preocupações para a empresa ou suspeitas de violação de segurança.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-107">Auditing can help you maintain regulatory compliance, understand  database activity, and gain insight into discrepancies and anomalies that could indicate business concerns or suspected security violations.</span></span> <span data-ttu-id="cb5d4-108">Auditoria de SQL Data Warehouse também integra-se com o Microsoft Power BI para desagregar relatórios e análise.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-108">SQL Data Warehouse auditing also integrates with Microsoft Power BI for drill-down reporting and analysis.</span></span>

<span data-ttu-id="cb5d4-109">As ferramentas de auditoria ativarem e facilitam as normas de toocompliance aderência, mas não garantir a compatibilidade.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-109">Auditing tools enable and facilitate adherence toocompliance standards but don't guarantee compliance.</span></span> <span data-ttu-id="cb5d4-110">Para obter mais informações sobre o Azure programas que conformidade de padrões de suporte, consulte Olá <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Centro de fidedignidade do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-110">For more information about Azure programs that support standards compliance, see hello <a href="http://azure.microsoft.com/support/trust-center/compliance/" target="_blank">Azure Trust Center</a>.</span></span>

* <span data-ttu-id="cb5d4-111">[Noções básicas de auditoria de base de dados]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-111">[Database Auditing basics]</span></span>
* <span data-ttu-id="cb5d4-112">[Configurar a auditoria da base de dados]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-112">[Set up auditing for your database]</span></span>
* <span data-ttu-id="cb5d4-113">[Analisar registos de auditoria e relatórios]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-113">[Analyze audit logs and reports]</span></span>

## <span data-ttu-id="cb5d4-114"><a id="subheading-1"></a>Noções básicas de auditoria da base de dados de armazém de dados do SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="cb5d4-114"><a id="subheading-1"></a>Azure SQL Data Warehouse Database Auditing basics</span></span>
<span data-ttu-id="cb5d4-115">Auditoria de base de dados do SQL Data Warehouse permite-lhe:</span><span class="sxs-lookup"><span data-stu-id="cb5d4-115">SQL Data Warehouse database auditing allows you to:</span></span>

* <span data-ttu-id="cb5d4-116">**Manter** um registo de auditoria de eventos selecionados.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-116">**Retain** an audit trail of selected events.</span></span> <span data-ttu-id="cb5d4-117">Pode definir categorias de base de dados ações toobe auditada.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-117">You can define categories of database actions  toobe audited.</span></span>
* <span data-ttu-id="cb5d4-118">**Relatório** na atividade de base de dados.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-118">**Report** on database activity.</span></span> <span data-ttu-id="cb5d4-119">Pode utilizar relatórios pré-configurados e tooget um dashboard a trabalhar rapidamente com atividade e o relatório de eventos.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-119">You can use preconfigured reports and a dashboard tooget started quickly with activity and event reporting.</span></span>
* <span data-ttu-id="cb5d4-120">**Analisar** relatórios.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-120">**Analyze** reports.</span></span> <span data-ttu-id="cb5d4-121">Pode encontrar eventos suspeitos, atividade invulgar e tendências.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-121">You can find suspicious events, unusual activity, and trends.</span></span>

<span data-ttu-id="cb5d4-122">Pode configurar a auditoria para Olá seguintes categorias de evento:</span><span class="sxs-lookup"><span data-stu-id="cb5d4-122">You can configure auditing for hello following event categories:</span></span>

<span data-ttu-id="cb5d4-123">**SQL simples** e **parametrizadas SQL** para que Olá registos de auditoria recolhidos são classificados como</span><span class="sxs-lookup"><span data-stu-id="cb5d4-123">**Plain SQL** and **Parameterized SQL** for which hello collected audit logs are classified as</span></span>  

* <span data-ttu-id="cb5d4-124">**Acesso toodata**</span><span class="sxs-lookup"><span data-stu-id="cb5d4-124">**Access toodata**</span></span>
* <span data-ttu-id="cb5d4-125">**Alterações do esquema (DDL)**</span><span class="sxs-lookup"><span data-stu-id="cb5d4-125">**Schema changes (DDL)**</span></span>
* <span data-ttu-id="cb5d4-126">**Alterações de dados (DML)**</span><span class="sxs-lookup"><span data-stu-id="cb5d4-126">**Data changes (DML)**</span></span>
* <span data-ttu-id="cb5d4-127">**Contas, funções e permissões (DCL)**</span><span class="sxs-lookup"><span data-stu-id="cb5d4-127">**Accounts, roles, and permissions (DCL)**</span></span>
* <span data-ttu-id="cb5d4-128">**Procedimento armazenado**, **início de sessão** e, **transação gestão**.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-128">**Stored Procedure**, **Login** and, **Transaction Management**.</span></span>

<span data-ttu-id="cb5d4-129">Para cada categoria de evento de auditoria de **êxito** e **falha** operações configuradas em separado.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-129">For each Event Category, Auditing of **Success** and **Failure** operations are configured separately.</span></span>

<span data-ttu-id="cb5d4-130">Para obter mais informações sobre atividades de Olá e os eventos auditados, consulte Olá <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">referência de formatos de registo de auditoria (transferência de ficheiro do documento)</a>.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-130">For more information about hello activities and events audited, see hello <a href="http://go.microsoft.com/fwlink/?LinkId=506733" target="_blank">Audit Log Format Reference (doc file download)</a>.</span></span>

<span data-ttu-id="cb5d4-131">Os registos de auditoria são armazenados na sua conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-131">Audit logs are stored in your Azure storage account.</span></span> <span data-ttu-id="cb5d4-132">Pode definir um período de retenção do registo de auditoria.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-132">You can define an audit log retention period.</span></span>

<span data-ttu-id="cb5d4-133">Uma política de auditoria pode ser definida para uma base de dados específica ou como uma política de servidor de predefinição.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-133">An auditing policy can be defined for a specific database or as a default server policy.</span></span> <span data-ttu-id="cb5d4-134">Uma política de auditoria do servidor predefinido aplica-se tooall bases de dados num servidor, que não dispõe de uma substituição da base de dados auditoria política específica definida.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-134">A default server auditing policy applies tooall databases on a server, which do not have a specific overriding database auditing policy defined.</span></span>

<span data-ttu-id="cb5d4-135">Antes de configurar a auditoria de auditoria de verificação se estiver a utilizar um ["Clientes de nível inferior."](sql-data-warehouse-auditing-downlevel-clients.md)</span><span class="sxs-lookup"><span data-stu-id="cb5d4-135">Before setting up audit auditing check if you are using a ["Downlevel Client."](sql-data-warehouse-auditing-downlevel-clients.md)</span></span>

## <span data-ttu-id="cb5d4-136"><a id="subheading-2"></a>Configurar a auditoria da base de dados</span><span class="sxs-lookup"><span data-stu-id="cb5d4-136"><a id="subheading-2"></a>Set up auditing for your database</span></span>
1. <span data-ttu-id="cb5d4-137">Iniciar Olá <a href="https://portal.azure.com" target="_blank">portal do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-137">Launch hello <a href="https://portal.azure.com" target="_blank">Azure portal</a>.</span></span>
2. <span data-ttu-id="cb5d4-138">Aceda toohello **definições** painel de Olá pretende tooaudit do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-138">Go toohello **Settings** blade of hello SQL Data Warehouse you want tooaudit.</span></span> <span data-ttu-id="cb5d4-139">No Olá **definições** painel, selecione **deteção de ameaças e auditoria**.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-139">In hello **Settings** blade, select **Auditing & Threat detection**.</span></span>
   
    ![][1]
3. <span data-ttu-id="cb5d4-140">Em seguida, ativar a auditoria clicando Olá **ON** botão.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-140">Next, enable auditing by clicking hello **ON** button.</span></span>
   
    ![][3]
4. <span data-ttu-id="cb5d4-141">No painel Configuração de auditoria de Olá, selecione **detalhes armazenamento** painel de armazenamento de registos de auditoria de Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-141">In hello auditing configuration blade, select **STORAGE DETAILS** tooopen hello Audit Logs Storage blade.</span></span> <span data-ttu-id="cb5d4-142">Selecione Olá conta de armazenamento do Azure onde serão guardados registos e Olá período de retenção.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-142">Select hello Azure storage account where logs will be saved and, hello retention period.</span></span> 
>[!TIP]
><span data-ttu-id="cb5d4-143">Olá utilize mesma conta de armazenamento para todos os Olá de tooget auditada bases de dados mais fora Olá pré-configurados relatórios de modelos.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-143">Use hello same storage account for all audited databases tooget hello most out of hello pre-configured reports templates.</span></span>
   
    ![][4]
5. <span data-ttu-id="cb5d4-144">Clique em Olá **OK** configuração de detalhes do botão toosave Olá armazenamento.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-144">Click hello **OK** button toosave hello storage details configuration.</span></span>
6. <span data-ttu-id="cb5d4-145">Em **registo pelo evento**, clique em **êxito** e **falha** toolog todos os eventos, ou escolha categorias de eventos individuais.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-145">Under **LOGGING BY EVENT**, click **SUCCESS** and **FAILURE** toolog all events, or choose individual event categories.</span></span>
7. <span data-ttu-id="cb5d4-146">Se estiver a configurar auditoria para uma base de dados, poderá ser necessário a cadeia de ligação de Olá tooalter do seu tooensure cliente auditoria de dados é capturado corretamente.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-146">If you are configuring Auditing for a database, you may need tooalter hello connection string of your client tooensure data auditing is correctly captured.</span></span> <span data-ttu-id="cb5d4-147">Verifique Olá [modificar FDQN de servidor na cadeia de ligação de Olá](sql-data-warehouse-auditing-downlevel-clients.md) tópico para ligações de cliente de nível inferior.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-147">Check hello [Modify Server FDQN in hello connection string](sql-data-warehouse-auditing-downlevel-clients.md) topic for downlevel client connections.</span></span>
8. <span data-ttu-id="cb5d4-148">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-148">Click **OK**.</span></span>

## <span data-ttu-id="cb5d4-149"><a id="subheading-3"></a>Analisar registos de auditoria e relatórios</span><span class="sxs-lookup"><span data-stu-id="cb5d4-149"><a id="subheading-3"></a>Analyze audit logs and reports</span></span>
<span data-ttu-id="cb5d4-150">Os registos de auditoria são agregados de uma coleção de tabelas de arquivo com um **SQLDBAuditLogs** prefixo no Olá que escolheu durante a configuração de conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-150">Audit logs are aggregated in a collection of Store Tables with a **SQLDBAuditLogs** prefix in hello Azure storage account you chose during setup.</span></span> <span data-ttu-id="cb5d4-151">Pode ver ficheiros de registo utilizando uma ferramenta como <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Explorador de armazenamento do Azure</a>.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-151">You can view log files using a tool such as <a href="http://azurestorageexplorer.codeplex.com/" target="_blank">Azure Storage Explorer</a>.</span></span>

<span data-ttu-id="cb5d4-152">Um modelo de relatório do dashboard pré-configurada está disponível como uma <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">transferível folha de cálculo do Excel</a> toohelp analisar rapidamente os dados de registo.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-152">A preconfigured dashboard report template is available as a <a href="http://go.microsoft.com/fwlink/?LinkId=403540" target="_blank">downloadable Excel spreadsheet</a> toohelp you quickly analyze log data.</span></span> <span data-ttu-id="cb5d4-153">modelo de Olá toouse nos seus registos de auditoria, terá de Excel 2013 ou posterior e o Power Query, que pode transferir <a href="http://www.microsoft.com/download/details.aspx?id=39379">aqui</a>.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-153">toouse hello template on your audit logs, you need Excel 2013 or later and Power Query, which you can download <a href="http://www.microsoft.com/download/details.aspx?id=39379">here</a>.</span></span>

<span data-ttu-id="cb5d4-154">modelo de Olá tem dados de exemplo fictícias no mesmo e, pode configurar Power Query tooimport o registo de auditoria diretamente a partir da sua conta do storage do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-154">hello template has fictional sample data in it, and you can set up Power Query tooimport your audit log directly from your Azure storage account.</span></span>

## <span data-ttu-id="cb5d4-155"><a id="subheading-4"></a>Regeneração da chave de armazenamento</span><span class="sxs-lookup"><span data-stu-id="cb5d4-155"><a id="subheading-4"></a>Storage key regeneration</span></span>
<span data-ttu-id="cb5d4-156">Na produção, é provável toorefresh o armazenamento de chaves periodicamente.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-156">In production, you are likely toorefresh your storage keys periodically.</span></span> <span data-ttu-id="cb5d4-157">Ao atualizar as suas chaves, terá de política de Olá toosave.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-157">When refreshing your keys, you need toosave hello policy.</span></span> <span data-ttu-id="cb5d4-158">processo de Olá é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="cb5d4-158">hello process is as follows:</span></span>

1. <span data-ttu-id="cb5d4-159">No Olá auditoria painel de configuração (descrito acima em auditoria secção de configuração de Olá) comutador Olá **chave de acesso de armazenamento** de *primário* demasiado*secundário* e  **GUARDAR**.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-159">In hello auditing configuration blade (described above in hello setup auditing section) switch hello **Storage Access Key** from *Primary* too*Secondary* and **SAVE**.</span></span>

   ![][4]
2. <span data-ttu-id="cb5d4-160">Painel de configuração de armazenamento toohello aceda e **regenerar** Olá *chave de acesso primária*.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-160">Go toohello storage configuration blade and **regenerate** hello *Primary Access Key*.</span></span>
3. <span data-ttu-id="cb5d4-161">Voltar atrás toohello auditoria painel de configuração, o comutador Olá **chave de acesso de armazenamento** de *secundário* demasiado*primário* e prima **guardar**.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-161">Go back toohello auditing configuration blade, switch hello **Storage Access Key** from *Secondary* too*Primary* and press **SAVE**.</span></span>
4. <span data-ttu-id="cb5d4-162">Voltar atrás toohello armazenamento IU e **regenerar** Olá *chave de acesso secundária* (como preparação para Olá chaves seguintes atualização ciclo.</span><span class="sxs-lookup"><span data-stu-id="cb5d4-162">Go back toohello storage UI and **regenerate** hello *Secondary Access Key* (as preparation for hello next keys refresh cycle.</span></span>

## <span data-ttu-id="cb5d4-163"><a id="subheading-5"></a>Automatização (do PowerShell/REST API)</span><span class="sxs-lookup"><span data-stu-id="cb5d4-163"><a id="subheading-5"></a>Automation (PowerShell/REST API)</span></span>
<span data-ttu-id="cb5d4-164">Também pode configurar a auditoria no Azure SQL Data Warehouse, utilizando Olá seguintes ferramentas de automatização:</span><span class="sxs-lookup"><span data-stu-id="cb5d4-164">You can also configure auditing in Azure SQL Data Warehouse by using hello following automation tools:</span></span>

* <span data-ttu-id="cb5d4-165">**Cmdlets do PowerShell**:</span><span class="sxs-lookup"><span data-stu-id="cb5d4-165">**PowerShell cmdlets**:</span></span>

   * <span data-ttu-id="cb5d4-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-166">[Get-AzureRMSqlDatabaseAuditingPolicy][101]</span></span>
   * <span data-ttu-id="cb5d4-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-167">[Get-AzureRMSqlServerAuditingPolicy][102]</span></span>
   * <span data-ttu-id="cb5d4-168">[Remover AzureRMSqlDatabaseAuditing][103]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-168">[Remove-AzureRMSqlDatabaseAuditing][103]</span></span>
   * <span data-ttu-id="cb5d4-169">[Remover AzureRMSqlServerAuditing][104]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-169">[Remove-AzureRMSqlServerAuditing][104]</span></span>
   * <span data-ttu-id="cb5d4-170">[Conjunto AzureRMSqlDatabaseAuditingPolicy][105]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-170">[Set-AzureRMSqlDatabaseAuditingPolicy][105]</span></span>
   * <span data-ttu-id="cb5d4-171">[Conjunto AzureRMSqlServerAuditingPolicy][106]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-171">[Set-AzureRMSqlServerAuditingPolicy][106]</span></span>
   * <span data-ttu-id="cb5d4-172">[Utilize AzureRMSqlServerAuditingPolicy][107]</span><span class="sxs-lookup"><span data-stu-id="cb5d4-172">[Use-AzureRMSqlServerAuditingPolicy][107]</span></span>

<!--Anchors-->
[Noções básicas de auditoria de base de dados]: #subheading-1
[Configurar a auditoria da base de dados]: #subheading-2
[Analisar registos de auditoria e relatórios]: #subheading-3


<!--Image references-->
[1]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing.png
[2]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-inherit.png
[3]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-enable.png
[4]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-storage-account.png
[5]: ./media/sql-data-warehouse-auditing-overview/sql-data-warehouse-auditing-dashboard.png


<!--Link references-->
[101]: /powershell/module/azurerm.sql/get-azurermsqldatabaseauditingpolicy
[102]: /powershell/module/azurerm.sql/Get-AzureRMSqlServerAuditingPolicy
[103]: /powershell/module/azurerm.sql/Remove-AzureRMSqlDatabaseAuditing
[104]: /powershell/module/azurerm.sql/Remove-AzureRMSqlServerAuditing
[105]: /powershell/module/azurerm.sql/Set-AzureRMSqlDatabaseAuditingPolicy
[106]: /powershell/module/azurerm.sql/Set-AzureRMSqlServerAuditingPolicy
[107]: /powershell/module/azurerm.sql/Use-AzureRMSqlServerAuditingPolicy