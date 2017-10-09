---
title: "aaaAzure CLI Script de exemplo - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa numa região diferente | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na subscrição idêntica ou diferente"
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
ms.openlocfilehash: 027c5e588c4f10d64d125c17f4c78a7d8e1ef060
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-cli"></a><span data-ttu-id="e8730-103">Exportar/cópia gerido instantâneos como conta de armazenamento do VHD tooa numa região diferente com a CLI</span><span class="sxs-lookup"><span data-stu-id="e8730-103">Export/Copy managed snapshots as VHD tooa storage account in different region with CLI</span></span>

<span data-ttu-id="e8730-104">Este script exporta uma conta de armazenamento do instantâneo gerido tooa numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="e8730-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="e8730-105">-Lo primeiro gera Olá URI de SAS do instantâneo Olá e, em seguida, utiliza-toocopy-tooa a conta de armazenamento numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="e8730-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="e8730-106">Utilize este script toomaintain de cópia de segurança aos discos geridos numa região diferente para a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="e8730-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span> 


[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e8730-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e8730-107">Sample script</span></span>

[!code-azurecli[main](../../../cli_scripts/storage/copy-snapshots-to-storage-account/copy-snapshots-to-storage-account.sh "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="e8730-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="e8730-108">Script explanation</span></span>

<span data-ttu-id="e8730-109">Este script utiliza os seguintes comandos toogenerate URI de SAS para um Olá gerido de instantâneos e cópias de instantâneos tooa conta de armazenamento com o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="e8730-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="e8730-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="e8730-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e8730-111">Comando</span><span class="sxs-lookup"><span data-stu-id="e8730-111">Command</span></span> | <span data-ttu-id="e8730-112">Notas</span><span class="sxs-lookup"><span data-stu-id="e8730-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e8730-113">AZ instantâneo conceder acesso de leitura</span><span class="sxs-lookup"><span data-stu-id="e8730-113">az snapshot grant-access</span></span>](https://docs.microsoft.com/cli/azure/snapshot#grant-access) | <span data-ttu-id="e8730-114">Gera SAS só de leitura, que é utilizado toocopy subjacente a conta de armazenamento de tooa de ficheiros VHD ou transferi-lo tooon local</span><span class="sxs-lookup"><span data-stu-id="e8730-114">Generates read-only SAS that is used toocopy underlying VHD file tooa storage account or download it tooon-premises</span></span>  |
| [<span data-ttu-id="e8730-115">iniciar a cópia de BLOBs de armazenamento AZ</span><span class="sxs-lookup"><span data-stu-id="e8730-115">az storage blob copy start</span></span>](https://docs.microsoft.com/en-us/cli/azure/storage/blob/copy#start) | <span data-ttu-id="e8730-116">Copia um blob de forma assíncrona a partir de um tooanother de conta de armazenamento</span><span class="sxs-lookup"><span data-stu-id="e8730-116">Copies a blob asynchronously from one storage account tooanother</span></span> |

## <a name="next-steps"></a><span data-ttu-id="e8730-117">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="e8730-117">Next steps</span></span>

[<span data-ttu-id="e8730-118">Criar um disco gerido a partir de um VHD</span><span class="sxs-lookup"><span data-stu-id="e8730-118">Create a managed disk from a VHD</span></span>](./../scripts/storage-linux-cli-sample-create-managed-disk-from-vhd.md?toc=%2fcli%2fmodule%2ftoc.json)

[<span data-ttu-id="e8730-119">Criar uma máquina virtual a partir de um disco gerido</span><span class="sxs-lookup"><span data-stu-id="e8730-119">Create a virtual machine from a managed disk</span></span>](./../../virtual-machines/scripts/virtual-machines-linux-cli-sample-create-vm-from-managed-os-disks.md?toc=%2fcli%2fmodule%2ftoc.json)

<span data-ttu-id="e8730-120">Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="e8730-120">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="e8730-121">Máquina virtual adicional e discos geridos amostras de script da CLI podem ser encontrados na Olá [documentação de VM do Linux do Azure](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="e8730-121">Additional virtual machine and managed disks CLI script samples can be found in hello [Azure Linux VM documentation](../../virtual-machines/linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>
