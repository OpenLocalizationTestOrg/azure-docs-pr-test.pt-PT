---
title: aaaDeploy VMs do Linux na rede existente com a CLI do Azure 1.0 | Microsoft Docs
description: "Como toodeploy uma VM com Linux para uma rede Virtual existente utilizando Olá CLI do Azure 1.0"
services: virtual-machines-linux
documentationcenter: virtual-machines
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/11/2017
ms.author: iainfou
ms.openlocfilehash: e660f1563d386efc7788bd236f8b067145ea09bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toodeploy-a-linux-virtual-machine-into-an-existing-azure-virtual-network-with-hello-azure-cli-10"></a>Como toodeploy uma máquina virtual do Linux para uma rede Virtual do Azure existente com Olá CLI do Azure 1.0

Este artigo mostra como toouse CLI do Azure 1.0 toodeploy uma máquina virtual (VM) numa rede Virtual existente (VNet). requisitos de Olá são:

- [uma conta do Azure](https://azure.microsoft.com/pricing/free-trial/)
- [Ficheiros de chaves públicas e privadas SSH](mac-create-ssh-keys.md)


## <a name="cli-versions-toocomplete-hello-task"></a>Tarefas do CLI versões toocomplete Olá
Pode concluir tarefas Olá utilizando uma das seguintes versões do CLI de Olá:

- [Azure CLI 1.0](#quick-commands) – nosso CLI para Olá clássica e resource Gestão modelos de implementação (Este artigo)
- [Azure CLI 2.0](deploy-linux-vm-into-existing-vnet-using-cli.md) -nossa próxima geração CLI do modelo de implementação da gestão de recursos de Olá


## <a name="quick-commands"></a>Comandos Rápidos

Se precisar de tooquickly realizar tarefas Olá, Olá seguinte secção fornece detalhes sobre os comandos de Olá necessários. Mais informações e o contexto de cada passo pode ser encontrado rest Olá documento Olá, [Iniciar aqui](deploy-linux-vm-into-existing-vnet-using-cli.md#detailed-walkthrough).

Pré-requisitos: Grupo de recursos, VNet, NSG com SSH de entrada, sub-rede. Substitua qualquer exemplos as suas próprias definições.

### <a name="deploy-hello-vm-into-hello-virtual-network-infrastructure"></a>Implementar Olá VM numa infraestrutura de rede virtual Olá

```azurecli
azure vm create myVM \
    -g myResourceGroup \
    -l eastus \
    -y linux \
    -Q Debian \
    -o mystorageaccount \
    -u myAdminUser \
    -M ~/.ssh/id_rsa.pub \
    -n myVM \
    -F myVNet \
    -j mySubnet \
    -N myVNic
```

## <a name="detailed-walkthrough"></a>Instruções detalhadas

Recursos do Azure como Olá VNets e grupos de segurança de rede devem ser estáticos e tempo lived recursos que raramente são implementados. Assim que tiver sido implementada uma VNet, pode ser reutilizada por novas implementações sem qualquer infraestrutura de toohello afeta adversos. Pensa sobre uma VNet como sendo um comutador de rede de hardware tradicional. Não terá tooconfigure um novo hardware mudar com cada implementação. Com uma VNet configurada corretamente, pode prosseguir toodeploy novos servidores para essa VNet mais e mais alguns, se existirem, as alterações necessárias ao longo da vida Olá de Olá VNet.

## <a name="create-hello-resource-group"></a>Criar grupo de recursos de Olá

Em primeiro lugar, crie um tooorganize do grupo de recursos tudo que criar esta explicação passo a passo. Para obter mais informações sobre grupos de recursos, consulte [descrição geral do Azure Resource Manager](../../azure-resource-manager/resource-group-overview.md)

```azurecli
azure group create myResourceGroup --location eastus
```

## <a name="create-hello-vnet"></a>Criar Olá VNet

Step-by-Olá primeiro passo é toobuild toolaunch uma VNet Olá VMs no. Olá VNet contém uma sub-rede para esta instrução. Para obter mais informações sobre as VNets do Azure, consulte [criar uma rede virtual, utilizando Olá CLI do Azure](../../virtual-network/virtual-networks-create-vnet-arm-cli.md)

```azurecli
azure network vnet create myVNet \
    --resource-group myResourceGroup \
    --address-prefixes 10.10.0.0/24 \
    --location eastus
```

## <a name="create-hello-network-security-group"></a>Criar grupo de segurança de rede Olá

a sub-rede de Olá baseia-se por trás de um grupo de segurança de rede existente para criar o grupo de segurança de rede Olá antes de sub-rede Olá. Grupos de segurança de rede do Azure são equivalentes tooa firewall na camada de rede Olá. Para obter mais informações sobre grupos de segurança de rede do Azure, consulte [como de grupos de segurança de rede toocreate Olá CLI do Azure](../../virtual-network/virtual-networks-create-nsg-arm-cli.md)

```azurecli
azure network nsg create myNetworkSecurityGroup \
    --resource-group myResourceGroup \
    --location eastus
```

## <a name="add-an-inbound-ssh-allow-rule"></a>Adicionar regra de permissão de um SSH de entrada

Olá VM tem acesso a partir de Olá internet, para que uma regra que permite a porta de entrada 22 tráfego toobe transmitido através da rede de Olá tooport 22 Olá VM é necessária.

```azurecli
azure network nsg rule create inboundSSH \
    --resource-group myResourceGroup \
    --nsg-name myNSG \
    --access Allow \
    --protocol Tcp \
    --direction Inbound \
    --priority 100 \
    --source-address-prefix Internet \
    --source-port-range 22 \
    --destination-address-prefix 10.10.0.0/24 \
    --destination-port-range 22
```

## <a name="add-a-subnet-toohello-vnet"></a>Adicionar uma sub-rede toohello VNet

VMs dentro Olá VNet tem de estar localizadas numa sub-rede. Cada VNet pode ter várias sub-redes. Criar a sub-rede de Olá e associar grupo de segurança de rede Olá.

```azurecli
azure network vnet subnet create mySubNet \
    --resource-group myResourceGroup \
    --vnet-name myVNet \
    --address-prefix 10.10.0.0/26 \
    --network-security-group-name myNetworkSecurityGroup
```

Olá sub-rede agora é adicionado no interior Olá VNet e associada ao grupo de segurança de rede Olá e regra.


## <a name="add-a-vnic-toohello-subnet"></a>Adicionar uma sub-rede de toohello VNic

Placas de rede virtuais (VNics) são importantes, como pode reutilize-as ao ligá-las toodifferent VMs. Esta abordagem mantém Olá VNic como um recurso estático enquanto Olá VMs pode ser temporário. Criar um VNic e associá-la a sub-rede de Olá criada no passo anterior Olá.

```azurecli
azure network nic create myVNic \
    --resource-group myResourceGroup \
    --location eastus \
    ---subnet-vnet-name myVNet \
    --subnet-name mySubNet
```

## <a name="deploy-hello-vm-into-hello-vnet-and-nsg"></a>Implementar Olá VM em Olá VNet e o NSG

Tem agora uma VNet e sub-rede dentro desse VNet e um grupo de segurança de rede que atuam sub-rede de Olá tooprotect ao bloquear todo o tráfego de entrada, exceto a porta 22 para SSH. Agora pode ser implementado Olá VM dentro esta infraestrutura de rede existente.

Utilizar Olá CLI do Azure e Olá `azure vm create` comando, Olá VM com Linux é implementado toohello existente grupo de recursos do Azure, uma VNet, sub-rede e VNic. Para obter mais informações sobre como utilizar Olá CLI toodeploy uma VM completa, consulte [criar um ambiente de Linux completado utilizando Olá CLI do Azure](create-cli-complete.md)

```azurecli
azure vm create myVM \
    --resource-group myResourceGroup \
    --location eastus \
    --os-type linux \
    --image-urn Debian \
    --storage-account-name mystorageaccount \
    --admin-username myAdminUser \
    --ssh-publickey-file ~/.ssh/id_rsa.pub \
    --vnet-name myVNet \
    --vnet-subnet-name mySubnet \
    --nic-name myVNic
```

Ao utilizar Olá CLI sinalizadores toocall horizontalmente recursos existentes, instruir VM do Azure toodeploy Olá dentro da rede existente Olá. Depois de tem sido implementados uma VNet e sub-rede, pode ser deixados como estáticos ou permanentes recursos dentro da região do Azure.  

## <a name="next-steps"></a>Passos seguintes

* [Utilize um toocreate de modelo do Azure Resource Manager uma implementação específica](../windows/cli-deploy-templates.md)
* [Criar um ambiente personalizado para uma VM com Linux diretamente através dos comandos da CLI do Azure](create-cli-complete.md)
* [Criar uma VM com Linux no Azure utilizando modelos](create-ssh-secured-vm-from-template.md)
