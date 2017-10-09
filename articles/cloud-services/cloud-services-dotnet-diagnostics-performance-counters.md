---
title: "aaaUse os contadores de desempenho do diagnóstico do Azure | Microsoft Docs"
description: "Utilize os contadores de desempenho cloud services do Azure ou a máquina virtual toofind constrangimentos e otimizar o desempenho."
services: cloud-services
documentationcenter: .net
author: rboucher
manager: jwhit
editor: tysonn
ms.assetid: fc4c61e9-d49d-4ed9-a32c-b91cdf851909
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/29/2016
ms.author: robb
ms.openlocfilehash: f3250816c01fc6e164a6aae48da5035845e6d2b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-use-performance-counters-in-an-azure-application"></a><span data-ttu-id="870b4-103">Criar e utilizar os contadores de desempenho na aplicação do Azure</span><span class="sxs-lookup"><span data-stu-id="870b4-103">Create and use performance counters in an Azure application</span></span>
<span data-ttu-id="870b4-104">Este artigo descreve os benefícios de Olá do e como contadores de desempenho do tooput na sua aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-104">This article describes hello benefits of and how tooput performance counters into your Azure application.</span></span> <span data-ttu-id="870b4-105">Pode utilizá-los toocollect dados, localizar congestionamentos e otimizar o desempenho do sistema e de aplicações.</span><span class="sxs-lookup"><span data-stu-id="870b4-105">You can use them toocollect data, find bottlenecks, and tune system and application performance.</span></span>

<span data-ttu-id="870b4-106">Contadores de desempenho disponíveis para o Windows Server, IIS e ASP.NET também podem ser recolhidos e utilizado o estado de funcionamento do toodetermine Olá das suas funções da web do Azure, as funções de trabalho e máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="870b4-106">Performance counters available for Windows Server, IIS, and ASP.NET can also be collected and used toodetermine hello health of your Azure web roles, worker roles, and Virtual Machines.</span></span> <span data-ttu-id="870b4-107">Também pode criar e utilizar os contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="870b4-107">You can also create and use custom performance counters.</span></span>  

<span data-ttu-id="870b4-108">Pode examinar os dados de contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="870b4-108">You can examine performance counter data</span></span>

