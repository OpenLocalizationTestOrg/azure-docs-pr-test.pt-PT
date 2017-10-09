---
title: "aaaAzure dimensionamento programática do Service Fabric | Microsoft Docs"
description: "Um cluster do Azure Service Fabric entrada ou saída de escala através de programação, de acordo com os acionadores de toocustom"
services: service-fabric
documentationcenter: .net
author: mjrousos
manager: jonjung
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/29/2017
ms.author: mikerou
ms.openlocfilehash: a0c6499b1a143a173006248cf8a15380632637e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="scale-a-service-fabric-cluster-programmatically"></a>Dimensionar um cluster do Service Fabric através de programação 

Noções básicas de dimensionamento de um cluster do Service Fabric no Azure são abrangidas na documentação no [dimensionamento de clusters](./service-fabric-cluster-scale-up-down.md). Este artigo abrange como clusters de Service Fabric assentes em conjuntos de dimensionamento de máquina virtual e podem ser ampliadas manualmente ou com regras de dimensionamento automático. Este documento observa programáticos métodos de coordenação Azure dimensionamento operações para cenários mais avançados. 

## <a name="reasons-for-programmatic-scaling"></a>Razões para dimensionamento programático
Em vários cenários, dimensionar manualmente ou através de regras de dimensionamento automático é boas soluções. Noutros cenários, no entanto, estes podem não ser Olá ajustar à direita. Abordagens de toothese desvantagens potenciais incluem:

- Dimensionar Manualmente requer toolog no e explicitamente o pedido de dimensionamento de operações. Se operações de dimensionamento forem necessárias com frequência, ou em alturas imprevisíveis, esta abordagem não pode ser uma boa solução.
- Quando as regras de dimensionamento automático remover uma instância de um conjunto de dimensionamento de máquina virtual, estes não remove automaticamente dados de conhecimento desse nó de cluster do Service Fabric Olá associado, a menos que tipo de nó Olá tem um nível de durabilidade de Silver ou Gold. Porque as regras de dimensionamento automático funcionam em escala Olá definido ao nível (em vez de em Olá nível de Service Fabric), as regras de dimensionamento automático podem remover nós de Service Fabric sem encerrado-las sem problemas. Esta remoção de nó grosseiro sair "fantasma" Estado do nó de Service Fabric após operações de escala. Uma pessoa (ou um serviço), seria necessário tooperiodically Limpar estado do nó removido no cluster do Service Fabric Olá.
  - Tenha em atenção que um tipo de nó com um nível de durabilidade de ouro ou Silver irá limpar automaticamente remover nós.  
- Apesar de existirem [métricas muitos](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) suportado pelas regras de dimensionamento automático, é ainda um conjunto limitado. Se o seu cenário chama-se em algum métrica não abrangida desse conjunto de dimensionamento, em seguida, as regras de dimensionamento automático não podem ser uma boa opção.

Com base nestas limitações, pode ser útil tooimplement mais personalizados Automáticos dimensionamento modelos. 

## <a name="scaling-apis"></a>APIs de dimensionamento
As APIs do Azure existem que permitem que aplicações tooprogrammatically trabalho com conjuntos de dimensionamento de máquina virtual e clusters de Service Fabric. Se as opções de dimensionamento automático existente não funcionam para o seu cenário, estas APIs tornam possível tooimplement lógica de dimensionamento personalizada. 

Tooimplementing uma abordagem isto 'home-efetuadas' dimensionamento automático funcionalidade é tooadd um novo serviço sem estado toohello Service Fabric aplicação toomanage operações de dimensionamento. No âmbito do serviço de Olá `RunAsync` método, um conjunto de acionadores pode determinar se o dimensionamento é necessário (incluindo a verificação de parâmetros, tais como o tamanho máximo do cluster e dimensionamento cooldowns).   

