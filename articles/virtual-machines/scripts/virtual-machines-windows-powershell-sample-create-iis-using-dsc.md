---
title: aaaAzure exemplo de Script do PowerShell - IIS com DSC | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - IIS com o DSC
services: virtual-machines-windows
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 03/01/2017
ms.author: nepeters
ms.openlocfilehash: ef855bf92ef7b0fd07466527bc5f71f688e150fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-iis-vm-with-powershell"></a><span data-ttu-id="96ee9-103">Criar uma VM do IIS com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="96ee9-103">Create an IIS VM with PowerShell</span></span>

<span data-ttu-id="96ee9-104">Este script cria uma máquina de Virtual do Azure a executar o Windows Server 2016 e, em seguida, utiliza a extensão de DSC na máquina Virtual do Azure de Olá tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="96ee9-104">This script creates an Azure Virtual Machine running Windows Server 2016, and then uses hello Azure Virtual Machine DSC Extension tooinstall IIS.</span></span> <span data-ttu-id="96ee9-105">Depois de executar o script de Olá, pode aceder a Olá site predefinido do IIS no endereço IP público Olá da máquina virtual de Olá.</span><span class="sxs-lookup"><span data-stu-id="96ee9-105">After running hello script, you can access hello default IIS website on hello public IP address of hello virtual machine.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="96ee9-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="96ee9-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-dsc/create-windows-vm-iis-dsc.ps1 "Create VM IIS DSC")]

## <a name="clean-up-deployment"></a><span data-ttu-id="96ee9-107">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="96ee9-107">Clean up deployment</span></span> 

<span data-ttu-id="96ee9-108">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="96ee9-108">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="96ee9-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="96ee9-109">Script explanation</span></span>

<span data-ttu-id="96ee9-110">Este script utiliza Olá após a implementação de Olá toocreate de comandos.</span><span class="sxs-lookup"><span data-stu-id="96ee9-110">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="96ee9-111">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="96ee9-111">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="96ee9-112">Comando</span><span class="sxs-lookup"><span data-stu-id="96ee9-112">Command</span></span> | <span data-ttu-id="96ee9-113">Notas</span><span class="sxs-lookup"><span data-stu-id="96ee9-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="96ee9-114">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="96ee9-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="96ee9-115">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="96ee9-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="96ee9-116">Novo AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="96ee9-116">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="96ee9-117">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-117">Creates a subnet configuration.</span></span> <span data-ttu-id="96ee9-118">Esta configuração é utilizada com o processo de criação de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="96ee9-118">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="96ee9-119">Novo-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="96ee9-119">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="96ee9-120">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="96ee9-120">Creates a virtual network.</span></span> |
| [<span data-ttu-id="96ee9-121">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="96ee9-121">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="96ee9-122">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="96ee9-122">Creates a public IP address.</span></span> |
| [<span data-ttu-id="96ee9-123">Novo AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="96ee9-123">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="96ee9-124">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-124">Creates a network security group rule configuration.</span></span> <span data-ttu-id="96ee9-125">Esta configuração é utilizada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="96ee9-125">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="96ee9-126">Novo AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="96ee9-126">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="96ee9-127">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-127">Creates a network security group.</span></span> |
| [<span data-ttu-id="96ee9-128">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="96ee9-128">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="96ee9-129">Obtém as informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-129">Gets subnet information.</span></span> <span data-ttu-id="96ee9-130">Estas informações são utilizadas durante a criação de uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-130">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="96ee9-131">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="96ee9-131">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="96ee9-132">Cria uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="96ee9-132">Creates a network interface.</span></span> |
| [<span data-ttu-id="96ee9-133">Novo AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="96ee9-133">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="96ee9-134">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="96ee9-134">Creates a VM configuration.</span></span> <span data-ttu-id="96ee9-135">Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="96ee9-135">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="96ee9-136">configuração de Olá é utilizada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="96ee9-136">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="96ee9-137">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="96ee9-137">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="96ee9-138">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="96ee9-138">Create a virtual machine.</span></span> |
| [<span data-ttu-id="96ee9-139">Conjunto AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="96ee9-139">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="96ee9-140">Adicione uma máquina virtual de toohello de extensão VM.</span><span class="sxs-lookup"><span data-stu-id="96ee9-140">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="96ee9-141">Neste exemplo, a extensão de script personalizado Olá é utilizado tooinstall IIS.</span><span class="sxs-lookup"><span data-stu-id="96ee9-141">In this sample, hello custom script extension is used tooinstall IIS.</span></span> |
|[<span data-ttu-id="96ee9-142">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="96ee9-142">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="96ee9-143">Remove um grupo de recursos e todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="96ee9-143">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="96ee9-144">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="96ee9-144">Next steps</span></span>

<span data-ttu-id="96ee9-145">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="96ee9-145">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="96ee9-146">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="96ee9-146">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
