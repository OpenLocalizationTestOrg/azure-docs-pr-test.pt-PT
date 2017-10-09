---
title: "aaaAzure CLI Script de exemplo - tooVMs de tráfego de balanceamento de carga para elevada disponibilidade | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - tooVMs de tráfego de balanceamento de carga para elevada disponibilidade"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a><span data-ttu-id="df757-103">Carregar saldo tráfego tooVMs para elevada disponibilidade</span><span class="sxs-lookup"><span data-stu-id="df757-103">Load balance traffic tooVMs for high availability</span></span>

<span data-ttu-id="df757-104">Este script de exemplo cria tudo necessário toorun várias máquinas virtuais Ubuntu configurado numa elevada disponibilidade e carga com balanceamento de configuração.</span><span class="sxs-lookup"><span data-stu-id="df757-104">This script sample creates everything needed toorun several Ubuntu virtual machines configured in a highly available and load balanced configuration.</span></span> <span data-ttu-id="df757-105">Depois de executar o script Olá, terá três máquinas virtuais, tooan associados a um conjunto de disponibilidade do Azure e é acessível através de um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="df757-105">After running hello script, you will have three virtual machines, joined tooan Azure Availability Set, and accessible through an Azure Load Balancer.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="df757-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="df757-106">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a><span data-ttu-id="df757-107">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="df757-107">Clean up deployment</span></span> 

<span data-ttu-id="df757-108">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="df757-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="df757-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="df757-109">Script explanation</span></span>

