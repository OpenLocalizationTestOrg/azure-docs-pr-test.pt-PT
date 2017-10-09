---
title: "aaaAzure CLI Script de exemplo - cópia (mover) geridos toosame de discos ou outra subscrição | Microsoft Docs"
description: "Azure CLI Script de exemplo - toosame de discos de cópia (mover) gerida ou uma subscrição diferente"
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
ms.openlocfilehash: 8581169baa0fd0e0eec1c72eab77b657f48b1cfa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="copy-managed-disks-toosame-or-different-subscription-with-cli"></a><span data-ttu-id="fdd56-103">Copiar discos geridos toosame ou outra subscrição com a CLI</span><span class="sxs-lookup"><span data-stu-id="fdd56-103">Copy managed disks toosame or different subscription with CLI</span></span>

<span data-ttu-id="fdd56-104">Este script copia um toosame de disco gerido ou uma subscrição diferente, mas no Olá mesma região.</span><span class="sxs-lookup"><span data-stu-id="fdd56-104">This script copies a managed disk toosame or different subscription but in hello same region.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="fdd56-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="fdd56-105">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.sh "Copy managed disk")]


## <a name="script-explanation"></a><span data-ttu-id="fdd56-106">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="fdd56-106">Script explanation</span></span>

<span data-ttu-id="fdd56-107">Este script utiliza os seguintes comandos toocreate um novo disco gerido na utilização de subscrição de destino de Olá Olá Id da origem de Olá de gerido disco.</span><span class="sxs-lookup"><span data-stu-id="fdd56-107">This script uses following commands toocreate a new managed disk in hello target subscription using hello Id of hello source managed disk.</span></span> <span data-ttu-id="fdd56-108">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="fdd56-108">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="fdd56-109">Comando</span><span class="sxs-lookup"><span data-stu-id="fdd56-109">Command</span></span> | <span data-ttu-id="fdd56-110">Notas</span><span class="sxs-lookup"><span data-stu-id="fdd56-110">Notes</span></span> |
|---|---|
| [<span data-ttu-id="fdd56-111">Mostrar de disco AZ</span><span class="sxs-lookup"><span data-stu-id="fdd56-111">az disk show</span></span>](https://docs.microsoft.com/cli/azure/disk#show) | <span data-ttu-id="fdd56-112">Obtém todas as propriedades de Olá de um disco gerido utilizando as propriedades do grupo de recursos e nome Olá de disco Olá de gerido.</span><span class="sxs-lookup"><span data-stu-id="fdd56-112">Gets all hello properties of a managed disk using hello name and resource group properties of hello managed disk.</span></span> <span data-ttu-id="fdd56-113">Propriedade de ID é utilizado toocopy Olá gerido disco toodifferent subscrição.</span><span class="sxs-lookup"><span data-stu-id="fdd56-113">Id property is used toocopy hello managed disk toodifferent subscription.</span></span>  |
| [<span data-ttu-id="fdd56-114">criar disco de AZ</span><span class="sxs-lookup"><span data-stu-id="fdd56-114">az disk create</span></span>](https://docs.microsoft.com/cli/azure/disk#create) | <span data-ttu-id="fdd56-115">Copia um disco gerido através da criação de um novo disco gerido na subscrição diferentes com o Id e nome principal de Olá geridos disco.</span><span class="sxs-lookup"><span data-stu-id="fdd56-115">Copies a managed disk by creating a new managed disk in different subscription using Id and name hello parent managed disk.</span></span>  |

## <a name="next-steps"></a><span data-ttu-id="fdd56-116">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="fdd56-116">Next steps</span></span>

[<span data-ttu-id="fdd56-117">Criar uma máquina virtual a partir de um disco gerido</span><span class="sxs-lookup"><span data-stu-id="fdd56-117">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="fdd56-118">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="fdd56-118">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="fdd56-119">Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="fdd56-119">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
