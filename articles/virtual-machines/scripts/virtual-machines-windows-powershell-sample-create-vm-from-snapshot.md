---
title: "aaaAzure exemplo de Script do PowerShell - criar uma VM a partir de um instantâneo | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar uma VM a partir de um instantâneo"
services: virtual-machines-windows
documentationcenter: virtual-machines
author: ramankum
manager: kavithag
editor: ramankum
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure
ms.date: 05/10/2017
ms.author: ramankum
ms.custom: mvc
ms.openlocfilehash: 89c65171b55bff0582c4a26df0b0f29f556845fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-from-a-snapshot-with-powershell"></a>Criar uma máquina virtual a partir de um instantâneo com o PowerShell

Este script cria uma máquina virtual a partir de um instantâneo de um disco de SO. 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from managed os disk")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos tooget propriedades de instantâneo, criar um disco gerido a partir do instantâneo e criar uma VM. Cada item na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Get-AzureRmSnapshot](/powershell/module/azurerm.compute/get-azurermsnapshot) | Obtém um instantâneo com o nome do instantâneo. |
| [Novo AzureRmDiskConfig](/powershell/module/azurerm.compute/new-azurermdiskconfig) | Cria uma configuração de disco. Esta configuração é utilizada com o processo de criação do disco Olá. |
| [Novo AzureRmDisk](/powershell/module/azurerm.compute/new-azurermdisk) | Cria um disco gerido. |
| [Novo AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Cria uma configuração de VM. Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas. configuração de Olá é utilizada durante a criação da VM. |
| [Conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | Anexa o disco Olá de gerido como disco de SO toohello máquina de virtual |
| [Novo AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Cria um endereço IP público. |
| [Novo AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria uma interface de rede. |
| [Novo-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Cria uma máquina virtual. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Remove um grupo de recursos e todos os recursos contidos. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
