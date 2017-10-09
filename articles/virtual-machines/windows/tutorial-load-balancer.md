---
title: "aaaHow tooload equilibrar máquinas virtuais do Windows no Azure | Microsoft Docs"
description: "Saiba como toouse Olá Azure carregar balanceador toocreate uma aplicação de elevada disponibilidade e segura entre três VMs do Windows"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 08/11/2017
ms.author: iainfou
ms.custom: mvc
ms.openlocfilehash: bfbd6a24e90a33e60d7d4f7b0c471af5d4e71f45
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooload-balance-windows-virtual-machines-in-azure-toocreate-a-highly-available-application"></a><span data-ttu-id="a0c58-103">Como tooload equilibrar virtual machines Windows no Azure toocreate uma aplicação altamente disponível</span><span class="sxs-lookup"><span data-stu-id="a0c58-103">How tooload balance Windows virtual machines in Azure toocreate a highly available application</span></span>
<span data-ttu-id="a0c58-104">Balanceamento de carga fornece um nível mais elevado de disponibilidade propagando-se os pedidos recebidos em várias máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="a0c58-104">Load balancing provides a higher level of availability by spreading incoming requests across multiple virtual machines.</span></span> <span data-ttu-id="a0c58-105">Neste tutorial, pode saber mais sobre Olá diferentes componentes do Balanceador de carga do Azure de Olá que distribui o tráfego de e para fornecem elevada disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="a0c58-105">In this tutorial, you learn about hello different components of hello Azure load balancer that distribute traffic and provide high availability.</span></span> <span data-ttu-id="a0c58-106">Saiba como:</span><span class="sxs-lookup"><span data-stu-id="a0c58-106">You learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0c58-107">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="a0c58-107">Create an Azure load balancer</span></span>
> * <span data-ttu-id="a0c58-108">Criar uma sonda de estado de funcionamento do Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-108">Create a load balancer health probe</span></span>
> * <span data-ttu-id="a0c58-109">Criar regras de tráfego de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-109">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="a0c58-110">Utilizar Olá extensão de Script personalizado toocreate um site do IIS básico</span><span class="sxs-lookup"><span data-stu-id="a0c58-110">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="a0c58-111">Criar máquinas virtuais e anexe tooa Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-111">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="a0c58-112">Ver um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="a0c58-112">View a load balancer in action</span></span>
> * <span data-ttu-id="a0c58-113">Adicionar e remover as VMs a partir de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-113">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="a0c58-114">Este tutorial requer Olá Azure PowerShell versão do módulo 3,6 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a0c58-114">This tutorial requires hello Azure PowerShell module version 3.6 or later.</span></span> <span data-ttu-id="a0c58-115">Executar ` Get-Module -ListAvailable AzureRM` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="a0c58-115">Run ` Get-Module -ListAvailable AzureRM` toofind hello version.</span></span> <span data-ttu-id="a0c58-116">Se precisar de tooupgrade, consulte [módulo Azure PowerShell instalar](/powershell/azure/install-azurerm-ps).</span><span class="sxs-lookup"><span data-stu-id="a0c58-116">If you need tooupgrade, see [Install Azure PowerShell module](/powershell/azure/install-azurerm-ps).</span></span>


## <a name="azure-load-balancer-overview"></a><span data-ttu-id="a0c58-117">Descrição geral do Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="a0c58-117">Azure load balancer overview</span></span>
<span data-ttu-id="a0c58-118">Um balanceador de carga do Azure é um balanceador de carga de camada 4 (TCP, UDP) que fornece elevada disponibilidade, distribuição de tráfego de entrada entre VMs em bom estado.</span><span class="sxs-lookup"><span data-stu-id="a0c58-118">An Azure load balancer is a Layer-4 (TCP, UDP) load balancer that provides high availability by distributing incoming traffic among healthy VMs.</span></span> <span data-ttu-id="a0c58-119">Uma sonda de estado de funcionamento do Balanceador de carga monitoriza uma porta especificada em cada VM e distribui apenas tráfego tooan VM operacional.</span><span class="sxs-lookup"><span data-stu-id="a0c58-119">A load balancer health probe monitors a given port on each VM and only distributes traffic tooan operational VM.</span></span>

<span data-ttu-id="a0c58-120">É possível definir uma configuração de IP Front-end que contém um ou mais endereços IP públicos.</span><span class="sxs-lookup"><span data-stu-id="a0c58-120">You define a front-end IP configuration that contains one or more public IP addresses.</span></span> <span data-ttu-id="a0c58-121">Esta configuração de IP Front-end permite a sua toobe de aplicações e de Balanceador de carga acessível através de Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="a0c58-121">This front-end IP configuration allows your load balancer and applications toobe accessible over hello Internet.</span></span> 

