---
title: "aaaIT conector de gestão de serviço no OMS | Microsoft Docs"
description: "Utilize o monitor de toocentrally Olá conector de gestão de serviços de TI e gerir itens de trabalho ITSM Olá no OMS e resolva os problemas rapidamente."
services: log-analytics
documentationcenter: 
author: JYOTHIRMAISURI
manager: riyazp
editor: 
ms.assetid: 0b1414d9-b0a7-4e4e-a652-d3a6ff1118c4
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/19/2017
ms.author: v-jysur
ms.openlocfilehash: 33ed5d432591b836eb41ba982c66c96f22879444
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="centrally-manage-itsm-work-items-using-it-service-management-connector-preview"></a><span data-ttu-id="00e4d-103">Gerir centralmente a itens de trabalho ITSM utilizando o conector de gestão de serviços de TI (pré-visualização)</span><span class="sxs-lookup"><span data-stu-id="00e4d-103">Centrally manage ITSM work items using IT Service Management Connector (Preview)</span></span>

![Símbolo do conector de gestão do serviço IT](./media/log-analytics-itsmc/itsmc-symbol.png)

<span data-ttu-id="00e4d-105">Pode utilizar Olá conector de gestão de serviço de TI (ITSMC) na análise de registos do OMS toocentrally monitorizar e gerir itens de trabalho em seu ITSM produtos/serviços.</span><span class="sxs-lookup"><span data-stu-id="00e4d-105">You can use hello IT Service Management Connector (ITSMC) in OMS Log Analytics toocentrally monitor and manage work items across your ITSM products/services.</span></span>

<span data-ttu-id="00e4d-106">Olá conector de gestão de serviços de TI integra seus serviços e produtos de gestão de serviço de TI (ITSM) existente com a análise de registos do OMS.</span><span class="sxs-lookup"><span data-stu-id="00e4d-106">hello IT Service Management Connector integrates your existing IT Service Management (ITSM) products and services with OMS Log Analytics.</span></span>  <span data-ttu-id="00e4d-107">solução Olá tem integração bidirecional com ITSM produtos/serviços, onde fornece Olá OMS utilizadores incidentes de toocreate uma opção, alertas ou eventos na solução ITSM.</span><span class="sxs-lookup"><span data-stu-id="00e4d-107">hello solution has bidirectional integration with ITSM products/services, where it provides hello OMS users an option toocreate incidents, alerts, or events in ITSM solution.</span></span> <span data-ttu-id="00e4d-108">conector Olá também importa dados, tais como incidentes e pedidos de alteração da solução ITSM para análise de registos do OMS.</span><span class="sxs-lookup"><span data-stu-id="00e4d-108">hello connector also  imports data such as incidents, and change requests from ITSM solution into OMS Log Analytics.</span></span>

<span data-ttu-id="00e4d-109">Com o conector de gestão de serviços de TI, pode:</span><span class="sxs-lookup"><span data-stu-id="00e4d-109">With IT Service Management Connector, you can:</span></span>

  - <span data-ttu-id="00e4d-110">Monitorizar e gerir itens de trabalho para ITSM produtos/serviços utilizados em toda a organização centralmente.</span><span class="sxs-lookup"><span data-stu-id="00e4d-110">Centrally monitor and manage work items for ITSM products/services used across your organization.</span></span>
  - <span data-ttu-id="00e4d-111">Crie itens de trabalho ITSM (por exemplo, o alerta do evento, incidente) no ITSM de alertas do OMS e através de pesquisa de registo.</span><span class="sxs-lookup"><span data-stu-id="00e4d-111">Create ITSM work items (like alert, event, incident) in ITSM from OMS alerts and through log search.</span></span>
  - <span data-ttu-id="00e4d-112">Leia os incidentes e pedidos de alteração da solução ITSM e correlacionar com dados de registo relevantes na área de trabalho de análise de registos.</span><span class="sxs-lookup"><span data-stu-id="00e4d-112">Read incidents and change requests from your ITSM solution and correlate with relevant log data in Log Analytics workspace.</span></span>
  - <span data-ttu-id="00e4d-113">Localize quaisquer eventos de atividade invulgares e inesperados e resolvê-los, mesmo antes dos utilizadores finais de Olá chamar e comunicá-los toohello técnico.</span><span class="sxs-lookup"><span data-stu-id="00e4d-113">Find any unexpected and unusual events and resolve them, even before hello end users call and report them toohello helpdesk.</span></span>
  - <span data-ttu-id="00e4d-114">Importar dados de itens de trabalho para análise de registos e criar a chave de desempenho (KPI) do indicador relatórios.</span><span class="sxs-lookup"><span data-stu-id="00e4d-114">Import work items data into Log Analytics and create key performance indicator (KPI) reports.</span></span>  <span data-ttu-id="00e4d-115">Utilizar estes relatórios, pode identificar, avaliar e atuar sobre vários itens importantes, tais como a avaliação de malware.</span><span class="sxs-lookup"><span data-stu-id="00e4d-115">Using these reports, you can identify, assess and act on several important items such as malware assessment.</span></span>
  - <span data-ttu-id="00e4d-116">Ver organizados dashboards para informações mais aprofundadas sobre incidentes, pedidos de alteração e sistemas afetados.</span><span class="sxs-lookup"><span data-stu-id="00e4d-116">View curated dashboards for deeper insights on incidents, change requests and impacted systems.</span></span>
  - <span data-ttu-id="00e4d-117">Resolva os problemas mais rápida através da correlação entre a com outras soluções de gestão na área de trabalho de análise de registos de Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-117">Troubleshoot faster by correlating with other management solutions in hello Log Analytics workspace.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="00e4d-118">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00e4d-118">Prerequisites</span></span>

<span data-ttu-id="00e4d-119">tooimport Olá ITSM itens de trabalho para análise de registos do OMS, a solução de Olá requer uma ligação entre Olá conector de gestão de serviços de TI no Olá OMS e Olá TI SM produtos/serviços a partir do qual importar itens de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-119">tooimport hello ITSM work items into OMS Log Analytics, hello solution requires a connection between hello IT Service Management Connector in hello OMS and hello IT SM product/service from which you import hello work items.</span></span>


## <a name="configuration"></a><span data-ttu-id="00e4d-120">Configuração</span><span class="sxs-lookup"><span data-stu-id="00e4d-120">Configuration</span></span>

