---
title: aaaAzure CLI Script de exemplo - criar duas VMs com um NSG interno e externo | Microsoft Docs
description: Script CLI do Azure de exemplo - criar duas VMs com NSG interno e externo
services: virtual-machines-linux
documentationcenter: virtual-machines
author: neilpeterson
manager: timlt
editor: tysonn
tags: azure-service-management
ms.assetid: 
ms.service: virtual-machines-linux
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 02/27/2017
ms.author: nepeters
ms.custom: mvc
ms.openlocfilehash: ba6a70200ca2923369e37b13531bd7ca65b05a1f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="secure-network-traffic-between-virtual-machines"></a>Proteger o tráfego de rede entre as máquinas virtuais

Este script cria duas máquinas virtuais e protege receber tráfego tooboth. Olá uma máquina virtual está acessível na internet e um grupo de segurança de rede (NSG) configurou tooallow tráfego na porta 22 e a porta 80. não está acessível na segunda de máquina virtual Olá Olá internet e tem um NSG configurado tooonly permitir o tráfego da máquina de virtual primeiro Olá. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nsg/create-vm-nsg.sh "Create VM with NSG")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, a máquina virtual, e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ rede vnet](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma rede virtual do Azure e a sub-rede. |
| [criar a sub-rede da vnet AZ rede](https://docs.microsoft.com/cli/azure/network/vnet/subnet#create) | Cria uma sub-rede. |
| [Criar AZ vm](https://docs.microsoft.com/cli/azure/vm#create) | Cria a máquina virtual de Olá e liga toohello placa de rede, uma rede virtual, sub-rede e NSG. Este comando também especifica toobe de imagem de máquina virtual de Olá utilizado e credenciais administrativas.  |
| [lista de regras de nsg de rede AZ](https://docs.microsoft.com/cli/azure/network/nsg/rule#list) | Devolve informações sobre uma regra de grupo de segurança de rede. Neste exemplo, o nome da regra Olá é armazenado numa variável para utilização posterior num script Olá. |
| [actualização da regra AZ rede nsg](https://docs.microsoft.com/cli/azure/network/nsg/rule#update) | Atualiza uma regra NSG. Neste exemplo, a regra de back-end de Olá é toopass atualizado através de tráfego apenas a partir da sub-rede Olá de front-end. |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
