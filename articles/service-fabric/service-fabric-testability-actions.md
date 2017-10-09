---
title: "falhas de aaaSimulate no Azure micro-serviços | Microsoft Docs"
description: "Este artigo aborda as ações de teste de Olá encontradas no Microsoft Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: motanv
manager: timlt
editor: toddabel
ms.assetid: ed53ca5c-4d5e-4b48-93c9-e386f32d8b7a
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: motanv;heeldin
ms.openlocfilehash: 5bdda1c0c5a40b243ab956c4791afd52e11c4089
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="testability-actions"></a><span data-ttu-id="19a44-103">Ações de teste</span><span class="sxs-lookup"><span data-stu-id="19a44-103">Testability actions</span></span>
<span data-ttu-id="19a44-104">Na ordem toosimulate uma infraestrutura pouco fiável, Azure Service Fabric fornece, programador Olá, com formas toosimulate várias falhas do mundo real e transições de estado.</span><span class="sxs-lookup"><span data-stu-id="19a44-104">In order toosimulate an unreliable infrastructure, Azure Service Fabric provides you, hello developer, with ways toosimulate various real-world failures and state transitions.</span></span> <span data-ttu-id="19a44-105">Estes são expostos como ações de teste.</span><span class="sxs-lookup"><span data-stu-id="19a44-105">These are exposed as testability actions.</span></span> <span data-ttu-id="19a44-106">ações de Olá são Olá APIs de baixo nível que fazer com que uma inserção de falhas específicas, transição de estado ou validação.</span><span class="sxs-lookup"><span data-stu-id="19a44-106">hello actions are hello low-level APIs that cause a specific fault injection, state transition, or validation.</span></span> <span data-ttu-id="19a44-107">Ao combinar estas ações, pode escrever cenários de teste abrangente para os serviços.</span><span class="sxs-lookup"><span data-stu-id="19a44-107">By combining these actions, you can write comprehensive test scenarios for your services.</span></span>

<span data-ttu-id="19a44-108">O Service Fabric fornece que alguns cenários comuns de teste é composto por estas ações.</span><span class="sxs-lookup"><span data-stu-id="19a44-108">Service Fabric provides some common test scenarios composed of these actions.</span></span> <span data-ttu-id="19a44-109">Recomendamos vivamente que utilizam estes cenários incorporados, que são escolhidos cuidadosamente tootest transições de estado comum e cenários de falha.</span><span class="sxs-lookup"><span data-stu-id="19a44-109">We highly recommend that you utilize these built-in scenarios, which are carefully chosen tootest common state transitions and failure cases.</span></span> <span data-ttu-id="19a44-110">No entanto, ações podem ser utilizados toocreate cenários de teste personalizado quando quiser tooadd cobertura para cenários que não são abrangidos por cenários incorporada Olá ainda ou que são personalizados adaptados para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="19a44-110">However, actions can be used toocreate custom test scenarios when you want tooadd coverage for scenarios that are not covered by hello built-in scenarios yet or that are custom tailored for your application.</span></span>

<span data-ttu-id="19a44-111">C# implementações das ações de Olá encontram Olá System.Fabric.dll assemblagem.</span><span class="sxs-lookup"><span data-stu-id="19a44-111">C# implementations of hello actions are found in hello System.Fabric.dll assembly.</span></span> <span data-ttu-id="19a44-112">módulo do PowerShell de recursos de infraestrutura de sistema Olá encontra-se no Olá Microsoft.ServiceFabric.Powershell.dll assemblagem.</span><span class="sxs-lookup"><span data-stu-id="19a44-112">hello System Fabric PowerShell module is found in hello Microsoft.ServiceFabric.Powershell.dll assembly.</span></span> <span data-ttu-id="19a44-113">Como parte da instalação de tempo de execução, Olá módulo ServiceFabric PowerShell é instalado tooallow facilidade de utilização.</span><span class="sxs-lookup"><span data-stu-id="19a44-113">As part of runtime installation, hello ServiceFabric PowerShell module is installed tooallow for ease of use.</span></span>

## <a name="graceful-vs-ungraceful-fault-actions"></a><span data-ttu-id="19a44-114">Correto vs ações ungraceful falhas</span><span class="sxs-lookup"><span data-stu-id="19a44-114">Graceful vs. ungraceful fault actions</span></span>
<span data-ttu-id="19a44-115">Ações de teste são classificadas em dois registos principais:</span><span class="sxs-lookup"><span data-stu-id="19a44-115">Testability actions are classified into two major buckets:</span></span>

