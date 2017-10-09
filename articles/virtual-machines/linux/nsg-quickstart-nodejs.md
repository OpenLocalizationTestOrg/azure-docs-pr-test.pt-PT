---
title: aaaOpen portas tooa VM com Linux com a CLI do Azure 1.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto final tooyour VM com Linux utilizando a implementação de Gestor de recursos do Azure Olá modelar e Olá CLI do Azure 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a><span data-ttu-id="2c1dc-103">Abrir portas e os pontos finais tooa VM com Linux no Azure com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="2c1dc-103">Opening ports and endpoints tooa Linux VM in Azure using hello Azure CLI 1.0</span></span>
<span data-ttu-id="2c1dc-104">Abrir uma porta ou criar um ponto final, tooa máquina virtual (VM) no Azure através da criação de um filtro de rede numa sub-rede ou interface de rede VM.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-104">You open a port, or create an endpoint, tooa virtual machine (VM) in Azure by creating a network filter on a subnet or VM network interface.</span></span> <span data-ttu-id="2c1dc-105">Colocar estes filtros que controlam o tráfego de entrada e saído, num grupo de segurança de rede ligado toohello recurso que recebe o tráfego de Olá.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-105">You place these filters, which control both inbound and outbound traffic, on a Network Security Group attached toohello resource that receives hello traffic.</span></span> <span data-ttu-id="2c1dc-106">Vamos utilizar um exemplo comum de tráfego da web na porta 80.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-106">Let's use a common example of web traffic on port 80.</span></span> <span data-ttu-id="2c1dc-107">Este artigo mostra como tooopen uma porta tooa VM utilizando Olá CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-107">This article shows you how tooopen a port tooa VM using hello Azure CLI 1.0.</span></span>


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="2c1dc-108">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="2c1dc-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="2c1dc-109">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="2c1dc-110">[Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="2c1dc-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="2c1dc-111">[Azure CLI 2.0](nsg-quickstart.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="2c1dc-111">[Azure CLI 2.0](nsg-quickstart.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="2c1dc-112">Comandos rápidos</span><span class="sxs-lookup"><span data-stu-id="2c1dc-112">Quick commands</span></span>
<span data-ttu-id="2c1dc-113">toocreate um grupo de segurança de rede e as regras terá [Olá CLI do Azure 1.0](../../cli-install-nodejs.md) instalado e o modo Resource Manager:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-113">toocreate a Network Security Group and rules you need [hello Azure CLI 1.0](../../cli-install-nodejs.md) installed and using Resource Manager mode:</span></span>

```azurecli
azure config mode arm
```

<span data-ttu-id="2c1dc-114">No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-114">In hello following examples, replace example parameter names with your own values.</span></span> <span data-ttu-id="2c1dc-115">Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *myNetworkSecurityGroup*, e *myVnet*.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-115">Example parameter names included *myResourceGroup*, *myNetworkSecurityGroup*, and *myVnet*.</span></span>

<span data-ttu-id="2c1dc-116">Crie o grupo de segurança de rede, introduzir os seus próprios nomes e a localização correta.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-116">Create your Network Security Group, entering your own names and location appropriately.</span></span> <span data-ttu-id="2c1dc-117">Olá exemplo seguinte cria um grupo de segurança de rede com o nome *myNetworkSecurityGroup* no Olá *eastus* localização:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-117">hello following example creates a Network Security Group named *myNetworkSecurityGroup* in hello *eastus* location:</span></span>

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

<span data-ttu-id="2c1dc-118">Adicionar uma regra tooallow HTTP tráfego tooyour webserver (ou ajustar o seus próprios cenário, tais como a conectividade de acesso ou a base de dados SSH).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-118">Add a rule tooallow HTTP traffic tooyour webserver (or adjust for your own scenario, such as SSH access or database connectivity).</span></span> <span data-ttu-id="2c1dc-119">Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-119">hello following example creates a rule named *myNetworkSecurityGroupRule* tooallow TCP traffic on port 80:</span></span>

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

<span data-ttu-id="2c1dc-120">Olá associar grupo de segurança de rede com a interface de rede da VM (NIC).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-120">Associate hello Network Security Group with your VM's network interface (NIC).</span></span> <span data-ttu-id="2c1dc-121">Olá exemplo seguinte associa uma NIC existente com o nome *myNic* com o grupo de segurança de rede com o nome de Olá *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-121">hello following example associates an existing NIC named *myNic* with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

<span data-ttu-id="2c1dc-122">Em alternativa, pode associar o seu grupo de segurança de rede com uma sub-rede da rede virtual em vez de apenas interface de rede toohello numa única VM.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-122">Alternatively, you can associate your Network Security Group with a virtual network subnet rather than just toohello network interface on a single VM.</span></span> <span data-ttu-id="2c1dc-123">Olá exemplo seguinte associa uma sub-rede existente com o nome *mySubnet* no Olá *myVnet* rede virtual com o grupo de segurança de rede com o nome de Olá *myNetworkSecurityGroup*:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-123">hello following example associates an existing subnet named *mySubnet* in hello *myVnet* virtual network with hello Network Security Group named *myNetworkSecurityGroup*:</span></span>

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a><span data-ttu-id="2c1dc-124">Obter mais informações sobre grupos de segurança de rede</span><span class="sxs-lookup"><span data-stu-id="2c1dc-124">More information on Network Security Groups</span></span>
<span data-ttu-id="2c1dc-125">comandos rápidos Olá aqui permitem-lhe tooget cópias de segurança e em execução com tooyour de fluxo de tráfego VM.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-125">hello quick commands here allow you tooget up and running with traffic flowing tooyour VM.</span></span> <span data-ttu-id="2c1dc-126">Grupos de segurança de rede fornecem várias funcionalidades excelentes e granularidade para controlar aceder a recursos tooyour.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-126">Network Security Groups provide many great features and granularity for controlling access tooyour resources.</span></span> <span data-ttu-id="2c1dc-127">Pode ler mais sobre [criar um grupo de segurança de rede e a ACL regras aqui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-127">You can read more about [creating a Network Security Group and ACL rules here](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).</span></span>

<span data-ttu-id="2c1dc-128">Pode definir grupos de segurança de rede e as regras de ACL como parte dos modelos Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-128">You can define Network Security Groups and ACL rules as part of Azure Resource Manager templates.</span></span> <span data-ttu-id="2c1dc-129">Leia mais sobre [criar grupos de segurança de rede com modelos](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-129">Read more about [creating Network Security Groups with templates](../../virtual-network/virtual-networks-create-nsg-arm-template.md).</span></span>

<span data-ttu-id="2c1dc-130">Se precisar de toouse porta reencaminhamento toomap uma porta de interno tooan porta externa exclusivo na sua VM, utilize um balanceador de carga e regras de tradução de endereços de rede (NAT).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-130">If you need toouse port-forwarding toomap a unique external port tooan internal port on your VM, use a load balancer and Network Address Translation (NAT) rules.</span></span> <span data-ttu-id="2c1dc-131">Por exemplo, pode pretender tooexpose TCP porta 8080 externamente e ter tráfego direcionado tooTCP porta 80 numa VM.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-131">For example, you may want tooexpose TCP port 8080 externally and have traffic directed tooTCP port 80 on a VM.</span></span> <span data-ttu-id="2c1dc-132">Pode saber mais sobre [criação de um balanceador de carga para a Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span><span class="sxs-lookup"><span data-stu-id="2c1dc-132">You can learn about [creating an Internet-facing load balancer](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2c1dc-133">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="2c1dc-133">Next steps</span></span>
<span data-ttu-id="2c1dc-134">Neste exemplo, criou um tráfego de tooallow HTTP regra simples.</span><span class="sxs-lookup"><span data-stu-id="2c1dc-134">In this example, you created a simple rule tooallow HTTP traffic.</span></span> <span data-ttu-id="2c1dc-135">Pode encontrar informações sobre como criar ambientes mais detalhados no Olá seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="2c1dc-135">You can find information on creating more detailed environments in hello following articles:</span></span>

* [<span data-ttu-id="2c1dc-136">Descrição geral do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="2c1dc-136">Azure Resource Manager overview</span></span>](../../azure-resource-manager/resource-group-overview.md)
* [<span data-ttu-id="2c1dc-137">O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)</span><span class="sxs-lookup"><span data-stu-id="2c1dc-137">What is a Network Security Group (NSG)?</span></span>](../../virtual-network/virtual-networks-nsg.md)
* [<span data-ttu-id="2c1dc-138">Descrição geral do Gestor de recursos do Azure para balanceadores de carga</span><span class="sxs-lookup"><span data-stu-id="2c1dc-138">Azure Resource Manager Overview for Load Balancers</span></span>](../../load-balancer/load-balancer-arm.md)