<span data-ttu-id="df757-110">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="df757-110">This script uses hello following commands toocreate a resource group, virtual machine, availability set, load balancer, and all related resources.</span></span> <span data-ttu-id="df757-111">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="df757-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="df757-112">Comando</span><span class="sxs-lookup"><span data-stu-id="df757-112">Command</span></span> | <span data-ttu-id="df757-113">Notas</span><span class="sxs-lookup"><span data-stu-id="df757-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="df757-114">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="df757-114">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="df757-115">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="df757-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="df757-116">Criar AZ rede vnet</span><span class="sxs-lookup"><span data-stu-id="df757-116">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="df757-117">Cria uma rede virtual do Azure e a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="df757-117">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="df757-118">Criar AZ público-ip da rede</span><span class="sxs-lookup"><span data-stu-id="df757-118">az network public-ip create</span></span>](https://docs.microsoft.com/cli/azure/network/public-ip#create) | <span data-ttu-id="df757-119">Cria um endereço IP público com um endereço IP estático e um nome DNS associado.</span><span class="sxs-lookup"><span data-stu-id="df757-119">Creates a public IP address with a static IP address and an associated DNS name.</span></span> |
| [<span data-ttu-id="df757-120">Criar AZ lb de rede</span><span class="sxs-lookup"><span data-stu-id="df757-120">az network lb create</span></span>](https://docs.microsoft.com/cli/azure/network/lb#create) | <span data-ttu-id="df757-121">Cria um balanceador de carga do Azure.</span><span class="sxs-lookup"><span data-stu-id="df757-121">Creates an Azure load balancer.</span></span> |
| [<span data-ttu-id="df757-122">criar a sonda de lb AZ rede</span><span class="sxs-lookup"><span data-stu-id="df757-122">az network lb probe create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | <span data-ttu-id="df757-123">Cria uma sonda do Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="df757-123">Creates a load balancer probe.</span></span> <span data-ttu-id="df757-124">Uma sonda do Balanceador de carga é utilizado toomonitor cada VM no conjunto de Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="df757-124">A load balancer probe is used toomonitor each VM in hello load balancer set.</span></span> <span data-ttu-id="df757-125">Se qualquer VM torna-se inacessível, o tráfego não é encaminhado toohello VM.</span><span class="sxs-lookup"><span data-stu-id="df757-125">If any VM becomes inaccessible, traffic is not routed toohello VM.</span></span> |
| [<span data-ttu-id="df757-126">Criar regra de lb AZ de rede</span><span class="sxs-lookup"><span data-stu-id="df757-126">az network lb rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="df757-127">Cria uma regra de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="df757-127">Creates a load balancer rule.</span></span> <span data-ttu-id="df757-128">Neste exemplo, é criada uma regra para a porta 80.</span><span class="sxs-lookup"><span data-stu-id="df757-128">In this sample, a rule is created for port 80.</span></span> <span data-ttu-id="df757-129">Como o tráfego HTTP chega ao balanceador de carga Olá, é encaminhado tooport 80 uma das VMs Olá no conjunto de Olá LB.</span><span class="sxs-lookup"><span data-stu-id="df757-129">As HTTP traffic arrives at hello load balancer, it is routed tooport 80 one of hello VMs in hello LB set.</span></span> |
| [<span data-ttu-id="df757-130">Criar AZ rede lb-nat-regras de entrada</span><span class="sxs-lookup"><span data-stu-id="df757-130">az network lb inbound-nat-rule create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | <span data-ttu-id="df757-131">Cria a regra de tradução de endereços de rede (NAT) do Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="df757-131">Creates load balancer Network Address Translation (NAT) rule.</span></span>  <span data-ttu-id="df757-132">As regras NAT de mapeiam uma porta da porta tooa de Balanceador de carga do Olá numa VM.</span><span class="sxs-lookup"><span data-stu-id="df757-132">NAT rules map a port of hello load balancer tooa port on a VM.</span></span> <span data-ttu-id="df757-133">Neste exemplo, é criada uma regra NAT para SSH tráfego tooeach VM no conjunto de Balanceador de carga Olá.</span><span class="sxs-lookup"><span data-stu-id="df757-133">In this sample, a NAT rule is created for SSH traffic tooeach VM in hello load balancer set.</span></span>  |
| [<span data-ttu-id="df757-134">Criar AZ rede nsg</span><span class="sxs-lookup"><span data-stu-id="df757-134">az network nsg create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg#create) | <span data-ttu-id="df757-135">Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre Olá internet e Olá das máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="df757-135">Creates a network security group (NSG), which is a security boundary between hello internet and hello virtual machine.</span></span> |
| [<span data-ttu-id="df757-136">criar regras de nsg AZ rede</span><span class="sxs-lookup"><span data-stu-id="df757-136">az network nsg rule create</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | <span data-ttu-id="df757-137">Cria um tooallow de regras do NSG tráfego de entrada.</span><span class="sxs-lookup"><span data-stu-id="df757-137">Creates an NSG rule tooallow inbound traffic.</span></span> <span data-ttu-id="df757-138">Neste exemplo, a porta 22 é aberta para tráfego SSH.</span><span class="sxs-lookup"><span data-stu-id="df757-138">In this sample, port 22 is opened for SSH traffic.</span></span> |
| [<span data-ttu-id="df757-139">Criar AZ nic da rede</span><span class="sxs-lookup"><span data-stu-id="df757-139">az network nic create</span></span>](https://docs.microsoft.com/cli/azure/network/nic#create) | <span data-ttu-id="df757-140">Cria uma placa de rede virtual e anexa-toohello de rede virtual, uma sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="df757-140">Creates a virtual network card and attaches it toohello virtual network, subnet, and NSG.</span></span> |
| [<span data-ttu-id="df757-141">criar a vm AZ conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="df757-141">az vm availability-set create</span></span>](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | <span data-ttu-id="df757-142">Cria um conjunto de disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="df757-142">Creates an availability set.</span></span> <span data-ttu-id="df757-143">Conjuntos de disponibilidade garantir a disponibilidade de aplicações, propagando-se máquinas de virtuais Olá em recursos físicos, de modo a que o se ocorrer uma falha, o conjunto completo de Olá não é afetado.</span><span class="sxs-lookup"><span data-stu-id="df757-143">Availability sets ensure application uptime by spreading hello virtual machines across physical resources such that if failure occurs, hello entire set is not effected.</span></span> |
| [<span data-ttu-id="df757-144">Criar AZ vm</span><span class="sxs-lookup"><span data-stu-id="df757-144">az vm create</span></span>](/cli/azure/vm#create) | <span data-ttu-id="df757-145">Cria a máquina virtual de Olá e liga toohello placa de rede, uma rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="df757-145">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="df757-146">Este comando também especifica toobe de imagem de máquina virtual de Olá utilizado e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="df757-146">This command also specifies hello virtual machine image toobe used and administrative credentials.</span></span>  |
| [<span data-ttu-id="df757-147">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="df757-147">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="df757-148">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="df757-148">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="df757-149">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="df757-149">Next steps</span></span>

<span data-ttu-id="df757-150">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="df757-150">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="df757-151">Exemplos de script a CLI de redes do Azure adicionais podem ser encontrados na Olá [redes do Azure documentação](../cli-samples.md).</span><span class="sxs-lookup"><span data-stu-id="df757-151">Additional Azure Networking CLI script samples can be found in hello [Azure Networking documentation](../cli-samples.md).</span></span>
