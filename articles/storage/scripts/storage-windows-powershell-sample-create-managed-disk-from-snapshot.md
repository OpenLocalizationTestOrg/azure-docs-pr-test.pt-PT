---
title: "aaaAzure exemplo de Script do PowerShell - criar um disco gerido a partir de um instantâneo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um disco gerido a partir de um instantâneo"
services: virtual-machines-windows
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 06/05/2017
ms.author: ramankum
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a><span data-ttu-id="fb221-103">Criar um disco gerido a partir de um instantâneo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="fb221-103">Create a managed disk from a snapshot with PowerShell</span></span>

<span data-ttu-id="fb221-104">Este script cria um disco gerido a partir de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="fb221-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="fb221-105">Utilizá-lo toorestore uma máquina virtual de instantâneos de discos de dados e SO.</span><span class="sxs-lookup"><span data-stu-id="fb221-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="fb221-106">Crie o SO e discos geridos dos respetivos instantâneos de dados e, em seguida, criar uma nova máquina virtual ligando discos geridos.</span><span class="sxs-lookup"><span data-stu-id="fb221-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="fb221-107">Também pode restaurar os discos de dados de uma VM existente ao anexar a criação de instantâneos de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="fb221-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fb221-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="fb221-108">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="fb221-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="fb221-109">Script explanation</span></span>

<span data-ttu-id="fb221-110">Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="fb221-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="fb221-111">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="fb221-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fb221-112">Comando</span><span class="sxs-lookup"><span data-stu-id="fb221-112">Command</span></span> | <span data-ttu-id="fb221-113">Notas</span><span class="sxs-lookup"><span data-stu-id="fb221-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fb221-114">Get-AzureRmSnapshot</span><span class="sxs-lookup"><span data-stu-id="fb221-114">Get-AzureRmSnapshot</span></span>](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | <span data-ttu-id="fb221-115">Obtém as propriedades de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="fb221-115">Gets snapshot properties.</span></span>  |
| [<span data-ttu-id="fb221-116">Novo AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="fb221-116">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="fb221-117">Cria a configuração de disco que é utilizada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="fb221-117">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="fb221-118">Inclui Olá Id do recurso de instantâneo de principal de Olá, localização que seja igual à localização de Olá do tipo de armazenamento de instantâneos e Olá principal.</span><span class="sxs-lookup"><span data-stu-id="fb221-118">It includes hello resource Id of hello parent snapshot, location that is same as hello location of parent snapshot and hello storage type.</span></span>  |
| [<span data-ttu-id="fb221-119">Novo AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="fb221-119">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="fb221-120">Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="fb221-120">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="fb221-121">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fb221-121">Next steps</span></span>

[<span data-ttu-id="fb221-122">Criar uma máquina virtual a partir de um disco gerido</span><span class="sxs-lookup"><span data-stu-id="fb221-122">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="fb221-123">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fb221-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="fb221-124">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fb221-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
