---
title: aaaSet configurar um cluster do Service Fabric do Azure | Microsoft Docs
description: "Guia de introdução - criar um cluster do Service Fabric do Windows ou Linux no Azure."
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotNet
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 13c60e293d19d607bb41ee4859706508c219a833
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-your-first-service-fabric-cluster-on-azure"></a><span data-ttu-id="ae385-103">Crie o primeiro cluster Service Fabric no Azure</span><span class="sxs-lookup"><span data-stu-id="ae385-103">Create your first Service Fabric cluster on Azure</span></span>
<span data-ttu-id="ae385-104">Um [cluster do Service Fabric](service-fabric-deploy-anywhere.md) é um conjunto ligado à rede de máquinas virtuais ou físicas, no qual os microsserviços são implementados e geridos.</span><span class="sxs-lookup"><span data-stu-id="ae385-104">A [Service Fabric cluster](service-fabric-deploy-anywhere.md) is a network-connected set of virtual or physical machines into which your microservices are deployed and managed.</span></span> <span data-ttu-id="ae385-105">Este guia de introdução ajuda-o a toocreate um cluster de cinco nós, em execução no Windows ou Linux, através de Olá [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) ou [portal do Azure](http://portal.azure.com) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ae385-105">This quickstart helps you toocreate a five-node cluster, running on either Windows or Linux, through hello [Azure PowerShell](https://msdn.microsoft.com/library/dn135248) or [Azure portal](http://portal.azure.com) in just a few minutes.</span></span>  

<span data-ttu-id="ae385-106">Se não tiver uma subscrição do Azure, crie uma [conta gratuita](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) antes de começar.</span><span class="sxs-lookup"><span data-stu-id="ae385-106">If you don't have an Azure subscription, create a [free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) before you begin.</span></span>


## <a name="use-hello-azure-portal"></a><span data-ttu-id="ae385-107">Utilizar Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="ae385-107">Use hello Azure portal</span></span>

<span data-ttu-id="ae385-108">Início de sessão toohello do portal do Azure em [http://portal.azure.com](http://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="ae385-108">Log in toohello Azure portal at [http://portal.azure.com](http://portal.azure.com).</span></span>

### <a name="create-hello-cluster"></a><span data-ttu-id="ae385-109">Criar cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ae385-109">Create hello cluster</span></span>

1. <span data-ttu-id="ae385-110">Clique em Olá **novo** botão encontrado no canto esquerda superior Olá de Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae385-110">Click hello **New** button found on hello upper left-hand corner of hello Azure portal.</span></span>
2. <span data-ttu-id="ae385-111">Selecione **computação** de Olá **novo** painel e, em seguida, selecione **Cluster do Service Fabric** de Olá **computação** painel.</span><span class="sxs-lookup"><span data-stu-id="ae385-111">Select **Compute** from hello **New** blade and then select **Service Fabric Cluster** from hello **Compute** blade.</span></span>
3. <span data-ttu-id="ae385-112">Preencha Olá Service Fabric **Noções básicas** formulário.</span><span class="sxs-lookup"><span data-stu-id="ae385-112">Fill out hello Service Fabric **Basics** form.</span></span> <span data-ttu-id="ae385-113">Para **sistema operativo**, selecione versão Olá do Windows ou Linux que pretende Olá toorun de nós de cluster.</span><span class="sxs-lookup"><span data-stu-id="ae385-113">For **Operating system**, select hello version of Windows or Linux you want hello cluster nodes toorun.</span></span> <span data-ttu-id="ae385-114">nome de utilizador Olá e a palavra-passe introduzida aqui é toolog utilizado na máquina virtual de toohello.</span><span class="sxs-lookup"><span data-stu-id="ae385-114">hello user name and password entered here is used toolog in toohello virtual machine.</span></span> <span data-ttu-id="ae385-115">Para o **Grupo de recursos** crie um novo.</span><span class="sxs-lookup"><span data-stu-id="ae385-115">For **Resource group**, create a new one.</span></span> <span data-ttu-id="ae385-116">Um grupo de recursos é um contentor lógico no qual os recursos do Azure são criados e geridos coletivamente.</span><span class="sxs-lookup"><span data-stu-id="ae385-116">A resource group is a logical container into which Azure resources are created and collectively managed.</span></span> <span data-ttu-id="ae385-117">Quando terminar, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae385-117">When complete, click **OK**.</span></span>

    ![Saída do programa de configuração do cluster][cluster-setup-basics]

4. <span data-ttu-id="ae385-119">Preencha Olá **configuração de Cluster** formulário.</span><span class="sxs-lookup"><span data-stu-id="ae385-119">Fill out hello **Cluster configuration** form.</span></span>  <span data-ttu-id="ae385-120">Para a **contagem do tipo de Nó**, introduza "1".</span><span class="sxs-lookup"><span data-stu-id="ae385-120">For **Node type count**, enter "1".</span></span>

5. <span data-ttu-id="ae385-121">Selecione **1 (principal) do tipo de nó** e preencher Olá **configuração de tipo de nó** formulário.</span><span class="sxs-lookup"><span data-stu-id="ae385-121">Select **Node type 1 (Primary)** and fill out hello **Node type configuration** form.</span></span>  <span data-ttu-id="ae385-122">Introduza um nome de tipo de nó e defina Olá [o escalão de durabilidade](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) demasiado "Bronze."</span><span class="sxs-lookup"><span data-stu-id="ae385-122">Enter a node type name and set hello [Durability tier](service-fabric-cluster-capacity.md#the-durability-characteristics-of-the-cluster) too"Bronze."</span></span>  <span data-ttu-id="ae385-123">Selecione um tamanho de VM.</span><span class="sxs-lookup"><span data-stu-id="ae385-123">Select a VM size.</span></span>

    <span data-ttu-id="ae385-124">Tipos de nó definem o tamanho da VM Olá, número de VMs, os pontos finais personalizados e outras definições para Olá VMs desse tipo.</span><span class="sxs-lookup"><span data-stu-id="ae385-124">Node types define hello VM size, number of VMs, custom endpoints, and other settings for hello VMs of that type.</span></span> <span data-ttu-id="ae385-125">Cada tipo de nó definido está configurado como um conjunto de dimensionamento de máquina virtual separada, o que é utilizado toodeploy e máquinas virtuais geridas como um conjunto.</span><span class="sxs-lookup"><span data-stu-id="ae385-125">Each node type defined is set up as a separate virtual machine scale set, which is used toodeploy and managed virtual machines as a set.</span></span> <span data-ttu-id="ae385-126">Cada tipo de nó pode ser aumentado ou reduzido verticalmente de forma independente, pode ter conjuntos diferentes de portas abertas e ter métricas de capacidade diferente.</span><span class="sxs-lookup"><span data-stu-id="ae385-126">Each node type can be scaled up or down independently, have different sets of ports open, and can have different capacity metrics.</span></span>  <span data-ttu-id="ae385-127">Olá primeiro ou primária, tipo de nó é onde os serviços de sistema do Service Fabric alojados e tem de ter cinco ou mais VMs.</span><span class="sxs-lookup"><span data-stu-id="ae385-127">hello first, or primary, node type is where Service Fabric system services are hosted and must have five or more VMs.</span></span>

    <span data-ttu-id="ae385-128">Para qualquer implementação de produção, o [planeamento da capacidade](service-fabric-cluster-capacity.md) é um passo importante.</span><span class="sxs-lookup"><span data-stu-id="ae385-128">For any production deployment, [capacity planning](service-fabric-cluster-capacity.md) is an important step.</span></span>  <span data-ttu-id="ae385-129">Para este guia de introdução, no entanto, não está a executar aplicações, pelo que deve selecionar um tamanho da VM *DS1_v2 Standard* .</span><span class="sxs-lookup"><span data-stu-id="ae385-129">For this quick start, however, you aren't running applications so select a *DS1_v2 Standard* VM size.</span></span>  <span data-ttu-id="ae385-130">Selecione "Silver" para Olá [escalão de fiabilidade](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) e um dimensionamento da máquina de virtual inicial defina a capacidade de 5.</span><span class="sxs-lookup"><span data-stu-id="ae385-130">Select "Silver" for hello [reliability tier](service-fabric-cluster-capacity.md#the-reliability-characteristics-of-the-cluster) and an initial virtual machine scale set capacity of 5.</span></span>  

    <span data-ttu-id="ae385-131">Os pontos finais personalizados abrir portas no balanceador de carga do Azure de Olá para que possam ligar com as aplicações em execução no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-131">Custom endpoints open up ports in hello Azure load balancer so that you can connect with applications running on hello cluster.</span></span>  <span data-ttu-id="ae385-132">Introduza "80, 8172" tooopen se as portas 80 e 8172.</span><span class="sxs-lookup"><span data-stu-id="ae385-132">Enter "80, 8172" tooopen up ports 80 and 8172.</span></span>

    <span data-ttu-id="ae385-133">Não verificar Olá **configurar as definições avançada** caixa, que é utilizada para personalizar os pontos finais de gestão TCP/HTTP, intervalos de portas de aplicação, [restrições de posicionamento](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), e [capacidade propriedades](service-fabric-cluster-resource-manager-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="ae385-133">Do not check hello **Configure advanced settings** box, which is used for customizing TCP/HTTP management endpoints, application port ranges, [placement constraints](service-fabric-cluster-resource-manager-configure-services.md#placement-constraints), and [capacity properties](service-fabric-cluster-resource-manager-metrics.md).</span></span>    

    <span data-ttu-id="ae385-134">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae385-134">Select **OK**.</span></span>

6. <span data-ttu-id="ae385-135">No Olá **configuração de Cluster** formulário, defina **diagnóstico** demasiado**no**.</span><span class="sxs-lookup"><span data-stu-id="ae385-135">In hello **Cluster configuration** form, set **Diagnostics** too**On**.</span></span>  <span data-ttu-id="ae385-136">Para este início rápido, não é necessário tooenter qualquer [recursos de infraestrutura definição](service-fabric-cluster-fabric-settings.md) propriedades.</span><span class="sxs-lookup"><span data-stu-id="ae385-136">For this quickstart, you do not need tooenter any [fabric setting](service-fabric-cluster-fabric-settings.md) properties.</span></span>  <span data-ttu-id="ae385-137">No **versão do Fabric**, selecione **automática** Atualize modo para que a Microsoft atualiza automaticamente a versão de Olá do código de recursos de infraestrutura de Olá em execução cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-137">In **Fabric version**, select **Automatic** upgrade mode so that Microsoft automatically updates hello version of hello fabric code running hello cluster.</span></span>  <span data-ttu-id="ae385-138">Definir o modo de Olá demasiado**Manual** se quiser demasiado[escolher uma versão suportada](service-fabric-cluster-upgrade.md) tooupgrade para.</span><span class="sxs-lookup"><span data-stu-id="ae385-138">Set hello mode too**Manual** if you want too[choose a supported version](service-fabric-cluster-upgrade.md) tooupgrade to.</span></span> 

    ![Configuração do tipo de nó][node-type-config]

    <span data-ttu-id="ae385-140">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae385-140">Select **OK**.</span></span>

7. <span data-ttu-id="ae385-141">Preencha Olá **segurança** formulário.</span><span class="sxs-lookup"><span data-stu-id="ae385-141">Fill out hello **Security** form.</span></span>  <span data-ttu-id="ae385-142">Para este guia de introdução, selecione **Inseguro**.</span><span class="sxs-lookup"><span data-stu-id="ae385-142">For this quick start select **Unsecure**.</span></span>  <span data-ttu-id="ae385-143">É altamente recomendado toocreate um cluster seguro para cargas de trabalho de produção, no entanto, uma vez que qualquer pessoa pode ligar a clusters não seguros tooan anonimamente e efetuar operações de gestão.</span><span class="sxs-lookup"><span data-stu-id="ae385-143">It is highly recommended toocreate a secure cluster for production workloads, however, since anyone can anonymously connect tooan unsecure cluster and perform management operations.</span></span>  

    <span data-ttu-id="ae385-144">Os certificados são utilizados no Service Fabric tooprovide autenticação e encriptação toosecure diferentes aspetos de um cluster e respetivas aplicações.</span><span class="sxs-lookup"><span data-stu-id="ae385-144">Certificates are used in Service Fabric tooprovide authentication and encryption toosecure various aspects of a cluster and its applications.</span></span> <span data-ttu-id="ae385-145">Para obter mais informações sobre como os certificados são utilizados no Service Fabric, consulte [Service Fabric cluster security scenarios (Cenários de segurança do cluster do Service Fabric)](service-fabric-cluster-security.md).</span><span class="sxs-lookup"><span data-stu-id="ae385-145">For more information on how certificates are used in Service Fabric, see [Service Fabric cluster security scenarios](service-fabric-cluster-security.md).</span></span>  <span data-ttu-id="ae385-146">com o Azure Active Directory ou tooset configurar certificados para uma segurança de aplicação, a autenticação de utilizador tooenable [criar um cluster a partir de um modelo do Resource Manager](service-fabric-cluster-creation-via-arm.md).</span><span class="sxs-lookup"><span data-stu-id="ae385-146">tooenable user authentication using Azure Active Directory or tooset up certificates for application security, [create a cluster from a Resource Manager template](service-fabric-cluster-creation-via-arm.md).</span></span>

    <span data-ttu-id="ae385-147">Selecione **OK**.</span><span class="sxs-lookup"><span data-stu-id="ae385-147">Select **OK**.</span></span>

8. <span data-ttu-id="ae385-148">Resumo de Olá de revisão.</span><span class="sxs-lookup"><span data-stu-id="ae385-148">Review hello summary.</span></span>  <span data-ttu-id="ae385-149">Se gostaria de toodownload um modelo do Resource Manager construído a partir das definições de Olá introduziu, selecione **transferir modelo e os parâmetros**.</span><span class="sxs-lookup"><span data-stu-id="ae385-149">If you'd like toodownload a Resource Manager template built from hello settings you entered, select **Download template and parameters**.</span></span>  <span data-ttu-id="ae385-150">Selecione **criar** cluster de Olá toocreate.</span><span class="sxs-lookup"><span data-stu-id="ae385-150">Select **Create** toocreate hello cluster.</span></span>

    <span data-ttu-id="ae385-151">Pode ver o progresso da criação Olá em notificações Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-151">You can see hello creation progress in hello notifications.</span></span> <span data-ttu-id="ae385-152">(Clique ícone de campainha"Olá" junto da barra de estado de Olá na Olá canto superior direito do ecrã). Se clicou em **Pin tooStartboard** ao criar o cluster de Olá, consulte **implementação de Cluster do Service Fabric** afixado toohello **iniciar** quadro.</span><span class="sxs-lookup"><span data-stu-id="ae385-152">(Click hello "Bell" icon near hello status bar at hello upper right of your screen.) If you clicked **Pin tooStartboard** while creating hello cluster, you see **Deploying Service Fabric Cluster** pinned toohello **Start** board.</span></span>

### <a name="view-cluster-status"></a><span data-ttu-id="ae385-153">Ver o estado do cluster</span><span class="sxs-lookup"><span data-stu-id="ae385-153">View cluster status</span></span>
<span data-ttu-id="ae385-154">Depois do cluster foi criado, pode inspecionar o cluster Olá **descrição geral** painel no portal de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-154">Once your cluster is created, you can inspect your cluster in hello **Overview** blade in hello portal.</span></span> <span data-ttu-id="ae385-155">Agora, pode ver os detalhes de Olá do cluster no dashboard de Olá, incluindo o ponto de final público do cluster Olá e tooService uma ligação Explorador de recursos de infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="ae385-155">You can now see hello details of your cluster in hello dashboard, including hello cluster's public endpoint and a link tooService Fabric Explorer.</span></span>

![Estado do cluster][cluster-status]

### <a name="visualize-hello-cluster-using-service-fabric-explorer"></a><span data-ttu-id="ae385-157">Visualizar o cluster de Olá através do Service Fabric explorer</span><span class="sxs-lookup"><span data-stu-id="ae385-157">Visualize hello cluster using Service Fabric explorer</span></span>
<span data-ttu-id="ae385-158">O [Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) é uma boa ferramenta para visualizar o seu cluster e gerir aplicações.</span><span class="sxs-lookup"><span data-stu-id="ae385-158">[Service Fabric Explorer](service-fabric-visualizing-your-cluster.md) is a good tool for visualizing your cluster and managing applications.</span></span>  <span data-ttu-id="ae385-159">Explorador de recursos de infraestrutura de serviço é um serviço que é executado no cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-159">Service Fabric Explorer is a service that runs in hello cluster.</span></span>  <span data-ttu-id="ae385-160">Aceder ao mesmo utilizando um browser clicando Olá **Service Fabric Explorer** ligação de cluster Olá **descrição geral** página Olá portal.</span><span class="sxs-lookup"><span data-stu-id="ae385-160">Access it using a web browser by clicking hello **Service Fabric Explorer** link of hello cluster **Overview** page in hello portal.</span></span>  <span data-ttu-id="ae385-161">Também pode introduzir o endereço de Olá diretamente no browser Olá: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span><span class="sxs-lookup"><span data-stu-id="ae385-161">You can also enter hello address directly into hello browser: [http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer](http://quickstartcluster.westus.cloudapp.azure.com:19080/Explorer)</span></span>

<span data-ttu-id="ae385-162">dashboard de cluster Olá fornece uma descrição geral do cluster, incluindo um resumo das aplicações e estado de funcionamento do nó.</span><span class="sxs-lookup"><span data-stu-id="ae385-162">hello cluster dashboard provides an overview of your cluster, including a summary of application and node health.</span></span> <span data-ttu-id="ae385-163">Vista de nó de Olá mostra o esquema físico do Olá do cluster de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-163">hello node view shows hello physical layout of hello cluster.</span></span> <span data-ttu-id="ae385-164">Para um determinado nó, pode inspecionar as aplicações que têm um código implementado nesse nó.</span><span class="sxs-lookup"><span data-stu-id="ae385-164">For a given node, you can inspect which applications have code deployed on that node.</span></span>

![Service Fabric Explorer][service-fabric-explorer]

### <a name="connect-toohello-cluster-using-powershell"></a><span data-ttu-id="ae385-166">Ligue o cluster de toohello através do PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae385-166">Connect toohello cluster using PowerShell</span></span>
<span data-ttu-id="ae385-167">Certifique-se de que esse cluster Olá está em execução, ligando-se com o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae385-167">Verify that hello cluster is running by connecting using PowerShell.</span></span>  <span data-ttu-id="ae385-168">Olá ServiceFabric módulo do PowerShell é instalado com Olá [SDK de Service Fabric](service-fabric-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ae385-168">hello ServiceFabric PowerShell module is installed with hello [Service Fabric SDK](service-fabric-get-started.md).</span></span>  <span data-ttu-id="ae385-169">Olá [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet estabelece um cluster de toohello de ligação.</span><span class="sxs-lookup"><span data-stu-id="ae385-169">hello [Connect-ServiceFabricCluster](/powershell/module/servicefabric/connect-servicefabriccluster?view=azureservicefabricps) cmdlet establishes a connection toohello cluster.</span></span>   

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint quickstartcluster.westus2.cloudapp.azure.com:19000
```
<span data-ttu-id="ae385-170">Consulte [Connect tooa segura cluster](service-fabric-connect-to-secure-cluster.md) para outros exemplos de ligação de tooa de cluster.</span><span class="sxs-lookup"><span data-stu-id="ae385-170">See [Connect tooa secure cluster](service-fabric-connect-to-secure-cluster.md) for other examples of connecting tooa cluster.</span></span> <span data-ttu-id="ae385-171">Depois de estabelecer ligação toohello cluster, utilize Olá [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay uma lista de nós no Olá cluster e informações de estado para cada nó.</span><span class="sxs-lookup"><span data-stu-id="ae385-171">After connecting toohello cluster, use hello [Get-ServiceFabricNode](/powershell/module/servicefabric/get-servicefabricnode?view=azureservicefabricps) cmdlet toodisplay a list of nodes in hello cluster and status information for each node.</span></span> <span data-ttu-id="ae385-172">O **HealthState** deve ser *OK* para cada nó.</span><span class="sxs-lookup"><span data-stu-id="ae385-172">**HealthState** should be *OK* for each node.</span></span>

```powershell
PS C:\Users\sfuser> Get-ServiceFabricNode |Format-Table

NodeDeactivationInfo NodeName     IpAddressOrFQDN NodeType  CodeVersion  ConfigVersion NodeStatus NodeUpTime NodeDownTime HealthState
-------------------- --------     --------------- --------  -----------  ------------- ---------- ---------- ------------ -----------
                     _nodetype1_2 10.0.0.6        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_1 10.0.0.5        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_0 10.0.0.4        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_4 10.0.0.8        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
                     _nodetype1_3 10.0.0.7        nodetype1 5.7.198.9494 1                     Up 03:00:38   00:00:00              Ok
```

### <a name="remove-hello-cluster"></a><span data-ttu-id="ae385-173">Remover cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ae385-173">Remove hello cluster</span></span>
<span data-ttu-id="ae385-174">Um cluster do Service Fabric é constituído por outros recursos do Azure Ademais toohello recurso de cluster em si.</span><span class="sxs-lookup"><span data-stu-id="ae385-174">A Service Fabric cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ae385-175">Pelo toocompletely eliminar um cluster do Service Fabric também precisa de toodelete que Olá todos os recursos que é composto.</span><span class="sxs-lookup"><span data-stu-id="ae385-175">So toocompletely delete a Service Fabric cluster you also need toodelete all hello resources it is made of.</span></span> <span data-ttu-id="ae385-176">cluster de Olá para Olá mais simples forma toodelete e todos os recursos de Olá que consome é o grupo de recursos de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="ae385-176">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> <span data-ttu-id="ae385-177">Para outro toodelete formas um cluster ou toodelete algumas (mas não todos) recursos de Olá num grupo de recursos, consulte [eliminar um cluster](service-fabric-cluster-delete.md)</span><span class="sxs-lookup"><span data-stu-id="ae385-177">For other ways toodelete a cluster or toodelete some (but not all) hello resources in a resource group, see [Delete a cluster](service-fabric-cluster-delete.md)</span></span>

<span data-ttu-id="ae385-178">Elimine um grupo de recursos no Olá portal do Azure:</span><span class="sxs-lookup"><span data-stu-id="ae385-178">Delete a resource group in hello Azure portal:</span></span>
1. <span data-ttu-id="ae385-179">Navegue de cluster do Service Fabric toohello pretende toodelete.</span><span class="sxs-lookup"><span data-stu-id="ae385-179">Navigate toohello Service Fabric cluster you want toodelete.</span></span>
2. <span data-ttu-id="ae385-180">Clique em Olá **grupo de recursos** nome na página do Olá cluster essentials.</span><span class="sxs-lookup"><span data-stu-id="ae385-180">Click hello **Resource Group** name on hello cluster essentials page.</span></span>
3. <span data-ttu-id="ae385-181">No Olá **Essentials do grupo de recursos** página, clique em **eliminar grupo de recursos** e siga as instruções de Olá nessa página toocomplete Olá a eliminação do grupo de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-181">In hello **Resource Group Essentials** page, click **Delete resource group** and follow hello instructions on that page toocomplete hello deletion of hello resource group.</span></span>
    <span data-ttu-id="ae385-182">![Eliminar grupo de recursos de Olá][cluster-delete]</span><span class="sxs-lookup"><span data-stu-id="ae385-182">![Delete hello resource group][cluster-delete]</span></span>


## <a name="use-azure-powershell-toodeploy-a-secure-cluster"></a><span data-ttu-id="ae385-183">Utilizar o Azure Powershell toodeploy um cluster seguro</span><span class="sxs-lookup"><span data-stu-id="ae385-183">Use Azure Powershell toodeploy a secure cluster</span></span>
1. <span data-ttu-id="ae385-184">Transferir Olá [Azure Powershell versão 4.0 ou superior do módulo](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) no seu computador.</span><span class="sxs-lookup"><span data-stu-id="ae385-184">Download hello [Azure Powershell module version 4.0 or higher](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) on your machine.</span></span>

2. <span data-ttu-id="ae385-185">Abra uma janela do Windows PowerShell, Olá de executar os seguintes comandos.</span><span class="sxs-lookup"><span data-stu-id="ae385-185">Open a Windows PowerShell window, Run hello following command.</span></span> 
    
    ```powershell

    Get-Command -Module AzureRM.ServiceFabric 
    ```

    <span data-ttu-id="ae385-186">Deverá ver um resultado semelhante toohello seguintes procedimentos.</span><span class="sxs-lookup"><span data-stu-id="ae385-186">You should see an output similar toohello following.</span></span>

    ![ps-list][ps-list]

3. <span data-ttu-id="ae385-188">Início de sessão tooAzure e selecione Olá subscrição toowhich pretende que o cluster de Olá toocreate</span><span class="sxs-lookup"><span data-stu-id="ae385-188">Login tooAzure and Select hello subscription toowhich you want toocreate hello cluster</span></span>

    ```powershell

    Login-AzureRmAccount

    Select-AzureRmSubscription -SubscriptionId "Subcription ID" 
    ```

4. <span data-ttu-id="ae385-189">Olá execute os seguintes comandos toonow criar um cluster seguro.</span><span class="sxs-lookup"><span data-stu-id="ae385-189">Run hello following command toonow create a secure cluster.</span></span> <span data-ttu-id="ae385-190">Não se esqueça de parâmetros de Olá toocustomize.</span><span class="sxs-lookup"><span data-stu-id="ae385-190">Do not forget toocustomize hello parameters.</span></span> 

    ```powershell
    $certpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force
    $RDPpwd="Password#1234" | ConvertTo-SecureString -AsPlainText -Force 
    $RDPuser="vmadmin"
    $RGname="mycluster" # this is also hello name of your cluster
    $clusterloc="SouthCentralUS"
    $subname="$RGname.$clusterloc.cloudapp.azure.com"
    $certfolder="c:\mycertificates\"
    $clustersize=1 # can take values 1, 3-99

    New-AzureRmServiceFabricCluster -ResourceGroupName $RGname -Location $clusterloc -ClusterSize $clustersize -VmUserName $RDPuser -VmPassword $RDPpwd -CertificateSubjectName $subname -CertificatePassword $certpwd -CertificateOutputFolder $certfolder
    ```

    <span data-ttu-id="ae385-191">comando Olá pode tomar entre toocomplete minutos, too30 10 minutos, no fim Olá, deve obter um resultado semelhante toohello seguintes procedimentos.</span><span class="sxs-lookup"><span data-stu-id="ae385-191">hello command can take anywhere from 10 minutes too30 minutes toocomplete, at hello end of it, you should get an output similar toohello following.</span></span> <span data-ttu-id="ae385-192">saída de Olá tem informações sobre o certificado de Olá, Olá KeyVault em que foi carregado, e Olá pasta local onde o certificado de Olá é copiado.</span><span class="sxs-lookup"><span data-stu-id="ae385-192">hello output has information about hello certificate, hello KeyVault where it was uploaded to, and hello local folder where hello certificate is copied.</span></span> 

    ![ps-out][ps-out]

5. <span data-ttu-id="ae385-194">Copiar resultado completo Olá e guarde o ficheiro de texto tooa como precisamos toorefer tooit.</span><span class="sxs-lookup"><span data-stu-id="ae385-194">Copy hello entire output and save tooa text file as we need toorefer tooit.</span></span> <span data-ttu-id="ae385-195">Tome nota do Olá seguintes informações de saída de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-195">Make a note of hello following information from hello output.</span></span> 

    - <span data-ttu-id="ae385-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span><span class="sxs-lookup"><span data-stu-id="ae385-196">**CertificateSavedLocalPath** : c:\mycertificates\mycluster20170504141137.pfx</span></span>
    - <span data-ttu-id="ae385-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span><span class="sxs-lookup"><span data-stu-id="ae385-197">**CertificateThumbprint** : C4C1E541AD512B8065280292A8BA6079C3F26F10</span></span>
    - <span data-ttu-id="ae385-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span><span class="sxs-lookup"><span data-stu-id="ae385-198">**ManagementEndpoint** : https://mycluster.southcentralus.cloudapp.azure.com:19080</span></span>
    - <span data-ttu-id="ae385-199">**ClientConnectionEndpointPort** : 19000</span><span class="sxs-lookup"><span data-stu-id="ae385-199">**ClientConnectionEndpointPort** : 19000</span></span>

### <a name="install-hello-certificate-on-your-local-machine"></a><span data-ttu-id="ae385-200">Instalar o certificado de Olá no seu computador local</span><span class="sxs-lookup"><span data-stu-id="ae385-200">Install hello certificate on your local machine</span></span>
  
<span data-ttu-id="ae385-201">tooconnect toohello cluster, precisa de tooinstall Olá certificado no arquivo de pessoais (os meus) Olá do utilizador atual Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-201">tooconnect toohello cluster, you need tooinstall hello certificate into hello Personal (My) store of hello current user.</span></span> 

<span data-ttu-id="ae385-202">Executar Olá seguir PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae385-202">Run hello following PowerShell</span></span>

```powershell
Import-PfxCertificate -Exportable -CertStoreLocation Cert:\CurrentUser\My `
        -FilePath C:\mycertificates\hello name of hello cert.pfx `
        -Password (ConvertTo-SecureString -String certpwd -AsPlainText -Force)
```

<span data-ttu-id="ae385-203">Agora, está pronto tooconnect tooyour segura cluster.</span><span class="sxs-lookup"><span data-stu-id="ae385-203">You are now ready tooconnect tooyour secure cluster.</span></span>

### <a name="connect-tooa-secure-cluster"></a><span data-ttu-id="ae385-204">Ligue o cluster segura tooa</span><span class="sxs-lookup"><span data-stu-id="ae385-204">Connect tooa secure cluster</span></span> 

<span data-ttu-id="ae385-205">Execute o seguinte de Olá de comando do PowerShell tooconnect tooa segura cluster.</span><span class="sxs-lookup"><span data-stu-id="ae385-205">Run hello following PowerShell command tooconnect tooa secure cluster.</span></span> <span data-ttu-id="ae385-206">Detalhes do certificado Olá devem coincidir com um certificado que foi utilizado tooset segurança cluster Olá.</span><span class="sxs-lookup"><span data-stu-id="ae385-206">hello certificate details must match a certificate that was used tooset up hello cluster.</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint <Cluster FQDN>:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint <Certificate Thumbprint> `
          -FindType FindByThumbprint -FindValue <Certificate Thumbprint> `
          -StoreLocation CurrentUser -StoreName My
```


<span data-ttu-id="ae385-207">Olá seguinte exemplo mostra Olá parâmetros completed:</span><span class="sxs-lookup"><span data-stu-id="ae385-207">hello following example shows hello completed parameters:</span></span> 

```powershell
Connect-ServiceFabricCluster -ConnectionEndpoint mycluster.southcentralus.cloudapp.azure.com:19000 `
          -KeepAliveIntervalInSec 10 `
          -X509Credential -ServerCertThumbprint C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -FindType FindByThumbprint -FindValue C4C1E541AD512B8065280292A8BA6079C3F26F10 `
          -StoreLocation CurrentUser -StoreName My
```

<span data-ttu-id="ae385-208">Execute Olá seguir toocheck comandos que estão ligadas e cluster Olá está em bom estado.</span><span class="sxs-lookup"><span data-stu-id="ae385-208">Run hello following command toocheck that you are connected and hello cluster is healthy.</span></span>

```powershell

Get-ServiceFabricClusterHealth

```
### <a name="publish-your-apps-tooyour-cluster-from-visual-studio"></a><span data-ttu-id="ae385-209">Publicar o seu cluster tooyour de aplicações a partir do Visual Studio</span><span class="sxs-lookup"><span data-stu-id="ae385-209">Publish your apps tooyour cluster from Visual Studio</span></span>

<span data-ttu-id="ae385-210">Agora que configurou um cluster do Azure, pode publicar o seu tooit de aplicações a partir do Visual Studio por Olá seguinte [publicar tooan cluster](service-fabric-publish-app-remote-cluster.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ae385-210">Now that you have set up an Azure cluster, you can publish your applications tooit from Visual Studio by following hello [Publish tooan cluster](service-fabric-publish-app-remote-cluster.md) document.</span></span> 

### <a name="remove-hello-cluster"></a><span data-ttu-id="ae385-211">Remover cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ae385-211">Remove hello cluster</span></span>
<span data-ttu-id="ae385-212">Um cluster é constituído por outros recursos do Azure Ademais toohello recurso de cluster em si.</span><span class="sxs-lookup"><span data-stu-id="ae385-212">A cluster is made up of other Azure resources in addition toohello cluster resource itself.</span></span> <span data-ttu-id="ae385-213">cluster de Olá para Olá mais simples forma toodelete e todos os recursos de Olá que consome é o grupo de recursos de Olá toodelete.</span><span class="sxs-lookup"><span data-stu-id="ae385-213">hello simplest way toodelete hello cluster and all hello resources it consumes is toodelete hello resource group.</span></span> 

```powershell

Remove-AzureRmResourceGroup -Name $RGname -Force

```

## <a name="next-steps"></a><span data-ttu-id="ae385-214">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ae385-214">Next steps</span></span>
<span data-ttu-id="ae385-215">Agora que configurou um cluster de desenvolvimento, experimente o seguinte Olá:</span><span class="sxs-lookup"><span data-stu-id="ae385-215">Now that you have set up a development cluster, try hello following:</span></span>
* [<span data-ttu-id="ae385-216">Criar um cluster seguro no portal de Olá</span><span class="sxs-lookup"><span data-stu-id="ae385-216">Create a secure cluster in hello portal</span></span>](service-fabric-cluster-creation-via-portal.md)
* [<span data-ttu-id="ae385-217">Criar um cluster a partir de um modelo</span><span class="sxs-lookup"><span data-stu-id="ae385-217">Create a cluster from a template</span></span>](service-fabric-cluster-creation-via-arm.md) 
* [<span data-ttu-id="ae385-218">Implementar aplicações com o Powershell</span><span class="sxs-lookup"><span data-stu-id="ae385-218">Deploy apps using PowerShell</span></span>](service-fabric-deploy-remove-applications.md)


[cluster-setup-basics]: ./media/service-fabric-get-started-azure-cluster/basics.png
[node-type-config]: ./media/service-fabric-get-started-azure-cluster/nodetypeconfig.png
[cluster-status]: ./media/service-fabric-get-started-azure-cluster/clusterstatus.png
[service-fabric-explorer]: ./media/service-fabric-get-started-azure-cluster/sfx.png
[cluster-delete]: ./media/service-fabric-get-started-azure-cluster/delete.png
[ps-list]: ./media/service-fabric-get-started-azure-cluster/pslist.PNG
[ps-out]: ./media/service-fabric-get-started-azure-cluster/psout.PNG