<span data-ttu-id="00e4d-121">Adicionar Olá espaço de trabalho do conector de gestão de serviços de TI solução tooyour OMS, utilizando o processo de Olá descrito em [soluções de análise de registos de adicionar de Olá soluções galeria](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="00e4d-121">Add hello IT Service Management Connector solution tooyour OMS work space, using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

<span data-ttu-id="00e4d-122">O conector de gestão do serviço IT mosaico como ver na Galeria de soluções de Olá:</span><span class="sxs-lookup"><span data-stu-id="00e4d-122">IT Service Management Connector tile as you see in hello Solutions gallery:</span></span>

![mosaico de conector](./media/log-analytics-itsmc/itsmc-solutions-tile.png)

<span data-ttu-id="00e4d-124">Após a adição com êxito, verá Olá conector de gestão de serviços de TI em **OMS** > **definições** > **origens ligadas.**</span><span class="sxs-lookup"><span data-stu-id="00e4d-124">After successful addition, you will see hello IT Service Management Connector under **OMS** > **Settings** > **Connected Sources.**</span></span>

![ITSMC ligado](./media/log-analytics-itsmc/itsmc-overview-solution-in-connected-sources.png)

> [!NOTE]

> <span data-ttu-id="00e4d-126">Por predefinição, o Olá conector de gestão de serviços de TI atualiza os dados da ligação de Olá uma vez em cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="00e4d-126">By default, hello IT Service Management Connector refreshes hello connection's data once in every 24 hours.</span></span> <span data-ttu-id="00e4d-127">toorefresh da ligação atualizações dos dados de forma instantânea para qualquer modelo ou as edições que efetuar, clique em Olá atualização botão apresentado seguinte tooyour a ligação.</span><span class="sxs-lookup"><span data-stu-id="00e4d-127">toorefresh your connection's data instantly for any edits or template updates that you make, click hello refresh button displayed next tooyour connection.</span></span>

 ![Atualização ITSMC](./media/log-analytics-itsmc/itsmc-connection-refresh.png)

## <a name="management-packs"></a><span data-ttu-id="00e4d-129">Pacotes de gestão</span><span class="sxs-lookup"><span data-stu-id="00e4d-129">Management packs</span></span>
<span data-ttu-id="00e4d-130">Esta solução não requer quaisquer pacotes de gestão.</span><span class="sxs-lookup"><span data-stu-id="00e4d-130">This solution does not require any management packs.</span></span>

## <a name="connected-sources"></a><span data-ttu-id="00e4d-131">Origens ligadas</span><span class="sxs-lookup"><span data-stu-id="00e4d-131">Connected sources</span></span>

<span data-ttu-id="00e4d-132">Olá ITSM seguintes produtos/serviços são suportados pelo Olá conector de gestão de serviços de TI:</span><span class="sxs-lookup"><span data-stu-id="00e4d-132">hello following ITSM products/services are supported by hello IT Service Management Connector:</span></span>

- [<span data-ttu-id="00e4d-133">O System Center Service Manager (SCSM)</span><span class="sxs-lookup"><span data-stu-id="00e4d-133">System Center Service Manager (SCSM)</span></span>](log-analytics-itsmc-connections.md#connect-system-center-service-manager-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="00e4d-134">ServiceNow</span><span class="sxs-lookup"><span data-stu-id="00e4d-134">ServiceNow</span></span>](log-analytics-itsmc-connections.md#connect-servicenow-to-it-service-management-connector-in-oms)

- [<span data-ttu-id="00e4d-135">Provance</span><span class="sxs-lookup"><span data-stu-id="00e4d-135">Provance</span></span>](log-analytics-itsmc-connections.md#connect-provance-to-it-service-management-connector-in-oms)  

- [<span data-ttu-id="00e4d-136">Cherwell</span><span class="sxs-lookup"><span data-stu-id="00e4d-136">Cherwell</span></span>](log-analytics-itsmc-connections.md#connect-cherwell-to-it-service-management-connector-in-oms)

## <a name="using-hello-solution"></a><span data-ttu-id="00e4d-137">Utilizar a solução de Olá</span><span class="sxs-lookup"><span data-stu-id="00e4d-137">Using hello solution</span></span>

<span data-ttu-id="00e4d-138">Depois de ligar Olá conector de gestão do serviço de TI do OMS com o serviço ITSM, serviços de análise de registos de Olá inicia a recolha de dados de Olá de Olá ligado ITSM produtos/serviços.</span><span class="sxs-lookup"><span data-stu-id="00e4d-138">Once you connect hello OMS IT Service Management Connector with your ITSM service, hello Log Analytics services starts gathering hello data from hello connected ITSM products/service.</span></span>

> [!NOTE]
> - <span data-ttu-id="00e4d-139">Dados importados pela solução de conector de gestão de serviços de TI aparecem na análise de registos como eventos com o nome **ServiceDesk_CL**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-139">Data imported by IT Service Management Connector solution appears in Log Analytics as events named **ServiceDesk_CL**.</span></span>
- <span data-ttu-id="00e4d-140">Evento contém um campo com o nome **ServiceDeskWorkItemType_s**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-140">Event contains a field named **ServiceDeskWorkItemType_s**.</span></span> <span data-ttu-id="00e4d-141">que pode colocar o respetivo valor como incidentes, ou pedido de alteração, consoante Olá do item de trabalho dados contidos em Olá **ServiceDesk_CL** eventos.</span><span class="sxs-lookup"><span data-stu-id="00e4d-141">which can take its value as incident, or change request, depending on hello work item data contained in hello **ServiceDesk_CL** event.</span></span>

## <a name="input-data"></a><span data-ttu-id="00e4d-142">Dados de entrada</span><span class="sxs-lookup"><span data-stu-id="00e4d-142">Input data</span></span>
<span data-ttu-id="00e4d-143">Itens de trabalho importados do Olá ITSM produtos/serviços.</span><span class="sxs-lookup"><span data-stu-id="00e4d-143">Work items imported from hello ITSM products/services.</span></span>

<span data-ttu-id="00e4d-144">Olá informações seguintes mostram exemplos de dados recolhidos pelo conector do serviço de TI a gestão de Olá:</span><span class="sxs-lookup"><span data-stu-id="00e4d-144">hello following information shows examples of data gathered by hello IT Service Management connector:</span></span>

> [!NOTE]
> <span data-ttu-id="00e4d-145">Consoante Olá do item de trabalho importado para análise de registos do tipo **ServiceDesk_CL** contém Olá seguintes campos:</span><span class="sxs-lookup"><span data-stu-id="00e4d-145">Depending on hello work item type imported into Log Analytics, **ServiceDesk_CL** contains hello following fields:</span></span>

<span data-ttu-id="00e4d-146">**Item de trabalho:** **incidentes**</span><span class="sxs-lookup"><span data-stu-id="00e4d-146">**Work item:** **Incidents**</span></span>  
<span data-ttu-id="00e4d-147">ServiceDeskWorkItemType_s = "Incidente"</span><span class="sxs-lookup"><span data-stu-id="00e4d-147">ServiceDeskWorkItemType_s="Incident"</span></span>

<span data-ttu-id="00e4d-148">**Campos**</span><span class="sxs-lookup"><span data-stu-id="00e4d-148">**Fields**</span></span>

- <span data-ttu-id="00e4d-149">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="00e4d-149">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="00e4d-150">ID do serviço de suporte técnico</span><span class="sxs-lookup"><span data-stu-id="00e4d-150">Service Desk ID</span></span>
- <span data-ttu-id="00e4d-151">Estado</span><span class="sxs-lookup"><span data-stu-id="00e4d-151">State</span></span>
- <span data-ttu-id="00e4d-152">Urgência</span><span class="sxs-lookup"><span data-stu-id="00e4d-152">Urgency</span></span>
- <span data-ttu-id="00e4d-153">Impacto</span><span class="sxs-lookup"><span data-stu-id="00e4d-153">Impact</span></span>
- <span data-ttu-id="00e4d-154">Prioridade</span><span class="sxs-lookup"><span data-stu-id="00e4d-154">Priority</span></span>
- <span data-ttu-id="00e4d-155">Escalamento</span><span class="sxs-lookup"><span data-stu-id="00e4d-155">Escalation</span></span>
- <span data-ttu-id="00e4d-156">Criado por</span><span class="sxs-lookup"><span data-stu-id="00e4d-156">Created By</span></span>
- <span data-ttu-id="00e4d-157">Resolvido pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-157">Resolved By</span></span>
- <span data-ttu-id="00e4d-158">Fechada pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-158">Closed By</span></span>
- <span data-ttu-id="00e4d-159">Origem</span><span class="sxs-lookup"><span data-stu-id="00e4d-159">Source</span></span>
- <span data-ttu-id="00e4d-160">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="00e4d-160">Assigned To</span></span>
- <span data-ttu-id="00e4d-161">Categoria</span><span class="sxs-lookup"><span data-stu-id="00e4d-161">Category</span></span>
- <span data-ttu-id="00e4d-162">Título</span><span class="sxs-lookup"><span data-stu-id="00e4d-162">Title</span></span>
- <span data-ttu-id="00e4d-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="00e4d-163">Description</span></span>
- <span data-ttu-id="00e4d-164">Data de criação</span><span class="sxs-lookup"><span data-stu-id="00e4d-164">Created Date</span></span>
- <span data-ttu-id="00e4d-165">Data de fecho</span><span class="sxs-lookup"><span data-stu-id="00e4d-165">Closed Date</span></span>
- <span data-ttu-id="00e4d-166">Data de resolução</span><span class="sxs-lookup"><span data-stu-id="00e4d-166">Resolved Date</span></span>
- <span data-ttu-id="00e4d-167">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="00e4d-167">Last Modified Date</span></span>
- <span data-ttu-id="00e4d-168">Computador</span><span class="sxs-lookup"><span data-stu-id="00e4d-168">Computer</span></span>


<span data-ttu-id="00e4d-169">**Item de trabalho:** **pedidos de alteração**</span><span class="sxs-lookup"><span data-stu-id="00e4d-169">**Work item:** **Change Requests**</span></span>

<span data-ttu-id="00e4d-170">ServiceDeskWorkItemType_s = "ChangeRequest"</span><span class="sxs-lookup"><span data-stu-id="00e4d-170">ServiceDeskWorkItemType_s="ChangeRequest"</span></span>

<span data-ttu-id="00e4d-171">**Campos**</span><span class="sxs-lookup"><span data-stu-id="00e4d-171">**Fields**</span></span>
- <span data-ttu-id="00e4d-172">ServiceDeskConnectionName</span><span class="sxs-lookup"><span data-stu-id="00e4d-172">ServiceDeskConnectionName</span></span>
- <span data-ttu-id="00e4d-173">ID do serviço de suporte técnico</span><span class="sxs-lookup"><span data-stu-id="00e4d-173">Service Desk ID</span></span>
- <span data-ttu-id="00e4d-174">Criado por</span><span class="sxs-lookup"><span data-stu-id="00e4d-174">Created By</span></span>
- <span data-ttu-id="00e4d-175">Fechada pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-175">Closed By</span></span>
- <span data-ttu-id="00e4d-176">Origem</span><span class="sxs-lookup"><span data-stu-id="00e4d-176">Source</span></span>
- <span data-ttu-id="00e4d-177">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="00e4d-177">Assigned To</span></span>
- <span data-ttu-id="00e4d-178">Título</span><span class="sxs-lookup"><span data-stu-id="00e4d-178">Title</span></span>
- <span data-ttu-id="00e4d-179">Tipo</span><span class="sxs-lookup"><span data-stu-id="00e4d-179">Type</span></span>
- <span data-ttu-id="00e4d-180">Categoria</span><span class="sxs-lookup"><span data-stu-id="00e4d-180">Category</span></span>
- <span data-ttu-id="00e4d-181">Estado</span><span class="sxs-lookup"><span data-stu-id="00e4d-181">State</span></span>
- <span data-ttu-id="00e4d-182">Escalamento</span><span class="sxs-lookup"><span data-stu-id="00e4d-182">Escalation</span></span>
- <span data-ttu-id="00e4d-183">Estado de conflito</span><span class="sxs-lookup"><span data-stu-id="00e4d-183">Conflict Status</span></span>
- <span data-ttu-id="00e4d-184">Urgência</span><span class="sxs-lookup"><span data-stu-id="00e4d-184">Urgency</span></span>
- <span data-ttu-id="00e4d-185">Prioridade</span><span class="sxs-lookup"><span data-stu-id="00e4d-185">Priority</span></span>
- <span data-ttu-id="00e4d-186">Risco</span><span class="sxs-lookup"><span data-stu-id="00e4d-186">Risk</span></span>
- <span data-ttu-id="00e4d-187">Impacto</span><span class="sxs-lookup"><span data-stu-id="00e4d-187">Impact</span></span>
- <span data-ttu-id="00e4d-188">Atribuído a</span><span class="sxs-lookup"><span data-stu-id="00e4d-188">Assigned To</span></span>
- <span data-ttu-id="00e4d-189">Data de criação</span><span class="sxs-lookup"><span data-stu-id="00e4d-189">Created Date</span></span>
- <span data-ttu-id="00e4d-190">Data de fecho</span><span class="sxs-lookup"><span data-stu-id="00e4d-190">Closed Date</span></span>
- <span data-ttu-id="00e4d-191">Data da última modificação</span><span class="sxs-lookup"><span data-stu-id="00e4d-191">Last Modified Date</span></span>
- <span data-ttu-id="00e4d-192">Data de pedido</span><span class="sxs-lookup"><span data-stu-id="00e4d-192">Requested Date</span></span>
- <span data-ttu-id="00e4d-193">Data de início planeada</span><span class="sxs-lookup"><span data-stu-id="00e4d-193">Planned Start Date</span></span>
- <span data-ttu-id="00e4d-194">A ser planeada a data de fim</span><span class="sxs-lookup"><span data-stu-id="00e4d-194">Planned End Date</span></span>
- <span data-ttu-id="00e4d-195">Data de início do trabalho</span><span class="sxs-lookup"><span data-stu-id="00e4d-195">Work Start Date</span></span>
- <span data-ttu-id="00e4d-196">Data de fim de trabalho</span><span class="sxs-lookup"><span data-stu-id="00e4d-196">Work End Date</span></span>
- <span data-ttu-id="00e4d-197">Descrição</span><span class="sxs-lookup"><span data-stu-id="00e4d-197">Description</span></span>
- <span data-ttu-id="00e4d-198">Computador</span><span class="sxs-lookup"><span data-stu-id="00e4d-198">Computer</span></span>

## <a name="output-data-for-a-servicenow-incident"></a><span data-ttu-id="00e4d-199">Dados de saída para um incidente de ServiceNow</span><span class="sxs-lookup"><span data-stu-id="00e4d-199">Output data for a ServiceNow incident</span></span>

| <span data-ttu-id="00e4d-200">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-200">OMS field</span></span> | <span data-ttu-id="00e4d-201">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="00e4d-201">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="00e4d-202">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-202">ServiceDeskId_s</span></span>| <span data-ttu-id="00e4d-203">Número</span><span class="sxs-lookup"><span data-stu-id="00e4d-203">Number</span></span> |
| <span data-ttu-id="00e4d-204">IncidentState_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-204">IncidentState_s</span></span> | <span data-ttu-id="00e4d-205">Estado</span><span class="sxs-lookup"><span data-stu-id="00e4d-205">State</span></span> |
| <span data-ttu-id="00e4d-206">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-206">Urgency_s</span></span> |<span data-ttu-id="00e4d-207">Urgência</span><span class="sxs-lookup"><span data-stu-id="00e4d-207">Urgency</span></span> |
| <span data-ttu-id="00e4d-208">Impact_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-208">Impact_s</span></span> |<span data-ttu-id="00e4d-209">Impacto</span><span class="sxs-lookup"><span data-stu-id="00e4d-209">Impact</span></span>|
| <span data-ttu-id="00e4d-210">Priority_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-210">Priority_s</span></span> | <span data-ttu-id="00e4d-211">Prioridade</span><span class="sxs-lookup"><span data-stu-id="00e4d-211">Priority</span></span> |
| <span data-ttu-id="00e4d-212">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-212">CreatedBy_s</span></span> | <span data-ttu-id="00e4d-213">Abrir por</span><span class="sxs-lookup"><span data-stu-id="00e4d-213">Opened by</span></span> |
| <span data-ttu-id="00e4d-214">ResolvedBy_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-214">ResolvedBy_s</span></span> | <span data-ttu-id="00e4d-215">Resolvido pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-215">Resolved by</span></span>|
| <span data-ttu-id="00e4d-216">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-216">ClosedBy_s</span></span>  | <span data-ttu-id="00e4d-217">Fechada pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-217">Closed by</span></span> |
| <span data-ttu-id="00e4d-218">Source_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-218">Source_s</span></span>| <span data-ttu-id="00e4d-219">Tipo de contacto</span><span class="sxs-lookup"><span data-stu-id="00e4d-219">Contact type</span></span> |
| <span data-ttu-id="00e4d-220">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-220">AssignedTo_s</span></span> | <span data-ttu-id="00e4d-221">Atribuído demasiado</span><span class="sxs-lookup"><span data-stu-id="00e4d-221">Assigned too</span></span> |
| <span data-ttu-id="00e4d-222">Category_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-222">Category_s</span></span> | <span data-ttu-id="00e4d-223">Categoria</span><span class="sxs-lookup"><span data-stu-id="00e4d-223">Category</span></span> |
| <span data-ttu-id="00e4d-224">Title_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-224">Title_s</span></span>|  <span data-ttu-id="00e4d-225">Breve descrição</span><span class="sxs-lookup"><span data-stu-id="00e4d-225">Short description</span></span> |
| <span data-ttu-id="00e4d-226">Description_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-226">Description_s</span></span>|  <span data-ttu-id="00e4d-227">Notas</span><span class="sxs-lookup"><span data-stu-id="00e4d-227">Notes</span></span> |
| <span data-ttu-id="00e4d-228">CreatedDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-228">CreatedDate_t</span></span>|  <span data-ttu-id="00e4d-229">Abrir</span><span class="sxs-lookup"><span data-stu-id="00e4d-229">Opened</span></span> |
| <span data-ttu-id="00e4d-230">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-230">ClosedDate_t</span></span>| <span data-ttu-id="00e4d-231">Fechado</span><span class="sxs-lookup"><span data-stu-id="00e4d-231">closed</span></span>|
| <span data-ttu-id="00e4d-232">ResolvedDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-232">ResolvedDate_t</span></span>|<span data-ttu-id="00e4d-233">Resolvido</span><span class="sxs-lookup"><span data-stu-id="00e4d-233">Resolved</span></span>|
| <span data-ttu-id="00e4d-234">Computador</span><span class="sxs-lookup"><span data-stu-id="00e4d-234">Computer</span></span>  | <span data-ttu-id="00e4d-235">item de configuração</span><span class="sxs-lookup"><span data-stu-id="00e4d-235">Configuration item</span></span> |

## <a name="output-data-for-a-servicenow-change-request"></a><span data-ttu-id="00e4d-236">Pedido de alteração de dados de saída para um ServiceNow</span><span class="sxs-lookup"><span data-stu-id="00e4d-236">Output data for a ServiceNow change request</span></span>

| <span data-ttu-id="00e4d-237">Campo do OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-237">OMS field</span></span> | <span data-ttu-id="00e4d-238">Campo ITSM</span><span class="sxs-lookup"><span data-stu-id="00e4d-238">ITSM field</span></span> |
|:--- |:--- |
| <span data-ttu-id="00e4d-239">ServiceDeskId_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-239">ServiceDeskId_s</span></span>| <span data-ttu-id="00e4d-240">Número</span><span class="sxs-lookup"><span data-stu-id="00e4d-240">Number</span></span> |
| <span data-ttu-id="00e4d-241">CreatedBy_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-241">CreatedBy_s</span></span> | <span data-ttu-id="00e4d-242">Pedido pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-242">Requested by</span></span> |
| <span data-ttu-id="00e4d-243">ClosedBy_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-243">ClosedBy_s</span></span> | <span data-ttu-id="00e4d-244">Fechada pelo</span><span class="sxs-lookup"><span data-stu-id="00e4d-244">Closed by</span></span> |
| <span data-ttu-id="00e4d-245">AssignedTo_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-245">AssignedTo_s</span></span> | <span data-ttu-id="00e4d-246">Atribuído demasiado</span><span class="sxs-lookup"><span data-stu-id="00e4d-246">Assigned too</span></span> |
| <span data-ttu-id="00e4d-247">Title_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-247">Title_s</span></span>|  <span data-ttu-id="00e4d-248">Breve descrição</span><span class="sxs-lookup"><span data-stu-id="00e4d-248">Short description</span></span> |
| <span data-ttu-id="00e4d-249">Type_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-249">Type_s</span></span>|  <span data-ttu-id="00e4d-250">Tipo</span><span class="sxs-lookup"><span data-stu-id="00e4d-250">Type</span></span> |
| <span data-ttu-id="00e4d-251">Category_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-251">Category_s</span></span>|  <span data-ttu-id="00e4d-252">Catgory</span><span class="sxs-lookup"><span data-stu-id="00e4d-252">Catgory</span></span> |
| <span data-ttu-id="00e4d-253">CRState_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-253">CRState_s</span></span>|  <span data-ttu-id="00e4d-254">Estado</span><span class="sxs-lookup"><span data-stu-id="00e4d-254">State</span></span>|
| <span data-ttu-id="00e4d-255">Urgency_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-255">Urgency_s</span></span>|  <span data-ttu-id="00e4d-256">Urgência</span><span class="sxs-lookup"><span data-stu-id="00e4d-256">Urgency</span></span> |
| <span data-ttu-id="00e4d-257">Priority_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-257">Priority_s</span></span>| <span data-ttu-id="00e4d-258">Prioridade</span><span class="sxs-lookup"><span data-stu-id="00e4d-258">Priority</span></span>|
| <span data-ttu-id="00e4d-259">Risk_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-259">Risk_s</span></span>| <span data-ttu-id="00e4d-260">Risco</span><span class="sxs-lookup"><span data-stu-id="00e4d-260">Risk</span></span>|
| <span data-ttu-id="00e4d-261">Impact_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-261">Impact_s</span></span>| <span data-ttu-id="00e4d-262">Impacto</span><span class="sxs-lookup"><span data-stu-id="00e4d-262">Impact</span></span>|
| <span data-ttu-id="00e4d-263">RequestedDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-263">RequestedDate_t</span></span>  | <span data-ttu-id="00e4d-264">Pedido por data</span><span class="sxs-lookup"><span data-stu-id="00e4d-264">Requested by date</span></span> |
| <span data-ttu-id="00e4d-265">ClosedDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-265">ClosedDate_t</span></span> | <span data-ttu-id="00e4d-266">Data de fecho</span><span class="sxs-lookup"><span data-stu-id="00e4d-266">Closed date</span></span> |
| <span data-ttu-id="00e4d-267">PlannedStartDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-267">PlannedStartDate_t</span></span>  |     <span data-ttu-id="00e4d-268">Data de início planeada</span><span class="sxs-lookup"><span data-stu-id="00e4d-268">Planned start date</span></span> |
| <span data-ttu-id="00e4d-269">PlannedEndDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-269">PlannedEndDate_t</span></span>  |   <span data-ttu-id="00e4d-270">Data de fim planeada</span><span class="sxs-lookup"><span data-stu-id="00e4d-270">Planned end date</span></span> |
| <span data-ttu-id="00e4d-271">WorkStartDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-271">WorkStartDate_t</span></span>  | <span data-ttu-id="00e4d-272">Data de início real</span><span class="sxs-lookup"><span data-stu-id="00e4d-272">Actual start date</span></span> |
| <span data-ttu-id="00e4d-273">WorkEndDate_t</span><span class="sxs-lookup"><span data-stu-id="00e4d-273">WorkEndDate_t</span></span> | <span data-ttu-id="00e4d-274">Data de fim real</span><span class="sxs-lookup"><span data-stu-id="00e4d-274">Actual end date</span></span>|
| <span data-ttu-id="00e4d-275">Description_s</span><span class="sxs-lookup"><span data-stu-id="00e4d-275">Description_s</span></span> | <span data-ttu-id="00e4d-276">Descrição</span><span class="sxs-lookup"><span data-stu-id="00e4d-276">Description</span></span> |
| <span data-ttu-id="00e4d-277">Computador</span><span class="sxs-lookup"><span data-stu-id="00e4d-277">Computer</span></span>  | <span data-ttu-id="00e4d-278">Item de configuração</span><span class="sxs-lookup"><span data-stu-id="00e4d-278">Configuration Item</span></span> |

<span data-ttu-id="00e4d-279">**Ecrã de análise de registos de exemplo para dados ITSM:**</span><span class="sxs-lookup"><span data-stu-id="00e4d-279">**Sample Log Analytics screen for ITSM data:**</span></span>

![Ecrã de análise do registo](./media/log-analytics-itsmc/itsmc-overview-sample-log-analytics.png)

## <a name="it-service-management-connector--integration-with-other-oms-solutions"></a><span data-ttu-id="00e4d-281">Conector de gestão do serviço IT – integração com outras soluções do OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-281">IT Service Management connector – integration with other OMS solutions</span></span>

<span data-ttu-id="00e4d-282">Conector de gestão do serviço IT, suporta atualmente a integração com Olá solução de mapa de serviço.</span><span class="sxs-lookup"><span data-stu-id="00e4d-282">IT Service Management Connector, currently supports integration with hello Service Map solution.</span></span>

<span data-ttu-id="00e4d-283">Mapa de serviço Deteta automaticamente Olá componentes da aplicação no Windows e comunicação entre os serviços de Olá sistemas Linux e mapas.</span><span class="sxs-lookup"><span data-stu-id="00e4d-283">Service Map automatically discovers hello application components on Windows and Linux systems and maps hello communication between services.</span></span> <span data-ttu-id="00e4d-284">Permite-lhe tooview seus servidores como considerá-los – como interligados sistemas que fornecem serviços críticos.</span><span class="sxs-lookup"><span data-stu-id="00e4d-284">It allows you tooview your servers as you think of them – as interconnected systems that deliver critical services.</span></span> <span data-ttu-id="00e4d-285">Mapa de serviço mostra as ligações entre servidores, processos, e portas em qualquer arquitetura TCP ligados sem qualquer configuração necessária à instalação de um agente.</span><span class="sxs-lookup"><span data-stu-id="00e4d-285">Service Map shows connections between servers, processes, and ports across any TCP-connected architecture with no configuration required other than installation of an agent.</span></span> <span data-ttu-id="00e4d-286">Obter mais informações: [mapa de serviço](../operations-management-suite/operations-management-suite-service-map.md).</span><span class="sxs-lookup"><span data-stu-id="00e4d-286">More information: [Service Map](../operations-management-suite/operations-management-suite-service-map.md).</span></span>

<span data-ttu-id="00e4d-287">Esta integração, pode ver itens de suporte técnico Olá serviço criados em soluções ITSM Olá, conforme mostrado no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="00e4d-287">With this integration, you can view hello service desk items created in hello ITSM solutions as shown in hello following example:</span></span>

![<span data-ttu-id="00e4d-288">Solução integrada</span><span class="sxs-lookup"><span data-stu-id="00e4d-288">Integrated solution</span></span> ](./media/log-analytics-itsmc/itsmc-overview-integrated-solutions.png)
## <a name="create-itsm-work-items-for-oms-alerts"></a><span data-ttu-id="00e4d-289">Criar itens de trabalho ITSM para alertas do OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-289">Create ITSM work items for OMS alerts</span></span>

<span data-ttu-id="00e4d-290">Existência de alertas do OMS Olá, pode criar itens de trabalho associados no Olá ligado ITSM origens.</span><span class="sxs-lookup"><span data-stu-id="00e4d-290">For hello OMS alerts, you can create associated work items in hello connected ITSM sources.</span></span>  <span data-ttu-id="00e4d-291">toodo Olá, utilize seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="00e4d-291">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="00e4d-292">De **pesquisa registo** janela, executar um registo de tooview de consulta de pesquisa de dados.</span><span class="sxs-lookup"><span data-stu-id="00e4d-292">From **Log Search** window, run a log search query tooview data.</span></span> <span data-ttu-id="00e4d-293">Os resultados da consulta são origem Olá para itens de trabalho.</span><span class="sxs-lookup"><span data-stu-id="00e4d-293">Query results are hello source for work items.</span></span>
2. <span data-ttu-id="00e4d-294">No **pesquisa registo**, clique em **alerta** tooopen Olá **Adicionar regra de alerta** página.</span><span class="sxs-lookup"><span data-stu-id="00e4d-294">In **Log Search**, click **Alert** tooopen hello **Add Alert Rule** page.</span></span>

    ![Ecrã de análise do registo](./media/log-analytics-itsmc/itsmc-work-items-for-oms-alerts.png)

3. <span data-ttu-id="00e4d-296">No Olá **Adicionar regra de alerta** janela, forneça detalhes Olá necessário para **nome**, **gravidade**, **consulta de pesquisa**, e  **Critérios de alerta** (medida janela/métrica de tempo).</span><span class="sxs-lookup"><span data-stu-id="00e4d-296">On hello **Add Alert Rule** window, provide hello required details for **Name**, **Severity**,  **Search query**, and **Alert criteria** (Time Window/Metric measurement).</span></span>
4. <span data-ttu-id="00e4d-297">Selecione **Sim** para **ITSM ações**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-297">Select **Yes** for **ITSM Actions**.</span></span>
5. <span data-ttu-id="00e4d-298">Selecione a ligação de ITSM Olá **selecione ligação** lista.</span><span class="sxs-lookup"><span data-stu-id="00e4d-298">Select your ITSM connection from hello **Select Connection** list.</span></span>
6. <span data-ttu-id="00e4d-299">Forneça detalhes Olá conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="00e4d-299">Provide hello details as required.</span></span>
7. <span data-ttu-id="00e4d-300">um item de trabalho separada para cada entrada de registo de Olá este alerta, selecione de toocreate **criar itens de trabalho individuais para cada entrada de registo** caixa de verificação.</span><span class="sxs-lookup"><span data-stu-id="00e4d-300">toocreate a separate work item for each log entry of this alert, select hello **Create individual work items for each log entry** checkbox.</span></span>

    <span data-ttu-id="00e4d-301">Ou</span><span class="sxs-lookup"><span data-stu-id="00e4d-301">Or</span></span>

    <span data-ttu-id="00e4d-302">Deixe este item de trabalho apenas uma caixa de verificação toocreate não seleccionado para qualquer número de entradas de registo neste alerta.</span><span class="sxs-lookup"><span data-stu-id="00e4d-302">leave this checkbox unselected toocreate only one work item for any number of log entries under this alert.</span></span>

7. <span data-ttu-id="00e4d-303">Clique em **Guardar**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-303">Click **Save**.</span></span>

<span data-ttu-id="00e4d-304">alerta OMS Olá será criada em **alertas**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-304">hello OMS alert will be created under **Alerts**.</span></span> <span data-ttu-id="00e4d-305">Olá trabalho da ligação ITSM correspondente itens são criados quando for cumprida a condição do alerta Olá especificado.</span><span class="sxs-lookup"><span data-stu-id="00e4d-305">hello corresponding ITSM connection's work items are created when hello specified alert's condition is met.</span></span>

## <a name="create-itsm-work-items-from-oms-logs"></a><span data-ttu-id="00e4d-306">Criar itens de trabalho ITSM a partir de registos do OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-306">Create ITSM work items from OMS logs</span></span>

<span data-ttu-id="00e4d-307">Pode criar itens de trabalho em origens de ITSM Olá ligado utilizando a pesquisa de registo do OMS.</span><span class="sxs-lookup"><span data-stu-id="00e4d-307">You can create work items in hello connected ITSM sources by using OMS Log Search.</span></span> <span data-ttu-id="00e4d-308">toodo Olá, utilize seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="00e4d-308">toodo this, use hello following procedure:</span></span>

1. <span data-ttu-id="00e4d-309">De **pesquisa registo**, procurar dados Olá necessário, selecione de detalhe de Olá e, em **Criar item de trabalho**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-309">From **Log Search**,  search hello required data, select hello detail, and click **Create work item**.</span></span>

    <span data-ttu-id="00e4d-310">Olá **item de trabalho de ITSM criar** surge a janela:</span><span class="sxs-lookup"><span data-stu-id="00e4d-310">hello **Create ITSM Work item** window appears:</span></span>

    ![Ecrã de análise do registo](media/log-analytics-itsmc/itsmc-work-items-from-oms-logs.png)

2.   <span data-ttu-id="00e4d-312">Adicione os detalhes de Olá:</span><span class="sxs-lookup"><span data-stu-id="00e4d-312">Add hello following details:</span></span>

  - <span data-ttu-id="00e4d-313">**Título do item de trabalho**: título para o item de trabalho de Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-313">**Work item Title**: Title for hello work item.</span></span>
  - <span data-ttu-id="00e4d-314">**Descrição do item de trabalho**: uma descrição para o novo item de trabalho Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-314">**Work item Description**: Description for hello new work item.</span></span>
  - <span data-ttu-id="00e4d-315">**Afetados computador**: nome do computador olá onde estes dados de registo foi encontrados.</span><span class="sxs-lookup"><span data-stu-id="00e4d-315">**Affected Computer**: Name of hello computer where this log data was found.</span></span>
  - <span data-ttu-id="00e4d-316">**Selecione a ligação**: ligação ITSM em que pretende toocreate este item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="00e4d-316">**Select Connection**:  ITSM connection in which you want toocreate this work item.</span></span>
  - <span data-ttu-id="00e4d-317">**Item de trabalho**: tipo de item de trabalho.</span><span class="sxs-lookup"><span data-stu-id="00e4d-317">**Work item**:  Type of work item.</span></span>

3. <span data-ttu-id="00e4d-318">toouse um modelo de item de trabalho existente para um incidente, clique em **Sim** em **gerar item de trabalho baseado num modelo de Olá** opção e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-318">toouse an existing work item template for an incident, click **Yes** under **Generate work item based on hello template** option and then click **Create**.</span></span>

    <span data-ttu-id="00e4d-319">Ou,</span><span class="sxs-lookup"><span data-stu-id="00e4d-319">Or,</span></span>

    <span data-ttu-id="00e4d-320">Clique em **não** se quiser tooprovide os valores personalizados.</span><span class="sxs-lookup"><span data-stu-id="00e4d-320">Click **No** if you want tooprovide your customized values.</span></span>

4. <span data-ttu-id="00e4d-321">Forneça os valores corretos Olá no Olá **contacte tipo**, **impacto**, **urgência**, **categoria**, e **Sub categoria**  caixas de texto e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="00e4d-321">Provide hello appropriate values in hello **Contact Type**, **Impact**, **Urgency**, **Category**, and **Sub Category** text boxes, and then click **Create**.</span></span>

<span data-ttu-id="00e4d-322">item de trabalho de Olá será criado na Olá ITSM, que também pode ver no OMS.</span><span class="sxs-lookup"><span data-stu-id="00e4d-322">hello work item will be created in hello ITSM, which you can also view in OMS.</span></span>

## <a name="troubleshoot-itsm-connections-in-oms"></a><span data-ttu-id="00e4d-323">Resolver problemas de ligações de ITSM no OMS</span><span class="sxs-lookup"><span data-stu-id="00e4d-323">Troubleshoot ITSM connections in OMS</span></span>
1.  <span data-ttu-id="00e4d-324">Se a ligação falha a partir IU da origem ligados e obter Olá **erro na ligação de guardar** da mensagem, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="00e4d-324">If connection fails from connected source's UI and you get hello **Error in saving connection** message, do hello following:</span></span>
 - <span data-ttu-id="00e4d-325">Em caso de ligações de ServiceNow, Cherwell e Provance, certifique-se a segredo de ID/cliente do nome de utilizador/palavra-passe e o cliente Olá introduzido corretamente para cada uma das ligações de Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-325">In case of ServiceNow, Cherwell and Provance connections, ensure you correctly entered  hello username/password and  client ID/client secret  for each of hello connections.</span></span> <span data-ttu-id="00e4d-326">Se Olá erro persistir, verifique se tem privilégios suficientes no Olá correspondente ITSM produto toomake Olá ligação.</span><span class="sxs-lookup"><span data-stu-id="00e4d-326">If hello error persists, check if you have sufficient privileges  in hello corresponding ITSM product toomake hello connection.</span></span>
 - <span data-ttu-id="00e4d-327">No caso do Service Manager, certifique-se de que Olá Web aplicação for implementada com êxito e é criada a ligação híbrida.</span><span class="sxs-lookup"><span data-stu-id="00e4d-327">In case of Service Manager, ensure that hello Web app is successfully deployed and hybrid connection is created.</span></span> <span data-ttu-id="00e4d-328">tooverify Olá é estabelecida ligação com êxito máquina do Olá no local do Service Manager, visite o URL da aplicação Web Olá conforme especificado na documentação de Olá para efetuar Olá [da ligação híbrida](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span><span class="sxs-lookup"><span data-stu-id="00e4d-328">tooverify hello connection is successfully established with hello on-prem Service Manager machine, visit hello  Web app URL as detailed in hello documentation for making hello [hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection).</span></span>

2.  <span data-ttu-id="00e4d-329">Se os dados a partir do ServiceNow não está a obter sincronizados na OMS, certifique-se de que essa instância do ServiceNow Olá não está suspenso.</span><span class="sxs-lookup"><span data-stu-id="00e4d-329">If data from ServiceNow is not getting synced in OMS, ensure that hello ServiceNow instance is not sleeping.</span></span> <span data-ttu-id="00e4d-330">Isto poderá membros acontecer algum tempo no Olá instâncias de desenvolvimento do ServiceNow, se inativo.</span><span class="sxs-lookup"><span data-stu-id="00e4d-330">This might sometime happen in hello ServiceNow Dev instances, when idle.</span></span> <span data-ttu-id="00e4d-331">Outra forma, problema de Olá de relatório.</span><span class="sxs-lookup"><span data-stu-id="00e4d-331">Else, report hello issue.</span></span>
3.  <span data-ttu-id="00e4d-332">Se os alertas são a obter desencadeados da OMS, mas os itens de trabalho não estão a obter criados no produto ITSM ou itens de configuração não estiver a obter itens de toowork criado/ligado ou para quaisquer informações genéricos, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="00e4d-332">If Alerts are getting fired from OMS but work items are not getting created in ITSM product or configuration items are not getting created/linked toowork items or for any generic information, do hello following:</span></span>
 -  <span data-ttu-id="00e4d-333">Solução do conector de gestão do serviço IT no portal do OMS pode ser utilizado tooget um resumo ligações/computador de trabalho itens/etc. Clique em mensagens de erro Olá no painel de estado de Olá, navegue demasiado**pesquisa de registo** e ver a ligação de Olá com erro de Olá utilizando detalhes da Olá na mensagem de erro de saudação.</span><span class="sxs-lookup"><span data-stu-id="00e4d-333">IT Service Management Connector solution in OMS portal could be used tooget a summary of connections/work items/computers etc. Click hello error message in hello status blade, navigate too**Log Search** and view hello connection that has hello error by using hello details in hello error message.</span></span>
 - <span data-ttu-id="00e4d-334">diretamente pode ver informações de erros/relacionados Olá no Olá **pesquisa registo** página com *tipo = ServiceDeskLog_CL*.</span><span class="sxs-lookup"><span data-stu-id="00e4d-334">you can directly view hello errors/related information in hello **Log Search** page using *Type=ServiceDeskLog_CL*.</span></span>

## <a name="troubleshoot-service-manager-web-app-deployment"></a><span data-ttu-id="00e4d-335">Resolver problemas de implementação de aplicação de Web do Service Manager</span><span class="sxs-lookup"><span data-stu-id="00e4d-335">Troubleshoot Service Manager Web App deployment</span></span>
1.  <span data-ttu-id="00e4d-336">Em caso de problemas para implementação de aplicações web, certifique-se de que tem permissões suficientes na subscrição Olá mencionado toocreate/implementar recursos.</span><span class="sxs-lookup"><span data-stu-id="00e4d-336">In case of any trouble with web app deployment, ensure you have sufficient permissions in hello subscription mentioned toocreate/deploy resources.</span></span>
2.  <span data-ttu-id="00e4d-337">Se **referência de objeto não definida tooinstance de um objeto** é apresentada a mensagem de erro durante a execução Olá [script](log-analytics-itsmc-service-manager-script.md) Certifique-se de que introduziu valores válidos em **configuração do utilizador**secção.</span><span class="sxs-lookup"><span data-stu-id="00e4d-337">If **Object reference not set tooinstance of an object** error message appears while running hello [script](log-analytics-itsmc-service-manager-script.md) ensure that you entered valid values  under **User Configuration** section.</span></span>
3.  <span data-ttu-id="00e4d-338">Se falhar o espaço de nomes do toocreate service bus reencaminhamento, certifique-se de que Olá necessário fornecedor de recursos está registado na subscrição Olá.</span><span class="sxs-lookup"><span data-stu-id="00e4d-338">If you fail toocreate service bus relay namespace, ensure that hello required resource provider is registered in hello subscription.</span></span> <span data-ttu-id="00e4d-339">Se não registado manualmente criá-la de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00e4d-339">If not registered, manually create it from hello Azure portal.</span></span> <span data-ttu-id="00e4d-340">Também pode criá-la ao [criação da ligação híbrida Olá](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="00e4d-340">You can also create it while [creating hello hybrid connection](log-analytics-itsmc-connections.md#configure-the-hybrid-connection) from hello Azure portal.</span></span>


## <a name="contact-us"></a><span data-ttu-id="00e4d-341">Contacte-nos</span><span class="sxs-lookup"><span data-stu-id="00e4d-341">Contact us</span></span>

<span data-ttu-id="00e4d-342">Para consultas ou comentários sobre Olá conector de gestão de serviços de TI, contacte-nos [ omsitsmfeedback@microsoft.com ](mailto:omsitsmfeedback@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="00e4d-342">For any queries or feedback on hello IT Service Management Connector, contact us at [omsitsmfeedback@microsoft.com](mailto:omsitsmfeedback@microsoft.com).</span></span>

## <a name="next-steps"></a><span data-ttu-id="00e4d-343">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="00e4d-343">Next steps</span></span>
<span data-ttu-id="00e4d-344">[Adicionar ITSM produtos/serviços tooIT conector do serviço de gestão](log-analytics-itsmc-connections.md).</span><span class="sxs-lookup"><span data-stu-id="00e4d-344">[Add ITSM products/services tooIT Service Management Connector](log-analytics-itsmc-connections.md).</span></span>
