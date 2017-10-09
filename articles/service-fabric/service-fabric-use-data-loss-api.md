---
title: "aaaHow tooInvoke perda de dados nos serviços de recursos de infraestrutura de serviço | Microsoft Docs"
description: "Descreve como toouse Olá perda de dados api"
services: service-fabric
documentationcenter: .net
author: LMWF
manager: rsinha
editor: 
ms.assetid: f4e70f6f-cad9-4a3e-9655-009b4db09c6d
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 09/19/2016
ms.author: lemai
redirect_url: /azure/service-fabric/service-fabric-testability-overview
ms.openlocfilehash: 014c7ebfd2c42d79a5fe1802ecc3fa0c1f26f9d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooinvoke-data-loss-on-services"></a><span data-ttu-id="ce10a-103">Como tooInvoke perda de dados nos serviços</span><span class="sxs-lookup"><span data-stu-id="ce10a-103">How tooInvoke Data Loss on Services</span></span>
> [!WARNING]
> <span data-ttu-id="ce10a-104">Este documento descrevem como toocause perda de dados nos serviços e deve ser utilizado com cuidado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-104">This document describe how toocause data loss in your services, and should be used with care.</span></span>
> 
> 

## <a name="introduction"></a><span data-ttu-id="ce10a-105">Introdução</span><span class="sxs-lookup"><span data-stu-id="ce10a-105">Introduction</span></span>
<span data-ttu-id="ce10a-106">Pode invocar perda de dados numa partição do seu serviço de recursos de infraestrutura de serviço por StartPartitionDataLossAsync() chamada.</span><span class="sxs-lookup"><span data-stu-id="ce10a-106">You can invoke data loss on a partition of your Service Fabric Service by calling StartPartitionDataLossAsync().</span></span>  <span data-ttu-id="ce10a-107">Esta api utiliza Olá Injeção de falhas e Analysis Service tooperform Olá trabalho toocause perda condições de dados.</span><span class="sxs-lookup"><span data-stu-id="ce10a-107">This api uses hello Fault Injection and Analysis Service tooperform hello work toocause data loss conditions.</span></span>

## <a name="using-hello-fault-injection-and-analysis-service"></a><span data-ttu-id="ce10a-108">Utilizar Olá Injeção de falhas e Analysis Service</span><span class="sxs-lookup"><span data-stu-id="ce10a-108">Using hello Fault Injection and Analysis Service</span></span>
<span data-ttu-id="ce10a-109">Olá Injeção de falhas e o serviço de análise suporta atualmente Olá seguir APIs no gráfico de Olá abaixo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-109">hello Fault Injection and Analysis Service currently supports hello following APIs in hello chart below.</span></span>  <span data-ttu-id="ce10a-110">Olá direita do gráfico Olá mostra Olá cmdlet do PowerShell correspondente.</span><span class="sxs-lookup"><span data-stu-id="ce10a-110">hello right side of hello chart shows hello corresponding PowerShell cmdlet.</span></span>  <span data-ttu-id="ce10a-111">Para mais informações sobre cada um deles, consulte documentação de msdn toohello em cada API.</span><span class="sxs-lookup"><span data-stu-id="ce10a-111">Please refer toohello msdn documentation on each API for more information on each one.</span></span>

