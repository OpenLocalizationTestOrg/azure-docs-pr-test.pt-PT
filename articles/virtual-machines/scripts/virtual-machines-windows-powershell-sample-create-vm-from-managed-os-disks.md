---
title: aaaAzure exemplo de Script do PowerShell - criar uma VM ao anexar um disco como disco de SO gerido | Microsoft Docs
description: Script do PowerShell do Azure de exemplo - criar uma VM ao anexar um disco gerido como disco do SO
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
ms.openlocfilehash: 8ae5b14df3977a4af91b92692cb925199cfb8058
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-virtual-machine-using-an-existing-managed-os-disk-with-powershell"></a>Criar uma máquina virtual utilizando um disco de SO existente gerido com o PowerShell

Este script cria uma máquina virtual, anexar um disco existente gerido como disco do SO. Utilize este script no precedente cenários:
* Criar uma VM a partir de um disco de SO gerido existente que foi copiado a partir de um disco gerido numa subscrição diferente
* Criar uma VM a partir de um disco gerido existente criada a partir do ficheiro VHD especializado 
* Criar uma VM a partir de um disco de SO gerido existente que foi criado a partir de um instantâneo 

[!INCLUDE [sample-powershell-install](../../../includes/sample-powershell-install-no-ssh.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-powershell[main](../../../powershell_scripts/virtual-machine/create-vm-from-snapshot/create-vm-from-snapshot.ps1 "Create VM from snapshot")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá seguintes propriedades de disco de tooget gerido de comandos, anexar um disco gerido tooa nova VM e criar uma VM. Cada item na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Get-AzureRmDisk](/powershell/module/azurerm.compute/Get-AzureRmDisk) | Obtém o objeto de disco com base no nome de Olá e grupo de recursos de Olá de um disco. Propriedade de ID de Olá devolveu o objeto de disco é utilizado tooattach Olá disco tooa nova VM |
| [Novo AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) | Cria uma configuração de VM. Esta configuração inclui informações como o nome VM, sistema operativo e as credenciais administrativas. configuração de Olá é utilizada durante a criação da VM. |
| [Conjunto AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) | Anexa um disco gerido utilizando a propriedade de Id de Olá dos discos de Olá como SO disco tooa nova máquina virtual |
| [Novo AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Cria um endereço IP público. |
| [Novo AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria uma interface de rede. |
| [Novo-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Crie uma máquina virtual. |
|[Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Remove um grupo de recursos e todos os recursos contidos. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre o módulo do Azure PowerShell Olá, consulte [documentação do Azure PowerShell](/powershell/azure/overview).

Exemplos de script do PowerShell de máquina virtual adicional que podem ser encontrados no Olá [documentação do Azure Windows VM](../windows/powershell-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).
