---
title: aaaAzure CLI Script de exemplo - criar duas VMs com um NSG interno e externo | Microsoft Docs
description: Script CLI do Azure de exemplo - criar duas VMs com NSG interno e externo
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a><span data-ttu-id="9e4b0-103">Proteger o tráfego de rede entre as máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="9e4b0-103">Secure network traffic between virtual machines</span></span>

<span data-ttu-id="9e4b0-104">Este script cria duas máquinas virtuais e protege receber tráfego tooboth.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-104">This script creates two virtual machines and secures incoming traffic tooboth.</span></span> <span data-ttu-id="9e4b0-105">Olá uma máquina virtual está acessível na internet e um grupo de segurança de rede (NSG) configurou tooallow tráfego na porta 22 e a porta 80.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-105">One virtual machine is accessible on hello internet and has a network security group (NSG) configured tooallow traffic on port 22 and port 80.</span></span> <span data-ttu-id="9e4b0-106">não está acessível na segunda de máquina virtual Olá Olá internet e tem um NSG configurado tooonly permitir o tráfego da máquina de virtual primeiro Olá.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-106">hello second virtual machine is not accessible on hello internet, and has an NSG configured tooonly allow traffic from hello first virtual machine.</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9e4b0-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9e4b0-107">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9e4b0-108">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="9e4b0-108">Clean up deployment</span></span> 

<span data-ttu-id="9e4b0-109">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9e4b0-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="9e4b0-110">Script explanation</span></span>

<span data-ttu-id="9e4b0-111">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-111">This script uses hello following commands toocreate a resource group, virtual machine, and all related resources.</span></span> <span data-ttu-id="9e4b0-112">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9e4b0-113">Comando</span><span class="sxs-lookup"><span data-stu-id="9e4b0-113">Command</span></span> | <span data-ttu-id="9e4b0-114">Notas</span><span class="sxs-lookup"><span data-stu-id="9e4b0-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9e4b0-115">Criar grupo AZ</span><span class="sxs-lookup"><span data-stu-id="9e4b0-115">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="9e4b0-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9e4b0-117">Criar AZ rede vnet</span><span class="sxs-lookup"><span data-stu-id="9e4b0-117">az network vnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet#create) | <span data-ttu-id="9e4b0-118">Cria uma rede virtual do Azure e a sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-118">Creates an Azure virtual network and subnet.</span></span> |
| [<span data-ttu-id="9e4b0-119">criar a sub-rede da vnet AZ rede</span><span class="sxs-lookup"><span data-stu-id="9e4b0-119">az network vnet subnet create</span></span>](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | <span data-ttu-id="9e4b0-120">Cria uma sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-120">Creates a subnet.</span></span> |
| [<span data-ttu-id="9e4b0-121">Criar AZ vm</span><span class="sxs-lookup"><span data-stu-id="9e4b0-121">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="9e4b0-122">Cria a máquina virtual de Olá e liga toohello placa de rede, uma rede virtual, sub-rede e NSG.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-122">Creates hello virtual machine and connects it toohello network card, virtual network, subnet, and NSG.</span></span> <span data-ttu-id="9e4b0-123">Este comando também especifica toobe de imagem de máquina virtual de Olá utilizado e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-123">This command also specifies hello virtual machine image toobe used, and administrative credentials.</span></span>  |
| [<span data-ttu-id="9e4b0-124">lista de regras de nsg de rede AZ</span><span class="sxs-lookup"><span data-stu-id="9e4b0-124">az network nsg rule list</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | <span data-ttu-id="9e4b0-125">Devolve informações sobre uma regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-125">Returns information about a network security group rule.</span></span> <span data-ttu-id="9e4b0-126">Neste exemplo, o nome da regra Olá é armazenado numa variável para utilização posterior num script Olá.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-126">In this sample, hello rule name is stored in a variable for use later in hello script.</span></span> |
| [<span data-ttu-id="9e4b0-127">actualização da regra AZ rede nsg</span><span class="sxs-lookup"><span data-stu-id="9e4b0-127">az network nsg rule update</span></span>](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | <span data-ttu-id="9e4b0-128">Atualiza uma regra NSG.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-128">Updates an NSG rule.</span></span> <span data-ttu-id="9e4b0-129">Neste exemplo, a regra de back-end de Olá é toopass atualizado através de tráfego apenas a partir da sub-rede Olá de front-end.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-129">In this sample, hello back-end rule is updated toopass through traffic only from hello front-end subnet.</span></span> |
| [<span data-ttu-id="9e4b0-130">eliminação do grupo de AZ</span><span class="sxs-lookup"><span data-stu-id="9e4b0-130">az group delete</span></span>](https://docs.microsoft.com/cli/azure/vm/extension#set) | <span data-ttu-id="9e4b0-131">Elimina um grupo de recursos, incluindo todos os recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="9e4b0-131">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9e4b0-132">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9e4b0-132">Next steps</span></span>

<span data-ttu-id="9e4b0-133">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9e4b0-133">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="9e4b0-134">Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9e4b0-134">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