| <span data-ttu-id="ce10a-112">API C#</span><span class="sxs-lookup"><span data-stu-id="ce10a-112">C# API</span></span> | <span data-ttu-id="ce10a-113">Cmdlet do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ce10a-113">PowerShell Cmdlet</span></span> |
| --- | ---:|
| <span data-ttu-id="ce10a-114">[StartPartitionDataLossAsync][dl]</span><span class="sxs-lookup"><span data-stu-id="ce10a-114">[StartPartitionDataLossAsync][dl]</span></span> |<span data-ttu-id="ce10a-115">[Início ServiceFabricPartitionDataLoss][psdl]</span><span class="sxs-lookup"><span data-stu-id="ce10a-115">[Start-ServiceFabricPartitionDataLoss][psdl]</span></span> |
| <span data-ttu-id="ce10a-116">[StartPartitionQuorumLossAsync][ql]</span><span class="sxs-lookup"><span data-stu-id="ce10a-116">[StartPartitionQuorumLossAsync][ql]</span></span> |<span data-ttu-id="ce10a-117">[Início ServiceFabricPartitionQuorumLoss][psql]</span><span class="sxs-lookup"><span data-stu-id="ce10a-117">[Start-ServiceFabricPartitionQuorumLoss][psql]</span></span> |
| <span data-ttu-id="ce10a-118">[StartPartitionRestartAsync][rp]</span><span class="sxs-lookup"><span data-stu-id="ce10a-118">[StartPartitionRestartAsync][rp]</span></span> |<span data-ttu-id="ce10a-119">[Início ServiceFabricPartitionRestart][psrp]</span><span class="sxs-lookup"><span data-stu-id="ce10a-119">[Start-ServiceFabricPartitionRestart][psrp]</span></span> |

## <a name="conceptual-overview-of-running-a-command"></a><span data-ttu-id="ce10a-120">Descrição geral concetual de um comando em execução</span><span class="sxs-lookup"><span data-stu-id="ce10a-120">Conceptual Overview of Running a Command</span></span>
<span data-ttu-id="ce10a-121">Olá Injeção de falhas e Analysis Service utiliza um modelo assíncrono onde deve começar Olá comando com uma API, referido tooas Olá "Start" API neste documento, em seguida, verificações Olá progresso deste comando com uma API de "GetProgress" até atingiu um terminal Estado, ou até cancelá-lo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-121">hello Fault Injection and Analysis Service uses an asynchronous model where you start hello command with one API, referred tooas hello “Start” API in this document, then checks hello progress of this command using a “GetProgress” API until it has reached a terminal state, or until you cancel it.</span></span>
<span data-ttu-id="ce10a-122">toostart um comando, chamar a API de "Iniciar" Olá para API correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="ce10a-122">toostart a command, call hello “Start” API for hello corresponding API.</span></span>  <span data-ttu-id="ce10a-123">Esta API devolve quando hello Injeção de falhas e Analysis Service aceitou o pedido de Olá.</span><span class="sxs-lookup"><span data-stu-id="ce10a-123">This API returns when hello Fault Injection and Analysis Service has accepted hello request.</span></span>  <span data-ttu-id="ce10a-124">No entanto, isto não indicar até que ponto foi executado um comando, ou mesmo que o se ainda foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-124">However, it does not indicate how far a command has run, or even if it has started yet.</span></span>  <span data-ttu-id="ce10a-125">Em curso toocheck de ordem de um comando, chame Olá "GetProgress" API que corresponde ao toohello "Start" API anteriormente denominada.</span><span class="sxs-lookup"><span data-stu-id="ce10a-125">In order toocheck progress of a command, call hello “GetProgress” API that corresponds toohello “Start” API previously called.</span></span>  <span data-ttu-id="ce10a-126">Olá "GetProgress" API irá devolver um objeto que indica o estado atual do Olá do comando de Olá dentro da respetiva propriedade de estado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-126">hello “GetProgress” API will return an object indicating hello current status of hello command inside its State property.</span></span>  <span data-ttu-id="ce10a-127">Executa um comando indefinidamente até:</span><span class="sxs-lookup"><span data-stu-id="ce10a-127">A command runs indefinitely until:</span></span>

