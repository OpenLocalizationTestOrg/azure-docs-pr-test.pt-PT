---
title: "recomendações de desempenho de aaaApply - SQL Database do Azure | Microsoft Docs"
description: "Pode utilizar Olá toofind portal do Azure desempenho recomendações que podem otimizar o desempenho da SQL Database do Azure ou toocorrect algum problema identificado na sua carga de trabalho."
services: sql-database
documentationcenter: 
author: stevestein
manager: jhubbard
editor: monicar
ms.assetid: cda8a646-0584-4368-b28a-85cdd9b54fcd
ms.service: sql-database
ms.custom: monitor & tune
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-management
ms.date: 07/05/2017
ms.author: sstein
ms.openlocfilehash: 0b2234840fc3254d235db9e7d18f5bc912851c6d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="find-and-apply-performance-recommendations"></a><span data-ttu-id="351e4-103">Localizar e aplicar as recomendações de desempenho</span><span class="sxs-lookup"><span data-stu-id="351e4-103">Find and apply performance recommendations</span></span>

<span data-ttu-id="351e4-104">Pode utilizar Olá toofind portal do Azure desempenho recomendações que podem otimizar o desempenho da SQL Database do Azure ou toocorrect algum problema identificado na sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="351e4-104">You can use hello Azure portal toofind performance recommendations that can optimize performance of your Azure SQL Database or toocorrect some issue identified in your workload.</span></span> <span data-ttu-id="351e4-105">**Recomendação de desempenho** página no portal do Azure permite-lhe toofind Olá superior as recomendações com base no respetivo impacto potencial.</span><span class="sxs-lookup"><span data-stu-id="351e4-105">**Performance recommendation** page in Azure portal enables you toofind hello top recommendations based on their potential impact.</span></span> 

## <a name="viewing-recommendations"></a><span data-ttu-id="351e4-106">Recomendações de visualização</span><span class="sxs-lookup"><span data-stu-id="351e4-106">Viewing recommendations</span></span>

<span data-ttu-id="351e4-107">tooview e aplicar as recomendações de desempenho, precisa de Olá correto [controlo de acesso baseado em funções](../active-directory/role-based-access-control-what-is.md) permissões no Azure.</span><span class="sxs-lookup"><span data-stu-id="351e4-107">tooview and apply performance recommendations, you need hello correct [role-based access control](../active-directory/role-based-access-control-what-is.md) permissions in Azure.</span></span> <span data-ttu-id="351e4-108">**Leitor**, **contribuinte da BD SQL** permissões são necessárias tooview recomendações, e **proprietário**, **contribuinte da BD SQL** são necessárias permissões tooexecute quaisquer ações; Criar ou remova índices e cancelar a criação de índices.</span><span class="sxs-lookup"><span data-stu-id="351e4-108">**Reader**, **SQL DB Contributor** permissions are required tooview recommendations, and **Owner**, **SQL DB Contributor** permissions are required tooexecute any actions; create or drop indexes and cancel index creation.</span></span>

<span data-ttu-id="351e4-109">Utilize Olá seguir as recomendações de desempenho de toofind passos no portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="351e4-109">Use hello following steps toofind performance recommendations on Azure portal:</span></span>

1. <span data-ttu-id="351e4-110">Inicie sessão no toohello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="351e4-110">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="351e4-111">Aceda demasiado**mais serviços** > **bases de dados SQL**e selecione a base de dados.</span><span class="sxs-lookup"><span data-stu-id="351e4-111">Go too**More services** > **SQL databases**, and select your database.</span></span>
3. <span data-ttu-id="351e4-112">Navegue demasiado**recomendação de desempenho** tooview recomendações disponíveis para a base de dados selecionada Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-112">Navigate too**Performance recommendation** tooview available recommendations for hello selected database.</span></span>

<span data-ttu-id="351e4-113">Recomendações de desempenho são shonw no Olá tabela toohello de semelhante mostrado na Olá figura a seguir:</span><span class="sxs-lookup"><span data-stu-id="351e4-113">Performance recommendations are shonw in hello table similar toohello one shown on hello following figure:</span></span>

