---
title: "aaaAzure exemplo de script do PowerShell - criar uma rede para aplicações de várias camadas | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar uma rede virtual para aplicações de várias camadas."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a><span data-ttu-id="01832-103">Criar uma rede para aplicações de várias camadas</span><span class="sxs-lookup"><span data-stu-id="01832-103">Create a network for multi-tier applications</span></span>

<span data-ttu-id="01832-104">Este script de exemplo cria uma rede virtual com as sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="01832-104">This script sample creates a virtual network with front-end and back-end subnets.</span></span> <span data-ttu-id="01832-105">Sub-rede de front-end do tráfego toohello tooHTTP limitado e SSH, ao tráfego toohello sub-rede de back-end é limitado tooMySQL, porta 3306.</span><span class="sxs-lookup"><span data-stu-id="01832-105">Traffic toohello front-end subnet is limited tooHTTP and SSH, while traffic toohello back-end subnet is limited tooMySQL, port 3306.</span></span> <span data-ttu-id="01832-106">Depois de executar o script Olá tem duas máquinas virtuais, um em cada sub-rede que pode implementar MySQL software e do servidor web.</span><span class="sxs-lookup"><span data-stu-id="01832-106">After running hello script, you will have two virtual machines, one in each subnet that you can deploy web server and MySQL software to.</span></span>

<span data-ttu-id="01832-107">Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure.</span><span class="sxs-lookup"><span data-stu-id="01832-107">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="01832-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="01832-108">Sample script</span></span>


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a><span data-ttu-id="01832-109">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="01832-109">Clean up deployment</span></span> 

<span data-ttu-id="01832-110">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="01832-110">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="01832-111">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="01832-111">Script explanation</span></span>

<span data-ttu-id="01832-112">Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, rede virtual e os grupos de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="01832-112">This script uses hello following commands toocreate a resource group, virtual network,  and network security groups.</span></span> <span data-ttu-id="01832-113">Cada comando na documentação do Olá tabela ligações toocommand específicos.</span><span class="sxs-lookup"><span data-stu-id="01832-113">Each command in hello table links toocommand-specific documentation.</span></span>

| <span data-ttu-id="01832-114">Comando</span><span class="sxs-lookup"><span data-stu-id="01832-114">Command</span></span> | <span data-ttu-id="01832-115">Notas</span><span class="sxs-lookup"><span data-stu-id="01832-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="01832-116">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01832-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="01832-117">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="01832-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="01832-118">Novo-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="01832-118">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="01832-119">Cria uma rede virtual do Azure e a sub-rede do front-end.</span><span class="sxs-lookup"><span data-stu-id="01832-119">Creates an Azure virtual network and front-end subnet.</span></span> |
| [<span data-ttu-id="01832-120">Novo AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="01832-120">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="01832-121">Cria uma sub-rede de back-end.</span><span class="sxs-lookup"><span data-stu-id="01832-121">Creates a back-end subnet.</span></span> |
| [<span data-ttu-id="01832-122">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="01832-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="01832-123">Cria um Olá de tooaccess de endereço IP público VM a partir de Olá Internet.</span><span class="sxs-lookup"><span data-stu-id="01832-123">Creates a public IP address tooaccess hello VM from hello Internet.</span></span> |
| [<span data-ttu-id="01832-124">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="01832-124">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="01832-125">Cria interfaces de rede virtual e anexa-las a sub-redes da rede virtual toohello de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="01832-125">Creates virtual network interfaces and attaches them toohello virtual network's front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="01832-126">Novo AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="01832-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="01832-127">Cria grupos de segurança de rede (NSG) que são toohello associados a sub-redes de front-end e back-end.</span><span class="sxs-lookup"><span data-stu-id="01832-127">Creates network security groups (NSG) that are associated toohello front-end and back-end subnets.</span></span> |
| [<span data-ttu-id="01832-128">Novo AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="01832-128">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |<span data-ttu-id="01832-129">Cria regras do NSG que permitem ou bloquear sub-redes de toospecific portas específicas.</span><span class="sxs-lookup"><span data-stu-id="01832-129">Creates NSG rules that allow or block specific ports toospecific subnets.</span></span> |
| [<span data-ttu-id="01832-130">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="01832-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="01832-131">Cria máquinas virtuais e anexa um tooeach NIC VM.</span><span class="sxs-lookup"><span data-stu-id="01832-131">Creates virtual machines and attaches a NIC tooeach VM.</span></span> <span data-ttu-id="01832-132">Este comando também especifica toouse de imagem de máquina virtual de Olá e credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="01832-132">This command also specifies hello virtual machine image toouse and administrative credentials.</span></span> |
| [<span data-ttu-id="01832-133">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="01832-133">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="01832-134">Elimina um grupo de recursos e todos os recursos que nele contidos.</span><span class="sxs-lookup"><span data-stu-id="01832-134">Deletes a resource group and all resources it contains.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="01832-135">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="01832-135">Next steps</span></span>

<span data-ttu-id="01832-136">Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="01832-136">For more information on hello Azure PowerShell, see [Azure PowerShell documentation](https://docs.microsoft.com/powershell/azure/overview).</span></span>

<span data-ttu-id="01832-137">Exemplos de script do PowerShell redes adicionais podem ser encontrados na Olá [documentação de descrição geral de funcionamento em rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="01832-137">Additional networking PowerShell script samples can be found in hello [Azure Networking Overview documentation](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).</span></span>
