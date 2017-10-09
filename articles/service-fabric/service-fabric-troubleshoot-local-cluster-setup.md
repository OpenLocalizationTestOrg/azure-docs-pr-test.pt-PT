---
title: "aaaTroubleshoot a configuração de cluster do Service Fabric local | Microsoft Docs"
description: "Este artigo aborda um conjunto de sugestões de resolução de problemas de cluster de desenvolvimento local"
services: service-fabric
documentationcenter: .net
author: mikkelhegn
manager: timlt
editor: 
ms.assetid: 97f4feaa-bba0-47af-8fdd-07f811fe2202
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/07/2017
ms.author: mikkelhegn
ms.openlocfilehash: ce36f62a4bc69d2cd5b6c3df4abda6ca88fa84f0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-your-local-development-cluster-setup"></a><span data-ttu-id="d3750-103">Resolver problemas relacionados com a configuração de cluster de desenvolvimento local</span><span class="sxs-lookup"><span data-stu-id="d3750-103">Troubleshoot your local development cluster setup</span></span>
<span data-ttu-id="d3750-104">Caso se depare com um problema ao interagir com o cluster de desenvolvimento local do Azure Service Fabric, reveja Olá sugestões para possíveis soluções a seguir.</span><span class="sxs-lookup"><span data-stu-id="d3750-104">If you run into an issue while interacting with your local Azure Service Fabric development cluster, review hello following suggestions for potential solutions.</span></span>

## <a name="cluster-setup-failures"></a><span data-ttu-id="d3750-105">Falhas de configuração de cluster</span><span class="sxs-lookup"><span data-stu-id="d3750-105">Cluster setup failures</span></span>
### <a name="cannot-clean-up-service-fabric-logs"></a><span data-ttu-id="d3750-106">Não é possível limpar os registos de Service Fabric</span><span class="sxs-lookup"><span data-stu-id="d3750-106">Cannot clean up Service Fabric logs</span></span>
#### <a name="problem"></a><span data-ttu-id="d3750-107">Problema</span><span class="sxs-lookup"><span data-stu-id="d3750-107">Problem</span></span>
<span data-ttu-id="d3750-108">Ao executar o script de DevClusterSetup Olá, verá um erro semelhante isto:</span><span class="sxs-lookup"><span data-stu-id="d3750-108">While running hello DevClusterSetup script, you see an error like this:</span></span>

    Cannot clean up C:\SfDevCluster\Log fully as references are likely being held tooitems in it. Please remove those and run this script again.
    At line:1 char:1 + .\DevClusterSetup.ps1
    + ~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : NotSpecified: (:) [Write-Error], WriteErrorException
    + FullyQualifiedErrorId : Microsoft.PowerShell.Commands.WriteErrorException,DevClusterSetup.ps1


#### <a name="solution"></a><span data-ttu-id="d3750-109">Solução</span><span class="sxs-lookup"><span data-stu-id="d3750-109">Solution</span></span>
<span data-ttu-id="d3750-110">Feche Olá atual janela do PowerShell e abrir uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d3750-110">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="d3750-111">Agora, deve ser toosuccessfully capaz de executar o script de Olá.</span><span class="sxs-lookup"><span data-stu-id="d3750-111">You should now be able toosuccessfully run hello script.</span></span>

## <a name="cluster-connection-failures"></a><span data-ttu-id="d3750-112">Falhas de ligação de cluster</span><span class="sxs-lookup"><span data-stu-id="d3750-112">Cluster connection failures</span></span>
### <a name="service-fabric-powershell-cmdlets-are-not-recognized-in-azure-powershell"></a><span data-ttu-id="d3750-113">Cmdlets do PowerShell de Service Fabric não são reconhecidos no Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3750-113">Service Fabric PowerShell cmdlets are not recognized in Azure PowerShell</span></span>
#### <a name="problem"></a><span data-ttu-id="d3750-114">Problema</span><span class="sxs-lookup"><span data-stu-id="d3750-114">Problem</span></span>
<span data-ttu-id="d3750-115">Se tentar toorun qualquer um dos Olá cmdlets do PowerShell de Service Fabric, tais como `Connect-ServiceFabricCluster` numa janela do PowerShell do Azure, não conseguir, indicando que cmdlet Olá não é reconhecido.</span><span class="sxs-lookup"><span data-stu-id="d3750-115">If you try toorun any of hello Service Fabric PowerShell cmdlets, such as `Connect-ServiceFabricCluster` in an Azure PowerShell window, it fails, saying that hello cmdlet is not recognized.</span></span> <span data-ttu-id="d3750-116">razão Olá para este é o Azure PowerShell utiliza a versão de 32 bits Olá do Windows PowerShell (mesmo em versões de SO de 64 bits), enquanto Olá cmdlets do Service Fabric só funcionam nos ambientes de 64 bits.</span><span class="sxs-lookup"><span data-stu-id="d3750-116">hello reason for this is that Azure PowerShell uses hello 32-bit version of Windows PowerShell (even on 64-bit OS versions), whereas hello Service Fabric cmdlets only work in 64-bit environments.</span></span>

