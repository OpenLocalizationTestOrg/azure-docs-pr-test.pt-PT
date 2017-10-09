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
# <a name="testability-actions"></a>Ações de teste
Na ordem toosimulate uma infraestrutura pouco fiável, Azure Service Fabric fornece, programador Olá, com formas toosimulate várias falhas do mundo real e transições de estado. Estes são expostos como ações de teste. ações de Olá são Olá APIs de baixo nível que fazer com que uma inserção de falhas específicas, transição de estado ou validação. Ao combinar estas ações, pode escrever cenários de teste abrangente para os serviços.

O Service Fabric fornece que alguns cenários comuns de teste é composto por estas ações. Recomendamos vivamente que utilizam estes cenários incorporados, que são escolhidos cuidadosamente tootest transições de estado comum e cenários de falha. No entanto, ações podem ser utilizados toocreate cenários de teste personalizado quando quiser tooadd cobertura para cenários que não são abrangidos por cenários incorporada Olá ainda ou que são personalizados adaptados para a sua aplicação.

C# implementações das ações de Olá encontram Olá System.Fabric.dll assemblagem. módulo do PowerShell de recursos de infraestrutura de sistema Olá encontra-se no Olá Microsoft.ServiceFabric.Powershell.dll assemblagem. Como parte da instalação de tempo de execução, Olá módulo ServiceFabric PowerShell é instalado tooallow facilidade de utilização.

## <a name="graceful-vs-ungraceful-fault-actions"></a>Correto vs ações ungraceful falhas
Ações de teste são classificadas em dois registos principais:

* Falhas ungraceful: estas falhas simular falhas como reinícios da máquina e de falhas de processos. Nestes casos de falhas, contexto de execução de Olá do processo interrompe abruptamente. Isto significa que nenhum limpeza do Estado de Olá pode executar antes de aplicação Olá começa novamente.
* Falhas correto: estas falhas simulam correto ações como move de réplica e remoções acionadas por balanceamento de carga. Nestes casos, o serviço de Olá obtém uma notificação de Olá fechar e pode limpar estado Olá antes de sair.

Para melhor validação da qualidade, executar o serviço de Olá e carga de trabalho do negócio ao inducing várias falhas ungraceful e correto. Falhas ungraceful exercer cenários em que o processo de serviço de Olá sai abruptamente no meio de Olá de algumas fluxo de trabalho. Isto testa o caminho de recuperação Olá assim que a réplica do serviço de Olá é restaurada pelo Service Fabric. Isto irá ajudar a testar a consistência dos dados e se o estado de serviço de Olá é mantido corretamente após falhas. Olá outro conjunto de falhas (Olá correto de falhas) de teste que o serviço de Olá reage corretamente tooreplicas que está a ser movidos em torno do Service Fabric. Isto testa o processamento de cancelamento no método runasync com de Olá. serviço de Olá necessita toocheck para Olá cancelamento token que está a ser definido, corretamente guardar o estado e sair do método runasync com de Olá.

