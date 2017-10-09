---
title: "aaaConfigure um serviço de escuta do ILB Always On para grupos de disponibilidade no Azure | Microsoft Docs"
description: "Este tutorial utiliza recursos criados no modelo de implementação clássica Olá e cria uma escuta do grupo Always On disponibilidade no Azure que utiliza um balanceador de carga interno."
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 291288a0-740b-4cfa-af62-053218beba77
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 05/02/2017
ms.author: mikeray
ms.openlocfilehash: 2ce9b64fea491c945b58f7641e41fd39d90b078a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="configure-an-ilb-listener-for-always-on-availability-groups-in-azure"></a><span data-ttu-id="ae35c-103">Configurar um serviço de escuta do ILB para grupos de disponibilidade Always On no Azure</span><span class="sxs-lookup"><span data-stu-id="ae35c-103">Configure an ILB listener for Always On availability groups in Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ae35c-104">Serviço de escuta interno</span><span class="sxs-lookup"><span data-stu-id="ae35c-104">Internal listener</span></span>](../classic/ps-sql-int-listener.md)
> * [<span data-ttu-id="ae35c-105">Serviço de escuta externo</span><span class="sxs-lookup"><span data-stu-id="ae35c-105">External listener</span></span>](../classic/ps-sql-ext-listener.md)
>
>

## <a name="overview"></a><span data-ttu-id="ae35c-106">Descrição geral</span><span class="sxs-lookup"><span data-stu-id="ae35c-106">Overview</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ae35c-107">O Azure tem dois modelos de implementação diferentes para criar e trabalhar com recursos: [do Azure Resource Manager e clássico](../../../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="ae35c-107">Azure has two different deployment models for creating and working with resources: [Azure Resource Manager and classic](../../../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="ae35c-108">Este artigo abrange a utilização de Olá do modelo de implementação clássica Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-108">This article covers hello use of hello classic deployment model.</span></span> <span data-ttu-id="ae35c-109">Recomendamos que as implementações mais novas utilizem o modelo de Gestor de recursos de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-109">We recommend that most new deployments use hello Resource Manager model.</span></span>