1. <span data-ttu-id="ce10a-128">Se for concluída com êxito.</span><span class="sxs-lookup"><span data-stu-id="ce10a-128">It completes successfully.</span></span>  <span data-ttu-id="ce10a-129">Se chamar "GetProgress" no mesmo neste caso, o estado do objeto de progresso Olá vai ser concluído.</span><span class="sxs-lookup"><span data-stu-id="ce10a-129">If you call “GetProgress” on it in this case, hello progress object’s State will be Completed.</span></span>
2. <span data-ttu-id="ce10a-130">Encontrar um erro fatal.</span><span class="sxs-lookup"><span data-stu-id="ce10a-130">It encounters a fatal error.</span></span>  <span data-ttu-id="ce10a-131">Se chamar "GetProgress" no mesmo neste caso, o estado do objeto de progresso Olá irá falhar</span><span class="sxs-lookup"><span data-stu-id="ce10a-131">If you call “GetProgress” on it in this case, hello progress object’s State will be Faulted</span></span>
3. <span data-ttu-id="ce10a-132">Cancelá-lo através de Olá [CancelTestCommandAsync] [ cancel] API, ou [Stop-ServiceFabricTestCommand] [ cancelps] cmdlet do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ce10a-132">You cancel it through hello [CancelTestCommandAsync][cancel] API, or [Stop-ServiceFabricTestCommand][cancelps] PowerShell cmdlet.</span></span>  <span data-ttu-id="ce10a-133">Se chamar "GetProgress" no mesmo neste caso, hello estado do objeto de progresso será cancelada ou ForceCancelled, consoante toothat um argumento API.</span><span class="sxs-lookup"><span data-stu-id="ce10a-133">If you call “GetProgress” on it in this case, hello progress object’s State will be either Cancelled or ForceCancelled, depending on an argument toothat API.</span></span>  <span data-ttu-id="ce10a-134">Consulte a documentação de Olá para [CancelTestCommandAsync] [ cancel] para obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ce10a-134">See hello documentation for [CancelTestCommandAsync][cancel] for more details.</span></span>

## <a name="details-of-running-a-command"></a><span data-ttu-id="ce10a-135">Detalhes de um comando em execução</span><span class="sxs-lookup"><span data-stu-id="ce10a-135">Details of Running a Command</span></span>
<span data-ttu-id="ce10a-136">Na ordem toostart um comando, chame Olá iniciar API com argumentos de Olá esperado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-136">In order toostart a command, call hello Start API with hello expected arguments.</span></span>  <span data-ttu-id="ce10a-137">Todos os APIs de começar a ter um argumento de Guid denominado operationId.</span><span class="sxs-lookup"><span data-stu-id="ce10a-137">All Start APIs have a Guid argument named operationId.</span></span>  <span data-ttu-id="ce10a-138">Deve manter registo do argumento de operationId Olá, uma vez que é utilizado tootrack progresso deste comando.</span><span class="sxs-lookup"><span data-stu-id="ce10a-138">You should keep track of hello operationId argument, since it is used tootrack progress of this command.</span></span>  <span data-ttu-id="ce10a-139">Isto deve ser transmitido Olá "GetProgress" API em curso de tootrack ordem do comando de Olá.</span><span class="sxs-lookup"><span data-stu-id="ce10a-139">This must be passed into hello “GetProgress” API in order tootrack progress of hello command.</span></span>  <span data-ttu-id="ce10a-140">Olá operationId tem de ser exclusivo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-140">hello operationId must be unique.</span></span>

