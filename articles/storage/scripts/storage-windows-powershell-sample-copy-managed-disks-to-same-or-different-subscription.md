---
title: "aaaAzure exemplo de Script do PowerShell - cópia (mover) geridos toosame de discos ou outra subscrição | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - toosame de discos de cópia (mover) gerida ou uma subscrição diferente"
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
ms.date: 06/06/2017
ms.author: ramankum
ms.openlocfilehash: 5a92118e10a14615e5b1713f1b90188b37b05305
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a><span data-ttu-id="40ce5-103">Cópia gerida discos no Olá mesma subscrição ou outra subscrição com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="40ce5-103">Copy managed disks in hello same subscription or different subscription with PowerShell</span></span>

<span data-ttu-id="40ce5-104">Este script cria uma cópia de um disco gerido existente no Olá mesma subscrição ou uma subscrição diferente.</span><span class="sxs-lookup"><span data-stu-id="40ce5-104">This script creates a copy of an existing managed disk in hello same subscription or different subscription.</span></span> <span data-ttu-id="40ce5-105">Olá novo disco é criado na Olá mesma região principal Olá geridos disco.</span><span class="sxs-lookup"><span data-stu-id="40ce5-105">hello new disk is created in hello same region as hello parent managed disk.</span></span>   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="40ce5-106">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="40ce5-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="40ce5-107">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="40ce5-107">Script explanation</span></span>

<span data-ttu-id="40ce5-108">Este script utiliza os seguintes comandos toocreate um novo disco gerido na utilização de subscrição de destino de Olá Olá Id da origem de Olá de gerido disco.</span><span class="sxs-lookup"><span data-stu-id="40ce5-108">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="40ce5-109">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="40ce5-109">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="40ce5-110">Comando</span><span class="sxs-lookup"><span data-stu-id="40ce5-110">Command</span></span> | <span data-ttu-id="40ce5-111">Notas</span><span class="sxs-lookup"><span data-stu-id="40ce5-111">Notes</span></span> |
|---|---|
| [<span data-ttu-id="40ce5-112">Novo AzureRmDiskConfig</span><span class="sxs-lookup"><span data-stu-id="40ce5-112">New-AzureRmDiskConfig</span></span>](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | <span data-ttu-id="40ce5-113">Cria a configuração de disco que é utilizada para a criação do disco.</span><span class="sxs-lookup"><span data-stu-id="40ce5-113">Creates disk configuration that is used for disk creation.</span></span> <span data-ttu-id="40ce5-114">Inclui Olá Id do recurso de disco principal de Olá e a localização que seja igual à localização de Olá do disco principal.</span><span class="sxs-lookup"><span data-stu-id="40ce5-114">It includes hello resource Id of hello parent disk and location that is same as hello location of parent disk.</span></span>  |
| [<span data-ttu-id="40ce5-115">Novo AzureRmDisk</span><span class="sxs-lookup"><span data-stu-id="40ce5-115">New-AzureRmDisk</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="40ce5-116">Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros.</span><span class="sxs-lookup"><span data-stu-id="40ce5-116">Creates a disk using disk configuration, disk name, and resource group name passed as parameters.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="40ce5-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="40ce5-117">Next steps</span></span>

[<span data-ttu-id="40ce5-118">Criar uma máquina virtual a partir de um disco gerido</span><span class="sxs-lookup"><span data-stu-id="40ce5-118">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="40ce5-119">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="40ce5-119">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="40ce5-120">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="40ce5-120">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
