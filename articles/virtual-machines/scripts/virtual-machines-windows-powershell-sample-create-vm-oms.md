---
title: aaaAzure exemplo de Script do PowerShell - OMS | Microsoft Docs
description: Exemplo de Script do PowerShell do Azure - OMS
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
ms.date: 03/14/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: 1eeafbe743013e97bf3fcefb5ce87f72cb503a4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-operations-management-suite-monitored-vm-with-powershell"></a><span data-ttu-id="5353a-103">Criar um Operations Management Suite monitorizado VM com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5353a-103">Create an Operations Management Suite monitored VM with PowerShell</span></span>

<span data-ttu-id="5353a-104">Este script cria uma Máquina Virtual do Azure, instala o agente do Operations Management Suite (OMS) Olá e inscreve o sistema de Olá com uma área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="5353a-104">This script creates an Azure Virtual Machine, installs hello Operations Management Suite (OMS) agent, and enrolls hello system with an OMS workspace.</span></span> <span data-ttu-id="5353a-105">Assim que tiver executado o script de Olá, máquina virtual de Olá serão visível na consola do OMS Olá.</span><span class="sxs-lookup"><span data-stu-id="5353a-105">Once hello script has run, hello virtual machine will be visible in hello OMS console.</span></span> <span data-ttu-id="5353a-106">Além disso, terá de tooupdate Olá OMS área de trabalho ID e a área de trabalho chave.</span><span class="sxs-lookup"><span data-stu-id="5353a-106">Also, you need tooupdate hello OMS workspace ID and workspace key.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="5353a-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="5353a-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-monitor-oms/create-windows-vm-detailed-oms.ps1 "Create VM OMS")]

## <a name="clean-up-deployment"></a><span data-ttu-id="5353a-108">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="5353a-108">Clean up deployment</span></span> 

<span data-ttu-id="5353a-109">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="5353a-109">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="5353a-110">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="5353a-110">Script explanation</span></span>

<span data-ttu-id="5353a-111">Este script utiliza Olá após a implementação de Olá toocreate de comandos.</span><span class="sxs-lookup"><span data-stu-id="5353a-111">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="5353a-112">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="5353a-112">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="5353a-113">Comando</span><span class="sxs-lookup"><span data-stu-id="5353a-113">Command</span></span> | <span data-ttu-id="5353a-114">Notas</span><span class="sxs-lookup"><span data-stu-id="5353a-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5353a-115">Novo-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5353a-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="5353a-116">Cria um grupo de recursos na qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="5353a-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5353a-117">Novo AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5353a-117">New-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5353a-118">Cria uma configuração de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-118">Creates a subnet configuration.</span></span> <span data-ttu-id="5353a-119">Esta configuração é utilizada com o processo de criação de rede virtual Olá.</span><span class="sxs-lookup"><span data-stu-id="5353a-119">This configuration is used with hello virtual network creation process.</span></span> |
| [<span data-ttu-id="5353a-120">Novo-AzureRmVirtualNetwork</span><span class="sxs-lookup"><span data-stu-id="5353a-120">New-AzureRmVirtualNetwork</span></span>](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | <span data-ttu-id="5353a-121">Cria uma rede virtual.</span><span class="sxs-lookup"><span data-stu-id="5353a-121">Creates a virtual network.</span></span> |
| [<span data-ttu-id="5353a-122">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="5353a-122">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="5353a-123">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="5353a-123">Creates a public IP address.</span></span> |
| [<span data-ttu-id="5353a-124">Novo AzureRmNetworkSecurityRuleConfig</span><span class="sxs-lookup"><span data-stu-id="5353a-124">New-AzureRmNetworkSecurityRuleConfig</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) | <span data-ttu-id="5353a-125">Cria uma configuração de regra de grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-125">Creates a network security group rule configuration.</span></span> <span data-ttu-id="5353a-126">Esta configuração é utilizada toocreate uma regra NSG quando Olá NSG é criado.</span><span class="sxs-lookup"><span data-stu-id="5353a-126">This configuration is used toocreate an NSG rule when hello NSG is created.</span></span> |
| [<span data-ttu-id="5353a-127">Novo AzureRmNetworkSecurityGroup</span><span class="sxs-lookup"><span data-stu-id="5353a-127">New-AzureRmNetworkSecurityGroup</span></span>](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | <span data-ttu-id="5353a-128">Cria um grupo de segurança de rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-128">Creates a network security group.</span></span> |
| [<span data-ttu-id="5353a-129">Get-AzureRmVirtualNetworkSubnetConfig</span><span class="sxs-lookup"><span data-stu-id="5353a-129">Get-AzureRmVirtualNetworkSubnetConfig</span></span>](/powershell/module/azurerm.network/get-azurermvirtualnetworksubnetconfig) | <span data-ttu-id="5353a-130">Obtém as informações de sub-rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-130">Gets subnet information.</span></span> <span data-ttu-id="5353a-131">Estas informações são utilizadas durante a criação de uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-131">This information is used when creating a network interface.</span></span> |
| [<span data-ttu-id="5353a-132">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="5353a-132">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="5353a-133">Cria uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="5353a-133">Creates a network interface.</span></span> |
| [<span data-ttu-id="5353a-134">Novo AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="5353a-134">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="5353a-135">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="5353a-135">Creates a VM configuration.</span></span> <span data-ttu-id="5353a-136">Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="5353a-136">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="5353a-137">configuração de Olá é utilizada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="5353a-137">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="5353a-138">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="5353a-138">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="5353a-139">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="5353a-139">Create a virtual machine.</span></span> |
| [<span data-ttu-id="5353a-140">Conjunto AzureRmVMExtension</span><span class="sxs-lookup"><span data-stu-id="5353a-140">Set-AzureRmVMExtension</span></span>](/powershell/module/azurerm.compute/set-azurermvmextension) | <span data-ttu-id="5353a-141">Adicione uma máquina virtual de toohello de extensão VM.</span><span class="sxs-lookup"><span data-stu-id="5353a-141">Add a VM extension toohello virtual machine.</span></span> <span data-ttu-id="5353a-142">Neste caso, Olá extensão de agente do Operations Management Suite é o agente do OMS tooinstall utilizados Olá e inscrever Olá VM com uma área de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="5353a-142">In this case, hello Operations Management Suite agent extension is used tooinstall hello OMS agent and enroll hello VM in an OMS workspace.</span></span> |
|[<span data-ttu-id="5353a-143">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="5353a-143">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="5353a-144">Remove um grupo de recursos e todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="5353a-144">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5353a-145">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="5353a-145">Next steps</span></span>

<span data-ttu-id="5353a-146">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="5353a-146">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="5353a-147">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="5353a-147">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