<span data-ttu-id="a0c58-122">As máquinas virtuais ligar tooa Balanceador de carga com o seu cartão de interface de rede virtual (NIC).</span><span class="sxs-lookup"><span data-stu-id="a0c58-122">Virtual machines connect tooa load balancer using their virtual network interface card (NIC).</span></span> <span data-ttu-id="a0c58-123">toodistribute tráfego toohello VMs, um conjunto de endereços de back-end contém endereços IP Olá Olá virtual (NICs) ligado toohello de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0c58-123">toodistribute traffic toohello VMs, a back-end address pool contains hello IP addresses of hello virtual (NICs) connected toohello load balancer.</span></span>

<span data-ttu-id="a0c58-124">fluxo de Olá toocontrol de tráfego, é possível definir as regras de Balanceador de carga para portas específicas e protocolos que mapeiam tooyour VMs.</span><span class="sxs-lookup"><span data-stu-id="a0c58-124">toocontrol hello flow of traffic, you define load balancer rules for specific ports and protocols that map tooyour VMs.</span></span>


## <a name="create-azure-load-balancer"></a><span data-ttu-id="a0c58-125">Criar Balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="a0c58-125">Create Azure load balancer</span></span>
<span data-ttu-id="a0c58-126">Esta secção descreve em detalhe como pode criar e configurar cada componente Olá de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0c58-126">This section details how you can create and configure each component of hello load balancer.</span></span> <span data-ttu-id="a0c58-127">Antes de poder criar seu Balanceador de carga, crie um grupo de recursos com [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="a0c58-127">Before you can create your load balancer, create a resource group with [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup).</span></span> <span data-ttu-id="a0c58-128">Olá exemplo seguinte cria um grupo de recursos denominado *myResourceGroupLoadBalancer* no Olá *EastUS* localização:</span><span class="sxs-lookup"><span data-stu-id="a0c58-128">hello following example creates a resource group named *myResourceGroupLoadBalancer* in hello *EastUS* location:</span></span>

```powershell
New-AzureRmResourceGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS
```