* <span data-ttu-id="19a44-116">Falhas ungraceful: estas falhas simular falhas como reinícios da máquina e de falhas de processos.</span><span class="sxs-lookup"><span data-stu-id="19a44-116">Ungraceful faults: These faults simulate failures like machine restarts and process crashes.</span></span> <span data-ttu-id="19a44-117">Nestes casos de falhas, contexto de execução de Olá do processo interrompe abruptamente.</span><span class="sxs-lookup"><span data-stu-id="19a44-117">In such cases of failures, hello execution context of process stops abruptly.</span></span> <span data-ttu-id="19a44-118">Isto significa que nenhum limpeza do Estado de Olá pode executar antes de aplicação Olá começa novamente.</span><span class="sxs-lookup"><span data-stu-id="19a44-118">This means no cleanup of hello state can run before hello application starts up again.</span></span>
* <span data-ttu-id="19a44-119">Falhas correto: estas falhas simulam correto ações como move de réplica e remoções acionadas por balanceamento de carga.</span><span class="sxs-lookup"><span data-stu-id="19a44-119">Graceful faults: These faults simulate graceful actions like replica moves and drops triggered by load balancing.</span></span> <span data-ttu-id="19a44-120">Nestes casos, o serviço de Olá obtém uma notificação de Olá fechar e pode limpar estado Olá antes de sair.</span><span class="sxs-lookup"><span data-stu-id="19a44-120">In such cases, hello service gets a notification of hello close and can clean up hello state before exiting.</span></span>

<span data-ttu-id="19a44-121">Para melhor validação da qualidade, executar o serviço de Olá e carga de trabalho do negócio ao inducing várias falhas ungraceful e correto.</span><span class="sxs-lookup"><span data-stu-id="19a44-121">For better quality validation, run hello service and business workload while inducing various graceful and ungraceful faults.</span></span> <span data-ttu-id="19a44-122">Falhas ungraceful exercer cenários em que o processo de serviço de Olá sai abruptamente no meio de Olá de algumas fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="19a44-122">Ungraceful faults exercise scenarios where hello service process abruptly exits in hello middle of some workflow.</span></span> <span data-ttu-id="19a44-123">Isto testa o caminho de recuperação Olá assim que a réplica do serviço de Olá é restaurada pelo Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="19a44-123">This tests  hello recovery path once hello service replica is restored by Service Fabric.</span></span> <span data-ttu-id="19a44-124">Isto irá ajudar a testar a consistência dos dados e se o estado de serviço de Olá é mantido corretamente após falhas.</span><span class="sxs-lookup"><span data-stu-id="19a44-124">This will help test data consistency and whether hello service state is maintained correctly after failures.</span></span> <span data-ttu-id="19a44-125">Olá outro conjunto de falhas (Olá correto de falhas) de teste que o serviço de Olá reage corretamente tooreplicas que está a ser movidos em torno do Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="19a44-125">hello other set of failures (hello graceful failures) test that hello service correctly reacts tooreplicas being moved around by Service Fabric.</span></span> <span data-ttu-id="19a44-126">Isto testa o processamento de cancelamento no método runasync com de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-126">This tests handling of cancellation in hello RunAsync method.</span></span> <span data-ttu-id="19a44-127">serviço de Olá necessita toocheck para Olá cancelamento token que está a ser definido, corretamente guardar o estado e sair do método runasync com de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-127">hello service needs toocheck for hello cancellation token being set, correctly save its state, and exit hello RunAsync method.</span></span>

