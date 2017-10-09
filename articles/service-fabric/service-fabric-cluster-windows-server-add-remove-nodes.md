---
title: "aaaAdd ou remover cluster do Service Fabric nós tooa autónomo | Microsoft Docs"
description: "Saiba como tooadd ou remover nós tooan Azure Service Fabric cluster numa máquina física ou virtual com o Windows Server, que pode ser no local ou em nenhuma nuvem."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: bc6b8fc0-d2af-42f8-a164-58538be38d02
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 2/02/2017
ms.author: dekapur
ms.openlocfilehash: 1da908ad9840faa052e0b4021bc2d4ce732b02bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="add-or-remove-nodes-tooa-standalone-service-fabric-cluster-running-on-windows-server"></a><span data-ttu-id="85940-103">Adicionar ou remover nós tooa autónomo cluster do Service Fabric em execução no Windows Server</span><span class="sxs-lookup"><span data-stu-id="85940-103">Add or remove nodes tooa standalone Service Fabric cluster running on Windows Server</span></span>
<span data-ttu-id="85940-104">Depois de ter [criado o seu cluster do Service Fabric autónomo nas máquinas do Windows Server](service-fabric-cluster-creation-for-windows-server.md), podem alterar as necessidades de negócio e pode precisar de tooadd ou remover nós tooyour cluster.</span><span class="sxs-lookup"><span data-stu-id="85940-104">After you have [created your standalone Service Fabric cluster on Windows Server machines](service-fabric-cluster-creation-for-windows-server.md), your business needs may change and you might need tooadd or remove nodes tooyour cluster.</span></span> <span data-ttu-id="85940-105">Este artigo fornece os passos detalhados tooachieve isto.</span><span class="sxs-lookup"><span data-stu-id="85940-105">This article provides detailed steps tooachieve this.</span></span> <span data-ttu-id="85940-106">Tenha em atenção que adicionar/remover a funcionalidade de nó não é suportada em clusters de desenvolvimento local.</span><span class="sxs-lookup"><span data-stu-id="85940-106">Please note that add/remove node functionality is not supported in local development clusters.</span></span>

