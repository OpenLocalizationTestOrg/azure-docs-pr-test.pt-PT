---
title: aaaOptimize ambiente do SQL Server com o Log Analytics do Azure | Microsoft Docs
description: "Análise de registos do Azure, pode utilizar Olá avaliação do SQL Server solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor do SQL Server num intervalo regular."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e297eb57-1718-4cfe-a241-b9e84b2c42ac
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f31326d8cdad3ef5d5a190614d1a18c1dac826ed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-sql-server-environment-with-hello-sql-assessment-solution-in-log-analytics"></a><span data-ttu-id="84aa7-103">Otimizar o seu ambiente do SQL Server com Olá solução de avaliação do SQL Server na análise de registos</span><span class="sxs-lookup"><span data-stu-id="84aa7-103">Optimize your SQL Server environment with hello SQL Assessment solution in Log Analytics</span></span>

![Símbolo de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assessment-symbol.png)

<span data-ttu-id="84aa7-105">Pode utilizar Olá avaliação do SQL Server solução tooassess Olá risco e estado de funcionamento dos seus ambientes de servidor num intervalo regular.</span><span class="sxs-lookup"><span data-stu-id="84aa7-105">You can use hello SQL Assessment solution tooassess hello risk and health of your server environments on a regular interval.</span></span> <span data-ttu-id="84aa7-106">Este artigo irá ajudá-lo a instalar solução Olá, de modo a que possa tomar medidas corretivas para potenciais problemas.</span><span class="sxs-lookup"><span data-stu-id="84aa7-106">This article will help you install hello solution so that you can take corrective actions for potential problems.</span></span>

<span data-ttu-id="84aa7-107">Esta solução fornece uma lista prioritária de infraestrutura de servidor implementado recomendações tooyour específico.</span><span class="sxs-lookup"><span data-stu-id="84aa7-107">This solution provides a prioritized list of recommendations specific tooyour deployed server infrastructure.</span></span> <span data-ttu-id="84aa7-108">recomendações de Olá são categorizadas em seis foco áreas que rapidamente a ajudar a compreender Olá risco e tome as medidas corretivas.</span><span class="sxs-lookup"><span data-stu-id="84aa7-108">hello recommendations are categorized across six focus areas which help you quickly understand hello risk and take corrective action.</span></span>

<span data-ttu-id="84aa7-109">recomendações de Olá efetuadas baseiam-se em conhecimentos Olá e experiência adquiridos por engenheiros de Microsoft de milhares de visitas de cliente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-109">hello recommendations made are based on hello knowledge and experience gained by Microsoft engineers from thousands of customer visits.</span></span> <span data-ttu-id="84aa7-110">Cada recomendação fornece orientações sobre por que razão poderá importa tooyou a um problema e como tooimplement Olá sugerida alterações.</span><span class="sxs-lookup"><span data-stu-id="84aa7-110">Each recommendation provides guidance about why an issue might matter tooyou and how tooimplement hello suggested changes.</span></span>

<span data-ttu-id="84aa7-111">Pode escolher áreas que são mais importante tooyour organização e controlam o progresso em direção a executar um ambiente de livre e bom estado de funcionamento de risco.</span><span class="sxs-lookup"><span data-stu-id="84aa7-111">You can choose focus areas that are most important tooyour organization and track your progress toward running a risk free and healthy environment.</span></span>

<span data-ttu-id="84aa7-112">Depois de acrescentar solução Olá e uma avaliação estiver concluída, resumo informações de áreas de foco são apresentadas na Olá **avaliação do SQL Server** dashboard para a infraestrutura de Olá no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-112">After you've added hello solution and an assessment is completed, summary information for focus areas is shown on hello **SQL Assessment** dashboard for hello infrastructure in your environment.</span></span> <span data-ttu-id="84aa7-113">Olá secções seguintes descrevem como toouse Olá informações sobre Olá **avaliação do SQL Server** dashboard, onde pode ver e, em seguida, tome as ações para a sua infraestrutura de servidor SQL recomendadas.</span><span class="sxs-lookup"><span data-stu-id="84aa7-113">hello following sections describe how toouse hello information on hello **SQL Assessment** dashboard, where you can view and then take recommended actions for your SQL server infrastructure.</span></span>

![imagem do mosaico de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-tile.png)

![imagem do dashboard de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-dash.png)

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="84aa7-116">Instalar e configurar a solução de Olá</span><span class="sxs-lookup"><span data-stu-id="84aa7-116">Installing and configuring hello solution</span></span>
<span data-ttu-id="84aa7-117">Avaliação do SQL Server funciona com todas as versões atualmente suportadas do SQL Server para as edições Standard, Developer e Enterprise do Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-117">SQL Assessment works with all currently supported versions of SQL Server for hello Standard, Developer, and Enterprise editions.</span></span>

<span data-ttu-id="84aa7-118">Utilize Olá tooinstall informações a seguir e configurar a solução de Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-118">Use hello following information tooinstall and configure hello solution.</span></span>