## <a name="testability-actions-list"></a><span data-ttu-id="19a44-128">Lista de ações de teste</span><span class="sxs-lookup"><span data-stu-id="19a44-128">Testability actions list</span></span>
| <span data-ttu-id="19a44-129">Ação</span><span class="sxs-lookup"><span data-stu-id="19a44-129">Action</span></span> | <span data-ttu-id="19a44-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="19a44-130">Description</span></span> | <span data-ttu-id="19a44-131">API gerido</span><span class="sxs-lookup"><span data-stu-id="19a44-131">Managed API</span></span> | <span data-ttu-id="19a44-132">Cmdlet do PowerShell</span><span class="sxs-lookup"><span data-stu-id="19a44-132">PowerShell cmdlet</span></span> | <span data-ttu-id="19a44-133">Falhas correto/ungraceful</span><span class="sxs-lookup"><span data-stu-id="19a44-133">Graceful/ungraceful faults</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="19a44-134">CleanTestState</span><span class="sxs-lookup"><span data-stu-id="19a44-134">CleanTestState</span></span> |<span data-ttu-id="19a44-135">Remove todos os Estados de teste de Olá cluster Olá em caso de um encerramento incorreto de controlador de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-135">Removes all hello test state from hello cluster in case of a bad shutdown of hello test driver.</span></span> |<span data-ttu-id="19a44-136">CleanTestStateAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-136">CleanTestStateAsync</span></span> |<span data-ttu-id="19a44-137">Remove-ServiceFabricTestState</span><span class="sxs-lookup"><span data-stu-id="19a44-137">Remove-ServiceFabricTestState</span></span> |<span data-ttu-id="19a44-138">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="19a44-138">Not applicable</span></span> |
| <span data-ttu-id="19a44-139">InvokeDataLoss</span><span class="sxs-lookup"><span data-stu-id="19a44-139">InvokeDataLoss</span></span> |<span data-ttu-id="19a44-140">Induces perda de dados para uma partição de serviço.</span><span class="sxs-lookup"><span data-stu-id="19a44-140">Induces data loss into a service partition.</span></span> |<span data-ttu-id="19a44-141">InvokeDataLossAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-141">InvokeDataLossAsync</span></span> |<span data-ttu-id="19a44-142">Invoke-ServiceFabricPartitionDataLoss</span><span class="sxs-lookup"><span data-stu-id="19a44-142">Invoke-ServiceFabricPartitionDataLoss</span></span> |<span data-ttu-id="19a44-143">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-143">Graceful</span></span> |
| <span data-ttu-id="19a44-144">InvokeQuorumLoss</span><span class="sxs-lookup"><span data-stu-id="19a44-144">InvokeQuorumLoss</span></span> |<span data-ttu-id="19a44-145">Coloca uma partição de serviço com estado fornecido no perda de quórum.</span><span class="sxs-lookup"><span data-stu-id="19a44-145">Puts a given stateful service partition into quorum loss.</span></span> |<span data-ttu-id="19a44-146">InvokeQuorumLossAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-146">InvokeQuorumLossAsync</span></span> |<span data-ttu-id="19a44-147">ServiceFabricQuorumLoss invocar</span><span class="sxs-lookup"><span data-stu-id="19a44-147">Invoke-ServiceFabricQuorumLoss</span></span> |<span data-ttu-id="19a44-148">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-148">Graceful</span></span> |
| <span data-ttu-id="19a44-149">Mover primário</span><span class="sxs-lookup"><span data-stu-id="19a44-149">Move Primary</span></span> |<span data-ttu-id="19a44-150">Move Olá especificado réplica primária de um nó de cluster especificado do serviço com estado toohello.</span><span class="sxs-lookup"><span data-stu-id="19a44-150">Moves hello specified primary replica of a stateful service toohello specified cluster node.</span></span> |<span data-ttu-id="19a44-151">MovePrimaryAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-151">MovePrimaryAsync</span></span> |<span data-ttu-id="19a44-152">Mover ServiceFabricPrimaryReplica</span><span class="sxs-lookup"><span data-stu-id="19a44-152">Move-ServiceFabricPrimaryReplica</span></span> |<span data-ttu-id="19a44-153">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-153">Graceful</span></span> |
| <span data-ttu-id="19a44-154">Mover secundário</span><span class="sxs-lookup"><span data-stu-id="19a44-154">Move Secondary</span></span> |<span data-ttu-id="19a44-155">Move a réplica secundária atual Olá um serviço com estado tooa diferente do nó do cluster.</span><span class="sxs-lookup"><span data-stu-id="19a44-155">Moves hello current secondary replica of a stateful service tooa different cluster node.</span></span> |<span data-ttu-id="19a44-156">MoveSecondaryAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-156">MoveSecondaryAsync</span></span> |<span data-ttu-id="19a44-157">Mover ServiceFabricSecondaryReplica</span><span class="sxs-lookup"><span data-stu-id="19a44-157">Move-ServiceFabricSecondaryReplica</span></span> |<span data-ttu-id="19a44-158">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-158">Graceful</span></span> |
| <span data-ttu-id="19a44-159">RemoveReplica</span><span class="sxs-lookup"><span data-stu-id="19a44-159">RemoveReplica</span></span> |<span data-ttu-id="19a44-160">Simula uma falha de réplica ao remover uma réplica de um cluster.</span><span class="sxs-lookup"><span data-stu-id="19a44-160">Simulates a replica failure by removing a replica from a cluster.</span></span> <span data-ttu-id="19a44-161">Isto irá fechar réplica Olá e irão transitar-toorole 'None', removendo todos os Estado do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-161">This will close hello replica and will transition it toorole 'None', removing all of its state from hello cluster.</span></span> |<span data-ttu-id="19a44-162">RemoveReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-162">RemoveReplicaAsync</span></span> |<span data-ttu-id="19a44-163">Remover ServiceFabricReplica</span><span class="sxs-lookup"><span data-stu-id="19a44-163">Remove-ServiceFabricReplica</span></span> |<span data-ttu-id="19a44-164">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-164">Graceful</span></span> |
| <span data-ttu-id="19a44-165">RestartDeployedCodePackage</span><span class="sxs-lookup"><span data-stu-id="19a44-165">RestartDeployedCodePackage</span></span> |<span data-ttu-id="19a44-166">Simula uma falha de processo de pacote do código reiniciando um pacote do código implementado num nó num cluster.</span><span class="sxs-lookup"><span data-stu-id="19a44-166">Simulates a code package process failure by restarting a code package deployed on a node in a cluster.</span></span> <span data-ttu-id="19a44-167">Isto interrompe o processo de pacote do Olá código, que será reiniciado todas as réplicas de serviço do utilizador Olá alojadas no processo.</span><span class="sxs-lookup"><span data-stu-id="19a44-167">This aborts hello code package process, which will restart all hello user service replicas hosted in that process.</span></span> |<span data-ttu-id="19a44-168">RestartDeployedCodePackageAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-168">RestartDeployedCodePackageAsync</span></span> |<span data-ttu-id="19a44-169">ServiceFabricDeployedCodePackage de reinício</span><span class="sxs-lookup"><span data-stu-id="19a44-169">Restart-ServiceFabricDeployedCodePackage</span></span> |<span data-ttu-id="19a44-170">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="19a44-170">Ungraceful</span></span> |
| <span data-ttu-id="19a44-171">RestartNode</span><span class="sxs-lookup"><span data-stu-id="19a44-171">RestartNode</span></span> |<span data-ttu-id="19a44-172">Simula uma falha de nó de cluster do Service Fabric reiniciando um nó.</span><span class="sxs-lookup"><span data-stu-id="19a44-172">Simulates a Service Fabric cluster node failure by restarting a node.</span></span> |<span data-ttu-id="19a44-173">RestartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-173">RestartNodeAsync</span></span> |<span data-ttu-id="19a44-174">ServiceFabricNode de reinício</span><span class="sxs-lookup"><span data-stu-id="19a44-174">Restart-ServiceFabricNode</span></span> |<span data-ttu-id="19a44-175">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="19a44-175">Ungraceful</span></span> |
| <span data-ttu-id="19a44-176">RestartPartition</span><span class="sxs-lookup"><span data-stu-id="19a44-176">RestartPartition</span></span> |<span data-ttu-id="19a44-177">Simula um cenário de blackout datacenter blackout ou cluster reiniciando algumas ou todas as réplicas de uma partição.</span><span class="sxs-lookup"><span data-stu-id="19a44-177">Simulates a datacenter blackout or cluster blackout scenario by restarting some or all replicas of a partition.</span></span> |<span data-ttu-id="19a44-178">RestartPartitionAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-178">RestartPartitionAsync</span></span> |<span data-ttu-id="19a44-179">Restart-ServiceFabricPartition</span><span class="sxs-lookup"><span data-stu-id="19a44-179">Restart-ServiceFabricPartition</span></span> |<span data-ttu-id="19a44-180">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-180">Graceful</span></span> |
| <span data-ttu-id="19a44-181">RestartReplica</span><span class="sxs-lookup"><span data-stu-id="19a44-181">RestartReplica</span></span> |<span data-ttu-id="19a44-182">Simula uma falha de réplica ao reiniciar uma réplica persistente num cluster, réplica Olá a fechar e, em seguida, abri-lo.</span><span class="sxs-lookup"><span data-stu-id="19a44-182">Simulates a replica failure by restarting a persisted replica in a cluster, closing hello replica and then reopening it.</span></span> |<span data-ttu-id="19a44-183">RestartReplicaAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-183">RestartReplicaAsync</span></span> |<span data-ttu-id="19a44-184">ServiceFabricReplica de reinício</span><span class="sxs-lookup"><span data-stu-id="19a44-184">Restart-ServiceFabricReplica</span></span> |<span data-ttu-id="19a44-185">Correto</span><span class="sxs-lookup"><span data-stu-id="19a44-185">Graceful</span></span> |
| <span data-ttu-id="19a44-186">StartNode</span><span class="sxs-lookup"><span data-stu-id="19a44-186">StartNode</span></span> |<span data-ttu-id="19a44-187">Inicia um nó num cluster que já é parado.</span><span class="sxs-lookup"><span data-stu-id="19a44-187">Starts a node in a cluster that is already stopped.</span></span> |<span data-ttu-id="19a44-188">StartNodeAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-188">StartNodeAsync</span></span> |<span data-ttu-id="19a44-189">Start-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19a44-189">Start-ServiceFabricNode</span></span> |<span data-ttu-id="19a44-190">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="19a44-190">Not applicable</span></span> |
| <span data-ttu-id="19a44-191">StopNode</span><span class="sxs-lookup"><span data-stu-id="19a44-191">StopNode</span></span> |<span data-ttu-id="19a44-192">Simula uma falha de nó por parar um nó num cluster.</span><span class="sxs-lookup"><span data-stu-id="19a44-192">Simulates a node failure by stopping a node in a cluster.</span></span> <span data-ttu-id="19a44-193">nó de Olá permanecerão para baixo até StartNode é chamado.</span><span class="sxs-lookup"><span data-stu-id="19a44-193">hello node will stay down until StartNode is called.</span></span> |<span data-ttu-id="19a44-194">StopNodeAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-194">StopNodeAsync</span></span> |<span data-ttu-id="19a44-195">Stop-ServiceFabricNode</span><span class="sxs-lookup"><span data-stu-id="19a44-195">Stop-ServiceFabricNode</span></span> |<span data-ttu-id="19a44-196">Ungraceful</span><span class="sxs-lookup"><span data-stu-id="19a44-196">Ungraceful</span></span> |
| <span data-ttu-id="19a44-197">ValidateApplication</span><span class="sxs-lookup"><span data-stu-id="19a44-197">ValidateApplication</span></span> |<span data-ttu-id="19a44-198">Valida Olá disponibilidade e o estado de funcionamento de todos os serviços do Service Fabric dentro de uma aplicação, normalmente, após inducing algumas falhas no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-198">Validates hello availability and health of all Service Fabric services within an application, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="19a44-199">ValidateApplicationAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-199">ValidateApplicationAsync</span></span> |<span data-ttu-id="19a44-200">Teste ServiceFabricApplication</span><span class="sxs-lookup"><span data-stu-id="19a44-200">Test-ServiceFabricApplication</span></span> |<span data-ttu-id="19a44-201">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="19a44-201">Not applicable</span></span> |
| <span data-ttu-id="19a44-202">ValidateService</span><span class="sxs-lookup"><span data-stu-id="19a44-202">ValidateService</span></span> |<span data-ttu-id="19a44-203">Valida Olá disponibilidade e o estado de funcionamento de um serviço do Service Fabric, geralmente após inducing algumas falhas no sistema de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-203">Validates hello availability and health of a Service Fabric service, usually after inducing some fault into hello system.</span></span> |<span data-ttu-id="19a44-204">ValidateServiceAsync</span><span class="sxs-lookup"><span data-stu-id="19a44-204">ValidateServiceAsync</span></span> |<span data-ttu-id="19a44-205">Teste ServiceFabricService</span><span class="sxs-lookup"><span data-stu-id="19a44-205">Test-ServiceFabricService</span></span> |<span data-ttu-id="19a44-206">Não aplicável</span><span class="sxs-lookup"><span data-stu-id="19a44-206">Not applicable</span></span> |