![Recomendações](./media/sql-database-advisor-portal/recommendations.png)

<span data-ttu-id="351e4-115">Recomendações são ordenadas pelo respetivo potencial impacto no desempenho no Olá seguintes categorias:</span><span class="sxs-lookup"><span data-stu-id="351e4-115">Recommendations are sorted by their potential impact on performance into hello following categories:</span></span>

| <span data-ttu-id="351e4-116">Impacto</span><span class="sxs-lookup"><span data-stu-id="351e4-116">Impact</span></span> | <span data-ttu-id="351e4-117">Descrição</span><span class="sxs-lookup"><span data-stu-id="351e4-117">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="351e4-118">Elevado</span><span class="sxs-lookup"><span data-stu-id="351e4-118">High</span></span> |<span data-ttu-id="351e4-119">Recomendações de elevado impacto devem fornecer o impacto no desempenho mais significativo Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-119">High impact recommendations should provide hello most significant performance impact.</span></span> |
| <span data-ttu-id="351e4-120">Médio</span><span class="sxs-lookup"><span data-stu-id="351e4-120">Medium</span></span> |<span data-ttu-id="351e4-121">Impacto médio recomendações devem melhorar o desempenho, mas não substancialmente.</span><span class="sxs-lookup"><span data-stu-id="351e4-121">Medium impact recommendations should improve performance, but not substantially.</span></span> |
| <span data-ttu-id="351e4-122">Baixo</span><span class="sxs-lookup"><span data-stu-id="351e4-122">Low</span></span> |<span data-ttu-id="351e4-123">Recomendações de impacto baixa devem fornecer um melhor desempenho sem, mas poderão não ser significativos melhoramentos.</span><span class="sxs-lookup"><span data-stu-id="351e4-123">Low impact recommendations should provide better performance than without, but improvements might not be significant.</span></span> |


> [!NOTE]
> <span data-ttu-id="351e4-124">Base de dados SQL do Azure necessita toomonitor atividades com pelo menos um dia na ordem tooidentify algumas recomendações.</span><span class="sxs-lookup"><span data-stu-id="351e4-124">Azure SQL Database needs toomonitor activities at least for a day in order tooidentify some recommendations.</span></span> <span data-ttu-id="351e4-125">Olá SQL Database do Azure pode otimizar mais facilmente para padrões de consulta consistente que pode para aleatórios bursts spotty da atividade.</span><span class="sxs-lookup"><span data-stu-id="351e4-125">hello Azure SQL Database can more easily optimize for consistent query patterns than it can for random spotty bursts of activity.</span></span> <span data-ttu-id="351e4-126">Se as recomendações não estão disponível corrently, Olá **recomendação de desempenho** página fornece uma mensagem explicar o motivo.</span><span class="sxs-lookup"><span data-stu-id="351e4-126">If recommendations are not corrently available, hello **Performance recommendation** page provides a message explaining why.</span></span>
> 

<span data-ttu-id="351e4-127">Também pode ver o estado de Olá do histórico de operações Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-127">You can also view hello status of hello historical operations.</span></span> <span data-ttu-id="351e4-128">Selecione uma recomendação ou estado toosee mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="351e4-128">Select a recommendation or status toosee  more details.</span></span>

<span data-ttu-id="351e4-129">Eis um exemplo de recomendação "Criar índice" no Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="351e4-129">Here is an example of "Create index" recommendation in hello Azure portal.</span></span>

![Criar o índice](./media/sql-database-advisor-portal/sql-database-performance-recommendation.png)

## <a name="applying-recommendations"></a><span data-ttu-id="351e4-131">Aplicar as recomendações</span><span class="sxs-lookup"><span data-stu-id="351e4-131">Applying recommendations</span></span>
<span data-ttu-id="351e4-132">Base de dados SQL do Azure dá-lhe controlo total sobre a forma como as recomendações são ativada utilizando qualquer um dos Olá seguintes três opções:</span><span class="sxs-lookup"><span data-stu-id="351e4-132">Azure SQL Database gives you full control over how recommendations are enabled using any of hello following three options:</span></span> 

