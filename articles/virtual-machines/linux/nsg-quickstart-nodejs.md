---
title: aaaOpen portas tooa VM com Linux com a CLI do Azure 1.0 | Microsoft Docs
description: "Saiba como tooopen uma porta / criar um ponto final tooyour VM com Linux utilizando a implementação de Gestor de recursos do Azure Olá modelar e Olá CLI do Azure 1.0"
services: virtual-machines-linux
documentationcenter: 
author: iainfoulds
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: 337c37d151f527b43d4852291159b2f70a00accc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="opening-ports-and-endpoints-tooa-linux-vm-in-azure-using-hello-azure-cli-10"></a>Abrir portas e os pontos finais tooa VM com Linux no Azure com Olá CLI do Azure 1.0
Abrir uma porta ou criar um ponto final, tooa máquina virtual (VM) no Azure através da criação de um filtro de rede numa sub-rede ou interface de rede VM. Colocar estes filtros que controlam o tráfego de entrada e saído, num grupo de segurança de rede ligado toohello recurso que recebe o tráfego de Olá. Vamos utilizar um exemplo comum de tráfego da web na porta 80. Este artigo mostra como tooopen uma porta tooa VM utilizando Olá CLI do Azure 1.0.


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá
Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

- [Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](nsg-quickstart.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá


## <a name="quick-commands"></a>Comandos rápidos
toocreate um grupo de segurança de rede e as regras terá [Olá CLI do Azure 1.0](../../cli-install-nodejs.md) instalado e o modo Resource Manager:

```azurecli
azure config mode arm
```

No Olá exemplos a seguir, substitua os nomes dos parâmetros de exemplo com os seus próprios valores. Os nomes de parâmetros de exemplo incluídos *myResourceGroup*, *myNetworkSecurityGroup*, e *myVnet*.

Crie o grupo de segurança de rede, introduzir os seus próprios nomes e a localização correta. Olá exemplo seguinte cria um grupo de segurança de rede com o nome *myNetworkSecurityGroup* no Olá *eastus* localização:

```azurecli
azure network nsg create \
    --resource-group myResourceGroup \
    --location eastus \
    --name myNetworkSecurityGroup
```

Adicionar uma regra tooallow HTTP tráfego tooyour webserver (ou ajustar o seus próprios cenário, tais como a conectividade de acesso ou a base de dados SSH). Olá exemplo seguinte cria uma regra com o nome *myNetworkSecurityGroupRule* tooallow TCP de tráfego na porta 80:

```azurecli
azure network nsg rule create \
    --resource-group myResourceGroup \
    --nsg-name myNetworkSecurityGroup \
    --name myNetworkSecurityGroupRule \
    --protocol tcp \
    --direction inbound \
    --priority 1000 \
    --destination-port-range 80 \
    --access allow
```

Olá associar grupo de segurança de rede com a interface de rede da VM (NIC). Olá exemplo seguinte associa uma NIC existente com o nome *myNic* com o grupo de segurança de rede com o nome de Olá *myNetworkSecurityGroup*:

```azurecli
azure network nic set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --name myNic
```

Em alternativa, pode associar o seu grupo de segurança de rede com uma sub-rede da rede virtual em vez de apenas interface de rede toohello numa única VM. Olá exemplo seguinte associa uma sub-rede existente com o nome *mySubnet* no Olá *myVnet* rede virtual com o grupo de segurança de rede com o nome de Olá *myNetworkSecurityGroup*:

```azurecli
azure network vnet subnet set \
    --resource-group myResourceGroup \
    --network-security-group-name myNetworkSecurityGroup \
    --vnet-name myVnet --name mySubnet
```

## <a name="more-information-on-network-security-groups"></a>Obter mais informações sobre grupos de segurança de rede
comandos rápidos Olá aqui permitem-lhe tooget cópias de segurança e em execução com tooyour de fluxo de tráfego VM. Grupos de segurança de rede fornecem várias funcionalidades excelentes e granularidade para controlar aceder a recursos tooyour. Pode ler mais sobre [criar um grupo de segurança de rede e a ACL regras aqui](../../virtual-network/virtual-networks-create-nsg-arm-cli.md).

Pode definir grupos de segurança de rede e as regras de ACL como parte dos modelos Azure Resource Manager. Leia mais sobre [criar grupos de segurança de rede com modelos](../../virtual-network/virtual-networks-create-nsg-arm-template.md).

Se precisar de toouse porta reencaminhamento toomap uma porta de interno tooan porta externa exclusivo na sua VM, utilize um balanceador de carga e regras de tradução de endereços de rede (NAT). Por exemplo, pode pretender tooexpose TCP porta 8080 externamente e ter tráfego direcionado tooTCP porta 80 numa VM. Pode saber mais sobre [criação de um balanceador de carga para a Internet](../../load-balancer/load-balancer-get-started-internet-arm-cli.md).

## <a name="next-steps"></a>Passos seguintes
Neste exemplo, criou um tráfego de tooallow HTTP regra simples. Pode encontrar informações sobre como criar ambientes mais detalhados no Olá seguintes artigos:

* [Descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)
* [O que é um Grupo de Segurança de Rede (NSG)? (What is a Network Security Group (NSG)?)](../../virtual-network/virtual-networks-nsg.md)
* [Descrição geral do Gestor de recursos do Azure para balanceadores de carga](../../load-balancer/load-balancer-arm.md)