## <a name="running-a-testability-action-using-powershell"></a><span data-ttu-id="19a44-207">Execução de uma ação de teste com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="19a44-207">Running a testability action using PowerShell</span></span>
<span data-ttu-id="19a44-208">Este tutorial mostra como toorun uma ação de teste utilizando o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a44-208">This tutorial shows you how toorun a testability action by using PowerShell.</span></span> <span data-ttu-id="19a44-209">Ficará a saber como toorun uma ação de teste contra um cluster (uma caixa) local ou um cluster do Azure.</span><span class="sxs-lookup"><span data-stu-id="19a44-209">You will learn how toorun a testability action against a local (one-box) cluster or an Azure cluster.</span></span> <span data-ttu-id="19a44-210">Microsoft.Fabric.Powershell.dll – hello módulo do PowerShell de Service Fabric – é instalada automaticamente ao instalar Olá MSI de recursos de infraestrutura de serviço do Microsoft.</span><span class="sxs-lookup"><span data-stu-id="19a44-210">Microsoft.Fabric.Powershell.dll--hello Service Fabric PowerShell module--is installed automatically when you install hello Microsoft Service Fabric MSI.</span></span> <span data-ttu-id="19a44-211">módulo Olá é carregado automaticamente quando abrir uma linha de comandos do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="19a44-211">hello module is loaded automatically when you open a PowerShell prompt.</span></span>