#### <a name="solution"></a><span data-ttu-id="d3750-117">Solução</span><span class="sxs-lookup"><span data-stu-id="d3750-117">Solution</span></span>
<span data-ttu-id="d3750-118">Sempre executar cmdlets do Service Fabric diretamente a partir do Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d3750-118">Always run Service Fabric cmdlets directly from Windows PowerShell.</span></span>

> [!NOTE]
> <span data-ttu-id="d3750-119">versão mais recente do Olá do Azure PowerShell não criar um atalho especial, pelo que este já não deve ocorrer.</span><span class="sxs-lookup"><span data-stu-id="d3750-119">hello latest version of Azure PowerShell does not create a special shortcut, so this should no longer occur.</span></span>
> 
> 

### <a name="type-initialization-exception"></a><span data-ttu-id="d3750-120">Exceção de inicialização do tipo</span><span class="sxs-lookup"><span data-stu-id="d3750-120">Type Initialization exception</span></span>
#### <a name="problem"></a><span data-ttu-id="d3750-121">Problema</span><span class="sxs-lookup"><span data-stu-id="d3750-121">Problem</span></span>
<span data-ttu-id="d3750-122">Quando estiverem a ligar toohello cluster no PowerShell, consulte o erro de Olá TypeInitializationException para System.Fabric.Common.AppTrace.</span><span class="sxs-lookup"><span data-stu-id="d3750-122">When you are connecting toohello cluster in PowerShell, you see hello error TypeInitializationException for System.Fabric.Common.AppTrace.</span></span>

#### <a name="solution"></a><span data-ttu-id="d3750-123">Solução</span><span class="sxs-lookup"><span data-stu-id="d3750-123">Solution</span></span>
<span data-ttu-id="d3750-124">A variável de caminho não foi corretamente definida durante a instalação.</span><span class="sxs-lookup"><span data-stu-id="d3750-124">Your path variable was not correctly set during installation.</span></span> <span data-ttu-id="d3750-125">Terminar a sessão do Windows e inicie sessão novamente.</span><span class="sxs-lookup"><span data-stu-id="d3750-125">Sign out of Windows and sign back in.</span></span> <span data-ttu-id="d3750-126">Isto atualiza o seu caminho.</span><span class="sxs-lookup"><span data-stu-id="d3750-126">This refreshes your path.</span></span>

### <a name="cluster-connection-fails-with-object-is-closed"></a><span data-ttu-id="d3750-127">Falha da ligação de cluster com "Objeto está fechado"</span><span class="sxs-lookup"><span data-stu-id="d3750-127">Cluster connection fails with "Object is closed"</span></span>
#### <a name="problem"></a><span data-ttu-id="d3750-128">Problema</span><span class="sxs-lookup"><span data-stu-id="d3750-128">Problem</span></span>
<span data-ttu-id="d3750-129">Uma chamada tooConnect-ServiceFabricCluster falha com o erro seguinte:</span><span class="sxs-lookup"><span data-stu-id="d3750-129">A call tooConnect-ServiceFabricCluster fails with an error like this:</span></span>

    Connect-ServiceFabricCluster : hello object is closed.
    At line:1 char:1
    + Connect-ServiceFabricCluster
    + ~~~~~~~~~~~~~~~~~~~~~~~~~~~~
    + CategoryInfo : InvalidOperation: (:) [Connect-ServiceFabricCluster], FabricObjectClosedException
    + FullyQualifiedErrorId : CreateClusterConnectionErrorId,Microsoft.ServiceFabric.Powershell.ConnectCluster

