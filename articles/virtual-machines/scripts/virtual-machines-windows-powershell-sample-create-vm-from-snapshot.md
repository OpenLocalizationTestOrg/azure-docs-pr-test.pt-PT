---
title: "aaaAzure exemplo de Script do PowerShell - criar uma VM a partir de um instantâneo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar uma VM a partir de um instantâneo"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a><span data-ttu-id="7c0a9-103">Criar uma máquina virtual a partir de um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="7c0a9-103">Create a virtual machine from a snapshot with PowerShell</span></span>

<span data-ttu-id="7c0a9-104">Este script cria uma máquina virtual a partir de um instantâneo de um disco de SO.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-104">This script creates a virtual machine from a snapshot of an OS disk.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="7c0a9-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="7c0a9-105">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="7c0a9-106">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="7c0a9-106">Clean up deployment</span></span> 

<span data-ttu-id="7c0a9-107">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-107">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="7c0a9-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="7c0a9-108">Script explanation</span></span>

<span data-ttu-id="7c0a9-109">Este script utiliza Olá os seguintes comandos tooget propriedades de instantâneo, criar um disco gerido a partir do instantâneo e criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-109">This script uses hello following commands tooget snapshot properties, create a managed disk from snapshot and create a VM.</span></span> <span data-ttu-id="7c0a9-110">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="7c0a9-111">Comando</span><span class="sxs-lookup"><span data-stu-id="7c0a9-111">Command</span></span> | <span data-ttu-id="7c0a9-112">Notas</span><span class="sxs-lookup"><span data-stu-id="7c0a9-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="7c0a9-113">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="7c0a9-113">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/get-azurermsnapshot) | <span data-ttu-id="7c0a9-114">Obtém um instantâneo com o nome do instantâneo.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-114">Gets a snapshot using snapshot name.</span></span> |
| [<span data-ttu-id="7c0a9-115">Novo AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="7c0a9-115">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/new-azurermdiskconfig) | <span data-ttu-id="7c0a9-116">Cria uma configuração de disco.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-116">Creates a disk configuration.</span></span> <span data-ttu-id="7c0a9-117">Esta configuração é utilizada com o processo de criação do disco Olá.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-117">This configuration is used with hello disk creation process.</span></span> |
| [<span data-ttu-id="7c0a9-118">Novo AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="7c0a9-118">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/new-azurermdisk) | <span data-ttu-id="7c0a9-119">Cria um disco gerido.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-119">Creates a managed disk.</span></span> |
| [<span data-ttu-id="7c0a9-120">Novo AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="7c0a9-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="7c0a9-121">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-121">Creates a VM configuration.</span></span> <span data-ttu-id="7c0a9-122">Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="7c0a9-123">configuração de Olá é utilizada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="7c0a9-124">Conjunto AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="7c0a9-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="7c0a9-125">Anexa o disco Olá de gerido como disco de SO toohello máquina de virtual</span><span class="sxs-lookup"><span data-stu-id="7c0a9-125">Attaches hello managed disk as OS disk toohello virtual machine</span></span> |
| [<span data-ttu-id="7c0a9-126">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="7c0a9-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="7c0a9-127">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="7c0a9-128">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="7c0a9-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="7c0a9-129">Cria uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="7c0a9-130">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="7c0a9-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="7c0a9-131">Cria uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-131">Creates a virtual machine.</span></span> |
|[<span data-ttu-id="7c0a9-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="7c0a9-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="7c0a9-133">Remove um grupo de recursos e todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="7c0a9-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="7c0a9-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="7c0a9-134">Next steps</span></span>

<span data-ttu-id="7c0a9-135">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="7c0a9-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="7c0a9-136">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="7c0a9-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