<span data-ttu-id="19a44-212">Tutorial segmentos:</span><span class="sxs-lookup"><span data-stu-id="19a44-212">Tutorial segments:</span></span>

* [<span data-ttu-id="19a44-213">Executar uma ação contra um cluster de um caixa</span><span class="sxs-lookup"><span data-stu-id="19a44-213">Run an action against a one-box cluster</span></span>](#run-an-action-against-a-one-box-cluster)
* [<span data-ttu-id="19a44-214">Executar uma ação contra um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="19a44-214">Run an action against an Azure cluster</span></span>](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a><span data-ttu-id="19a44-215">Executar uma ação contra um cluster de um caixa</span><span class="sxs-lookup"><span data-stu-id="19a44-215">Run an action against a one-box cluster</span></span>
<span data-ttu-id="19a44-216">toorun uma ação de teste contra um cluster local, ligam pela primeira vez toohello cluster e o pedido de PowerShell Olá aberto no modo de administrador.</span><span class="sxs-lookup"><span data-stu-id="19a44-216">toorun a testability action against a local cluster, first connect toohello cluster and open hello PowerShell prompt in administrator mode.</span></span> <span data-ttu-id="19a44-217">Informe-nos observar Olá **reinício ServiceFabricNode** ação.</span><span class="sxs-lookup"><span data-stu-id="19a44-217">Let us look at hello **Restart-ServiceFabricNode** action.</span></span>

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

<span data-ttu-id="19a44-218">Aqui Olá ação **reinício ServiceFabricNode** está a ser executado num nó com o nome "Nó1".</span><span class="sxs-lookup"><span data-stu-id="19a44-218">Here hello action **Restart-ServiceFabricNode** is being run on a node named "Node1".</span></span> <span data-ttu-id="19a44-219">modo de conclusão de Olá Especifica que este deve não verificar se ação de reinício do nó de Olá, na verdade, foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="19a44-219">hello completion mode specifies that it should not verify whether hello restart-node action actually succeeded.</span></span> <span data-ttu-id="19a44-220">Modo de conclusão de Olá especificação como "Verificar" fará com que este tooverify se a ação de reinício de Olá, na verdade, foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="19a44-220">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="19a44-221">Em vez de especificar diretamente nó Olá pelo respetivo nome, pode especificá-la através de um tipo de chave e Olá de partição de réplica, da seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="19a44-221">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica, as follows:</span></span>

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

<span data-ttu-id="19a44-222">**Reinício ServiceFabricNode** deve ser um nó de Service Fabric num cluster toorestart utilizado.</span><span class="sxs-lookup"><span data-stu-id="19a44-222">**Restart-ServiceFabricNode** should be used toorestart a Service Fabric node in a cluster.</span></span> <span data-ttu-id="19a44-223">Isto irá parar o processo de Fabric.exe Olá, o que irá reiniciar todos os Olá sistema serviço e o utilizador serviço réplicas alojadas nesse nó.</span><span class="sxs-lookup"><span data-stu-id="19a44-223">This will stop hello Fabric.exe process, which will restart all of hello system service and user service replicas hosted on that node.</span></span> <span data-ttu-id="19a44-224">Este tootest de API a utilizar o serviço de ajuda-o desvendar erros ao longo de caminhos de recuperação de ativação pós-falha de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-224">Using this API tootest your service helps uncover bugs along hello failover recovery paths.</span></span> <span data-ttu-id="19a44-225">Ajuda a simular falhas de nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-225">It helps simulate node failures in hello cluster.</span></span>

<span data-ttu-id="19a44-226">Olá seguinte captura de ecrã mostra Olá **reinício ServiceFabricNode** comando de teste em ação.</span><span class="sxs-lookup"><span data-stu-id="19a44-226">hello following screenshot shows hello **Restart-ServiceFabricNode** testability command in action.</span></span>

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

<span data-ttu-id="19a44-227">Olá primeiro de saída de Olá **Get-ServiceFabricNode** (um cmdlet do módulo do PowerShell de Service Fabric de Olá) mostra esse cluster local Olá com cinco nós: Node.1 tooNode.5.</span><span class="sxs-lookup"><span data-stu-id="19a44-227">hello output of hello first **Get-ServiceFabricNode** (a cmdlet from hello Service Fabric PowerShell module) shows that hello local cluster has five nodes: Node.1 tooNode.5.</span></span> <span data-ttu-id="19a44-228">Após a ação de teste de Olá (cmdlet) **reinício ServiceFabricNode** é executada num nó de Olá, com o nome Node.4, vemos disponibilidade nesse nó Olá foi reposta.</span><span class="sxs-lookup"><span data-stu-id="19a44-228">After hello testability action (cmdlet) **Restart-ServiceFabricNode** is executed on hello node, named Node.4, we see that hello node's uptime has been reset.</span></span>

### <a name="run-an-action-against-an-azure-cluster"></a><span data-ttu-id="19a44-229">Executar uma ação contra um cluster do Azure</span><span class="sxs-lookup"><span data-stu-id="19a44-229">Run an action against an Azure cluster</span></span>
<span data-ttu-id="19a44-230">Execução de uma ação de teste (utilizando o PowerShell) contra um cluster do Azure é semelhante toorunning Olá contra um cluster local.</span><span class="sxs-lookup"><span data-stu-id="19a44-230">Running a testability action (by using PowerShell) against an Azure cluster is similar toorunning hello action against a local cluster.</span></span> <span data-ttu-id="19a44-231">Olá apenas diferença é que, antes de poder executar a ação de Olá, em vez de estabelecer ligação toohello cluster local, terá de tooconnect toohello Azure cluster primeiro.</span><span class="sxs-lookup"><span data-stu-id="19a44-231">hello only difference is that before you can run hello action, instead of connecting toohello local cluster, you need tooconnect toohello Azure cluster first.</span></span>

## <a name="running-a-testability-action-using-c35"></a><span data-ttu-id="19a44-232">Execução de uma ação de teste com C &#35;</span><span class="sxs-lookup"><span data-stu-id="19a44-232">Running a testability action using C&#35;</span></span>
<span data-ttu-id="19a44-233">toorun uma ação de teste ao utilizar c#, primeiro tem de tooconnect toohello cluster utilizando FabricClient.</span><span class="sxs-lookup"><span data-stu-id="19a44-233">toorun a testability action by using C#, first you need tooconnect toohello cluster by using FabricClient.</span></span> <span data-ttu-id="19a44-234">Em seguida, obter Olá parâmetros necessários toorun Olá ação.</span><span class="sxs-lookup"><span data-stu-id="19a44-234">Then obtain hello parameters needed toorun hello action.</span></span> <span data-ttu-id="19a44-235">Parâmetros diferentes podem ser utilizados toorun Olá a mesma ação.</span><span class="sxs-lookup"><span data-stu-id="19a44-235">Different parameters can be used toorun hello same action.</span></span>
<span data-ttu-id="19a44-236">Observar Olá RestartServiceFabricNode ação, toorun unidirecional é através da utilização de informações do nó de Olá (nome de nó e o ID de instância do nó) no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-236">Looking at hello RestartServiceFabricNode action, one way toorun it is by using hello node information (node name and node instance ID) in hello cluster.</span></span>

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

<span data-ttu-id="19a44-237">Explicação de parâmetro:</span><span class="sxs-lookup"><span data-stu-id="19a44-237">Parameter explanation:</span></span>

* <span data-ttu-id="19a44-238">**CompleteMode** especifica de que modo Olá não deve verificar se ação de reinício de Olá, na verdade, foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="19a44-238">**CompleteMode** specifies that hello mode should not verify whether hello restart action actually succeeded.</span></span> <span data-ttu-id="19a44-239">Modo de conclusão de Olá especificação como "Verificar" fará com que este tooverify se a ação de reinício de Olá, na verdade, foi concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="19a44-239">Specifying hello completion mode as "Verify" will cause it tooverify whether hello restart action actually succeeded.</span></span>  
* <span data-ttu-id="19a44-240">**OperationTimeout** conjuntos Olá quantidade de tempo para Olá operação toofinish antes de que é emitida uma exceção de TimeoutException.</span><span class="sxs-lookup"><span data-stu-id="19a44-240">**OperationTimeout** sets hello amount of time for hello operation toofinish before a TimeoutException exception is thrown.</span></span>
* <span data-ttu-id="19a44-241">**CancellationToken** permite um toobe chamada pendente cancelada.</span><span class="sxs-lookup"><span data-stu-id="19a44-241">**CancellationToken** enables a pending call toobe canceled.</span></span>

<span data-ttu-id="19a44-242">Em vez de especificar diretamente nó Olá pelo respetivo nome, pode especificá-la através de um tipo de chave e Olá de partição de réplica.</span><span class="sxs-lookup"><span data-stu-id="19a44-242">Instead of directly specifying hello node by its name, you can specify it via a partition key and hello kind of replica.</span></span>

<span data-ttu-id="19a44-243">Para obter mais informações, consulte [PartitionSelector e ReplicaSelector](#partition_replica_selector).</span><span class="sxs-lookup"><span data-stu-id="19a44-243">For further information, see [PartitionSelector and ReplicaSelector](#partition_replica_selector).</span></span>

```csharp
// Add a reference tooSystem.Fabric.Testability.dll and System.Fabric.dll
using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Fabric.Testability;
using System.Fabric;
using System.Threading;
using System.Numerics;

class Test
{
    public static int Main(string[] args)
    {
        string clusterConnection = "localhost:19000";
        Uri serviceName = new Uri("fabric:/samples/PersistentToDoListApp/PersistentToDoListService");
        string nodeName = "N0040";
        BigInteger nodeInstanceId = 130743013389060139;

        Console.WriteLine("Starting RestartNode test");
        try
        {
            //Restart hello node by using ReplicaSelector
            RestartNodeAsync(clusterConnection, serviceName).Wait();

            //Another way toorestart node is by using nodeName and nodeInstanceId
            RestartNodeAsync(clusterConnection, nodeName, nodeInstanceId).Wait();
        }
        catch (AggregateException exAgg)
        {
            Console.WriteLine("RestartNode did not complete: ");
            foreach (Exception ex in exAgg.InnerExceptions)
            {
                if (ex is FabricException)
                {
                    Console.WriteLine("HResult: {0} Message: {1}", ex.HResult, ex.Message);
                }
            }
            return -1;
        }

        Console.WriteLine("RestartNode completed.");
        return 0;
    }

    static async Task RestartNodeAsync(string clusterConnection, Uri serviceName)
    {
        PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);
        ReplicaSelector primaryofReplicaSelector = ReplicaSelector.PrimaryOf(randomPartitionSelector);

        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(primaryofReplicaSelector, CompletionMode.Verify);
    }

    static async Task RestartNodeAsync(string clusterConnection, string nodeName, BigInteger nodeInstanceId)
    {
        // Create FabricClient with connection and security information here
        FabricClient fabricclient = new FabricClient(clusterConnection);
        await fabricclient.FaultManager.RestartNodeAsync(nodeName, nodeInstanceId, CompletionMode.Verify);
    }
}
```

## <a name="partitionselector-and-replicaselector"></a><span data-ttu-id="19a44-244">PartitionSelector e ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="19a44-244">PartitionSelector and ReplicaSelector</span></span>
### <a name="partitionselector"></a><span data-ttu-id="19a44-245">PartitionSelector</span><span class="sxs-lookup"><span data-stu-id="19a44-245">PartitionSelector</span></span>
<span data-ttu-id="19a44-246">PartitionSelector é um programa auxiliar exposta no teste e é utilizado tooselect específico de partição na qual tooperform qualquer uma das ações de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-246">PartitionSelector is a helper exposed in testability and is used tooselect a specific partition on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="19a44-247">Pode ser utilizado tooselect uma partição específica se o ID de partição Olá é conhecido previamente.</span><span class="sxs-lookup"><span data-stu-id="19a44-247">It can be used tooselect a specific partition if hello partition ID is known beforehand.</span></span> <span data-ttu-id="19a44-248">Em alternativa, pode fornecer a chave de partição Olá e operação Olá irá resolver o ID de partição Olá internamente.</span><span class="sxs-lookup"><span data-stu-id="19a44-248">Or, you can provide hello partition key and hello operation will resolve hello partition ID internally.</span></span> <span data-ttu-id="19a44-249">Tem também a opção Olá da seleção de uma partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="19a44-249">You also have hello option of selecting a random partition.</span></span>

<span data-ttu-id="19a44-250">toouse esta ajuda, criar Olá PartitionSelector objeto e selecione o partição Olá utilizando um dos métodos de Olá selecione *.</span><span class="sxs-lookup"><span data-stu-id="19a44-250">toouse this helper, create hello PartitionSelector object and select hello partition by using one of hello Select* methods.</span></span> <span data-ttu-id="19a44-251">Então, passe no Olá PartitionSelector objeto toohello API que obriga.</span><span class="sxs-lookup"><span data-stu-id="19a44-251">Then pass in hello PartitionSelector object toohello API that requires it.</span></span> <span data-ttu-id="19a44-252">Se nenhuma opção for selecionada, assume partição aleatório tooa.</span><span class="sxs-lookup"><span data-stu-id="19a44-252">If no option is selected, it defaults tooa random partition.</span></span>

```csharp
Uri serviceName = new Uri("fabric:/samples/InMemoryToDoListApp/InMemoryToDoListService");
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
string partitionName = "Partition1";
Int64 partitionKeyUniformInt64 = 1;

// Select a random partition
PartitionSelector randomPartitionSelector = PartitionSelector.RandomOf(serviceName);

// Select a partition based on ID
PartitionSelector partitionSelectorById = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);

// Select a partition based on name
PartitionSelector namedPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionName);

// Select a partition based on partition key
PartitionSelector uniformIntPartitionSelector = PartitionSelector.PartitionKeyOf(serviceName, partitionKeyUniformInt64);
```

### <a name="replicaselector"></a><span data-ttu-id="19a44-253">ReplicaSelector</span><span class="sxs-lookup"><span data-stu-id="19a44-253">ReplicaSelector</span></span>
<span data-ttu-id="19a44-254">ReplicaSelector é um programa auxiliar exposta no teste e é utilizado toohelp selecionar uma réplica no qual tooperform qualquer uma das ações de teste de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-254">ReplicaSelector is a helper exposed in testability and is used toohelp select a replica on which tooperform any of hello testability actions.</span></span> <span data-ttu-id="19a44-255">Pode ser utilizado tooselect uma réplica específica se o ID de réplica Olá é conhecido previamente.</span><span class="sxs-lookup"><span data-stu-id="19a44-255">It can be used tooselect a specific replica if hello replica ID is known beforehand.</span></span> <span data-ttu-id="19a44-256">Além disso, terá de opção de Olá da seleção de uma réplica primária ou secundária aleatória.</span><span class="sxs-lookup"><span data-stu-id="19a44-256">In addition, you have hello option of selecting a primary replica or a random secondary.</span></span> <span data-ttu-id="19a44-257">ReplicaSelector deriva de PartitionSelector, por isso terá de tooselect ambos Olá partição de réplica e Olá no qual pretende a operação de teste de Olá tooperform.</span><span class="sxs-lookup"><span data-stu-id="19a44-257">ReplicaSelector derives from PartitionSelector, so you need tooselect both hello replica and hello partition on which you wish tooperform hello testability operation.</span></span>

<span data-ttu-id="19a44-258">toouse esta ajuda, crie um objeto de ReplicaSelector e defina Olá gosta tooselect de partição de réplica e Olá de Olá.</span><span class="sxs-lookup"><span data-stu-id="19a44-258">toouse this helper, create a ReplicaSelector object and set hello way you want tooselect hello replica and hello partition.</span></span> <span data-ttu-id="19a44-259">Em seguida, pode passar para Olá API que obriga.</span><span class="sxs-lookup"><span data-stu-id="19a44-259">You can then pass it into hello API that requires it.</span></span> <span data-ttu-id="19a44-260">Se nenhuma opção for selecionada, assume réplica aleatório tooa e partição aleatória.</span><span class="sxs-lookup"><span data-stu-id="19a44-260">If no option is selected, it defaults tooa random replica and random partition.</span></span>

```csharp
Guid partitionIdGuid = new Guid("8fb7ebcc-56ee-4862-9cc0-7c6421e68829");
PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(serviceName, partitionIdGuid);
long replicaId = 130559876481875498;

// Select a random replica
ReplicaSelector randomReplicaSelector = ReplicaSelector.RandomOf(partitionSelector);

// Select hello primary replica
ReplicaSelector primaryReplicaSelector = ReplicaSelector.PrimaryOf(partitionSelector);

// Select hello replica by ID
ReplicaSelector replicaByIdSelector = ReplicaSelector.ReplicaIdOf(partitionSelector, replicaId);

// Select a random secondary replica
ReplicaSelector secondaryReplicaSelector = ReplicaSelector.RandomSecondaryOf(partitionSelector);
```

## <a name="next-steps"></a><span data-ttu-id="19a44-261">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="19a44-261">Next steps</span></span>
* [<span data-ttu-id="19a44-262">Cenários de teste</span><span class="sxs-lookup"><span data-stu-id="19a44-262">Testability scenarios</span></span>](service-fabric-testability-scenarios.md)
* <span data-ttu-id="19a44-263">Como tootest seu serviço</span><span class="sxs-lookup"><span data-stu-id="19a44-263">How tootest your service</span></span>
  * [<span data-ttu-id="19a44-264">Simular falhas durante a cargas de trabalho do serviço</span><span class="sxs-lookup"><span data-stu-id="19a44-264">Simulate failures during service workloads</span></span>](service-fabric-testability-workload-tests.md)
  * [<span data-ttu-id="19a44-265">Falhas de comunicação de serviço de serviço</span><span class="sxs-lookup"><span data-stu-id="19a44-265">Service-to-service communication failures</span></span>](service-fabric-testability-scenarios-service-communication.md)