### <a name="create-a-public-ip-address"></a><span data-ttu-id="a0c58-129">Crie um endereço IP público</span><span class="sxs-lookup"><span data-stu-id="a0c58-129">Create a public IP address</span></span>
<span data-ttu-id="a0c58-130">tooaccess Olá, a aplicação na Internet, tem um endereço IP público Olá Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="a0c58-130">tooaccess your app on hello Internet, you need a public IP address for hello load balancer.</span></span> <span data-ttu-id="a0c58-131">Criar um endereço IP público com [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="a0c58-131">Create a public IP address with [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress).</span></span> <span data-ttu-id="a0c58-132">Olá exemplo seguinte cria um endereço IP público com o nome *myPublicIP* no Olá *myResourceGroupLoadBalancer* grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="a0c58-132">hello following example creates a public IP address named *myPublicIP* in hello *myResourceGroupLoadBalancer* resource group:</span></span>

```powershell
$publicIP = New-AzureRmPublicIpAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -AllocationMethod Static `
  -Name myPublicIP
```

### <a name="create-a-load-balancer"></a><span data-ttu-id="a0c58-133">Criar um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-133">Create a load balancer</span></span>
<span data-ttu-id="a0c58-134">Criar um endereço IP de front-end com [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span><span class="sxs-lookup"><span data-stu-id="a0c58-134">Create a frontend IP address with [New-AzureRmLoadBalancerFrontendIpConfig](/powershell/module/azurerm.network/new-azurermloadbalancerfrontendipconfig).</span></span> <span data-ttu-id="a0c58-135">Olá exemplo seguinte cria um endereço IP de front-end com o nome *myFrontEndPool*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-135">hello following example creates a frontend IP address named *myFrontEndPool*:</span></span> 

```powershell
$frontendIP = New-AzureRmLoadBalancerFrontendIpConfig `
  -Name myFrontEndPool `
  -PublicIpAddress $publicIP
```

<span data-ttu-id="a0c58-136">Criar um conjunto de endereços de back-end com [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span><span class="sxs-lookup"><span data-stu-id="a0c58-136">Create a backend address pool with [New-AzureRmLoadBalancerBackendAddressPoolConfig](/powershell/module/azurerm.network/new-azurermloadbalancerbackendaddresspoolconfig).</span></span> <span data-ttu-id="a0c58-137">Olá exemplo seguinte cria um conjunto de endereços de back-end com o nome *myBackEndPool*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-137">hello following example creates a backend address pool named *myBackEndPool*:</span></span>

```powershell
$backendPool = New-AzureRmLoadBalancerBackendAddressPoolConfig -Name myBackEndPool
```

<span data-ttu-id="a0c58-138">Agora, crie o Balanceador de carga Olá com [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span><span class="sxs-lookup"><span data-stu-id="a0c58-138">Now, create hello load balancer with [New-AzureRmLoadBalancer](/powershell/module/azurerm.network/new-azurermloadbalancer).</span></span> <span data-ttu-id="a0c58-139">Olá exemplo seguinte cria um balanceador de carga com o nome *myLoadBalancer* utilizando Olá *myPublicIP* endereço:</span><span class="sxs-lookup"><span data-stu-id="a0c58-139">hello following example creates a load balancer named *myLoadBalancer* using hello *myPublicIP* address:</span></span>

```powershell
$lb = New-AzureRmLoadBalancer `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myLoadBalancer `
  -Location EastUS `
  -FrontendIpConfiguration $frontendIP `
  -BackendAddressPool $backendPool
```

### <a name="create-a-health-probe"></a><span data-ttu-id="a0c58-140">Criar uma sonda do Estado de funcionamento</span><span class="sxs-lookup"><span data-stu-id="a0c58-140">Create a health probe</span></span>
<span data-ttu-id="a0c58-141">tooallow Olá balanceador toomonitor Olá estado da carga da sua aplicação, utilize uma sonda do Estado de funcionamento.</span><span class="sxs-lookup"><span data-stu-id="a0c58-141">tooallow hello load balancer toomonitor hello status of your app, you use a health probe.</span></span> <span data-ttu-id="a0c58-142">sonda de estado de funcionamento de Olá dinamicamente adiciona ou remove as VMs da rotação de Balanceador de carga de Olá com base na respetiva verificações de toohealth de resposta.</span><span class="sxs-lookup"><span data-stu-id="a0c58-142">hello health probe dynamically adds or removes VMs from hello load balancer rotation based on their response toohealth checks.</span></span> <span data-ttu-id="a0c58-143">Por predefinição, uma VM é removida da distribuição de Balanceador de carga Olá após duas falhas consecutivas em intervalos de 15 segundo.</span><span class="sxs-lookup"><span data-stu-id="a0c58-143">By default, a VM is removed from hello load balancer distribution after two consecutive failures at 15-second intervals.</span></span> <span data-ttu-id="a0c58-144">Criar uma sonda do Estado de funcionamento com base num protocolo ou uma página de verificação do Estado de funcionamento específico para a sua aplicação.</span><span class="sxs-lookup"><span data-stu-id="a0c58-144">You create a health probe based on a protocol or a specific health check page for your app.</span></span> 

<span data-ttu-id="a0c58-145">Olá seguinte exemplo cria uma sonda TCP.</span><span class="sxs-lookup"><span data-stu-id="a0c58-145">hello following example creates a TCP probe.</span></span> <span data-ttu-id="a0c58-146">Também pode criar das sondas personalizadas do HTTP para obter mais detalhada do Estado de funcionamento verificações.</span><span class="sxs-lookup"><span data-stu-id="a0c58-146">You can also create custom HTTP probes for more fine grained health checks.</span></span> <span data-ttu-id="a0c58-147">Quando utilizar uma pesquisa HTTP personalizada, tem de criar página de verificação do Estado de funcionamento de Olá, tais como *healthcheck.aspx*.</span><span class="sxs-lookup"><span data-stu-id="a0c58-147">When using a custom HTTP probe, you must create hello health check page, such as *healthcheck.aspx*.</span></span> <span data-ttu-id="a0c58-148">sonda de Olá tem de devolver um **HTTP 200 OK** resposta para o anfitrião Olá tookeep de Balanceador de carga de Olá no rotação.</span><span class="sxs-lookup"><span data-stu-id="a0c58-148">hello probe must return an **HTTP 200 OK** response for hello load balancer tookeep hello host in rotation.</span></span>

<span data-ttu-id="a0c58-149">toocreate uma sonda do Estado de funcionamento TCP, utilize [adicionar AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span><span class="sxs-lookup"><span data-stu-id="a0c58-149">toocreate a TCP health probe, you use [Add-AzureRmLoadBalancerProbeConfig](/powershell/module/azurerm.network/add-azurermloadbalancerprobeconfig).</span></span> <span data-ttu-id="a0c58-150">Olá exemplo seguinte cria uma sonda do Estado de funcionamento com o nome *myHealthProbe* que monitoriza a cada VM:</span><span class="sxs-lookup"><span data-stu-id="a0c58-150">hello following example creates a health probe named *myHealthProbe* that monitors each VM:</span></span>

```powershell
Add-AzureRmLoadBalancerProbeConfig `
  -Name myHealthProbe `
  -LoadBalancer $lb `
  -Protocol tcp `
  -Port 80 `
  -IntervalInSeconds 15 `
  -ProbeCount 2
```

<span data-ttu-id="a0c58-151">Atualizar o Balanceador de carga Olá com [conjunto AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="a0c58-151">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```

### <a name="create-a-load-balancer-rule"></a><span data-ttu-id="a0c58-152">Criar uma regra de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-152">Create a load balancer rule</span></span>
<span data-ttu-id="a0c58-153">Uma regra de Balanceador de carga é toodefine utilizado como o tráfego é distribuído toohello VMs.</span><span class="sxs-lookup"><span data-stu-id="a0c58-153">A load balancer rule is used toodefine how traffic is distributed toohello VMs.</span></span> <span data-ttu-id="a0c58-154">Definir a configuração IP de front-end do Olá para tráfego de entrada Olá e Olá back-end conjunto tooreceive Olá tráfego IP, juntamente com a origem necessários Olá e porta de destino.</span><span class="sxs-lookup"><span data-stu-id="a0c58-154">You define hello front-end IP configuration for hello incoming traffic and hello back-end IP pool tooreceive hello traffic, along with hello required source and destination port.</span></span> <span data-ttu-id="a0c58-155">toomake se de que apenas as VMs bom receberem tráfego, também define toouse de sonda de estado de funcionamento de Olá.</span><span class="sxs-lookup"><span data-stu-id="a0c58-155">toomake sure only healthy VMs receive traffic, you also define hello health probe toouse.</span></span>

<span data-ttu-id="a0c58-156">Criar uma regra de Balanceador de carga com [adicionar AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span><span class="sxs-lookup"><span data-stu-id="a0c58-156">Create a load balancer rule with [Add-AzureRmLoadBalancerRuleConfig](/powershell/module/azurerm.network/add-azurermloadbalancerruleconfig).</span></span> <span data-ttu-id="a0c58-157">Olá exemplo seguinte cria uma regra de Balanceador de carga com o nome *myLoadBalancerRule* e equilibrar o tráfego na porta *80*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-157">hello following example creates a load balancer rule named *myLoadBalancerRule* and balances traffic on port *80*:</span></span>

```powershell
$probe = Get-AzureRmLoadBalancerProbeConfig -LoadBalancer $lb -Name myHealthProbe

Add-AzureRmLoadBalancerRuleConfig `
  -Name myLoadBalancerRule `
  -LoadBalancer $lb `
  -FrontendIpConfiguration $lb.FrontendIpConfigurations[0] `
  -BackendAddressPool $lb.BackendAddressPools[0] `
  -Protocol Tcp `
  -FrontendPort 80 `
  -BackendPort 80 `
  -Probe $probe
```

<span data-ttu-id="a0c58-158">Atualizar o Balanceador de carga Olá com [conjunto AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="a0c58-158">Update hello load balancer with [Set-AzureRmLoadBalancer](/powershell/module/azurerm.network/set-azurermloadbalancer):</span></span>

```powershell
Set-AzureRmLoadBalancer -LoadBalancer $lb
```


## <a name="configure-virtual-network"></a><span data-ttu-id="a0c58-159">Configurar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="a0c58-159">Configure virtual network</span></span>
<span data-ttu-id="a0c58-160">Antes de implementar algumas VMs e pode testar o seu balanceador, crie Olá suporte recursos de rede virtual.</span><span class="sxs-lookup"><span data-stu-id="a0c58-160">Before you deploy some VMs and can test your balancer, create hello supporting virtual network resources.</span></span> <span data-ttu-id="a0c58-161">Para obter mais informações sobre as redes virtuais, consulte Olá [gerir redes virtuais do Azure](tutorial-virtual-network.md) tutorial.</span><span class="sxs-lookup"><span data-stu-id="a0c58-161">For more information about virtual networks, see hello [Manage Azure Virtual Networks](tutorial-virtual-network.md) tutorial.</span></span>

### <a name="create-network-resources"></a><span data-ttu-id="a0c58-162">Criar recursos de rede</span><span class="sxs-lookup"><span data-stu-id="a0c58-162">Create network resources</span></span>
<span data-ttu-id="a0c58-163">Criar uma rede virtual com [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="a0c58-163">Create a virtual network with [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork).</span></span> <span data-ttu-id="a0c58-164">Olá exemplo seguinte cria uma rede virtual denominada *myVnet* com *mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-164">hello following example creates a virtual network named *myVnet* with *mySubnet*:</span></span>

```powershell
# Create subnet config
$subnetConfig = New-AzureRmVirtualNetworkSubnetConfig `
  -Name mySubnet `
  -AddressPrefix 192.168.1.0/24

# Create hello virtual network
$vnet = New-AzureRmVirtualNetwork `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myVnet `
  -AddressPrefix 192.168.0.0/16 `
  -Subnet $subnetConfig
```

<span data-ttu-id="a0c58-165">Criar uma regra de grupo de segurança de rede com [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), em seguida, crie um grupo de segurança de rede com [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span><span class="sxs-lookup"><span data-stu-id="a0c58-165">Create a network security group rule with [New-AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig), then create a network security group with [New-AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup).</span></span> <span data-ttu-id="a0c58-166">Adicionar sub-rede toohello grupo de segurança de rede de Olá com [conjunto AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) e, em seguida, atualize a rede virtual do Olá com [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span><span class="sxs-lookup"><span data-stu-id="a0c58-166">Add hello network security group toohello subnet with [Set-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/set-azurermvirtualnetworksubnetconfig) and then update hello virtual network with [Set-AzureRmVirtualNetwork](/powershell/module/azurerm.network/set-azurermvirtualnetwork).</span></span> 

<span data-ttu-id="a0c58-167">Olá exemplo seguinte cria uma regra de grupo de segurança de rede com o nome *myNetworkSecurityGroup* e aplica-demasiado*mySubnet*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-167">hello following example creates a network security group rule named *myNetworkSecurityGroup* and applies it too*mySubnet*:</span></span>

```powershell
# Create security rule config
$nsgRule = New-AzureRmNetworkSecurityRuleConfig `
  -Name myNetworkSecurityGroupRule `
  -Protocol Tcp `
  -Direction Inbound `
  -Priority 1001 `
  -SourceAddressPrefix * `
  -SourcePortRange * `
  -DestinationAddressPrefix * `
  -DestinationPortRange 80 `
  -Access Allow

# Create hello network security group
$nsg = New-AzureRmNetworkSecurityGroup `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Location EastUS `
  -Name myNetworkSecurityGroup `
  -SecurityRules $nsgRule

# Apply hello network security group tooa subnet
Set-AzureRmVirtualNetworkSubnetConfig `
  -VirtualNetwork $vnet `
  -Name mySubnet `
  -NetworkSecurityGroup $nsg `
  -AddressPrefix 192.168.1.0/24

# Update hello virtual network
Set-AzureRmVirtualNetwork -VirtualNetwork $vnet
```

<span data-ttu-id="a0c58-168">NICs virtuais são criados com [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span><span class="sxs-lookup"><span data-stu-id="a0c58-168">Virtual NICs are created with [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface).</span></span> <span data-ttu-id="a0c58-169">Olá exemplo seguinte cria três NICs virtuais.</span><span class="sxs-lookup"><span data-stu-id="a0c58-169">hello following example creates three virtual NICs.</span></span> <span data-ttu-id="a0c58-170">(Uma NIC virtual para cada VM criar para a aplicação no Olá seguindo os passos).</span><span class="sxs-lookup"><span data-stu-id="a0c58-170">(One virtual NIC for each VM you create for your app in hello following steps).</span></span> <span data-ttu-id="a0c58-171">Pode criar o NICs virtuais adicionais e VMs em qualquer altura e adicioná-los toohello Balanceador de carga:</span><span class="sxs-lookup"><span data-stu-id="a0c58-171">You can create additional virtual NICs and VMs at any time and add them toohello load balancer:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   New-AzureRmNetworkInterface `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -Name myNic$i `
     -Location EastUS `
     -Subnet $vnet.Subnets[0] `
     -LoadBalancerBackendAddressPool $lb.BackendAddressPools[0]
}
```

## <a name="create-virtual-machines"></a><span data-ttu-id="a0c58-172">Criar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a0c58-172">Create virtual machines</span></span>
<span data-ttu-id="a0c58-173">elevada disponibilidade da tooimprove Olá da sua aplicação, coloque as suas VMs num conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="a0c58-173">tooimprove hello high availability of your app, place your VMs in an availability set.</span></span>

<span data-ttu-id="a0c58-174">Criar um conjunto de disponibilidade com [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span><span class="sxs-lookup"><span data-stu-id="a0c58-174">Create an availability set with [New-AzureRmAvailabilitySet](/powershell/module/azurerm.compute/new-azurermavailabilityset).</span></span> <span data-ttu-id="a0c58-175">Olá exemplo seguinte cria um conjunto nomeado de disponibilidade *myAvailabilitySet*:</span><span class="sxs-lookup"><span data-stu-id="a0c58-175">hello following example creates an availability set named *myAvailabilitySet*:</span></span>

```powershell
$availabilitySet = New-AzureRmAvailabilitySet `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myAvailabilitySet `
  -Location EastUS `
  -Managed `
  -PlatformFaultDomainCount 3 `
  -PlatformUpdateDomainCount 2
```

<span data-ttu-id="a0c58-176">Definir um administrador do nome de utilizador e palavra-passe para as VMs de Olá com [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span><span class="sxs-lookup"><span data-stu-id="a0c58-176">Set an administrator username and password for hello VMs with [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential):</span></span>

```powershell
$cred = Get-Credential
```

<span data-ttu-id="a0c58-177">Agora pode criar VMs Olá com [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span><span class="sxs-lookup"><span data-stu-id="a0c58-177">Now you can create hello VMs with [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm).</span></span> <span data-ttu-id="a0c58-178">Olá seguinte exemplo cria três VMs:</span><span class="sxs-lookup"><span data-stu-id="a0c58-178">hello following example creates three VMs:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
  $vm = New-AzureRmVMConfig `
    -VMName myVM$i `
    -VMSize Standard_D1 `
    -AvailabilitySetId $availabilitySet.Id
  $vm = Set-AzureRmVMOperatingSystem `
    -VM $vm `
    -Windows `
    -ComputerName myVM$i `
    -Credential $cred `
    -ProvisionVMAgent `
    -EnableAutoUpdate
  $vm = Set-AzureRmVMSourceImage `
    -VM $vm `
    -PublisherName MicrosoftWindowsServer `
    -Offer WindowsServer `
    -Skus 2016-Datacenter `
    -Version latest
  $vm = Set-AzureRmVMOSDisk `
    -VM $vm `
    -Name myOsDisk$i `
    -DiskSizeInGB 128 `
    -CreateOption FromImage `
    -Caching ReadWrite
  $nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic$i
  $vm = Add-AzureRmVMNetworkInterface -VM $vm -Id $nic.Id
  New-AzureRmVM `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Location EastUS `
    -VM $vm
}
```

<span data-ttu-id="a0c58-179">Este demora alguns minutos toocreate e configurar todos os três VMs.</span><span class="sxs-lookup"><span data-stu-id="a0c58-179">It takes a few minutes toocreate and configure all three VMs.</span></span>

### <a name="install-iis-with-custom-script-extension"></a><span data-ttu-id="a0c58-180">Instalar o IIS com a extensão de Script personalizado</span><span class="sxs-lookup"><span data-stu-id="a0c58-180">Install IIS with Custom Script Extension</span></span>
<span data-ttu-id="a0c58-181">Um tutorial anterior em [como toocustomize máquina virtual do Windows](tutorial-automate-vm-deployment.md), aprendeu como tooautomate personalização de VM com Olá extensão de Script personalizado para Windows.</span><span class="sxs-lookup"><span data-stu-id="a0c58-181">In a previous tutorial on [How toocustomize a Windows virtual machine](tutorial-automate-vm-deployment.md), you learned how tooautomate VM customization with hello Custom Script Extension for Windows.</span></span> <span data-ttu-id="a0c58-182">Pode utilizar Olá mesmo abordar tooinstall e configurar o IIS nas suas VMs.</span><span class="sxs-lookup"><span data-stu-id="a0c58-182">You can use hello same approach tooinstall and configure IIS on your VMs.</span></span>

<span data-ttu-id="a0c58-183">Utilize [conjunto AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall Olá extensão de Script personalizado.</span><span class="sxs-lookup"><span data-stu-id="a0c58-183">Use [Set-AzureRmVMExtension](/powershell/module/azurerm.compute/set-azurermvmextension) tooinstall hello Custom Script Extension.</span></span> <span data-ttu-id="a0c58-184">Olá execuções de extensão `powershell Add-WindowsFeature Web-Server` tooinstall Olá servidor Web do IIS e, em seguida, Olá atualizações *Default.htm* página tooshow Olá nome do anfitrião do Olá VM:</span><span class="sxs-lookup"><span data-stu-id="a0c58-184">hello extension runs `powershell Add-WindowsFeature Web-Server` tooinstall hello IIS webserver and then updates hello *Default.htm* page tooshow hello hostname of hello VM:</span></span>

```powershell
for ($i=1; $i -le 3; $i++)
{
   Set-AzureRmVMExtension `
     -ResourceGroupName myResourceGroupLoadBalancer `
     -ExtensionName IIS `
     -VMName myVM$i `
     -Publisher Microsoft.Compute `
     -ExtensionType CustomScriptExtension `
     -TypeHandlerVersion 1.4 `
     -SettingString '{"commandToExecute":"powershell Add-WindowsFeature Web-Server; powershell Add-Content -Path \"C:\\inetpub\\wwwroot\\Default.htm\" -Value $($env:computername)"}' `
     -Location EastUS
}
```

## <a name="test-load-balancer"></a><span data-ttu-id="a0c58-185">Balanceador de carga de teste</span><span class="sxs-lookup"><span data-stu-id="a0c58-185">Test load balancer</span></span>
<span data-ttu-id="a0c58-186">Obter o endereço IP público de Olá do seu Balanceador de carga com [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span><span class="sxs-lookup"><span data-stu-id="a0c58-186">Obtain hello public IP address of your load balancer with [Get-AzureRmPublicIPAddress](/powershell/module/azurerm.network/get-azurermpublicipaddress).</span></span> <span data-ttu-id="a0c58-187">Olá exemplo seguinte obtém o endereço IP Olá *myPublicIP* criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="a0c58-187">hello following example obtains hello IP address for *myPublicIP* created earlier:</span></span>

```powershell
Get-AzureRmPublicIPAddress `
  -ResourceGroupName myResourceGroupLoadBalancer `
  -Name myPublicIP | select IpAddress
```

<span data-ttu-id="a0c58-188">Em seguida, pode introduzir o endereço IP público Olá no tooa browser.</span><span class="sxs-lookup"><span data-stu-id="a0c58-188">You can then enter hello public IP address in tooa web browser.</span></span> <span data-ttu-id="a0c58-189">é apresentado o Web site de Olá, incluindo o nome de anfitrião de Olá do Olá VM Balanceador de carga que Olá distribuídas tooas de tráfego no seguinte exemplo de Olá:</span><span class="sxs-lookup"><span data-stu-id="a0c58-189">hello website is displayed, including hello hostname of hello VM that hello load balancer distributed traffic tooas in hello following example:</span></span>

![Web site do IIS em execução](./media/tutorial-load-balancer/running-iis-website.png)

<span data-ttu-id="a0c58-191">Balanceador de carga de Olá toosee distribuir o tráfego entre todas as três VMs executar a sua aplicação, pode forçar atualizar o browser.</span><span class="sxs-lookup"><span data-stu-id="a0c58-191">toosee hello load balancer distribute traffic across all three VMs running your app, you can force-refresh your web browser.</span></span>


## <a name="add-and-remove-vms"></a><span data-ttu-id="a0c58-192">Adicionar e remover VMs</span><span class="sxs-lookup"><span data-stu-id="a0c58-192">Add and remove VMs</span></span>
<span data-ttu-id="a0c58-193">Poderá ser necessário tooperform manutenção no Olá as VMs com a sua aplicação, como a instalação de atualizações do SO.</span><span class="sxs-lookup"><span data-stu-id="a0c58-193">You may need tooperform maintenance on hello VMs running your app, such as installing OS updates.</span></span> <span data-ttu-id="a0c58-194">toodeal com maior tráfego tooyour aplicação, poderá ser necessário tooadd VMs adicionais.</span><span class="sxs-lookup"><span data-stu-id="a0c58-194">toodeal with increased traffic tooyour app, you may need tooadd additional VMs.</span></span> <span data-ttu-id="a0c58-195">Esta secção mostra-lhe como tooremove ou adicionar uma VM do Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="a0c58-195">This section shows you how tooremove or add a VM from hello load balancer.</span></span>

### <a name="remove-a-vm-from-hello-load-balancer"></a><span data-ttu-id="a0c58-196">Remover uma VM do Balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="a0c58-196">Remove a VM from hello load balancer</span></span>
<span data-ttu-id="a0c58-197">Obter Olá placa de interface com [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), em seguida, conjunto Olá *LoadBalancerBackendAddressPools* Olá de propriedade de virtual NIC demasiado*$null*.</span><span class="sxs-lookup"><span data-stu-id="a0c58-197">Get hello network interface card with [Get-AzureRmNetworkInterface](/powershell/module/azurerm.network/get-azurermnetworkinterface), then set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC too*$null*.</span></span> <span data-ttu-id="a0c58-198">Por fim, atualize o NIC virtual. Olá:</span><span class="sxs-lookup"><span data-stu-id="a0c58-198">Finally, update hello virtual NIC.:</span></span>

```powershell
$nic = Get-AzureRmNetworkInterface `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myNic2
$nic.Ipconfigurations[0].LoadBalancerBackendAddressPools=$null
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

<span data-ttu-id="a0c58-199">Balanceador de carga de Olá toosee distribuir o tráfego entre Olá restantes duas VMs executar a sua aplicação, pode forçar atualizar o browser.</span><span class="sxs-lookup"><span data-stu-id="a0c58-199">toosee hello load balancer distribute traffic across hello remaining two VMs running your app you can force-refresh your web browser.</span></span> <span data-ttu-id="a0c58-200">Pode agora efetuar manutenção num Olá VM, tais como instalar atualizações do SO ou efetuar um reinício VM.</span><span class="sxs-lookup"><span data-stu-id="a0c58-200">You can now perform maintenance on hello VM, such as installing OS updates or performing a VM reboot.</span></span>

### <a name="add-a-vm-toohello-load-balancer"></a><span data-ttu-id="a0c58-201">Adicionar um balanceador de carga de toohello VM</span><span class="sxs-lookup"><span data-stu-id="a0c58-201">Add a VM toohello load balancer</span></span>
<span data-ttu-id="a0c58-202">Após efetuar a manutenção VM, ou se precisar de capacidade de tooexpand, defina Olá *LoadBalancerBackendAddressPools* propriedade toohello NIC virtual Olá *BackendAddressPool* de [ Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span><span class="sxs-lookup"><span data-stu-id="a0c58-202">After performing VM maintenance, or if you need tooexpand capacity, set hello *LoadBalancerBackendAddressPools* property of hello virtual NIC toohello *BackendAddressPool* from [Get-AzureRMLoadBalancer](/powershell/module/azurerm.network/get-azurermloadbalancer):</span></span>

<span data-ttu-id="a0c58-203">Obter o Balanceador de carga Olá:</span><span class="sxs-lookup"><span data-stu-id="a0c58-203">Get hello load balancer:</span></span>

```powershell
$lb = Get-AzureRMLoadBalancer `
    -ResourceGroupName myResourceGroupLoadBalancer `
    -Name myLoadBalancer 
$nic.IpConfigurations[0].LoadBalancerBackendAddressPools=$lb.BackendAddressPools[0]
Set-AzureRmNetworkInterface -NetworkInterface $nic
```

## <a name="next-steps"></a><span data-ttu-id="a0c58-204">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="a0c58-204">Next steps</span></span>

<span data-ttu-id="a0c58-205">Neste tutorial, criou um balanceador de carga e anexado VMs tooit.</span><span class="sxs-lookup"><span data-stu-id="a0c58-205">In this tutorial, you created a load balancer and attached VMs tooit.</span></span> <span data-ttu-id="a0c58-206">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="a0c58-206">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a0c58-207">Criar um balanceador de carga do Azure</span><span class="sxs-lookup"><span data-stu-id="a0c58-207">Create an Azure load balancer</span></span>
> * <span data-ttu-id="a0c58-208">Criar uma sonda de estado de funcionamento do Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-208">Create a load balancer health probe</span></span>
> * <span data-ttu-id="a0c58-209">Criar regras de tráfego de Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-209">Create load balancer traffic rules</span></span>
> * <span data-ttu-id="a0c58-210">Utilizar Olá extensão de Script personalizado toocreate um site do IIS básico</span><span class="sxs-lookup"><span data-stu-id="a0c58-210">Use hello Custom Script Extension toocreate a basic IIS site</span></span>
> * <span data-ttu-id="a0c58-211">Criar máquinas virtuais e anexe tooa Balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-211">Create virtual machines and attach tooa load balancer</span></span>
> * <span data-ttu-id="a0c58-212">Ver um balanceador de carga em ação</span><span class="sxs-lookup"><span data-stu-id="a0c58-212">View a load balancer in action</span></span>
> * <span data-ttu-id="a0c58-213">Adicionar e remover as VMs a partir de um balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="a0c58-213">Add and remove VMs from a load balancer</span></span>

<span data-ttu-id="a0c58-214">Avançar toohello toolearn de tutorial seguinte como toomanage redes de VM.</span><span class="sxs-lookup"><span data-stu-id="a0c58-214">Advance toohello next tutorial toolearn how toomanage VM networking.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a0c58-215">Gerir VMs e redes virtuais</span><span class="sxs-lookup"><span data-stu-id="a0c58-215">Manage VMs and virtual networks</span></span>](./tutorial-virtual-network.md)
