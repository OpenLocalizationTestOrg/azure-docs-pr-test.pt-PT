---
title: "aaaAzure exemplo de Script do PowerShell - criar um instantâneo de um VHD toocreate vários discos geridos idênticos num pequeno período de tempo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um instantâneo de um VHD toocreate vários discos geridos idênticos num pequeno período de tempo"
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
ms.openlocfilehash: 5f11793b3669df099b6c31dfdbe906c96ba51786
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a><span data-ttu-id="f0456-103">Criar um instantâneo de um VHD toocreate vários discos geridos idênticos num pequeno período de tempo com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="f0456-103">Create a snapshot from a VHD toocreate multiple identical managed disks in small amount of time with PowerShell</span></span>

<span data-ttu-id="f0456-104">Este script cria um instantâneo de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente.</span><span class="sxs-lookup"><span data-stu-id="f0456-104">This script creates a snapshot from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="f0456-105">Utilize este script tooimport um instantâneo de tooa VHD (não generalizado/processado pelo Sysprep) especializado e utilize Olá instantâneo toocreate vários discos geridos idênticos num pequeno período de tempo.</span><span class="sxs-lookup"><span data-stu-id="f0456-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD tooa snapshot and then use hello snapshot toocreate multiple identical managed disks in small amount of time.</span></span> <span data-ttu-id="f0456-106">Além disso, utilizá-la tooimport um instantâneo dos dados VHD tooa e, em seguida, utilize Olá instantâneo toocreate vários discos geridos pequena quantidade de tempo.</span><span class="sxs-lookup"><span data-stu-id="f0456-106">Also, use it tooimport a data VHD tooa snapshot and then use hello snapshot toocreate multiple managed disks in small amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="f0456-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="f0456-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="f0456-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="f0456-108">Script explanation</span></span>

<span data-ttu-id="f0456-109">Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um VHD numa subscrição diferente.</span><span class="sxs-lookup"><span data-stu-id="f0456-109">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="f0456-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="f0456-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="f0456-111">Comando</span><span class="sxs-lookup"><span data-stu-id="f0456-111">Command</span></span> | <span data-ttu-id="f0456-112">Notas</span><span class="sxs-lookup"><span data-stu-id="f0456-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="f0456-113">Novo AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="f0456-113">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="f0456-114">Cria a configuração de disco que é utilizada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="f0456-114">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="f0456-115">Inclui o tipo de armazenamento, localização, Id da conta de armazenamento de olá onde está armazenada principal Olá VHD do recurso e URI de VHD do principal de Olá VHD.</span><span class="sxs-lookup"><span data-stu-id="f0456-115">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, and VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="f0456-116">Novo AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="f0456-116">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="f0456-117">Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f0456-117">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="f0456-118">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="f0456-118">Next steps</span></span>

[<span data-ttu-id="f0456-119">Criar um disco gerido a partir do instantâneo</span><span class="sxs-lookup"><span data-stu-id="f0456-119">Create a managed disk from snapshot</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[<span data-ttu-id="f0456-120">Criar uma máquina virtual ao anexar um disco gerido como disco do SO</span><span class="sxs-lookup"><span data-stu-id="f0456-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="f0456-121">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="f0456-121">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="f0456-122">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="f0456-122">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