* <span data-ttu-id="84aa7-119">Os agentes devem ser instalados em servidores que tenham o SQL Server instalada.</span><span class="sxs-lookup"><span data-stu-id="84aa7-119">Agents must be installed on servers that have SQL Server installed.</span></span>
* <span data-ttu-id="84aa7-120">Olá solução de avaliação do SQL Server necessita de uma versão suportada do .NET Framework 4 está instalado em cada computador que tenha um agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="84aa7-120">hello SQL Assessment solution requires a supported version of .NET Framework 4 installed on each computer that has an OMS agent.</span></span>
* <span data-ttu-id="84aa7-121">Solução do ordem tooinstall Olá, Olá utilizador tem de ser um administrador ou de contribuinte toohello subscrição do Azure quando utilizar Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="84aa7-121">In order tooinstall hello solution, hello user must be an administrator or contributor toohello Azure subscription when using hello Azure portal.</span></span> <span data-ttu-id="84aa7-122">Além disso, Olá utilizador tem de ser um membro de Olá OMS área de trabalho contribuinte da função ou de administrador no portal do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-122">In addition, hello user must be a member of hello OMS workspace contributor or administrator role in hello OMS portal.</span></span>
* <span data-ttu-id="84aa7-123">Ao utilizar o agente do Operations Manager Olá com avaliação do SQL Server, terá de toouse uma conta de Run-As do Operations Manager.</span><span class="sxs-lookup"><span data-stu-id="84aa7-123">When using hello Operations Manager agent with SQL Assessment, you'll need toouse an Operations Manager Run-As account.</span></span> <span data-ttu-id="84aa7-124">Consulte [do Operations Manager Run as contas do OMS](#operations-manager-run-as-accounts-for-oms) abaixo para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="84aa7-124">See [Operations Manager run-as accounts for OMS](#operations-manager-run-as-accounts-for-oms) below for more information.</span></span>

  > [!NOTE]
  > <span data-ttu-id="84aa7-125">agente MMA Olá não suporta contas do Operations Manager Run-As.</span><span class="sxs-lookup"><span data-stu-id="84aa7-125">hello MMA agent does not support Operations Manager Run-As accounts.</span></span>
  >
  >
