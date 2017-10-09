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
ms.openlocfilehash: 47acff274cdf79d6fc3cd685cda01cad3d14ca8e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-vhd-file-in-a-storage-account-in-same-or-different-subscription-with-powershell"></a>Criar um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente com o PowerShell

Este script cria um disco gerido a partir de um ficheiro VHD numa conta de armazenamento na subscrição idêntica ou diferente. Utilize este script tooimport um especializadas (não generalizado/processado pelo Sysprep) VHD toomanaged SO disco toocreate uma máquina virtual. Além disso, utilize tooimport um disco de dados de toomanaged VHD de dados. 

Não crie múltiplos discos geridos idênticos de um ficheiro VHD num pequeno período de tempo. toocreate discos geridos de um ficheiro vhd, blob do ficheiro de vhd Olá instantâneo e, em seguida, é utilizado toocreate gerido discos. Instantâneo de apenas um blob pode ser criado num minuto que provoca falhas na criação do disco toothrottling devida. tooavoid esta limitação, crie um [gerido instantâneo de ficheiro de vhd Olá](virtual-machines-windows-powershell-sample-create-snapshot-from-vhd.md?toc=%2fpowershell%2fmodule%2ftoc.json) e, em seguida, utilize Olá geridos instantâneo toocreate vários discos geridos num curto período de tempo. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-managed-disks-from-vhd-in-different-subscription/create-managed-disks-from-vhd-in-different-subscription.ps1 "Create managed disk from VHD")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um VHD numa subscrição diferente. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração de disco que é utilizada para a criação do disco. Inclui o tipo de armazenamento, localização, Id de Olá conta do storage onde está armazenada principal Olá VHD, URI do VHD do principal de Olá VHD do recurso. |
| [Novo AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros. |

## <a name="next-steps"></a>Passos seguintes

[Criar uma máquina virtual ao anexar um disco gerido como disco do SO](./virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../app-service-web/app-service-powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
