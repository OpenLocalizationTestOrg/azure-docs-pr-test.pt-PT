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
# <a name="create-a-snapshot-from-a-vhd-toocreate-multiple-identical-managed-disks-in-small-amount-of-time-with-powershell"></a>Criar um instantâneo de um VHD toocreate vários discos geridos idênticos num pequeno período de tempo com o PowerShell

Este script cria um instantâneo de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente. Utilize este script tooimport um instantâneo de tooa VHD (não generalizado/processado pelo Sysprep) especializado e utilize Olá instantâneo toocreate vários discos geridos idênticos num pequeno período de tempo. Além disso, utilizá-la tooimport um instantâneo dos dados VHD tooa e, em seguida, utilize Olá instantâneo toocreate vários discos geridos pequena quantidade de tempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-snapshots-from-vhd-in-different-subscription/create-snapshots-from-vhd-in-different-subscription.ps1 "Create snapshot from VHD")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um VHD numa subscrição diferente. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração de disco que é utilizada para a criação do disco. Inclui o tipo de armazenamento, localização, Id da conta de armazenamento de olá onde está armazenada principal Olá VHD do recurso e URI de VHD do principal de Olá VHD. |
| [Novo AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros. |

## <a name="next-steps"></a>Passos seguintes

[Criar um disco gerido a partir do instantâneo](virtual-machines-windows-powershell-sample-create-managed-disk-from-snapshot.md?toc=%2fpowershell%2fmodule%2ftoc.json)


[Criar uma máquina virtual ao anexar um disco gerido como disco do SO](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
