---
title: "aaaAzure exemplo de Script do PowerShell - criar um disco gerido a partir de um instantâneo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar um disco gerido a partir de um instantâneo"
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
ms.openlocfilehash: 4fa34a8d6c67171083fba9a9ad73ecca5e0f0229
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-managed-disk-from-a-snapshot-with-powershell"></a>Criar um disco gerido a partir de um instantâneo com o PowerShell

Este script cria um disco gerido a partir de um instantâneo. Utilizá-lo toorestore uma máquina virtual de instantâneos de discos de dados e SO. Crie o SO e discos geridos dos respetivos instantâneos de dados e, em seguida, criar uma nova máquina virtual ligando discos geridos. Também pode restaurar os discos de dados de uma VM existente ao anexar a criação de instantâneos de discos de dados.

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/storage/create-managed-disk-from-snapshot/create-managed-disk-from-snapshot.ps1 "Create managed disk from snapshot")]


## <a name="script-explanation"></a>Explicação de script

Este script utiliza os seguintes comandos toocreate um disco gerido a partir de um instantâneo. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/Get-AzureRmSnapshot) | Obtém as propriedades de instantâneos.  |
| [Novo AzureRmDiskConfig](/powershell/module/azurerm.compute/New-AzureRmDiskConfig) | Cria a configuração de disco que é utilizada para a criação do disco. Inclui Olá Id do recurso de instantâneo de principal de Olá, localização que seja igual à localização de Olá do tipo de armazenamento de instantâneos e Olá principal.  |
| [Novo AzureRmDisk](/powershell/module/azurerm.compute/New-AzureRmDisk) | Cria um disco com a configuração do disco, o nome do disco e o nome do grupo de recursos transmitido como parâmetros. |


## <a name="next-steps"></a>Passos seguintes

[Criar uma máquina virtual a partir de um disco gerido](./../../virtual-machines/scripts/virtual-machines-windows-powershell-sample-create-vm-from-managed-os-disks.md?toc=%2fpowershell%2fmodule%2ftoc.json)

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../../virtual-machines/windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