* <span data-ttu-id="351e4-133">Aplica recomendações individuais um cada vez.</span><span class="sxs-lookup"><span data-stu-id="351e4-133">Apply individual recommendations one at a time.</span></span>
* <span data-ttu-id="351e4-134">Ativar Olá tooautomatically otimização automática aplicar recomendações.</span><span class="sxs-lookup"><span data-stu-id="351e4-134">Enable hello Automatic tuning tooautomatically apply recommendations.</span></span>
* <span data-ttu-id="351e4-135">tooimplement uma recomendação manualmente, execute Olá recomendado script T-SQL em relação a sua base de dados.</span><span class="sxs-lookup"><span data-stu-id="351e4-135">tooimplement a recommendation manually, run hello recommended T-SQL script against your database.</span></span>

<span data-ttu-id="351e4-136">Selecione qualquer tooview recomendação os respectivos detalhes e, em seguida, clique em **Ver script** tooreview Olá obter detalhes exatos sobre como a recomendação de Olá é criada.</span><span class="sxs-lookup"><span data-stu-id="351e4-136">Select any recommendation tooview its details and then click **View script** tooreview hello exact details of how hello recommendation is created.</span></span>

<span data-ttu-id="351e4-137">base de dados de Olá permanece online enquanto é aplicada a recomendação de Olá – utilizar a recomendação de desempenho ou a otimização automática nunca demora uma base de dados offline.</span><span class="sxs-lookup"><span data-stu-id="351e4-137">hello database remains online while hello recommendation is applied -- using performance recommendation or automatic tuning never takes a database offline.</span></span>

### <a name="apply-an-individual-recommendation"></a><span data-ttu-id="351e4-138">Aplicar uma recomendação individuais</span><span class="sxs-lookup"><span data-stu-id="351e4-138">Apply an individual recommendation</span></span>
<span data-ttu-id="351e4-139">Pode rever e aceitar recomendações um cada vez.</span><span class="sxs-lookup"><span data-stu-id="351e4-139">You can review and accept recommendations one at a time.</span></span>

1. <span data-ttu-id="351e4-140">No Olá **recomendações** painel, selecione uma recomendação.</span><span class="sxs-lookup"><span data-stu-id="351e4-140">On hello **Recommendations** blade, select a recommendation.</span></span>
2. <span data-ttu-id="351e4-141">No Olá **detalhes** painel clique **aplicar** botão.</span><span class="sxs-lookup"><span data-stu-id="351e4-141">On hello **Details** blade click **Apply** button.</span></span>
   
    ![aplicar a recomendação](./media/sql-database-advisor-portal/apply.png)

<span data-ttu-id="351e4-143">Recomendação selecionada será aplicada na base de dados de Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-143">Selected recommendation will be applied on hello database.</span></span>

### <a name="removing-recommendations-from-hello-list"></a><span data-ttu-id="351e4-144">A remover as recomendações da lista de Olá</span><span class="sxs-lookup"><span data-stu-id="351e4-144">Removing recommendations from hello list</span></span>
<span data-ttu-id="351e4-145">Se a lista de recomendações contiver itens que pretende que o tooremove da lista de Olá, pode eliminar recomendação Olá:</span><span class="sxs-lookup"><span data-stu-id="351e4-145">If your list of recommendations contains items that you want tooremove from hello list, you can discard hello recommendation:</span></span>

1. <span data-ttu-id="351e4-146">Selecione uma recomendação na lista de Olá de **recomendações** detalhes de Olá tooopen.</span><span class="sxs-lookup"><span data-stu-id="351e4-146">Select a recommendation in hello list of **Recommendations** tooopen hello details.</span></span>
2. <span data-ttu-id="351e4-147">Clique em **rejeitar** no Olá **detalhes** painel.</span><span class="sxs-lookup"><span data-stu-id="351e4-147">Click **Discard** on hello **Details** blade.</span></span>