<span data-ttu-id="ce10a-141">Depois de chamar com êxito Olá iniciar API, Olá GetProgress API deve ser chamado num ciclo até Olá devolveu o progresso da propriedade de estado do objeto está concluída.</span><span class="sxs-lookup"><span data-stu-id="ce10a-141">After successfully calling hello Start API, hello GetProgress API should be called in a loop until hello returned progress object’s State property is Completed.</span></span>  <span data-ttu-id="ce10a-142">Todos os [do FabricTransientException] [ fte] e OperationCanceledException deve ser repetida.</span><span class="sxs-lookup"><span data-stu-id="ce10a-142">All [FabricTransientException’s][fte] and OperationCanceledException’s should be retried.</span></span>
<span data-ttu-id="ce10a-143">Quando o comando de Olá atingiu um Estado terminal (concluído, Faulted ou cancelada), Olá devolveu a propriedade de resultado do objeto de progresso tem informações adicionais.</span><span class="sxs-lookup"><span data-stu-id="ce10a-143">When hello command has reached a terminal state (Completed, Faulted, or Cancelled), hello returned progress object’s Result property will have additional information.</span></span>  <span data-ttu-id="ce10a-144">Se o estado de Olá estiver concluído, Result.SelectedPartition.PartitionId irá conter o id de partição Olá que foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-144">If hello state is Completed, Result.SelectedPartition.PartitionId will contain hello partition id that was selected.</span></span>  <span data-ttu-id="ce10a-145">Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-145">Result.Exception will be null.</span></span>  <span data-ttu-id="ce10a-146">Se o estado de Olá falhou, Result.Exception terão Olá de razão Olá Injeção de falhas e ocorreram falhas no serviço do Analysis Services Olá comando.</span><span class="sxs-lookup"><span data-stu-id="ce10a-146">If hello state is Faulted, Result.Exception will have hello reason hello Fault Injection and Analysis Service faulted hello command.</span></span>  <span data-ttu-id="ce10a-147">Result.SelectedPartition.PartitionId terá um id de partição Olá que foi selecionado.</span><span class="sxs-lookup"><span data-stu-id="ce10a-147">Result.SelectedPartition.PartitionId will have hello partition id that was selected.</span></span>  <span data-ttu-id="ce10a-148">Em algumas situações, o comando de Olá poderá não ter proceeded até que ponto suficiente toochoose uma partição.</span><span class="sxs-lookup"><span data-stu-id="ce10a-148">In some situations, hello command may not have proceeded far enough toochoose a partition.</span></span>  <span data-ttu-id="ce10a-149">Nesse caso, Olá PartitionId será 0.</span><span class="sxs-lookup"><span data-stu-id="ce10a-149">In that case, hello PartitionId will be 0.</span></span>  <span data-ttu-id="ce10a-150">Se o estado de Olá foi cancelado, Result.Exception será nulo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-150">If hello state is Cancelled, Result.Exception will be null.</span></span>  <span data-ttu-id="ce10a-151">Como Olá Faulted caso, Result.SelectedPartition.PartitionId terá um id de partição de Olá foi escolhido, mas se o comando de Olá não tem proceeded até que ponto suficiente toodo por isso, será 0.</span><span class="sxs-lookup"><span data-stu-id="ce10a-151">Like hello Faulted case, Result.SelectedPartition.PartitionId will have hello partition id that was chosen, but if hello command has not proceeded far enough toodo so, it will be 0.</span></span>  <span data-ttu-id="ce10a-152">Consulte também toohello exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="ce10a-152">Please also refer toohello sample below.</span></span>

<span data-ttu-id="ce10a-153">código de exemplo de Olá abaixo mostra como toostart, em seguida, verificar progresso na perda de dados de toocause comando numa partição específica.</span><span class="sxs-lookup"><span data-stu-id="ce10a-153">hello sample code below shows how toostart then check progress on a command toocause data loss on a specific partition.</span></span>

```csharp
    static async Task PerformDataLossSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/MyService");

        // hello id of hello target partition inside hello target service
        Guid targetPartitionId = new Guid("00000000-0000-0000-0000-000002233445");

        PartitionSelector partitionSelector = PartitionSelector.PartitionIdOf(targetServiceName, targetPartitionId);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.        

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                // In a terminal state .Result.SelectedPartition.PartitionId will have hello chosen partition
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);
                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}'", operationId, progress.Result.Exception);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(5.0d)).ConfigureAwait(false);
        }
    }
```

