---
title: aaaAzure exemplo de Script do PowerShell - criar uma VM ao anexar um disco como disco de SO gerido | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - criar uma VM ao anexar um disco gerido como disco do SO
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a><span data-ttu-id="ab26a-103">Criar uma máquina virtual utilizando um disco de SO existente gerido com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ab26a-103">Create a virtual machine using an existing managed OS disk with PowerShell</span></span>

<span data-ttu-id="ab26a-104">Este script cria uma máquina virtual, anexar um disco existente gerido como disco do SO.</span><span class="sxs-lookup"><span data-stu-id="ab26a-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="ab26a-105">Utilize este script no precedente cenários:</span><span class="sxs-lookup"><span data-stu-id="ab26a-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="ab26a-106">Criar uma VM a partir de um disco de SO gerido existente que foi copiado a partir de um disco gerido numa subscrição diferente</span><span class="sxs-lookup"><span data-stu-id="ab26a-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="ab26a-107">Criar uma VM a partir de um disco gerido existente criada a partir do ficheiro VHD especializado</span><span class="sxs-lookup"><span data-stu-id="ab26a-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="ab26a-108">Criar uma VM a partir de um disco de SO gerido existente que foi criado a partir de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="ab26a-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="ab26a-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="ab26a-109">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a><span data-ttu-id="ab26a-110">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="ab26a-110">Clean up deployment</span></span> 

<span data-ttu-id="ab26a-111">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="ab26a-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="ab26a-112">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="ab26a-112">Script explanation</span></span>

<span data-ttu-id="ab26a-113">Este script utiliza Olá seguintes propriedades de disco de tooget gerido de comandos, anexar um disco gerido tooa nova VM e criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="ab26a-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="ab26a-114">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="ab26a-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="ab26a-115">Comando</span><span class="sxs-lookup"><span data-stu-id="ab26a-115">Command</span></span> | <span data-ttu-id="ab26a-116">Notas</span><span class="sxs-lookup"><span data-stu-id="ab26a-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="ab26a-117">Get-AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="ab26a-117">Get-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/Get-AzureRmDisk) | <span data-ttu-id="ab26a-118">Obtém o objeto de disco com base no nome de Olá e grupo de recursos de Olá de um disco.</span><span class="sxs-lookup"><span data-stu-id="ab26a-118">Gets disk object based on hello name and hello resource group of a disk.</span></span> <span data-ttu-id="ab26a-119">Propriedade de ID de Olá devolveu o objeto de disco é utilizado tooattach Olá disco tooa nova VM</span><span class="sxs-lookup"><span data-stu-id="ab26a-119">Id property of hello returned disk object is used tooattach hello disk tooa new VM</span></span> |
| [<span data-ttu-id="ab26a-120">Novo AzureRmVMConfig</span><span class="sxs-lookup"><span data-stu-id="ab26a-120">New-AzureRmVMConfig</span></span>](/powershell/module/azurerm.compute/new-azurermvmconfig) | <span data-ttu-id="ab26a-121">Cria uma configuração de VM.</span><span class="sxs-lookup"><span data-stu-id="ab26a-121">Creates a VM configuration.</span></span> <span data-ttu-id="ab26a-122">Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas.</span><span class="sxs-lookup"><span data-stu-id="ab26a-122">This configuration includes information such as VM name, operating system, and administrative credentials.</span></span> <span data-ttu-id="ab26a-123">configuração de Olá é utilizada durante a criação da VM.</span><span class="sxs-lookup"><span data-stu-id="ab26a-123">hello configuration is used during VM creation.</span></span> |
| [<span data-ttu-id="ab26a-124">Conjunto AzureRmVMOSDisk</span><span class="sxs-lookup"><span data-stu-id="ab26a-124">Set-AzureRmVMOSDisk</span></span>](/powershell/module/azurerm.compute/set-azurermvmosdisk) | <span data-ttu-id="ab26a-125">Anexa um disco gerido utilizando a propriedade de Id de Olá dos discos de Olá como SO disco tooa nova máquina virtual</span><span class="sxs-lookup"><span data-stu-id="ab26a-125">Attaches a managed disk using hello Id property of hello disk as OS disk tooa new virtual machine</span></span> |
| [<span data-ttu-id="ab26a-126">Novo AzureRmPublicIpAddress</span><span class="sxs-lookup"><span data-stu-id="ab26a-126">New-AzureRmPublicIpAddress</span></span>](/powershell/module/azurerm.network/new-azurermpublicipaddress) | <span data-ttu-id="ab26a-127">Cria um endereço IP público.</span><span class="sxs-lookup"><span data-stu-id="ab26a-127">Creates a public IP address.</span></span> |
| [<span data-ttu-id="ab26a-128">Novo AzureRmNetworkInterface</span><span class="sxs-lookup"><span data-stu-id="ab26a-128">New-AzureRmNetworkInterface</span></span>](/powershell/module/azurerm.network/new-azurermnetworkinterface) | <span data-ttu-id="ab26a-129">Cria uma interface de rede.</span><span class="sxs-lookup"><span data-stu-id="ab26a-129">Creates a network interface.</span></span> |
| [<span data-ttu-id="ab26a-130">Novo-AzureRmVM</span><span class="sxs-lookup"><span data-stu-id="ab26a-130">New-AzureRmVM</span></span>](/powershell/module/azurerm.compute/new-azurermvm) | <span data-ttu-id="ab26a-131">Crie uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="ab26a-131">Create a virtual machine.</span></span> |
|[<span data-ttu-id="ab26a-132">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="ab26a-132">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="ab26a-133">Remove um grupo de recursos e todos os recursos contidos.</span><span class="sxs-lookup"><span data-stu-id="ab26a-133">Removes a resource group and all resources contained within.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="ab26a-134">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="ab26a-134">Next steps</span></span>

<span data-ttu-id="ab26a-135">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="ab26a-135">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="ab26a-136">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="ab26a-136">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