1. <span data-ttu-id="870b4-109">Diretamente no anfitrião da aplicação Olá com a ferramenta de Monitor de desempenho de Olá acedida através de ambiente de trabalho remoto</span><span class="sxs-lookup"><span data-stu-id="870b4-109">Directly on hello application host with hello Performance Monitor tool accessed using Remote Desktop</span></span>
2. <span data-ttu-id="870b4-110">Utilizar o System Center Operations Manager Olá pacote de gestão do Azure</span><span class="sxs-lookup"><span data-stu-id="870b4-110">With System Center Operations Manager using hello Azure Management Pack</span></span>
3. <span data-ttu-id="870b4-111">Com outras ferramentas de monitorização que acedem ao hello dados de diagnóstico transferidos tooAzure armazenamento.</span><span class="sxs-lookup"><span data-stu-id="870b4-111">With other monitoring tools that access hello diagnostic data transferred tooAzure storage.</span></span> <span data-ttu-id="870b4-112">Consulte [loja e ver os dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="870b4-112">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for more information.</span></span>  

<span data-ttu-id="870b4-113">Para obter mais informações sobre como monitorizar o desempenho de Olá da sua aplicação no Olá [portal do Azure](http://portal.azure.com/), consulte [como tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span><span class="sxs-lookup"><span data-stu-id="870b4-113">For more information on monitoring hello performance of your application in hello [Azure portal](http://portal.azure.com/), see [How tooMonitor Cloud Services](https://www.azure.com/manage/services/cloud-services/how-to-monitor-a-cloud-service/).</span></span>

<span data-ttu-id="870b4-114">Para obter orientações aprofundadas adicionais sobre como criar um registo e rastreio estratégia e utilizando os diagnósticos e outros problemas de tootroubleshoot técnicas e otimizar aplicações do Azure, consulte [resolução de problemas de melhores práticas para desenvolvimento do Azure Aplicações](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="870b4-114">For additional in-depth guidance on creating a logging and tracing strategy and using diagnostics and other techniques tootroubleshoot problems and optimize Azure applications, see [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/azure/hh771389.aspx).</span></span>

## <a name="enable-performance-counter-monitoring"></a><span data-ttu-id="870b4-115">Ativar a monitorização do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="870b4-115">Enable performance counter monitoring</span></span>
<span data-ttu-id="870b4-116">Contadores de desempenho não estão ativados por predefinição.</span><span class="sxs-lookup"><span data-stu-id="870b4-116">Performance counters are not enabled by default.</span></span> <span data-ttu-id="870b4-117">A aplicação ou uma tarefa de arranque tem de modificar o diagnóstico de predefinição Olá contadores de desempenho de específica de Olá de tooinclude de configuração de agente que pretende toomonitor para cada instância de função.</span><span class="sxs-lookup"><span data-stu-id="870b4-117">Your application or a startup task must modify hello default diagnostics agent configuration tooinclude hello specific performance counters that you wish toomonitor for each role instance.</span></span>

### <a name="performance-counters-available-for-microsoft-azure"></a><span data-ttu-id="870b4-118">Contadores de desempenho disponíveis para o Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="870b4-118">Performance counters available for Microsoft Azure</span></span>
<span data-ttu-id="870b4-119">O Azure oferece um subconjunto dos contadores de desempenho de Olá disponíveis para Windows Server, IIS e Olá pilha do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="870b4-119">Azure provides a subset of hello performance counters available for Windows Server, IIS and hello ASP.NET stack.</span></span> <span data-ttu-id="870b4-120">Olá tabela seguinte lista algumas Olá contadores de desempenho do especial interesse para aplicações do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-120">hello following table lists some of hello performance counters of particular interest for Azure applications.</span></span>

| <span data-ttu-id="870b4-121">Categoria do contador: Objeto (instância)</span><span class="sxs-lookup"><span data-stu-id="870b4-121">Counter Category: Object (Instance)</span></span> | <span data-ttu-id="870b4-122">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="870b4-122">Counter Name</span></span> | <span data-ttu-id="870b4-123">Referência</span><span class="sxs-lookup"><span data-stu-id="870b4-123">Reference</span></span> |
| --- | --- | --- |
| <span data-ttu-id="870b4-124">Exceções de CLR de .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="870b4-124">.NET CLR Exceptions(*Global*)</span></span> |<span data-ttu-id="870b4-125"># Exceções iniciadas / seg</span><span class="sxs-lookup"><span data-stu-id="870b4-125"># Exceps Thrown / sec</span></span> |<span data-ttu-id="870b4-126">Contadores de desempenho de exceção</span><span class="sxs-lookup"><span data-stu-id="870b4-126">Exception Performance Counters</span></span> |
| <span data-ttu-id="870b4-127">Memória CLR de .NET (*Global*)</span><span class="sxs-lookup"><span data-stu-id="870b4-127">.NET CLR Memory(*Global*)</span></span> |<span data-ttu-id="870b4-128">% De tempo na GC</span><span class="sxs-lookup"><span data-stu-id="870b4-128">% Time in GC</span></span> |<span data-ttu-id="870b4-129">Contadores de desempenho de memória</span><span class="sxs-lookup"><span data-stu-id="870b4-129">Memory Performance Counters</span></span> |
| <span data-ttu-id="870b4-130">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-130">ASP.NET</span></span> |<span data-ttu-id="870b4-131">Reinício da aplicação</span><span class="sxs-lookup"><span data-stu-id="870b4-131">Application Restarts</span></span> |<span data-ttu-id="870b4-132">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-132">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-133">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-133">ASP.NET</span></span> |<span data-ttu-id="870b4-134">Tempo de execução do pedido</span><span class="sxs-lookup"><span data-stu-id="870b4-134">Request Execution Time</span></span> |<span data-ttu-id="870b4-135">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-135">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-136">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-136">ASP.NET</span></span> |<span data-ttu-id="870b4-137">Pedidos desligados</span><span class="sxs-lookup"><span data-stu-id="870b4-137">Requests Disconnected</span></span> |<span data-ttu-id="870b4-138">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-138">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-139">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-139">ASP.NET</span></span> |<span data-ttu-id="870b4-140">Reinício do processo de trabalho</span><span class="sxs-lookup"><span data-stu-id="870b4-140">Worker Process Restarts</span></span> |<span data-ttu-id="870b4-141">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-141">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-142">Aplicações do ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="870b4-142">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="870b4-143">Total de pedidos</span><span class="sxs-lookup"><span data-stu-id="870b4-143">Requests Total</span></span> |<span data-ttu-id="870b4-144">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-144">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-145">Aplicações do ASP.NET (**Total**)</span><span class="sxs-lookup"><span data-stu-id="870b4-145">ASP.NET Applications(**Total**)</span></span> |<span data-ttu-id="870b4-146">Pedidos/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-146">Requests/Sec</span></span> |<span data-ttu-id="870b4-147">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-147">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-148">ASP.NET v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="870b4-148">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="870b4-149">Tempo de execução do pedido</span><span class="sxs-lookup"><span data-stu-id="870b4-149">Request Execution Time</span></span> |<span data-ttu-id="870b4-150">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-150">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-151">ASP.NET v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="870b4-151">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="870b4-152">Tempo de espera do pedido</span><span class="sxs-lookup"><span data-stu-id="870b4-152">Request Wait Time</span></span> |<span data-ttu-id="870b4-153">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-153">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-154">ASP.NET v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="870b4-154">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="870b4-155">Pedidos atuais</span><span class="sxs-lookup"><span data-stu-id="870b4-155">Requests Current</span></span> |<span data-ttu-id="870b4-156">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-156">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-157">ASP.NET v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="870b4-157">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="870b4-158">Pedidos colocados em fila</span><span class="sxs-lookup"><span data-stu-id="870b4-158">Requests Queued</span></span> |<span data-ttu-id="870b4-159">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-159">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-160">ASP.NET v 4.0.30319</span><span class="sxs-lookup"><span data-stu-id="870b4-160">ASP.NET v4.0.30319</span></span> |<span data-ttu-id="870b4-161">Pedidos rejeitados</span><span class="sxs-lookup"><span data-stu-id="870b4-161">Requests Rejected</span></span> |<span data-ttu-id="870b4-162">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-162">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-163">Memória</span><span class="sxs-lookup"><span data-stu-id="870b4-163">Memory</span></span> |<span data-ttu-id="870b4-164">MBytes disponíveis</span><span class="sxs-lookup"><span data-stu-id="870b4-164">Available MBytes</span></span> |<span data-ttu-id="870b4-165">Contadores de desempenho de memória</span><span class="sxs-lookup"><span data-stu-id="870b4-165">Memory Performance Counters</span></span> |
| <span data-ttu-id="870b4-166">Memória</span><span class="sxs-lookup"><span data-stu-id="870b4-166">Memory</span></span> |<span data-ttu-id="870b4-167">Bytes consolidadas</span><span class="sxs-lookup"><span data-stu-id="870b4-167">Committed Bytes</span></span> |<span data-ttu-id="870b4-168">Contadores de desempenho de memória</span><span class="sxs-lookup"><span data-stu-id="870b4-168">Memory Performance Counters</span></span> |
| <span data-ttu-id="870b4-169">Processor(_Total)</span><span class="sxs-lookup"><span data-stu-id="870b4-169">Processor(_Total)</span></span> |<span data-ttu-id="870b4-170">% Tempo do processador</span><span class="sxs-lookup"><span data-stu-id="870b4-170">% Processor Time</span></span> |<span data-ttu-id="870b4-171">Contadores de desempenho para o ASP.NET</span><span class="sxs-lookup"><span data-stu-id="870b4-171">Performance Counters for ASP.NET</span></span> |
| <span data-ttu-id="870b4-172">TCPv4</span><span class="sxs-lookup"><span data-stu-id="870b4-172">TCPv4</span></span> |<span data-ttu-id="870b4-173">Falhas de ligação</span><span class="sxs-lookup"><span data-stu-id="870b4-173">Connection Failures</span></span> |<span data-ttu-id="870b4-174">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="870b4-174">TCP Object</span></span> |
| <span data-ttu-id="870b4-175">TCPv4</span><span class="sxs-lookup"><span data-stu-id="870b4-175">TCPv4</span></span> |<span data-ttu-id="870b4-176">Ligações estabelecidas</span><span class="sxs-lookup"><span data-stu-id="870b4-176">Connections Established</span></span> |<span data-ttu-id="870b4-177">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="870b4-177">TCP Object</span></span> |
| <span data-ttu-id="870b4-178">TCPv4</span><span class="sxs-lookup"><span data-stu-id="870b4-178">TCPv4</span></span> |<span data-ttu-id="870b4-179">Reposição de ligações</span><span class="sxs-lookup"><span data-stu-id="870b4-179">Connections Reset</span></span> |<span data-ttu-id="870b4-180">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="870b4-180">TCP Object</span></span> |
| <span data-ttu-id="870b4-181">TCPv4</span><span class="sxs-lookup"><span data-stu-id="870b4-181">TCPv4</span></span> |<span data-ttu-id="870b4-182">Segmentos enviados/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-182">Segments Sent/sec</span></span> |<span data-ttu-id="870b4-183">Objeto TCP</span><span class="sxs-lookup"><span data-stu-id="870b4-183">TCP Object</span></span> |
| <span data-ttu-id="870b4-184">Interface(*) de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-184">Network Interface(*)</span></span> |<span data-ttu-id="870b4-185">Bytes recebidos/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-185">Bytes Received/sec</span></span> |<span data-ttu-id="870b4-186">Objeto de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-186">Network Interface Object</span></span> |
| <span data-ttu-id="870b4-187">Interface(*) de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-187">Network Interface(*)</span></span> |<span data-ttu-id="870b4-188">Bytes enviados/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-188">Bytes Sent/sec</span></span> |<span data-ttu-id="870b4-189">Objeto de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-189">Network Interface Object</span></span> |
| <span data-ttu-id="870b4-190">Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="870b4-190">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="870b4-191">Bytes recebidos/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-191">Bytes Received/sec</span></span> |<span data-ttu-id="870b4-192">Objeto de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-192">Network Interface Object</span></span> |
| <span data-ttu-id="870b4-193">Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="870b4-193">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="870b4-194">Bytes enviados/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-194">Bytes Sent/sec</span></span> |<span data-ttu-id="870b4-195">Objeto de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-195">Network Interface Object</span></span> |
| <span data-ttu-id="870b4-196">Interface de rede (_2 de adaptador de rede de barramento de Máquina Virtual da Microsoft)</span><span class="sxs-lookup"><span data-stu-id="870b4-196">Network Interface(Microsoft Virtual Machine Bus Network Adapter _2)</span></span> |<span data-ttu-id="870b4-197">Bytes totais/seg</span><span class="sxs-lookup"><span data-stu-id="870b4-197">Bytes Total/sec</span></span> |<span data-ttu-id="870b4-198">Objeto de Interface de rede</span><span class="sxs-lookup"><span data-stu-id="870b4-198">Network Interface Object</span></span> |

## <a name="create-and-add-custom-performance-counters-tooyour-application"></a><span data-ttu-id="870b4-199">Criar e adicionar a aplicação de tooyour de contadores de desempenho personalizado</span><span class="sxs-lookup"><span data-stu-id="870b4-199">Create and add custom performance counters tooyour application</span></span>
<span data-ttu-id="870b4-200">O Azure tem suporte toocreate e modificar os contadores de desempenho personalizado para funções da web e funções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="870b4-200">Azure has support toocreate and modify custom performance counters for web roles and worker roles.</span></span> <span data-ttu-id="870b4-201">contadores de Olá podem ser utilizado comportamento tootrack e monitor e específicas da aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-201">hello counters may be used tootrack and monitor application-specific behavior.</span></span> <span data-ttu-id="870b4-202">Pode criar e eliminar categorias de contador de desempenho personalizados e os especificadores de uma tarefa de arranque, a função da web ou a função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="870b4-202">You can create and delete custom performance counter categories and specifiers from a startup task, web role, or worker role with elevated permissions.</span></span>

> [!NOTE]
> <span data-ttu-id="870b4-203">Código que faz alterações toocustom contadores de desempenho tem de ter elevados toorun de permissões.</span><span class="sxs-lookup"><span data-stu-id="870b4-203">Code that makes changes toocustom performance counters must have elevated permissions toorun.</span></span> <span data-ttu-id="870b4-204">Se Olá código numa função da web ou função de trabalho, a função de Olá tem de incluir tag Olá <Runtime executionContext="elevated" /> nos Olá servicedefinition. Csdef de ficheiros para Olá função tooinitialize corretamente.</span><span class="sxs-lookup"><span data-stu-id="870b4-204">If hello code is in a web role or worker role, hello role must include hello tag <Runtime executionContext="elevated" /> in hello ServiceDefinition.csdef file for hello role tooinitialize properly.</span></span>
>
>

<span data-ttu-id="870b4-205">Pode enviar desempenho personalizado contador tooAzure o armazenamento de dados com o agente de diagnóstico de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-205">You can send custom performance counter data tooAzure storage using hello diagnostics agent.</span></span>

<span data-ttu-id="870b4-206">dados de contador de desempenho padrão de Olá são gerados pelo Olá que processa do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-206">hello standard performance counter data is generated by hello Azure processes.</span></span> <span data-ttu-id="870b4-207">Dados de contador de desempenho personalizado tem de ser criados pela sua aplicação de função web ou função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="870b4-207">Custom performance counter data must be created by your web role or worker role application.</span></span> <span data-ttu-id="870b4-208">Consulte [tipos de contador de desempenho](https://msdn.microsoft.com/library/z573042h.aspx) para obter informações sobre tipos de Olá de dados que podem ser armazenados nos contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="870b4-208">See [Performance Counter Types](https://msdn.microsoft.com/library/z573042h.aspx) for information on hello types of data that can be stored in custom performance counters.</span></span> <span data-ttu-id="870b4-209">Consulte [PerformanceCounters exemplo](http://code.msdn.microsoft.com/azure/) para obter um exemplo que cria e define os dados do contador de desempenho personalizados numa função da web.</span><span class="sxs-lookup"><span data-stu-id="870b4-209">See [PerformanceCounters Sample](http://code.msdn.microsoft.com/azure/) for an example that creates and sets custom performance counter data in a web role.</span></span>

## <a name="store-and-view-performance-counter-data"></a><span data-ttu-id="870b4-210">Arquivo e a vista de dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="870b4-210">Store and view performance counter data</span></span>
<span data-ttu-id="870b4-211">Azure coloca em cache os dados de contador de desempenho com outras informações de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="870b4-211">Azure caches performance counter data with other diagnostic information.</span></span> <span data-ttu-id="870b4-212">Estes dados estão disponíveis para monitorização remota durante a execução da instância de função Olá utilizando as ferramentas de tooview de acesso de ambiente de trabalho remoto, tais como o Monitor de desempenho.</span><span class="sxs-lookup"><span data-stu-id="870b4-212">This data is available for remote monitoring while hello role instance is running using remote desktop access tooview tools such as Performance Monitor.</span></span> <span data-ttu-id="870b4-213">toopersist Olá fora da instância de função Olá, agente de diagnóstico de Olá tem transferência de dados de armazenamento de tooAzure Olá dados.</span><span class="sxs-lookup"><span data-stu-id="870b4-213">toopersist hello data outside of hello role instance, hello diagnostics agent must transfer hello data tooAzure storage.</span></span> <span data-ttu-id="870b4-214">limite de tamanho de Olá de dados do contador de desempenho de Olá em cache pode ser configurado no agente de diagnóstico hello, ou pode ser configurado toobe parte de um limite partilhado para Olá todos os dados de diagnóstico.</span><span class="sxs-lookup"><span data-stu-id="870b4-214">hello size limit of hello cached performance counter data can be configured in hello diagnostics agent, or it may be configured toobe part of a shared limit for all hello diagnostic data.</span></span> <span data-ttu-id="870b4-215">Para obter mais informações sobre como definir o tamanho da memória intermédia de Olá, consulte [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) e [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span><span class="sxs-lookup"><span data-stu-id="870b4-215">For more information about setting hello buffer size, see [OverallQuotaInMB](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.diagnosticmonitorconfiguration.overallquotainmb.aspx) and [DirectoriesBufferConfiguration](https://msdn.microsoft.com/library/azure/microsoft.windowsazure.diagnostics.directoriesbufferconfiguration.aspx).</span></span> <span data-ttu-id="870b4-216">Consulte [loja e ver os dados de diagnóstico no armazenamento do Azure](https://msdn.microsoft.com/library/azure/hh411534.aspx) para uma descrição geral de como configurar Olá diagnóstico agente tootransfer dados tooa conta do storage.</span><span class="sxs-lookup"><span data-stu-id="870b4-216">See [Store and View Diagnostic Data in Azure Storage](https://msdn.microsoft.com/library/azure/hh411534.aspx) for an overview of setting up hello diagnostics agent tootransfer data tooa storage account.</span></span>

<span data-ttu-id="870b4-217">Cada instância do contador de desempenho configurados é registada uma taxa de amostragem especificado e são transferidos dados Olá amostragem toohello de conta do storage por um pedido de transferência agendada ou um pedido de transferência a pedido.</span><span class="sxs-lookup"><span data-stu-id="870b4-217">Each configured performance counter instance is recorded at a specified sampling rate, and hello sampled data is transferred toohello storage account either by a scheduled transfer request or an on-demand transfer request.</span></span> <span data-ttu-id="870b4-218">Transferências automáticas podem ser agendadas no máximo, uma vez por minuto.</span><span class="sxs-lookup"><span data-stu-id="870b4-218">Automatic transfers may be scheduled as often as once per minute.</span></span> <span data-ttu-id="870b4-219">Dados de contador de desempenho transferidos pelo agente de diagnóstico de Olá são armazenados numa tabela, WADPerformanceCountersTable, na conta do storage Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-219">Performance counter data transferred by hello diagnostics agent is stored in a table, WADPerformanceCountersTable, in hello storage account.</span></span> <span data-ttu-id="870b4-220">Esta tabela pode ser acedida e consultar com métodos de armazenamento do Azure standard API.</span><span class="sxs-lookup"><span data-stu-id="870b4-220">This table may be accessed and queried with standard Azure storage API methods.</span></span> <span data-ttu-id="870b4-221">Consulte [exemplo do Microsoft Azure PerformanceCounters](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) para obter um exemplo de consulta e apresentar dados de contador de desempenho da tabela de WADPerformanceCountersTable Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-221">See [Microsoft Azure PerformanceCounters Sample](http://code.msdn.microsoft.com/Windows-Azure-PerformanceCo-7d80ebf9) for an example of querying and displaying performance counter data from hello WADPerformanceCountersTable table.</span></span>

> [!NOTE]
> <span data-ttu-id="870b4-222">Consoante a frequência de transferência de agente de diagnóstico Olá e a latência de fila, hello mais recentes dados de contador de desempenho na conta do storage Olá poderá vários minutos desatualizada.</span><span class="sxs-lookup"><span data-stu-id="870b4-222">Depending on hello diagnostics agent transfer frequency and queue latency, hello most recent performance counter data in hello storage account may be several minutes out of date.</span></span>
>
>

## <a name="enable-performance-counters-using-diagnostics-configuration-file"></a><span data-ttu-id="870b4-223">Ativar os contadores de desempenho com o ficheiro de configuração de diagnóstico</span><span class="sxs-lookup"><span data-stu-id="870b4-223">Enable performance counters using diagnostics configuration file</span></span>
<span data-ttu-id="870b4-224">Utilize Olá seguir o procedimento tooenable os contadores de desempenho da aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-224">Use hello following procedure tooenable performance counters in your Azure application.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="870b4-225">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="870b4-225">Prerequisites</span></span>
<span data-ttu-id="870b4-226">Esta secção assume que importou o monitor de diagnóstico de Olá na sua aplicação e adicionados Olá diagnóstico configuração ficheiro tooyour solução do Visual Studio (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima).</span><span class="sxs-lookup"><span data-stu-id="870b4-226">This section assumes that you have imported hello Diagnostics monitor into your application and added hello diagnostics configuration file tooyour Visual Studio solution (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above).</span></span> <span data-ttu-id="870b4-227">Consulte os passos 1 e 2 no [ativar diagnósticos no Cloud Services do Azure e máquinas virtuais](cloud-services-dotnet-diagnostics.md)) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="870b4-227">See steps 1 and 2 in [Enabling Diagnostics in Azure Cloud Services and Virtual Machines](cloud-services-dotnet-diagnostics.md)) for more information.</span></span>

## <a name="step-1-collect-and-store-data-from-performance-counters"></a><span data-ttu-id="870b4-228">Passo 1: Recolher e armazenar dados de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="870b4-228">Step 1: Collect and store data from performance counters</span></span>
<span data-ttu-id="870b4-229">Depois de ter adicionado Olá diagnóstico ficheiro tooyour solução do Visual Studio, pode configurar o armazenamento de dados do contador de desempenho e a recolha de Olá numa aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-229">After you have added hello diagnostics file tooyour Visual Studio solution, you can configure hello collection and storage of performance counter data in an Azure application.</span></span> <span data-ttu-id="870b4-230">Isto é feito ao adicionar ficheiros de diagnóstico de toohello de contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="870b4-230">This is done by adding performance counters toohello diagnostics file.</span></span> <span data-ttu-id="870b4-231">Dados de diagnóstico, incluindo os contadores de desempenho, primeiro são recolhidos na instância de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-231">Diagnostics data, including performance counters, is first collected on hello instance.</span></span> <span data-ttu-id="870b4-232">dados de Olá, em seguida, toohello persistente WADPerformanceCountersTable tabela no Olá serviço tabela do Azure, pelo que irá também precisar toospecify Olá conta de armazenamento na sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-232">hello data is then persisted toohello WADPerformanceCountersTable table in hello Azure Table service, so you will also need toospecify hello storage account in your application.</span></span> <span data-ttu-id="870b4-233">Se estiver a testar a aplicação localmente no Olá emulador de computação, pode também armazenar dados de diagnóstico localmente no Olá emulador do Storage.</span><span class="sxs-lookup"><span data-stu-id="870b4-233">If you're testing your application locally in hello Compute Emulator, you can also store diagnostics data locally in hello Storage Emulator.</span></span> <span data-ttu-id="870b4-234">Antes de o armazenar dados de diagnóstico, primeiro tem de ir toohello [portal do Azure](http://portal.azure.com/) e crie uma conta de armazenamento clássico.</span><span class="sxs-lookup"><span data-stu-id="870b4-234">Before you store diagnostics data, you must first go toohello [Azure portal](http://portal.azure.com/) and create a classic storage account.</span></span> <span data-ttu-id="870b4-235">Uma melhor prática é toolocate na sua conta do storage Olá geolocalização mesma que a aplicação do Azure.</span><span class="sxs-lookup"><span data-stu-id="870b4-235">A best practice is toolocate your storage account in hello same geo-location as your Azure application.</span></span> <span data-ttu-id="870b4-236">Ao manter Olá conta de armazenamento e de aplicações do Azure estão em Olá mesma geolocalização, evitar pagar os custos de largura de banda externa e reduzir a latência.</span><span class="sxs-lookup"><span data-stu-id="870b4-236">By keeping hello Azure application and storage account are in hello same geo-location, you avoid paying external bandwidth costs and reduce latency.</span></span>

### <a name="add-performance-counters-toohello-diagnostics-file"></a><span data-ttu-id="870b4-237">Adicionar ficheiros de diagnóstico de toohello de contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="870b4-237">Add performance counters toohello diagnostics file</span></span>
<span data-ttu-id="870b4-238">Existem muitos contadores, que pode utilizar.</span><span class="sxs-lookup"><span data-stu-id="870b4-238">There are many counters you can use.</span></span> <span data-ttu-id="870b4-239">Olá exemplo seguinte mostra vários contadores de desempenho que são recomendados para web e a monitorização da função de trabalho.</span><span class="sxs-lookup"><span data-stu-id="870b4-239">hello following example shows several performance counters that are recommended for web and worker role monitoring.</span></span>

<span data-ttu-id="870b4-240">Abrir o ficheiro de diagnóstico Olá (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima) e adicione Olá toohello DiagnosticMonitorConfiguration elemento a seguir:</span><span class="sxs-lookup"><span data-stu-id="870b4-240">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration element:</span></span>

```xml
<PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
    <PerformanceCounterConfiguration counterSpecifier="\Memory\Available Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Processor(_Total)\% Processor Time" sampleRate="PT30S" />

    <!-- Use hello Process(w3wp) category counters in a web role -->

    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\% Processor Time" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Private Bytes" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\Process(w3wp)\Thread Count" sampleRate="PT30S" />

    <!-- Use hello Process(WaWorkerHost) category counters in a worker role.
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\% Processor Time" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Private Bytes" sampleRate="PT30S" />
        <PerformanceCounterConfiguration counterSpecifier="\Process(WaWorkerHost)\Thread Count" sampleRate="PT30S" />
    -->

    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Interop(_Global_)\# of marshalling" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Loading(_Global_)\% Time Loading" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR LocksAndThreads(_Global_)\Contention Rate / sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Memory(_Global_)\# Bytes in all Heaps" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Networking(_Global_)\Connections Established" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Remoting(_Global_)\Remote Calls/sec" sampleRate="PT30S" />
    <PerformanceCounterConfiguration counterSpecifier="\.NET CLR Jit(_Global_)\% Time in Jit" sampleRate="PT30S" />
</PerformanceCounters>
```

<span data-ttu-id="870b4-241">Olá bufferQuotaInMB atributo, o que especifica a quantidade máxima de Olá de armazenamento do sistema de ficheiros que está disponível para o tipo de coleção de dados Olá (os registos do Azure, registos de IIS, etc.).</span><span class="sxs-lookup"><span data-stu-id="870b4-241">hello bufferQuotaInMB attribute, which specifies hello maximum amount of file system storage that is available for hello data collection type (Azure logs, IIS logs, etc.).</span></span> <span data-ttu-id="870b4-242">Olá predefinição é 0.</span><span class="sxs-lookup"><span data-stu-id="870b4-242">hello default is 0.</span></span> <span data-ttu-id="870b4-243">Quando for atingida a quota de Olá, os dados mais antigos Olá são eliminados como sendo adicionados dados novos.</span><span class="sxs-lookup"><span data-stu-id="870b4-243">When hello quota is reached, hello oldest data is deleted as new data is added.</span></span> <span data-ttu-id="870b4-244">soma de Olá de todas as propriedades de bufferQuotaInMB Olá tem de ser superior ao valor do atributo de OverallQuotaInMB Olá Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-244">hello sum of all hello bufferQuotaInMB properties must be greater than hello value of hello OverallQuotaInMB attribute.</span></span> <span data-ttu-id="870b4-245">Para ver um debate mais detalhado de determinar a quantidade de armazenamento será necessária para a coleção de Olá dos dados de diagnóstico, consulte Olá secção de configuração WAD de [resolução de problemas de melhores práticas para desenvolver aplicações do Azure](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span><span class="sxs-lookup"><span data-stu-id="870b4-245">For a more detailed discussion of determining how much storage will be required for hello collection of diagnostics data, see hello Setup WAD section of [Troubleshooting Best Practices for Developing Azure Applications](https://msdn.microsoft.com/library/windowsazure/hh771389.aspx).</span></span>

<span data-ttu-id="870b4-246">atributo de scheduledTransferPeriod Olá, o que especifica o intervalo de Olá entre agendada transferências de dados, arredondado toohello mais próximo minuto.</span><span class="sxs-lookup"><span data-stu-id="870b4-246">hello scheduledTransferPeriod attribute, which specifies hello interval between scheduled transfers of data, rounded up toohello nearest minute.</span></span> <span data-ttu-id="870b4-247">No Olá seguir exemplos, está definido tooPT30M (30 minutos).</span><span class="sxs-lookup"><span data-stu-id="870b4-247">In hello following examples, it is set tooPT30M (30 minutes).</span></span> <span data-ttu-id="870b4-248">Definição Olá transferência tooa período pequeno valor, tal como 1 minuto, negativamente irá afetar o desempenho da aplicação na produção, mas pode ser útil para ver o diagnóstico trabalhar rapidamente quando estiver a testar.</span><span class="sxs-lookup"><span data-stu-id="870b4-248">Setting hello transfer period tooa small value, such as 1 minute, will adversely impact your application's performance in production but can be useful for seeing diagnostics working quickly when you are testing.</span></span> <span data-ttu-id="870b4-249">período de transferência agendada de Olá deve ser suficientemente pequena tooensure que dados de diagnóstico não são substituídos na instância de Olá, mas suficientemente grande para que não irá afetar desempenho Olá da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-249">hello scheduled transfer period should be small enough tooensure that diagnostic data is not overwritten on hello instance, but large enough that it will not impact hello performance of your application.</span></span>

<span data-ttu-id="870b4-250">atributo de counterSpecifier Olá Especifica toocollect de contador de desempenho de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-250">hello counterSpecifier attribute specifies hello performance counter toocollect.</span></span> <span data-ttu-id="870b4-251">atributo de sampleRate Olá Especifica taxa Olá no qual o contador de desempenho de Olá deve ser objeto de amostragem, neste caso, 30 segundos.</span><span class="sxs-lookup"><span data-stu-id="870b4-251">hello sampleRate attribute specifies hello rate at which hello performance counter should be sampled, in this case 30 seconds.</span></span>

<span data-ttu-id="870b4-252">Depois de adicionar contadores de desempenho de Olá que pretende que o toocollect, guarde o ficheiro de diagnóstico de toohello de alterações.</span><span class="sxs-lookup"><span data-stu-id="870b4-252">Once you've added hello performance counters that you want toocollect, save your changes toohello diagnostics file.</span></span> <span data-ttu-id="870b4-253">Em seguida, terá de conta de armazenamento de Olá toospecify dados de diagnóstico de Olá serão transferidos para o.</span><span class="sxs-lookup"><span data-stu-id="870b4-253">Next, you need toospecify hello storage account that hello diagnostics data will be persisted to.</span></span>

### <a name="specify-hello-storage-account"></a><span data-ttu-id="870b4-254">Especifique a conta de armazenamento Olá</span><span class="sxs-lookup"><span data-stu-id="870b4-254">Specify hello storage account</span></span>
<span data-ttu-id="870b4-255">toopersist conta sua tooyour de informações de diagnóstico do armazenamento do Azure, tem de especificar uma cadeia de ligação no ficheiro de configuração (serviceconfiguration. Cscfg) do serviço.</span><span class="sxs-lookup"><span data-stu-id="870b4-255">toopersist your diagnostics information tooyour Azure Storage account, you must specify a connection string in your service configuration (ServiceConfiguration.cscfg) file.</span></span>

<span data-ttu-id="870b4-256">Para o Azure SDK 2.5, Olá conta de armazenamento pode ser especificado no ficheiro de diagnostics.wadcfgx Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-256">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>

> [!NOTE]
> <span data-ttu-id="870b4-257">Estas instruções aplicam-se apenas tooAzure SDK 2.4 e abaixo.</span><span class="sxs-lookup"><span data-stu-id="870b4-257">These instructions only apply tooAzure SDK 2.4 and below.</span></span> <span data-ttu-id="870b4-258">Para o Azure SDK 2.5, Olá conta de armazenamento pode ser especificado no ficheiro de diagnostics.wadcfgx Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-258">For Azure SDK 2.5, hello Storage Account can be specified in hello diagnostics.wadcfgx file.</span></span>
>
>

<span data-ttu-id="870b4-259">cadeias de ligação de Olá tooset:</span><span class="sxs-lookup"><span data-stu-id="870b4-259">tooset hello connection strings:</span></span>

1. <span data-ttu-id="870b4-260">Abra o ficheiro de Serviceconfiguration Olá utilizando o seu editor de texto favorito e a cadeia de ligação de Olá de conjunto para o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="870b4-260">Open hello ServiceConfiguration.Cloud.cscfg file using your favorite text editor and set hello connection string for your storage.</span></span> <span data-ttu-id="870b4-261">Olá *AccountName* e *AccountKey* valores encontram Olá portal do Azure no dashboard de conta de armazenamento de Olá, sob as chaves de acesso.</span><span class="sxs-lookup"><span data-stu-id="870b4-261">hello *AccountName* and *AccountKey* values are found in hello Azure portal in hello storage account dashboard, under Access keys.</span></span>

    ```xml
    <ConfigurationSettings>
      <Setting name="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="DefaultEndpointsProtocol=https;AccountName=<name>;AccountKey=<key>"/>
    </ConfigurationSettings>
    ```
2. <span data-ttu-id="870b4-262">Guarde o ficheiro do Olá Serviceconfiguration.</span><span class="sxs-lookup"><span data-stu-id="870b4-262">Save hello ServiceConfiguration.Cloud.cscfg file.</span></span>
3. <span data-ttu-id="870b4-263">Abrir o ficheiro de ServiceConfiguration.Local.cscfg Olá e certifique-se de que UseDevelopmentStorage está definida tootrue.</span><span class="sxs-lookup"><span data-stu-id="870b4-263">Open hello ServiceConfiguration.Local.cscfg file and verify that UseDevelopmentStorage is set tootrue.</span></span>

    ```xml
    <ConfigurationSettings>
      <Settingname="Microsoft.WindowsAzure.Plugins.Diagnostics.ConnectionString" value="UseDevelopmentStorage=true"/>
    </ConfigurationSettings>
    ```
   <span data-ttu-id="870b4-264">Agora que o conjunto de cadeias de ligação de Olá, a aplicação será mantido conta de armazenamento do diagnostics dados tooyour quando a aplicação for implementada.</span><span class="sxs-lookup"><span data-stu-id="870b4-264">Now that hello connection strings are set, your application will persist diagnostics data tooyour storage account when your application is deployed.</span></span>
4. <span data-ttu-id="870b4-265">Guardar e criar o projeto e, em seguida, implementar a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-265">Save and build your project, then deploy your application.</span></span>

## <a name="step-2-optional-create-custom-performance-counters"></a><span data-ttu-id="870b4-266">Passo 2: Os contadores de desempenho personalizados (opcional) criar</span><span class="sxs-lookup"><span data-stu-id="870b4-266">Step 2: (Optional) Create custom performance counters</span></span>
<span data-ttu-id="870b4-267">Além disso toohello predefinidas contadores de desempenho, pode adicionar que o seus próprios desempenho personalizado contadores toomonitor funções de web ou de trabalho.</span><span class="sxs-lookup"><span data-stu-id="870b4-267">In addition toohello pre-defined performance counters, you can add your own custom performance counters toomonitor web or worker roles.</span></span> <span data-ttu-id="870b4-268">Contadores de desempenho personalizado podem estar utilizado tootrack e monitor específico da aplicação o comportamento e pode ser criados ou eliminados numa tarefa de arranque, a função da web ou a função de trabalho com permissões elevadas.</span><span class="sxs-lookup"><span data-stu-id="870b4-268">Custom performance counters may be used tootrack and monitor application-specific behavior and can be created or deleted in a startup task, web role, or worker role with elevated permissions.</span></span>

<span data-ttu-id="870b4-269">agente de diagnóstico do Azure Olá atualiza Olá desempenho contador configuração a partir do ficheiro de .wadcfg Olá um minuto após a iniciar.</span><span class="sxs-lookup"><span data-stu-id="870b4-269">hello Azure diagnostics agent refreshes hello performance counter configuration from hello .wadcfg file one minute after starting.</span></span>  <span data-ttu-id="870b4-270">Se criar os contadores de desempenho personalizado no Olá método OnStart e as tarefas de arranque demorar mais do que um minuto tooexecute, os contadores de desempenho personalizados serão não ter sido criados quando o agente de diagnóstico do Azure Olá tenta tooload-los.</span><span class="sxs-lookup"><span data-stu-id="870b4-270">If you create custom performance counters in hello OnStart method and your startup tasks take longer than one minute tooexecute, your custom performance counters will not have been created when hello Azure Diagnostics agent tries tooload them.</span></span>  <span data-ttu-id="870b4-271">Neste cenário, verá que o Azure Diagnostics captura corretamente todos os dados de diagnóstico, exceto os contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="870b4-271">In this scenario, you will see that Azure Diagnostics correctly captures all diagnostics data except your custom performance counters.</span></span>  <span data-ttu-id="870b4-272">tooresolve este problema, crie Olá contadores de desempenho numa tarefa de arranque ou mover algumas das suas tarefas de arranque trabalham toohello OnStart método depois de criar Olá contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="870b4-272">tooresolve this issue, create hello performance counters in a startup task or move some of your startup task work toohello OnStart method after creating hello performance counters.</span></span>

<span data-ttu-id="870b4-273">Execute os seguintes passos toocreate de desempenho personalizado simple contador com o nome "\MyCustomCounterCategory\MyButton1Counter" de Olá:</span><span class="sxs-lookup"><span data-stu-id="870b4-273">Perform hello following steps toocreate a simple custom performance counter named "\MyCustomCounterCategory\MyButton1Counter":</span></span>

1. <span data-ttu-id="870b4-274">Abrir Olá serviço de ficheiro de definição (. CSDEF) para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-274">Open hello service definition file (CSDEF) for your application.</span></span>
2. <span data-ttu-id="870b4-275">Adicione Olá Runtime elemento toohello WebRole ou WorkerRole elemento tooallow execução com privilégios elevados:</span><span class="sxs-lookup"><span data-stu-id="870b4-275">Add hello Runtime element toohello WebRole or WorkerRole element tooallow execution with elevated privileges:</span></span>

    ```xml
    <runtime executioncontext="elevated"/>
    ```
3. <span data-ttu-id="870b4-276">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-276">Save hello file.</span></span>
4. <span data-ttu-id="870b4-277">Abrir o ficheiro de diagnóstico Olá (diagnostics.wadcfg no SDK 2.4 e abaixo ou diagnostics.wadcfgx no SDK 2.5 e acima) e adicione Olá seguir toohello DiagnosticMonitorConfiguration</span><span class="sxs-lookup"><span data-stu-id="870b4-277">Open hello diagnostics file (diagnostics.wadcfg in SDK 2.4 and below or diagnostics.wadcfgx in SDK 2.5 and above) and add hello following toohello DiagnosticMonitorConfiguration</span></span>

    ```xml
    <PerformanceCounters bufferQuotaInMB="0" scheduledTransferPeriod="PT30M">
      <PerformanceCounterConfiguration counterSpecifier="\MyCustomCounterCategory\MyButton1Counter" sampleRate="PT30S"/>
    </PerformanceCounters>
    ```
5. <span data-ttu-id="870b4-278">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-278">Save hello file.</span></span>
6. <span data-ttu-id="870b4-279">Crie categoria de contador de desempenho personalizados Olá no método de OnStart Olá da sua função, antes de invocar base. OnStart.</span><span class="sxs-lookup"><span data-stu-id="870b4-279">Create hello custom performance counter category in hello OnStart method of your role, before invoking base.OnStart.</span></span> <span data-ttu-id="870b4-280">Olá c# exemplo seguinte cria uma categoria personalizada, se já existir:</span><span class="sxs-lookup"><span data-stu-id="870b4-280">hello following C# example creates a custom category, if it does not already exist:</span></span>

    ```csharp
    public override bool OnStart()
    {
      if (!PerformanceCounterCategory.Exists("MyCustomCounterCategory"))
      {
         CounterCreationDataCollection counterCollection = new CounterCreationDataCollection();

         // add a counter tracking user button1 clicks
         CounterCreationData operationTotal1 = new CounterCreationData();
         operationTotal1.CounterName = "MyButton1Counter";
         operationTotal1.CounterHelp = "My Custom Counter for Button1";
         operationTotal1.CounterType = PerformanceCounterType.NumberOfItems32;
         counterCollection.Add(operationTotal1);

         PerformanceCounterCategory.Create(
           "MyCustomCounterCategory",
           "My Custom Counter Category",
           PerformanceCounterCategoryType.SingleInstance, counterCollection);

         Trace.WriteLine("Custom counter category created.");
      }
      else {
        Trace.WriteLine("Custom counter category already exists.");
      }

    return base.OnStart();
    }
    ```
7. <span data-ttu-id="870b4-281">Atualize contadores Olá dentro da sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="870b4-281">Update hello counters within your application.</span></span> <span data-ttu-id="870b4-282">Olá seguinte o exemplo de atualizações de um contador de desempenho personalizados Button1_Click eventos:</span><span class="sxs-lookup"><span data-stu-id="870b4-282">hello following example updates a custom performance counter on Button1_Click events:</span></span>

    ```csharp
    protected void Button1_Click(object sender, EventArgs e)
    {
      PerformanceCounter button1Counter = new PerformanceCounter(
        "MyCustomCounterCategory",
        "MyButton1Counter",
        string.Empty,
        false);
      button1Counter.Increment();
      this.Button1.Text = "Button 1 count: " +
        button1Counter.RawValue.ToString();
    }
    ```
8. <span data-ttu-id="870b4-283">Guarde o ficheiro de Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-283">Save hello file.</span></span>  

<span data-ttu-id="870b4-284">Dados do contador de desempenho personalizados agora serão recolhidos pelo monitor de diagnóstico do Azure Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-284">Custom performance counter data will now be collected by hello Azure diagnostics monitor.</span></span>

## <a name="step-3-query-performance-counter-data"></a><span data-ttu-id="870b4-285">Passo 3: Dados de contador de desempenho de consulta</span><span class="sxs-lookup"><span data-stu-id="870b4-285">Step 3: Query performance counter data</span></span>
<span data-ttu-id="870b4-286">Depois da aplicação é implementada e em execução, monitor de diagnóstico de Olá começará a recolher contadores de desempenho e a persistência desse tooAzure o armazenamento de dados.</span><span class="sxs-lookup"><span data-stu-id="870b4-286">Once your application is deployed and running, hello Diagnostics monitor will begin collecting performance counters and persisting that data tooAzure storage.</span></span> <span data-ttu-id="870b4-287">Utilize ferramentas como o Explorador de servidores no Visual Studio, [Explorador de armazenamento do Azure](http://azurestorageexplorer.codeplex.com/), ou [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) por Cerebrata dados Olá de contadores de desempenho de Olá tooview Tabela WADPerformanceCountersTable.</span><span class="sxs-lookup"><span data-stu-id="870b4-287">You use tools such as Server Explorer in Visual Studio,  [Azure Storage Explorer](http://azurestorageexplorer.codeplex.com/), or [Azure Diagnostics Manager](http://www.cerebrata.com/Products/AzureDiagnosticsManager/Default.aspx) by Cerebrata tooview hello performance counters data in hello WADPerformanceCountersTable table.</span></span> <span data-ttu-id="870b4-288">Pode também programaticamente consultar Olá tabela serviço a utilizar [c#](../cosmos-db/table-storage-how-to-use-dotnet.md), [Java](../cosmos-db/table-storage-how-to-use-java.md), [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), ou [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span><span class="sxs-lookup"><span data-stu-id="870b4-288">You can also programmatically query hello Table service using [C#](../cosmos-db/table-storage-how-to-use-dotnet.md),  [Java](../cosmos-db/table-storage-how-to-use-java.md),  [Node.js](../cosmos-db/table-storage-how-to-use-nodejs.md), [Python](../cosmos-db/table-storage-how-to-use-python.md), [Ruby](../cosmos-db/table-storage-how-to-use-ruby.md), or [PHP](../cosmos-db/table-storage-how-to-use-php.md).</span></span>

<span data-ttu-id="870b4-289">Olá c# exemplo seguinte mostra uma consulta básica relativamente à tabela de WADPerformanceCountersTable Olá e guarda Olá diagnóstico dados tooa um ficheiro CSV.</span><span class="sxs-lookup"><span data-stu-id="870b4-289">hello following C# example shows a basic query against hello WADPerformanceCountersTable table and saves hello diagnostics data tooa CSV file.</span></span> <span data-ttu-id="870b4-290">Depois dos contadores de desempenho de Olá são guardados tooa um ficheiro CSV, pode utilizar Olá graphing capacidades no Microsoft Excel ou alguns outros dados de ferramenta toovisualize Olá.</span><span class="sxs-lookup"><span data-stu-id="870b4-290">Once hello performance counters are saved tooa CSV file, you can use hello graphing capabilities in Microsoft Excel or some other tool toovisualize hello data.</span></span> <span data-ttu-id="870b4-291">Ser tooadd se um tooMicrosoft.WindowsAzure.Storage.dll de referência, que está incluído no Olá Azure SDK para .NET Outubro 2012 e posterior.</span><span class="sxs-lookup"><span data-stu-id="870b4-291">Be sure tooadd a reference tooMicrosoft.WindowsAzure.Storage.dll, which is included in hello Azure SDK for .NET October 2012 and later.</span></span> <span data-ttu-id="870b4-292">a assemblagem de Olá é instalado toohello % programa Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version num\ref\ diretório.</span><span class="sxs-lookup"><span data-stu-id="870b4-292">hello assembly is installed toohello %Program Files%\Microsoft SDKs\Microsoft Azure.NET SDK\version-num\ref\ directory.</span></span>

```csharp
using Microsoft.WindowsAzure.Storage;
using Microsoft.WindowsAzure.Storage.Auth;
using Microsoft.WindowsAzure.Storage.Table;
...

// Get hello connection string. When using Microsoft Azure Cloud Services, it is recommended
// you store your connection string using hello Microsoft Azure service configuration
// system (*.csdef and *.cscfg files). You can you use hello CloudConfigurationManager type
// tooretrieve your storage connection string.  If you're not using Cloud Services, it's
// recommended that you store hello connection string in your web.config or app.config file.
// Use hello ConfigurationManager type tooretrieve your storage connection string.

string connectionString = Microsoft.WindowsAzure.CloudConfigurationManager.GetSetting("StorageConnectionString");
//string connectionString = System.Configuration.ConfigurationManager.ConnectionStrings["StorageConnectionString"].ConnectionString;

// Get a reference toohello storage account using hello connection string.  You can also use hello development
// storage account (Storage Emulator) for local debugging.
CloudStorageAccount storageAccount = CloudStorageAccount.Parse(connectionString);
//CloudStorageAccount storageAccount = CloudStorageAccount.DevelopmentStorageAccount;

// Create hello table client.
CloudTableClient tableClient = storageAccount.CreateCloudTableClient();

// Create hello CloudTable object that represents hello "WADPerformanceCountersTable" table.
CloudTable table = tableClient.GetTableReference("WADPerformanceCountersTable");

// Create hello table query, filter on a specific CounterName, DeploymentId and RoleInstance.
TableQuery<PerformanceCountersEntity> query = new TableQuery<PerformanceCountersEntity>()
  .Where(
    TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("CounterName", QueryComparisons.Equal, @"\Processor(_Total)\% Processor Time"),
      TableOperators.And,
      TableQuery.CombineFilters(
      TableQuery.GenerateFilterCondition("DeploymentId", QueryComparisons.Equal, "ec26b7a1720447e1bcdeefc41c4892a3"),
      TableOperators.And,
      TableQuery.GenerateFilterCondition("RoleInstance", QueryComparisons.Equal, "WebRole1_IN_0")
    )
  )
);

// Execute hello table query.
IEnumerable<PerformanceCountersEntity> result = table.ExecuteQuery(query);

// Process hello query results and build a CSV file.
StringBuilder sb = new StringBuilder("TimeStamp,EventTickCount,DeploymentId,Role,RoleInstance,CounterName,CounterValue\n");

foreach (PerformanceCountersEntity entity in result)
{
  sb.Append(entity.Timestamp + "," + entity.EventTickCount + "," + entity.DeploymentId + ","
    + entity.Role + "," + entity.RoleInstance + "," + entity.CounterName + "," + entity.CounterValue+"\n");
}

StreamWriter sw = File.CreateText(@"C:\temp\PerfCounters.csv");
sw.Write(sb.ToString());
sw.Close();
```

<span data-ttu-id="870b4-293">As entidades mapeiam tooC # objetos utilizando uma classe personalizada derivada de **TableEntity**.</span><span class="sxs-lookup"><span data-stu-id="870b4-293">Entities map tooC# objects using a custom class derived from **TableEntity**.</span></span> <span data-ttu-id="870b4-294">Olá código seguinte define uma classe de entidade que representa um contador de desempenho Olá **WADPerformanceCountersTable** tabela.</span><span class="sxs-lookup"><span data-stu-id="870b4-294">hello following code defines an entity class that represents a performance counter in hello **WADPerformanceCountersTable** table.</span></span>

```csharp
public class PerformanceCountersEntity : TableEntity
{
  public long EventTickCount { get; set; }
  public string DeploymentId { get; set; }
  public string Role { get; set; }
  public string RoleInstance { get; set; }
  public string CounterName { get; set; }
  public double CounterValue { get; set; }
}
```

## <a name="next-steps"></a><span data-ttu-id="870b4-295">Passos Seguintes</span><span class="sxs-lookup"><span data-stu-id="870b4-295">Next Steps</span></span>
[<span data-ttu-id="870b4-296">Vista de artigos adicionais no diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="870b4-296">View additional articles on Azure Diagnostics</span></span>](../azure-diagnostics.md)