<span data-ttu-id="ce10a-154">exemplo de Olá abaixo mostra como toouse Olá PartitionSelector toochoose uma partição aleatória de um serviço especificado:</span><span class="sxs-lookup"><span data-stu-id="ce10a-154">hello sample below shows how toouse hello PartitionSelector toochoose a random partition of a specified service:</span></span>

```csharp
    static async Task PerformDataLossUseSelectorSample()
    {
        // Create a unique operation id for hello command below
        Guid operationId = Guid.NewGuid();

        // Note: Use hello appropriate overload for your configuration
        FabricClient fabricClient = new FabricClient();

        // hello name of hello target service
        Uri targetServiceName = new Uri("fabric:/SampleService ");

        // Use a PartitionSelector that will have hello Fault Injection and Analysis Service choose a random partition of “targetServiceName”
        PartitionSelector partitionSelector = PartitionSelector.RandomOf(targetServiceName);

        // Start hello command.  Retry OperationCanceledException and all FabricTransientException's.  Note when StartPartitionDataLossAsync completes
        // successfully it only means hello Fault Injection and Analysis Service has saved hello intent tooperform this work.  It does not say anything about hello progress
        // of hello command.
        while (true)
        {
            try
            {
                await fabricClient.TestManager.StartPartitionDataLossAsync(operationId, partitionSelector, DataLossMode.FullDataLoss).ConfigureAwait(false);
                break;
            }
            catch (OperationCanceledException)
            {
            }
            catch (FabricTransientException)
            {
            }
            catch (Exception e)
            {
                Console.WriteLine("Unexpected exception '{0}'", e);
                throw;
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }

        PartitionDataLossProgress progress = null;

        // Poll hello progress using GetPartitionDataLossProgressAsync until it is either Completed or Faulted.  In this example, we're assuming
        // hello command won't be cancelled.

        while (true)
        {
            try
            {
                progress = await fabricClient.TestManager.GetPartitionDataLossProgressAsync(operationId).ConfigureAwait(false);
            }
            catch (OperationCanceledException)
            {
                continue;
            }
            catch (FabricTransientException)
            {
                continue;
            }

            if (progress.State == TestCommandProgressState.Completed)
            {
                Console.WriteLine("Command '{0}' completed successfully", operationId);

                Console.WriteLine("Printing progress.Result:");
                Console.WriteLine("  Printing selected partition='{0}'", progress.Result.SelectedPartition.PartitionId);

                break;
            }
            else if (progress.State == TestCommandProgressState.Faulted)
            {
                // If State is Faulted, hello progress object's Result property's Exception property will have hello reason why.
                Console.WriteLine("Command '{0}' failed with '{1}', SelectedPartition {2}", operationId, progress.Result.Exception, progress.Result.SelectedPartition);
                break;
            }
            else
            {
                Console.WriteLine("Command '{0}' is currently Running", operationId);
            }

            await Task.Delay(TimeSpan.FromSeconds(1.0d)).ConfigureAwait(false);
        }
    }
```

## <a name="history-and-truncation"></a><span data-ttu-id="ce10a-155">Histórico e truncagem</span><span class="sxs-lookup"><span data-stu-id="ce10a-155">History and Truncation</span></span>
<span data-ttu-id="ce10a-156">Depois de um comando atingiu um Estado terminal, os metadados irão permanecer na Olá Injeção de falhas e Analysis Service para um determinado período de tempo, antes de será removido toosave espaço.</span><span class="sxs-lookup"><span data-stu-id="ce10a-156">After a command has reached a terminal state, its metadata will remain in hello Fault Injection and Analysis Service for a certain time, before it will be removed toosave space.</span></span>  <span data-ttu-id="ce10a-157">Se "GetProgress" é chamado utilizando Olá operationId de um comando depois de serem removido, devolverá uma FabricException com um código de erro KeyNotFound.</span><span class="sxs-lookup"><span data-stu-id="ce10a-157">If “GetProgress” is called using hello operationId of a command after it has been removed, it will return a FabricException with an ErrorCode of KeyNotFound.</span></span>

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