<span data-ttu-id="351e4-148">Se assim o desejar, pode adicionar itens rejeitados fazer uma cópia toohello **recomendações** lista:</span><span class="sxs-lookup"><span data-stu-id="351e4-148">If desired, you can add discarded items back toohello **Recommendations** list:</span></span>

1. <span data-ttu-id="351e4-149">No Olá **recomendações** painel clique **vista rejeitada**.</span><span class="sxs-lookup"><span data-stu-id="351e4-149">On hello **Recommendations** blade click **View discarded**.</span></span>
2. <span data-ttu-id="351e4-150">Selecione um item rejeitado Olá lista tooview os respetivos detalhes.</span><span class="sxs-lookup"><span data-stu-id="351e4-150">Select a discarded item from hello list tooview its details.</span></span>
3. <span data-ttu-id="351e4-151">Opcionalmente, clique em **anular rejeitar** tooadd Olá índice back toohello principal lista de **recomendações**.</span><span class="sxs-lookup"><span data-stu-id="351e4-151">Optionally, click **Undo Discard** tooadd hello index back toohello main list of **Recommendations**.</span></span>


### <a name="enable-automatic-tuning"></a><span data-ttu-id="351e4-152">Ativar o ajuste automático</span><span class="sxs-lookup"><span data-stu-id="351e4-152">Enable automatic tuning</span></span>
<span data-ttu-id="351e4-153">Pode definir automaticamente recomendações de tooimplement Olá SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="351e4-153">You can set hello Azure SQL Database tooimplement recommendations automatically.</span></span> <span data-ttu-id="351e4-154">Como recomendações fiquem disponíveis automaticamente serão aplicadas.</span><span class="sxs-lookup"><span data-stu-id="351e4-154">As recommendations become available they will automatically be applied.</span></span> <span data-ttu-id="351e4-155">Como com todas as recomendações geridas pelo Olá serviço esteja de impacto no desempenho de Olá recomendação Olá negativo será revertido.</span><span class="sxs-lookup"><span data-stu-id="351e4-155">As with all recommendations managed by hello service if hello performance impact is negative hello recommendation will be reverted.</span></span>

1. <span data-ttu-id="351e4-156">No Olá **recomendações** painel, clique em **Automate**:</span><span class="sxs-lookup"><span data-stu-id="351e4-156">On hello **Recommendations** blade, click **Automate**:</span></span>
   
    ![Definições do Advisor](./media/sql-database-advisor-portal/settings.png)
2. <span data-ttu-id="351e4-158">Selecione tooautomate ações:</span><span class="sxs-lookup"><span data-stu-id="351e4-158">Select actions tooautomate:</span></span>
   
    ![Recomendado índices](./media/sql-database-advisor-portal/automation.png)

### <a name="manually-run-hello-recommended-t-sql-script"></a><span data-ttu-id="351e4-160">Executar manualmente Olá recomendado script T-SQL</span><span class="sxs-lookup"><span data-stu-id="351e4-160">Manually run hello recommended T-SQL script</span></span>
<span data-ttu-id="351e4-161">Selecione qualquer recomendação e, em seguida, clique em **Ver script**.</span><span class="sxs-lookup"><span data-stu-id="351e4-161">Select any recommendation and then click **View script**.</span></span> <span data-ttu-id="351e4-162">Execute este script na sua base de dados toomanually aplicar a recomendação de Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-162">Run this script against your database toomanually apply hello recommendation.</span></span>

