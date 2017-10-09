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
# <a name="scale-a-service-fabric-cluster-programmatically"></a><span data-ttu-id="7d9fc-103">Dimensionar um cluster do Service Fabric através de programação</span><span class="sxs-lookup"><span data-stu-id="7d9fc-103">Scale a Service Fabric cluster programmatically</span></span> 

<span data-ttu-id="7d9fc-104">Noções básicas de dimensionamento de um cluster do Service Fabric no Azure são abrangidas na documentação no [dimensionamento de clusters](./service-fabric-cluster-scale-up-down.md).</span><span class="sxs-lookup"><span data-stu-id="7d9fc-104">Fundamentals of scaling a Service Fabric cluster in Azure are covered in documentation on [cluster scaling](./service-fabric-cluster-scale-up-down.md).</span></span> <span data-ttu-id="7d9fc-105">Este artigo abrange como clusters de Service Fabric assentes em conjuntos de dimensionamento de máquina virtual e podem ser ampliadas manualmente ou com regras de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-105">That article covers how Service Fabric clusters are built on top of virtual machine scale sets and can be scaled either manually or with auto-scale rules.</span></span> <span data-ttu-id="7d9fc-106">Este documento observa programáticos métodos de coordenação Azure dimensionamento operações para cenários mais avançados.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-106">This document looks at programmatic methods of coordinating Azure scaling operations for more advanced scenarios.</span></span> 

## <a name="reasons-for-programmatic-scaling"></a><span data-ttu-id="7d9fc-107">Razões para dimensionamento programático</span><span class="sxs-lookup"><span data-stu-id="7d9fc-107">Reasons for programmatic scaling</span></span>
<span data-ttu-id="7d9fc-108">Em vários cenários, dimensionar manualmente ou através de regras de dimensionamento automático é boas soluções.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-108">In many scenarios, scaling manually or via auto-scale rules are good solutions.</span></span> <span data-ttu-id="7d9fc-109">Noutros cenários, no entanto, estes podem não ser Olá ajustar à direita.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-109">In other scenarios, though, they may not be hello right fit.</span></span> <span data-ttu-id="7d9fc-110">Abordagens de toothese desvantagens potenciais incluem:</span><span class="sxs-lookup"><span data-stu-id="7d9fc-110">Potential drawbacks toothese approaches include:</span></span>

- <span data-ttu-id="7d9fc-111">Dimensionar Manualmente requer toolog no e explicitamente o pedido de dimensionamento de operações.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-111">Manually scaling requires you toolog in and explicitly request scaling operations.</span></span> <span data-ttu-id="7d9fc-112">Se operações de dimensionamento forem necessárias com frequência, ou em alturas imprevisíveis, esta abordagem não pode ser uma boa solução.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-112">If scaling operations are required frequently or at unpredictable times, this approach may not be a good solution.</span></span>
- <span data-ttu-id="7d9fc-113">Quando as regras de dimensionamento automático remover uma instância de um conjunto de dimensionamento de máquina virtual, estes não remove automaticamente dados de conhecimento desse nó de cluster do Service Fabric Olá associado, a menos que tipo de nó Olá tem um nível de durabilidade de Silver ou Gold.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-113">When auto-scale rules remove an instance from a virtual machine scale set, they do not automatically remove knowledge of that node from hello associated Service Fabric cluster unless hello node type has a durability level of Silver or Gold.</span></span> <span data-ttu-id="7d9fc-114">Porque as regras de dimensionamento automático funcionam em escala Olá definido ao nível (em vez de em Olá nível de Service Fabric), as regras de dimensionamento automático podem remover nós de Service Fabric sem encerrado-las sem problemas.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-114">Because auto-scale rules work at hello scale set level (rather than at hello Service Fabric level), auto-scale rules can remove Service Fabric nodes without shutting them down gracefully.</span></span> <span data-ttu-id="7d9fc-115">Esta remoção de nó grosseiro sair "fantasma" Estado do nó de Service Fabric após operações de escala.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-115">This rude node removal will leave 'ghost' Service Fabric node state behind after scale-in operations.</span></span> <span data-ttu-id="7d9fc-116">Uma pessoa (ou um serviço), seria necessário tooperiodically Limpar estado do nó removido no cluster do Service Fabric Olá.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-116">An individual (or a service) would need tooperiodically clean up removed node state in hello Service Fabric cluster.</span></span>
  - <span data-ttu-id="7d9fc-117">Tenha em atenção que um tipo de nó com um nível de durabilidade de ouro ou Silver irá limpar automaticamente remover nós.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-117">Note that a node type with a durability level of Gold or Silver will automatically clean up removed nodes.</span></span>  
