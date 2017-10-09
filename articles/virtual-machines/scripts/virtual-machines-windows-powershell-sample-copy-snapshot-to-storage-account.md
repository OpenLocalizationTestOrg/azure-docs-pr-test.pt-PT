---
title: "Exemplo de Script do PowerShell - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa numa região diferente de aaaAzure | Microsoft Docs"
description: "Exemplo de Script do PowerShell do Azure - instantâneo de exportação/copiar como conta de armazenamento do VHD tooa na mesma região diferente"
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
ms.openlocfilehash: c18ad4fa0bf12033fafe941a807e7b4c8d233a30
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a><span data-ttu-id="655bb-103">Exportar/cópia gerido instantâneos como conta de armazenamento do VHD tooa numa região diferente com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="655bb-103">Export/Copy managed snapshots as VHD tooa storage account in different region with PowerShell</span></span>

<span data-ttu-id="655bb-104">Este script exporta uma conta de armazenamento do instantâneo gerido tooa numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="655bb-104">This script exports a managed snapshot tooa storage account in different region.</span></span> <span data-ttu-id="655bb-105">-Lo primeiro gera Olá URI de SAS do instantâneo Olá e, em seguida, utiliza-toocopy-tooa a conta de armazenamento numa região diferente.</span><span class="sxs-lookup"><span data-stu-id="655bb-105">It first generates hello SAS URI of hello snapshot and then uses it toocopy it tooa storage account in different region.</span></span> <span data-ttu-id="655bb-106">Utilize este script toomaintain de cópia de segurança aos discos geridos numa região diferente para a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="655bb-106">Use this script toomaintain backup of your managed disks in different region for disaster recovery.</span></span>  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="655bb-107">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="655bb-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a><span data-ttu-id="655bb-108">Explicação de script</span><span class="sxs-lookup"><span data-stu-id="655bb-108">Script explanation</span></span>

<span data-ttu-id="655bb-109">Este script utiliza os seguintes comandos toogenerate URI de SAS para um Olá gerido de instantâneos e cópias de instantâneos tooa conta de armazenamento com o URI de SAS.</span><span class="sxs-lookup"><span data-stu-id="655bb-109">This script uses following commands toogenerate SAS URI for a managed snapshot and copies hello snapshot tooa storage account using SAS URI.</span></span> <span data-ttu-id="655bb-110">Cada comando na tabela de Olá contém ligações a documentação específica toocommand.</span><span class="sxs-lookup"><span data-stu-id="655bb-110">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="655bb-111">Comando</span><span class="sxs-lookup"><span data-stu-id="655bb-111">Command</span></span> | <span data-ttu-id="655bb-112">Notas</span><span class="sxs-lookup"><span data-stu-id="655bb-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="655bb-113">Conceder AzureRmSnapshotAccess</span><span class="sxs-lookup"><span data-stu-id="655bb-113">Grant-AzureRmSnapshotAccess</span></span>](/powershell/module/azurerm.compute/New-AzureRmDisk) | <span data-ttu-id="655bb-114">Gera o URI de SAS para um instantâneo toocopy utilizado-tooa conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="655bb-114">Generates SAS URI for a snapshot that is used toocopy it tooa storage account.</span></span> |
| [<span data-ttu-id="655bb-115">Novo AzureStorageContext</span><span class="sxs-lookup"><span data-stu-id="655bb-115">New-AzureStorageContext</span></span>](/powershell/module/azure.storage/New-AzureStorageContext) | <span data-ttu-id="655bb-116">Cria um contexto de conta de armazenamento com o nome da conta Olá e a chave.</span><span class="sxs-lookup"><span data-stu-id="655bb-116">Creates a storage account context using hello account name and key.</span></span> <span data-ttu-id="655bb-117">Neste contexto pode ser utilizados tooperform operações de leitura/escrita na conta de armazenamento Olá.</span><span class="sxs-lookup"><span data-stu-id="655bb-117">This context can be used tooperform read/write operations on hello storage account.</span></span> |
| [<span data-ttu-id="655bb-118">Início AzureStorageBlobCopy</span><span class="sxs-lookup"><span data-stu-id="655bb-118">Start-AzureStorageBlobCopy</span></span>](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | <span data-ttu-id="655bb-119">Cópias Olá subjacente VHD de uma conta de armazenamento do instantâneo tooa</span><span class="sxs-lookup"><span data-stu-id="655bb-119">Copies hello underlying VHD of a snapshot tooa storage account</span></span> |

## <a name="next-steps"></a><span data-ttu-id="655bb-120">Passos seguintes</span><span class="sxs-lookup"><span data-stu-id="655bb-120">Next steps</span></span>

[<span data-ttu-id="655bb-121">Criar um disco gerido a partir de um VHD</span><span class="sxs-lookup"><span data-stu-id="655bb-121">Create a managed disk from a VHD</span></span>](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[<span data-ttu-id="655bb-122">Criar uma máquina virtual a partir de um disco gerido</span><span class="sxs-lookup"><span data-stu-id="655bb-122">Create a virtual machine from a managed disk</span></span>](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

<span data-ttu-id="655bb-123">Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="655bb-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="655bb-124">Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span><span class="sxs-lookup"><span data-stu-id="655bb-124">Additional virtual machine PowerShell script samples can be found in hello [Azure Windows VM documentation](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>