#### <a name="solution"></a><span data-ttu-id="d3750-130">Solução</span><span class="sxs-lookup"><span data-stu-id="d3750-130">Solution</span></span>
<span data-ttu-id="d3750-131">Feche Olá atual janela do PowerShell e abrir uma nova janela do PowerShell como administrador.</span><span class="sxs-lookup"><span data-stu-id="d3750-131">Close hello current PowerShell window and open a new PowerShell window as an administrator.</span></span> <span data-ttu-id="d3750-132">Agora deve ser capaz de ligar toosuccessfully.</span><span class="sxs-lookup"><span data-stu-id="d3750-132">You should now be able toosuccessfully connect.</span></span>

### <a name="fabric-connection-denied-exception"></a><span data-ttu-id="d3750-133">Excepção de ligação negado de recursos de infraestrutura</span><span class="sxs-lookup"><span data-stu-id="d3750-133">Fabric Connection Denied exception</span></span>
#### <a name="problem"></a><span data-ttu-id="d3750-134">Problema</span><span class="sxs-lookup"><span data-stu-id="d3750-134">Problem</span></span>
<span data-ttu-id="d3750-135">Quando a depuração do Visual Studio, receberá um erro de FabricConnectionDeniedException.</span><span class="sxs-lookup"><span data-stu-id="d3750-135">When debugging from Visual Studio, you get a FabricConnectionDeniedException error.</span></span>

#### <a name="solution"></a><span data-ttu-id="d3750-136">Solução</span><span class="sxs-lookup"><span data-stu-id="d3750-136">Solution</span></span>
<span data-ttu-id="d3750-137">Este erro ocorre normalmente quando tenta toostart um processo de anfitrião do serviço manualmente, em vez de permitir toostart de tempo de execução do Service Fabric Olá-lo por si.</span><span class="sxs-lookup"><span data-stu-id="d3750-137">This error usually occurs when you try toostart a service host process manually, rather than allowing hello Service Fabric runtime toostart it for you.</span></span>

<span data-ttu-id="d3750-138">Certifique-se de que não têm qualquer projetos do serviço definido como projetos de arranque na sua solução.</span><span class="sxs-lookup"><span data-stu-id="d3750-138">Ensure that you do not have any service projects set as startup projects in your solution.</span></span> <span data-ttu-id="d3750-139">Projetos de aplicação de Service Fabric só devem ser definidos como projetos de arranque.</span><span class="sxs-lookup"><span data-stu-id="d3750-139">Only Service Fabric application projects should be set as startup projects.</span></span>

> [!TIP]
> <span data-ttu-id="d3750-140">Se, a seguir o programa de configuração, o cluster local começa toobehave anormalmente, pode repô-lo utilizando a aplicação de tabuleiro do sistema de Gestor do Olá local cluster.</span><span class="sxs-lookup"><span data-stu-id="d3750-140">If, following setup, your local cluster begins toobehave abnormally, you can reset it using hello local cluster manager system tray application.</span></span> <span data-ttu-id="d3750-141">Este remove Olá cluster existente e configure um novo.</span><span class="sxs-lookup"><span data-stu-id="d3750-141">This removes hello existing cluster and set up a new one.</span></span> <span data-ttu-id="d3750-142">Tenha em atenção que todas as aplicações implementadas e dados associados são removidos.</span><span class="sxs-lookup"><span data-stu-id="d3750-142">Note that all deployed applications and associated data is removed.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="d3750-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="d3750-143">Next steps</span></span>
* [<span data-ttu-id="d3750-144">Compreender e resolver problemas de cluster com relatórios de estado de funcionamento do sistema</span><span class="sxs-lookup"><span data-stu-id="d3750-144">Understand and troubleshoot your cluster with system health reports</span></span>](service-fabric-understand-and-troubleshoot-with-system-health-reports.md)
* [<span data-ttu-id="d3750-145">Visualizar o cluster com o Service Fabric Explorer</span><span class="sxs-lookup"><span data-stu-id="d3750-145">Visualize your cluster with Service Fabric Explorer</span></span>](service-fabric-visualizing-your-cluster.md)

