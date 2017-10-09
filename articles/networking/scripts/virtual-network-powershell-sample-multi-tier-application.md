---
title: "aaaAzure exemplo de script do PowerShell - criar uma rede para aplicações de várias camadas | Microsoft Docs"
description: "Script do PowerShell do Azure de exemplo - criar uma rede virtual para aplicações de várias camadas."
services: virtual-network
documentationcenter: virtual-network
author: georgewallace
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: powershell
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 05/16/2017
ms.author: gwallace
ms.openlocfilehash: 46d6d16dc5dbc8be467359f31346f017727b1abe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-network-for-multi-tier-applications"></a>Criar uma rede para aplicações de várias camadas

Este script de exemplo cria uma rede virtual com as sub-redes de front-end e back-end. Sub-rede de front-end do tráfego toohello tooHTTP limitado e SSH, ao tráfego toohello sub-rede de back-end é limitado tooMySQL, porta 3306. Depois de executar o script Olá tem duas máquinas virtuais, um em cada sub-rede que pode implementar MySQL software e do servidor web.

Se necessário, instale Olá, Azure PowerShell, utilizando a instrução de Olá encontrado no Olá [Guia do Azure PowerShell](https://docs.microsoft.com/powershell/azureps-cmdlets-docs/)e, em seguida, execute `Login-AzureRmAccount` toocreate uma ligação com o Azure.

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo


[!code-powershell[main](../../../powershell_scripts/virtual-network/virtual-network-multi-tier-application/virtual-network-multi-tier-application.ps1  "Virtual network for multi-tier application")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, rede virtual e os grupos de segurança de rede. Cada comando na documentação do Olá tabela ligações toocommand específicos.

| Comando | Notas |
|---|---|
| [Novo-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Novo-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) | Cria uma rede virtual do Azure e a sub-rede do front-end. |
| [Novo AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) | Cria uma sub-rede de back-end. |
| [Novo AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) | Cria um Olá de tooaccess de endereço IP público VM a partir de Olá Internet. |
| [Novo AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) | Cria interfaces de rede virtual e anexa-las a sub-redes da rede virtual toohello de front-end e back-end. |
| [Novo AzureRmNetworkSecurityGroup](/powershell/module/azurerm.network/new-azurermnetworksecuritygroup) | Cria grupos de segurança de rede (NSG) que são toohello associados a sub-redes de front-end e back-end. |
| [Novo AzureRmNetworkSecurityRuleConfig](/powershell/module/azurerm.network/new-azurermnetworksecurityruleconfig) |Cria regras do NSG que permitem ou bloquear sub-redes de toospecific portas específicas. |
| [Novo-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) | Cria máquinas virtuais e anexa um tooeach NIC VM. Este comando também especifica toouse de imagem de máquina virtual de Olá e credenciais administrativas. |
| [Remove-AzureRmResourceGroup](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | Elimina um grupo de recursos e todos os recursos que nele contidos. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá Azure PowerShell, consulte [documentação do Azure PowerShell](https://docs.microsoft.com/powershell/azure/overview).

Exemplos de script do PowerShell redes adicionais podem ser encontrados na Olá [documentação de descrição geral de funcionamento em rede do Azure](../powershell-samples.md?toc=%2fazure%2fnetworking%2ftoc.json).
