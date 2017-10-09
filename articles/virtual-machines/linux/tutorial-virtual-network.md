---
title: "aaaAzure redes virtuais e máquinas virtuais do Linux | Microsoft Docs"
description: "Tutorial - Gerir redes virtuais do Azure e máquinas virtuais do Linux com Olá CLI do Azure"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 57e6bd4de16f0e31d53dc67bf50dc5730d43712b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-virtual-networks-and-linux-virtual-machines-with-hello-azure-cli"></a><span data-ttu-id="8de79-103">Gerir redes virtuais do Azure e máquinas virtuais do Linux com Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8de79-103">Manage Azure Virtual Networks and Linux Virtual Machines with hello Azure CLI</span></span>

<span data-ttu-id="8de79-104">Máquinas virtuais do Azure utilizar redes do Azure para a comunicação de rede internos e externos.</span><span class="sxs-lookup"><span data-stu-id="8de79-104">Azure virtual machines use Azure networking for internal and external network communication.</span></span> <span data-ttu-id="8de79-105">Este tutorial explica duas máquinas virtuais a implementar e configurar redes do Azure para estas VMs.</span><span class="sxs-lookup"><span data-stu-id="8de79-105">This tutorial walks through deploying two virtual machines and configuring Azure networking for these VMs.</span></span> <span data-ttu-id="8de79-106">Exemplos de Olá neste tutorial partem do princípio de que as VMs de Olá estão a alojar uma aplicação web com um back-end da base de dados, no entanto, uma aplicação não está implementada no tutorial Olá.</span><span class="sxs-lookup"><span data-stu-id="8de79-106">hello examples in this tutorial assume that hello VMs are hosting a web application with a database back-end, however an application is not deployed in hello tutorial.</span></span> <span data-ttu-id="8de79-107">Neste tutorial, ficará a saber como:</span><span class="sxs-lookup"><span data-stu-id="8de79-107">In this tutorial, you learn how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8de79-108">Implementar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-108">Deploy a virtual network</span></span>
> * <span data-ttu-id="8de79-109">Criar uma sub-rede dentro de uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-109">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="8de79-110">Ligar máquinas virtuais tooa sub-rede</span><span class="sxs-lookup"><span data-stu-id="8de79-110">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="8de79-111">Gerir endereços IP públicos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-111">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="8de79-112">Proteger o tráfego de internet de entrada</span><span class="sxs-lookup"><span data-stu-id="8de79-112">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="8de79-113">Proteger o tráfego de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="8de79-113">Secure VM tooVM traffic</span></span>


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="8de79-114">Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8de79-114">If you choose tooinstall and use hello CLI locally, this tutorial requires that you are running hello Azure CLI version 2.0.4 or later.</span></span> <span data-ttu-id="8de79-115">Executar `az --version` versão de Olá toofind.</span><span class="sxs-lookup"><span data-stu-id="8de79-115">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="8de79-116">Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli).</span><span class="sxs-lookup"><span data-stu-id="8de79-116">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="vm-networking-overview"></a><span data-ttu-id="8de79-117">Descrição geral de redes VM</span><span class="sxs-lookup"><span data-stu-id="8de79-117">VM networking overview</span></span>

<span data-ttu-id="8de79-118">Redes virtuais do Azure ativar as ligações de rede seguro entre máquinas virtuais, Olá internet e outros serviços do Azure, tais como a base de dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="8de79-118">Azure virtual networks enable secure network connections between virtual machines, hello internet, and other Azure services such as Azure SQL database.</span></span> <span data-ttu-id="8de79-119">Redes virtuais são divididas em segmentos lógicos denominados sub-redes.</span><span class="sxs-lookup"><span data-stu-id="8de79-119">Virtual networks are broken down into logical segments called subnets.</span></span> <span data-ttu-id="8de79-120">Sub-redes são utilizadas toocontrol fluxo de rede e como um limite de segurança.</span><span class="sxs-lookup"><span data-stu-id="8de79-120">Subnets are used toocontrol network flow, and as a security boundary.</span></span> <span data-ttu-id="8de79-121">Quando implementar uma VM, incluem-se, geralmente, uma interface de rede virtual, que é anexado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-121">When deploying a VM, it generally includes a virtual network interface, which is attached tooa subnet.</span></span>

## <a name="deploy-virtual-network"></a><span data-ttu-id="8de79-122">Implementar a rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-122">Deploy virtual network</span></span>

<span data-ttu-id="8de79-123">Para este tutorial, é criada uma única rede virtual com duas sub-redes.</span><span class="sxs-lookup"><span data-stu-id="8de79-123">For this tutorial, a single virtual network is created with two subnets.</span></span> <span data-ttu-id="8de79-124">Uma sub-rede do front-end para alojar uma aplicação web e uma sub-rede de back-end para o alojamento de um servidor de base de dados.</span><span class="sxs-lookup"><span data-stu-id="8de79-124">A front-end subnet for hosting a web application, and a back-end subnet for hosting a database server.</span></span>