<span data-ttu-id="351e4-163">*Índices que são executados manualmente não são monitorizados e validados de impacto no desempenho pelo serviço de Olá* pelo que é sugerido que monitorizar estes índices após criação tooverify fornecer ganhos de desempenho e ajustar ou eliminá-los se necessário.</span><span class="sxs-lookup"><span data-stu-id="351e4-163">*Indexes that are manually executed are not monitored and validated for performance impact by hello service* so it is suggested that you monitor these indexes after creation tooverify they provide performance gains and adjust or delete them if necessary.</span></span> <span data-ttu-id="351e4-164">Para obter detalhes sobre a criação de índices, consulte [criar índice (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span><span class="sxs-lookup"><span data-stu-id="351e4-164">For details about creating indexes, see [CREATE INDEX (Transact-SQL)](https://msdn.microsoft.com/library/ms188783.aspx).</span></span>

### <a name="canceling-recommendations"></a><span data-ttu-id="351e4-165">Cancelar recomendações</span><span class="sxs-lookup"><span data-stu-id="351e4-165">Canceling recommendations</span></span>
<span data-ttu-id="351e4-166">Recomendações que estão num **pendente**, **verificar**, ou **êxito** Estado pode ser cancelado.</span><span class="sxs-lookup"><span data-stu-id="351e4-166">Recommendations that are in a **Pending**, **Verifying**, or **Success** status can be canceled.</span></span> <span data-ttu-id="351e4-167">Recomendações com um Estado de **Executing** não pode ser cancelado.</span><span class="sxs-lookup"><span data-stu-id="351e4-167">Recommendations with a status of **Executing** cannot be canceled.</span></span>

1. <span data-ttu-id="351e4-168">Selecione uma recomendação Olá **otimização histórico** Olá de tooopen área **os detalhes das recomendações** painel.</span><span class="sxs-lookup"><span data-stu-id="351e4-168">Select a recommendation in hello **Tuning History** area tooopen hello **recommendations details** blade.</span></span>
2. <span data-ttu-id="351e4-169">Clique em **Cancelar** tooabort o processo de Olá aplicar a recomendação de Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-169">Click **Cancel** tooabort hello process of applying hello recommendation.</span></span>

## <a name="monitoring-operations"></a><span data-ttu-id="351e4-170">Operações de monitorização</span><span class="sxs-lookup"><span data-stu-id="351e4-170">Monitoring operations</span></span>
<span data-ttu-id="351e4-171">Aplicar a recomendação não poderá acontecer instantaneamente.</span><span class="sxs-lookup"><span data-stu-id="351e4-171">Applying a recommendation might not happen instantaneously.</span></span> <span data-ttu-id="351e4-172">portal de Olá fornece detalhes sobre o estado de Olá de recomendação.</span><span class="sxs-lookup"><span data-stu-id="351e4-172">hello portal provides details regarding hello status of recommendation.</span></span> <span data-ttu-id="351e4-173">Olá, são possíveis Estados que um índice pode ser:</span><span class="sxs-lookup"><span data-stu-id="351e4-173">hello following are possible states that an index can be in:</span></span>

| <span data-ttu-id="351e4-174">Estado</span><span class="sxs-lookup"><span data-stu-id="351e4-174">Status</span></span> | <span data-ttu-id="351e4-175">Descrição</span><span class="sxs-lookup"><span data-stu-id="351e4-175">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="351e4-176">Pendente</span><span class="sxs-lookup"><span data-stu-id="351e4-176">Pending</span></span> |<span data-ttu-id="351e4-177">Aplica a recomendação comando foi recebido e está agendado para execução.</span><span class="sxs-lookup"><span data-stu-id="351e4-177">Apply recommendation command has been received and is scheduled for execution.</span></span> |
| <span data-ttu-id="351e4-178">Executar</span><span class="sxs-lookup"><span data-stu-id="351e4-178">Executing</span></span> |<span data-ttu-id="351e4-179">está a ser aplicada a recomendação de Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-179">hello recommendation is being applied.</span></span> |
| <span data-ttu-id="351e4-180">A verificar</span><span class="sxs-lookup"><span data-stu-id="351e4-180">Verifying</span></span> |<span data-ttu-id="351e4-181">Recomendação foi aplicada com êxito e o serviço de Olá é medir vantagens Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-181">Recommendation was successfully applied and hello service is measuring hello benefits.</span></span> |
| <span data-ttu-id="351e4-182">Êxito</span><span class="sxs-lookup"><span data-stu-id="351e4-182">Success</span></span> |<span data-ttu-id="351e4-183">Recomendação foi aplicada com êxito e tem sido medidos benefícios.</span><span class="sxs-lookup"><span data-stu-id="351e4-183">Recommendation was successfully applied and benefits have been measured.</span></span> |
| <span data-ttu-id="351e4-184">Erro</span><span class="sxs-lookup"><span data-stu-id="351e4-184">Error</span></span> |<span data-ttu-id="351e4-185">Ocorreu um erro durante o processo de Olá aplicar a recomendação de Olá.</span><span class="sxs-lookup"><span data-stu-id="351e4-185">An error occurred during hello process of applying hello recommendation.</span></span> <span data-ttu-id="351e4-186">Isto pode ser um problema passageiro ou, possivelmente, uma tabela de toohello de alteração de esquema e scripts de Olá já não é válido.</span><span class="sxs-lookup"><span data-stu-id="351e4-186">This can be a transient issue, or possibly a schema change toohello table and hello script is no longer valid.</span></span> |
| <span data-ttu-id="351e4-187">A reversão</span><span class="sxs-lookup"><span data-stu-id="351e4-187">Reverting</span></span> |<span data-ttu-id="351e4-188">recomendação de Olá foi aplicada, mas foi considerado vvalidação não performant e está a ser revertida automaticamente.</span><span class="sxs-lookup"><span data-stu-id="351e4-188">hello recommendation was applied, but has been deemed non-performant and is being automatically reverted.</span></span> |
| <span data-ttu-id="351e4-189">Reverter</span><span class="sxs-lookup"><span data-stu-id="351e4-189">Reverted</span></span> |<span data-ttu-id="351e4-190">recomendação de Olá foi revertida.</span><span class="sxs-lookup"><span data-stu-id="351e4-190">hello recommendation was reverted.</span></span> |

<span data-ttu-id="351e4-191">Clique uma recomendação de no processo do Olá lista toosee mais detalhes:</span><span class="sxs-lookup"><span data-stu-id="351e4-191">Click an in-process recommendation from hello list toosee more details:</span></span>

![Recomendado índices](./media/sql-database-advisor-portal/operations.png)

### <a name="reverting-a-recommendation"></a><span data-ttu-id="351e4-193">Reverter uma recomendação</span><span class="sxs-lookup"><span data-stu-id="351e4-193">Reverting a recommendation</span></span>
<span data-ttu-id="351e4-194">Se utilizou a recomendação do Olá desempenho recomendações tooapply Olá (que significa que não foi executado manualmente script Olá T-SQL)-la automaticamente reverterá se localiza toobe de impacto do desempenho de Olá negativo.</span><span class="sxs-lookup"><span data-stu-id="351e4-194">If you used hello performance recommendations tooapply hello recommendation (meaning you did not manually run hello T-SQL script) it will automatically revert it if it finds hello performance impact toobe negative.</span></span> <span data-ttu-id="351e4-195">Se por alguma razão pretende simplesmente toorevert uma recomendação para fazer o seguinte de Olá:</span><span class="sxs-lookup"><span data-stu-id="351e4-195">If for any reason you simply want toorevert a recommendation you can do hello following:</span></span>

1. <span data-ttu-id="351e4-196">Selecione uma recomendação aplicada com êxito na Olá **otimização histórico** área.</span><span class="sxs-lookup"><span data-stu-id="351e4-196">Select a successfully applied recommendation in hello **Tuning history** area.</span></span>
2. <span data-ttu-id="351e4-197">Clique em **reverter** no Olá **detalhes de recomendação** painel.</span><span class="sxs-lookup"><span data-stu-id="351e4-197">Click **Revert** on hello **recommendation details** blade.</span></span>

![Recomendado índices](./media/sql-database-advisor-portal/details.png)

## <a name="monitoring-performance-impact-of-index-recommendations"></a><span data-ttu-id="351e4-199">Impacto no desempenho das recomendações do índice de monitorização</span><span class="sxs-lookup"><span data-stu-id="351e4-199">Monitoring performance impact of index recommendations</span></span>
<span data-ttu-id="351e4-200">Depois das recomendações são implementadas com êxito (atualmente, operações de índice e parametrizar recomendações de consultas só), pode clicar em **informações acerca das consultas** no tooopen de painel de detalhes de recomendação Olá [consulta Informações acerca do desempenho](sql-database-query-performance.md) e ver o impacto do desempenho Olá das suas consultas superiores.</span><span class="sxs-lookup"><span data-stu-id="351e4-200">After recommendations are successfully implemented (currently, index operations and parameterize queries recommendations only) you can click **Query Insights** on hello recommendation details blade tooopen [Query Performance Insights](sql-database-query-performance.md) and see hello performance impact of your top queries.</span></span>

![Impacto no desempenho do monitor](./media/sql-database-advisor-portal/query-insights.png)

## <a name="summary"></a><span data-ttu-id="351e4-202">Resumo</span><span class="sxs-lookup"><span data-stu-id="351e4-202">Summary</span></span>
<span data-ttu-id="351e4-203">Base de dados SQL do Azure fornece recomendações para melhorar o desempenho de base de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="351e4-203">Azure SQL Database provides recommendations for improving SQL database performance.</span></span> <span data-ttu-id="351e4-204">Fornecendo scripts T-SQL, bem como individuais e totalmente-automático, obter um assistência útil para otimizar a base de dados e, em última análise melhorar o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="351e4-204">By providing T-SQL scripts, as well as individual and fully-automatic, you get a helpful assistance in optimizing your database and ultimately improving query performance.</span></span>

## <a name="next-steps"></a><span data-ttu-id="351e4-205">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="351e4-205">Next steps</span></span>
<span data-ttu-id="351e4-206">Monitorizar as recomendações e continuar tooapply-los toorefine desempenho.</span><span class="sxs-lookup"><span data-stu-id="351e4-206">Monitor your recommendations and continue tooapply them toorefine performance.</span></span> <span data-ttu-id="351e4-207">Cargas de trabalho de base de dados são dinâmicas e alterar continuamente.</span><span class="sxs-lookup"><span data-stu-id="351e4-207">Database workloads are dynamic and change continuously.</span></span> <span data-ttu-id="351e4-208">Base de dados SQL do Azure irá prosseguir toomonitor e fornecer recomendações podem potencialmente melhorar o desempenho da base de dados.</span><span class="sxs-lookup"><span data-stu-id="351e4-208">Azure SQL Database will continue toomonitor and provide recommendations that can potentially improve your database's performance.</span></span> 

* <span data-ttu-id="351e4-209">Consulte [otimização automática](sql-database-automatic-tuning.md) toolearn mais informações sobre como Olá otimização automática na SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="351e4-209">See [Automatic tuning](sql-database-automatic-tuning.md) toolearn more about hello automatic tuning in Azure SQL Database.</span></span>
* <span data-ttu-id="351e4-210">Consulte [recomendações de desempenho](sql-database-advisor.md) para uma descrição geral das recomendações de desempenho de SQL Database do Azure.</span><span class="sxs-lookup"><span data-stu-id="351e4-210">See [Performance recommendations](sql-database-advisor.md) for an overview of Azure SQL Database performance recommendations.</span></span>
* <span data-ttu-id="351e4-211">Consulte [Query Performance Insight](sql-database-query-performance.md) toolearn sobre a visualização de impacto no desempenho de Olá das suas consultas superiores.</span><span class="sxs-lookup"><span data-stu-id="351e4-211">See [Query Performance Insights](sql-database-query-performance.md) toolearn about viewing hello performance impact of your top queries.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="351e4-212">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="351e4-212">Additional resources</span></span>
* [<span data-ttu-id="351e4-213">O arquivo de consultas</span><span class="sxs-lookup"><span data-stu-id="351e4-213">Query Store</span></span>](https://msdn.microsoft.com/library/dn817826.aspx)
* [<span data-ttu-id="351e4-214">CRIAR O ÍNDICE</span><span class="sxs-lookup"><span data-stu-id="351e4-214">CREATE INDEX</span></span>](https://msdn.microsoft.com/library/ms188783.aspx)
* [<span data-ttu-id="351e4-215">Controlo de acesso baseado em funções</span><span class="sxs-lookup"><span data-stu-id="351e4-215">Role-based access control</span></span>](../active-directory/role-based-access-control-what-is.md)