## <a name="add-nodes-tooyour-cluster"></a><span data-ttu-id="85940-107">Adicionar nós tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="85940-107">Add nodes tooyour cluster</span></span>
1. <span data-ttu-id="85940-108">Preparar Olá VM/máquina que pretende tooadd tooyour cluster seguindo os passos de Olá mencionados Olá [Olá preparar máquinas pré-requisitos de Olá toomeet para implementação de cluster](service-fabric-cluster-creation-for-windows-server.md) secção</span><span class="sxs-lookup"><span data-stu-id="85940-108">Prepare hello VM/machine you want tooadd tooyour cluster by following hello steps mentioned in hello [Prepare hello machines toomeet hello prerequisites for cluster deployment](service-fabric-cluster-creation-for-windows-server.md) section</span></span>
2. <span data-ttu-id="85940-109">Identificar o domínio de falhas e são curso tooadd desta VM máquina para o domínio de atualização</span><span class="sxs-lookup"><span data-stu-id="85940-109">Identify which fault domain and upgrade domain you are going tooadd this VM/machine to</span></span>
3. <span data-ttu-id="85940-110">Ambiente de trabalho remoto (RDP) para Olá VM/máquina que pretende que o cluster de toohello tooadd</span><span class="sxs-lookup"><span data-stu-id="85940-110">Remote desktop (RDP) into hello VM/machine that you want tooadd toohello cluster</span></span>
4. <span data-ttu-id="85940-111">Copiar ou [transferir o pacote de autónomo do Olá para recursos de infraestrutura de serviço para o Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/máquina e deszipe o pacote de Olá</span><span class="sxs-lookup"><span data-stu-id="85940-111">Copy or [download hello standalone package for Service Fabric for Windows Server](http://go.microsoft.com/fwlink/?LinkId=730690) toohello VM/machine and unzip hello package</span></span>
5. <span data-ttu-id="85940-112">Executar o Powershell com privilégios elevados e navegue até toohello localização do pacote deszipada Olá</span><span class="sxs-lookup"><span data-stu-id="85940-112">Run Powershell with elevated privileges, and navigate toohello location of hello unzipped package</span></span>
6. <span data-ttu-id="85940-113">Executar Olá *AddNode.ps1* script com parâmetros de Olá descrever Olá novo nó tooadd.</span><span class="sxs-lookup"><span data-stu-id="85940-113">Run hello *AddNode.ps1* script with hello parameters describing hello new node tooadd.</span></span> <span data-ttu-id="85940-114">exemplo de Olá abaixo adiciona um novo nó chamado VM5, com o tipo NodeType0 e endereços IP 182.17.34.52, UD1 e DF: / dc1/r0.</span><span class="sxs-lookup"><span data-stu-id="85940-114">hello example below adds a new node called VM5, with type NodeType0 and IP address 182.17.34.52, into UD1 and fd:/dc1/r0.</span></span> <span data-ttu-id="85940-115">Olá *ExistingClusterConnectionEndPoint* já se encontra um ponto final de ligação para um nó de cluster existente Olá, que pode ser o endereço IP Olá *qualquer* nó no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="85940-115">hello *ExistingClusterConnectionEndPoint* is a connection endpoint for a node already in hello existing cluster, which can be hello IP address of *any* node in hello cluster.</span></span>

    ```
    .\AddNode.ps1 -NodeName VM5 -NodeType NodeType0 -NodeIPAddressorFQDN 182.17.34.52 -ExistingClientConnectionEndpoint 182.17.34.50:19000 -UpgradeDomain UD1 -FaultDomain fd:/dc1/r0 -AcceptEULA
    ```
    <span data-ttu-id="85940-116">Assim que o script de Olá termina em execução, pode verificar se o novo nó de Olá foi adicionado ao executar Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span><span class="sxs-lookup"><span data-stu-id="85940-116">Once hello script finishes running, you can check if hello new node has been added by running hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet.</span></span>

7. <span data-ttu-id="85940-117">consistência tooensure em diferentes nós num cluster de Olá, tem de iniciar uma atualização da configuração.</span><span class="sxs-lookup"><span data-stu-id="85940-117">tooensure consistency across different nodes in hello cluster, you must initiate a configuration upgrade.</span></span> <span data-ttu-id="85940-118">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget Olá o ficheiro de configuração mais recente e adicione Olá recém-adicionada nó demasiado secção "Nós".</span><span class="sxs-lookup"><span data-stu-id="85940-118">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and add hello newly added node too"Nodes" section.</span></span> <span data-ttu-id="85940-119">Recomenda-se também tooalways ter Olá mais recente configuração de cluster disponível no caso de Olá terá tooredploy num cluster com Olá mesma configuração.</span><span class="sxs-lookup"><span data-stu-id="85940-119">It is also recommended tooalways have hello latest cluster configuration available in hello case that you need tooredploy a cluster with hello same configuration.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
8. <span data-ttu-id="85940-120">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.</span><span class="sxs-lookup"><span data-stu-id="85940-120">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="85940-121">Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="85940-121">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="85940-122">Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="85940-122">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-nodes-tooclusters-configured-with-windows-security-using-gmsa"></a><span data-ttu-id="85940-123">Adicionar nós tooclusters configurado com a segurança do Windows utilizam a gMSA</span><span class="sxs-lookup"><span data-stu-id="85940-123">Add nodes tooclusters configured with Windows Security using gMSA</span></span>
<span data-ttu-id="85940-124">Para clusters configurados com o grupo gerido serviço Account(gMSA) (https://technet.microsoft.com/library/hh831782.aspx), um novo nó pode ser adicionado através de uma atualização da configuração:</span><span class="sxs-lookup"><span data-stu-id="85940-124">For clusters configured with Group Managed Service Account(gMSA)(https://technet.microsoft.com/library/hh831782.aspx), a new node can be added using a configuration upgrade:</span></span>
1. <span data-ttu-id="85940-125">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) em qualquer um de nós existentes Olá tooget Olá o ficheiro de configuração mais recente e adicione os detalhes sobre o novo nó de Olá pretende tooadd na secção de nós"Olá".</span><span class="sxs-lookup"><span data-stu-id="85940-125">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) on any of hello existing nodes tooget hello latest configuration file and add details about hello new node you want tooadd in hello "Nodes" section.</span></span> <span data-ttu-id="85940-126">Certifique-se de que o novo nó de Olá faz parte de Olá mesmo a conta gerida de grupo.</span><span class="sxs-lookup"><span data-stu-id="85940-126">Make sure hello new node is part of hello same group managed account.</span></span> <span data-ttu-id="85940-127">Esta conta deve ser um administrador em todas as máquinas.</span><span class="sxs-lookup"><span data-stu-id="85940-127">This account should be an Administrator on all machines.</span></span>

    ```
        {
            "nodeName": "vm5",
            "iPAddress": "182.17.34.52",
            "nodeTypeRef": "NodeType0",
            "faultDomain": "fd:/dc1/r0",
            "upgradeDomain": "UD1"
        }
    ```
2. <span data-ttu-id="85940-128">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.</span><span class="sxs-lookup"><span data-stu-id="85940-128">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>
    ```
    <span data-ttu-id="85940-129">Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="85940-129">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="85940-130">Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="85940-130">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

### <a name="add-node-types-tooyour-cluster"></a><span data-ttu-id="85940-131">Adicionar nó tipos tooyour cluster</span><span class="sxs-lookup"><span data-stu-id="85940-131">Add node types tooyour cluster</span></span>
<span data-ttu-id="85940-132">Na ordem tooadd um novo tipo de nó, modifique a sua configuração tooinclude Olá novo tipo de nó na secção "NodeTypes" em "Propriedades" e começar a uma configuração de fazer a actualização utilizando [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="85940-132">In order tooadd a new node type, modify your configuration tooinclude hello new node type in "NodeTypes" section under "Properties" and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span> <span data-ttu-id="85940-133">Uma vez concluída a atualização de Olá, pode adicionar o novo cluster de tooyour de nós com este tipo de nó.</span><span class="sxs-lookup"><span data-stu-id="85940-133">Once hello upgrade completes, you can add new nodes tooyour cluster with this node type.</span></span>

## <a name="remove-nodes-from-your-cluster"></a><span data-ttu-id="85940-134">Remover nós do cluster</span><span class="sxs-lookup"><span data-stu-id="85940-134">Remove nodes from your cluster</span></span>
<span data-ttu-id="85940-135">Um nó pode ser removido de um cluster com uma atualização da configuração, no Olá seguinte forma:</span><span class="sxs-lookup"><span data-stu-id="85940-135">A node can be removed from a cluster using a configuration upgrade, in hello following manner:</span></span>

1. <span data-ttu-id="85940-136">Executar [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) ficheiro de configuração mais recente do tooget Olá e *remover* nó Olá da secção "Nós".</span><span class="sxs-lookup"><span data-stu-id="85940-136">Run [Get-ServiceFabricClusterConfiguration](/powershell/module/servicefabric/get-servicefabricclusterconfiguration?view=azureservicefabricps) tooget hello latest configuration file and *remove* hello node from "Nodes" section.</span></span>
<span data-ttu-id="85940-137">Adicionar Olá "NodesToBeRemoved" parâmetro demasiado "Configurar" secção no interior da secção "FabricSettings".</span><span class="sxs-lookup"><span data-stu-id="85940-137">Add hello "NodesToBeRemoved" parameter too"Setup" section inside "FabricSettings" section.</span></span> <span data-ttu-id="85940-138">Olá "valor" deve ser uma lista separada por vírgulas de nomes de nó de nós que necessitam de toobe removido.</span><span class="sxs-lookup"><span data-stu-id="85940-138">hello "value" should be a comma separated list of node names of nodes that need toobe removed.</span></span>

    ```
         "fabricSettings": [
            {
            "name": "Setup",
            "parameters": [
                {
                "name": "FabricDataRoot",
                "value": "C:\\ProgramData\\SF"
                },
                {
                "name": "FabricLogRoot",
                "value": "C:\\ProgramData\\SF\\Log"
                },
                {
                "name": "NodesToBeRemoved",
                "value": "vm0, vm1"
                }
            ]
            }
        ]
    ```
2. <span data-ttu-id="85940-139">Executar [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) atualização de Olá toobegin.</span><span class="sxs-lookup"><span data-stu-id="85940-139">Run [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps) toobegin hello upgrade.</span></span>

    ```
    Start-ServiceFabricClusterConfigurationUpgrade -ClusterConfigPath <Path tooConfiguration File>

    ```
    <span data-ttu-id="85940-140">Pode monitorizar o progresso Olá Olá atualização no Service Fabric Explorer.</span><span class="sxs-lookup"><span data-stu-id="85940-140">You can monitor hello progress of hello upgrade on Service Fabric Explorer.</span></span> <span data-ttu-id="85940-141">Em alternativa, pode executar [Get ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span><span class="sxs-lookup"><span data-stu-id="85940-141">Alternatively, you can run [Get-ServiceFabricClusterUpgrade](/powershell/module/servicefabric/get-servicefabricclusterupgrade?view=azureservicefabricps)</span></span>

> [!NOTE]
> <span data-ttu-id="85940-142">Remoção de nós, pode iniciar várias atualizações.</span><span class="sxs-lookup"><span data-stu-id="85940-142">Removal of nodes may initiate multiple upgrades.</span></span> <span data-ttu-id="85940-143">Alguns nós são marcados com `IsSeedNode=”true”` Etiquetar e podem ser identificados através de consultas cluster Olá manifesto utilizando `Get-ServiceFabricClusterManifest`.</span><span class="sxs-lookup"><span data-stu-id="85940-143">Some nodes are marked with `IsSeedNode=”true”` tag and can be identified by querying hello cluster manifest using `Get-ServiceFabricClusterManifest`.</span></span> <span data-ttu-id="85940-144">Remoção de nós pode demorar mais do que outras pessoas, uma vez que nós de seed Olá terão toobe moveu em torno em tais cenários.</span><span class="sxs-lookup"><span data-stu-id="85940-144">Removal of such nodes may take longer than others since hello seed nodes will have toobe moved around in such scenarios.</span></span> <span data-ttu-id="85940-145">cluster de Olá tem de manter um mínimo de 3 nós de tipo de nó principal.</span><span class="sxs-lookup"><span data-stu-id="85940-145">hello cluster must maintain a minimum of 3 primary node type nodes.</span></span>
> 
> 

### <a name="remove-node-types-from-your-cluster"></a><span data-ttu-id="85940-146">Remover tipos de nó do cluster</span><span class="sxs-lookup"><span data-stu-id="85940-146">Remove node types from your cluster</span></span>
<span data-ttu-id="85940-147">Antes de remover um tipo de nó, verifique duplo se existem quaisquer nós que referencia o tipo de nó Olá.</span><span class="sxs-lookup"><span data-stu-id="85940-147">Before removing a node type, please double check if there are any nodes referencing hello node type.</span></span> <span data-ttu-id="85940-148">Remova estes nós antes de remover o tipo de nó Olá correspondente.</span><span class="sxs-lookup"><span data-stu-id="85940-148">Remove these nodes before removing hello corresponding node type.</span></span> <span data-ttu-id="85940-149">Depois de todos os nós correspondentes são removidos, pode remover a configuração de cluster Olá Olá NodeType e começar a uma configuração de fazer a actualização utilizando [início ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span><span class="sxs-lookup"><span data-stu-id="85940-149">Once all corresponding nodes are removed, you can remove hello NodeType from hello cluster configuration and begin a configuration upgrade using [Start-ServiceFabricClusterConfigurationUpgrade](/powershell/module/servicefabric/start-servicefabricclusterconfigurationupgrade?view=azureservicefabricps).</span></span>


### <a name="replace-primary-nodes-of-your-cluster"></a><span data-ttu-id="85940-150">Substitua primários nós do cluster</span><span class="sxs-lookup"><span data-stu-id="85940-150">Replace primary nodes of your cluster</span></span>
<span data-ttu-id="85940-151">substituição de Olá de nós principais deve ser executado um nó após a outra, em vez de remover e, em seguida, adicionar em lotes.</span><span class="sxs-lookup"><span data-stu-id="85940-151">hello replacement of primary nodes should be performed one node after another, instead of removing and then adding in batches.</span></span>


## <a name="next-steps"></a><span data-ttu-id="85940-152">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="85940-152">Next steps</span></span>
* [<span data-ttu-id="85940-153">Definições de configuração do cluster do Windows autónomo</span><span class="sxs-lookup"><span data-stu-id="85940-153">Configuration settings for standalone Windows cluster</span></span>](service-fabric-cluster-manifest.md)
* [<span data-ttu-id="85940-154">Proteger um cluster autónomo no Windows utilizando X509 certificados</span><span class="sxs-lookup"><span data-stu-id="85940-154">Secure a standalone cluster on Windows using X509 certificates</span></span>](service-fabric-windows-cluster-x509-security.md)
* [<span data-ttu-id="85940-155">Criar um cluster do Service Fabric autónomo com as VMs do Azure com o Windows</span><span class="sxs-lookup"><span data-stu-id="85940-155">Create a standalone Service Fabric cluster with Azure VMs running Windows</span></span>](service-fabric-cluster-creation-with-windows-azure-vms.md)

