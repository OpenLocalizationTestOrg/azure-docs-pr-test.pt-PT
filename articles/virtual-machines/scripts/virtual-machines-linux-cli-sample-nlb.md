---
title: aaaAzure CLI Script de exemplo - criar uma VM com Linux com NLB | Microsoft Docs
description: CLI do Azure Script de exemplo - criar uma VM com Linux com NLB
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
ms.openlocfilehash: 79b245c1268734fead313b34c120f74ab2330d4b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-highly-available-vm"></a>Criar uma VM de elevada disponibilidade

Este script de exemplo cria tudo necessário toorun várias máquinas virtuais Ubuntu configurado numa elevada disponibilidade e carga com balanceamento de configuração. Depois de executar o script Olá, terá três máquinas virtuais, tooan associados a um conjunto de disponibilidade do Azure e é acessível através de um balanceador de carga do Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli-interactive 
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ rede vnet](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma rede virtual do Azure e a sub-rede. |
| [Criar AZ público-ip da rede](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [Criar AZ lb de rede](https://docs.microsoft.com/cli/azure/network/lb#create) | Cria um balanceador de carga de rede do Azure (NLB). |
| [criar a sonda de lb AZ rede](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Cria uma pesquisa NLB. Uma pesquisa NLB está toomonitor utilizado cada VM de conjunto NLB Olá. Se qualquer VM torna-se inacessível, o tráfego não é encaminhado toohello VM. |
| [Criar regra de lb AZ de rede](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria uma regra NLB. Neste exemplo, é criada uma regra para a porta 80. Como o tráfego HTTP chega Olá NLB, é encaminhado tooport 80 uma das VMs Olá no conjunto NLB Olá. |
| [Criar AZ rede lb-nat-regras de entrada](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Cria uma regra de tradução de endereços de rede (NAT) do NLB.  As regras NAT de mapeiam uma porta de Olá porta tooa NLB numa VM. Neste exemplo, é criada uma regra NAT para SSH tráfego tooeach VM num conjunto NLB Olá.  |
| [Criar AZ rede nsg](https://docs.microsoft.com/cli/azure/network/nsg#create) | Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre Olá internet e Olá das máquinas virtuais. |
| [criar regras de nsg AZ rede](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Cria um tooallow de regras do NSG tráfego de entrada. Neste exemplo, a porta 22 é aberta para tráfego SSH. |
| [Criar AZ nic da rede](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e anexa-toohello de rede virtual, uma sub-rede e NSG. |
| [criar a vm AZ conjunto de disponibilidade](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantir a disponibilidade de aplicações, propagando-se máquinas de virtuais Olá em recursos físicos, de modo a que o se ocorrer uma falha, o conjunto completo de Olá não é afetado. |
| [Criar AZ vm](https://docs.microsoft.com/cli/azure/vm/availability-set#create) | Cria a máquina virtual de Olá e liga toohello placa de rede, uma rede virtual, sub-rede e NSG. Este comando também especifica toobe de imagem de máquina virtual de Olá utilizado e credenciais administrativas.  |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script do CLI de máquina virtual adicional que podem ser encontrados no Olá [documentação de VM do Linux do Azure](../linux/cli-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).