<span data-ttu-id="ae35c-110">tooconfigure um serviço de escuta para um grupo de disponibilidade Always On no modelo do Resource Manager Olá, consulte [configurar um balanceador de carga para um grupo de disponibilidade Always On no Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span><span class="sxs-lookup"><span data-stu-id="ae35c-110">tooconfigure a listener for an Always On availability group in hello Resource Manager model, see [Configure a load balancer for an Always On availability group in Azure](../sql/virtual-machines-windows-portal-sql-alwayson-int-listener.md).</span></span>

<span data-ttu-id="ae35c-111">O grupo de disponibilidade pode conter réplicas que são apenas no local ou para o Azure apenas, ou que abrangem no local e o Azure para configurações híbridas.</span><span class="sxs-lookup"><span data-stu-id="ae35c-111">Your availability group can contain replicas that are on-premises only or Azure only, or that span both on-premises and Azure for hybrid configurations.</span></span> <span data-ttu-id="ae35c-112">As réplicas do Azure podem residir no Olá mesma região ou em várias regiões que utilizem várias redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ae35c-112">Azure replicas can reside within hello same region or across multiple regions that use multiple virtual networks.</span></span> <span data-ttu-id="ae35c-113">Olá procedimentos neste artigo partem do princípio de que já tem [configurado um grupo de disponibilidade](../classic/portal-sql-alwayson-availability-groups.md) , mas ainda não tiver configurado um serviço de escuta.</span><span class="sxs-lookup"><span data-stu-id="ae35c-113">hello procedures in this article assume that you have already [configured an availability group](../classic/portal-sql-alwayson-availability-groups.md) but have not yet configured a listener.</span></span>

## <a name="guidelines-and-limitations-for-internal-listeners"></a><span data-ttu-id="ae35c-114">Diretrizes e limitações para os serviços de escuta internas</span><span class="sxs-lookup"><span data-stu-id="ae35c-114">Guidelines and limitations for internal listeners</span></span>
<span data-ttu-id="ae35c-115">utilização Olá um balanceador de carga interno (ILB) com um serviço de escuta do grupo de disponibilidade no Azure é toohello requerente seguintes diretrizes:</span><span class="sxs-lookup"><span data-stu-id="ae35c-115">hello use of an internal load balancer (ILB) with an availability group listener in Azure is subject toohello following guidelines:</span></span>

* <span data-ttu-id="ae35c-116">escuta do grupo de disponibilidade de hello é suportada no Windows Server 2008 R2, Windows Server 2012 e Windows Server 2012 R2.</span><span class="sxs-lookup"><span data-stu-id="ae35c-116">hello availability group listener is supported on Windows Server 2008 R2, Windows Server 2012, and Windows Server 2012 R2.</span></span>
* <span data-ttu-id="ae35c-117">Apenas uma escuta do grupo de disponibilidade interno é suportada para cada serviço em nuvem, porque o serviço de escuta de Olá é configurado toohello ILB, e não existe apenas um ILB para cada serviço em nuvem.</span><span class="sxs-lookup"><span data-stu-id="ae35c-117">Only one internal availability group listener is supported for each cloud service, because hello listener is configured toohello ILB, and there is only one ILB for each cloud service.</span></span> <span data-ttu-id="ae35c-118">No entanto, é possível toocreate vários serviços de escuta externos.</span><span class="sxs-lookup"><span data-stu-id="ae35c-118">However, it is possible toocreate multiple external listeners.</span></span> <span data-ttu-id="ae35c-119">Para obter mais informações, consulte [configurar um serviço de escuta externo para grupos de disponibilidade Always On no Azure](../classic/ps-sql-ext-listener.md).</span><span class="sxs-lookup"><span data-stu-id="ae35c-119">For more information, see [Configure an external listener for Always On availability groups in Azure](../classic/ps-sql-ext-listener.md).</span></span>

## <a name="determine-hello-accessibility-of-hello-listener"></a><span data-ttu-id="ae35c-120">Determinar a acessibilidade de Olá do serviço de escuta de Olá</span><span class="sxs-lookup"><span data-stu-id="ae35c-120">Determine hello accessibility of hello listener</span></span>
[!INCLUDE [ag-listener-accessibility](../../../../includes/virtual-machines-ag-listener-determine-accessibility.md)]

<span data-ttu-id="ae35c-121">Este artigo foca-se sobre a criação de um serviço de escuta que utiliza um ILB.</span><span class="sxs-lookup"><span data-stu-id="ae35c-121">This article focuses on creating a listener that uses an ILB.</span></span> <span data-ttu-id="ae35c-122">Se precisar de um serviço de escuta público ou externo, consulte a versão de Olá deste artigo que descreve a definição de segurança de um [escuta externa](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ae35c-122">If you need an public or external listener, see hello version of this article that discusses setting up an [external listener](../classic/ps-sql-ext-listener.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="create-load-balanced-vm-endpoints-with-direct-server-return"></a><span data-ttu-id="ae35c-123">Criar os pontos finais VM com balanceamento de carga com direta do servidor retorno</span><span class="sxs-lookup"><span data-stu-id="ae35c-123">Create load-balanced VM endpoints with direct server return</span></span>
<span data-ttu-id="ae35c-124">Cria um ILB pela primeira vez ao executar o script de Olá posteriormente nesta secção.</span><span class="sxs-lookup"><span data-stu-id="ae35c-124">You first create an ILB by running hello script later in this section.</span></span>

<span data-ttu-id="ae35c-125">Crie um ponto final com balanceamento de carga para cada VM que aloja uma réplica do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae35c-125">Create a load-balanced endpoint for each VM that hosts an Azure replica.</span></span> <span data-ttu-id="ae35c-126">Se tiver réplicas em várias regiões, cada réplica para essa região tem de ser Olá mesmo serviço de nuvem Olá mesma rede virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae35c-126">If you have replicas in multiple regions, each replica for that region must be in hello same cloud service in hello same Azure virtual network.</span></span> <span data-ttu-id="ae35c-127">Criação de réplicas do grupo que abrangem várias regiões do Azure de disponibilidade necessita de configurar várias redes virtuais.</span><span class="sxs-lookup"><span data-stu-id="ae35c-127">Creating availability group replicas that span multiple Azure regions requires configuring multiple virtual networks.</span></span> <span data-ttu-id="ae35c-128">Para obter mais informações sobre como configurar cruzada conectividade de rede virtual, consulte [configurar a conectividade de rede de toovirtual de rede virtual](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span><span class="sxs-lookup"><span data-stu-id="ae35c-128">For more information on configuring cross virtual network connectivity, see [Configure virtual network toovirtual network connectivity](../../../vpn-gateway/virtual-networks-configure-vnet-to-vnet-connection.md).</span></span>

1. <span data-ttu-id="ae35c-129">No portal do Azure Olá, visite tooeach VM que aloja um detalhes da réplica tooview Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-129">In hello Azure portal, go tooeach VM that hosts a replica tooview hello details.</span></span>

2. <span data-ttu-id="ae35c-130">Clique em Olá **pontos finais** separador para cada VM.</span><span class="sxs-lookup"><span data-stu-id="ae35c-130">Click hello **Endpoints** tab for each VM.</span></span>

3. <span data-ttu-id="ae35c-131">Certifique-se de que Olá **nome** e **Porta pública** do ponto final de serviço de escuta de Olá que pretende que sejam toouse ainda não estiverem em utilização.</span><span class="sxs-lookup"><span data-stu-id="ae35c-131">Verify that hello **Name** and **Public Port** of hello listener endpoint that you want toouse are not already in use.</span></span> <span data-ttu-id="ae35c-132">Exemplo de Olá nesta secção, é o nome de Olá *MyEndpoint*, e é a porta de Olá *1433*.</span><span class="sxs-lookup"><span data-stu-id="ae35c-132">In hello example in this section, hello name is *MyEndpoint*, and hello port is *1433*.</span></span>

4. <span data-ttu-id="ae35c-133">No seu cliente local, transfira e instale os mais recentes Olá [módulo do PowerShell](https://azure.microsoft.com/downloads/).</span><span class="sxs-lookup"><span data-stu-id="ae35c-133">On your local client, download and install hello latest [PowerShell module](https://azure.microsoft.com/downloads/).</span></span>

5. <span data-ttu-id="ae35c-134">Inicie o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae35c-134">Start Azure PowerShell.</span></span>  
    <span data-ttu-id="ae35c-135">Abre uma nova sessão do PowerShell, com Olá Azure administrativos módulos carregados.</span><span class="sxs-lookup"><span data-stu-id="ae35c-135">A new PowerShell session opens, with hello Azure administrative modules loaded.</span></span>

6. <span data-ttu-id="ae35c-136">Execute `Get-AzurePublishSettingsFile`.</span><span class="sxs-lookup"><span data-stu-id="ae35c-136">Run `Get-AzurePublishSettingsFile`.</span></span> <span data-ttu-id="ae35c-137">Este cmdlet direciona toodownload de browser tooa um publicar definições ficheiro tooa diretório local.</span><span class="sxs-lookup"><span data-stu-id="ae35c-137">This cmdlet directs you tooa browser toodownload a publish settings file tooa local directory.</span></span> <span data-ttu-id="ae35c-138">Pode ser pedido para as credenciais de início de sessão para a sua subscrição do Azure.</span><span class="sxs-lookup"><span data-stu-id="ae35c-138">You might be prompted for your sign-in credentials for your Azure subscription.</span></span>

7. <span data-ttu-id="ae35c-139">Execute o seguinte de Olá `Import-AzurePublishSettingsFile` comando com o caminho de Olá de Olá publicar o ficheiro de definições que transferiu a:</span><span class="sxs-lookup"><span data-stu-id="ae35c-139">Run hello following `Import-AzurePublishSettingsFile` command with hello path of hello publish settings file that you downloaded:</span></span>

        Import-AzurePublishSettingsFile -PublishSettingsFile <PublishSettingsFilePath>

    <span data-ttu-id="ae35c-140">Depois de publicar Olá importado do ficheiro de definições, pode gerir a sua subscrição do Azure numa sessão do PowerShell de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-140">After hello publish settings file is imported, you can manage your Azure subscription in hello PowerShell session.</span></span>

8. <span data-ttu-id="ae35c-141">Para *ILB*, atribuir um endereço IP estático.</span><span class="sxs-lookup"><span data-stu-id="ae35c-141">For *ILB*, assign a static IP address.</span></span> <span data-ttu-id="ae35c-142">Examine a configuração de rede virtual atual Olá executando Olá os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="ae35c-142">Examine hello current virtual network configuration by running hello following command:</span></span>

        (Get-AzureVNetConfig).XMLConfiguration
9. <span data-ttu-id="ae35c-143">Olá nota *sub-rede* nome para a sub-rede de Olá que contenha VMs Olá que alojam as réplicas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-143">Note hello *Subnet* name for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="ae35c-144">Este nome é utilizado no parâmetro Olá $SubnetName no script de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-144">This name is used in hello $SubnetName parameter in hello script.</span></span>

10. <span data-ttu-id="ae35c-145">Olá nota *VirtualNetworkSite* name e Olá iniciar *AddressPrefix* para sub-rede Olá que contenha VMs Olá que alojam as réplicas de Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-145">Note hello *VirtualNetworkSite* name and hello starting *AddressPrefix* for hello subnet that contains hello VMs that host hello replicas.</span></span> <span data-ttu-id="ae35c-146">Procurar um endereço IP disponível através da transmissão de ambos os valores toohello `Test-AzureStaticVNetIP` comando e, examinando Olá *AvailableAddresses*.</span><span class="sxs-lookup"><span data-stu-id="ae35c-146">Look for an available IP address by passing both values toohello `Test-AzureStaticVNetIP` command and by examining hello *AvailableAddresses*.</span></span> <span data-ttu-id="ae35c-147">Por exemplo, se hello rede virtual é denominada *MyVNet* e tem um intervalo de endereços de sub-rede que inicia no *172.16.0.128*, seguinte Olá comando seria lista endereços disponíveis:</span><span class="sxs-lookup"><span data-stu-id="ae35c-147">For example, if hello virtual network is named *MyVNet* and has a subnet address range that starts at *172.16.0.128*, hello following command would list available addresses:</span></span>

        (Test-AzureStaticVNetIP -VNetName "MyVNet"-IPAddress 172.16.0.128).AvailableAddresses
11. <span data-ttu-id="ae35c-148">Selecione um dos endereços disponíveis Olá e utilizá-lo no parâmetro Olá $ILBStaticIP do script Olá no passo seguinte Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-148">Select one of hello available addresses, and use it in hello $ILBStaticIP parameter of hello script in hello next step.</span></span>

12. <span data-ttu-id="ae35c-149">Copiar Olá seguir o editor de texto de tooa de script do PowerShell e defina Olá valores das variáveis toosuit seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ae35c-149">Copy hello following PowerShell script tooa text editor, and set hello variable values toosuit your environment.</span></span> <span data-ttu-id="ae35c-150">As predefinições foram fornecidas para alguns parâmetros.</span><span class="sxs-lookup"><span data-stu-id="ae35c-150">Defaults have been provided for some parameters.</span></span>  

    <span data-ttu-id="ae35c-151">As implementações existentes que utilizam grupos de afinidade não é possível adicionar um ILB.</span><span class="sxs-lookup"><span data-stu-id="ae35c-151">Existing deployments that use affinity groups cannot add an ILB.</span></span> <span data-ttu-id="ae35c-152">Para obter mais informações sobre os requisitos do ILB, consulte [descrição geral do Balanceador de carga interno](../../../load-balancer/load-balancer-internal-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ae35c-152">For more information about ILB requirements, see [Internal load balancer overview](../../../load-balancer/load-balancer-internal-overview.md).</span></span>

    <span data-ttu-id="ae35c-153">Além disso, se o grupo de disponibilidade abranger regiões do Azure, tem de executar o script de Olá uma vez cada centro de dados para o serviço em nuvem Olá e nós que residem em que Centro de dados.</span><span class="sxs-lookup"><span data-stu-id="ae35c-153">Also, if your availability group spans Azure regions, you must run hello script once in each datacenter for hello cloud service and nodes that reside in that datacenter.</span></span>

        # Define variables
        $ServiceName = "<MyCloudService>" # hello name of hello cloud service that contains hello availability group nodes
        $AGNodes = "<VM1>","<VM2>","<VM3>" # all availability group nodes containing replicas in hello same cloud service, separated by commas
        $SubnetName = "<MySubnetName>" # subnet name that hello replicas use in hello virtual network
        $ILBStaticIP = "<MyILBStaticIPAddress>" # static IP address for hello ILB in hello subnet
        $ILBName = "AGListenerLB" # customize hello ILB name or use this default value

        # Create hello ILB
        Add-AzureInternalLoadBalancer -InternalLoadBalancerName $ILBName -SubnetName $SubnetName -ServiceName $ServiceName -StaticVNetIPAddress $ILBStaticIP

        # Configure a load-balanced endpoint for each node in $AGNodes by using ILB
        ForEach ($node in $AGNodes)
        {
            Get-AzureVM -ServiceName $ServiceName -Name $node | Add-AzureEndpoint -Name "ListenerEndpoint" -LBSetName "ListenerEndpointLB" -Protocol tcp -LocalPort 1433 -PublicPort 1433 -ProbePort 59999 -ProbeProtocol tcp -ProbeIntervalInSeconds 10 -InternalLoadBalancerName $ILBName -DirectServerReturn $true | Update-AzureVM
        }

13. <span data-ttu-id="ae35c-154">Após definir variáveis de Olá, Olá cópia script de Olá texto editor tooyour PowerShell sessão toorun-lo.</span><span class="sxs-lookup"><span data-stu-id="ae35c-154">After you have set hello variables, copy hello script from hello text editor tooyour PowerShell session toorun it.</span></span> <span data-ttu-id="ae35c-155">Se a linha de Olá continua a mostrar  **>>** , prima Enter novamente o script de Olá se toomake entra em execução.</span><span class="sxs-lookup"><span data-stu-id="ae35c-155">If hello prompt still shows **>>**, press Enter again toomake sure hello script starts running.</span></span>

## <a name="verify-that-kb2854082-is-installed-if-necessary"></a><span data-ttu-id="ae35c-156">Certifique-se de que KB2854082 está instalado, se necessário</span><span class="sxs-lookup"><span data-stu-id="ae35c-156">Verify that KB2854082 is installed if necessary</span></span>
[!INCLUDE [kb2854082](../../../../includes/virtual-machines-ag-listener-kb2854082.md)]

## <a name="open-hello-firewall-ports-in-availability-group-nodes"></a><span data-ttu-id="ae35c-157">Abrir portas de firewall de Olá em nós do grupo de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="ae35c-157">Open hello firewall ports in availability group nodes</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-open-firewall.md)]

## <a name="create-hello-availability-group-listener"></a><span data-ttu-id="ae35c-158">Criar a escuta do grupo de disponibilidade de Olá</span><span class="sxs-lookup"><span data-stu-id="ae35c-158">Create hello availability group listener</span></span>

<span data-ttu-id="ae35c-159">Crie a escuta do grupo de disponibilidade de Olá em dois passos.</span><span class="sxs-lookup"><span data-stu-id="ae35c-159">Create hello availability group listener in two steps.</span></span> <span data-ttu-id="ae35c-160">Em primeiro lugar, crie o recurso de cluster de ponto de acesso de cliente de Olá e configurar as dependências.</span><span class="sxs-lookup"><span data-stu-id="ae35c-160">First, create hello client access point cluster resource and configure  dependencies.</span></span> <span data-ttu-id="ae35c-161">Segundo, configure os recursos do cluster Olá no PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ae35c-161">Second, configure hello cluster resources in PowerShell.</span></span>

### <a name="create-hello-client-access-point-and-configure-hello-cluster-dependencies"></a><span data-ttu-id="ae35c-162">Criar ponto de acesso de cliente Olá e configurar as dependências de cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ae35c-162">Create hello client access point and configure hello cluster dependencies</span></span>
[!INCLUDE [firewall](../../../../includes/virtual-machines-ag-listener-create-listener.md)]

### <a name="configure-hello-cluster-resources-in-powershell"></a><span data-ttu-id="ae35c-163">Configurar recursos de cluster Olá no PowerShell</span><span class="sxs-lookup"><span data-stu-id="ae35c-163">Configure hello cluster resources in PowerShell</span></span>
1. <span data-ttu-id="ae35c-164">Para o ILB, tem de utilizar o endereço IP Olá Olá ILB criado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ae35c-164">For ILB, you must use hello IP address of hello ILB that was created earlier.</span></span> <span data-ttu-id="ae35c-165">tooobtain este IP abordar no PowerShell, Olá de utilização seguintes script:</span><span class="sxs-lookup"><span data-stu-id="ae35c-165">tooobtain this IP address in PowerShell, use hello following script:</span></span>

        # Define variables
        $ServiceName="<MyServiceName>" # hello name of hello cloud service that contains hello AG nodes
        (Get-AzureInternalLoadBalancer -ServiceName $ServiceName).IPAddress

2. <span data-ttu-id="ae35c-166">Dos Olá VMs, copie o script do PowerShell de Olá para o seu editor de texto de tooa do sistema operativo e, em seguida, definir variáveis de Olá valores toohello que anotou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ae35c-166">On one of hello VMs, copy hello PowerShell script for your operating system tooa text editor, and then set hello variables toohello values you noted earlier.</span></span>

    <span data-ttu-id="ae35c-167">Para o Windows Server 2012 ou posterior, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="ae35c-167">For Windows Server 2012 or later, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        Get-ClusterResource $IPResourceName | Set-ClusterParameter -Multiple @{"Address"="$ILBIP";"ProbePort"="59999";"SubnetMask"="255.255.255.255";"Network"="$ClusterNetworkName";"EnableDhcp"=0}

    <span data-ttu-id="ae35c-168">Para o Windows Server 2008 R2, utilize Olá seguintes script:</span><span class="sxs-lookup"><span data-stu-id="ae35c-168">For Windows Server 2008 R2, use hello following script:</span></span>

        # Define variables
        $ClusterNetworkName = "<MyClusterNetworkName>" # hello cluster network name (Use Get-ClusterNetwork on Windows Server 2012 of higher toofind hello name)
        $IPResourceName = "<IPResourceName>" # hello IP address resource name
        $ILBIP = “<X.X.X.X>” # hello IP address of hello ILB

        Import-Module FailoverClusters

        cluster res $IPResourceName /priv enabledhcp=0 address=$ILBIP probeport=59999  subnetmask=255.255.255.255

3. <span data-ttu-id="ae35c-169">Depois de ter as variáveis de Olá conjunto, abra uma janela elevada do Windows PowerShell, colar Olá script de editor de texto Olá no seu toorun de sessão do PowerShell-lo.</span><span class="sxs-lookup"><span data-stu-id="ae35c-169">After you have set hello variables, open an elevated Windows PowerShell window, paste hello script from hello text editor into your PowerShell session toorun it.</span></span> <span data-ttu-id="ae35c-170">Se a linha de Olá continua a mostrar  **>>** , prima Enter novamente toomake certificar-se de que o script de Olá entra em execução.</span><span class="sxs-lookup"><span data-stu-id="ae35c-170">If hello prompt still shows **>>**, Press Enter again toomake sure that hello script starts running.</span></span>

4. <span data-ttu-id="ae35c-171">Repita Olá precedente passos para cada VM.</span><span class="sxs-lookup"><span data-stu-id="ae35c-171">Repeat hello preceding steps for each VM.</span></span>  
    <span data-ttu-id="ae35c-172">Este script configura o recurso de endereço IP de Olá com o endereço IP Olá do serviço de nuvem Olá e define outros parâmetros, tais como a porta da sonda Olá.</span><span class="sxs-lookup"><span data-stu-id="ae35c-172">This script configures hello IP address resource with hello IP address of hello cloud service and sets other parameters, such as hello probe port.</span></span> <span data-ttu-id="ae35c-173">Quando o recurso de endereço IP de Olá seja colocado online, pode responder toohello consulta na porta de sonda de Olá Olá com balanceamento de carga ponto final de que criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="ae35c-173">When hello IP address resource is brought online, it can respond toohello polling on hello probe port from hello load-balanced endpoint that you created earlier.</span></span>

## <a name="bring-hello-listener-online"></a><span data-ttu-id="ae35c-174">Coloque online serviço de escuta de Olá</span><span class="sxs-lookup"><span data-stu-id="ae35c-174">Bring hello listener online</span></span>
[!INCLUDE [Bring-Listener-Online](../../../../includes/virtual-machines-ag-listener-bring-online.md)]

## <a name="follow-up-items"></a><span data-ttu-id="ae35c-175">Itens de seguimento</span><span class="sxs-lookup"><span data-stu-id="ae35c-175">Follow-up items</span></span>
[!INCLUDE [Follow-up](../../../../includes/virtual-machines-ag-listener-follow-up.md)]

## <a name="test-hello-availability-group-listener-within-hello-same-virtual-network"></a><span data-ttu-id="ae35c-176">Escuta do grupo de disponibilidade do teste Olá (Olá da mesma rede virtual)</span><span class="sxs-lookup"><span data-stu-id="ae35c-176">Test hello availability group listener (within hello same virtual network)</span></span>
[!INCLUDE [Test-Listener-Within-VNET](../../../../includes/virtual-machines-ag-listener-test.md)]

## <a name="next-steps"></a><span data-ttu-id="ae35c-177">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ae35c-177">Next steps</span></span>
[!INCLUDE [Listener-Next-Steps](../../../../includes/virtual-machines-ag-listener-next-steps.md)]