<span data-ttu-id="8de79-125">Antes de poder criar uma rede virtual, crie um grupo de recursos com [criar grupo az](/cli/azure/group#create).</span><span class="sxs-lookup"><span data-stu-id="8de79-125">Before you can create a virtual network, create a resource group with [az group create](/cli/azure/group#create).</span></span> <span data-ttu-id="8de79-126">Olá exemplo seguinte cria um grupo de recursos denominado *myRGNetwork* na localização de eastus Olá.</span><span class="sxs-lookup"><span data-stu-id="8de79-126">hello following example creates a resource group named *myRGNetwork* in hello eastus location.</span></span>

```azurecli-interactive 
az group create --name myRGNetwork --location eastus
```

### <a name="create-virtual-network"></a><span data-ttu-id="8de79-127">Criar a rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-127">Create virtual network</span></span>

<span data-ttu-id="8de79-128">Nos Olá [az rede vnet criar](/cli/azure/network/vnet#create) comando toocreate uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="8de79-128">Us hello [az network vnet create](/cli/azure/network/vnet#create) command toocreate a virtual network.</span></span> <span data-ttu-id="8de79-129">Neste exemplo, é denominado rede Olá *mvVnet* e é dado um prefixo de endereço de *10.0.0.0/16*.</span><span class="sxs-lookup"><span data-stu-id="8de79-129">In this example, hello network is named *mvVnet* and is given an address prefix of *10.0.0.0/16*.</span></span> <span data-ttu-id="8de79-130">Uma sub-rede também é criada com um nome de *mySubnetFrontEnd* e um prefixo de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8de79-130">A subnet is also created with a name of *mySubnetFrontEnd* and a prefix of *10.0.1.0/24*.</span></span> <span data-ttu-id="8de79-131">Mais tarde no tutorial uma VM de front-end é ligado toothis sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-131">Later in this tutorial a front-end VM is connected toothis subnet.</span></span> 

```azurecli-interactive 
az network vnet create \
  --resource-group myRGNetwork \
  --name myVnet \
  --address-prefix 10.0.0.0/16 \
  --subnet-name mySubnetFrontEnd \
  --subnet-prefix 10.0.1.0/24
```

### <a name="create-subnet"></a><span data-ttu-id="8de79-132">Criar sub-rede</span><span class="sxs-lookup"><span data-stu-id="8de79-132">Create subnet</span></span>

<span data-ttu-id="8de79-133">Uma nova sub-rede é adicionada a rede virtual toohello utilizando Olá [az rede vnet sub-rede](/cli/azure/network/vnet/subnet#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8de79-133">A new subnet is added toohello virtual network using hello [az network vnet subnet create](/cli/azure/network/vnet/subnet#create) command.</span></span> <span data-ttu-id="8de79-134">Neste exemplo, é denominado sub-rede Olá *mySubnetBackEnd* e é dado um prefixo de endereço de *10.0.2.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8de79-134">In this example, hello subnet is named *mySubnetBackEnd* and is given an address prefix of *10.0.2.0/24*.</span></span> <span data-ttu-id="8de79-135">Esta sub-rede é utilizada com todos os serviços de back-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-135">This subnet is used with all back-end services.</span></span>

```azurecli-interactive 
az network vnet subnet create \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --address-prefix 10.0.2.0/24
```

<span data-ttu-id="8de79-136">Neste momento, uma rede foi criada e segmentada em duas sub-redes, um para serviços front-end e outra para serviços de back-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-136">At this point, a network has been created and segmented into two subnets, one for front-end services, and another for back-end services.</span></span> <span data-ttu-id="8de79-137">Na secção seguinte, Olá, as máquinas virtuais são criadas e ligados a sub-redes toothese.</span><span class="sxs-lookup"><span data-stu-id="8de79-137">In hello next section, virtual machines are created and connected toothese subnets.</span></span>

## <a name="understand-public-ip-address"></a><span data-ttu-id="8de79-138">Compreender o endereço IP público</span><span class="sxs-lookup"><span data-stu-id="8de79-138">Understand public IP address</span></span>

<span data-ttu-id="8de79-139">Um endereço IP público permite toobe de recursos do Azure acessíveis no Olá internet.</span><span class="sxs-lookup"><span data-stu-id="8de79-139">A public IP address allows Azure resources toobe accessible on hello internet.</span></span> <span data-ttu-id="8de79-140">Esta secção do tutorial Olá, é criada uma VM toodemonstrate como endereços toowork com IP público.</span><span class="sxs-lookup"><span data-stu-id="8de79-140">In this section of hello tutorial, a VM is created toodemonstrate how toowork with public IP addresses.</span></span>

### <a name="allocation-method"></a><span data-ttu-id="8de79-141">Método de alocação</span><span class="sxs-lookup"><span data-stu-id="8de79-141">Allocation method</span></span>

<span data-ttu-id="8de79-142">Um endereço IP público que pode ser atribuído como dinâmico ou estático.</span><span class="sxs-lookup"><span data-stu-id="8de79-142">A public IP address can be allocated as either dynamic or static.</span></span> <span data-ttu-id="8de79-143">Por predefinição, o endereço IP público dinamicamente atribuído.</span><span class="sxs-lookup"><span data-stu-id="8de79-143">By default, public IP address dynamically allocated.</span></span> <span data-ttu-id="8de79-144">Endereços IP dinâmicos são lançados quando uma VM é desalocada.</span><span class="sxs-lookup"><span data-stu-id="8de79-144">Dynamic IP addresses are released when a VM is deallocated.</span></span> <span data-ttu-id="8de79-145">Este comportamento faz com que toochange de endereço IP de Olá durante qualquer operação que inclua uma Desalocação da VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-145">This behavior causes hello IP address toochange during any operation that includes a VM deallocation.</span></span>

<span data-ttu-id="8de79-146">método de alocação de Olá pode ser definido toostatic, que garante que o endereço IP Olá permanecem atribuídos tooa VM, mesmo durante um Estado desalocado.</span><span class="sxs-lookup"><span data-stu-id="8de79-146">hello allocation method can be set toostatic, which ensures that hello IP address remain assigned tooa VM, even during a deallocated state.</span></span> <span data-ttu-id="8de79-147">Quando utilizar um endereço IP estaticamente atribuído, não não possível especificar endereços IP Olá próprio.</span><span class="sxs-lookup"><span data-stu-id="8de79-147">When using a statically allocated IP address, hello IP address itself cannot be specified.</span></span> <span data-ttu-id="8de79-148">Em vez disso, é atribuído partir de um conjunto de endereços disponíveis.</span><span class="sxs-lookup"><span data-stu-id="8de79-148">Instead, it is allocated from a pool of available addresses.</span></span>

### <a name="dynamic-allocation"></a><span data-ttu-id="8de79-149">Alocação dinâmica</span><span class="sxs-lookup"><span data-stu-id="8de79-149">Dynamic allocation</span></span>

<span data-ttu-id="8de79-150">Ao criar uma VM com Olá [az vm criar](/cli/azure/vm#create) comando, Olá público IP endereço alocação método predefinido é dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8de79-150">When creating a VM with hello [az vm create](/cli/azure/vm#create) command, hello default public IP address allocation method is dynamic.</span></span> <span data-ttu-id="8de79-151">No seguinte exemplo de Olá, é criada uma VM com um endereço IP dinâmico.</span><span class="sxs-lookup"><span data-stu-id="8de79-151">In hello following example, a VM is created with a dynamic IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myFrontEndVM \
  --vnet-name myVnet \
  --subnet mySubnetFrontEnd \
  --nsg myNSGFrontEnd \
  --public-ip-address myFrontEndIP \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="static-allocation"></a><span data-ttu-id="8de79-152">Alocação estática</span><span class="sxs-lookup"><span data-stu-id="8de79-152">Static allocation</span></span>

<span data-ttu-id="8de79-153">Ao criar uma máquina virtual utilizando Olá [az vm criar](/cli/azure/vm#create) comando, incluir Olá `--public-ip-address-allocation static` argumento tooassign um endereço IP público estático.</span><span class="sxs-lookup"><span data-stu-id="8de79-153">When creating a virtual machine using hello [az vm create](/cli/azure/vm#create) command, include hello `--public-ip-address-allocation static` argument tooassign a static public IP address.</span></span> <span data-ttu-id="8de79-154">Esta operação não é demonstrada neste tutorial, no entanto na Olá secção seguinte, um endereço IP alocado dinamicamente é alterada tooa estaticamente o endereço alocado.</span><span class="sxs-lookup"><span data-stu-id="8de79-154">This operation is not demonstrated in this tutorial, however in hello next section a dynamically allocated IP address is changed tooa statically allocated address.</span></span> 

### <a name="change-allocation-method"></a><span data-ttu-id="8de79-155">Alterar o método de alocação</span><span class="sxs-lookup"><span data-stu-id="8de79-155">Change allocation method</span></span>

<span data-ttu-id="8de79-156">método de alocação de endereço IP Olá pode ser alterado utilizando Olá [atualização de ip público de rede az](/cli/azure/network/public-ip#update) comando.</span><span class="sxs-lookup"><span data-stu-id="8de79-156">hello IP address allocation method can be changed using hello [az network public-ip update](/cli/azure/network/public-ip#update) command.</span></span> <span data-ttu-id="8de79-157">Neste exemplo, Olá método de alocação de endereço IP de front-end VM é alterado de Olá toostatic.</span><span class="sxs-lookup"><span data-stu-id="8de79-157">In this example, hello IP address allocation method of hello front-end VM is changed toostatic.</span></span>

<span data-ttu-id="8de79-158">Em primeiro lugar, desalocar Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-158">First, deallocate hello VM.</span></span>

```azurecli-interactive 
az vm deallocate --resource-group myRGNetwork --name myFrontEndVM
```

<span data-ttu-id="8de79-159">Olá utilize [atualização de ip público de rede az](/cli/azure/network/public-ip#update) método de alocação de Olá tooupdate de comandos.</span><span class="sxs-lookup"><span data-stu-id="8de79-159">Use hello [az network public-ip update](/cli/azure/network/public-ip#update) command tooupdate hello allocation method.</span></span> <span data-ttu-id="8de79-160">Neste caso, Olá `--allocation-method` está a ser definido demasiado*estático*.</span><span class="sxs-lookup"><span data-stu-id="8de79-160">In this case, hello `--allocation-method` is being set too*static*.</span></span>

```azurecli-interactive 
az network public-ip update --resource-group myRGNetwork --name myFrontEndIP --allocation-method static
```

<span data-ttu-id="8de79-161">Inicie Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-161">Start hello VM.</span></span>

```azurecli-interactive 
az vm start --resource-group myRGNetwork --name myFrontEndVM --no-wait
```

### <a name="no-public-ip-address"></a><span data-ttu-id="8de79-162">Nenhum endereço IP público</span><span class="sxs-lookup"><span data-stu-id="8de79-162">No public IP address</span></span>

<span data-ttu-id="8de79-163">Muitas vezes, uma VM não necessitam de toobe acessível através de Olá internet.</span><span class="sxs-lookup"><span data-stu-id="8de79-163">Often, a VM does not need toobe accessible over hello internet.</span></span> <span data-ttu-id="8de79-164">toocreate uma VM sem um endereço IP público, utilize Olá `--public-ip-address ""` argumento com um conjunto vazio de aspas duplas.</span><span class="sxs-lookup"><span data-stu-id="8de79-164">toocreate a VM without a public IP address, use hello `--public-ip-address ""` argument with an empty set of double quotes.</span></span> <span data-ttu-id="8de79-165">Esta configuração é demonstrada mais à frente neste tutorial</span><span class="sxs-lookup"><span data-stu-id="8de79-165">This configuration is demonstrated later in this tutorial</span></span>

## <a name="secure-network-traffic"></a><span data-ttu-id="8de79-166">Proteja o tráfego de rede</span><span class="sxs-lookup"><span data-stu-id="8de79-166">Secure network traffic</span></span>

<span data-ttu-id="8de79-167">Um grupo de segurança de rede (NSG) contém uma lista de regras de segurança que permitem ou negam tooresources de tráfego de rede ligado tooAzure redes virtuais (VNet).</span><span class="sxs-lookup"><span data-stu-id="8de79-167">A network security group (NSG) contains a list of security rules that allow or deny network traffic tooresources connected tooAzure Virtual Networks (VNet).</span></span> <span data-ttu-id="8de79-168">Os NSGs podem ser associados toosubnets ou as interfaces de rede individuais.</span><span class="sxs-lookup"><span data-stu-id="8de79-168">NSGs can be associated toosubnets or individual network interfaces.</span></span> <span data-ttu-id="8de79-169">Quando um NSG é associado uma interface de rede, aplica-se apenas Olá associado à VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-169">When an NSG is associated with a network interface, it applies only hello associated VM.</span></span> <span data-ttu-id="8de79-170">Quando um NSG é associado tooa sub-rede, Olá aplicam-se regras tooall recursos ligados toohello sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-170">When an NSG is associated tooa subnet, hello rules apply tooall resources connected toohello subnet.</span></span> 

### <a name="network-security-group-rules"></a><span data-ttu-id="8de79-171">Regras do grupo de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="8de79-171">Network security group rules</span></span>

<span data-ttu-id="8de79-172">Regras do NSG definem portas de rede durante o qual o tráfego é permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="8de79-172">NSG rules define networking ports over which traffic is allowed or denied.</span></span> <span data-ttu-id="8de79-173">regras de Olá podem incluir intervalos de endereços IP de origem e de destino para que o tráfego é controlado entre sistemas específicos ou sub-redes.</span><span class="sxs-lookup"><span data-stu-id="8de79-173">hello rules can include source and destination IP address ranges so that traffic is controlled between specific systems or subnets.</span></span> <span data-ttu-id="8de79-174">Regras do NSG também incluem uma prioridade de (entre 1 — e 4096).</span><span class="sxs-lookup"><span data-stu-id="8de79-174">NSG rules also include a priority (between 1—and 4096).</span></span> <span data-ttu-id="8de79-175">As regras são avaliadas por ordem de Olá de prioridade.</span><span class="sxs-lookup"><span data-stu-id="8de79-175">Rules are evaluated in hello order of priority.</span></span> <span data-ttu-id="8de79-176">Uma regra com uma prioridade de 100 é avaliada antes de uma regra com prioridade 200.</span><span class="sxs-lookup"><span data-stu-id="8de79-176">A rule with a priority of 100 is evaluated before a rule with priority 200.</span></span>

<span data-ttu-id="8de79-177">Todos os NSGs contêm um conjunto de regras predefinidas.</span><span class="sxs-lookup"><span data-stu-id="8de79-177">All NSGs contain a set of default rules.</span></span> <span data-ttu-id="8de79-178">regras de predefinidas Olá não podem ser eliminadas, mas como lhes é atribuída a prioridade mais baixa Olá, podem ser substituídas pelas regras de Olá que criar.</span><span class="sxs-lookup"><span data-stu-id="8de79-178">hello default rules cannot be deleted, but because they are assigned hello lowest priority, they can be overridden by hello rules that you create.</span></span>

- <span data-ttu-id="8de79-179">**Rede virtual** - tráfego com origem e de fim numa rede virtual é permitido nas direções de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="8de79-179">**Virtual network** - Traffic originating and ending in a virtual network is allowed both in inbound and outbound directions.</span></span>
- <span data-ttu-id="8de79-180">**Internet** - o tráfego de saída é permitido, mas o tráfego de entrada está bloqueado.</span><span class="sxs-lookup"><span data-stu-id="8de79-180">**Internet** - Outbound traffic is allowed, but inbound traffic is blocked.</span></span>
- <span data-ttu-id="8de79-181">**O Balanceador de carga** -carga balanceador tooprobe Olá estado de funcionamento permitir do Azure das VMs e instâncias de função.</span><span class="sxs-lookup"><span data-stu-id="8de79-181">**Load balancer** - Allow Azure’s load balancer tooprobe hello health of your VMs and role instances.</span></span> <span data-ttu-id="8de79-182">Se não estiver a utilizar um conjunto com balanceamento de carga, pode substituir esta regra.</span><span class="sxs-lookup"><span data-stu-id="8de79-182">If you are not using a load balanced set, you can override this rule.</span></span>

### <a name="create-network-security-groups"></a><span data-ttu-id="8de79-183">Criar grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="8de79-183">Create network security groups</span></span>

<span data-ttu-id="8de79-184">Um grupo de segurança de rede pode ser criado em Olá mesmo tempo, como uma VM utilizando Olá [az vm criar](/cli/azure/vm#create) comando.</span><span class="sxs-lookup"><span data-stu-id="8de79-184">A network security group can be created at hello same time as a VM using hello [az vm create](/cli/azure/vm#create) command.</span></span> <span data-ttu-id="8de79-185">Ao fazê-lo, Olá NSG é associado a interface de rede de VMs de Olá e uma regra de NSG é criada automaticamente tooallow tráfego na porta *22* de uma origem.</span><span class="sxs-lookup"><span data-stu-id="8de79-185">When doing so, hello NSG is associated with hello VMs network interface and an NSG rule is auto created tooallow traffic on port *22* from any source.</span></span> <span data-ttu-id="8de79-186">Anteriormente no tutorial, Olá front-end NSG foi criado automaticamente com Olá VM front-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-186">Earlier in this tutorial, hello front-end NSG was auto-created with hello front-end VM.</span></span> <span data-ttu-id="8de79-187">Uma regra NSG também foi criada para a porta 22 automaticamente.</span><span class="sxs-lookup"><span data-stu-id="8de79-187">An NSG rule was also auto created for port 22.</span></span> 

<span data-ttu-id="8de79-188">Em alguns casos, poderá ser útil toopre-criar um NSG, por exemplo, quando não devem ser criadas regras SSH predefinidas ou quando Olá NSG deve ser anexado tooa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-188">In some cases, it may be helpful toopre-create an NSG, such as when default SSH rules should not be created, or when hello NSG should be attached tooa subnet.</span></span> 

<span data-ttu-id="8de79-189">Olá utilize [az rede nsg criar](/cli/azure/network/nsg#create) comando toocreate um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-189">Use hello [az network nsg create](/cli/azure/network/nsg#create) command toocreate a network security group.</span></span>

```azurecli-interactive 
az network nsg create --resource-group myRGNetwork --name myNSGBackEnd
```

<span data-ttu-id="8de79-190">Em vez de associação de interface de rede do Olá NSG tooa, está associada a uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="8de79-190">Instead of associating hello NSG tooa network interface, it is associated with a subnet.</span></span> <span data-ttu-id="8de79-191">Nesta configuração, qualquer VM que é anexado toohello sub-rede herda as regras do NSG Olá.</span><span class="sxs-lookup"><span data-stu-id="8de79-191">In this configuration, any VM that is attached toohello subnet inherits hello NSG rules.</span></span>

<span data-ttu-id="8de79-192">Atualizar a sub-rede existente Olá designada *mySubnetBackEnd* com Olá novo NSG.</span><span class="sxs-lookup"><span data-stu-id="8de79-192">Update hello existing subnet named *mySubnetBackEnd* with hello new NSG.</span></span>

```azurecli-interactive 
az network vnet subnet update \
  --resource-group myRGNetwork \
  --vnet-name myVnet \
  --name mySubnetBackEnd \
  --network-security-group myNSGBackEnd
```

<span data-ttu-id="8de79-193">Agora criar uma máquina virtual, que é anexado toohello *mySubnetBackEnd*.</span><span class="sxs-lookup"><span data-stu-id="8de79-193">Now create a virtual machine, which is attached toohello *mySubnetBackEnd*.</span></span> <span data-ttu-id="8de79-194">Tenha em atenção que Olá `--nsg` argument tem um valor de aspas duplas vazios.</span><span class="sxs-lookup"><span data-stu-id="8de79-194">Notice that hello `--nsg` argument has a value of empty double quotes.</span></span> <span data-ttu-id="8de79-195">Um NSG não precisa de toobe criado com Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-195">An NSG does not need toobe created with hello VM.</span></span> <span data-ttu-id="8de79-196">Olá VM é sub-rede de back-end toohello anexado, o que é protegida com Olá pré-criadas NSG de back-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-196">hello VM is attached toohello back-end subnet, which is protected with hello pre-created back-end NSG.</span></span> <span data-ttu-id="8de79-197">Este NSG aplica-se toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-197">This NSG applies toohello VM.</span></span> <span data-ttu-id="8de79-198">Além disso, repare que Olá `--public-ip-address` argument tem um valor de aspas duplas vazios.</span><span class="sxs-lookup"><span data-stu-id="8de79-198">Also, notice here that hello `--public-ip-address` argument has a value of empty double quotes.</span></span> <span data-ttu-id="8de79-199">Esta configuração cria uma VM sem um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="8de79-199">This configuration creates a VM without a public IP address.</span></span> 

```azurecli-interactive 
az vm create \
  --resource-group myRGNetwork \
  --name myBackEndVM \
  --vnet-name myVnet \
  --subnet mySubnetBackEnd \
  --public-ip-address "" \
  --nsg "" \
  --image UbuntuLTS \
  --generate-ssh-keys
```

### <a name="secure-incoming-traffic"></a><span data-ttu-id="8de79-200">Proteger o tráfego de entrada</span><span class="sxs-lookup"><span data-stu-id="8de79-200">Secure incoming traffic</span></span>

<span data-ttu-id="8de79-201">Quando hello front-end VM foi criada, NSG foi criada uma regra tooallow tráfego de entrada na porta 22.</span><span class="sxs-lookup"><span data-stu-id="8de79-201">When hello front-end VM was created, an NSG rule was created tooallow incoming traffic on port 22.</span></span> <span data-ttu-id="8de79-202">Esta regra permite SSH ligações toohello VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-202">This rule allows SSH connections toohello VM.</span></span> <span data-ttu-id="8de79-203">Neste exemplo, também deve ser permitido tráfego na porta *80*.</span><span class="sxs-lookup"><span data-stu-id="8de79-203">For this example, traffic should also be allowed on port *80*.</span></span> <span data-ttu-id="8de79-204">Esta configuração permite que um toobe de aplicação web acedida num Olá VM.</span><span class="sxs-lookup"><span data-stu-id="8de79-204">This configuration allows a web application toobe accessed on hello VM.</span></span>

<span data-ttu-id="8de79-205">Olá utilize [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra para a porta *80*.</span><span class="sxs-lookup"><span data-stu-id="8de79-205">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port *80*.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGFrontEnd \
  --name http \
  --access allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range 80
```

<span data-ttu-id="8de79-206">Olá VM front-end agora só é acessível na porta *22* e a porta *80*.</span><span class="sxs-lookup"><span data-stu-id="8de79-206">hello front-end VM is now only accessible on port *22* and port *80*.</span></span> <span data-ttu-id="8de79-207">Todos os outro tráfego de entrada é bloqueado no grupo de segurança de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="8de79-207">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="8de79-208">Poderá ser útil toovisualize as configurações de regra do Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8de79-208">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="8de79-209">Configuração de regras NSG Olá retorno com Olá [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="8de79-209">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGFrontEnd --output table
```

<span data-ttu-id="8de79-210">Saída:</span><span class="sxs-lookup"><span data-stu-id="8de79-210">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix      DestinationPortRange  Direction    Name                 Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -----------------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                                               22  Inbound      default-allow-ssh        1000  Tcp         Succeeded            myRGNetwork      *                      *
Allow     *                                               80  Inbound      http                      200  Tcp         Succeeded            myRGNetwork      *                      *
```

### <a name="secure-vm-toovm-traffic"></a><span data-ttu-id="8de79-211">Proteger o tráfego de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="8de79-211">Secure VM tooVM traffic</span></span>

<span data-ttu-id="8de79-212">Regras do grupo de segurança de rede também podem aplicar entre as VMs.</span><span class="sxs-lookup"><span data-stu-id="8de79-212">Network security group rules can also apply between VMs.</span></span> <span data-ttu-id="8de79-213">Para este exemplo Olá VM front-end tem toocommunicate com Olá VM de back-end na porta *22* e *3306*.</span><span class="sxs-lookup"><span data-stu-id="8de79-213">For this example, hello front-end VM needs toocommunicate with hello back-end VM on port *22* and *3306*.</span></span> <span data-ttu-id="8de79-214">Esta configuração permite ligações SSH de Olá VM front-end e também permitir que uma aplicação no front-end VM toocommunicate Olá com uma base de dados MySQL back-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-214">This configuration allows SSH connections from hello front-end VM, and also allow an application on hello front-end VM toocommunicate with a back-end MySQL database.</span></span> <span data-ttu-id="8de79-215">Todo o restante tráfego deve ser bloqueado entre Olá front-end e back-end máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="8de79-215">All other traffic should be blocked between hello front-end and back-end virtual machines.</span></span>

<span data-ttu-id="8de79-216">Olá utilize [criar regras de nsg de rede az](/cli/azure/network/nsg/rule#create) comando toocreate uma regra para a porta 22.</span><span class="sxs-lookup"><span data-stu-id="8de79-216">Use hello [az network nsg rule create](/cli/azure/network/nsg/rule#create) command toocreate a rule for port 22.</span></span> <span data-ttu-id="8de79-217">Tenha em atenção que Olá `--source-address-prefix` argumento especifica um valor de *10.0.1.0/24*.</span><span class="sxs-lookup"><span data-stu-id="8de79-217">Notice that hello `--source-address-prefix` argument specifies a value of *10.0.1.0/24*.</span></span> <span data-ttu-id="8de79-218">Esta configuração assegura que apenas o tráfego de sub-rede de front-end Olá é permitido através de Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8de79-218">This configuration ensures that only traffic from hello front-end subnet is allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name SSH \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 100 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "22"
```

<span data-ttu-id="8de79-219">Agora, adicione uma regra para o tráfego de MySQL na porta 3306.</span><span class="sxs-lookup"><span data-stu-id="8de79-219">Now add a rule for MySQL traffic on port 3306.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name MySQL \
  --access Allow \
  --protocol Tcp \
  --direction Inbound \
  --priority 200 \
  --source-address-prefix 10.0.1.0/24 \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "3306"
```

<span data-ttu-id="8de79-220">Por fim, porque os NSGs tem uma regra predefinida, permitindo todo o tráfego entre VMs na Olá mesma VNet, uma regra pode ser criada para Olá back-end NSGs tooblock todo o tráfego.</span><span class="sxs-lookup"><span data-stu-id="8de79-220">Finally, because NSGs have a default rule allowing all traffic between VMs in hello same VNet, a rule can be created for hello back-end NSGs tooblock all traffic.</span></span> <span data-ttu-id="8de79-221">Repare que Olá `--priority` é atribuído um valor de *300*, que é menor do que Olá ambas as regras do NSG e MySQL.</span><span class="sxs-lookup"><span data-stu-id="8de79-221">Notice here that hello `--priority` is given a value of *300*, which is lower that both hello NSG and MySQL rules.</span></span> <span data-ttu-id="8de79-222">Esta configuração assegura que o tráfego SSH e o MySQL ainda é permitido através de Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8de79-222">This configuration ensures that SSH and MySQL traffic is still allowed through hello NSG.</span></span>

```azurecli-interactive 
az network nsg rule create \
  --resource-group myRGNetwork \
  --nsg-name myNSGBackEnd \
  --name denyAll \
  --access Deny \
  --protocol Tcp \
  --direction Inbound \
  --priority 300 \
  --source-address-prefix "*" \
  --source-port-range "*" \
  --destination-address-prefix "*" \
  --destination-port-range "*"
```

<span data-ttu-id="8de79-223">Olá VM de back-end agora só é acessível na porta *22* e a porta *3306* da sub-rede Olá de front-end.</span><span class="sxs-lookup"><span data-stu-id="8de79-223">hello back-end VM is now only accessible on port *22* and port *3306* from hello front-end subnet.</span></span> <span data-ttu-id="8de79-224">Todos os outro tráfego de entrada é bloqueado no grupo de segurança de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="8de79-224">All other incoming traffic is blocked at hello network security group.</span></span> <span data-ttu-id="8de79-225">Poderá ser útil toovisualize as configurações de regra do Olá NSG.</span><span class="sxs-lookup"><span data-stu-id="8de79-225">It may be helpful toovisualize hello NSG rule configurations.</span></span> <span data-ttu-id="8de79-226">Configuração de regras NSG Olá retorno com Olá [lista de regras de rede az](/cli/azure/network/nsg/rule#list) comando.</span><span class="sxs-lookup"><span data-stu-id="8de79-226">Return hello NSG rule configuration with hello [az network rule list](/cli/azure/network/nsg/rule#list) command.</span></span> 

```azurecli-interactive 
az network nsg rule list --resource-group myRGNetwork --nsg-name myNSGBackEnd --output table
```

<span data-ttu-id="8de79-227">Saída:</span><span class="sxs-lookup"><span data-stu-id="8de79-227">Output:</span></span>

```azurecli-interactive 
Access    DestinationAddressPrefix    DestinationPortRange    Direction    Name       Priority  Protocol    ProvisioningState    ResourceGroup    SourceAddressPrefix    SourcePortRange
--------  --------------------------  ----------------------  -----------  -------  ----------  ----------  -------------------  ---------------  ---------------------  -----------------
Allow     *                           22                      Inbound      SSH             100  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Allow     *                           3306                    Inbound      MySQL           200  Tcp         Succeeded            myRGNetwork      10.0.1.0/24            *
Deny      *                           *                       Inbound      denyAll         300  Tcp         Succeeded            myRGNetwork      *                      *
```

## <a name="next-steps"></a><span data-ttu-id="8de79-228">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="8de79-228">Next steps</span></span>

<span data-ttu-id="8de79-229">Neste tutorial, criou e redes do Azure como toovirtual relacionados máquinas protegidas.</span><span class="sxs-lookup"><span data-stu-id="8de79-229">In this tutorial, you created and secured Azure networks as related toovirtual machines.</span></span> <span data-ttu-id="8de79-230">Aprendeu a:</span><span class="sxs-lookup"><span data-stu-id="8de79-230">You learned how to:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8de79-231">Implementar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-231">Deploy a virtual network</span></span>
> * <span data-ttu-id="8de79-232">Criar uma sub-rede dentro de uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-232">Create a subnet within a virtual network</span></span>
> * <span data-ttu-id="8de79-233">Ligar máquinas virtuais tooa sub-rede</span><span class="sxs-lookup"><span data-stu-id="8de79-233">Attach virtual machines tooa subnet</span></span>
> * <span data-ttu-id="8de79-234">Gerir endereços IP públicos de máquina virtual</span><span class="sxs-lookup"><span data-stu-id="8de79-234">Manage virtual machine public IP addresses</span></span>
> * <span data-ttu-id="8de79-235">Proteger o tráfego de internet de entrada</span><span class="sxs-lookup"><span data-stu-id="8de79-235">Secure incoming internet traffic</span></span>
> * <span data-ttu-id="8de79-236">Proteger o tráfego de tooVM VM</span><span class="sxs-lookup"><span data-stu-id="8de79-236">Secure VM tooVM traffic</span></span>

<span data-ttu-id="8de79-237">Produzir toohello seguinte toolearn tutorial sobre como proteger dados em máquinas virtuais utilizando cópia de segurança do Azure.</span><span class="sxs-lookup"><span data-stu-id="8de79-237">Advance toohello next tutorial toolearn about securing data on virtual machines using Azure backup.</span></span> 

> [!div class="nextstepaction"]
> [<span data-ttu-id="8de79-238">Cópia de segurança de computadores virtuais Linux no Azure</span><span class="sxs-lookup"><span data-stu-id="8de79-238">Back up Linux virtual machines in Azure</span></span>](./tutorial-backup-vms.md)