Olá API utilizada para interações de conjunto de dimensionamento de máquina virtual (ambas número de instâncias de máquina virtual e toomodify toocheck Olá atuais-lo) é Olá [biblioteca de computação de gestão do Azure fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/). biblioteca de computação fluent Olá fornece uma API de fácil utilização para interagir com conjuntos de dimensionamento de máquina virtual.

utilizar toointeract com o cluster do Service Fabric Olá, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).

Obviamente, Olá dimensionamento código não necessita de toorun como um serviço no Olá cluster toobe ampliada. Ambos `IAzure` e `FabricClient` pode ligar recursos do Azure tootheir associado de remotamente, pelo Olá dimensionamento serviço facilmente pode ser uma aplicação de consola ou em execução da aplicação de Service Fabric Olá fora de serviço do Windows. 

## <a name="credential-management"></a>Gestão de credenciais
Um desafio de escrever um dimensionamento de toohandle de serviço é que o serviço de Olá tem de ser capaz de tooaccess recursos escala conjunto da máquina virtual sem um início de sessão interativo. Aceder ao hello do Service Fabric cluster é fácil se Olá dimensionar o serviço está a modificar as suas próprias aplicações de Service Fabric, mas as credenciais são necessárias tooaccess Olá conjunto de dimensionamento. toolog no, pode utilizar um [principal de serviço](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) criados com Olá [Azure CLI 2.0](https://github.com/azure/azure-cli).

Um principal de serviço pode ser criado com Olá os seguintes passos:

1. Inicie sessão no toohello CLI do Azure (`az login`) como um utilizador com o dimensionamento da máquina virtual toohello acesso definido
2. Criar o serviço de Olá principal com o`az ad sp create-for-rbac`
    1. Anote o appId Olá (denominado 'ID de cliente' noutro local), nome, a palavra-passe e inquilino para utilização posterior.
    2. Também terá do ID de subscrição, que pode ser visualizado com`az account list`

Olá biblioteca fluent computação pode iniciar sessão utilizando estas credenciais da seguinte forma (tenha em atenção que, como tipos de Azure fluent core `IAzure` em Olá [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pacote):

```C#
var credentials = new AzureCredentials(new ServicePrincipalLoginInformation {
                ClientId = AzureClientId,
                ClientSecret = 
                AzureClientKey }, AzureTenantId, AzureEnvironment.AzureGlobalCloud);
IAzure AzureClient = Azure.Authenticate(credentials).WithSubscription(AzureSubscriptionId);

if (AzureClient?.SubscriptionId == AzureSubscriptionId)
{
    ServiceEventSource.Current.ServiceMessage(Context, "Successfully logged into Azure");
}
else
{
    ServiceEventSource.Current.ServiceMessage(Context, "ERROR: Failed toologin tooAzure");
}
```

Assim que a sessão iniciada, a contagem de instâncias do conjunto de dimensionamento pode ser consultada através de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.

## <a name="scaling-out"></a>Aumentar horizontalmente
Utilizar Olá fluent SDK de computação do Azure, podem adicionar instâncias toohello dimensionamento da máquina virtual com apenas alguns chamadas-

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

Em alternativa, o tamanho do conjunto de dimensionamento de máquina virtual também pode ser gerido com os cmdlets do PowerShell. [`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Pode obter o objeto do conjunto de dimensionamento de máquina virtual de Olá. capacidade atual da Olá será armazenada nas Olá `.sku.capacity` propriedade. Depois de alterar Olá capacidade toohello valor pretendido, o dimensionamento da máquina virtual Olá definido no Azure pode ser atualizado com Olá [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.

Como ao adicionar um nó manualmente, adicionar a instância de conjunto de escala deve ser todos os toostart necessária da inclui um novo nó de Service Fabric, uma vez que o modelo de conjunto de dimensionamento de Olá extensões tooautomatically aderir a cluster do Service Fabric toohello instâncias novo. 

## <a name="scaling-in"></a>Dimensionamento no

Dimensionamento no é semelhante tooscaling enviados. conjunto de dimensionamento da máquina de virtual real Olá alterações são praticamente Olá mesmo. No entanto, tal como foi mencionado anteriormente, Service Fabric só limpa automaticamente removidas nós com uma durabilidade de ouro ou Silver. Portanto, Olá Bronze durabilidade na escala caso, é necessário toointeract com Olá Service Fabric tooshut baixo Olá nó toobe removido e cluster, em seguida, tooremove estado.

Preparar o nó de Olá para encerramento envolve localizar Olá nó toobe removido (Olá de nó mais recentemente adicionado) e desativá-lo. Para nós seed não, nós mais recentes podem ser encontrados comparando `NodeInstanceId`. 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

Tenha em atenção que *seed* nós não parecem tooalways siga Convenção Olá que maior IDs de instância são removidos pela primeira vez.

Depois de Olá nó toobe removida for encontrado, pode ser desativado e removida utilizando Olá mesmo `FabricClient` instância e Olá `IAzure` instância de versões anteriores.

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);

// Remove hello node from hello Service Fabric cluster
ServiceEventSource.Current.ServiceMessage(Context, $"Disabling node {mostRecentLiveNode.NodeName}");
await client.ClusterManager.DeactivateNodeAsync(mostRecentLiveNode.NodeName, NodeDeactivationIntent.RemoveNode);

// Wait (up tooa timeout) for hello node toogracefully shutdown
var timeout = TimeSpan.FromMinutes(5);
var waitStart = DateTime.Now;
while ((mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Up || mostRecentLiveNode.NodeStatus == System.Fabric.Query.NodeStatus.Disabling) &&
        DateTime.Now - waitStart < timeout)
{
    mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync()).FirstOrDefault(n => n.NodeName == mostRecentLiveNode.NodeName);
    await Task.Delay(10 * 1000);
}

// Decrement VMSS capacity
var newCapacity = (int)Math.Max(MinimumNodeCount, scaleSet.Capacity - 1); // Check min count 

scaleSet.Update().WithCapacity(newCapacity).Apply(); 
```

Como aumentar horizontalmente, cmdlets do PowerShell para modificar o dimensionamento da máquina virtual com o conjunto de capacidade também pode ser utilizada aqui se uma abordagem de script é preferível. Assim que a instância de máquina virtual de Olá for removida, pode remover o estado de nó de Service Fabric.

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a>Desvantagens potenciais

Como é demonstrado na Olá precedente fragmentos de código, criar o seu próprio serviço dimensionamento fornece grau mais elevado de Olá de controlo e customizability através da aplicação do dimensionamento comportamento. Isto pode ser útil para cenários que requerem controlo preciso sobre quando ou como uma aplicação dimensiona de entrada ou saída. No entanto, este controlo é fornecido com um compromisso de complexidade de código. Através desta abordagem significa que terá de tooown dimensionamento código, o que é não trivial.

Como deve abordar o dimensionamento do Service Fabric depende do seu cenário. Se o dimensionamento é invulgar, Olá capacidade tooadd ou remover nós manualmente é provavelmente suficiente. Para cenários mais complexos, regras de dimensionamento automático e SDKs exposição Olá capacidade tooscale programaticamente oferecem alternativas poderosas.

## <a name="next-steps"></a>Passos seguintes

tooget iniciado a implementar a sua própria lógica de dimensionamento automático, familiarize-se com Olá seguintes conceitos e APIs úteis:

- [Dimensionar manualmente ou com regras de dimensionamento automático](./service-fabric-cluster-scale-up-down.md)
- [Fluent bibliotecas de gestão do Azure para .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (útil para interagir com conjuntos de dimensionamento de máquina virtual do cluster do Service Fabric subjacente)
- [System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (útil para interagir com um cluster do Service Fabric e os respetivos nós)
