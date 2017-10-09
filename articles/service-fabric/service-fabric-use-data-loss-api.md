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
# <a name="how-tooinvoke-data-loss-on-services"></a>Como tooInvoke perda de dados nos serviços
> [!WARNING]
> Este documento descrevem como toocause perda de dados nos serviços e deve ser utilizado com cuidado.
> 
> 

## <a name="introduction"></a>Introdução
Pode invocar perda de dados numa partição do seu serviço de recursos de infraestrutura de serviço por StartPartitionDataLossAsync() chamada.  Esta api utiliza Olá Injeção de falhas e Analysis Service tooperform Olá trabalho toocause perda condições de dados.

## <a name="using-hello-fault-injection-and-analysis-service"></a>Utilizar Olá Injeção de falhas e Analysis Service
Olá Injeção de falhas e o serviço de análise suporta atualmente Olá seguir APIs no gráfico de Olá abaixo.  Olá direita do gráfico Olá mostra Olá cmdlet do PowerShell correspondente.  Para mais informações sobre cada um deles, consulte documentação de msdn toohello em cada API.

| API C# | Cmdlet do PowerShell |
| --- | ---:|
| [StartPartitionDataLossAsync][dl] |[Início ServiceFabricPartitionDataLoss][psdl] |
| [StartPartitionQuorumLossAsync][ql] |[Início ServiceFabricPartitionQuorumLoss][psql] |
| [StartPartitionRestartAsync][rp] |[Início ServiceFabricPartitionRestart][psrp] |

## <a name="conceptual-overview-of-running-a-command"></a>Descrição geral concetual de um comando em execução
Olá Injeção de falhas e Analysis Service utiliza um modelo assíncrono onde deve começar Olá comando com uma API, referido tooas Olá "Start" API neste documento, em seguida, verificações Olá progresso deste comando com uma API de "GetProgress" até atingiu um terminal Estado, ou até cancelá-lo.
toostart um comando, chamar a API de "Iniciar" Olá para API correspondente Olá.  Esta API devolve quando hello Injeção de falhas e Analysis Service aceitou o pedido de Olá.  No entanto, isto não indicar até que ponto foi executado um comando, ou mesmo que o se ainda foi iniciado.  Em curso toocheck de ordem de um comando, chame Olá "GetProgress" API que corresponde ao toohello "Start" API anteriormente denominada.  Olá "GetProgress" API irá devolver um objeto que indica o estado atual do Olá do comando de Olá dentro da respetiva propriedade de estado.  Executa um comando indefinidamente até:

1. Se for concluída com êxito.  Se chamar "GetProgress" no mesmo neste caso, o estado do objeto de progresso Olá vai ser concluído.
2. Encontrar um erro fatal.  Se chamar "GetProgress" no mesmo neste caso, o estado do objeto de progresso Olá irá falhar
3. Cancelá-lo através de Olá [CancelTestCommandAsync] [ cancel] API, ou [Stop-ServiceFabricTestCommand] [ cancelps] cmdlet do PowerShell.  Se chamar "GetProgress" no mesmo neste caso, hello estado do objeto de progresso será cancelada ou ForceCancelled, consoante toothat um argumento API.  Consulte a documentação de Olá para [CancelTestCommandAsync] [ cancel] para obter mais detalhes.

## <a name="details-of-running-a-command"></a>Detalhes de um comando em execução
Na ordem toostart um comando, chame Olá iniciar API com argumentos de Olá esperado.  Todos os APIs de começar a ter um argumento de Guid denominado operationId.  Deve manter registo do argumento de operationId Olá, uma vez que é utilizado tootrack progresso deste comando.  Isto deve ser transmitido Olá "GetProgress" API em curso de tootrack ordem do comando de Olá.  Olá operationId tem de ser exclusivo.

Depois de chamar com êxito Olá iniciar API, Olá GetProgress API deve ser chamado num ciclo até Olá devolveu o progresso da propriedade de estado do objeto está concluída.  Todos os [do FabricTransientException] [ fte] e OperationCanceledException deve ser repetida.
Quando o comando de Olá atingiu um Estado terminal (concluído, Faulted ou cancelada), Olá devolveu a propriedade de resultado do objeto de progresso tem informações adicionais.  Se o estado de Olá estiver concluído, Result.SelectedPartition.PartitionId irá conter o id de partição Olá que foi selecionado.  Result.Exception será nulo.  Se o estado de Olá falhou, Result.Exception terão Olá de razão Olá Injeção de falhas e ocorreram falhas no serviço do Analysis Services Olá comando.  Result.SelectedPartition.PartitionId terá um id de partição Olá que foi selecionado.  Em algumas situações, o comando de Olá poderá não ter proceeded até que ponto suficiente toochoose uma partição.  Nesse caso, Olá PartitionId será 0.  Se o estado de Olá foi cancelado, Result.Exception será nulo.  Como Olá Faulted caso, Result.SelectedPartition.PartitionId terá um id de partição de Olá foi escolhido, mas se o comando de Olá não tem proceeded até que ponto suficiente toodo por isso, será 0.  Consulte também toohello exemplo abaixo.

código de exemplo de Olá abaixo mostra como toostart, em seguida, verificar progresso na perda de dados de toocause comando numa partição específica.

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

exemplo de Olá abaixo mostra como toouse Olá PartitionSelector toochoose uma partição aleatória de um serviço especificado:

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

## <a name="history-and-truncation"></a>Histórico e truncagem
Depois de um comando atingiu um Estado terminal, os metadados irão permanecer na Olá Injeção de falhas e Analysis Service para um determinado período de tempo, antes de será removido toosave espaço.  Se "GetProgress" é chamado utilizando Olá operationId de um comando depois de serem removido, devolverá uma FabricException com um código de erro KeyNotFound.

[dl]: https://msdn.microsoft.com/library/azure/mt693569.aspx
[ql]: https://msdn.microsoft.com/library/azure/mt693558.aspx
[rp]: https://msdn.microsoft.com/library/azure/mt645056.aspx
[psdl]: https://msdn.microsoft.com/library/mt697573.aspx
[psql]: https://msdn.microsoft.com/library/mt697557.aspx
[psrp]: https://msdn.microsoft.com/library/mt697560.aspx
[cancel]: https://msdn.microsoft.com/library/azure/mt668910.aspx
[cancelps]: https://msdn.microsoft.com/library/mt697566.aspx
[fte]: https://msdn.microsoft.com/library/azure/system.fabric.fabrictransientexception.aspx
