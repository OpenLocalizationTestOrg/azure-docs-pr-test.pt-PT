---
title: aaaAzure CLI Script de exemplo - criar uma VM ao anexar um disco como disco de SO gerido | Microsoft Docs
description: Script CLI do Azure de exemplo - criar uma VM ao anexar um disco gerido como disco do SO
services: virtual-machines-linux
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 71fc5c6a577c64b913cfa35e99b2b9b75dea0c31
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-cli"></a><span data-ttu-id="45fdb-103">Criar uma máquina virtual utilizando um disco de SO gerido existente com a CLI</span><span class="sxs-lookup"><span data-stu-id="45fdb-103">Create a virtual machine using an existing managed OS disk with CLI</span></span>

<span data-ttu-id="45fdb-104">Este script cria uma máquina virtual, anexar um disco existente gerido como disco do SO.</span><span class="sxs-lookup"><span data-stu-id="45fdb-104">This script creates a virtual machine by attaching an existing managed disk as OS disk.</span></span> <span data-ttu-id="45fdb-105">Utilize este script no precedente cenários:</span><span class="sxs-lookup"><span data-stu-id="45fdb-105">Use this script in preceding scenarios:</span></span>
* <span data-ttu-id="45fdb-106">Criar uma VM a partir de um disco de SO gerido existente que foi copiado a partir de um disco gerido numa subscrição diferente</span><span class="sxs-lookup"><span data-stu-id="45fdb-106">Create a VM from an existing managed OS disk that was copied from a managed disk in different subscription</span></span>
* <span data-ttu-id="45fdb-107">Criar uma VM a partir de um disco gerido existente criada a partir do ficheiro VHD especializado</span><span class="sxs-lookup"><span data-stu-id="45fdb-107">Create a VM from an existing managed disk that was created from a specialized VHD file</span></span> 
* <span data-ttu-id="45fdb-108">Criar uma VM a partir de um disco de SO gerido existente que foi criado a partir de um instantâneo</span><span class="sxs-lookup"><span data-stu-id="45fdb-108">Create a VM from an existing managed OS disk that was created from a snapshot</span></span> 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="45fdb-109">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="45fdb-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-attach-existing-managed-os-disk/create-vm-attach-existing-managed-os-disk.sh "Create VM from a managed disk")]

## <a name="clean-up-deployment"></a><span data-ttu-id="45fdb-110">Limpar a implementação</span><span class="sxs-lookup"><span data-stu-id="45fdb-110">Clean up deployment</span></span> 

<span data-ttu-id="45fdb-111">Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.</span><span class="sxs-lookup"><span data-stu-id="45fdb-111">Run hello following command tooremove hello resource group, VM, and all related resources.</span></span>

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="45fdb-112">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="45fdb-112">Script explanation</span></span>

<span data-ttu-id="45fdb-113">Este script utiliza Olá seguintes propriedades de disco de tooget gerido de comandos, anexar um disco gerido tooa nova VM e criar uma VM.</span><span class="sxs-lookup"><span data-stu-id="45fdb-113">This script uses hello following commands tooget managed disk properties, attach a managed disk tooa new VM and create a VM.</span></span> <span data-ttu-id="45fdb-114">Cada item na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="45fdb-114">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="45fdb-115">Comando</span><span class="sxs-lookup"><span data-stu-id="45fdb-115">Command</span></span> | <span data-ttu-id="45fdb-116">Notas</span><span class="sxs-lookup"><span data-stu-id="45fdb-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="45fdb-117">Mostrar de disco AZ</span><span class="sxs-lookup"><span data-stu-id="45fdb-117">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="45fdb-118">Obtém as propriedades de disco gerido com o nome do disco e o nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="45fdb-118">Gets managed disk properties using disk name and resource group name.</span></span> <span data-ttu-id="45fdb-119">Propriedade de ID é utilizado tooattach tooa um disco gerido nova VM</span><span class="sxs-lookup"><span data-stu-id="45fdb-119">Id property is used tooattach a managed disk tooa new VM</span></span> |
| [<span data-ttu-id="45fdb-120">Criar AZ vm</span><span class="sxs-lookup"><span data-stu-id="45fdb-120">az vm create</span></span>](https://docs.microsoft.com/cli/azure/vm#create) | <span data-ttu-id="45fdb-121">Cria uma VM a utilizar um disco de SO gerido</span><span class="sxs-lookup"><span data-stu-id="45fdb-121">Creates a VM using a managed OS disk</span></span> |
## <a name="next-steps"></a><span data-ttu-id="45fdb-122">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="45fdb-122">Next steps</span></span>

<span data-ttu-id="45fdb-123">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="45fdb-123">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="45fdb-124">Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="45fdb-124">Additional virtual machine CLI script samples can be found in hello [Azure Linux VM documentation](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
