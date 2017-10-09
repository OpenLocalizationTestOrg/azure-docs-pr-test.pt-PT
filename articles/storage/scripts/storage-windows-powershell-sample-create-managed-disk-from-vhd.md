---
title: "aaaAzure exemplo de Script do PowerShell - criar um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente"
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
ms.openlocfilehash: 93157823eb3b8cddba5e0af455d16bff1d42ce00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a><span data-ttu-id="4e718-103">Criar um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="4e718-103">Create a managed disk from a VHD file in a storage account in same or different subscription with PowerShell</span></span>

<span data-ttu-id="4e718-104">Este script cria um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente.</span><span class="sxs-lookup"><span data-stu-id="4e718-104">This script creates a managed disk from a VHD file in a storage account in same or different subscription.</span></span> <span data-ttu-id="4e718-105">Utilize este script tooimport um especializadas (não generalizado/processado pelo Sysprep) VHD toomanaged SO disco toocreate uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="4e718-105">Use this script tooimport a specialized (not generalized/sysprepped) VHD toomanaged OS disk toocreate a virtual machine.</span></span> <span data-ttu-id="4e718-106">Além disso, utilize tooimport um disco de dados de toomanaged VHD de dados.</span><span class="sxs-lookup"><span data-stu-id="4e718-106">Also, use it tooimport a data VHD toomanaged data disk.</span></span> 

<span data-ttu-id="4e718-107">Não crie múltiplos discos geridos idênticos de um ficheiro VHD num pequeno período de tempo.</span><span class="sxs-lookup"><span data-stu-id="4e718-107">Don't create multiple identical managed disks from a VHD file in small amount of time.</span></span> <span data-ttu-id="4e718-108">toocreate discos geridos de um ficheiro vhd, blob do ficheiro de vhd Olá instantâneo e, em seguida, é utilizado toocreate gerido discos.</span><span class="sxs-lookup"><span data-stu-id="4e718-108">toocreate managed disks from a vhd file, blob snapshot of hello vhd file is created and then it is used toocreate managed disks.</span></span> <span data-ttu-id="4e718-109">Instantâneo de apenas um blob pode ser criado num minuto que provoca falhas na criação do disco toothrottling devida.</span><span class="sxs-lookup"><span data-stu-id="4e718-109">Only one blob snapshot can be created in a minute that causes disk creation failures due toothrottling.</span></span> <span data-ttu-id="4e718-110">tooavoid esta limitação, crie um [gerido instantâneo de ficheiro de vhd Olá](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e, em seguida, utilize Olá geridos instantâneo toocreate vários discos geridos num curto período de tempo.</span><span class="sxs-lookup"><span data-stu-id="4e718-110">tooavoid this throttling, create a [managed snapshot from hello vhd file](./../scripts/storage-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) and then use hello managed snapshot toocreate multiple managed disks in short amount of time.</span></span> 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="4e718-111">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="4e718-111">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a><span data-ttu-id="4e718-112">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="4e718-112">Script explanation</span></span>

<span data-ttu-id="4e718-113">Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um VHD numa subscrição diferente.</span><span class="sxs-lookup"><span data-stu-id="4e718-113">This script uses following commands toocreate a managed disk from a VHD in different subscription.</span></span> <span data-ttu-id="4e718-114">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="4e718-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4e718-115">Comando</span><span class="sxs-lookup"><span data-stu-id="4e718-115">Command</span></span> | <span data-ttu-id="4e718-116">Notas</span><span class="sxs-lookup"><span data-stu-id="4e718-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4e718-117">Novo AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="4e718-117">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="4e718-118">Cria a configuração de disco que é utilizada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="4e718-118">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="4e718-119">Inclui o tipo de armazenamento, localização, Id de Olá conta do storage onde está armazenada principal Olá VHD, URI do VHD do principal de Olá VHD do recurso.</span><span class="sxs-lookup"><span data-stu-id="4e718-119">It includes storage type, location, resource Id of hello storage account where hello parent VHD is stored, VHD URI of hello parent VHD.</span></span> |
| [<span data-ttu-id="4e718-120">Novo AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="4e718-120">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="4e718-121">Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="4e718-121">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4e718-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="4e718-122">Next steps</span></span>

[<span data-ttu-id="4e718-123">Criar uma máquina virtual ao anexar um disco gerido como disco do SO</span><span class="sxs-lookup"><span data-stu-id="4e718-123">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="4e718-124">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="4e718-124">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="4e718-125">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="4e718-125">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