- <span data-ttu-id="7d9fc-118">Apesar de existirem [métricas muitos](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) suportado pelas regras de dimensionamento automático, é ainda um conjunto limitado.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-118">Although there are [many metrics](../monitoring-and-diagnostics/insights-autoscale-common-metrics.md) supported by auto-scale rules, it is still a limited set.</span></span> <span data-ttu-id="7d9fc-119">Se o seu cenário chama-se em algum métrica não abrangida desse conjunto de dimensionamento, em seguida, as regras de dimensionamento automático não podem ser uma boa opção.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-119">If your scenario calls for scaling based on some metric not covered in that set, then auto-scale rules may not be a good option.</span></span>

<span data-ttu-id="7d9fc-120">Com base nestas limitações, pode ser útil tooimplement mais personalizados Automáticos dimensionamento modelos.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-120">Based on these limitations, you may wish tooimplement more customized automatic scaling models.</span></span> 

## <a name="scaling-apis"></a><span data-ttu-id="7d9fc-121">APIs de dimensionamento</span><span class="sxs-lookup"><span data-stu-id="7d9fc-121">Scaling APIs</span></span>
<span data-ttu-id="7d9fc-122">As APIs do Azure existem que permitem que aplicações tooprogrammatically trabalho com conjuntos de dimensionamento de máquina virtual e clusters de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-122">Azure APIs exist which allow applications tooprogrammatically work with virtual machine scale sets and Service Fabric clusters.</span></span> <span data-ttu-id="7d9fc-123">Se as opções de dimensionamento automático existente não funcionam para o seu cenário, estas APIs tornam possível tooimplement lógica de dimensionamento personalizada.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-123">If existing auto-scale options don't work for your scenario, these APIs make it possible tooimplement custom scaling logic.</span></span> 

<span data-ttu-id="7d9fc-124">Tooimplementing uma abordagem isto 'home-efetuadas' dimensionamento automático funcionalidade é tooadd um novo serviço sem estado toohello Service Fabric aplicação toomanage operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-124">One approach tooimplementing this 'home-made' auto-scaling functionality is tooadd a new stateless service toohello Service Fabric application toomanage scaling operations.</span></span> <span data-ttu-id="7d9fc-125">No âmbito do serviço de Olá `RunAsync` método, um conjunto de acionadores pode determinar se o dimensionamento é necessário (incluindo a verificação de parâmetros, tais como o tamanho máximo do cluster e dimensionamento cooldowns).</span><span class="sxs-lookup"><span data-stu-id="7d9fc-125">Within hello service's `RunAsync` method, a set of triggers can determine if scaling is required (including checking parameters such as maximum cluster size and scaling cooldowns).</span></span>   

