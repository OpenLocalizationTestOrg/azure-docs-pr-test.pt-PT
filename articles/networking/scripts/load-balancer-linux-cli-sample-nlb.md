---
title: "aaaAzure CLI Script de exemplo - tooVMs de tráfego de balanceamento de carga para elevada disponibilidade | Microsoft Docs"
description: "Exemplo de Script CLI do Azure - tooVMs de tráfego de balanceamento de carga para elevada disponibilidade"
services: load-balancer
documentationcenter: load-balancer
author: KumudD
manager: timlt
editor: tysonn
tags: 
ms.assetid: 
ms.service: load-balancer
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: 
ms.workload: infrastructure
ms.date: 07/07/2017
ms.author: kumud
ms.openlocfilehash: 0954b5c261512724dfb9c6e7be123c9d45624f4d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="load-balance-traffic-toovms-for-high-availability"></a>Carregar saldo tráfego tooVMs para elevada disponibilidade

Este script de exemplo cria tudo necessário toorun várias máquinas virtuais Ubuntu configurado numa elevada disponibilidade e carga com balanceamento de configuração. Depois de executar o script Olá, terá três máquinas virtuais, tooan associados a um conjunto de disponibilidade do Azure e é acessível através de um balanceador de carga do Azure. 

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Script de exemplo

[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine/create-vm-nlb/create-vm-nlb.sh "Quick Create VM")]

## <a name="clean-up-deployment"></a>Limpar a implementação 

Execute Olá grupo de recursos do comando tooremove Olá, VM e relacionados todos os recursos a seguir.

```azurecli
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Explicação de script

Este script utiliza Olá os seguintes comandos toocreate um grupo de recursos, máquina virtual, conjunto de disponibilidade, o Balanceador de carga e todos os recursos relacionados. Cada comando na tabela de Olá contém ligações a documentação específica toocommand.

| Comando | Notas |
|---|---|
| [Criar grupo AZ](https://docs.microsoft.com/cli/azure/group#create) | Cria um grupo de recursos na qual todos os recursos são armazenados. |
| [Criar AZ rede vnet](https://docs.microsoft.com/cli/azure/network/vnet#create) | Cria uma rede virtual do Azure e a sub-rede. |
| [Criar AZ público-ip da rede](https://docs.microsoft.com/cli/azure/network/public-ip#create) | Cria um endereço IP público com um endereço IP estático e um nome DNS associado. |
| [Criar AZ lb de rede](https://docs.microsoft.com/cli/azure/network/lb#create) | Cria um balanceador de carga do Azure. |
| [criar a sonda de lb AZ rede](https://docs.microsoft.com/cli/azure/network/lb/probe#create) | Cria uma sonda do Balanceador de carga. Uma sonda do Balanceador de carga é utilizado toomonitor cada VM no conjunto de Balanceador de carga Olá. Se qualquer VM torna-se inacessível, o tráfego não é encaminhado toohello VM. |
| [Criar regra de lb AZ de rede](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria uma regra de Balanceador de carga. Neste exemplo, é criada uma regra para a porta 80. Como o tráfego HTTP chega ao balanceador de carga Olá, é encaminhado tooport 80 uma das VMs Olá no conjunto de Olá LB. |
| [Criar AZ rede lb-nat-regras de entrada](https://docs.microsoft.com/cli/azure/network/lb/inbound-nat-rule#create) | Cria a regra de tradução de endereços de rede (NAT) do Balanceador de carga.  As regras NAT de mapeiam uma porta da porta tooa de Balanceador de carga do Olá numa VM. Neste exemplo, é criada uma regra NAT para SSH tráfego tooeach VM no conjunto de Balanceador de carga Olá.  |
| [Criar AZ rede nsg](https://docs.microsoft.com/cli/azure/network/nsg#create) | Cria um grupo de segurança de rede (NSG), que é um limite de segurança entre Olá internet e Olá das máquinas virtuais. |
| [criar regras de nsg AZ rede](https://docs.microsoft.com/cli/azure/network/nsg/rule#create) | Cria um tooallow de regras do NSG tráfego de entrada. Neste exemplo, a porta 22 é aberta para tráfego SSH. |
| [Criar AZ nic da rede](https://docs.microsoft.com/cli/azure/network/nic#create) | Cria uma placa de rede virtual e anexa-toohello de rede virtual, uma sub-rede e NSG. |
| [criar a vm AZ conjunto de disponibilidade](https://docs.microsoft.com/cli/azure/network/lb/rule#create) | Cria um conjunto de disponibilidade. Conjuntos de disponibilidade garantir a disponibilidade de aplicações, propagando-se máquinas de virtuais Olá em recursos físicos, de modo a que o se ocorrer uma falha, o conjunto completo de Olá não é afetado. |
| [Criar AZ vm](/cli/azure/vm#create) | Cria a máquina virtual de Olá e liga toohello placa de rede, uma rede virtual, sub-rede e NSG. Este comando também especifica toobe de imagem de máquina virtual de Olá utilizado e credenciais administrativas.  |
| [eliminação do grupo de AZ](https://docs.microsoft.com/cli/azure/vm/extension#set) | Elimina um grupo de recursos, incluindo todos os recursos aninhados. |

## <a name="next-steps"></a>Passos seguintes

Para obter mais informações sobre Olá CLI do Azure, consulte [documentação da CLI do Azure](https://docs.microsoft.com/cli/azure/overview).

Exemplos de script a CLI de redes do Azure adicionais podem ser encontrados na Olá [redes do Azure documentação](../cli-samples.md).
