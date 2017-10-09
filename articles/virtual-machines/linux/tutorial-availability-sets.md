---
title: aaaAvailability define tutorial para VMs com Linux no Azure | Microsoft Docs
description: "Saiba mais sobre Olá conjuntos de disponibilidade para VMs com Linux no Azure."
documentationcenter: 
services: virtual-machines-linux
author: cynthn
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machines-linux
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 05/22/2017
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: 2a91e4a6057180035ec51410d9fffccaca343758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-PT
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-availability-sets"></a>Como disponibilidade toouse define


Neste tutorial, ficará a saber como disponibilidade de Olá tooincrease e a fiabilidade das suas soluções de Máquina Virtual no Azure através de uma capacidade chamado conjuntos de disponibilidade. Conjuntos de disponibilidade Certifique-se de que Olá VMs implementar no Azure estão distribuídas em vários clusters hardware isolado. Fazer isto garante que se ocorre uma falha de hardware ou software no Azure, apenas um conjunto secundárias das suas VMs será afetado e que a solução global permanecerá disponível e operacional da perspetiva de Olá dos seus clientes utilizá-la.

Neste tutorial, ficará a saber como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM num conjunto de disponibilidade
> * Verifique os tamanhos VM disponíveis


[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

Se escolher tooinstall e utilizar Olá CLI localmente, este tutorial, necessita que está a executar versão CLI do Azure de Olá 2.0.4 ou posterior. Executar `az --version` versão de Olá toofind. Se precisar de tooinstall ou atualização, consulte [instalar o Azure CLI 2.0]( /cli/azure/install-azure-cli). 

## <a name="availability-set-overview"></a>Descrição geral do conjunto de disponibilidade

Um conjunto de disponibilidade é uma capacidade de agrupamento lógico que pode utilizar no Azure tooensure que estão isolados umas das outras Olá VM recursos que colocar dentro do mesmo quando estão implementadas dentro de um datacenter do Azure. Azure garante que Olá VMs colocar dentro de um conjunto de disponibilidade sejam executadas em vários servidores físicos, computação bastidores, unidades de armazenamento e comutadores de rede. Isto garante que no evento Olá de um hardware ou a falha de software do Azure, apenas um subconjunto das suas VMs será afetado, e global da sua aplicação irá manter cópias de segurança e continuar toobe tooyour disponíveis clientes. Utilizar conjuntos de disponibilidade é um tooleverage capacidade essencial quando quiser toobuild soluções de nuvem fiável.

Vejamos uma típica VM solução baseada em que poderá ter 4 servidores de web de front-end e utilize 2 VMs de back-end que aloja uma base de dados. Com o Azure, seria aconselhável toodefine dois conjuntos de disponibilidade antes de implementar as suas VMs: conjunto de disponibilidade de uma camada de "web" Olá e um conjunto de disponibilidade para camada de "base de dados" Olá. Quando cria uma nova VM, em seguida, pode especificar disponibilidade Olá definida como comando de criar uma vm do parâmetro toohello az e Azure será automaticamente Certifique-se de que Olá VMs que cria no Olá disponível conjunto são isoladas entre vários recursos de hardware físico. Isto significa que se o hardware físico Olá que o servidor Web ou VMs do servidor de base de dados está em execução no tem um problema, sabe que Olá outras instâncias do servidor Web e da base de dados VMs continuará em execução ajustar porque estão num hardware diferente.

Deve sempre utilizar conjuntos de disponibilidade quando quiser toodeploy fiável VM soluções baseadas no Azure.


## <a name="create-an-availability-set"></a>Criar um conjunto de disponibilidade

Pode criar um conjunto através de disponibilidade [az vm conjunto de disponibilidade criar](/cli/azure/vm/availability-set#create). Neste exemplo, vamos definir ambos os número de Olá de domínios de atualização e de falhas em *2* para o conjunto nomeada de disponibilidade de Olá *myAvailabilitySet* no Olá *myResourceGroupAvailability*grupo de recursos.

Crie um grupo de recursos.

```azurecli-interactive 
az group create --name myResourceGroupAvailability --location eastus
```


```azurecli-interactive 
az vm availability-set create \
    --resource-group myResourceGroupAvailability \
    --name myAvailabilitySet \
    --platform-fault-domain-count 2 \
    --platform-update-domain-count 2
```

Conjuntos de disponibilidade permitem-lhe tooisolate recursos em "domínios de falhas" e "domínios de atualização". A **domínio de falhas** representa uma coleção isolada do servidor + rede + armazenamento recursos. Nos Olá anterior exemplo, vamos indicar que queremos que nosso disponibilidade definido toobe distribuído, pelo menos, dois domínios de falhas quando os nossas VMs são implementadas. Também iremos indicar que queremos nosso conjunto distribuída em dois de disponibilidade **domínios de atualização**.  Dois domínios de atualização Certifique-se de que quando o Azure executa as atualizações de software nosso recursos VM isolados, impedir de todo o software Olá executando por baixo do nosso VM a partir de que está a ser atualizada no Olá mesmo tempo.

## <a name="configure-virtual-network"></a>Configurar uma rede virtual
Antes de implementar algumas VMs e pode testar o seu balanceador, crie Olá suporte recursos de rede virtual. Para obter mais informações sobre as redes virtuais, consulte Olá [gerir redes virtuais do Azure](tutorial-virtual-network.md) tutorial.

### <a name="create-network-resources"></a>Criar recursos de rede
Criar uma rede virtual com [az rede vnet criar](/cli/azure/network/vnet#create). Olá exemplo seguinte cria uma rede virtual denominada *myVnet* com uma sub-rede denominada *mySubnet*:

```azurecli-interactive 
az network vnet create \
    --resource-group myResourceGroupAvailability \
    --name myVnet \
    --subnet-name mySubnet
```
NICs virtuais são criados com [nic da rede az criar](/cli/azure/network/nic#create). Olá exemplo seguinte cria três NICs virtuais. (Uma NIC virtual para cada VM criar para a aplicação no Olá seguindo os passos). Pode criar o NICs virtuais adicionais e VMs em qualquer altura e adicioná-los toohello Balanceador de carga:

```bash
for i in `seq 1 3`; do
    az network nic create \
        --resource-group myResourceGroupAvailability \
        --name myNic$i \
        --vnet-name myVnet \
        --subnet mySubnet \
        --lb-name myLoadBalancer \
        --lb-address-pools myBackEndPool
done
```

## <a name="create-vms-inside-an-availability-set"></a>Criar VMs dentro de um conjunto de disponibilidade

As VMs têm de ser criadas no toomake de conjunto de disponibilidade de Olá se que corretamente estão distribuídos hardware Olá. Não é possível adicionar um existente VM tooan conjunto de disponibilidade depois de criado. 

Quando cria uma VM utilizando [az vm criar](/cli/azure/vm#create) especificar disponibilidade Olá definida utilizando Olá `--availability-set` toospecify Olá o nome do parâmetro de conjunto de disponibilidade de Olá.

```azurecli-interactive 
for i in `seq 1 2`; do
   az vm create \
     --resource-group myResourceGroupAvailability \
     --name myVM$i \
     --availability-set myAvailabilitySet \
     --nics myNic$i \
     --size Standard_DS1_v2  \
     --image Canonical:UbuntuServer:14.04.4-LTS:latest \
     --admin-username azureuser \
     --generate-ssh-keys \
     --no-wait
done 
```

Iremos agora, tem duas máquinas virtuais no nosso conjunto de disponibilidade criado recentemente. Porque estão em Olá mesmo conjunto de disponibilidade, o Azure irá garantir que VMs Olá e todos os respetivos recursos (incluindo os discos de dados) estão distribuídos isolado hardware físico. Esta distribuição ajuda Certifique-se muito maior disponibilidade da nossa solução global de VM.

Um aspeto que poderá encontrar à medida que adiciona VMs é que um determinado tamanho da VM já não está disponível toouse dentro do conjunto de disponibilidade. Este problema pode ocorrer se já não é suficiente tooadd de capacidade, mantendo o conjunto de disponibilidade do Olá isolamento regras Olá impõe. Pode verificar toosee os tamanhos VM são toouse disponível dentro de um conjunto utilizando Olá de disponibilidade existente `--availability-set list-sizes` parâmetro.

## <a name="check-for-available-vm-sizes"></a>Verifique a existência de tamanhos VM disponíveis 

Pode adicionar mais VMs toohello conjunto de disponibilidade mais tarde, mas tem tooknow tamanhos de VM que estão disponíveis no hardware de Olá. Utilize [lista-tamanhos do conjunto de disponibilidade de vm az](/cli/azure/availability-set#list-sizes) toolist todos os tamanhos disponíveis Olá no hardware de Olá cluster Olá para conjunto de disponibilidade.

```azurecli-interactive 
az vm availability-set list-sizes \
     --resource-group myResourceGroupAvailability \
     --name myAvailabilitySet \
     --output table  
```

## <a name="next-steps"></a>Passos seguintes

Neste tutorial, ficou a saber como:

> [!div class="checklist"]
> * Criar um conjunto de disponibilidade
> * Criar uma VM num conjunto de disponibilidade
> * Verifique os tamanhos VM disponíveis

Produzir toohello seguinte toolearn tutorial sobre conjuntos de dimensionamento de máquina virtual.

> [!div class="nextstepaction"]
> [Criar um conjunto de dimensionamento de VM](tutorial-create-vmss.md)

