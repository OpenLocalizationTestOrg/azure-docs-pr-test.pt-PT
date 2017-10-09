---
title: aaaAzure exemplo de Script do PowerShell - WordPress | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - WordPress
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: b011726a772bb4d13fcfcba088eac4d0305967c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-wordpress-vm-with-powershell"></a><span data-ttu-id="9d0ca-103">Criar uma VM WordPress com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="9d0ca-103">Create a WordPress VM with PowerShell</span></span>

<span data-ttu-id="9d0ca-104">Este script cria uma máquina virtual e utiliza o tooinstall de extensão de script personalizado do Olá Máquina Virtual do Azure WordPress.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-104">This script creates a virtual machine and uses hello Azure Virtual Machine custom script extension tooinstall WordPress.</span></span> <span data-ttu-id="9d0ca-105">Depois de script de Olá em execução, pode aceder ao site do configuration WordPress Olá em `http://<public IP of VM>/wordpress`.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-105">After running hello script, you can access hello WordPress configuration site at  `http://<public IP of VM>/wordpress`.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="9d0ca-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="9d0ca-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-wordpress-mysql/create-wordpress-mysql.ps1 "Create VM WordPress")]

## <a name="clean-up-deployment"></a><span data-ttu-id="9d0ca-107">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="9d0ca-107">Clean up deployment</span></span> 

<span data-ttu-id="9d0ca-108">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="9d0ca-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="9d0ca-109">Script explanation</span></span>

<span data-ttu-id="9d0ca-110">Este script utiliza Olá após a implementação de Olá toocreate de comandos.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="9d0ca-111">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="9d0ca-112">Comando</span><span class="sxs-lookup"><span data-stu-id="9d0ca-112">Command</span></span> | <span data-ttu-id="9d0ca-113">Notas</span><span class="sxs-lookup"><span data-stu-id="9d0ca-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="9d0ca-114">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9d0ca-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="9d0ca-115">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="9d0ca-116">Novo AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9d0ca-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9d0ca-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-117">Creates a subnet configuration.</span></span> <span data-ttu-id="9d0ca-118">Esta configuração é utilizada com o processo de criação de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="9d0ca-119">Novo-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="9d0ca-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="9d0ca-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="9d0ca-121">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="9d0ca-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="9d0ca-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="9d0ca-123">Novo AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="9d0ca-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="9d0ca-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="9d0ca-125">Esta configuração é utilizada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="9d0ca-126">Novo AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="9d0ca-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="9d0ca-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="9d0ca-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="9d0ca-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="9d0ca-129">Obtém as informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-129">Gets subnet information.</span></span> <span data-ttu-id="9d0ca-130">Estas informações são utilizadas durante a criação de uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="9d0ca-131">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="9d0ca-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="9d0ca-132">Cria uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="9d0ca-133">Novo AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="9d0ca-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="9d0ca-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-134">Creates a VM configuration.</span></span> <span data-ttu-id="9d0ca-135">Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="9d0ca-136">configuração de Olá é utilizada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="9d0ca-137">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="9d0ca-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="9d0ca-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="9d0ca-139">Conjunto AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="9d0ca-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="9d0ca-140">Adicione a máquina virtual do Olá extensão de Script personalizado toohello, que invoca uma tooinstall script WordPress.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-140">Add hello Custom Script Extension toohello virtual machine, which invokes a script tooinstall WordPress.</span></span> |
|[<span data-ttu-id="9d0ca-141">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="9d0ca-141">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="9d0ca-142">Remove um grupo de recursos e todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="9d0ca-142">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="9d0ca-143">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="9d0ca-143">Next steps</span></span>

<span data-ttu-id="9d0ca-144">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="9d0ca-144">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="9d0ca-145">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="9d0ca-145">Additional virtual machine PowerShell script samples can be found in hello [Azure Linux VM documentation](../linux/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
