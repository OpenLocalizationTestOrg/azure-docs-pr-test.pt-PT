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
# <a name="copy-managed-disks-in-hello-same-subscription-or-different-subscription-with-powershell"></a>Cópia gerida discos no Olá mesma subscrição ou outra subscrição com o PowerShell

Este script cria uma cópia de um disco gerido existente no Olá mesma subscrição ou uma subscrição diferente. Olá novo disco é criado na Olá mesma região principal Olá geridos disco.   

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/copy-managed-disks-to-same-or-different-subscription/copy-managed-disks-to-same-or-different-subscription.ps1 "Copy managed disk")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um novo disco gerido na utilização de subscrição de destino de Olá Olá Id da origem de Olá de gerido disco. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Novo AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração de disco que é utilizada para a criação do disco. Inclui Olá Id do recurso de disco principal de Olá e a localização que seja igual à localização de Olá do disco principal.  |
| [Novo AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros. |


## <a name="next-steps"></a>Passos seguintes

[Criar uma máquina virtual a partir de um disco gerido](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
