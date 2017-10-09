---
title: "aaaAzure CLI Script de exemplo - criar um disco gerido a partir de um instantâneo | Microsoft Docs"
description: "Script CLI do Azure de exemplo - criar um disco gerido a partir de um instantâneo"
services: virtual-machines-linux
documentationcenter: storage
author: ramankumarlive
manager: kavithag
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/19/2017
ms.author: ramankum
ms.openlocfilehash: f92059353bfb739cff05213a9d206bfde2829a98
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-cli"></a><span data-ttu-id="16168-103">Criar um disco gerido a partir de um instantâneo com o CLI</span><span class="sxs-lookup"><span data-stu-id="16168-103">Create a managed disk from a snapshot with CLI</span></span>

<span data-ttu-id="16168-104">Este script cria um disco gerido a partir de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="16168-104">This script creates a managed disk from a snapshot.</span></span> <span data-ttu-id="16168-105">Utilizá-lo toorestore uma máquina virtual de instantâneos de discos de dados e SO.</span><span class="sxs-lookup"><span data-stu-id="16168-105">Use it toorestore a virtual machine from snapshots of OS and data disks.</span></span> <span data-ttu-id="16168-106">Crie o SO e discos geridos dos respetivos instantâneos de dados e, em seguida, criar uma nova máquina virtual ligando discos geridos.</span><span class="sxs-lookup"><span data-stu-id="16168-106">Create OS and data managed disks from respective snapshots and then create a new virtual machine by attaching managed disks.</span></span> <span data-ttu-id="16168-107">Também pode restaurar os discos de dados de uma VM existente ao anexar a criação de instantâneos de discos de dados.</span><span class="sxs-lookup"><span data-stu-id="16168-107">You can also restore data disks of an existing VM by attaching data disks created from snapshots.</span></span>


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="16168-108">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="16168-108">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/create-managed-disks-from-snapshot/create-managed-disks-from-snapshot.sh "Create managed disk from snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="16168-109">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="16168-109">Script explanation</span></span>

<span data-ttu-id="16168-110">Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um instantâneo.</span><span class="sxs-lookup"><span data-stu-id="16168-110">This script uses following commands toocreate a managed disk from a snapshot.</span></span> <span data-ttu-id="16168-111">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="16168-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="16168-112">Comando</span><span class="sxs-lookup"><span data-stu-id="16168-112">Command</span></span> | <span data-ttu-id="16168-113">Notas</span><span class="sxs-lookup"><span data-stu-id="16168-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="16168-114">Mostrar de instantâneo AZ</span><span class="sxs-lookup"><span data-stu-id="16168-114">az snapshot show</span></span>](https://docs.microsoft.com/cli/azure/snapshot#show) | <span data-ttu-id="16168-115">Obtém todas as propriedades de Olá de um instantâneo com o nome de Olá e propriedades do grupo de recursos de instantâneo Olá.</span><span class="sxs-lookup"><span data-stu-id="16168-115">Gets all hello properties of a snapshot using hello name and resource group properties of hello snapshot.</span></span> <span data-ttu-id="16168-116">Propriedade de ID é utilizado toocreate de disco gerido.</span><span class="sxs-lookup"><span data-stu-id="16168-116">Id property is used toocreate managed disk.</span></span>  |
| [<span data-ttu-id="16168-117">criar disco de AZ</span><span class="sxs-lookup"><span data-stu-id="16168-117">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="16168-118">Cria um geridos utilizando o disco de instantâneos Id de um instantâneo gerido</span><span class="sxs-lookup"><span data-stu-id="16168-118">Creates a managed disk using snapshot Id of a managed snapshot</span></span> |

## <a name="next-steps"></a><span data-ttu-id="16168-119">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="16168-119">Next steps</span></span>

[<span data-ttu-id="16168-120">Criar uma máquina virtual ao anexar um disco gerido como disco do SO</span><span class="sxs-lookup"><span data-stu-id="16168-120">Create a virtual machine by attaching a managed disk as OS disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="16168-121">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="16168-121">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="16168-122">Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="16168-122">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