## <a name="testability-actions-list"></a>Lista de ações de teste
| Ação | Descrição | API gerido | Cmdlet do PowerShell | Falhas correto/ungraceful |
| --- | --- | --- | --- | --- |
| CleanTestState |Remove todos os Estados de teste de Olá cluster Olá em caso de um encerramento incorreto de controlador de teste de Olá. |CleanTestStateAsync |Remove-ServiceFabricTestState |Não aplicável |
| InvokeDataLoss |Induces perda de dados para uma partição de serviço. |InvokeDataLossAsync |Invoke-ServiceFabricPartitionDataLoss |Correto |
| InvokeQuorumLoss |Coloca uma partição de serviço com estado fornecido no perda de quórum. |InvokeQuorumLossAsync |ServiceFabricQuorumLoss invocar |Correto |
| Mover primário |Move Olá especificado réplica primária de um nó de cluster especificado do serviço com estado toohello. |MovePrimaryAsync |Mover ServiceFabricPrimaryReplica |Correto |
| Mover secundário |Move a réplica secundária atual Olá um serviço com estado tooa diferente do nó do cluster. |MoveSecondaryAsync |Mover ServiceFabricSecondaryReplica |Correto |
| RemoveReplica |Simula uma falha de réplica ao remover uma réplica de um cluster. Isto irá fechar réplica Olá e irão transitar-toorole 'None', removendo todos os Estado do cluster de Olá. |RemoveReplicaAsync |Remover ServiceFabricReplica |Correto |
| RestartDeployedCodePackage |Simula uma falha de processo de pacote do código reiniciando um pacote do código implementado num nó num cluster. Isto interrompe o processo de pacote do Olá código, que será reiniciado todas as réplicas de serviço do utilizador Olá alojadas no processo. |RestartDeployedCodePackageAsync |ServiceFabricDeployedCodePackage de reinício |Ungraceful |
| RestartNode |Simula uma falha de nó de cluster do Service Fabric reiniciando um nó. |RestartNodeAsync |ServiceFabricNode de reinício |Ungraceful |
| RestartPartition |Simula um cenário de blackout datacenter blackout ou cluster reiniciando algumas ou todas as réplicas de uma partição. |RestartPartitionAsync |Restart-ServiceFabricPartition |Correto |
| RestartReplica |Simula uma falha de réplica ao reiniciar uma réplica persistente num cluster, réplica Olá a fechar e, em seguida, abri-lo. |RestartReplicaAsync |ServiceFabricReplica de reinício |Correto |
| StartNode |Inicia um nó num cluster que já é parado. |StartNodeAsync |Start-ServiceFabricNode |Não aplicável |
| StopNode |Simula uma falha de nó por parar um nó num cluster. nó de Olá permanecerão para baixo até StartNode é chamado. |StopNodeAsync |Stop-ServiceFabricNode |Ungraceful |
| ValidateApplication |Valida Olá disponibilidade e o estado de funcionamento de todos os serviços do Service Fabric dentro de uma aplicação, normalmente, após inducing algumas falhas no sistema de Olá. |ValidateApplicationAsync |Teste ServiceFabricApplication |Não aplicável |
| ValidateService |Valida Olá disponibilidade e o estado de funcionamento de um serviço do Service Fabric, geralmente após inducing algumas falhas no sistema de Olá. |ValidateServiceAsync |Teste ServiceFabricService |Não aplicável |

## <a name="running-a-testability-action-using-powershell"></a>Execução de uma ação de teste com o PowerShell
Este tutorial mostra como toorun uma ação de teste utilizando o PowerShell. Ficará a saber como toorun uma ação de teste contra um cluster (uma caixa) local ou um cluster do Azure. Microsoft.Fabric.Powershell.dll – hello módulo do PowerShell de Service Fabric – é instalada automaticamente ao instalar Olá MSI de recursos de infraestrutura de serviço do Microsoft. módulo Olá é carregado automaticamente quando abrir uma linha de comandos do PowerShell.

Tutorial segmentos:

