---
title: aaaDeploy VMs do Linux na rede existente com a CLI do Azure 1.0 | Microsoft Docs
description: "Como toodeploy uma VM com Linux para uma rede Virtual existente utilizando Olá CLI do Azure 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a><span data-ttu-id="9a02c-103">Como toodeploy uma máquina virtual do Linux para uma rede Virtual do Azure existente com Olá CLI do Azure 1.0</span><span class="sxs-lookup"><span data-stu-id="9a02c-103">How toodeploy a Linux virtual machine into an existing Azure Virtual Network with hello Azure CLI 1.0</span></span>

<span data-ttu-id="9a02c-104">Este artigo mostra como toouse CLI do Azure 1.0 toodeploy uma máquina virtual (VM) numa rede Virtual existente (VNet).</span><span class="sxs-lookup"><span data-stu-id="9a02c-104">This article shows you how toouse Azure CLI 1.0 toodeploy a virtual machine (VM) into an existing Virtual Network (VNet).</span></span> <span data-ttu-id="9a02c-105">requisitos de Olá são:</span><span class="sxs-lookup"><span data-stu-id="9a02c-105">hello requirements are:</span></span>

- [<span data-ttu-id="9a02c-106">uma conta do Azure</span><span class="sxs-lookup"><span data-stu-id="9a02c-106">an Azure account</span></span>](https://azure.microsoft.com/pricing/free-trial/)
- [<span data-ttu-id="9a02c-107">Ficheiros de chaves públicas e privadas SSH</span><span class="sxs-lookup"><span data-stu-id="9a02c-107">SSH public and private key files</span></span>](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a><span data-ttu-id="9a02c-108">Tarefas do CLI versões toocomplete Olá</span><span class="sxs-lookup"><span data-stu-id="9a02c-108">CLI versions toocomplete hello task</span></span>
<span data-ttu-id="9a02c-109">Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:</span><span class="sxs-lookup"><span data-stu-id="9a02c-109">You can complete hello task using one of hello following CLI versions:</span></span>

- <span data-ttu-id="9a02c-110">[Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)</span><span class="sxs-lookup"><span data-stu-id="9a02c-110">[Azure CLI 1.0](#quick-commands) – our CLI for hello classic and resource management deployment models (this article)</span></span>
- <span data-ttu-id="9a02c-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="9a02c-111">[Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) - our next generation CLI for hello resource management deployment model</span></span>


## <a name="quick-commands"></a><span data-ttu-id="9a02c-112">Comandos Rápidos</span><span class="sxs-lookup"><span data-stu-id="9a02c-112">Quick Commands</span></span>

<span data-ttu-id="9a02c-113">Se precisar de tooquickly realizar tarefas Olá, Olá seguinte secção fornece detalhes sobre os comandos de Olá necessários.</span><span class="sxs-lookup"><span data-stu-id="9a02c-113">If you need tooquickly accomplish hello task, hello following section details hello commands needed.</span></span> <span data-ttu-id="9a02c-114">Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="9a02c-114">More detailed information and context for each step can be found hello rest of hello document, [starting here](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).</span></span>

<span data-ttu-id="9a02c-115">Pré-requisitos: Grupo de recursos, VNet, NSG com SSH de entrada, sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9a02c-115">Pre-requirements: Resource Group, VNet, NSG with SSH inbound, Subnet.</span></span> <span data-ttu-id="9a02c-116">Substitua qualquer exemplos as suas próprias definições.</span><span class="sxs-lookup"><span data-stu-id="9a02c-116">Replace any examples with your own settings.</span></span>

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a><span data-ttu-id="9a02c-117">Implementar Olá VM numa infraestrutura de rede virtual Olá</span><span class="sxs-lookup"><span data-stu-id="9a02c-117">Deploy hello VM into hello virtual network infrastructure</span></span>

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a><span data-ttu-id="9a02c-118">Instruções detalhadas</span><span class="sxs-lookup"><span data-stu-id="9a02c-118">Detailed walkthrough</span></span>

<span data-ttu-id="9a02c-119">Recursos do Azure como Olá VNets e grupos de segurança de rede devem ser estáticos e tempo lived recursos que raramente são implementados.</span><span class="sxs-lookup"><span data-stu-id="9a02c-119">Azure assets like hello VNets and network security groups should be static and long lived resources that are rarely deployed.</span></span> <span data-ttu-id="9a02c-120">Assim que tiver sido implementada uma VNet, pode ser reutilizada por novas implementações sem qualquer infraestrutura de toohello afeta adversos.</span><span class="sxs-lookup"><span data-stu-id="9a02c-120">Once a VNet has been deployed, it can be reused by new deployments without any adverse affects toohello infrastructure.</span></span> <span data-ttu-id="9a02c-121">Pensa sobre uma VNet como sendo um comutador de rede de hardware tradicional.</span><span class="sxs-lookup"><span data-stu-id="9a02c-121">Think about a VNet as being a traditional hardware network switch.</span></span> <span data-ttu-id="9a02c-122">Não terá tooconfigure um novo hardware mudar com cada implementação.</span><span class="sxs-lookup"><span data-stu-id="9a02c-122">You would not need tooconfigure a brand new hardware switch with each deployment.</span></span> <span data-ttu-id="9a02c-123">Com uma VNet configurada corretamente, pode prosseguir toodeploy novos servidores para essa VNet mais e mais alguns, se existirem, as alterações necessárias ao longo da vida Olá de Olá VNet.</span><span class="sxs-lookup"><span data-stu-id="9a02c-123">With a correctly configured VNet, you can continue toodeploy new servers into that VNet over and over with few, if any, changes required over hello life of hello VNet.</span></span>

## <a name="create-hello-resource-group"></a><span data-ttu-id="9a02c-124">Criar grupo de recursos de Olá</span><span class="sxs-lookup"><span data-stu-id="9a02c-124">Create hello resource group</span></span>

<span data-ttu-id="9a02c-125">Em primeiro lugar, crie um tooorganize do grupo de recursos tudo que criar esta explicação passo a passo.</span><span class="sxs-lookup"><span data-stu-id="9a02c-125">First, create a resource group tooorganize everything you create in this walkthrough.</span></span> <span data-ttu-id="9a02c-126">Para obter mais informações sobre grupos de recursos, consulte [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)</span><span class="sxs-lookup"><span data-stu-id="9a02c-126">For more information about resource groups, see [Azure Resource Manager overview](../../azure-resource-manager/resource-group-overview.md)</span></span>

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a><span data-ttu-id="9a02c-127">Criar Olá VNet</span><span class="sxs-lookup"><span data-stu-id="9a02c-127">Create hello VNet</span></span>

<span data-ttu-id="9a02c-128">Step-by-Olá primeiro passo é toobuild toolaunch uma VNet Olá VMs no.</span><span class="sxs-lookup"><span data-stu-id="9a02c-128">hello first step is toobuild a VNet toolaunch hello VMs into.</span></span> <span data-ttu-id="9a02c-129">Olá VNet contém uma sub-rede para esta instrução.</span><span class="sxs-lookup"><span data-stu-id="9a02c-129">hello VNet contains one subnet for this walkthrough.</span></span> <span data-ttu-id="9a02c-130">Para obter mais informações sobre as VNets do Azure, consulte [criar uma rede virtual, utilizando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9a02c-130">For more information on Azure VNets, see [Create a virtual network by using hello Azure CLI](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)</span></span>

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a><span data-ttu-id="9a02c-131">Criar grupo de segurança de rede Olá</span><span class="sxs-lookup"><span data-stu-id="9a02c-131">Create hello network security group</span></span>

<span data-ttu-id="9a02c-132">a sub-rede de Olá baseia-se por trás de um grupo de segurança de rede existente para criar o grupo de segurança de rede Olá antes de sub-rede Olá.</span><span class="sxs-lookup"><span data-stu-id="9a02c-132">hello subnet is built behind an existing network security group so build hello network security group before hello subnet.</span></span> <span data-ttu-id="9a02c-133">Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="9a02c-133">Azure network security groups are equivalent tooa firewall at hello network layer.</span></span> <span data-ttu-id="9a02c-134">Para obter mais informações sobre grupos de segurança de rede do Azure, consulte [como de grupos de segurança de rede toocreate Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span><span class="sxs-lookup"><span data-stu-id="9a02c-134">For more information on Azure network security groups, see [How toocreate network security groups in hello Azure CLI](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)</span></span>

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a><span data-ttu-id="9a02c-135">Adicionar regra de permissão de um SSH de entrada</span><span class="sxs-lookup"><span data-stu-id="9a02c-135">Add an inbound SSH allow rule</span></span>

<span data-ttu-id="9a02c-136">Olá VM tem acesso a partir de Olá internet, para que uma regra que permite a porta de entrada 22 tráfego toobe transmitido através da rede de Olá tooport 22 Olá VM é necessária.</span><span class="sxs-lookup"><span data-stu-id="9a02c-136">hello VM needs access from hello internet so a rule allowing inbound port 22 traffic toobe passed through hello network tooport 22 on hello VM is needed.</span></span>

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a><span data-ttu-id="9a02c-137">Adicionar uma sub-rede toohello VNet</span><span class="sxs-lookup"><span data-stu-id="9a02c-137">Add a subnet toohello VNet</span></span>

<span data-ttu-id="9a02c-138">VMs dentro Olá VNet tem de estar localizadas numa sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9a02c-138">VMs within hello VNet must be located in a subnet.</span></span> <span data-ttu-id="9a02c-139">Cada VNet pode ter várias sub-redes.</span><span class="sxs-lookup"><span data-stu-id="9a02c-139">Each VNet can have multiple subnets.</span></span> <span data-ttu-id="9a02c-140">Criar a sub-rede de Olá e associar grupo de segurança de rede Olá.</span><span class="sxs-lookup"><span data-stu-id="9a02c-140">Create hello subnet and associate with hello network security group.</span></span>

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

<span data-ttu-id="9a02c-141">Olá sub-rede agora é adicionado no interior Olá VNet e associada ao grupo de segurança de rede Olá e regra.</span><span class="sxs-lookup"><span data-stu-id="9a02c-141">hello Subnet is now added inside hello VNet and associated with hello network security group and rule.</span></span>


## <a name="add-a-vnic-toohello-subnet"></a><span data-ttu-id="9a02c-142">Adicionar uma sub-rede de toohello VNic</span><span class="sxs-lookup"><span data-stu-id="9a02c-142">Add a VNic toohello subnet</span></span>

<span data-ttu-id="9a02c-143">Placas de rede virtuais (VNics) são importantes, como pode reutilize-as ao ligá-las toodifferent VMs.</span><span class="sxs-lookup"><span data-stu-id="9a02c-143">Virtual network cards (VNics) are important as you can reuse them by connecting them toodifferent VMs.</span></span> <span data-ttu-id="9a02c-144">Esta abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário.</span><span class="sxs-lookup"><span data-stu-id="9a02c-144">This approach keeps hello VNic as a static resource while hello VMs can be temporary.</span></span> <span data-ttu-id="9a02c-145">Criar um VNic e associá-la a sub-rede de Olá criada no passo anterior Olá.</span><span class="sxs-lookup"><span data-stu-id="9a02c-145">Create a VNic and associate it with hello subnet created in hello previous step.</span></span>

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a><span data-ttu-id="9a02c-146">Implementar Olá VM em Olá VNet e o NSG</span><span class="sxs-lookup"><span data-stu-id="9a02c-146">Deploy hello VM into hello VNet and NSG</span></span>

<span data-ttu-id="9a02c-147">Tem agora uma VNet e sub-rede dentro desse VNet e um grupo de segurança de rede que atuam sub-rede de Olá tooprotect ao bloquear todo o tráfego de entrada, exceto a porta 22 para SSH.</span><span class="sxs-lookup"><span data-stu-id="9a02c-147">You now have a VNet and subnet inside that VNet, and a network security group acting tooprotect hello subnet by blocking all inbound traffic except port 22 for SSH.</span></span> <span data-ttu-id="9a02c-148">Agora pode ser implementado Olá VM dentro esta infraestrutura de rede existente.</span><span class="sxs-lookup"><span data-stu-id="9a02c-148">hello VM can now be deployed inside this existing network infrastructure.</span></span>

<span data-ttu-id="9a02c-149">Utilizar Olá CLI do Azure e Olá `azure vm create` comando, Olá VM com Linux é implementado toohello existente grupo de recursos do Azure, uma VNet, sub-rede e VNic.</span><span class="sxs-lookup"><span data-stu-id="9a02c-149">Using hello Azure CLI, and hello `azure vm create` command, hello Linux VM is deployed toohello existing Azure Resource Group, VNet, Subnet, and VNic.</span></span> <span data-ttu-id="9a02c-150">Para obter mais informações sobre como utilizar Olá CLI toodeploy uma VM completa, consulte [criar um ambiente de Linux completado utilizando Olá CLI do Azure](create-cli-complete.md)</span><span class="sxs-lookup"><span data-stu-id="9a02c-150">For more information on using hello CLI toodeploy a complete VM, see [Create a complete Linux environment by using hello Azure CLI](create-cli-complete.md)</span></span>

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

<span data-ttu-id="9a02c-151">Ao utilizar Olá CLI sinalizadores toocall horizontalmente recursos existentes, instruir VM do Azure toodeploy Olá dentro da rede existente Olá.</span><span class="sxs-lookup"><span data-stu-id="9a02c-151">By using hello CLI flags toocall out existing resources, you instruct Azure toodeploy hello VM inside hello existing network.</span></span> <span data-ttu-id="9a02c-152">Depois de tem sido implementados uma VNet e sub-rede, pode ser deixados como estáticos ou permanentes recursos dentro da região do Azure.</span><span class="sxs-lookup"><span data-stu-id="9a02c-152">Once a VNet and subnet have been deployed, they can be left as static or permanent resources inside your Azure region.</span></span>  

## <a name="next-steps"></a><span data-ttu-id="9a02c-153">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9a02c-153">Next steps</span></span>

* [<span data-ttu-id="9a02c-154">Utilize um toocreate de modelo do Azure Resource Manager uma implementação específica</span><span class="sxs-lookup"><span data-stu-id="9a02c-154">Use an Azure Resource Manager template toocreate a specific deployment</span></span>](../windows/cli-deploy-templates.md)
* [<span data-ttu-id="9a02c-155">Criar um ambiente personalizado para uma VM com Linux diretamente através dos comandos da CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="9a02c-155">Create your own custom environment for a Linux VM using Azure CLI commands directly</span></span>](create-cli-complete.md)
* [<span data-ttu-id="9a02c-156">Criar uma VM com Linux no Azure utilizando modelos</span><span class="sxs-lookup"><span data-stu-id="9a02c-156">Create a Linux VM on Azure using templates</span></span>](create-ssh-secured-vm-from-template.md)