* <span data-ttu-id="84aa7-126">Adicionar tooyour de solução de avaliação do SQL Server Olá área de trabalho do OMS através de Olá processo descrita no [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="84aa7-126">Add hello SQL Assessment solution tooyour OMS workspace using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="84aa7-127">Não há nenhuma configuração adicional.</span><span class="sxs-lookup"><span data-stu-id="84aa7-127">There is no further configuration required.</span></span>

> [!NOTE]
> <span data-ttu-id="84aa7-128">Depois de acrescentar solução Olá, o ficheiro de AdvisorAssessment.exe Olá é adicionado tooservers com agentes.</span><span class="sxs-lookup"><span data-stu-id="84aa7-128">After you've added hello solution, hello AdvisorAssessment.exe file is added tooservers with agents.</span></span> <span data-ttu-id="84aa7-129">Dados de configuração é lido e, em seguida, enviados o serviço OMS toohello na nuvem de Olá para processamento.</span><span class="sxs-lookup"><span data-stu-id="84aa7-129">Configuration data is read and then sent toohello OMS service in hello cloud for processing.</span></span> <span data-ttu-id="84aa7-130">Lógica é aplicado toohello recebida dados e o serviço em nuvem Olá regista dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-130">Logic is applied toohello received data and hello cloud service records hello data.</span></span>

## <a name="sql-assessment-data-collection-details"></a><span data-ttu-id="84aa7-131">Detalhes de recolha de dados de avaliação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="84aa7-131">SQL Assessment data collection details</span></span>
<span data-ttu-id="84aa7-132">Avaliação do SQL Server recolhe dados WMI, dados de registo, dados de desempenho e SQL Server gestão dinâmica ver os resultados utilizando os agentes de Olá que tiver ativado.</span><span class="sxs-lookup"><span data-stu-id="84aa7-132">SQL Assessment collects WMI data, registry data, performance data, and SQL Server dynamic management view results using hello agents that you have enabled.</span></span>

<span data-ttu-id="84aa7-133">Olá tabela seguinte mostra os métodos de recolha de dados para os agentes, se o Operations Manager (SCOM) é necessário e como muitas vezes, os dados são recolhidos por um agente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-133">hello following table shows data collection methods for agents, whether Operations Manager (SCOM) is required, and how often data is collected by an agent.</span></span>

| <span data-ttu-id="84aa7-134">Plataforma</span><span class="sxs-lookup"><span data-stu-id="84aa7-134">platform</span></span> | <span data-ttu-id="84aa7-135">Direcionar o agente</span><span class="sxs-lookup"><span data-stu-id="84aa7-135">Direct Agent</span></span> | <span data-ttu-id="84aa7-136">Agente do SCOM</span><span class="sxs-lookup"><span data-stu-id="84aa7-136">SCOM agent</span></span> | <span data-ttu-id="84aa7-137">Storage do Azure</span><span class="sxs-lookup"><span data-stu-id="84aa7-137">Azure Storage</span></span> | <span data-ttu-id="84aa7-138">SCOM necessário?</span><span class="sxs-lookup"><span data-stu-id="84aa7-138">SCOM required?</span></span> | <span data-ttu-id="84aa7-139">Dados de agente do SCOM enviados através do grupo de gestão</span><span class="sxs-lookup"><span data-stu-id="84aa7-139">SCOM agent data sent via management group</span></span> | <span data-ttu-id="84aa7-140">Frequência de recolha</span><span class="sxs-lookup"><span data-stu-id="84aa7-140">collection frequency</span></span> |
| --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="84aa7-141">Windows</span><span class="sxs-lookup"><span data-stu-id="84aa7-141">Windows</span></span> | <span data-ttu-id="84aa7-142">&#8226;</span><span class="sxs-lookup"><span data-stu-id="84aa7-142">&#8226;</span></span> | <span data-ttu-id="84aa7-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="84aa7-143">&#8226;</span></span> |  |  | <span data-ttu-id="84aa7-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="84aa7-144">&#8226;</span></span> |<span data-ttu-id="84aa7-145">7 dias</span><span class="sxs-lookup"><span data-stu-id="84aa7-145">7 days</span></span> |

## <a name="operations-manager-run-as-accounts-for-oms"></a><span data-ttu-id="84aa7-146">Executar como contas do Operations Manager para OMS</span><span class="sxs-lookup"><span data-stu-id="84aa7-146">Operations Manager run-as accounts for OMS</span></span>
<span data-ttu-id="84aa7-147">Análise de registos na OMS utiliza Olá agente do Operations Manager e toocollect do grupo de gestão e enviar serviço de dados do toohello OMS.</span><span class="sxs-lookup"><span data-stu-id="84aa7-147">Log Analytics in OMS uses hello Operations Manager agent and management group toocollect and send data toohello OMS service.</span></span> <span data-ttu-id="84aa7-148">Compilações OMS após os pacotes de gestão para cargas de trabalho tooprovide de valor acrescentado serviços.</span><span class="sxs-lookup"><span data-stu-id="84aa7-148">OMS builds upon management packs for workloads tooprovide value-add services.</span></span> <span data-ttu-id="84aa7-149">Cada carga de trabalho necessita de pacotes de gestão de toorun de privilégios específico da carga de trabalho num contexto de segurança diferentes, tais como uma conta de domínio.</span><span class="sxs-lookup"><span data-stu-id="84aa7-149">Each workload requires workload-specific privileges toorun management packs in a different security context, such as a domain account.</span></span> <span data-ttu-id="84aa7-150">Terá de informações de credencial tooprovide ao configurar uma conta do Operations Manager Run As.</span><span class="sxs-lookup"><span data-stu-id="84aa7-150">You need tooprovide credential information by configuring an Operations Manager Run As account.</span></span>

<span data-ttu-id="84aa7-151">Utilize Olá seguir informações tooset Olá do Operations Manager conta Run as para avaliação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84aa7-151">Use hello following information tooset hello Operations Manager run-as account for SQL Assessment.</span></span>

### <a name="set-hello-run-as-account-for-sql-assessment"></a><span data-ttu-id="84aa7-152">Definir Olá conta Run As para avaliação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="84aa7-152">Set hello Run As account for SQL assessment</span></span>
 <span data-ttu-id="84aa7-153">Se já estiver a utilizar Olá pacote de gestão do SQL Server, deve utilizar essa conta Run As.</span><span class="sxs-lookup"><span data-stu-id="84aa7-153">If you are already using hello SQL Server management pack, you should use that Run As account.</span></span>

#### <a name="tooconfigure-hello-sql-run-as-account-in-hello-operations-console"></a><span data-ttu-id="84aa7-154">Olá tooconfigure SQL conta Run as na consola de operações de Olá</span><span class="sxs-lookup"><span data-stu-id="84aa7-154">tooconfigure hello SQL Run As account in hello Operations console</span></span>
> [!NOTE]
> <span data-ttu-id="84aa7-155">Se estiver a utilizar hello OMS direcionar o agente, em vez do agente do SCOM Olá, o pacote de gestão de Olá sempre é executado no contexto de segurança de Olá de Olá conta do sistema Local.</span><span class="sxs-lookup"><span data-stu-id="84aa7-155">If you are using hello OMS direct agent, rather than hello SCOM agent, hello management pack always runs in hello security context of hello Local System account.</span></span> <span data-ttu-id="84aa7-156">Ignorar os passos 1 a 5 abaixo e execute Olá: exemplo de T-SQL ou o Powershell, especificando NT AUTHORITY\SYSTEM como nome de utilizador Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-156">Skip steps 1-5 below, and run either hello T-SQL or Powershell sample, specifying NT AUTHORITY\SYSTEM as hello user name.</span></span>
>
>

1. <span data-ttu-id="84aa7-157">No Operations Manager, abra a consola de operações de Olá e, em seguida, clique em **administração**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-157">In Operations Manager, open hello Operations console, and then click **Administration**.</span></span>
2. <span data-ttu-id="84aa7-158">Em **configuração de Run As**, clique em **perfis**e abra **OMS SQL avaliação perfil Run As**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-158">Under **Run As Configuration**, click **Profiles**, and open **OMS SQL Assessment Run As Profile**.</span></span>
3. <span data-ttu-id="84aa7-159">No Olá **contas Run as** página, clique em **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-159">On hello **Run As Accounts** page, click **Add**.</span></span>
4. <span data-ttu-id="84aa7-160">Selecione uma conta Run As do Windows que contém as credenciais de Olá necessárias para o SQL Server, ou clique em **novo** toocreate um.</span><span class="sxs-lookup"><span data-stu-id="84aa7-160">Select a Windows Run As account that contains hello credentials needed for SQL Server, or click **New** toocreate one.</span></span>

   > [!NOTE]
   > <span data-ttu-id="84aa7-161">Olá tipo conta Run As tem de ser Windows.</span><span class="sxs-lookup"><span data-stu-id="84aa7-161">hello Run As account type must be Windows.</span></span> <span data-ttu-id="84aa7-162">Olá conta Run As tem de ser também parte do grupo de administradores Local em todos os servidores do Windows que aloja instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84aa7-162">hello Run As account must also be part of Local Administrators group on all Windows Servers hosting SQL Server Instances.</span></span>
   >
   >
5. <span data-ttu-id="84aa7-163">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-163">Click **Save**.</span></span>
6. <span data-ttu-id="84aa7-164">Modificar e, em seguida, executar Olá seguinte exemplo de T-SQL em cada instância do SQL Server toogrant permissões mínimas necessária tooRun como conta tooperform avaliação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84aa7-164">Modify and then execute hello following T-SQL sample on each SQL Server Instance toogrant minimum permissions required tooRun As Account tooperform SQL Assessment.</span></span> <span data-ttu-id="84aa7-165">No entanto, não precisa de toodo isto se uma conta Run As já faz parte da função de servidor sysadmin Olá nas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="84aa7-165">However, you don’t need toodo this if a Run As Account is already part of hello sysadmin server role on SQL Server Instances.</span></span>

```
---
    -- Replace <UserName> with hello actual user name being used as Run As Account.
    USE master

    -- Create login for hello user, comment this line if login is already created.
    CREATE LOGIN [<UserName>] FROM WINDOWS

    -- Grant permissions toouser.
    GRANT VIEW SERVER STATE too[<UserName>]
    GRANT VIEW ANY DEFINITION too[<UserName>]
    GRANT VIEW ANY DATABASE too[<UserName>]

    -- Add database user for all hello databases on SQL Server Instance, this is required for connecting tooindividual databases.
    -- NOTE: This command must be run anytime new databases are added tooSQL Server instances.
    EXEC sp_msforeachdb N'USE [?]; CREATE USER [<UserName>] FOR LOGIN [<UserName>];'

```
#### <a name="tooconfigure-hello-sql-run-as-account-using-windows-powershell"></a><span data-ttu-id="84aa7-166">Olá tooconfigure SQL conta Run as com o Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="84aa7-166">tooconfigure hello SQL Run As account using Windows PowerShell</span></span>
<span data-ttu-id="84aa7-167">Abra uma janela do PowerShell e execute o seguinte script depois atualizou-lo com as suas informações de Olá:</span><span class="sxs-lookup"><span data-stu-id="84aa7-167">Open a PowerShell window and run hello following script after you’ve updated it with your information:</span></span>

```

    import-module OperationsManager
    New-SCOMManagementGroupConnection "<your management group name>"

    $profile = Get-SCOMRunAsProfile -DisplayName "OMS SQL Assessment Run As Profile"
    $account = Get-SCOMrunAsAccount | Where-Object {$_.Name -eq "<your run as account name>"}
    Set-SCOMRunAsProfile -Action "Add" -Profile $Profile -Account $Account
```

## <a name="understanding-how-recommendations-are-prioritized"></a><span data-ttu-id="84aa7-168">Compreender a forma como as recomendações são prioritários</span><span class="sxs-lookup"><span data-stu-id="84aa7-168">Understanding how recommendations are prioritized</span></span>
<span data-ttu-id="84aa7-169">Cada recomendação efetuada é atribuída um valor de peso que identifica a importância relativa de Olá da recomendação Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-169">Every recommendation made is given a weighting value that identifies hello relative importance of hello recommendation.</span></span> <span data-ttu-id="84aa7-170">São apresentadas apenas Olá dez mais importantes recomendações.</span><span class="sxs-lookup"><span data-stu-id="84aa7-170">Only hello ten most important recommendations are shown.</span></span>

### <a name="how-weights-are-calculated"></a><span data-ttu-id="84aa7-171">Como são calculadas ponderações</span><span class="sxs-lookup"><span data-stu-id="84aa7-171">How weights are calculated</span></span>
<span data-ttu-id="84aa7-172">As ponderações são valores de agregação com base nas três principais fatores:</span><span class="sxs-lookup"><span data-stu-id="84aa7-172">Weightings are aggregate values based on three key factors:</span></span>

* <span data-ttu-id="84aa7-173">Olá *probabilidade* que um problema identificado causará problemas.</span><span class="sxs-lookup"><span data-stu-id="84aa7-173">hello *probability* that an issue identified will cause problems.</span></span> <span data-ttu-id="84aa7-174">Uma probabilidade superior equivale tooa maior pontuação geral para recomendação Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-174">A higher probability equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="84aa7-175">Olá *impacto* problema Olá na sua organização se provocar um problema.</span><span class="sxs-lookup"><span data-stu-id="84aa7-175">hello *impact* of hello issue on your organization if it does cause a problem.</span></span> <span data-ttu-id="84aa7-176">Um impacto superior equivale tooa maior pontuação geral para recomendação Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-176">A higher impact equates tooa larger overall score for hello recommendation.</span></span>
* <span data-ttu-id="84aa7-177">Olá *esforço* necessário recomendação de Olá tooimplement.</span><span class="sxs-lookup"><span data-stu-id="84aa7-177">hello *effort* required tooimplement hello recommendation.</span></span> <span data-ttu-id="84aa7-178">Um maior esforço equivale tooa pontuação geral mais pequenas de recomendação Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-178">A higher effort equates tooa smaller overall score for hello recommendation.</span></span>

<span data-ttu-id="84aa7-179">Olá weighting para cada recomendação é expresso como uma percentagem da classificação total Olá disponíveis para cada área de foco.</span><span class="sxs-lookup"><span data-stu-id="84aa7-179">hello weighting for each recommendation is expressed as a percentage of hello total score available for each focus area.</span></span> <span data-ttu-id="84aa7-180">Por exemplo, se uma recomendação na área de foco de conformidade e segurança de Olá tem uma pontuação de 5%, implementar dessa recomendação irá aumentar a sua geral de segurança e conformidade pontuação por 5%.</span><span class="sxs-lookup"><span data-stu-id="84aa7-180">For example, if a recommendation in hello Security and Compliance focus area has a score of 5%, implementing that recommendation will increase your overall Security and Compliance score by 5%.</span></span>

### <a name="focus-areas"></a><span data-ttu-id="84aa7-181">Áreas de foco</span><span class="sxs-lookup"><span data-stu-id="84aa7-181">Focus areas</span></span>
<span data-ttu-id="84aa7-182">**Segurança e conformidade** -esta área de foco mostra recomendações para potenciais ameaças de segurança e falhas, políticas empresariais e requisitos de conformidade técnicos, jurídicos e regulamentares.</span><span class="sxs-lookup"><span data-stu-id="84aa7-182">**Security and Compliance** - This focus area shows recommendations for potential security threats and breaches, corporate policies, and technical, legal and regulatory compliance requirements.</span></span>

<span data-ttu-id="84aa7-183">**Disponibilidade e continuidade do negócio** -esta área de foco mostra recomendações para a disponibilidade do serviço, a resiliência da sua infraestrutura e a proteção do negócio.</span><span class="sxs-lookup"><span data-stu-id="84aa7-183">**Availability and Business Continuity** - This focus area shows recommendations for service availability, resiliency of your infrastructure, and business protection.</span></span>

<span data-ttu-id="84aa7-184">**Desempenho e escalabilidade** -esta área de foco mostra toohelp recomendações da sua organização infraestrutura de TI aumentar, certifique-se de que o ambiente de TI cumpre os requisitos de desempenho atuais e é capaz de toorespond toochanging Tem a infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="84aa7-184">**Performance and Scalability** - This focus area shows recommendations toohelp your organization's IT infrastructure grow, ensure that your IT environment meets current performance requirements, and is able toorespond toochanging infrastructure needs.</span></span>

<span data-ttu-id="84aa7-185">**Atualizar, implementação e migração** - esta área de foco mostra toohelp recomendações atualizar, migrar e implementar a infraestrutura existente do SQL Server tooyour.</span><span class="sxs-lookup"><span data-stu-id="84aa7-185">**Upgrade, Migration and Deployment** - This focus area shows recommendations toohelp you upgrade, migrate, and deploy SQL Server tooyour existing infrastructure.</span></span>

<span data-ttu-id="84aa7-186">**Operações e monitorização** - esta área de foco mostra recomendações toohelp otimizar as operações de TI implementar manutenção preventiva e maximizar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="84aa7-186">**Operations and Monitoring** - This focus area shows recommendations toohelp streamline your IT operations, implement preventative maintenance, and maximize performance.</span></span>

<span data-ttu-id="84aa7-187">**Gestão de configuração e alteração** -esta área de foco mostra recomendações toohelp Proteja as operações diárias, certifique-se de que as alterações não negativamente afetam a sua infraestrutura, estabeleça procedimentos de controlo de alterações e tootrack e de auditoria configurações do sistema.</span><span class="sxs-lookup"><span data-stu-id="84aa7-187">**Change and Configuration Management** - This focus area shows recommendations toohelp protect day-to-day operations, ensure that changes don't negatively affect your infrastructure, establish change control procedures, and tootrack and audit system configurations.</span></span>

### <a name="should-you-aim-tooscore-100-in-every-focus-area"></a><span data-ttu-id="84aa7-188">Deve, procure tooscore 100% cada área de foco?</span><span class="sxs-lookup"><span data-stu-id="84aa7-188">Should you aim tooscore 100% in every focus area?</span></span>
<span data-ttu-id="84aa7-189">Não necessariamente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-189">Not necessarily.</span></span> <span data-ttu-id="84aa7-190">recomendações de Olá baseiam-se em conhecimentos Olá e experiências adquiridas por engenheiros Microsoft entre milhares de visitas de cliente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-190">hello recommendations are based on hello knowledge and experiences gained by Microsoft engineers across thousands of customer visits.</span></span> <span data-ttu-id="84aa7-191">No entanto, nenhum infraestruturas de duas servidor são Olá mesmo e ver as recomendações específicas podem ser maior ou menor relevante tooyou.</span><span class="sxs-lookup"><span data-stu-id="84aa7-191">However, no two server infrastructures are hello same, and specific recommendations may be more or less relevant tooyou.</span></span> <span data-ttu-id="84aa7-192">Por exemplo, algumas recomendações de segurança poderão ser menos relevantes se as máquinas virtuais não são toohello exposto à Internet.</span><span class="sxs-lookup"><span data-stu-id="84aa7-192">For example, some security recommendations might be less relevant if your virtual machines are not exposed toohello Internet.</span></span> <span data-ttu-id="84aa7-193">Algumas recomendações de disponibilidade podem ser menos relevantes para os serviços que fornecem a recolha de dados ad hoc de baixa prioridade e relatórios.</span><span class="sxs-lookup"><span data-stu-id="84aa7-193">Some availability recommendations may be less relevant for services that provide low priority ad hoc data collection and reporting.</span></span> <span data-ttu-id="84aa7-194">Problemas que sejam negócio madura tooa importante poderão ser menos importante tooa arranque.</span><span class="sxs-lookup"><span data-stu-id="84aa7-194">Issues that are important tooa mature business may be less important tooa start-up.</span></span> <span data-ttu-id="84aa7-195">Poderá pretender tooidentify áreas que são as prioridades e, em seguida, observar como as pontuações alteram ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="84aa7-195">You may want tooidentify which focus areas are your priorities and then look at how your scores change over time.</span></span>

<span data-ttu-id="84aa7-196">Cada recomendação inclui orientações sobre por que motivo é importante.</span><span class="sxs-lookup"><span data-stu-id="84aa7-196">Every recommendation includes guidance about why it is important.</span></span> <span data-ttu-id="84aa7-197">Deve utilizar esta orientação tooevaluate se implementar a recomendação de Olá é adequada para si, dada natureza Olá sua TI Olá e serviços empresariais precisam da sua organização.</span><span class="sxs-lookup"><span data-stu-id="84aa7-197">You should use this guidance tooevaluate whether implementing hello recommendation is appropriate for you, given hello nature of your IT services and hello business needs of your organization.</span></span>

## <a name="use-assessment-focus-area-recommendations"></a><span data-ttu-id="84aa7-198">Utilize as recomendações de área de foco de avaliação</span><span class="sxs-lookup"><span data-stu-id="84aa7-198">Use assessment focus area recommendations</span></span>
<span data-ttu-id="84aa7-199">Antes de poder utilizar uma solução de avaliação na OMS, tem de ter solução Olá instalada.</span><span class="sxs-lookup"><span data-stu-id="84aa7-199">Before you can use an assessment solution in OMS, you must have hello solution installed.</span></span> <span data-ttu-id="84aa7-200">tooread mais sobre a instalação de soluções, consulte [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="84aa7-200">tooread more about installing solutions, see [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span> <span data-ttu-id="84aa7-201">Depois de ser instalado, pode ver o resumo de Olá das recomendações utilizando o mosaico de avaliação do SQL Server Olá na página de descrição geral de Olá no OMS.</span><span class="sxs-lookup"><span data-stu-id="84aa7-201">After it is installed, you can view hello summary of recommendations by using hello SQL Assessment tile on hello Overview page in OMS.</span></span>

<span data-ttu-id="84aa7-202">Olá vista resumida avaliações de conformidade para a sua infraestrutura e, em seguida, desagregação em recomendações.</span><span class="sxs-lookup"><span data-stu-id="84aa7-202">View hello summarized compliance assessments for your infrastructure and then drill-into recommendations.</span></span>

### <a name="tooview-recommendations-for-a-focus-area-and-take-corrective-action"></a><span data-ttu-id="84aa7-203">recomendações de tooview para um foco área e Adote as medidas corretivas</span><span class="sxs-lookup"><span data-stu-id="84aa7-203">tooview recommendations for a focus area and take corrective action</span></span>
1. <span data-ttu-id="84aa7-204">No Olá **descrição geral** página, clique em Olá **avaliação do SQL Server** mosaico.</span><span class="sxs-lookup"><span data-stu-id="84aa7-204">On hello **Overview** page, click hello **SQL Assessment** tile.</span></span>
2. <span data-ttu-id="84aa7-205">No Olá **avaliação do SQL Server** página, reveja as informações de resumo de Olá dos painéis de área de foco Olá e, em seguida, clique numa tooview recomendações para essa área de foco.</span><span class="sxs-lookup"><span data-stu-id="84aa7-205">On hello **SQL Assessment** page, review hello summary information in one of hello focus area blades and then click one tooview recommendations for that focus area.</span></span>
3. <span data-ttu-id="84aa7-206">Em qualquer uma das páginas de área de foco Olá, pode ver as recomendações de Olá definida efetuadas para o seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-206">On any of hello focus area pages, you can view hello prioritized recommendations made for your environment.</span></span> <span data-ttu-id="84aa7-207">Clique numa recomendação em **Objetos afetados** tooview detalhes sobre a razão pela qual Olá recomendação é feita.</span><span class="sxs-lookup"><span data-stu-id="84aa7-207">Click a recommendation under **Affected Objects** tooview details about why hello recommendation is made.</span></span>  
    <span data-ttu-id="84aa7-208">![Imagem das recomendações de avaliação do SQL Server](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span><span class="sxs-lookup"><span data-stu-id="84aa7-208">![image of SQL Assessment recommendations](./media/log-analytics-sql-assessment/sql-assess-focus.png)</span></span>
4. <span data-ttu-id="84aa7-209">Pode executar ações corretivas sugeridas na **as ações sugeridas**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-209">You can take corrective actions suggested in **Suggested Actions**.</span></span> <span data-ttu-id="84aa7-210">Quando tem sido resolvida item Olá, irão registar avaliações posteriores ações foram executadas e o modelo de pontuação de conformidade aumentam recomendadas.</span><span class="sxs-lookup"><span data-stu-id="84aa7-210">When hello item has been addressed, later assessments will record that recommended actions were taken and your compliance score will increase.</span></span> <span data-ttu-id="84aa7-211">Itens corrigidas aparecem como **transmitido objetos**.</span><span class="sxs-lookup"><span data-stu-id="84aa7-211">Corrected items appear as **Passed Objects**.</span></span>

## <a name="ignore-recommendations"></a><span data-ttu-id="84aa7-212">Ignorar as recomendações</span><span class="sxs-lookup"><span data-stu-id="84aa7-212">Ignore recommendations</span></span>
<span data-ttu-id="84aa7-213">Se tiver recomendações que pretende que o tooignore, pode criar um ficheiro de texto que OMS utilizará tooprevent recomendações a apresentação nos resultados da avaliação.</span><span class="sxs-lookup"><span data-stu-id="84aa7-213">If you have recommendations that you want tooignore, you can create a text file that OMS will use tooprevent recommendations from appearing in your assessment results.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

### <a name="tooidentify-recommendations-that-you-will-ignore"></a><span data-ttu-id="84aa7-214">recomendações de tooidentify que irão ignorar</span><span class="sxs-lookup"><span data-stu-id="84aa7-214">tooidentify recommendations that you will ignore</span></span>
1. <span data-ttu-id="84aa7-215">Iniciar sessão na área de trabalho tooyour e abrir o registo de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="84aa7-215">Sign in tooyour workspace and open Log Search.</span></span> <span data-ttu-id="84aa7-216">Utilize Olá seguir as recomendações de toolist de consulta que falharam por computadores no seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="84aa7-216">Use hello following query toolist recommendations that have failed for computers in your environment.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Failed | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```

   <span data-ttu-id="84aa7-217">Segue-se uma consulta de pesquisa de registo que de captura de ecrã mostra Olá: ![falha recomendações](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span><span class="sxs-lookup"><span data-stu-id="84aa7-217">Here's a screen shot showing hello Log Search query: ![failed recommendations](./media/log-analytics-sql-assessment/sql-assess-failed-recommendations.png)</span></span>
2. <span data-ttu-id="84aa7-218">Escolha as recomendações que pretende que o tooignore.</span><span class="sxs-lookup"><span data-stu-id="84aa7-218">Choose recommendations that you want tooignore.</span></span> <span data-ttu-id="84aa7-219">Irá utilizar valores de Olá para RecommendationId no procedimento seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-219">You’ll use hello values for RecommendationId in hello next procedure.</span></span>

### <a name="toocreate-and-use-an-ignorerecommendationstxt-text-file"></a><span data-ttu-id="84aa7-220">toocreate e utilizar um ficheiro de texto IgnoreRecommendations.txt</span><span class="sxs-lookup"><span data-stu-id="84aa7-220">toocreate and use an IgnoreRecommendations.txt text file</span></span>
1. <span data-ttu-id="84aa7-221">Crie um ficheiro denominado IgnoreRecommendations.txt.</span><span class="sxs-lookup"><span data-stu-id="84aa7-221">Create a file named IgnoreRecommendations.txt.</span></span>
2. <span data-ttu-id="84aa7-222">Colar ou escreva cada RecommendationId para cada recomendação pretende OMS tooignore numa linha separada e, em seguida, guarde e feche o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-222">Paste or type each RecommendationId for each recommendation that you want OMS tooignore on a separate line and then save and close hello file.</span></span>
3. <span data-ttu-id="84aa7-223">Coloque o ficheiro Olá no Olá seguir pasta em cada computador onde pretende que as recomendações de tooignore OMS.</span><span class="sxs-lookup"><span data-stu-id="84aa7-223">Put hello file in hello following folder on each computer where you want OMS tooignore recommendations.</span></span>
   * <span data-ttu-id="84aa7-224">Em computadores com Olá Microsoft Monitoring Agent (ligado diretamente ou através do Operations Manager) - *SystemDrive*: \Programas\Microsoft Agent\Agent de monitorização</span><span class="sxs-lookup"><span data-stu-id="84aa7-224">On computers with hello Microsoft Monitoring Agent (connected directly or through Operations Manager) - *SystemDrive*:\Program Files\Microsoft Monitoring Agent\Agent</span></span>
   * <span data-ttu-id="84aa7-225">No servidor de gestão do Operations Manager Olá - *SystemDrive*: \Programas\Microsoft System Center 2012 R2\Operations \ Operations Manager\Server</span><span class="sxs-lookup"><span data-stu-id="84aa7-225">On hello Operations Manager management server - *SystemDrive*:\Program Files\Microsoft System Center 2012 R2\Operations Manager\Server</span></span>

### <a name="tooverify-that-recommendations-are-ignored"></a><span data-ttu-id="84aa7-226">tooverify que recomendações são ignoradas</span><span class="sxs-lookup"><span data-stu-id="84aa7-226">tooverify that recommendations are ignored</span></span>
1. <span data-ttu-id="84aa7-227">Após a execução de Olá avaliação agendada seguinte, por predefinição, 7 dias, Olá especificados recomendações são marcadas ignoradas e não serão apresentados no dashboard de avaliação de Olá.</span><span class="sxs-lookup"><span data-stu-id="84aa7-227">After hello next scheduled assessment runs, by default every 7 days, hello specified recommendations are marked Ignored and will not appear on hello assessment dashboard.</span></span>
2. <span data-ttu-id="84aa7-228">Pode utilizar Olá seguir toolist de consultas de pesquisa de registo todas as recomendações de Olá ignorada.</span><span class="sxs-lookup"><span data-stu-id="84aa7-228">You can use hello following Log Search queries toolist all hello ignored recommendations.</span></span>

   ```
   Type=SQLAssessmentRecommendation RecommendationResult=Ignored | select  Computer, RecommendationId, Recommendation | sort  Computer
   ```
3. <span data-ttu-id="84aa7-229">Se, posteriormente, decida que pretende que as recomendações de toosee ignorado, remova quaisquer ficheiros IgnoreRecommendations.txt ou pode remover RecommendationIDs dos mesmos.</span><span class="sxs-lookup"><span data-stu-id="84aa7-229">If you decide later that you want toosee ignored recommendations, remove any IgnoreRecommendations.txt files, or you can remove RecommendationIDs from them.</span></span>

## <a name="sql-assessment-solution-faq"></a><span data-ttu-id="84aa7-230">Solução de avaliação do SQL Server FAQ</span><span class="sxs-lookup"><span data-stu-id="84aa7-230">SQL Assessment solution FAQ</span></span>
<span data-ttu-id="84aa7-231">*Frequência executa uma avaliação?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-231">*How often does an assessment run?*</span></span>

* <span data-ttu-id="84aa7-232">avaliação de Olá é executado a cada 7 dias.</span><span class="sxs-lookup"><span data-stu-id="84aa7-232">hello assessment runs every 7 days.</span></span>

<span data-ttu-id="84aa7-233">*Existe um tooconfigure de forma com que frequência avaliação Olá executa?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-233">*Is there a way tooconfigure how often hello assessment runs?*</span></span>

* <span data-ttu-id="84aa7-234">Neste momento, não.</span><span class="sxs-lookup"><span data-stu-id="84aa7-234">Not at this time.</span></span>

<span data-ttu-id="84aa7-235">*Se for detetado o outro servidor após posso adicionou Olá solução de avaliação do SQL Server, será-avaliada?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-235">*If another server is discovered after I’ve added hello SQL assessment solution, will it be assessed?*</span></span>

* <span data-ttu-id="84aa7-236">Sim, quando é detetado, é avaliado em matéria de, em seguida, no, 7 dias.</span><span class="sxs-lookup"><span data-stu-id="84aa7-236">Yes, once it is discovered it is assessed from then on, every 7 days.</span></span>

<span data-ttu-id="84aa7-237">*Se um servidor é encerrado, quando irá este ser removido do assessment Olá?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-237">*If a server is decommissioned, when will it be removed from hello assessment?*</span></span>

* <span data-ttu-id="84aa7-238">Se um servidor não submeter dados durante 3 semanas, este é removido.</span><span class="sxs-lookup"><span data-stu-id="84aa7-238">If a server does not submit data for 3 weeks, it is removed.</span></span>

<span data-ttu-id="84aa7-239">*O que é o nome de Olá do processo de Olá Olá a recolha de dados?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-239">*What is hello name of hello process that does hello data collection?*</span></span>

* <span data-ttu-id="84aa7-240">AdvisorAssessment.exe</span><span class="sxs-lookup"><span data-stu-id="84aa7-240">AdvisorAssessment.exe</span></span>

<span data-ttu-id="84aa7-241">*Quanto tempo demora para toobe dados recolhido?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-241">*How long does it take for data toobe collected?*</span></span>

* <span data-ttu-id="84aa7-242">recolha de dados real de Olá no servidor de Olá demora cerca de 1 hora.</span><span class="sxs-lookup"><span data-stu-id="84aa7-242">hello actual data collection on hello server takes about 1 hour.</span></span> <span data-ttu-id="84aa7-243">Pode demorar mais em servidores que tenham um grande número de instâncias do SQL Server ou bases de dados.</span><span class="sxs-lookup"><span data-stu-id="84aa7-243">It may take longer on servers that have a large number of SQL instances or databases.</span></span>

<span data-ttu-id="84aa7-244">*Que tipo de dados é recolhido?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-244">*What type of data is collected?*</span></span>

* <span data-ttu-id="84aa7-245">Olá, os seguintes tipos de dados é recolhido:</span><span class="sxs-lookup"><span data-stu-id="84aa7-245">hello following types of data are collected:</span></span>
  * <span data-ttu-id="84aa7-246">WMI</span><span class="sxs-lookup"><span data-stu-id="84aa7-246">WMI</span></span>
  * <span data-ttu-id="84aa7-247">Registo</span><span class="sxs-lookup"><span data-stu-id="84aa7-247">Registry</span></span>
  * <span data-ttu-id="84aa7-248">Contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="84aa7-248">Performance counters</span></span>
  * <span data-ttu-id="84aa7-249">Vistas de gestão dinâmica do SQL Server (DMV).</span><span class="sxs-lookup"><span data-stu-id="84aa7-249">SQL dynamic management views (DMV).</span></span>

<span data-ttu-id="84aa7-250">*Existe uma forma tooconfigure quando são recolhidos os dados?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-250">*Is there a way tooconfigure when data is collected?*</span></span>

* <span data-ttu-id="84aa7-251">Neste momento, não.</span><span class="sxs-lookup"><span data-stu-id="84aa7-251">Not at this time.</span></span>

<span data-ttu-id="84aa7-252">*Por que motivo tenho tooconfigure uma conta Run As?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-252">*Why do I have tooconfigure a Run As Account?*</span></span>

* <span data-ttu-id="84aa7-253">Para o SQL Server, um pequeno número de consultas SQL é executado.</span><span class="sxs-lookup"><span data-stu-id="84aa7-253">For SQL Server, a small number of SQL queries are run.</span></span> <span data-ttu-id="84aa7-254">Serem toorun, uma conta Run As com VIEW SERVER STATE permissões tooSQL tem de ser utilizado.</span><span class="sxs-lookup"><span data-stu-id="84aa7-254">In order for them toorun, a Run As Account with VIEW SERVER STATE permissions tooSQL must be used.</span></span>  <span data-ttu-id="84aa7-255">Além disso, na ordem tooquery WMI, as credenciais de administrador local são necessárias.</span><span class="sxs-lookup"><span data-stu-id="84aa7-255">In addition, in order tooquery WMI, local administrator credentials are required.</span></span>

<span data-ttu-id="84aa7-256">*Por que motivo apresentar apenas recomendações de 10 principais de Olá?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-256">*Why display only hello top 10 recommendations?*</span></span>

* <span data-ttu-id="84aa7-257">Em vez de dando-lhe uma lista exaustiva muito confuso das tarefas, recomendamos que lhe concentrar-se no endereçamento recomendações Olá definida primeiro.</span><span class="sxs-lookup"><span data-stu-id="84aa7-257">Instead of giving you an exhaustive overwhelming list of tasks, we recommend that you focus on addressing hello prioritized recommendations first.</span></span> <span data-ttu-id="84aa7-258">Depois de resolvê-los, recomendações adicionais deixará de estar disponíveis.</span><span class="sxs-lookup"><span data-stu-id="84aa7-258">After you address them, additional recommendations will become available.</span></span> <span data-ttu-id="84aa7-259">Se preferir lista detalhada de Olá toosee, pode ver todas as recomendações com pesquisa de registo do Olá OMS.</span><span class="sxs-lookup"><span data-stu-id="84aa7-259">If you prefer toosee hello detailed list, you can view all recommendations using hello OMS log search.</span></span>

<span data-ttu-id="84aa7-260">*Existe uma forma tooignore uma recomendação?*</span><span class="sxs-lookup"><span data-stu-id="84aa7-260">*Is there a way tooignore a recommendation?*</span></span>

* <span data-ttu-id="84aa7-261">Sim, consulte [ignorar recomendações](#ignore-recommendations) secção acima.</span><span class="sxs-lookup"><span data-stu-id="84aa7-261">Yes, see [Ignore recommendations](#ignore-recommendations) section above.</span></span>

## <a name="next-steps"></a><span data-ttu-id="84aa7-262">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="84aa7-262">Next steps</span></span>
* <span data-ttu-id="84aa7-263">[Pesquisar registos](log-analytics-log-searches.md) tooview detalhadas dados da avaliação do SQL Server e as recomendações.</span><span class="sxs-lookup"><span data-stu-id="84aa7-263">[Search logs](log-analytics-log-searches.md) tooview detailed SQL Assessment data and recommendations.</span></span>