* [Executar uma ação contra um cluster de um caixa](#run-an-action-against-a-one-box-cluster)
* [Executar uma ação contra um cluster do Azure](#run-an-action-against-an-azure-cluster)

### <a name="run-an-action-against-a-one-box-cluster"></a>Executar uma ação contra um cluster de um caixa
toorun uma ação de teste contra um cluster local, ligam pela primeira vez toohello cluster e o pedido de PowerShell Olá aberto no modo de administrador. Informe-nos observar Olá **reinício ServiceFabricNode** ação.

```powershell
Restart-ServiceFabricNode -NodeName Node1 -CompletionMode DoNotVerify
```

Aqui Olá ação **reinício ServiceFabricNode** está a ser executado num nó com o nome "Nó1". modo de conclusão de Olá Especifica que este deve não verificar se ação de reinício do nó de Olá, na verdade, foi concluída com êxito. Modo de conclusão de Olá especificação como "Verificar" fará com que este tooverify se a ação de reinício de Olá, na verdade, foi concluída com êxito. Em vez de especificar diretamente nó Olá pelo respetivo nome, pode especificá-la através de um tipo de chave e Olá de partição de réplica, da seguinte forma:

```powershell
Restart-ServiceFabricNode -ReplicaKindPrimary  -PartitionKindNamed -PartitionKey Partition3 -CompletionMode Verify
```


```powershell
$connection = "localhost:19000"
$nodeName = "Node1"

Connect-ServiceFabricCluster $connection
Restart-ServiceFabricNode -NodeName $nodeName -CompletionMode DoNotVerify
```

**Reinício ServiceFabricNode** deve ser um nó de Service Fabric num cluster toorestart utilizado. Isto irá parar o processo de Fabric.exe Olá, o que irá reiniciar todos os Olá sistema serviço e o utilizador serviço réplicas alojadas nesse nó. Este tootest de API a utilizar o serviço de ajuda-o desvendar erros ao longo de caminhos de recuperação de ativação pós-falha de Olá. Ajuda a simular falhas de nó no cluster de Olá.

Olá seguinte captura de ecrã mostra Olá **reinício ServiceFabricNode** comando de teste em ação.

![](media/service-fabric-testability-actions/Restart-ServiceFabricNode.png)

Olá primeiro de saída de Olá **Get-ServiceFabricNode** (um cmdlet do módulo do PowerShell de Service Fabric de Olá) mostra esse cluster local Olá com cinco nós: Node.1 tooNode.5. Após a ação de teste de Olá (cmdlet) **reinício ServiceFabricNode** é executada num nó de Olá, com o nome Node.4, vemos disponibilidade nesse nó Olá foi reposta.

### <a name="run-an-action-against-an-azure-cluster"></a>Executar uma ação contra um cluster do Azure
Execução de uma ação de teste (utilizando o PowerShell) contra um cluster do Azure é semelhante toorunning Olá contra um cluster local. Olá apenas diferença é que, antes de poder executar a ação de Olá, em vez de estabelecer ligação toohello cluster local, terá de tooconnect toohello Azure cluster primeiro.

## <a name="running-a-testability-action-using-c35"></a>Execução de uma ação de teste com C &#35;
toorun uma ação de teste ao utilizar c#, primeiro tem de tooconnect toohello cluster utilizando FabricClient. Em seguida, obter Olá parâmetros necessários toorun Olá ação. Parâmetros diferentes podem ser utilizados toorun Olá a mesma ação.
Observar Olá RestartServiceFabricNode ação, toorun unidirecional é através da utilização de informações do nó de Olá (nome de nó e o ID de instância do nó) no cluster de Olá.

```csharp
RestartNodeAsync(nodeName, nodeInstanceId, completeMode, operationTimeout, CancellationToken.None)
```

Explicação de parâmetro:

* **CompleteMode** especifica de que modo Olá não deve verificar se ação de reinício de Olá, na verdade, foi concluída com êxito. Modo de conclusão de Olá especificação como "Verificar" fará com que este tooverify se a ação de reinício de Olá, na verdade, foi concluída com êxito.  
* **OperationTimeout** conjuntos Olá quantidade de tempo para Olá operação toofinish antes de que é emitida uma exceção de TimeoutException.
* **CancellationToken** permite um toobe chamada pendente cancelada.

Em vez de especificar diretamente nó Olá pelo respetivo nome, pode especificá-la através de um tipo de chave e Olá de partição de réplica.

Para obter mais informações, consulte [PartitionSelector e ReplicaSelector](#partition_replica_selector).

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

## <a name="partitionselector-and-replicaselector"></a>PartitionSelector e ReplicaSelector
### <a name="partitionselector"></a>PartitionSelector
PartitionSelector é um programa auxiliar exposta no teste e é utilizado tooselect específico de partição na qual tooperform qualquer uma das ações de teste de Olá. Pode ser utilizado tooselect uma partição específica se o ID de partição Olá é conhecido previamente. Em alternativa, pode fornecer a chave de partição Olá e operação Olá irá resolver o ID de partição Olá internamente. Tem também a opção Olá da seleção de uma partição aleatória.

toouse esta ajuda, criar Olá PartitionSelector objeto e selecione o partição Olá utilizando um dos métodos de Olá selecione *. Então, passe no Olá PartitionSelector objeto toohello API que obriga. Se nenhuma opção for selecionada, assume partição aleatório tooa.

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

### <a name="replicaselector"></a>ReplicaSelector
ReplicaSelector é um programa auxiliar exposta no teste e é utilizado toohelp selecionar uma réplica no qual tooperform qualquer uma das ações de teste de Olá. Pode ser utilizado tooselect uma réplica específica se o ID de réplica Olá é conhecido previamente. Além disso, terá de opção de Olá da seleção de uma réplica primária ou secundária aleatória. ReplicaSelector deriva de PartitionSelector, por isso terá de tooselect ambos Olá partição de réplica e Olá no qual pretende a operação de teste de Olá tooperform.

toouse esta ajuda, crie um objeto de ReplicaSelector e defina Olá gosta tooselect de partição de réplica e Olá de Olá. Em seguida, pode passar para Olá API que obriga. Se nenhuma opção for selecionada, assume réplica aleatório tooa e partição aleatória.

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

## <a name="next-steps"></a>Passos seguintes
* [Cenários de teste](service-fabric-testability-scenarios.md)
* Como tootest seu serviço
  * [Simular falhas durante a cargas de trabalho do serviço](service-fabric-testability-workload-tests.md)
  * [Falhas de comunicação de serviço de serviço](service-fabric-testability-scenarios-service-communication.md)

