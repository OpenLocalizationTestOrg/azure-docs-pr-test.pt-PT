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
# <a name="exportcopy-managed-snapshots-as-vhd-tooa-storage-account-in-different-region-with-powershell"></a>Exportar/cópia gerido instantâneos como conta de armazenamento do VHD tooa numa região diferente com o PowerShell

Este script exporta uma conta de armazenamento do instantâneo gerido tooa numa região diferente. -Lo primeiro gera Olá URI de SAS do instantâneo Olá e, em seguida, utiliza-toocopy-tooa a conta de armazenamento numa região diferente. Utilize este script toomaintain de cópia de segurança aos discos geridos numa região diferente para a recuperação de desastre.  

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/copy-snapshot-to-storage-account/copy-snapshot-to-storage-account.ps1 "Copy snapshot")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toogenerate URI de SAS para um Olá gerido de instantâneos e cópias de instantâneos tooa conta de armazenamento com o URI de SAS. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Conceder AzureRmSnapshotAccess](/powershell/module/azurerm.compute/New-AzureRmDisk) | Gera o URI de SAS para um instantâneo toocopy utilizado-tooa conta de armazenamento. |
| [Novo AzureStorageContext](/powershell/module/azure.storage/New-AzureStorageContext) | Cria um contexto de conta de armazenamento com o nome da conta Olá e a chave. Neste contexto pode ser utilizados tooperform operações de leitura/escrita na conta de armazenamento Olá. |
| [Início AzureStorageBlobCopy](/powershell/module/azure.storage/Start-AzureStorageBlobCopy) | Cópias Olá subjacente VHD de uma conta de armazenamento do instantâneo tooa |

## <a name="next-steps"></a>Passos seguintes

[Criar um disco gerido a partir de um VHD](virtual-machines-windows-powershell-sample-create-managed-disk-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json)

[Criar uma máquina virtual a partir de um disco gerido](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