<span data-ttu-id="7d9fc-126">Olá API utilizada para interações de conjunto de dimensionamento de máquina virtual (ambas número de instâncias de máquina virtual e toomodify toocheck Olá atuais-lo) é Olá [biblioteca de computação de gestão do Azure fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span><span class="sxs-lookup"><span data-stu-id="7d9fc-126">hello API used for virtual machine scale set interactions (both toocheck hello current number of virtual machine instances and toomodify it) is hello [fluent Azure Management Compute library](https://www.nuget.org/packages/Microsoft.Azure.Management.Compute.Fluent/).</span></span> <span data-ttu-id="7d9fc-127">biblioteca de computação fluent Olá fornece uma API de fácil utilização para interagir com conjuntos de dimensionamento de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-127">hello fluent compute library provides an easy-to-use API for interacting with virtual machine scale sets.</span></span>

<span data-ttu-id="7d9fc-128">utilizar toointeract com o cluster do Service Fabric Olá, [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span><span class="sxs-lookup"><span data-stu-id="7d9fc-128">toointeract with hello Service Fabric cluster itself, use [System.Fabric.FabricClient](/dotnet/api/system.fabric.fabricclient).</span></span>

<span data-ttu-id="7d9fc-129">Obviamente, Olá dimensionamento código não necessita de toorun como um serviço no Olá cluster toobe ampliada.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-129">Of course, hello scaling code doesn't need toorun as a service in hello cluster toobe scaled.</span></span> <span data-ttu-id="7d9fc-130">Ambos `IAzure` e `FabricClient` pode ligar recursos do Azure tootheir associado de remotamente, pelo Olá dimensionamento serviço facilmente pode ser uma aplicação de consola ou em execução da aplicação de Service Fabric Olá fora de serviço do Windows.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-130">Both `IAzure` and `FabricClient` can connect tootheir associated Azure resources remotely, so hello scaling service could easily be a console application or Windows service running from outside hello Service Fabric application.</span></span> 

## <a name="credential-management"></a><span data-ttu-id="7d9fc-131">Gestão de credenciais</span><span class="sxs-lookup"><span data-stu-id="7d9fc-131">Credential management</span></span>
<span data-ttu-id="7d9fc-132">Um desafio de escrever um dimensionamento de toohandle de serviço é que o serviço de Olá tem de ser capaz de tooaccess recursos escala conjunto da máquina virtual sem um início de sessão interativo.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-132">One challenge of writing a service toohandle scaling is that hello service must be able tooaccess virtual machine scale set resources without an interactive login.</span></span> <span data-ttu-id="7d9fc-133">Aceder ao hello do Service Fabric cluster é fácil se Olá dimensionar o serviço está a modificar as suas próprias aplicações de Service Fabric, mas as credenciais são necessárias tooaccess Olá conjunto de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-133">Accessing hello Service Fabric cluster is easy if hello scaling service is modifying its own Service Fabric application, but credentials are needed tooaccess hello scale set.</span></span> <span data-ttu-id="7d9fc-134">toolog no, pode utilizar um [principal de serviço](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) criados com Olá [Azure CLI 2.0](https://github.com/azure/azure-cli).</span><span class="sxs-lookup"><span data-stu-id="7d9fc-134">toolog in, you can use a [service principal](https://github.com/Azure/azure-sdk-for-net/blob/Fluent/AUTH.md#creating-a-service-principal-in-azure) created with hello [Azure CLI 2.0](https://github.com/azure/azure-cli).</span></span>

<span data-ttu-id="7d9fc-135">Um principal de serviço pode ser criado com Olá os seguintes passos:</span><span class="sxs-lookup"><span data-stu-id="7d9fc-135">A service principal can be created with hello following steps:</span></span>

1. <span data-ttu-id="7d9fc-136">Inicie sessão no toohello CLI do Azure (`az login`) como um utilizador com o dimensionamento da máquina virtual toohello acesso definido</span><span class="sxs-lookup"><span data-stu-id="7d9fc-136">Log in toohello Azure CLI (`az login`) as a user with access toohello virtual machine scale set</span></span>
2. <span data-ttu-id="7d9fc-137">Criar o serviço de Olá principal com o`az ad sp create-for-rbac`</span><span class="sxs-lookup"><span data-stu-id="7d9fc-137">Create hello service principal with `az ad sp create-for-rbac`</span></span>
    1. <span data-ttu-id="7d9fc-138">Anote o appId Olá (denominado 'ID de cliente' noutro local), nome, a palavra-passe e inquilino para utilização posterior.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-138">Make note of hello appId (called 'client ID' elsewhere), name, password, and tenant for later use.</span></span>
    2. <span data-ttu-id="7d9fc-139">Também terá do ID de subscrição, que pode ser visualizado com`az account list`</span><span class="sxs-lookup"><span data-stu-id="7d9fc-139">You will also need your subscription ID, which can be viewed with `az account list`</span></span>

<span data-ttu-id="7d9fc-140">Olá biblioteca fluent computação pode iniciar sessão utilizando estas credenciais da seguinte forma (tenha em atenção que, como tipos de Azure fluent core `IAzure` em Olá [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) pacote):</span><span class="sxs-lookup"><span data-stu-id="7d9fc-140">hello fluent compute library can log in using these credentials as follows (note that core fluent Azure types like `IAzure` are in hello [Microsoft.Azure.Management.Fluent](https://www.nuget.org/packages/Microsoft.Azure.Management.Fluent/) package):</span></span>

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

<span data-ttu-id="7d9fc-141">Assim que a sessão iniciada, a contagem de instâncias do conjunto de dimensionamento pode ser consultada através de `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-141">Once logged in, scale set instance count can be queried via `AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId).Capacity`.</span></span>

## <a name="scaling-out"></a><span data-ttu-id="7d9fc-142">Aumentar horizontalmente</span><span class="sxs-lookup"><span data-stu-id="7d9fc-142">Scaling out</span></span>
<span data-ttu-id="7d9fc-143">Utilizar Olá fluent SDK de computação do Azure, podem adicionar instâncias toohello dimensionamento da máquina virtual com apenas alguns chamadas-</span><span class="sxs-lookup"><span data-stu-id="7d9fc-143">Using hello fluent Azure compute SDK, instances can be added toohello virtual machine scale set with just a few calls -</span></span>

```C#
var scaleSet = AzureClient.VirtualMachineScaleSets.GetById(ScaleSetId);
var newCapacity = (int)Math.Min(MaximumNodeCount, scaleSet.Capacity + 1);
scaleSet.Update().WithCapacity(newCapacity).Apply(); 
``` 

<span data-ttu-id="7d9fc-144">Em alternativa, o tamanho do conjunto de dimensionamento de máquina virtual também pode ser gerido com os cmdlets do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-144">Alternatively, virtual machine scale set size can also be managed with PowerShell cmdlets.</span></span> <span data-ttu-id="7d9fc-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss)Pode obter o objeto do conjunto de dimensionamento de máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-145">[`Get-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/get-azurermvmss) can retrieve hello virtual machine scale set object.</span></span> <span data-ttu-id="7d9fc-146">capacidade atual da Olá será armazenada nas Olá `.sku.capacity` propriedade.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-146">hello current capacity will be stored in hello `.sku.capacity` property.</span></span> <span data-ttu-id="7d9fc-147">Depois de alterar Olá capacidade toohello valor pretendido, o dimensionamento da máquina virtual Olá definido no Azure pode ser atualizado com Olá [ `Update-AzureRmVmss` ](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) comando.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-147">After changing hello capacity toohello desired value, hello virtual machine scale set in Azure can be updated with hello [`Update-AzureRmVmss`](https://docs.microsoft.com/en-us/powershell/module/azurerm.compute/update-azurermvmss) command.</span></span>

<span data-ttu-id="7d9fc-148">Como ao adicionar um nó manualmente, adicionar a instância de conjunto de escala deve ser todos os toostart necessária da inclui um novo nó de Service Fabric, uma vez que o modelo de conjunto de dimensionamento de Olá extensões tooautomatically aderir a cluster do Service Fabric toohello instâncias novo.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-148">As when adding a node manually, adding a scale set instance should be all that's needed toostart a new Service Fabric node since hello scale set template includes extensions tooautomatically join new instances toohello Service Fabric cluster.</span></span> 

## <a name="scaling-in"></a><span data-ttu-id="7d9fc-149">Dimensionamento no</span><span class="sxs-lookup"><span data-stu-id="7d9fc-149">Scaling in</span></span>

<span data-ttu-id="7d9fc-150">Dimensionamento no é semelhante tooscaling enviados. conjunto de dimensionamento da máquina de virtual real Olá alterações são praticamente Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-150">Scaling in is similar tooscaling out. hello actual virtual machine scale set changes are practically hello same.</span></span> <span data-ttu-id="7d9fc-151">No entanto, tal como foi mencionado anteriormente, Service Fabric só limpa automaticamente removidas nós com uma durabilidade de ouro ou Silver.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-151">But, as was discussed previously, Service Fabric only automatically cleans up removed nodes with a durability of Gold or Silver.</span></span> <span data-ttu-id="7d9fc-152">Portanto, Olá Bronze durabilidade na escala caso, é necessário toointeract com Olá Service Fabric tooshut baixo Olá nó toobe removido e cluster, em seguida, tooremove estado.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-152">So, in hello Bronze-durability scale-in case, it's necessary toointeract with hello Service Fabric cluster tooshut down hello node toobe removed and then tooremove its state.</span></span>

<span data-ttu-id="7d9fc-153">Preparar o nó de Olá para encerramento envolve localizar Olá nó toobe removido (Olá de nó mais recentemente adicionado) e desativá-lo.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-153">Preparing hello node for shutdown involves finding hello node toobe removed (hello most recently added node) and deactivating it.</span></span> <span data-ttu-id="7d9fc-154">Para nós seed não, nós mais recentes podem ser encontrados comparando `NodeInstanceId`.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-154">For non-seed nodes, newer nodes can be found by comparing `NodeInstanceId`.</span></span> 

```C#
using (var client = new FabricClient())
{
    var mostRecentLiveNode = (await client.QueryManager.GetNodeListAsync())
        .Where(n => n.NodeType.Equals(NodeTypeToScale, StringComparison.OrdinalIgnoreCase))
        .Where(n => n.NodeStatus == System.Fabric.Query.NodeStatus.Up)
        .OrderByDescending(n => n.NodeInstanceId)
        .FirstOrDefault();
```

<span data-ttu-id="7d9fc-155">Tenha em atenção que *seed* nós não parecem tooalways siga Convenção Olá que maior IDs de instância são removidos pela primeira vez.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-155">Be aware that *seed* nodes don't seem tooalways follow hello convention that greater instance IDs are removed first.</span></span>

<span data-ttu-id="7d9fc-156">Depois de Olá nó toobe removida for encontrado, pode ser desativado e removida utilizando Olá mesmo `FabricClient` instância e Olá `IAzure` instância de versões anteriores.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-156">Once hello node toobe removed is found, it can be deactivated and removed using hello same `FabricClient` instance and hello `IAzure` instance from earlier.</span></span>

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

<span data-ttu-id="7d9fc-157">Como aumentar horizontalmente, cmdlets do PowerShell para modificar o dimensionamento da máquina virtual com o conjunto de capacidade também pode ser utilizada aqui se uma abordagem de script é preferível.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-157">As with scaling out, PowerShell cmdlets for modifying virtual machine scale set capacity can also be used here if a scripting approach is preferable.</span></span> <span data-ttu-id="7d9fc-158">Assim que a instância de máquina virtual de Olá for removida, pode remover o estado de nó de Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-158">Once hello virtual machine instance is removed, Service Fabric node state can be removed.</span></span>

```C#
await client.ClusterManager.RemoveNodeStateAsync(mostRecentLiveNode.NodeName);
```

## <a name="potential-drawbacks"></a><span data-ttu-id="7d9fc-159">Desvantagens potenciais</span><span class="sxs-lookup"><span data-stu-id="7d9fc-159">Potential drawbacks</span></span>

<span data-ttu-id="7d9fc-160">Como é demonstrado na Olá precedente fragmentos de código, criar o seu próprio serviço dimensionamento fornece grau mais elevado de Olá de controlo e customizability através da aplicação do dimensionamento comportamento.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-160">As demonstrated in hello preceding code snippets, creating your own scaling service provides hello highest degree of control and customizability over your application's scaling behavior.</span></span> <span data-ttu-id="7d9fc-161">Isto pode ser útil para cenários que requerem controlo preciso sobre quando ou como uma aplicação dimensiona de entrada ou saída. No entanto, este controlo é fornecido com um compromisso de complexidade de código.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-161">This can be useful for scenarios requiring precise control over when or how an application scales in or out. However, this control comes with a tradeoff of code complexity.</span></span> <span data-ttu-id="7d9fc-162">Através desta abordagem significa que terá de tooown dimensionamento código, o que é não trivial.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-162">Using this approach means that you need tooown scaling code, which is non-trivial.</span></span>

<span data-ttu-id="7d9fc-163">Como deve abordar o dimensionamento do Service Fabric depende do seu cenário.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-163">How you should approach Service Fabric scaling depends on your scenario.</span></span> <span data-ttu-id="7d9fc-164">Se o dimensionamento é invulgar, Olá capacidade tooadd ou remover nós manualmente é provavelmente suficiente.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-164">If scaling is uncommon, hello ability tooadd or remove nodes manually is probably sufficient.</span></span> <span data-ttu-id="7d9fc-165">Para cenários mais complexos, regras de dimensionamento automático e SDKs exposição Olá capacidade tooscale programaticamente oferecem alternativas poderosas.</span><span class="sxs-lookup"><span data-stu-id="7d9fc-165">For more complex scenarios, auto-scale rules and SDKs exposing hello ability tooscale programmatically offer powerful alternatives.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d9fc-166">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7d9fc-166">Next steps</span></span>

<span data-ttu-id="7d9fc-167">tooget iniciado a implementar a sua própria lógica de dimensionamento automático, familiarize-se com Olá seguintes conceitos e APIs úteis:</span><span class="sxs-lookup"><span data-stu-id="7d9fc-167">tooget started implementing your own auto-scaling logic, familiarize yourself with hello following concepts and useful APIs:</span></span>

- [<span data-ttu-id="7d9fc-168">Dimensionar manualmente ou com regras de dimensionamento automático</span><span class="sxs-lookup"><span data-stu-id="7d9fc-168">Scaling manually or with auto-scale rules</span></span>](./service-fabric-cluster-scale-up-down.md)
- <span data-ttu-id="7d9fc-169">[Fluent bibliotecas de gestão do Azure para .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (útil para interagir com conjuntos de dimensionamento de máquina virtual do cluster do Service Fabric subjacente)</span><span class="sxs-lookup"><span data-stu-id="7d9fc-169">[Fluent Azure Management Libraries for .NET](https://github.com/Azure/azure-sdk-for-net/tree/Fluent) (useful for interacting with a Service Fabric cluster's underlying virtual machine scale sets)</span></span>
- <span data-ttu-id="7d9fc-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (útil para interagir com um cluster do Service Fabric e os respetivos nós)</span><span class="sxs-lookup"><span data-stu-id="7d9fc-170">[System.Fabric.FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient) (useful for interacting with a Service Fabric cluster and its nodes)</span></span>
